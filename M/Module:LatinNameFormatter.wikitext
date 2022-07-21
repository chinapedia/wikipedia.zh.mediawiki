local p = {}
local terms = {
	['subsp.'] = true,
	['ssp.'] = true,
	['var.'] = true,
	['subvar.'] = true,
	['f.'] = true,
	['subf.'] = true,
}

local function unformat( name )
	name = mw.ustring.gsub( name, "'", '' )
	name = mw.ustring.gsub( name, '<.->', '' )
	return name
end

local function split( name )
	local words = {}
	local extra = {}
	for piece in mw.ustring.gmatch( name, '%S+') do
		if #extra > 0 or (
			#words > 0 and
			not mw.ustring.match( mw.ustring.sub( piece, 1, 1 ), '[a-z]' )
		) then
			table.insert( extra, piece )
		else
			table.insert( words, piece )
		end
	end
	return words, extra
end

local function joinWords( words )
	modifiedWords = {}
	for i = 1, #words do
		local word = words[i]
		if not terms[word] then
			word = '<i>' .. word .. '</i>'
		end
		table.insert( modifiedWords, word )
	end
	return table.concat( modifiedWords, ' ' )
end

local function format( name )
	local words, extra = split( name )
	name = joinWords( words )
	if #extra > 0 then
		name = name .. ' ' .. table.concat( extra, ' ' )
	end
	return name
end

function p.format( frame )
	return format( unformat( frame.args.name ) )
end

return p