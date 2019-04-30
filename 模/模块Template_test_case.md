--[[
   A module for generating test case templates.

   This module incorporates code from the English Wikipedia's "Testcase table"
   module,[1] written by Frietjes [2] with contributions by Mr. Stradivarius [3]
   and Jackmcbarn,[4] and the English Wikipedia's "Testcase rows" module,[5]
   written by Mr. Stradivarius.

   The "Testcase table" and "Testcase rows" modules are released under the
   CC BY-SA 3.0 License [6] and the GFDL.[7]

   License: CC BY-SA 3.0 and the GFDL
   Author: Mr. Stradivarius

   [1] https://en.wikipedia.org/wiki/Module:Testcase_table
   [2] https://en.wikipedia.org/wiki/User:Frietjes
   [3] https://en.wikipedia.org/wiki/User:Mr._Stradivarius
   [4] https://en.wikipedia.org/wiki/User:Jackmcbarn
   [5] https://en.wikipedia.org/wiki/Module:Testcase_rows
   [6] https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License
   [7] https://en.wikipedia.org/wiki/Wikipedia:Text_of_the_GNU_Free_Documentation_License
]]

-- Load required modules
local yesno = require('Module:Yesno')

-- Set constants
local DATA_MODULE = 'Module:Template test case/data'

-------------------------------------------------------------------------------
-- Shared methods
-------------------------------------------------------------------------------

local function message(self, key, ...)
	-- This method is added to classes that need to deal with messages from the
	-- config module.
	local msg = self.cfg.msg[key]
	if select(1, ...) then
		return mw.message.newRawMessage(msg, ...):plain()
	else
		return msg
	end
end

-------------------------------------------------------------------------------
-- Template class
-------------------------------------------------------------------------------

local Template = {}

Template.memoizedMethods = {
	-- Names of methods to be memoized in each object. This table should only
	-- hold methods with no parameters.
	getFullPage = true,
	getName = true,
	makeHeader = true,
	getOutput = true
}

function Template.new(invocationObj, options)
	local obj = {}

	-- Set input
	for k, v in pairs(options or {}) do
		if not Template[k] then
			obj[k] = v
		end
	end
	obj._invocation = invocationObj

	-- Validate input
	if not obj.template and not obj.title then
		error('no template or title specified', 2)
	end

	-- Memoize expensive method calls
	local memoFuncs = {}
	return setmetatable(obj, {
		__index = function (t, key)
			if Template.memoizedMethods[key] then
				local func = memoFuncs[key]
				if not func then
					local val = Template[key](t)
					func = function () return val end
					memoFuncs[key] = func
				end
				return func
			else
				return Template[key]
			end
		end
	})
end

function Template:getFullPage()
	if self.template then
		local strippedTemplate, hasColon = self.template:gsub('^:', '', 1)
		hasColon = hasColon > 0
		local ns = strippedTemplate:match('^(.-):')
		ns = ns and mw.site.namespaces[ns]
		if ns then
			return strippedTemplate
		elseif hasColon then
			return strippedTemplate -- Main namespace
		else
			return mw.site.namespaces[10].name .. ':' .. strippedTemplate
		end
	else
		return self.title.prefixedText
	end
end

function Template:getName()
	if self.template then
		return self.template
	else
		return require('Module:Template invocation').name(self.title)
	end
end

function Template:makeLink(display)
	if display then
		return string.format('[[:%s|%s]]', self:getFullPage(), display)
	else
		return string.format('[[:%s|:%s]]', self:getFullPage())
	end
end

function Template:makeBraceLink(display)
	display = display or self:getName()
	local link = self:makeLink(display)
	return mw.text.nowiki('{{') .. link .. mw.text.nowiki('}}')
end

function Template:makeHeader()
	return self.heading or self:makeBraceLink()
end

