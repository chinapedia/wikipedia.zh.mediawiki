---------- Module:Wikibase ----------------
local p = {}

-- Return the item ID of the item linked to the current page.
function p.id(frame)
	if not mw.wikibase then
		return "无mw.wikibase"
	end
	entity = mw.wikibase.getEntityObject()

	if entity == nil then
		return "无项目"
	end
	return entity.id
end

-- Return the label of a given data item, or of connected page
-- if no argument is provided to this method.
function p.label(frame)
	if frame.args[1] == nil then
		entity = mw.wikibase.getEntityObject()
		if not entity then return nil end
		id = entity.id
	else
		id = mw.text.trim(frame.args[1])
	end
	return mw.wikibase.label( id )
end

-- Return the description of a given data item, or of connected page
-- if no argument is provided to this method.
function p.description(frame)
	if frame.args[1] == nil then
		entity = mw.wikibase.getEntityObject()
		if not entity then return nil end
		id = entity.id
	else
		id = mw.text.trim(frame.args[1])
	end
	return mw.wikibase.description( id )
end

-- Return the local page about a given data item, or of connected page
-- if id is not specified.
function p.page(frame)
	if frame.args[1] == nil then
		entity = mw.wikibase.getEntityObject()
		if not entity then return nil end
		id = entity.id
	else
		id = mw.text.trim(frame.args[1])
	end
	return mw.wikibase.sitelink( id )
end

-- Return the data type of a property
function p.datatype(frame)
	if frame.args[1] and string.find(frame.args[1], "Property:P") then
		if mw.wikibase.getEntityObject(string.gsub(frame.args[1], "Property:P", "P"))  then
			return mw.wikibase.getEntityObject(string.gsub(frame.args[1], "Property:P", "P") ).datatype
		end
	elseif frame.args[1] and string.find(frame.args[1], "P") then
		if mw.wikibase.getEntityObject(frame.args[1])  then
			return mw.wikibase.getEntityObject(frame.args[1]).datatype
		end
	end
end

return p