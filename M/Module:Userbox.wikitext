-- This module implements {{userbox}}.

local categoryHandler = require('Module:Category handler').main

local p = {}

--------------------------------------------------------------------------------
-- Helper functions
--------------------------------------------------------------------------------

local function checkNum(val, default)
	-- Checks whether a value is a number greater than or equal to zero. If so,
	-- returns it as a number. If not, returns a default value.
	val = tonumber(val)
	if val and val >= 0 then
		return val
	else
		return default
	end
end

local function addSuffix(num, suffix)
	-- Turns a number into a string and adds a suffix.
	if num then
		return tostring(num) .. suffix
	else
		return nil
	end
end

local function checkNumAndAddSuffix(num, default, suffix)
	-- Checks a value with checkNum and adds a suffix.
	num = checkNum(num, default)
	return addSuffix(num, suffix)
end

local function makeCat(cat, sort)
	-- Makes a category link.
	if sort then
		return mw.ustring.format('[[Category:%s|%s]]', cat, sort)
	else
		return mw.ustring.format('[[Category:%s|Category:%s]]', cat)
	end
end

--------------------------------------------------------------------------------
-- Argument processing
--------------------------------------------------------------------------------

local function makeInvokeFunc(funcName)
	return function (frame)
		local origArgs = require('Module:Arguments').getArgs(frame)
		local args = {}
		for k, v in pairs(origArgs) do
			args[k] = v
		end
		return p.main(funcName, args)
	end
end

p.userbox = makeInvokeFunc('_userbox')
p['userbox-2'] = makeInvokeFunc('_userbox-2')
p['userbox-r'] = makeInvokeFunc('_userbox-r')

--------------------------------------------------------------------------------
-- Main functions
--------------------------------------------------------------------------------

function p.main(funcName, args)
	local userboxData = p[funcName](args)
	local userbox = p.render(userboxData)
	local cats = p.categories(args)
	return userbox .. (cats or '')
end

function p._userbox(args)
	-- Does argument processing for {{userbox}}.
	local data = {}

	-- Get div tag values.
	data.float = args.float or 'left'
	local borderWidthNum = checkNum(args['border-width'] or args['border-s'], 1) -- Used to calculate width.
	data.borderWidth = addSuffix(borderWidthNum, 'px')
	data.borderColor = args['border-color'] or args[1] or args['border-c'] or args['id-c'] or '#999'
	data.width = addSuffix(240 - 2 * borderWidthNum, 'px') -- Also used in the table tag.
	data.bodyClass = args.bodyclass

	-- Get table tag values.
	data.backgroundColor = args['info-background'] or args[2] or args['info-c'] or '#eee'

	-- Get info values.
	data.info = args.info or args[4] or "<code>{{{info}}}</code>"
	data.infoTextAlign = args['info-a'] or 'left'
	data.infoFontSize = checkNumAndAddSuffix(args['info-size'] or args['info-s'], 8, 'pt')
	data.infoHeight = checkNumAndAddSuffix(args['logo-height'] or args['id-h'], 45, 'px')
	data.infoPadding = args['info-padding'] or args['info-p'] or '0 4px 0 4px'
	data.infoLineHeight = args['info-line-height'] or args['info-lh'] or '1.25em'
	data.infoColor = args['info-color'] or args['info-fc'] or 'black'
	data.infoOtherParams = args['info-other-param'] or args['info-op']
	data.infoClass = args['info-class']

	-- Get id values.
	local id = args.logo or args[3] or args.id
	data.id = id
	data.showId = id and true or false
	data.idWidth = checkNumAndAddSuffix(args['logo-width'] or args['id-w'], 45, 'px')
	data.idHeight = checkNumAndAddSuffix(args['logo-height'] or args['id-h'], 45, 'px')
	data.idBackgroundColor = args['logo-background'] or args[1] or args['id-c'] or '#ddd'
	data.idTextAlign = args['id-a'] or 'center'
	data.idFontSize = checkNumAndAddSuffix(args['logo-size'] or args[5] or args['id-s'], 14, 'pt')
	data.idColor = args['logo-color'] or args['id-fc'] or data.infoColor
	data.idPadding = args['logo-padding'] or args['id-p'] or '0 1px 0 0'
	data.idLineHeight = args['logo-line-height'] or args['id-lh'] or '1.25em'
	data.idOtherParams = args['logo-other-param'] or args['id-op']
	data.idClass = args['id-class']

	return data
end

