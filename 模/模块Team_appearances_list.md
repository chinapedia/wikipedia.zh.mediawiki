-- This module implements [[Template:Team_appearances_list|Template:Team appearances list]].

local p = {}

local data_competitions
local function load_data(frame)
	-- Load data module (or its sandbox) and set variables from its exported data.
	if not data_competitions then
		frame = frame or mw.getCurrentFrame()
		local sandbox = frame:getTitle():find('sandbox', 1, true) and '/sandbox' or ''
		local datamod = mw.loadData('Module:Team appearances list/data' .. sandbox)
		data_competitions = datamod.competitions
	end
end

local function strip_to_nil(text)
	-- If text is a string, return its trimmed content, or nil if empty.
	-- Otherwise return text (which may, for example, be nil).
	if type(text) == 'string' then
		text = text:match('(%S.-)%s*$')
	end
	return text
end

local function make_options(args)
	-- Return table of options from validated args or throw error.
	local options = {}
	local function valid_integer(name, min, max, is_optional)
		local arg = args[name]
		if arg == nil or arg == '' then
			if is_optional then
				return nil
			end
			error('Parameter ' .. name .. ' is missing')
		end
		arg = tonumber(arg)
		if type(arg) ~= 'number' then
			error('Parameter ' .. name .. ' is not a number')
		end
		if math.floor(arg) ~= arg then
			error('Parameter ' .. name .. ' is not an integer')
		end
		if not (min <= arg and arg <= max) then
			error('Parameter ' .. name .. ' is not valid')
		end
		return arg
	end
	local function valid_text(name)
		local arg = args[name]
		if arg == nil or arg == '' then
			error('Parameter ' .. name .. ' is missing')
		end
		if type(arg) ~= 'string' then
			error('Parameter ' .. name .. ' is not a string')
		end
		return arg
	end
	options.competition = valid_text('competition')
	options.team = valid_text('team')
	options.competitions = data_competitions[options.competition]
	local begin_optional
	if options.competitions then
		begin_optional = true
	else
		options.interval = valid_integer('interval', 1, 30)
	end
	options.begin_year = valid_integer('begin_year', 1800, 2100, begin_optional)
	options.end_year = valid_integer('end_year', 1800, 2100, true)
	if options.begin_year and options.end_year then
		if options.begin_year > options.end_year then
			error('Parameter end_year must not be before begin_year')
		end
	end
	options.disqualified_year = valid_integer('disqualified_year', 1800, 2100, true)
	return options
end

local function extract_range(text)
	-- Return first (if text is a single year), or first, last if a range.
	-- The returned values are numbers.
	-- Return nothing if text is invalid.
	local year = text:match('^(%d+)$')
	if year then
		if #year == 4 then
			return tonumber(year)
		end
		return
	end
	local first, dash, last = text:match('^(%d+)(%D+)(%d+)$')
	if not (first and #first == 4) then
		return
	end
	dash = strip_to_nil(dash)
	if not (dash == '-' or dash == '–') then
		return
	end
	if #last ~= 4 then
		if #last == 2 then
			last = first:sub(1, 2) .. last
		else
			return
		end
	end
	first = tonumber(first)
	last = tonumber(last)
	if first < last then
		return first, last
	elseif first == last then
		return first
	end
end

local function competition_absences(data)
	-- Return two tables with absent years and absent year ranges.
	-- Parameter data is an array of strings from template parameters, or
	-- numbers or strings from built-in data.
	-- Parameters that are blank or not numbers or strings are ignored.
	local absent_years, absent_ranges = {}, {}
	for _, item in ipairs(data) do
		if type(item) == 'number' then
			absent_years[item] = true
		else
			item = strip_to_nil(item)
			if type(item) == 'string' then
				local first, last = extract_range(item)
				if not first then
					error('Year ' .. item .. ' is not valid')
				end
				if last then
					table.insert(absent_ranges, {first, last})
				else
					absent_years[first] = true
				end
			end
		end
	end
	return absent_years, absent_ranges
end

local function competition_information(args)
	-- Return four tables with competition and team information:
	-- * List of competition years that the team attended or could have attended.
	-- * Table of disqualified years (the team was absent, but there is an
	--   article regarding the absent year).
	-- * Table of absent years (when the team did not attend).
	-- * List of pairs of years (absent for each year in range, inclusive).
	local options = make_options(args)
	local absences
	local comp_years = {}
	local begin_year = options.begin_year
	local end_year = options.end_year
	local competitions = options.competitions
	if competitions then
		absences = competitions[options.team]
		begin_year = begin_year or (absences and absences.begin_year) or 0
		end_year = end_year or (absences and absences.end_year) or 9999
		for _, y in ipairs(competitions) do
			if y > end_year then
				break
			elseif y >= begin_year then
				table.insert(comp_years, y)
			end
		end
	else
		end_year = end_year or (os.date('!*t').year + options.interval)
		for y = begin_year, end_year, options.interval do
			table.insert(comp_years, y)
		end
	end
	local disqualified_years = {}
	if options.disqualified_year then
		-- Input currently only allows entry of a single disqualified year.
		-- However processing works for any number of such years.
		disqualified_years[options.disqualified_year] = true
	end
	return comp_years, disqualified_years, competition_absences(absences or args)
end

function p._main(args)
	load_data()  -- in case this function is called by another module
	local hlist = require('Module:List').horizontal
	local competitions, disqualified_years, absent_years, absent_ranges = competition_information(args)
	local current_year = os.date('!*t').year
	local function is_absent(y)
		if absent_years[y] then
			return true
		end
		for _, range in ipairs(absent_ranges) do
			if range[1] <= y and y <= range[2] then
				return true
			end
		end
		return false
	end
	local appearances = {}
	local absent_first, absent_last
	for i = 1, #competitions + 1 do  -- +1 to handle any trailing absences
		local y = competitions[i]
		if y and is_absent(y) then
			if absent_first then
				absent_last = y
			else
				absent_first = y
			end
		else
			if absent_first then
				table.insert(appearances,
					'<span style="color:gray">' ..
					(absent_last and (absent_first .. '–' .. absent_last) or absent_first) ..
					'</span>')
				absent_first, absent_last = nil, nil
			end
			if y then
				local display = tostring(y)
				if y > current_year then
					display = '<i>' .. display .. '</i>'
				end
				if disqualified_years[y] then
					display = '<del>' .. display .. '</del>'
				end
				table.insert(appearances, string.format(
					'[[%d年%s%s代表團|%s]]',
					y, args.competition, args.team, display
				))
			end
		end
	end
	return hlist(appearances)
end

function p.main(frame)
	load_data(frame)
	return p._main(frame:getParent().args)
end

return p