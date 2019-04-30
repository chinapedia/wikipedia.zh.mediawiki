local z = {}

local function makeArticleLink( label, sitelink )
	if label ~= nil then
		if sitelink ~= nil then
			return '[[:'_.._sitelink_.._'|' .. label .. ']]'
		else
			return label
		end
	else
		if sitelink ~= nil then
			return '[[:'_.._sitelink_.._'|:' .. sitelink .. ']]'
		else
			return '' -- What's the best thing we can do here?
		end
	end
end

local function makeEntityLink( entity )
	local label = entity:getLabel()
	for _, statement in pairs( entity:getBestStatements( 'P1448' ) ) do
		if statement.mainsnak.datavalue.value.language == 'zh-cn' then
			label = statement.mainsnak.datavalue.value.text
			break
		end
	end
	local sitelink = entity:getSitelink()
	return makeArticleLink( label, sitelink )
end

local premadeItemLinks = {
	Q986065 = '[[街道办事处|街道]]',
	Q735428 = '[[行政建制镇|镇]]',
	Q1500350 = '[[乡级行政区|乡]]',
	Q2365159 = '[[苏木_(行政区划)#中华人民共和国|苏木]]',
	Q50231 = '其他'
}

local function makeItemLink( item )
	if premadeItemLinks[item] ~= nil then
		return premadeItemLinks[item]
	end
	local label = mw.wikibase.label( item )
	local sitelink = mw.wikibase.sitelink( item )
	return makeArticleLink( label, sitelink )
end

local function makeFullNames( items )
	if type( items ) ~= 'table' then
		items = { items }
	end
	local fullNames = {}
	for _, item in pairs( items ) do
		local entity = mw.wikibase.getEntity( item )
		local entityLink = makeEntityLink( entity )
		local upperStatements = entity:getBestStatements( 'P131' )
		local upperItems = {}, upperFullNames
		for _, upperStatement in pairs( upperStatements ) do
			table.insert( upperItems, 'Q' .. upperStatement.mainsnak.datavalue.value['numeric-id'] )
		end
		if #upperItems == 0 then
			-- Root item
			table.insert( fullNames, entityLink )
		else
			_, upperFullNames = makeFullNames( upperItems )
			for _, upperFullName in pairs( upperFullNames ) do
				table.insert( fullNames, upperFullName .. entityLink )
			end
		end
	end
	return mw.text.listToText( fullNames ), fullNames
end
local makeFullName = makeFullNames
z._makeFullNames = makeFullNames -- For debugging

-- items must be a table of entities
local function findUpperEntities( entities, levels )
	if levels <= 0 then
		return entities
	end
	local recursiveEntities = {}
	for _, entity in pairs( entities ) do
		local upperStatements = entity:getBestStatements( 'P131' )
		for _, upperStatement in pairs( upperStatements ) do
			table.insert( recursiveEntities, mw.wikibase.getEntity( 'Q' .. upperStatement.mainsnak.datavalue.value['numeric-id'] ) )
		end
	end
	return findUpperEntities( recursiveEntities, levels - 1 )
end

