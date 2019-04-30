-- This module converts support characters from half-width to full-width, and vice versa.
-- See [[Halfwidth_and_fullwidth_forms|Halfwidth and fullwidth forms]] for an explanation of half- and full-width characters.

-- @todo FIXME: Needs more characters adding, needs support for diacritic marks.

local data = mw.loadData( 'Module:Convert character width/data' )

local p = {}

-- Converts one half-width character to one full-width character.
local function getFull( s )
    return data[ s ] or s
end

-- Converts one full-width character to one half-width character.
local function getHalf( s )
    for half, full in pairs( data ) do
        if s == full then
            return half
        end
    end
    return s
end

-- Converts multiple half-width characters to full-width characters.
function p.full( frame )
    local s = type( frame ) == 'table' and frame.args and frame.args[ 1 ] or frame
    s = type( s ) == 'number' and tostring( s ) or s
    if type( s ) ~= 'string' then return end
    return ( mw.ustring.gsub( s, '.', getFull ) )
end

-- Converts multiple full-width characters to half-width characters.
function p.half( frame )
    local s = type( frame ) == 'table' and frame.args and frame.args[ 1 ] or frame
    s = type( s ) == 'number' and tostring( s ) or s
    if type( s ) ~= 'string' then return end
    return ( mw.ustring.gsub( s, '.', getHalf ) )
end

return p