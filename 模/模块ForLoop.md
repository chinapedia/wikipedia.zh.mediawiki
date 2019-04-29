-- This module implements {{for loop}}.

local getArgs = require('Module:Arguments').getArgs

p = {}

function p.main(frame)
	local args = getArgs(frame, {
		trim = false,
		removeBlanks = false
	})
	return p._main(args)
end

function p._main(args)
	local template = args['call'] or 'void'
	local variableParam = args.pv
	variableParam = tonumber(variableParam) or variableParam or 1 -- fix for positional parameters
	local variableValPrefix = args.prefix or ''
	local variableValPostfix = args.postfix or ''
	local sep = args[1] or ''
	local constantArgs = p.getConstants(args)
	local variableVals = p.getVariableVals(args)

	local result = ''
	for i, v in ipairs(variableVals) do
		v = mw.text.trim(v) -- trim whitespace
		local targs = constantArgs
		targs[variableParam] = variableValPrefix .. v .. variableValPostfix
		local expandedTemplate = p.callTemplate(template, targs)
		result = result .. expandedTemplate
		if variableVals[i + 1] then
			result = result .. sep
		end
	end
	return result
end

function p.getConstants(args)
	local constantArgNums = p.getArgNums(args, 'pc', 'n')
	local constantArgs = {}
	for _, num in ipairs(constantArgNums) do
		local keyArg = 'pc' .. tostring(num) .. 'n'
		local valArg = 'pc' .. tostring(num) .. 'v'
		local key = args[keyArg]
		key = tonumber(key) or key
		local value = args[valArg]
		constantArgs[key] = value
	end
	return constantArgs
end

function p.getVariableVals(args)
	local variableVals = {}
	for i, v in ipairs(args) do
		if i ~= 1 then
			variableVals[i - 1] = v
		end
	end
	return variableVals
end

function p.getArgNums(args, prefix, suffix)
	-- Returns a table containing the numbers of the arguments that exist
	-- for the specified prefix and suffix.
	local nums = {}
	local pattern = '^' .. prefix .. '([1-9]%d*)' .. suffix .. '$'
	for k, v in pairs(args) do
		local num = tostring(k):match(pattern)
		if num then
			nums[#nums + 1] = tonumber(num)
		end
	end
	table.sort(nums)
	return nums
end

function p.callTemplate(template, targs)
	return mw.getCurrentFrame():expandTemplate{title = template, args = targs}
end

return p