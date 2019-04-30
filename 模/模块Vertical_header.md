local p = {}

function p.cell(frame)
	local text = frame.args.text
	local sortPadding = frame.args.sortPadding
	local vertAlign = frame.args.vertAlign
	local maxWidth = frame.args.maxWidth
	local noBold = frame.args.noBold
	local style = frame.args.style
	local wikiText = "class = \"nowrap"
	local normalAlign = ""
	-- local stupidIEAlign = ""
	local rows = 1
	local width = 0
	if maxWidth ~= "" then
		width = maxWidth
	else
		for eachMatch in text:gmatch("<br>") do
			rows = rows + 1
		end
		width = rows * 0.875
		width = width .. "em"
	end
	if sortPadding == "" then
		wikiText = wikiText .. " unsortable"
	end
	wikiText = wikiText .. "\" style=\"line-height:99%;vertical-align:" .. vertAlign .. ";padding:"
	if sortPadding == "" then
		wikiText = wikiText .. ".4em"
	else
		wikiText = wikiText .. "21px"
	end
	wikiText = wikiText .. " .4em .2em;background-position:50% .4em !important;"
	wikiText = wikiText .. "min-width:" .. width .. ";max-width:" .. width .. ";width:" .. width .. ";overflow:hidden\""
	wikiText = wikiText .. " | <div style=\"" .. frame:preprocess("{{writing-mode|v1}}") .. "-ms-transform: none \ ;padding-left:1px;text-align:"
	if vertAlign == "top" then
		normalAlign = "right"
		-- stupidIEAlign = "left"
	elseif vertAlign == "middle" then
		normalAlign = "center"
		-- stupidIEAlign = "center"
	else
		normalAlign = "left"
		-- stupidIEAlign = "right"
	end
	wikiText = wikiText .. normalAlign .. ";" -- text-align:" .. stupidIEAlign .. " \ ;"
	wikiText = wikiText .. style .. "\">"
	if noBold == "" then
		wikiText = wikiText .. text
	else
		wikiText = wikiText .. frame:preprocess("{{nobold|1=" .. text .. "}}")
	end
	wikiText = wikiText .. "</div>"
	return wikiText
end

return p