local p = {}

local getArgs
local yesno = require('Module:Yesno')
local mm = require('Module:Math')
local contrast_ratio = require('Module:Color contrast')._ratio
local HTMLcolor = mw.loadData( 'Module:Color contrast/colors' )

function p.sublist(frame)
	return main(frame,true)
end

function p.list(frame)
	return main(frame,false)
end

function idtrim(val,search)
	local valfind = string.find(val, search)
	if valfind == nil then
		return val
	else
		return string.sub(val, 0, valfind-1)
	end
end

function main(frame, sublist)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	local args

	-- Most parameters should still display when blank, so don't remove blanks
	if sublist then
		args = getArgs(frame, {removeBlanks = false, wrappers = 'Template:Episode list/sublist'})
	else
		args = getArgs(frame, {removeBlanks = false, wrappers = 'Template:Episode list'})
	end
	
	local title = mw.title.getCurrentTitle()
	local page_title = mw.title.getCurrentTitle().text
	local mainlist = args.MainList or args['1'] or ''
	
	-- Is this list on the same page as the page directly calling the template?
	local on_main_page
	
	-- Only sublist had anything about hiding, so only it needs to even check
	if sublist then
		on_main_page = mw.uri.anchorEncode(page_title) == mw.uri.anchorEncode(mainlist)
		-- avoid processing ghost references
		if on_main_page then
			args.ShortSummary = nil
		end
	else
	-- Normal lists can ALWAYS show the summary
		on_main_page = false
	end
	
	-- Declare all the possible <td>/<th> tags here, and the return string
	local EpisodeNumber,EpisodeNumber2,Title,Aux1,DirectedBy,WrittenBy,
			DirectedBy,Aux2,Aux3,OriginalAirDate,AltDate,ProdCode,
			Aux5,Viewers,Aux4,return_table
	
	-- Need just this parameter removed if blank, no others
	if args.ShortSummary then
		if not args.ShortSummary:find('%S') then
			args.ShortSummary = nil
		end
	end

	-- Default color to light blue
	local line_color = args.LineColor or 'CCCCFF'
	
	-- Add # to color if necessary, and set to default color if invalid
	if HTMLcolor[line_color] == nil then
		line_color = '#'..(mw.ustring.match(line_color, '^[%s#]*([a-fA-F0-9]*)[%s]*$') or '')
		if line_color == '#' then
			line_color = '#CCCCFF'
		end
	end
	
	-- List of parameter names to test
	-- Keep this order as is
	local cell_names = {
		'EpisodeNumber2',
		'Title',
		'Aux1',
		'DirectedBy',
		'WrittenBy',
		'Aux2',
		'Aux3',
		'OriginalAirDate',
		'AltDate',
		'ProdCode',
		'Aux5',
		'Viewers',
		'Aux4'
	}
	
	-- Is there a way to call a variable by its name stored as a string? Doubt it
	-- This list matches strings with the table cell variables
	local td_tags = {
		['EpisodeNumber2'] = EpisodeNumber2,
		['Title'] = Title,
		['Aux1'] = Aux1,
		['DirectedBy'] = DirectedBy,
		['WrittenBy'] = WrittenBy,
		['DirectedBy'] = DirectedBy,
		['Aux2'] = Aux2,
		['Aux3'] = Aux3,
		['OriginalAirDate'] = OriginalAirDate,
		['AltDate'] = AltDate,
		['ProdCode'] = ProdCode,
		['Aux5'] = Aux5,
		['Viewers'] = Viewers,
		['Aux4'] = Aux4,
	}
	
	local table_row = mw.html.create('tr')
				:addClass('vevent')
				:css('text-align','center')
	
	local row_color = yesno(args.RowColor, false)
	if args.RowColor and string.lower(args.RowColor) == 'on' then
		row_color = true
	end

	local top_color
	local epn = mm._cleanNumber(args.EpisodeNumber) or 1
	if args.TopColor then
		top_color = '#'..args.TopColor
	elseif row_color and not on_main_page and mm._mod(epn,2) == 0 then
		top_color = '#E9E9E9'
	elseif not on_main_page and args.ShortSummary then
		top_color = '#F2F2F2'
	else
		top_color = 'inherit'
	end
		
	table_row:css('background',top_color)
	
	-- This will decide the colspan= of the summary cell
	-- Start as 1 because EpisodeNumber is always created
	local nonnil_params = 1
	
	-- Created separately because it is the only <th> tag
	
	if args.EpisodeNumber then
		if (args.EpisodeNumber == '') then args.EpisodeNumber = frame:expandTemplate{title='TableTBA'}; end
		EpisodeNumber = mw.html.create('th')
				:attr('scope','row')
				:attr('id','ep'..idtrim(idtrim(args.EpisodeNumber,' ----'),'<'))
				:css('text-align','center')
				:wikitext(args.EpisodeNumber)
		table_row:css('background',top_color)
		table_row:node(EpisodeNumber)
	end
	
	-- The wikitext in the Title cell is a little more involved than the others
	local function add_title()
		local title_string = ''
		
		-- Surround the Title with quotes; no quotes if empty
		if args.Title and args.Title:find('%S') then
			title_string = title_string..''..args.Title..''
		end
		
		if args.RTitle then
			title_string = title_string..args.RTitle
		end
		
		-- Surround the AltTitle with quotes; no quotes if empty
		if args.AltTitle and args.AltTitle:find('%S') and args.AltTitle ~= args.Title and string.gsub(args.AltTitle, "%s+", "") ~= '' then
			title_string = title_string..'<br><small>'..args.AltTitle..'</small>'
		end
			
		if args.RAltTitle then
			title_string = title_string..args.RAltTitle
		end
		return title_string
	end

	for _,v in ipairs(cell_names) do
		-- Title is in the middle, so it's probably better to just switch back and again instead of doing 2 nodes
		-- and then title, and then the rest in a loop
		if v == 'Title' then
			-- If Title is blank, then set Raw Title to TBA
			if args.Title == '' and (args.RTitle == '' or not args.RTitle) then args.RTitle = frame:expandTemplate{title='TableTBA'}; end
			nonnil_params = nonnil_params + 1
			local title_text = add_title()
			td_tags[v] = mw.html.create('td')
			td_tags[v]:wikitext(title_text)
					:addClass('summary')
					:css('text-align','left')
			table_row:node(td_tags[v])
		elseif args[v] then
			-- Set empty cells to TBA/TBD
			if args[v] == '' then
				-- Set to N/A if viewers haven't been available for four weeks, else set it as TBD
				if v == 'Viewers' then
					local month, day, year = args.OriginalAirDate:gsub(" "," "):match("(%a+) (%d+), (%d+)")
					if month == nil then
						day, month, year = args.OriginalAirDate:gsub(" "," "):match("(%d+) (%a+) (%d+)")
					end
					if day == nil then
						args[v] = frame:expandTemplate{title='TableTBA',args={'待定'}};
					else
						local MONTHS = {January=1, February=2, March=3, April=4, May=5, June=6, July=7, August=8, September=9, October=10, November=11, December=12}
						local seconds = os.time()-os.time({year=year,month=MONTHS[month],day=day,hour=0,min=0,sec=0})
						if seconds >= 60*60*24*7*4 then args[v] = frame:expandTemplate{title='TableTBA',args={'N/A'}};
						else args[v] = frame:expandTemplate{title='TableTBA',args={'待定'}}; end
					end
				else args[v] = frame:expandTemplate{title='TableTBA'}; end
			end
			nonnil_params = nonnil_params + 1
			td_tags[v] = mw.html.create('td')
			td_tags[v]:wikitext(args[v])
			table_row:node(td_tags[v])
		end
	end

	-- Production code also has an additional attribute, so add it separately here
	if td_tags.ProdCode and args.ProdCode and (string.find(args.ProdCode,'TBA') == nil) then
		td_tags.ProdCode:attr('id','pc'..idtrim(idtrim(args.ProdCode,' ----'),'<'))
	end
	
	local categories = ''
	
	-- add these categories only in the mainspace and only if they are on the page where the template is used
	if not on_main_page and title.namespace == 0 then
		if args.LineColor and args.LineColor ~= '' then
			local black_cr = contrast_ratio{args.LineColor, 'black', ['error'] = 0}
			local white_cr = contrast_ratio{'white', args.LineColor, ['error'] = 0}
			if black_cr < 7 and white_cr < 7 then
				
			end
		else
			categories = categories..'[[Category:使用默认线条颜色的剧集列表|Category:使用默认线条颜色的剧集列表]]'
		end
		
		if args.TopColor and args.TopColor ~= '' then
			categories = categories..'[[Category:行偏差的剧集列表|Category:行偏差的剧集列表]]'

			-- Track top colors that have a color contrast rating below AAA with
			-- respect to text color, link color, or visited link color. See
			-- [[WP:COLOR|WP:COLOR]] for more about color contrast requirements.
			local text_cr = contrast_ratio{args.TopColor, 'black', ['error'] = 0}
			local link_cr = contrast_ratio{args.TopColor, '#0B0080', ['error'] = 0}
			local visited_link_cr = contrast_ratio{args.TopColor, '#0645AD', ['error'] = 0}
			if text_cr < 7 or link_cr < 7 or visited_link_cr < 7 then
				categories = categories..'[[Category:使用無效顏色的劇集列表|Category:使用無效顏色的劇集列表]]'
			end
		end
	end
	
	-- Do not show the summary if this is being transcluded on the mainlist page
	-- Do include it on all other lists
	if not on_main_page and args.ShortSummary then
		local bottom_wrapper = mw.html.create('tr')
		-- fix for lists in the Short Summary
		local ss = args.ShortSummary
		if ss:match('^[*:;#]') or ss:match('^{|') then
			ss = '<span></span>\n' .. ss
		end
		if ss:match('\n[*:;#]') then
			ss = ss .. '\n<span></span>'
		end
		local ShortSummary = mw.html.create('td')
					:addClass('description')
					:css('border-bottom','solid 3px '..line_color)
					:attr('colspan',nonnil_params)
					:newline()
					:wikitext(ss)
		bottom_wrapper:node(ShortSummary)
		return tostring(table_row)..tostring(bottom_wrapper)..categories
	else
		return tostring(table_row)..categories
	end
end

return p