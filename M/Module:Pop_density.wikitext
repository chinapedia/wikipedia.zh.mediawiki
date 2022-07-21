--
-- This module implements {{Pop density}}
--
local p = {}
local math_module = require( "Module:Math" )
local precision = math_module._precision

local function rnd(num, digits)
	-- This function implements {{rnd}}
	return math_module._precision_format(tostring(num), tostring(digits))
end
local unitnames = {
	["km²"] = "km2",
	["sqkm"] = "km2",
	["km2"] = "km2",
	["mi2"] = "sqmi",
	["sqmi"] = "sqmi",
	["acres"] = "acre",
	["acre"] = "acre",
	["ha"] = "ha",
	["dunam"] = "dunam",
	["m²"] = "m2",
	["sqm"] = "m2",
	["m2"] = "m2"
}
local unitmult = {
	["km2"] = 1000000,
	["sqmi"] = 2589988.110336,
	["acre"] = 4046.8564224,
	["ha"] = 10000,
	["dunam"] = 1000,
	["m2"] = 1
}
local unitstr = {
	["km2"] = '平方公里',
	["sqmi"] = '平方英里',
	["acre"] = '英亩',
	["ha"] = '公顷',
	["dunam"] = '德南',
	["m2"] = '平方米'
}

local function popdensity(pop, area1, areaunit1, areaunit2, prec, disp, flip)
	local dens1, prec1 = nil, nil
	local dens2, prec2 = nil, nil
	local str1, str2 = '', ''
	local uniterror = '<sup>[[Template:Pop_density|单位错误]]</sup>[[Category:采用不支持单位的人口密度公式|Category:采用不支持单位的人口密度公式]]'
	
	if(pop ~= '' and area1 ~= '') then
		-- pop and area are defined
		local popnum = tonumber(pop)
		if not popnum then
			error(string.format('Unable to convert population "%s" to a number', pop), 2)
		end
		local area1num = tonumber(area1)
		if not area1num then
			error(string.format('Unable to convert area "%s" to a number', area1), 2)
		end
		local dens1num = popnum/area1num
		
		local unit1 = unitnames[areaunit1] or nil
		local unit2 = unitnames[areaunit2] or nil
		
		prec1 = (prec ~= '') and tonumber(prec) or (1+math.log10(2*area1/(1/10^precision(pop)+pop/area1/10^precision(area1))))
		dens1 = rnd(dens1num, math.floor(prec1 + 0.5))
		if (unit1) then
			str1 = '/' .. unitstr[unit1]
			if(unit2) then
				-- convert
				local mult = unitmult[unit2]/unitmult[unit1]
				prec2 = prec1 - math.log10(mult)
				dens2 = rnd(dens1num*mult, math.floor(prec2 + 0.5))
				str2 = '/' .. unitstr[unit2]
			elseif(areaunit2 ~= '') then
				if( disp ~= 'num' ) then
					dens2 = '?'
				else
					dens2 = '?' .. uniterror
				end
				str2 = '/' .. areaunit2 .. uniterror
			end
		elseif(areaunit1 ~= '') then
			if( disp ~= 'num' ) then
				dens2 = '?'
			else
				dens2 = '?' .. uniterror
			end
			if(unit2) then
				str2 = '/' .. unitstr[unit2]
			elseif(areaunit2 ~= '') then
				str2 = '/' .. areaunit2 .. uniterror				
			end
			str1 = '/' .. areaunit1 .. uniterror
		end

		-- form output
		if( str2 ~= '' ) then
			-- has a converted unit
			if( disp ~= 'num' and disp ~= 'table' ) then
				-- display input and output density numbers with units
				if( flip == 'on' ) then
					return dens2 .. str2 .. ' (' .. dens1 .. str1 .. ')'
				else
					return dens1 .. str1 .. ' (' .. dens2 .. str2 .. ')'
				end
			elseif( disp == 'table') then
				return pop .. '||' .. area1 .. '||' .. dens1 .. '||' .. dens2
			else
				-- display output density number without unit
				return dens2
			end
		else
			-- no converted unit
			if( disp ~= 'num' and disp ~= 'table' ) then
				-- display input density number with unit 
				return dens1 .. str1 
			elseif( disp == 'table') then
				return pop .. '||' .. area1 .. '||' .. dens1
			else
				-- display input density number without unit
				return dens1
			end
		end
	end
	return ''
end

function p.density(frame)
	local args = (frame.args[3] ~= nil) and frame.args or frame:getParent().args
	return popdensity(args[1] or '', args[2] or '', args[3] or '', args[4] or '', args['prec'] or '', args['disp'] or '', args['flip'] or '')
end

return p