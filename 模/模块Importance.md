local getArgs = require('Module:Arguments').getArgs
local yesno = require('Module:Yesno')

local importance = mw.loadData('Module:Importance/data')

local function getIdx(cont)
	if cont == nil then
		return 0
	end
	
	cont = string.lower(cont)
	
	for i, v in ipairs(importance) do
		
		if cont == v.code then
			return i
		end
		
		if cont == v.name then
			return i
		end
		
		if cont == v.name2 then
			return i
		end
		
		for _, w in ipairs(v.alias) do
			if cont == w then
				return i
			end
		end
	end
	
	return 0
end

local function makeInvokeFunc(funcName)
	return function (frame)
		local args = getArgs(frame)
		return p[funcName](args)
	end
end

p = {}

p.colour = makeInvokeFunc('_colour')

function p._colour(args, idx)
	local idx = idx or getIdx(args[1])
	
	return mw.text.nowiki(importance[idx].color)
end

p.icon = makeInvokeFunc('_icon')

function p._icon(args, idx, style)
	local idx = idx or getIdx(args[1])
	local style = style or (args.style or '')
	local ret = ''
		
	if importance[idx].icon then
		ret = string.format('<span style="%s">[[File:%s|%s]]</span>', style, importance[idx].icon, importance[idx].name)
	end
	
	return ret
end

p.importance = makeInvokeFunc('_importance')

function p._importance(args, idx)

	local idx = idx or getIdx(args[1])
	
	local code = importance[idx].code
	local name = importance[idx].name
	local importance = args.importance or ''
	local bold = yesno(args.bold) and 'normal' or 'bold'
	local background = p._colour(args, idx)
	local style = args.style or ''
	local attr = args.attr or ''
	local imgStyle = 'display: none;'
	local categoryName = args.fullcategory
	local category = args.category or '条目'

	if yesno(args.image) == false then
		-- Nothing to do
	elseif yesno(args.image) == true then
		imgStyle = nil
	else
		local dispImgImportance = { 'fa', 'a', 'ga', 'fl', 'al', 'fm'}
		for _, v in ipairs(dispImgImportance) do
			if code == v then
				imgStyle = nil
				break
			end
		end
	end

	if categoryName == nil then
		categoryName = name .. '重要度' .. category
	end
	
	local img = p._icon(args, idx, imgStyle)
	
	return string.format(
		'<td class="assess assess-%s %s" style="text-align:center; white-space:nowrap; font-weight:%s; background:%s; %s" %s> %s[[:Category:%s|%s]] </td>',
		code,
		name,
		bold,
		background,
		style,
		attr,
		img,
		categoryName,
		name
	)
end

return p