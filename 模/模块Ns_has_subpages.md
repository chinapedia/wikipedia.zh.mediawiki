-- This module implements [[Template:Ns_has_subpages|Template:Ns has subpages]].
-- While the template is fairly simple, this information is made available to
-- Lua directly, so using a module means that we don't have to update the
-- template as new namespaces are added.

local p = {}

function p._main(ns, frame)
	-- Get the current namespace if we were not passed one.
	if not ns then
		ns = mw.title.getCurrentTitle().namespace
	end

	-- Look up the namespace table from mw.site.namespaces. This should work
	-- for a majority of cases.
	local nsTable = mw.site.namespaces[ns]

	-- Try using string matching to get the namespace from page names.
	-- Do a quick and dirty bad title check to try and make sure we do the same
	-- thing as {{NAMESPACE}} in most cases.
	if not nsTable and type(ns) == 'string' and not ns:find('[<>|%[%]{}]') then
		local nsStripped = ns:gsub('^[_%s]*:', '')
		nsStripped = nsStripped:gsub(':.*$', '')
		nsTable = mw.site.namespaces[nsStripped]
	end

	-- If we still have no match then try the {{NAMESPACE}} parser function,
	-- which should catch the remainder of cases. Don't use a mw.title object,
	-- as this would increment the expensive function count for each new page
	-- tested.
	if not nsTable then
		frame = frame or mw.getCurrentFrame()
		local nsProcessed = frame:callParserFunction('NAMESPACE', ns)
		nsTable = nsProcessed and mw.site.namespaces[nsProcessed]
	end
	
	return nsTable and nsTable.hasSubpages
end

function p.main(frame)
	local ns = frame:getParent().args[1]
	if ns then
		ns = ns:match('^%s*(.-)%s*$') -- trim whitespace
		ns = tonumber(ns) or ns
	end
	local hasSubpages = p._main(ns, frame)
	return hasSubpages and 'yes' or ''
end

return p