-- Specify a division with item=Qxxx or defaults to current article
-- Other arguments: comment=, below=, see-also-upper=, see-also-upper-prefix=, see-also-upper-suffix=
function z.navbox( frame, args )
	if args == nil then
		args = frame.args
	end
	local item = ''
	if args.item ~= nil and args.item ~= '' then
		item = args.item
	end
	local entity = mw.wikibase.getEntity( item )
	if entity == nil then
		return ''
	end
	local navboxArgs = {
		name = 'd::' .. entity.id,
		title = makeEntityLink( entity ) .. '行政区划',
		state = args.state or frame:getParent().args.state or 'collapsed',
		listclass = 'hlist',
	}
	
	-- Navbox above
	local upperItems = {}
	for _, upperStatement in pairs( entity:getBestStatements( 'P131' ) ) do
		table.insert( upperItems, 'Q' .. upperStatement.mainsnak.datavalue.value['numeric-id'] )
	end
	local fullName = makeFullName( upperItems )
	if fullName ~= '' then
		navboxArgs.above = '行政隶属：' .. fullName
	end
	
	-- Navbox lists
	local lists = {} -- { ['Qxxx-type1-str'] = { 'Qxxx-div1-obj', 'Qxxx-div2-obj' } }
	local lowerStatements = entity:getBestStatements( 'P150' )
	for i, lowerStatement in pairs( lowerStatements ) do
		lowerStatement._entity = mw.wikibase.getEntity( 'Q' .. lowerStatement.mainsnak.datavalue.value['numeric-id'] )
		lowerStatement._code = 'X'
		for _, codeStatement in pairs( lowerStatement._entity:getBestStatements( 'P442' ) ) do
			if codeStatement.mainsnak.datavalue.value < lowerStatement._code then
				lowerStatement._code = codeStatement.mainsnak.datavalue.value
			end
		end
	end
	table.sort( lowerStatements, function( a, b )
		return a._code < b._code;
	end )
	local typeItems = {}
	for _, lowerStatement in pairs( lowerStatements ) do
		local lowerEntity = lowerStatement._entity
		for _, typeStatement in pairs( lowerEntity:getBestStatements( 'P31' ) ) do
			local typeItem = 'Q' .. typeStatement.mainsnak.datavalue.value['numeric-id']
			if lists[typeItem] ~= nil then
				table.insert( lists[typeItem], lowerEntity )
			else
				lists[typeItem] = { lowerEntity }
				table.insert( typeItems, typeItem )
			end
		end
	end
	local count = 1
	for i = 1, #typeItems do
		local typeItem = typeItems[i]
		local lowerEntities = lists[typeItem]
		navboxArgs['group' .. count] = makeItemLink( typeItem )
		local navboxListArgs = {}
		for _, lowerEntity in pairs( lowerEntities ) do
			table.insert( navboxListArgs, '*' .. makeEntityLink( lowerEntity ) )
		end
		navboxArgs['list' .. count] = table.concat( navboxListArgs, '\n' )
		count = count + 1
	end
	
	-- Comment
	if args.comment ~= nil then
		navboxArgs['list' .. count] = args.comment
	end
	
	-- Below and See also
	local below = ''
	if args.below ~= nil then
		below = args.below
	end
	local seeAlsoUpper = tonumber( args['see-also-upper'] )
	if seeAlsoUpper ~= nil then
		local seeAlsoUpperLinks = {}
		for _, upperEntity in pairs( findUpperEntities( { entity }, seeAlsoUpper ) ) do
			for _, statement in pairs( upperEntity:getBestStatements( 'P1448' ) ) do
				if statement.mainsnak.datavalue.value.language == 'zh-cn' then
					table.insert( seeAlsoUpperLinks, '[[:' .. ( args['see-also-upper-prefix'] or '' )
						.. statement.mainsnak.datavalue.value.text .. ( args['see-also-upper-suffix'] or '' ) .. ']]' )
					break
				end
			end
		end
		if #seeAlsoUpperLinks > 0 then
			if below ~= '' then
				below = below .. '<br>'
			end
			below = below .. '参见：' .. mw.text.listToText( seeAlsoUpperLinks )
		end
	end
	if below ~= '' then
		navboxArgs.belowstyle = 'text-align: left; font-size: 80%;';
		navboxArgs.below = below;
	end
	
	local border = args.border or frame:getParent().args.border or ''
	if border == 'child' then
		navboxArgs.border = border
		navboxArgs.name = nil
		navboxArgs.title = nil
		navboxArgs.state = nil
		navboxArgs.above = nil
		navboxArgs.below = nil
	end
	
	return frame:expandTemplate{
		title = 'Template:Navbox',
		args = navboxArgs
	}
end

-- Specify a division with item=Qxxx or defaults to current article
function z.children( frame, args )
	if args == nil then
		args = frame.args
	end
	local item = ''
	if args.item ~= nil and args.item ~= '' then
		item = args.item
	end
	local entity = mw.wikibase.getEntity( item )
	if entity == nil then
		return ''
	end
	
	-- Children lists
	local list = {}
	local lowerStatements = entity:getBestStatements( 'P150' )
	for i, lowerStatement in pairs( lowerStatements ) do
		lowerStatement._entity = mw.wikibase.getEntity( 'Q' .. lowerStatement.mainsnak.datavalue.value['numeric-id'] )
		lowerStatement._code = 'X'
		for _, codeStatement in pairs( lowerStatement._entity:getBestStatements( 'P442' ) ) do
			if codeStatement.mainsnak.datavalue.value < lowerStatement._code then
				lowerStatement._code = codeStatement.mainsnak.datavalue.value
			end
		end
	end
	table.sort( lowerStatements, function( a, b )
		return a._code < b._code;
	end )
	for _, lowerStatement in pairs( lowerStatements ) do
		local lowerEntity = lowerStatement._entity
		table.insert( list, makeEntityLink( lowerEntity ) )
	end
	
	return mw.text.listToText( list )
end

return z