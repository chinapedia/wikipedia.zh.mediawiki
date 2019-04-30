----------------------------------------------------------------------
--                          Module:Rfx                              --
-- This is a library for retrieving information about requests      --
-- for adminship and requests for bureaucratship on the English     --
-- Wikipedia. Please see the module documentation for instructions. --
----------------------------------------------------------------------

local libraryUtil = require('libraryUtil')
local lang = mw.getContentLanguage()
local textSplit = mw.text.split
local umatch = mw.ustring.match
local newTitle = mw.title.new
local validSignPrefixes = {
	['u']=1, ['user']=1, ['用户']=1, ['用戶']=1,
	['ut']=1, ['user talk']=1, ['用户讨论']=1, ['用戶討論']=1,
	['special:contribs']=1, ['特殊:contribs']=1,
	['special:contributions']=1, ['特殊:contributions']=1,
	['特殊:用户贡献']=1, ['特殊:用戶貢獻']=1,
	['special:用户贡献']=1, ['special:用戶貢獻']=1
}
local rfx = {}
local corrections = require('Module:Rfx/correction')

--------------------------------------
--         Helper functions         --
--------------------------------------

local function getTitleObject(title)
	local success, titleObject = pcall(newTitle, title)
	if success and titleObject then
		return titleObject
	else
		return nil
	end
end

