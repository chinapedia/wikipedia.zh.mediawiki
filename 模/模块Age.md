-- Implement various "age of" and other date-related templates.

local _Date, _currentDate
local function getExports(frame)
	-- Return objects exported from the date module or its sandbox.
	if not _Date then
		local sandbox = frame:getTitle():find('sandbox', 1, true) and '/sandbox' or ''
		local datemod = require('Module:Date' .. sandbox)
		_Date = datemod._Date
		_currentDate = datemod._current
	end
	return _Date, _currentDate
end

local Collection  -- a table to hold items
Collection = {
	add = function (self, item)
		if item ~= nil then
			self.n = self.n + 1
			self[self.n] = item
		end
	end,
	join = function (self, sep)
		return table.concat(self, sep)
	end,
	remove = function (self, pos)
		if self.n > 0 and (pos == nil or (0 < pos and pos <= self.n)) then
			self.n = self.n - 1
			return table.remove(self, pos)
		end
	end,
	sort = function (self, comp)
		table.sort(self, comp)
	end,
	new = function ()
		return setmetatable({n = 0}, Collection)
	end
}
Collection.__index = Collection

local function stripToNil(text)
	-- If text is a string, return its trimmed content, or nil if empty.
	-- Otherwise return text (which may, for example, be nil).
	if type(text) == 'string' then
		text = text:match('(%S.-)%s*$')
	end
	return text
end

local yes = require('Module:Yesno')

local function message(msg, id)
	-- Return formatted message text for an error or warning.
	local categories = {
		error = '[[Category:Age模块错误|Category:Age模块错误]]',
		warning = '[[Category:Age模块错误|Category:Age模块错误]]',  -- same as error until determine whether 'Age warning' would be worthwhile
	}
	local a, b, category
	if id == 'warning' then
		a = '<sup>[<i>'
		b = '</i>]</sup>'
	else
		a = '<strong class="error">错误：'
		b = '</strong>'
	end
	if mw.title.getCurrentTitle():inNamespaces(0) then
		-- Category only in namespaces: 0=article.
		category = categories[id or 'error']
	end
	return
		a ..
		mw.text.nowiki(msg) ..
		b ..
		(category or '')
end

local function formatNumber(number)
	-- Return the given number formatted with commas as group separators,
	-- given that the number is an integer.
	local numstr = tostring(number)
	local length = #numstr
	local places = Collection.new()
	local pos = 0
	repeat
		places:add(pos)
		pos = pos + 3
	until pos >= length
	places:add(length)
	local groups = Collection.new()
	for i = places.n, 2, -1 do
		local p1 = length - places[i] + 1
		local p2 = length - places[i - 1]
		groups:add(numstr:sub(p1, p2))
	end
	return groups:join(',')
end

local function spellNumber(number, options, i)
	-- Return result of spelling number, or
	-- return number (as a string) if cannot spell it.
	-- i == 1 for the first number which can optionally start with an uppercase letter.
	number = tostring(number)
	return require('Module:ConvertNumeric').spell_number(
		number,
		nil,                       -- fraction numerator
		nil,                       -- fraction denominator
		i == 1 and options.upper,  -- true: 'One' instead of 'one'
		not options.us,            -- true: use 'and' between tens/ones etc
		options.adj,               -- true: hyphenated
		options.ordinal            -- true: 'first' instead of 'one'
	) or number
end

local function makeSort(value, sortable)
	-- Return a sort key if requested.
	-- Assume value is a valid number which has not overflowed.
	if sortable == 'sortable_table' or sortable == 'sortable_on' or sortable == 'sortable_debug' then
		local sortkey
		if value == 0 then
			sortkey = '5000000000000000000'
		else
			local mag = math.floor(math.log10(math.abs(value)) + 1e-14)
			local prefix
			if value > 0 then
				prefix = 7000 + mag
			else
				prefix = 2999 - mag
				value = value + 10^(mag+1)
			end
			sortkey = string.format('%d', prefix) .. string.format('%015.0f', math.floor(value * 10^(14-mag)))
		end
		local lhs, rhs
		if sortable == 'sortable_table' then
			lhs = 'data-sort-value="'
			rhs = '"|'
		else
			lhs = sortable == 'sortable_debug' and
				'<span style="border:1px solid;display:inline;" class="sortkey">' or
				'<span style="display:none" class="sortkey">'
			rhs = '♠</span>'
		end
		return lhs .. sortkey .. rhs
	end
