-- This module finds the length of an array, or of a quasi-array with keys such
-- as "data1", "data2", etc., using a binary search algorithm.

local checkType = require('libraryUtil').checkType

local function midPoint(lower, upper)
	return lower + math.floor((upper - lower) / 2)
end

local function makeKey(prefix, i)
	if prefix then
		return prefix .. tostring(i)
	else
		return i
	end
end

local function findLength(t, prefix, i, lower, upper)
	local key = makeKey(prefix, i)
	if t[key] ~= nil then
		if i + 1 == upper then
			return i
		else
			lower = i
			if upper then
				i = midPoint(lower, upper)
				return findLength(t, prefix, i, lower, upper)
			else
				i = i * 2
				return findLength(t, prefix, i, lower, upper)
			end
		end
	else
		upper = i
		i = midPoint(lower, upper)
		return findLength(t, prefix, i, lower, upper)
	end
end

return function (t, prefix)
	checkType('Array length', 1, t, 'table')
	checkType('Array length', 2, prefix, 'string', true)
	local key = makeKey(prefix, 1)
	if t[key] == nil then
		return 0
	end
	return findLength(t, prefix, 2, 1, nil)
end