--
-- This module implements {{Sidebar games events}}
-- This module was created using code taken directly from [[Module:Sidebar|Module:Sidebar]] 
--
require('Module:No globals')

local p = {}

local getArgs = require('Module:Arguments').getArgs
local navbar = require('Module:Navbar')._navbar

function p.sidebar(frame, args)
	if not args then
		args = getArgs(frame)
	end
	
	local root = mw.html.create()

	root = root
		:tag('table')
		:addClass('vertical-navbox')
		:addClass('nowraplinks')
		:addClass(args.class or 'hlist')
		:css('float', args.float or 'right')
		:css('clear', (args.float == 'none' and 'both') or args.float or 'right')
		:css('width', args.width or 'auto')
		:css('max-width', args.maxwidth or '25em')
		:css('margin', args.float == 'left' and '0 1.0em 1.0em 0' or '0 0 1.0em 1.0em')
		:css('background', '#f5faff')
		:css('border', '1px solid #B8C7D9')
		:css('padding', '0.2em')
		:css('border-spacing', '0.4em 0')
		:css('text-align', 'center')
		:css('font-size', '88%')

	-- enumerate the rows and count the columns
	local cols = 1
	local colindex = {a = '2', b = '3', c = '4', d = '5', e = '6'}
	local lets = {'a', 'b', 'c', 'd', 'e'}
	local rowNums = {}
	local subevents = 0
	local hasevents = false

	for k, v in pairs(args) do
		k = '' .. k
		local num = k:match('^event(%d+)$') 
			or k:match('^image(%d+)$')
			or k:match('^type(%d+)[a-e]$')
			or k:match('^event(%d+)%.%d+$')
			or k:match('^results(%d+)%.%d+[a-e]?$')
		if num then table.insert(rowNums, tonumber(num)) end
		
		if k:match('^results%d+%.(%d+)$') then
			cols = (2 > cols) and 2 or cols
		end
		
		local let = k:match('^results%d+%.%d+([a-e])$')
			or k:match('^type%d+([a-e])$')
		if let and colindex[let] then
			local n = tonumber(colindex[let])
			cols = (n > cols) and n or cols
		end
		
		local subnum = k:match('^results%d+%.(%d+)[a-e]?$')
			or k:match('^event%d+%.(%d+)$')
		if subnum then
			subnum = tonumber(subnum)
			subevents = (subnum > subevents) and subnum or subevents
		end
		
		if k:match('^(event%d+%.%d+)$') then
			hasevents = true
		end
	end
	-- remove duplicates from the list (e.g. 3 will be duplicated if both event3 and image3 are specified)
	table.sort(rowNums)
	for i = #rowNums, 1, -1 do
		if rowNums[i] == rowNums[i - 1] then
			table.remove(rowNums, i)
		end
	end
	
	-- alignment
	local alignevents = 'text-align:left;'
	if args.alignevents and args.alignevents == 'right' then
		alignevents = 'text-align:right;'
	end
	local alignresults = nil
	if args.alignresults and args.alignresults == 'right' then
		alignresults = 'text-align:right; padding-right:1.5em'
	elseif args.alignresults and args.alignresults == 'left' then
		alignresults = 'text-align:left'
	end

	-- add the top level header	
	if args.event or args.title then
		local t = args.event
		if args.title then
			t = args.title
		elseif args.games then
			t = '[['_.._args.games_..''.._args.event_.._'比赛|' .. args.event .. '比赛]]'
			t = '[['_.._args.games_.._'|' .. args.games .. ']]<br>' ..t
		end
		local cell = root:tag('tr'):tag('th')
		cell
			:css('padding', '0.2em 0.4em 0.2em')
			:css('font-size', '100%')
			:css('line-height', '1.5em')
			:css('background', '#cedff2')
			:attr('colspan', cols)
		if args.imageright then
			local d = cell:tag('div')
				:css('display', 'table')
				:css('width', '100%')
			d:tag('div')
				:css('display', 'table-cell')
				:css('width', '95%')
				:wikitext(t)
			d:tag('div')
				:css('display', 'table-cell')
				:css('width', '5%')
				:wikitext(args.imageright)
		else
			cell:wikitext(t)
		end
	end

	if args.image then
		local imageCell = root:tag('tr'):tag('td')

		imageCell
			:css('padding', '0 0 0.2em')
			:css('background', '#cedff2')
			:attr('colspan', cols)
			:wikitext(args.image)

		if args.caption then
			imageCell
				:tag('div')
					:css('padding-top', '0.2em')
					:css('line-height', '1.2em')
					:wikitext(args.caption)
		end
	end

	if args.above then
		local cell = root:tag('tr'):tag('td')
		cell:attr('colspan', cols)
			:wikitext(args.above)
	end
	
	-- start adding rows
	for i, num in ipairs(rowNums) do
		local heading = nil
		local event = args['event' .. num]
		local image = args['image' .. num]
		if event and image then
			heading = event .. '<br>' .. image
		elseif event then
			heading = event
		elseif image then
			heading = image
		end
		
		if heading then
			root
				:tag('tr')
					:tag('th')
						:css('padding', '0.1em')
						:css('background', '#deeaf6')
						:css('border-top', '1px solid #f5faff')
						:attr('colspan', cols)
						:wikitext(heading)
		end

		local showtypes = false
		for j, let in ipairs(lets) do
			if j < cols then
				if args['type' .. num .. let] then
					showtypes = true
				end
			end
		end
		if showtypes == true then
			local row = root:tag('tr')
			row:tag('th'):css('display', (hasevents == false) and 'none' or nil)
			for j, let in ipairs(lets) do
				if j < cols then
					local t = args['type' .. num .. let]
					local cell = row:tag('th')
					if t then
						cell
							:css('font-weight', 'normal')
							:css('border-top', '1px solid #f5faff')
							:css('background', '#deeaf6')
							:css('width', (cols > 2) and tostring(math.floor(100/(cols-1))) .. '%' or nil)
							:wikitext(t)
					end
				end
			end
		end

		for k=1,subevents do
			local hasresults = false
			if args['results' .. num .. '.' .. k] then
				hasresults = true
			else
				for j, let in ipairs(lets) do
					if j < cols then
						if args['results' .. num .. '.' .. k .. let] then
							hasresults = true
						end
					end
				end
			end
	
			if hasresults then
				local row = root:tag('tr')
				local cell = row:tag('th'):css('display', (hasevents == false) and 'none' or nil)
				local t = args['event' .. num .. '.' .. k]
				local border = args['border' .. num .. '.' .. k]  and 'solid 1px #aaa' or nil
				if t then
					cell
						:cssText(alignevents)
						:css('line-height', '1.4em')
						:css('padding', '0.1em 0.4em 0.2em 0.1em')
						:css('font-weight', 'normal')
						:css('border-bottom', border)
						:wikitext(t)
				end
				if args['results' .. num .. '.' .. k] then
					row:tag('td')
							:attr('colspan', cols - 1)
							:css('border-bottom', border)
							:cssText(alignresults)
							:newline() -- newline required for bullet-points to work
							:wikitext(args['results' .. num .. '.' .. k])
				else
					for j, let in ipairs(lets) do
						if j < cols then
							t = args['results' .. num .. '.' .. k .. let]
							row:tag('td')
								:css('border-bottom', border)
								:cssText(alignresults)
								:wikitext(t)
						end
					end
				end
			end
		end
	end
	if args.below then
		root
			:tag('tr')
				:tag('td')
					:addClass(args.belowclass)
					:attr('colspan', cols)
					:cssText(args.belowstyle)
					:wikitext(args.below)
	end

	local navbarArg = args.navbar or args.tnavbar
	if navbarArg ~= 'none' and navbarArg ~= 'off' and (args.name or frame:getParent():getTitle():gsub('/sandbox$', '') ~= 'Template:Sidebar games events') then
		root
			:tag('tr')
				:tag('td')
					:css('text-align', 'right')
					:css('font-size', '115%')
					:css('padding-top', '0')
					:css('border-top', 'solid 1px #deeaf6')
					:attr('colspan', cols)
					:wikitext(navbar{
						args.name,
						mini = 1,
						fontstyle = args.navbarfontstyle or args.tnavbarfontstyle
					})
	end

	return tostring(root)
end

return p