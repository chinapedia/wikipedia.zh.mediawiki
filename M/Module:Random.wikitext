-- This module contains a number of functions that make use of random numbers.

local cfg = {}

--------------------------------------------------------------------------------------
-- Configuration
--------------------------------------------------------------------------------------

-- Set this to true if your wiki has a traffic rate of less than one edit every two minutes or so.
-- This will prevent the same "random" number being generated many times in a row until a new edit is made
-- to the wiki. This setting is only relevant if the |same= parameter is set.
cfg.lowTraffic = false

-- If cfg.lowTraffic is set to true, and the |same= parameter is set, this value is used for the refresh rate of the random seed.
-- This is the number of seconds until the seed is changed. Getting this right is tricky. If you set it too high, the same number
-- will be returned many times in a row. If you set it too low, you may get different random numbers appearing on the same page,
-- particularly for pages that take many seconds to process.
cfg.seedRefreshRate = 60

--------------------------------------------------------------------------------------
-- End configuration
--------------------------------------------------------------------------------------

local p = {} -- For functions available from other Lua modules.
local l = {} -- For functions not available from other Lua modules, but that need to be accessed using table keys.

local yesno = require('Module:Yesno')
local makeList = require('Module:List').makeList

--------------------------------------------------------------------------------------
-- Helper functions
--------------------------------------------------------------------------------------

local function raiseError(msg)
	-- This helps to generate a wikitext error. It is the calling function's responsibility as to how to include it in the output.
	return mw.ustring.format('<b class="error">[[Module:Random|Module:Random]] error: %s.</b>', msg)
end

--------------------------------------------------------------------------------------
-- random number function
--------------------------------------------------------------------------------------

local function getBigRandom(l, u)
	-- Gets a random integer between l and u, and is not limited to RAND_MAX.
	local r = 0
	local n = 2^math.random(30) -- Any power of 2.
	local limit = math.ceil(53 / (math.log(n) / math.log(2)))
	for i = 1, limit do
		r = r + math.random(0, n - 1) / (n^i)
	end
	return math.floor(r * (u - l + 1)) + l
end

function l.number(args)
	-- Gets a random number.
	first = tonumber(args[1])
	second = tonumber(args[2])
	-- This needs to use if statements as math.random won't accept explicit nil values as arguments.
	if first then
		if second then
			if first > second then -- Second number cannot be less than the first, or it causes an error.
				first, second = second, first
			end
			return getBigRandom(first, second)
		else
			return getBigRandom(1, first)
		end
	else
		return math.random()
	end
end

--------------------------------------------------------------------------------------
-- Date function
--------------------------------------------------------------------------------------

