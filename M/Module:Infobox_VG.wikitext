local p = {}

local getArgs = require('Module:Arguments').getArgs
local infobox = require('Module:Infobox').infobox
local parameterList = mw.loadData('Module:Infobox VG/parameterList')

local function getData(args, idx)
	for _, v in ipairs(parameterList[idx]) do
		if args[v] then	return args[v] end
	end
end

local function image(args)
	local variety = {'', '-hans', '-hant', '-cn', '-hk', '-mo', '-sg', '-tw'}
	local InfoboxImage = function(img) return require('Module:InfoboxImage').InfoboxImage{ args = { 
		image = img, 
		sizedefault = 'frameless', 
		upright = '1.15',
	} } end
	
	if (args['image-hans'] or args['image-cn'] or args['image-sg']) and (args['image-hant'] or args['image-hk'] or args['image-mo'] or args['image-tw']) then
		local temp = ''
		
		for _, v in ipairs(variety) do
			if args['image'..v] then
				temp = temp .. string.format(' zh%s:%s;', v, InfoboxImage(args['image'..v]))
			end
		end
	
		return string.format('-{%s }-', temp)
	end
	
	return InfoboxImage(getData(args, 'image')) or nil

end

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	-- Main module code goes here.
	local list = {}
	local cont = 0
	local usedImage, cleanupNeeded = false, false

	-- 预处理
	for i, v in ipairs(parameterList) do
		local data = getData(args, i)
		if data == nil then
		elseif string.find(data, '[Ff]ile:') or string.find(data, '[Ii]mage:') then
			usedImage = true
			break
		end
	end
	
	if string.find(args.official or '', '-{.*}-') then
		cleanupNeeded = true
	elseif string.find(args.common or '', '-{.*}-') then
		cleanupNeeded = true
	elseif string.match((args.original or args['origina_name']) or '..:', '^.. *:') == nil then
		cleanupNeeded = true
	end
	
	if args.official then
		args.official = require('Module:WikitextLC').converted(args.official, {'zh-hans', 'zh-hant'})
	end
	if args.common then
		args.common = require('Module:WikitextLC').converted(args.common, {'zh-hans', 'zh-hant'})
	end	
	
	-- 样式
	list.bodystyle = 'width:264px;'
	list.captionstyle = 'text-align: center;'
	list.subheaderstyle = 'text-align: center; vetical-align: middle; font-weight:normal;'
	list.labelstyle = 'white-space: nowrap;'
	list.headerstyle = 'background-color: #F0F0F0;'

	list.above = getData(args, 'above') or tostring(mw.title.getCurrentTitle())
	if getData(args, 'original') then
		list.subheader1 = string.gsub(getData(args, 'original'), '^(..) *: *(.+)$', '<span lang="%1" xml:lang="%1">-{%2}-</span>') or getData(args, 'original')
	else
		list.subheader1 =  getData(args, 'japanese') and string.format('-{<span lang="ja" xml:lang="ja">%s</span>}-', getData(args, 'japanese')) 
	end
	list.subheader2 = getData(args, 'english') and string.format('-{<span lang="en" xml:lang="en" style="font-style: italic;">%s</span>}-', getData(args, 'english'))
	list.image = image(args)
	list.caption = list.image and getData(args, 'caption')
	
	for i, v in ipairs(parameterList) do
		local data = getData(args, i)
		if data then
			cont = cont + 1
			list['data'..cont] = data
			list['label'..cont] = (v.labelOL and args.onlinegame) and v.labelOL or v.label
			list['header'..cont] = v.header
		end
	end
	
	return infobox(list) .. (usedImage and '[[Category:可能使用国旗图标的电子游戏信息框|Category:可能使用国旗图标的电子游戏信息框]]' or '') .. (cleanupNeeded and '[[Category:或需标准化参数格式的电子游戏信息框|Category:或需标准化参数格式的电子游戏信息框]]' or '')
end

return p