-- Note: Originally written on English Wikipedia at https://en.wikipedia.org/wiki/Module:Mapframe
-- ##### Localisation (L10n) settings #####
-- Replace values in quotes ("") with localised values

local L10n = {}

-- Template parameter names (unnumbered versions only)
--   Specify each as either a single string, or a table of strings (aliases)
--   Aliases are checked left-to-right, i.e. `{ "one", "two" }` is equivalent to using `{{{one| {{{two|}}} }}}` in a template
L10n.para = {
	display		= "display",
	type		= "type",
	id              = { "id", "ids" },
	from		= "from",
	raw		= "raw",
	title		= "title",
	description	= "description",
	strokeColor     = { "stroke-color", "stroke-colour" },
	strokeWidth	= "stroke-width",
	coord		= "coord",
	marker		= "marker",
	markerColor	= { "marker-color", "marker-colour" },
	text		= "text",
	icon		= "icon",
	zoom		= "zoom",
	frame		= "frame",
	plain		= "plain",
	frameWidth	= "frame-width",
	frameHeight	= "frame-height",
	frameCoordinates = { "frame-coordinates", "frame-coord" }, 
	frameLatitude	= { "frame-lat", "frame-latitude" },
	frameLongitude	= { "frame-long", "frame-longitude" },
	frameAlign	= "frame-align"
}

-- Names of other templates this module depends on
L10n.template = {
	Coord		= "Coord"
}

-- Error messages
L10n.error = {
	badDisplayPara	= "Invalid display parameter",
	noCoords	= "Coordinates must be specified on Wikidata or in |" .. ( type(L10n.para.coord)== 'table' and L10n.para.coord[1] or L10n.para.coord ) .. "=",
	wikidataCoords	= "Coordinates not found on Wikidata"
}

-- Other strings
L10n.str = {
	-- valid values for display parameter, e.g. (|display=inline) or (|display=title) or (|display=inline,title) or (|display=title,inline)
	inline		= "inline",			
	title		= "title",	
	dsep		= ",",			-- separator between inline and title (comma in the example above)

	-- valid values for type paramter
	line		= "line",		-- geoline feature (e.g. a road)
	shape		= "shape",		-- geoshape feature (e.g. a state or province)
	shapeInverse	= "shape-inverse",	-- geomask feature (the inverse of a geoshape)
	data		= "data",		-- geoJSON data page on Commons
	point		= "point",		-- single point feature (coordinates)

	-- valid values for icon, frame, and plain parameters
	affirmedWords = ' '..table.concat({
		"add",
		"added",
		"affirm",
		"affirmed",
		"include",
		"included",
		"on",
		"true",
		"yes",
		"y"
	}, ' ')..' ',
	declinedWords = ' '..table.concat({
		"decline",
		"declined",
		"exclude",
		"excluded",
		"false",
		"none",
		"not",
		"no",
		"n",
		"off",
		"omit",
		"omitted",
		"remove",
		"removed"
	}, ' ')..' '
}

-- Default values for parameters
L10n.defaults = {
	display		= L10n.str.inline,
	text		= "Map",
	frameWidth	= "300",
	frameHeight	= "200",
	markerColor	= "5E74F3",
	strokeColor	= "#ff0000",
	strokeWidth	= 6
}

-- #### End of L10n settings ####

function getParameterValue(args, param_id, suffix)
	suffix = suffix or ''
	if type( L10n.para[param_id] ) ~= 'table' then
		return args[L10n.para[param_id]..suffix]
	end
	for _i, paramAlias in ipairs(L10n.para[param_id]) do
		if args[paramAlias..suffix] then
			return args[paramAlias..suffix]
		end
	end
	return nil
end	


function setCleanArgs(argsTable)
	local cleanArgs = {}
	for key, val in pairs(argsTable) do
		if type(val) == 'string' then
			val = val:match('^%s*(.-)%s*$')
			if val ~= '' then
				cleanArgs[key] = val:gsub('%c',' ')
			end
		else
			cleanArgs[key] = val
		end
	end
	return cleanArgs
end

function isAffirmed(val)
	if not(val) then return false end
	return string.find(L10n.str.affirmedWords, ' '..val..' ', 1, true ) and true or false
end

function isDeclined(val)
	if not(val) then return false end
	return string.find(L10n.str.declinedWords , ' '..val..' ', 1, true ) and true or false
end

