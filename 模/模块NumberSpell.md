-- This module converts a number into its written English form.
-- For example, "2" becomes "two", and "79" becomes "seventy-nine".

local getArgs = require('Module:Arguments').getArgs

local p = {}

local max = 100 -- The maximum number that can be parsed.

local ones = {
	[0] = 'zero',
	[1] = 'one',
	[2] = 'two',
	[3] = 'three',
	[4] = 'four',
	[5] = 'five',
	[6] = 'six',
	[7] = 'seven',
	[8] = 'eight',
	[9] = 'nine'
}

local specials = {
	[10] = 'ten',
	[11] = 'eleven',
	[12] = 'twelve',
	[13] = 'thirteen',
	[15] = 'fifteen',
	[18] = 'eighteen',
	[20] = 'twenty',
	[30] = 'thirty',
	[40] = 'forty',
	[50] = 'fifty',
	[60] = 'sixty',
	[70] = 'seventy',
	[80] = 'eighty',
	[90] = 'ninety',
	[100] = 'one hundred'
}

local formatRules = {
	{num = 90, rule = 'ninety-%s'},
	{num = 80, rule = 'eighty-%s'},
	{num = 70, rule = 'seventy-%s'},
	{num = 60, rule = 'sixty-%s'},
	{num = 50, rule = 'fifty-%s'},
	{num = 40, rule = 'forty-%s'},
	{num = 30, rule = 'thirty-%s'},
	{num = 20, rule = 'twenty-%s'},
	{num = 10, rule = '%steen'}
}

function p.main(frame)
	local args = getArgs(frame)
	local num = tonumber(args[1])
	local success, result = pcall(p._main, num)
	if success then
		return result
	else
		return string.format('<strong class="error">Error: %s</strong>', result) -- "result" is the error message.
	end
	return p._main(num)
end

function p._main(num)
	if type(num) ~= 'number' or math.floor(num) ~= num or num < 0 or num > max then
		error('input must be an integer between 0 and ' .. tostring(max), 2)
	end
	-- Check for numbers from 0 to 9.
	local onesVal = ones[num]
	if onesVal then
		return onesVal
	end
	-- Check for special numbers.
	local specialVal = specials[num]
	if specialVal then
		return specialVal
	end
	-- Construct the number from its format rule.
	onesVal = ones[num % 10]
	if not onesVal then
		error('Unexpected error parsing input ' .. tostring(num))
	end
	for i, t in ipairs(formatRules) do
		if num >= t.num then
			return string.format(t.rule, onesVal)
		end
	end
	error('No format rule found for input ' .. tostring(num))
end

return p