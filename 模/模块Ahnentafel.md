--
-- implements [[Template:ahnentafel|Template:ahnentafel]]
--
local p = {}

-- table of row pointers
local rows = {}
-- first and last indices in rows table
local rowbegin, rowend = -1,-1
-- tracking
local tcats = ''

local function checkparameters(k)
	if (k == 'align' or k == 'collapsed' or k == 'collapsible' or
		k == 'title' or k == 'float' or k == 'clear' or k == 'ref' or
		k == 'headnotes' or k == 'headnotes_align' or 
		k == 'footnotes' or k == 'footnotes_align' or
		k == 'width' or k == 'min-width' or k == 'text-align') then
		return
	end
	if (k == 'boxstyle' or k == 'style' or k == 'border') then
		tcats = tcats .. '[[Category:使用ahnentafel模板帶有'_.._k_.._'的條目|Category:使用ahnentafel模板帶有' .. k .. '的條目]]'
		return
	end
	if k:find('^boxstyle_[1-8]$') then
		return
	end
	if k:find('^border_[1-8]$') then
		return
	end
	k = mw.ustring.gsub(k, '[^%w\-_ ]', '?')
	tcats = tcats .. '[[Category:使用ahnentafel模板未知參數的條目|' .. k .. ']]'
end

local function addcell(r, rspan, cspan, t, s)
	if ((r + rspan - 1) < rowbegin) or (r > rowend) then
		-- completely out of range; do nothing
		return
	elseif r < rowbegin then
		-- partially out of range, adjust
		rspan = rspan - (rowbegin - r)
		r = rowbegin
	elseif (r + rspan - 1) > rowend then
		-- partially out of range, adjust
		rspan = rowend + 1 - r
	end
	if rspan > 0 then
		rows[r]:tag('td')
			:attr('rowspan', (rspan > 1) and rspan or nil)
			:attr('colspan', (cspan > 1) and cspan or nil)
			:cssText(s)
			:wikitext(t)
	end
end

