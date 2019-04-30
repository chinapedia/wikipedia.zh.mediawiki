--
-- This template implements {{Historical populations}}
--
local p = {}
local lang = mw.getContentLanguage()

local function ifexist(page)
    if not page then return false end
    if mw.title.new(page).exists then return true end
    return false
end

local function isempty( s )
	return not s or s:match( '^%s*(.-)%s*$' ) == ''
end

local function splitnumandref( s )
	s = s:match( '^%s*(.-)%s*$' )
	local t1 = mw.text.unstrip(s)
        local t2 = s:match( '^([%d][%d,]*)' )
	if( t1 == t2 ) then
		local t3 = s:match( '^[%d][%d,]*(.-)$' )
		return t1, t3
	else
		return s, ''
	end
end

local function formatnumR(num)
	return tonumber(lang:parseFormattedNumber(num))
end

local function formatnum(num)
	return lang:parseFormattedNumber(num) and lang:formatNum(lang:parseFormattedNumber(num)) or num
end

-- this function creates an array with the {year, population, percent change}
local function getpoprow(year, popstr, pyear, ppopstr, linktype, percentages, current_year)
	local pop, popref = splitnumandref( popstr or '')
	local ppop, ppopref = splitnumandref( ppopstr or '')
	local percent = ''
	local yearnum = formatnumR(mw.ustring.gsub(year or '', '^%s*([%d][%d][%.%d]+).*$', '%1') or '')
	local pyearnum = formatnumR(mw.ustring.gsub(pyear or '', '^%s*([%d][%d][%.%d]+).*$', '%1') or '')
	local popnum = formatnumR(pop)
	local ppopnum = formatnumR(ppop)
	if( linktype == 'US' or linktype == 'USA' ) then
		if( (yearnum or 0) >= 1790 and yearnum <= current_year and math.fmod(math.floor(yearnum), 10) == 0) then
			if( yearnum < current_year ) then
				year = '[['_.._tostring(yearnum)_.._'年美国人口普查|' .. year .. ']]'
  			elseif( ifexist(tostring(yearnum) .. '年美国人口普查') ) then
				year = '[['_.._tostring(yearnum)_.._'年美国人口普查|' .. year .. ']]'
			end
		end
	end
	if( linktype == 'CN' or linktype == 'CHN' ) then
		if( (yearnum or 0) == 1953) then
			year = '[['_.._tostring(yearnum)_.._'年中国大陆人口普查|' .. year .. ']]'
		end
		if( (yearnum or 0) == 1964) then
			year = '[['_.._tostring(yearnum)_.._'年中国大陆人口普查|' .. year .. ']]'
		end
		if( (yearnum or 0) == 1982) then
			year = '[['_.._tostring(yearnum)_.._'年中国大陆人口普查|' .. year .. ']]'
		end
		if( (yearnum or 0) >= 1990 and yearnum <= current_year and math.fmod(math.floor(yearnum), 10) == 0) then
			if( yearnum < current_year ) then
				year = '[['_.._tostring(yearnum)_.._'年中国大陆人口普查|' .. year .. ']]'
  			elseif( ifexist(tostring(yearnum) .. '年中国大陆人口普查') ) then
				year = '[['_.._tostring(yearnum)_.._'年中国大陆人口普查|' .. year .. ']]'
			end
		end
	end
	if(percentages ~= 'off') then
		local pstr = '—    '
		if(popnum ~= nil and ppopnum ~= nil and (ppopnum > 0)) then
			if(percentages == 'pagr') then
				pstr = mw.ustring.format('%.2f', 100*math.abs(math.pow(popnum/ppopnum,1/(yearnum-pyearnum)) - 1))
			else
				pstr = mw.ustring.format('%.1f', 100*math.abs(popnum/ppopnum - 1))
			end
			if( popnum < ppopnum ) then
				pstr = '−' .. pstr .. '%'
			else
				pstr = '+' .. pstr .. '%'
			end
		elseif(popnum ~= nil and ppopnum ~= nil and (ppopnum == popnum)) then
			pstr = mw.ustring.format('%.2f', 0) .. '%'
		end
		percent = pstr
	end
	-- strip the fractional part of the year, if there is one
	year = mw.ustring.gsub(year or '', '^%s*([%d][%d][%d]+)%.[%d]*', '%1')
	
	return {year, formatnum(pop) .. popref, percent }
