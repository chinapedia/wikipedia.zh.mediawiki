local p = {}
function p.board(frame)
	local args = frame.args
	if args[1] == nil then
 		args = frame:getParent().args
	end
	local align = string.gsub(args[1] or '','\n','')
	if align == '' then
		align = 'tright'
	end
	local header = string.gsub(args[2] or '','\n','')
	local footer = string.gsub(args[84] or '','\n','')

	local ss = ''
	ss = ss .. '<div class="' .. align .. '" style="clear:right;width:250px;"><center>'
	ss = ss .. header .. '</center><div style="position:relative;width:250px;height:250px;">'
	ss = ss .. '<div style="position:absolute;top:0px;left:0px;width:250px;height:250px;">[[File:Shogi_board.svg|250x250px]]</div>'	
	for i = 0,8 do
		for j = 0,8 do
			local s = string.gsub(args[i * 9 + j + 3] or '','\n','')
			s = string.gsub(s,' ','')
			s = string.gsub(s,'_','')
			if s ~= '' then
				ss = ss .. '<div style="position:absolute;top:' .. ((i + 0.5) * 25) .. 'px;left:' .. ((j + 0.5) * 25) .. 'px;width:25px;height:25px;">[[File:Shogi_'_.._s_.._'1.svg|25x25px]]</div>'
			end
		end
	end
	ss = ss .. '</div>' .. footer .. '</div>'
	return ss
end

return p