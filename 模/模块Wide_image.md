-- This module implements [[template:wide_image|template:wide image]] and [[template:panorama|template:panorama]]
local p = {}

local function getfilename(s)
	s = mw.ustring.gsub(s or '', '^%s*[Ff][Ii][Ll][Ee]%s*:%s*', '')
	s = mw.ustring.gsub(s or '', '^%s*[Ii][Mm][Aa][Gg][Ee]%s*:%s*', '')
	return s
end

local function getwidth(s, w, h)
	w = mw.ustring.gsub(w or '0', '^%s*(%d+)%s*[Pp][Xx]*%s*$', '%1')
	h = mw.ustring.gsub(h or '0', '^%s*(%d+)%s*[Pp][Xx]*%s*$', '%1')
	w = tonumber(w) or 0
	h = tonumber(h) or 0
	if w > 0 then
		return w
	end
	
	local file = s and mw.title.new('File:' .. mw.uri.decode(mw.ustring.gsub(s,'%|.*$',''), 'WIKI'))
	file = file and file.file or {width = 0, height = 0}

	if h > 0 then
		w = math.floor(h * (tonumber(file.width) or 0)/(tonumber(file.height) or 1) + 0.5)
		if w > 0 then
			return w
		end
	end
	
	w = tonumber(file.width) or 0
	return w
end

local function getimage(s, w, a, c, rtl)
	if c == 'thumb' or c == 'thumbnail' or c == 'frame' or c == 'border' then
		c = s
	elseif rtl and c ~= '' then
		c = '‪' .. c .. '‬'
	end
	return '[[File:' .. (s or '') .. '|' .. (w or '') .. '|alt=' .. (a or '') 
		.. '|' .. mw.text.unstrip(c or '') .. ']]'
end

local function getcontainers(noborder, float, width, maxwidth)
	local r = mw.html.create('div')
	if noborder then
		if float == 'left' then
			r:addClass('floatleft')
		elseif float == 'right' then
			r:addClass('floatright')
		elseif float == 'none' then
			r:addClass('floatnone')
		else -- center is default
			r:addClass('floatnone')
		r:css('margin', '0 auto')
			r:css('overflow', 'hidden')
		end
	else
		r:addClass('thumb')
		if float == 'left' then
			r:addClass('tleft')
		elseif float == 'right' then
			r:addClass('tright')
		elseif float == 'none' then
			r:addClass('tnone')
		else -- center is default
			r:addClass('tnone')
			r:css('margin', '0 auto')
			r:css('overflow', 'hidden')
		end
	end
	r:css('width', width)
	r:css('max-width', maxwidth)
	local d = noborder and r or r:tag('div'):addClass('thumbinner')
	
	return r,d
end
	
function wideimage(image, width, height, caption, boxwidth, float, alt, border, capalign, dir)
	if image then
		image = getfilename(image)
		local iwidth = getwidth(image, width or '0', height or '0')
		if width == nil then
			width = iwidth .. 'px'
		end
		local maxwidth = noborder and (iwidth .. 'px') or ((iwidth + 8) .. 'px')
		local rtl = dir and dir == 'rtl' or nil
		local noborder = border and border == 'no' or nil
		
		local r,d = getcontainers(noborder, float or '', boxwidth or 'auto', maxwidth)
		
		if tonumber(width) then
			width = width .. 'px'
		end
		
		d:tag('div')
			:addClass('noresize')
			:css('overflow', 'auto')
			:css('direction', rtl and 'rtl' or nil)
			:wikitext(getimage(image,width,alt,caption or '',rtl))
		if caption then
			d = d:tag('div')
					:addClass('thumbcaption')
					:css('text-align', capalign)
			if noborder == nil then
				d:tag('div')
					:addClass('magnify')
					:wikitext('[[:File:'_.._image_.._'|]]')
			end
			d:wikitext(caption)
		end
		return tostring(r)
	end
	return ''
end

function p.main(frame)
	local getArgs = require('Module:Arguments').getArgs
	local args = getArgs(frame)
	return wideimage(
			args['image'] or args[1], args[2] or nil, -- width
			args['height'] or nil, args['caption'] or args[3], 
			args['width'] or args[4], args['align'] or args[5], 
			args['alt'], args['border'], args['align-cap'], args['dir']
			)
end

return p