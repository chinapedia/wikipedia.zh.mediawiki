local p = {}
 
function attachTone(a, n)
    n = tonumber(n)
	if a == "a" then
		if n == 1 then return "ā" end
		if n == 2 then return "á" end
		if n == 3 then return "ǎ" end
		if n == 4 then return "à" end
		return a
 
	end
 
	if a == "A" then
		if n == 1 then return "Ā" end
		if n == 2 then return "Á" end
		if n == 3 then return "Ǎ" end
		if n == 4 then return "À" end
		return a
 
	end
 
	if a == "e" then
		if n == 1 then return "ē" end
		if n == 2 then return "é" end
		if n == 3 then return "ě" end
		if n == 4 then return "è" end
		return a
 
	end
 
	if a == "E" then
		if n == 1 then return "Ē" end
		if n == 2 then return "É" end
		if n == 3 then return "Ě" end
		if n == 4 then return "È" end
		return a
 
	end
 
	if a == "i" then
		if n == 1 then return "ī" end
		if n == 2 then return "í" end
		if n == 3 then return "ǐ" end
		if n == 4 then return "ì" end
		return a
 
	end
 
	if a == "O" then
		if n == 1 then return "Ō" end
		if n == 2 then return "Ó" end
		if n == 3 then return "Ŏ" end
		if n == 4 then return "Ò" end
		return a
 
	end
 
	if a == "o" then
		if n == 1 then return "ō" end
		if n == 2 then return "ó" end
		if n == 3 then return "ǒ" end
		if n == 4 then return "ò" end
		return a
 
	end
 
	if a == "u" then
		if n == 1 then return "ū" end
		if n == 2 then return "ú" end
		if n == 3 then return "ǔ" end
		if n == 4 then return "ù" end
		return a
 
	end
 
	if (a == "v") or (a == "ü") then
		if n == 1 then return "ǖ" end
		if n == 2 then return "ǘ" end
		if n == 3 then return "ǚ" end
		if n == 4 then return "ǜ" end
		return "ü"
 
	end
 
	if a == "Ê" then
		if n == 1 then return "Ê̄" end
		if n == 2 then return "Ế" end
		if n == 3 then return "Ê̌" end
		if n == 4 then return "Ề" end
		return a
 
	end
 
	if a == "ê" then
		if n == 1 then return "ê̄" end
		if n == 2 then return "ế" end
		if n == 3 then return "ê̌" end
		if n == 4 then return "ề" end
		return a
 
	end
 
	if a == "N" then
		if n == 2 then return "Ń" end
		if n == 3 then return "Ň" end
		if n == 4 then return "Ǹ" end
		return a
 
	end
	if a == "n" then
		if n == 2 then return "ń" end
		if n == 3 then return "ň" end
		if n == 4 then return "ǹ" end
		return a
	end
 
	if a == "M" then
		if n == 2 then return "Ḿ" end
		if n == 4 then return "M̀" end
		return a
	end
	if a == "m" then
		if n == 2 then return "ḿ" end
		if n == 4 then return "m̀" end
		return a
	end
 
	return a
 
end
 
 
function selectVowel(chara, n)
 
	if not chara then
		return
	end
 
	if chara:find('^.*A') then
		return chara:gsub("A", attachTone("A", n))
	end
	if chara:find('^.*a') then
		return chara:gsub("a", attachTone("a", n))
	end
 
	if chara:find('^.*E') then
		return chara:gsub("E", attachTone("E", n))
	end
	if chara:find('^.*e') then
		return chara:gsub("e", attachTone("e", n))
	end
 
	if chara:find('^.*Ê') then
		return chara:gsub("Ê", attachTone("Ê", n))
	end
	if chara:find('^.*ê') then
		return chara:gsub("ê", attachTone("ê", n))
	end
 
	if chara:find('^.*iu') then
		return chara:gsub("iu", "i"..attachTone("u", n))
	end
	if chara:find('^.*i') then
		return chara:gsub("i", attachTone("i", n))
	end
 
	if chara:find('^.*O') then
		return chara:gsub("O", attachTone("O", n))
	end
	if chara:find('^.*o') then
		return chara:gsub("o", attachTone("o", n))
	end
 
	if chara:find('^.*u') then
		return chara:gsub("u", attachTone("u", n))
	end
 
	if chara:find('^.*v') then
		return chara:gsub("v", attachTone("v", n))
	end
	if chara:find('^.*ü') then
		return chara:gsub("ü", attachTone("ü", n))
	end
 
	if chara:find('^.*N') then
		return chara:gsub("N", attachTone("N", n))
	end
	if chara:find('^.*n') then
		return chara:gsub("n", attachTone("n", n))
	end
 
	if chara:find('^.*M') then
		return chara:gsub("M", attachTone("M", n))
	end
	if chara:find('^.*m') then
		return chara:gsub("m", attachTone("m", n))
	end
end
 
function p.pinyin(frame)
	local input = frame.args[1]
	if not input then
		return
	end
	local ve = input:gsub("nue", "nve"):gsub("lue", "lve")
	local out = ve:gsub("([%aüÊê]+)(%d)", selectVowel)
	return (out:gsub("v", "ü"))
end
 
 
return p