-- This module takes positional parameters as input and concatenates them with
-- an optional separator. The final separator (the "conjunction") can be
-- specified independently, enabling natural-language lists like
-- "foo, bar, baz and qux".

local compressSparseArray = require('Module:TableTools').compressSparseArray
local p = {}

function p._main(args)
	local separator = args.separator
		-- Decode (convert to Unicode) HTML escape sequences, such as " " for space.
		and mw.text.decode(args.separator) or ''
	local conjunction = args.conjunction and mw.text.decode(args.conjunction) or separator
	-- Discard named parameters.
	local values = compressSparseArray(args)
	return mw.text.listToText(values, separator, conjunction)
end

local function makeInvokeFunction(separator, conjunction)
	return function (frame)
		local args = require('Module:Arguments').getArgs(frame)
		args.separator = separator or args.separator
		args.conjunction = conjunction or args.conjunction
		return p._main(args)
	end
end

p.main = makeInvokeFunction()
p.br = makeInvokeFunction('<br />')
p.comma = makeInvokeFunction(mw.message.new('comma-separator'):plain())

return p