function l.date(args)
	-- This function gets random dates, and takes timestamps as positional arguments.
	-- With no arguments specified, it outputs a random date in the current year.
	-- With two arguments specified, it outputs a random date between the timestamps.
	-- With one argument specified, the date is a random date between the unix epoch (1 Jan 1970) and the timestamp.
	-- The output can be formatted using the "format" argument, which works in the same way as the #time parser function.
	-- The default format is the standard Wikipedia timestamp.
	local lang = mw.language.getContentLanguage()

	local function getDate(format, ts)
		local success, date = pcall(lang.formatDate, lang, format, ts)
		if success then
			return date
		end
	end

	local function getUnixTimestamp(ts)
		local unixts = getDate('U', ts)
		if unixts then
			return tonumber(unixts)
		end
	end

	local t1 = args[1]
	local t2 = args[2]
	
	-- Find the start timestamp and the end timestamp.
	local startTimestamp, endTimestamp
	if not t1 then
		-- Find the first and last second in the current year.
		local currentYear = tonumber(getDate('Y'))
		local currentYearStartUnix = tonumber(getUnixTimestamp('1 Jan ' .. tostring(currentYear)))
		local currentYearEndUnix = tonumber(getUnixTimestamp('1 Jan ' .. tostring(currentYear + 1))) - 1
		startTimestamp = '@' .. tostring(currentYearStartUnix) -- @ is used to denote Unix timestamps with lang:formatDate.
		endTimestamp = '@' .. tostring(currentYearEndUnix)
	elseif t1 and not t2 then
		startTimestamp = '@0' -- the Unix epoch, 1 January 1970
		endTimestamp = t1
	elseif t1 and t2 then
		startTimestamp = t1
		endTimestamp = t2
	end

	-- Get Unix timestamps and return errors for bad input (or for bugs in the underlying PHP library, of which there are unfortunately a few)
	local startTimestampUnix = getUnixTimestamp(startTimestamp)
	local endTimestampUnix = getUnixTimestamp(endTimestamp)
	if not startTimestampUnix then
		return raiseError('"' .. tostring(startTimestamp) .. '" was not recognised as a valid timestamp')
	elseif not endTimestampUnix then
		return raiseError('"' .. tostring(endTimestamp) .. '" was not recognised as a valid timestamp')
	elseif startTimestampUnix > endTimestampUnix then
		return raiseError('the start date must not be later than the end date (start date: "' .. startTimestamp .. '", end date: "' .. endTimestamp .. '")')
	end

	-- Get a random number between the two Unix timestamps and return it using the specified format.
	local randomTimestamp = getBigRandom(startTimestampUnix, endTimestampUnix)
	local dateFormat = args.format or 'H:i, d F Y (T)'
	local result = getDate(dateFormat, '@' .. tostring(randomTimestamp))
	if result then
		return result
	else
		return raiseError('"' .. dateFormat .. '" is not a valid date format')
	end
end

--------------------------------------------------------------------------------------
-- List functions
--------------------------------------------------------------------------------------

local function randomizeArray(t, limit)
	-- Randomizes an array. It works by iterating through the list backwards, each time swapping the entry
	-- "i" with a random entry. Courtesy of Xinhuan at http://forums.wowace.com/showthread.php?p=279756
	-- If the limit parameter is set, the array is shortened to that many elements after being randomized.
	-- The lowest possible value is 0, and the highest possible is the length of the array.
	local len = #t
	for i = len, 2, -1 do
		local r = math.random(i)
		t[i], t[r] = t[r], t[i]
	end
	if limit and limit < len then
		local ret = {}
		for i, v in ipairs(t) do
			if i > limit then
				break
			end
			ret[i] = v
		end
		return ret
	else
		return t
	end
end

local function removeBlanks(t)
	-- Removes blank entries from an array so that it can be used with ipairs.
	local ret = {}
	for k, v in pairs(t) do
		if type(k) == 'number' then
			table.insert(ret, k)
		end
	end
	table.sort(ret)
	for i, v in ipairs(ret) do
		ret[i] = t[v]
	end
	return ret
end

local function makeSeparator(sep)
	if sep == 'space' then
		-- Include an easy way to use spaces as separators.
		return ' '
	elseif sep == 'newline' then
		-- Ditto for newlines
		return '\n'
	elseif type(sep) == 'string' then
		-- If the separator is a recognised MediaWiki separator, use that. Otherwise use the value of sep if it is a string.
		local mwseparators = {'dot', 'pipe', 'comma', 'tpt-languages'}
		for _, mwsep in ipairs(mwseparators) do
			if sep == mwsep then
				return mw.message.new( sep .. '-separator' ):plain()
			end
		end
		return sep
	end
end

local function makeRandomList(args)
	local list = removeBlanks(args)
	list = randomizeArray(list, tonumber(args.limit))
	return list
end

function l.item(args)
	-- Returns a random item from a numbered list.
	local list = removeBlanks(args)
	local len = #list
	if len >= 1 then
		return list[math.random(len)]
	end
end

function l.list(args)
	-- Randomizes a list and concatenates the result with a separator.
	local list = makeRandomList(args)
	local sep = makeSeparator(args.sep or args.separator)
	return table.concat(list, sep)
end