end

-- this function creates an array with table header labels
local function getheadrow(percentages, popname, yearname, percentname)
	-- year cell	
	if(yearname == '') then
		yearname = '年份'
	end
	-- population cell
	if(popname == '') then
		popname = '人口'
	end

	-- percentages cell
	if( percentages ~= 'off' and percentname == '') then
		if( percentages == 'pagr' ) then
			percentname = '<abbr title="每年增长率">±% p.a.</abbr>'
		else
			percentname = '<abbr title="百分比变化">±%</abbr>'
		end
	end
	return {yearname, popname, percentname}
end

-- this function renders the population table in a vertical format
local function rendervertical(data, head, title, footnote, alignfn, class, style, width, shading, percol, cols)
	-- define a couple helper functions
	local function addrowcell(trow, tag, text, align, shading)
		cell = trow:tag(tag)
		cell
			:css('text-align', align)
			:css('padding', '1px')
			:wikitext(text)
			:css('border-bottom', shading ~= 'off' and '1px solid #bbbbbb' or nil)
	end
	local function addheadcell(trow, text, align, width, pad)
		cell = trow:tag('th')
		cell
			:css('border-bottom', '1px solid black')
			:css('padding', pad and ('1px ' .. pad) or '1px')
			:css('text-align', align)
			:css('width', width)
			:wikitext(text)
	end

	local colspan = 3
	local yearcount = #data
	local argcount = 2*yearcount
	
	if( isempty(width) ) then
		width = '15em'
	end
	
	-- override the value of cols if percol has been specified
	if( percol > 0 ) then
		cols = math.floor( (yearcount - 1) / percol ) + 1
	end
	
	-- compute the number of rows per col
	local rowspercol = math.floor( (yearcount - 1) / cols ) + 1

	-- specify the colspan for the title and footer lines
	if( cols > 1 ) then
		colspan = cols
	else
		if (head[3] == '') then 
			colspan = 2
		else
			colspan = 3
		end
	end

	-- compute outer table width
	local twidth = width
	if( (cols > 1) and width:match('^%s*[%d]+[%w]+%s*$') ) then
		local widthnum = mw.ustring.gsub( width, '^%s*([%d]+)([%w]+)%s*$', '%1' )
		local widthunit = mw.ustring.gsub( width, '^%s*([%d]+)([%w]+)%s*$', '%2' )
		twidth = tostring(widthnum*cols) .. widthunit
	end
	
	-- create the outer table
	local root = mw.html.create('table')
	root
		:addClass(class)
		:css('width', twidth)
		:cssText(style)
	-- add title
	local row = root:tag('tr')
	local cell = row:tag('th')
	cell
		:addClass('navbox-title')
		:attr('colspan', colspan)
		:css('padding', '0.25em')
		:css('font-size', '110%')
		:wikitext(title)
	
	-- loop over columns and rows within columns
	local offset = 1
	local t = root
	for c = 1,cols do
		-- add inner tables if we are rendering more than one column
		if( cols > 1) then
			if (c == 1) then
				row = root:tag('tr')
				row:attr('valign', 'top')
				cell = row:tag('td')
				cell:css('padding', '0 0.5em')
			else
				cell = row:tag('td')
				cell
					:css('padding', '0 0.5em')
					:css('border-left', 'solid 1px #aaa')
			end
			t = cell:tag('table')
			t
				:css('border-spacing', '0')
				:css('width', width)
		end
		-- start column headers
		local hrow = t:tag('tr')
		hrow:css('font-size', '95%')
		-- year header
		addheadcell(hrow, head[1], nil, head[3] ~= '' and '3em' or 'auto', nil, nil)
		-- population header
		addheadcell(hrow, head[2], 'right', nil, '2px')
		-- percentages header
		if( head[3] ~= '' ) then
			addheadcell(hrow, head[3], 'right', nil, nil)
		end
		-- end column headers
		-- start population rows
		for r = 1,rowspercol do
			-- generate the row if we have not exceeded the rowcount
			-- shade every fifth row, unless shading = off
			local s = 'off'
			if( math.fmod((c - 1)*rowspercol + r, 5) == 0 and r ~= rowspercol) then
				s = shading
			end
			if(offset <= yearcount) then
				-- start population row
				local prow = t:tag('tr')
				-- year cell
				addrowcell(prow, 'th', data[offset][1], 'center', s)
				-- population cell
				addrowcell(prow, 'td', data[offset][2], 'right', s)
				-- percentage cell
				if( not isempty(head[3]) ) then
					addrowcell(prow, 'td', data[offset][3], 'right', s)
				end
				-- end population row
				offset = offset + 1
			end
		end
	end

	-- add the footnote line 	
	if( footnote ~= '') then
		row = root:tag('tr')
		cell = row:tag('td')
		cell
			:attr('colspan', colspan)
			:css('border-top', '1px solid black')
			:css('font-size', '85%')
			:css('text-align', alignfn)
			:wikitext(footnote)
	end

	return tostring(root)
