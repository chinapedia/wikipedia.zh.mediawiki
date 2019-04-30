local list = { 

	{'特色级内容', '#6699ff'},
	{'甲级内容', '#66ffff'}, 
	{'优良级内容', '#66ff66'}, 
	{'乙级内容', '#b2ff66'},
	{'丙级内容', '#ffff66'},
	{'初级内容', '#ffaa66'}, 
	{'小作品级内容', '#ff6666'},
	{'列表级内容', '#aa88ff'},
	{'未评级内容', '#e2e2e2'},

}

local getArgs = require('Module:Arguments').getArgs
local p = {}

local function core( this, total, index )
	local td = mw.html.create( 'td' )
	local lang = mw.getLanguage( 'zh' )
	local percent = tostring( math.floor( this / total * 10000) / 100 ) .. '%'
	
	td
		:css( 'background', list[index][2] )
		:css( 'width', percent )
		:attr( 'title', list[index][1] .. '：' .. this .. '（' .. percent .. '）' )
			
	return tostring( td )
end

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end
 
function p._main(args)
	
	local temp = ''
	local sum = 0
	
	args[9] = args[9] or 100

	for i = 1, 6 do
		if not ( args[i] == nil or args[i] == '0' ) then
			temp = temp .. core( args[i], args[9], i )
			sum = sum + args[i]
		end
	end

	if args.list ~= 'start' then
		for i = 7, 8 do
			if not ( args[i] == nil or args[i] == '0' ) then
				temp = temp .. core( args[i], args[9], i )
				sum = sum + args[i]
			end
		end
	else
		for i = 8, 7, -1 do
			if not ( args[i] == nil or args[i] == '0' ) then
				temp = temp .. core( args[i], args[9], i )
				sum = sum + args[i]
			end
		end	
	end

	if sum < tonumber( args[9] ) then
		temp = temp .. core( args[9] - sum, args[9], 9 )
	end

	local tr = mw.html.create( 'tr' )
	tr
		:wikitext( temp )
		
	local tab = mw.html.create( 'table' )
	tab 
		:css( 'border', '1px solid grey')
		:css( 'height', '10px' )
		:css( 'width', '100%' )
		:attr( 'cellspacing', '1' )
		:wikitext( tostring( tr ) )
		
	return tostring( tab )
end
 
return p