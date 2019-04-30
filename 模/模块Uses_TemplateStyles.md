-- This module implements the {{Uses TemplateStyles}} template.
local yesno = require('Module:Yesno')
local mList = require('Module:List')
local mTableTools = require('Module:TableTools')
local mMessageBox = require('Module:Message box')

local p = {}

function p.main(frame)
	local origArgs = frame:getParent().args
	local args = {}
	for k, v in pairs(origArgs) do
		v = v:match('^%s*(.-)%s*$')
		if v ~= '' then
			args[k] = v
		end
	end
	return p._main(args)
end

function p._main(args)
	local tStyles = mTableTools.compressSparseArray(args)
	local box = p.renderBox(tStyles)
	local trackingCategories = p.renderTrackingCategories(args, tStyles)
	return box .. trackingCategories
end

function p.renderBox(tStyles)
	local boxArgs = {}
	if #tStyles < 1 then
		boxArgs.text = '<strong class="error">错误：未指定模板样式</strong>'
	else
		local tStylesLinks = {}
		for i, ts in ipairs(tStyles) do
			local sandboxLink = nil
			local tsTitle = mw.title.new(ts)
			if tsTitle then
				local tsSandboxTitle = mw.title.new(string.format('%s:%s/sandbox/%s', tsTitle.nsText, tsTitle.baseText, tsTitle.subpageText))
				if tsSandboxTitle and tsSandboxTitle.exists then
					sandboxLink = string.format('​（[[:%s|沙盒]]）', tsSandboxTitle.prefixedText)
				end
			end
			tStylesLinks[i] = string.format('[[:%s|:%s]]%s', ts, sandboxLink or '')
		end
		local tStylesList = mList.makeList('bulleted', tStylesLinks)
		boxArgs.text = '本' .. 
			(mw.title.getCurrentTitle():inNamespaces(828,829) and '-{zh-hans:模块; zh-hant:模組;}-' or '模板') ..
			'使用以下[[Wikipedia:模板样式|模板样式]]：\n' .. tStylesList
	end
	boxArgs.type = 'notice'
	boxArgs.small = true
	boxArgs.image = '[[File:Farm-Fresh_css_add.svg|32px]]'
	return mMessageBox.main('mbox', boxArgs)
end

function p.renderTrackingCategories(args, tStyles, titleObj)
	if yesno(args.nocat) then
		return ''
	end
	
	local cats = {}
	
	-- Error category
	if #tStyles < 1 then
		cats[#cats + 1] = '有模板样式错误的模板'
	end
	
	-- TemplateStyles category
	titleObj = titleObj or mw.title.getCurrentTitle()
	local subpageBlacklist = {
		doc = true,
		sandbox = true,
		sandbox2 = true,
		testcases = true
	}
	if titleObj.namespace == 10 
		and not subpageBlacklist[titleObj.subpageText]
	then
		local category = args.category
		if not category then
			category = category or '使用模板样式的模板'
		end
		cats[#cats + 1] = category
		local currentProt = titleObj.protectionLevels["edit"] and titleObj.protectionLevels["edit"][1] or nil
		for i, ts in ipairs(tStyles) do
			local tsTitleObj = mw.title.new(ts)
			local tsProt = tsTitleObj.protectionLevels["edit"] and tsTitleObj.protectionLevels["edit"][1] or nil
			if tsProt ~= currentProt then
				cats[#cats + 1] = "使用模板样式并受保护的模板"
				break
			end
		end
	end
	
	for i, cat in ipairs(cats) do
		cats[i] = string.format('[[Category:%s|Category:%s]]', cat)
	end
	return table.concat(cats)
end

return p