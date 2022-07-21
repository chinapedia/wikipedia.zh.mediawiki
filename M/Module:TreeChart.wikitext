require('Module:No globals')

local p = {}

local cells = mw.loadData('Module:TreeChart/data')

function p._main(cell_args)
	local ret = mw.html.create()
	local top = ret:tag('tr')
						:css{ height = '1px',
								['text-align'] = 'center' }
	local bottom = ret:tag('tr')
						:css{ height = '1px',
								['text-align'] = 'center' }
	for _, v in ipairs(cell_args) do
		if type(v) == 'string' then
			top:wikitext(cells[v].t)
			bottom:wikitext(cells[v].b)
		else
			top:tag('td')
				:attr{ colspan = v.colspan or cell_args.colspan or 6,
						rowspan = v.rowspan or cell_args.rowspan or 2 }
				:css{ padding = '0.2em',
						border = (v.border or cell_args.border or '2') .. 'px solid black' }
				:cssText(v.boxstyle or cell_args.boxstyle)
				:wikitext(v.text)
		end
	end
	return tostring(ret)
end

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {wrappers = 'Template:Tree chart', trim = false, removeBlanks = false})
	local cell_args = {
		colspan = args.colspan,
		rowspan = args.rowspan,
		border = args.border,
		boxstyle = args.boxstyle
	}
	for _, val in ipairs(args) do
		local trimmedVal = val:match('^%s*(.-)%s*$')
		if trimmedVal == '' then
			trimmedVal = '$'
		end
		if cells[trimmedVal] then
			table.insert(cell_args, trimmedVal)
		else
			-- Unnamed params behave weirdly
			-- white space at the front counts for param_{{{1}}}, but not whitespace at the end, so remove it
			local rightTrimmedVal = val:gsub('%s+$','')
			table.insert(cell_args, {
				text = args[trimmedVal] or ('{{{'..trimmedVal..'}}}'),
				colspan = args['colspan_'..rightTrimmedVal],
				rowspan = args['rowspan_'..rightTrimmedVal],
				border = args['border_'..rightTrimmedVal],
				boxstyle = args['boxstyle_'..rightTrimmedVal]
			})
		end
	end
	
	return p._main(cell_args)
end

return p