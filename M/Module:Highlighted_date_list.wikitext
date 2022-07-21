-- This module takes a list of dates and adds a marker highlighting the closest
-- date in the future.

local p = {}
local lang = mw.language.getContentLanguage()

local function normalizeDate(timestamp)
	local success, date = pcall(lang.formatDate, lang, 'Y-m-d', timestamp)
	return success and date
end

local function makeData(args)
	local data, unsorted = {}, {}
	for k, v in pairs(args) do
		if type(k) == 'string' then
			local datakey, num = k:match('^(.-)([1-9][0-9]*)$')
			if datakey == 'item' or datakey == 'date' then
				num = tonumber(num)
				unsorted[num] = unsorted[num] or {}
				unsorted[num][datakey] = v
			elseif datakey then
				error(string.format("invalid parameter '%s' detected", k), 3)
			end
		end
	end
	for num, t in pairs(unsorted) do
		if t.item and t.date then
			local date = normalizeDate(t.date)
			if not date then
				error(string.format(
					"invalid date '%s' in parameter 'date%d'",
					t.date, num
				), 3)
			end
			t.date = date
			table.insert(data, t)
		elseif t.item then
			error(string.format(
				"parameter 'item%d' was specified but parameter 'date%d' is missing",
				num, num
			), 3)
		else
			error(string.format(
				"parameter 'date%d' was specified but parameter 'item%d' is missing",
				num, num
			), 3)
		end
	end
	table.sort(data, function (t1, t2)
		return t1.date < t2.date
	end)
	return data
end

local function makeComparisonDate(gracePeriod)
	local timestamp
	if gracePeriod then
		timestamp = 'now - ' .. gracePeriod
	else
		timestamp = 'now'
	end
	local date = normalizeDate(timestamp)
	if date then
		return date
	else
		error(string.format("invalid grace period '%s'", gracePeriod), 3)
	end
end

local function makeHighlighter(color)
	color = color or '#FC6'
	local highlighter = mw.html.create('span')
	highlighter
		:css('background-color', color)
		:wikitext(lang:getArrow('forwards'))
	return tostring(highlighter)
end

function p._main(args)
	local data = makeData(args)
	local comparisonDate = makeComparisonDate(args.graceperiod)
	local highlighter = args.highlighter or makeHighlighter(args.highlightercolor)
	local root = mw.html.create('ul')
	root
		:addClass(args.class)
		:cssText(args.style)
	local doneHighlight = false
	for i, t in ipairs(data) do
		local item
		if not doneHighlight and t.date >= comparisonDate then
			doneHighlight = true
			item = highlighter .. ' ' .. t.item
		else
			item = t.item
		end
		root
			:newline()
			:tag('li')
				:wikitext(item)
	end
	root:newline()
	return tostring(root)
end

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {
		wrappers = 'Template:Highlighted date list'
	})
	return p._main(args)
end

return p