end

local translateParameters = {
	abbr = {
		off = 'abbr_off',
		on = 'abbr_on',
	},
	disp = {
		age = 'disp_age',
		raw = 'disp_raw',
	},
	format = {
		raw = 'format_raw',
		commas = 'format_commas',
	},
	round = {
		on = 'on',
		yes = 'on',
		months = 'ym',
		weeks = 'ymw',
		days = 'ymd',
		hours = 'ymdh',
	},
	sep = {
		comma = 'sep_comma',
		[','] = 'sep_comma',
		serialcomma = 'sep_serialcomma',
		space = 'sep_space',
	},
	show = {
		hide = { id = 'hide' },
		y = { 'y', id = 'y' },
		ym = { 'y', 'm', id = 'ym' },
		ymd = { 'y', 'm', 'd', id = 'ymd' },
		ymw = { 'y', 'm', 'w', id = 'ymw' },
		ymwd = { 'y', 'm', 'w', 'd', id = 'ymwd' },
		yd = { 'y', 'd', id = 'yd', keepZero = true },
		m = { 'm', id = 'm' },
		md = { 'm', 'd', id = 'md' },
		w = { 'w', id = 'w' },
		wd = { 'w', 'd', id = 'wd' },
		h = { 'H', id = 'h' },
		hm = { 'H', 'M', id = 'hm' },
		hms = { 'H', 'M', 'S', id = 'hms' },
		d = { 'd', id = 'd' },
		dh = { 'd', 'H', id = 'dh' },
		dhm = { 'd', 'H', 'M', id = 'dhm' },
		dhms = { 'd', 'H', 'M', 'S', id = 'dhms' },
		ymdh = { 'y', 'm', 'd', 'H', id = 'ymdh' },
		ymdhm = { 'y', 'm', 'd', 'H', 'M', id = 'ymdhm' },
		ymwdh = { 'y', 'm', 'w', 'd', 'H', id = 'ymwdh' },
		ymwdhm = { 'y', 'm', 'w', 'd', 'H', 'M', id = 'ymwdhm' },
	},
	sortable = {
		off = false,
		on = 'sortable_on',
		table = 'sortable_table',
		debug = 'sortable_debug',
	},
}

local spellOptions = {
	cardinal = {},
	Cardinal = { upper = true },
	cardinal_us = { us = true },
	Cardinal_us = { us = true, upper = true },
	ordinal = { ordinal = true },
	Ordinal = { ordinal = true, upper = true },
	ordinal_us = { ordinal = true, us = true },
	Ordinal_us = { ordinal = true, us = true, upper = true },
}

local function dateExtract(frame)
	-- Return part of a date after performing an optional operation.
	local Date = getExports(frame)
	local args = frame:getParent().args
	local parms = {}
	for i, v in ipairs(args) do
		parms[i] = v
	end
	if yes(args.fix) then
		table.insert(parms, 'fix')
	end
	if yes(args.partial) then
		table.insert(parms, 'partial')
	end
	local show = stripToNil(args.show) or 'dmy'
	local date = Date(unpack(parms))
	if not date then
		if show == 'format' then
			return 'error'
		end
		return message('需要有效的日期')
	end
	local add = stripToNil(args.add)
	if add then
		for item in add:gmatch('%S+') do
			date = date + item
			if not date then
				return message('无法添加“' .. item .. '”')
			end
		end
	end
	local prefix, result
	local sortable = translateParameters.sortable[args.sortable]
	if sortable then
		local value = (date.partial and date.partial.first or date).jdz
		prefix = makeSort(value, sortable)
	end
	if show ~= 'hide' then
		result = date[show]
		if result == nil then
			result = date:text(show)
		elseif type(result) == 'boolean' then
			result = result and '1' or '0'
		else
			result = tostring(result)
		end
	end
	return (prefix or '') .. (result or '')
end

local function rangeJoin(range)
	-- Return text to be used between a range of ages.
	return range == 'dash' and '–' or '或'
