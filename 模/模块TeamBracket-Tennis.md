--
-- This module implements many tennis bracket templates
--

local p = {}
local args = {}
local rounds
local sets = {}
local compact
local byes
local hideSeeds
local showSeeds
local hideHeadings
local showThird
local offsetThird
local compactFinal
local RD1seedmap = {}
local tcats = ''

local function isnotblank(s)
	return s and s ~= ''
end

local function isblank(s)
	return (not s) or (s == '')
end

local function parseArgs(frame)
	local fargs = frame.args
	local pargs = frame:getParent().args;

	local r = tonumber(fargs.rounds or '') or tonumber(pargs.rounds or '') or 2
	local teams = math.pow(2, r)
	local rdstr = 'RD' .. tostring(r)
	local rdbstr = 'RD' .. tostring(r) .. 'b'
	local rdp1str = 'RD' .. tostring(r+1)

	for i=1,2 do
		local targs = (i == 1) and pargs or fargs
		for k,v in pairs(targs) do
			if type(k) == 'string' then
				if k:find('^[R3][Dr][d1-9]b?%-[a-z][a-z]*00*') then
					k = mw.ustring.gsub(k, '^([R3][Dr][d1-9]b?%-[a-z][a-z]*)00*', '%1')
					if (teams < 10) then 
						tcats = tcats .. '[[Category:Pages_using_a_tennis_bracket_with_deprecated_syntax|P]]'
					end
				end
				if k:find('^' .. rdp1str) then
					k = mw.ustring.gsub(k, '^' .. rdp1str, '3rd')
					tcats = tcats .. '[[Category:Pages_using_a_tennis_bracket_with_deprecated_syntax|3]]'
				elseif k:find('^' .. rdbstr) then
					k = mw.ustring.gsub(k, '^' .. rdbstr, '3rd')
				elseif k:find('^' .. rdstr .. '%-[a-z][a-z]*3') then
					k = mw.ustring.gsub(k, '^' .. rdstr .. '(%-[a-z][a-z]*)3', '3rd%11')
				elseif k:find('^' .. rdstr .. '%-[a-z][a-z]*4') then
					k = mw.ustring.gsub(k, '^' .. rdstr .. '(%-[a-z][a-z]*)4', '3rd%12')
				elseif  k:find('^Consol') then
					k = mw.ustring.gsub(k, '^Consol', '3rd')
					tcats = tcats .. '[[Category:Pages_using_a_tennis_bracket_with_deprecated_syntax|3]]'
				elseif k:find('^group[0-9]') then
					tcats = tcats .. '[[Category:Pages_using_a_tennis_bracket_with_deprecated_syntax|G]]'
				end
			end
			args[k] = v
		end
	end

	if (args['byes'] and (args['byes'] == 'yes' or args['byes'] == 'y')) then
		tcats = tcats .. '[[Category:Pages_using_a_tennis_bracket_with_deprecated_syntax|B]]'
	end
end

local function parseSeedmap(s)
	s = mw.text.split((s or '0') .. '/', '[%s]*/[%s]*')
	local teams = math.pow(2, rounds)
	for r=1,teams do
		RD1seedmap[r] = 1
	end
	for r=1,#s do
		if tonumber(s[r] or 'x') then
			RD1seedmap[tonumber(s[r])] = 0
		end
	end
	local c = 1
	for r=1,teams do
		if RD1seedmap[r] > 0 then
			RD1seedmap[r] = c
			c = c + 1
		end
	end
end

local function parseSets(s)
	s = mw.text.split((s or '5') .. '/', '[%s]*/[%s]*')
	local n = showThird and (rounds + 1) or (rounds)
	for r=1,n do
		if s[r] ~= nil and s[r] ~= '' and tonumber(s[r]) then
			sets[r] = tonumber(s[r])
		elseif sets[r-1] then
			sets[r] = sets[r-1]
		else
			sets[r] = 5
		end
	end
end

local function addTableRow(tbl)
	return tbl:tag('tr')
end

local function addBlank(row, width)
	local cell = row:tag('td')
	if width then
		cell:css('width', width)
	end
	return cell
end

local function addHeading(row, r, text)
	row:tag('td')
		:attr('colspan', tonumber(hideSeeds and '1' or '2') + sets[r])
		:css('text-align', 'center')
		:css('border', '1px solid #aaa')
		:css('background-color', args['RD-shade'] or '#f2f2f2')
		:wikitext(text)
		:newline()
end

local function getWidth(param, default)
	local arg = args[param .. '-width']
	if isblank(arg) then
		arg = default
	end
	if tonumber(arg) ~= nil then
		arg = arg .. 'px'
	end
	return arg
end

