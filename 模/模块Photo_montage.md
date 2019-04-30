-- implements [[template:photomontage|template:photomontage]]
local p = {}
 
local function isnotempty(s)
	return s and s:match( '^%s*(.-)%s*$' ) ~= ''
end

local function photomontage( frame )
	local tracking = ''
	local args = frame:getParent().args
	local size = tonumber(args['size'] or '200') or 200
	local border = tonumber(args['border'] or '1') or 1
	local spacing = tonumber(args['spacing'] or '1') or 1
	local color = args['color'] or 'black'
	local color_border = args['color_border'] or 'black'
	local position = (args['position'] or ''):lower()
	local caption = args['text'] or ''
	local text_background = isnotempty(args['text_background']) and args['text_background'] or '#F8F8FF'
	local foot_montage = args['foot_montage'] or ''
	local lastnum = nil
	local rownum = nil
	local floatstyle = nil
	if( position == 'left' or position == 'right' or position == 'none') then
		floatstyle = 'float:' .. position
		tracking = tracking .. '[[Category:Pages_using_photo_montage_without_center_alignment|' .. position .. ']]'
	else
		floatstyle = 'margin-left: auto; margin-right: auto;'
	end
	if isnotempty(foot_montage) then
		local div = mw.html.create('div')
		div:css('font-size', 'smaller')
			:wikitext(foot_montage)
		foot_montage = '\n' .. tostring(div)
	end

	local lettertonumber = { 
		a = '01', b = '02',	c = '03', d = '04',	e = '05', f = '06',	g = '07',
		h = '08', i = '09',	j = '10', k = '11',	l = '12', m = '13',	n = '14',
		o = '15', p = '16',	q = '17', r = '18', s = '19', t = '20', u = '21',
		v = '22', w = '23', x = '26', y = '27', z = '28' }
	local letters = {
		'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm',
		'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'
		}

	-- find all the nonempty photo numbers
	local photos = {}
	local photocount = 0
	for k, v in pairs( args ) do
		local i = tonumber(tostring(k):match( '^%s*photo([%d]+)[a-z]%s*$' ) or '0')
		if( i > 0 and isnotempty(v) ) then
			local c = lettertonumber[tostring(k):match( '^%s*photo[%d]+([a-z])%s*$' )]
			table.insert( photos, tonumber(i .. '.' .. c ) )
			photocount = photocount + 1
		end
	end
	-- sort the photo numbers
	table.sort(photos)
	
	-- compute the number of the photos in each row
	local count = {}
	lastnum = -1
	rownum = 0
	for k=1,photocount do
		local num = math.floor(photos[k])
		if(num == lastnum) then
			count[rownum] = count[rownum] + 1
		else
			rownum = rownum + 1
			count[rownum] = 1
		end
		lastnum = num
	end

	if(photocount > 0) then
	-- start table
	root = mw.html.create('div')
	root
		:css('background-color', color)
		:css('border-collapse', 'collapse')
		:css('border', border .. 'px solid ' .. color_border)
		:css('width', size .. 'px')
		:css('display', 'table')
		:cssText(floatstyle)
	local innercell = root
		:tag('div'):css('display', 'table-row')
			:tag('div'):css('display', 'table-cell')
				:css('border-top', 0)
				:css('padding', spacing .. 'px 0 0 ' .. spacing .. 'px')
 
	-- loop over the photos
	lastnum = -1
	rownum = 0
	local row
	for k=1,photocount do
		local num = math.floor(photos[k])
		local c = letters[math.floor(0.5 + 100*(photos[k] - num))]
		if(num ~= lastnum) then
			rownum = rownum + 1
			row = innercell
				:tag('div'):css('display', 'table')
					:css('background-color', color)
					:css('border-collapse', 'collapse')
						:tag('div'):css('display', 'table-row')
		end
		local image = string.format( '[[File:%s|%dpx]]',
			args['photo' .. num .. c],
			(size - spacing*(count[rownum] - 1))/count[rownum] )
		row
			:tag('div'):css('display', 'table-cell')
				:css('border-top', 0)
				:css('padding', '0 ' .. spacing .. 'px ' .. spacing .. 'px ' .. '0')
				:wikitext(image)
		lastnum = num
	end
	if isnotempty(caption) then
		root
			:tag('div'):css('display', 'table-row')
				:tag('div'):css('display', 'table-cell')
					:addClass('thumbcaption')
					:css('background-color', text_background)
					:css('font-size', '88%')
					:wikitext(caption)
	end
	-- end table
	end
	if photocount < 2 then
		tracking = tracking .. '[[Category:Pages_using_photo_montage_with_one_or_fewer_images|' .. photocount ..']]'
	end
    return tostring(root or '') .. foot_montage .. tracking
end

function p.montage( frame )
    return photomontage( frame )
end
 
return p