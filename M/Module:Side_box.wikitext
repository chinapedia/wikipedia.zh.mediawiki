--本模塊嵌入{{side box}}

local yesno = require('Module:Yesno')

local p = {}

function p.main(frame)
	local origArgs = frame:getParent().args
	local args = {}
	for k, v in pairs(origArgs) do
		v = v:match('%s*(.-)%s*$')
		if v ~= '' then
			args[k] = v
		end
	end
	return p._main(args)
end

function p._main(args)
	local data = p.makeData(args)
	return p.renderSidebox(data)
end

function p.makeData(args)
	local data = {}

	-- Main table classes
	data.classes = {}
	if yesno(args.metadata) ~= false then
		table.insert(data.classes, 'metadata')
	end
	if args.position and args.position:lower() == 'left' then
		table.insert(data.classes, 'mbox-small-left')
	else
		table.insert(data.classes, 'mbox-small')
	end
	table.insert(data.classes, args.class)
	
	-- Image
	if args.image and args.image ~= 'none' then
		data.image = args.image
	end

	-- Copy over data that doesn't need adjusting
	local argsToCopy = {
		-- Styles
		'style',
		'textstyle',

		-- Above row
		'above',
		'abovestyle',

		-- Body row
		'text',
		'imageright',

		-- Below row
		'below',
	}
	for i, key in ipairs(argsToCopy) do
		data[key] = args[key]
	end

	return data
end

function p.renderSidebox(data)
	-- Renders the sidebox HTML.

	-- Table root
	local root = mw.html.create('table')
	for i, class in ipairs(data.classes or {}) do
		root:addClass(class)
	end
	root:css{border = '1px solid #aaa', ['background-color'] = '#f9f9f9'}
	if data.style then
		root:cssText(data.style)
	end

	-- The "above" row
	if data.above then
		local aboveCell = root:newline():tag('tr'):tag('td')
		aboveCell
			:attr('colspan', data.imageright and 3 or 2)
			:addClass('mbox-text')
		if data.textstyle then
			aboveCell:cssText(data.textstyle)
		end
		if data.abovestyle then
			aboveCell:cssText(data.abovestyle)
		end
		aboveCell
			:newline()
			:wikitext(data.above)
	end

	-- The body row
	local bodyRow = root:newline():tag('tr'):newline()
	if data.image then
		bodyRow:tag('td')
			:addClass('mbox-image')
			:wikitext(data.image)
	else
		bodyRow:tag('td'):css('width', '1px')
	end
	local textCell = bodyRow:newline():tag('td')
	textCell:addClass('mbox-text plainlist')
	if data.textstyle then
		textCell:cssText(data.textstyle)
	end
	textCell:wikitext(data.text)
	if data.imageright then
		bodyRow:newline():tag('td')
			:addClass('mbox-imageright')
			:wikitext(data.imageright)
	end

	-- The below row
	if data.below then
		local belowCell = root:newline():tag('tr'):tag('td')
		belowCell
			:attr('colspan', data.imageright and 3 or 2)
			:addClass('mbox-text')
		if data.textstyle then
			belowCell:cssText(data.textstyle)
		end
		belowCell:wikitext(data.below)
	end

	return tostring(root)
end

return p