local function getTeamArgName(round, type, team)
	if round > rounds then
		return string.format('3rd-%s%d', type, team)
	else
		if (round == 1) then
			team = RD1seedmap[team]
			if team == 0 then
				return 'NIL'
			end
		end
		return string.format('RD%d-%s%d', round, type, team)
	end
end

local function getShadeArg(round, team, s)
	local argname = getTeamArgName(round, 'shade', team) .. (s and ('-' .. s) or '')
	local value = args[argname]
	if isblank(value) then
		return '#f9f9f9'
	end
	return value
end

local function getScoreArg(round, team, s)
	local argname = getTeamArgName(round, 'score', team) .. (s and ('-' .. s) or '')
	local value = args[argname]
	if isblank(value) then
		return ''
	end
	return value
end

local function getTeamArg(round, type, team)
	local argname = getTeamArgName(round, type, team)
	local value = args[argname]
	if isblank(value) then
		return ''
	end
	if mw.ustring.find(value, '[%s]*<[%s/]*[Bb][Rr][%s/]*>[%s ]*&[Nn][Bb][Ss][Pp];[%s]*') then
		tcats = '[[Category:Pages_using_a_team_bracket_with_nbsp|Category:Pages using a team bracket with nbsp]]'
	end
	return mw.ustring.gsub(value, '[%s]*<[%s/]*[Bb][Rr][%s/]*>[%s ]*&[Nn][Bb][Ss][Pp];[%s]*', '<br/>')
end

local function isHidden(r, team)
	return isblank( getTeamArg(r, 'team', team) )
end

local function getRoundName(round)
	local name = args['RD' .. round]
	if isnotblank(name) then
		return name
	end
	local roundFromLast = rounds - round + 1
	if roundFromLast == 1 then
		return "Finals"
	elseif roundFromLast == 2 then
		return "Semifinals"
	elseif roundFromLast == 3 then
		return "Quarterfinals"
	else
		return "Round of " .. math.pow(2, roundFromLast)
	end
end

local function addPath(rows, index, round, top, left, w)
	local prop = top and 'border-bottom-width' or 'border-top-width'
	if left and round == 1 then
		if compact then
			addBlank(rows[index])
		else
			addBlank(rows[index]):css('height', '7px')
			addBlank(rows[index + 1]):css('height', '7px')
		end
		return nil
	else
		local cell = addBlank(rows[index])
			:attr('rowspan', (not compact) and '2' or nil)
			:css('border-width', '0')
			:css('border-style', 'solid')
			:css('border-color', 'black')
		if left or round < rounds and not left then
			cell:css(prop, w or '2px')
		end
		return cell
	end
end

local function renderTeam(row, round, team, top, otherbye)
	local seedCell
	local seedArg = getTeamArg(round, 'seed', team)
	-- seed value for the paired team
	local pairSeedArg = otherbye and '' 
		or getTeamArg(round, 'seed', team % 2 == 0 and team-1 or team+1)
	-- show seed if seed is defined for either or both
	local showSeed = showSeeds
		or isnotblank(seedArg)
		or isnotblank(pairSeedArg)
	if showSeed and (not hideSeeds) then
		seedCell = row:tag('td')
			:css('text-align', 'center')
			:css('background-color', '#f2f2f2')
			:css('border', '1px solid #aaa')
			:css('border-top-width', (top or otherbye) and '1px' or '0')
			:attr('rowspan', (not compact) and '2' or nil)
			:wikitext(seedArg)
			:newline()
	end

	local teamArg = getTeamArg(round, 'team', team)
	if isblank(teamArg) then
		teamArg = ' '
	end

	local teamCell = row:tag('td')
		:css('background-color', '#f9f9f9')
		:css('border', '1px solid #aaa')
		:css('border-top-width', (top or otherbye) and '1px' or '0')
		:css('padding', '0 2px')
		:attr('rowspan', (not compact) and '2' or nil)
		:wikitext(teamArg)
		:newline()
	if not showSeed and (not hideSeeds) then
		teamCell:attr('colspan', '2')
	end

	local scoreCells = {}
	for s = 1, sets[round] do
		scoreCells[s] = row:tag('td')
			:css('text-align', 'center')
			:css('border-color', '#aaa')
			:css('border-style', 'solid')
			:css('border-top-width', (top or otherbye) and '1px' or '0')
			:css('border-left-width', '0')
			:css('border-right-width', '1px')
			:css('border-bottom-width', '1px')	
			:css('background-color', getShadeArg(round, team, s))
			:attr('rowspan', (not compact) and '2' or nil)
			:wikitext(getScoreArg(round, team, s))
			:newline()
	end
end

