local p = {}

-- List of default title texts.
local defaultTitleTextlist = {
	["TBA"] = "待宣布",
	["TBD"] = "待定",
	["N/A"] = "不适用"	
}

-- Local function which is used to retrieve the title text.
local function getTitleText(args, altText)
	local titleText = args[2] or args["title_text"]

	-- If the title text was manually added, return it.
	if (titleText) then
		return titleText
	end
	
	-- The title text was not set, get the correct default text which corresponds to the alt text.
	for k, v in pairs(defaultTitleTextlist) do
		if (altText == k) then
			return v
		end
	end
end

-- Local function which is used to retrieve the alt text.
local function getAltText(args)
	local altText = args[1] or args["alt_text"]
	
	if (altText == nil) then
		altText = "TBA"
	end
	
	return altText
end

-- Local function which does the actual main process.
function p._main(args)
	local altText = getAltText(args)
	local titleText = getTitleText(args, altText)

	return "<small><span style=\"color: #2C2C2C\" title=\"" .. titleText .. "\">" .. altText .. "</span></small>"
end

--[[
Public function which is used to create information for an empty text cell.

Parameters:
	-- |1= or |alt_text=		— optional; The text which will be written in the cell.
	-- |2= or |title_text=		— optional; The text which will be shown when hovering over the cell.
--]]
function p.main(frame)
	local getArgs = require('Module:Arguments').getArgs;
	local args = getArgs(frame);
	return p._main(args)
end

return p