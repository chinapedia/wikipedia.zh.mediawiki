--[==[ This module is a Lua implementation of the old {{Portal}} template. As of August 2013 it is used on nearly 5,000,000 articles.
-- Please take care when updating it! It outputs two functions: p.portal, which generates a list of portals, and p.image, which
-- produces the image name for an individual portal.

-- The portal image data is kept in submodules of [[Module:Portal/images|Module:Portal/images]], listed below:
-- [[Module:Portal/images/letter|Module:Portal/images/letter]]		
-- [[Module:Portal/images/chinese|Module:Portal/images/chinese]]		
-- [[Module:Portal/images/other|Module:Portal/images/other]]	- for portal names beginning with any other letters. This includes numbers,
-- 									  letters with diacritics, and letters in non-Latin alphabets.
-- [[Module:Portal/images/aliases|Module:Portal/images/aliases]]	- for adding aliases for existing portal names. Use this page for variations
-- 									  in spelling and diacritics, etc., no matter what letter the portal begins with.
--
-- The images data pages are separated by the first letter to reduce server load when images are added, changed, or removed.
-- Previously all the images were on one data page at [[Module:Portal/images|Module:Portal/images]], but this had the disadvantage that all
-- 5,000,000 pages using this module needed to be refreshed every time an image was added or removed.
]==]

local p = {}

local function matchImagePage(s)
	-- Finds the appropriate image subpage given a lower-case
	-- portal name plus the first letter of that portal name.
	if type(s) ~= 'string' or #s < 1 then return end
	local firstLetter = mw.ustring.sub(s, 1, 1)
	local imagePage
	if mw.ustring.find(firstLetter, '^[a-z]') then
		imagePage = 'Module:Portal/images/letter'
	else
		imagePage = 'Module:Portal/images/chinese'
	end
	-- Hey, we have a thing called "other"
	return mw.loadData(imagePage)[s] or
		   mw.loadData('Module:Portal/images/other')[s]
end

local function getAlias(s)
	-- Gets an alias from the image alias data page.
	local aliasData = mw.loadData('Module:Portal/images/aliases')
	return aliasData[s]
end

local function getImageName(s)
	-- Gets the image name and the un-aliased "normal name" for a given portal.
	local default = 'Portal-puzzle.svg|link=|alt='
	if type(s) ~= 'string' or #s < 1 then
		return default
	end
	local sl = mw.ustring.lower(s)
	local sr = s
	local img = matchImagePage(sl)
	if not img then
		sr = getAlias(sl)
		if sr then
			img = matchImagePage(mw.ustring.lower(sr))
		end
		if not img then
			img = default
			sr = s
		end
	end
	return img, sr
end

function p._portal(portals, args)
	-- This function builds the portal box used by the {{portal}} template.
	local root = mw.html.create('div')
		:attr('role', 'navigation')
		:attr('aria-label', 'Portals')
		:addClass('noprint portal plainlist')
		:addClass(args.left and 'tleft' or 'tright')
		:css('margin', args.margin or (args.left == 'yes' and '0.5em 1em 0.5em 0') or '0.5em 0 0.5em 1em')
		:css('border', 'solid #aaa 1px')
		:newline()

	-- If no portals have been specified, display an error and add the page to a tracking category.
	if not portals[1] then
		-- zhwp compat: name={{{1}}}|image={{{image1}}}
		-- no tracking needed as no expensive involved
		if args['name'] ~= nil then
			portals[1] = args['name']
			args['image1'] = args['image']
		else
			root:wikitext('<strong class="error">未指定主题：请至少添加一个主题</strong>[[Category:Portal模版没有使用参数|Category:Portal模版没有使用参数]]')
			return tostring(root)
		end
	end

	-- Start the list. This corresponds to the start of the wikitext table in the old [[Template:Portal|Template:Portal]].
	local listroot = root:tag('ul')
		:css('display', 'table')
		:css('box-sizing', 'border-box')
		:css('padding', '0.1em')
		:css('max-width', '175px')
		:css('width', type(args.boxsize) == 'string' and (args.boxsize .. 'px') or nil)
		:css('background', '#f9f9f9')
		:css('font-size', '85%')
		:css('line-height', '110%')
		:css('font-weight', 'bold')

    -- zhwp compatibility: check for |2= as |image1
    local compat_image1 = false
    if #portals == 2 and (args['image1'] == nil) then
    	local file = portals[2]
    	local parts = mw.text.split(file, '%.')
    	if #parts > 1 then
	    	local ext = (parts[#parts]):lower()
	    	-- likely
	    	if #ext == 3 or #ext == 4 then
	    		local assume_img = (ext == 'png') or (ext == 'jpg') or (ext == 'svg')
	    		-- expensive, hence pre-checks & assumption
	    		if assume_img or mw.title.new(file, 'Media').exists then
		    		args['image1'] = portals[2]
		    		compat_image1 = true
		    		table.remove(portals, 2)
	    		end
			end
		end
	end

	-- Display the portals specified in the positional arguments.
	for i, portal in ipairs(portals) do
		-- Support |image1= |image2= ...
		-- Rationale: [[Template:WPBannerMeta|Template:WPBannerMeta]] usage.
		local image = ''
		if args['image' .. tostring(i)] ~= nil then
			image = args['image' .. tostring(i)] .. '|alt=' .. portal
		else
			-- get the alias too
			image, portal = getImageName(portal)
		end

		-- Generate the html for the image and the portal name.
		listroot
			:newline()
			:tag('li')
				:css('display', 'table-row')
				:tag('span')
					:css('display', 'table-cell')
					:css('padding', '0.2em')
					:css('vertical-align', 'middle')
					:css('text-align', 'center')
					:wikitext(string.format('[[File:%s|32x28px]]', image))
					:done()
				:tag('span')
					:css('display', 'table-cell')
					:css('padding', '0.2em 0.2em 0.2em 0.3em')
					:css('vertical-align', 'middle')
					:wikitext(string.format('[[Portal:%s|%s主题]]', portal, portal))
	end
	local ret = tostring(root)
	if compat_image1 == true then
		ret = ret .. '[[Category:使用2號參數傳遞Portal模板圖像的頁面|Category:使用2號參數傳遞Portal模板圖像的頁面]]'
	end
	return ret
end

function p._image(portals)
	-- Wrapper function to allow getImageName() to be accessed through #invoke.
	local name = getImageName(portals[1])
	return name:match('^(.-)|') or name -- FIXME: use a more elegant way to separate borders etc. from the image name
end

local function getAllImageTables()
	-- Returns an array containing all image subpages (minus aliases) as loaded by mw.loadData.
	local images = {}
	for i, subpage in ipairs{'letter', 'chinese', 'other'} do
		images[i] = mw.loadData('Module:Portal/images/' .. subpage)
	end
	return images
end

function p._displayAll(portals, args)
	-- This function displays all portals that have portal images. This function is for maintenance purposes and should not be used in
	-- articles, for two reasons: 1) there are over 1500 portals with portal images, and 2) the module doesn't record how the portal
	-- names are capitalized, so the portal links may be broken.
	local lang = mw.language.getContentLanguage()
	local count = 1
	for _, imageTable in ipairs(getAllImageTables()) do
		for portal in pairs(imageTable) do
			portals[count] = lang:ucfirst(portal)
			count = count + 1
		end
	end
	return p._portal(portals, args)
