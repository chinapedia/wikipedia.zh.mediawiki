-- Date functions for use by other modules.
-- I18N and time zones are not supported.

local MINUS = '−'  -- Unicode U+2212 MINUS SIGN
local floor = math.floor

local Date, DateDiff, diffmt  -- forward declarations
local uniq = { 'unique identifier' }

local function is_date(t)
	-- The system used to make a date read-only means there is no unique
	-- metatable that is conveniently accessible to check.
	return type(t) == 'table' and t._id == uniq
end

local function is_diff(t)
	return type(t) == 'table' and getmetatable(t) == diffmt
end

local function _list_join(list, sep)
	return table.concat(list, sep)
end

local function collection()
	-- Return a table to hold items.
	return {
		n = 0,
		add = function (self, item)
			self.n = self.n + 1
			self[self.n] = item
		end,
		join = _list_join,
	}
end

local function strip_to_nil(text)
	-- If text is a string, return its trimmed content, or nil if empty.
	-- Otherwise return text (convenient when Date fields are provided from
	-- another module which may pass a string, a number, or another type).
	if type(text) == 'string' then
		text = text:match('(%S.-)%s*$')
	end
	return text
end

local function is_leap_year(year, calname)
	-- Return true if year is a leap year.
	if calname == 'Julian' then
		return year % 4 == 0
	end
	return (year % 4 == 0 and year % 100 ~= 0) or year % 400 == 0
end

local function days_in_month(year, month, calname)
	-- Return number of days (1..31) in given month (1..12).
	if month == 2 and is_leap_year(year, calname) then
		return 29
	end
	return ({ 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 })[month]
end

local function h_m_s(time)
	-- Return hour, minute, second extracted from fraction of a day.
	time = floor(time * 24 * 3600 + 0.5)  -- number of seconds
	local second = time % 60
	time = floor(time / 60)
	return floor(time / 60), time % 60, second
end

local function hms(date)
	-- Return fraction of a day from date's time, where (0 <= fraction < 1)
	-- if the values are valid, but could be anything if outside range.
	return (date.hour + (date.minute + date.second / 60) / 60) / 24
end

local function julian_date(date)
	-- Return jd, jdz from a Julian or Gregorian calendar date where
	--   jd = Julian date and its fractional part is zero at noon
	--   jdz = same, but assume time is 00:00:00 if no time given
	-- http://www.tondering.dk/claus/cal/julperiod.php#formula
	-- Testing shows this works for all dates from year -9999 to 9999!
	-- JDN 0 is the 24-hour period starting at noon UTC on Monday
	--    1 January 4713 BC  = (-4712, 1, 1)   Julian calendar
	--   24 November 4714 BC = (-4713, 11, 24) Gregorian calendar
	local offset
	local a = floor((14 - date.month)/12)
	local y = date.year + 4800 - a
	if date.calendar == 'Julian' then
		offset = floor(y/4) - 32083
	else
		offset = floor(y/4) - floor(y/100) + floor(y/400) - 32045
	end
	local m = date.month + 12*a - 3
	local jd = date.day + floor((153*m + 2)/5) + 365*y + offset
	if date.hastime then
		jd = jd + hms(date) - 0.5
		return jd, jd
	end
	return jd, jd - 0.5
end

local function set_date_from_jd(date)
	-- Set the fields of table date from its Julian date field.
	-- Return true if date is valid.
	-- http://www.tondering.dk/claus/cal/julperiod.php#formula
	-- This handles the proleptic Julian and Gregorian calendars.
	-- Negative Julian dates are not defined but they work.
	local calname = date.calendar
	local low, high  -- min/max limits for date ranges −9999-01-01 to 9999-12-31
	if calname == 'Gregorian' then
		low, high = -1930999.5, 5373484.49999
	elseif calname == 'Julian' then
		low, high = -1931076.5, 5373557.49999
	else
		return
	end
	local jd = date.jd
	if not (type(jd) == 'number' and low <= jd and jd <= high) then
		return
	end
	local jdn = floor(jd)
	if date.hastime then
		local time = jd - jdn  -- 0 <= time < 1
		if time >= 0.5 then    -- if at or after midnight of next day
			jdn = jdn + 1
			time = time - 0.5
		else
			time = time + 0.5
		end
		date.hour, date.minute, date.second = h_m_s(time)
	else
		date.second = 0
		date.minute = 0
		date.hour = 0
	end
	local b, c
	if calname == 'Julian' then
		b = 0
		c = jdn + 32082
	else  -- Gregorian
		local a = jdn + 32044
		b = floor((4*a + 3)/146097)
		c = a - floor(146097*b/4)
	end
	local d = floor((4*c + 3)/1461)
	local e = c - floor(1461*d/4)
	local m = floor((5*e + 2)/153)
	date.day = e - floor((153*m + 2)/5) + 1
	date.month = m + 3 - 12*floor(m/10)
	date.year = 100*b + d - 4800 + floor(m/10)
	return true
end

local function fix_numbers(numbers, y, m, d, H, M, S, partial, hastime, calendar)
	-- Put the result of normalizing the given values in table numbers.
	-- The result will have valid m, d values if y is valid; caller checks y.
	-- The logic of PHP mktime is followed where m or d can be zero to mean
	-- the previous unit, and -1 is the one before that, etc.
	-- Positive values carry forward.
	local date
	if not (1 <= m and m <= 12) then
		date = Date(y, 1, 1)
		if not date then return end
		date = date + ((m - 1) .. 'm')
		y, m = date.year, date.month
	end
	local days_hms
	if not partial then
		if hastime and H and M and S then
			if not (0 <= H and H <= 23 and
					0 <= M and M <= 59 and
					0 <= S and S <= 59) then
				days_hms = hms({ hour = H, minute = M, second = S })
			end
		end
		if days_hms or not (1 <= d and d <= days_in_month(y, m, calendar)) then
			date = date or Date(y, m, 1)
			if not date then return end
			date = date + (d - 1 + (days_hms or 0))
			y, m, d = date.year, date.month, date.day
			if days_hms then
				H, M, S = date.hour, date.minute, date.second
			end
		end
	end
	numbers.year = y
	numbers.month = m
	numbers.day = d
	if days_hms then
		-- Don't set H unless it was valid because a valid H will set hastime.
		numbers.hour = H
		numbers.minute = M
		numbers.second = S
	end
end