end

local function makeText(values, components, names, options, noUpper)
	-- Return wikitext representing an age or duration.
	local text = Collection.new()
	local count = #values
	local sep = names.sep or ''
	for i, v in ipairs(values) do
		-- v is a number (say 4 for 4 years), or a table ({4,5} for 4 or 5 years).
		local islist = type(v) == 'table'
		if (islist or v > 0) or (text.n == 0 and i == count) or (text.n > 0 and components.keepZero) then
			local fmt, vstr
			if options.spell then
				fmt = function(number)
					return spellNumber(number, options.spell, noUpper or i)
				end
			elseif i == 1 and options.format == 'format_commas' then
				-- Numbers after the first should be small and not need formatting.
				fmt = formatNumber
			else
				fmt = tostring
			end
			if islist then
				vstr = fmt(v[1]) .. rangeJoin(options.range)
				noUpper = true
				vstr = vstr .. fmt(v[2])
			else
				vstr = fmt(v)
			end
			local name = names[components[i]]
			if name then
				local plural = names.plural
				if not plural or (islist and v[2] or v) == 1 then
					plural = ''
				end
				text:add(vstr .. sep .. name .. plural)
			else
				text:add(vstr)
			end
		end
	end
	local first, last
	-- hh mm ss
	if options.join == 'sep_space' then
		first = ' '
		last = ' '
	-- hh时，mm分，ss秒
	elseif options.join == 'sep_comma' then
		first = '，'
		last = '，'
	-- hh时，mm分又ss秒
	elseif options.join == 'sep_serialcomma' then
		first = '，'
		last = text.n > 2 and (names.y == '年' and '又' or '零') or '，'
	-- hh时mm分ss秒
	elseif options.join == 'sep_none' then
		first = ''
		last = ''
	-- hh时mm分又ss秒
	else  -- 'sep_serial'
		first = ''
		last = text.n > 2 and (names.y == '年' and '又' or '零') or ''
	end
	if yes(options.range, true) and options.join ~= 'sep_space' and string.sub(last, 1, 1) ~= '，' then
		last = '，' .. last
	end
	for i, v in ipairs(text) do
		if i < text.n then
			text[i] = v .. (i + 1 < text.n and first or last)
		end
	end
	local sign = ''
	if options.isnegative then
		-- Do not display negative zero.
		if text.n > 1 or (text.n == 1 and text[1]:sub(1, 1) ~= '0' ) then
			if options.format == 'format_raw' then
				sign = '-'  -- plain hyphen so result can be used in a calculation
			else
				sign = '−'  -- Unicode U+2212 MINUS SIGN
			end
		end
	end
	return
		(options.prefix or '') ..
		(options.extra or '') ..
		sign ..
		text:join() ..
		(options.suffix or '')
end

