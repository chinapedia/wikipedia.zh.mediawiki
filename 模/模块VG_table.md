require('Module:No globals')
local getArgs = require('Module:Arguments').getArgs
local yesno = require('Module:Yesno')

local p = {}
 
function p.main(frame)
	local args = getArgs(frame, { frameOnly = true } )
	-- Main module code goes here.
	local ret

	local function col( col3, col5 )
		return ( args['column-3'] and col3 or col5 )
	end

	ret = '{| class="wikitable plainrowheaders" width="100%" align="center" style="font-size: ' .. col( '100%', 'small' ) .. ';"' .. '\n'
	ret = ret .. '|- style="text-align: center;"' .. '\n'
	ret = ret .. '! scope="col" width="' .. col( '31%', '17.5%' ) .. '" align="center" rowspan="2" | 作品' .. '\n'
	ret = ret .. '! colspan="' .. col( '3', '5' ) .. '" | 首次发行日期' .. '\n'
	ret = ret .. '|- style="border-bottom: solid #ccf 3px;"' .. '\n'
	
	for i = 1, col( 3, 5 ) do
		ret = ret .. '! scope="col" style="padding: 0 1% 0 1%; text-align: center; width: ' .. col( '23%', '16.5%' ) .. '; font-weight: bold; background-color: transparent;" |' .. ( args['region' .. i] ).. '\n'
	end

	if args.body then
		ret = ret .. args.body .. '\n'
	end
	ret = ret .. '|}'
	
	return ret
end

function p.item(frame)
	local args = getArgs(frame, {
		frameOnly = true,
		valueFunc = function (key, value)
			if key == 'notes' and string.sub( value, -1, -1 ) == '\n' then
				value = string.sub( value, 1, -2 )
			end
			return value
		end,
	} )
	
	local ret
	local col = args['column-3'] and 3 or 5
	
	ret = '|- bgcolor="#F2F2F2" align="center"' .. '\n'
	ret = ret .. '! scope="row" style="text-align: center;" | ' .. args.title .. '\n'
	for i = 1, col do
		ret = ret .. '|' .. args['release' .. i] .. '\n'
	end
	if args.notes then
		ret = ret .. '|-' .. '\n'
		ret = ret .. '| scope="row" colspan="' .. ( col + 1 ) .. '" style="border: none; vertical-align: top; background-color: transparent; text-align: left;" | <b>注解：</b>' .. '\n'
		ret = ret .. args.notes
	end
	
	return ret
end

return p