local function set_date_from_numbers(date, numbers, options)
	-- Set the fields of table date from numeric values.
	-- Return true if date is valid.
	if type(numbers) ~= 'table' then
		return
	end
	local y = numbers.year   or date.year
	local m = numbers.month  or date.month
	local d = numbers.day    or date.day
	local H = numbers.hour
	local M = numbers.minute or date.minute or 0
	local S = numbers.second or date.second or 0
	local need_fix
	if y and m and d then
		date.partial = nil
		if not (-9999 <= y and y <= 9999 and
			1 <= m and m <= 12 and
			1 <= d and d <= days_in_month(y, m, date.calendar)) then
				if not date.want_fix then
					return
				end
				need_fix = true
		end
	elseif y and date.partial then
		if d or not (-9999 <= y and y <= 9999) then
			return
		end
		if m and not (1 <= m and m <= 12) then
			if not date.want_fix then
				return
			end
			need_fix = true
		end
	else
		return
	end
	if date.partial then
		H = nil  -- ignore any time
		M = nil
		S = nil
	else
		if H then
			-- It is not possible to set M or S without also setting H.
			date.hastime = true
		else
			H = 0
		end
		if not (0 <= H and H <= 23 and
				0 <= M and M <= 59 and
				0 <= S and S <= 59) then
			if date.want_fix then
				need_fix = true
			else
				return
			end
		end
	end
	date.want_fix = nil
	if need_fix then
		fix_numbers(numbers, y, m, d, H, M, S, date.partial, date.hastime, date.calendar)
		return set_date_from_numbers(date, numbers, options)
	end
	date.year = y    -- -9999 to 9999 ('n BC' → year = 1 - n)
	date.month = m   -- 1 to 12 (may be nil if partial)
	date.day = d     -- 1 to 31 (* = nil if partial)
	date.hour = H    -- 0 to 59 (*)
	date.minute = M  -- 0 to 59 (*)
	date.second = S  -- 0 to 59 (*)
	if type(options) == 'table' then
		for _, k in ipairs({ 'am', 'era', 'format' }) do
			if options[k] then
				date.options[k] = options[k]
			end
		end
	end
	return true
end

local function make_option_table(options1, options2)
	-- If options1 is a string, return a table with its settings, or
	-- if it is a table, use its settings.
	-- Missing options are set from table options2 or defaults.
	-- If a default is used, a flag is set so caller knows the value was not intentionally set.
	-- Valid option settings are:
	-- am: 'am', 'a.m.', 'AM', 'A.M.'
	--     'pm', 'p.m.', 'PM', 'P.M.' (each has same meaning as corresponding item above)
	-- era: 'BCMINUS', 'BCNEGATIVE', 'BC', 'B.C.', 'BCE', 'B.C.E.', 'AD', 'A.D.', 'CE', 'C.E.'
	-- Option am = 'am' does not mean the hour is AM; it means 'am' or 'pm' is used, depending on the hour,
	--    and am = 'pm' has the same meaning.
	-- Similarly, era = 'BC' means 'BC' is used if year <= 0.
	-- BCMINUS displays a MINUS if year < 0 and the display format does not include %{era}.
	-- BCNEGATIVE is similar but displays a hyphen.
	local result = { bydefault = {} }
	if type(options1) == 'table' then
		result.am = options1.am
		result.era = options1.era
	elseif type(options1) == 'string' then
		-- Example: 'am:AM era:BC' or 'am=AM era=BC'.
		for item in options1:gmatch('%S+') do
			local lhs, rhs = item:match('^(%w+)[:=](.+)$')
			if lhs then
				result[lhs] = rhs
			end
		end
	end
	options2 = type(options2) == 'table' and options2 or {}
	local defaults = { am = 'am', era = 'BC' }
	for k, v in pairs(defaults) do
		if not result[k] then
			if options2[k] then
				result[k] = options2[k]
			else
				result[k] = v
				result.bydefault[k] = true
			end
		end
	end
	return result
end

local ampm_options = {
	-- lhs = input text accepted as an am/pm option
	-- rhs = code used internally
	['am']   = 'am',
	['AM']   = 'AM',
	['a.m.'] = 'a.m.',
	['A.M.'] = 'A.M.',
	['pm']   = 'am',  -- same as am
	['PM']   = 'AM',
	['p.m.'] = 'a.m.',
	['P.M.'] = 'A.M.',
}

local era_text = {
	-- Text for displaying an era with a positive year (after adjusting
	-- by replacing year with 1 - year if date.year <= 0).
	-- options.era = { year<=0 , year>0 }
	['BCMINUS']    = { 'BC'    , ''    , isbc = true, sign = MINUS },
	['BCNEGATIVE'] = { 'BC'    , ''    , isbc = true, sign = '-'   },
	['BC']         = { 'BC'    , ''    , isbc = true },
	['B.C.']       = { 'B.C.'  , ''    , isbc = true },
	['BCE']        = { 'BCE'   , ''    , isbc = true },
	['B.C.E.']     = { 'B.C.E.', ''    , isbc = true },
	['AD']         = { 'BC'    , 'AD'   },
	['A.D.']       = { 'B.C.'  , 'A.D.' },
	['CE']         = { 'BCE'   , 'CE'   },
	['C.E.']       = { 'B.C.E.', 'C.E.' },
}

local function get_era_for_year(era, year)
	return (era_text[era] or era_text['BC'])[year > 0 and 2 or 1] or ''
end

