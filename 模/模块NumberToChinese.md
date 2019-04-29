local p = {}

function stringToTable(s) --字串轉陣列
	local t = {}
	for i = 1, #s do
		t[i] = s:sub(i, i)
	end
	return t
end
local ClearTenOne, NoClearOne, ClearAllOne = 0, 1, 2 --清除首位1的狀況，清十前1、不清1、清所有首位1
local Normal, Financial = 0, 1 --小寫和大寫
local Over, Ten, Hundred, Thousand, LargeStart = 10, 11, 12, 13, 14 --Over是萬進的節點ID，LargeStart是萬進位數中文的開始ID
local standard = { { '〇', '一', '二', '三', '四', '五', '六', '七', '八', '九' }, { '零', '壹', '貳', '叄', '䦉', '伍', '陸', '柒', '捌', '玖' } }
local decimal = { { '', '十', '百', '千' }, { '', '拾', '佰', '仟' } }
local large = { '', '萬', '億', '兆', '京', '垓', '秭', '穰', '溝', '澗', '正', '載', '極', '恆河沙', '阿僧祇', '那由他', '不可思議', '無量', '大數' }
local largeSize = #large

function argsToVariable(frame) --輸入參數陣列轉變數
	local args = require('Module:Arguments').getArgs(frame)
	local number = args.num or args.number or args[1] or 0
	local numberType = args.b or args.daiji or args.numberType or Normal
	numberType = tonumber(numberType) or Normal
	if (numberType > Financial) then
		numberType = Financial
	end
	local clearOne = args.ten or args.clearOne or ClearTenOne
	clearOne = tonumber(clearOne) or ClearTenOne
	if (clearOne > ClearAllOne) then
		clearOne = ClearAllOne
	end
	return number, numberType, clearOne
end
function p.Number_to_Chinese(frame) --進位系統的中文數字
	return NumberToChinese(argsToVariable(frame))
end
function p.Number_to____(frame) --編號的中文數字
	return NumberToChineseNumbering(argsToVariable(frame))
end

function IDToChinese(id, numberType) --由上述定義可以知道ID代表意義
	if id < Over then
		return standard[numberType + 1][id + 1]
	elseif id < LargeStart then
		return decimal[numberType + 1][id - Over + 1]
	elseif id < LargeStart + largeSize then
		return large[id - LargeStart + 1]
	else
		local overlying, quotient = '', (id - LargeStart)
		remainder = quotient % (largeSize - 1)
		overlying = large[remainder + 1]
		quotient = (quotient - remainder) / (largeSize - 1)
		for i=1,quotient do overlying = overlying .. large[largeSize] end
		return overlying
		--return 'large' .. (id - LargeStart)
	end
