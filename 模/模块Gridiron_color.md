--
-- This module implements
-- {{Gridiron primary color}} -- {{Gridiron primary color raw}} -- {{Gridiron primary style}}
-- {{Gridiron secondary color}} -- {{Gridiron secondary color raw}}
-- {{Gridiron tertiary color raw}}
-- {{Gridiron alt primary color}} -- {{Gridiron alt primary style}} -- {{Gridiron alt secondary color}}
--

local p = {}

local color_data = mw.loadData("Module:Gridiron color/data")

local yesno = require('Module:Yesno')

local prefixes = {
	"background: ",
	"color: ",
	"/**/",
	"background: ",
	"color: "
	}
	
local default = {"#DCDCDC", "#000000", "none", "", ""}

local function get_year(colors, year)
	if colors and colors[6] and type(colors[6] == 'table') then
		for team, year_colors in pairs(colors[6]) do
			if mw.ustring.find(team, "%d%d%d%dthru%d%d%d%d$") then
				local start_year, end_year = mw.ustring.match(team, "(%d%d%d%d)thru(%d%d%d%d)$")
				if (tonumber(start_year) <= tonumber(year)) and (tonumber(year) <= tonumber(end_year)) then
					return year_colors
				end
			end
		end
	end
	
	return colors
end

local function get_colors(team, unknown, year)
	team = (team or ''):match("^%s*(.-)%s*$")
	year = tonumber(year)
	unknown = unknown or color_data["#default"] or default
	
	local use_default = {
		[""] = 1,
		["retired"] = 1,
		["free agent"] = 1,
	}
	
	local colors = nil
	
	if ( team and use_default[team:lower()] ) then
		colors = unknown
	else
		if mw.ustring.find(team, "%d?%d?%d%dthru%d?%d?%d%d$") then
			if (not year or year <= 0) then
				team, year = mw.ustring.match(team, "^(.-) -(%d?%d?%d%d)thru%d?%d?%d%d$")
				team, year = team:match("^%s*(.-)%s*$"), tonumber(year)
				
				if year >= 20 and year < 100 then -- Two-digit years were deprecated in 2018
					year = year + 1900
				elseif year < 20 then
					year = year + 2000
				elseif year < 1000 then
					year = nil
				end
			else
				team = mw.ustring.match(team, "^(.-) -%d?%d?%d%dthru%d?%d?%d%d$") or team
			end
		end
		
		if year and year > 0 then
			--code for handling year parameter
			colors = get_year(color_data[team], year)
		else
			colors = color_data[team]
		end
		
		if ( colors and type(colors) == 'string') then
			if team == colors then year = nil end
			-- follow alias recursively
			return  get_colors (colors, unknown, year)
		end
	end
	
	return colors or unknown
end

local function bordercss(c, w)
	if w > 0 then
		local s = 'inset ' .. w .. 'px ' .. w .. 'px 0 ' .. c 
			.. ', inset -' .. w .. 'px -' .. w .. 'px 0 ' .. c
		return '-moz-box-shadow: ' .. s .. '; -webkit-box-shadow: ' .. s .. '; box-shadow: ' .. s .. ';'
	else
		return ''
	end
end

local function contrast_check(background, text, colors, alt)
	local c_limit = 4.5
	local contrast = require('Module:Color_contrast')
	if contrast._ratio({[1] = text, [2] = background, ['error'] = 0}) < c_limit then
		if contrast._ratio({[1] = '#FFFFFF', [2] = background, ['error'] = 0}) >= c_limit then
			text = '#FFFFFF'
		elseif contrast._ratio({[1] = '#000000', [2] = background, ['error'] = 0}) >= c_limit then
			text = '#000000'
		elseif (not alt) and (contrast._ratio({[1] = colors[5], [2] = colors[4], ['error'] = 0}) >= c_limit) then
			background, text = colors[4], colors[5]
		else
			background, text = default[1], default[2]
		end
	end
	return background, text
end

function p.test(frame)
	local args = frame.args.team and frame.args or frame:getParent().args
	local colors = get_colors((args.team or args[1]), nil, args.year)
	return '["' .. args.team .. '"] = {{ "' .. colors[1] .. '", '.. colors[2] ..
		'", '.. colors[3] .. '", '.. colors[4] .. '", '.. colors[5] .. '"}}'
end

function p.color(frame, column, altcolumn)
	local args = frame.args.team and frame.args or frame:getParent().args
	local colors = get_colors((args.team or args[1]), nil, args.year)

	column = (column or tonumber(frame.args.column)) or 1
	altcolumn = altcolumn or tonumber(frame.args.altcolumn)
	if ((not colors[column]) or (colors[column] == '')) and altcolumn then
		column = altcolumn
	end
	
	return (yesno(frame.args.raw) and "" or prefixes[column]) .. colors[column]
end

function p.style(frame)
	local team = frame.args.team or frame.args[1] or frame:getParent().args.team or frame:getParent().args[1]
	local year = frame.args.year or frame:getParent().args.year
	local border = frame.args.border or frame:getParent().args.border
	local alt = yesno(frame.args.alt or frame:getParent().args.alt)
	
	local colors = get_colors(team, nil, year)
	
	local background, text
	if alt then background, text = colors[4], colors[5] end
	if ((not background) or (background  == '')) then background = colors[1] end
	if ((not background) or (background  == '')) then background = default[1] end
	if ((not text) or (text  == '')) then text = colors[2] end
	if ((not text) or (text  == '')) then text = default[2] end
	
	-- background, text = contrast_check(background, text, colors, alt)
	
	local s = prefixes[1] .. background .. "; " .. prefixes[2] .. text .. "; "
	if tonumber(border) or yesno(border) then
		border = tonumber(border) and border or 2
		s = s .. bordercss(colors[3], tonumber(border))
	end
	return '' .. s
end

return p