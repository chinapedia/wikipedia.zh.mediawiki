-- This module implements {{sports rivalry series table}}
local p = {}
local root = nil
local lang =mw.getContentLanguage()

local function formatnumR(num)
	num = mw.ustring.gsub(num, '^[^%d]*([%d,%.]-)[^%d]*$', '%1')
	return lang:parseFormattedNumber(num)
end

local function isnotempty(s)
	return s and s:match( '^%s*(.-)%s*$' ) ~= ''
end
local function addheader(header1, header2, series_summary, compact, winner_only, 
	compact_score, nonumber, nolocation, trophy_series, notes, notes_label,
	date_width, location_width)
	-- create the header row
	local row = root:tag('tr')
	if(not nonumber) then
		row:tag('th'):wikitext('No.')
	end
	row:tag('th'):css('width', date_width):wikitext('Date')
	if(not nolocation) then
		row:tag('th'):css('width', location_width):wikitext('Location')
	end
	if((not compact) and (not winner_only) and (not compact_score)) then
		row:tag('th'):attr('colspan', 2):wikitext(header1 or 'Winning team')
		row:tag('th'):attr('colspan', 2):wikitext(header2 or 'Losing team')
		if(not series_summary) then
			row:tag('th'):wikitext('Series')
		end
	else
		if compact_score then
			row:tag('th'):wikitext(header1 or 'Winning team')
			row:tag('th'):wikitext(header2 or 'Losing team')
		else	
			row:tag('th'):wikitext(header1 or 'Winner')
		end
		row:tag('th'):wikitext('Score')
		if( (winner_only or compact_score) and (not series_summary)) then
			row:tag('th'):wikitext('Series')
		end
	end
	if(trophy_series) then
		row:tag('th'):wikitext('Trophy series')
	end
	if(notes) then
		row:tag('th'):wikitext(notes_label)
	end  
end

local function series_text(team1name, team1wins, team2name, team2wins, ties, leads)
	local res = ''
	local t1 = mw.ustring.gsub(team1name, '%s*/.*', '')
	local t2 = mw.ustring.gsub(team2name, '%s*/.*', '')
	if (team1wins > team2wins) then
		res = t1 .. ' ' .. (leads and 'leads ' or '') .. team1wins .. '–' .. team2wins .. ( (ties > 0) and '–' .. ties or '')
	elseif (team2wins > team1wins) then
		res = t2 .. ' ' .. (leads and 'leads ' or '') .. team2wins .. '–' .. team1wins .. ( (ties > 0) and '–' .. ties or '')
	else
		res = 'Tied ' .. team1wins .. '–' .. team2wins .. ( (ties > 0) and '–' .. ties or '') 
	end
	return res
end

local function small_rank(team)
	team = mw.ustring.gsub(team or '', '(%(.-%))', '<small style="font-size:85%; font-weight:normal;">%1</small>')
	team = mw.ustring.gsub(team or '', '([Nn]o%.%s*[0-9][0-9]*)', '<small style="font-size:85%; font-weight:normal;">%1</small>')
	team = mw.ustring.gsub(team or '', '#([0-9][0-9]*%s*)([A-Z%)])', '<abbr title="Number">#</abbr>%1%2')
	team = mw.ustring.gsub(team or '', '(<abbr[^<>]*>[^<>]*</abbr>%s*[0-9][0-9]*)', '<small style="font-size:85%; font-weight:normal;">%1</small>')
	team = mw.ustring.gsub(team or '', '(<small[^<>]*>%()<small[^<>]*>(.-)</small>(%)</small>)', '%1%2%3')
	return team
end

local function get_name(team)
	team = mw.text.trim(team or '')
	team = mw.ustring.gsub(team, '%[%[[^%[%]|]*|(.-)%]%]', '%1')
	team = mw.ustring.gsub(team, '%([^%(%)]*%)', '')
	team = mw.ustring.gsub(team, '<abbr[^<>]*>[^<>]*</abbr>', '')
	team = mw.ustring.gsub(team, '^[Nn]o%.%s*[0-9][0-9]*', '')
	team = mw.ustring.gsub(team, '^[^A-Za-z%.]*(.-)[^A-Za-z%.]*$', '%1')
	return team
end

local function ismultiequal(s1, s2)
	for k1, a1 in pairs( mw.text.split(s1, '[%s]/[%s]') ) do
		for k2, a2 in pairs( mw.text.split(s2, '[%s]/[%s]') ) do
			if a1 == a2 then
				return 1
			end
		end
	end
	return nil
end
	
