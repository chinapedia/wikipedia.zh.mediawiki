--------------------------------------------------------------------------------
--                                                                            --
--                              CATEGORY HANDLER                              --
--                                                                            --
--      This module implements the {{category handler}} template in Lua,      --
--      with a few improvements: all namespaces and all namespace aliases     --
--      are supported, and namespace names are detected automatically for     --
--      the local wiki. This module requires [[Module:Namespace_detect|Module:Namespace detect]]      --
--      and [[Module:Yesno|Module:Yesno]] to be available on the local wiki. It can be     --
--      configured for different wikis by altering the values in              --
--      [[Module:Category_handler/config|Module:Category handler/config]], and pages can be blacklisted      --
--      from categorisation by using [[Module:Category_handler/blacklist|Module:Category handler/blacklist]].   --
--                                                                            --
--------------------------------------------------------------------------------

-- Load required modules
local yesno = require('Module:Yesno')

-- Lazily load things we don't always need
local mShared, mappings

local p = {}

--------------------------------------------------------------------------------
-- Helper functions
--------------------------------------------------------------------------------

local function trimWhitespace(s, removeBlanks)
	if type(s) ~= 'string' then
		return s
	end
	s = s:match('^%s*(.-)%s*$')
	if removeBlanks then
		if s ~= '' then
			return s
		else
			return nil
		end
	else
		return s
	end
end

--------------------------------------------------------------------------------
-- CategoryHandler class
--------------------------------------------------------------------------------

local CategoryHandler = {}
CategoryHandler.__index = CategoryHandler

function CategoryHandler.new(data, args)
	local obj = setmetatable({ _data = data, _args = args }, CategoryHandler)
	
	-- Set the title object
	do
		local pagename = obj:parameter('demopage')
		local success, titleObj
		if pagename then
			success, titleObj = pcall(mw.title.new, pagename)
		end
		if success and titleObj then
			obj.title = titleObj
			if titleObj == mw.title.getCurrentTitle() then
				obj._usesCurrentTitle = true
			end
		else
			obj.title = mw.title.getCurrentTitle()
			obj._usesCurrentTitle = true
		end
	end

	-- Set suppression parameter values
	for _, key in ipairs{'nocat', 'categories'} do
		local value = obj:parameter(key)
		value = trimWhitespace(value, true)
		obj['_' .. key] = yesno(value)
	end
	do
		local subpage = obj:parameter('subpage')
		local category2 = obj:parameter('category2')
		if type(subpage) == 'string' then
			subpage = mw.ustring.lower(subpage)
		end
		if type(category2) == 'string' then
			subpage = mw.ustring.lower(category2)
		end
		obj._subpage = trimWhitespace(subpage, true)
		obj._category2 = trimWhitespace(category2) -- don't remove blank values
	end
	return obj
end

function CategoryHandler:parameter(key)
	local parameterNames = self._data.parameters[key]
	local pntype = type(parameterNames)
	if pntype == 'string' or pntype == 'number' then
		return self._args[parameterNames]
	elseif pntype == 'table' then
		for _, name in ipairs(parameterNames) do
			local value = self._args[name]
			if value ~= nil then
				return value
			end
		end
		return nil
	else
		error(string.format(
			'invalid config key "%s"',
			tostring(key)
		), 2)
	end
end

function CategoryHandler:isSuppressedByArguments()
	return
		-- See if a category suppression argument has been set.
		self._nocat == true
		or self._categories == false
		or (
			self._category2
			and self._category2 ~= self._data.category2Yes
			and self._category2 ~= self._data.category2Negative
		)

		-- Check whether we are on a subpage, and see if categories are
		-- suppressed based on our subpage status.
		or self._subpage == self._data.subpageNo and self.title.isSubpage
		or self._subpage == self._data.subpageOnly and not self.title.isSubpage
end

function CategoryHandler:shouldSkipBlacklistCheck()
	-- Check whether the category suppression arguments indicate we
	-- should skip the blacklist check.
	return self._nocat == false
		or self._categories == true
		or self._category2 == self._data.category2Yes
end

function CategoryHandler:matchesBlacklist()
	if self._usesCurrentTitle then
		return self._data.currentTitleMatchesBlacklist
	else
		mShared = mShared or require('Module:Category handler/shared')
		return mShared.matchesBlacklist(
			self.title.prefixedText,
			mw.loadData('Module:Category handler/blacklist')
		)
	end
end

function CategoryHandler:isSuppressed()
	-- Find if categories are suppressed by either the arguments or by
	-- matching the blacklist.
	return self:isSuppressedByArguments()
		or not self:shouldSkipBlacklistCheck() and self:matchesBlacklist()
end

function CategoryHandler:getNamespaceParameters()
	if self._usesCurrentTitle then
		return self._data.currentTitleNamespaceParameters
	else
		if not mappings then
			mShared = mShared or require('Module:Category handler/shared')
			mappings = mShared.getParamMappings(true) -- gets mappings with mw.loadData
		end
		return mShared.getNamespaceParameters(
			self.title,
			mappings
		)
	end
end

function CategoryHandler:namespaceParametersExist()
	-- Find whether any namespace parameters have been specified.
	-- We use the order "all" --> namespace params --> "other" as this is what
	-- the old template did.
	if self:parameter('all') then
		return true
	end
	if not mappings then
		mShared = mShared or require('Module:Category handler/shared')
		mappings = mShared.getParamMappings(true) -- gets mappings with mw.loadData
	end
	for ns, params in pairs(mappings) do
		for i, param in ipairs(params) do
			if self._args[param] then
				return true
			end
		end
	end
	if self:parameter('other') then
		return true
	end
	return false
end

function CategoryHandler:getCategories()
	local params = self:getNamespaceParameters()
	local nsCategory
	for i, param in ipairs(params) do
		local value = self._args[param]
		if value ~= nil then
			nsCategory = value
			break
		end
	end
	if nsCategory ~= nil or self:namespaceParametersExist() then
		-- Namespace parameters exist - advanced usage.
		if nsCategory == nil then
			nsCategory = self:parameter('other')
		end
		local ret = {self:parameter('all')}
		local numParam = tonumber(nsCategory)
		if numParam and numParam >= 1 and math.floor(numParam) == numParam then
			-- nsCategory is an integer
			ret[#ret + 1] = self._args[numParam]
		else
			ret[#ret + 1] = nsCategory
		end
		if #ret < 1 then
			return nil
		else
			return table.concat(ret)
		end
	elseif self._data.defaultNamespaces[self.title.namespace] then
		-- Namespace parameters don't exist, simple usage.
		return self._args[1]
	end
	return nil
end

--------------------------------------------------------------------------------
-- Exports
--------------------------------------------------------------------------------

local p = {}

function p._exportClasses()
	-- Used for testing purposes.
	return {
		CategoryHandler = CategoryHandler
	}
end

function p._main(args, data)
	data = data or mw.loadData('Module:Category handler/data')
	local handler = CategoryHandler.new(data, args)
	if handler:isSuppressed() then
		return nil
	end
	return handler:getCategories()
end

function p.main(frame, data)
	data = data or mw.loadData('Module:Category handler/data')
	local args = require('Module:Arguments').getArgs(frame, {
		wrappers = data.wrappers,
		valueFunc = function (k, v)
			v = trimWhitespace(v)
			if type(k) == 'number' then
				if v ~= '' then
					return v
				else
					return nil
				end
			else
				return v
			end
		end
	})
	return p._main(args, data)
end

return p