end
function LessThan10000ToID(number) --低於10000的轉換，用途為中文數字是萬進
	local id = {}
	table.insert(id, 0) --先丟0讓千位判斷較容易
	local numberArr = stringToTable(number .. '')
	for i = 1, 4 do
		repeat
			if id[#id] == 0 and numberArr[i] == '0' then --當連續0的時候直接跳出
				break
			elseif id[#id] ~= 0 and numberArr[i] == '0' then --當上一位不是0，目前是0時單純加入0不加入千百十的ID
				table.insert(id, 0)
				break
			end
			table.insert(id, tonumber(numberArr[i])) --其他狀況就照一般說法位數大小和位數名稱
			table.insert(id, Thousand - i + 1)
		until true
	end
	if numberArr[1] ~= '0' then --如果千位不為0把首位0去除
		table.remove(id, 1)
	end
	if #id > 1 then --只有在0000的時候ID個數才會只有1
		id[#id] = Over
	else
		table.insert(id, Over)
	end
	return id
end
function FrontNumberToChinese(number, numberType, clearOne) --這邊的前數指的是大數，但實際英文並非如此稱呼，只是要讓名稱淺顯易懂
	number = '0000' .. number --把位數補到4的倍數，先補4個0在清除多餘的，下列程式本身有去除首位0的功能，若首位0會自動消除
	number = number:sub(#number % 4 + 1)
	local numberLargeLength = #number / 4
	local id = {}
	table.insert(id, 0) --先補0讓最高的萬進位數容易判斷
	for i = 1, numberLargeLength do
		repeat
			local data = LessThan10000ToID(number:sub(i * 4 - 3, i * 4 - 3 + 4))
			if id[#id] == 0 and #data == 2 then --如果上一個萬進位數為0，目前也為0(0000的ID個數最後有加上Over，所以為2)，則直接跳出
				break
			elseif id[#id] ~= 0 and #data == 2 then --如果上一個萬進位數不為0，目前為0，補0跳出
				table.insert(id, 0)
				break
			elseif id[#id] == 0 and data[1] == 0 then --如果上一個萬進位數為0，目前的萬進位數首位為0，清除掉首位0
				table.remove(data, 1)
			end
			for j = 1, #data do --將目前的萬進位數加入到ID陣列裡
				table.insert(id, data[j])
			end
			id[#id] = LargeStart + numberLargeLength - i --最後補上萬進位數的ID
		until true
	end
	if #id == 1 then --ID長度為1代表答案是0
		return IDToChinese(0, numberType)
	end
	table.remove(id, 1) --清除首位0
	table.remove(id, #id) --清除最後一個元素，有可能是萬進位數的第1個空格ID，也有可能是末位0
	if clearOne == ClearTenOne and id[1] == 1 and id[2] == Ten then --如果是選擇清十前1，則必須首位要是一十才清1
		table.remove(id, 1)
	elseif clearOne == ClearAllOne and id[1] == 1 and #id > 1 then --不管如何首位1都清，但是單獨1不清1
		table.remove(id, 1)
	end
	local chinese = '' --轉成中文回傳
	for i = 1, #id do
		chinese = chinese .. IDToChinese(id[i], numberType)
	end
	return chinese
end
function BackNumberToChinese(number, numberType) --這邊的後數指的是小數，但實際英文並非如此稱呼，只是要讓名稱淺顯易懂
	local chinese = ''
	local numberLength = #number
	local numberArr = stringToTable(number .. '')
	while numberLength > 0 do --尋找末位0的個數，並扣除個數
		if numberArr[numberLength] ~= '0' then
			break
		else
			numberLength = numberLength - 1
		end
	end
	for i = 1, numberLength do --直接轉成中文回傳
		chinese = chinese .. IDToChinese(tonumber(numberArr[i]), numberType)
	end
	return chinese
end

--轉給其他模組使用，但為了避免影響其他運作中模板，改為函數呼叫
--因此此函數命名遵照[[Wikipedia:Lua代码风格#命名常规|Wikipedia:Lua代码风格#命名常规]]
function p._numberToChinese(number, numberType, clearOne)
	return NumberToChinese(tostring(number), numberType or 0, clearOne or 0) --轉中文
end

function NumberToChinese(number, numberType, clearOne) --轉中文
	standard[Normal + 1][0 + 1] = standard[Financial + 1][0 + 1] --一般數量時大小寫的0皆使用「零」，然後Lua的陣列從1開始
	local chinese = ''
	if number:sub(1, 1) == '+' then --有正號才顯示正
		chinese = chinese .. '正'
		number = number:sub(2, #number)
	elseif number:sub(1, 1) == '-' then
		chinese = chinese .. '負'
		number = number:sub(2, #number)
	end
	if number == '∞' then
		chinese = chinese .. '無窮大'
		return chinese
	end
	local frontNumber, backNumber = '', ''
	local point = number:find('%.')
	if point == nil then --如果小數點不存在代表只有大數
		frontNumber = number
	else
		frontNumber = number:sub(1, point - 1)
		backNumber = number:sub(point + 1, #number)
	end
	if tonumber('0' .. frontNumber) == nil or tonumber(backNumber .. '0') == nil then --lua空字串判斷為非數值，所以一定要至少補1個0
		return '這不是一個數字'
	end
	chinese = chinese .. FrontNumberToChinese(frontNumber, numberType, clearOne)
	local backChinese = BackNumberToChinese(backNumber, numberType)
	if backChinese ~= '' then --如果小數為空字串則連小數點都不加入中文字串
		chinese = chinese .. '點' .. backChinese
	end
	return chinese
end
function NumberToChineseNumbering(number, numberType) --編號用途，編號只敘述數字不敘述進位系統，且有多個「點」和「之」
	local chinese = ''
	local numberLength = #number
	local numberArr = stringToTable(number .. '')
	for i = 1, numberLength do
		if numberArr[i] == '.' then --小數點在編號時中文通常念作「點」
			chinese = chinese .. '點'
		elseif numberArr[i] == '-' then --減號在編號時中文通常念作「之」
			chinese = chinese .. '之'
		elseif tonumber(numberArr[i]) ~= nil then
			chinese = chinese .. IDToChinese(tonumber(numberArr[i]), numberType)
		end
	end
	return chinese	
end
return p