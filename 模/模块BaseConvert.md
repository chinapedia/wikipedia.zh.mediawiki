local p = {}

local digits = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ'

function normalizeFullWidthChars(s)
    return mw.ustring.gsub(s, '[！-～]', function(s) 
        return mw.ustring.char(mw.ustring.codepoint(s, 1) - 0xFEE0) 
    end)    
end

function _convert(n, base, from, precision, width, default, prefix, suffix)
    n = '' .. n   -- convert to a string
    
    -- strip off any leading '0x' (unless x is a valid digit in the input base)
    from = tonumber(from)
    if not from or from < 34 then
        local c
        n, c = n:gsub('^(-?)0[Xx]', '%1')
        if c > 0 and not from then from = 16 end
    end

    -- check for a negative sign. Do this while the input is still in string form,
    -- because tonumber doesn't support negative numbers in non-10 bases.
    local sign = ''
    local c
    n, c = n:gsub('^-', '')
    if c > 0 then sign = '-' end
    
    -- replace any full-width Unicode characters in the string with their ASCII equivalents
    n = normalizeFullWidthChars(n)
    
    -- handle scientific notation with whitespace around the 'e' e.g. '5 e7'
    n = n:gsub('%s*[eE]%s*', 'e')
    
    from = from or 10
    local num = tonumber(n, from)
    base = tonumber(base)
    precision = tonumber(precision)
    width = tonumber(width)
    
    if not num or not base then return default or n end
    
    local i, f = math.modf(num)

    local t = {}
    repeat
        local d = (i % base) + 1
        i = math.floor(i / base)
        table.insert(t, 1, digits:sub(d, d))
    until i == 0
    while #t < (width or 0) do
        table.insert(t, 1, '0') 
    end
    local intPart = table.concat(t, '')
    
    -- compute the fractional part
    local tf = {}
    while f > 0 and #tf < (precision or 10) do
        f = f * base
        i, f = math.modf(f)
        table.insert(tf, digits:sub(i + 1, i + 1))
    end
    
    -- add trailing zeros if needed
    if precision and #tf < precision then
        for i = 1, precision - #tf do
            table.insert(tf, '0') 
        end
    end

    fracPart = table.concat(tf, '')
    
    -- remove trailing zeros if not needed
    if not precision then
        fracPart = fracPart:gsub('0*$', '')
    end
    
    -- add the radix point if needed
    if #fracPart > 0 then
        fracPart = '.' .. fracPart
    end
    
    return (prefix or '') .. sign .. intPart .. fracPart .. (suffix or '')
end

function p.convert(frame)
    -- Allow for invocation via #invoke or directly from another module
    local args
    if frame == mw.getCurrentFrame() then
        args = frame.args
    else
        args = frame
    end
    
    local n = args.n
    local base = args.base
    local from = args.from
    local precision = args.precision
    local width = args.width
    local default = args.default
    local prefix = args.prefix
    local suffix = args.suffix
    return _convert(n, base, from, precision, width, default, prefix, suffix)
end

return p