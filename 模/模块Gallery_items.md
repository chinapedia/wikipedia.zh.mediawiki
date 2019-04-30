-- this module implements [[template:gallery_items|template:gallery items]]
local p = {}

function p.main(frame)
	local getArgs = require('Module:Arguments').getArgs
	local args = getArgs(frame)

	local width = args.width or '150px'

	local items = {}
	for k, v in pairs(args) do
    	if k ~= nil and tonumber(k) and math.fmod(k,2) == 1 then
    		local i = math.floor(k/2) + 1
    		local item = mw.html.create('li')
    			:addClass('gallerybox')
    			:css('width', args['width' .. k] or width)
    		item:tag('div')
    				:css('width', args['width' .. k] or width)
    				:css('text-align', args['itemalign'] or 'center')
    				:css('margin', '0 auto')
    				:wikitext(args[k])
    		if args[tonumber(k)+1] then
    			item
    				:tag('div')
    				:addClass('gallerytext')
    				:css('width', args['width' .. k] or width)
    				:css('text-align', args['captionalign'] or 'center')
    				:wikitext('<p>' .. args[tonumber(k)+1] .. '<p>')
    		end
    		items[i] = tostring(item) .. ' '
    	end
	end
	local root = mw.html.create('ul')
		:addClass('gallery mw-gallery-nolines nochecker')
		:cssText(args.style)
		:wikitext(table.concat(items))
	
	return frame:extensionTag{ name = 'gallery' } .. tostring(root)
end

return p