local function strftime(date, format, options)
	-- Return date formatted as a string using codes similar to those
	-- in the C strftime library function.
	local sformat = string.format
	local shortcuts = {
		['%c'] = '%-I:%M %p %-d %B %-Y %{era}',  -- date and time: 2:30 pm 1 April 2016
		['%x'] = '%-d %B %-Y %{era}',            -- date:          1 April 2016
		['%X'] = '%-I:%M %p',                    -- time:          2:30 pm
	}
	if shortcuts[format] then
		format = shortcuts[format]
	end
	local codes = {
		a = { field = 'dayabbr' },
		A = { field = 'dayname' },
		b = { field = 'monthabbr' },
		B = { field = 'monthname' },
		u = { fmt = '%d'  , field = 'dowiso' },
		w = { fmt = '%d'  , field = 'dow' },
		d = { fmt = '%02d', fmt2 = '%d', field = 'day' },
		m = { fmt = '%02d', fmt2 = '%d', field = 'month' },
		Y = { fmt = '%04d', fmt2 = '%d', field = 'year' },
		H = { fmt = '%02d', fmt2 = '%d', field = 'hour' },
		M = { fmt = '%02d', fmt2 = '%d', field = 'minute' },
		S = { fmt = '%02d', fmt2 = '%d', field = 'second' },
		j = { fmt = '%03d', fmt2 = '%d', field = 'dayofyear' },
		I = { fmt = '%02d', fmt2 = '%d', field = 'hour', special = 'hour12' },
		p = { field = 'hour', special = 'am' },
	}
	options = make_option_table(options, date.options)
	local amopt = options.am
	local eraopt = options.era
	local function replace_code(spaces, modifier, id)
		local code = codes[id]
		if code then
			local fmt = code.fmt
			if modifier == '-' and code.fmt2 then
				fmt = code.fmt2
			end
			local value = date[code.field]
			if not value then
				return nil  -- an undefined field in a partial date
			end
			local special = code.special
			if special then
				if special == 'hour12' then
					value = value % 12
					value = value == 0 and 12 or value
				elseif special == 'am' then
					local ap = ({
						['a.m.'] = { 'a.m.', 'p.m.' },
						['AM'] = { 'AM', 'PM' },
						['A.M.'] = { 'A.M.', 'P.M.' },
					})[ampm_options[amopt]] or { 'am', 'pm' }
					return (spaces == '' and '' or ' ') .. (value < 12 and ap[1] or ap[2])
				end
			end
			if code.field == 'year' then
				local sign = (era_text[eraopt] or {}).sign
				if not sign or format:find('%{era}', 1, true) then
					sign = ''
					if value <= 0 then
						value = 1 - value
					end
				else
					if value >= 0 then
						sign = ''
					else
						value = -value
					end
				end
				return spaces .. sign .. sformat(fmt, value)
			end
			return spaces .. (fmt and sformat(fmt, value) or value)
		end
	end
	local function replace_property(spaces, id)
		if id == 'era' then
			-- Special case so can use local era option.
			local result = get_era_for_year(eraopt, date.year)
			if result == '' then
				return ''
			end
			return (spaces == '' and '' or ' ') .. result
		end
		local result = date[id]
		if type(result) == 'string' then
			return spaces .. result
		end
		if type(result) == 'number' then
			return  spaces .. tostring(result)
		end
		if type(result) == 'boolean' then
			return  spaces .. (result and '1' or '0')
		end
		-- This occurs if id is an undefined field in a partial date, or is the name of a function.
		return nil
	end
	local PERCENT = '\127PERCENT\127'
	return (format
		:gsub('%%%%', PERCENT)
		:gsub('(%s*)%%{(%w+)}', replace_property)
		:gsub('(%s*)%%(%-?)(%a)', replace_code)
		:gsub(PERCENT, '%%')
	)
end

local function _date_text(date, fmt, options)
	-- Return a formatted string representing the given date.
	if not is_date(date) then
		error('date:text: need a date (use "date:text()" with a colon)', 2)
	end
	if type(fmt) == 'string' and fmt:match('%S') then
		if fmt:find('%', 1, true) then
			return strftime(date, fmt, options)
		end
	elseif date.partial then
		fmt = date.month and 'my' or 'y'
	else
		fmt = 'dmy'
		if date.hastime then
			fmt = (date.second > 0 and 'hms ' or 'hm ') .. fmt
		end
	end
	local function bad_format()
		-- For consistency with other format processing, return given format
		-- (or cleaned format if original was not a string) if invalid.
		return mw.text.nowiki(fmt)
	end
	if date.partial then
		-- Ignore days in standard formats like 'ymd'.
		if fmt == 'ym' or fmt == 'ymd' then
			fmt = date.month and '%Y-%m %{era}' or '%Y %{era}'
		elseif fmt == 'my' or fmt == 'dmy' or fmt == 'mdy' then
			fmt = date.month and '%B %-Y %{era}' or '%-Y %{era}'
		elseif fmt == 'y' then
			fmt = date.month and '%-Y %{era}' or '%-Y %{era}'
		else
			return bad_format()
		end
		return strftime(date, fmt, options)
	end
	local function hm_fmt()
		local plain = make_option_table(options, date.options).bydefault.am
		return plain and '%H:%M' or '%-I:%M %p'
	end
	local need_time = date.hastime
	local t = collection()
	for item in fmt:gmatch('%S+') do
		local f
		if item == 'hm' then
			f = hm_fmt()
			need_time = false
		elseif item == 'hms' then
			f = '%H:%M:%S'
			need_time = false
		elseif item == 'ymd' then
			f = '%Y-%m-%d %{era}'
		elseif item == 'mdy' then
			f = '%B %-d, %-Y %{era}'
		elseif item == 'dmy' then
			f = '%-d %B %-Y %{era}'
		else
			return bad_format()
		end
		t:add(f)
	end
	fmt = t:join(' ')
	if need_time then
		fmt = hm_fmt() .. ' ' .. fmt
	end
	return strftime(date, fmt, options)
end

local day_info = {
	-- 0=Sun to 6=Sat
	[0] = { 'Sun', 'Sunday' },
	{ 'Mon', 'Monday' },
	{ 'Tue', 'Tuesday' },
	{ 'Wed', 'Wednesday' },
	{ 'Thu', 'Thursday' },
	{ 'Fri', 'Friday' },
	{ 'Sat', 'Saturday' },
}

local month_info = {
	-- 1=Jan to 12=Dec
	{ 'Jan', 'January' },
	{ 'Feb', 'February' },
	{ 'Mar', 'March' },
	{ 'Apr', 'April' },
	{ 'May', 'May' },
	{ 'Jun', 'June' },
	{ 'Jul', 'July' },
	{ 'Aug', 'August' },
	{ 'Sep', 'September' },
	{ 'Oct', 'October' },
	{ 'Nov', 'November' },
	{ 'Dec', 'December' },
}

local function name_to_number(text, translate)
	if type(text) == 'string' then
		return translate[text:lower()]
	end
end

local function day_number(text)
	return name_to_number(text, {
		sun = 0, sunday = 0,
		mon = 1, monday = 1,
		tue = 2, tuesday = 2,
		wed = 3, wednesday = 3,
		thu = 4, thursday = 4,
		fri = 5, friday = 5,
		sat = 6, saturday = 6,
	})
end

local function month_number(text)
	return name_to_number(text, {
		jan = 1, january = 1,
		feb = 2, february = 2,
		mar = 3, march = 3,
		apr = 4, april = 4,
		may = 5,
		jun = 6, june = 6,
		jul = 7, july = 7,
		aug = 8, august = 8,
		sep = 9, september = 9, sept = 9,
		oct = 10, october = 10,
		nov = 11, november = 11,
		dec = 12, december = 12,
	})
end

local function _list_text(list, fmt)
	-- Return a list of formatted strings from a list of dates.
	if not type(list) == 'table' then
		error('date:list:text: need "list:text()" with a colon', 2)
	end
	local result = { join = _list_join }
	for i, date in ipairs(list) do
		result[i] = date:text(fmt)
	end
	return result
