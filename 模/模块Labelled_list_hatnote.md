--------------------------------------------------------------------------------
--                               Labelled list                                --
--                                                                            --
-- This module does the core work of creating a hatnote composed of a list    --
-- prefixed by a colon-terminated label, i.e. "LABEL: [andList of pages]",    --
-- for {{see also}} and similar templates.                                    --
--------------------------------------------------------------------------------

local mHatnote = require('Module:Hatnote')
local mHatlist = require('Module:Hatnote list')
local mArguments --initialize lazily
local p = {}

-- Defaults global to this module
-- 本地化注意
local defaults = {
	label = '参见', --Final fallback for label argument
	labelForm = '%s：%s',
	prefixes = {'label', 'label ', 'l'},
	template = 'Module:Labelled list hatnote'
}

-- Helper function that pre-combines display parameters into page arguments.
-- Also compresses sparse arrays, as a desirable side-effect.
function p.preprocessDisplays (args, prefixes)
	-- Prefixes specify which parameters, in order, to check for display options
	-- They each have numbers auto-appended, e.g. 'label1', 'label 1', & 'l1'
	prefixes = prefixes or defaults.prefixes
	local pages = {}
	for k, v in pairs(args) do
		if type(k) == 'number' then
			local display
			for i = 1, #prefixes do
				display = args[prefixes[i] .. k]
				if display then break end
			end
			local page = display and
				string.format('%s|%s', string.gsub(v, '|.*$', ''), display) or v
			pages[#pages + 1] = page
		end
	end
	return pages
end

-- Produces a labelled pages-list hatnote.
-- The main frame (template definition) takes 1 or 2 arguments, for a singular
-- and (optionally) plural label respectively:
-- * {{#invoke:Labelled list hatnote|labelledList|Singular label|Plural label}}
-- The resulting template takes pagename & label parameters normally.
function p.labelledList (frame)
	mArguments = require('Module:Arguments')
	local labels = {frame.args[1] or defaults.label}
	labels[2] = frame.args[2] or labels[1]
	local template = frame:getParent():getTitle()
	local args = mArguments.getArgs(frame, {parentOnly = true})
	local pages = p.preprocessDisplays(args)
	local options = {
		extraclasses = frame.args.extraclasses,
		category = args.category,
		selfref = frame.args.selfref or args.selfref,
		template = template
	}
	return p._labelledList(pages, labels, options)
end

function p._labelledList (pages, labels, options)
	labels = labels or {}
	if #pages == 0 then
		-- 本地化注意
		return mHatnote.makeWikitextError(
			'未指定页面名称',
			(options.template or defaults.template) .. '#错误',
			options.category
		)
	end
	label = (#pages == 1 and labels[1] or labels[2]) or defaults.label
	local text = string.format(
		options.labelForm or defaults.labelForm,
		label,
		mHatlist.andList(pages, true)
	)
	local hnOptions = {
		extraclasses = options.extraclasses,
		selfref = options.selfref
	}
	return mHatnote._hatnote(text, hnOptions)
end

return p