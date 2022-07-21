local getArgs = require('Module:Arguments').getArgs
local clist = require('Module:Collapsible list').main
local compressSparseArray = require('Module:TableTools').compressSparseArray
local p = {}

--[[
Combine named-and-numbered arguments into a pretty list.
"Named-and-numbered" means foo, foo0, foo_1, foo234: anything that matches foo_?%d+

Arguments:
  args[1] = name to search arguments
  rest of args = arguments to search
Returns:
  Pretty list, in order of argument number.
  "foo" comes first, then "foo0", "foo1", ... "fooN"
  The argument numbering does not have to be sequential
  
  If number of args that match <= args[_limit] (4 default),
     returns text list of the form "A, B, C and D"
  otherwise returns collapsible list ({{clist}})
--]]
function p._main(args)
	local pattern = "^"..args[1].."_?(%d+)$"  -- pattern to match
	local values = {}
	for k, v in pairs(args) do  --- loop through all arguments
		if k == args[1] then    --- if argument is just "foo", put it first
			values[1] = v
		else
			ord = tonumber(mw.ustring.match(k,pattern)) --- if "foo_?%d+", extract number
			if ord then
				values[ord+2] = v  --- put value into list at number+2 (to keep "foo" first, even for foo0)
			end
		end
	end
	values = compressSparseArray(values)  --- squeeze out gaps/nils in values, keep ordering
	local limit = tonumber(args._limit) or 4
	if #values > limit then
		return clist(values)   --- if longer than limit, call Module:Collapsible list
	end
	return mw.text.listToText(values) --- otherwise just print out pretty text list
end

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

return p