local function dateDifference(parms)
	-- Return a formatted date difference using the given parameters
	-- which have been validated.
	local names = {
		abbr_off = {
			plural = '',
			sep = '',
			y = '年',
			m = '个月',
			w = '周',
			d = '天',
			H = '小时',
			M = '分',
			S = '秒',
		},
		abbr_on = {
			y = 'y',
			m = 'm',
			w = 'w',
			d = 'd',
			H = 'h',
			M = 'm',
			S = 's',
		},
		abbr_age = {
			plural = '',
			sep = '',
			y = '岁',
			m = '个月',
			w = '周',
			d = '天',
			H = '小时',
			M = '分',
			S = '秒',
		},
		abbr_raw = {},
	}
	local diff = parms.diff  -- must be a valid date difference
	local show = parms.show  -- may be nil; default is set below
	local abbr = parms.abbr or 'abbr_off'
	local defaultJoin  -- 中文应该全为nil
	if abbr ~= 'abbr_off' then
		defaultJoin = nil
	end
	if not show then
		show = 'ymd'
		if parms.disp == 'disp_age' then
			if diff.years < 3 then
				defaultJoin = nil
				if diff.years >= 1 then
					show = 'ym'
				else
					show = 'md'
				end
			else
				show = 'y'
			end
		end
	end
	if type(show) ~= 'table' then
		show = translateParameters.show[show]
	end
	if parms.disp == 'disp_raw' then
		defaultJoin = 'sep_space'
		abbr = 'abbr_raw'
	elseif parms.wantSc then
		defaultJoin = 'sep_serialcomma'
	end
	local diffOptions = {
		round = parms.round,
		duration = parms.wantDuration,
		range = parms.range and true or nil,
	}
	local prefix
	if parms.sortable then
		local value = diff.age_days + (parms.wantDuration and 1 or 0)  -- days and fraction of a day
		if diff.isnegative then
			value = -value
		end
		prefix = makeSort(value, parms.sortable)
	end
	local textOptions = {
		prefix = prefix,
		suffix = parms.suffix,  -- not currently used
		extra = parms.extra,
		format = parms.format,
		join = parms.sep or defaultJoin,
		isnegative = diff.isnegative,
		range = parms.range,
		spell = parms.spell,
	}
	if show.id == 'hide' then
		return prefix or ''
	end
	local values = { diff:age(show.id, diffOptions) }
	if values[1] then
		return makeText(values, show, names[abbr], textOptions)
	end
	if diff.partial then
		-- Handle a more complex range such as
		-- {{age_yd|20 Dec 2001|2003|range=yes}} → 1 year, 12 days or 2 years, 11 days
		local opt = {
			format = textOptions.format,
			join = textOptions.join,
			isnegative = textOptions.isnegative,
			spell = textOptions.spell,
		}
		return
			(textOptions.prefix or '') ..
			makeText({ diff.partial.mindiff:age(show.id, diffOptions) }, show, names[abbr], opt) ..
			rangeJoin(textOptions.range) ..
			makeText({ diff.partial.maxdiff:age(show.id, diffOptions) }, show, names[abbr], opt, true) ..
			(textOptions.suffix or '')
	end
	return message('此处不支持参数show=' .. show.id)
end

local function getDates(frame, getopt)
	-- Parse template parameters and return one of:
	-- * date         (a date table, if single)
	-- * date1, date2 (two date tables, if not single)
	-- * text         (a string error message)
	-- A missing date is optionally replaced with the current date.
	-- If wantMixture is true, a missing date component is replaced
	-- from the current date, so can get a bizarre mixture of
	-- specified/current y/m/d as has been done by some "age" templates.
	-- Some results may be placed in table getopt.
	local Date, currentDate = getExports(frame)
	getopt = getopt or {}
	local function flagCurrent(text)
		-- This allows the calling template to detect if the current date has been used,
		-- that is, whether both dates have been entered in a template expecting two.
		-- For example, an infobox may want the age when an event occurred, not the current age.
		-- Don't bother detecting if wantMixture is used because not needed and it is a poor option.
		if not text then
			text = 'currentdate'
			if getopt.flag == 'usesCurrent' then
				getopt.usesCurrent = true
			end
		end
		return text
	end
	local args = frame:getParent().args
	local fields = {}
	local isNamed = args.year or args.year1 or args.year2 or
		args.month or args.month1 or args.month2 or
		args.day or args.day1 or args.day2
	if isNamed then
		fields[1] = args.year1 or args.year
		fields[2] = args.month1 or args.month
		fields[3] = args.day1 or args.day
		fields[4] = args.year2
		fields[5] = args.month2
		fields[6] = args.day2
	else
		for i = 1, 6 do
			fields[i] = args[i]
		end
	end
	local imax = 0
	for i = 1, 6 do
		fields[i] = stripToNil(fields[i])
		if fields[i] then
			imax = i
		end
		if getopt.omitZero and i % 3 ~= 1 then  -- omit zero months and days as unknown values but keep year 0 which is 1 BCE
			if tonumber(fields[i]) == 0 then
				fields[i] = nil
				getopt.partial = true
			end
		end
	end
	local fix = getopt.fix and 'fix' or ''
	local noDefault = imax == 0 and getopt.noMissing
	local partialText = getopt.partial and 'partial' or ''
	local dates = {}
	if isNamed or imax >= 3 then
		local nrDates = getopt.single and 1 or 2
		if getopt.wantMixture then
			-- Cannot be partial since empty fields are set from current.
			local components = { 'year', 'month', 'day' }
			for i = 1, nrDates * 3 do
				fields[i] = fields[i] or currentDate[components[i > 3 and i - 3 or i]]
			end
			for i = 1, nrDates do
				local index = i == 1 and 1 or 4
				dates[i] = Date(fields[index], fields[index+1], fields[index+2])
			end
		else
			-- If partial dates are allowed, accept
			--     year only, or
			--     year and month only
			-- Do not accept year and day without a month because that makes no sense
			-- (and because, for example, Date('partial', 2001, nil, 12) sets day = nil, not 12).
			for i = 1, nrDates do
				local index = i == 1 and 1 or 4
				local y, m, d = fields[index], fields[index+1], fields[index+2]
				if (getopt.partial and y and (m or not d)) or (y and m and d) then
					dates[i] = Date(fix, partialText, y, m, d)
				elseif not y and not m and not d and not noDefault then
					dates[i] = Date(flagCurrent())
				end
			end
		end
	elseif not noDefault then
		getopt.textdates = true  -- have parsed each date from a single text field
		dates[1] = Date(fix, partialText, flagCurrent(fields[1]))
		if not getopt.single then
			dates[2] = Date(fix, partialText, flagCurrent(fields[2]))
		end
	end
	if not dates[1] then
		return message('需要有效的年月日')
	end
	if getopt.single then
		return dates[1]
	end
	if not dates[2] then
		return message('第二个日期应该是年月日')
	end
	return dates[1], dates[2]
