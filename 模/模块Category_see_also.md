-- This module implements {{Category see also}}

local mHatnote = require('Module:Hatnote')

local p = {}

local function makeWikitextError(msg)
	return string.format(
		'<strong class="error">错误：%s（[[Template:Category_see_also|Template:Category see also]]）</strong>',
		msg
	)
end

-- Gets the length of the sequence seq. Usually this should be done with the #
-- operator, but we need to work with tables that get their values through an
-- __index metamethod.
local function getSequenceLength(seq)
	local length = 0
	for i in ipairs(seq) do
		length = i
	end
	return length
end

-- Given a table of options, returns a function that formats categories for
-- those options.
--
-- Options:
-- project - a project code such as "fr" (for the French Wikipedia)
-- showPrefix - a boolean value for whether to show the "Category:" prefix
--              (and the project prefix if specified)
--
-- This is implemented as a function generator rather than a simple function
-- so that we can just process the options once, instead of every time we
-- generate a category.
local function newCategoryLinker(options)
	local formatString
	if options.project then
		if options.showPrefix then
			formatString = '[[:'_.._options.project_.._':Category:%s|:' .. options.project .. ':Category:%s]]'
		else
			formatString = '[[:'_.._options.project_.._':Category:%s|%s]]'
		end
	else
		if options.showPrefix then
			formatString = '[[:Category:%s|:Category:%s]]'
		else
			formatString = '[[:Category:%s|%s]]'
		end
	end
	return function (category)
		local title = mw.title.new(category)
		local pageName, display
		if not title then
			-- category is not a valid title, usually because of invalid
			-- characters like < or [. Raise an error and suppress the stack
			-- level information so that we can catch it and format the error
			-- message as wikitext.
			error(string.format(
				"“%s”不是有效的分类名",
				category
			), 0)
		elseif title.namespace == 14 then -- Category namespace
			pageName = title.text
			display = title.text
		else
			pageName = title.prefixedText
			display = category
		end
		-- We can get away with using two arguments even when
		-- options.showDisplay is false, as string.format ignores extra
		-- arguments as long as there is an argument for each flag in the
		-- format string.
		return formatString:format(pageName, display)
	end
end

function p._main(args)
	local nLinks = getSequenceLength(args)

	if nLinks < 1 then
		return makeWikitextError('至少需要一个参数')
	end

	local makeCategoryLink = newCategoryLinker{
		project = args.project,
		showPrefix = nLinks == 1,
	}

	local links = {}
	for i, cat in ipairs(args) do
		local success, categoryLink = pcall(makeCategoryLink, cat)
		if success then
			links[i] = categoryLink
		else
			-- If there was an error, then categoryLink is the error message.
			return makeWikitextError(categoryLink)
		end
	end

	local formatString
	if nLinks == 1 then
		formatString = '%s：%s。'
	else
		formatString = '%s分类：%s。'
	end

	-- Don't output a comma before the "and" if we have only two links.
	-- 中文不需要
	local conjunction = '和'

	local hatnoteText = formatString:format(
		args.LABEL or '参见',
		mw.text.listToText(links, '、', conjunction)
	)
	return mHatnote._hatnote(hatnoteText, {selfref = true})
end

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {
		wrappers = 'Template:Category see also',
	})
	return p._main(args)
end

return p