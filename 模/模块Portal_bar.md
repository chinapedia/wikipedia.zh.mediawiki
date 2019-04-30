-- This module implements {{portal bar}}.

require('Module:No globals')

local p = {}

local getImageName = require( 'Module:Portal' ).image
local yesno = require( 'Module:Yesno' )

-- Builds the portal bar used by {{portal bar}}.
function p._main( portals, args )
	if #portals < 1 then return '' end -- Don't display a blank navbox if no portals were specified.
	
	local nav = mw.html.create( 'div' )
		:addClass( 'noprint metadata' )
		:attr( 'role', 'navigation' )
		:attr( 'aria-label' , 'Portals' )
		:css( 'font-weight', 'bold' )
	if yesno( args.border ) == false then
		nav
			:css( 'padding', '0.3em 1.7em 0.1em' )
			:css( 'font-size', '88%' )
			:css( 'text-align', 'center' )
	else
		nav
			:addClass( 'navbox' )
			:css( 'padding', '0.4em 0' )
            :css( 'box-sizing', 'border-box' )
	end
	
	local list = mw.html.create( 'ul' )
		:css( 'margin', '0.1em 0 0' )
	for _, portal in ipairs( portals ) do
		list
			:tag( 'li' )
				:css( 'display', 'inline' )
				:tag( 'span' ) -- Inline-block on inner span for IE6-7 compatibility.
					:css( 'display', 'inline-block' )
					:css( 'white-space', 'nowrap' )
					:tag( 'span' )
						:css( 'margin', '0 0.5em' )
						:wikitext( string.format( '[[File:%s|24x21px]]', getImageName{ portal } ) )
						:done()
					:wikitext( string.format( '[[Portal:%s|%s主题]]', portal, portal ) )
	end
	
	nav
		:node( list )
	
	return tostring( nav )
end

-- Processes external arguments and sends them to the other functions.
function p.main( frame )
	-- If called via #invoke, use the args passed into the invoking
	-- template, or the args passed to #invoke if any exist. Otherwise
	-- assume args are being passed directly in from the debug console
	-- or from another Lua module.
	local origArgs
	if type( frame.getParent ) == 'function' then
		origArgs = frame:getParent().args
		for k, v in pairs( frame.args ) do
			origArgs = frame.args
			break
		end
	else
		origArgs = frame
	end
	-- Process the args to make an array of portal names that can be used with ipairs. We need to use ipairs because we want to list
	-- all the portals in the order they were passed to the template, but we also want to be able to deal with positional arguments
	-- passed explicitly, for example {{portal|2=Politics}}. The behaviour of ipairs is undefined if nil values are present, so we
	-- need to make sure they are all removed.
	local portals, args = {}, {}
	for k, v in pairs( origArgs ) do
		if type( k ) == 'number' and type( v ) == 'string' then -- Make sure we have no non-string portal names.
			if mw.ustring.find( v, '%S' ) then -- Remove blank values.
				table.insert( portals, k )
			end
		elseif type( k ) ~= 'number' then -- Separate named arguments from portals.
			if type( v ) == 'string' then
				v = mw.text.trim( v )
			end
			args[ k ] = v
		end
	end
	table.sort( portals )
	for i, v in ipairs( portals ) do
		portals[ i ] = mw.text.trim( origArgs[ v ] ) -- Swap keys with values, trimming whitespace.
	end
	return p._main( portals, args )
end

return p