-- This module implements {{Armenian}}. It converts numbers to old Armenian
-- numerals, for numbers from 1-29999.

local p = {}

function p.main( frame )
    -- If we are being called from #invoke, then the number is the first positional
    -- argument. If not, it is the frame parameter.
    local num
    if frame == mw.getCurrentFrame() then
        num = frame:getParent().args[ 1 ]
        local frameArgsNum = frame.args[ 1 ]
        if frameArgsNum then
            num = frameArgsNum
        end
    else
        num = frame
    end

    -- Convert the input to an integer if possible.
    if type( num ) ~= 'number' then
        num = tonumber( num )
    end
    if not num then return '' end

    num = math.floor( num )
    -- Exit if the number is not expressible in Armenian numerals.
    -- FIXME: Check if Armenian numerals can really be made 10,000x bigger through
    -- overlining them as it says in our article. (That claim is unsourced.) If they
    -- can, there is code at [[Module:Roman|Module:Roman]] that can be stolen from to make it work.
    if num < 1 or num > 29999 then return '' end
    
    local numerals = {
        { 20000, "Ֆ" }, { 10000, "Օ" },
        { 9000, "Ք" },  { 8000, "Փ" },  { 7000, "Ւ" },  { 6000, "Ց" },  { 5000, "Ր" },  { 4000, "Տ" },  { 3000, "Վ" },  { 2000, "Ս" },  { 1000, "Ռ" },
        { 900, "Ջ" },   { 800, "Պ" },   { 700, "Չ" },   { 600, "Ո" },   { 500, "Շ" },   { 400, "Ն" },   { 300, "Յ" },   { 200, "Մ" },   { 100, "Ճ" },
        { 90, "Ղ" },    { 80, "Ձ" },    { 70, "Հ" },    { 60, "Կ" },    { 50, "Ծ" },    { 40, "Խ" },    { 30, "Լ" },    { 20, "Ի" },    { 10, "Ժ" },
        { 9, "Թ" },     { 8, "Ը" },     { 7, "Է" },     { 6, "Զ" },     { 5, "Ե" },     { 4, "Դ" },     { 3, "Գ" },     { 2, "Բ" },     { 1, "Ա" }
    }
    
	local ret = {}
    for _, v in ipairs( numerals ) do
        local val, letter = unpack( v )
        while num >= val do
            num = num - val
            table.insert( ret, letter )
        end
    end
    return table.concat( ret )
end

return p