local function parseVoteBoundaries(section)
	-- Returns an array containing the raw wikitext of RfX votes in a given section.
	section = section:match('^.-\n#(.*)$') -- Strip non-votes from the start.
	if not section then
		return {}
	end
	-- WhitePhosphorus: Do not discard anything, or we may lose votes.
	--- See [[special:permalink/45633636|special:permalink/45633636]].
	-- section = section:match('^(.-)\n[^#]') or section -- Discard subsequent numbered lists.
	local comments = textSplit(section, '\n#')
	local votes = {}
	for i, comment in ipairs(comments) do
		if comment:find('^[^#*;:].*%S') then
			votes[#votes + 1] = comment
		end
	end
	return votes
end

local function parseVote(vote)
	-- parses a username from an RfX vote.
	local b, e, link, username, page, colon, slash, prefix = nil, 0
	while true do
		-- extract all links
		b, e, link = vote:find('%[%[[_%s]*:?[_%s]*(.-)[_%s]*%]%]', e+1)
		if not link then
			break
		end
		-- some strange links like User__  ___talk:_ __ Example is also valid.
		link = link:gsub('|.*', ''):gsub('[%s_]+', ' '):gsub('([:/]) ', '%1')
		colon, slash = link:find('/'), link:find(':')
		if colon then
			prefix = link:sub(1, colon-1):lower()
			if validSignPrefixes[prefix] then
				username = link:sub(colon+1)
			end
		end
		if slash then
			prefix = link:sub(1, slash-1):lower()
			if validSignPrefixes[prefix] then
				username = link:sub(slash+1)
			end
		end
	end
	if not username then
		return string.format( "'''签名-{zh-cn:解析;zh-tw:剖析}-失败'''：''%s''", vote )
	end
	return username:match('^[^/#]*')
end

local function parseVoters(votes)
	local voters = {}
	for i, vote in ipairs(votes) do
		voters[#voters + 1] = parseVote(vote)
	end
	return voters
end

local function dupesExist(...)
	local exists = {}
	local tables = {...}
	local dupes = {}
	for i, usernames in ipairs(tables) do
		for j, username in ipairs(usernames) do
			username = lang:ucfirst(username)
			if exists[username] then
				dupes[username] = true
			else
				exists[username] = true
			end
		end
	end
	local result = {}
	for username, _ in pairs(dupes) do
		table.insert(result, username)
	end
	return result
end

------------------------------------------
--   Define the constructor function    --
------------------------------------------

function rfx.new(title)
	local obj = {}
	local data = {}
	local checkSelf = libraryUtil.makeCheckSelfFunction( 'Module:Rfx', 'rfx', obj, 'rfx object' )
	
	-- Get the title object and check to see whether we are a subpage of WP:RFA or WP:RFB.
	title = getTitleObject(title)
	if not title then
		return nil
	end
	
	function data:getTitleObject()
		checkSelf(self, 'getTitleObject')
		return title
	end
	
	if title.namespace == 4 then
		local rootText = title.rootText
		if rootText == '申请成为管理员' then
			data.type = 'rfa'
		elseif rootText == '申请成为行政员' then
			data.type = 'rfb'
		elseif rootText == '申请成为用户查核员' then
			data.type = 'rfcu'
		elseif rootText == '申请成为监督员' then
			data.type = 'rfo'
		else
			return nil
		end
		
		local n = umatch(title.subpageText, '^第(%d+)次$')
		if n ~= nil then
			data.attempt = n
		else
			data.attempt = '1'
		end
	else
		return nil
	end

	-- Get the page content and divide it into sections.
	local pageText = title:getContent()
	if not pageText then
		return nil
	end
	frame = mw.getCurrentFrame()
	pageText = string.gsub(pageText, "{{%s*[Ff]ollow[Ll]ast[Ii]ndent|(.*)%s*}}",
		function (s)
			return frame:expandTemplate{ title = 'FollowLastIndent', args = { s } }
		end
	)
	
	-- FIXME: 反对？
	--- 其实这个不太重要，毕竟大家都用RfA模版，后者生成出来是繁体的。
	local introText, supportText, opposeText, neutralText = umatch(
		pageText,
		'^(.-)\n=====%s*支持%s*=====(.-)'
		.. '\n=====%s*反對%s*=====(.-)'
		.. '\n=====%s*中立%s*=====(.-)'
		.. '\n=====%s*意見%s*=====.*'
	)
	if not introText then
		introText, supportText, opposeText, neutralText = umatch(
			pageText,
			"^(.-\n'''[^\n]-''')\n.-"
			.. "\n'''支持'''(.-)\n'''反對'''(.-)\n'''中立'''(.-)'''意見'''.*"
		)
	end

	-- Get vote counts.
	local supportVotes, opposeVotes, neutralVotes
	if supportText and opposeText and neutralText then
		supportVotes = parseVoteBoundaries(supportText)
		opposeVotes = parseVoteBoundaries(opposeText)
		neutralVotes = parseVoteBoundaries(neutralText)
	end
	local correction = corrections[title.text] or {0, 0, 0}
	local supports, opposes, neutrals
	if supportVotes and opposeVotes and neutralVotes then
		supports = #supportVotes + correction[1]
		data.supports = math.max(supports, 0)
		opposes = #opposeVotes + correction[2]
		data.opposes = math.max(opposes, 0)
		neutrals = #neutralVotes + correction[3]
		data.neutrals = math.max(neutrals, 0)
	end

	-- Voter methods and dupe check.

	function data:getSupportUsers()
		checkSelf(self, 'getSupportUsers')
		if supportVotes then
			return parseVoters(supportVotes)
		else
			return nil
		end
	end

	function data:getOpposeUsers()
		checkSelf(self, 'getOpposeUsers')
		if opposeVotes then
			return parseVoters(opposeVotes)
		else
			return nil
		end
	end

	function data:getNeutralUsers()
		checkSelf(self, 'getNeutralUsers')
		if neutralVotes then
			return parseVoters(neutralVotes)
		else
			return nil
		end
	end

	function data:dupesExist()
		checkSelf(self, 'dupesExist')
		local supportUsers = self:getSupportUsers()
		local opposeUsers = self:getOpposeUsers()
		local neutralUsers = self:getNeutralUsers()
		if not (supportUsers and opposeUsers and neutralUsers) then
			return nil
		end
		return dupesExist(supportUsers, opposeUsers, neutralUsers)
	end

	if supports and opposes then
		local total = supports + opposes
		if total <= 0 then
			data.percent = 0
		else
			data.percent = math.floor((supports / total * 100) + 0.5)
		end
	end
	if introText then
		data.rawEndTime = umatch(introText, '%d+年%d+月%d+日%s*%([日一二三四五六]%)%s*%d+:%d+ %(UTC%)')
		if data.rawEndTime then
			local Y, n, j, m, s = umatch(data.rawEndTime, '(%d+)年(%d+)月(%d+)日%s*%([日一二三四五六]%)%s*(%d+):(%d+) %(UTC%)')
			data.endTime = string.format('%04d-%02d-%02dT%02d:%02dZ', Y, n, j, m, s)
		end
		-- === [[User:Example|Nickname]] ===
		data.user = umatch(introText, '===%s*%[%[[_%s]*[uU]ser[_%s]*:[_%s]*([^\n]-)|[^\n]-%]%]%s*===') or
		-- === [[U:Example|Nickname]] ===
		umatch(introText, '===%s*%[%[[_%s]*[uU][_%s]*:[_%s]*([^\n]-)|[^\n]-%]%]%s*===') or
		-- === [[用户:Example|Nickname]] ===
		umatch(introText, '===%s*%[%[[_%s]*用户[_%s]*:[_%s]*([^\n]-)|[^\n]-%]%]%s*===') or
		-- === [[用戶:Example|Nickname]] ===
		umatch(introText, '===%s*%[%[[_%s]*用戶[_%s]*:[_%s]*([^\n]-)|[^\n]-%]%]%s*===') or
		-- === [[User:Example|User:Example]] ===
		umatch(introText, '===%s*%[%[[_%s]*[uU]ser[_%s]*:[_%s]*([^\n]-)%]%]%s*===') or
		-- === [[U:Example|U:Example]] ===
		umatch(introText, '===%s*%[%[[_%s]*[uU][_%s]*:[_%s]*([^\n]-)%]%]%s*===') or
		-- === [[用户:Example|用户:Example]] ===
		umatch(introText, '===%s*%[%[[_%s]*用户[_%s]*:[_%s]*([^\n]-)%]%]%s*===') or
		-- === [[用戶:Example|用戶:Example]] ===
		umatch(introText, '===%s*%[%[[_%s]*用戶[_%s]*:[_%s]*([^\n]-)%]%]%s*===') or
		-- === User:Example ===
		umatch(introText, '===%s*[uU]ser[_%s]*:[_%s]*([^\n]-)%s*===') or
		-- === U:Example ===
		umatch(introText, '===%s*[uU][_%s]*:[_%s]*([^\n]-)%s*===') or
		-- === 用户:Example ===
		umatch(introText, '===%s*用户[_%s]*:[_%s]*([^\n]-)%s*===') or
		-- === 用戶:Example ===
		umatch(introText, '===%s*用戶[_%s]*:[_%s]*([^\n]-)%s*===') or
		-- === Example ===
		umatch(introText, '===%s*([^\n]-)%s*===')
	end
	
	-- Methods for seconds left and time left.
	
	function data:getSecondsLeft()
		checkSelf(self, 'getSecondsLeft')
		local endTime = self.endTime
		if not endTime then
			return nil
		end
		local now = tonumber(lang:formatDate("U"))
		local success, endTimeU = pcall(lang.formatDate, lang, 'U', endTime)
		if not success then
			return nil
		end
		endTimeU = tonumber(endTimeU)
		if not endTimeU then
			return nil
		end
		local secondsLeft = endTimeU - now
		if secondsLeft <= 0 then
			return 0
		else
			return secondsLeft
		end
	end

	function data:getTimeLeft()
		checkSelf(self, 'getTimeLeft')
		local secondsLeft = self:getSecondsLeft()
		if not secondsLeft then
			return nil
		end
		return mw.ustring.gsub(lang:formatDuration(secondsLeft, {'days', 'hours'}), ' and', ',')
	end
	
	function data:getReport()
		-- Gets the URI object for Jimmy's RfA Analysis tool
		checkSelf(self, 'getReport')
		return mw.uri.new('//tools.wmflabs.org/jimmy/cgi-bin/rfa.py?title=' .. mw.uri.encode(title.prefixedText))
	end
	
	function data:getStatus()
		-- Gets the current status of the RfX. Returns either "successful", "unsuccessful",
		-- "open", or "pending closure". Returns nil if the status could not be found.
		checkSelf( self, 'getStatus' )
		-- 中文维基百科的RfX并没有有效判断成功与失败的方法，只能判断结束与否。
		local secondsLeft = self:getSecondsLeft()
		if secondsLeft and secondsLeft > 0 then
			return '投票中'
		elseif secondsLeft and secondsLeft <= 0 then
			return '已结束'
		else
			return nil
		end
	end
	
	-- Specify which fields are read-only, and prepare the metatable.
	local readOnlyFields = {
		getTitleObject = true,
		['type'] = true,
		getSupportUsers = true,
		getOpposeUsers = true,
		getNeutralUsers = true,
		supports = true,
		opposes = true,
		neutrals = true,
		endTime = true,
		rawEndTime = true,
		percent = true,
		user = true,
		dupesExist = true,
		getSecondsLeft = true,
		getTimeLeft = true,
		getReport = true,
		getStatus = true
	}
	
	local function pairsfunc( t, k )
		local v
		repeat
			k = next( readOnlyFields, k )
			if k == nil then
				return nil
			end
			v = t[k]
		until v ~= nil
		return k, v
	end

	return setmetatable( obj, {
		__pairs = function ( t )
			return pairsfunc, t, nil
		end,
		__index = data,
		__newindex = function( t, key, value )
			if readOnlyFields[ key ] then
				error( '下标"' .. key .. '"只读', 2 )
			else
				rawset( t, key, value )
			end
		end,
		__tostring = function( t )
			return t:getTitleObject().prefixedText
		end
	} )
end

return rfx