local p = {}
function p.board(frame)
	local args = require('Module:Arguments').getArgs(frame)
	local align = string.gsub(args[1] or '','\n','')
	if align == '' then
		align = 'tright'
	end
	local header = string.gsub(args[2] or '','\n','')
	local footer = string.gsub(args[93] or '','\n','')

	local size
	local width
	local height

	if args.size ~= nil then
		size = args.size
		width = size * 9
		height = size * 12
	elseif args.width ~= nil then
		width = args.width
		size = width / 9
		height = size * 12
	elseif args.height ~= nil then
		height = args.height
		size = height / 12
		width = size * 9
	else
		size = 25
		width = 225
		height = 300
	end

	local ss = ''
	ss = ss .. '<div class="' .. align .. '" style="clear:right;">'
	ss = ss .. '<div style="width:' .. width .. 'px"><center>' .. header .. '</center></div><div style="position:relative;width:' .. width .. 'px;height:' .. height .. 'px;">'
	ss = ss .. '<div style="position:absolute;top:0px;left:0px;width:' .. width .. 'px;">[[File:Xiangqi_board.svg|' .. width .. 'px]]</div>'
	for i = 0,9 do
		for j = 0,8 do
			local s = string.gsub(args[i * 9 + j + 3] or '','\n','')
			s = string.gsub(s,' ','')
			s = string.gsub(s,'　','')
			s = string.gsub(s,'_','')
			-- 繁簡轉換:
            -- -{D|zh-hans:车;zh-hant:車;}-
            -- -{D|zh-hans:伡;zh-hant:俥;}-
            -- -{D|zh-hans:马;zh-hant:馬;}-
            -- -{D|zh-hans:㐷;zh-hant:傌;}-
            -- -{D|zh-hans:帅;zh-hant:帥;}-
            -- -{D|zh-hans:将;zh-hant:將;}-
			if s == '车' or s == '車' then
				s = 'rd'
			elseif s == '伡' or s == '俥' then
				s = 'rl'
			elseif s == '马' or s == '馬' then
				s = 'hd'
			elseif s == '㐷' or s == '傌' then
				s = 'hl'
			elseif s == '相' then
				s = 'el'
			elseif s == '象' then
				s = 'ed'
			elseif s == '仕' then
				s = 'al'
			elseif s == '士' then
				s = 'ad'
			elseif s == '炮' then
				s = 'cl'
			elseif s == '砲' then
				s = 'cd'
			elseif s == '兵' then
				s = 'sl'
			elseif s == '卒' then
				s = 'sd'
			elseif s == '帅' or s == '帥' then
				s = 'gl'
			elseif s == '将' or s == '將' then
				s = 'gd'
			end
			
			if s ~= '' then
				ss = ss .. '<div style="position:absolute;top:' .. ((i + 1) * size) .. 'px;left:' .. (j * size) .. 'px;width:' .. size .. 'px;">[[File:Xiangqi_'_.._s_.._'1.svg|' .. size .. 'px]]</div>'
			end
		end
	end
	ss = ss .. '</div><div style="width:' .. width .. 'px">' .. footer .. '</div></div>'
	return ss
end

return p