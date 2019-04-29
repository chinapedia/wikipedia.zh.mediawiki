-- This module implements {{gallery}}

local p = {}

local templatestyles = 'Template:Gallery/styles.css'

local function trim(s)
	return (mw.ustring.gsub(s, "^%s*(.-)%s*$", "%1"))
end

function p.gallery(frame)
	local origArgs
	-- If called via #invoke, use the args passed into the invoking template.
	-- Otherwise, for testing purposes, assume args are being passed directly in.
	if type(frame.getParent) == 'function' then
		origArgs = frame:getParent().args
	else
		origArgs = frame
	end
    
    -- ParserFunctions considers the empty string to be false, so to preserve the previous 
    -- behavior of {{gallery}}, change any empty arguments to nil, so Lua will consider
    -- them false too.
    local args = {}
    for k, v in pairs(origArgs) do
    	if v ~= '' then
    		args[k] = v
    	end
	end

	local tbl = mw.html.create('table')
    
	if args.state then
		tbl
			:addClass('gallery-mod-collapsible')
			:addClass('collapsible')
			:addClass(args.state)
	end
	
	if args.style then
		tbl:cssText(args.style)
	else
		tbl
			:addClass('gallery-mod')
	end
	
	if args.align then
		if args.align == 'center' then
			tbl
				:addClass('gallery-mod-center')
		else
			tbl:css('float', args.align)
		end
	end
	
	if args.title then
		tbl
			:tag('tr')
				:tag('th')
					:addClass('gallery-mod-title')
					:wikitext(args.title)
	end
	
	local mainCell = tbl:tag('tr'):tag('td')
	
	local imageCount = math.ceil(#args / 2)
	local cellWidth = tonumber(args.cellwidth) or tonumber(args.width) or 180
	local imgHeight = tonumber(args.height) or 180
	local lines = tonumber(args.lines) or 2
	local captionstyle = args.captionstyle
	
    for i = 1, imageCount do
		local img = trim(args[i*2 - 1] or '')
		local caption = trim(args[i*2] or '')
		local imgWidth = tonumber(args['width' .. i]) or tonumber(args.width) or 180
		local alt = args['alt' .. i] or ''
		
		local textWidth
		if cellWidth < 30 then
			textWidth = imgHeight + 27
		else
			textWidth = cellWidth + 7
		end

		if img ~= '' then
			local imgTbl = mainCell:tag('table')
            
			imgTbl
				:css('width', (cellWidth + 20) .. 'px')
				:addClass('gallery-mod-box')
				:tag('tr')
					:tag('td')
						:addClass('thumb')
						:css('height', (imgHeight + 20) .. 'px')
						:wikitext(string.format('[[%s|center]]', img, imgWidth, imgHeight, alt, mw.text.unstrip(caption)))
						:done()
					:done()
				:tag('tr')
					:addClass('gallery-mod-text')
					:tag('td')
						:addClass('core')
						:tag('div')
							:addClass('caption')
							:css('min-height', (0.1 + 1.5*lines) .. 'em')
							:css('width', textWidth .. 'px')
							:cssText(captionstyle)
							:wikitext(caption .. ' ')
		end
	end
    
	if args.footer then
		tbl
			:tag('tr')
				:tag('td')
					:addClass('gallery-mod-footer')
					:wikitext(args.footer)
	end
	if args.perrow then
		tbl:css('width', 8 + (cellWidth + 20 + 6)*tonumber(args.perrow) .. 'px')
	end

	return frame:extensionTag{ name = 'templatestyles', args = { src = templatestyles} } .. tostring(tbl)
end

return p