end

local function _date_list(date, spec)
	-- Return a possibly empty numbered table of dates meeting the specification.
	-- Dates in the list are in ascending order (oldest date first).
	-- The spec should be a string of form "<count> <day> <op>"
	-- where each item is optional and
	--   count = number of items wanted in list
	--   day = abbreviation or name such as Mon or Monday
	--   op = >, >=, <, <= (default is > meaning after date)
	-- If no count is given, the list is for the specified days in date's month.
	-- The default day is date's day.
	-- The spec can also be a positive or negative number:
	--   -5 is equivalent to '5 <'
	--   5  is equivalent to '5' which is '5 >'
	if not is_date(date) then
		error('date:list: need a date (use "date:list()" with a colon)', 2)
	end
	local list = { text = _list_text }
	if date.partial then
		return list
	end
	local count, offset, operation
	local ops = {
		['>='] = { before = false, include = true  },
		['>']  = { before = false, include = false },
		['<='] = { before = true , include = true  },
		['<']  = { before = true , include = false },
	}
	if spec then
		if type(spec) == 'number' then
			count = floor(spec + 0.5)
			if count < 0 then
				count = -count
				operation = ops['<']
			end
		elseif type(spec) == 'string' then
			local num, day, op = spec:match('^%s*(%d*)%s*(%a*)%s*([<>=]*)%s*$')
			if not num then
				return list
			end
			if num ~= '' then
				count = tonumber(num)
			end
			if day ~= '' then
				local dow = day_number(day:gsub('[sS]$', ''))  -- accept plural days
				if not dow then
					return list
				end
				offset = dow - date.dow
			end
			operation = ops[op]
		else
			return list
		end
	end
	offset = offset or 0
	operation = operation or ops['>']
	local datefrom, dayfirst, daylast
	if operation.before then
		if offset > 0 or (offset == 0 and not operation.include) then
			offset = offset - 7
		end
		if count then
			if count > 1 then
				offset = offset - 7*(count - 1)
			end
			datefrom = date + offset
		else
			daylast = date.day + offset
			dayfirst = daylast % 7
			if dayfirst == 0 then
				dayfirst = 7
			end
		end
	else
		if offset < 0 or (offset == 0 and not operation.include) then
			offset = offset + 7
		end
		if count then
			datefrom = date + offset
		else
			dayfirst = date.day + offset
			daylast = date.monthdays
		end
	end
	if not count then
		if daylast < dayfirst then
			return list
		end
		count = floor((daylast - dayfirst)/7) + 1
		datefrom = Date(date, {day = dayfirst})
	end
	for i = 1, count do
		if not datefrom then break end  -- exceeds date limits
		list[i] = datefrom
		datefrom = datefrom + 7
	end
	return list
end

-- A table to get the current date/time (UTC), but only if needed.
local current = setmetatable({}, {
	__index = function (self, key)
		local d = os.date('!*t')
		self.year = d.year
		self.month = d.month
		self.day = d.day
		self.hour = d.hour
		self.minute = d.min
		self.second = d.sec
		return rawget(self, key)
	end })

local function extract_date(newdate, text)
	-- Parse the date/time in text and return n, o where
	--   n = table of numbers with date/time fields
	--   o = table of options for AM/PM or AD/BC or format, if any
	-- or return nothing if date is known to be invalid.
	-- Caller determines if the values in n are valid.
	-- A year must be positive ('1' to '9999'); use 'BC' for BC.
	-- In a y-m-d string, the year must be four digits to avoid ambiguity
	-- ('0001' to '9999'). The only way to enter year <= 0 is by specifying
	-- the date as three numeric parameters like ymd Date(-1, 1, 1).
	-- Dates of form d/m/y, m/d/y, y/m/d are rejected as potentially ambiguous.
	local date, options = {}, {}
	if text:sub(-1) == 'Z' then
		-- Extract date/time from a Wikidata timestamp.
		-- The year can be 1 to 16 digits but this module handles 1 to 4 digits only.
		-- Examples: '+2016-06-21T14:30:00Z', '-0000000180-00-00T00:00:00Z'.
		local sign, y, m, d, H, M, S = text:match('^([+%-])(%d+)%-(%d%d)%-(%d%d)T(%d%d):(%d%d):(%d%d)Z$')
		if sign then
			y = tonumber(y)
			if sign == '-' and y > 0 then
				y = -y
			end
			if y <= 0 then
				options.era = 'BCE'
			end
			date.year = y
			m = tonumber(m)
			d = tonumber(d)
			H = tonumber(H)
			M = tonumber(M)
			S = tonumber(S)
			if m == 0 then
				newdate.partial = true
				return date, options
			end
			date.month = m
			if d == 0 then
				newdate.partial = true
				return date, options
			end
			date.day = d
			if H > 0 or M > 0 or S > 0 then
				date.hour = H
				date.minute = M
				date.second = S
			end
			return date, options
		end
		return
	end
	local function extract_ymd(item)
		-- Called when no day or month has been set.
		local y, m, d = item:match('^(%d%d%d%d)%-(%w+)%-(%d%d?)$')
		if y then
			if date.year then
				return
			end
			if m:match('^%d%d?$') then
				m = tonumber(m)
			else
				m = month_number(m)
			end
			if m then
				date.year = tonumber(y)
				date.month = m
				date.day = tonumber(d)
				return true
			end
		end
	end
	local function extract_day_or_year(item)
		-- Called when a day would be valid, or
		-- when a year would be valid if no year has been set and partial is set.
		local number, suffix = item:match('^(%d%d?%d?%d?)(.*)$')
		if number then
			local n = tonumber(number)
			if #number <= 2 and n <= 31 then
				suffix = suffix:lower()
				if suffix == '' or suffix == 'st' or suffix == 'nd' or suffix == 'rd' or suffix == 'th' then
					date.day = n
					return true
				end
			elseif suffix == '' and newdate.partial and not date.year then
				date.year = n
				return true
			end
		end
	end
	local function extract_month(item)
		-- A month must be given as a name or abbreviation; a number could be ambiguous.
		local m = month_number(item)
		if m then
			date.month = m
			return true
		end
	end
	local function extract_time(item)
		local h, m, s = item:match('^(%d%d?):(%d%d)(:?%d*)$')
		if date.hour or not h then
			return
		end
		if s ~= '' then
			s = s:match('^:(%d%d)$')
			if not s then
				return
			end
		end
		date.hour = tonumber(h)
		date.minute = tonumber(m)
		date.second = tonumber(s)  -- nil if empty string
		return true
	end
	local item_count = 0
	local index_time
	local function set_ampm(item)
		local H = date.hour
		if H and not options.am and index_time + 1 == item_count then
			options.am = ampm_options[item]  -- caller checked this is not nil
			if item:match('^[Aa]') then
				if not (1 <= H and H <= 12) then
					return
				end
				if H == 12 then
					date.hour = 0
				end
			else
				if not (1 <= H and H <= 23) then
					return
				end
				if H <= 11 then
					date.hour = H + 12
				end
			end
			return true
		end
	end
	for item in text:gsub(',', ' '):gsub(' ', ' '):gmatch('%S+') do
		item_count = item_count + 1
		if era_text[item] then
			-- Era is accepted in peculiar places.
			if options.era then
				return
			end
			options.era = item
		elseif ampm_options[item] then
			if not set_ampm(item) then
				return
			end
		elseif item:find(':', 1, true) then
			if not extract_time(item) then
				return
			end
			index_time = item_count
		elseif date.day and date.month then
			if date.year then
				return  -- should be nothing more so item is invalid
			end
			if not item:match('^(%d%d?%d?%d?)$') then
				return
			end
			date.year = tonumber(item)
		elseif date.day then
			if not extract_month(item) then
				return
			end
		elseif date.month then
			if not extract_day_or_year(item) then
				return
			end
		elseif extract_month(item) then
			options.format = 'mdy'
		elseif extract_ymd(item) then
			options.format = 'ymd'
		elseif extract_day_or_year(item) then
			if date.day then
				options.format = 'dmy'
			end
		else
			return
		end
	end
	if not date.year or date.year == 0 then
		return
	end
	local era = era_text[options.era]
	if era and era.isbc then
		date.year = 1 - date.year
	end
	return date, options
