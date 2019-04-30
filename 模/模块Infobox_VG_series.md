local parameterList = {

	above = { 'title' },
	image = { 'image' },
	caption = { 'caption' },
	original = { 'original' },
	japanese = { 'japanese' },
	english = { 'english' },
	
	{ label = '[[电子游戏类型|类型]]'; 'genre' },
	{ label = '[[游戏开发者|开发]]'; 'developer' },
	{ label = '[[游戏发行商|发行]]'; 'publisher'},
	{ label = '创始人'; 'producer', 'creator', 'creater' },
	{ label = '编剧'; 'writer' },
	{ label = '美术'; 'artist'},
	{ label = '音乐'; 'composer' },	
	{ label = '[[游戏平台|平台]]'; 'platform', 'platforms' },
	{ label = '首版平台'; 'platform of origin' },
	{ label = '首发时间'; 'released', 'release' },
	{ label = '首作'; 'first release version', 'first release date' },
	{ label = '最新作'; 'latest release version', 'latest release date' },	
	{ label = '演绎产品'; 'spinoffs' },
	
}

local p = {}

local getArgs = require('Module:Arguments').getArgs
local infobox = require('Module:Infobox').infobox

local function getData(args, idx)
	for _, v in ipairs(parameterList[idx]) do
		if args[v] then	return args[v] end
	end
end

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	-- Main module code goes here.
	local list = {}
	local cont = 0
	
	list.captionstyle = 'text-align: center;'
	list.subheaderstyle = 'text-align: center; vetical-align: middle; font-weight:normal;'
	list.labelstyle = 'text-align: left; vetical-align: middle; white-space: nowrap;'
	
	list.above = getData(args, 'above') or tostring(mw.title.getCurrentTitle())
	if getData(args, 'original') then
		list.subheader1 = string.gsub(getData(args, 'original'), '^(..) *: *(.+)$', '<span lang="%1" xml:lang="%1">-{%2}-</span>') or getData(args, 'original')
	else
		list.subheader1 =  getData(args, 'japanese') and string.format('-{<span lang="ja" xml:lang="ja">%s</span>}-', getData(args, 'japanese')) 
	end
	list.subheader2 = getData(args, 'english') and string.format('-{<span lang="en" xml:lang="en" style="font-style: italic;">%s</span>}-', getData(args, 'english'))
	list.image = require('Module:InfoboxImage').InfoboxImage{ args = { 
		image = args.image, 
		sizedefault = 'frameless', 
		upright = '1.15',
	} }
	list.caption = list.image and getData(args, 'caption')
	
	for i, v in ipairs(parameterList) do
		local data = getData(args, i)
		if data then
			cont = cont + 1
			list['data'..cont] = data
			list['label'..cont] = v.label
			list['header'..cont] = v.header
		end
	end

	if (args['latest release version'] and args['latest release date']) then
		for i = #parameterList, 1, -1 do
			if list['label'..i] == '最新作' then
				list['data'..i] = args['latest release version'] .. '<br />' .. args['latest release date']
				break
			end
		end
	end

	if (args['first release version'] and args['first release date']) then
		for i = #parameterList, 1, -1 do
			if list['label'..i] == '首作' then
				list['data'..i] = args['first release version'] .. '<br />' .. args['first release date']
				break
			end
		end
	end

	return infobox(list)
end

return p