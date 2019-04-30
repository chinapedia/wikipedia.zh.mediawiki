-- 本模組將一般字母和數字聲調轉換為台語白話字。
-- 範例："Peh8-oe7-ji7"會被轉換為"Pe̍h-ōe-jī"。
-- 請透過{{模板:POJ}}來使用本模組的功能。

-- Pún bô͘-cho͘ kā it-poaⁿ Lô-má-jī kap sò͘-jī pian-e̍k chò Tâi-oân-ōe Pe̍h-ōe-jī.
-- Lē:  Peh8-oe7-ji7--> Pe̍h-ōe-jī
-- Chhiáⁿ sú-iōng {{Pang-bô͘:POJ}} lâi kek-oa̍h chia ê kong-lêng.

local p = {}

function attachTone(a, n)
    n = tonumber(n)
	
	if a == "O" then
	local upperO = {"O", "Ó", "Ò", "O", "Ô", "Ǒ", "Ō", "O̍"}
		if (n>=1 and n<=8) then return upperO[n] end
	return a
	end
 
 	if a == "o" then
    local lowerO = {"o", "ó", "ò", "o", "ô", "ǒ", "ō", "o̍"} 
		if (n>=1 and n<=8) then return lowerO[n] end
		return a
	end

	if a == "E" then
    local upperE = {"E", "É", "È", "E", "Ê", "Ě", "Ē", "E̍"}
		if (n>=1 and n<=8) then return upperE[n] end
		return a
	end
 
 	if a == "e" then
    local lowerE = {"e", "é", "è", "e", "ê", "ě", "ē", "e̍"}
		if (n>=1 and n<=8) then return lowerE[n] end
		return a
	end
	
    if a == "A" then
    local upperA = {"A", "Á", "À", "A", "Â", "Ǎ", "Ā", "A̍"}
    	if (n>=1 and n<=8) then return upperA[n] end
		return a
	end
	
	if a == "a" then
    local lowerA = {"a", "á", "à", "a", "â", "ǎ", "ā", "a̍"}
		if (n>=1 and n<=8) then return lowerA[n] end
		return a
	end

    if a == "U" then
    local upperU = {"U", "Ú", "Ù", "U", "Û", "Ǔ", "Ū", "U̍"}
		if (n>=1 and n<=8) then return upperU[n] end
		return a
	end

    if a == "u" then
    local lowerU = {"u", "ú", "ù", "u", "û", "ǔ", "ū", "u̍"}
		if (n>=1 and n<=8) then return lowerU[n] end
		return a
	end
 
    if a == "I" then
    local upperI = {"I", "Í", "Ì", "I", "Î", "Ǐ", "Ī", "I̍"}
		if (n>=1 and n<=8) then return upperI[n] end
		return a
	end
	
	if a == "i" then
    local lowerI = {"i", "í", "ì", "i", "î", "ǐ", "ī", "i̍"}
		if (n>=1 and n<=8) then return lowerI[n] end
		return a
	end
	
	if a == "N" then
    local upperN = {"N", "Ń", "Ǹ", "N", "N̂", "Ň", "N̄", "N̍"}
		if (n>=1 and n<=8) then return upperN[n] end
		return a
	end
	
    if a == "n" then
    local lowerN = {"n", "ń", "ǹ", "n", "n̂", "ň", "n̄", "n̍"}
		if (n>=1 and n<=8) then return lowerN[n] end
		return a
	end

    if a == "M" then
	local upperM = {"M", "Ḿ", "M̀", "M", "M̂", "M̌", "M̄", "M̍"}
        if (n>=1 and n<=8) then return upperM[n] end
		return a
	end
	
	if a == "m" then
	local lowerM = {"m", "ḿ", "m̀", "m", "m̂", "m̌", "m̄", "m̍"}
		if (n>=1 and n<=8) then return lowerM[n] end
		return a
	end
    
    if a == "Oo" then
    local upperOo = {"O͘", "Ó͘", "Ò͘", "O͘", "Ô͘", "Ǒ͘", "Ō͘", "O̍͘"} 
		if (n>=1 and n<=8) then return upperOo[n] end
        return a
	end
    
    if a == "oo" then
    local lowerOo = {"o͘", "ó͘", "ò͘", "o͘", "ô͘", "ǒ͘", "ō͘", "o̍͘"} 
		if (n>=1 and n<=8) then return lowerOo[n] end
		return a
	end
	return a
 
end

-- 以下依照字母附加調號的優先序排列，更動排列會導致輸出不同。
-- 順序：oa_, oe_, o, e, a, u, i, ng, m.
function selectVowel(rplce, n)
 
	if not rplce then return end
    -- oa_
    oax = {
        'Oai',
        'oai',
        'Oan',
        'oan',
        'Oah', --5
        'oah',
        'Oak',
        'oak',
        'Oat',
        'oat', --10
        'Oap',
        'oap'
    }
    for i=1, #oax do
        if rplce:find(oax[i]) then return rplce:gsub('a', attachTone('a', n)) end
    end
    
    OAx = {
        'OAI',
        'OAN',
        'OAH',
        'OAK',
        'OAT', --5
        'OAP',
    }
    for i=1, #OAx do
        if rplce:find(OAx[i]) then return rplce:gsub('A', attachTone('A', n)) end
    end

    -- oe_
   oex = {
        'Oei',
        'oei',
        'Oen',
        'oen',
        'Oeh', --5
        'oeh',
        'Oek',
        'oek',
        'Oet',
        'oet', --10
        'Oep',
        'oep'
    }
    for i=1, #oex do
        if rplce:find(oex[i]) then return rplce:gsub('e', attachTone('e', n)) end
    end
    
    OEx = {
        'OEI',
        'OEN',
        'OEH',
        'OEK',
        'OET', --5
        'OEP',
    }
    for i=1, #OEx do
        if rplce:find(OEx[i]) then return rplce:gsub('E', attachTone('E', n)) end
    end

    -- o, e, a, u, i, ng, m
    local oeauingm = {
        'oo',
        'Oo',
        'OO',
        'o',
        'O', --5
        'e',
        'E',
        'a',
        'A',
        'u', --10
        'U',
        'i',
        'I',
        'ng',
        'Ng', --15
        'NG',
        'm',
        'M'
    }
    local chara = {
        'oo',
        'Oo',
        'Oo',
        'o',
        'O', --5
        'e',
        'E',
        'a',
        'A',
        'u', --10
        'U',
        'i',
        'I',
        'n',
        'N', --15
        'N',
        'm',
        'M'
    }
    for i=1, #oeauingm do
        if rplce:find(oeauingm[i]) then
            return rplce:gsub(chara[i], attachTone(chara[i], n))
        end
    end
    
end
 
function p.POJ(frame)
	local input = frame.args[1]
	if not input then return end
	local out = input:gsub("([%a]+)(%d)", selectVowel):gsub("nn", "ⁿ"):gsub("NN", "ⁿ"):gsub("oo", "o͘"):gsub("Oo", "O͘"):gsub("OO", "O͘")
	return (out)
end
 
return p