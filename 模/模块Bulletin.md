local p = {}

function p._getcolor( color )
	local colorlist = {
		["公告"] = "Pink",
		["人事"] = "LightGreen",
		["投票"] = "LightGreen",
		["编辑"] = "LightGreen",
		["讨论"] = "LightBlue",
		["討論"] = "LightBlue",
		["請求"] = "Orange",
		["请求"] = "Orange",
		["通知"] = "Skyblue",
		["调查"] = "Yellow",
		["調查"] = "Yellow",
		["聚會"] = "PaleGoldenrod",
		["聚会"] = "PaleGoldenrod",
		["獎勵"] = "PaleGoldenrod",
		["奖励"] = "PaleGoldenrod",
		["解任"] = "#99FF4D",
		["離任"] = "#99FF4D",
		["离任"] = "#99FF4D",
		["广告"] = "#EEFFDD",
		["廣告"] = "#EEFFDD"
	}
	if colorlist[color] == nil then
		return "transparent"
	end
	return colorlist[color]
end

function p.item( frame )
	local args = frame:getParent().args
	prefix = args["prefix"]
	if prefix == nil then
		prefix = ""
	end
		
	suffix = args["suffix"]
	if suffix == nil then
		suffix = ""
	end
		
	separator = args["separator"]
	if separator == nil then
		separator = "、"
	end
	
	conjunction = args["conjunction"]
	if conjunction == nil then
		conjunction = "及"
	end
	
	type = args[1]
	if type == nil then
		type = "公告"
	end
	
	local items = {}
	local i = 2
	local value
	while args[i] ~= nil do
		value = mw.text.trim( args[i] )
		if value ~= "" then
			table.insert( items, value )
		end
		i = i + 1
	end
	return '<span class="bulletin-type" style="font-weight: bold; background-color:' .. 
		p._getcolor(type) .. ';">[' .. type .. ']</span> ' ..
		'<span class="bulletin-prefix">' .. prefix .. "</span>" ..
		'<span class="bulletin-item">' .. mw.text.listToText(
			items,
			'</span><span class="bulletin-separator">' .. separator .. '</span><span class="bulletin-item">',
			'</span><span class="bulletin-conjunction">' .. conjunction .. '</span><span class="bulletin-item">'
		) .. '</span>' ..
		'<span class="bulletin-suffix">' .. suffix .. '</span>'
end

return p