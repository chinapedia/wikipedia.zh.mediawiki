local p = {}

function p.row(frame)
	local somelist = frame.args[1]
	local div = frame.args['div']
	local result, para1, para2, para3, para4, para1_1, para1_empty, sep
	result = ''
	para1 = ''
	para2 = ''
	para3 = ''
	para4 = ''
	para1_1 = ''
	para1_empty = false
	sep = ''
	for k1, v1 in ipairs(mw.text.split(somelist, '+')) do
		for k2, v2 in ipairs(mw.text.split(v1 .. '\\', '\\')) do
			if k2 > 4 then break
				elseif k2 == 1 then
					if para1 == '' then
						para1_1 = v2
					else sep = ' '
					end
					if v2 == nil or v2 == '' then
						para1 = para1_1
						para1_empty = true
					else
						para1 = v2
						para1_empty = false
					end
				elseif k2 == 2 then
					if v2 == nil or v2 == '' then
						para2 = nil
					else
						para2 = v2
					end
				elseif k2 == 3 then
					if v2 == nil or v2 == '' then
						para3 = nil
					else
						para3 = v2
					end
				elseif k2 == 4 then
					if v2 == nil or v2 == '' then
						para4 = nil
					else
						para4 = v2
					end
				if para1_empty == true and para2 == nil then
				else result = result .. sep .. frame:expandTemplate{ title = 'Rail-interchange', args = { para1, para2, para3, para4 } }
				end
			end
		end
	end
	if div == 'yes' or div == 'y' then result = '<div style="display: table-cell; vertical-align: middle; padding-left: 3px; white-space: nowrap;">' .. result .. '</div>'
	end
	return result
end

function p.doublerow(frame)
	local somelist = frame.args[1]
	local result, para1, para2, para3, para4, para1_1, para1_empty, sep
	result = ''
	para1 = ''
	para2 = ''
	para3 = ''
	para4 = ''
	para1_1 = ''
	para1_empty = false
	sep = ''
	for k1, v1 in ipairs(mw.text.split(somelist, '+')) do
		for k2, v2 in ipairs(mw.text.split(v1 .. '\\', '\\')) do
			if k2 > 4 then break
				elseif k2 == 1 then
					if para1 == '' then
						para1 = v2
						para1_1 = v2
					else
						if v2 == nil or v2 == '' then
							para1 = para1_1
							para1_empty = true
						else
							para1 = v2
							para1_empty = false
						end
						if (k1 % 2 == 1) then sep = '</div><div style="display: table-cell; vertical-align: middle; padding-left: 3px; white-space: nowrap;">'
						else sep = '<br/>'
						end
					end
				elseif k2 == 2 then
					if v2 == nil or v2 == '' then
						para2 = nil
					else
						para2 = v2
					end
				elseif k2 == 3 then
					if v2 == nil or v2 == '' then
						para3 = nil
					else
						para3 = v2
					end
				elseif k2 == 4 then
					if v2 == nil or v2 == '' then
						para4 = nil
					else
						para4 = v2
					end
				if para1_empty == true and para2 == nil then result = result .. sep
				else result = result .. sep .. frame:expandTemplate{ title = 'Rail-interchange', args = { para1, para2, para3, para4 } }
				end
			end
		end
	end
	result = '<div style="display: table-cell; vertical-align: middle; padding-left: 3px; white-space: nowrap;">' .. result .. '</div>'
	return result
end
 
return p