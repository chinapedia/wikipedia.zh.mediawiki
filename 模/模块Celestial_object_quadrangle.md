-- This module implements/replaces
-- [[Template:Lunar_quadrangle|Template:Lunar quadrangle]]
-- [[Template:Mars_quadrangle|Template:Mars quadrangle]]
-- [[Template:Mercury_quadrangle_category|Template:Mercury quadrangle category]]
-- [[Template:Venus_quadrangle|Template:Venus quadrangle]]
local p = {}
-- 月球區
local function moonquad(lat, lon)
	local function LQ(n)
		if n < 10 then 
			return 'LQ0' .. n
		else 
			return 'LQ' .. n
		end
	end
	-- Note: requires positive longitude coordinates
	if lat > 65 then
		return LQ(1)
	elseif lat > 30 then
		if lon >= 180 then
			return LQ(2 + math.floor( (lon - 180) / 60 ) )
		else
			return LQ(5 + math.floor( lon / 60 ) )
		end
	elseif lat >= 0 then
		if lon >= 180 then
			return LQ(8 + math.floor( (lon - 180) / 45 ) )
		else
			return LQ(12 + math.floor( lon / 45 ) )
		end
	elseif lat >= -30 then
		if lon >= 180 then
			return LQ(16 + math.floor( (lon - 180) / 45 ) )
		else
			return LQ(20 + math.floor( lon / 45 ) )
		end
	elseif lat >= -65 then
		if lon >= 180 then
			return LQ(24 + math.floor( (lon - 180) / 60 ) )
		else
			return LQ(27 + math.floor( lon / 60 ) )
		end
	else
		return LQ(30)
	end

	return 'Error'
end
--火星區
local function marsquad(lat, lon)
	-- Note: requires positive longitude coordinates
	if lat > 65 then 
		return '北海'
	elseif lat > 30 then 
		if lon < 60 then return '伊斯墨诺斯湖'
		elseif lon < 120 then return '卡西乌斯'
		elseif lon < 180 then return '刻布瑞尼亚'
		elseif lon < 240 then return '狄阿克里亚'
		elseif lon < 300 then return '阿卡迪亚'
		else return '阿基达利亚海' end
	elseif lat >= 0 then 
		if lon < 45 then return '阿拉伯'
		elseif lon <  90 then return '大三角'
		elseif lon < 135 then return '亚马孙'
		elseif lon < 180 then return '埃律西昂'
		elseif lon < 225 then return '亚马孙'
		elseif lon < 270 then return '塔尔西斯'
		elseif lon < 315 then return '月沼'
		else return '欧克西亚沼' end
	elseif lat >= -30 then 
		if lon < 45 then return '示巴湾'
		elseif lon <  90 then return '雅庇吉亚'
		elseif lon < 135 then return '第勒尼安海'
		elseif lon < 180 then return '埃俄利斯'
		elseif lon < 225 then return '门农'
		elseif lon < 270 then return '凤凰湖'
		elseif lon < 315 then return '科普剌塔斯'
		else return '珍珠湾' end
	elseif lat >= -65 then 
		if lon < 60 then return '挪亚'
		elseif lon < 120 then return '赫拉斯'
		elseif lon < 180 then return '波江'
		elseif lon < 240 then return '法厄同'
		elseif lon < 300 then return '陶马斯'
		else return '阿耳古瑞' end
	else
		return '火星南海'
	end
end
--水星區
local function mercuryquad(lat, lon)
	-- Note: requires positive longitude coordinates
	if lat >= 66 then
		return '水星北極'
	elseif lat >= 21 then
		if lon < 90 then return '北齋'
		elseif lon < 180 then return '拉德特拉迪'
		elseif lon < 270 then return '莎士比亞'
		else return '維多利亞' end
	elseif lat > -21 then
		if lon < 72 then return '德蘭'
		elseif lon < 144 then return '愛明內斯庫'
		elseif lon < 216 then return '托爾斯泰'
		elseif lon < 266 then return '貝多芬'
		else return '古柏' end
	elseif lat > -66 then
		if lon < 90 then return '德布西'
		elseif lon < 180 then return '聶魯達'
		elseif lon < 270 then return '米開朗基羅'
		else return '發現號' end
	else
		return '巴赫'
	end

	return 'Error'
end
--金星區
local function venusquad(lat, lon)
	-- Note: requires positive longitude coordinates
	if lat > 57 then
		return '伊絲塔'
	elseif lat >= 0 then
		if lon < 60 or lon >= 300 then return '賽德娜'
		elseif lon < 180 then return '尼俄伯'
		else return '關妮薇' end
	elseif lat >= -57 then
		if lon < 60  or lon >= 300 then return '拉維尼亞'
		elseif lon < 180 then return '阿佛洛狄忒'
		else return '海倫' end
	else
		return '拉達'
	end
end

local function quad_name(lat, lon, globe)
	-- lower case
	globe = globe:lower() or ''

	-- convert to numbers
	lat = tonumber(lat) or ''
	lon = tonumber(lon) or ''

	-- get the quad name
	if lat ~= '' and lon ~= '' and globe ~= '' then
		if lon < 0 then lon = lon + 360 end
		if lon < 0 or lon > 360 then
			return 'Error'
		end
		if globe == 'mars' then
			return marsquad(lat, lon)
		elseif globe == 'mercury' then
			return mercuryquad(lat, lon)
		elseif globe == 'moon' then
			return moonquad(lat, lon)
		elseif globe == 'venus' then
			return venusquad(lat, lon)
		end
	end

	return 'Error'
end

function p.category(frame)
	local args = frame.args
	local res = quad_name(args['lat'] or '', args['lon'] or '', args['globe'] or '')
	
	if res ~= 'Error' then
		if args['nameonly'] and args['nameonly'] ~= '' then
			return res
		else
			return '[[Category:'_.._res_.._'方格|Category:' .. res .. '方格]]'
		end
	end

	return '<span class="error">Error</span>'
end

function p.name(frame)
	local args = frame.args
	local res = quad_name(args['lat'] or '', args['lon'] or '', args['globe'] or '')
	
	if res ~= 'Error' then
		return res
	end
	return '<span class="error">Error</span>'
end

return p