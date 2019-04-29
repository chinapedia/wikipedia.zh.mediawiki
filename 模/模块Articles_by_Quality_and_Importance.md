require('Module:No globals')

local getArgs = require('Module:Arguments').getArgs
local yesno = require('Module:Yesno')

local classList = {
	
	{'fa', score = 10},
	{'a', score = 9},
	{'ga', score = 8},
	{'bplus', score = 7.5, enabled = false},
	{'b', score = 7},
	{'c', score = 5},
	{'start', score = 3},
	{'stub', score = 1},
	
	{'fl', score = 10},
	{'al', score = 9, enabled = false},
	{'bl', score = 7, enabled = false},
	{'cl', score = 5, enabled = false},
	{'list', score = 3},
	{'sl', score = 1, enabled = false},
	
	{'category'},
	{'disambig'},
	{'draft'},
	{'file'},
	{'portal'},
	{'project'},
	{'template'},
	{'module'},
	{'na'},
	
	{'unassessed', score = 0},

}

local importanceList = {
	{'top'},
	{'high'},
	{'mid'},
	{'low'},
	{'bottom', enabled = false},
	{'no', enabled = false},
	{'na'},
	{'unknown'},
}

local function getClassName(class, writingSystem)
	if class == 'ALL' then return '' end
	return require('Module:Class/convert')._main({class, writingSystem}) .. (writingSystem == 'trad' and '級' or '级')
end

local function getImportanceName(importance, writingSystem)
	if importance == 'ALL' then return '' end
	return require('Module:Importance/convert')._main({importance, writingSystem}) .. '重要度'
end

local function categoryName(args, class, importance)
	local categoryNamingFormat
	local writingSystem = yesno(args.trad) and 'trad' or 'simp'
	
	if class == 'ALL' and importance ~= 'ALL' then
		return string.format('%s%s%s', getImportanceName(importance, writingSystem), args.project, writingSystem == 'trad' and '條目' or '条目')
	end
	
	if importance == 'ALL' and class ~= 'ALL' then
		return string.format('%s%s%s', getClassName(class, writingSystem), args.project, writingSystem == 'trad' and '條目' or '条目')
	end
	
	if class == 'ALL' and importance == 'ALL' then
		return string.format('%s%s', args.project, writingSystem == 'trad' and '條目' or '条目')
	end
	
	if args.format == 'ICT' then
		categoryNamingFormat = getImportanceName(importance, writingSystem) .. getClassName(class, writingSystem)
	else
		categoryNamingFormat = getClassName(class, writingSystem) .. getImportanceName(importance, writingSystem)
	end
	
	return string.format('%s%s%s', categoryNamingFormat, args.project, writingSystem == 'trad' and '條目' or '条目')
end

local function pageNumberOfClassAndImportance(args, class, importance, enabledClassList, enabledImportanceList)
	local nonArticle = {
			'category', 'disambig', 'draft', 'file', 'portal', 
			'project', 'template', 'module', 'na' 
		}
	
	if yesno(args.manual) then
		if class == 'ALL' and importance == 'ALL' then
			local sumClass, sumImportance = 0, 0
			for _, class in ipairs(enabledClassList) do
				sumClass = sumClass + args[class .. '_ALL'] or 0
			end
			for _, importance in ipairs(enabledImportanceList) do
				sumImportance = sumImportance + args['ALL_' .. importance] or 0
			end
			return (sumClass > sumImportance) and sumClass or sumImportance
		end
		return tonumber(args[class..'_'..importance]) or 0
	end
	
	if class == 'ALL' and importance == 'ALL' then
		local sumClass, sumImportance = 0, 0
		for _, class in ipairs(enabledClassList) do
			sumClass = sumClass + tonumber( mw.getCurrentFrame():callParserFunction('PAGESINCATEGORY', categoryName(args, class, 'ALL'), 'pages', 'R') )
		end
		for _, importance in ipairs(enabledImportanceList) do
			sumImportance = sumImportance + tonumber( mw.getCurrentFrame():callParserFunction('PAGESINCATEGORY', categoryName(args, 'ALL', importance), 'pages', 'R') )
		end
		return (sumClass < sumImportance) and sumClass or sumImportance
	end
	
	for _, v in pairs(nonArticle) do
		if class == v and importance == 'na' then
			return tonumber( mw.getCurrentFrame():callParserFunction('PAGESINCATEGORY', categoryName(args, class, 'ALL'), 'pages', 'R' ) )
		end
	end
	
	return tonumber( mw.getCurrentFrame():callParserFunction('PAGESINCATEGORY',  categoryName(args, class, importance), 'pages', 'R' ))

