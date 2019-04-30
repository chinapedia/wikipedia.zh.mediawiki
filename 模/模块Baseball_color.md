--
-- This module implements
-- {{Baseball primary color}}, {{Baseball secondary color}}, 
-- {{Baseball alternative primary color}}, {{Baseball alternative secondary color}}
-- {{Baseball primary style}}, {{Baseball secondary style}}
--
local p = {}

local data_module = "Module:Baseball color/data"

local function stripwhitespace(text)
	return text:match("^%s*(.-)%s*$")
end

local function get_colors(team, unknown)
	team = stripwhitespace(team or '')
	unknown = unknown or {"DCDCDC", "000000", "DCDCDC", "000000"}
	
	local use_default = {
		[""] = 1,
		["retired"] = 1,
		["free agent"] = 1,
	}
	
	local colors = nil
	
	if ( team and use_default[team:lower()] ) then
		colors = {"DCDCDC", "000000", "DCDCDC", "000000"}
	else
		local all_colors = mw.loadData(data_module)
		
		colors = all_colors[team]
		if ( colors and type(colors) == 'string' ) then
			colors = all_colors[colors]
		end
	end

	return colors or unknown
end

local function team_check(team, unknown)
	local colors = get_colors(team, unknown)
	if type(colors) == 'table' then
		return 'known'
	else
		return unknown
	end
end

local function team_color(team, num)
	local colors = get_colors(team, nil)
	
	num = tonumber(num:match('[1-4]') or '0')
	if ( num ) then
		return colors[num]
	else
		return ''
	end
end

local function team_colorcell(team, borderwidth, bg, fg, bd)
	local colors = get_colors(team, nil)
	local border = ''
	borderwidth = tonumber(borderwidth or '0') or 0
	
	if (borderwidth > 0) then
		local bordercolor = stripwhitespace(colors[bd]) or 'FFFFFF'
		if bordercolor ~= 'FFFFFF' then
			border = 'border:' .. borderwidth .. 'px solid #' .. bordercolor .. ';'
		end
	end

	return 'background-color:#' .. stripwhitespace(colors[bg]) .. ';color:#' .. stripwhitespace(colors[fg]) .. ';' .. border
end

function p.check(frame)
	local args = (frame.args[1] ~= nil) and frame.args or frame:getParent().args
	return team_check(args[1] or '', args[2] or '')
end

function p.color(frame)
	local args = (frame.args[1] ~= nil) and frame.args or frame:getParent().args
	return team_color(args[1] or '', args[2] or '')
end

function p.colorcell(frame)
	local args = (frame.args[1] ~= nil) and frame.args or frame:getParent().args
	return team_colorcell(args[1] or '', args['border'] or '', 1, 2, 3)
end

function p.colorcell2(frame)
	local args = (frame.args[1] ~= nil) and frame.args or frame:getParent().args
	return team_colorcell(args[1] or '', args['border'] or '', 3, 4, 1)
end

return p