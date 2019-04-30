-- This module produces a count of all the arguments passed to it.

local yesno = require('Module:Yesno')

-- Trim a string
local function trim(s)
	return s:match('^%s*(.-)%s*$')
end

-- Test whether a string is blank
local function isBlank(s)
	return not s:find('%S')
end

-- Tests whether a string is a valid positional key, and if so, returns it. If
-- the key is invalid, this returns nil.
local function isPositionalKey(s)
	s = trim(s)
	if s:find('^[1-9][0-9]*$') then
		return tonumber(s)
	end
end

-- Return the count of all arguments for which testFunc returns a truthy value.
local function count(args, testFunc)
	local ret = 0
	for key, val in pairs(args) do
		if testFunc(key, val) then
			ret = ret + 1
		end
	end
	return ret
end

-- Check shared arguments and get the parent argument count.
local function main(frame, testFunc)
	local blankifiedTestFunc
	if yesno(frame.args.checkblanks) ~= false then
		-- Extend the test function to check for blanks as well.
		blankifiedTestFunc = function (key, val)
			if not isBlank(val) then
				return testFunc(key, val)
			end
		end
	else
		blankifiedTestFunc = testFunc
	end
	return count(frame:getParent().args, blankifiedTestFunc)
end

return {
	-- Called with {{#invoke:ParameterCount|all}}
	-- All specified parameters are counted, even those not supported by the
	-- template.
	all = function (frame)
		return main(frame, function () return true end)
	end,

	-- Called with {{#invoke:ParameterCount|main}}
	-- Users can specify a list of parameters to check, and a list of Lua
	-- Ustring patterns to check each parameter against.
	main = function (frame)
		local args = frame.args
		local keys, patterns = {}, {}
		
		-- Get key list
		for i, key in ipairs(args) do
			local positionalKey = isPositionalKey(key)
			if positionalKey then
				keys[positionalKey] = true
			else
				keys[trim(key)] = true
			end
		end

		-- Get patterns
		do
			local function getPattern(i)
				local pattern = args['pattern' .. tostring(i)]
				if pattern and pattern ~= '' then
					return pattern
				end
			end
			local i = 1
			local pattern = getPattern(i)
			while pattern do
				patterns[i] = pattern
				i = i + 1
				pattern = getPattern(i)
			end
		end

		-- Construct the test function
		local testFunc = function (key, val)
			if keys[key] then
				return true
			end
			for i, pattern in ipairs(patterns) do
				if mw.ustring.find(tostring(key), pattern) then
					return true
				end
			end
			return false
		end

		return main(frame, testFunc)
	end
}