function l.text_list(args)
	-- Randomizes a list and concatenates the result, text-style. Accepts separator and conjunction arguments.
	local list = makeRandomList(args)
	local sep = makeSeparator(args.sep or args.separator)
	local conj = makeSeparator(args.conj or args.conjunction)
	return mw.text.listToText(list, sep, conj)
end

function l.array(args)
	-- Returns a Lua array, randomized. For use from other Lua modules.
	return randomizeArray(args.t, args.limit)
end

--------------------------------------------------------------------------------------
-- HTML list function
--------------------------------------------------------------------------------------

function l.html_list(args, listType)
	-- Randomizes a list and turns it into an HTML list. Uses [[Module:List|Module:List]].
	listType = listType or 'bulleted'
	local listArgs = makeRandomList(args) -- Arguments for [[Module:List|Module:List]].
	for k, v in pairs(args) do
		if type(k) == 'string' then
			listArgs[k] = v
		end
	end
	return makeList(listType, listArgs)
end

--------------------------------------------------------------------------------------
-- The main function. Called from other Lua modules.
--------------------------------------------------------------------------------------

function p.main(funcName, args, listType)
	-- Sets the seed for the random number generator and passes control over to the other functions.
	local same = yesno(args.same)
	if not same then
		-- Generates a different number every time the module is called, even from the same page.
		-- This is because of the variability of os.clock (the time in seconds that the Lua script has been running for).
		math.randomseed(mw.site.stats.edits + mw.site.stats.pages + os.time() + math.floor(os.clock() * 1000000000))
	else
		if not cfg.lowTraffic then
			-- Make the seed as random as possible without using anything time-based. This means that the same random number
			-- will be generated for the same input from the same page - necessary behaviour for some wikicode templates that
			-- assume bad pseudo-random-number generation.
			local stats = mw.site.stats
			local views = stats.views or 0 -- This is not always available, so we need a backup.
			local seed = views + stats.pages + stats.articles + stats.files + stats.edits + stats.users + stats.activeUsers + stats.admins -- Make this as random as possible without using os.time() or os.clock()
			math.randomseed(seed)
		else
			-- Make the random seed change every n seconds, where n is set by cfg.seedRefreshRate.
			-- This is useful for low-traffic wikis where new edits may not happen very often.
			math.randomseed(math.floor(os.time() / cfg.seedRefreshRate))
		end
	end
	if type(args) ~= 'table' then
		error('the second argument to p.main must be a table')
	end
	return l[funcName](args, listType)
end
	
--------------------------------------------------------------------------------------
-- Process arguments from #invoke
--------------------------------------------------------------------------------------

local function makeWrapper(funcName, listType)
	-- This function provides a wrapper for argument-processing from #invoke.
	-- listType is only used with p.html_list, and is nil the rest of the time.
	return function (frame)
		-- If called via #invoke, use the args passed into the invoking template, or the args passed to #invoke if any exist.
		-- Otherwise assume args are being passed directly in from the debug console or from another Lua module.
		local origArgs
		if frame == mw.getCurrentFrame() then
			origArgs = frame:getParent().args
			for k, v in pairs(frame.args) do
				origArgs = frame.args
				break
			end
		else
			origArgs = frame
		end
		-- Trim whitespace and remove blank arguments.
		local args = {}
		for k, v in pairs(origArgs) do
			if type(v) == 'string' then
				v = mw.text.trim(v)
			end
			if v ~= '' then
				args[k] = v
			end
		end
		return p.main(funcName, args, listType)
	end
end

-- Process arguments for HTML list functions.
local htmlListFuncs = {
	bulleted_list           = 'bulleted',
	unbulleted_list         = 'unbulleted',
	horizontal_list         = 'horizontal',
	ordered_list            = 'ordered',
	horizontal_ordered_list = 'horizontal_ordered'
}
for funcName, listType in pairs(htmlListFuncs) do
	p[funcName] = makeWrapper('html_list', listType)
end

-- Process arguments for other functions.
local otherFuncs = {'number', 'date', 'item', 'list', 'text_list'}
for _, funcName in ipairs(otherFuncs) do
	p[funcName] = makeWrapper(funcName)
end

return p