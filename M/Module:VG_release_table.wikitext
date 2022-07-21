require('Module:No globals')

local getArgs = require('Module:Arguments').getArgs
local p = {}

local function usedRow(args, maxLine)
	local usedRow = {}
	
	for lineNum = 1, 5 do -- rowHeader has 5 items
		local row = string.char(lineNum + 64) -- 1 => 'A', 2 => 'B'
		for line = 1, maxLine do
			if args[line .. row] then
				table.insert(usedRow, row)
				break
			end
		end
	end
	
	return usedRow
end

local function row(builder, args, usedRow, line)
	if args[line] == nil then return end
	
	local tr = builder:tag('tr')
	local th = tr:tag('th')
	th:wikitext(args[line]):attr('scope', 'row'):css('background-color', 'transparent')
	
	if args[line .. 'W'] then -- 'W' for worldwide
		tr:tag('td'):attr('colspan', table.maxn(usedRow)):wikitext(args[line .. 'W'])
		return
	end
	
	for index, row in ipairs(usedRow) do
		local text = args[line .. row] or ''
		if string.lower(text) ~= 'left' then
			local colspan = 1
			for flag = index + 1, table.maxn(usedRow) do
				if string.lower(args[line .. usedRow[flag]] or '') == 'left' then
					colspan = colspan + 1
				else
					break
				end
			end
			local td = tr:tag('td')
			if string.lower(text) == 'n/a' then
				td:wikitext('无')
					:addClass('table-na')
					:css('background-color', '#ececec')
					:css('color', 'grey')
			else
				td:wikitext(text)
			end
			if colspan > 1 then
				td:attr('colspan', colspan)
			end
		end
	end
	
end

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	-- Main module code goes here.
	local builder = mw.html.create('table')
	local maxLine = 24
	local usedRow = usedRow(args, maxLine)
	local rowHeader = {
		A = '日本',
		B = '北美',
		C = '欧洲',
		D = '<abbr title="中国大陆">大陆</abbr>',
		E = '台港'
	}

	builder
		:addClass('infobox wikitable')
		:css('margin-top', '0')
		:css('text-align', 'center')
		:css('vertical-align', 'middle')
		:css('font-size', '80%')
		:css('margin', '0em 1em 1em 1em')
	builder:tag('caption'):wikitext(args.title or '各平台发行年表')
	
	local tr = builder:tag('tr')

	tr:tag('th'):attr('scope', 'col')
	for _, row in ipairs(usedRow) do
		if args['region' .. row] then
			rowHeader[row] = args['region' .. row]
		end
		tr:tag('th'):wikitext(rowHeader[row]):attr('scope', 'col')
	end
	
	for line = 1, maxLine do
		row(builder, args, usedRow, line)
	end
	
	return builder
end

return p