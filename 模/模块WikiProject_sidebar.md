require('Module:No globals')

local getArgs = require('Module:Arguments').getArgs
local p = {}

local function buildSidebarColumn(builder, args, columnCode)
	local columnAlias = mw.text.split(args[columnCode..'_alias'], '%s*,%s*')
	
	local builder = builder:tag('table')
		:addClass('mw-collapsible')
		:attr('cellpadding', '3')
		:attr('cellspacing', '0')
		:css('width', '100%')
	
	local state
	for _, v in ipairs(columnAlias) do
		if args[v] == 'expanded' then
			state = 'mw-uncollapsed'
			break
		elseif args[v] == 'collapsed' then
			state = 'mw-collapsed'
			break
		end
	end

	if state then
		builder:addClass(state)
	elseif args.all == 'expanded' then
		builder:addClass('mw-uncollapsed')
	else
		builder:addClass('mw-collapsed')		
	end
	
	builder:tag('tr'):tag('th')
		:attr('colspan', '2')
		:css('text-align', 'left')
		:css('border-top', '1px solid ' .. args.borderColor)
		:css('background-color', args.backgroundColor)
		:wikitext(args[columnCode])

	for i = 1, 10 do
		local itemCode, itemTalkCode
		itemCode = columnCode .. i
		itemTalkCode = itemCode .. '_talk'
		
		if args[itemCode] then
			local builder = builder:tag('tr')
			builder:tag('td'):wikitext(args[itemCode])
			builder:tag('td'):css('width', '20%'):wikitext(args[itemTalkCode] or '')
			
			for j = 97, 106 do
				local subItemCode, subItemTalkCode
				subItemCode = itemCode .. string.char(j)
				subItemTalkCode = subItemCode .. '_talk'
				
				if args[subItemCode] then
					local builder = builder:tag('tr')
					builder:tag('td'):css('text-indent', '1em'):wikitext(args[subItemCode])
					builder:tag('td'):css('width', '20%'):wikitext(args[subItemTalkCode] or '')
				end
			end
		end
	end	
end

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	local ret = mw.html.create('div')
		:addClass('floatright')
		:css('margin-right', '1em')
		:css('margin-bottom', '0.3em')
		:css('width', '15.5em')
		:css('font-size', '90%')
		
	-- Shortcut 
	if args[1] then
		local shortcut = ret:tag('table')
			:addClass('shortcutbox')
			:attr('cellpadding', '0')
			:attr('cellspacing', '0')
			:css('background-color', '#F9F9F9')
			:css('border', '1px solid #aaa')
			:css('width', '100%')
			:css('margin-bottom', '0.3em')
			
		shortcut:tag('tr'):tag('td')
			:css('font-size', 'small')
			:css('text-align', 'center')
			:css('font-weight', 'bold')
			:wikitext('[[Wikipedia:捷徑|-{zh-cn:快捷方式; zh-tw:捷徑;}-]]：')
			:wikitext('[['_.._args[1]_.._'|' .. args[1] .. ']]')
	end

	-- Archive 
	if args.archive then
		local archive = ret:tag('table')
			:attr('cellpadding', '0')
			:attr('cellspacing', '0')
			:css('background-color', '#F9F9F9')
			:css('border', '1px solid #aaa')
			:css('border-collapse', 'collapse')
			:css('width', '100%')
			:css('margin-bottom', '0.3em')
			
		archive:tag('tr'):css('font-size', '100%'):tag('th')
			:wikitext('[[File:Replacement_filing_cabinet.svg|40px]]<br />[[Wikipedia:存档|存档]]')
				
		archive:tag('tr'):tag('td')
			:wikitext(args.archive)
	end

	-- Sidebar
	local navbar = ret:tag('table')
		:attr('cellpadding', '0')
		:attr('cellspacing', '0')
		:css('background-color', '#F9F9F9')
		:css('border', '1px solid ' .. args.borderColor)
		:css('border-collapse', 'collapse')
		:css('width', '100%')
	
	local header = navbar:tag('tr'):tag('th')
		:css('padding', '0px')
		:css('border-bottom', '1px solid ' .. args.borderColor)
	header = header:tag('table')
		:attr('cellpadding', '0')
		:attr('cellspacing', '0')
		:css('background-color', args.backgroundHighlightColor)
		:css('width', '100%')
		:css('font-size', '111%')
		:css('text-align', 'center')
		:tag('tr')	
	header:tag('td')
		:css('width' ,'48px')
		:wikitext('[[File:'_.._args.icon_.._'|30px]]')	
	header:tag('td')
		:wikitext('[[Wikipedia:' .. args.project ..'|')
		:wikitext('<span style="font-weight: bold; color: ' .. args.textHighlightColor .. ';">')
		:wikitext(args.project)
		:wikitext('</span>]]')
		
	local columnZero = navbar:tag('tr'):tag('td'):attr('colspan', '2')	
	columnZero = columnZero:tag('table')
		:attr('cellpadding', '3')
		:attr('cellspacing', '0')
		:css('width', '100%')
		:tag('tr')		
	columnZero:tag('td'):wikitext('[[Wikipedia:'_.._args.project_.._'|-{zh-cn:主页; zh-tw:首頁}-]]')
	columnZero:tag('td'):css('width', '20%'):wikitext('[[Wikipedia_talk:'_.._args.project_.._'|讨论]]')
	
	for i = 65, 74 do
		local columnCode = string.char(i)
		if args[columnCode] then
			local builder = navbar:tag('tr'):tag('td'):attr('colspan', '2')
			buildSidebarColumn(builder, args, columnCode)
		end
	end
	
	local alsoList = {}
	for i = 1, 5 do
		local paraLink, paraName
		paraLink = 'also' .. i
		paraName = 'also' .. i  .. '_name'
		if args['also' .. i] then
			table.insert(alsoList, {link = args[paraLink], name = args[paraName]})
		end
	end
	
	if #alsoList > 0 then
		local also = navbar:tag('tr'):tag('td'):attr('colspan', '2')
			:css('border-top', '1px solid ' .. args.borderColor)
			:css('border-bottom', '1px solid ' .. args.borderColor)
			:css('background-color', args.backgroundColor)
			:css('text-align', 'center')
		also = also:tag('ol')
			:addClass('hlist')
			:css('margin', 'auto')
		for _, v in ipairs(alsoList) do
			also:tag('li')
				:wikitext('[[' .. v.link .. '|')
				:wikitext('<span style="' .. args.textColor .. ';">')
				:wikitext(v.name)
				:wikitext('</span>]]')
		end
	end
	
	local bottom = navbar:tag('tr'):tag('td'):css('text-align', 'center'):attr('colspan', '2')
	bottom = bottom:tag('ol')
		:addClass('hlist')
		:addClass('plainlinks')
		:css('font-size', '95%')
		:css('margin', 'auto')
	bottom:tag('li'):wikitext('[[Wikipedia:'_.._args.link_.._'|-{zh-cn:查看; zh-tw:檢視}-]]')
	bottom:tag('li'):wikitext('[[Wikipedia_talk:'_.._args.link_.._'|讨论]]')
	bottom:tag('li')
		:wikitext('[')
		:wikitext(mw.getCurrentFrame():callParserFunction('fullurl:Wikipedia:' .. args.link, 'action=edit'))
		:wikitext(' 编辑]')
	bottom:tag('li'):wikitext('[[Special:RecentChangesLinked/Wikipedia:'_.._args.link_.._'|变动]]')
	
	return ret
end

return p