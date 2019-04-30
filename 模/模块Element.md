local p = {}
local origArgs
local error = require( 'Module:Error' )
local element_data = require( 'Module:Element/data' )
local series_name_data = {{"錒系元素", "锕系元素", "錒系金屬", "锕系金属", "actinide"},{"鹼金屬", "碱金属", "alkali metal"},{"鹼金屬（預測）", "碱金属（预测）", "alkali metal (predicted)"},{"鹼土金屬", "碱土金属", "alkaline earth metal"},{"鹼土金屬（預測）", "碱土金属（预测）", "alkaline earth metal (predicted)"},{"雙原子非金屬", "双原子非金属", "diatomic nonmetal"},{"雙原子非金屬（預測）", "双原子非金属（预测）", "diatomic nonmetal (predicted)"},{"多原子非金屬", "多原子非金属", "polyatomic nonmetal"},{"多原子非金屬（預測）", "多原子非金属（预测）", "polyatomic nonmetal (predicted)"},{"eka-超錒系元素", "eka-超锕系元素", "下超錒系元素", "eka-superactinide"},{"eka-超錒系元素（預測）", "eka-超锕系元素（预测）", "eka-superactinide (predicted)"},{"惰性氣體", "惰性气体", "稀有氣體", "稀有气体", "noble gas"},{"惰性氣體（預測）", "惰性气体（预测）", "稀有氣體（預測）", "稀有气体（预测）", "noble gas (predicted)"},{"鹵素", "卤素", "halogen"},{"鹵素（預測）", "卤素（预测）", "halogen (predicted)"},{"金屬", "金属", "metal"},{"類金屬", "类金属", "metalloid"},{"類金屬（預測）", "类金属（预测）", "metalloid (predicted)"},{"鑭系元素", "镧系元素", "鑭系金屬", "镧系金属", "lanthanide"},{"其他非金屬", "其他非金属", "非金属", "非金屬", "other non-metal"},{"其他非金屬（預測）", "其他非金属（预测）", "非金屬（預測）", "other non-metal (predicted)"},{"貧金屬", "贫金属", "主族金屬", "主族金属", "post-transition metal"},{"貧金屬（預測）", "贫金属（预测）", "主族金屬（預測）", "主族金属（预测）", "post-transition metal (predicted)"},{"超錒系元素", "超锕系元素", "superactinide"},{"超錒系元素（預測）", "超锕系元素（预测）", "superactinide (predicted)"},{"過渡金屬", "过渡金属", "过渡元素", "過渡元素", "transition metal"},{"過渡金屬（預測）", "过渡金属（预测）", "过渡元素（预测）", "過渡元素（預測）", "transition metal (predicted)"},{"超臨界原子", "離子態", "超临界原子", "离子态", "supercritical atoms", "supercritical atoms (predicted)"},{"無電子", "无电子", "no electron"},{"可能不存在", "maybe not exist"},{"s區元素", "s区元素", "s區", "s区", "s block"},{"s區元素（預測）", "s区元素（预测）", "s區（預測）", "s区（预测）", "s block (predicted)"},{"p區元素", "p区元素", "p區", "p区", "p block"},{"p區元素（預測）", "p区元素（预测）", "p區（預測）", "p区（预测）", "p block (predicted)"},{"d區元素", "d区元素", "d區", "d区", "d block"},{"d區元素（預測）", "d区元素（预测）", "d區（預測）", "d区（预测）", "d block (predicted)"},{"ds區元素", "ds区元素", "ds區", "ds区", "ds block"},{"ds區元素（預測）", "ds区元素（预测）", "ds區（預測）", "ds区（预测）", "ds block (predicted)"},{"f區元素", "f区元素", "f區", "f区", "f block"},{"f區元素（預測）", "f区元素（预测）", "f區（預測）", "f区（预测）", "f block (predicted)"},{"g區元素", "g区元素", "g區", "g区", "g block"},{"g區元素（預測）", "g区元素（预测）", "f區（預測）", "g区（预测）", "g block (predicted)"},{"h區元素", "h区元素", "h區", "h区", "h block"},{"h區元素（預測）", "h区元素（预测）", "h區（預測）", "h区（预测）", "h block (predicted)"},{"未知特性", "未知", "化學性質未知", "化学性质未知", "unknown", "unknown chemical properties"}}