end

local function autofill(date1, date2)
	-- Fill any missing month or day in each date using the
	-- corresponding component from the other date, if present,
	-- or with 1 if both dates are missing the month or day.
	-- This gives a good result for calculating the difference
	-- between two partial dates when no range is wanted.
	-- Return filled date1, date2 (two full dates).
	local function filled(a, b)
		local fillmonth, fillday
		if not a.month then
			fillmonth = b.month or 1
		end
		if not a.day then
			fillday = b.day or 1
		end
		if fillmonth or fillday then  -- need to create a new date
			a = Date(a, { month = fillmonth, day = fillday })
		end
		return a
	end
	return filled(date1, date2), filled(date2, date1)
end

local function date_add_sub(lhs, rhs, is_sub)
	-- Return a new date from calculating (lhs + rhs) or (lhs - rhs),
	-- or return nothing if invalid.
	-- The result is nil if the calculated date exceeds allowable limits.
	-- Caller ensures that lhs is a date; its properties are copied for the new date.
	if lhs.partial then
		-- Adding to a partial is not supported.
		-- Can subtract a date or partial from a partial, but this is not called for that.
		return
	end
	local function is_prefix(text, word, minlen)
		local n = #text
		return (minlen or 1) <= n and n <= #word and text == word:sub(1, n)
	end
	local function do_days(n)
		local forcetime, jd
		if floor(n) == n then
			jd = lhs.jd
		else
			forcetime = not lhs.hastime
			jd = lhs.jdz
		end
		jd = jd + (is_sub and -n or n)
		if forcetime then
			jd = tostring(jd)
			if not jd:find('.', 1, true) then
				jd = jd .. '.0'
			end
		end
		return Date(lhs, 'juliandate', jd)
	end
	if type(rhs) == 'number' then
		-- Add/subtract days, including fractional days.
		return do_days(rhs)
	end
	if type(rhs) == 'string' then
		-- rhs is a single component like '26m' or '26 months' (with optional sign).
		-- Fractions like '3.25d' are accepted for the units which are handled as days.
		local sign, numstr, id = rhs:match('^%s*([+-]?)([%d%.]+)%s*(%a+)$')
		if sign then
			if sign == '-' then
				is_sub = not (is_sub and true or false)
			end
			local y, m, days
			local num = tonumber(numstr)
			if not num then
				return
			end
			id = id:lower()
			if is_prefix(id, 'years') then
				y = num
				m = 0
			elseif is_prefix(id, 'months') then
				y = floor(num / 12)
				m = num % 12
			elseif is_prefix(id, 'weeks') then
				days = num * 7
			elseif is_prefix(id, 'days') then
				days = num
			elseif is_prefix(id, 'hours') then
				days = num / 24
			elseif is_prefix(id, 'minutes', 3) then
				days = num / (24 * 60)
			elseif is_prefix(id, 'seconds') then
				days = num / (24 * 3600)
			else
				return
			end
			if days then
				return do_days(days)
			end
			if numstr:find('.', 1, true) then
				return
			end
			if is_sub then
				y = -y
				m = -m
			end
			assert(-11 <= m and m <= 11)
			y = lhs.year + y
			m = lhs.month + m
			if m > 12 then
				y = y + 1
				m = m - 12
			elseif m < 1 then
				y = y - 1
				m = m + 12
			end
			local d = math.min(lhs.day, days_in_month(y, m, lhs.calendar))
			return Date(lhs, y, m, d)
		end
	end
	if is_diff(rhs) then
		local days = rhs.age_days
		if (is_sub or false) ~= (rhs.isnegative or false) then
			days = -days
		end
		return lhs + days
	end
end

local full_date_only = {
	dayabbr = true,
	dayname = true,
	dow = true,
	dayofweek = true,
	dowiso = true,
	dayofweekiso = true,
	dayofyear = true,
	gsd = true,
	juliandate = true,
	jd = true,
	jdz = true,
	jdnoon = true,
}

