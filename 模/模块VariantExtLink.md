local z = {}
local lc = require( 'Module:WikitextLC' )

local function gatebig5_c( uri )
	uri:parse( '//' .. uri.path:sub( 12 ) )
end

local transcoders = {
	['big5%.xinhuanet%.com'] = gatebig5_c,
}

local function gatebig5( host, port )
	return function( uri )
		local big5uri = uri:clone()
		local prefix = '/gate/big5/' .. uri.host
		if uri.port then
			prefix = path .. ':' .. uri.port
		end
		big5uri.path = prefix .. uri.path
		big5uri.host = host
		big5uri.port = port
		return {
			['zh-hans'] = tostring( uri ),
			['zh-hant'] = tostring( big5uri ),
		}
	end
end

local websites = {
	['www%.xinhuanet%.com'] = gatebig5( 'big5.xinhuanet.com' ),
}

local function clean( url )
	uri = mw.uri.new( url )
	for pattern, cleaner in pairs( transcoders ) do
		if uri.host:match( '^' .. pattern .. '$' ) then
			cleaner( uri )
			break
		end
	end
	return uri
end

local function extend( uri )
	for pattern, extender in pairs( transcoders ) do
		if uri.host:match( '^' .. pattern .. '$' ) then
			return extender( uri )
		end
	end
	return tostring( uri )
end

return z