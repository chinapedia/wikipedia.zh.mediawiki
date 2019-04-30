-- <nowiki>
-- DISCLAIMER:The module's origin page is on http://elderscrolls.wikia.com/wiki/Module:DragonScript, and it was made by FLIGHTMARE, a FANDOM user. 
-- Thanks a lot, Flightmare! Now Let's begin!
 
local p = {}
 
local doublelut = {
	["aa"] = true,
	["ah"] = true,
	["ei"] = true,
	["ey"] = true,
	["ii"] = true,
	["ir"] = true,
	["oo"] = true,
	["uu"] = true,
	["ur"] = true
}
 
local singlelut = {
    ["a"] = true,
    ["b"] = true,
    ["d"] = true,
    ["e"] = true,
    ["f"] = true,
    ["g"] = true,
    ["h"] = true,
    ["i"] = true,
    ["j"] = true,
    ["k"] = true,
    ["l"] = true,
    ["m"] = true,
    ["n"] = true,
    ["o"] = true,
    ["p"] = true,
    ["q"] = true,
    ["r"] = true,
    ["s"] = true,
    ["t"] = true,
    ["u"] = true,
    ["v"] = true,
    ["w"] = true,
    ["x"] = true,
    ["y"] = true,
    ["z"] = true
}
 
function parse(s, size, result)
	if string.len(s) == 0 then
		return result
	end
	if string.sub(s, 1, 1) == "_" then
		result = result .. "[[File:TransparentSpacer.png|" .. size .."]]"
		return parse(string.sub(s, 2), size, result)
	end
	if  doublelut[string.sub(s, 1, 2)] then
		result = result .. "[[File:Dovahzul-"_.._string.upper(string.sub(s,_1,_2))_.._".png|" .. size .."]]"
		return parse(string.sub(s, 3), size, result)
	end
	if  singlelut[string.sub(s, 1, 1)] then
		result = result .. "[[File:Dovahzul-"_.._string.upper(string.sub(s,_1,_1))_.._".png|" .. size .."]]"
		return parse(string.sub(s, 2), size, result)
	end
	return result
end
 
function p.transcribe(frame)
	local result = ''
	if(frame.args[2]) then
		size = frame.args[2]
	else
		size = "16px"
	end
	return parse (frame.args[1]:lower(), size, result)
end
 
return p
 
--</nowiki>