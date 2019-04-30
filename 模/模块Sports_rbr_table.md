-- This module implements {{Sports rbr table}}
local p = {}

-- Internationalisation
local labels = {
	teamround = '隊伍 ╲ 輪次',
	source = ' 資料來源：',
	notes = ' 附註：',
	matches = '排名結果',
	updatedto = ' <matches>更新至<date>',
	firstplayed = ' 第一場比賽將在<date>舉行',
	futuredate = '?',
	complete = 'complete',
	future = 'future'
}

local args = nil

local colorlist = {}
local textlist = {}

local color_map = {
		green1='#BBF3BB', green2='#CCF9CC', green3='#DDFCDD', green4='#EEFFEE',
		blue1='#BBF3FF', blue2='#CCF9FF', blue3='#DDFCFF', blue4='#EEFFFF',
		yellow1='#FFFFBB', yellow2='#FFFFCC', yellow3='#FFFFDD', yellow4='#FFFFEE',
		red1='#FFBBBB', red2='#FFCCCC', red3='#FFDDDD', red4='#FFEEEE',
		black1='#BBBBBB', black2='#CCCCCC', black3='#DDDDDD', black4='#EEEEEE',
		['1st']='#FFD700', ['2nd']='#C0C0C0', ['3rd']='#CC9966'
	}
	
local legend_symbols = {
	W='W', D='D', L='L', B='B', O='W/O'
}

local function isnotempty(s)
	return s and s:match( '^%s*(.-)%s*$' ) ~= ''
end

local function zeropad(n)
	if n>=0 and n < 10 then
		return '00' .. n
	end
	if n>=0 and n < 100 then
		return '0' .. n
	end
	return '' .. n
end

local function pad_key(k)
	-- Zero pad, fix ranges and dashes
	if k then
		k = k .. ' '
		k = mw.ustring.gsub(k, '–', '-')
		k = mw.ustring.gsub(k, '_([%d][^%d])', '_0%1')
		k = mw.ustring.gsub(k, '%-([%d][^%d])', '-0%1')
		k = mw.ustring.gsub(k, '_([%d][%d][^%d])', '_0%1')
		k = mw.ustring.gsub(k, '%-([%d][%d][^%d])', '-0%1')
		k = mw.ustring.gsub(k, '([^%d])%-([%d])', '%1000-%2')
		k = mw.ustring.gsub(k, '([%d])%-%s*$', '%1-999')
		k = mw.ustring.gsub(k, '^%s*(.-)%s*$', '%1')
	end

	return k
end

local function matches_date(text, m, d)
	return mw.ustring.gsub(mw.ustring.gsub(text .. '', '<matches>', m), '<date>', d)
end

local function get_color(p)
	local c = colorlist[p] or colorlist[zeropad(tonumber(p) or -1)]
	if c then
		return color_map[c] or c
	end
	p = tonumber(p or '0') or 0
	if p <= 0 then
		return nil
	end
	-- ranges in order of specificity
	local offset1, offset2 = 999, 999
	for k,v in pairs( colorlist ) do
		local r1 = tostring(k):match( '^%s*([%d]+)%-[%d]+%s*$' )
		local r2 = tostring(k):match( '^%s*[%d]+%-([%d]+)%s*$' )
		if r1 and r2 then
			r1 = tonumber(r1)
			r2 = tonumber(r2)
			if (r1 <= p) and (r2 >= p) then
				if (c == nil) or ((p - r1) <= offset1 and (r2 - p) <= offset2) then
					c = color_map[v] or v
					offset1 = p - r1
					offset2 = r2 - p
				end
			end
		end
	end
	return c
end	