end

local function ageGeneric(frame)
	-- Return the result required by the specified template.
	-- Can use sortable=x where x = on/table/off/debug in any supported template.
	-- Some templates default to sortable=on but can be overridden.
	local name = frame.args.template
	if not name then
		return message('调用它的模板必须有“|template=x”参数，其中x是所需的操作')
	end
	local args = frame:getParent().args
	local specs = {
		-- 重点！切勿随意更改！
		age_days = {                -- {{age in days}}
			show = 'd',
			disp = 'disp_raw',
		},
		age_days_nts = {            -- {{age in days nts}}
			show = 'd',
			disp = 'disp_raw',
			format = 'format_commas',
			sortable = 'on',
		},
		duration_days = {           -- {{duration in days}}
			show = 'd',
			disp = 'disp_raw',
			duration = true,
		},
		duration_days_nts = {       -- {{duration in days nts}}
			show = 'd',
			disp = 'disp_raw',
			format = 'format_commas',
			sortable = 'on',
			duration = true,
		},
		age_full_years = {          -- {{age}}
			show = 'y',
			abbr = 'abbr_raw',
			flag = 'usesCurrent',
			omitZero = true,
			range = 'no',
		},
		age_full_years_nts = {      -- {{age nts}}
			show = 'y',
			abbr = 'abbr_raw',
			format = 'format_commas',
			sortable = 'on',
		},
		age_in_years = {            -- {{age in years}}
			show = 'y',
			abbr = 'abbr_raw',
			negative = 'error',
			range = 'dash',
		},
		age_in_years_nts = {        -- {{age in years nts}}
			show = 'y',
			abbr = 'abbr_raw',
			negative = 'error',
			range = 'dash',
			format = 'format_commas',
			sortable = 'on',
		},
		age_infant = {              -- {{age for infant}}
			-- Do not set show because special processing is done later.
			abbr = 'abbr_off',
			disp = 'disp_age',
			sortable = 'on',
			age = true,
		},
		age_m = {                   -- {{age in months}}
			show = 'm',
			disp = 'disp_raw',
		},
		age_w = {                   -- {{age in weeks}}
			show = 'w',
			disp = 'disp_raw',
		},
		age_wd = {                  -- {{age in weeks and days}}
			show = 'wd',
		},
		age_yd = {                  -- {{age in years and days}}
			show = 'yd',
			format = 'format_commas',
			sep = args.sep == 'and' and 'sep_serialcomma' or nil,
			age = true,
		},
		age_yd_nts = {              -- {{age in years and days nts}}
			show = 'yd',
			format = 'format_commas',
			sep = args.sep == 'and' and 'sep_serialcomma' or nil,
			sortable = 'on',
			age = true,
		},
		age_ym = {                  -- {{age in years and months}}
			show = 'ym',
			sep = args.sep == 'and' and 'sep_serialcomma' or nil,
		},
		age_ymd = {                 -- {{age in years, months and days}}
			show = 'ymd',
		},
		age_ymwd = {                -- {{age in years, months, weeks and days}}
			show = 'ymwd',
			wantMixture = true,
		},
	}
	local spec = specs[name]
	if not spec then
		return message('指定的模板名称无效')
	end
	if name == 'age_days' then
		local su = stripToNil(args['show unit'])
		if su then
			if su == 'abbr' or su == 'full' then
				spec.disp = nil
				spec.abbr = su == 'abbr' and 'abbr_on' or nil
			end
		end
	end
	local partial, autofill
	local range = stripToNil(args.range) or spec.range
	if range then
		-- Suppose partial dates are used and age could be 11 or 12 years.
		-- "|range=" (empty value) has no effect (spec is used).
		-- "|range=yes" or spec.range == true sets range = true (gives "11 or 12")
		-- "|range=dash" or spec.range == 'dash' sets range = 'dash' (gives "11–12").
		-- "|range=no" or spec.range == 'no' sets range = nil and fills each date in the diff (gives "12").
		--     ("on" is equivalent to "yes", and "off" is equivalent to "no").
		-- "|range=OTHER" sets range = nil and rejects partial dates.
		range = ({ dash = 'dash', off = 'no', no = 'no', [true] = true })[range] or yes(range)
		if range then
			partial = true  -- accept partial dates with a possible age range for the result
			if range == 'no' then
				autofill = true  -- missing month/day in first or second date are filled from other date or 1
				range = nil
			end
		end
	end
	local getopt = {
		fix = yes(args.fix),
		flag = stripToNil(args.flag) or spec.flag,
		omitZero = spec.omitZero,
		partial = partial,
		wantMixture = spec.wantMixture,
	}
	local date1, date2 = getDates(frame, getopt)
	if type(date1) == 'string' then
		return date1
	end
	local useAge = spec.age
	if args.age ~= nil then
		useAge = yes(args.age, spec.age)
	end
	local format = stripToNil(args.format)
	local spell = spellOptions[format]
	if format then
		format = 'format_' .. format
	elseif name == 'age_days' and getopt.textdates then
		format = 'format_commas'
	end
	local parms = {
		diff = date2:subtract(date1, { fill = autofill }),
		wantDuration = spec.duration or yes(args.duration),
		range = range,
		wantSc = yes(args.sc),
		show = args.show == 'hide' and 'hide' or spec.show,
		abbr = useAge and 'abbr_age' or spec.abbr,
		disp = spec.disp,
		extra = (getopt.usesCurrent and format ~= 'format_raw') and '<span class="currentage"></span>' or nil,
		format = format or spec.format,
		round = yes(args.round),
		sep = spec.sep,
		sortable = translateParameters.sortable[args.sortable or spec.sortable],
		spell = spell,
	}
	if (spec.negative or frame.args.negative) == 'error' and parms.diff.isnegative then
		return message('第二个日期不应该在第一个日期之前')
	end
	return dateDifference(parms)
