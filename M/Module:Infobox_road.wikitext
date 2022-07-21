local p = {}
local getArgs = require('Module:Arguments').getArgs

function p.headerStyle(frame)
	local args = getArgs(frame)
	local deleted = args.decommissioned or args.deleted
	if deleted then
		return "background:#AAA;"
	end
	local colors = require"Module:Infobox road/color"
	return colors.color(frame)
end

local function browse(args)
	local previousRoute = args.previous_route
	local extended = args.browse
	if previousRoute or extended then
		local box = mw.html.create('table'):cssText("width:100%; background:none; border-collapse:collapse")
		if previousRoute then
			local boxModule = require "Module:Road data/browse"
			local primary = boxModule._browse(args)
			box:wikitext(primary)
		end
		if extended then
			box:wikitext(extended)
		end
		return tostring(box)
	else
		return ''
	end
end

function p.browse(frame)
	local args = getArgs(frame)
	return browse(args)
end

return p