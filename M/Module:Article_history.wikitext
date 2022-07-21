-------------------------------------------------------------------------------
--                            頁面歷史
--
-- 此模塊允許編者連入頁面歷史的重要事件，
-- 像是優良或特色內容的提名。
-- 它也展示該頁面的現狀以及一樣好的其他訊息，
-- 像是通過的提名之後展示於首頁上的日期。
-------------------------------------------------------------------------------

local CONFIG_PAGE = 'Module:Article history/config'
local WRAPPER_TEMPLATE = 'Template:Article history'
local DEBUG_MODE = false -- If true, errors are not caught.

-- Load required modules.
require('Module:No globals')
local Category = require('Module:Article history/Category')
local yesno = require('Module:Yesno')
local lang = mw.language.getContentLanguage()

-------------------------------------------------------------------------------
-- Helper functions
-------------------------------------------------------------------------------

local function isPositiveInteger(num)
	return type(num) == 'number'
		and math.floor(num) == num
		and num > 0
		and num < math.huge
end

-- lua cannot interpret xxxx年yy月zz日
local function convertDate(dateString)
	for y,m,d in string.gmatch(dateString, "(%d+)年(%d+)月(%d+)日") do
		return y .. "-" .. m .. "-" .. d
	end
end

local function substituteParams(msg, ...)
	return mw.message.newRawMessage(msg, ...):plain()
end

local function makeUrlLink(url, display)
	return string.format('[%s %s]', url, display)
end

local function maybeCallFunc(val, ...)
	-- Checks whether val is a function, and if so calls it with the specified
	-- arguments. Otherwise val is returned as-is.
	if type(val) == 'function' then
		return val(...)
	else
		return val
	end
end

local function renderImage(image, caption, size)
	if caption then
		caption = '|' .. caption
	else
		caption = ''
	end
	return string.format('[[File:%s|%s%s]]', image, size, caption)
end

local function addMixin(class, mixin)
	-- Add a mixin to a class. The functions will be shared across classes, so
	-- don't use it for functions that keep state.
	for name, method in pairs(mixin) do
		class[name] = method
	end
end

-------------------------------------------------------------------------------
-- Message mixin
-- This mixin is used by all classes to add message-related methods.
-------------------------------------------------------------------------------

local Message = {}

function Message:message(key, ...)
	-- This fetches the message from the config with the specified key, and
	-- substitutes parameters $1, $2 etc. with the subsequent values it is
	-- passed.
	local msg = self.cfg.msg[key]
	if select('#', ...) > 0 then
		return substituteParams(msg, ...)
	else
		return msg
	end
end

function Message:raiseError(msg, help)
	-- Raises an error with the specified message and help link. Execution
	-- stops unless the error is caught. This is used for errors where
	-- subsequent processing becomes impossible.
	local errorText
	if help then
		errorText = self:message('error-message-help', msg, help)
	else
		errorText = self:message('error-message-nohelp', msg)
	end
	error(errorText, 0)
end

function Message:addWarning(msg, help)
	-- Adds a warning to the object's warnings table. Execution continues as
	-- normal. This is used for errors that should be fixed but that do not
	-- prevent the module from outputting something useful.
	self.warnings = self.warnings or {}
	local warningText
	if help then
		warningText = self:message('warning-help', msg, help)
	else
		warningText = self:message('warning-nohelp', msg)
	end
	table.insert(self.warnings, warningText)
end

function Message:getWarnings()
	return self.warnings or {}
end

-------------------------------------------------------------------------------
-- Row class
-- This class represents one row in the template.
-------------------------------------------------------------------------------

local Row = {}
Row.__index = Row
addMixin(Row, Message)

function Row.new(data)
	local obj = setmetatable({}, Row)
	obj.cfg = data.cfg
	obj.currentTitle = data.currentTitle
	obj.isSmall = data.isSmall
	obj.makeData = data.makeData -- used by Row:getData
	return obj
end

function Row:_cachedTry(cacheKey, errorCacheKey, func)
	-- This method is for use in Row object methods that are called more than
	-- once. The results of such methods should be cached to avoid unnecessary
	-- processing. We also cache any errors found and abort if an error was
	-- raised previously, otherwise error messages could be displayed multiple
	-- times.
	--
	-- We use false as a key to cache nil results, so func cannot return false.
	--
	-- @param cacheKey The key to cache successful results with
	-- @param errorCacheKey The key to cache errors with
	-- @param func an anonymous function that returns the method result
	if self[errorCacheKey] then
		return nil
	end
	local ret = self[cacheKey]
	if ret then
		return ret
	elseif ret == false then
		return nil
	end
	local success
	if DEBUG_MODE then
		success = true
		ret = func()
	else
		success, ret = pcall(func)
	end
	if success then
		if ret then
			self[cacheKey] = ret
			return ret
		else
			self[cacheKey] = false
			return nil
		end
	else
		self[errorCacheKey] = true
		-- We have already formatted the error message, so no need to format it
		-- again.
		error(ret, 0)
	end
