--[=[
-- This module implements {{user}}. {{user}} is a high-use template, sometimes
-- with thousands of transclusions on a page. This module optimises the
-- template's performance by reducing the number of parameters called from
-- wikitext, while still allowing all the features provided by
-- [[Module:UserLinks|Module:UserLinks]]. It is about twice as fast as the version of {{user}}
-- that called the {{user-multi}} template from wikitext.
--]=]

local mUserLinks = require('Module:UserLinks')
local mShared = require('Module:UserLinks/shared')
local yesno = require('Module:Yesno')

local p = {}

local function validateArg(arg)
	-- Validates one argument. Whitespace is stripped, and blank arguments
	-- are treated as nil.
	if not arg then
		return nil
	end
	arg = arg:match('^%s*(.-)%s*$')
	if arg ~= '' then
		return arg
	else
		return nil
	end
end

function p.main(frame)
	-- Grab the user, project and lang args from wikitext.
	local argKeys = {
		user = {
			1,
			'User',
			'user'
		},
		project = {
			2,
			'Project',
			'project'
		},
		lang = {
			3,
			'Lang',
			'lang'
		}
	}
	local origArgs = frame:getParent().args
	local args = {}
	for argKey, t in pairs(argKeys) do
		for i, origArgKey in ipairs(t) do
			local value = origArgs[origArgKey]
			value = validateArg(value)
			if value then
				args[argKey] = value
				-- If we have found a value, break the loop. For the average
				-- invocation this saves two argument lookups.
				break
			end
		end
	end
	
	-- Generate options. Some of these need wikitext args also.
	local options = {
		span = false,
		separator = validateArg(origArgs.separator) or 'dot',
		isDemo = yesno(validateArg(origArgs.demo))
	}
	
	-- Input the codes directly. This saves two argument lookups for each
	-- invocation.
	local codes = {'t', 'c'}
	
	-- Plug the data into [[Module:UserLinks|Module:UserLinks]].
	local snippets = mUserLinks.getSnippets(args)
	local links = mUserLinks.getLinks(snippets)
	local success, result = pcall(mUserLinks.export, codes, links, options)
	if success then
		return result
	else
		return mShared.makeWikitextError(result, options.isDemo)
	end
end

return p