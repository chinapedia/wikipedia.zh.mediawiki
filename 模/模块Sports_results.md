-- Module to build results cross-tables for standings in Sports
-- See documentation for details
 
require('Module:No globals')

local p = {}
 
-- Main function
function p.main(frame)
	-- Declare locals
	local Args = frame.args
	local N_teams = 0
	local t = {}
	local t_footer = {}
	local t_return = {}
	local team_list = {}
	local ii, ii_fw, bg_col, team_name, team_code_ii
	
	-- Edit links if requested
	local template_name = Args['template_name'] or ''
	local edit_links = template_name == '' and '' 
		or frame:expandTemplate{ title = 'navbar', 
			args = { mini=1, style='float:right', template_name} }
	
	-- Load some other modules
	local p_sub = require('Module:Sports table/sub')
	
	-- Read in number of consecutive teams (ignore entries after skipping a spot)
	while Args['team'..N_teams+1] ~= nil do
		N_teams = N_teams+1
		-- Sneakily add it twice to the team_list parameter, once for the actual
		-- ranking, the second for position lookup in sub-tables
		-- This is possible because Lua allows both numbers and strings as indices.
		team_list[N_teams] = Args['team'..N_teams] -- i^th entry is team X
		team_list[Args['team'..N_teams]] = N_teams -- team X entry is position i
	end
	
	-- Get team to show
	local ii_show = team_list[Args['showteam']] -- nil if non-existant
	
	-- Create header
	-- Open table
	table.insert(t,'{|class="wikitable plainrowheaders" style="text-align:center;"\n') 
	-- First column
	t_return.count = 0 			-- Dummy parameter, using subfunction call seems best at this point because both module are intertwined
	t_return.tab_text = t		-- Actual text
	t_return = p_sub.colhead(t_return,'auto', edit_links .. ' 主隊 \\ 客隊')	
	-- Other columns passed to subfunction
	t_return = p.header(t_return,Args,p_sub,N_teams,team_list)
	t = t_return.tab_text
	
	-- Now create individual rows
	for ii=1,N_teams do
		-- Get team info
		team_code_ii = team_list[ii]
		team_name = Args['name_'..team_code_ii]		 	or team_code_ii
		local ii_style = 'text-align:right;'
		if ii and ii == ii_show then
			ii_style = ii_style .. 'font-weight:bold;'
		end
		-- Team names
		table.insert(t,'|- \n')	-- New row
		table.insert(t,'! scope="row" style="' 
			.. ii_style ..'"| '..team_name..'\n')	-- Position number
		
		-- Then individual results
		t = p.row(t,Args,N_teams,team_list,ii,ii_show)
	end
	
	-- Close table
	table.insert(t, '|}\n')
	
	-- Get info for footer
	local update = Args['update']			or 'unknown'
	local start_date = Args['start_date'] 	or 'unknown'
	local source = Args['source']			or frame:expandTemplate{ title = 'citation needed', args = { reason='No source parameter defined', date=os.date('%B %Y') } }
	
	-- Create footer text
	-- Date updating
	if string.lower(update)=='complete' then
		-- Do nothing
	elseif update=='' then
		-- Empty parameter
		table.insert(t_footer,'Updated to match(es) played on unknown. ')
	elseif string.lower(update)=='future' then
		-- Future start date
		table.insert(t_footer,'首場比賽會於'..start_date..'舉行。 ')
	else
		table.insert(t_footer,'比賽更新至'..update..'. ')
	end
	table.insert(t_footer,'來源：'..source)
	if (Args['matches_style'] or '') == 'FBR' then
		table.insert(t_footer, '<br>顏色：綠色 = 主隊勝 ； 黃色 = 賽和 ； 紅色 = 客隊勝。')
	end
	if (Args['a_note'] or '') ~= '' then
		table.insert(t_footer, '<br>未來的賽事欄位若顯示a，表示有該比賽的相關維基條目。')
	end
	-- As reflist size text
	t_footer = '<div class="reflist">'..table.concat(t_footer)..'</div>'
	-- Add footer to main text table
	table.insert(t,t_footer)
	
	return table.concat(t)
end

