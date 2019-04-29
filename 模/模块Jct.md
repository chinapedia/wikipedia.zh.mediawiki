local p = {}

local concat = table.concat
local insert = table.insert
local getArgs = require('Module:Arguments').getArgs -- Import module function to work with passed arguments
local parserModule = require "Module:Road data/parser"
local parser = parserModule.parser

-- Shields
local rdt

local function size(args)
	local state = args.state or args.province or ''
	local type = args.type
	if rdt then
		return 'x17'
	elseif state == 'FL' then
		if type == 'Toll' or type == 'FLTP' or type == 'HEFT' then
			return '20'
		elseif type == 'Both' then
			return '20', 'x20'
		end
	elseif state == 'NY' then
		if type == 'NY 1927' or type == 'NY 1948' or (type == 'Parkway' and args.route == "Robert Moses") or (type == 'CR' and args.county == 'Erie') then
			return '20'
		end
	elseif state == 'AB' then
		if type == 'AB' or type == 'Hwy' or type == '2ndHwy' or type == 'TCH' then
			return '18'
		end
	elseif state == 'NS' and type == 'Hwy' or type == 'TCH' then
		return '18'
	elseif state == 'ON' then
		if type == 'ON' or type == 'Hwy' or type == 'Highway' or type == 'QEW' then
			return '24x22'
		elseif type == 'KLR' then
			return '21'
		else
			local countyTypes = {CH = true, RH = true, District = true, Regional = true, County = true, Municipal = true}
			if countyTypes[type] then
				return '19'
			end
		end
	elseif state == 'QC' then
		if type == 'QC' or type == 'Route' or type == 'A' or type == 'Autoroute' or type == 'TCH' or type == 'ON' then
			return '18'
		end
	elseif state == 'SK' then
		if type == 'Hwy' or type == 'SK' then
			return 'x25'
		end
	end

	return 'x20'
end

local function shield(args, frame)
	if args.noshield then return '' end
	local firstSize, secondSize = size(args)
	local shield, second = parser(args, 'shield')
	if not shield or shield == '' then
		return ''
	elseif type(shield) == 'table' then
		shield, second = shield[1], shield[2]
	end
	local function render(shield, size)
		if frame:callParserFunction('#ifexist', 'Media:' .. shield, '1') ~= '' then
			return string.format("[[File:%s|%spx]]", shield, size)
		else
			args.shielderr = true
			local page = mw.title.getCurrentTitle().prefixedText -- Get transcluding page's title
			return mw.ustring.format("[[Category:Jct模板錯誤|1 %s]]", page)
		end
	end
	local rendered = render(shield, firstSize)
	if second then
		local size = secondSize or firstSize
		rendered = rendered .. render(second, size)
	end
	return rendered
end

-- Links/abbreviations
local function link(args)
	local nolink = args.nolink
	local abbr = parser(args, 'abbr')
	if nolink then
		return abbr
	else
		local link = parser(args, 'link')
		if not link or link == '' then
			return abbr
		else
			return mw.ustring.format("<span class=\"nowrap\">[[%s|%s]]</span>", link, abbr)
		end
	end
end

local function completeLink(args, num)
	local actualLink = link(args)
	if not actualLink then
		local page = mw.title.getCurrentTitle().prefixedText -- Get transcluding page's title
		actualLink = string.format("<span class=\"error\">Invalid type: %s</span>[[Category:Jct模板錯誤|2 %s]]", args.type, page)
	end
	local isTo = args.to
	local prefix
	if num == 1 then
		if isTo then
			prefix = "To "
		else
			prefix = ''
		end
	else
		if isTo then
			prefix = " 至 " -- 对应英文维基的“to”
		else
			prefix = "／"
		end
	end
	local suffix = {}
	local dir = args.dir
	if dir then
		insert(suffix, ' ' .. string.lower(dir))
	end
	local name = args.name
	if name then
		insert(suffix, mw.ustring.format('（%s）', name))
	end
	return prefix .. actualLink .. concat(suffix)
end

local function namedLink(args, num)
	local actualLink = link(args)
	local name = args.name or ''
	local isTo = args.to
	local prefix
	if num == 1 then
		if isTo then
			prefix = "To "
		else
			prefix = ''
		end
	else
		if isTo then
			prefix = " 至 " -- 对应英文维基的“to”
		else
			prefix = " / "
		end
	end
	local suffix = {}
	local dir = args.dir
	if name ~= '' then
		if dir then
			insert(suffix, mw.ustring.format(' (%s %s)', actualLink, dir))
		else
			insert(suffix, mw.ustring.format(' (%s)', actualLink))
		end
	else
		insert(suffix, actualLink)
		if dir then insert(suffix, ' ' .. string.lower(dir)) end
	end
	return prefix .. name .. concat(suffix)
end