end

local function pageNumberWithLink(args, class, importance, enabledClassList, enabledImportanceList)
	local pageNumber = pageNumberOfClassAndImportance(args, class, importance, enabledClassList, enabledImportanceList)
	
	if pageNumber == 0 and args.dispzero ~= 'yes' then
		return ''
	end
	
	pageNumber = mw.language.new('zh'):formatNum(pageNumber)
	
	if args.linkstyle == 'disabled' then
		return pageNumber
	end
	
	if args.linkstyle == 'catscan' then
		local query = 'doit=1&interface_language=zh&ns[1]=1&ns[3]=1&ns[5]=1&ns[7]=1&ns[9]=1&ns[11]=1&ns[13]=1&ns[15]=1&ns[101]=1&ns[119]=1&ns[829]=1'
		
		if args.template and args.taskforce ~= 'yes' then
			query = string.format('%s&templates_yes=%s', query, args.template)
			if class == 'ALL' and importance == 'ALL' then
				return string.format('[%s %s]', tostring(mw.uri.fullUrl('toollabs:catscan3/catscan2.php', query)), pageNumber)
			end
		end
		
		if class == 'ALL' and importance == 'ALL' then
			return pageNumber
		elseif yesno(args.manual) then
			query = string.format('%s&categories=%s|%s', query, categoryName(args, class, 'ALL'), categoryName(args, 'ALL', importance))
		else
			query = string.format('%s&categories=%s', query, categoryName(args, class, importance))
		end
			
		return string.format('[%s %s]', tostring(mw.uri.fullUrl('toollabs:catscan3/catscan2.php', query)), pageNumber)
	end
	
	if args.linkstyle == 'catscan2' then
		-- 等会再做
	end
	
	if args.linkstyle == 'forced'and yesno(args.manual) ~= false then
		return string.format('[[:Category:%s|%s]]', categoryName(args, class, importance), pageNumber)
	end
	
	if mw.title.makeTitle('Category', categoryName(args, class, importance)).exists and yesno(args.manual) ~= false then
		return string.format('[[:Category:%s|%s]]', categoryName(args, class, importance), pageNumber)
	end
	
	return pageNumber
	
end

local function getColNumubers(args, enabledClassList, enabledImportanceList)
	local col = 0

	for _, importance in ipairs(enabledImportanceList) do
		if pageNumberOfClassAndImportance(args, 'ALL', importance) > 0 then
			col = col + 1
		end
	end
	return col + 1
end

local function makeRow(args, class, enabledImportanceList)
	local ret 
	if pageNumberOfClassAndImportance(args, class, 'ALL') > 0 then
		ret = '<tr>'
		ret = ret .. mw.getCurrentFrame():expandTemplate{ title = 'Class', args = { require('Module:Class/convert')._main({class, 'simp'}), fullcategory = categoryName(args, class, 'ALL') } }
		for _, importance in ipairs(enabledImportanceList) do
			if pageNumberOfClassAndImportance(args, 'ALL', importance) > 0 then
				ret = string.format('%s<td style="text-align: right;">%s</td>', ret, pageNumberWithLink(args, class, importance))
			end
		end
		return string.format('%s<th style="text-align: right;">%s</td></tr>', ret, pageNumberWithLink(args, class, 'ALL'))
	end
	
	return ''
end

local function rowScore(args, enabledClassList, col)
	local totalScore, pages, summaryTable = 0, 0, {}
	local ret = ''
	for _, class in ipairs(enabledClassList) do
		for _, value in ipairs(classList) do
			if class == value[1] and tonumber(value.score) then
				local pageNumber = pageNumberOfClassAndImportance(args, class, 'ALL')
				totalScore = totalScore + value.score * pageNumber
				pages = pages + pageNumber
				table.insert(summaryTable, string.format('%s条目%s分', getClassName(class, 'simp'), value.score))
			end
		end
	end

	ret = '<tr style="text-align: center;">'
	ret = string.format('%s<td colspan="2" style="font-weight: bold;"><abbr title="%s">-{zh-hans:质量;zh-hant:質量;zh-tw:品質;}-指数</abbr> ([[Template:Articles_by_Quality_and_Importance#质量指数|?]])</td>', ret, args['custom_score'] or table.concat(summaryTable, '，'))
	ret = string.format('%s<td colspan="%s">Σ=%s</td>', ret, col - 1, mw.language.new('zh'):formatNum( math.ceil( (pages * classList[1].score - totalScore) / classList[1].score ) ) )
	ret = string.format('%s<td colspan="2">σ=%s</td>', ret, math.ceil(totalScore / pages * 100) / 100)
	ret = ret .. '</tr>'
	
	return ret
