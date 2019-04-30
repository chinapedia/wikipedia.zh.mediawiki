local getArgs = require('Module:Arguments').getArgs
local p = { PrimeTable = {} }
local numdata = nil
--[[
輸入一個數字n，檢查n是否為半完全數，如是列出最先搜到的和為自身之因數數列，否則輸出空陣列 (一般Lua函數)

注意 : 此為指數時間複雜問題
	--最差情況時間複雜度為 O(2^因數個數)
	--呼叫時請謹慎
]]
function p._checkSemiperfectNumber(input)
	local number = tonumber(input) or 0
	if p.PrimeTable.table_max == nil then p.PrimeTable = require('Module:Factorization') end
	local divs_all = p.PrimeTable._findDivisor(number)
	return p._checkSemiperfectNumberByDivisor(divs_all)
end

--[[
輸入因數列表檢查數字是否為半完全數，如是列出最先搜到的和為自身之因數數列，否則輸出空陣列 (一般Lua函數)

注意 : 此為指數時間複雜問題
	--最差情況時間複雜度為 O(2^因數個數)
	--呼叫時請謹慎
]]
function p._checkSemiperfectNumberByDivisor(input)
	if xpcall(function()_=#input pairs(input) end,function(_)end) == true then
		local flattern = function(a_table)
			local flattern_result = {}
			if xpcall(function()_=#a_table pairs(a_table) end,function(_)end) == true then
				for key,value in pairs(a_table) do
					if value == 1 then flattern_result[#flattern_result + 1] = key end
				end
				table.sort(flattern_result)
			end
			return flattern_result
		end
		local number = input[#input]
		local divs_all = input
		local divs = {}
		local result = {}
		local divs_subset = require("Module:Combination").getCombinationGenerator()
		local sum = 0
		for i = 1, #divs_all do if divs_all[i] ~= number then 
			divs[divs_all[i]] = 1 
			sum = sum + divs_all[i]
			result[divs_all[i]] = 1
		end end
		if sum < number then return {} end
		if sum == number then return flattern(result) end
		divs_subset:init(divs, 0)
	
		local calc_semi = sum - number
		local add_buffer = 0
		
		for i = 1, (#divs_all)-1 do
			divs_subset.count = i
			divs_subset:set({nil})
			divs_subset:fill()
			local middle_flag = true;
			while middle_flag == true do
				local inside_flag = true;
				while inside_flag == true do
					add_buffer=0
					for j=1,#(divs_subset.list) do
						add_buffer = add_buffer + divs_subset.list[j]
					end
					if calc_semi - add_buffer == 0 then
						for j=1,#(divs_subset.list) do
							result[divs_subset.list[j]] = nil
						end
						return flattern(result)
					end
					inside_flag = divs_subset:next()
				end
				
				local backtrack_flag = true;
				while backtrack_flag == true do
					local delete_num = divs_subset.list[#(divs_subset.list)]
					divs_subset.number_count[delete_num] = divs_subset.number_count[delete_num] - 1
					divs_subset.list[#(divs_subset.list)] = nil
					if #(divs_subset.list) <= 0 then break end
					middle_flag = divs_subset:next()
					divs_subset:fill()
					backtrack_flag = (#(divs_subset.list) < divs_subset.count) or #(divs_subset.list) <= 0
				end
				if #(divs_subset.list) <= 0 then break end
			end
		end
	end
	return {}
end

--[[
檢查一個數字是否為半完全數，如是列出最先搜到的和為自身之因數數列，否則不輸出 (支援#invoke:)

注意 : 此為指數時間複雜問題
	--最差情況時間複雜度為 O(2^因數個數)
	--呼叫時請謹慎
]]
function p.checkSemiperfectNumber(frame)
    local args
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = getArgs(frame) --frame.args
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
	return tostring(table.concat(p._checkSemiperfectNumber(args[1] or args['1']),','))
end

--[[
列出一個或多個整數與因數相關的性質 (支援#invoke:)
運算速度較快，適合進行大量輸出，如1000個以下的數字
]]
function p.numberDivisorInformation(frame)
	-- For calling from #invoke.
    local args
    local can_math = false
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = getArgs(frame) --frame.args
        local yesno = require('Module:Yesno')
        can_math = yesno(args['use math'] or args['use_math'])
        SemiperfectNumber = yesno(args['SemiperfectNumber'] or args['semiperfectNumber'] or 
        	args['Semiperfect Number'] or args['semiperfect Number'] or args['Semiperfect_Number'] or args['semiperfect_Number'] or 'yes')
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
    local body = ''
    local print_information = function(result_str, number, page, name, display, linkQ, bullet, describe, head_describe)
    	local head_text = args[tostring(number) .. (name or '數字')] or args[tostring(number) .. (page or '數字')] or 
    						args[tostring(number) .. (display or '數字')]

    	local tail_text = args[tostring(number) .. (page or '數字') .. "end"] or args[tostring(number) .. (page or '數字') .. "f"] or 
    					args[tostring(number) .. (name or '數字') .. "end"] or args[tostring(number) .. (name or '數字') .. "f"] or
    					args[tostring(number) .. (display or '數字') .. "end"] or args[tostring(number) .. (display or '數字') .. "f"]

    	result_str = result_str .. bullet .. (head_text or '')
    	result_str = result_str .. (head_describe or '')
    	if linkQ == true then
    		result_str = result_str .. "[[" .. page
    		if (display ~= nil) and (display ~= '') then result_str = result_str .. '|' .. display end
    		result_str = result_str .. "]]"
    	else
    		if (display ~= nil) and (display ~= '') then 
    			result_str = result_str .. display 
    		else
    			result_str = result_str .. name 
    		end
    	end
		if (describe ~= nil) and (describe ~= '') then
			result_str = result_str .. '，' .. describe
		end
		if tail_text ~= nil then result_str = result_str .. '，' .. tail_text end
		result_str = result_str .. '。\n'
		return result_str
    end
    --預設為只處理參數1的數字
	local num_start = args[1] or args['1']
    local num_end = args[1] or args['1']
    --讀取範圍
    if args['start'] then num_start = args['start'] end
    if args['end'] then num_end = args['end'] end
    --範圍內只有1個數字
    local one_number = false
    if num_start == num_end then one_number = true end
    --建立白名單
    local white_list = {}
    local white_index = {}
    local white_list_enable = false
    if args['white_list'] or args['white list'] then 
    	white_list = mw.text.split((args['white_list'] or args['white list']),',') 
    	white_list_enable = true
    end
	--建立白名單查表
	for first,second in pairs(white_list) do
		if tonumber(second) then
			white_index[tonumber(second)] = 1
		end
	end
	--未輸入視為預設，從零開始
    num_start = tonumber(num_start or 0)
    num_end = tonumber(num_end or 0)
	if mw.ustring.lower(tostring(num_start)) == 'nan' or mw.ustring.lower(tostring(num_end)) == 'nan' then 
		return require("Module:Error").error({[1]="錯誤：\'" .. (args[1] or args['1'] or args['start'] or args['end']) .. '\' '
			.. '不是一個數-{}-字。'
		})
	end
    --超出可處理範圍
    if p.PrimeTable.table_max == nil then p.PrimeTable = require('Module:Factorization') end
	if (num_start or 0) > p.PrimeTable.limit or (num_end or 0) > p.PrimeTable.limit
		or (num_start == nil) or (num_end == nil) 
		then 
			return require("Module:Error").error({[1]="錯誤：無法處理數-{}-字\'" .. (args[1] or args['1'] or args['start'] or args['end']) .. '\''})
	end
    
    if (num_end or 0) < (num_start or 0) then
    	return require("Module:Error").error({[1]="錯誤：範圍不正確"})
    end
    --輸入太多數字
    if (num_end or 0) - (num_start or 0) > 1510 then
    	if(#white_list > 1510) then
    		--無論是計算時間或者模板展開大小都有超出的風險
    		return require("Module:Error").error({[1]="錯誤：數字太多"})
    	end
    end
    local high_time_complexity = false
    local print_number_count = num_end - num_start + 1
    if white_list_enable then print_number_count = math.min( print_number_count, #white_list ) end
    
    --開始列印數字與因數分解相關的性質
    local number = tonumber(args[1] or args['1'] or 0)
	for number = num_start , num_end do
		--數字位於白名單內
		if(not white_list_enable or white_index[number] == 1) then
			if one_number == false then
				--如果數字很多建立章節 (用[[#數字|#數字]]可跳到的章節)
				body = body .. ';' .. tostring(number) .. '<span id=\"' .. tostring(number) .. '\">\n'
			end
			 if args[tostring(number)..'_head'] or args[tostring(number)..' head'] then 
			 	--列印位於章節頭部的資訊，如主條目
			 	local str = string.gsub((args[tostring(number)..'_head'] or args[tostring(number)..' head']) , "\n", "\n:")
			 	body = body .. str .. '\n'
			 end
			 
			if math.abs(math.floor(number) - number) > 0 then
				body = body .. p._simpleRealText(number, can_math, frame) .. '\n'
			else
				if p.PrimeTable.table_max == nil then p.PrimeTable = require('Module:Factorization') end
				--因數分解
				local primedata = p.PrimeTable._factorization(number)
				local divdata = p.PrimeTable._findDivisorByPrimeFactor(primedata)
	
				--因數分解發生錯誤，停止執行並返回錯誤
				if primedata.has_err ~= nil or divdata.has_err ~= nil then
					local Error = require("Module:Error")
					if primedata.has_err ~= nil then return body .. '\n' .. Error.error({[1]="錯誤：" .. primedata.has_err})
					else return body .. '\n' .. Error.error({[1]="錯誤：" .. divdata.has_err}) end
				end
				
				local is_prime = true --表示數字是否為質數
				local num_sqrt = math.sqrt(number) --表示數字的平方根
				local admirable_div = nil --表示佩服數的相減因數
				local is_unusual = nil --表示數字是否有大於平方根的質因數
				local div_sum = 0 --因數和
				local prime_count = 0 --相異質因數個數
				local div_sum_harmonic = 0 --因數調和總和
				local div_harmonic_avg = 0.001 --因數調和平均數
				local div_count = 0 --因數數量
				local exp_num = 0 --質因數總指數 (Ω)
				local prime_digits = 0
				local buffer_text = ''
				
				--掃描質因數
				for first,second in pairs(primedata) do
					if first ~= 'has_err' then 
						if first ~= 1 and first ~= number then 
							is_prime = false
							--判斷是否為不尋常數 (是否有大於平方根的質因數)
							if first > num_sqrt then is_unusual = first end
						end
						if first ~= 1 then
							--計算質因數總指數 (Ω)
							exp_num = exp_num + second
							--計算相異質因數數量
							prime_count = prime_count + 1
							prime_digits = prime_digits + 
								mw.ustring.len( mw.ustring.format( "%d",math.floor(math.abs(first)) ) )
							if second > 1 then prime_digits = prime_digits + 
								mw.ustring.len( mw.ustring.format( "%d",math.floor(math.abs(second)) ) ) end
						end
					end
				end
		
				--計算因數和
				for first,second in pairs(divdata) do
					if first ~= 'has_err' then 
						if second ~= number then div_sum = div_sum + second end
						div_sum_harmonic = div_sum_harmonic + (1.0 / second)
						div_count = div_count + 1
					end
				end
				--計算因數的調和平均數
				div_harmonic_avg = (div_count + 0.000000) / div_sum_harmonic
				for first,second in pairs(divdata) do
					if first ~= 'has_err' then 
						--判斷數字是否為佩服數
						if div_sum - second * 2 == number then admirable_div = second end
					end
				end
		
				--產生<math>格式，以印出質因數分解於條目
				local times = " x "
				local pow_h = "<sup>"
				local pow_f = "</sup>"
				if can_math then
					times = "\\times "
					pow_h = "^{"
					pow_f = "} "
				end
				--印出質因數分解於條目
				local factors_str = p.PrimeTable.create_factorization_string(primedata, times, pow_h, pow_f)
				if can_math then factors_str = frame:callParserFunction{name = "#tag:math", args = {factors_str}} end
				--開始列印整數性質
				if is_prime == true then
					--質因數分解只有一個元素的情況
					if number == 0 then
						body = body .. '*[[0|中性數]]。\n' 
					elseif number == 1 then
						body = body .. '*[[单位數字|單位數]]。\n'
					elseif number == -1 then
						body = body .. '*[[負數|負數]][[单位數字|單位]]。\n' 
					else
						--是個質數
						body = body .. '*'
						if p.PrimeTable.lists[number] ~= nil then
							body = body .. '第' .. tostring(p.PrimeTable.lists[number]) .. '個'
						end
						body = body .. '[[質數|質數]]。\n' 
						
						if p.PrimeTable.table_max == nil then p.PrimeTable = require('Module:Factorization') end
						--查質數表，找前一個和下一個質數
						local next_p = p.PrimeTable._nextPrime(number)
						local last_p = p.PrimeTable._lastPrime(number)
						if number > 7919 then high_time_complexity = true end
						if tonumber(next_p) ~= nil or tonumber(last_p) ~= nil then
							--判斷是否為孿生質數
							if (next_p or number) - number == 2 or number - (last_p or number) == 2 then
								body = body .. '**' .. (args[tostring(number) .. "孿生質數"] or '')
								body = body .. "[[孪生素数|孪生素数]]，" 
								local is_printted = false
								if tonumber(next_p) ~= nil then
									if (next_p or number) - number == 2 then
										is_printted = true
										body = body .. '為（' .. number ..'、 [['_.._next_p_..'|' .. next_p ..']]）'
									end
	
									if number - (last_p or number) == 2 then
										if is_printted == true then body = body .. '以及' 
										else body = body .. '為' end
										body = body .. '（[['_.._last_p_..'|' .. last_p ..']]、 ' .. number ..'）'
									end
									
									body = body .. '\n'
								end
							end
						end
					end
				else 
					if number < 0 then 
						body = print_information(body, number, "负数", "負數", nil, true, '*')
					end
					--列印所有因數和質因數
					local div_string = ''
	
					body = print_information(body, number, "合数", "合數", nil, true, '*', (args["因數說明h"] or "[[因數|正因數]]有") .. 
						table.concat( divdata, '、', 1, #divdata - 1 ) ..'和' .. tostring(number) .. (args["因數說明f"] or '') )
					body = print_information(body, number, "整数分解", "整數分解", "質因數分解", true, "*:", factors_str)
					if number > 2 then
						--列印純粹因數和相關性質 (虧數/完全數/過剩數)
						if div_sum ~= number then
							local tail_str=''
							if div_sum < number then
								body = body .. '*' .. (args[tostring(number) .. "虧數"] or '')
								body = body .. '[[亏数|亏数]]'
								tail_str = "，虧度為" .. tostring(number-div_sum)
								if args[tostring(number) .. "虧數f"] ~= nil then tail_str = tail_str .. '，' .. args[tostring(number) .. "虧數f"] end
							else
								body = body .. '*' .. (args[tostring(number) .. "過剩數"] or '')
								body = body .. '[[过剩数|过剩数]]'
								tail_str = "，盈度為" .. tostring(div_sum-number)
								if args[tostring(number) .. "過剩數f"] ~= nil then tail_str = tail_str .. '，' .. args[tostring(number) .. "過剩數f"] end
							end
							body = body .. '，[[除數函數|真因數和]]為' .. tostring(div_sum) .. tail_str .. '\n'
						else
							body = print_information(body, number, "完全数", "完全數", nil, true, '*')
						end
						if SemiperfectNumber and print_number_count <= 1010 and div_sum >= number then --過剩數才需探討是否半完全或奇異
							--最差情況時間複雜度為 O(2^因數個數)
							--因此根據要做的數字數量決定是否放棄計算
							if (#divdata <= 12 or (print_number_count <= 505 and #divdata <= 14) 
								or (print_number_count <= 200 and #divdata <= 16) or (print_number_count <= 10 and #divdata <= 20)
								 or (print_number_count <= 2 and #divdata <= 25) or (print_number_count <= 1 and #divdata <= 32) ) then
								--此為指數時間複雜度演算法，因此當數字量大於505時則放棄計算
								local simi_div = p._checkSemiperfectNumberByDivisor(divdata)
								if #simi_div > 0 then
									buffer_text = ''
									if div_sum ~= number then 
										buffer_text = "和為本身的其中一組因數為[["_.._tostring(_table.concat(simi_div,_"|" .. tostring( table.concat(simi_div, "]]、 [[")_)_.._"|") ) .. "]]"
									end
									body = print_information(body, number, "半完全数", "半完全數", nil, true, "**", buffer_text )
								else
									body = print_information(body, number, "奇異數_(數論)", "奇异数", "奇異數", true, "**")
								end
								if #divdata > 16 then high_time_complexity = true end
							end
						end
						--列印與因數平均數相關性質
						if math.abs(div_harmonic_avg - math.floor(div_harmonic_avg)) <= 1e-6 then
							body = print_information(body, number, "歐爾調和數", "欧尔调和数", nil, true, '*', 
								"因數[[调和平均数|调和平均数]]為" .. string.format("%d",math.floor(div_harmonic_avg)))
						end
						--列印與質因數相關性質
						if is_unusual ~= nil then 
							body = print_information(body, number, "不尋常數", "不寻常数", nil, true, '*', 
								"大於平方根的質因數為" .. tostring(is_unusual) )
						end
						if exp_num == 2  then 
							body = print_information(body, number, "半素数", "半質數", nil, true, '*' )
						end
						if admirable_div ~= nil then 
							body = print_information(body, number, "佩服數", "佩服数", nil, true, '*', 
								"佩服[[因數|因數]]為" .. tostring(admirable_div) )
						end
						--列印無平方數因數的數之相關性質
						if exp_num == prime_count then 
							body = print_information(body, number, 
									"无平方数因数的数", "無平方數因數的數", nil, true, '*' )
							if prime_count == 3 then 
								body = print_information(body, number, "楔形数", "楔形數", nil, true, "**" )
							end
						end
					end
					--列印自然數相關性質
					if number > -1 then
						if math.abs(num_sqrt - math.floor(num_sqrt)) <= 1e-6 then
							body = print_information(body, number, "平方数", "平方數", nil, true, '*', 
								"為" .. string.format("%d", math.floor(num_sqrt)) .. "的平方" )
						end
					end
				end
				if number > -1 and number ~=1 then
					if math.abs(math.ceil(num_sqrt) - math.floor(num_sqrt)) > 1e-6 and math.abs(math.ceil(num_sqrt) * math.floor(num_sqrt) - number) <= 1e-6 then
						body = print_information(body, number, "普洛尼克数", "普洛尼克數", nil, true, '*', 
							"為" .. mw.ustring.format( "%d", math.floor(num_sqrt) ) .."與"
								.. mw.ustring.format( "%d", math.ceil(num_sqrt) ) .."的乘積" )
					end
					if is_prime ~= true then
						local num_digts = mw.ustring.len( mw.ustring.format( "%d",math.floor(math.abs(number)) ) ) 
						if prime_digits == num_digts then
							body = print_information(body, number, "等數位數", "等数位数", nil, true, '*', nil, "[[十进制|十进制]]的")
						elseif prime_digits < num_digts then
							body = print_information(body, number, "節儉數", "节俭数", nil, true, '*', nil, "[[十进制|十进制]]的")
						elseif prime_digits > num_digts then
							body = print_information(body, number, "奢侈數", "奢侈数", nil, true, '*', nil, "[[十进制|十进制]]的")
						end
					end
				end
			end
			--列印其他性質
			if args[number] or args[tostring(number)] then 
				local str = (args[number] or args[tostring(number)])
				body = body .. str .. '\n'
			end
		end
	end 
	if high_time_complexity == true then body = body .. '[[Category:使用高時間複雜度演算法的條目|Category:使用高時間複雜度演算法的條目]]' end
	return mw.text.trim(body)
end

--用於少量數字(十幾個) 性質輸出 (支援客製化)
function p.manyNumberInformation(frame)
	numdata = require("Module:Number/data")
	local can_math = false
	local args
	if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        local yesno = require('Module:Yesno')
        args = getArgs(frame, {readOnly = false}) --frame.args
        can_math = yesno(args['use math'] or args['use_math'])
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
    if _flag_mass_output == nil then _flag_mass_output = true end
    local count = tonumber(args['count']) or 1
    local number = args[1] or args['1']
    local body = ''
    if number == nil then return '' end
    for i = number,number+count+1 do
			if count > 1 then
				--如果數字很多建立章節 (用[[#數字|#數字]]可跳到的章節)
				body = body .. ';' .. tostring(i) .. '<span id=\"' .. tostring(i) .. '\">\n'
			end
			 if args[tostring(i)..'_head'] or args[tostring(i)..' head'] then 
			 	--列印位於章節頭部的資訊，如主條目
			 	local str = string.gsub((args[tostring(i)..'_head'] or args[tostring(i)..' head']) , "\n", "\n:")
			 	body = body .. str .. '\n'
			 end
			if(can_math)then if args[1] then args[1] = i frame.args[1] = i end if args['1'] then args['1'] = i frame.args['1'] = i end
				body = body .. p.singleNumberInformation(frame) .. '\n'
			else if args[1] then args[1] = i end if args['1'] then args['1'] = i end
				body = body .. p.singleNumberInformation(args) .. '\n'
			end
			 --列印其他性質
			if args[i] or args[tostring(i)] then 
				local str = (args[i] or args[tostring(i)])
				body = body .. str .. '\n'
			end
	end
	body = mw.text.trim(body)
	if _flag_use_user_define_string == true then body = body .. "[[Category:使用自定義Module:Number語句的頁面|Category:使用自定義Module:Number語句的頁面]]" end
	return body
end

function p._checkAddSubtract(num_str)
	local body = ''
	local real, imag = 0, 0
	local split_str = mw.text.split(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(
			num_str or '',
		'%s+',''),'%++([%d%.])',',+%1'),'%++([ij])',',+1%1'),'%-+([%d%.])',',-%1'),'%-+([ij])',',-1%1'),'%*+([%d%.])',',*%1'),'%*+([ij])',',*1%1'),'%/+([%d%.])',',/%1'),'%/+([ij])',',/1%1'),',')
	local first = true
	local continue = false
	
	for k,v in pairs(split_str) do
		continue = false
		local val = mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.text.trim(v),'[ij]+','i'),'^(%.)','0%1'),'^([%d%.])','+%1'),'([%+%-])([%d%.])','%1\48%2'),'^([ij])','+1%1')
		if mw.ustring.find(val,"%/") or mw.ustring.find(val,"%*") then return end
		if val == nil or val == '' then if first == true then first = false continue = true else return end end
		if not continue then
			local num_text = mw.ustring.match(val,"[%+%-][%d%.]+i?")
			if num_text ~= val then return end
			local num_part = tonumber(mw.ustring.match(num_text,"[%+%-][%d%.]+"))
			if num_part == nil then return end
			if mw.ustring.find(num_text,"i") then
				imag = imag + num_part
			else
				real = real + num_part
			end
		end
	end
	return real, imag
end

function p._checkInf(num_str)
	local inf_siring = {'inf','infinitas','infinitas','infinity','無限','无限','无限大','無限大','無窮','无穷','无穷大','無窮大','∞','-∞','+∞',
		'正無限','正无限','正无限大','正無限大','正無窮','正无穷','正无穷大','正無窮大',
		'負無限','負无限','負无限大','負無限大','負無窮','負无穷','負无穷大','負無窮大'
	}
	for k,v in pairs(inf_siring) do
		if num_str == v then
			return tonumber("inf")
		end
	end
end

function p._simpleRealText(number, can_math, frame)
	local body = ''
	body = '*' .. tostring(number) .. '是一個[[实数|实数]]。\n'
	if number < 0 then
		body = body .. '*' .. '[[负数|负数]]。\n'
	else
		body = body .. '*' .. '[[正數|正數]]。\n'
	end
	if math.abs(math.floor(1 / number) - 1 / number)  <= 1e-15 then -- 要求超高精度
		body = body .. '*' .. tostring(1 / number) .. '的[[倒数|倒数]]。\n'
	end
	if math.abs(math.floor(number * number) - number * number) <= 1e-15 then -- 要求超高精度
		body = body .. '*' .. tostring(number * number) .. '的[[平方根|平方根]]。\n'
	end
	if math.abs(number - math.pi) <= 1e-15 then -- 要求超高精度
		body = body .. '*[[圓周率|圓周率]]。\n'
	end
	return body
end

function p._simpleComplexText(real, imag, can_math, frame)
	local body = ''
	
	if cmath==nil then cmath = require("Module:Complex Number").cmath.init() end
	local the_number = cmath.getComplexNumber(real, imag)
	local length = cmath.abs(the_number)
	local argument = cmath.arg(the_number)
	local complex_str, gfactors_str = tostring(the_number), ""
	local sq_len = math.sqrt(length)
	local sq_real, sq_imag = sq_len * math.cos(argument/2.0), sq_len * math.sin(argument/2.0)
	local sq_num, sq_str = cmath.getComplexNumber(sq_real, sq_imag), ""

	if can_math then complex_str = frame:callParserFunction{name = "#tag:math", args = {complex_str}} end
		
	body = '*' .. complex_str .. '是一個[[复数_(数学)|複數]]。\n'
	if numdata._is_integer(real) and numdata._is_integer(imag) then
		body = body ..'*' .. '[[高斯整數|高斯整數]]。\n'
		local is_gprime = cmath.is_prime_quadrant1(the_number) or cmath.is_prime_quadrant1(-the_number) or
			cmath.is_prime_quadrant1(cmath.getComplexNumber(0, 1) * the_number) or
			cmath.is_prime_quadrant1(cmath.getComplexNumber(0, -1) * the_number)
		if is_gprime ~= nil then
			if not is_gprime then
				local gprimedata, gfactors = p.PrimeTable._gaussianFactorization(tostring(the_number)), {}
				--產生<math>格式，以印出質因數分解於條目
				local times = " x "
				local pow_h = "<sup>"
				local pow_f = "</sup>"
				local left_ = "("
				local right_ = ")"
				if can_math then
					times = "\\times "
					pow_h = "^{"
					pow_f = "} "
					left_ = "\\left( "
					right_ = "\\right) "
				end
				for first,second in pairs(gprimedata) do
					if first ~= 'has_err' then 
						local complex_num = cmath.toComplexNumber(first) 
						if complex_num.real ~= 0 and complex_num.imag ~= 0 then
							gfactors[left_ .. tostring(first) .. right_] = second
						else
							gfactors[first] = second
						end
					end
				end
				--印出質因數分解於條目
				gfactors_str = p.PrimeTable.create_factorization_string(gfactors, times, pow_h, pow_f)
				if mw.text.trim(gfactors_str) == '' then is_gprime = true end
				if can_math then 
					gfactors_str = frame:callParserFunction{name = "#tag:math", args = {gfactors_str}} 
				end
			end
		end
		if is_gprime then body = body ..'*' .. '[[高斯整數#作为唯一分解整环|高斯質數]]。\n'
		elseif length > 1 then body = body ..'*' .. '[[高斯整數#作为唯一分解整环|高斯]][[合数|合数]]。\n'
			body = body ..'*:' .. '[[高斯整數#作为唯一分解整环|高斯]][[整数分解|整数分解]]為，' .. gfactors_str ..'。\n'
		end
	end
	if numdata._is_integer(sq_real) and numdata._is_integer(sq_imag) then
		sq_str = tostring(sq_num)
		if can_math then sq_str = frame:callParserFunction{name = "#tag:math", args = {sq_str}} end
		body = body ..'*' .. '[[平方數|平方數]]，為' .. tostring(sq_str) .. '的平方。\n'
	end

	if numdata._is_integer(length) then
		body = body ..'*' .. '[[絕對值|絕對值]]為' .. tostring(length) .. '。\n'
	else
		body = body ..'*' .. '[[絕對值|絕對值]]約為' .. string.format("%.4f",length) .. '。\n'
	end

	local deg = math.deg(argument)
	if numdata._is_integer(deg) then
		body = body ..'*' .. '[[幅角|幅角]]為' .. tostring(deg) .. '[[度_(角)|度]]。\n'
	else
		body = body ..'*' .. '[[幅角|幅角]]約為' .. string.format("%.4f",deg) .. '[[度_(角)|度]]。\n'
	end

	return body
end

--用於單一數字性質輸出 (支援客製化)
function p.singleNumberInformation(frame)
	if numdata == nil then numdata = require("Module:Number/data") end
	-- For calling from #invoke.
    local args
    local can_math, SemiperfectNumber = false, true
	local all_list = {"負數","自然數","整數","質數","孿生質數","梅森質數","高斯質數","合數","質因數分解","高斯整數分解","虧數",
		"過剩數","完全數","半完全數","本原半完全數","奇異數","歐爾調和數","高合成數","不尋常數","半質數","佩服數","無平方數因數的數",
		"楔形數","平方數","立方數","普洛尼克數","佩爾數","斐波那契數","階乘","質數階乘","自我數","哈沙德數","全哈沙德數","等數位數",
		"節儉數","奢侈數","史密夫數","不可及數","可作圖多邊形"};
	local print_list, addit_print_list, print_prop_list, print_black_list, black_list = {}, {}, {}, {}, {"自然數","整數","高斯整數分解"};
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = getArgs(frame) --frame.args
        local yesno = require('Module:Yesno')
        can_math = yesno(args['use math'] or args['use_math'])
        SemiperfectNumber = yesno(args['SemiperfectNumber'] or args['semiperfectNumber'] or 
        	args['Semiperfect Number'] or args['semiperfect Number'] or args['Semiperfect_Number'] or args['semiperfect_Number'] or 'yes')
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
    if args['other_print_list'] or args['other print list'] then
    	addit_print_list = mw.text.split(args['other_print_list'] or args['other print list'] or '',',')
   	end
    if args['print_list'] or args['print list'] then
        print_list = mw.text.split(args['print_list'] or args['print list'] or '',',')
    end
    if args['print_black_list'] or args['print black list'] then
        print_black_list = mw.text.split(args['print_black_list'] or args['print black list'] or '',',')
    end
    local print_list_table, print_list_array = {}, {}
    for k,v in pairs(print_list) do local val_iter = mw.text.trim(v) if val_iter ~= '' then print_list_table[val_iter] = 1 end end
	for k,v in pairs(print_list_table) do print_list_array[#print_list_array + 1] = k end
	if #print_list_array <= 0 then
		for k,v in pairs(all_list) do local val_iter = mw.text.trim(v) if val_iter ~= '' then print_list_table[val_iter] = 1 end end
	end
	for k,v in pairs(print_black_list) do 
		local val_iter = mw.text.trim(v) 
		if val_iter ~= '' then 
			print_list_table[val_iter] = nil 
		end 
	end
	for k,v in pairs(black_list) do 
		local val_iter = mw.text.trim(v) 
		if val_iter ~= '' then 
			print_list_table[val_iter] = nil 
		end 
	end
	for k,v in pairs(addit_print_list) do 
		local val_iter = mw.text.trim(v) 
		if val_iter ~= '' then 
			print_list_table[val_iter] = 1
		end
	end
	if #print_list_array > 0 then
		for k,v in pairs(print_list) do 
			local val_iter = mw.text.trim(v) 
			if (tonumber(print_list_table[val_iter]) or 0) == 1 then
				print_prop_list[#print_prop_list + 1] = val_iter
				print_list_table[val_iter] = print_list_table[val_iter] + 1
			end
		end
	else
		for k,v in pairs(all_list) do 
			local val_iter = mw.text.trim(v) 
			if (tonumber(print_list_table[val_iter]) or 0) == 1 then
				print_prop_list[#print_prop_list + 1] = val_iter
				print_list_table[val_iter] = print_list_table[val_iter] + 1
			end
		end
	end
    local body, number = '', tonumber(args[1] or args['1'])

	--例外處理 : NaN因平方根不存在，造成短除法，除質數無窮迴圈
	if mw.ustring.lower(tostring(number)) == 'nan' then 
		return require("Module:Error").error({[1]="錯誤：\'" .. (args[1] or args['1'] or args['start'] or args['end']) .. '\' '
			.. '不是一個數-{}-字。'
		})
	end
	
	--例外處理 : 預期內的數字，但不應送進短除法做因數分解的數字
	local real, imag = (number or 0), 0
	if number == nil then 
		local test_str = mw.ustring.lower(mw.text.trim(args[1] or args['1']))
		number = p._checkInf(test_str)
		if number == nil then 
			real,imag = p._checkAddSubtract(test_str)
			if real~=nil and imag~=nil then
				number = math.sqrt(real*real+imag*imag)
			end
		end
		--例外處理 : 不是數字的東西，直接告知錯誤
		if number == nil then 
			return require("Module:Error").error({[1]="錯誤：\'" .. (args[1] or args['1'] or args['start'] or args['end']) .. '\' '
				.. '不是一個數-{}-字。'
			})
		end
	end
	
	--超出可處理範圍
    if p.PrimeTable.table_max == nil then p.PrimeTable = require('Module:Factorization') end
	if (number or 0) > p.PrimeTable.limit or -(number or 0) > p.PrimeTable.limit then 
			return require("Module:Error").error({[1]="錯誤：無法處理數-{}-字 \'" .. (args[1] or args['1'] or args['start'] or args['end']) .. '\' ，'
				.. '其[[絕對值|絕對值]]已超出支援的處理範圍。'
			})
	end
	
	if imag ~= 0 then return p._simpleComplexText(real, imag, can_math, frame) end

	--例外處理 : 非整數的數字被送進短除法，當然在根號n內不會整除，因此會被當成質數，所以不能將非整數的數字被送進短除法做因數分解
	if math.abs(math.floor(number) - number) > 0 then
		return p._simpleRealText(number, can_math, frame)
	end
	
	--------------------------------------------
	----- 例外處理結束，開始短除法因數分解 -----
	--------------------------------------------
	
	--因數分解
	local primedata = p.PrimeTable._factorization(number)
	local divdata = p.PrimeTable._findDivisorByPrimeFactor(primedata)
 	--因數分解發生錯誤，停止執行並返回錯誤
	if primedata.has_err ~= nil or divdata.has_err ~= nil then
		local Error = require("Module:Error")
		if primedata.has_err ~= nil then return body .. '\n' .. Error.error({[1]="錯誤：" .. primedata.has_err})
		else return body .. '\n' .. Error.error({[1]="錯誤：" .. divdata.has_err}) end
	end
	
	--產生<math>格式，以印出質因數分解於條目
	local times = " x "
	local pow_h = "<sup>"
	local pow_f = "</sup>"
	local left_ = "("
	local right_ = ")"
	if can_math then
		times = "\\times "
		pow_h = "^{"
		pow_f = "} "
		left_ = "\\left( "
		right_ = "\\right) "
	end
	
	local is_gprime = true
	local gfactors_str = ''
	if tonumber(print_list_table["高斯整數分解"] or -1) >= 1 then
		if cmath==nil then cmath = require("Module:Complex Number").cmath.init() end
		local cnum = cmath.toComplexNumber(tostring(number))
		is_gprime = cmath.is_prime_quadrant1(cnum)
		if is_gprime ~= nil then
			if not is_gprime then
				local gprimedata, gfactors = p.PrimeTable._gaussianFactorization(tostring(number)), {}
				for first,second in pairs(gprimedata) do
					if first ~= 'has_err' then 
						local complex_num = cmath.toComplexNumber(first) 
						if complex_num.real ~= 0 and complex_num.imag ~= 0 then
							gfactors[left_ .. tostring(first) .. right_] = second
						else
							gfactors[first] = second
						end
					end
				end
				--印出質因數分解於條目
				gfactors_str = p.PrimeTable.create_factorization_string(gfactors, times, pow_h, pow_f)
				if mw.text.trim(gfactors_str) == '' then is_gprime = true end
				if can_math then 
					gfactors_str = frame:callParserFunction{name = "#tag:math", args = {gfactors_str}} 
				end
			end
		end
	end
	
	local is_prime = true --表示數字是否為質數
	local num_sqrt = math.sqrt(number) --表示數字的平方根
	local admirable_div = nil --表示佩服數的相減因數
	local is_unusual = nil --表示數字是否有大於平方根的質因數
	local div_sum = 0 --因數和
	local prime_count = 0 --相異質因數個數
	local div_sum_harmonic = 0 --因數調和總和
	local div_harmonic_avg = 0.001 --因數調和平均數
	local div_count = 0 --因數數量
	local exp_num = 0 --質因數總指數 (Ω)
	local prime_digits = 0
	local buffer_text = ''
	local mersenne_prime_for_perfect_number = ''
	--掃描質因數
	for first,second in pairs(primedata) do
		if first ~= 'has_err' then 
			if first ~= 1 and first ~= number then 
				is_prime = false
			end
			if first ~= 1 then
				--判斷是否為不尋常數 (是否有大於平方根的質因數)
				if first > num_sqrt then is_unusual = first end
				--計算質因數總指數 (Ω)
				exp_num = exp_num + second
				--計算相異質因數數量
				prime_count = prime_count + 1
				prime_digits = prime_digits + 
				mw.ustring.len( mw.ustring.format( "%d",math.floor(math.abs(first)) ) )
				if second > 1 then prime_digits = prime_digits + 
				mw.ustring.len( mw.ustring.format( "%d",math.floor(math.abs(second)) ) ) end
			end
		end
	end
	
	--計算因數和
	for first,second in pairs(divdata) do
		if first ~= 'has_err' then 
			if second ~= number then div_sum = div_sum + second end
			div_sum_harmonic = div_sum_harmonic + (1.0 / second)
			div_count = div_count + 1
		end
	end
	
	--計算因數的調和平均數
	div_harmonic_avg = (div_count + 0.000000) / div_sum_harmonic
	for first,second in pairs(divdata) do
		if first ~= 'has_err' then 
			--判斷數字是否為佩服數
			if div_sum - second * 2 == number then admirable_div = second end
		end
	end
	
	--印出質因數分解於條目
	local factors_str = p.PrimeTable.create_factorization_string(primedata, times, pow_h, pow_f)
	if can_math then 
		factors_str = frame:callParserFunction{name = "#tag:math", args = {factors_str}} 
		if div_sum == number then
			mersenne_prime_for_perfect_number= "2^{" .. tostring(primedata[2]) .. "}\\times\\left( 2^{" .. 
				tostring(primedata[2]+1) .. "}-1\\right)"
			mersenne_prime_for_perfect_number = frame:callParserFunction{name = "#tag:math", args = {mersenne_prime_for_perfect_number}} 
		end
	end
	
	local simi_div = {}
	if div_sum > number and number > 0 then 
		if SemiperfectNumber and #divdata <= 32 then
			--此為指數時間複雜度演算法，因此當因數超過32個時則放棄計算
			simi_div = p._checkSemiperfectNumberByDivisor(divdata)
		end
	end
	
	local printer = numdata.getIntegerInfoPrinter()
	printer:init({
		number=number,
		is_prime=is_prime,
		admirable_div=admirable_div,
		is_unusual=is_unusual,
		div_sum=div_sum,
		prime_count=prime_count,
		div_sum_harmonic=div_sum_harmonic,
		div_harmonic_avg=div_harmonic_avg,
		div_count=div_count,
		exp_num=exp_num,
		prime_digits=prime_digits,
		divdata=divdata,
		primedata=primedata,
		simi_div=simi_div,
		factors_str=factors_str,
		mersenne_prime_for_perfect_number=mersenne_prime_for_perfect_number,
		is_gprime=is_gprime,
		gfactors_str=gfactors_str,
	});

	local text = ''
	for k,v in pairs(print_prop_list) do
		if _flag_use_user_define_string == nil and mw.text.trim(args[v] or "") ~= "" then _flag_use_user_define_string = true end
		text = mw.text.trim(printer:printInfo(args[v] or "",v) or '')
		if text ~= nil and text ~= '' then
			body = body .. text ..'\n'
		end
	end
	body = mw.text.trim(body)
	if (_flag_use_user_define_string == true) and 
		(not (_flag_mass_output == true)) then body = body .. "[[Category:使用自定義Module:Number語句的頁面|Category:使用自定義Module:Number語句的頁面]]" end
	return body
end

return p