local function renderRound(rows, count, r)
	local teams = math.pow(2, rounds - r + 1)
	local step = count / teams
	local topTeam = true -- is top row in match-up
	local topPair = true -- is top match-up in pair of match-ups
	local team = 1

	for i = 1, count, step do
		local offset, height, blank

		local hideteam = false
		local otherhideteam = false
		local hideleftpath = false
		if r <= byes then
			hideteam = isHidden(r, team)
			otherhideteam = isHidden(r, team % 2 == 0 and team-1 or team+1)
		end
		if (r == 1) and (RD1seedmap[team] <= 0) then
				hideteam = true
		end
		if (r > 1) and (r <= (byes + 1)) then
			hideleftpath = isHidden(r-1, 2*team-1) and isHidden(r-1, 2*team)
		end
		if (r == 2) and (RD1seedmap[2*team-1] <= 0 and RD1seedmap[2*team] <= 0) then
			hideleftpath = true
		end
		if compactFinal and (r == rounds) then
			hideleftpath = true
		end

		-- empty space above or below
		if compact then
			offset = topTeam and i or i + 1
			height = step - 1
		-- leave room for groups for teams other than first and last
		elseif team == 1 or team == teams then
			offset = topTeam and i or i + 2
			height = step - 2
		else
			offset = topTeam and i + 1 or i + 2
			height = step - 3
		end
		if showThird and (r == rounds) and (not topTeam) then
			height = offset - offsetThird
		end
		if compactFinal and (r == (rounds - 1)) then
			if team == 2 then
				height = height - 3
			end
			if team == 3 then
				height = height - 1
				offset = offset + 1
				rows[offset-3]:tag('td')
					:attr('colspan', tonumber(hideSeeds and '2' or '3') + sets[r])
				rows[offset-4]:tag('td')
				addHeading(rows[offset-4], r + 1, getRoundName(r+1))
				rows[offset-4]:tag('td')
					:attr('rowspan', 2)
					:css('border-color', 'black')
					:css('border-style', 'solid')
					:css('border-width', '0')
					:css('border-right-width', '2px')
			end
		end
		if height > 0 then
			blank = addBlank(rows[offset])
				:attr('colspan', tonumber(hideSeeds and '3' or '4') + sets[r])
				:attr('rowspan', height)
				:css('border-color', 'black')
				:css('border-style', 'solid')
				:css('border-width', '0')
		end
		-- add bracket
		local j = topTeam and i + step - (compact and 1 or 2) or i
		-- add left path
		addPath(rows, j, r, topTeam, true, hideleftpath and '0' or '2px')
		if hideteam then
			rows[j]:tag('td')
				:attr('colspan', tonumber(hideSeeds and '1' or '2') + sets[r])
				:attr('rowspan', (not compact) and 2 or nil)
		else
			renderTeam(rows[j], r, team, topTeam, otherhideteam)
		end
		local rightPath = addPath(rows, j, r, topTeam, false, hideteam and '0' or '2px')
		if not topTeam then topPair = not topPair end
		if not topPair and r < rounds and (not hideteam) then
			if blank then blank:css('border-right-width', '2px') end
			rightPath:css('border-right-width', '2px')
		end
		if compactFinal and (r == rounds) then
			local prop = (team == 1) and 'border-bottom-width' or 'border-top-width'
			rightPath:css('border-right-width', '2px')
				:css(prop, '2px')
		end
		team = team + 1
		topTeam = not topTeam
	end
end

local function renderGroups(rows, count, round)
	local roundFromLast = rounds - round + 1
	local groups = math.pow(2, roundFromLast - 2)
	local step = count / groups
	local group = 1
	local offset = 0
	local team = 0
	local w = '2px'

	for r = 1,round do
		offset = offset + (hideSeeds and 3 or 4) + sets[r]
	end
	for i = step / 2, count, step do
		local name = 'RD' .. round .. '-group' .. group
		addBlank(rows[i]):css('height', '7px')
		addBlank(rows[i + 1]):css('height', '7px')
		addBlank(rows[i])
			:attr('rowspan', '2')
			:attr('colspan', offset - 2)
			:css('text-align', 'center')
			:wikitext(args[name])
			:newline()
		if (round <= byes) then
			team = i/(step/2)
			w = isHidden(round, 2*team-1) and isHidden(round, 2*team) and '0' or '2px'
		end
		addBlank(rows[i])
			:css('border-color', 'black')
			:css('border-style', 'solid')
			:css('border-width', '0 ' .. w .. ' 0 0')
		if (round <= byes) then
			team = team + 1
			w = isHidden(round, 2*team-1) and isHidden(round, 2*team) and '0' or '2px'
		end
		addBlank(rows[i+1])
			:css('border-color', 'black')
			:css('border-style', 'solid')
			:css('border-width', '0 ' .. w ..' 0 0')
		group = group + 1
	end
end

local function getThirdOffset()
	local offset = (compact and 1 or 3) * (math.pow(2, rounds) - math.pow(2, rounds-3)) - (compact and 2 or 4)
	if rounds < 4 then
		offset = compact and 8 or 17
		if rounds < 3 then
			offset = compact and 6 or 10
			if rounds < 2 then
				offset = compact and 4 or 6
			end
		end
	end
	return offset
