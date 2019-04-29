require('Module:No globals')
local getArgs = require('Module:Arguments').getArgs
local p = {}

local function items(args, year)
	local itemList = {}
	if args[year] or args[year .. 'a'] then
		table.insert(itemList, args[year] or args[year .. 'a'])
	end
	for asciiletter = 98, 106 do -- 98 > b, 106 > j
		if args[year .. string.char(asciiletter)] then
			table.insert(itemList, args[year .. string.char(asciiletter)])
		end
	end
	return table.maxn(itemList), itemList
end

local function color(args, year, itemNum)
	
	if args[year .. '_color'] then
		return args[year .. '_color'] 
	end
	
	for yearrange = 1, 5 do
		if args['range' .. yearrange] and args['range' .. yearrange .. '_color'] then
			local _, _, beginyear, endyear = string.find( args['range' .. yearrange], '^(%d%d%d%d)%D+(%d%d%d%d)$' )
			
			local year = tonumber(year) or 9999 -- For year == 'TBA'
			beginyear = tonumber(beginyear) or 0
			endyear =  tonumber(endyear) or 9999
			
			if year >= beginyear and year <= endyear then
				local _, _, color1, color2 = string.find( args['range' .. yearrange .. '_color'], '^(%S*)%s*(%S*)$' )
				color2 = string.find(color2, '^#?%w+$') and color2 or color1
				return itemNum > 0 and color1 or color2
			end
		end
	end
	
	return itemNum > 0 and '#0BDA51' or '#228B22'
end

local function barLeft(builder, args, year, itemNum, outerPadding)
	builder = builder:tag('td')
		:attr('scope', 'row')
		:css('text-align', 'right') -- For year = 'TBA'
		:css('border', 'none')
		:css('padding', outerPadding)
		:css('border-right', '16px solid ' .. color(args, year, itemNum))
		:wikitext(year == 'TBA' and '待定' or year)
	if itemNum > 1 then
		builder = builder:attr('rowspan', itemNum)
	end
	
end

local function barRight(builder, args, year, itemNum, itemList, outerPadding, innerPadding)
	if itemNum == 0 then return end
	
	if itemNum == 1 then
		builder:tag('td')
			:css('padding', outerPadding)
			:css('border', 'none')
			:wikitext(itemList[1])
		return
	end
	
	-- if itemNum >= 2
	builder:tag('td')
		:css('border', 'none')
		:css('padding', outerPadding .. ' ' .. outerPadding .. ' ' .. innerPadding)
		:wikitext(itemList[1])
		
	for key = 2, itemNum - 1 do
		builder = builder:tag('tr')
			:tag('td')
			:css('border', 'none')
			:css('padding', innerPadding .. ' ' .. outerPadding)
			:wikitext(itemList[key])
	end
	
	builder = builder:tag('tr')
		:tag('td')
		:css('border', 'none')
		:css('padding', innerPadding .. ' ' .. outerPadding)
		:wikitext(itemList[itemNum])

end

local function row(builder, args, year, outerPadding, innerPadding)
	local itemNum, itemList = items(args, year)
	builder = builder:tag('tr')
	barLeft(builder, args, year, itemNum, outerPadding)
	barRight(builder, args, year, itemNum, itemList, outerPadding, innerPadding)
end

--------------------------------------------------------------------------------

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	-- Main module code goes here.
	local outerPadding, innerPadding = '5px', '2px'
	local currentyear = os.date('%Y')
		
	local ret
	local firstyear, lastyear
	local TBA = items(args, 'TBA') > 0 and true or false
	
	ret = mw.html.create( 'table' )
		:addClass('wikitable')
		:css('border', 'none')
		:css('float', args.align == 'left' and 'left' or 'right')
		:css('clear', args.align == 'left' and 'left' or 'right')
		:css('margin', args.align == 'left' and '0 1em 0.5ex 0' or '0 0 0.5ex 1em')
		:css('font-size', '80%')
		:css('line-height', '100%')
		:css('border-collapse', 'separate')
		:css('border-spacing', '0 1px')
		:css('background-color', 'transparent')
		
	ret:tag('caption')
		:css('padding', outerPadding .. ' ' .. outerPadding .. ' ' .. (args.subtitle and '0px' or innerPadding))
		:css('font-size', '112.5%') -- 90% / 80%
		:addClass('nowrap')
		:wikitext(args.title or '发行时间轴')
		
	if args.subtitle then
		ret:tag('tr'):tag('td')
			:attr('colspan', '2')
			:css('padding', '0px ' .. outerPadding .. ' ' .. innerPadding)
			:css('border', 'none')
			:css('text-align', 'center')
			:wikitext(args.subtitle)
	end
		
	if tonumber(args.first) then
		firstyear = tonumber(args.first)
	else
		for i = 1940, currentyear do
			if items(args, i) > 0 then
				firstyear = i
				break
			end
		end
	end
	
	if tonumber(args.last) then
		lastyear = tonumber(args.last)
	else
		for i = currentyear + 3, TBA and currentyear or firstyear, -1 do
			if items(args, i) > 0 then
				lastyear = i
				break
			end
		end
		lastyear = lastyear or (currentyear - 1)
	end

	for year = firstyear, lastyear do
		row(ret, args, year, outerPadding, innerPadding)
	end
	
	if TBA then
		row(ret, args, 'TBA', outerPadding, innerPadding)
	end
	
	return ret
end

return p