end

-- this function renders the population table in a horizontal format
local function renderhorizontal(data, head, title, footnote, alignfn, class, style, width, shading, perrow, rows)
	local row
	local cell
	local yearcount = #data
	local argcount = 2*yearcount
	
	-- override the value of rows if perrow has been specified
	if( perrow > 0 ) then
		rows = math.floor( (yearcount - 1) / perrow ) + 1
	end
	
	-- compute the number of cols per row
	local colsperrow = math.floor( (yearcount - 1) / rows ) + 1

	-- create the outer table
	local root = mw.html.create('table')
	root
		:addClass(class)
		:css('font-size', '90%')
		:cssText(style)
	-- create title row
	row = root:tag('tr')
	cell = row:tag('th')
	cell
		:css('padding', '0.25em')
		:css('font-size', '110%')
		:attr('colspan', colsperrow + 1)
		:wikitext(title)

	-- loop over rows and columns within rows
	local offset = 1
	for r = 1,rows do
		local rowoffset = offset
		-- render the years
		row = root:tag('tr')
		cell = row:tag('th')
		cell:wikitext(head[1])
			:css('border-top', r > 1 and '2px solid #000' or nil)
		for c = 1,colsperrow do
			cell = row:tag('td')
			if(offset <= yearcount) then
				cell:wikitext(data[offset][1])
					:css('text-align', 'center')
					:css('border-top', r > 1 and '2px solid #000' or nil)
			else
				cell:css('border-width', r > 1 and '2px 0 0 0' or 0)
					:css('border-top', r > 1 and '2px solid #000' or nil)
			end
			offset = offset + 1
		end
		-- render the pop
		offset = rowoffset
		row = root:tag('tr')
		cell = row:tag('th')
		cell:wikitext(head[2])
		for c = 1,colsperrow do
			cell = row:tag('td')
			if(offset <= yearcount) then
				cell:wikitext(data[offset][2])
					:css('text-align', 'right')
					:css('padding-right', '2px')
			else
				cell:css('border-width', 0)
			end
			offset = offset + 1
		end
		-- render the percentages
		if(head[3] ~= '') then
			offset = rowoffset
			row = root:tag('tr')
			cell = row:tag('th')
			cell:wikitext(head[3])
			for c = 1,colsperrow do
				cell = row:tag('td')
				if(offset <= yearcount) then
					cell:wikitext(data[offset][3])
						:css('text-align', 'right')
						:css('padding-right', '2px')
				else
					cell:css('border-width', 0)
				end
				offset = offset + 1
			end
		end
	end

	-- add the footnote line 	
	if( footnote ~= '') then
		row = root:tag('tr')
		cell = row:tag('td')
		cell
			:css('border-top', '2px solid black')
			:css('font-size', '85%')
			:css('text-align', alignfn)
			:attr('colspan', colsperrow + 1)
			:wikitext(footnote)
	end

	return tostring(root)
