local makeUrl = require('Module:URL')._url

local p = {}

-- Wrapper for pcall which returns nil on failure.
local function quickPcall(func)
	local success, result = pcall(func)
	if success then
		return result
	end
end

-- Gets the rank for a Wikidata property table. Returns 1, 0 or -1, in
-- order of rank.
local function getRank(prop)
	local rank = prop.rank
	if rank == 'preferred' then
		return 1
	elseif rank == 'normal' then
		return 0
	elseif rank == 'deprecated' then
		return -1
	else
		-- No rank or undefined rank is treated as "normal".
		return 0
	end
end

-- Finds whether a Wikidata property is qualified as being in Chinese.
local function isChinese(prop)
	local ret = quickPcall(function ()
		for i, lang in ipairs(prop.qualifiers.P407) do
			if lang.datavalue.value['numeric-id'] == 7850 then
				return true
			end
		end
		return false
	end)
	return ret == true
end

-- Fetches the official website URL from Wikidata.
local fetchWikidataUrl
fetchWikidataUrl = function()
	-- Get objects for all official sites on Wikidata.
	local websites = quickPcall(function ()
		return mw.wikibase.getEntityObject().claims.P856
	end)

	-- Clone the objects in case other code needs them in their original order.
	websites = websites and mw.clone(websites) or {}

	-- Add the table index to the objects in case it is needed in the sort.
	for i, website in ipairs(websites) do
		website._index = i
	end

	-- Sort the websites, first by highest rank, and then by websites in the
	-- English language, then by the website's original position in the
	-- property list. When we are done, get the URL from the highest-sorted
	-- object.
	table.sort(websites, function(ws1, ws2)
		local r1 = getRank(ws1)
		local r2 = getRank(ws2)
		if r1 ~= r2 then
			return r1 > r2
		end
		local e1 = isChinese(ws1)
		local e2 = isChinese(ws2)
		if e1 ~= e2 then
			return e1
		end
		return ws1._index < ws2._index
	end)
	local url = quickPcall(function ()
		return websites[1].mainsnak.datavalue.value
	end)

	-- Cache the result so that we only do the heavy lifting once per #invoke.
	fetchWikidataUrl = function ()
		return url
	end

	return url
end

-- Render the URL link, plus other visible output.
local function renderUrl(options)
	if not options.url and not options.wikidataurl then
		return '<strong class="error">' ..
			'找不到URL。请在此处指定URL或在维基数据上添加。' ..
			'</strong>'
	end
	local ret = {}
	ret[#ret + 1] = string.format(
		'<span class="official-website">%s</span>',
		makeUrl(options.url or options.wikidataurl, options.display)
	)
	if options.wikidataurl and not options.url then
		local entity = mw.wikibase.getEntityObject() or {}
		local qid = entity.id
		if qid then
			ret[#ret + 1] = '[[File:Blue_pencil.svg|frameless]]'
		end
	end
	if options.format == 'flash' then
		ret[#ret + 1] = mw.getCurrentFrame():expandTemplate{
			title = 'Link note',
			args = {note = '需要[[Adobe_Flash_Player|Adobe Flash Player]]'}
		}
	end
	if options.mobile then
		ret[#ret + 1] = '（' .. makeUrl(options.mobile, '-{zh-cn:移动端;zh-tw:行動端;zh-hk:流動端;}-') .. '）'
	end
	return table.concat(ret, ' ')
end

-- Render the tracking category.
local function renderTrackingCategory(url, wikidataurl)
	if mw.title.getCurrentTitle().namespace ~= 0 then
		return ''
	end
	local category
	if not url and not wikidataurl then
		category = '官方网站没有URL'
	elseif not url and wikidataurl then
		return ''
	elseif url and wikidataurl then
		if url:gsub('/%s*$', '') ~= wikidataurl:gsub('/%s*$', '') then
			category = '维基百科和维基数据上的官方网站不同'
		end
	else
		category = '维基数据上没有官方网站'
	end
	return category and string.format('[[Category:%s|Category:%s]]', category) or ''
end

function p._main(args)
	local url = args[1] or args.URL or args.url
	local wikidataurl = fetchWikidataUrl()
	local formattedUrl = renderUrl{
		url = url,
		wikidataurl = wikidataurl,
		display = args[2] or args.name or '官方网站',
		format = args.format,
		mobile = args.mobile
	}
	return formattedUrl .. renderTrackingCategory(url, wikidataurl)
end

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {
		wrappers = 'Template:Official website'
	})
	return p._main(args)
end

return p