p['_userbox-2'] = function (args)
	-- Does argument processing for {{userbox-2}}.
	local data = {}

	-- Get div tag values.
	data.float = args.float or 'left'
	local borderWidthNum = checkNum(args[9] or args['border-s'], 1) -- Used to calculate width.
	data.borderWidth = addSuffix(borderWidthNum, 'px')
	data.borderColor = args[1] or args['border-c'] or args['id1-c'] or '#999999'
	data.width = addSuffix(240 - 2 * borderWidthNum, 'px') -- Also used in the table tag.
	data.bodyClass = args.bodyclass

	-- Get table tag values.
	data.backgroundColor = args[2] or args['info-c'] or '#eeeeee'

	-- Get info values.
	data.info = args[4] or args.info or "<code>{{{info}}}</code>"
	data.infoTextAlign = args['info-a'] or 'left'
	data.infoFontSize = checkNumAndAddSuffix(args['info-s'], 8, 'pt')
	data.infoColor = args[8] or args['info-fc'] or 'black'
	data.infoPadding = args['info-p'] or '0 4px 0 4px'
	data.infoLineHeight = args['info-lh'] or '1.25em'
	data.infoOtherParams = args['info-op']

	-- Get id values.
	data.showId = true
	data.id = args.logo or args[3] or args.id1 or 'id1'
	data.idWidth = checkNumAndAddSuffix(args['id1-w'], 45, 'px')
	data.idHeight = checkNumAndAddSuffix(args['id-h'], 45, 'px')
	data.idBackgroundColor = args[1] or args['id1-c'] or '#dddddd'
	data.idTextAlign = 'center'
	data.idFontSize = checkNumAndAddSuffix(args['id1-s'], 14, 'pt')
	data.idLineHeight = args['id1-lh'] or '1.25em'
	data.idColor = args['id1-fc'] or data.infoColor
	data.idPadding = args['id1-p'] or '0 1px 0 0'
	data.idOtherParams = args['id1-op']

	-- Get id2 values.
	data.showId2 = true
	data.id2 = args.logo or args[5] or args.id2 or 'id2'
	data.id2Width = checkNumAndAddSuffix(args['id2-w'], 45, 'px')
	data.id2Height = data.idHeight
	data.id2BackgroundColor = args[7] or args['id2-c'] or args[1] or '#dddddd'
	data.id2TextAlign = 'center'
	data.id2FontSize = checkNumAndAddSuffix(args['id2-s'], 14, 'pt')
	data.id2LineHeight = args['id2-lh'] or '1.25em'
	data.id2Color = args['id2-fc'] or data.infoColor
	data.id2Padding = args['id2-p'] or '0 0 0 1px'
	data.id2OtherParams = args['id2-op']

	return data
end

p['_userbox-r'] = function (args)
	-- Does argument processing for {{userbox-r}}.
	local data = {}

	-- Get div tag values.
	data.float = args.float or 'left'
	local borderWidthNum = checkNum(args['border-width'] or args['border-s'], 1) -- Used to calculate width.
	data.borderWidth = addSuffix(borderWidthNum, 'px')
	data.borderColor = args['border-color'] or args[1] or args['border-c'] or args['id-c'] or '#999'
	data.width = addSuffix(240 - 2 * borderWidthNum, 'px') -- Also used in the table tag.
	data.bodyClass = args.bodyclass
	
	-- Get table tag values.
	data.backgroundColor = args['info-background'] or args[2] or args['info-c'] or '#eee'

	-- Get id values.
	data.showId = false -- We only show id2 in userbox-r.

	-- Get info values.
	data.info = args.info or args[4] or "<code>{{{info}}}</code>"
	data.infoTextAlign = args['info-align'] or args['info-a'] or 'left'
	data.infoFontSize = checkNumAndAddSuffix(args['info-size'] or args['info-s'], 8, 'pt')
	data.infoPadding = args['info-padding'] or args['info-p'] or '0 4px 0 4px'
	data.infoLineHeight = args['info-line-height'] or args['info-lh'] or '1.25em'
	data.infoColor = args['info-color'] or args['info-fc'] or 'black'
	data.infoOtherParams = args['info-other-param'] or args['info-op']
	
	-- Get id2 values.
	data.showId2 = true
	data.id2 = args.logo or args[3] or args.id or 'id'
	data.id2Width = checkNumAndAddSuffix(args['logo-width'] or args['id-w'], 45, 'px')
	data.id2Height = checkNumAndAddSuffix(args['logo-height'] or args['id-h'], 45, 'px')
	data.id2BackgroundColor = args['logo-background'] or args[1] or args['id-c'] or '#ddd'
	data.id2TextAlign = args['id-a'] or 'center'
	data.id2FontSize = checkNumAndAddSuffix(args['logo-size'] or args[5] or args['id-s'], 14, 'pt')
	data.id2Color = args['logo-color'] or args['id-fc'] or data.infoColor
	data.id2Padding = args['logo-padding'] or args['id-p'] or '0 0 0 1px'
	data.id2LineHeight = args['logo-line-height'] or args['id-lh'] or '1.25em'
	data.id2OtherParams = args['logo-other-param'] or args['id-op']

	return data
end

