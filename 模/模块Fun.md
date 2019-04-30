local p = {}

local ustring = mw.ustring
local libraryUtil = require "libraryUtil"
local checkType = libraryUtil.checkType
local checkTypeMulti = libraryUtil.checkTypeMulti

local iterableTypes = { "table", "string" }

local _checkCache = {}
local function _check(funcName, expectType)
	if type(expectType) == "string" then
		return function(argIndex, arg, nilOk)
			return checkType(funcName, argIndex, arg, expectType, nilOk)
		end
	else
		-- Lua 5.1 doesn't cache functions as Lua 5.3 does.
		local checkFunc = _checkCache[funcName]
			or function(argIndex, arg, expectType, nilOk)
				if type(expectType) == "table" then
					if not (nilOk and arg == nil) then
						return checkTypeMulti(funcName, argIndex, arg, expectType)
					end
				else
					return checkType(funcName, argIndex, arg, expectType, nilOk)
				end
			end
		_checkCache[funcName] = checkFunc
		return checkFunc
	end
end

-- Iterate over UTF-8-encoded codepoints in string.
local function iterString(str)
	local iter = string.gmatch(str, "[%z\1-\127\194-\244][\128-\191]*")
	local i = 0
	local function iterator()
		i = i + 1
		local char = iter()
		if char then
			return i, char
		end
	end
	
	return iterator
end

-- funcName and startArg are for argument type-checking.
-- The varargs (...) can be either an iterator and its optional state and start
-- value, or an iterable type, in which case the function calls the appropriate
-- iterator generator function.
local function getIteratorTriplet(funcName, startArg, ...)
	local t = type(...)
	if t == "function" then
		return ...
	end
	
	local first = ...
	checkTypeMulti(funcName, startArg, first, iterableTypes)
	if t == "string" then
		return iterString(first)
	elseif first[1] ~= nil then
		return ipairs(first)
	else
		return pairs(first)
	end
end

function p.chain(func1, func2, ...)
	return func1(func2(...))
end

--	map(function(number) return number ^ 2 end,
--		{ 1, 2, 3 })									--> { 1, 4, 9 }
--	map(function (char) return string.char(string.byte(char) - 0x20) end,
--		"abc")											--> { "A", "B", "C" }
-- Two argument formats:
-- map(func, iterable)
-- map(func, iterator[, state[, start_value]])
-- func is a function that takes a maximum of two return values of the iterator
-- in reverse order. They are supplied in reverse order because the ipairs
-- iterator returns the index before the value, but the value is most often more
-- important than the index.

-- Any need for map that retains original keys, rather than creating an array?
function p.map(func, keepOriginalKeys, ...)
	checkType("map", 1, func, "function")
	
	local iter, state, start_value
	if type(keepOriginalKeys) == "boolean" then
		iter, state, start_value = getIteratorTriplet("map", 3, ...)
	else -- keepOriginalKeys is actually iterator or iterable.
		iter, state, start_value = getIteratorTriplet("map", 2, keepOriginalKeys, ...)
		keepOriginalKeys = false
	end
	
	local result = {}
	if keepOriginalKeys then
		for val1, val2 in iter, state, start_value do
			result[val1] = func(val2, val1, state)
		end
	else
		local i = 0
		for val1, val2 in iter, state, start_value do
			i = i + 1
			result[i] = func(val2, val1, state)
		end
	end
	return result
end

p.mapIter = p.map

local function fold(func, result, ...)
	checkType("fold", 1, func, "function")
	local iter, state, start_value = getIteratorTriplet("fold", 3, ...)
	for val1, val2 in iter, state, start_value do
		result = func(result, val2, val1, state)
	end
	return result
end
p.fold = fold

function p.count(func, ...)
	checkType("count", 1, func, "function")
	
	return fold(
		function (count, val)
			if func(val) then
				return count + 1
			end
			return count
		end,
		0,
		...)
end

function p.forEach(func, ...)
	checkType("forEach", 1, func, "function")
	
	local iter, state, start_value = getIteratorTriplet("forEach", 2, ...)
	for val1, val2 in iter, state, start_value do
		func(val2, val1, state)
	end
	return nil
end

