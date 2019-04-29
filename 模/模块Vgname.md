require('Module:No globals')

local getArgs = require('Module:Arguments').getArgs
local yesno = require('Module:Yesno')
local lc = require('Module:WikitextLC')
local foreignRegionList = mw.loadData('Module:Vgname/languages')

local chineseRegion = {
	['cn'] = {simp = '中国大陆', trad = '中國大陸'},
	['cnhk'] = {simp = '中国大陆和香港', trad = '中國大陸和香港'},
	['cntw'] = {simp = '中国大陆和台湾', trad = '中國大陸和台灣'},
	['hk'] = {simp = '香港', trad = '香港'},
	['tw'] = {simp = '台湾', trad = '台灣'},
	['twhk'] = {simp = '港台', trad = '港台'},
}

local translationTypeList = {
	{'aka', '#又译作'},
	{'official', '官方#译为'},
	{'old', '#旧译'},
}

local translationPortionList = {
	{'main:', '主标题'},
	{'sub:', '副标题'},
	{'', ''}
}

local p = {}

local function separateFootnotesFromText(str)
	local pattern = '\127\'"`UNIQ%-%-[Rr][Ee][Ff]%-%x+%-QINU`"\'\127' -- [[en:WP:UNIQ|en:WP:UNIQ]]
	str = str or ''
	
	local s, _ = str:find(pattern)
	if s then
		return str:sub(1, s-1), str:sub(s)
	end
	
	return str, ''
end

local function bold(args, str, openBracket, closeBracket, isConvert)
	local text, footnotes = separateFootnotesFromText(str)
	
	if yesno(isConvert) == true then
		text = lc.converted(text, {'zh-hans', 'zh-hant'})
	end
	
	if yesno(args.bold) ~= false then
		text = '<b>' .. text .. '</b>'
	end

	return openBracket .. text .. closeBracket .. footnotes
end

local function boldWithIdeographicComma(args, str, openBracket, closeBracket, isConvert)
	local tab, _tab = mw.text.split(str, '、'), {}
	
	for _, value in ipairs(tab) do
		local str = bold(args, value, openBracket, closeBracket, isConvert)
		table.insert(_tab, str)
	end
	
	return table.concat(_tab, '、')
end

local function styleForeignLanguageAndAddLabel(args, indexOfTheForeignRegion, str)
	local text, footnotes = separateFootnotesFromText(str)
	local theLanguage = foreignRegionList[indexOfTheForeignRegion]
	local langcode = theLanguage.langcode
	local style
	local label

	if yesno(args.italic) == false then
		style = 'normal'
	elseif theLanguage.italic then
		style = 'italic'
	else
		style = 'normal'
	end


	if yesno(args.label) == false then
		label = nil
	elseif yesno(args.diff) == true then
		label = theLanguage.diff
	elseif yesno(args.diff) == false then
		label = theLanguage.same
	elseif args.na or args.eu or args.au then
		label = theLanguage.diff
	else
		label = theLanguage.same
	end

	label = label and (label .. '：') or ''
	
	return string.format('%s<span lang="%s" style="font-style:%s;">-{%s}-</span>%s',
		label,
		langcode,
		style,
		text,
		footnotes
	)
end

local function buildVariety(args, _args, tab, usedRegionList, mode)
	local textModeConfig = {
		simp = {
			'hans', 'cn', 'sg', 'my';
			inEnglish = '常用英文', translationAs = '译作',
			openBracket = '“', closeBracket = '”'
		},
		trad = {
			'hant', 'hk', 'tw';
			inEnglish = '常用英文', translationAs = '譯作',
			openBracket = '「', closeBracket = '」'
		},
	}
	
	for _, variety in ipairs(textModeConfig[mode]) do
		local subTab = {}
		for _, region in ipairs(usedRegionList) do
			local para, text = region:sub(1, 2), region:sub(-2, -1) -- reuse text
			if para ~= variety and text ~= variety then
				if _args[para] == 'en' then
					text = chineseRegion[region][mode] .. textModeConfig[mode].inEnglish
				else
					text = chineseRegion[region][mode] .. textModeConfig[mode].translationAs .. bold(
						args,
						_args[para],
						textModeConfig[mode].openBracket,
						textModeConfig[mode].closeBracket,
						true
					)
				end
				table.insert(subTab, text)
			end
		end
		tab['zh-' .. variety] = table.concat(subTab, '，')
	end
	
	return tab
end