-- Metatable for a date's calculated fields.
local datemt = {
	__index = function (self, key)
		if rawget(self, 'partial') then
			if full_date_only[key] then return end
			if key == 'monthabbr' or key == 'monthdays' or key == 'monthname' then
				if not self.month then return end
			end
		end
		local value
		if key == 'dayabbr' then
			value = day_info[self.dow][1]
		elseif key == 'dayname' then
			value = day_info[self.dow][2]
		elseif key == 'dow' then
			value = (self.jdnoon + 1) % 7  -- day-of-week 0=Sun to 6=Sat
		elseif key == 'dayofweek' then
			value = self.dow
		elseif key == 'dowiso' then
			value = (self.jdnoon % 7) + 1  -- ISO day-of-week 1=Mon to 7=Sun
		elseif key == 'dayofweekiso' then
			value = self.dowiso
		elseif key == 'dayofyear' then
			local first = Date(self.year, 1, 1, self.calendar).jdnoon
			value = self.jdnoon - first + 1  -- day-of-year 1 to 366
		elseif key == 'era' then
			-- Era text (never a negative sign) from year and options.
			value = get_era_for_year(self.options.era, self.year)
		elseif key == 'format' then
			value = self.options.format or 'dmy'
		elseif key == 'gsd' then
			-- GSD = 1 from 00:00:00 to 23:59:59 on 1 January 1 AD Gregorian calendar,
			-- which is from jd 1721425.5 to 1721426.49999.
			value = floor(self.jd - 1721424.5)
		elseif key == 'juliandate' or key == 'jd' or key == 'jdz' then
			local jd, jdz = julian_date(self)
			rawset(self, 'juliandate', jd)
			rawset(self, 'jd', jd)
			rawset(self, 'jdz', jdz)
			return key == 'jdz' and jdz or jd
		elseif key == 'jdnoon' then
			-- Julian date at noon (an integer) on the calendar day when jd occurs.
			value = floor(self.jd + 0.5)
		elseif key == 'isleapyear' then
			value = is_leap_year(self.year, self.calendar)
		elseif key == 'monthabbr' then
			value = month_info[self.month][1]
		elseif key == 'monthdays' then
			value = days_in_month(self.year, self.month, self.calendar)
		elseif key == 'monthname' then
			value = month_info[self.month][2]
		end
		if value ~= nil then
			rawset(self, key, value)
			return value
		end
	end,
}

-- Date operators.
local function mt_date_add(lhs, rhs)
	if not is_date(lhs) then
		lhs, rhs = rhs, lhs  -- put date on left (it must be a date for this to have been called)
	end
	return date_add_sub(lhs, rhs)
end

local function mt_date_sub(lhs, rhs)
	if is_date(lhs) then
		if is_date(rhs) then
			return DateDiff(lhs, rhs)
		end
		return date_add_sub(lhs, rhs, true)
	end
end

local function mt_date_concat(lhs, rhs)
	return tostring(lhs) .. tostring(rhs)
end

local function mt_date_tostring(self)
	return self:text()
end

local function mt_date_eq(lhs, rhs)
	-- Return true if dates identify same date/time where, for example,
	-- Date(-4712, 1, 1, 'Julian') == Date(-4713, 11, 24, 'Gregorian') is true.
	-- This is called only if lhs and rhs have the same type and the same metamethod.
	if lhs.partial or rhs.partial then
		-- One date is partial; the other is a partial or a full date.
		-- The months may both be nil, but must be the same.
		return lhs.year == rhs.year and lhs.month == rhs.month and lhs.calendar == rhs.calendar
	end
	return lhs.jdz == rhs.jdz
end

local function mt_date_lt(lhs, rhs)
	-- Return true if lhs < rhs, for example,
	-- Date('1 Jan 2016') < Date('06:00 1 Jan 2016') is true.
	-- This is called only if lhs and rhs have the same type and the same metamethod.
	if lhs.partial or rhs.partial then
		-- One date is partial; the other is a partial or a full date.
		if lhs.calendar ~= rhs.calendar then
			return lhs.calendar == 'Julian'
		end
		if lhs.partial then
			lhs = lhs.partial.first
		end
		if rhs.partial then
			rhs = rhs.partial.first
		end
	end
	return lhs.jdz < rhs.jdz
end

--[[ Examples of syntax to construct a date:
Date(y, m, d, 'julian')             default calendar is 'gregorian'
Date(y, m, d, H, M, S, 'julian')
Date('juliandate', jd, 'julian')    if jd contains "." text output includes H:M:S
Date('currentdate')
Date('currentdatetime')
Date('1 April 1995', 'julian')      parse date from text
Date('1 April 1995 AD', 'julian')   using an era sets a flag to do the same for output
Date('04:30:59 1 April 1995', 'julian')
Date(date)                          copy of an existing date
Date(date, t)                       same, updated with y,m,d,H,M,S fields from table t
Date(t)                       		date with y,m,d,H,M,S fields from table t
]]
function Date(...)  -- for forward declaration above
	-- Return a table holding a date assuming a uniform calendar always applies
	-- (proleptic Gregorian calendar or proleptic Julian calendar), or
	-- return nothing if date is invalid.
	-- A partial date has a valid year, however its month may be nil, and
	-- its day and time fields are nil.
	-- Field partial is set to false (if a full date) or a table (if a partial date).
	local calendars = { julian = 'Julian', gregorian = 'Gregorian' }
	local newdate = {
		_id = uniq,
		calendar = 'Gregorian',  -- default is Gregorian calendar
		hastime = false,  -- true if input sets a time
		hour = 0,  -- always set hour/minute/second so don't have to handle nil
		minute = 0,
		second = 0,
		options = {},
		list = _date_list,
		subtract = function (self, rhs, options)
			return DateDiff(self, rhs, options)
		end,
		text = _date_text,
	}
	local argtype, datetext, is_copy, jd_number, tnums
	local numindex = 0
	local numfields = { 'year', 'month', 'day', 'hour', 'minute', 'second' }
	local numbers = {}
	for _, v in ipairs({...}) do
		v = strip_to_nil(v)
		local vlower = type(v) == 'string' and v:lower() or nil
		if v == nil then
			-- Ignore empty arguments after stripping so modules can directly pass template parameters.
		elseif calendars[vlower] then
			newdate.calendar = calendars[vlower]
		elseif vlower == 'partial' then
			newdate.partial = true
		elseif vlower == 'fix' then
			newdate.want_fix = true
		elseif is_date(v) then
			-- Copy existing date (items can be overridden by other arguments).
			if is_copy or tnums then
				return
			end
			is_copy = true
			newdate.calendar = v.calendar
			newdate.partial = v.partial
			newdate.hastime = v.hastime
			newdate.options = v.options
			newdate.year = v.year
			newdate.month = v.month
			newdate.day = v.day
			newdate.hour = v.hour
			newdate.minute = v.minute
			newdate.second = v.second
		elseif type(v) == 'table' then
			if tnums then
				return
			end
			tnums = {}
			local tfields = { year=1, month=1, day=1, hour=2, minute=2, second=2 }
			for tk, tv in pairs(v) do
				if tfields[tk] then
					tnums[tk] = tonumber(tv)
				end
				if tfields[tk] == 2 then
					newdate.hastime = true
				end
			end
		else
			local num = tonumber(v)
			if not num and argtype == 'setdate' and numindex == 1 then
				num = month_number(v)
			end
			if num then
				if not argtype then
					argtype = 'setdate'
				end
				if argtype == 'setdate' and numindex < 6 then
					numindex = numindex + 1
					numbers[numfields[numindex]] = num
				elseif argtype == 'juliandate' and not jd_number then
					jd_number = num
					if type(v) == 'string' then
						if v:find('.', 1, true) then
							newdate.hastime = true
						end
					elseif num ~= floor(num) then
						-- The given value was a number. The time will be used
						-- if the fractional part is nonzero.
						newdate.hastime = true
					end
				else
					return
				end
			elseif argtype then
				return
			elseif type(v) == 'string' then
				if v == 'currentdate' or v == 'currentdatetime' or v == 'juliandate' then
					argtype = v
				else
					argtype = 'datetext'
					datetext = v
				end
			else
				return
			end
		end
	end
	if argtype == 'datetext' then
		if tnums or not set_date_from_numbers(newdate, extract_date(newdate, datetext)) then
			return
		end
	elseif argtype == 'juliandate' then
		newdate.partial = nil
		newdate.jd = jd_number
		if not set_date_from_jd(newdate) then
			return
		end
	elseif argtype == 'currentdate' or argtype == 'currentdatetime' then
		newdate.partial = nil
		newdate.year = current.year
		newdate.month = current.month
		newdate.day = current.day
		if argtype == 'currentdatetime' then
			newdate.hour = current.hour
			newdate.minute = current.minute
			newdate.second = current.second
			newdate.hastime = true
		end
		newdate.calendar = 'Gregorian'  -- ignore any given calendar name
	elseif argtype == 'setdate' then
		if tnums or not set_date_from_numbers(newdate, numbers) then
			return
		end
	elseif not (is_copy or tnums) then
		return
	end
	if tnums then
		newdate.jd = nil  -- force recalculation in case jd was set before changes from tnums
		if not set_date_from_numbers(newdate, tnums) then
			return
		end
	end
	if newdate.partial then
		local year = newdate.year
		local month = newdate.month
		local first = Date(year, month or 1, 1, newdate.calendar)
		month = month or 12
		local last = Date(year, month, days_in_month(year, month), newdate.calendar)
		newdate.partial = { first = first, last = last }
	else
		newdate.partial = false  -- avoid index lookup
	end
	setmetatable(newdate, datemt)
	local readonly = {}
	local mt = {
		__index = newdate,
		__newindex = function(t, k, v) error('date.' .. tostring(k) .. ' is read-only', 2) end,
		__add = mt_date_add,
		__sub = mt_date_sub,
		__concat = mt_date_concat,
		__tostring = mt_date_tostring,
		__eq = mt_date_eq,
		__lt = mt_date_lt,
	}
	return setmetatable(readonly, mt)