end

local function renderThird(rows, count)
	local k = offsetThird
	local row = rows[k]
	local blank
	--if (offsetThird < count) then
		--blank = addBlank(row)
		--blank:attr('colspan', tonumber(hideSeeds and '3' or '4') + sets[1])
	--end
	blank = addBlank(row)
	addHeading(row, rounds + 1, args['3rd'] or 'Third place')
	k = k + (compact and 2 or 3)
	for i = 1,2 do
		row = rows[k]
		blank = addBlank(row)
		renderTeam(row, rounds + 1, i, i == 1, false)
		k = k + (compact and 1 or 2)
	end
end

local function renderTree(tbl)
	-- create 3 or 1 rows for every team
	local count = math.pow(2, rounds) * (compact and 1 or 3)
	local offsetcount = 2 * (compact and 1 or 3) + (compact and 2 or 3)
	local rows = {}
	offsetThird = getThirdOffset()
	for i = 1, count do
		rows[i] = addTableRow(tbl)
	end
	if showThird then
		for i = (count+1), (offsetcount + offsetThird) do
			rows[i] = addTableRow(tbl)
			if (rounds > 1) then
				local blank = addBlank(rows[i])
				blank:attr('colspan', tonumber(hideSeeds and '3' or '4') + sets[1])
				if compact and (rounds > 2) then
					blank = addBlank(rows[i])
					blank:attr('colspan', tonumber(hideSeeds and '3' or '4') + sets[1])
				end
			end
		end
	end
	if not compact then
		-- fill rows with groups
		for r = 1, rounds - 1 do
			renderGroups(rows, count, r)
		end
	end
	-- fill rows with bracket
	for r = 1, rounds do
		renderRound(rows, count, r)
	end
	if showThird then
		renderThird(rows, count, compact)
	end
end

local function renderHeadings(tbl)
	local titleRow = addTableRow((not hideHeadings) and tbl or mw.html.create('table'))
	local widthRow = addTableRow(tbl)
	for r = 1, (compactFinal and (rounds-1) or rounds) do
		addBlank(titleRow)
		addBlank(widthRow, r > 1 and '5px' or '1px')
		addHeading(titleRow, r, getRoundName(r) )
		local seedCell
		if (not hideSeeds) then
			seedCell = addBlank(widthRow, getWidth('seed', '25px'))
		end
		local teamCell = addBlank(widthRow, getWidth('team', '150px'))
		local scoreCells = {}
		for s = 1, sets[r] do
			scoreCells[s] = addBlank(widthRow, getWidth('score', '12px'))
		end
		addBlank(titleRow)
		addBlank(widthRow, r < rounds and '5px' or '1px')

		if compact then
			teamCell:css('height', '7px')
		else
			if seedCell then
				seedCell:wikitext(' ')
			end
			teamCell:wikitext(' ')
			for s = 1, sets[r] do
				scoreCells[s]:wikitext(' ')
			end
		end
	end
end

function p.teamBracket(frame)
	parseArgs(frame)
	rounds = tonumber(args.rounds) or 2
	local teams = math.pow(2, rounds)
	compact = (args['compact'] and (args['compact'] == 'yes' or args['compact'] == 'y'))
	compactFinal = ((rounds > 4) and compact and args['compact-final'] and (args['compact-final'] == 'yes' or args['compact-final'] == 'y'))
	hideSeeds = (args['seeds'] and (args['seeds'] == 'no' or args['seeds'] == 'n'))
	showSeeds = (args['seeds'] and (args['seeds'] == 'yes' or args['seeds'] == 'y'))
	byes = (args['byes'] and (args['byes'] == 'yes' or args['byes'] == 'y') and 1) or (tonumber(args['byes'] or '0') or 0)
	hideHeadings = (args['headings'] and (args['headings'] == 'no' or args['headings'] == 'n'))
	showThird = isnotblank(args['3rd']) or isnotblank(args['3rd-team1']) or isnotblank(args['3rd-team2'])
	parseSeedmap(args['RD1-omit'])
	parseSets(args.sets)

	-- create the table
	local tbl = mw.html.create('table')
		:css('border-style', 'none')
		:css('font-size', '90%')
		:css('margin', '1em 2em 1em 1em')
		:css('border-collapse', 'separate')
		:css('border-spacing', '0')
		:attr('cellpadding', '0')

	if (args['nowrap'] and (args['nowrap'] == 'yes' or args['nowrap'] == 'y')) then
		tbl:css('white-space', 'nowrap')
	end

	renderHeadings(tbl)
	renderTree(tbl)
	return tostring(tbl) .. tcats
end

return p