end

local p = {}

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	local builder
	local enabledClassList, enabledImportanceList = {}, {}
	local col = 0
	
	args.project = (args.project or args.topic) or ''

	if args.articleonly == 'yes' then
		local nonArticles = { 'category', 'disambig', 'draft', 'file', 'portal', 'project', 'template', 'module', 'na' }
		for _, value in ipairs(nonArticles) do
			args[value .. '_'] = 'false'
		end
		args['_na'] = 'false'
	end
	
	for i, v in ipairs(classList) do
		if args[v[1] .. '_'] == 'false' then
			v.enabled = false
		elseif args[v[1] .. '_'] == 'true' then
			v.enabled = true
		end
	end

	for i, v in ipairs(importanceList) do
		if args['_' .. v[1]] == 'false' then
			v.enabled = false
		elseif args['_' .. v[1]] == 'true' then
			v.enabled = true
		end
	end

	for i, v in ipairs(classList) do
		if v.enabled ~= false then
			table.insert(enabledClassList, v[1])
		end
	end
	
	for i, v in ipairs(importanceList) do
		if v.enabled ~= false then
			table.insert(enabledImportanceList, v[1])
		end
	end
	
	if yesno(args.manual) then
		for i, v in ipairs(enabledClassList) do
			for j, w in ipairs(enabledImportanceList) do
				args[v .. '_' .. w] = pageNumberOfClassAndImportance(args, v, w)
				args[v .. '_ALL'] = (args[v .. '_ALL'] or 0) + args[v .. '_' .. w]
				args['ALL_' .. w] = (args['ALL_' .. w] or 0) + args[v .. '_' .. w]
			end
		end
	end

	for _, class in ipairs(enabledClassList) do
		for key, value in ipairs(classList) do
			if class == value[1] then
				if tonumber(args[class .. '_score']) then
					classList[key].score = tonumber(args[class .. '_score'])
				elseif args[class .. '_score'] == 'no' then
					classList[key].score = nil
				end
			end
		end
	end

	col = getColNumubers(args, enabledClassList, enabledImportanceList)
	
	builder = '<table class="wikitable plainlinks">'
	builder = string.format('%s<caption>%s%s条目状态</caption>', builder, args.project or '', yesno(args.taskforce) and '工作组' or '专题' or '專題')
	builder = builder .. '<tr><th rowspan="2">-{zh-hans:质量;zh-hant:質量;zh-tw:品質;}-</th>'
	builder = string.format('%s<th colspan="%s">重要度</th></tr><tr>', builder, col)
	for _, importance in ipairs(enabledImportanceList) do
		if pageNumberOfClassAndImportance(args, 'ALL', importance) > 0 then
			builder = builder .. mw.getCurrentFrame():expandTemplate{ title = 'Importance', args = { require('Module:Importance/convert')._main({importance, 'simp'}), fullcategory = categoryName(args, 'ALL', importance) } }
		end
	end
	builder = builder .. '<th>合计</th></tr>'
	for _, class in ipairs(enabledClassList) do
		builder = builder .. makeRow(args, class, enabledImportanceList)
	end
	
	builder = builder .. '<tr><th>合计</th>'
	for _, importance in ipairs(enabledImportanceList) do
		if pageNumberOfClassAndImportance(args, 'ALL', importance) > 0 then
			builder = string.format('%s<th style="text-align: right;">%s</th>', builder, pageNumberWithLink(args, 'ALL', importance))
		end
	end
	builder = string.format('%s<th style="text-align: right;">%s</th>', builder, pageNumberWithLink(args, 'ALL', 'ALL', enabledClassList, enabledImportanceList))
	builder = builder .. '</tr>'

	builder = builder .. rowScore(args, enabledClassList, col - 2)
	
	if yesno(args.manual) then
		if args.updated then
			local ret = args.updated .. (args.updatelink and string.format(' [%s ↻]', args.updatelink) or '')
			builder = string.format('%s<tr><td colspan="%s" style="text-align: center;">%s</td></tr>', builder, col + 1, ret)
		end
	else
		local ret = mw.language.new('zh'):formatDate('Y-m-d H:i:s') .. ' (UTC)'
		builder = string.format('%s<tr><td colspan="%s" style="text-align: center;">%s</td></tr>', builder, col + 1, ret)
	end
	
	return builder .. '</table>'
end

return p