function makeContent(args)
	if getParameterValue(args, 'raw') then
		return getParameterValue(args, 'raw')
	end

	local content = {};
	local contentIndex = '';
	local nextTypeOrFromExists = getParameterValue(args, 'type') or getParameterValue(args, 'from')
	while nextTypeOrFromExists do
		local contentArgs = {}
		for k, v in pairs(args) do
			if string.match(k, '.*'..contentIndex) then
				contentArgs[string.gsub(k, contentIndex, '')] = v
			end
		end

		if contentIndex == '' then contentIndex = 1 end
		content[contentIndex] = makeContentJson(contentArgs)
		contentIndex = contentIndex + 1
		nextTypeOrFromExists = getParameterValue(args, 'type', contentIndex) or getParameterValue(args, 'from', contentIndex)
	end
	
	--Single item, no array needed
	if #content==1 then return content[1] end

	--Multiple items get placed in a FeatureCollection
	local contentArray = '[\n' .. table.concat( content, ',\n') .. '\n]'
	return contentArray
end

function parseCoords(coords)
	local parts = mw.text.split((mw.ustring.match(coords,'[_%.%d]+[NS][_%.%d]+[EW]') or ''), '_')

	local lat_d = tonumber(parts[1])
	local lat_m = tonumber(parts[2]) -- nil if coords are in decimal format
	local lat_s = lat_m and tonumber(parts[3]) -- nil if coords are either in decimal format or degrees and minutes only
	local lat = lat_d + (lat_m or 0)/60 + (lat_s or 0)/3600
	if parts[#parts/2] == 'S' then
		lat = lat * -1
	end

	local long_d = tonumber(parts[1+#parts/2])
	local long_m = tonumber(parts[2+#parts/2]) -- nil if coords are in decimal format
	local long_s = long_m and tonumber(parts[3+#parts/2]) -- nil if coords are either in decimal format or degrees and minutes only
	local long = long_d + (long_m or 0)/60 + (long_s or 0)/3600
	if parts[#parts] == 'W' then
		long = long * -1
	end

	return lat, long
end

function wikidataCoords(item_id)
	if not(mw.wikibase.isValidEntityId(item_id)) or not(mw.wikibase.entityExists(item_id)) then
		error(L10n.error.noCoords, 0)
	end
	local coordStatements = mw.wikibase.getBestStatements(item_id, 'P625')
	if not coordStatements or #coordStatements == 0 then
		error(L10n.error.wikidataCoords, 0)
	end
	local hasNoValue = ( coordStatements[1].mainsnak and coordStatements[1].mainsnak.snaktype == 'novalue' )
	if hasNoValue then
		error(L10n.error.wikidataCoords, 0)
	end
	local wdCoords = coordStatements[1]['mainsnak']['datavalue']['value']
	return tonumber(wdCoords['latitude']), tonumber(wdCoords['longitude'])
end

function makeCoords(args, plainOutput) 
	local coords, lat, long
	local frame = mw.getCurrentFrame()
	if getParameterValue(args, 'coord') then
		coords = frame:preprocess( getParameterValue(args, 'coord') )
		lat, long = parseCoords(coords)
	else
		lat, long = wikidataCoords(getParameterValue(args, 'id') or mw.wikibase.getEntityIdForCurrentPage())
	end
	if plainOutput then
		return lat, long
	end
	return {[0] = long, [1] = lat}
end

function makeContentJson(contentArgs)
	local data = {}

	if getParameterValue(contentArgs, 'type') == L10n.str.point then
		data.type = "Feature"
		data.geometry = {
			type = "Point",
			coordinates = makeCoords(contentArgs)
		}
		data.properties = {
			title = getParameterValue(contentArgs, 'title') or mw.getCurrentFrame():getParent():getTitle(),
			["marker-symbol"] = getParameterValue(contentArgs, 'marker') or  L10n.defaults.marker,
			["marker-color"] = getParameterValue(contentArgs, 'markerColor') or L10n.defaults.markerColor
		}
	else
		data.type = "ExternalData"

		if getParameterValue(contentArgs, 'type') == L10n.str.data or getParameterValue(contentArgs, 'from') then
			data.service = "page"
		elseif getParameterValue(contentArgs, 'type') == L10n.str.line then
			data.service = "geoline"
		elseif getParameterValue(contentArgs, 'type') == L10n.str.shape then
			data.service = "geoshape"
		elseif getParameterValue(contentArgs, 'type') == L10n.str.shapeInverse then
			data.service = "geomask"
		end

		if getParameterValue(contentArgs, 'id') or (not (getParameterValue(contentArgs, 'from')) and mw.wikibase.getEntityIdForCurrentPage()) then
			data.ids = getParameterValue(contentArgs, 'id') or mw.wikibase.getEntityIdForCurrentPage()
		else 
			data.title = getParameterValue(contentArgs, 'from')
		end

		data.properties = {
			stroke = getParameterValue(contentArgs, 'strokeColor') or L10n.defaults.strokeColor,
			["stroke-width"] = tonumber(getParameterValue(contentArgs, 'strokeWidth')) or L10n.defaults.strokeWidth
		}
	end

	data.properties.title = getParameterValue(contentArgs, 'title') or mw.getCurrentFrame():preprocess('{{PAGENAME}}')
	if getParameterValue(contentArgs, 'description') then
		data.properties.description = getParameterValue(contentArgs, 'description')
	end

	return mw.text.jsonEncode(data)
end

function makeTagAttribs(args, isTitle)
	local attribs = {}
	if getParameterValue(args, 'zoom') then
		attribs.zoom = getParameterValue(args, 'zoom')
	end
	if isDeclined(getParameterValue(args, 'icon')) then
		attribs.class = "no-icon"
	end
	if getParameterValue(args, 'type') == L10n.str.point then
		local lat, long = makeCoords(args, 'plainOutput')
		attribs.latitude = tostring(lat)
		attribs.longitude = tostring(long)
	end
	if isAffirmed(getParameterValue(args, 'frame')) and not(isTitle) then
		attribs.width = getParameterValue(args, 'frameWidth') or L10n.defaults.frameWidth
		attribs.height = getParameterValue(args, 'frameHeight') or L10n.defaults.frameHeight
		if getParameterValue(args, 'frameCoordinates') then
			local frameLat, frameLong = parseCoords(getParameterValue(args, 'frameCoordinates'))
			attribs.latitude = frameLat
			attribs.longitude = frameLong
		else
			if getParameterValue(args, 'frameLatitude') then
				attribs.latitude = getParameterValue(args, 'frameLatitude')
			end
			if getParameterValue(args, 'frameLongitude') then
				attribs.longitude = getParameterValue(args, 'frameLongitude')
			end
		end
		if not attribs.latitude and not attribs.longitude then
			local success, lat, long = pcall(wikidataCoords, getParameterValue(args, 'id') or mw.wikibase.getEntityIdForCurrentPage())
			if success then
				attribs.latitude = tostring(lat)
				attribs.longitude = tostring(long)
			end
		end
		if getParameterValue(args, 'frameAlign') then
			attribs.align = getParameterValue(args, 'frameAlign')
		end
		if isAffirmed(getParameterValue(args, 'plain')) then
			attribs.frameless = "1"
		else
			attribs.text = getParameterValue(args, 'text') or L10n.defaults.text
		end
	else
		attribs.text = getParameterValue(args, 'text') or L10n.defaults.text
	end
	return attribs
end

function makeTitleOutput(args, tagContent)
 	local titleTag = mw.text.tag('maplink', makeTagAttribs(args, true), tagContent)
	local spanAttribs = {
		style = "font-size: small;",
		id = "coordinates"
	}
	return mw.text.tag('span', spanAttribs, titleTag)
end

function makeInlineOutput(args, tagContent)
	local tagName = 'maplink'
	if getParameterValue(args, 'frame') then
		tagName = 'mapframe'
	end

	return mw.text.tag(tagName, makeTagAttribs(args), tagContent)
end

local p = {}

-- Entry point for templates
function p.main(frame)
	local parent = frame.getParent(frame)
	local output = p._main(parent.args)
	return frame:preprocess(output)
end

-- Entry point for modules
function p._main(_args)
	local args = setCleanArgs(_args)
 
	local tagContent = makeContent(args)

	local display = mw.text.split(getParameterValue(args, 'display') or L10n.defaults.display, '%s*' .. L10n.str.dsep .. '%s*')
	local displayInTitle = display[1] ==  L10n.str.title or display[2] ==  L10n.str.title
	local displayInline = display[1] ==  L10n.str.inline or display[2] ==  L10n.str.inline

	local output
	if displayInTitle and displayInline then
		output = makeTitleOutput(args, tagContent) .. makeInlineOutput(args, tagContent)
	elseif displayInTitle then
		output = makeTitleOutput(args, tagContent)
	elseif displayInline then
		output = makeInlineOutput(args, tagContent)
	else
		error(L10n.error.badDisplayPara)
	end

	return output
end

return p