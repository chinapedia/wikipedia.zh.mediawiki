-- This module implements {{italic title}}.

require('Module:No globals')
local libraryUtil = require('libraryUtil')
local checkType = libraryUtil.checkType
local checkTypeForNamedArg = libraryUtil.checkTypeForNamedArg
local yesno = require('Module:Yesno')

--------------------------------------------------------------------------------
-- ItalicTitle class
--------------------------------------------------------------------------------

local ItalicTitle = {}

do
	----------------------------------------------------------------------------
	-- Class attributes and functions
	-- Things that belong to the class are here. Things that belong to each
	-- object are in the constructor.
	----------------------------------------------------------------------------

	-- Keys of title parts that can be italicized.
	local italicizableKeys = {
		namespace = true,
		title = true,
		dab = true,
	}

	----------------------------------------------------------------------------
	-- ItalicTitle constructor
	-- This contains all the dynamic attributes and methods.
	----------------------------------------------------------------------------

	function ItalicTitle.new()
		local obj = {}

		-- Function for checking self variable in methods.
		local checkSelf = libraryUtil.makeCheckSelfFunction(
			'ItalicTitle',
			'obj',
			obj,
			'ItalicTitle object'
		)

		-- Checks a key is present in a lookup table.
		-- Param: name - the function name.
		-- Param: argId - integer position of the key in the argument list.
		-- Param: key - the key.
		-- Param: lookupTable - the table to look the key up in.
		local function checkKey(name, argId, key, lookupTable)
			if not lookupTable[key] then
				error(string.format(
					"bad argument #%d to '%s' ('%s' is not a valid key)",
					argId,
					name,
					key
				), 3)
			end
		end

		-- Set up object structure.
		local parsed = false
		local categories = {}
		local italicizedKeys = {}
		local italicizedSubstrings = {}

		-- Parses a title object into its namespace text, title, and
		-- disambiguation text.
		-- Param: options - a table of options with the following keys:
		--     title - the title object to parse
		--     ignoreDab - ignore any disambiguation parentheses
		-- Returns the current object.
		function obj:parseTitle(options)
			checkSelf(self, 'parseTitle')
			checkType('parseTitle', 1, options, 'table')
			checkTypeForNamedArg('parseTitle', 'title', options.title, 'table')
			local title = options.title
		
			-- Title and dab text
			local prefix, parentheses
			if not options.ignoreDab then
				prefix, parentheses = mw.ustring.match(
					title.text,
					'^(.+) %(([^%(%)]+)%)$'
				)
			end
			if prefix and parentheses then
				self.title = prefix
				self.dab = parentheses
			else
				self.title = title.text
			end
		
			-- Namespace
			local namespace = mw.site.namespaces[title.namespace].name
			if namespace and #namespace >= 1 then
				self.namespace = namespace
			end

			-- Register the object as having parsed a title.
			parsed = true
		
			return self
		end

		-- Italicizes part of the title.
		-- Param: key - the key of the title part to be italicized. Possible
		-- keys are contained in the italicizableKeys table.
		-- Returns the current object.
		function obj:italicize(key)
			checkSelf(self, 'italicize')
			checkType('italicize', 1, key, 'string')
			checkKey('italicize', 1, key, italicizableKeys)
			italicizedKeys[key] = true
			return self
		end

		-- Un-italicizes part of the title.
		-- Param: key - the key of the title part to be un-italicized. Possible
		-- keys are contained in the italicizableKeys table.
		-- Returns the current object.
		function obj:unitalicize(key)
			checkSelf(self, 'unitalicize')
			checkType('unitalicize', 1, key, 'string')
			checkKey('unitalicize', 1, key, italicizableKeys)
			italicizedKeys[key] = nil
			return self
		end

		-- Italicizes a substring in the title. This only affects the main part
		-- of the title, not the namespace or the disambiguation text.
		-- Param: s - the substring to be italicized.
		-- Returns the current object.
		function obj:italicizeSubstring(s)
			checkSelf(self, 'italicizeSubstring')
			checkType('italicizeSubstring', 1, s, 'string')
			italicizedSubstrings[s] = true
			return self
		end

		-- Un-italicizes a substring in the title. This only affects the main
		-- part of the title, not the namespace or the disambiguation text.
		-- Param: s - the substring to be un-italicized.
		-- Returns the current object.
		function obj:unitalicizeSubstring(s)
			checkSelf(self, 'unitalicizeSubstring')
			checkType('unitalicizeSubstring', 1, s, 'string')
			italicizedSubstrings[s] = nil
			return self
		end

		-- Renders the object into a page name. If no title has yet been parsed,
		-- the current title is used.
		-- Returns string
		function obj:renderTitle()
			checkSelf(self, 'renderTitle')

			-- Italicizes a string
			-- Param: s - the string to italicize
			-- Returns string.
			local function italicize(s)
				assert(type(s) == 'string', 's was not a string')
				assert(s ~= '', 's was the empty string')
				return string.format('<i>%s</i>', s)
			end
		
			-- Escape characters in a string that are magic in Lua patterns.
			-- Param: pattern - the pattern to escape
			-- Returns string.
			local function escapeMagicCharacters(s)
				assert(type(s) == 'string', 's was not a string')
				return s:gsub('%p', '%%%0')
			end

			-- If a title hasn't been parsed yet, parse the current title.
			if not parsed then
				self:parseTitle{title = mw.title.getCurrentTitle()}
			end

			-- Italicize the different parts of the title and store them in a
			-- titleParts table to be joined together later.
			local titleParts = {}

			-- Italicize the italicizable keys.
			for key in pairs(italicizableKeys) do
				if self[key] then
					if italicizedKeys[key] then
						titleParts[key] = italicize(self[key])
					else
						titleParts[key] = self[key]
					end
				end
			end

			-- Italicize substrings. If there are any substrings to be
			-- italicized then start from the raw title, as this overrides any
			-- italicization of the main part of the title.
			if next(italicizedSubstrings) then
				titleParts.title = self.title
				for s in pairs(italicizedSubstrings) do
					local pattern = escapeMagicCharacters(s)
					local italicizedTitle, nReplacements = titleParts.title:gsub(
						pattern,
						italicize
					)
					titleParts.title = italicizedTitle

					-- If we didn't make any replacements then it means that we
					-- have been passed a bad substring or that the page has
					-- been moved to a bad title, so add a tracking category.
					if nReplacements < 1 then
						categories['Pages using italic title with no matching string'] = true
					end
				end
			end

			-- Assemble the title together from the parts.
			local ret = ''
			if titleParts.namespace then
				ret = ret .. titleParts.namespace .. ':'
			end
			ret = ret .. titleParts.title
			if titleParts.dab then
				ret = ret .. ' (' .. titleParts.dab .. ')'
			end

			return ret
		end

		-- Returns an expanded DISPLAYTITLE parser function called with the
		-- result of obj:renderTitle, plus any other optional arguments.
		-- Returns string
		function obj:renderDisplayTitle(...)
			checkSelf(self, 'renderDisplayTitle')
			return mw.getCurrentFrame():callParserFunction(
				'DISPLAYTITLE',
				self:renderTitle(),
				...
			)
		end

		-- Returns an expanded DISPLAYTITLE parser function called with the
		-- result of obj:renderTitle, plus any other optional arguments, plus
		-- any tracking categories.
		-- Returns string
		function obj:render(...)
			checkSelf(self, 'render')
			local ret = self:renderDisplayTitle(...)
			for cat in pairs(categories) do
				ret = ret .. string.format(
					'[[Category:%s|Category:%s]]',
					cat
				)
			end
			return ret
		end

		return obj
	end
end

--------------------------------------------------------------------------------
-- Exports
--------------------------------------------------------------------------------

local p = {}

local function getArgs(frame, wrapper)
	assert(type(wrapper) == 'string', 'wrapper was not a string')
	return require('Module:Arguments').getArgs(frame, {
		wrappers = wrapper
	})
end

-- Main function for {{italic title}}
function p._main(args)
	checkType('_main', 1, args, 'table')
	local italicTitle = ItalicTitle.new()
	italicTitle:parseTitle{
		title = mw.title.getCurrentTitle(),
		ignoreDab = yesno(args.all, false)
	}
	if args.string then
		italicTitle:italicizeSubstring(args.string)
	else
		italicTitle:italicize('title')
	end
	return italicTitle:render(args[1])
end

function p.main(frame)
	return p._main(getArgs(frame, 'Template:Italic title'))
end

function p._dabonly(args)
	return ItalicTitle.new()
		:italicize('dab')
		:render(args[1])
end

function p.dabonly(frame)
	return p._dabonly(getArgs(frame, 'Template:Italic dab'))
end


return p