function p.table(frame)
	local args = (frame.args[3] ~= nil) and frame.args or frame:getParent().args
	local compact = (args['format'] or ''):lower() == 'compact'
	local winner_only = (args['format'] or ''):lower() == 'winner only'
	local compact_score = (args['format'] or ''):lower() == 'compact score'
	local no_number = isnotempty(args['no_number'])
	local no_location = isnotempty(args['no_location'])
	local notes = isnotempty(args['notes']) or isnotempty(args['notes_label'])
	local notes_label = isnotempty(args['notes_label']) and args['notes_label'] or 'Notes'
	local team1style = args['team1style'] or ''
	local team1name = mw.text.trim(args['team1'] or '')
	local team1abbr = isnotempty(args['team1abbr']) and mw.text.trim(args['team1abbr'] or '') or team1name
	local team2style = args['team2style'] or ''
	local team2name = mw.text.trim(args['team2'] or '')
	local team2abbr = isnotempty(args['team2abbr']) and mw.text.trim(args['team2abbr'] or '') or team2name
	local team1wins = tonumber(args['team1win_start']) or 0
	local team2wins = tonumber(args['team2win_start']) or 0
	local ties = tonumber(args['tie_start']) or 0
	local series_summary = isnotempty(args['series_summary'])
	local legend = (args['legend'] and args['legend'] ~= 'no') or (args['legend'] == nil)
	local cols = tonumber(args['cols'] or '') or 0
	local tiestyle = args['tiestyle'] or 'background-color:#DDD; color:#000;'
	local nowinstyle = args['nowinstyle'] or ''
	local number_start = tonumber(args['number_start'] or '1') or 1
	local tseries_start = tonumber(args['trophy_series_start'] or '0') or 0
	local tseries_end = tonumber(args['trophy_series_end'] or '0') or 0
	local tsteam1wins = 0
	local tsteam2wins = 0
	local tsties = 0
	
	local res = ''
	local topres = ''
 
	if (cols < 1 ) then cols = 1 end

	-- compute the maximum cell index
	local cellcount = 0
	for k, v in pairs( args ) do
		if type( k ) == 'number' then
			cellcount = math.max(cellcount, k)
		end
	end
	-- datacols
	local datacols = 6
	if notes then datacols = datacols + 1 end
	if no_location then datacols = datacols - 1 end
	
	-- dataoffsets
	local doffsets = no_location 
		and { ['date'] = 1, ['t1'] = 2, ['s1'] = 3, ['t2'] = 4, ['s2'] = 5, ['note'] = 6}
		or { ['date'] = 1, ['loc'] = 2, ['t1'] = 3, ['s1'] = 4, ['t2'] = 5, ['s2'] = 6, ['note'] = 7}
	
	-- compute the number of rows
	local rows = math.ceil(cellcount / datacols)
	
	-- compute the number of rows per column
	local totalrows = rows
	if (series_summary ) then totalrows = totalrows + 1 end
	if (isnotempty(args['note'])) then totalrows = totalrows + 1 end
	local percol = math.ceil( totalrows / cols )

	if( (tseries_start > 0) or (tseries_end > 0) ) then
		if( tseries_start < 1 ) then
			tseries_start = 1
		end
		if( tseries_end < 1 ) then
			tseries_end = rows
		end
	end

	-- generate the legend
	if( legend ) then
		local legendtable = mw.html.create('table')
		local col3 = args['legend_tie_text'] or 'Tie games'
		local col4 = args['legend_forfeit_text'] or ''
		local lcc = 2
		if isnotempty(col3) then lcc = lcc + 1 else col3 = nil end
		if isnotempty(col4) then lcc = lcc + 1 else col4 = nil end
		local w12 = math.floor(100/lcc + 0.5)
		local w34 = 0
		if lcc > 2 then w34 = (100 - 2*w12)/(lcc - 2) end
		legendtable
			:addClass('wikitable')
			:css('text-align', 'center')
			:css('font-size', '90%')
			:css('white-space', 'nowrap')
			:cssText(args['style'])
		local lrow = legendtable:tag('tr')
		local t1 = mw.ustring.gsub(team1name, '%s*/.*', '')
		local t2 = mw.ustring.gsub(team2name, '%s*/.*', '')
		lrow:tag('td')
			:cssText(team1style)
			:css('font-weight', 'bold')
			:css('width', w12 .. '%')
			:wikitext(t1 .. ' 勝場')
		lrow:tag('td')
			:cssText(team2style)
			:css('font-weight', 'bold')
			:css('width', w12 .. '%')
			:wikitext(t2 .. ' 勝場')
		if( col3 ) then
			lrow:tag('td')
				:cssText(tiestyle)
				:css('width', w34 .. '%')
				:wikitext(col3)
		end
		if( col4 ) then
			lrow:tag('td')
				:css('width', w34 .. '%')
				:wikitext(col4)
		end
		topres = topres .. tostring(legendtable)
	end

	-- build the table content
	for j=1,rows do
		if(math.fmod(j - 1, percol) == 0 ) then
			-- create the root table
			res = res .. (root and tostring(root) or '')
			root = mw.html.create('table')
			root:addClass('wikitable')
			root:css('text-align', 'center')
				:css('font-size', '90%')
			root:cssText(args['style'])
			if(cols > 1) then
				root:css('float', 'left')
				root:css('margin-right', '1em')
			end
			addheader(args['header1'], args['header2'], series_summary, 
				compact, winner_only, compact_score, no_number, no_location, 
				(tseries_start > 0), notes, notes_label,
				args['date_width'], args['location_width'])
		end
		-- start a new row
		row = root:tag('tr')
		row:css('vertical-align', 'top')
		-- Number
		if (not no_number) then row:tag('td'):wikitext(j - 1 + number_start) end
		-- Date
		row:tag('td'):wikitext(args[datacols*(j-1)+doffsets['date']] or '')
		-- Location
		if(not no_location) then
			row:tag('td'):wikitext(args[datacols*(j-1)+doffsets['loc']] or '')
		end
		-- Team1 / Team2 / Score1 / Score2
		local team1 = get_name(args[datacols*(j-1)+doffsets['t1']])
		local score1 = mw.ustring.gsub(args[datacols*(j-1)+doffsets['s1']] or '', '^%s*(.-)%s*$', '%1')
		local team2 = get_name(args[datacols*(j-1)+doffsets['t2']])
		local score2 = mw.ustring.gsub(args[datacols*(j-1)+doffsets['s2']] or '', '^%s*(.-)%s*$', '%1')
		local shade1 = nil
		local shade2 = nil
		local win = mw.ustring.gsub(args['win' .. (j - 1 + number_start)] or '', '^%s*(.-)%s*$', '%1') or ''
		if( isnotempty(win) ) then
			topres = topres .. '[[Category:Pages_using_sports_rivalry_series_table_with_a_win_parameter|Category:Pages using sports rivalry series table with a win parameter]]'
		end
		if( isnotempty(win) or (score1 ~= '' and score2 ~= '') ) then
			local score1num = tonumber(formatnumR(score1)) or 0
			local score2num = tonumber(formatnumR(score2)) or 0
			if( isnotempty(win) ) then
				score1num = -1
				score2num = -1
			end
			if ( (win == team1) or (score1num > score2num) ) then
				if( ismultiequal(team1, team1name) ) then
					shade1 = 'font-weight:bold;' .. team1style
					if isnotempty(win) then shade2 = nowinstyle end
					team1wins = team1wins + 1
					if (j >= tseries_start and j <= tseries_end) then tsteam1wins = tsteam1wins + 1 end
				elseif ( ismultiequal(team1, team2name) ) then
					shade1 = 'font-weight:bold;' .. team2style
					if isnotempty(win) then shade2 = nowinstyle end
					team2wins = team2wins + 1
					if (j >= tseries_start and j <= tseries_end) then tsteam2wins = tsteam2wins + 1 end
				end
			elseif ( (win == team2) or (score2num > score1num) ) then
				if( ismultiequal(team2, team1name) ) then
					shade2 = 'font-weight:bold;' .. team1style
					if isnotempty(win) then shade1 = nowinstyle end
					if (j >= tseries_start and j <= tseries_end) then tsteam1wins = tsteam1wins + 1 end
					team1wins = team1wins + 1
				elseif ( ismultiequal(team2, team2name) ) then
					shade2 = 'font-weight:bold;' .. team2style
					if isnotempty(win) then shade1 = nowinstyle end
					team2wins = team2wins + 1
					if (j >= tseries_start and j <= tseries_end) then tsteam2wins = tsteam2wins + 1 end
				end
			elseif ( (win == 'tie') or (not isnotempty(win) ) ) then
				shade1 = tiestyle
				shade2 = tiestyle
				if not args['header1'] then 
					args[datacols*(j-1)+doffsets['t1']] = 'Tie'
					args[datacols*(j-1)+doffsets['t2']] = 'Tie'
				end
				ties = ties + 1
				if (j >= tseries_start and j <= tseries_end) then tsties = tsties + 1 end
			end
		end
		shaderow = args['style' .. (j - 1 + number_start)]
		if( (not compact) and (not winner_only) and (not compact_score)) then
			-- Team 1
			row:tag('td')
				:cssText(shaderow or shade1)
				:wikitext(small_rank(args[datacols*(j-1)+doffsets['t1']]))
			-- Team 1 score
			row:tag('td')
				:cssText(shaderow or shade1)
				:wikitext(score1)
			-- Team 2
			row:tag('td')
				:cssText(shaderow or shade2)
				:wikitext(small_rank(args[datacols*(j-1)+doffsets['t2']]))
			-- Team 2 score
			row:tag('td')
				:cssText(shaderow or shade2)
				:wikitext(score2)
			-- Series
			if(not series_summary) then
				local seriescell = row:tag('td')
				if( score1 ~= '' and score2 ~= '') then
					seriescell:wikitext(series_text(team1abbr, team1wins, team2abbr, team2wins, ties, nil))
				end
			end
			if(tseries_start > 0) then
				local seriescell = row:tag('td')
				if( score1 ~= '' and score2 ~= '' and j >= tseries_start and j <= tseries_end) then
					seriescell:wikitext(series_text(team1abbr, tsteam1wins, team2abbr, tsteam2wins, tsties, nil))
				end
			end
		else
			if( isnotempty(win) or (score1 ~= '' and score2 ~= '') ) then
				local score1num = tonumber(formatnumR(score1)) or 0
				local score2num = tonumber(formatnumR(score2)) or 0
				if(score1num > score2num) then
					-- Winner
					row:tag('td')
						:cssText(shaderow or shade1)
						:wikitext(small_rank(args[datacols*(j-1)+doffsets['t1']]))
					if compact_score then
						-- Loser
						row:tag('td')
							:wikitext(small_rank(args[datacols*(j-1)+doffsets['t2']]))
					end
					-- Score
					row:tag('td')
						:wikitext(score1 .. '–' .. score2)
				elseif(score2num > score1num) then
					if compact_score then
						-- Loser
						row:tag('td')
							:wikitext(small_rank(args[datacols*(j-1)+doffsets['t1']]))
					end
					-- Winner
					row:tag('td')
						:cssText(shaderow or shade2)
						:wikitext(small_rank(args[datacols*(j-1)+doffsets['t2']]))
					-- Score
					row:tag('td')
						:wikitext(score2 .. '–' .. score1)
				else
					if compact_score then
						row:tag('td'):cssText(shaderow or tiestyle):attr('colspan',2):wikitext('Tie')
					else
						-- Winner
						row:tag('td'):cssText(shaderow or tiestyle):wikitext('Tie')
					end
					-- Score
					row:tag('td')
						:wikitext(score1 .. '–' .. score2)
				end
				if( (winner_only or compact_score) and (not series_summary)) then
					local seriescell = row:tag('td')
					if( score1 ~= '' and score2 ~= '') then
						seriescell:wikitext(series_text(team1abbr, team1wins, team2abbr, team2wins, ties, nil))
					end
				end
				if(tseries_start > 0) then
					local seriescell = row:tag('td')
					if( score1 ~= '' and score2 ~= '' and j >= tseries_start and j <= tseries_end) then
						seriescell:wikitext(series_text(team1abbr, tsteam1wins, team2abbr, tsteam2wins, tsties, nil))
					end
				end
			end
		end
		if(notes) then row:tag('td'):wikitext(args[datacols*(j-1)+doffsets['note']] or '') end
	end

	if( series_summary and root) then
		local ftext = '\'\'\'Series:\'\'\' '
		local ftext = ftext .. series_text(team1name, team1wins, team2name, team2wins, ties, 1)
		if(args['footnote']) then
			ftext = ftext .. args['footnote']
		end
		row = root:tag('tr')
		row:tag('td')
			:attr('colspan', 9)
			:css('background-color', '#f0f0f0')
			:wikitext(ftext)
	end

	if(isnotempty(args['note']) and root) then
		row = root:tag('tr')
		row:tag('td')
			:attr('colspan', 9)
			:wikitext(args['note'])
	end
	
	res = res .. (root and tostring(root) or '')
	
	if (cols > 1 ) then
		root = mw.html.create('table')
		root:attr('role', 'presentation') 
		row = root:tag('tr')
		row:tag('td'):wikitext(res)
		res = tostring(root)
	end

	-- return the root table
	return topres .. res
end
 
return p