end

local function bda(frame)
	-- Implement [[Template:Birth_date_and_age|Template:Birth date and age]].
	local args = frame:getParent().args
	local options = { noMissing=true, single=true }
	local date = getDates(frame, options)
	if type(date) == 'string' then
		return date  -- error text
	end
	local Date = getExports(frame)
	local diff = Date('currentdate') - date
	if diff.isnegative or diff.years > 150 then
		return message('计算年龄所需的出生日期无效')
	end
	local disp, show = 'disp_raw', 'y'
	if diff.years < 2 then
		disp = 'disp_age'
		if diff.years == 0 and diff.months == 0 then
			show = 'd'
		else
			show = 'm'
		end
	end
	local result = '%-Y年%B月%-d日'
	result = '（<span class="bday">%-Y-%m-%d</span>) </span>' .. result
	result = '<span style="display:none"> ' ..
		date:text(result) ..
		'<span class="noprint ForceAgeToShow"> ' ..
		'（' ..
		dateDifference({
			diff = diff,
			show = show,
			abbr = 'abbr_off',
			disp = disp,
			sep = 'sep_space',
		}) ..
		'）</span>'
	local warnings = tonumber(frame.args.warnings)
	if warnings and warnings > 0 then
		local good = {
			df = true,
			mf = true,
			day = true,
			day1 = true,
			month = true,
			month1 = true,
			year = true,
			year1 = true,
		}
		local invalid
		local imax = options.textdates and 1 or 3
		for k, _ in pairs(args) do
			if type(k) == 'number' then
				if k > imax then
					invalid = tostring(k)
					break
				end
			else
				if not good[k] then
					invalid = k
					break
				end
			end
		end
		if invalid then
			result = result .. message(invalid .. '参数无效', 'warning')
		end
	end
	return result
