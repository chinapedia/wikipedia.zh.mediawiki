-- This module provides functions for making MediaWiki template invocations.

local checkType = require('libraryUtil').checkType

local p = {}

------------------------------------------------------------------------
--         Name:  p.name
--      Purpose:  Find a template invocation name from a page name or a
--                mw.title object.
--  Description:  This function detects whether a string or a mw.title
--                object has been passed in, and uses that to find a
--                template name as it is used in template invocations.
--   Parameters:  title - full page name or mw.title object for the
--                template (string or mw.title object)
--      Returns:  String
------------------------------------------------------------------------

function p.name(title)
	if type(title) == 'string' then
		title = mw.title.new(title)
		if not title then
			error("invalid title in parameter #1 of function 'name'", 2)
		end
	elseif type(title) ~= 'table' or type(title.getContent) ~= 'function' then
		error("parameter #1 of function 'name' must be a string or a mw.title object", 2)
	end
	if title.namespace == 10 then
		return title.text
	elseif title.namespace == 0 then
		return ':' .. title.prefixedText
	else
		return title.prefixedText
	end
end

------------------------------------------------------------------------
--         Name:  p.invocation
--      Purpose:  Construct a MediaWiki template invocation.
--  Description:  This function makes a template invocation from the
--                name and the arguments given. Note that it isn't
--                perfect: we have no way of knowing what whitespace was
--                in the original invocation, the order of the parameters
--                may be changed, and any parameters with duplicate keys
--                will be removed.
--   Parameters:  name - the template name, formatted as it will appear
--                    in the invocation. (string)
--                args - a table of template arguments. (table)
--                format - formatting options. (string, optional)
--                    Set to "nowiki" to escape, curly braces, pipes and
--                    equals signs with their HTML entities. The default
--                    is unescaped.
--      Returns:  String
------------------------------------------------------------------------

function p.invocation(name, args, format)
	checkType('invocation', 1, name, 'string')
	checkType('invocation', 2, args, 'table')
	checkType('invocation', 3, format, 'string', true)

	-- Validate the args table and make a copy to work from. We need to
	-- make a copy of the table rather than just using the original, as
	-- some of the values may be erased when building the invocation.
	local invArgs = {}
	for k, v in pairs(args) do
		local typek = type(k)
		local typev = type(v)
		if typek ~= 'string' and typek ~= 'number'
			or typev ~= 'string' and typev ~= 'number'
		then
			error("invalid arguments table in parameter #2 of " ..
			"'invocation' (keys and values must be strings or numbers)", 2)
		end
		invArgs[k] = v
	end

	-- Get the separators to use.
	local seps = {
		openb = '{{',
		closeb = '}}',
		pipe = '|',
		equals = '='
	}
	if format == 'nowiki' then
		for k, v in pairs(seps) do
			seps[k] = mw.text.nowiki(v)
		end
	end

	-- Build the invocation body with numbered args first, then named.
	local ret = {}
	ret[#ret + 1] = seps.openb
	ret[#ret + 1] = name
	for k, v in ipairs(invArgs) do
		if v:find('=', 1, true) then
			-- Likely something like 1=foo=bar, we need to do it as a named arg
			break
		end
		ret[#ret + 1] = seps.pipe
		ret[#ret + 1] = v
		invArgs[k] = nil -- Erase the key so that we don't add the value twice
	end
	for k, v in pairs(invArgs) do
		ret[#ret + 1] = seps.pipe
		ret[#ret + 1] = k
		ret[#ret + 1] = seps.equals
		ret[#ret + 1] = v
	end
	ret[#ret + 1] = seps.closeb

	return table.concat(ret)
end

return p