function Template:getInvocation(format)
	local invocation = self._invocation:getInvocation{
		template = self:getName(),
		requireMagicWord = self.requireMagicWord,
	}
	if format == 'code' then
		invocation = '<code>' .. mw.text.nowiki(invocation) .. '</code>'
	elseif format == 'plain' then
		invocation = mw.text.nowiki(invocation)
	else
		-- Default is pre tags
		invocation = mw.text.encode(invocation, '&')
		invocation = '<pre style="white-space: pre-wrap;">' .. invocation .. '</pre>'
		invocation = mw.getCurrentFrame():preprocess(invocation)
	end
	return invocation
end

function Template:getOutput()
	return self._invocation:getOutput{
		template = self:getName(),
		requireMagicWord = self.requireMagicWord,
	}
end

-------------------------------------------------------------------------------
-- TestCase class
-------------------------------------------------------------------------------

local TestCase = {}
TestCase.__index = TestCase
TestCase.message = message -- add the message method

TestCase.renderMethods = {
	-- Keys in this table are values of the "format" option, values are the
	-- method for rendering that format.
	columns = 'renderColumns',
	rows = 'renderRows',
	inline = 'renderInline',
	default = 'renderDefault'
}

function TestCase.new(invocationObj, options, cfg)
	local obj = setmetatable({}, TestCase)
	obj.cfg = cfg

	-- Separate general options from template options. Template options are
	-- numbered, whereas general options are not.
	local generalOptions, templateOptions = {}, {}
	for k, v in pairs(options) do
		local prefix, num
		if type(k) == 'string' then
			prefix, num = k:match('^(.-)([1-9][0-9]*)$')
		end
		if prefix then
			num = tonumber(num)
			templateOptions[num] = templateOptions[num] or {}
			templateOptions[num][prefix] = v
		else
			generalOptions[k] = v
		end
	end

	-- Set general options
	generalOptions.showcode = yesno(generalOptions.showcode)
	generalOptions.showheader = yesno(generalOptions.showheader) ~= false
	generalOptions.collapsible = yesno(generalOptions.collapsible)
	obj.options = generalOptions

	-- Preprocess template args
	for num, t in pairs(templateOptions) do
		if t.showtemplate ~= nil then
			t.showtemplate = yesno(t.showtemplate)
		end
	end

	-- Set up first two template options tables, so that if only the
	-- "template3" is specified it isn't made the first template when the
	-- the table options array is compressed.
	templateOptions[1] = templateOptions[1] or {}
	templateOptions[2] = templateOptions[2] or {}

	-- Allow the "template" option to override the "template1" option for
	-- backwards compatibility with [[Module:Testcase_table|Module:Testcase table]].
	if generalOptions.template then
		templateOptions[1].template = generalOptions.template
	end

	-- Add default template options
	if templateOptions[1].template and not templateOptions[2].template then
		templateOptions[2].template = templateOptions[1].template ..
			'/' .. obj.cfg.sandboxSubpage
	end
	if not templateOptions[1].template then
		templateOptions[1].title = mw.title.getCurrentTitle().basePageTitle
	end
	if not templateOptions[2].template then
		templateOptions[2].title = templateOptions[1].title:subPageTitle(
			obj.cfg.sandboxSubpage
		)
	end

	-- Remove template options for any templates where the showtemplate
	-- argument is false. This prevents any output for that template.
	for num, t in pairs(templateOptions) do
		if t.showtemplate == false then
			templateOptions[num] = nil
		end
	end

	-- Check for missing template names.
	for num, t in pairs(templateOptions) do
		if not t.template and not t.title then
			error(obj:message(
				'missing-template-option-error',
				num, num
			), 2)
		end
	end

	-- Compress templateOptions table so we can iterate over it with ipairs.
	templateOptions = (function (t)
		local nums = {}
		for num in pairs(t) do
			nums[#nums + 1] = num
		end
		table.sort(nums)
		local ret = {}
		for i, num in ipairs(nums) do
			ret[i] = t[num]
		end
		return ret
	end)(templateOptions)

	-- Don't require the __TEMPLATENAME__ magic word for nowiki invocations if
	-- there is only one template being output.
	if #templateOptions <= 1 then
		templateOptions[1].requireMagicWord = false
	end

	mw.logObject(templateOptions)

	-- Make the template objects
	obj.templates = {}
	for i, options in ipairs(templateOptions) do
		table.insert(obj.templates, Template.new(invocationObj, options))
	end

	-- Add tracking categories. At the moment we are only tracking templates
	-- that use any "heading" parameters.
	obj.categories = {}
	for k, v in pairs(options) do
		if type(k) == 'string' and k:find('heading') then
			obj.categories['Test cases using heading parameters'] = true
			break
		end
	end

	return obj
end

function TestCase:getTemplateOutput(templateObj)
	local output = templateObj:getOutput()
	if self.options.resetRefs then
		mw.getCurrentFrame():extensionTag('references')
	end
	return output
end

function TestCase:templateOutputIsEqual()
	-- Returns a boolean showing whether all of the template outputs are equal.
	-- The random parts of strip markers (see [[Help:Strip_markers|Help:Strip markers]]) are
	-- removed before comparison. This means a strip marker can contain anything
	-- and still be treated as equal, but it solves the problem of otherwise
	-- identical wikitext not returning as exactly equal.
	local function normaliseOutput(obj)
		local out = obj:getOutput()
		-- Remove the random parts from strip markers.
		out = out:gsub('(%cUNIQ).-(QINU%c)', '%1%2')
		return out
	end
	local firstOutput = normaliseOutput(self.templates[1])
	for i = 2, #self.templates do
		local output = normaliseOutput(self.templates[i])
		if output ~= firstOutput then
			return false
		end
	end
	return true
end

function TestCase:makeCollapsible(s)
	local isEqual = self:templateOutputIsEqual()
	local root = mw.html.create('table')
	root
		:addClass('collapsible')
		:addClass(isEqual and 'collapsed' or nil)
		:css('background-color', 'transparent')
		:css('width', '100%')
		:css('border', 'solid silver 1px')
		:tag('tr')
			:tag('th')
				:css('background-color', isEqual and 'lightgreen' or 'yellow')
				:wikitext(self.options.title or self.templates[1]:makeHeader())
				:done()
			:done()
		:tag('tr')
			:tag('td')
				:newline()
				:wikitext(s)
				:newline()
	return tostring(root)
end

function TestCase:renderColumns()
	local root = mw.html.create()
	if self.options.showcode then
		root
			:wikitext(self.templates[1]:getInvocation())
			:newline()
	end

	local tableroot = root:tag('table')

	if self.options.showheader then
		-- Caption
		tableroot
			:addClass(self.options.class)
			:cssText(self.options.style)
			:tag('caption')
				:wikitext(self.options.caption or self:message('columns-header'))

		-- Headers
		local headerRow = tableroot:tag('tr')
		if self.options.rowheader then
			-- rowheader is correct here. We need to add another th cell if
			-- rowheader is set further down, even if heading0 is missing.
			headerRow:tag('th'):wikitext(self.options.heading0)
		end
		local width
		if #self.templates > 0 then
			width = tostring(math.floor(100 / #self.templates)) .. '%'
		else
			width = '100%'
		end
		for i, obj in ipairs(self.templates) do
			headerRow
				:tag('th')
					:css('width', width)
					:wikitext(obj:makeHeader())
		end
	end

	-- Row header
	local dataRow = tableroot:tag('tr'):css('vertical-align', 'top')
	if self.options.rowheader then
		dataRow:tag('th')
			:attr('scope', 'row')
			:wikitext(self.options.rowheader)
	end
	
	-- Template output
	for i, obj in ipairs(self.templates) do
		dataRow:tag('td')
			:newline()
			:wikitext(self.options.before)
			:wikitext(self:getTemplateOutput(obj))
			:wikitext(self.options.after)
	end
	
	return tostring(root)
end

function TestCase:renderRows()
	local root = mw.html.create()
	if self.options.showcode then
		root
			:wikitext(self.templates[1]:getInvocation())
			:newline()
	end

	local tableroot = root:tag('table')
	tableroot
		:addClass(self.options.class)
		:cssText(self.options.style)

	if self.options.caption then
		tableroot
			:tag('caption')
				:wikitext(self.options.caption)
	end

	for _, obj in ipairs(self.templates) do
		-- Build the row HTML
		if self.options.showheader then
			tableroot:tag('tr'):tag('td')
				:css('text-align', 'center')
				:css('font-weight', 'bold')
				:wikitext(obj:makeHeader())
		end
		tableroot:tag('tr'):tag('td')
			:newline()
			:wikitext(self:getTemplateOutput(obj))
	end

	return tostring(root)
end

function TestCase:renderInline()
	local arrow = mw.language.getContentLanguage():getArrow('forwards')
	local ret = {}
	for i, obj in ipairs(self.templates) do
		local line = {}
		line[#line + 1] = '* '
		if self.options.showcode then
			line[#line + 1] = obj:getInvocation('code')
			line[#line + 1] = ' '
			line[#line + 1] = arrow
			line[#line + 1] = ' '
		end
		line[#line + 1] = self:getTemplateOutput(obj)
		ret[#ret + 1] = table.concat(line)
	end
	return table.concat(ret, '\n')
end

function TestCase:renderDefault()
	local ret = {}
	if self.options.showcode then
		ret[#ret + 1] = self.templates[1]:getInvocation()
	end
	for i, obj in ipairs(self.templates) do
		ret[#ret + 1] = '<div style="clear: both;"></div>'
		if self.options.showheader then
			ret[#ret + 1] = obj:makeHeader()
		end
		ret[#ret + 1] = self:getTemplateOutput(obj)
	end
	return table.concat(ret, '\n\n')
end

function TestCase:__tostring()
	local format = self.options.format
	local method = format and TestCase.renderMethods[format] or 'renderDefault'
	local ret = self[method](self)
	if self.options.collapsible then
		ret = self:makeCollapsible(ret)
	end
	for cat in pairs(self.categories) do
		ret = ret .. string.format('[[Category:%s|Category:%s]]', cat)
	end
	return ret
end

-------------------------------------------------------------------------------
-- Nowiki invocation class
-------------------------------------------------------------------------------

local NowikiInvocation = {}
NowikiInvocation.__index = NowikiInvocation
NowikiInvocation.message = message -- Add the message method

function NowikiInvocation.new(invocation, cfg)
	local obj = setmetatable({}, NowikiInvocation)
	obj.cfg = cfg
	invocation = mw.text.unstrip(invocation)
	-- Decode HTML entities for <, >, and ". This means that HTML entities in
	-- the original code must be escaped as e.g. &lt;, which is unfortunate,
	-- but it is the best we can do as the distinction between <, >, " and <,
	-- >, " is lost during the original nowiki operation.
	invocation = invocation:gsub('<', '<')
	invocation = invocation:gsub('>', '>')
	invocation = invocation:gsub('"', '"')
	obj.invocation = invocation
	return obj
end

function NowikiInvocation:getInvocation(options)
	local template = options.template:gsub('%%', '%%%%') -- Escape "%" with "%%"
	local invocation, count = self.invocation:gsub(
		self.cfg.templateNameMagicWordPattern,
		template
	)
	if options.requireMagicWord ~= false and count < 1 then
		error(self:message(
			'nowiki-magic-word-error',
			self.cfg.templateNameMagicWord
		))
	end
	return invocation
end

function NowikiInvocation:getOutput(options)
	local invocation = self:getInvocation(options)
	return mw.getCurrentFrame():preprocess(invocation)
end

-------------------------------------------------------------------------------
-- Table invocation class
-------------------------------------------------------------------------------

local TableInvocation = {}
TableInvocation.__index = TableInvocation
TableInvocation.message = message -- Add the message method

function TableInvocation.new(invokeArgs, nowikiCode, cfg)
	local obj = setmetatable({}, TableInvocation)
	obj.cfg = cfg
	obj.invokeArgs = invokeArgs
	obj.code = nowikiCode
	return obj
end

function TableInvocation:getInvocation(options)
	if self.code then
		local nowikiObj = NowikiInvocation.new(self.code, self.cfg)
		return nowikiObj:getInvocation(options)
	else
		return require('Module:Template invocation').invocation(
			options.template,
			self.invokeArgs
		)
	end
end

function TableInvocation:getOutput(options)
	return mw.getCurrentFrame():expandTemplate{
		title = options.template,
		args = self.invokeArgs
	}
end

-------------------------------------------------------------------------------
-- Bridge functions
--
-- These functions translate template arguments into forms that can be accepted
-- by the different classes, and return the results.
-------------------------------------------------------------------------------

local bridge = {}

function bridge.table(args, cfg)
	cfg = cfg or mw.loadData(DATA_MODULE)

	local options, invokeArgs = {}, {}
	for k, v in pairs(args) do
		local optionKey = type(k) == 'string' and k:match('^_(.*)$')
		if optionKey then
			if type(v) == 'string' then
				v = v:match('^%s*(.-)%s*$') -- trim whitespace
			end
			if v ~= '' then
				options[optionKey] = v
			end
		else
			invokeArgs[k] = v
		end
	end

	-- Allow passing a nowiki invocation as an option. While this means users
	-- have to pass in the code twice, whitespace is preserved and < etc.
	-- will work as intended.
	local nowikiCode = options.code
	options.code = nil

	local invocationObj = TableInvocation.new(invokeArgs, nowikiCode, cfg)
	local testCaseObj = TestCase.new(invocationObj, options, cfg)
	return tostring(testCaseObj)
end

function bridge.nowiki(args, cfg)
	cfg = cfg or mw.loadData(DATA_MODULE)

	local code = args.code or args[1]
	local invocationObj = NowikiInvocation.new(code, cfg)
	args.code = nil
	args[1] = nil
	-- Assume we want to see the code as we already passed it in.
	args.showcode = args.showcode or true
	local testCaseObj = TestCase.new(invocationObj, args, cfg)
	return tostring(testCaseObj)
end

-------------------------------------------------------------------------------
-- Exports
-------------------------------------------------------------------------------

local p = {}

function p.main(frame, cfg)
	cfg = cfg or mw.loadData(DATA_MODULE)

	-- Load the wrapper config, if any.
	local wrapperConfig
	if frame.getParent then
		local title = frame:getParent():getTitle()
		local template = title:gsub(cfg.sandboxSubpagePattern, '')
		wrapperConfig = cfg.wrappers[template]
	end

	-- Work out the function we will call, use it to generate the config for
	-- Module:Arguments, and use Module:Arguments to find the arguments passed
	-- by the user.
	local func = wrapperConfig and wrapperConfig.func or 'table'
	local userArgs = require('Module:Arguments').getArgs(frame, {
		parentOnly = wrapperConfig,
		frameOnly = not wrapperConfig,
		trim = func ~= 'table',
		removeBlanks = func ~= 'table'
	})

	-- Get default args and build the args table. User-specified args overwrite
	-- default args.
	local defaultArgs = wrapperConfig and wrapperConfig.args or {}
	local args = {}
	for k, v in pairs(defaultArgs) do
		args[k] = v
	end
	for k, v in pairs(userArgs) do
		args[k] = v
	end

	return bridge[func](args, cfg)
end

function p._exportClasses() -- For testing
	return {
		Template = Template,
		TestCase = TestCase,
		NowikiInvocation = NowikiInvocation,
		TableInvocation = TableInvocation
	}
end

return p