-- This module implements [[Template:Random_portal_component|Template:Random portal component]]

local p = {}

local mRandom = require('Module:Random')
local currentTitle = mw.title.getCurrentTitle()

local function getRandomNumber(max)
	-- gets a random integer between 1 and max; max defaults to 1
	return mRandom.number{max or 1}
end

local function expandArg(args, key)
	-- Emulate how unspecified template parameters appear in wikitext. If the
	-- specified argument exists, its value is returned, and if not the argument
	-- name is returned inside triple curly braces.
	local val = args[key]
	if val then
		return val
	else
		return string.format('{{{%s}}}', key)
	end
end

local function getPages(args)
	local pages = {}
	pages.root = args.rootpage or currentTitle.prefixedText
	pages.subpage = pages.root .. '/' .. expandArg(args, 'subpage')
	pages.random = pages.subpage .. '/' .. getRandomNumber(args.max)
	pages.footer = 'Template:Box-footer'
	return pages
end

local function tryExpandTemplate(frame, title, args)
	local success, result = pcall(frame.expandTemplate, frame, {title = title, args = args})
	if success then
		return result
	else
		local msg = string.format(
			'<strong class="error">The page "[[%s|%s]]" does not exist.</strong>',
			title
		)
		if mw.title.getCurrentTitle().namespace == 100 then -- is in the portal namespace
			msg = msg .. '[[Category:Portals_needing_attention|Category:Portals needing attention]]'
		end
		return msg
	end
end

local function getHeader(frame, pages, header, template)
	return tryExpandTemplate(
		frame,
		template or pages.root .. '/box-header',
		{header, pages.random}
	)
end

local function getRandomSubpageContent(frame, pages)
	return tryExpandTemplate(
		frame,
		pages.random
	)
end

local function getFooter(frame, pages, link)
	return tryExpandTemplate(
		frame,
		pages.footer,
		{link}
	)
end

function p._main(args, frame)
	frame = frame or mw.getCurrentFrame()
	local pages = getPages(args)

	local ret = {}
	ret[#ret + 1] = getHeader(frame, pages, args.header or 'subpage', args.headertemplate)
	ret[#ret + 1] = getRandomSubpageContent(frame, pages)
	if not args.footer or not args.footer:find('%S') then
		ret[#ret + 1] = '<div style="clear:both;"></div></div>'
	else
		ret[#ret + 1] = getFooter(frame, pages, string.format(
			'[[%s|%s]]',
			pages.subpage,
			expandArg(args, 'footer')
		))
	end

	return table.concat(ret, '\n')
end

function p._nominate(args, frame)
	frame = frame or mw.getCurrentFrame()
	local pages = getPages(args)
	
	local ret = {}
	ret[#ret + 1] = getHeader(frame, pages, expandArg(args, 'header'), args.headertemplate)
	ret[#ret + 1] = getRandomSubpageContent(frame, pages)
	ret[#ret + 1] = getFooter(frame, pages, string.format(
		'[[模块:Random_portal_component/提議/%s|建議]] • [[%s|%s]] ',
		expandArg(args, 'subpage'),
		pages.subpage,
		args.footer or 'Archive'
	))

	return table.concat(ret, '\n')
end

local function makeInvokeFunction(func)
	return function (frame)
		local args = require('Module:Arguments').getArgs(frame, {
			trim = false,
			removeBlanks = false,
			wrappers = {
				'Template:Random portal component',
				'Template:Random portal component with nominate'
			}
		})
		return func(args, frame)
	end
end

p.main = makeInvokeFunction(p._main)
p.nominate = makeInvokeFunction(p._nominate)

return p