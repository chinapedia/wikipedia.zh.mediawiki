-- Module for different search and replace operations on strings.
local p = {}

-- Takes one string parameter, and returns the string with all characters with special meaning for Lua patterns escaped with a preceding `%`.
function p.escape_pattern(text)
    -- Replaces each occurrence of any of ().%+-*?[^$ with a `%` and then the character.
    local r = string.gsub(text, "[%(%)%.%%%+%-%*%?%[%^%$]", "%%%1")
    return r
end

-- Returns the first parameter, with all occurrences of the second parameter replaced with the third parameter.
-- All special characters are ignored: {{#invoke:StringReplace|replace_all|test.a%1$foo|%1|bar}} results in `test.abarfoo`.
function p.replace_all(frame)
    local str = frame.args[1]
    local strToFind = frame.args[2]
    local strToreplaceWith = frame.args[3]
    local r = string.gsub(str, p.escape_pattern(strToFind), p.escape_pattern(strToreplaceWith))
    return r
end

p['encode wiki page name'] = function( frame )
	local x = mw.ustring.gsub( 
		frame.args[1] or '', 
		'[\'"&_]', 
		{ 
			["'"] = '&#39;', 
			['"'] = '"', 
			['&'] = '&', 
			['_'] = ' ', 
		} 
	)
	return mw.text.trim( x )
end

return p