local p = {}

local function isnotempty(s)
	return s and s:match( '^%s*(.-)%s*$' ) ~= ''
end
 
function p.table(frame)
	local args = (frame.args[1] ~= nil) and frame.args or frame:getParent().args
	local cols = isnotempty(args['3rdcoltitle']) and 3 or 2

	-- compute the maximum cell index
	local cellcount = 0
	for k, v in pairs( args ) do
		if type( k ) == 'number' and isnotempty(v) then
			cellcount = math.max(cellcount, k)
		end
	end
	-- compute the number of rows
	local rows = math.ceil(cellcount / cols)

	-- create the root table
	local root = mw.html.create('table')
	root
		:addClass('wikitable')
		:addClass('sortable')
		:css('font-size', '95%')

	-- add the header row
	local row = root:tag('tr')
	local cell= row:tag('th')
	cell:wikitext('航空公司')
	cell= row:tag('th')
	cell:addClass('unsortable')
	cell:wikitext('目的地')
	if (isnotempty(args['3rdcoltitle'])) then
		cell= row:tag('th')
		cell:css('width','10%')
		cell:wikitext(args['3rdcoltitle'])
	end
	-- loop over rows
	for j=1,rows do
		row = root:tag('tr')
		for i=1,cols do
			cell= row:tag('td')
			if (i > 2) then cell:css('text-align','center') end
			cell:wikitext(args[cols*(j - 1) + i] or '')
		end
	end
	-- return the root table
	return tostring(root)
end

return p