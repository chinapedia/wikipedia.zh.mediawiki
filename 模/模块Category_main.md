-- This module implements {{category main}}.

local mHatnote = require('Module:Hatnote')
local yesno = require('Module:Yesno')
local mTableTools -- lazily initialise
local mArguments -- lazily initialise

local p = {}

function p.categoryMain(frame)
	mTableTools = require('Module:TableTools')
	mArguments = require('Module:Arguments')
	local args = mArguments.getArgs(frame, {wrappers = 'Template:Category main'})
	local pages = mTableTools.compressSparseArray(args)
	local options = {
		article = args.article,
		selfref = args.selfref
	}
	return p._categoryMain(options, unpack(pages))
end

function p._categoryMain(options, ...)
	options = options or {}

	-- Get the links table.
	local links = mHatnote.formatPages(...)
	if not links[1] then
		local page = mw.title.getCurrentTitle().text
		links[1] = mHatnote._formatLink(page)
	end
	for i, link in ipairs(links) do
		links[i] = string.format("'''%s'''", link)
	end

	-- Get the pagetype.
	local pagetype
	if yesno(options.article) ~= false then
		pagetype = '条目'
	else
		pagetype = '页面'
	end

	-- Work out whether we need to be singular or plural.
	-- 不需要，没有复数。
	local stringToFormat = '此[[Wikipedia:頁面分類|页面分类]]的主%s是%s。'

	-- Get the text.
	local text = string.format(
		stringToFormat,
		pagetype,
		mw.text.listToText(links)
	)
	
	-- Pass it through to Module:Hatnote.
	local hnOptions = {}
	hnOptions.selfref = options.selfref
	hnOptions.extraclasses = 'relarticle mainarticle'

	return mHatnote._hatnote(text, hnOptions)
end

return p