function p.render(data)
	-- Renders the userbox html using the content of the data table. 
	-- Render the div tag html.
	local root = mw.html.create('div')
	root
		:css('float', data.float)
		:css('border', (data.borderWidth or '') .. ' solid ' .. (data.borderColor or ''))
		:css('margin', '1px')
		:css('width', data.width)
		:addClass('wikipediauserbox')
		:addClass(data.bodyClass)

	-- Render the table tag html.
	local tableroot = root:tag('table')
	tableroot
		:attr('role', 'presentation')
		:css('border-collapse', 'collapse')
		:css('width', data.width)
		:css('margin-bottom', '0')
		:css('margin-top', '0')
		:css('background', data.backgroundColor)
	
	-- Render the id html.
	local tablerow = tableroot:tag('tr')
	if data.showId then
		tablerow:tag('td')
			:css('border', '0')
			:css('width', data.idWidth)
			:css('height', data.idHeight)
			:css('background', data.idBackgroundColor)
			:css('text-align', data.idTextAlign)
			:css('font-size', data.idFontSize)
			:css('font-weight', 'bold')
			:css('color', data.idColor)
			:css('padding', data.idPadding)
			:css('line-height', data.idLineHeight)
			:css('vertical-align', 'middle')
			:cssText(data.idOtherParams)
			:addClass(data.idClass)
			:wikitext(data.id)
	end

	-- Render the info html.
	tablerow:tag('td')
		:css('border', '0')
		:css('text-align', data.infoTextAlign)
		:css('font-size', data.infoFontSize)
		:css('padding', data.infoPadding)
		:css('height', data.infoHeight)
		:css('line-height', data.infoLineHeight)
		:css('color', data.infoColor)
		:css('vertical-align', 'middle')
		:cssText(data.infoOtherParams)
		:addClass(data.infoClass)
		:wikitext(data.info)
	
	-- Render the second id html.
	if data.showId2 then
		tablerow:tag('td')
			:css('border', '0')
			:css('width', data.id2Width)
			:css('height', data.id2Height)
			:css('background', data.id2BackgroundColor)
			:css('text-align', data.id2TextAlign)
			:css('font-size', data.id2FontSize)
			:css('font-weight', 'bold')
			:css('color', data.id2Color)
			:css('padding', data.id2Padding)
			:css('line-height', data.id2LineHeight)
			:css('vertical-align', 'middle')
			:cssText(data.id2OtherParams)
			:wikitext(data.id2)
	end

	local title = mw.title.getCurrentTitle()
	if (title.namespace == 2) and not title.text:match("/") then
		return tostring(root) -- regular user page
	elseif title.namespace == 14 then
		return tostring(root) -- category
	elseif title.isTalkPage then
		return tostring(root) -- talk page
	end

	local legible = true
	local contrast = require('Module:Color contrast')._ratio

	local function has_text(wikitext)
		local function get_alt(text)
			return text:match("|alt=([^|]*)") or ""
		end
	
		wikitext = wikitext:gsub("]]", "|]]")
		wikitext = wikitext:gsub("%[%[%s*[Mm][Ee][Dd][Ii][Aa]%s*:[^|]-(|.-)]]", get_alt)
		wikitext = wikitext:gsub("%[%[%s*[Ii][Mm][Aa][Gg][Ee]%s*:[^|]-(|.-)]]", get_alt)
		wikitext = wikitext:gsub("%[%[%s*[Ff][Ii][Ll][Ee]%s*:[^|]-(|.-)]]", get_alt)
		return mw.text.trim(wikitext) ~= ""
	end

	if contrast { data.infoColor, data.backgroundColor, error = 0 } < 4.5 then
		legible = false
	end

	if data.showId and contrast { data.idColor, data.idBackgroundColor, error = 0 } < 4.5 then
		if has_text(data.id or "") then
			legible = false
		end
	end

	if data.showId2 and contrast { data.id2Color, data.id2BackgroundColor, error = 0 } < 4.5 then
		if has_text(data.id2 or "") then
			legible = false
		end
	end

	if not legible then
		root:wikitext('[[Category:可能难以辨认的用户框模板|Category:可能难以辨认的用户框模板]]')
	end

	return tostring(root)
end

function p.categories(args, page)
	-- Gets categories from [[Module:Category_handler|Module:Category handler]].
	-- The page parameter makes the function act as though the module was being called from that page.
	-- It is included for testing purposes.
	local cats = {}
	cats[#cats + 1] = args.usercategory
	cats[#cats + 1] = args.usercategory2
	cats[#cats + 1] = args.usercategory3
	if #cats > 0 then
		-- Get the title object
		local title
		if page then
			title = mw.title.new(page)
		else
			title = mw.title.getCurrentTitle()
		end
		-- Build category handler arguments.
		local chargs = {}
		chargs.page = page
		chargs.nocat = args.nocat
		chargs.main = '[[Category:未正確放置討論頁模板的頁面|Category:未正確放置討論頁模板的頁面]]'
		if args.notcatsubpages then
			chargs.subpage = 'no'
		end
		-- User namespace.
		local user = ''
		for i, cat in ipairs(cats) do
			user = user .. makeCat(cat)
		end
		chargs.user = user
		-- Template namespace.
		local basepage = title.baseText
		local template = ''
		for i, cat in ipairs(cats) do
			template = template .. makeCat(cat, ' ' .. basepage)
		end
		chargs.template = template
		return categoryHandler(chargs)
	else
		return nil
	end
end

return p