end

function Row:getData(articleHistoryObj)
	return self:_cachedTry('_dataCache', '_isDataError', function ()
		return self.makeData(articleHistoryObj)
	end)
end

function Row:setIconValues(icon, caption, size, smallSize)
	self.icon = icon
	self.iconCaption = caption
	self.iconSize = size
	self.iconSmallSize = smallSize
end

function Row:getIcon(articleHistoryObj)
	return maybeCallFunc(self.icon, articleHistoryObj, self)
end

function Row:getIconCaption(articleHistoryObj)
	return maybeCallFunc(self.iconCaption, articleHistoryObj, self)
end

function Row:getIconSize()
	if self.isSmall then
		return self.iconSmallSize or self.cfg.defaultSmallIconSize or '15px'
	else
		return self.iconSize or self.cfg.defaultIconSize or '30px'
	end
end

function Row:renderIcon(articleHistoryObj)
	local icon = self:getIcon(articleHistoryObj)
	if not icon then
		return nil
	end
	return renderImage(
		icon,
		self:getIconCaption(articleHistoryObj),
		self:getIconSize()
	)
end

function Row:setNoticeBarIconValues(icon, caption, size)
	self.noticeBarIcon = icon
	self.noticeBarIconCaption = caption
	self.noticeBarIconSize = size
end

function Row:getNoticeBarIcon(articleHistoryObj)
	local icon = maybeCallFunc(self.noticeBarIcon, articleHistoryObj, self)
	if icon == true then
		icon = self:getIcon(articleHistoryObj)
		if not icon then
			self:raiseError(
				self:message('row-error-missing-icon'),
				self:message('row-error-missing-icon-help')
			)
		end
	end
	return icon
end

function Row:getNoticeBarIconCaption(articleHistoryObj)
	local caption = maybeCallFunc(
		self.noticeBarIconCaption,
		articleHistoryObj,
		self
	)
	if not caption then
		caption = self:getIconCaption(articleHistoryObj)
	end
	return caption
end

function Row:getNoticeBarIconSize()
	return self.noticeBarIconSize or self.cfg.defaultNoticeBarIconSize or '15px'
end

function Row:exportNoticeBarIcon(articleHistoryObj)
	local icon = self:getNoticeBarIcon(articleHistoryObj)
	if not icon then
		return nil
	end
	return renderImage(
		icon,
		self:getNoticeBarIconCaption(articleHistoryObj),
		self:getNoticeBarIconSize()
	)
end

function Row:setText(text)
	self.text = text
end

function Row:getText(articleHistoryObj)
	return maybeCallFunc(self.text, articleHistoryObj, self)
end

function Row:exportHtml(articleHistoryObj)
	if self._html then
		return self._html
	end
	local text = self:getText(articleHistoryObj)
	if not text then
		return nil
	end
	local html = mw.html.create('tr')
	html
		:tag('td')
			:addClass('mbox-image')
			:wikitext(self:renderIcon(articleHistoryObj))
			:done()
		:tag('td')
			:addClass('mbox-text')
			:wikitext(text)
	self._html = html
	return html
end

function Row:setCategories(val)
	-- Set the categories from the object's config. val can be either an array
	-- of strings or a function returning an array of category objects.
	self.categories = val
end

