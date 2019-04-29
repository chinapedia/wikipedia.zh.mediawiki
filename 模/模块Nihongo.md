require('Module:No globals')
local getArgs = require('Module:Arguments').getArgs
local p = {}

local function ja(text)
	return string.format('<span lang="ja" xml:lang="ja">-{%s}-</span>', text)
end

local function romaji(text)
	return string.format('<span lang="ja-Latn" xml:lang="ja-Latn" title="日文转写">-{%s}-</span>', text)
end

local function label(args, label, content)
	if args.lead == 'yes' then
		return string.format('%s：%s', label, content)
	end
	return content
end

function p.main(frame)
	local args = getArgs(frame, {frameOnly = true})
	return p._main(args)
end

function p._main(args)
	local bracketArr, temp = {}

	if args[1] then
		if args[2] then table.insert(bracketArr, label(args, '日语', ja(args[2]))) end
		if args['romaji'] then table.insert(bracketArr, label(args, '[[平文式罗马字|罗马字]]', romaji(args['romaji']))) end
		if args[3] then table.insert(bracketArr, args[3]) end
		if args[4] then table.insert(bracketArr, args[4]) end
		if #bracketArr > 0 then temp = '（' .. table.concat(bracketArr, '，') .. '）' end
		if args[5] then temp = temp and (temp .. '　' .. args[5]) or ('　' .. args[5]) end
		if temp then return string.format('%s<span style="font-weight: normal;">%s</span>', args[1], temp) end
		return args[1]
	end
	
	if args['romaji'] then 
		if args[2] then table.insert(bracketArr, label(args, '日语', ja(args[2]))) end
		if args[3] then table.insert(bracketArr, args[3]) end
		if args[4] then table.insert(bracketArr, args[4]) end
		if #bracketArr > 0 then temp = '（' .. table.concat(bracketArr, '，') .. '）' end
		if args[5] then temp = temp and (temp .. '　' .. args[5]) or ('　' .. args[5]) end
		if temp then return string.format('%s<span style="font-weight: normal;">%s</span>', romaji(args.romaji), temp) end
		return romaji(args.romaji)
	end
	
	if args[3] then 
		if args[2] then table.insert(bracketArr, label(args, '日语', ja(args[2]))) end
		if args[4] then table.insert(bracketArr, args[4]) end
		if #bracketArr > 0 then temp = '（' .. table.concat(bracketArr, '，') .. '）' end
		if args[5] then temp = temp and (temp .. '　' .. args[5]) or ('　' .. args[5]) end
		if temp then return string.format('%s<span style="font-weight: normal;">%s</span>', args[3], temp) end
		return args[3]
	end
	
	if args[2] then
		if args[4] then temp = '（' .. args[4] .. '）' end
		if args[5] then temp = temp and (temp .. '　' .. args[5]) or ('　' .. args[5]) end
		if temp then return string.format('%s<span style="font-weight: normal;">%s</s>', ja(args[2]), temp) end
		return ja(args[2])
	end
	
	return '<span class="error">未指定对象名称</span>'
	
end

return p