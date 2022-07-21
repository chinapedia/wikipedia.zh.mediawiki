local p = {}
function p.pipe( f )
	local out = {}
	for _, arg in ipairs( f:getParent().args ) do
		table.insert( out, arg )
	end

	return  mw.text.trim( table.concat( out, '|' ) )
end

return p