function p.symbol(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = pframe.args
	return p._symbol(args)
end

function p.link(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = pframe.args
	return p._link(args)
end

function p.check(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = pframe.args
	return p._check(args)
end

function p.neutron(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = pframe.args
	return p._neutron(args)
end

function p._neutron(args)
	--去除模板引用時可能產生的空格
	eleString='' if (args[1] and args[1] ~= '') then eleString = string.gsub(args[1] , "%s$", "") else return '' end
	eleid = p.getListID(eleString)
	ele1 = element_data[eleid]
	if (eleid==-1) then
		return ''
	end
	if (ele1.correct and ele1.correct  ~= '') then
		return ''
	end
	if (ele1.N and ele1.N ~= '') then
		return ele1.N
	end
	return ''
end

function p.compare_series(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	arg1=''	if (args[1] and args[1] ~= '') then	arg1 = string.gsub(args[1] , "%s$", "") end
	arg2=''	if (args[2] and args[2] ~= '') then	arg2 = string.gsub(args[2] , "%s$", "") end
	return p.compareSeries(arg1, arg2)
end

function p.compareSeries(series1, series2)
	checked = false
	for v, x in ipairs(series_name_data) do
		for v1, x1 in ipairs(x) do
			if (x1 == series1) then 
				series_left = {x[1]}
				checked = true
				break
			end
		end
		if checked then break end
	end
	if not checked then
		eleSeries = p.getSeries({series1})
		eleSeries = mw.text.split( table.concat(eleSeries, ',') .. ',' .. series1 , ',' ) 
		for index, it in ipairs(eleSeries) do
			checked = false
			for v, x in ipairs(series_name_data) do
				for v1, x1 in ipairs(x) do
					if (x1 == it) then 
						eleSeries[index] = x[1]
						checked = true
						break
					end
				end
				if checked then break end
			end
		end
		series_left = eleSeries
	end
	
	checked = false
	for v, x in ipairs(series_name_data) do
		for v1, x1 in ipairs(x) do
			if (x1 == series2) then 
				series_right = {x[1]}
				checked = true
				break
			end
		end
		if checked then break end
	end
	if not checked then
		eleSeries = p.getSeries({series2})
		eleSeries = mw.text.split( table.concat(eleSeries, ',') .. ',' .. series2 , ','  ) 
		for index, it in ipairs(eleSeries) do
			checked = false
			for v, x in ipairs(series_name_data) do
				for v1, x1 in ipairs(x) do
					if (x1 == it) then 
						eleSeries[index] = x[1]
						checked = true
						break
					end
				end
				if checked then break end
			end
		end
		series_right = eleSeries
	end
	if series_left.predicted then series_left.predicted = nil end
	if series_right.predicted then series_right.predicted = nil end
	for v_left, x_left in ipairs(series_left) do
		for v_right, x_right in ipairs(series_right) do
			if mw.text.trim(x_left) == mw.text.trim(x_right) then return 'yes' end
		end
	end
	if series_left == series_right then return 'yes' end
	return ''
end

function p.series(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	
	eleSeries = p.getSeries(args)
	if (eleSeries.predicted) then return eleSeries[1] .. '（預測）' end
	return eleSeries[1]
end

function p.getSeries(args)
	--去除模板引用時可能產生的空格
	eleString='' if (args[1] and args[1] ~= '') then eleString = string.gsub(args[1] , "%s$", "") else return {'錯誤'} end
	eleid = p.getListID(eleString)
	ele1 = element_data[eleid]
	if (eleid==-1) then return {'未知'} end
	if (ele1.correct and ele1.correct  ~= '') then
		eleid = p.getListID(ele1.correct)
		ele1 = element_data[eleid]
		if (eleid==-1) then return {'未知'} end
	end
	if (ele1.series and ele1.series ~= '') then
		if (ele1.predictedSeries and ele1.predictedSeries ~= '') then ele1.series.predicted=1 end
		return ele1.series
	end
	return {'錯誤'}
end

function p.protons(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = pframe.args
	return p._protons(args)
end

function p._protons(args)
	--去除模板引用時可能產生的空格
	eleString='' if (args[1] and args[1] ~= '') then eleString = string.gsub(args[1] , "%s$", "") else return '' end
	eleid = p.getListID(eleString)
	ele1 = element_data[eleid]
	if (eleid==-1) then
		return ''
	end
	if (ele1.correct and ele1.correct  ~= '') then
		return ''
	end
	if (ele1.Z and ele1.Z ~= '') then
		return ele1.Z
	end
	return ''
end
function p._check(args)
	--去除模板引用時可能產生的空格
	eleString='' if (args[1] and args[1] ~= '') then eleString = string.gsub(args[1] , "%s$", "") else return error.error{ '未輸入元素' } end
	linkString='' if (args['link'] and args['link'] ~= '') then	linkString = string.gsub(args['link'] , "%s$", "") end
	if (linkString and linkString  ~= '') then
		if (linkString == 'yes') then
			pagetest=true
		end
	end
	eleid = p.getListID(eleString)
	ele1 = element_data[eleid]
	if (eleid==-1) then
		return error.error{ '未知的元素“' .. args[1] .. '”' } .. '[[Category:含有錯誤元素符號的條目|Category:含有錯誤元素符號的條目]]'
	end
	if (ele1.correct and ele1.correct  ~= '') then
		return error.error{ '“' .. args[1] .. '”不是“'.. ele1.correct .. '”的正確拼法。' }
	end
	if (ele1.page and ele1.page ~= '') then
		return ''
	end
	if(pagetest)then
		return error.error{ '元素“' .. args[1] .. '”' .. '沒有對應的頁面。'}
	else
		return ''
	end
end

function p._symbol(args)
	if not(args[1] and args[1] ~= '') then return error.error{ '未輸入元素' } end
	myString = string.gsub(args[1] , "%s$", "") --去除模板引用時可能產生的空格
	eleid = p.getListID(myString)
	if (eleid==-1) then
		return error.error{ '未知的元素“' .. args[1] .. '”' } .. '[[Category:含有錯誤元素符號的條目|Category:含有錯誤元素符號的條目]]'
	end
	ele1 = element_data[eleid]
	if(ele1.NotElement)then
		return ele1.Symbol
	end
	num = ele1.Z + ele1.N --計算質量數
	n = ele1.N
	number=tonumber(args[2])
	if (number and number  ~= '') then
		num = number
		n = num - ele1.Z
		if (n > 0) then --讀到有效的原子量才會進來這裡執行
			if (ele1.Isotope) then
				for v, x in ipairs(ele1.Isotope) do
					if (x.N == n) then
						if (x.Symbol and x.Symbol  ~= '') then
							return x.Symbol
						end
					end
				end
			end
		end
	end
	return ele1.Symbol 
end

function p._link(args)
	--去除模板引用時可能產生的空格
	arg1=''	if (args[1] and args[1] ~= '') then	arg1 = string.gsub(args[1] , "%s$", "") else return error.error{ '未輸入元素' } end
	arg2=''	if (args[2] and args[2] ~= '') then	arg2 = string.gsub(args[2] , "%s$", "") end
	arg3=''	if (args[3] and args[3] ~= '') then	arg3 = string.gsub(args[3] , "%s$", "") end
	eleid = p.getListID(arg1)
	has_m=''
	if (arg3 and arg3  ~= '') then
		has_m=arg3
	end
	if (eleid == -1) then
		return error.error{ '未知的元素“' .. arg1 .. '”' } .. '[[Category:含有錯誤元素符號的條目|Category:含有錯誤元素符號的條目]]'
	end
	ele1 = element_data[eleid]
	if(ele1.NotElement)then
		return ele1.page
	end
	if (ele1.page and ele1.page  ~= '') then
		num = ele1.Z + ele1.N --計算質量數
		n = ele1.N
		hasmass=false
		number=tonumber(arg2)
		if (number and number  ~= '') then
			num = number
			n = num - ele1.Z
			hasmass=true
			if (n < 0) then
				return error.error{ '中子數不得為“' .. n .. '”' }
			end
		else
			if (args2 and args2 ~= '') then
				return error.error{ '未知的質量數“' .. args2 .. '”' }
			end
		end
		if (hasmass == true) then
			if (ele1.Isotope) then
				for v, x in ipairs(ele1.Isotope) do
					if (x.N == n) then
						if (x.page and x.page  ~= '') then
							return  x.page
						else
							return error.error{ '元素“' .. args[1] .. '”' .. '質量數為“'.. num  ..'”的同位素沒有對應的頁面。'}
						end
					end
				end
				return ele1.page .. '-' .. num .. has_m
			end
		end
		return ele1.page 
	end
	return error.error{ '元素“' .. args[1] .. '”' .. '沒有對應的頁面。'}
end

function p.getListID(names)
	local body =''         
	i=1
	for v, x in ipairs(element_data) do                                
		if ((x.name == names) or (x.page == names)) then
			return  i
		end
		for v1, x1 in ipairs(x.othername) do
			if (x1 == names) then
				return  i
			end
		end
		i=i+1
	end
	return -1 
end

function p.decaylink(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = pframe.args
	return p._decaylink(args)
end

function p.elementlink(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = pframe.args
	return p._elementlink(args)
end

function p._elementlink(args)
	arg1=''	if (args[1] and args[1] ~= '') then	arg1 = string.gsub(args[1] , "%s$", "") else return '' end
	arg2=''	if (args[2] and args[2] ~= '') then	arg2 = string.gsub(args[2] , "%s$", "") end
	eleid = p.getListID(arg1)
	if (eleid==-1) then
		return error.error{ '未知的元素“' .. arg1 .. '”' } .. '[[Category:含有錯誤元素符號的條目|Category:含有錯誤元素符號的條目]]'
	end
	ele1 = element_data[eleid]
	symbol1=ele1.Symbol
	if(arg2 and arg2 ~= '')then if(arg2 ~= '1' )then
		if (ele1.compound)then symbol1 ='(' .. symbol1 .. ')' end
		symbol1 = symbol1 .. '<sub>' .. arg2 .. '</sub>'
	end end
	if (ele1.compound)then
		return '[['_.._ele1.page_.._'|' .. symbol1 .. ']]'
	end
	if (ele1.NotElement)then
		return error.error{ '“' .. args[1] .. '”不是元素。'}
	end
	if (ele1.correct and ele1.correct  ~= '') then
		return error.error{ '“' .. args[1] .. '”不是“'.. ele1.correct .. '”的正確拼法。' }
	end
	if (ele1.page and ele1.page  ~= '') then
		return '[['_.._ele1.page_.._'|' .. symbol1 .. ']]'
	else
		return error.error{ '元素“' .. args[1] .. '”沒有對應的頁面。'}
	end
	return ''
end

function p._element_symbol(args)
	arg1=''	if (args[1] and args[1] ~= '') then	arg1 = string.gsub(args[1] , "%s$", "") else return '' end
	arg2=''	if (args[2] and args[2] ~= '') then	arg2 = string.gsub(args[2] , "%s$", "") end
	eleid = p.getListID(arg1)
	if (eleid==-1) then
		return error.error{ '未知的元素“' .. arg1 .. '”' } .. '[[Category:含有錯誤元素符號的條目|Category:含有錯誤元素符號的條目]]'
	end
	ele1 = element_data[eleid]
	symbol1=ele1.Symbol
	if(arg2 and arg2 ~= '')then if(arg2 ~= '1' )then
		if (ele1.compound)then symbol1 ='(' .. symbol1 .. ')' end
		symbol1 = symbol1 .. '<sub>' .. arg2 .. '</sub>'
	end end
	if (ele1.compound)then
		return symbol1
	end
	if (ele1.NotElement)then
		return error.error{ '“' .. args[1] .. '”不是元素。'}
	end
	if (ele1.correct and ele1.correct  ~= '') then
		return error.error{ '“' .. args[1] .. '”不是“'.. ele1.correct .. '”的正確拼法。' }
	end
	if (ele1.page and ele1.page  ~= '') then
		return symbol1
	else
		return error.error{ '元素“' .. args[1] .. '”沒有對應的頁面。'}
	end
	return ''
end

function p._decaylink(args)
	arg1=''	if (args[1] and args[1] ~= '') then	arg1 = string.gsub(args[1] , "%s$", "") else return '' end
	if(arg1=='p') then arg1='p+'end if(arg1=='n') then arg1='n0'end
	decayid = p.getListID(arg1)
	if (decayid==-1) then
		return ''
	end
	decay1 = element_data[decayid]
	if (decay1.decay)then
		return '[['_.._decay1.page_.._'|' .. decay1.Symbol .. ']]'
	end
	return ''
end

p.IUPAC = { [0] = 'n', [1] = 'u', [2] = 'b', [3] = 't', [4] = 'q', [5] = 'p', [6] = 'h', [7] = 's', [8] = 'o', [9] = 'e' }
p.IUPAC_name = { [0] = 'nil', [1] = 'un', [2] = 'bi', [3] = 'tri', [4] = 'quad', [5] = 'pent', 
					[6] = 'hex', [7] = 'sept', [8] = 'oct', [9] = 'enn', [10] = 'ium', [11] = 'um' }

function p.DecodeByIUPAC_rules(symbol_data)
	symbol = mw.ustring.lower(symbol_data)
	symbol_len = mw.ustring.len(symbol)
	Z_data = ''
	for i = 1, symbol_len do
		get_id = nil
		for j = 0, 9 do if mw.ustring.sub(symbol ,i, i) == p.IUPAC[j] then get_id = j end end
		if get_id == nil then return nil end
		Z_data = Z_data .. get_id
	end
	return tonumber(Z_data)
end

function p.getElementByIUPAC_rules(index_input)
	result = ''
	result_name = ''
	index = tonumber(index_input)
	if index ~= nil then index = math.floor(index) else index = 0 end
	index_str = '' .. index
	index_len = mw.ustring.len(index_str)
	if index > 100 then
		for i = 1, index_len do
			data = p.IUPAC[tonumber('' .. mw.ustring.sub(index_str ,i, i)) or 0]
			name = p.IUPAC_name[tonumber('' .. mw.ustring.sub(index_str ,i, i)) or 0]
			if i == 1 then 
				result = result .. mw.ustring.upper(data)
				result_name = result_name .. mw.ustring.upper(mw.ustring.sub(name,1,1)) .. mw.ustring.sub(name,2,-1)
			else
				result = result .. data
				result_name = result_name .. name
			end
		end
	end
	if result == '' then
		return nil
	end
	result_name_index = 11 if mw.ustring.sub(result_name,-1,-1) ~= 'i' then result_name_index = result_name_index - 1 end
	return { name=result_name .. p.IUPAC_name[result_name_index] , page=result, Symbol=result, Z=index }
end

function p.getElementByZ(index)
	local body =''         
	for v, x in ipairs(element_data) do                                
		if (x.Z == index) then
			return  x
		end
	end
	if index > 0 then
		return p.getElementByIUPAC_rules(index)
	end
	return nil 
end

function p.next_element(symbol)
	eleid = p.getListID(symbol)
	ele1 = element_data[eleid]
	
	if ele1 == nil then ele_z = p.DecodeByIUPAC_rules(symbol) else if ele1.Z == nil then
		ele_z = p.DecodeByIUPAC_rules(symbol) else ele_z = ele1.Z end
	end

	if ele_z ~= nil then
		return p.getElementByZ(ele_z + 1)
	end
	return nil
end

function p.last_element(symbol)
	eleid = p.getListID(symbol)
	ele1 = element_data[eleid]
	
	if ele1 == nil then ele_z = p.DecodeByIUPAC_rules(symbol) else if ele1.Z == nil then
		ele_z = p.DecodeByIUPAC_rules(symbol) else ele_z = ele1.Z end
	end

	if ele_z ~= nil then
		return p.getElementByZ(ele_z - 1)
	end
	return nil
end

--本模塊的沙盒(測試)函數
function p.sandbox(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = pframe.args
	return p._elementlink(args)
end
function p._sandbox(args)
	return element_data[p.getListID(args[1])].name 
end
return p