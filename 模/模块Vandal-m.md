-- This module implements {{vandal-m}}.

local p = {}

local su = require('Module:Su')._main

local function makeWikilink(link, display)
	if display then
		return string.format('[[%s|%s]]', link, display)
	else
		return string.format('[[%s|%s]]', link)
	end
end

local function makeUrlLink(data, display)
	local url = mw.uri.new(data)
	url = tostring(url)
	return string.format('[%s %s]', url, display)
end

local function makeFullUrlLink(page, query, display)
	local url = mw.uri.fullUrl(page, query)
	url = tostring(url)
	return string.format('[%s %s]', url, display)
end

local function getTitle(page)
	local success, title = pcall(mw.title.new, page)
	if success then
		return title
	else
		return nil
	end
end

local function getLinkIfExists(pagePrefix, username, display)
	local title = getTitle(pagePrefix .. username)
	if title and title.exists then
		return makeWikilink(title.prefixedText, display)
	end
end

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {parentOnly = true})
	return p._main(args)
end

function p._main(args)
	local username, usernameEncoded
	do
		local lang = mw.language.getContentLanguage()
		username = args.User or args[1] or 'Example'
		username = lang:ucfirst(username)
		usernameEncoded = mw.uri.encode(username)
	end

	local links = {}

	-- Talk
	links[#links + 1] = makeWikilink('User talk:' .. username, 'talk')

	-- Contribs
	links[#links + 1] = makeWikilink(
		'Special:Contributions/' .. username,
		'<span title="Contributions: ' .. username .. '">contribs</span>'
	)

	-- Block log and autoblocks
	do
		local blockLogLink = makeFullUrlLink(
			'Special:Log/block',
			{page = 'User:' .. username},
			'<span title="Blocklog: '
				.. username
				.. '" style="color:#002bb8">block log</span>'
		)
		local autoblocksLink = makeUrlLink(
			{
				host = 'tools.wmflabs.org',
				path = '/xtools/autoblock/',
				query = {user = username}
			},
			'<sup title="Autoblock: '
				.. username
				.. '" style="color:#002bb8">auto</sup>'
		)
		links[#links + 1] = blockLogLink .. autoblocksLink
	end

	-- Ban listing
	if args.ban then
		links[#links + 1] = makeWikilink(
			mw.site.namespaces[4].name .. 'List of banned users#' .. username,
			'ban'
		)
	end

	-- Arbitration requests
	links[#links + 1] = getLinkIfExists(
		'Wikipedia:Requests for arbitration/',
		username,
		'rfarb'
	)

	-- Requests for comment
	links[#links + 1] = getLinkIfExists(
		'Wikipedia:Requests for comment/',
		username,
		'rfcuser'
	)

	-- Long-term abuse
	links[#links + 1] = getLinkIfExists(
		'Wikipedia:Long term abuse/',
		username,
		'lta'
	)

	-- Requests for checkuser
	links[#links + 1] = getLinkIfExists(
		'Wikipedia:Requests for checkuser/Case/',
		username,
		'rfcu'
	)

	-- Sockpuppet investigations
	links[#links + 1] = getLinkIfExists(
		'Wikipedia:Sockpuppet investigations/',
		username,
		'spi'
	)

	-- Suspected sockpuppets
	links[#links + 1] = getLinkIfExists(
		'Wikipedia:Suspected sock puppets/',
		username,
		'ssp'
	)

	-- Sockpuppet categories
	-- There isn't a seperator between these and the suspected sockpuppets link,
	-- so we will add them later instead of adding them to the links table.
	local sockCategoryLinks
	do
		local confirmed = getTitle(
			'Category:Wikipedia sockpuppets of ' .. username
		)
		local suspected = getTitle(
			'Category:Suspected Wikipedia sockpuppets of ' .. username
		)
		if confirmed and confirmed.exists or suspected and suspected.exists then
			local sup, sub
			if confirmed and confirmed.exists then
				sup = ' ' .. makeWikilink(
					':' .. confirmed.prefixedText,
					'confirmed socks'
				)
			end
			if suspected and suspected.exists then
				sub = ' ' .. makeWikilink(
					':' .. suspected.prefixedText,
					'suspected socks'
				)
			end
			sockCategoryLinks = su(sup, sub)
		end
	end

	-- Add the user link and the outer span tags.
	return string.format(
		'<span id="%s" class="plainlinks">%s (%s%s)</span>',
		username,
		makeWikilink('User:' .. username, username),
		table.concat(links, ' • '),
		sockCategoryLinks or ''
	)
end

return p