-------------------------------------------------
-- From http://lua-users.org/wiki/CurriedLua.
-- reverse(...) : take some tuple and return a tuple of elements in reverse order
--
-- e.g. "reverse(1,2,3)" returns 3,2,1
local function reverse(...)
	-- reverse args by building a function to do it, similar to the unpack() example
	local function reverseHelper(acc, v, ...)
		if select("#", ...) == 0 then
			return v, acc()
		else
			return reverseHelper(function() return v, acc() end, ...)
		end
	end
	
	-- initial acc is the end of the list
	return reverseHelper(function() return end, ...)
end

function p.curry(func, numArgs)
	-- currying 2-argument functions seems to be the most popular application
	numArgs = numArgs or 2
	
	-- no sense currying for 1 arg or less
	if numArgs <= 1 then return func end
	
	-- helper takes an argTrace function, and number of arguments remaining to be applied
	local function curryHelper(argTrace, n)
		if n == 0 then
			-- kick off argTrace, reverse argument list, and call the original function
			return func(reverse(argTrace()))
		else
			-- "push" argument (by building a wrapper function) and decrement n
			return function(onearg)
				return curryHelper(function() return onearg, argTrace() end, n - 1)
			end
		end
	end
	
	-- push the terminal case of argTrace into the function first
	return curryHelper(function() return end, numArgs)
end

-------------------------------------------------

--	some(function(val) return val % 2 == 0 end,
--		{ 2, 3, 5, 7, 11 })						--> true
function p.some(func, ...)
	checkType("some", 1, func, "function")
	
	local iter, state, start_value = getIteratorTriplet("some", 2, ...)
	for val1, val2 in iter, state, start_value do
		if func(val2, val1, state) then
			return true
		end
	end
	
	return false
end

--	all(function(val) return val % 2 == 0 end,
--		{ 2, 4, 8, 10, 12 })					--> true
function p.all(func, ...)
	checkType("some", 1, func, "function")
	
	local iter, state, start_value = getIteratorTriplet("all", 2, ...)
	for val1, val2 in iter, state, start_value do
		if not func(val2, val1, state) then
			return false
		end
	end
	
	return true
end

function p.indexOf(func, ...)
	local iter, state, start_value = getIteratorTriplet("indexOf", 2, ...)
	
	if type(func) == "function" then
		for val1, val2 in iter, state, start_value do
			if func(val2, val1, state) then
				return val1
			end
		end
	
	-- func is actually value to search for.
	-- Not a great idea to combine these two separate functions.
	elseif func ~= nil then -- check for NaN?
		for val1, val2 in iter, state, start_value do
			if func == val2 then
				return val1
			end
		end
	else
		error("value to search for is nil")
	end
	
	return nil
end

function p.filter(func, ...)
	local check = _check 
	checkType("filter", 1, func, "function")
	
	local new_t = {}
	local new_i = 0
	local iter, state, start_value = getIteratorTriplet("filter", 2, ...)
	for val1, val2 in iter, state, start_value do
		if func(v2, v1, state) then
			new_i = new_i + 1
			new_t[new_i] = v
		end
	end
	
	return new_t
end

function p.range(low, high)
	low = low - 1
	return function ()
		if low < high then
			low = low + 1
			return low
		end
	end
end


-------------------------------
-- Fancy stuff
local function capture(...)
	local vals = { ... }
	return function()
		return unpack(vals)
	end
end

-- Log input and output of function.
-- Receives a function and returns a modified form of that function.
function p.logReturnValues(func, prefix)
	return function(...)
		local inputValues = capture(...)
		local returnValues = capture(func(...))
		if prefix then
			mw.log(prefix, inputValues())
			mw.log(returnValues())
		else
			mw.log(inputValues())
			mw.log(returnValues())
		end
		return returnValues()
	end
end

p.log = p.logReturnValues

-- Convenience function to make all functions in a table log their input and output.
function p.logAll(t)
	for k, v in pairs(t) do
		if type(v) == "function" then
			t[k] = p.logReturnValues(v, tostring(k))
		end
	end
	return t
end

----- M E M O I Z A T I O N-----
-- metamethod that does the work
-- Currently supports one argument and one return value.
local func_key = {}
local function callMethod(self, x)
	local output = self[x]
	if not output then
		output = self[func_key](x)
		self[x] = output
	end
	return output
end

-- shared metatable
local mt = { __call = callMethod }

-- Create callable table.
function p.memoize(func)
	return setmetatable({ [func_key] = func }, mt)
end

-------------------------------

return p