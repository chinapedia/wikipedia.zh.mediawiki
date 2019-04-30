-- This module renders the calendar seen on [[Portal:Current_events|Portal:Current events]].

local p = {}

local function makeWikilink(link, display)
	if display then
		return string.format('[[%s|%s]]', link, display)
	else
		return string.format('[[%s|%s]]', link)
	end
end

function p.main()
	local dateStuff = p.getDateStuff()
	local dayStrings = p.makeDayStrings(dateStuff)
	return p.export(dayStrings, dateStuff)
end

function p.getDateStuff()
	-- Gets date data.
	local dateStuff = {}
	local lang = mw.language.getContentLanguage()
	--Year
	local year = lang:formatDate('Y')
	year = tonumber(year)
	dateStuff.year = year
	-- Month
	local month = lang:formatDate('F')
	dateStuff.month = month
	-- Month and year
	local monthAndYear = lang:formatDate('F Y')
	local firstOfMonth = lang:formatDate('01-m-Y')
	dateStuff.monthAndYear = monthAndYear
	-- Previous month and year
	dateStuff.previousMonthAndYear = lang:formatDate('F Y', firstOfMonth .. ' -1 month')
	-- Next month and year
	dateStuff.nextMonthAndYear = lang:formatDate('F Y', firstOfMonth .. ' +1 month')
	-- Day
	local day = lang:formatDate('j')
	day = tonumber(day)
	dateStuff.day = day
	-- Days in month
	local daysInMonth = lang:formatDate('j', firstOfMonth .. ' +1 month -1 day')
	daysInMonth = tonumber(daysInMonth)
	dateStuff.daysInMonth = daysInMonth
	-- Weekday of the first day of the month
	local firstWeekday = lang:formatDate('w', firstOfMonth) -- Sunday = 0, Saturday = 6
	firstWeekday = tonumber(firstWeekday)
	firstWeekday = firstWeekday + 1 -- Make compatible with Lua tables. Sunday = 1, Saturday = 7.
	dateStuff.firstWeekday = firstWeekday
	return dateStuff
end

function p.makeDayStrings(dateStuff)
	local calStrings = {}
	local currentDay = dateStuff.day
	local isLinkworthy = p.isLinkworthy
	local currentMonth = dateStuff.month
	local currentYear = dateStuff.year
	local makeDayLink = p.makeDayLink
	for day = 1, dateStuff.daysInMonth do
		if isLinkworthy(day, currentDay) then
			calStrings[#calStrings + 1] = makeDayLink(day, currentMonth, currentYear)
		else
			calStrings[#calStrings + 1] = tostring(day)
		end
	end
	return calStrings
end

function p.isLinkworthy(day, currentDay)
	-- Returns true if the calendar day should be linked, and false if not.
	-- Days should be linked if they are the current day or if they are within the six
	-- preceding days, as that is the number of items on the current events page.
	if currentDay - 6 <= day and day <= currentDay then
		return true
	else
		return false
	end
end

function p.makeDayLink(day, month, year)
	return string.format("'''[[#%d_%s_%d|  %d  ]]'''", year, month, day, day)
end

function p.export(dayStrings, dateStuff)
	-- Generates the calendar HTML.
	local monthAndYear = dateStuff.monthAndYear
	local root = mw.html.create('table')
	root
		:addClass('infobox')
		:css{
			display = 'table',
			width = '100%',
			float = 'initial', 
			['max-width'] = '350px',
			margin = 'auto !important',
			['text-align'] = 'center',
			['background-color'] = '#f5faff',
			border = '1px solid #cedff2'
		}
		-- Headings
		:tag('tr')
			:css('background-color', '#cedff2')
			:tag('th')
				:css{['text-align'] = 'center'}
				:wikitext(makeWikilink('Portal:Current events/' .. dateStuff.previousMonthAndYear, '◀'))
				:done()
			:tag('th')
				:attr('colspan', '5')
				:css{['text-align'] = 'center'}
				:wikitext(makeWikilink('Portal:Current events/' .. monthAndYear, monthAndYear))
				:done()
			:tag('th')
				:css{['text-align'] = 'center'}
				:wikitext(makeWikilink('Portal:Current events/' .. dateStuff.nextMonthAndYear, '▶'))

	-- Day of week headings
	local dayHeadingRow = root:tag('tr')
	local weekdays = {'S', 'M', 'T', 'W', 'T', 'F', 'S'}
	for i, weekday in ipairs(weekdays) do
		dayHeadingRow:tag('th')
			:css{['width'] = '14%', ['text-align'] = 'center'}
			:wikitext(weekday)
	end
	
	-- Days
	local colspan = dateStuff.firstWeekday - 1
	local cellCount = 0 -- Tracks the number of day cells.
	local firstDayRow = root:tag('tr')
	if colspan > 1 then
		firstDayRow:tag('td')
			:attr('colspan', tostring(colspan))
	elseif colspan == 1 then
		firstDayRow:tag('td')
	end
	for i = colspan + 1, 7 do -- Finish the first row
		cellCount = cellCount + 1
		firstDayRow:tag('td')
			:css{['text-align'] = 'center'}
			:wikitext(dayStrings[cellCount])
	end
	while cellCount < #dayStrings do -- Second day row onwards
		local otherDayRow = root:tag('tr')
		for i = 1, 7 do
			cellCount = cellCount + 1
			local dayString = dayStrings[cellCount]
			if not dayString then
				dayString = " "
			end
			otherDayRow:tag('td')
				:css{['text-align'] = 'center'}
				:wikitext(dayString)
		end
	end

	-- Footer
	root:tag('tr')
		:tag('td')
			:attr('colspan', '7')
			:css{['padding-top'] = '3px', ['padding-bottom'] = '5px', ['font-size'] = '78%', ['text-align'] = 'right'}
			:wikitext('   ' .. makeWikilink('Portal:Current events/' .. monthAndYear, 'More ' .. monthAndYear .. ' events...   '))
	
	return tostring(root)
end

return p