local getArgs = require('Module:Arguments').getArgs

local p = {}

function p._encode(sortkey)
	-- Protect against sortkey nesting.
	-- Example: {{sort|{{dts|2013|07|07}}|{{dts|1990|12|01}}}}
	if string.find(sortkey, "sortkey") or string.find(sortkey, "data-sort-value") then
		return "";
	end
    return mw.text.encode(sortkey)
end

function p.encode(frame)
	local args = getArgs(frame);
	return p._encode(args[1] or "")
end

local function valid_number(num)
	-- Return true if num is a valid number.
	-- In Scribunto (different from some standard Lua), when expressed as a string,
	-- overflow or other problems are indicated with text like "inf" or "nan"
	-- which are regarded as invalid here (each contains "n").
	if type(num) == 'number' and tostring(num):find('n', 1, true) == nil then
		return true
	end
end

function p._sortKeyForNumber(value)
	if not valid_number(value) then
		if value < 0 then
			sortkey = '1000000000000000000'
		else
			sortkey = '9000000000000000000'
		end
	elseif value == 0 then
		sortkey = '5000000000000000000'
	else
		local mag = math.floor(math.log10(math.abs(value)) + 1e-14)
		local prefix
		if value > 0 then
			prefix = 7000 + mag
		else
			prefix = 2999 - mag
			value = value + 10^(mag+1)
		end
		sortkey = string.format('%d', prefix) .. string.format('%015.0f', math.floor(value * 10^(math.min(28,14-mag))))
	end
	return sortkey;
end

function p.sortKeyForNumber(frame)
	local args = getArgs(frame);
	return p._sortKeyForNumber(args[1] or "")
end

return p