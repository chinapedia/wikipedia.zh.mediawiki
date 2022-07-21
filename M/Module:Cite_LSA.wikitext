local p = {}
function p.cite(frame)
	local pframe = frame:getParent()
	local config = frame.args
	local args = pframe.args
	local authorfirst = {}
	local authorlast = {}
	local editorfirst = {}
	local editorlast = {}
	local title = args.title
	local journal = args.journal
	local chapter = args.chapter
	local series = args.seriestitle or args.series
	local year = args.year
	local volume = args.volume
	local edition = args.edition
	local pages = args.pages
	local publisher = args.publisher
	local author = args.last
	local url = args.url
	local accessdate = args.accessdate
	local editorlist = nil
	local place = args.place
	local citation = nil
	argTable = {title,journal,chapter,series, year, volume, edition,pages,publisher,editors,place}
	for k,v in pairs(args) do
		if string.find(k, "first") ~= nil then
			if string.find(k, "%d") ~= nil then
				i,j = string.find(k, "%d")
				num = string.sub(k,i,j)
				num = tonumber(num)
			else
				num = 1
			end
			if string.find(k, "editor") ~= nil then
				editorfirst[num] = v
			else
				authorfirst[num] = v
			end
		elseif string.find(k, "last") ~= nil then
			if string.find(k, "%d") ~= nil then
				i,j = string.find(k, "%d")
				num = string.sub(k,i,j)
				num = tonumber(num)
			else
				num = 1
			end
			if string.find(k, "editor") ~= nil then
				editorlast[num] = v
			else
				authorlast[num] = v
			end
		end
	end
	if table.getn(authorlast) < 1 and publisher ~= nil then
		authorlist="<span class=\"smallcaps\" style=\"font-variant:small-caps;\">" .. publisher .. "</span>. "
		author=""
	elseif table.getn(authorlast) > 0 then
		alimit = table.getn(authorlast)
		for i,v in ipairs(authorlast) do
			if i == 1 then
				authorlist = "<span class=\"smallcaps\" style=\"font-variant:small-caps;\">" .. authorlast[1] .. ", " .. authorfirst[1] .. "</span>"
			elseif i > 1 and i <= alimit then
				authorlist = authorlist .. "<span class=\"smallcaps\" style=\"font-variant:small-caps;\">" .. authorfirst[i] .. " " .. authorlast[i] .. "</span>"
			end
			if i+1 == alimit then
				authorlist = authorlist .. ", and "
			elseif alimit == 1 then
				authorlist = authorlist .. ". "
			elseif alimit > 2 and i ~= alimit then
				authorlist = authorlist .. "; "
			elseif i == alimit then
				authorlist = authorlist .. ". "
			end
		end
	end
	if editorlast ~= {} then
		editorlist = ""
		elimit = table.getn(editorlast)
		for i,v in ipairs(editorlast) do
			editorlist = editorlist .. editorfirst[i] .. " " .. editorlast[i]
			if i+1 == elimit and editorlist ~= " " then
				editorlist = editorlist .. ", and "
			elseif elimit > i and editorlist ~= " " then
				editorlist = editorlist .. ", "
			end
		end
		if editorlist == "" or editorlist == " " then
			editorlist = ""
		end
	end
	if author ~= nil then
		authorlist = authorlist .. year .. ". "
	elseif author == nil then
		authorlist = "<span style=\"color:#F00\">Missing author name</span>" .. year .. ". "
	end
	if journal ~= nil then
		if url ~= nil then
			if accessdate ~= nil then
				citation = authorlist .. "[" .. url .. " " .. title .. "]. \'\'" .. journal .. "\'\' " .. volume .. ". " .. pages .. ". Accessed " .. accessdate .. "."
			else
				citation = authorlist .. "[" .. url .. " " .. title .. "]. \'\'" .. journal .. "\'\' " .. volume .. ". " .. pages .. ". <span style=\"color:#F00\">Missing <span style=\"font-family: monospace;\">accessdate</span></span>"
			end
		else
			citation = authorlist .. title .. ". \'\'" .. journal .. "\'\' " .. volume .. ". " .. pages
		end
	elseif journal == nil then
		if chapter ~= nil then
			if url ~= nil then
				citation = authorlist .. "[" .. url .. " " .. chapter .. "]."
			else
				citation = authorlist .. chapter .. ". "
			end
			if title ~= nil then
				citation = citation .. "\'\'" .. title .. "\'\'"
				if editorlist ~= nil and editorlist ~= "" then
					citation = citation .. " ed. by " .. editorlist
				end
				if pages ~= nil then
					citation = citation .. ", " .. pages .. ". "
				else
					citation = citation .. ". "
				end
				if edition ~= nil and volume ~= nil then
					citation = citation .. edition .. ", " .. volume .. "; " 
				elseif edition ~= nil and volume == nil then
					citation = citation .. edition .. "; "
				elseif edition == nil and volume ~= nil then
					citation = citation .. volume .. "; "
				end
				if series ~= nil then
					citation = citation .. "(" .. series .. "). "
				end
				if place ~= nil and publisher ~= nil then
					citation = citation .. place .. ": " .. publisher .. "."
				elseif place ~= nil and publisher == nil then
					citation = citation .. place .. "."
				elseif place == nil and publisher ~= nil then
					citation = citation .. publisher .. "."
				end
				if url ~= nil then
					if accessdate ~= nil then
						citation = citation .. " Accessed " .. accessdate .. ". "
					else
						citation = citation .. "<span style=\"color:#F00\">Missing <span style=\"font-family: monospace;\">accessdate</span></span>"
					end
				end
			end
		else
			if title ~= nil then
				if url ~= nil then
					citation = authorlist .. "\'\'[" .. url .. " " .. title .. "]\'\'"
				else
					citation = authorlist .. "\'\'" .. title .. "\'\'"
				end
				if editorlist ~= nil and editorlist ~= "" then
					citation = citation .. ", ed. by " .. editorlist
				end
				if pages ~= nil then
					citation = citation .. ", " .. pages .. ". "
				else
					citation = citation .. ". "
				end
				if edition ~= nil and volume ~= nil then
					citation = citation .. edition .. ", " .. volume .. "; " 
				elseif edition ~= nil and volume == nil then
					citation = citation .. edition .. "; "
				elseif edition == nil and volume ~= nil then
					citation = citation .. volume .. "; "
				end
				if series ~= nil then
					citation = citation .. "(" .. series .. "). "
				end
				if place ~= nil and publisher ~= nil then
					citation = citation .. place .. ": " .. publisher .. "."
				elseif place ~= nil and publisher == nil then
					citation = citation .. place .. "."
				elseif place == nil and publisher ~= nil then
					citation = citation .. publisher .. "."
				end
				if url ~= nil then
					if accessdate ~= nil then
						citation = citation .. " Accessed " .. accessdate .. "."
					else
						citation = citation .. "<span style=\"color:#F00\">Missing <span style=\"font-family: monospace;\">accessdate</span></span>"
					end
				end
			end
		end
	end
	return citation
end

return p