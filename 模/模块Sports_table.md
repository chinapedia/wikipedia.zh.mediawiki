-- Module to build tables for standings in Sports
-- See documentation for details

require('Module:No globals')

local p = {}

-- Helper functions
local function isnotblank(s)
	return s and s:match( '^%s*(.-)%s*$' ) ~= ''
end

local function firstnonblank(s1,s2)
	if ( s1 and s1:match( '^%s*(.-)%s*$' ) ~= '' ) then
		return s1
	elseif ( s2 and s2:match( '^%s*(.-)%s*$' ) ~= '' ) then
		return s2
	end
	return nil
end
 
-- Main function
function p.main(frame)
	-- Declare locals
	local Args = frame.args
	local Pargs = frame:getParent().args
	local ii_start, ii_end, N_rows_res = 0
	local text_field_result
	local notes_exist = false
	local t = {}
	local t_footer = {}
	local t_return = {}
	local team_list = {}
	local jj, jjj
	
	-- Exit early if we are using section transclusion for a different section
	if( isnotblank(Pargs['transcludesection']) and isnotblank(Args['section']) ) then
		if( Pargs['transcludesection'] ~= Args['section'] ) then
			return ''
		end
	end

	-- Get the custom start point for the table (most will start by default at 1
	local top_pos = tonumber(Args['highest_pos']) or 1
	local N_teams = top_pos - 1 -- Default to 0 at start, but higher number needed to skip certain entries
	
	-- Load modules
	local yesno = require('Module:Yesno')
	-- Load style and (sub) modules
	local style_def = Args['style'] or 'WDL'
	-- Historically 'football' exists as style, this is now forwarded to WDL
	if style_def == 'football' then style_def = 'WDL' end
	local p_style = require('Module:Sports table/'..style_def)
	local p_sub = require('Module:Sports table/sub')
	
	-- Random value used for uniqueness
	math.randomseed( os.clock() * 10^8 )
	local rand_val = math.random()
	
	-- Declare colour scheme
	local result_col = {}
	result_col = {green1='#BBF3BB', green2='#CCF9CC', green3='#DDFCDD', green4='#EEFFEE',
		blue1='#BBF3FF', blue2='#CCF9FF', blue3='#DDFCFF', blue4='#EEFFFF',
		yellow1='#FFFFBB', yellow2='#FFFFCC', yellow3='#FFFFDD', yellow4='#FFFFEE',
		red1='#FFBBBB', red2='#FFCCCC', red3='#FFDDDD', red4='#FFEEEE',
		black1='#BBBBBB', black2='#CCCCCC', black3='#DDDDDD', black4='#EEEEEE'}
	
	-- Declare results column header
	local results_header = {}
	results_header = {Q='出線資格', QR='出線 或 降級',
		P='升級', PQR='出線，升級 或 降級',
		PR='升級 或 降級', R='降級', FR='最終成績'}
	local results_defined = false -- Check whether this would be needed
	-- Now define line for column header (either option or custom)
	local local_res_header = results_header[Args['res_col_header']] or Args['res_col_header']  or ''
	-- Check whether it includes a note
	local res_head_note = Args['note_header_res']
	local res_head_note_text = ''
	if res_head_note then
		notes_exist = true
		res_head_note_text = frame:expandTemplate{ title = 'efn', args = { group='Table_notes',  res_head_note} }
	end
	local results_header_txt = '! scope="col" |'..local_res_header..res_head_note_text..'\n'
	
	-- Get status option
	local t_status = p_style.status(Args)
	
	-- Read in number of consecutive teams (ignore entries after skipping a spot)
	while Args['team'..N_teams+1] ~= nil do
		N_teams = N_teams+1
		-- Sneakily add it twice to the team_list parameter, once for the actual
		-- ranking, the second for position lookup in sub-tables
		-- This is possible because Lua allows both numbers and strings as indices.
		team_list[N_teams] = Args['team'..N_teams] -- i^th entry is team X
		team_list[Args['team'..N_teams]] = N_teams -- team X entry is position i
	end
	
	-- Show all stats in table or just matches played and points
	local pld_pts_val = firstnonblank(Pargs['only_pld_pts'], Args['only_pld_pts']) or 'no'
	local full_table
	local hide_class_rules = false
	-- True if par doesn't exist, false otherwise
	-- First convert to lower case if it is a string
	pld_pts_val = string.lower(pld_pts_val)
	if yesno(pld_pts_val) then
		full_table = false
	elseif pld_pts_val=='no_hide_class_rules' then
		full_table = true
		hide_class_rules = true
	else
		full_table = true
	end
	
	-- Show groups or note
	local show_groups_val = firstnonblank(Pargs['show_groups'], Args['show_groups']) or 'no'
	local group_col = false
	if yesno(show_groups_val) then group_col = true end
	
	-- Show match_table or not
	local show_matches_val = firstnonblank(Pargs['show_matches'], Args['show_matches']) or 'no'
	local match_table = false
	if yesno(show_matches_val) then match_table = true end
	local p_matches = match_table and require('Module:Sports results')
	
	-- Custom position column label or note
	local pos_label = Args['postitle'] or ''
	if pos_label == '' then
		-- If empty (or undeclared) then default
		pos_label = '<abbr title="Position">Pos</abbr>'
	end

	-- Get VTE button text (but only for non-empty text)
	local template_name = Args['template_name'] or ''
	local VTE_text = ''
	if template_name~='' then
		VTE_text = frame:expandTemplate{ title = 'navbar', args = { mini=1, style='float:right',  template_name} }
	end

	-- Write column headers
	t_return = p_style.header(t,Args,p_sub,pos_label,group_col,VTE_text,full_table,results_header_txt)
	if match_table then
		-- Add empty column header
		t_return.count = t_return.count+1
		table.insert(t_return.tab_text,'! scope="row" class="unsortable" style="background-color:white;border-top:white;border-bottom:white;line-width:3pt;"| \n')
		
		-- Add rest of header
		t_return = p_matches.header(t_return,Args,p_sub,N_teams,team_list)
	end
	t = t_return.tab_text
	local N_cols = t_return.count
	
	-- Determine what entries go into table
	-- Find out which team to show (if any)
	local ii_show = team_list[firstnonblank(Pargs['showteam'], Args['showteam'])] -- nil if non-existant
	-- Start and end positions to show
	local n_to_show = tonumber(Args['show_limit']) or N_teams
	-- Check for "legal value", if not legal (or non declared), then show all
	local check_n = ((n_to_show>=(N_teams-top_pos+1)) or (n_to_show<=1) or (n_to_show~=math.floor(n_to_show)))
	-- Also check whether there is a valid ii_show
	if check_n or (not ii_show) then
		ii_start = top_pos
		ii_end = N_teams
	else
		-- It's a proper integer between top_pos+1 and N_teams-1
		-- If it is in the middle show the same number above and below
		-- If it is in the top or bottom, show the exact number
		-- How many to show on the side
		local n_show_side = math.floor(n_to_show/2)
		if (ii_show-top_pos+1)<=n_show_side then
			-- Top team
			ii_start = top_pos
			ii_end = top_pos+n_to_show-1
		elseif ii_show>=(N_teams+1-n_show_side) then
			-- Bottom team
			ii_start = N_teams+1-n_to_show
			ii_end = N_teams
		else
			-- Normal case
			ii_start = ii_show-n_show_side
			ii_end = ii_show+n_show_side
		end
	end
	
	-- For results column
	local new_res_ii = ii_start
	-- Pre-check for existence of column
	for ii = ii_start, ii_end do
		if Args['result'..ii] then results_defined = true end
	end
	-- Remove results header if it is unused
	if full_table and not results_defined then
		-- First get it as one string, then use string replace to replace that header by empty string
		local t_str = tostring(table.concat(t))
		t_str = mw.ustring.gsub( t_str, results_header_txt, '' )
		N_cols = N_cols-1 -- There is actually one column less
		t = {}
		table.insert(t, t_str)
	end
	
	-- Write rows
	local team_name, team_code_ii, team_code_jj, pos_num, group_txt, note_local
	local note_string, note_local, note_local_num, note_id
	local note_id_list = {}
	local hth_id_list = {}
	for ii = ii_start, ii_end do
		-- First get code
		team_code_ii = team_list[ii]
		-- Now read values
		pos_num = Args['pos_'..team_code_ii]			or ii
		group_txt = Args['group_'..team_code_ii]		or ' '
		team_name = Args['name_'..team_code_ii]		 	or team_code_ii
		note_local = Args['note_'..team_code_ii] 		or nil
		
		-- Does it need a promotion/qualification/relegation tag
		local result_local = Args['result'..ii] or nil
		local bg_col = nil
		-- Get local background colour
		if result_local then
			bg_col = result_col[Args['col_'..result_local]] or Args['col_'..result_local] or 'white'
			bg_col = 'background-color:'..bg_col..';' 	-- Full style tag
		end
		if not bg_col then bg_col = 'background-color:transparent;' end -- Becomes default if undefined
		
		-- Bold this line or not
		local ii_fw = ii == ii_show and 'font-weight: bold;' or 'font-weight: normal;'
		
		-- Check whether there is a note or not, if so get text ready for it
		if note_local and full_table then
			-- Set global check for notes to true
			notes_exist = true
			-- There are now 3 options for notes
			-- 1) It is a full note
			-- 2) It is a referal to another note (i.e. it's just a team code; e.g. note_AAA=Text, note_BBB=AAA) in which the note for BBB should link to the same footnote as AAA, with
			-- 2a) The other linked note exist in the part of the table shown
			-- 2b) The part of the note does not exist in the part of the table shown
			if not Args['note_'..note_local] then
				-- Option 1
				-- Now define the identifier for this
				note_id = '"table_note_'..team_code_ii..rand_val..'"' -- Add random end for unique ID if more tables are present on article (which might otherwise share an ID)
				note_id_list[team_code_ii] = note_id
				
				-- Call refn template
				note_string = frame:expandTemplate{ title = 'efn', args = { group='Table_notes',  name=note_id, note_local} }
			else 
				-- Option 2
				-- It is option 2a in either one if either the main note is inside the sub-table
				--                                  or another ref to that note is inside the sub-table
				-- Basically when it either has been defined, or the main link will be in the table
				note_local_num = team_list[note_local]
				if note_id_list[note_local] or ((note_local_num >= ii_start) and (note_local_num <= ii_end)) then
					-- Option 2a
					note_id = '"table_note_'..note_local..rand_val..'"'
					note_string = frame:extensionTag{ name = 'ref', args = { group = 'lower-alpha', name = note_id} }
				else
					-- Option 2b
					-- Now define the identifier for this
					note_id = '"table_note_'..note_local..rand_val..'"' -- Add random end for unique ID
					note_id_list[note_local] = note_id
					
					-- Call refn template
					note_string = frame:expandTemplate{ title = 'efn', args = { group='Table_notes',  name=note_id, Args['note_'..note_local]} }
				end
			end
		else
			note_string = '';
		end
		
		-- Insert status when needed
		local status_string = ''
		local status_local = Args['status_'..team_code_ii]
		local status_let_first = true
		local curr_letter
		-- Only if it is defined
		if status_local then
			-- Take it letter by letter
			for jjj = 1,mw.ustring.len(status_local) do
				curr_letter = mw.ustring.upper(mw.ustring.sub(status_local,jjj,jjj))
				-- See whether it exist
				if t_status.code[curr_letter] then
					-- Depending on whether it is the first letter of not
					if status_let_first then
						status_string = curr_letter
						t_status.called[curr_letter] = true
						status_let_first = false
					else
						status_string = status_string..', '..curr_letter
						t_status.called[curr_letter] = true
					end
				end
		end
		-- Only add brackets/dash and bolding if it exist
			if not status_let_first then 
				if t_status.position == 'before' then
					status_string = '<span style="font-weight:bold">'..string.lower(status_string)..' –</span> ' 
				else
					status_string = ' <span style="font-weight:bold">('..status_string..')</span>' 
				end
			end
		end
		
		-- Now build the rows
		table.insert(t,'|- \n')																			-- New row
		table.insert(t,'! scope="row" style="text-align: center;'..ii_fw..bg_col..'"| '..pos_num..'\n')	-- Position number
		if full_table and group_col then
			table.insert(t,'| style="'..ii_fw..bg_col..'" |'..group_txt..'\n') 							-- Group number/name
		end
		-- Build the team string order based on status position
		local team_string
		if t_status.position == 'before' then
			team_string = status_string..team_name..note_string
		else
			team_string = team_name..note_string..status_string
		end
		table.insert(t,'| style="text-align: left; white-space:nowrap;'..ii_fw..bg_col..'"| '..team_string..'\n')-- Team (with possible note)
		-- Call to subfunction
		t_return = p_style.row(frame,t,Args,p_sub,notes_exist,hth_id_list,full_table,rand_val,team_list,team_code_ii,ii_start,ii_end,ii_fw,bg_col,N_teams,ii,ii_show)
		t = t_return.t
		notes_exist = t_return.notes_exist
		hth_id_list = t_return.hth_id_list
		
		-- Now check what needs to be added inside the results column
		if full_table then
			local res_jjj
			if ii == new_res_ii then
				-- First check how many rows you need for this
				N_rows_res = 1
				jjj = ii+1
				result_local = Args['result'..ii] or ''
				local cont_loop = true
				while (jjj<=ii_end) and cont_loop do
					if Args['split'..tostring(jjj-1)] then
						cont_loop = false
						new_res_ii = jjj
					else
						res_jjj = Args['result'..jjj] or ''
						if result_local == res_jjj then 
							N_rows_res = N_rows_res+1 
						else
							cont_loop = false
							new_res_ii = jjj
						end
					end
					jjj = jjj+1
				end
				-- Now create this field (reuse ii_fw and bg_col)
				-- Bold (if in range) or not
				if ii_show and (ii_show>=ii) and (ii_show<=(ii+N_rows_res-1)) then
					ii_fw = 'font-weight: bold;'
				else
					ii_fw = 'font-weight: normal;'
				end
				-- Get background colour
				bg_col = nil
				if Args['result'..ii] then
					bg_col = result_col[Args['col_'..result_local]] or Args['col_'..result_local] or 'white'
					bg_col = 'background-color:'..bg_col..';' 	-- Full style tag
				end
				if not bg_col then bg_col = 'background-color:transparent;' end -- Becomes default if undefined
				-- Check for notes
				local note_res_string, note_ref, note_text
				if Args['note_res_'..result_local] then
					notes_exist = true
					local note_res_local = Args['note_res_'..result_local]
					if not Args['note_res_'..note_res_local] then
						-- It does not point to another result note
						note_ref = 'res_'..result_local
						note_id = '"table_note_res_'..result_local..rand_val..'"' -- Identifier
						note_text = note_res_local
					else
						-- It does point to another result note
						note_ref = 'res_'..note_res_local
						note_id = '"table_note_res_'..note_res_local..rand_val..'"' -- Identifier
						note_text = Args['note_res_'..note_res_local]
					end
					-- Check whether it is already printed
					if not note_id_list[note_ref] then
						-- Print it
						note_id_list[note_ref] = note_id
						note_res_string = frame:expandTemplate{ title = 'efn', args = { group='Table_notes',  name=note_id, note_text} }
					else
						-- Refer to it
						note_res_string = frame:extensionTag{ name = 'ref', args = { group = 'lower-alpha', name = note_id} }
					end
				else
					note_res_string = ''
				end
				-- Get text
				local text_result = Args['text_'..result_local] or ''
				text_field_result = '| style="'..ii_fw..bg_col..'" rowspan="'..tostring(N_rows_res)..'" |'..text_result..note_res_string..'\n'
				-- See whether it is needed (only when blank for all entries)
				if results_defined then table.insert(t,text_field_result) end
			end
		end
	
		-- Insert match row if needed
		if match_table then
			-- Add empty cell
			table.insert(t,'| style="background-color:white;border-top:white;border-bottom:white;"| \n')
			
			-- Now include note to match results if needed 
			for jj=top_pos,N_teams do
				team_code_jj = team_list[jj]
				if ii == jj then
					-- Nothing
				else
					local match_note = Args['match_'..team_code_ii..'_'..team_code_jj..'_note']
					if match_note then
						notes_exist = true
						-- Only when it exist
						-- First check for existence of reference for note
						if not (Args['note_'..match_note] or Args['match_'..match_note..'_note']) then
							-- It's the entry
							note_id = '"table_note_'..team_code_ii..'_'..team_code_jj..rand_val..'"' -- Add random end for unique ID if more tables are present on article (which might otherwise share an ID)
							note_id_list[team_code_ii..'_'..team_code_jj] = note_id
							
							note_string = frame:expandTemplate{ title = 'efn', args = { group='Table_notes', name=note_id,  match_note} }
						else 
							-- Check for existence elsewhere
							note_local_num = team_list[match_note] or ii_end + 1
							if note_id_list[match_note] or ((note_local_num >= ii_start) and (note_local_num <= ii_end)) then
								-- It exists
								note_id = '"table_note_'..match_note..rand_val..'"' -- Identifier
								note_string = frame:extensionTag{ name = 'ref', args = { group = 'lower-alpha', name = note_id} }
							else
								-- Now define the identifier for this
								note_id = '"table_note_'..match_note..rand_val..'"' -- Add random end for unique ID
								note_id_list[match_note] = note_id
								-- Call refn template
								note_string = frame:expandTemplate{ title = 'efn', args = { group='Table_notes', name=note_id, Args['note_'..match_note]} }
							end
						end

						-- Now append this to the match result string
						Args['match_'..team_code_ii..'_'..team_code_jj] = Args['match_'..team_code_ii..'_'..team_code_jj]..note_string
					end
				end
			end
			
			-- Add rest of match row
			t = p_matches.row(t,Args,N_teams,team_list,ii,ii_show)
		end
	
		-- Now, if needed, insert a split (solid line to indicate split in standings, but only when it is not at the last shown position)
		if Args['split'..ii] and (ii<ii_end) then
			-- Base size on N_cols (it needs 2*N_cols |)
			table.insert(t,'|- style="background-color:'..result_col['black1']..'; line-height:3pt;"\n')
			table.insert(t,string.rep('|',2*N_cols)..'\n')
		end
	end
	
	-- Close table
	table.insert(t, '|}\n')
	
	-- Get info for footer
	local update = Args['update']			or 'unknown'
	local start_date = Args['start_date'] 	or 'unknown'
	local source = Args['source']			or frame:expandTemplate{ title = 'citation needed', args = { reason='No source parameter defined', date=os.date('%B %Y') } }
	local class_rules = Args['class_rules']	or nil
	
	-- Create footer text
	-- Date updating
	local matches_text = Args['matches_text'] or 'match(es)'
	if string.lower(update)=='complete' then
		-- Do nothing
	elseif update=='' then
		-- Empty parameter
		table.insert(t_footer,' '..matches_text..' played on unknown. ')
	elseif string.lower(update)=='future' then
		-- Future start date
		table.insert(t_footer,'首場比賽將於'..start_date..'開始。 ')
	else
		table.insert(t_footer,'比賽更新至'..update..'結果。 ')
	end
	
	-- Stack footer or not
	local stack_footer_val = firstnonblank(Pargs['stack_footer'], Args['stack_footer']) or 'no'
	local footer_break = false
	if yesno(stack_footer_val) then footer_break = true end
	
	-- Variable for linebreak
	local stack_string = '<br>'
	
	if footer_break and (not (string.lower(update)=='complete')) then table.insert(t_footer,stack_string) end
	
	table.insert(t_footer,'資料來源：'..source)
	if class_rules and full_table and (not hide_class_rules) then
		table.insert(t_footer,'<br>排名規則順序：'..class_rules)
	end
	
	-- Now for the named status
	local status_exist = false
	local status_string = ''
	local curr_letter
	for jjj = 1,mw.ustring.len(t_status.letters) do
		curr_letter = mw.ustring.upper(mw.ustring.sub(t_status.letters,jjj,jjj))
		if t_status.called[curr_letter] then
			if (footer_break and status_exist) then
				status_string = status_string..stack_string
			end
			if t_status.position == 'before' then
				status_string = status_string..'<span style="font-weight:bold">'..string.lower(curr_letter)..' –</span> '..t_status.code[curr_letter]..'; '
			else
				status_string = status_string..'<span style="font-weight:bold">('..curr_letter..')</span> '..t_status.code[curr_letter]..'; '
			end
			status_exist = true
		end
	end
	-- Now end it with a point instead (if it contains entries the '; ' needs to be removed)
	if status_exist then
		status_string = '<br>'..mw.ustring.sub(status_string,1,mw.ustring.len(status_string)-2)..'.'
		table.insert(t_footer,status_string)
	end
	-- Add notes (if applicable)
	if notes_exist then
		table.insert(t_footer,'<br>注譯：')
		-- As reflist size text
		t_footer = '<div class="reflist">'..table.concat(t_footer)..'</div>'
		t_footer = t_footer..frame:expandTemplate{ title = 'notelist', args = { group='Table_notes'} }
	else
		-- As reflist size text
		t_footer = '<div class="reflist">'..table.concat(t_footer)..'</div>'
	end
	-- Add footer to main text table
	table.insert(t,t_footer)
	
	return table.concat(t)
end
 
return p