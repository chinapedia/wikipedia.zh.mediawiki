--[=[
Functions are not "local", so other modules can require this module and call them directly.
We return an object with 3 small stub functions to call the real ones so that the functions
can be called from templates also.

Only [[dotted_decimal|dotted decimal]] notation for IPv4 supported. Does not support
dotted hexadecimal, dotted octal, or single-number formats (see [[IPv4#Address_representations|IPv4#Address_representations]]).

Unit tests at Module:IPAddress/tests
]=]

function _isIpV6( s )
    local dcolon, groups
    if type( s ) ~= "string"
        or s:len() == 0
        or s:find( "[^:%x]" ) -- only colon and hex digits are legal chars
        or s:find( "^:[^:]" ) -- can begin or end with :: but not with single :
        or s:find( "[^:]:$" )
        or s:find( ":::" )
    then
        return false
    end 
    s, dcolon = s:gsub( "::", ":" )
    if dcolon > 1 then return false end -- at most one ::
    s = s:gsub( "^:?", ":" ) -- prepend : if needed, upper
    s, groups = s:gsub( ":%x%x?%x?%x?", "" ) -- remove valid groups, and count them
    return ( ( dcolon == 1 and groups < 8 ) or ( dcolon == 0 and groups == 8 ) )
        and ( s:len() == 0 or ( dcolon == 1 and s == ":" ) ) -- might be one dangling : if original ended with ::
end

function _isIpV4( s )
    local function legal( n ) return ( tonumber( n ) or 256 ) < 256  and not n:match("^0%d") end-- in lua 0 is true!
    
    if type( s ) ~= "string" then return false end
    local p1, p2, p3, p4 = s:match( "^(%d+)%.(%d+)%.(%d+)%.(%d+)$" ) 
    return legal( p1 ) and legal( p2 ) and legal( p3 ) and legal( p4 )
end

function _isIp( s )
    return _isIpV4( s ) and "4" or _isIpV6( s ) and "6"
end

local p = {}

function p.isIpV6(frame) return _isIpV6( frame.args[ 1 ] ) and "1" or "0" end
function p.isIpV4(frame) return _isIpV4( frame.args[ 1 ] ) and "1" or "0" end
function p.isIp(frame) return _isIp( frame.args[ 1 ] ) or "" end

return p