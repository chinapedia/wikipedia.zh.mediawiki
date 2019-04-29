-- This module implements {{clickable button 2}}.

local yesno = require('Module:Yesno')

local p = {}

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {
		wrappers = 'Template:Clickable button 2'
	})
	return p.luaMain(args)
end

function p.luaMain(args)
	if not args[1] and not args.url then
		return ''
	end
	local data = p.makeLinkData(args)
	local link = p.renderLink(data)
	local trackingCategories = p.renderTrackingCategories(args)
	return link .. trackingCategories
end

function p.makeLinkData(args)
	local data = {}

	-- Get the link and display values, and find whether we are outputting a
	-- wikilink or a URL.
	if args.url then
		data.isUrl = true
		data.link = args.url
		if args[1] then
			data.display = args[1]
		else
			data.display = args.url
		end
	else
		data.isUrl = false
		data.link = args[1]
		if args[2] then
			data.display = args[2]
		else
			data.display = args[1]
		end
	end

	-- Classes
	local class = args.class and args.class:lower()
	data.classes = {}
	if class == 'ui-button-green'
		or class == 'ui-button-blue'
		or class == 'ui-button-red'
	then
		table.insert(
			data.classes,
			'submit ui-button ui-widget ui-state-default ui-corner-all'
				.. ' ui-button-text-only ui-button-text'
		)
	else
		table.insert(data.classes, 'mw-ui-button')
	end
	if class then
		table.insert(data.classes, class)
	end

	-- Styles
	do
		--[[
		-- Check whether we are on the same page as we have specified in
		-- args[1], but not if we are using a URL link, as then args[1] is only
		-- a display value. If we are currently on the page specified in
		-- args[1] make the button colour darker so that it stands out from
		-- other buttons on the page.
		--]]
		local success, linkTitle, currentTitle
		if not data.isUrl then
			currentTitle = mw.title.getCurrentTitle()
			success, linkTitle = pcall(mw.title.new, args[1])
		end
		if success
			and linkTitle
			and mw.title.equals(currentTitle, linkTitle)
		then
			if class == 'ui-button-blue'
				or class == 'mw-ui-progressive'
				or class == 'mw-ui-constructive'
			then
				data.backgroundColor = '#2962CB'
			elseif class == 'ui-button-green' then
				data.backgroundColor = '#008B6D'
			elseif class == 'ui-button-red' or class == 'mw-ui-destructive' then
				data.backgroundColor = '#A6170F'
			else
				data.backgroundColor = '#CCC'
				data.color = '#666'
			end
		end
		-- Add user-specified styles.
		data.style = args.style
	end

	return data
end

function p.renderLink(data)
	-- Render the display span tag.
	local display
	do
		local displaySpan = mw.html.create('span')
		for i, class in ipairs(data.classes or {}) do
			displaySpan:addClass(class)
		end
		displaySpan
			:attr('role', 'button')
			:attr('aria-disabled', 'false')
			:css{
				['background-color'] = data.backgroundColor,
				color = data.color
			}
		if data.style then
			displaySpan:cssText(data.style)
		end
		displaySpan:wikitext(data.display)
		display = tostring(displaySpan)
	end

	-- Render the link
	local link 
	if data.isUrl then
		link = string.format('[%s %s]', data.link, display)
	else
		link = string.format('[[%s|%s]]', data.link, display)
	end

	return string.format('<span class="plainlinks">%s</span>', link)
end

function p.renderTrackingCategories(args)
	if yesno(args.category) == false then
		return ''
	end
	local class = args.class and args.class:lower()
	if class == 'ui-button-green'
		or class == 'ui-button-blue'
		or class == 'ui-button-red'
	then
		return '[[Category:Pages_using_old_style_ui-button-color|Category:Pages using old style ui-button-color]]'
	else
		return ''
	end
end

return p