local function buildAka(args, theTranslationTypeItem)
	local _chineseRegionList = {'cnhk', 'cntw', 'twhk', 'cn', 'hk', 'tw'}
	local translationTypeCode = theTranslationTypeItem[1]
	local paramentValueNoSpecialRegion = args[translationTypeCode]
	local tab = {}
	
	local fixParamentValue = function(regionCode)
		local paramentNameWithPrefix = translationTypeCode .. '-' .. regionCode
		
		if args[paramentNameWithPrefix] then
			return args[paramentNameWithPrefix]
		end
		
		if #regionCode == 2 then
			return nil
		end
		
		paramentNameWithPrefix = translationTypeCode .. '-' .. regionCode:sub(3, 4) .. regionCode:sub(1, 2)
		if args[paramentNameWithPrefix] then
			return args[paramentNameWithPrefix]
		end
	end
	
	for _, regionCode in ipairs(_chineseRegionList) do
		local paramentValue = fixParamentValue(regionCode)

		if paramentValue then
			local translationTypeText = theTranslationTypeItem[2]
			for _, portion in ipairs(translationPortionList) do
				local paramentValuePattern = '^' .. portion[1] .. '(.+)$'
				if paramentValue:find(paramentValuePattern) then
					paramentValue = paramentValue:gsub(paramentValuePattern, '%1')
					translationTypeText = translationTypeText:gsub('^(.*)#(.*)$', '%1' .. portion[2] .. '%2')
					break
				end
			end
			translationTypeText = chineseRegion[regionCode].simp .. translationTypeText .. boldWithIdeographicComma(
				args,
				paramentValue,
				'「',
				'」',
				true
			)
			table.insert(tab, translationTypeText)
		end
	end
	
	
	if paramentValueNoSpecialRegion then
		local translationTypeText = theTranslationTypeItem[2]
		for _, portion in ipairs(translationPortionList) do
			local paramentValuePattern = '^' .. portion[1] .. '(.+)$'
			if paramentValueNoSpecialRegion:find(paramentValuePattern) then
				paramentValueNoSpecialRegion = paramentValueNoSpecialRegion:gsub(paramentValuePattern, '%1')
				translationTypeText = translationTypeText:gsub('^(.*)#(.*)$', '%1' .. portion[2] .. '%2')
				break
			end
		end
		local text = translationTypeText .. boldWithIdeographicComma(
			args,
			paramentValueNoSpecialRegion,
			'「',
			'」',
			true
		)
		table.insert(tab, 1, text)
	end

	if #tab == 0 then return nil end
	return table.concat(tab, '，')
end

local function head(args)
	local str = args[1] or mw.getCurrentFrame():expandTemplate{title = 'PAGENAME'}
	local openBracket, closeBracket
	
	if yesno(args.bracket) == false then
		openBracket, closeBracket = '', ''
	elseif args.bracket == 'q' then
		openBracket, closeBracket = '「', '」'
	else
		openBracket, closeBracket = '《', '》'
	end
	
	return bold(args, str, openBracket, closeBracket, false)
end

local function foreign(args)
	local tab = {}
	local englishRegionList = {'na', 'eu', 'au'}
	
	for _, value in ipairs(englishRegionList) do
		local str = args[value]
		if str then
			local text = styleForeignLanguageAndAddLabel(args, value, str)
			table.insert(tab, text)
		end
	end
	
	if #tab == 0 and args.en then
		local text = styleForeignLanguageAndAddLabel(args, 'en', args.en)
		table.insert(tab, text)
	end
	
	for key, value in ipairs(foreignRegionList) do
		local str = args[value.langcode]
		if str then
			local text = styleForeignLanguageAndAddLabel(args, key, str)
			table.insert(tab, 1, text)
		end
	end
	
	if #tab == 0 then return '' end
	return table.concat(tab, '，')
end

local function variety(args)
	if args.cn == nil or args.tw == nil then
		return ''
	end

	local tab, usedRegionList = {}, {}
	local _args = {}
	for _, value in ipairs{'cn', 'hk', 'tw'} do
		_args[value] = args[value]
	end
	
	if _args.hk == nil or _args.hk == 'tw' or _args.hk == _args.tw then
		usedRegionList = {'cn', 'twhk'}
	elseif _args.hk == 'cn' or _args.hk == _args.cn then
		usedRegionList = {'cnhk', 'tw'}
	elseif _args.tw == 'cn' or _args.tw == _args.cn then
		usedRegionList = {'cntw', 'hk'}
	elseif _args.cn == 'tw' then
		_args.cn = _args.tw
		usedRegionList = {'cntw', 'hk'}
	else
		usedRegionList = {'cn', 'hk', 'tw'}
	end
	
	tab = buildVariety(args, _args, tab, usedRegionList, 'simp')
	tab = buildVariety(args, _args, tab, usedRegionList, 'trad')
	tab['zh-mo'] = tab['zh-hk']
	
	return lc.selective(tab)
end

local function aka(args)
	local tab = {}
	for _, value in ipairs(translationTypeList) do
		local text = buildAka(args, value)
		if text then
			table.insert(tab, text)
		end
	end

	return table.concat(tab, '，')
end

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	local tab, _tab = {}, {}
	
	tab = {
		foreign(args),
		variety(args),
		aka(args),
		args[2] or ''
	}
	
	for _, value in ipairs(tab) do
		if value ~= '' then
			table.insert(_tab, value)
		end
	end
	
	if #_tab > 0 then
		return string.format('%s<span style="font-weight:normal;">（%s）</span>',
			head(args),
			table.concat(_tab, '，')
		)
	end
	return head(args)
end

return p