local function banners(routes)
	local format = string.format
	local firstRun = {}
	local hasBanner = false
	for k,v in ipairs(routes) do
		local banner
		if v.shield == '' or v.shielderr then
			banner = false
		else
			banner = parser(v, 'banner') or ''
			if banner and banner ~= '' then
				hasBanner = true
			end
		end
		insert(firstRun, banner)
	end
	if not hasBanner then return '' end
	local secondRun = {}
	for k,v in ipairs(routes) do
		local bannerFile = firstRun[k]
		if not bannerFile then

		elseif bannerFile == '' then
			local widthCode = parser(v, 'width') or 'square'
			if type(widthCode) == 'number' then
				insert(secondRun, "[[File:No_image_wide.svg|" .. tostring(widthCode) .. "px]]")
			elseif widthCode == 'square' then
				insert(secondRun, "[[File:No_image_wide.svg|20px]]")
			elseif widthCode == 'expand' then
				local route = v.route
				local width = (#route >= 3) and '25' or '20'
				insert(secondRun, format("[[File:No_image_wide.svg|%spx]]", width))
			elseif widthCode == 'wide' then
				insert(secondRun, "[[File:No_image_wide.svg|25px]]")
			elseif widthCode == 'US1926' then
				insert(secondRun, "[[File:No_image_wide.svg|21px]]")
			elseif widthCode == 'SD' then
				local route = v.route
				local width = (#route >= 3) and '23' or '20'
				insert(secondRun, format("[[File:No_image_wide.svg|%spx]]", width))
			elseif (v.state == 'CA') or (v.type == 'CA') then
				local route = v.route
				local widths = {default = {'20', '25'}, I = {'20', '24'}, US = {'20', '23'}, SR = {'19', '22'}}
				local width = widths[widthCode] or widths.default
				local pixels = (#route >= 3) and width[2] or width[1]
				insert(secondRun, format("[[File:No_image_wide.svg|%spx]]", pixels))
			end
		else
			local widthCode = parser(v, 'width') or 'square'
			if widthCode == 'square' then
				insert(secondRun, format("[[File:%s|20px]]", bannerFile))
			elseif widthCode == 'expand' then
				local route = v.route
				if #route >= 3 then
					insert(secondRun, format("[[File:No_image.svg|2px]][[File:%s|20px]][[File:No_image.svg|3px]]", bannerFile))
				else
					insert(secondRun, format("[[File:%s|20px]]", bannerFile))
				end
			elseif widthCode == 'wide' then
				insert(secondRun, format("[[File:No_image.svg|2px]][[File:%s|20px]][[File:No_image.svg|3px]]", bannerFile))
			elseif widthCode == 'SD' then
				local route = v.route
				if #route >= 3 then
					insert(secondRun, format("[[File:No_image.svg|1px]][[File:%s|20px]][[File:No_image.svg|2px]]", bannerFile))
				else
					insert(secondRun, format("[[File:%s|20px]]", bannerFile))
				end
			elseif widthCode == 'MOSupp' then
				local route = v.route
				if #route >= 2 then
					insert(secondRun, format("[[File:No_image.svg|2px]][[File:%s|20px]][[File:No_image.svg|3px]]", bannerFile))
				else
					insert(secondRun, format("[[File:%s|20px]]", bannerFile))
				end
			elseif widthCode == 'US1926' then
				insert(secondRun, format("[[File:%s|20px]][[File:No_image.svg|1px]]", bannerFile))
			elseif v.state == 'CA' then
				local route = v.route
				local type = v.type
				if type == 'US-Bus' then
					if #route >= 3 then
						insert(secondRun, format("[[File:No_image.svg|1px]][[File:%s|20px]][[File:No_image.svg|2px]]", bannerFile))
					else
						insert(secondRun, format("[[File:%s|20px]]", bannerFile))
					end
				elseif type == 'CA-Bus' or type == 'SR-Bus' then
					if #route >= 3 then
						insert(secondRun, format("[[File:No_image.svg|1px]][[File:%s|19px]][[File:No_image.svg|2px]]", bannerFile))
					else
						insert(secondRun, format("[[File:%s|19px]]", bannerFile))
					end
				end
			end
		end
	end
	return concat(secondRun) .. '<br>'
end

local function extra(args)
	local extraTypes = mw.loadData('Module:Road data/extra')
	local extraIcon = extraTypes[string.lower(args.extra or '')]
	if not extraIcon then return '' end
	local countryIcon = extraIcon[args.country] or extraIcon.default
	if type(countryIcon) == 'table' then
		return countryIcon[args.state] or countryIcon.default
	else
		return countryIcon
	end
end

local function parseArgs(args)
	local state = args.state or args.province
	local country
	if args.country then
		country = string.upper(args.country)
	else
		local countryModule = mw.loadData("Module:Road data/countrymask")
		country = countryModule[state] or 'UNK'
		args.country = country
	end
	local params = {'denom', 'county', 'township', 'dab', 'nolink', 'noshield', 'to', 'dir', 'name'}
	local routeArgs = {}
	local routeCount = 1
	while true do
		local routeType = args[routeCount * 2 - 1]
		if not routeType then break end
		local route = {type = routeType, route = args[routeCount * 2]}
		for _,v in pairs(params) do
			route[v] = args[v .. routeCount]
		end
		route.country = country
		route.state = state
		insert(routeArgs, route)
		routeCount = routeCount + 1
	end
	return routeArgs
end

function p._jct(args, frame)
	rdt = args.rdt
	local routes = parseArgs(args)
	local extra = extra(args)
	local shields = {}
	local links = {}
	frame = frame or mw.getCurrentFrame()
	for num,route in ipairs(routes) do
		local routeShield = shield(route, frame)
		insert(shields, routeShield)
		route.shield = routeShield
		if args.jctname then
			insert(links, namedLink(route, num))
		else
			insert(links, completeLink(route, num))
		end
	end
	local bannerText = banners(routes)
	local shieldText = concat(shields)
	local linkText = concat(links)
	local graphics = (not(args.noshield) and (bannerText .. shieldText) or '') .. extra .. ''

	local cities = ''
	if args.city1 or args.location1 then
		local cityModule = require "Module:Jct/city"
		cities = cityModule.city(args)
	end

	local roadStr = ''
	local road = args.road
	if road then
		if args.toroad then
			roadStr = ' to ' .. road
		else
			roadStr = ' / ' .. road
		end
	end

	local output = graphics .. linkText .. roadStr .. cities
	return mw.text.trim(output)
end

function p.jct(frame)
	local args = getArgs(frame)
	return p._jct(args, frame)
end

return p