function Row:getCategories(articleHistoryObj)
	local ret = {}
	if type(self.categories) == 'table' then
		for _, cat in ipairs(self.categories) do
			ret[#ret + 1] = Category.new(cat)
		end
	elseif type(self.categories) == 'function' then
		local t = self.categories(articleHistoryObj, self) or {}
		for _, categoryObj in ipairs(t) do
			ret[#ret + 1] = categoryObj
		end
	end
	return ret
end

-------------------------------------------------------------------------------
-- Status class
-- Status objects deal with possible current statuses of the article.
-------------------------------------------------------------------------------

local Status = setmetatable({}, Row)
Status.__index = Status

function Status.new(data)
	local obj = Row.new(data)
	setmetatable(obj, Status)

	obj.id = data.id
	obj.statusCfg = obj.cfg.statuses[obj.id]
	obj.name = obj.statusCfg.name
	obj:setIconValues(
		obj.statusCfg.icon,
		obj.statusCfg.iconCaption or obj.name,
		data.iconSize
	)
	obj:setNoticeBarIconValues(
		obj.statusCfg.noticeBarIcon,
		obj.statusCfg.noticeBarIconCaption or obj.name,
		obj.statusCfg.noticeBarIconSize
	)
	obj:setText(obj.statusCfg.text)
	obj:setCategories(obj.statusCfg.categories)

	return obj
end

function Status:getIconSize()
	if self.isSmall then
		return self.statusCfg.smallIconSize
			or self.cfg.defaultSmallStatusIconSize
			or '30px'
	else
		return self.iconSize
			or self.statusCfg.iconSize
			or self.cfg.defaultStatusIconSize
			or '50px'
	end
end

function Status:getText(articleHistoryObj)
	local text = Row.getText(self, articleHistoryObj)
	if text then
		return substituteParams(
			text,
			self.currentTitle.subjectPageTitle.prefixedText,
			self.currentTitle.text
		)
	end
end

-------------------------------------------------------------------------------
-- MultiStatus class
-- For when an article can have multiple distinct statuses, e.g. former
-- featured article status and good article status.
-------------------------------------------------------------------------------

local MultiStatus = setmetatable({}, Row)
MultiStatus.__index = MultiStatus

function MultiStatus.new(data)
	local obj = Row.new(data)
	setmetatable(obj, MultiStatus)

	obj.id = data.id
	obj.statusCfg = obj.cfg.statuses[data.id]
	obj.name = obj.statusCfg.name

	-- Set child status objects
	local function getChildStatusData(data, id, iconSize)
		local ret = {}
		for k, v in pairs(data) do
			ret[k] = v
		end
		ret.id = id
		ret.iconSize = iconSize
		return ret
	end
	obj.statuses = {}
	local defaultIconSize = obj.cfg.defaultSmallStatusIconSize or '30px'
	for i, id in ipairs(obj.statusCfg.statuses) do
		table.insert(obj.statuses, Status.new(getChildStatusData(
			data,
			id,
			obj.cfg.statuses[id].iconMultiSize or defaultIconSize
		)))
	end

	return obj
end

function MultiStatus:exportHtml(articleHistoryObj)
	local ret = mw.html.create()
	for i, obj in ipairs(self.statuses) do
		ret:node(obj:exportHtml(articleHistoryObj))
	end
	return ret
end

function MultiStatus:getCategories(articleHistoryObj)
	local ret = {}
	for i, obj in ipairs(self.statuses) do
		for j, categoryObj in ipairs(obj:getCategories(articleHistoryObj)) do
			ret[#ret + 1] = categoryObj
		end
	end
	return ret
end

function MultiStatus:exportNoticeBarIcon()
	local ret = {}
	for i, obj in ipairs(self.statuses) do
		ret[#ret + 1] = obj:exportNoticeBarIcon()
	end
	return table.concat(ret)
end

function MultiStatus:getWarnings()
	local ret = {}
	for i, obj in ipairs(self.statuses) do
		for j, msg in ipairs(obj:getWarnings()) do
			ret[#ret + 1] = msg
		end
	end
	return ret
end

-------------------------------------------------------------------------------
-- Notice class
-- Notice objects contain notices about an article that aren't part of its
-- current status, e.g. the date an article was featured on the main page.
-------------------------------------------------------------------------------

local Notice = setmetatable({}, Row)
Notice.__index = Notice

function Notice.new(data)
	local obj = Row.new(data)
	setmetatable(obj, Notice)

	obj:setIconValues(
		data.icon,
		data.iconCaption,
		data.iconSize,
		data.iconSmallSize
	)
	obj:setNoticeBarIconValues(
		data.noticeBarIcon,
		data.noticeBarIconCaption,
		data.noticeBarIconSize
	)
	obj:setText(data.text)
	obj:setCategories(data.categories)

	return obj
end

-------------------------------------------------------------------------------
-- Action class
-- Action objects deal with a single action in the history of the article. We
-- use getter methods rather than properties for the name and result, etc., as
-- their processing needs to be delayed until after the status object has been
-- initialised. The status object needs to parse the action objects when it is
-- initialised, and the value of some names, etc., in the action objects depend
-- on the status object, so this is necessary to avoid errors/infinite loops.
-------------------------------------------------------------------------------

local Action = setmetatable({}, Row)
Action.__index = Action

function Action.new(data)
	local obj = Row.new(data)
	setmetatable(obj, Action)

	obj.paramNum = data.paramNum

	-- Set the ID
	do
		if not data.code then
			obj:raiseError(
				obj:message('action-error-no-code', obj:getParameter('code')),
				obj:message('action-error-no-code-help')
			)
		end
		local code = mw.ustring.upper(data.code)
		obj.id = obj.cfg.actions[code] and obj.cfg.actions[code].id
		if not obj.id then
			obj:raiseError(
				obj:message(
					'action-error-invalid-code',
					data.code,
					obj:getParameter('code')
				),
				obj:message('action-error-invalid-code-help')
			)
		end
	end

	-- Add a shortcut for this action's config.
	obj.actionCfg = obj.cfg.actions[obj.id]

	-- Set the link
	obj.link = data.link or obj.currentTitle.talkPageTitle.prefixedText

	-- Set the result ID
	do
		local resultCode = data.resultCode
			and mw.ustring.lower(data.resultCode)
			or '_BLANK'
		if obj.actionCfg.results[resultCode] then
			obj.resultId = obj.actionCfg.results[resultCode].id
		elseif resultCode == '_BLANK' then
			obj:raiseError(
				obj:message(
					'action-error-blank-result',
					obj.id,
					obj:getParameter('resultCode')
				),
				obj:message('action-error-blank-result-help')
			)
		else
			obj:raiseError(
				obj:message(
					'action-error-invalid-result',
					data.resultCode,
					obj.id,
					obj:getParameter('resultCode')
				),
				obj:message('action-error-invalid-result-help')
			)
		end
	end

	-- Set the date convertDate
	if data.date then
		local isChineseDate, tempChineseDate = pcall(convertDate, data.date)
		if isChineseDate and tempChineseDate then
			data.date = tempChineseDate
		end
		local success, date = pcall(
			lang.formatDate,
			lang,
			obj:message('action-date-format'),
			data.date
		)
		if success and date then
			obj.date = date
		else
			obj:addWarning(
				obj:message(
					'action-warning-invalid-date',
					data.date,
					obj:getParameter('date')
				),
				obj:message('action-warning-invalid-date-help')
			)
		end
	else
		obj:addWarning(
			obj:message(
				'action-warning-no-date',
				obj.paramNum,
				obj:getParameter('date'),
				obj:getParameter('code')
			),
			obj:message('action-warning-no-date-help')
		)
	end
	obj.date = obj.date or obj:message('action-date-missing')

	-- Set the oldid
	obj.oldid = tonumber(data.oldid)
	if data.oldid and (not obj.oldid or not isPositiveInteger(obj.oldid)) then
		obj.oldid = nil
		obj:addWarning(
			obj:message(
				'action-warning-invalid-oldid',
				data.oldid,
				obj:getParameter('oldid')
			),
			obj:message('action-warning-invalid-oldid-help')
		)
	end

	-- Set the notice bar icon values
	obj:setNoticeBarIconValues(
		data.noticeBarIcon,
		data.noticeBarIconCaption,
		data.noticeBarIconSize
	)

	-- Set the categories
	obj:setCategories(obj.actionCfg.categories)
	
	-- Set ignore action for calculation
	obj.ignore = data.ignore

	return obj
end

function Action:getParameter(key)
	-- Finds the original parameter name for the given key that was passed to
	-- Action.new.
	local prefix = self.cfg.actionParamPrefix
	local suffix
	for k, v in pairs(self.cfg.actionParamSuffixes) do
		if v == key then
			suffix = k
			break
		end
	end
	if not suffix then
		error('invalid key "' .. tostring(key) .. '" passed to Action:getParameter', 2)
	end
	return prefix .. tostring(self.paramNum) .. suffix
end

function Action:getName(articleHistoryObj)
	return maybeCallFunc(self.actionCfg.name, articleHistoryObj, self)
end

function Action:getResult(articleHistoryObj)
	return maybeCallFunc(
		self.actionCfg.results[self.resultId].text,
		articleHistoryObj,
		self
	)
end

function Action:exportHtml(articleHistoryObj)
	if self._html then
		return self._html
	end

	local row = mw.html.create('tr')

	-- Date cell
	local dateCell = row:tag('td')
	if self.oldid then
		dateCell
			:tag('span')
				:addClass('plainlinks')
				:wikitext(makeUrlLink(
					self.currentTitle.subjectPageTitle:fullUrl{oldid = self.oldid},
					self.date
				))
	else
		dateCell:wikitext(self.date)
	end

	-- Process cell
	row
		:tag('td')
			:wikitext(string.format(
				"'''[[%s|%s]]'''",
				self.link,
				self:getName(articleHistoryObj)
			))
	
	-- Result cell
	row
		:tag('td')
			:wikitext(self:getResult(articleHistoryObj))

	self._html = row
	return row
end

-------------------------------------------------------------------------------
-- CollapsibleNotice class
-- This class makes notices that go in the collapsible part of the template,
-- underneath the list of actions.
-------------------------------------------------------------------------------

local CollapsibleNotice = setmetatable({}, Row)
CollapsibleNotice.__index = CollapsibleNotice

function CollapsibleNotice.new(data)
	local obj = Row.new(data)
	setmetatable(obj, CollapsibleNotice)

	obj:setIconValues(
		data.icon,
		data.iconCaption,
		data.iconSize,
		data.iconSmallSize
	)
	obj:setNoticeBarIconValues(
		data.noticeBarIcon,
		data.noticeBarIconCaption,
		data.noticeBarIconSize
	)
	obj:setText(data.text)
	obj:setCollapsibleText(data.collapsibleText)
	obj:setCategories(data.categories)

	return obj
end

function CollapsibleNotice:setCollapsibleText(s)
	self.collapsibleText = s
end

function CollapsibleNotice:getCollapsibleText(articleHistoryObj)
	return maybeCallFunc(self.collapsibleText, articleHistoryObj, self)
end

function CollapsibleNotice:getIconSize()
	if self.isSmall then
		return self.iconSmallSize
			or self.cfg.defaultSmallCollapsibleNoticeIconSize
			or '15px'
	else
		return self.iconSize
			or self.cfg.defaultCollapsibleNoticeIconSize
			or '20px'
	end
end

function CollapsibleNotice:exportHtml(articleHistoryObj, isInCollapsibleTable)
	local cacheKey = isInCollapsibleTable
		and '_htmlCacheCollapsible'
		or '_htmlCacheDefault'
	return self:_cachedTry(cacheKey, '_isHtmlError', function ()
		local text = self:getText(articleHistoryObj)
		if not text then
			return nil
		end

		local function maybeMakeCollapsibleTable(cell, text, collapsibleText)
			-- If collapsible text is specified, makes a collapsible table
			-- inside the cell with two rows, a header row with one cell and a
			-- collapsed row with one cell. These are filled with text and
			-- collapsedText, respectively. If no collapsible text is
			-- specified, the text is added to the cell as-is.
			if collapsibleText then
				cell
					:tag('div')
						:addClass('mw-collapsible mw-collapsed')
						:tag('div')
							:wikitext(text)
							:done()
						:tag('div')
							:addClass('mw-collapsible-content')
							:css('border', '1px silver solid')
							:wikitext(collapsibleText)
			else
				cell:wikitext(text)
			end
		end

		local html = mw.html.create('tr')
		local icon = self:renderIcon(articleHistoryObj)
		local collapsibleText = self:getCollapsibleText(articleHistoryObj)
		if isInCollapsibleTable then
			local textCell = html:tag('td')
				:attr('colspan', 3)
				:css('width', '100%')
			local rowText
			if icon then
				rowText = icon .. ' ' .. text
			else
				rowText = text
			end
			maybeMakeCollapsibleTable(textCell, rowText, collapsibleText)
		else
			local textCell = html
				:tag('td')
					:addClass('mbox-image')
					:wikitext(icon)
					:done()
				:tag('td')
					:addClass('mbox-text')
			maybeMakeCollapsibleTable(textCell, text, collapsibleText)
		end

		return html
	end)
end

-------------------------------------------------------------------------------
-- ArticleHistory class
-- This class represents the whole template.
-------------------------------------------------------------------------------

local ArticleHistory = {}
ArticleHistory.__index = ArticleHistory
addMixin(ArticleHistory, Message)

function ArticleHistory.new(args, cfg, currentTitle)
	local obj = setmetatable({}, ArticleHistory)

	-- Set input
	obj.args = args or {}
	obj.currentTitle = currentTitle or mw.title.getCurrentTitle()

	-- Set isSmall
	obj.isSmall = yesno(obj.args.small) or false

	-- Define object structure.
	obj._errors = {}
	obj._allObjectsCache = {}
	
	-- Format the config
	local function substituteAliases(t, ret)
		-- This function substitutes strings found in an "aliases" subtable
		-- as keys in the parent table. It works recursively, so "aliases"
		-- subtables can be placed at any level. It assumes that tables will
		-- not be nested recursively, which should be true in the case of our
		-- config file.
		ret = ret or {}
		for k, v in pairs(t) do
			if k ~= 'aliases' then
				if type(v) == 'table' then
					local newRet = {}
					ret[k] = newRet
					if v.aliases then
						for _, alias in ipairs(v.aliases) do
							ret[alias] = newRet
						end
					end
					substituteAliases(v, newRet)
				else
					ret[k] = v
				end
			end
		end
		return ret
	end
	obj.cfg = substituteAliases(cfg or require(CONFIG_PAGE))

	--[[
	-- Get a table of the arguments sorted by prefix and number. Non-string
	-- keys and keys that don't contain a number are ignored. (This means that
	-- positional parameters are ignored, as they are numbers, not strings.)
	-- The parameter numbers are stored in the first positional parameter of
	-- the subtables, and any gaps are removed so that the tables can be
	-- iterated over with ipairs.
	--
	-- For example, these arguments:
	--   {a1x = 'eggs', a1y = 'spam', a2x = 'chips', b1z = 'beans', b3x = 'bacon'}
	-- would translate into this prefixArgs table.
	--   {
	--     a = {
	--       {1, x = 'eggs', y = 'spam'},
	--       {2, x = 'chips'}
	--     },
	--     b = {
	--       {1, z = 'beans'},
	--       {3, x = 'bacon'}
	--     }
	--   }
	--]]
	do
		local prefixArgs = {}
		for k, v in pairs(obj.args) do
			if type(k) == 'string' then
				local prefix, num, suffix = k:match('^(.-)([1-9][0-9]*)(.*)$')
				if prefix then
					num = tonumber(num)
					prefixArgs[prefix] = prefixArgs[prefix] or {}
					prefixArgs[prefix][num] = prefixArgs[prefix][num] or {}
					prefixArgs[prefix][num][suffix] = v
					prefixArgs[prefix][num][1] = num
				end
			end
		end
		-- Remove the gaps
		local prefixArrays = {}
		for prefix, prefixTable in pairs(prefixArgs) do
			prefixArrays[prefix] = {}
			local numKeys = {}
			for num in pairs(prefixTable) do
				numKeys[#numKeys + 1] = num
			end
			table.sort(numKeys)
			for _, num in ipairs(numKeys) do
				table.insert(prefixArrays[prefix], prefixTable[num])
			end
		end
		obj.prefixArgs = prefixArrays
	end

	return obj
end

function ArticleHistory:try(func, ...)
	if DEBUG_MODE then
		local val = func(...)
		return val
	else
		local success, val = pcall(func, ...)
		if success then
			return val
		else
			table.insert(self._errors, val)
			return nil
		end
	end
end

function ArticleHistory:getActionObjects()
	-- Gets an array of action objects for the parameters specified by the
	-- user. We memoise this so that the parameters only have to be processed
	-- once.
	if self.actions then
		return self.actions
	end

	-- Get the action args, and exit if they don't exist.
	local actionArgs = self.prefixArgs[self.cfg.actionParamPrefix]
	if not actionArgs then
		self.actions = {}
		return self.actions
	end

	-- Make the objects.
	local actions = {}
	local suffixes = self.cfg.actionParamSuffixes
	for i, t in ipairs(actionArgs) do
		local objArgs = {}
		for k, v in pairs(t) do
			local newK = suffixes[k]
			if newK then
				objArgs[newK] = v
			end
		end
		objArgs.paramNum = t[1]
		objArgs.cfg = self.cfg
		objArgs.currentTitle = self.currentTitle
		local actionObj = self:try(Action.new, objArgs)
		table.insert(actions, actionObj)
	end
	self.actions = actions
	return actions
end

function ArticleHistory:getStatusObj()
	-- Get the status object for the current status.
	if self.statusObj == false then
		return nil
	elseif self.statusObj ~= nil then
		return self.statusObj
	end
	local statusId = self:try(self.cfg.getStatusIdFunction, self)
	if not statusId or statusId == "" then
		self.statusObj = false
		return nil
	elseif not self.cfg.statuses[statusId] then
		self:addWarning(
			self:message('articlehistory-warning-invalid-status'),
			self:message('articlehistory-warning-invalid-status-help')
		)
		self.statusObj = false
		return nil
	end

	-- Check that some actions were specified, and if not add a warning.
	local actions = self:getActionObjects()
	if #actions < 1 then
		self:addWarning(
			self:message('articlehistory-warning-status-no-actions'),
			self:message('articlehistory-warning-status-no-actions-help')
		)
	end

	-- Make a new status object.
	local statusObjData = {
		id = statusId,
		currentTitle = self.currentTitle,
		cfg = self.cfg,
		isSmall = self.isSmall
	}
	local isMulti = self.cfg.statuses[statusId].isMulti
	local initFunc = isMulti and MultiStatus.new or Status.new
	local statusObj = self:try(initFunc, statusObjData)
	self.statusObj = statusObj or false
	return self.statusObj or nil
end

function ArticleHistory:getStatusId()
	local statusObj = self:getStatusObj()
	return statusObj and statusObj.id
end

function ArticleHistory:_noticeFactory(memoizeKey, configKey, class)
	-- This holds the logic for fetching tables of Notice and CollapsibleNotice
	-- objects.
	if self[memoizeKey] then
		return self[memoizeKey]
	end
	local ret = {}
	for i, t in ipairs(self.cfg[configKey] or {}) do
		if t.isActive(self) then
			local data = {}
			for k, v in pairs(t) do
				if k ~= 'isActive' then
					data[k] = v
				end
			end
			data.cfg = self.cfg
			data.currentTitle = self.currentTitle
			data.isSmall = self.isSmall
			ret[#ret + 1] = class.new(data)
		end
	end
	self[memoizeKey] = ret
	return ret
end

function ArticleHistory:getNoticeObjects()
	return self:_noticeFactory('notices', 'notices', Notice)
end

function ArticleHistory:getCollapsibleNoticeObjects()
	return self:_noticeFactory(
		'collapsibleNotices',
		'collapsibleNotices',
		CollapsibleNotice
	)
end

function ArticleHistory:getAllObjects(addSelf)
	local cacheKey = addSelf and 'addSelf' or 'default'
	local ret = self._allObjectsCache[cacheKey]
	if not ret then
		ret = {}
		local statusObj = self:getStatusObj()
		if statusObj then
			ret[#ret + 1] = statusObj
		end
		local objTables = {
			self:getNoticeObjects(),
			self:getActionObjects(),
			self:getCollapsibleNoticeObjects()
		}
		for i, t in ipairs(objTables) do
			for j, obj in ipairs(t) do
				ret[#ret + 1] = obj
			end
		end
		if addSelf then
			ret[#ret + 1] = self
		end
		self._allObjectsCache[cacheKey] = ret
	end
	return ret
end

function ArticleHistory:getNoticeBarIcons()
	local ret = {}
	-- Icons that aren't part of a row.
	if self.cfg.noticeBarIcons then
		for _, data in ipairs(self.cfg.noticeBarIcons) do
			if data.isActive(self) then
				ret[#ret + 1] = renderImage(
					data.icon,
					nil,
					data.size or self.cfg.defaultNoticeBarIconSize
				)
			end
		end
	end
	-- Icons in row objects.
	for _, obj in ipairs(self:getAllObjects()) do
		ret[#ret + 1] = obj:exportNoticeBarIcon(self)
	end
	return ret
end

function ArticleHistory:getErrorMessages()
	-- Returns an array of error/warning strings. Error strings come first.
	local ret = {}
	for _, msg in ipairs(self._errors) do
		ret[#ret + 1] = msg
	end
	for i, obj in ipairs(self:getAllObjects(true)) do
		for j, msg in ipairs(obj:getWarnings()) do
			ret[#ret + 1] = msg
		end
	end
	return ret
end

function ArticleHistory:categoriesAreActive()
	-- Returns a boolean indicating whether categories should be output or not.
	local title = self.currentTitle
	local ns = title.namespace
	return title.isTalkPage
		and ns ~= 3 -- not user talk
		and ns ~= 119 -- not draft talk
end

function ArticleHistory:renderCategories()
	local ret = {}

	if self:categoriesAreActive() then
		-- Child object categories
		for i, obj in ipairs(self:getAllObjects()) do
			local categories = self:try(obj.getCategories, obj, self)
			for j, categoryObj in ipairs(categories or {}) do
				ret[#ret + 1] = tostring(categoryObj)
			end
		end
	
		-- Extra categories
		for i, func in ipairs(self.cfg.extraCategories or {}) do
			local cats = func(self) or {}
			for i, categoryObj in ipairs(cats) do
				ret[#ret + 1] = tostring(categoryObj)
			end
		end
	end

	return table.concat(ret)
end

function ArticleHistory:__tostring()
	local root = mw.html.create()

	-- Table root
	local tableRoot = root:tag('table')
	tableRoot:addClass('tmbox tmbox-notice')
	if self.isSmall then
		tableRoot:addClass('mbox-small')
	else
		tableRoot:css('width', '80%')
	end
	
	-- Status
	local statusObj = self:getStatusObj()
	if statusObj then
		tableRoot:node(self:try(statusObj.exportHtml, statusObj, self))
	end

	-- Notices
	local notices = self:getNoticeObjects()
	for _, noticeObj in ipairs(notices) do
		tableRoot:node(self:try(noticeObj.exportHtml, noticeObj, self))
	end

	-- Get action objects and the collapsible notice objects, and generate the
	-- HTML objects for the action objects. We need the action HTML objects so
	-- that we can accurately calculate the number of collapsible rows, as some
	-- action objects may generate errors when the HTML is generated.
	local actions = self:getActionObjects() or {}
	local collapsibleNotices = self:getCollapsibleNoticeObjects() or {}
	local collapsibleNoticeHtmlObjects, actionHtmlObjects = {}, {}
	for _, obj in ipairs(actions) do
		table.insert(
			actionHtmlObjects,
			self:try(obj.exportHtml, obj, self)
		)
	end
	for _, obj in ipairs(collapsibleNotices) do
		table.insert(
			collapsibleNoticeHtmlObjects,
			self:try(obj.exportHtml, obj, self, true) -- Render the collapsed version
		)
	end
	local nActionRows = #actionHtmlObjects
	local nCollapsibleRows = nActionRows + #collapsibleNoticeHtmlObjects
	
	-- Find out if we are collapsed or not.
	local isCollapsed
	if self.cfg.uncollapsedRows == 'all' then
		isCollapsed = false
	elseif nCollapsibleRows == 1 then
		isCollapsed = false
	else
		isCollapsed = nCollapsibleRows > (tonumber(self.cfg.uncollapsedRows) or 3)
	end

	-- If we are not collapsed, re-render the collapsible notices in the
	-- non-collapsed version.
	if not isCollapsed then
		collapsibleNoticeHtmlObjects = {}
		for _, obj in ipairs(collapsibleNotices) do
			table.insert(
				collapsibleNoticeHtmlObjects,
				self:try(obj.exportHtml, obj, self, false)
			)
		end
	end

	-- Collapsible table for actions and collapsible notices. Collapsible
	-- notices are only included in the table if it is collapsed. Action rows
	-- are always included.
	local collapsibleTable
	if isCollapsed or nActionRows > 0 then
		-- Collapsible table base
		collapsibleTable = tableRoot
			:tag('tr')
				:tag('td')
					:attr('colspan', 2)
					:css('width', '100%')
					:tag('table')
						:addClass('AH-milestones')
						:addClass(isCollapsed and 'mw-collapsible mw-collapsed' or nil)
						:css('width', '100%')
						:css('background', 'transparent')
						:css('font-size', '90%')

		if nCollapsibleRows > 1 then
			-- Header row
			local ctHeader = collapsibleTable
				:tag('tr')
					:tag('th')
						:attr('colspan', 3)
						:css('font-size', '110%')

			-- Notice bar
			if isCollapsed then
				local noticeBarIcons = self:getNoticeBarIcons()
				if #noticeBarIcons > 0 then
					local noticeBar = ctHeader:tag('span'):css('float', 'left')
					for _, icon in ipairs(noticeBarIcons) do
						noticeBar:wikitext(icon)
					end
					ctHeader:wikitext(' ')
				end
			end

			-- Header text
			if mw.site.namespaces[self.currentTitle.namespace].subject.id == 0 then
				ctHeader:wikitext(self:message('milestones-header'))
			else
				ctHeader:wikitext(self:message(
					'milestones-header-other-ns',
					self.currentTitle.subjectNsText
				))
			end
	
			-- Subheadings
			if nActionRows > 0 then
				collapsibleTable
					:tag('tr')
						:css('text-align', 'left')
						:tag('th')
							:wikitext(self:message('milestones-date-header'))
							:done()
						:tag('th')
							:wikitext(self:message('milestones-process-header'))
							:done()
						:tag('th')
							:wikitext(self:message('milestones-result-header'))
			end
		end

		-- Actions
		for _, htmlObj in ipairs(actionHtmlObjects) do
			collapsibleTable:node(htmlObj)
		end
	end
		
	-- Collapsible notices and current status
	-- These are only included in the collapsible table if it is collapsed.
	-- Otherwise, they are added afterwards, so that they align with the
	-- notices.
	do
		local tableNode, statusColspan
		if isCollapsed then
			tableNode = collapsibleTable
			statusColspan = 3
		else
			tableNode = tableRoot
			statusColspan = 2
		end
		
		-- Collapsible notices
		for _, obj in ipairs(collapsibleNotices) do
			tableNode:node(self:try(obj.exportHtml, obj, self, isCollapsed))
		end
		
		-- Current status
		if statusObj and nActionRows > 1 then
			tableNode
				:tag('tr')
					:tag('td')
						:attr('colspan', statusColspan)
						:wikitext(self:message('status-blurb', statusObj.name))
		end
	end

	-- Get the categories. We have to do this before the error row, so that
	-- category errors display.
	local categories = self:renderCategories()

	-- Error row and error category
	local errors = self:getErrorMessages()
	local errorCategory
	if #errors > 0 then
		local errorList = tableRoot
			:tag('tr')
				:tag('td')
					:attr('colspan', 2)
					:addClass('mbox-text')
					:tag('ul')
						:addClass('error')
						:css('font-weight', 'bold')
		for _, msg in ipairs(errors) do
			errorList:tag('li'):wikitext(msg)
		end
		if self:categoriesAreActive() then
			errorCategory = tostring(Category.new(self:message(
				'error-category'
			)))
		end

	-- If there are no errors and no active objects, then exit. We can't make
	-- this check earlier as we don't know where the errors may be until we
	-- have finished rendering the banner.
	elseif #self:getAllObjects() < 1 then
		return ''
	end

	-- Add the categories
	root:wikitext(categories)
	root:wikitext(errorCategory)

	return tostring(root)
end

-------------------------------------------------------------------------------
-- Exports
-- These functions are called from Lua and from wikitext.
-------------------------------------------------------------------------------

local p = {}

function p._main(args, cfg, currentTitle)
	local articleHistoryObj = ArticleHistory.new(args, cfg, currentTitle)
	return tostring(articleHistoryObj)
end

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {
		wrappers = WRAPPER_TEMPLATE
	})
	return p._main(args)
end

function p._exportClasses()
	return {
		Message = Message,
		Row = Row,
		Status = Status,
		MultiStatus = MultiStatus,
		Notice = Notice,
		Action = Action,
		CollapsibleNotice = CollapsibleNotice,
		ArticleHistory = ArticleHistory
	}
end

return p