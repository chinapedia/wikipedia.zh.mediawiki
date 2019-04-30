local p = {}
local origArgs
local periodicTable_tlcss = ''
local error = require( 'Module:Error' )
local element_lib = require( 'Module:Element' )
local roman = require( 'Module:Roman' )
p.element_lib = require( 'Module:Element' )
local element_data = require( 'Module:Element/data' )
local p_data = require( 'Module:PeriodicTable/data' )
local yesno = require( 'Module:Yesno' )

function p.navPeriodicTable(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	periodicTable_tlcss = frame:callParserFunction{ name = '#tag:templatestyles', args = { '', src='元素週期表/styles.css' } }
	local arg1=''	if (args[1] and args[1] ~= '') then	arg1 = string.gsub(args[1] , "%s$", "") end
	local mark=''	if (args[2] and args[2] ~= '') then	mark = string.gsub(args[2] , "%s$", "") end
	
	if (args['number'] and args['number'] ~= '') then arg1 = string.gsub(args['number'] , "%s$", "") end
	if (args['mark'] and args['mark'] ~= '') then mark = string.gsub(args['mark'] , "%s$", "") end
	local markele='' if (args['markele'] and args['markele'] ~= '') then markele = string.gsub(args['markele'] , "%s$", "") end
	local rtype='normal' if (args['type'] and args['type'] ~= '') then rtype = string.gsub(args['type'] , "%s$", "") end
	if rtype == 'isotope' or rtype == 'isotope nav' then periodicTable_tlcss = periodicTable_tlcss ..
		frame:callParserFunction{ name = '#tag:templatestyles', args = { '', src='Isotope nav/styles.css' } }
	end
	-- fricke --nefedov
	local pmodel='fricke' if (args['model'] and args['model'] ~= '') then pmodel = string.gsub(args['model'] , "%s$", "") end
	no173='yes' if (args['no173'] and args['no173'] ~= '') then no173 = string.gsub(args['no173'] , "%s$", "") end
	noTag='no' if (args['noTag'] and args['noTag'] ~= '') then noTag = string.gsub(args['noTag'] , "%s$", "") end
	no173=yesno(no173)
	noTag=yesno(noTag)
	local number = tonumber(arg1)
	return p.renderNavElementTable(number, mark, mw.text.split(markele,','), rtype, pmodel)
end

function p.templatePeriodicTable(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	periodicTable_tlcss = frame:callParserFunction{ name = '#tag:templatestyles', args = { '', src='元素週期表/styles.css' } }
	local arg1=''	if (args[1] and args[1] ~= '') then	arg1 = string.gsub(args[1] , "%s$", "") end
	local mark=''	if (args[2] and args[2] ~= '') then	mark = string.gsub(args[2] , "%s$", "") end
	
	if (args['number'] and args['number'] ~= '') then arg1 = string.gsub(args['number'] , "%s$", "") end
	if (args['mark'] and args['mark'] ~= '') then mark = string.gsub(args['mark'] , "%s$", "") end
	if (args['no mark'] and args['no mark'] ~= '') then
		nomark = yesno(string.gsub(args['no mark'] , "%s$", ""))
	else
		nomark = false
	end
	local markele='' if (args['markele'] and args['markele'] ~= '') then markele = string.gsub(args['markele'] , "%s$", "") end
	local rtype='normal' if (args['type'] and args['type'] ~= '') then rtype = string.gsub(args['type'] , "%s$", "") end
	
	-- fricke --nefedov
	local pmodel='fricke' if (args['model'] and args['model'] ~= '') then pmodel = string.gsub(args['model'] , "%s$", "") end
	no173='yes' if (args['no173'] and args['no173'] ~= '') then no173 = string.gsub(args['no173'] , "%s$", "") end
	no173=yesno(no173)
	
	local number = tonumber(arg1)
	-- p.renderTemplatePeriodicTable(number, mark, markele, rtype)
	return p.renderTemplatePeriodicTable(number, mark, mw.text.split(markele,','), rtype, pmodel)
end

function p.isotopePeriodicTable(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	periodicTable_tlcss = frame:callParserFunction{ name = '#tag:templatestyles', args = { '', src='Isotope nav/styles.css' } }
	local arg1=''	if (args[1] and args[1] ~= '') then	arg1 = string.gsub(args[1] , "%s$", "") end

	if (args['number'] and args['number'] ~= '') then arg1 = string.gsub(args['number'] , "%s$", "") end
	local rtype='normal' if (args['type'] and args['type'] ~= '') then rtype = string.gsub(args['type'] , "%s$", "") end
	local classtype='' if (args['classtype'] and args['classtype'] ~= '') then classtype = string.gsub(args['classtype'] , "%s$", "") end
	
	local number = tonumber(arg1)
	if classtype and classtype ~= '' then classtype = classtype .. '_' end
	return p.renderIsotopePeriodicTable(number, rtype, classtype)
end

-----------------------
--draw Periodic Table
-----------------------
function p.renderTemplatePeriodicTable(number, mark, markele, rtype, pmodel)
	option = {}
	local has_119 = (number >= 119)
	local body = ''
	group_order = {1,2,19,20,21,22,23,24,25,26,27,28,29,30,31,32,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18}
	group_inverse = {1,2,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,3,4,5,6,7,8,9,10,11,12,13,14,15,16}
	local spans = 0
	local group_id = 1
	local period_id = 0
	local main_loop_max = 118
	if has_119 then spans = 1; main_loop_max = 118 end
	if has_119 and pmodel=='nefedov' then main_loop_max=121 end
	body = body .. p.renderPeriodicTableGroupHeader(has_119, pmodel)
	if number==0 then body = body .. p.renderPeriodicTablePeriodHeader(0)
		--p._templatePeriodicTableElementCell(element,span,mark,markele,number,rtype,option)
		body = body .. p._templatePeriodicTableElementCell(
			element_lib.getElementByZ(0),31,
			mark,markele,number,rtype,option
		) .. '\n'
	end
	local index = 1
	for index = 1,main_loop_max do
		local iteratorElement = element_lib.getElementByZ(index)
		if iteratorElement then
			if index>120 then
				iteratorElement.series={'化學性質未知'}
				iteratorElement.predictedSeries = nil
			end
			if period_id ~= iteratorElement.period then 
				period_id = iteratorElement.period
				group_id = 1
				body = body .. p.renderPeriodicTablePeriodHeader(iteratorElement.period)
			end
			local iterator_group = iteratorElement.group or 19
			local spans_data = group_inverse[iterator_group] - group_id

			if has_119 and pmodel=='nefedov' then
				
				if iteratorElement.period < 6 then
					if iterator_group==3 then
						iterator_group = 19
						spans_data = group_inverse[iterator_group] - group_id
					elseif iterator_group==4 then
						spans_data = spans_data - 1 + spans
					end
				end

			end
		
			local skip_eleid=38
			local split_eleg=19
			if has_119 and pmodel=='nefedov' then skip_eleid=57;
			elseif has_119 and pmodel=='fricke' then skip_eleid=38;
			end
			
			if has_119 and pmodel=='nefedov' then split_eleg=20
			elseif has_119 and pmodel=='fricke' then split_eleg=19
			end
			
			if spans_data > 0 or iterator_group==split_eleg then
				spans_data = spans_data + spans
			end
			if index == skip_eleid+1 then spans_data = spans_data - 1 end

			body = body .. 
			p._templatePeriodicTableElementCell(
				iteratorElement,spans_data,
				mark,markele,number,
				rtype,option
			) .. '\n'
			if index == skip_eleid then
				if has_119 then
					body = body .. '| style=\"border:none; width:6px; min-width:6px;\" |\n'
				else
					body = body .. '| style=\"border:none; width:0;\" |\n'
				end
			end
			group_id = group_inverse[iterator_group]+1
		end
	end
	
	if has_119 and pmodel=='nefedov' then 
		body = body .. '| style=\"border:none; width:0;\" |*\n'
		local old_eleid=144
		body = body .. p._renderTemplateElementTable_Extended(144, 172, '化學性質未知', false, mark, markele, number, rtype)

		body = body .. '\n|-\n|style=\"border:none; padding:0;\"|<div style=\"width:1px; height:4px;\"></div>\n|-\n| colspan=4|\n'
		body = body .. '| style=\"border:none; width:0;\" |*\n'
		body = body .. p._renderTemplateElementTable_Extended(main_loop_max+1, 143, '化學性質未知', false, mark, markele, number, rtype)
		if not no173 or number >= 173 then
			body = body .. '| style=\"border:none; width:0;\" |\n'
			body = body .. '\n|-\n|style=\"border:none; padding:0;\"|<div style=\"width:1px; height:4px;\"></div>'
			body = body .. '\n|-\n|colspan=5|\n|colspan=4|[[未發現元素列表#周期未定|族未定]]\n|-\n| colspan=2|'
			body = body .. '\n|colspan=3|[[未發現元素列表#周期未定|周期未定]]\n'
	
			local extindex = 173
			local check_number = number + 1; if check_number < 184 then check_number = 184 end
			local is_first = true
			local max_index = extindex
			while extindex <= check_number do
				if is_first then is_first = false
				else body = body .. '|-\n| colspan=5|\n' end
				max_index = extindex+28
				if max_index >= check_number then max_index = check_number end
				body = body .. p._renderTemplateElementTable_Extended(
						extindex, max_index, '超臨界原子', true, 
						mark, markele, number, rtype, option)
				extindex = extindex + 29
			end
			
			local check_side = max_index-173
			check_side = math.mod(check_side,29)
			if (check_side == 0 or check_side >= 28) then body = body .. '|-\n| colspan=5|\n' end
			body = body .. '\n| colspan=1|.....\n'
		end
		body = body .. '\n|-\n| colspan=5|\n'
		body = body .. '\n| colspan=25|※註：119號及以後的元素並無公認的排位，上表之排位是從理論計算的電子排布推論而得的一種\n'
	end
	
	return body
end

function p.renderIsotopePeriodicTable(number, rtype, classtype)
	local option = {index=true,class_type=classtype}
	local has_119 = (number >= 119)
	local body = ''
	group_order = {1,2,19,20,21,22,23,24,25,26,27,28,29,30,31,32,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18}
	group_inverse = {1,2,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,3,4,5,6,7,8,9,10,11,12,13,14,15,16}
	local spans = 0
	local group_id = 1
	local period_id = 0
	local main_loop_max = 118
	local is_lanthanide_below = (mw.ustring.lower(rtype) == 'lanthanide below')
	local gobal_spans = 31
	if is_lanthanide_below then gobal_spans = 18 end
	if has_119 then spans = 1; main_loop_max = 118 end
	--body = body  .. p.renderPeriodicTableGroupHeader(has_119) .. p.renderPeriodicTablePeriodHeader(0)
		body = body .. p._isotopePeriodicTableElementCell(
			element_lib.getElementByZ(0),gobal_spans,
			number,rtype,option
		) .. '\n'
	--Lanthanide below
	local index = 1
	for index = 1,118 do
		local iteratorElement = element_lib.getElementByZ(index)
		if iteratorElement then
			if period_id ~= iteratorElement.period then 
				period_id = iteratorElement.period
				group_id = 1
				body = body .. '|-\n'
				-- .. p.renderPeriodicTablePeriodHeader(iteratorElement.period)
			end
			
			local iterator_group = iteratorElement.group or 19
			local spans_data = group_inverse[iterator_group] - group_id

			if is_lanthanide_below then
				
				if iteratorElement.period < 6 then
					if iterator_group==3 then
						iterator_group = 19
						spans_data = group_inverse[iterator_group] - group_id
					elseif iterator_group==4 then
						spans_data = spans_data - 1 + spans
					end
				end

			end
		
			local skip_eleid=38
			local split_eleg=19
			local skip_gp=-1
			
			if is_lanthanide_below then skip_eleid=57; skip_gp=19;  end
			if is_lanthanide_below then split_eleg=20
				if spans_data >= 13 then 
					spans_data = spans_data - 14 
					if index < 56 then spans_data = spans_data + 1 end
				end
			end
			
			if spans_data > 0 or iterator_group==split_eleg then spans_data = spans_data + spans end
			if index == skip_eleid+1 then spans_data = spans_data - 1 end
			if (not is_lanthanide_below) or (iterator_group <= 19 and index~=71 and index~=103) then 
				body = body .. 
				p._isotopePeriodicTableElementCell(
					iteratorElement,spans_data,
					number,
					rtype,option
				) .. '\n'
				if index == skip_eleid or (iterator_group == skip_gp) then
					if is_lanthanide_below then
						body = body .. '| style=\"border:none; width:6px; min-width:6px;\" |'
						if index > 56 then body = body .. '*' end
						if index > 88 then body = body .. '*' end
						body = body .. '\n'
					else
						body = body .. '| style=\"border:none; width:0;\" |\n'
					end
				end
			end
			group_id = group_inverse[iterator_group]+1
		end
	end
	if is_lanthanide_below then
		body = body .. '\n|-\n|style=\"border:none; padding:0;\"|<div style=\"width:1px; height:4px;\"></div>\n|-\n| colspan=1|\n'
		body = body .. '| colspan=1 style=\"border:none; width:0;\" |*\n'
		body = body .. '| colspan=2 style=\"border:none; width:0;\" |[[镧系元素|鑭系<br/>元素]]\n'
		for index = 57,71 do
			local iteratorElement = element_lib.getElementByZ(index)
			if iteratorElement then
				body = body .. 
					p._isotopePeriodicTableElementCell(
						iteratorElement,0,
						number,
						rtype,option
					) .. '\n'
			end
		end
		body = body .. '\n|-\n| colspan=1|\n'
		body = body .. '| colspan=1 style=\"border:none; width:0;\" |**\n'
		body = body .. '| colspan=2 style=\"border:none; width:0;\" |[[锕系元素|錒系<br/>元素]]\n'
		
		for index = 89,103 do
			local iteratorElement = element_lib.getElementByZ(index)
			if iteratorElement then
				body = body .. 
					p._isotopePeriodicTableElementCell(
						iteratorElement,0,
						number,
						rtype,option
					) .. '\n'
			end
		end
	end
	return body
end

function p.renderNavElementTable(number, mark, markele, rtype, pmodel)
	local has_119 = (number >= 119)
	tlcss_inserted = false
	local body = '{| class=\"nogrid\" cellpadding=0 cellspacing=1 style=\"background-color: transparent; text-align: center; empty-cells: show; border: none\"\n'
	group_order = {1,2,19,20,21,22,23,24,25,26,27,28,29,30,31,32,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18}
	group_inverse = {1,2,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,3,4,5,6,7,8,9,10,11,12,13,14,15,16}
	local spans = 0
	local group_id = 1
	local period_id = 1
	local main_loop_max = 118
	if has_119 then spans = 1; main_loop_max = 118 end
	if has_119 and pmodel=='nefedov' then main_loop_max=121 end
	if number==0 then body = body .. "| style=\"border:none\" | \n| colspan=30 style=\"border:none\" | \n| style=\"border:none\" | "
		body = body .. p._navElementCell(
			element_lib.getElementByZ(0),
			mark,markele,number,rtype
		) .. '\n|-\n'
	end
	for index = 1,main_loop_max do
		local iterator = element_lib.getElementByZ(index)
		if iterator then
			if index>120 then
				iterator.series={'化學性質未知'}
				iterator.predictedSeries = nil
			end
			if period_id ~= iterator.period then 
				period_id = iterator.period
				group_id = 1
				body = body .. '|-\n'
			end
			local iterator_group = iterator.group or 19
			local spans_data = group_inverse[iterator_group] - group_id

			if has_119 and pmodel=='nefedov' then
				
				if iterator.period < 6 then
					if iterator_group==3 then
						iterator_group = 19
						spans_data = group_inverse[iterator_group] - group_id
					elseif iterator_group==4 then
						spans_data = spans_data - 1 + spans
					end
				end

			end
		
			local skip_eleid=38
			local split_eleg=19
			if has_119 and pmodel=='nefedov' then skip_eleid=57;
			elseif has_119 and pmodel=='fricke' then skip_eleid=38;
			end
			
			if has_119 and pmodel=='nefedov' then split_eleg=20
			elseif has_119 and pmodel=='fricke' then split_eleg=19
			end
			
			if spans_data > 0 or iterator_group==split_eleg then
				spans_data = spans_data + spans
			end
			if index == skip_eleid + 1 then spans_data = spans_data - 1 end

			body = body .. p.renderNavElementColHeader(spans_data)
			if not tlcss_inserted then
				tlcss_inserted = true
				body = body .. periodicTable_tlcss
			end
			body = body .. p._navElementCell(iterator,mark,markele,number,rtype) .. '\n'
			if index == skip_eleid then
				if has_119 then
					body = body .. '| style=\"border:none; width:6px; min-width:6px;\" |\n'
				else
					body = body .. '| style=\"border:none; width:0;\" |\n'
				end
			end
			group_id = group_inverse[iterator_group]+1
		end
	end
	
	if has_119 and pmodel=='nefedov' then 
		body = body .. '| style=\"border:none; width:0;\" |<div style=\"float:left; margin:3px 2px; background:black; width:2px; height:2px;\"></div>\n'
		local old_eleid=144
		body = body .. p._renderNavElementTable_Extended(144, 172, '化學性質未知', false, mark, markele, number, rtype)

		body = body .. '\n|-\n|style=\"border:none; padding:0;\"|<div style=\"width:1px; height:4px;\"></div>\n|-\n| colspan=3|\n'
		body = body .. '| style=\"border:none; width:0;\" |<div style=\"float:left; margin:3px 2px; background:black; width:2px; height:2px;\"></div>\n'
		body = body .. p._renderNavElementTable_Extended(main_loop_max+1, 143, '化學性質未知', false, mark, markele, number, rtype)
		if not no173 or number >= 173 then
			body = body .. '| style=\"border:none; width:0;\" |\n'
			body = body .. '\n|-\n|style=\"border:none; padding:0;\"|<div style=\"width:1px; height:4px;\"></div>\n|-\n| colspan=3|\n'
			body = body .. '| style=\"border:none; width:0;\" |<div style=\"float:left; margin:3px 2px; background:blue; width:2px; height:2px;\"></div>\n'
	
			local extindex = 173
			local check_number = number + 1; if check_number < 184 then check_number = 184 end
			local is_first = true
			local max_index = extindex
			while extindex <= check_number do
				if is_first then is_first = false
				else body = body .. '|-\n| colspan=4|\n' end
				max_index = extindex+28
				if max_index >= check_number then max_index = check_number end
				body = body .. p._renderNavElementTable_Extended(extindex, max_index, '超臨界原子', true, mark, markele, number, rtype)
				extindex = extindex + 29
			end
			
			local check_side = max_index-173
			check_side = math.mod(check_side,29)
			if (check_side == 0 or check_side >= 28) then body = body .. '|-\n| colspan=4|\n' end
			body = body .. '\n| colspan=2 style=\"font-size:10px; line-height:5px\"|...\n'
		end
		if not noTag then
			body = body .. '\n|-\n| colspan=32 style=\"font-size:10px; line-height:10px\"|※註：119號及以後的元素並無公認的排位，上表<br/>之排位是從理論計算的電子排布推論而得的一種\n'
		end
	end
	
	return body .. '|}'
end

-----------------------
--Draw Sub Row
-----------------------
function p._renderTemplateElementTable_Extended(start_id, end_id, ele_series, pred, mark, markele, number, rtype, option)
	local body = ''
	local old_eleid=start_id
	local index = start_id
	for index = start_id, end_id do
		local iterator = element_lib.getElementByZ(index)
		if iterator then
			local spans_data = index - old_eleid
			iterator.series={ele_series}
			iterator.predictedSeries = nil
			if pred then iterator.predictedSeries = 1 end
			if not iterator.othername then 
				iterator.othername={iterator.name}
			else
				table.insert(iterator.othername, iterator.name)
			end
			iterator.name = tostring( index )
			--高度耗費剖析器函數
			if index <= 174 then
				if not mw.title.new( iterator.page or 'This Element Doesn\'t Exist.', 0).exists then iterator.page = nil end
			else
				iterator.page = nil
			end
			body = body .. 
			p._templatePeriodicTableElementCell(
				iterator,spans_data,
				mark,markele,number,
				rtype,option
			) .. '\n'
			old_eleid = index + 1
		end
	end
	return body
end
function p._renderNavElementTable_Extended(start_id, end_id, ele_series, pred, mark, markele, number, rtype)
	local body = ''
	local old_eleid=start_id
	local index = start_id
	for index = start_id, end_id do
		iterator = element_lib.getElementByZ(index)
		if iterator then
			local spans_data = index - old_eleid
			iterator.series={ele_series}
			iterator.predictedSeries = nil
			if pred then iterator.predictedSeries = 1 end
			if not iterator.othername then 
				iterator.othername={iterator.name}
			else
				table.insert(iterator.othername, iterator.name)
			end
			iterator.name = tostring( index ) .. ' ' .. iterator.name

			--高度耗費剖析器函數
			--if not mw.title.new( iterator.page or 'This Element Doesn\'t Exist.', 0).exists then iterator.page = nil end
				
			body = body .. p.renderNavElementColHeader(spans_data)
			body = body .. p._navElementCell(iterator,mark,markele,number,rtype) .. '\n'
			old_eleid = index + 1
		end
	end
	return body
end

-----------------------
--Utils
-----------------------
function p.getHalflifeStyle(element)
	if element.stability then
		local stability = element.stability
		if stability.stableCount and stability.stableCount > 0 then
			for v, stables in ipairs(p_data.halflifestyle.stables) do
				if ( stability.stableCount >= stables.stables) then
					return stables.styleclass
				end
			end
		end
		if stability.halflife then
			local halflife = tonumber(stability.halflife)
			for v, halflifes in ipairs(p_data.halflifestyle.halflifes) do
				if ( halflife >= halflifes.halflife) then
					return halflifes.styleclass
				end
			end
		end
	end
	return '';
end

function p.getTimeDesc(seconds)
	string.format( "%.2f", 0.2453435 )
	if seconds < 1e-3 then
		local digs = math.floor(math.log10( seconds ))
		local first_dig = seconds / math.pow( 10, digs )
		return string.format("%.2f",first_dig) .. '×10^' .. string.format( "%d",digs) .. '秒'
	elseif seconds < 0.1 then --ms
		local val = seconds / (1e-3)
		return string.format( "%.2f", val) .. '豪秒'
	elseif seconds < 60 then --seconds
		return string.format( "%.2f", seconds) .. '秒'
	elseif seconds < 3600 then --min
		local val = seconds / 60.0
		return string.format( "%.2f", val) .. '分鐘'
	elseif seconds < 86400 then --hour
		local val = seconds / 3600.0
		return string.format( "%.2f", val) .. '小時'
	elseif seconds < 2.592e6 then --day
		local val = seconds / 86400.0
		return string.format( "%.2f", val) .. '天'
	elseif seconds < 3.1536e7 then --month
		local val = seconds / 2.592e6
		return string.format( "%.2f", val) .. '個月'
	elseif seconds < 3.1536e11 then --years
		local val = seconds / 3.1536e7
		return string.format( "%.2f", val) .. '年'
	elseif seconds < 3.1536e15 then --ten_KYear
		local val = seconds / 3.1536e11
		return string.format( "%.2f", val) .. '萬年'
	elseif seconds < 3.1536e19 then --ten_MYear
		local val = seconds / 3.1536e15
		return string.format( "%.2f", val) .. '億年'
	else
		local years = seconds / 3.1536e7
		local digs = math.floor(math.log10( years ))
		local first_dig = years / math.pow( 10, digs )
		return string.format( "%.2f", first_dig) .. '×10^' .. string.format( "%d",digs) .. '年'
	end
end

function p.getSeriesData(input_name)
	for v, x in ipairs(p_data.series_data) do                                
		if (x.page == input_name) then
			return p_data.series_data[v]
		end
		for v1, x1 in ipairs(x.name) do
			if (x1 == input_name) then
				return p_data.series_data[v]
			end
		end
	end
end
function p.compareSeriesList(left_list, right_list)
	for left_index, left_value in ipairs(left_list) do
		for right_index, right_value in ipairs(right_list) do
			if left_value.name and right_value.name then
				if left_value.name[1] == right_value.name[1] then return true end
			end
		end
	end
	return false
end
function p.getSeriesDataByString(input_str)
	local series_list = {}; local series_list_n = 0
	local input_list = {}
	if string.find( input_str, ',') then
		input_list=mw.text.split(input_str, ',')
	else input_list={input_str}
	end
	for v, x in ipairs(input_list) do
		local result_series = p.getSeriesData(x)
		if result_series then
			series_list[series_list_n + 1] = result_series
			series_list_n = series_list_n + 1
		else
			local ele_check = element_lib.getListID(x)
			local predicted = false
			if ele_check > 0 then
				local ele1 = element_data[ele_check]
				if ele1.series then
					if (ele1.predictedSeries and ele1.predictedSeries ~= '') then predicted=true end
					for v_ele, x_ele in ipairs(ele1.series) do
						result_series = p.getSeriesData(x_ele)
						if result_series.name and result_series.name[1] ~= "金屬" then 
							if predicted then result_series.predicted = true end
							result_series.fromElement = ele1.name
							if result_series then
								series_list[series_list_n + 1] = result_series
								series_list_n = series_list_n + 1
							end
						end
					end
				end
			end
		end
	end
	return series_list
end
function p.elementDataPreview(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	periodicTable_tlcss = frame:callParserFunction{ name = '#tag:templatestyles', args = { '', src='元素週期表/styles.css' } }
	local st=''	if (args[1] and args[1] ~= '') then	st = string.gsub(args[1] , "%s$", "") end
	local ed=''	if (args[2] and args[2] ~= '') then	ed = string.gsub(args[2] , "%s$", "") end
	
	if (args['start'] and args['start'] ~= '') then st = string.gsub(args['start'] , "%s$", "") end
	if (args['end'] and args['end'] ~= '') then ed = string.gsub(args['end'] , "%s$", "") end
	local cols='種類,穩定性,週期,族,分區,性質,核子數,其他名稱,同位素' if (args['cols'] and args['cols'] ~= '') then cols = string.gsub(args['cols'] , "%s$", "") end

	no_head='no' if (args['no_head'] and args['no_head'] ~= '') then no_head = string.gsub(args['no_head'] , "%s$", "") end
	no_head=yesno(no_head)
	
	no_start_end='no' if (args['no_start_end'] and args['no_start_end'] ~= '') then no_start_end = string.gsub(args['no_start_end'] , "%s$", "") end
	no_start_end=yesno(no_start_end)
	
	withZ='no' if (args['withZ'] and args['withZ'] ~= '') then withZ = string.gsub(args['withZ'] , "%s$", "") end
	withZ=yesno(withZ)
	
	cols = mw.text.split(cols or {},',')
	local colarr = {}
	for keyi, vali in pairs( cols ) do
		colarr[vali] = true
	end
	return p._elementDataPreview(tonumber(st), tonumber(ed), no_head, withZ, no_start_end, colarr)
end
function p._elementDataPreviewRow(value, cols)
	local body = ''
			if value then
				if tonumber(value.Z or -2) >= 173 then
					value.series={'超臨界原子'}
				end
				
				if not withZ and cols['序號'] then
					body = body .. '|-\n|'
					body = body .. '<span style=\"display:none\" class="sortkey\">'
					body = body .. string.format( '%016.8f', tonumber(value.tableid or 0) )  .. ' </span> '
					body = body .. tostring(value.tableid) .. '\n|'
				else
					body = body .. '|-\n|'
				end
				local seriesdata = {}
				if value.series then
					if value.series[1] then
						seriesdata = p.getSeriesData(value.series[1])
						if seriesdata and seriesdata.style then body = body .. 'class=\"' .. seriesdata.style ..'\"|' end
					end
				end
				body = body .. ' '
				if value.name then 
					body = body .. value.name 
					if not periodicTable_tlcss_inserted then 
						body = body .. (periodicTable_tlcss or '') 
						periodicTable_tlcss_inserted = true
					end
				end body = body .. ' || '
				if value.page then body = body .. '[['_.._value.page_.._'|' .. value.page .. ']]' end body = body .. ' || '
				if value.Symbol then body = body .. value.Symbol end body = body .. ' || '
				
				if cols['種類'] then
					if value.compound == true then body = body .. '[[化合物|化合物]]'
					elseif value.decay == true then body = body .. '[[衰变方式|衰变方式]]'
					elseif value.IsIsotope == true then body = body .. '[[同位素|同位素]]'
					elseif not (value.NotElement == true) then body = body .. '[[化學元素|化學元素]]'
					end body = body .. ' || '
				end
				
				local stabilitydata = value.stability or {stableCount=0}
				
				if cols['穩定性'] then
					if stabilitydata then 
						
						body = body .. '<span style=\"display:none\" class="sortkey\">'
						local sort_key = 0
						if stabilitydata.stableCount > 0 then 
							sort_key = math.log10(tonumber(tostring(((stabilitydata.stableCount + 1.0) / 2.0) + 1.0) .. 'e+32'))
						elseif stabilitydata.halflife and stabilitydata.halflife > 0 then
							sort_key = math.log10(stabilitydata.halflife)
						end
						
						if tonumber(value.Z or -2) >= 119 then
							body = body .. string.format( '%016.8f', 1 ) .. ' </span> '
						elseif value.NotElement or value.OtherElement or value.correct or value.IsIsotope 
							or (value.Symbol or 'x')=='X' or tonumber(value.Z or -2) < 0 then
							body = body .. ' </span> '
						else
							body = body .. string.format( '%016.8f', sort_key + 1000 ) .. ' </span> '
						end
						
						local stability_desc = ''
						if stabilitydata.stableCount > 0 then 
							stability_desc = tostring(stabilitydata.stableCount) .. '個穩定同位素'
						elseif stabilitydata.halflife and stabilitydata.halflife > 0 then
							stability_desc = '半衰期約' .. p.getTimeDesc(stabilitydata.halflife)
						end
						if stabilitydata.magicNumber then stability_desc = stability_desc .. ' （幻數）' end
						body = body .. stability_desc
					end body = body .. ' || '
				end
				
				if tonumber(value.Z or -2) >= 173 then value.period = '周期未定' end
				
				if cols['週期'] then
					if value.period then 
						body = body .. '<span style=\"display:none\" class="sortkey\">'
						if value.period == '周期未定' or tonumber(value.period) <= 0 then 
							body = body .. string.format( '%016.8f', 999 ) 
						else
							body = body .. string.format( '%016.8f', tonumber(value.period) ) 
						end
						body = body .. ' </span> '
						
						local iterator = p_data.period_data[value.period]
						if tonumber(value.Z or -2) >= 173 then iterator={name={"週期未定"},page='未發現元素列表#周期未定'} end
						local lprefix = ' '; local lpostfix = ''; local lmiddle = ''
						if iterator then
							if iterator.page then lprefix = ' [[';_lpostfix_=_'|'; lpostfix = ']]'; lmiddle = iterator.page .. '|' end
						end
						body = body .. lprefix .. lmiddle .. tostring(value.period) .. lpostfix
					else
						body = body .. '<span style=\"display:none\" class="sortkey\">'
						body = body .. string.format( '%016.8f', 999 )  .. ' </span> '
					end body = body .. ' || '
				end
				
				if cols['族'] then
					if value.group then 
						local iterator = p_data.group_data[value.group]
						body = body .. '<span style=\"display:none\" class="sortkey\">'
						if tonumber(value.group) <= 0 then 
							body = body .. string.format( '%016.8f', 999 ) 
						else
							body = body .. string.format( '%016.8f', tonumber(value.group) ) 
						end
						body = body .. ' </span> '
						if iterator and iterator.name and iterator.name[1] then
							if iterator.page then
								body = body .. '[['_.._iterator.page_.._'|' .. iterator.page .. ']]'
							else
								body = body .. iterator.name[1]
							end
						end
					else
						body = body .. '<span style=\"display:none\" class="sortkey\">'
						body = body .. string.format( '%016.8f', 999 )  .. ' </span> '
					end body = body .. ' || '
				end
				
				if cols['分區'] then
					if value.block then 
						local iterator = p.getSeriesData(value.block .. ' block')
						if iterator then
							if iterator.page then
								body = body .. '[['_.._iterator.page_.._'|' .. iterator.page .. ']]'
							else
								body = body .. (iterator.name or {value.block})[1]
							end
						end
					end body = body .. ' || '
				end
				
				if cols['性質'] then
					if seriesdata then 
						if seriesdata.page then
							body = body .. '[['_.._seriesdata.page_.._'|' .. seriesdata.page .. ']]'
						else
							if seriesdata.name then body = body .. seriesdata.name[1] end
						end
					end body = body .. '\n|'
				end
				
				local ele_flag = ( ((value.Z or 0) <= 0) and ((value.N or 0) <= 0) )
				
				if cols['核子數'] then
					if ele_flag then body = body .. 'colspan=3|' else body = body .. '|' end 
					if not ele_flag then
						if (value.Z or -1) >= 0 then 
							body = body .. '<span style=\"display:none\" class="sortkey\">'
							body = body .. string.format( '%016.8f', value.Z )  .. ' </span> '
							body = body .. tostring(value.Z) 
						end body = body .. ' || '
						if value.N ~= nil then
							if (value.N or -1) >= 0 then body = body .. tostring(value.N) end 
						else
							body = body .. '<span style=\"display:none\" class="sortkey\">'
							body = body .. string.format( '%016.8f', 999 )  .. ' </span> '
							body = body .. '?'
						end body = body .. ' || '
						if value.N ~= nil then 
							body = body .. tostring((tonumber(value.Z) or 0) + (tonumber(value.N) or 0)) 
						else
							body = body .. '<span style=\"display:none\" class="sortkey\">'
							body = body .. string.format( '%016.8f', 999 )  .. ' </span> '
							body = body .. '?'
						end
					else
						body = body .. '<span style=\"display:none\" class="sortkey\">'
						body = body .. string.format( '%016.8f', 999 )  .. ' </span> '
					end body = body .. ' || '
				end
				
				if cols['其他名稱'] then
					if value.othername then 
						body = body .. '-{' .. table.concat(value.othername,"、 ") .. '}-' 
					end body = body .. ' || '
				end
				
				if cols['同位素'] then
					if not (value.NotElement == true) then
						if value.isotopePage then 
							body = body .. '[['_.._value.isotopePage_.._'|' .. value.isotopePage .. ']]' 
						else
							body = body .. value.name .. '的同位素'
						end
						if value.Isotope then
							local iso_str = ''
							local first_iso = true
							for iso_tmp, isotope_iterator in ipairs(value.Isotope) do
								if first_iso then first_iso = false else iso_str = iso_str .. "、 " end
								if isotope_iterator.name then
									if isotope_iterator.page then
										iso_str = iso_str .. '[['_.._isotope_iterator.page_.._'|' .. isotope_iterator.name .. ']]' 
									else
										iso_str = iso_str .. isotope_iterator.name
									end
								end
							end
							if not first_iso then body = body .. '（' .. iso_str .. '）' end
						end
					end body = body .. ' || '
				end

				body = body .. ' \n'
			end
	return body
end
function p._elementDataPreview(start_id, end_id, no_head, withZ, no_start_end, cols)
	local body = ''
	if not no_start_end then body = body .. '{| class="wikitable sortable" \n' end
	local periodicTable_tlcss_inserted = false
	if not no_head then
		if not withZ and cols['序號'] then
			body = body .. '!序號' .. (periodicTable_tlcss or '') .. ' !! 名稱'
		else
			body = body .. '!名稱' .. (periodicTable_tlcss or '')
		end
		body = body .. '!! 條目 !! 符號'
		col_lists = {'種類','穩定性','週期','族','分區','性質','核子數','其他名稱','同位素'}
		for keyi, vali in pairs( col_lists ) do
			if cols[vali] then
				if vali == '核子數' then
					body = body .. ' !! 質子數 !! 中子數 !! 質量數'
				else
					body = body .. ' !! ' .. vali
				end
			end
		end
		body = body .. '\n'
		--!! 種類 !! 穩定性 !! 週期 !! 族 !! 分區 !! 性質 !! 質子數 !! 中子數 !! 質量數 !! 其他名稱 !! 同位素\n'
		periodicTable_tlcss_inserted = true
	end
	local start_i = start_id or 1; local end_i = end_id or 0
	if start_i > end_i then end_i = 0 end
	if start_i <= 0 and not withZ then start_i = 1 end
	if end_i <= 0 then end_i = 0 end
	if end_i == 0 and withZ then end_i = start_i + 300 end
	local i = start_i
	if withZ then 
		local i = start_i
		for i = start_i,end_i do
			local value = element_lib.getElementByZ(i)
			body = body .. p._elementDataPreviewRow(value, cols)
		end
	else
		for key, value in ipairs(element_data) do
			if tonumber(key or 0) == i then
				value.tableid = key
				body = body .. p._elementDataPreviewRow(value, cols)
				if end_i ~= 0 and end_i <= i-1 then 
					if no_start_end then return body end
					return body .. '|}\n' 
				end
				i = i + 1
			end
		end
	end
	if no_start_end then return body end
	return body .. '|}'
end

function p.checkElementList(element, list)
	local check_list = mw.text.split(table.concat(element.othername,',') .. ',' ..
		element.name .. ',' .. (element.page or element.name) .. ',' .. element.Symbol, ',')
	for vl, xl in ipairs(element.othername) do
		for vr, xr in ipairs(list) do
			if mw.text.trim(xl) == mw.text.trim(xr) then return true end
		end
	end
	return false
end

-----------------------
--rendering
-----------------------
function p.renderPeriodicTablePeriodHeader(period)
	local body = '|-\n| '
	local iterator = p_data.period_data[period]
	local lprefix = ' '; local lpostfix = ''; local lmiddle = ''
	if iterator then
		if iterator.page then lprefix = ' [[';_lpostfix_=_'|'; lpostfix = ']]'; lmiddle = iterator.page .. '|' end
	end
	return body .. lprefix .. lmiddle .. tostring(period) .. lpostfix .. '\n'
end

function p.renderPeriodicTableGroupHeader(has_119, pmodel)
	local body = '|-\n|  \n'
	local group_id = 1
	tlcss_inserted = false
	for index = 1,18 do
		local iterator = p_data.group_data[index]
		if iterator then
			local spans_data = iterator.order_id - group_id
			if pmodel=='nefedov' then
				if index == 3 then
					spans_data = 0
				elseif index == 4 then
					spans_data = p_data.group_data[index - 1].order_id - index + 1
				end
			end

			body = body .. p.renderNavElementColHeader(spans_data)
			if not tlcss_inserted then
				tlcss_inserted = true
				body = body .. periodicTable_tlcss
			end
			
			local test_index = index ; if index % 10 > 8 or index == 10 then test_index = 8 end
			test_index = test_index % 10
			local group_text = tostring(index)
			if roman.getRomam then
				group_text = string.upper(roman.getRomam(test_index) .. iterator.group_type) .. '<br/>' .. tostring(index)
			else
				group_text = error.error({[1]="羅馬數字模組錯誤：疑似有人誤刪[[模块:Roman|模块:Roman]]中的getRomam函數。"})
			end
			body = body .. ' [['_.._iterator.page_.._'|' .. group_text .. ']]' .. '\n'
			if has_119 and ((pmodel~='nefedov' and index == 2) or (pmodel=='nefedov' and index == 3)) then body = body .. '|\n' end
			group_id = iterator.order_id+1
		end
	end
	return body
end

function p.renderNavElementColHeader(span)
	local body = '|'
	local span_flag = false
	if span then span_flag = (tonumber(span) > 0) end
	if span_flag then body = body .. ' colspan=' .. tostring(span) .. ' ' end
	body = body .. 'style=\"border:none\" | '
	if span_flag then return body .. '\n| style=\"border:none\" | '
	else return body
	end
end	

function p._templatePeriodicTableElementCell(element,span,mark,markele,number,rtype,option)
	local predicted = false
	local otheratt = ''
	if element and element.period == 6 then otheratt = 'width=\"3.125%\"' end
	if element.series then
		if (element.predictedSeries and element.predictedSeries ~= '') then predicted=true end
		local series_text = element.series[1]
		if rtype == 'block' then
			series_text = (element.block or 'x') .. '區元素'
		elseif rtype == 'predicted' then
			if predicted then series_text = '未知特性' end
		end
		local result_series = p.getSeriesData(series_text)
		
		if not result_series then result_series = p_data.error_series end
		local style_class = result_series.style
		if predicted and rtype ~= 'predicted' then style_class = style_class .. '_predicted' end

		return p.renderTemplatePeriodicTableElementCell(element, span, style_class, otheratt,
			(number==element.Z and (not (nomark or false))) or p.compareSeriesList({result_series}, p.getSeriesDataByString(mark))
			or p.checkElementList(element,markele) ,option
		)
	end
	return ''
end

function p._isotopePeriodicTableElementCell(element,span,number,rtype,option)
	local is_lanthanide_below = (mw.ustring.lower(rtype) == 'lanthanide below')
	local otheratt = ''
	if element and element.period == 6 then 
		otheratt = 'width=\"3.125%\"' 
		if is_lanthanide_below then otheratt = 'width=\"5.54%\"' end
	end
	return p.renderIsotopePeriodicTableElementCell(element, span, 
		'Isotope_nav_' .. option.class_type ..  p.getHalflifeStyle(element)
		, otheratt,option)
end

function p._navElementCell(element,mark,markele,number,rtype)
	local predicted = false
	if element.series then
		if (element.predictedSeries and element.predictedSeries ~= '') then predicted=true end
		local series_text = element.series[1]
		if rtype == 'block' then
			series_text = (element.block or 'x') .. '區元素'
		elseif rtype == 'predicted' then
			if predicted then series_text = '未知特性' end
		end
		local result_series = p.getSeriesData(series_text)
			
		if not result_series then result_series = p_data.error_series end
		local style_class = result_series.style
		if predicted and rtype ~= 'predicted' then style_class = style_class .. '_predicted' end
		
		if rtype == 'isotope' or rtype == 'isotope nav' then
			style_class = 'Isotope_nav_' .. p.getHalflifeStyle(element)
		end
		
		return p.renderNavElementCell(element, style_class, 
			number==element.Z or p.compareSeriesList({result_series}, p.getSeriesDataByString(mark))
			or p.checkElementList(element,markele), rtype
		)
	end
	return ''
end

function p.renderTemplatePeriodicTableElementCell(element,span,styleclass,otheratt,mark,option)
	local body = '|'
	mark_style='border:2px solid black; margin:-2px;';
	local span_flag = false
	if span then span_flag = (tonumber(span) > 0) end
	if span_flag then body = body .. ' colspan=' .. tostring(span) .. ' ' end
	local divatt = ' class=\"' .. styleclass .. '\"'
	local divstyle = 'border:none;'
	if mark then divstyle = mark_style end
	divatt = divatt .. ' ' .. otheratt .. ' style=\"' .. divstyle .. '\"'
	
	if span_flag then body = body .. ' style=\"border:none\" |   \n| ' .. divatt .. ' | '
	else body = body .. ' ' .. divatt .. ' | ' end
	if option and option.index == true then
		body = body .. tostring(element.Z or '') .. '<br/>'
	end
	local display_name=element.Symbol or tostring(element.Z)
	if display_name then
		if element.Z > 118 then display_name = tostring(element.Z or 0) end
		if element.page then 
			body = body .. '[['_.._element.page_.._'|' .. display_name .. ']]'
		else
			body = body ..  display_name
		end
	end
	return body
end	

function p.renderIsotopePeriodicTableElementCell(element,span,styleclass,otheratt,option)
	local body = '|'
	local classtype=option.class_type
	local stabilitydata = element.stability or {stableCount=0}
	local stability_desc = ''
	if stabilitydata.stableCount > 0 then 
		stability_desc = tostring(stabilitydata.stableCount) .. '個穩定同位素'
	elseif stabilitydata.halflife and stabilitydata.halflife > 0 then
		stability_desc = '半衰期約' .. p.getTimeDesc(stabilitydata.halflife)
	end
	local magicNumber = ''
	if stabilitydata.magicNumber then magicNumber = ' Isotope_nav_' .. classtype .. 'magicnumber' end
	local span_flag = false
	if span then span_flag = (tonumber(span) > 0) end
	if span_flag then body = body .. ' colspan=' .. tostring(span) .. ' ' end
	local divatt = ' class=\"' .. styleclass .. magicNumber .. '\"'

	divatt = divatt .. ' ' .. otheratt .. ' '
	
	if span_flag then body = body .. ' style=\"border:none\" |   \n| '
		.. ' title=\"' .. stability_desc .. '\" ' .. divatt .. ' | '
	else body = body
		.. ' title=\"' .. stability_desc .. '\" ' .. divatt .. ' | '
	end
	body = body .. "<div" .. 
		" title=\"" .. stability_desc .. "\" " .. 
		"style=\"width:82%;height:82%;float:none;\" class=\"vectorMenu " .. styleclass .. "\">"
	if option and option.index == true then
		if element.page then 
			body = body .. '[['_.._element.page_.._'|' .. tostring(element.Z or '') .. ']]<br/>'
		else
			body = body .. tostring(element.Z or '') .. '<br/>'
		end
	end
	if element.Symbol then
		if element.isotopePage then 
			body = body .. '[['_.._element.isotopePage_.._'|' .. element.Symbol .. ']]'
		else
			body = body .. element.Symbol
		end
	end
	local isotope_str=''
	local has_iso=false
	if element.Isotope then
		for v, isotope in ipairs(element.Isotope) do
			if isotope.page then
				has_iso = true
				isotope_str = isotope_str .. '*' .. '[['_.._isotope.page_.._'|' .. isotope.name .. ']]\n'
			end
		end
		if has_iso then
			body = body .. '<div class=\"menu\">\n' .. isotope_str .. '</div>'
		end
	end
	body = body .. '</div>'
	return body
end	

function p.renderNavElementCell(element,styleclass,mark,rtype)
	local body=''
	local stabilitydata = element.stability or {stableCount=0}
	local stability_desc = ''
	if rtype == 'isotope' or rtype == 'isotope nav' then
		if stabilitydata.stableCount > 0 then 
			stability_desc = tostring(stabilitydata.stableCount) .. '個穩定同位素'
		elseif stabilitydata.halflife and stabilitydata.halflife > 0 then
			stability_desc = '半衰期約' .. p.getTimeDesc(stabilitydata.halflife)
		end
	end
	styles='position:relative; overflow:hidden; width:6px; height:8px; z-index:2;'
	mark_style='border:1px solid black; margin:-1px;';
	local ele_desc = element.name
	
	if rtype == 'isotope' or rtype == 'isotope nav' then
		ele_desc = ele_desc .. '（' .. stability_desc .. '）'
	elseif element.series then 
		ele_desc = ele_desc .. '（'
		if element.predictedSeries then ele_desc = ele_desc .. '預測為'  end
		ele_desc = ele_desc .. element.series[1] .. '）'
	end
	
	local divatt = ' class=\"' .. styleclass .. '\"'
	local divstyle = styles
	if mark then divstyle = divstyle .. mark_style end
	divatt = divatt .. ' style=\"' .. divstyle .. '\"'
	body = body .. '<div title=\"' .. ele_desc .. '\" ' .. divatt .. '>[[File:Transparent.gif|12px|link='
	if rtype == 'isotope nav' then
		if element.isotopePage then body = body .. element.isotopePage end
	else
		if element.page then body = body .. element.page end
	end
	body = body .. '|' .. ele_desc .. ']]</div>'
	return body
end

return p