function p.chart( frame )
	local getArgs = require('Module:Arguments').getArgs
	local args = getArgs(frame)
	local align = (args['align'] or ''):lower()
	local style = args['style'] or ''
	local topbranch = 'border-top:#000 solid 1px; border-left:#000 solid 1px;'
	local botbranch = 'border-bottom:#000 solid 1px; border-left:#000 solid 1px;'
	
	local yesno = require('Module:Yesno')
	
	if args['collapsed'] and args['collapsed'] ~= '' then
		args['collapsible'] = 'yes'
	end
	
	if args['title'] and args['title'] ~= '' then
		args['collapsible'] = 'yes'
		if yesno(args['collapsed'] or 'no') then
			args['collapsed'] = 'yes'
		else
			args['collapsed'] = 'no'
		end
	end
	
	-- style for floating
	if (align == 'right') then
		style = 'float:right;' .. style
	elseif (align == 'left') then
		style = 'float:left;' .. style
	elseif (align == 'center') then
		style = 'margin-left:auto; margin-right:auto;' .. style
	end
	
	-- compute the number of levels and track unsupported parameters
	local maxnum = 0
	for k, v in pairs( args ) do
		if (k and type(k) == 'number' or 
			(type(k) == 'string' and (tonumber(k) or 0) > 0)) then
			if tonumber(k) > maxnum then
				maxnum = k
			end
		else
			if (k and type(k) == 'string') then
				checkparameters(k)
			end
		end
	end

	-- limit the number of levels
	maxnum = (maxnum > 511) and 511 or maxnum
	
	local levels = math.ceil(math.log(maxnum+1)/math.log(2))
	local cells  = math.pow(2, levels) - 1
	
	-- "fill in" missing boxes
	for k=cells,2,-1 do
		local j = math.floor(k/2)
		if args[k] and args[k] ~= '' then
			if args[j] == nil or args[j] == '' then
				args[j] = ' ' -- single space
			end
		end
	end
	
	-- compute the first and last row number
	rowbegin = 2*cells+1
	rowend   = 2*cells+2
	local cellnum = 0
	for l = 1,levels do
		local cellsk = math.pow(2,l-1)
		local offset = 1
		for k = 1,cellsk do
			cellnum = cellnum + 1
			offset = offset + 2*(math.pow(2,levels-l+1)-1)
			if args[cellnum] and args[cellnum] ~= '' then
				rowbegin = (offset < rowbegin) and offset or rowbegin
				rowend = ((offset+1) > rowend) and (offset+1) or rowend
			end
			if args[cellnum] and args[cellnum] == '' then
				args[cellnum] = nil
			end
			offset = offset + 2*(math.pow(2,levels-l+1)-1) + 4
		end
	end
	
	-- add a collapsing outer container if required
	local res = mw.html.create('')
	local innercell = res
	local innerfs = '88%'
	if yesno(args['collapsible'] or 'no') then
		local r = res:tag('table')
		local t = args['title'] or (mw.title.getCurrentTitle().text .. '的先祖')
		r:addClass('collapsible')
		if yesno(args['collapsed'] or 'yes') then
			r:addClass('collapsed')
		end
		local f = args['float'] or ''
		if f == 'left' then
			r:css('margin', '0.3em 1em 0.3em 0')
			r:css('float', 'left')
			r:css('clear', args['clear'] or 'left')
			r:css('min-width', args['min-width'] or args['width'] or '33em')
		elseif f == 'right' then
			r:css('margin', '0.3em 0 0.3em 1em')
			r:css('float', 'right')
			r:css('clear', args['clear'] or 'right')
			r:css('min-width', args['min-width'] or args['width'] or '33em')
		elseif f == 'none' then
			r:css('margin', '0.3em 0')
			r:css('min-width', args['min-width'] or args['width'] or '60em')
		else
			r:css('margin', '0.3em auto')
			r:css('clear', args['clear'] or 'none')
			r:css('min-width', args['min-width'] or args['width'] or '60em')
		end
		r:css('width', args['width'] or 'auto')
		r:css('font-size', '88%')
		r:css('border', '1px solid #aaa')
		r:tag('tr'):tag('th')
				:css('padding', '0.2em 0.3em 0.2em 4.3em')
				:css('background', 'none')
				:css('width', args['width'] or 'auto')
				:wikitext(t .. (args['ref'] or ''))
		innercell = r:tag('tr'):tag('td')
				:css('text-align', args['text-align'] or 'center')
		innerfs = nil
		args['ref'] = nil
	end

	-- add content before the table if required
	if args['headnotes'] then
		if args['headnotes_align'] then
			innercell:tag('div')
				:css('width','100%')
				:css('text-align',args['headnotes_align'])
				:wikitext(args['headnotes'])
		else
			innercell:wikitext(args['headnotes'])
		end
	end

	-- build the inner table
	local root = innercell:tag('table')
	root:css('border-collapse', 'separate')
		:css('border-spacing', '0')
		:css('line-height', '130%')
		:css('font-size', innerfs)
		:cssText(style)

	-- initialize the rows with 1 by 1 blank cells
	for k = rowbegin, (rowend+1) do
		rows[k] = root:tag('tr'):css('text-align', 'center')
		rows[k]:tag('td'):wikitext(' ')
	end
	-- add a blank row of cells to assist with alignment
	for k = 1,(3*levels + 1) do
		rows[rowend+1]:tag('td'):wikitext(' ')
	end
	
	local cellnum = 0
	for l = 1,levels do
		local levelstyle = args['boxstyle_' .. l] or ''
		if args['boxstyle'] and args['boxstyle'] ~= '' then
			levelstyle = args['boxstyle'] .. ';' .. levelstyle
		end
		levelstyle = 'height:0.5em; padding:0 0.2em;' .. levelstyle
		levelstyle = 'border:' .. (args['border_' .. l] or args['border'] or '1') .. 'px solid black;' .. levelstyle
		
		local cellsk = math.pow(2,l-1)
		local offset = 1
		for k = 1,cellsk do
			cellnum = cellnum + 1
			-- top padding
			addcell(offset, 2*(math.pow(2,levels-l+1)-1), (l < levels) and 2 or 4, ' ', nil)
			-- top branch
			if l < levels then
				addcell(offset, math.pow(2,levels-l+1)-1, 1, ' ', nil)
				addcell(offset + math.pow(2,levels-l+1)-1, math.pow(2,levels-l+1)-1, 1, ' ',
					args[2*cellnum] and topbranch or nil)
			end
			offset = offset + 2*(math.pow(2,levels-l+1)-1)
			-- cell
			addcell(offset, 2, 4, args[cellnum] or ' ', args[cellnum] and levelstyle or nil)
			if l < levels then
				addcell(offset, 2, 3 + 4*(levels - l - 1), ' ', nil)
			end
			offset = offset + 2
			-- bottom padding
			addcell(offset, 2*(math.pow(2,levels-l+1)-1), (l < levels) and 2 or 4, ' ', nil)
			-- bottom branch
			if l < levels then
				addcell(offset, math.pow(2,levels-l+1)-1, 1, ' ', 
					args[2*cellnum+1] and botbranch or nil)
				addcell(offset + math.pow(2,levels-l+1)-1, math.pow(2,levels-l+1)-1, 1, ' ', nil)
			end
			offset = offset + 2*(math.pow(2,levels-l+1)-1) + 2
		end
	end
	
	-- add content after the table if required
	if args['footnotes'] or args['ref'] then
		if args['footnotes_align'] then
			innercell:tag('div')
				:css('width','100%')
				:css('text-align',args['footnotes_align'])
				:wikitext(args['footnotes'])
		else
			innercell:wikitext(args['ref'])
			innercell:wikitext(args['footnotes'])
		end
	end
	
	return '<div class="noresize">' .. tostring(res) .. '</div>' .. tcats
end

return p