-- Other functions
local function get_short_name(s, t, n)
	-- return short name if defined
	if s and s ~= '' then 
		return s 
	end
	-- replace link text in name with team abbr if possible
	if n and t and n:match('(%[%[[^%[%|^%[%]]*%]%])') then
		n = mw.ustring.gsub(n, '(%[%[[^%|%]]*%|)[^%|%]]*(%]%])', '%1' .. t .. '%2')
		n = mw.ustring.gsub(n, '(%[%[[^%|%]]*)(%]%])', '%1|' .. t .. '%2')
		return n
	end
	-- nothing worked, so just return the unlinked team abbr
	return t or ''
end

local function get_score_background(s)
	local s1, s2
	-- Define the colouring
	local wc, lc, tc = '#CCFFCC', '#FFCCCC', '#FFFFCC'

	-- delink if necessary	
	if s:match('^%s*%[%[[^%[%|^%[%]]*%|([^%[%]]*)%]%]') then
		s = s:match('^%s*%[%[[^%[%|^%[%]]*%|([^%[%]]*)%]%]')
	end

	-- get the scores
	s1 = tonumber(mw.ustring.gsub( s or '', 
		'^%s*([%d][%d]*)%s*–%s*([%d][%d]*).*', '%1' ) or '') or ''
	s2 = tonumber(mw.ustring.gsub( s or '', 
		'^%s*([%d][%d]*)%s*–%s*([%d][%d]*).*', '%2' ) or '') or ''
	
	-- return colouring if possible
	if s1 ~= '' and s2 ~= '' then
		return (s1 > s2) and wc or ((s2 > s1) and lc or tc)
	else
		return 'transparent'
	end
end

local function format_score(s)
	s = mw.ustring.gsub(s or '', '^%s*([%d]+)%s*[–−—%-]%s*([%d]+)', '%1–%2')
	s = mw.ustring.gsub(s, '^%s*([%d]+)%s*&[MmNn][Dd][Aa][Ss][Hh];%s*([%d]+)', '%1–%2')
	s = mw.ustring.gsub(s, '^%s*(%[%[[^%[%|^%[%]]*%|[%d]+)%s*%-%s*([%d]+)', '%1–%2')
	s = mw.ustring.gsub(s, '^%s*(%[%[[^%[%|^%[%]]*%|[%d]+)%s*&[MmNn][Dd][Aa][Ss][Hh];%s*([%d]+)', '%1–%2')
	return s
end

function p.header(tt,Args,p_sub,N_teams,team_list)
	local ii, team_code_ii, short_name
	
	-- Set match column width
	local col_width = Args['match_col_width'] or '28'
	
	-- Get some default values in case it doesn't start at 1
	local top_pos = tonumber(Args['highest_pos']) or 1
	
	for ii=top_pos,N_teams do
		team_code_ii = team_list[ii]
		short_name = get_short_name(Args['short_'..team_code_ii], 
			team_code_ii, Args['name_'..team_code_ii])
		tt = p_sub.colhead(tt,col_width,short_name)
	end
	
	return tt
end

function p.row(tt,Args,N_teams,team_list,ii,ii_show)
	-- Note ii is the row number being shown
	local jj, fw, bg, result, team_code_ii, team_code_jj
	local cell_bold = false
	
	-- Set score cell style
	local matches_style = Args['matches_style'] or ''
	
	team_code_ii = team_list[ii]
	
	-- Get some default values in case it doesn't start at 1
	local top_pos = tonumber(Args['highest_pos']) or 1
	
	for jj=top_pos,N_teams do
		if ii == jj then
			-- Solid cell
			if ii==ii_show then cell_bold = true else cell_bold = false end
			fw = cell_bold and 'font-weight: bold;' or 'font-weight: normal;'
			bg = 'background-color:transparent;'
			table.insert(tt,'| style="'..fw..bg..'" | —\n')
		else
			-- Content cell
			-- Set bolding and background
			if ii==ii_show or jj == ii_show then cell_bold = true else cell_bold = false end
			fw = cell_bold and 'font-weight: bold;' or 'font-weight: normal;'
			bg = 'background-color:transparent;'
			
			-- Now for the actual result
			team_code_jj = team_list[jj]
			result = Args['match_'..team_code_ii..'_'..team_code_jj] or ''
			-- Reformat dashes
			if result ~= '' then
				result = format_score(result)
			end
			-- Background coloring if enabled
			if matches_style == 'FBR' and result ~= '' then
				bg = 'background-color:' .. get_score_background(result) .. ';'
			end
			table.insert(tt,'| style="white-space:nowrap;'..fw..bg..'" |'..result..'\n')
		end
	end
	
	return tt
end

return p