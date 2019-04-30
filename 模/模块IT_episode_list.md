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
		args = getArgs(frame, {removeBlanks = false, wrappers = 'Template:IT episode list/sublist'})
	else
		args = getArgs(frame, {removeBlanks = false, wrappers = 'Template:IT episode list'})
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
			args.Culture = nil
		end
	else
	-- Normal lists can ALWAYS show the summary
		on_main_page = false
	end
	
	-- Declare all the possible <td>/<th> tags here, and the return string
	local Number,SNumber,Date,
			President,Vice,Secretary,Clerk,Representative,
			return_table
	
	-- Need just this parameter removed if blank, no others
	if args.Culture then
		if not args.Culture:find('%S') then
			args.Culture = nil
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
		'Date',
		'President',
		'Vice',
		'Secretary',
		'Clerk',
		'Representative',
	}
	
	-- Is there a way to call a variable by its name stored as a string? Doubt it
	-- This list matches strings with the table cell variables
	local td_tags = {
		['Date'] = Date,
		['President'] = President,
		['Vice'] = Vice,
		['Secretary'] = Secretary,
		['Clerk'] = Clerk,
		['Representative'] = Representative,
	}
	
	local table_row = mw.html.create('tr')
				:addClass('vevent')
				:css('text-align','center')
	
	local row_color = yesno(args.RowColor, false)
	if args.RowColor and string.lower(args.RowColor) == 'on' then
		row_color = true
	end

	local top_color
	local epn = mm._cleanNumber(args.Number) or 1
	if args.TopColor then
		top_color = '#'..args.TopColor
	elseif row_color and not on_main_page and mm._mod(epn,2) == 0 then
		top_color = '#E9E9E9'
	elseif not on_main_page and args.Culture then
		top_color = '#F2F2F2'
	else
		top_color = 'inherit'
	end
		
	table_row:css('background',top_color)
	
	-- This will decide the colspan= of the summary cell
	-- Start as 1 because Number is always created
	local nonnil_params = 0
	
	-- Created separately because it is the only <th> tag
	
	if args.Number then
		if (args.Number == '') then args.Number = frame:expandTemplate{title='TableTBA'}; end
		Number = mw.html.create('th')
				:attr('id','e'..args.Number)
				:attr('scope','row')
				:css('text-align','center')
				:wikitext(args.Number)
		table_row:css('background',top_color)
		table_row:node(Number)
	end

	if args.SNumber then
		if (args.SNumber == '') then args.SNumber = frame:expandTemplate{title='TableTBA'}; end
		SNumber = mw.html.create('th')
				:attr('scope','row')
				:attr('id','ep'..idtrim(idtrim(args.SNumber,' ----'),'<'))
				:css('text-align','center')
				:wikitext(args.SNumber)
		table_row:css('background',top_color)
		table_row:node(SNumber)
	end

	for _,v in ipairs(cell_names) do
		-- Title is in the middle, so it's probably better to just switch back and again instead of doing 2 nodes
		-- and then title, and then the rest in a loop
		if args[v] == '-' then
			nonnil_params = nonnil_params + 1
			td_tags[v] = mw.html.create('td')
						:addClass('destable-na')
						:css('background','#ECECEC')
						:css('color','#2C2C2C')
						:css('font-size','small')
						:wikitext('空缺')
			table_row:node(td_tags[v])
		elseif args[v] then
			-- Set empty cells to TBA/TBD
			if args[v] == '' then
				-- Set to N/A if viewers haven't been available for four weeks, else set it as TBD
				args[v] = frame:expandTemplate{title='TableTBA',args={'N/A'}};
			end
			nonnil_params = nonnil_params + 1
			td_tags[v] = mw.html.create('td')
			td_tags[v]:wikitext(args[v])
			table_row:node(td_tags[v])
		end
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
	if not on_main_page and args.Culture then
		bottom_wrapper_c = mw.html.create('tr')
		-- fix for lists in the Short Summary
		local ssc = args.Culture
		if ssc:match('^[*:;#]') or ssc:match('^{|') then
			ssc = '<span></span>\n' .. ssc
		end
		if ssc:match('\n[*:;#]') then
			ssc = ssc .. '\n<span></span>'
		end
		local CultureTitle = mw.html.create('th')
					:attr('colspan',2)
					:css('text-align','center')
					:wikitext('全球文化相对论')
		bottom_wrapper_c:node(CultureTitle)
		local Culture = mw.html.create('td')
					:addClass('description')
					:attr('colspan',nonnil_params)
					:wikitext(ssc)
		bottom_wrapper_c:node(Culture)
	else bottom_wrapper_c = ''
	end

	if not on_main_page and args.Proposal then
		bottom_wrapper_p = mw.html.create('tr')
		-- fix for lists in the Short Summary
		local ssp = args.Proposal
		if ssp:match('^[*:;#]') or ssp:match('^{|') then
			ssp = '<span></span>\n' .. ssp
		end
		if ssp:match('\n[*:;#]') then
			ssp = ssp .. '\n<span></span>'
		end
		local ProposalTitle = mw.html.create('th')
					:attr('colspan',2)
					:css('text-align','center')
					:wikitext('提案环节')
		bottom_wrapper_p:node(ProposalTitle)
		local Proposal = mw.html.create('td')
					:addClass('description')
					:attr('colspan',nonnil_params)
					:wikitext(ssp)
		bottom_wrapper_p:node(Proposal)
	else bottom_wrapper_p = ''
	end
	
	if not on_main_page and args.AuxTitle then
		bottom_wrapper_a = mw.html.create('tr')
		-- fix for lists in the Short Summary
		local ssat = args.AuxTitle
		if ssat:match('^[*:;#]') or ssat:match('^{|') then
			ssat = '<span></span>\n' .. ssat
		end
		if ssat:match('\n[*:;#]') then
			ssat = ssat .. '\n<span></span>'
		end
		local ssa = args.Aux
		if ssa:match('^[*:;#]') or ssa:match('^{|') then
			ssa = '<span></span>\n' .. ssa
		end
		if ssa:match('\n[*:;#]') then
			ssa = ssa .. '\n<span></span>'
		end
		local AuxTitle = mw.html.create('th')
					:attr('colspan',2)
					:css('text-align','center')
					:wikitext(ssat)
		bottom_wrapper_a:node(AuxTitle)
		local Aux = mw.html.create('td')
					:addClass('description')
					:attr('colspan',nonnil_params)
					:wikitext(ssa)
		bottom_wrapper_a:node(Aux)
	else bottom_wrapper_a = ''
	end

	if not on_main_page and args.Guest then
		bottom_wrapper_g = mw.html.create('tr')
		-- fix for lists in the Short Summary
		local ssg = args.Guest
		if ssg:match('^[*:;#]') or ssg:match('^{|') then
			ssg = '<span></span>\n' .. ssg
		end
		if ssg:match('\n[*:;#]') then
			ssg = ssg .. '\n<span></span>'
		end
		local GuestTitle = mw.html.create('th')
					:attr('colspan',2)
					:css('text-align','center')
					:wikitext('特别嘉宾')
		bottom_wrapper_g:node(GuestTitle)
		local Guest = mw.html.create('td')
					:addClass('description')
					:attr('colspan',nonnil_params)
					:css('text-align','center')
					:wikitext(ssg)
		bottom_wrapper_g:node(Guest)
	else bottom_wrapper_g = ''
	end

	nonnil_params = nonnil_params + 2

	if not on_main_page then
		bottom_wrapper_b = mw.html.create('tr')
		-- fix for lists in the Short Summary
		local Bar = mw.html.create('td')
					:addClass('description')
					:css('height','3px')
					:css('background',line_color)
					:css('border-top','none')
					:css('border-bottom','none')				
					:attr('colspan',nonnil_params)
					:wikitext('<span></span>')
		bottom_wrapper_b:node(Bar)
		return tostring(table_row)..tostring(bottom_wrapper_c)..tostring(bottom_wrapper_p)..tostring(bottom_wrapper_a)..tostring(bottom_wrapper_g)..tostring(bottom_wrapper_b)..categories
	else
		return tostring(table_row)..categories
	end
end

return p