-- This module implements {{Roman}}.

local p = {}

-- This function implements the {{overline}} template.
local function overline(s)
    return mw.ustring.format( '<span style="text-decoration:overline;">%s</span>', s )
end

-- Gets the Roman numerals for a given numeral table. Returns both the string of
-- numerals and the value of the number after it is finished being processed.
local function getLetters(num, t)
    local ret = {}
    for _, v in ipairs(t) do
        local val, letter = unpack(v)
        while num >= val do
            num = num - val
            table.insert(ret, letter)
        end
    end

    return table.concat(ret), num
end

-- The main control flow of the module.
local function _main(args)
    -- Get input and exit displaying nothing if the input is empty.
    if args[1] == nil then return end
    local num = tonumber(args[1])
    if not num or num < 0 or num == math.huge then
    	error('无效数字' .. args[1], 2)
    elseif num == 0 then
        return 'N'
    end

    -- Return a message for numbers too big to be expressed in Roman numerals.
    if num >= 5000000 then
        return args[2] or 'N/A'
    end

    local ret = ''
    -- Find the Roman numerals for the large part of numbers.
    -- 23 April 2016 - tweaked to >= 4000 to accept big Roman 'IV'
    -- The if statement is not strictly necessary, but makes the algorithm 
    -- more efficient for smaller numbers.
    if num >= 4000 then
        local bigRomans = {
            { 1000000, 'M' },
            { 900000, 'CM' }, { 500000, 'D' }, { 400000, 'CD' }, { 100000, 'C' },
            {  90000, 'XC' }, {  50000, 'L' }, {  40000, 'XL' }, {  10000, 'X' },
            {   9000, 'IX' }, {   5000, 'V' }, {   4000, 'IV' },
        }
        local bigLetters
        bigLetters, num = getLetters(num, bigRomans)
        ret = overline(bigLetters)
    end

    -- Find the Roman numerals for numbers less than the big Roman threshold.
    local smallRomans = {
        { 1000, 'M' },
        { 900, 'CM' }, { 500, 'D' }, { 400, 'CD' }, { 100, 'C' },
        {  90, 'XC' }, {  50, 'L' }, {  40, 'XL' }, {  10, 'X' },
        {   9, 'IX' }, {   5, 'V' }, {   4, 'IV' }, {   1, 'I' }
    }
    local smallLetters = getLetters( num, smallRomans )
    ret = ret .. smallLetters

    if args.fraction == 'yes' then
        -- Find the Roman numerals for the fractional parts of numbers.
        -- If num is not a whole number, add half of 1/1728 (the smallest unit) to equate to rounding.
        -- Ensure we're not less than the smallest unit or larger than 1 - smallest unit
        -- to avoid getting two "half" symbols or no symbols at all
        num = num - math.floor(num)
        if num ~= 0 then
            num = math.max(1.1/1728, math.min(1727.1/1728, num + 1/3456))
        end
        local fractionalRomans = {
            { 1/2, 'S' }, { 5/12, "''':'''•''':'''" }, { 1/3, "'''::'''" },
            { 1/4, "''':'''•" }, { 1/6, "''':'''" }, { 1/12, '•' },
            { 1/24, 'Є' }, { 1/36, 'ƧƧ' }, { 1/48, 'Ɔ' }, { 1/72, 'Ƨ' }, { 1/144, 'ƻ' },
            { 1/288, '℈' }, { 1/1728, '»' },
        }
        local fractionalLetters = getLetters(num, fractionalRomans)
        
        ret = ret .. fractionalLetters
    end

    return ret
end

function p.getRomam(numinput, failed, fraction)
	--for [[模块:PeriodicTable|模块:PeriodicTable]]
	local number = tonumber(numinput or 0);
	if number < 0 or numinput == nil then return failed or '' end
	local nargs = {[1] = number}
	if failed ~= nil then nargs[2] = failed end
	if fraction ~= nil then nargs.fraction = fraction end
	return _main(nargs);
end

function p.main(frame)
    -- If called via #invoke, use the args passed into the invoking
    -- template, or the args passed to #invoke if any exist. Otherwise
    -- assume args are being passed directly in from the debug console
    -- or from another Lua module.
    local origArgs
    if frame == mw.getCurrentFrame() then
        origArgs = frame:getParent().args
        for k, v in pairs(frame.args) do
            origArgs = frame.args
            break
        end
    else
        origArgs = frame
    end
    -- Trim whitespace and remove blank arguments.
    local args = {}
    for k, v in pairs(origArgs) do
        if type( v ) == 'string' then
            v = mw.text.trim(v)
        end
        if v ~= '' then
            args[k] = v
        end
    end
    
    -- exit if not given anything
    if args == nil or args == {} then return end
    -- Given mathematical expression, simplify to a number
    if type(args[1]) == 'string' then
        args[1] = mw.ext.ParserFunctions.expr(args[1])
    end
    return _main(args)
end

return p