function p.table(frame)
	local getArgs = require('Module:Arguments').getArgs
	local yesno = require('Module:Yesno')
	args = getArgs(frame, {wrappers = {'Template:Sports rbr table'}})
	local rounds = tonumber(args['rounds'] or '0') or 0
	local firstround = tonumber(args['firstround'] or 1) or 1
	local sortable = yesno(args['sortable'] or 'no')
	local updated = args['updated'] or args['update']
	local source = args['source']
	local notes = args['notes']
	local addlegend = false
	local legendpos = (args['legendpos'] or 'tr'):lower()
	local header, footer = '', ''
	
	-- Lowercase two labels --
	labels['complete'] = string.lower(labels['complete'])
	labels['future'] = string.lower(labels['future'])
	
	-- Adjust rounds
	rounds = rounds - (firstround - 1)
	
	-- Require a source
	-- source = source or frame:expandTemplate{ title = 'citation needed', args = { reason='No source parameter defined', date=os.date('%B %Y') } }
	
	-- Process team, pos, and color args
	local team_list = {}
	local maxrounds = 0
	for k, v in pairs( args ) do
		-- Preprocess ranges
		if tostring(k):match( '^%s*text_?(.-)%s*$' ) then
			k = pad_key(k)
		end
		if tostring(k):match( '^%s*colou?r_?(.-)%s*$' ) then
			k = pad_key(k)
		end
		
		-- Create the list of teams and count rounds
		local i = tonumber(
				tostring(k):match( '^%s*team([%d]+)%s*$' ) or 
				tostring(k):match( '^%s*label([%d]+)%s*$' ) or '0'
				)
		if ( i > 0 and isnotempty(v) ) then
			table.insert( team_list, i)
			local p = args['pos' .. i] or args['res' .. i] or ''
			if args['name_' .. v] then
				local t = args['team' .. i] or args['label' .. i] or ''
				p = args['pos_' .. t] or args['res_' .. t] or ''
			end
			local pos = mw.text.split(p, '%s*[/~]%s*')
			maxrounds = (#pos > maxrounds) and #pos or maxrounds
		end
		-- Create the list of colors
		local s = tostring(k):match( '^%s*colou?r_?(.-)%s*$' )
		if ( s and isnotempty(v) ) then
			colorlist[s] = v:lower()
		end
		-- Check if we are adding a legend
		s = tostring(k):match( '^%s*text_?(.-)%s*$' )
		if ( s and isnotempty(v) ) then
			textlist[s] = v
			addlegend = true
		end
	end
	maxrounds = (rounds > maxrounds) and rounds or maxrounds
	addlegend = yesno(args['legend'] or (addlegend and 'yes' or 'no'))
	
	-- sort the teams
	table.sort(team_list)

	local fs = 95
	if ((maxrounds - firstround) > 37 ) then
		fs = fs - 2*(maxrounds - firstround - 37)
	end

	-- Build the table
	local root = mw.html.create('table')
	root:addClass('wikitable')
	root:addClass(sortable and 'sortable' or nil)
	root:css('font-size', fs .. '%')
	root:css('text-align', 'center')
	
	if args['title'] then
		root:tag('caption'):wikitext(args['title'])
	end
	
	-- Heading row
	local row = root:tag('tr')
	row:tag('th')
		:attr('rowspan', args['sortable'] and 2 or nil)
		:wikitext(args['header'] or labels['teamround'])
	for r=1,maxrounds do
		row:tag('th')
			:css('width', '15px')
			:css('border-bottom', args['sortable'] and 'none' or nil)
			:wikitext(args['round' .. (r + (firstround - 1)) .. '_label'] 
				or (r + (firstround - 1)))
	end
	if args['sortable'] then
		row = root:tag('tr')
		for r=1,maxrounds do
			row:tag('th')
				:css('height', '1.2ex')
				:css('border-top', 'none')
		end
	end
	
	-- Team positions
	for k=1,#team_list do
		local i = team_list[k]
		local t = args['team' .. i] or args['label' .. i] or ''
		local p = args['pos' .. i] or args['res' .. i] or ''
		if args['name_' .. t] then
			p = args['pos_' .. t] or args['res_' .. t] or ''
			t = args['name_' .. t]
		end
		row = root:tag('tr')
		row:tag('td'):css('text-align', 'left'):wikitext(t)
		local pos = mw.text.split(p, '%s*[/~]%s*')
		for r=1,maxrounds do
			s = args['team' .. i .. '_round' .. r .. '_' .. 'color'] or 
				args['team' .. i .. '_round' .. r .. '_' .. 'colour']
			row:tag('td')
				:css('background-color', (s and colorlist[s]) or s or get_color(pos[r]))
				:wikitext(legend_symbols[pos[r]] or pos[r])
		end
	end

	-- build the legend
	if addlegend then
		-- Sort the keys for the legend
		legendkeys = {}
		for k,v in pairs( textlist ) do
			table.insert(legendkeys, k)
		end
		table.sort(legendkeys)
		
		if args['legendorder'] then
			legendkeys = mw.text.split(args['legendorder'] .. '/' .. table.concat(legendkeys, '/'), '%s*[/~]%s*')
		end
		
		local lroot = mw.html.create('table')
		if legendpos == 'tl' or legendpos == 'bl' then
			lroot:addClass('wikitable')
			lroot:css('font-size', '88%')
		else
			lroot:addClass('infobox')
			lroot:addClass('bordered')
			-- lroot:css('width', 'auto')
		end
		for k,v in pairs( legendkeys ) do
			if v and textlist[v] then
				local c = colorlist[v] or ''
				local row = (legendpos == 'tl' or legendpos == 'bl') and lroot or lroot:tag('tr')
				local l = row:tag('th'):css('background-color', color_map[c] or c)
				if legend_symbols[v] then
					l:css('font-weight', 'normal')
						:css('padding', '1px 3px')
						:wikitext(legend_symbols[v])
				else
					l:css('width', '10px')
				end
				row:tag('td')
					:css('padding', '1px 3px')
					:wikitext(textlist[v])
				textlist[v] = nil
			end
		end
		if (legendpos == 'bl' or legendpos == 'br') then
			footer = footer .. tostring(lroot)
		else
			header = header .. tostring(lroot)
		end
	end

	-- simplify updated == complete case
	local lupdated = updated and string.lower(updated) or ''
	if lupdated == labels['complete'] or lupdated == 'complete' then
		lupdated = ''
	end
	
	-- build the footer	
	if notes or source or lupdated ~= '' then
		footer = footer .. frame:expandTemplate{ title = 'refbegin' }
		if lupdated ~= '' then
			local mtext = args['matches_text'] or labels['matches']
			if lupdated == labels['future'] or lupdated == 'future' then
				footer = footer .. matches_date(labels['firstplayed'] .. ' ', 
					mtext, args['start_date'] or labels['futuredate'])
			else
				footer = footer .. matches_date(labels['updatedto'] .. ' ', 
					mtext, updated)
			end
		end
		if source then
			footer = footer .. labels['source'] .. ' ' .. source
		end
		if notes then
			if lupdated ~= '' or source then
				footer = footer .. '<br>'
			end
			footer = footer .. labels['notes'] .. ' ' .. notes
		end
		footer = footer .. frame:expandTemplate{ title = 'refend' } 
	end
	-- add clear right for the legend if necessary
	footer = footer .. ((addlegend and (legendpos == 'bl' or legendpos == 'br')) 
		and '<div style="clear:right"></div>' or '')
	return header .. (args['toptext'] or '') .. tostring(root) .. footer
end

return p