end

local function _diff_age(diff, code, options)
	-- Return a tuple of integer values from diff as specified by code, except that
	-- each integer may be a list of two integers for a diff with a partial date, or
	-- return nil if the code is not supported.
	-- If want round, the least significant unit is rounded to nearest whole unit.
	-- For a duration, an extra day is added.
	local wantround, wantduration, wantrange
	if type(options) == 'table' then
		wantround = options.round
		wantduration = options.duration
		wantrange = options.range
	else
		wantround = options
	end
	if not is_diff(diff) then
		local f = wantduration and 'duration' or 'age'
		error(f .. ': need a date difference (use "diff:' .. f .. '()" with a colon)', 2)
	end
	if diff.partial then
		-- Ignore wantround, wantduration.
		local function choose(v)
			if type(v) == 'table' then
				if not wantrange or v[1] == v[2] then
					-- Example: Date('partial', 2005) - Date('partial', 2001) gives
					-- diff.years = { 3, 4 } to show the range of possible results.
					-- If do not want a range, choose the second value as more expected.
					return v[2]
				end
			end
			return v
		end
		if code == 'ym' or code == 'ymd' then
			if not wantrange and diff.iszero then
				-- This avoids an unexpected result such as
				-- Date('partial', 2001) - Date('partial', 2001)
				-- giving diff = { years = 0, months = { 0, 11 } }
				-- which would be reported as 0 years and 11 months.
				return 0, 0
			end
			return choose(diff.partial.years), choose(diff.partial.months)
		end
		if code == 'y' then
			return choose(diff.partial.years)
		end
		if code == 'm' or code == 'w' or code == 'd' then
			return choose({ diff.partial.mindiff:age(code), diff.partial.maxdiff:age(code) })
		end
		return nil
	end
	local extra_days = wantduration and 1 or 0
	if code == 'wd' or code == 'w' or code == 'd' then
		local offset = wantround and 0.5 or 0
		local days = diff.age_days + extra_days
		if code == 'wd' or code == 'd' then
			days = floor(days + offset)
			if code == 'd' then
				return days
			end
			return floor(days/7), days % 7
		end
		return floor(days/7 + offset)
	end
	local H, M, S = diff.hours, diff.minutes, diff.seconds
	if code == 'dh' or code == 'dhm' or code == 'dhms' or code == 'h' or code == 'hm' or code == 'hms' then
		local days = floor(diff.age_days + extra_days)
		local inc_hour
		if wantround then
			if code == 'dh' or code == 'h' then
				if M >= 30 then
					inc_hour = true
				end
			elseif code == 'dhm' or code == 'hm' then
				if S >= 30 then
					M = M + 1
					if M >= 60 then
						M = 0
						inc_hour = true
					end
				end
			else
				-- Nothing needed because S is an integer.
			end
			if inc_hour then
				H = H + 1
				if H >= 24 then
					H = 0
					days = days + 1
				end
			end
		end
		if code == 'dh' or code == 'dhm' or code == 'dhms' then
			if code == 'dh' then
				return days, H
			elseif code == 'dhm' then
				return days, H, M
			else
				return days, H, M, S
			end
		end
		local hours = days * 24 + H
		if code == 'h' then
			return hours
		elseif code == 'hm' then
			return hours, M
		end
		return hours, M, S
	end
	if wantround then
		local inc_hour
		if code == 'ymdh' or code == 'ymwdh' then
			if M >= 30 then
				inc_hour = true
			end
		elseif code == 'ymdhm' or code == 'ymwdhm' then
			if S >= 30 then
				M = M + 1
				if M >= 60 then
					M = 0
					inc_hour = true
				end
			end
		elseif code == 'ymd' or code == 'ymwd' or code == 'yd' or code == 'md' then
			if H >= 12 then
				extra_days = extra_days + 1
			end
		end
		if inc_hour then
			H = H + 1
			if H >= 24 then
				H = 0
				extra_days = extra_days + 1
			end
		end
	end
	local y, m, d = diff.years, diff.months, diff.days
	if extra_days > 0 then
		d = d + extra_days
		if d > 28 or code == 'yd' then
			-- Recalculate in case have passed a month.
			diff = diff.date1 + extra_days - diff.date2
			y, m, d = diff.years, diff.months, diff.days
		end
	end
	if code == 'ymd' then
		return y, m, d
	elseif code == 'yd' then
		if y > 0 then
			-- It is known that diff.date1 > diff.date2.
			diff = diff.date1 - (diff.date2 + (y .. 'y'))
		end
		return y, floor(diff.age_days)
	elseif code == 'md' then
		return y * 12 + m, d
	elseif code == 'ym' or code == 'm' then
		if wantround then
			if d >= 16 then
				m = m + 1
				if m >= 12 then
					m = 0
					y = y + 1
				end
			end
		end
		if code == 'ym' then
			return y, m
		end
		return y * 12 + m
	elseif code == 'ymw' then
		local weeks = floor(d/7)
		if wantround then
			local days = d % 7
			if days > 3 or (days == 3 and H >= 12) then
				weeks = weeks + 1
			end
		end
		return y, m, weeks
	elseif code == 'ymwd' then
		return y, m, floor(d/7), d % 7
	elseif code == 'ymdh' then
		return y, m, d, H
	elseif code == 'ymwdh' then
		return y, m, floor(d/7), d % 7, H
	elseif code == 'ymdhm' then
		return y, m, d, H, M
	elseif code == 'ymwdhm' then
		return y, m, floor(d/7), d % 7, H, M
	end
	if code == 'y' then
		if wantround and m >= 6 then
			y = y + 1
		end
		return y
	end
	return nil