end

function p._imageDupes()
	-- This function searches the image subpages to find duplicate images. If duplicate images exist, it is not necessarily a bad thing,
	-- as different portals might just happen to choose the same image. However, this function is helpful in identifying images that
	-- should be moved to a portal alias for ease of maintenance.
	local exists, dupes = {}, {}
	for _, imageTable in ipairs(getAllImageTables()) do
		for portal, image in pairs(imageTable) do
			if not exists[image] then
				exists[image] = portal
			else
				table.insert(dupes, string.format('The image "[[:File:%s|%s]]" is used for both portals "%s" and "%s".', image, image, exists[image], portal))
			end
		end
	end
	if #dupes < 1 then
		return 'No duplicate images found.'
	else
		return 'The following duplicate images were found:\n* ' .. table.concat(dupes, '\n* ')
	end
end

local function processPortalArgs(args)
	-- This function processes a table of arguments and returns two tables: an array of portal names for processing by ipairs, and a table of
	-- the named arguments that specify style options, etc. We need to use ipairs because we want to list all the portals in the order
	-- they were passed to the template, but we also want to be able to deal with positional arguments passed explicitly, for example
	-- {{portal|2=Politics}}. The behaviour of ipairs is undefined if nil values are present, so we need to make sure they are all removed.
	args = type(args) == 'table' and args or {}
	local portals = {}
	local namedArgs = {}
	for k, v in pairs(args) do
		if type(k) == 'number' and type(v) == 'string' then -- Make sure we have no non-string portal names.
			table.insert(portals, k)
		elseif type(k) ~= 'number' then
			namedArgs[k] = v
		end
	end
	table.sort(portals)
	for i, v in ipairs(portals) do
		portals[i] = args[v]
	end
	return portals, namedArgs
end

local function makeWrapper(funcName)
	-- Processes external arguments and sends them to the other functions.
	return function (frame)
		-- If called via #invoke, use the args passed into the invoking
		-- template, or the args passed to #invoke if any exist. Otherwise
		-- assume args are being passed directly in from the debug console
		-- or from another Lua module.
		local origArgs
		if type(frame.getParent) == 'function' then
			origArgs = frame:getParent().args
			for k, v in pairs(frame.args) do
				origArgs = frame.args
				break
			end
		else
			origArgs = frame
		end
		-- Trim whitespace and remove blank arguments.
		local args = {}
		for k, v in pairs(origArgs) do
			if type(v) == 'string' then
				v = mw.text.trim(v)
			end
			if v ~= '' then
				args[k] = v
			end
		end
		return p[funcName](processPortalArgs(args)) -- passes two tables to func: an array of portal names, and a table of named arguments.
	end
end

for _, funcName in ipairs{'portal', 'image', 'imageDupes', 'displayAll'} do
	p[funcName] = makeWrapper('_' .. funcName)
end

return p