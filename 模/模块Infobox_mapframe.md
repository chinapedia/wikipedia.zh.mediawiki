local mf = require('Module:Mapframe')

-- Trim whitespace from args, and remove empty args
function trimArgs(argsTable)
	local cleanArgs = {}
	for key, val in pairs(argsTable) do
		if type(val) == 'string' then
			val = val:match('^%s*(.-)%s*$')
			if val ~= '' then
				cleanArgs[key] = val
			end
		else
			cleanArgs[key] = val
		end
	end
	return cleanArgs
end

function hasWikidataProperty(item_id, property_id)
	if not(item_id) or not(mw.wikibase.isValidEntityId(item_id)) or not(mw.wikibase.entityExists(item_id)) then
		return false
	end
	local statements = mw.wikibase.getBestStatements(item_id, property_id)
	if not statements or #statements == 0 then
		return false
	end
	local hasNoValue = ( statements[1].mainsnak and statements[1].mainsnak.snaktype == 'novalue' )
	if hasNoValue then
		return false
	end
	return true
end


function getZoom(length_km)
	-- max for zoom 2 is 6400km, for zoom 3 is 3200km, for zoom 4 is 1600km, etc
	local zoom = math.floor(8 - (math.log10(length_km) - 2)/(math.log10(2)))
	-- limit to values between 1 and 17
	return math.max(1, math.min(17, zoom))
end

local p = {}

p.main = function(frame)
	local parent = frame.getParent(frame)
	local parentArgs = parent.args
	local mapframe = p._main(parentArgs)
	return frame:preprocess(mapframe)
end

p._main = function(_config)
	-- `config` is the args passed to this module
	local config = trimArgs(_config)
	
	-- Use wikidata by default
	local useWikidata = true
	-- Do not use wikidata when coords are specified, unless explicitly set
	if config.coord then
		useWikidata = config.wikidata and true or false
	end
	
	-- Require wikidata item, or specified coords
	local wikidataId = config.id or mw.wikibase.getEntityIdForCurrentPage()
	if not(wikidataId) and not(config.coord) then
		return ''
	end

	-- Require coords (specified or from wikidata), so that map will be centred somewhere
	-- (P625 = coordinate location)
	local hasCoordinates = hasWikidataProperty(wikidataId, 'P625') or config.coordinates or config.coord
	if not hasCoordinates then  
		return ''
	end

	-- `args` is the arguments which will be passed to the mapframe module
	local args = {}

	-- Some defaults/overrides for infobox presentation
	args.display = "inline"
	args.frame = "yes"
	args.plain = "yes"
	args["frame-width"]  = config["frame-width"] or "270"
	args["frame-height"] = config["frame-height"] or "200"
	args["frame-align"]  = "center"

	args["frame-coord"] = config["frame-coordinates"] or config["frame-coord"] or ""
	-- Note: config["coordinates"] or config["coord"] should not be used for the alignment of the frame;
	-- see talk page ( https://en.wikipedia.org/wiki/Special:Diff/876492931 )

	-- deprecated lat and long parameters
	args["frame-lat"]    = config["frame-lat"] or config["frame-latitude"] or ""
	args["frame-long"]   = config["frame-long"] or config["frame-longitude"] or ""

	-- Calculate zoom from length or area (converted to km or km2)
	if config.length_km then
		args.zoom = getZoom(tonumber(config.length_km))
	elseif config.length_mi then
		args.zoom = getZoom(tonumber(config.length_mi)*1.609344)
	elseif config.area_km2 then
		args.zoom = getZoom(math.sqrt(tonumber(config.area_km2)))
	elseif config.area_mi2 then
		args.zoom = getZoom(math.sqrt(tonumber(config.area_mi2))*1.609344)
	else
		args.zoom = config.zoom or 10
	end

	-- Shape
	if useWikidata then
		args.type = "shape"
		if config.id then args.id = config.id end
		args["stroke-width"] = config["shape-stroke-width"] or config["stroke-width"] or "3"
		args["stroke-color"] = config["shape-stroke-color"] or config["shape-stroke-colour"] or config["stroke-color"] or config["stroke-colour"] or "#FF0000"
	end
	
	-- Line
	if useWikidata then
		args.type2 = "line"
		if config.id then args.id2 = config.id end
		args["stroke-width2"] = config["line-stroke-width"] or config["stroke-width"] or "5"
		args["stroke-color2"] = config["line-stroke-color"] or config["line-stroke-colour"] or config["stroke-color"] or config["stroke-colour"] or "#FF0000"
	end

	-- Point
	local hasOsmRelationId = hasWikidataProperty(wikidataId, 'P402') -- P402 is OSM relation ID
	local shouldShowPointMarker = not(hasOsmRelationId) or (config.marker and config.marker ~= 'none') or (config.coordinates or config.coord)
	if shouldShowPointMarker then
		local argNumber = useWikidata and "3" or ""
		args["type"..argNumber] = "point"
		if config.id then args["id"..argNumber] = config.id end
		if config.coord then args["coord"..argNumber] = config.coord end
		if config.marker then args["marker"..argNumber] = config.marker end
		args["marker-color"..argNumber] = config["marker-color"] or config["marker-colour"] or "#5E74F3"
	end
	local mapframe = mf._main(args)
	local tracking = hasOsmRelationId and '' or '[[Category:Infobox_mapframe在维基数据上没有OSM关系标识符|Category:Infobox mapframe在维基数据上没有OSM关系标识符]]'
	return mapframe .. tracking
end

return p