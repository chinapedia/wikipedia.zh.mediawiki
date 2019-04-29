--[[
------------------------------------------------------------------------------------
--                               TableTools                                       --
--                                                                                --
-- This module includes a number of functions for dealing with Lua tables.        --
-- It is a meta-module, meant to be called from other Lua modules, and should     --
-- not be called directly from #invoke.                                           --
------------------------------------------------------------------------------------
--]]

local libraryUtil = require('libraryUtil')

local p = {}

-- Define often-used variables and functions.
local floor = math.floor
local infinity = math.huge
local checkType = libraryUtil.checkType

--[[
------------------------------------------------------------------------------------
-- isPositiveInteger
--
-- This function returns true if the given value is a positive integer, and false
-- if not. Although it doesn't operate on tables, it is included here as it is
-- useful for determining whether a given table key is in the array part or the
-- hash part of a table.
------------------------------------------------------------------------------------
--]]
function p.isPositiveInteger(v)
	if type(v) == 'number' and v >= 1 and floor(v) == v and v < infinity then
		return true
	else
		return false
	end
end

--[[
------------------------------------------------------------------------------------
-- isNan
--
-- This function returns true if the given number is a NaN value, and false
-- if not. Although it doesn't operate on tables, it is included here as it is
-- useful for determining whether a value can be a valid table key. Lua will
-- generate an error if a NaN is used as a table key.
------------------------------------------------------------------------------------
--]]
function p.isNan(v)
	if type(v) == 'number' and tostring(v) == '-nan' then
		return true
	else
		return false
	end
end

--[[
------------------------------------------------------------------------------------
-- shallowClone
--
-- This returns a clone of a table. The value returned is a new table, but all
-- subtables and functions are shared. Metamethods are respected, but the returned
-- table will have no metatable of its own.
------------------------------------------------------------------------------------
--]]
function p.shallowClone(t)
	local ret = {}
	for k, v in pairs(t) do
		ret[k] = v
	end
	return ret
end

--[[
------------------------------------------------------------------------------------
-- removeDuplicates
--
-- This removes duplicate values from an array. Non-positive-integer keys are
-- ignored. The earliest value is kept, and all subsequent duplicate values are
-- removed, but otherwise the array order is unchanged.
------------------------------------------------------------------------------------
--]]
function p.removeDuplicates(t)
	checkType('removeDuplicates', 1, t, 'table')
	local isNan = p.isNan
	local ret, exists = {}, {}
	for i, v in ipairs(t) do
		if isNan(v) then
			-- NaNs can't be table keys, and they are also unique, so we don't need to check existence.
			ret[#ret + 1] = v
		else
			if not exists[v] then
				ret[#ret + 1] = v
				exists[v] = true
			end
		end	
	end
	return ret
end			

--[[
------------------------------------------------------------------------------------
-- numKeys
--
-- This takes a table and returns an array containing the numbers of any numerical
-- keys that have non-nil values, sorted in numerical order.
------------------------------------------------------------------------------------
--]]
function p.numKeys(t)
	checkType('numKeys', 1, t, 'table')
	local isPositiveInteger = p.isPositiveInteger
	local nums = {}
	for k, v in pairs(t) do
		if isPositiveInteger(k) then
			nums[#nums + 1] = k
		end
	end
	table.sort(nums)
	return nums
end

--[[
------------------------------------------------------------------------------------
-- affixNums
--
-- This takes a table and returns an array containing the numbers of keys with the
-- specified prefix and suffix. For example, for the table
-- {a1 = 'foo', a3 = 'bar', a6 = 'baz'} and the prefix "a", affixNums will
-- return {1, 3, 6}.
------------------------------------------------------------------------------------
--]]
function p.affixNums(t, prefix, suffix)
	checkType('affixNums', 1, t, 'table')
	checkType('affixNums', 2, prefix, 'string', true)
	checkType('affixNums', 3, suffix, 'string', true)

	local function cleanPattern(s)
		-- Cleans a pattern so that the magic characters ()%.[]*+-?^$ are interpreted literally.
		s = s:gsub('([%(%)%%%.%[%]%*%+%-%?%^%$])', '%%%1')
		return s
	end

	prefix = prefix or ''
	suffix = suffix or ''
	prefix = cleanPattern(prefix)
	suffix = cleanPattern(suffix)
	local pattern = '^' .. prefix .. '([1-9]%d*)' .. suffix .. '$'

	local nums = {}
	for k, v in pairs(t) do
		if type(k) == 'string' then			
			local num = mw.ustring.match(k, pattern)
			if num then
				nums[#nums + 1] = tonumber(num)
			end
		end
	end
	table.sort(nums)
	return nums
end

--[[
------------------------------------------------------------------------------------
-- numData
--
-- Given a table with keys like ("foo1", "bar1", "foo2", "baz2"), returns a table
-- of subtables in the format 
-- { [1] = {foo = 'text', bar = 'text'}, [2] = {foo = 'text', baz = 'text'} }
-- Keys that don't end with an integer are stored in a subtable named "other".
-- The compress option compresses the table so that it can be iterated over with
-- ipairs.
------------------------------------------------------------------------------------
--]]
function p.numData(t, compress)
	checkType('numData', 1, t, 'table')
	checkType('numData', 2, compress, 'boolean', true)
	local ret = {}
	for k, v in pairs(t) do
		local prefix, num = mw.ustring.match(tostring(k), '^([^0-9]*)([1-9][0-9]*)$')
		if num then
			num = tonumber(num)
			local subtable = ret[num] or {}
			if prefix == '' then
				-- Positional parameters match the blank string; put them at the start of the subtable instead.
				prefix = 1
			end
			subtable[prefix] = v
			ret[num] = subtable
		else
			local subtable = ret.other or {}
			subtable[k] = v
			ret.other = subtable
		end
	end
	if compress then
		local other = ret.other
		ret = p.compressSparseArray(ret)
		ret.other = other
	end
	return ret
end

--[[
------------------------------------------------------------------------------------
-- compressSparseArray
--
-- This takes an array with one or more nil values, and removes the nil values
-- while preserving the order, so that the array can be safely traversed with
-- ipairs.
------------------------------------------------------------------------------------
--]]
function p.compressSparseArray(t)
	checkType('compressSparseArray', 1, t, 'table')
	local ret = {}
	local nums = p.numKeys(t)
	for _, num in ipairs(nums) do
		ret[#ret + 1] = t[num]
	end
	return ret
end

--[[
------------------------------------------------------------------------------------
-- sparseIpairs
--
-- This is an iterator for sparse arrays. It can be used like ipairs, but can
-- handle nil values.
------------------------------------------------------------------------------------
--]]
function p.sparseIpairs(t)
	checkType('sparseIpairs', 1, t, 'table')
	local nums = p.numKeys(t)
	local i = 0
	local lim = #nums
	return function ()
		i = i + 1
		if i <= lim then
			local key = nums[i]
			return key, t[key]
		else
			return nil, nil
		end
	end
end

--[[
------------------------------------------------------------------------------------
-- size
--
-- This returns the size of a key/value pair table. It will also work on arrays,
-- but for arrays it is more efficient to use the # operator.
------------------------------------------------------------------------------------
--]]
function p.size(t)
	checkType('size', 1, t, 'table')
	local i = 0
	for k in pairs(t) do
		i = i + 1
	end
	return i
end

return p