end

local function _diff_duration(diff, code, options)
	if type(options) ~= 'table' then
		options = { round = options }
	end
	options.duration = true
	return _diff_age(diff, code, options)
end

-- Metatable for some operations on date differences.
diffmt = {  -- for forward declaration above
	__concat = function (lhs, rhs)
		return tostring(lhs) .. tostring(rhs)
	end,
	__tostring = function (self)
		return tostring(self.age_days)
	end,
	__index = function (self, key)
		local value
		if key == 'age_days' then
			if rawget(self, 'partial') then
				local function jdz(date)
					return (date.partial and date.partial.first or date).jdz
				end
				value = jdz(self.date1) - jdz(self.date2)
			else
				value = self.date1.jdz - self.date2.jdz
			end
		end
		if value ~= nil then
			rawset(self, key, value)
			return value
		end
	end,
}

function DateDiff(date1, date2, options)  -- for forward declaration above
	-- Return a table with the difference between two dates (date1 - date2).
	-- The difference is negative if date1 is older than date2.
	-- Return nothing if invalid.
	-- If d = date1 - date2 then
	--     date1 = date2 + d
	-- If date1 >= date2 and the dates have no H:M:S time specified then
	--     date1 = date2 + (d.years..'y') + (d.months..'m') + d.days
	-- where the larger time units are added first.
	-- The result of Date(2015,1,x) + '1m' is Date(2015,2,28) for
	-- x = 28, 29, 30, 31. That means, for example,
	--     d = Date(2015,3,3) - Date(2015,1,31)
	-- gives d.years, d.months, d.days = 0, 1, 3 (excluding date1).
	if not (is_date(date1) and is_date(date2) and date1.calendar == date2.calendar) then
		return
	end
	local wantfill
	if type(options) == 'table' then
		wantfill = options.fill
	end
	local isnegative = false
	local iszero = false
	if date1 < date2 then
		isnegative = true
		date1, date2 = date2, date1
	elseif date1 == date2 then
		iszero = true
	end
	-- It is known that date1 >= date2 (period is from date2 to date1).
	if date1.partial or date2.partial then
		-- Two partial dates might have timelines:
		---------------------A=================B--- date1 is from A to B inclusive
		--------C=======D-------------------------- date2 is from C to D inclusive
		-- date1 > date2 iff A > C (date1.partial.first > date2.partial.first)
		-- The periods can overlap ('April 2001' - '2001'):
		-------------A===B------------------------- A=2001-04-01  B=2001-04-30
		--------C=====================D------------ C=2001-01-01  D=2001-12-31
		if wantfill then
			date1, date2 = autofill(date1, date2)
		else
			local function zdiff(date1, date2)
				local diff = date1 - date2
				if diff.isnegative then
					return date1 - date1  -- a valid diff in case we call its methods
				end
				return diff
			end
			local function getdate(date, which)
				return date.partial and date.partial[which] or date
			end
			local maxdiff = zdiff(getdate(date1, 'last'), getdate(date2, 'first'))
			local mindiff = zdiff(getdate(date1, 'first'), getdate(date2, 'last'))
			local years, months
			if maxdiff.years == mindiff.years then
				years = maxdiff.years
				if maxdiff.months == mindiff.months then
					months = maxdiff.months
				else
					months = { mindiff.months, maxdiff.months }
				end
			else
				years = { mindiff.years, maxdiff.years }
			end
			return setmetatable({
				date1 = date1,
				date2 = date2,
				partial = {
					years = years,
					months = months,
					maxdiff = maxdiff,
					mindiff = mindiff,
				},
				isnegative = isnegative,
				iszero = iszero,
				age = _diff_age,
				duration = _diff_duration,
			}, diffmt)
		end
	end
	local y1, m1 = date1.year, date1.month
	local y2, m2 = date2.year, date2.month
	local years = y1 - y2
	local months = m1 - m2
	local d1 = date1.day + hms(date1)
	local d2 = date2.day + hms(date2)
	local days, time
	if d1 >= d2 then
		days = d1 - d2
	else
		months = months - 1
		-- Get days in previous month (before the "to" date) given December has 31 days.
		local dpm = m1 > 1 and days_in_month(y1, m1 - 1, date1.calendar) or 31
		if d2 >= dpm then
			days = d1 - hms(date2)
		else
			days = dpm - d2 + d1
		end
	end
	if months < 0 then
		years = years - 1
		months = months + 12
	end
	days, time = math.modf(days)
	local H, M, S = h_m_s(time)
	return setmetatable({
		date1 = date1,
		date2 = date2,
		partial = false,  -- avoid index lookup
		years = years,
		months = months,
		days = days,
		hours = H,
		minutes = M,
		seconds = S,
		isnegative = isnegative,
		iszero = iszero,
		age = _diff_age,
		duration = _diff_duration,
	}, diffmt)
end

return {
	_current = current,
	_Date = Date,
	_days_in_month = days_in_month,
}