local z = {}
local error = require( 'Module:Error' )

local function makeText( frame, v )
	local text = v.text
	if not v.preprocessed then
		text = frame:preprocess( text )
	end
	return mw.text.trim( text ) .. '\n'
end

local function makeItem( frame, v )
	local text = '* '
	if v.original then
		text = text .. '原文：' .. v.original .. '；'
	end
	return text .. '-{D|' .. v.rule .. '}-当前显示为：-{|' .. v.rule .. '}-\n'
end

function z.main( frame )
	local name = frame.args[1]
	if not name or name == '' then
		return ''
	end
	local data = require( 'Module:CGroup/' .. name )
	if type( data ) ~= 'table' or not data.name or data.name == '' then
		return error.error{ '指定模块“' .. name .. '”不是有效的转换组' }
	end
	if data.name ~= name then
		return frame:expandTemplate{ title = 'Template:CGroup redirect', args = { 'Module:CGroup/' .. data.name } }
	end
	local pieces = { '<strong>以下是[[Wikipedia:字詞轉換處理/公共轉換組|公共转换组]]“' .. data.description .. '”。</strong>\n\n' }
	for i, v in ipairs( data.content ) do
		if v.type == 'text' then
			table.insert( pieces, makeText( frame, v ) )
		elseif v.type == 'item' then
			table.insert( pieces, makeItem( frame, v ) )
		end
	end
	table.insert( pieces, '[[Category:公共轉換組模板|' .. name .. ']]' )
	return table.concat( pieces )
end

function z.dialog( frame )
	local name = frame.args[1]
	if not name or name == '' then
		return ''
	end
	local data = require( 'Module:CGroup/' .. name )
	local pieces = { '<div class="mw-collapsible mw-collapsed"><span class="plainlinks" style="float: right;">[[',
		tostring( mw.uri.fullUrl( 'Module:CGroup/' .. name, { action = 'edit' } ) ), ' 编辑]]</span>\n',
		'; 本文使用[[Wikipedia:字詞轉換處理/公共轉換組|公共转换组]]“' .. data.description .. '”。\n',
		'<div class="mw-collapsible-content">\n' }
	for i, v in ipairs( data.content ) do
		if v.type == 'item' then
			table.insert( pieces, makeItem( frame, v ) )
		end
	end
	table.insert( pieces, '</div></div>' )
	return table.concat( pieces )
end

function z.json( frame )
	local name = frame.args[1]
	if not name or name == '' then
		return 'null'
	end
	local data = require( 'Module:CGroup/' .. name )
	local json = require( 'Module:MicroJSON' )
	return json.encode_object( data, {
		name = '',
		description = '',
		content = {
			{ type = '', [true] = '' },
		},
	} )
end

return z