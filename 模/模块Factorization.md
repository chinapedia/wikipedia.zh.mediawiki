local p = {table_max=7919,max_index=1000,limit=35184372088831}

function p.factor(frame)
	-- For calling from #invoke.
    local args
    local can_math = false
    local yesno = require('Module:Yesno')
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = frame.args
        
        can_math = yesno(args['use math'] or args['use_math'])
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
	-- Consider calling the parser function #expr
	--   to simplify a potential mathematical expression?
    number = tonumber(args[1])
    if number == nil then
    	return require("Module:Error").error({[1]="錯誤：輸入的內容 '" .. tostring(args[1]) .. "' 不是一個有效的數字"})
    end
    
    productSymbol = args['product'] or '·'
    bold = yesno(args['bold'] or 'no')
    big = yesno(args['big'] or 'no')
    serif = yesno(args['serif'] or 'no')
    primeLink = yesno(args['prime'] or 'no')

    number = math.floor(number)
    if number < 2 or number > p.limit or number == math.huge then
        return require("Module:Error").error({[1]="錯誤：'" .. tostring(number) .. "' 超出範圍"})
    end
    
    local factors = p._factorization(args[1])
	if factors.has_err ~= nil then
		return require("Module:Error").error({[1]="錯誤：" .. factors.has_err})
	end

    result = ""
    currentNumber = number
    power = 0
    divisor = 2
    local checker = {}

    -- Attempt factoring by the value of the divisor
    --   divisor increments by 2, except first iteration (2 to 3)
    for divisor, power in pairs(factors) do
    	-- Concat result and increment divisor
		-- when divisor is 2, go to 3. All other times, add 2
		result = result .. powerformat(divisor, power, productSymbol)
        checker[#checker + 1] = divisor
    end
	
    if checker[#checker] == number and primeLink then
        return '[[素数|素数]]'
    end

	if can_math then 
		local times, pow_h, pow_f = frame.args['product'] or "\\times ", "^{", "} " 
		return frame:callParserFunction{name = "#tag:math", args = {p.create_factorization_string(factors, times, pow_h, pow_f)}}
	end

    result = string.sub(result,1,-4)

    return format(result)
end

function powerformat(divisor, power, productSymbol)
	if power < 1      then return ''
    elseif power == 1 then return divisor .. ' ' .. productSymbol .. ' '
    else return divisor .. '<sup>' .. power .. '</sup>' .. productSymbol .. ' '
    end
end

function format(numString)
    if bold then
    	numString = '<b>'..numString..'</b>'
    end

	ret = (serif or big) and '<span ' or ''
	if serif then ret = ret .. 'class="texhtml" ' end
	if big   then ret = ret .. 'style="font-size:165%" ' end
	ret = ret .. ((serif or big) and '>' or '') .. numString
	ret = ret .. ((serif or big) and '</span>' or '')

    return ret
end

--[[
輸入一個整數，列出其所有因數 (支援#invoke:)
]]
function p.findDivisor(frame)
	-- For calling from #invoke.
    local args
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = frame.args
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
	local divisors = p._findDivisor(args[1])
	if divisors.has_err ~= nil then
		return require("Module:Error").error({[1]="錯誤：" .. divisors.has_err})
	end
	return table.concat( divisors, ',' )
end

--[[
輸入一個整數，輸出其質因數分解的式子 (支援#invoke:)
]]
function p.factorization(frame)
	-- For calling from #invoke.
    local args
    local can_math = false
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = frame.args
        local yesno = require('Module:Yesno')
        can_math = yesno(args['use math'] or args['use_math'])
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
	local factors = p._factorization(args[1])
	if factors.has_err ~= nil then
		return require("Module:Error").error({[1]="錯誤：" .. factors.has_err})
	end

	local times = " x "
	local pow_h = "<sup>"
	local pow_f = "</sup>"
	if can_math then
		times = "\\times "
		pow_h = "^{"
		pow_f = "} "
	end
	
	local body = p.create_factorization_string(factors, times, pow_h, pow_f)

	if can_math then body = frame:callParserFunction{name = "#tag:math", args = {body}} end
	return body
end

function p.gaussianFactorization(frame)
	-- For calling from #invoke.
    local args
    local can_math = false
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = frame.args
        local yesno = require('Module:Yesno')
        can_math = yesno(args['use math'] or args['use_math'])
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
	local factors = p._gaussianFactorization(args[1])
	local gfactors = {}
	if factors.has_err ~= nil then
		return require("Module:Error").error({[1]="錯誤：" .. factors.has_err})
	end

	if cmath==nil then cmath = require("Module:Complex Number").cmath.init() end

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
	
	for first,second in pairs(factors) do
		if first ~= 'has_err' then 
			local complex_num = cmath.toComplexNumber(first) 
			if complex_num.real ~= 0 and complex_num.imag ~= 0 then
				gfactors[left_ .. tostring(first) .. right_] = second
			else
				gfactors[first] = second
			end
		end
	end
	
	local body = p.create_factorization_string(gfactors, times, pow_h, pow_f)

	if can_math then body = frame:callParserFunction{name = "#tag:math", args = {body}} end
	return body
end

--[[
輸入質因數分解結果和對應格式，輸出其質因數分解字串 (一般Lua函數)
]]
function p.create_factorization_string(factors, times, pow_h, pow_f)
	local body = ''
	local is_first = true
	local nums = {}
	for first,second in pairs(factors) do
		if first ~= 'has_err' then nums[#nums + 1] = first end
	end
	table.sort(nums)
	--對所有的質因數
	for key,value in pairs(nums) do
		local first = nums[key]
		local second = factors[first]
		--如果有次方
		if (second > 1) then
			--如果前方有數字則加上乘號
			if is_first == true then
				is_first = false
			else 
				--加上乘號
				body = body .. times
			end
			--印出次方
			body = body .. tostring(first) .. pow_h .. tostring(second) .. pow_f
		--如果沒有次方
		elseif (second == 1) then
			--如果前方有數字則加上乘號
			if is_first == true then
				is_first = false
			else 
				--加上乘號
				body = body .. times
			end
			--只印數字
			body = body .. tostring(first)
		end
	end
	return body
end

--[[
輸入質因數分解結果和對應格式，輸出其所有因數 (一般Lua函數)
]]
function p._findDivisorByPrimeFactor(prime_factors)
	--已知質因數，透過排列組合列出因數
	--最糟情況時間複雜度 O( 2 ^ prime omega function(n) )
	local check = {[1]=1}
	local result = {}
	--產生排列組合物件
	local gened=require('Module:Combination').getCombinationGenerator()
	--以質因數表初始化
	gened:init(prime_factors,0)
	--找出所有子集以及排列
	local combination = gened:findSubset()
	--計算每一種排列方式的乘積
	for i = 1,#combination do
		local product = 1
		for j = 1,#(combination[i]) do
			product = product * (tonumber(combination[i][j]) or 1)
		end
		check[product] = 1
	end
	--每一種排列方式的乘積即為所有因數
	for key,value in pairs(check) do
		if tostring(tonumber(tostring(key)) or 0) == tostring(key) then
			--填入因數到陣列
			result[#result+1] = key
		end
	end
	--使因數由小排到大
	table.sort(result)

	return result
end

--[[
輸入一個整數，透過質因數分解，列出其所有因數 (一般Lua函數)
]]
function p._findDivisor(num)
	--使用短除法找出質因數，透過排列組合列出因數
	--最糟情況 (質數，小於62,710,561) 時間複雜度 O(√n/ln √n + 2 ^ prime omega function(n) )
	local number = tonumber(num)
	if number == nil then return {} end
	--質因數分解
	local prime_factors=p._factorization(tonumber(num or 2))
	local check = {[1]=1,[number]=1}
	local result = {}
	local gened=require('Module:Combination').getCombinationGenerator()

	gened:init(prime_factors,0)
	local combination = gened:findSubset()
	
	for i = 1,#combination do
		local product = 1
		for j = 1,#(combination[i]) do
			product = product * (tonumber(combination[i][j]) or 1)
		end
		check[product] = 1
	end
	for key,value in pairs(check) do
		if tostring(tonumber(tostring(key)) or 0) == tostring(key) then 
			result[#result+1] = key
		end
	end
	table.sort(result)

	return result
end

--[[
輸入一個整數，透過試除法(試除小於平方根的每個整數)，列出其所有因數 (一般Lua函數，較慢)
]]
function p._findDivisor_old(input)
	--使用傳統式試除法找出因數
	--最糟情況時間複雜度 O(√n)
	local number = tonumber(input or 0)
	local result = {1,number}
	local checker = {}
	if(p.lists[number] ~= nil) then
		return result
	end
	if(number < 0) then
		return {has_err = "負值沒有小於自己的正因數"}
	end
	local m = number
	local max_count = math.ceil(math.sqrt(m + 2)) + 2
	local i = 2
	for i = 2,max_count do
		if m % i == 0 then
			checker[i] = true
			checker[m / i] = true
		end
	end
	for first,second in pairs(checker) do
		result[#result + 1] = first
	end
	
	local check = {[1]=1,[number]=1}
	for i = 1,#result do
		check[result[i]] = 1
	end
	result={}
	for key,value in pairs(check) do
		if tostring(tonumber(tostring(key)) or 0) == tostring(key) then 
			result[#result+1] = key
		end
	end
	table.sort(result)
	return result
end

--[[
輸入一個整數，透過短除法 (使用小於平方根的每個質數，於質數表)，列出其所有因數 (一般Lua函數)
]]
function p._factorization(input)
	--使用短除法做質因數分解 (整數分解)
	--最糟情況 (質數，小於62,710,561) 時間複雜度 O(√n/ln √n )
	--最糟情況 (質數，大於62,710,561) 時間複雜度 O(n√n)
	local number = tonumber(input or 0)
	if number == nil then return {has_err = "不正確的數字"} end
	local has_factor = ((number or 0) < 0)
	local result = {}
	if number == 1 or number == 0 then return {} end
	
	if p.lists[number] ~= nil or number == -1 then return {[number] = 1} end

	local m = number
	local has_err = false 
	--如果為負，先將負號提出來
	if number < 0 then 
		m = -number
		result[-1] = (result[-1] or 0) + 1
	end
	if m > p.limit then return {has_err = "數字過大"} end
	--最多跑到√n後停止
	local max_count = math.ceil(math.sqrt(m + 2)) + 2
	--自定義for迴圈，用while do實現
	local i = 2 while i < max_count and i < m do
		--發現質因數
		while m % i == 0 do
			--紀錄質因數
			result[i] = (result[i] or 0) + 1
			--短除法，除到此數除不盡為止
			m = m / i
			--調整終止範圍為新的數之平方根
			max_count = math.ceil(math.sqrt(m + 2)) + 2
			--因此此演算法最佳情況約 O(ln n)
			--已經找到質因數了
			has_factor = true
		end
		--迴圈末端
	i = p._nextPrime(i) if i == nil then has_err = "數字過大" break end end

	--短除法最後剩下的數是質數
	if m > 1 then
		--紀錄質因數
		result[m] = (result[m] or 0) + 1
		has_factor = true
	end
	if has_err then result.has_err = has_err end
	return result
end

function p._gaussianFactorization(complex_num)
	if cmath==nil then cmath = require("Module:Complex Number").cmath.init() end
	if numdata==nil then numdata = require("Module:Number/data") end
	local input = cmath.toComplexNumber(complex_num) 
	if input == nil then return {} end
	if input == cmath.getComplexNumber(0, 0) or input == cmath.getComplexNumber(1, 0) then return {} end
	if (math.abs(input.imag) == 1 and input.real == 0) or cmath.is_prime_quadrant1(input) then return {[tostring(input)] = 1}  end
	if cmath.is_prime_quadrant1(-input) then return {[tostring(-input)] = 1,["-1"]=1}  end
	if cmath.is_prime_quadrant1(input / cmath.getComplexNumber(0, 1)) then return {[tostring(input / cmath.getComplexNumber(0, 1))] = 1,["i"]=1}  end
	if cmath.is_prime_quadrant1(input / cmath.getComplexNumber(0, -1)) then return {[tostring(input / cmath.getComplexNumber(0, -1))] = 1,["-i"]=1}  end
	local result = {}
	local loop_state, loop_action = 1, {function(x)x.imag=x.imag+1 return x end,function(x)x.real=x.real-1 return x end}
	local check_input = cmath.getComplexNumber(input.real, input.imag) 
	local n = math.sqrt(input.real*input.real + input.imag*input.imag)
	local m, val1, i, j= n, cmath.getComplexNumber(1, 0), 1, 0
	while i < m do
		val1.real, val1.imag = i, 0
		loop_state = 1
		for j=1,i*2 do
			if loop_state == 1 and val1.real == val1.imag then loop_state=2 end
			if cmath.is_prime_quadrant1(val1)then
				local can_div = true
				while can_div do
					local dived = check_input / val1
					dived:clean()
					if numdata._is_integer(dived.real) and numdata._is_integer(dived.imag) then
						--紀錄質因數
						result[tostring(val1)] = (result[tostring(val1)] or 0) + 1
						check_input.real = math.floor(dived.real)
						check_input.imag = math.floor(dived.imag)
						m = math.sqrt(dived.real*dived.real + dived.imag*dived.imag)
						can_div = true
					else
						can_div = false
					end
				end
			end
			val1 = loop_action[loop_state](val1)
		end
		i = i + 1
	end
	--短除法最後剩下的數是質數
	if not (check_input:clean() == cmath.getComplexNumber(1, 0)) then
		if check_input.real < 0 and check_input.imag == 0 then
			result[tostring(-1)] = (result[tostring(-1)] or 0) + 1
			check_input = check_input / (-1)
		end
		if check_input.real == 0 and check_input.imag < 0 then
			result["-i"] = (result["-i"] or 0) + 1
			check_input = check_input / (-cmath.i)
		end
		if math.abs(check_input.real) ~= 1 and math.abs(check_input.imag) ~= 1 then
			--紀錄質因數
			result[tostring(check_input)] = (result[tostring(check_input)] or 0) + 1
		end
	end
	return result
end
function p._listGaussianDivisorSum(start, stop)
	for i = start, stop do
		mw.log(i, p._GaussianDivisorSum(i)-i)
	end
end
function p._GaussianDivisorSum(complex_num, first_q)
	if cmath==nil then cmath = require("Module:Complex Number").cmath.init() end
	if numdata==nil then numdata = require("Module:Number/data") end
	local number = cmath.toComplexNumber(complex_num) 
	if number == nil then return "0" end
	if number == cmath.zero then return "0" end
	local divisors = p._findGaussianDivisor(complex_num)
	local sum = cmath.getComplexNumber(0, 0) 
	for i = 1,#divisors do
		if first_q then
			local test = cmath.toComplexNumber(divisors[i]) 
			if test.real >= 0 and test.imag >= 0 then
				sum = sum + test
			end
		else
			sum = sum + cmath.toComplexNumber(divisors[i]) 
		end
	end
	return sum
end
function p._findGaussianDivisor(complex_num)
	if cmath==nil then cmath = require("Module:Complex Number").cmath.init() end
	if numdata==nil then numdata = require("Module:Number/data") end
	local number = cmath.toComplexNumber(complex_num) 
	if number == nil then return {} end
	if number == cmath.zero then return {} end
	local result = {}
	--質因數分解
	local prime_factors=p._gaussianFactorization(complex_num)
	
	local check = {['1']=1,[tostring(number)]=1}
	local result = {}
	local gened=require('Module:Combination').getCombinationGenerator()
	gened:init(prime_factors,0)
	local combination = gened:findSubset()
	for i = 1,#combination do
		local product = cmath.getComplexNumber(1, 0) 
		for j = 1,#(combination[i]) do
			product = product * (cmath.toComplexNumber(combination[i][j]) or cmath.getComplexNumber(1, 0) )
		end
		product:clean()
		check[tostring(product)] = 1
	end
	for key,value in pairs(check) do
		local ckey = cmath.toComplexNumber(key)
		if ckey then 
			result[#result+1] = tostring(ckey)
		end
	end
	table.sort(result)

	return result
end

--[[
找下一個質數：輸入一個整數n，輸出大於n的最小質數 (一般Lua函數)
]]
function p._nextPrime(input)
	--找下一個質數
	--小於7,919 (第1000個質數) 用查表法
	--大於7,919 則往下找質數
	--考量到記憶體限制，根據素数计数函数，10^7的以下質數有664,579個，其質數表容量已經要以 MB 為單位計算
	--因此限制質數表最大只能建立到5,931,641(第408,493個質數)，對應上方演算法√n
	--因此限制訂為35,184,372,088,831 (5,931,641 ^ 2) 
	--約為 2^45，位於維基lua運算限制內
	local number = tonumber(input or 0)
	if number > p.limit then return nil end
	if number < 2 then return 2 end
	if number < p.table_max then
		--查表直接命中
		if(p.lists[number] ~= nil) then
			local this_id = p.lists[number]
			--回傳下一個質數
			return p.arr[this_id+1]
		else
			--否則用binary search找出最近質數
			local min_test = 1
			local max_test = p.max_index
			local testing = math.floor(number / math.log( number ))
			
			while number ~= p.arr[testing] do

				if p.arr[testing] > number then
					max_test = testing
					testing = math.floor((min_test + max_test) / 2)
				elseif p.arr[testing] < number then
					min_test = testing
					testing = math.floor((min_test + max_test) / 2)
				end
				if math.abs(min_test - max_test) == 1 then 
					return p.arr[math.max(min_test,max_test)]
				end
			end
			
		end
	else
		--跑到上限 35,184,372,088,831 為止
		local i = p.table_max + 1 while i < p.limit do
			--使用埃拉托斯特尼筛法過濾掉部分合數
			if not((i > 101)and((i % 3 == 0)or(i % 5 == 0)or(i % 7 == 0)or(i % 11 == 0)or(i % 13 == 0)
				or (i % 17 == 0) or (i % 19 == 0) or (i % 23 == 0) or (i % 29 == 0) or (i % 31 == 0)
				or (i % 37 == 0) or (i % 41 == 0) or (i % 43 == 0) or (i % 47 == 0) or (i % 53 == 0)
				or (i % 59 == 0) or (i % 61 == 0) or (i % 67 == 0) or (i % 71 == 0) or (i % 73 == 0)
				or (i % 79 == 0) or (i % 83 == 0) or (i % 89 == 0) or (i % 97 == 0) or (i % 101 == 0)))then
					--跳過偶數
					if not(i ~= 2 and i % 2 == 0) then
						local is_prime = true;
						--使用AKS質數測試的第一條規則再在篩掉部分合數
						local board = math.ceil(math.log( i + 2 ) / math.log( 2 ))
						local b = 2 while b <= board do
							local a = math.pow(i, (1.0/b))
							if math.abs(a - math.floor(a)) <= 1e-9 then
								is_prime = false
								break;
							end
						b=b+1 end
						--若還不能確定其質數性
						--由於AKS質數測試的第二條規則牽扯到二項式，需要大整數計算 (會乘出很大的數字，可能會失去精確度)
						--因此此處就回歸傳統試除法
						if is_prime == true then
							local last_prime = 0
							for iterator = 1, #(p.arr) do
								local kv = p.arr[iterator]
								--將小於平方根的所有質數試除一次
								if (kv >= (math.ceil(math.sqrt(i + 2))) + 2) then break end
								last_prime = kv
								if (i % kv == 0) then
									is_prime = false;
									break;
								end
							end

							if (last_prime < (math.ceil(math.sqrt(i + 2))) + 2) and last_prime >= p.arr[#(p.arr)] and
								last_prime > 0 and is_prime == true then 

								 local kv = last_prime
								 while (kv < (math.ceil(math.sqrt(i + 2))) + 2) do
									if (i % kv == 0) then
										is_prime = false;
										break;
									end
								 	kv = kv + 2
								 end
							end
						end
		
						--一定會確定是否為質數
						if (is_prime) then--i is prime
							--確認為新的質數
							if(p.lists[i] == nil and p.arr[p.max_index + 1] == nil) then
								p.max_index = #(p.arr) + 1
								p.lists[i] = p.max_index
								p.arr[p.max_index] = i
								p.table_max = i
							end
							
							--找到的質數比輸入的數大則輸出
							if i>number then return i end
						end
						
					end
				end
				--如果是偶數則加成奇數，否則2個數2個數跳(下一個數必為奇數，除了2外沒有偶質數)
			if i % 2 == 0 then i = i + 1 else i = i + 2 end
		end
	end
end

--[[
找上一個質數：輸入一個整數n，輸出小於n的最大質數 (一般Lua函數)
]]
function p._lastPrime(input)
	--同於上方演算法，只是會輸出前一個質數
	local number = tonumber(input or 0)
	if number > p.limit then return nil end
	if number <= 2 then return nil end
	if number <= 3 then return 2 end
	if number < p.table_max then
		if(p.lists[number] ~= nil) then
			local this_id = p.lists[number]
			return p.arr[this_id-1]
		else
			local min_test = 1
			local max_test = p.max_index
			local testing = math.floor(number / math.log( number ))
			
			while number ~= p.arr[testing] do

				if p.arr[testing] > number then
					max_test = testing
					testing = math.floor((min_test + max_test) / 2)
				elseif p.arr[testing] < number then
					min_test = testing
					testing = math.floor((min_test + max_test) / 2)
				end
				if math.abs(min_test - max_test) == 1 then 
					return p.arr[math.min(min_test,max_test)]
				end
			end
			
		end
	else
		local last_prime = p.table_max + 0
		local i = p.table_max + 1 while i < p.limit do
			if not((i > 101)and((i % 3 == 0)or(i % 5 == 0)or(i % 7 == 0)or(i % 11 == 0)or(i % 13 == 0)
				or (i % 17 == 0) or (i % 19 == 0) or (i % 23 == 0) or (i % 29 == 0) or (i % 31 == 0)
				or (i % 37 == 0) or (i % 41 == 0) or (i % 43 == 0) or (i % 47 == 0) or (i % 53 == 0)
				or (i % 59 == 0) or (i % 61 == 0) or (i % 67 == 0) or (i % 71 == 0) or (i % 73 == 0)
				or (i % 79 == 0) or (i % 83 == 0) or (i % 89 == 0) or (i % 97 == 0) or (i % 101 == 0)))then
					if not(i ~= 2 and i % 2 == 0) then
						local is_prime = true;
						local board = math.ceil(math.log( i + 1 ) / math.log( 2 ))
						local b = 2 while b <= board do
							local a = math.pow(i, (1.0/b))
							if math.abs(a - math.floor(a)) <= 1e-9 then
								is_prime = false
								break;
							end
						b=b+1 end
						
						if is_prime == true then
							local last_prime = 0
							for iterator = 1, #(p.arr) do
								local kv = p.arr[iterator]
								--將小於平方根的所有質數試除一次
								if (kv >= (math.ceil(math.sqrt(i + 2))) + 2) then break end
								last_prime = kv
								if (i % kv == 0) then
									is_prime = false;
									break;
								end
							end

							if (last_prime < (math.ceil(math.sqrt(i + 2))) + 2) and last_prime >= p.arr[#(p.arr)] and
								last_prime > 0 and is_prime == true then 

								 local kv = last_prime
								 while (kv < (math.ceil(math.sqrt(i + 2))) + 2) do
									if (i % kv == 0) then
										is_prime = false;
										break;
									end
								 	kv = kv + 2
								 end
							end
						end
		
						--new stage
						if (is_prime) then--i is prime
							
							if(p.lists[i] == nil and p.arr[p.max_index + 1] == nil) then
								p.max_index = #(p.arr) + 1
								p.lists[i] = p.max_index
								p.arr[p.max_index] = i
								p.table_max = i
							end

							if i>=number then return last_prime end
							last_prime = i+0
						end
						
					end
				end
			if i % 2 == 0 then i = i + 1 else i = i + 2 end
		end
	end
end

--[[
找下一個質數：輸入一個整數n，輸出大於n的最小質數 (支援#invoke:)
]]
function p.nextPrime(frame)
	-- For calling from #invoke.
    local args
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = frame.args
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
	return tostring( p._nextPrime(tonumber(args[1])) or '' )
end


--[[
找上一個質數：輸入一個整數n，輸出小於n的最大質數 (支援#invoke:)
]]
function p.lastPrime(frame)
	-- For calling from #invoke.
    local args
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = frame.args
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
	return tostring( p._lastPrime(tonumber(args[1])) or '' )
end

--[[
輸入一個整數n，輸出第n個質數 (支援#invoke:)
]]
function p.primeIndex(frame)
	-- For calling from #invoke.
    local args
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = frame.args
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
    local number = tonumber(args[1])
    if number == nil then return '' end
    if number >= 408493 then
    	if number == 408493 then return '5931641' end
    	return require("Module:Error").error({[1]="錯誤：數字太大"})
    end
	if number <= #(p.arr) then
		return tostring(p.arr[number])
	else
		for i = (#(p.arr))-1 , number + 1 do
			p._nextPrime(p.arr[i]+1)
		end
		return tostring(p.arr[number])
	end
	return ''
end


--[[
輸入一個整數n，輸出小於等於n的質數個數 (支援#invoke:)
]]
function p.primeIndexOf(frame)
	-- For calling from #invoke.
    local args
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = frame.args
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
    local number = tonumber(args[1])
    if number == nil then return '' end
    if number >= 5931641 then
    	if number == 5931641 then return '408493' end
    	return require("Module:Error").error({[1]="錯誤：數字太大"})
    end
    if number <= 1 then return 0 end
    
	if number >= p.arr[#(p.arr)] then
		p._nextPrime(number+1)
	end
	
	--查表直接命中
	if(p.lists[number] ~= nil) then
		return tostring(p.lists[number])
	else
		--否則用binary search找出最近質數
		local min_test = 1
		local max_test = p.max_index
		local testing = math.floor(number / math.log( number ))
			
		while number ~= p.arr[testing] do

			if p.arr[testing] > number then
				max_test = testing
				testing = math.floor((min_test + max_test) / 2)
			elseif p.arr[testing] < number then
				min_test = testing
				testing = math.floor((min_test + max_test) / 2)
			end
			if math.abs(min_test - max_test) == 1 then 
				return tostring(math.min(min_test,max_test))
			end
		end
			
	end
	
	return ''
end

--[[
質數表
以下列Mathematica程式碼產生
]]
--Table[Prime[i], {i, 1, 1000}]
p.arr={2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103, 107, 109, 113, 127, 131, 137, 139, 149, 151, 157, 163, 167, 173, 179, 181, 191, 193, 197, 199, 211, 223, 227, 229, 233, 239, 241, 251, 257, 263, 269, 271, 277, 281, 283, 293, 307, 311, 313, 317, 331, 337, 347, 349, 353, 359, 367, 373, 379, 383, 389, 397, 401, 409, 419, 421, 431, 433, 439, 443, 449, 457, 461, 463, 467, 479, 487, 491, 499, 503, 509, 521, 523, 541, 547, 557, 563, 569, 571, 577, 587, 593, 599, 601, 607, 613, 617, 619, 631, 641, 643, 647, 653, 659, 661, 673, 677, 683, 691, 701, 709, 719, 727, 733, 739, 743, 751, 757, 761, 769, 773, 787, 797, 809, 811, 821, 823, 827, 829, 839, 853, 857, 859, 863, 877, 881, 883, 887, 907, 911, 919, 929, 937, 941, 947, 953, 967, 971, 977, 983, 991, 997, 1009, 1013, 1019, 1021, 1031, 1033, 1039, 1049, 1051, 1061, 1063, 1069, 1087, 1091, 1093, 1097, 1103, 1109, 1117, 1123, 1129, 1151, 1153, 1163, 1171, 1181, 1187, 1193, 1201, 1213, 1217, 1223, 1229, 1231, 1237, 1249, 1259, 1277, 1279, 1283, 1289, 1291, 1297, 1301, 1303, 1307, 1319, 1321, 1327, 1361, 1367, 1373, 1381, 1399, 1409, 1423, 1427, 1429, 1433, 1439, 1447, 1451, 1453, 1459, 1471, 1481, 1483, 1487, 1489, 1493, 1499, 1511, 1523, 1531, 1543, 1549, 1553, 1559, 1567, 1571, 1579, 1583, 1597, 1601, 1607, 1609, 1613, 1619, 1621, 1627, 1637, 1657, 1663, 1667, 1669, 1693, 1697, 1699, 1709, 1721, 1723, 1733, 1741, 1747, 1753, 1759, 1777, 1783, 1787, 1789, 1801, 1811, 1823, 1831, 1847, 1861, 1867, 1871, 1873, 1877, 1879, 1889, 1901, 1907, 1913, 1931, 1933, 1949, 1951, 1973, 1979, 1987, 1993, 1997, 1999, 2003, 2011, 2017, 2027, 2029, 2039, 2053, 2063, 2069, 2081, 2083, 2087, 2089, 2099, 2111, 2113, 2129, 2131, 2137, 2141, 2143, 2153, 2161, 2179, 2203, 2207, 2213, 2221, 2237, 2239, 2243, 2251, 2267, 2269, 2273, 2281, 2287, 2293, 2297, 2309, 2311, 2333, 2339, 2341, 2347, 2351, 2357, 2371, 2377, 2381, 2383, 2389, 2393, 2399, 2411, 2417, 2423, 2437, 2441, 2447, 2459, 2467, 2473, 2477, 2503, 2521, 2531, 2539, 2543, 2549, 2551, 2557, 2579, 2591, 2593, 2609, 2617, 2621, 2633, 2647, 2657, 2659, 2663, 2671, 2677, 2683, 2687, 2689, 2693, 2699, 2707, 2711, 2713, 2719, 2729, 2731, 2741, 2749, 2753, 2767, 2777, 2789, 2791, 2797, 2801, 2803, 2819, 2833, 2837, 2843, 2851, 2857, 2861, 2879, 2887, 2897, 2903, 2909, 2917, 2927, 2939, 2953, 2957, 2963, 2969, 2971, 2999, 3001, 3011, 3019, 3023, 3037, 3041, 3049, 3061, 3067, 3079, 3083, 3089, 3109, 3119, 3121, 3137, 3163, 3167, 3169, 3181, 3187, 3191, 3203, 3209, 3217, 3221, 3229, 3251, 3253, 3257, 3259, 3271, 3299, 3301, 3307, 3313, 3319, 3323, 3329, 3331, 3343, 3347, 3359, 3361, 3371, 3373, 3389, 3391, 3407, 3413, 3433, 3449, 3457, 3461, 3463, 3467, 3469, 3491, 3499, 3511, 3517, 3527, 3529, 3533, 3539, 3541, 3547, 3557, 3559, 3571, 3581, 3583, 3593, 3607, 3613, 3617, 3623, 3631, 3637, 3643, 3659, 3671, 3673, 3677, 3691, 3697, 3701, 3709, 3719, 3727, 3733, 3739, 3761, 3767, 3769, 3779, 3793, 3797, 3803, 3821, 3823, 3833, 3847, 3851, 3853, 3863, 3877, 3881, 3889, 3907, 3911, 3917, 3919, 3923, 3929, 3931, 3943, 3947, 3967, 3989, 4001, 4003, 4007, 4013, 4019, 4021, 4027, 4049, 4051, 4057, 4073, 4079, 4091, 4093, 4099, 4111, 4127, 4129, 4133, 4139, 4153, 4157, 4159, 4177, 4201, 4211, 4217, 4219, 4229, 4231, 4241, 4243, 4253, 4259, 4261, 4271, 4273, 4283, 4289, 4297, 4327, 4337, 4339, 4349, 4357, 4363, 4373, 4391, 4397, 4409, 4421, 4423, 4441, 4447, 4451, 4457, 4463, 4481, 4483, 4493, 4507, 4513, 4517, 4519, 4523, 4547, 4549, 4561, 4567, 4583, 4591, 4597, 4603, 4621, 4637, 4639, 4643, 4649, 4651, 4657, 4663, 4673, 4679, 4691, 4703, 4721, 4723, 4729, 4733, 4751, 4759, 4783, 4787, 4789, 4793, 4799, 4801, 4813, 4817, 4831, 4861, 4871, 4877, 4889, 4903, 4909, 4919, 4931, 4933, 4937, 4943, 4951, 4957, 4967, 4969, 4973, 4987, 4993, 4999, 5003, 5009, 5011, 5021, 5023, 5039, 5051, 5059, 5077, 5081, 5087, 5099, 5101, 5107, 5113, 5119, 5147, 5153, 5167, 5171, 5179, 5189, 5197, 5209, 5227, 5231, 5233, 5237, 5261, 5273, 5279, 5281, 5297, 5303, 5309, 5323, 5333, 5347, 5351, 5381, 5387, 5393, 5399, 5407, 5413, 5417, 5419, 5431, 5437, 5441, 5443, 5449, 5471, 5477, 5479, 5483, 5501, 5503, 5507, 5519, 5521, 5527, 5531, 5557, 5563, 5569, 5573, 5581, 5591, 5623, 5639, 5641, 5647, 5651, 5653, 5657, 5659, 5669, 5683, 5689, 5693, 5701, 5711, 5717, 5737, 5741, 5743, 5749, 5779, 5783, 5791, 5801, 5807, 5813, 5821, 5827, 5839, 5843, 5849, 5851, 5857, 5861, 5867, 5869, 5879, 5881, 5897, 5903, 5923, 5927, 5939, 5953, 5981, 5987, 6007, 6011, 6029, 6037, 6043, 6047, 6053, 6067, 6073, 6079, 6089, 6091, 6101, 6113, 6121, 6131, 6133, 6143, 6151, 6163, 6173, 6197, 6199, 6203, 6211, 6217, 6221, 6229, 6247, 6257, 6263, 6269, 6271, 6277, 6287, 6299, 6301, 6311, 6317, 6323, 6329, 6337, 6343, 6353, 6359, 6361, 6367, 6373, 6379, 6389, 6397, 6421, 6427, 6449, 6451, 6469, 6473, 6481, 6491, 6521, 6529, 6547, 6551, 6553, 6563, 6569, 6571, 6577, 6581, 6599, 6607, 6619, 6637, 6653, 6659, 6661, 6673, 6679, 6689, 6691, 6701, 6703, 6709, 6719, 6733, 6737, 6761, 6763, 6779, 6781, 6791, 6793, 6803, 6823, 6827, 6829, 6833, 6841, 6857, 6863, 6869, 6871, 6883, 6899, 6907, 6911, 6917, 6947, 6949, 6959, 6961, 6967, 6971, 6977, 6983, 6991, 6997, 7001, 7013, 7019, 7027, 7039, 7043, 7057, 7069, 7079, 7103, 7109, 7121, 7127, 7129, 7151, 7159, 7177, 7187, 7193, 7207, 7211, 7213, 7219, 7229, 7237, 7243, 7247, 7253, 7283, 7297, 7307, 7309, 7321, 7331, 7333, 7349, 7351, 7369, 7393, 7411, 7417, 7433, 7451, 7457, 7459, 7477, 7481, 7487, 7489, 7499, 7507, 7517, 7523, 7529, 7537, 7541, 7547, 7549, 7559, 7561, 7573, 7577, 7583, 7589, 7591, 7603, 7607, 7621, 7639, 7643, 7649, 7669, 7673, 7681, 7687, 7691, 7699, 7703, 7717, 7723, 7727, 7741, 7753, 7757, 7759, 7789, 7793, 7817, 7823, 7829, 7841, 7853, 7867, 7873, 7877, 7879, 7883, 7901, 7907, 7919}

--[[
質數表 (反查表)
以下列Mathematica程式碼產生
]]
--		Module[
--			{
--				result = "{", 
--				firstPrint = True
--			}, 
--			Do[
--				If[firstPrint == True, 
--					firstPrint = False, 
--				(* Else *)
--					result = result <> ","
--				]; 
--				result = result <> "[" <> ToString[Prime[i]] <> "]=" <> ToString[i], 
--			{i, 1, 1000}];
--			result <> "}"
--		]
p.lists={[2]=1,[3]=2,[5]=3,[7]=4,[11]=5,[13]=6,[17]=7,[19]=8,[23]=9,[29]=10,[31]=11,[37]=12,[41]=13,[43]=14,[47]=15,[53]=16,[59]=17,[61]=18,[67]=19,[71]=20,[73]=21,[79]=22,[83]=23,[89]=24,[97]=25,[101]=26,[103]=27,[107]=28,[109]=29,[113]=30,[127]=31,[131]=32,[137]=33,[139]=34,[149]=35,[151]=36,[157]=37,[163]=38,[167]=39,[173]=40,[179]=41,[181]=42,[191]=43,[193]=44,[197]=45,[199]=46,[211]=47,[223]=48,[227]=49,[229]=50,[233]=51,[239]=52,[241]=53,[251]=54,[257]=55,[263]=56,[269]=57,[271]=58,[277]=59,[281]=60,[283]=61,[293]=62,[307]=63,[311]=64,[313]=65,[317]=66,[331]=67,[337]=68,[347]=69,[349]=70,[353]=71,[359]=72,[367]=73,[373]=74,[379]=75,[383]=76,[389]=77,[397]=78,[401]=79,[409]=80,[419]=81,[421]=82,[431]=83,[433]=84,[439]=85,[443]=86,[449]=87,[457]=88,[461]=89,[463]=90,[467]=91,[479]=92,[487]=93,[491]=94,[499]=95,[503]=96,[509]=97,[521]=98,[523]=99,[541]=100,[547]=101,[557]=102,[563]=103,[569]=104,[571]=105,[577]=106,[587]=107,[593]=108,[599]=109,[601]=110,[607]=111,[613]=112,[617]=113,[619]=114,[631]=115,[641]=116,[643]=117,[647]=118,[653]=119,[659]=120,[661]=121,[673]=122,[677]=123,[683]=124,[691]=125,[701]=126,[709]=127,[719]=128,[727]=129,[733]=130,[739]=131,[743]=132,[751]=133,[757]=134,[761]=135,[769]=136,[773]=137,[787]=138,[797]=139,[809]=140,[811]=141,[821]=142,[823]=143,[827]=144,[829]=145,[839]=146,[853]=147,[857]=148,[859]=149,[863]=150,[877]=151,[881]=152,[883]=153,[887]=154,[907]=155,[911]=156,[919]=157,[929]=158,[937]=159,[941]=160,[947]=161,[953]=162,[967]=163,[971]=164,[977]=165,[983]=166,[991]=167,[997]=168,[1009]=169,[1013]=170,[1019]=171,[1021]=172,[1031]=173,[1033]=174,[1039]=175,[1049]=176,[1051]=177,[1061]=178,[1063]=179,[1069]=180,[1087]=181,[1091]=182,[1093]=183,[1097]=184,[1103]=185,[1109]=186,[1117]=187,[1123]=188,[1129]=189,[1151]=190,[1153]=191,[1163]=192,[1171]=193,[1181]=194,[1187]=195,[1193]=196,[1201]=197,[1213]=198,[1217]=199,[1223]=200,[1229]=201,[1231]=202,[1237]=203,[1249]=204,[1259]=205,[1277]=206,[1279]=207,[1283]=208,[1289]=209,[1291]=210,[1297]=211,[1301]=212,[1303]=213,[1307]=214,[1319]=215,[1321]=216,[1327]=217,[1361]=218,[1367]=219,[1373]=220,[1381]=221,[1399]=222,[1409]=223,[1423]=224,[1427]=225,[1429]=226,[1433]=227,[1439]=228,[1447]=229,[1451]=230,[1453]=231,[1459]=232,[1471]=233,[1481]=234,[1483]=235,[1487]=236,[1489]=237,[1493]=238,[1499]=239,[1511]=240,[1523]=241,[1531]=242,[1543]=243,[1549]=244,[1553]=245,[1559]=246,[1567]=247,[1571]=248,[1579]=249,[1583]=250,[1597]=251,[1601]=252,[1607]=253,[1609]=254,[1613]=255,[1619]=256,[1621]=257,[1627]=258,[1637]=259,[1657]=260,[1663]=261,[1667]=262,[1669]=263,[1693]=264,[1697]=265,[1699]=266,[1709]=267,[1721]=268,[1723]=269,[1733]=270,[1741]=271,[1747]=272,[1753]=273,[1759]=274,[1777]=275,[1783]=276,[1787]=277,[1789]=278,[1801]=279,[1811]=280,[1823]=281,[1831]=282,[1847]=283,[1861]=284,[1867]=285,[1871]=286,[1873]=287,[1877]=288,[1879]=289,[1889]=290,[1901]=291,[1907]=292,[1913]=293,[1931]=294,[1933]=295,[1949]=296,[1951]=297,[1973]=298,[1979]=299,[1987]=300,[1993]=301,[1997]=302,[1999]=303,[2003]=304,[2011]=305,[2017]=306,[2027]=307,[2029]=308,[2039]=309,[2053]=310,[2063]=311,[2069]=312,[2081]=313,[2083]=314,[2087]=315,[2089]=316,[2099]=317,[2111]=318,[2113]=319,[2129]=320,[2131]=321,[2137]=322,[2141]=323,[2143]=324,[2153]=325,[2161]=326,[2179]=327,[2203]=328,[2207]=329,[2213]=330,[2221]=331,[2237]=332,[2239]=333,[2243]=334,[2251]=335,[2267]=336,[2269]=337,[2273]=338,[2281]=339,[2287]=340,[2293]=341,[2297]=342,[2309]=343,[2311]=344,[2333]=345,[2339]=346,[2341]=347,[2347]=348,[2351]=349,[2357]=350,[2371]=351,[2377]=352,[2381]=353,[2383]=354,[2389]=355,[2393]=356,[2399]=357,[2411]=358,[2417]=359,[2423]=360,[2437]=361,[2441]=362,[2447]=363,[2459]=364,[2467]=365,[2473]=366,[2477]=367,[2503]=368,[2521]=369,[2531]=370,[2539]=371,[2543]=372,[2549]=373,[2551]=374,[2557]=375,[2579]=376,[2591]=377,[2593]=378,[2609]=379,[2617]=380,[2621]=381,[2633]=382,[2647]=383,[2657]=384,[2659]=385,[2663]=386,[2671]=387,[2677]=388,[2683]=389,[2687]=390,[2689]=391,[2693]=392,[2699]=393,[2707]=394,[2711]=395,[2713]=396,[2719]=397,[2729]=398,[2731]=399,[2741]=400,[2749]=401,[2753]=402,[2767]=403,[2777]=404,[2789]=405,[2791]=406,[2797]=407,[2801]=408,[2803]=409,[2819]=410,[2833]=411,[2837]=412,[2843]=413,[2851]=414,[2857]=415,[2861]=416,[2879]=417,[2887]=418,[2897]=419,[2903]=420,[2909]=421,[2917]=422,[2927]=423,[2939]=424,[2953]=425,[2957]=426,[2963]=427,[2969]=428,[2971]=429,[2999]=430,[3001]=431,[3011]=432,[3019]=433,[3023]=434,[3037]=435,[3041]=436,[3049]=437,[3061]=438,[3067]=439,[3079]=440,[3083]=441,[3089]=442,[3109]=443,[3119]=444,[3121]=445,[3137]=446,[3163]=447,[3167]=448,[3169]=449,[3181]=450,[3187]=451,[3191]=452,[3203]=453,[3209]=454,[3217]=455,[3221]=456,[3229]=457,[3251]=458,[3253]=459,[3257]=460,[3259]=461,[3271]=462,[3299]=463,[3301]=464,[3307]=465,[3313]=466,[3319]=467,[3323]=468,[3329]=469,[3331]=470,[3343]=471,[3347]=472,[3359]=473,[3361]=474,[3371]=475,[3373]=476,[3389]=477,[3391]=478,[3407]=479,[3413]=480,[3433]=481,[3449]=482,[3457]=483,[3461]=484,[3463]=485,[3467]=486,[3469]=487,[3491]=488,[3499]=489,[3511]=490,[3517]=491,[3527]=492,[3529]=493,[3533]=494,[3539]=495,[3541]=496,[3547]=497,[3557]=498,[3559]=499,[3571]=500,[3581]=501,[3583]=502,[3593]=503,[3607]=504,[3613]=505,[3617]=506,[3623]=507,[3631]=508,[3637]=509,[3643]=510,[3659]=511,[3671]=512,[3673]=513,[3677]=514,[3691]=515,[3697]=516,[3701]=517,[3709]=518,[3719]=519,[3727]=520,[3733]=521,[3739]=522,[3761]=523,[3767]=524,[3769]=525,[3779]=526,[3793]=527,[3797]=528,[3803]=529,[3821]=530,[3823]=531,[3833]=532,[3847]=533,[3851]=534,[3853]=535,[3863]=536,[3877]=537,[3881]=538,[3889]=539,[3907]=540,[3911]=541,[3917]=542,[3919]=543,[3923]=544,[3929]=545,[3931]=546,[3943]=547,[3947]=548,[3967]=549,[3989]=550,[4001]=551,[4003]=552,[4007]=553,[4013]=554,[4019]=555,[4021]=556,[4027]=557,[4049]=558,[4051]=559,[4057]=560,[4073]=561,[4079]=562,[4091]=563,[4093]=564,[4099]=565,[4111]=566,[4127]=567,[4129]=568,[4133]=569,[4139]=570,[4153]=571,[4157]=572,[4159]=573,[4177]=574,[4201]=575,[4211]=576,[4217]=577,[4219]=578,[4229]=579,[4231]=580,[4241]=581,[4243]=582,[4253]=583,[4259]=584,[4261]=585,[4271]=586,[4273]=587,[4283]=588,[4289]=589,[4297]=590,[4327]=591,[4337]=592,[4339]=593,[4349]=594,[4357]=595,[4363]=596,[4373]=597,[4391]=598,[4397]=599,[4409]=600,[4421]=601,[4423]=602,[4441]=603,[4447]=604,[4451]=605,[4457]=606,[4463]=607,[4481]=608,[4483]=609,[4493]=610,[4507]=611,[4513]=612,[4517]=613,[4519]=614,[4523]=615,[4547]=616,[4549]=617,[4561]=618,[4567]=619,[4583]=620,[4591]=621,[4597]=622,[4603]=623,[4621]=624,[4637]=625,[4639]=626,[4643]=627,[4649]=628,[4651]=629,[4657]=630,[4663]=631,[4673]=632,[4679]=633,[4691]=634,[4703]=635,[4721]=636,[4723]=637,[4729]=638,[4733]=639,[4751]=640,[4759]=641,[4783]=642,[4787]=643,[4789]=644,[4793]=645,[4799]=646,[4801]=647,[4813]=648,[4817]=649,[4831]=650,[4861]=651,[4871]=652,[4877]=653,[4889]=654,[4903]=655,[4909]=656,[4919]=657,[4931]=658,[4933]=659,[4937]=660,[4943]=661,[4951]=662,[4957]=663,[4967]=664,[4969]=665,[4973]=666,[4987]=667,[4993]=668,[4999]=669,[5003]=670,[5009]=671,[5011]=672,[5021]=673,[5023]=674,[5039]=675,[5051]=676,[5059]=677,[5077]=678,[5081]=679,[5087]=680,[5099]=681,[5101]=682,[5107]=683,[5113]=684,[5119]=685,[5147]=686,[5153]=687,[5167]=688,[5171]=689,[5179]=690,[5189]=691,[5197]=692,[5209]=693,[5227]=694,[5231]=695,[5233]=696,[5237]=697,[5261]=698,[5273]=699,[5279]=700,[5281]=701,[5297]=702,[5303]=703,[5309]=704,[5323]=705,[5333]=706,[5347]=707,[5351]=708,[5381]=709,[5387]=710,[5393]=711,[5399]=712,[5407]=713,[5413]=714,[5417]=715,[5419]=716,[5431]=717,[5437]=718,[5441]=719,[5443]=720,[5449]=721,[5471]=722,[5477]=723,[5479]=724,[5483]=725,[5501]=726,[5503]=727,[5507]=728,[5519]=729,[5521]=730,[5527]=731,[5531]=732,[5557]=733,[5563]=734,[5569]=735,[5573]=736,[5581]=737,[5591]=738,[5623]=739,[5639]=740,[5641]=741,[5647]=742,[5651]=743,[5653]=744,[5657]=745,[5659]=746,[5669]=747,[5683]=748,[5689]=749,[5693]=750,[5701]=751,[5711]=752,[5717]=753,[5737]=754,[5741]=755,[5743]=756,[5749]=757,[5779]=758,[5783]=759,[5791]=760,[5801]=761,[5807]=762,[5813]=763,[5821]=764,[5827]=765,[5839]=766,[5843]=767,[5849]=768,[5851]=769,[5857]=770,[5861]=771,[5867]=772,[5869]=773,[5879]=774,[5881]=775,[5897]=776,[5903]=777,[5923]=778,[5927]=779,[5939]=780,[5953]=781,[5981]=782,[5987]=783,[6007]=784,[6011]=785,[6029]=786,[6037]=787,[6043]=788,[6047]=789,[6053]=790,[6067]=791,[6073]=792,[6079]=793,[6089]=794,[6091]=795,[6101]=796,[6113]=797,[6121]=798,[6131]=799,[6133]=800,[6143]=801,[6151]=802,[6163]=803,[6173]=804,[6197]=805,[6199]=806,[6203]=807,[6211]=808,[6217]=809,[6221]=810,[6229]=811,[6247]=812,[6257]=813,[6263]=814,[6269]=815,[6271]=816,[6277]=817,[6287]=818,[6299]=819,[6301]=820,[6311]=821,[6317]=822,[6323]=823,[6329]=824,[6337]=825,[6343]=826,[6353]=827,[6359]=828,[6361]=829,[6367]=830,[6373]=831,[6379]=832,[6389]=833,[6397]=834,[6421]=835,[6427]=836,[6449]=837,[6451]=838,[6469]=839,[6473]=840,[6481]=841,[6491]=842,[6521]=843,[6529]=844,[6547]=845,[6551]=846,[6553]=847,[6563]=848,[6569]=849,[6571]=850,[6577]=851,[6581]=852,[6599]=853,[6607]=854,[6619]=855,[6637]=856,[6653]=857,[6659]=858,[6661]=859,[6673]=860,[6679]=861,[6689]=862,[6691]=863,[6701]=864,[6703]=865,[6709]=866,[6719]=867,[6733]=868,[6737]=869,[6761]=870,[6763]=871,[6779]=872,[6781]=873,[6791]=874,[6793]=875,[6803]=876,[6823]=877,[6827]=878,[6829]=879,[6833]=880,[6841]=881,[6857]=882,[6863]=883,[6869]=884,[6871]=885,[6883]=886,[6899]=887,[6907]=888,[6911]=889,[6917]=890,[6947]=891,[6949]=892,[6959]=893,[6961]=894,[6967]=895,[6971]=896,[6977]=897,[6983]=898,[6991]=899,[6997]=900,[7001]=901,[7013]=902,[7019]=903,[7027]=904,[7039]=905,[7043]=906,[7057]=907,[7069]=908,[7079]=909,[7103]=910,[7109]=911,[7121]=912,[7127]=913,[7129]=914,[7151]=915,[7159]=916,[7177]=917,[7187]=918,[7193]=919,[7207]=920,[7211]=921,[7213]=922,[7219]=923,[7229]=924,[7237]=925,[7243]=926,[7247]=927,[7253]=928,[7283]=929,[7297]=930,[7307]=931,[7309]=932,[7321]=933,[7331]=934,[7333]=935,[7349]=936,[7351]=937,[7369]=938,[7393]=939,[7411]=940,[7417]=941,[7433]=942,[7451]=943,[7457]=944,[7459]=945,[7477]=946,[7481]=947,[7487]=948,[7489]=949,[7499]=950,[7507]=951,[7517]=952,[7523]=953,[7529]=954,[7537]=955,[7541]=956,[7547]=957,[7549]=958,[7559]=959,[7561]=960,[7573]=961,[7577]=962,[7583]=963,[7589]=964,[7591]=965,[7603]=966,[7607]=967,[7621]=968,[7639]=969,[7643]=970,[7649]=971,[7669]=972,[7673]=973,[7681]=974,[7687]=975,[7691]=976,[7699]=977,[7703]=978,[7717]=979,[7723]=980,[7727]=981,[7741]=982,[7753]=983,[7757]=984,[7759]=985,[7789]=986,[7793]=987,[7817]=988,[7823]=989,[7829]=990,[7841]=991,[7853]=992,[7867]=993,[7873]=994,[7877]=995,[7879]=996,[7883]=997,[7901]=998,[7907]=999,[7919]=1000}

return p