end

local function dateToGsd(frame)
	-- Implement [[Template:Gregorian_serial_date|Template:Gregorian serial date]].
	-- Return Gregorian serial date of the given date, or the current date.
	-- The returned value is negative for dates before 1 January 1 AD
	-- despite the fact that GSD is not defined for such dates.
	local date = getDates(frame, { wantMixture=true, single=true })
	if type(date) == 'string' then
		return date
	end
	return tostring(date.gsd)
end

local function jdToDate(frame)
	-- Return formatted date from a Julian date.
	-- The result includes a time if the input includes a fraction.
	-- The word 'Julian' is accepted for the Julian calendar.
	local Date = getExports(frame)
	local args = frame:getParent().args
	local date = Date('juliandate', args[1], args[2])
	if date then
		return date:text()
	end
	return message('需要有效的儒略历日期')
end

local function dateToJd(frame)
	-- Return Julian date (a number) from a date which may include a time,
	-- or the current date ('currentdate') or current date and time ('currentdatetime').
	-- The word 'Julian' is accepted for the Julian calendar.
	local Date = getExports(frame)
	local args = frame:getParent().args
	local date = Date(args[1], args[2], args[3], args[4], args[5], args[6], args[7])
	if date then
		return tostring(date.jd)
	end
	return message('需要有效的年/月/日或“currentdate”（当前）')
end

local function timeInterval(frame)
	-- Implement [[Template:Time_interval|Template:Time interval]].
	-- There are two positional arguments: date1, date2.
	-- The default for each is the current date and time.
	-- Result is date2 - date1 formatted.
	local Date = getExports(frame)
	local args = frame:getParent().args
	local parms = {
		wantDuration = yes(args.duration),
		range = yes(args.range) or (args.range == 'dash' and 'dash' or nil),
		wantSc = yes(args.sc),
	}
	local fix = yes(args.fix) and 'fix' or ''
	local date1 = Date(fix, 'partial', stripToNil(args[1]) or 'currentdatetime')
	if not date1 then
		return message('第一个参数中的开始日期无效')
	end
	local date2 = Date(fix, 'partial', stripToNil(args[2]) or 'currentdatetime')
	if not date2 then
		return message('第二个参数中的结束日期无效')
	end
	parms.diff = date2 - date1
	for argname, translate in pairs(translateParameters) do
		local parm = stripToNil(args[argname])
		if parm then
			parm = translate[parm]
			if parm == nil then  -- test for nil because false is a valid setting
				return message('参数' .. argname .. '=' .. args[argname] .. '无效')
			end
			parms[argname] = parm
		end
	end
	if parms.round then
		local round = parms.round
		local show = parms.show
		if round ~= 'on' then
			if show then
				if show.id ~= round then
					return message('参数show=' .. args.show .. '与round=' .. args.round .. '冲突')
				end
			else
				parms.show = translateParameters.show[round]
			end
		end
		parms.round = true
	end
	return dateDifference(parms)
end

return {
	age_generic = ageGeneric,           -- can emulate several age templates
	birth_date_and_age = bda,           -- Template:Birth_date_and_age
	gsd = dateToGsd,                    -- Template:Gregorian_serial_date
	extract = dateExtract,              -- Template:Extract
	jd_to_date = jdToDate,              -- Template:?
	JULIANDAY = dateToJd,               -- Template:JULIANDAY
	time_interval = timeInterval,       -- Template:Time_interval
}