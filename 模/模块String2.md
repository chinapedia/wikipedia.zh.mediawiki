local p = {}


p.upper = function(frame)
	local s = mw.text.trim(frame.args[1] or "")
	return string.upper(s)
end

p.lower = function(frame)
	local s = mw.text.trim(frame.args[1] or "")
	return string.lower(s)
end


p.sentence = function (frame )
	frame.args[1] = string.lower(frame.args[1])
	return p.ucfirst(frame)
end


p.ucfirst = function (frame )
	local s =  mw.text.trim( frame.args[1] or "" )
	local s1 = ""
	-- if it's a list chop off and (store as s1) everything up to the first <li>
	local lipos = string.find(s, "<li>" )
	if lipos then
		s1 = string.sub(s, 1, lipos + 3)
		s = string.sub(s, lipos + 4)
	end
	-- s1 is either "" or the first part of the list markup, so we can continue
	-- and prepend s1 to the returned string
	if string.find(s, "^%[%[[^|]+]]+%]%]") then
		-- this is a piped wikilink, so we capitalise the text, not the pipe
		local b, c = string.find(s, "|%A*%a") -- find the first letter after the pipe
		return s1 .. string.sub(s, 1, c-1) .. string.upper(string.sub(s, c, c)) .. string.sub(s, c+1)
	end
	local letterpos = string.find(s, '%a')
	if letterpos then
		local first = string.sub(s, 1, letterpos - 1)
		local letter = string.sub(s, letterpos, letterpos)
		local rest = string.sub(s, letterpos + 1)
		return s1 .. first .. string.upper(letter) .. rest
	else
		return s1 .. s
	end
end


p.title = function (frame )
	-- http://grammar.yourdictionary.com/capitalization/rules-for-capitalization-in-titles.html
	-- recommended by The U.S. Government Printing Office Style Manual:
	-- "Capitalize all words in titles of publications and documents,
	-- except a, an, the, at, by, for, in, of, on, to, up, and, as, but, or, and nor."
	local alwayslower = {['a'] = 1, ['an'] = 1, ['the'] = 1, 
		['and'] = 1, ['but'] = 1, ['or'] = 1, ['for'] = 1,
		['nor'] = 1, ['on'] = 1, ['in'] = 1, ['at'] = 1, ['to'] = 1,
		['from'] = 1, ['by'] = 1, ['of'] = 1, ['up'] = 1 }
	local res = ''
	local s =  mw.text.trim( frame.args[1] or "" )
	local words = mw.text.split( s, " ")
	for i, s in ipairs(words) do
		s = string.lower( s )
		if( i > 1 and alwayslower[s] == 1) then
			-- leave in lowercase
		else
			s = mw.getContentLanguage():ucfirst(s)
		end
		words[i] = s
	end
	return table.concat(words, " ")
end


-- stripZeros finds the first number and strips leading zeros (apart from units)
-- e.g "0940" -> "940"; "Year: 0023" -> "Year: 23"; "00.12" -> "0.12"
p.stripZeros = function(frame)
	local s = mw.text.trim(frame.args[1] or "")
	n = tonumber( string.match( s, "%d+" ) ) or ""
	s = string.gsub( s, "%d+", n, 1 )
	return s
end


-- nowiki ensures that a string of text is treated by the MediaWiki software as just a string
-- it takes an unnamed parameter and trims whitespace, then removes any wikicode
p.nowiki = function(frame)
	local str = mw.text.trim(frame.args[1] or "")
	return mw.text.nowiki(str)
end


-- posnq (position, no quotes) returns the numerical start position of the first occurrence
-- of one piece of text ("match") inside another ("str").
-- It returns nil if no match is found, or if either parameter is blank.
-- It takes the text to be searched in as the first unnamed parameter, which is trimmed.
-- It takes the text to match as the second unnamed parameter, which is trimmed and
-- any double quotes " are stripped out.
p.posnq = function(frame)
	local str = mw.text.trim(frame.args[1] or "")
	local match = mw.text.trim(frame.args[2] or ""):gsub('"', '')
	if  str == "" or match == "" then return nil end
	-- just take the start position
	local pos = str:find(match, 1, true)
	return pos
end


return p