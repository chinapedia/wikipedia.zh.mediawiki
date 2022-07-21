local p = {}

function p.parse(frame)
	local args = frame:getParent().args -- This gets the arguments passed to the template that called #invoke, so we don't need to pass them all through to the module. See also [[Module:Arguments|Module:Arguments]].
	local vauthors = args[1] or args.vauthors
	local authorTable
	local lastfirstTable
	local nauthors
	if vauthors then
		if string.find(vauthors, ';') or string.find(vauthors, '%.') then
			verror = true -- Vancouver author format should not contain semicolons or periods
		else
			verror = false
		end
		authorTable = mw.text.split(vauthors, "%s*,%s*")
	else
		authorTable = {}
	end
	local citeArgs = {}
	for k, v in pairs(args) do
		citeArgs[k] = v
	end
	citeArgs[1] = nil -- Erase vauthors from the citation arguments.
	citeArgs.vauthors = nil -- Erase vauthors from the citation arguments.
	nauthors = 0
	for i, author in ipairs(authorTable) do
		if string.find(author, "%s") then
		    lastfirstTable = {}
		    lastfirstTable = mw.text.split(author, "%s")
		    first = table.remove(lastfirstTable)
		    last  = table.concat(lastfirstTable, " ")
		    citeArgs['first' .. i] = first
		    citeArgs['last' .. i]  = last
		    nauthors = nauthors + 1
		else
			citeArgs['first' .. i] = ""
			citeArgs['last' .. i]  = author
		    nauthors = nauthors + 1
		end
	end

    if next(authorTable) == nil then
	    citeArgs['authorformat'] = "vanc" -- change default settings of authorformat, etc. parameters so that Vancouver style author format is used
	end
	if citeArgs['author-separator'] == nil then
	    citeArgs['author-separator'] = ","
	end
	if citeArgs['author-name-separator'] == nil then
	    citeArgs['author-name-separator'] = " "
	end
	if citeArgs['display-authors'] == nil and citeArgs['displayauthors'] == nil and nauthors > 6 then
		citeArgs['display-authors'] = '6'
    end

	if verror then
        errorArgs = {}
        errorArgs['1']='vauthors format'
		return frame:expandTemplate{title = 'cite journal', args = citeArgs}, frame:expandTemplate{title = 'citation error', args = errorArgs}
	else
		return frame:expandTemplate{title = 'cite journal', args = citeArgs}
	end
end

return p