end

-- this is the main function
function p.poptable(frame)
	local data = {}
	local args = frame.args[1] and frame.args or frame:getParent().args

	local title			= args['title']			or ''
	local align			= args['align']			or ''
	local clear			= args['clear']			or ''
	local direction		= args['direction']		or ''
	local percentages	= args['percentages']	or ''
	local state			= args['state']			or ''
	local linktype		= args['type']			or ''
	local shading		= args['shading']		or 'on'
	local width			= args['width']			or ''
	local subbox		= args['subbox']		or ''
	local popname		= args['pop_name']		or ''
	local yearname		= args['year_name']		or ''
	local percentname   = args['percent_name']  or ''
	local footnote		= args['footnote']		or ''
	local alignfn		= args['align-fn']		or ''
	local source		= args['source']		or ''
	local percol = tonumber(args['percol'])	or 0
	local cols	 = tonumber(args['cols'])	or 1
	local perrow = tonumber(args['perrow'])	or 0
	local rows	 = tonumber(args['rows'])	or 1

	-- setup classes and styling for outer table
	local class = direction == 'horizontal' and 'wikitable' or 'toccolours'
	if( state == 'collapsed' ) then
		class = class .. ' collapsible collapsed'
	end

	if( isempty(title) ) then
		title = '歷史人口'
	end

	if( isempty(align) ) then
		align = direction ~= 'horizontal' and 'right' or 'center'
	end
	
	if( isempty(alignfn) ) then
		alignfn = 'left'
	end
	
	if( isempty(clear) ) then
		clear = align == 'center' and '' or align
	end
	
	local margin = '0.5em 0 1em 0.5em'
	if( align == 'left' ) then
		margin = '0.5em 1em 0.5em 0'
	elseif( align == 'none' ) then
		margin = '0.5em 1em 0.5em 0'
	elseif( align == 'center' ) then
		margin = '0.5em auto'
		align = ''
	end

	if( isempty(subbox) ) then
		style =
			'border-spacing: 0;' ..
			(align ~= '' and 'float:' .. align .. ';' or '') ..
			(clear ~= '' and 'clear:' .. clear .. ';' or '') ..
			'margin:' .. margin .. ';'
	else
		style =
			'margin:0;' ..
			'border-collapse:collapse;' ..
			'border:none;'
	end	
		
	-- setup the footer text
	if( source ~= '' ) then
		source = '來源：' .. source
		if( footnote ~= '' ) then
			footnote = footnote .. '<br/>'
		end
	end
	footnote = footnote .. source
	
	-- setup the data header cols/rows
	local head = getheadrow(percentages, popname, yearname, percentname)
	
	-- count the total number of population rows
	local argcount = 0
	local rowcount = 0
	for k, v in pairs( args ) do
		if ( (type( k ) == 'number') and (not isempty(args[k])) ) then
			if( k >= 1 and math.floor(k) == k and k > argcount) then
				argcount = k
			end
			if( math.fmod(k - 1, 2) == 0 ) then
				rowcount = rowcount + 1
			end
		end
	end

	-- here is where we build all the data for the table
	-- loop over columns and rows within columns
	local pyear = ''
	local ppop = ''
	local offset = 1
	local current_year = tonumber(os.date("%Y", os.time()))
	for r = 1,rowcount do
		-- skip blank rows
		while(isempty(args[offset]) and offset <= argcount) do
			offset = offset + 2
		end
		-- generate the row if we have not exceeded the rowcount
		if(offset <= argcount) then
			table.insert(data, getpoprow(args[offset], args[offset + 1] or '', pyear, ppop, 
				linktype, percentages, current_year) )
			pyear = args[offset]
			ppop = args[offset+1] or ''
			offset = offset + 2
		end
	end

	-- now that we have the data for the table, render it in the requested format
    if (direction == 'horizontal') then
		return renderhorizontal(data, head, title, footnote, alignfn, class, style, width, shading, perrow, rows)
	else
		return rendervertical(data, head, title, footnote, alignfn, class, style, width, shading, percol, cols)
	end
end

return p