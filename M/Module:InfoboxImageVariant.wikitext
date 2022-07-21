require('Module:No globals')
local infoboxImage = require('Module:InfoboxImage').InfoboxImage
local lc = require('Module:WikitextLC').selective

local getArgs = require('Module:Arguments').getArgs
local p = {}

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	local variety = {'', '-hans', '-hant', '-cn', '-hk', '-mo', '-my', '-sg', '-tw'}
	local varietyHans = {'-hans', '-cn', '-my', '-sg'}
	local varietyHant = {'-hant', '-hk', '-mo', '-tw'}
	local hansIndicator, hantIndicator = false, false
	
	for i, v in ipairs(varietyHans) do
		if args['image' .. v] then
			hansIndicator = true
			break
		end
	end

	for i, v in ipairs(varietyHant) do
		if args['image' .. v] then
			hantIndicator = true
			break
		end
	end

	if hansIndicator and hantIndicator then
		local content = {}

		for i, v in ipairs(variety) do
			if args['image' .. v] then
				content['zh' .. v] = infoboxImage{args = {
					image = args['image' .. v],
					size = args['size' .. v] or args.size,
					maxsize = args['maxsize' .. v] or args.maxsize,
					sizedefault = args['sizedefault' .. v] or args.sizedefault,
					link = args['link' .. v] or args.link,
					title = args['title' .. v] or args.title,
					border = args['border' .. v] or args.border,
					upright = args['upright' .. v] or args.upright,
					thumbtime = args['thumbtime' .. v] or args.thumbtime,
					center = args['center' .. v] or args.center,
					alt = args['alt' .. v] or args.alt,
				} }
			end
		end
	
		return lc(content)
	end
	
	for i, v in ipairs(variety) do
		if args['image' .. v] then
			return infoboxImage{args = {
				image = args['image' .. v],
				size = args['size' .. v] or args.size,
				maxsize = args['maxsize' .. v] or args.maxsize,
				sizedefault = args['sizedefault' .. v] or args.sizedefault,
				link = args['link' .. v] or args.link,
				title = args['title' .. v] or args.title,
				border = args['border' .. v] or args.border,
				upright = args['upright' .. v] or args.upright,
				thumbtime = args['thumbtime' .. v] or args.thumbtime,
				center = args['center' .. v] or args.center,
				alt = args['alt' .. v] or args.alt,
			} }
		end
	end

end

return p