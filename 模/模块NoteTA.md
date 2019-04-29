local z = {}
local WikitextLC = require( 'Module:WikitextLC' )

function Tcode( args )
	if args.T == nil or args.T == '' then
		return ''
	end
	local div = mw.html.create( 'div' )
		:attr( 'class', 'noteTA-title' )
		:attr( 'data-noteta-code', args.T )
		:wikitext( WikitextLC.title( args.T ) )
	if args.dt ~= nil and args.dt ~= '' then
		div:attr( 'data-noteta-desc', args.dt )
	end
	return tostring( div )
end

function group( name, frame )
	if name == nil or name == '' then
		return ''
	end
	local moduleTitle = mw.title.makeTitle( 'Module', 'CGroup/' .. name )
	if moduleTitle and moduleTitle.exists then
		local data = require( 'Module:CGroup/' .. name )
		local pieces = {}
		if data.content then
			for i, v in ipairs( data.content ) do
				if v.type == 'item' and v.rule then
					table.insert( pieces, '-{H|' .. v.rule .. '}-' )
				end
			end
			return tostring( mw.html.create( 'div' )
				:attr( 'data-noteta-group-source', 'module' )
				:attr( 'data-noteta-group', data.name or name )
				:wikitext( table.concat( pieces ) ) )
		end
	end
	local templateTitle = mw.title.makeTitle( 'Template', 'CGroup/' .. name )
	if templateTitle and templateTitle.exists then
		return frame:expandTemplate{ title = templateTitle }
	end
	return tostring( mw.html.create( 'div' )
			-- :attr( 'id', 'noteTA-group-' .. mw.uri.anchorEncode( name ) )
			:attr( 'data-noteta-group-source', 'none' )
			:attr( 'data-noteta-group', name ) )
end

function Gcode( args, frame )
	local code = {}
	for i = 1, 30 do
		table.insert( code, group( args['G' .. i], frame ) )
	end
	code = table.concat( code )
	if code ~= '' then
		code = tostring( mw.html.create( 'div' )
				:attr( 'class', 'noteTA-group' )
				:wikitext( code ) )
		if args.G31 ~= nil then
			code = code .. '[[Category:NoteTA模板参数使用数量超过限制的页面|G]]'
		end
	end
	return code
end

function local_( i, code, desc )
	if code == nil or code == '' then
		return ''
	end
	local div = mw.html.create( 'div' )
		-- :attr( 'id', 'noteTA-local-' .. i )
		:attr( 'data-noteta-code', code )
		:wikitext( WikitextLC.hidden( code ) )
	if desc ~= nil and desc ~= '' then
		div:attr( 'data-noteta-desc', desc )
	end
	return tostring( div )
end

function Lcode( args )
	local code = {}
	for i = 1, 30 do
		table.insert( code, local_( i, args[i], args['d' .. i] ) )
	end
	code = table.concat( code )
	if code ~= '' then
		code = tostring( mw.html.create( 'div' )
				:attr( 'class', 'noteTA-local' )
				:wikitext( code ) )
		if args[31] ~= nil then
			code = code .. '[[Category:NoteTA模板参数使用数量超过限制的页面|L]]'
		end
	end
	return code
end

function z.main( frame )
	local args
	if frame == mw.getCurrentFrame() then
		-- Being called from {{noteTA}}
		args = frame:getParent().args
	else
		-- Being called from another module
		args = frame
		frame = mw.getCurrentFrame()
	end
	local Tc = Tcode( args )
	local Gc = Gcode( args, frame )
	local Lc = Lcode( args )
	local code = Tc .. Gc .. Lc
	if code ~= '' then
		local hash = require( 'Module:Crc32lua' ).crc32( mw.dumpObject( args ) )
		code = frame:extensionTag{
			name = 'indicator',
			content = '[[File:Zh_conversion_icon_m.svg|35px]]',
			args = { name = string.format( 'noteTA-%x', hash ) },
		} .. tostring( mw.html.create( 'div' )
				:attr( 'id', string.format( 'noteTA-%x', hash ) )
				:attr( 'class', 'noteTA' )
				:wikitext( code ) )
		if mw.title.getCurrentTitle():inNamespace( 'Template' ) then
			code = code .. '[[Category:放置于模板的noteTA|Category:放置于模板的noteTA]]'
		end
	end
	return code
end

return z