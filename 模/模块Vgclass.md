local getArgs = require('Module:Arguments').getArgs
local p = {}

local function classicon(class) 
	return mw.getCurrentFrame():expandTemplate{ title = 'Class/icon', args = { class, ['style'] = "padding-right: 0.25em;" } }
end

local function iconAndTitle(class, title)
	title = title or mw.title.getCurrentTitle()
	return classicon(class) .. '[['_.._title_.._'|' .. title .. ']]'
end

local function buildItem(talkPageContent, title, tamplateAlias, classAlias)
	local pos, templateName

	for _, v in ipairs(tamplateAlias) do
		pos = mw.ustring.find(talkPageContent, '{{%s*' .. v)
		if pos then
			templateName = v
			break
		end
	end
	
	if templateName == nil then
		return '[['_.._title_.._'|' .. title .. ']]'
	end
	
	for _, v in ipairs(classAlias) do
		for _, w in ipairs(v) do
			if mw.ustring.find(talkPageContent, '{{%s*' .. templateName ..'[^{]*|%s*class%s*=%s*' .. w .. '%s*[|}]', pos) then
				return iconAndTitle(v.retval, title)
			end
		end
	end
	
	return iconAndTitle('NA', title)
end

local tamplateAlias = {
	'[Ww]iki[Pp]roject[ _][Vv]ideo[ _]games',
	'[电電]子[游遊][戏戲][专專][题題]',
	'[电電]子[游遊][戏戲]',
	'WPVG',
	'Minecraft專題',
}

local classAlias = {
	{'[Ss]tub', '小', '小作品', '小[条條]目'; retval = 'Stub'},
	{'[Ss]tart', '初', '初[级級]', '初[级級][条條]目'; retval = 'Start'},	
	{'[Ll]ist', '列表'; retval = 'List'},
	{'[Cc]', '丙', '丙[级級]', '丙[级級][条條]目'; retval = 'C'},	
	{'[Cc][Ll]', '丙[级級]列表'; retval = 'CL'},
	{'[Bb]', '乙', '乙[级級]', '乙[级級][条條]目'; retval = 'B'},
	{'[Bb][Ll]', '乙[级級]列表'; retval = 'BL'},
	{'[Gg][Aa]', '[优優]良', '[优優]良[条條]目'; retval = 'GA'},
	{'[Ff][Aa]', '特色', '特色[条條]目', '典[范範]', '典[范範][条條]目'; retval = 'FA'},
	{'[Ff][Ll]', '特色列表'; retval = 'FL'},
	{'[Dd]isambig', '[Dd]ab', '消歧[义義]'; retval = 'Disambig'},
}

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	local title, talkPageContent, retval
	title = mw.title.new(args[1])

	talkPageContent = title.talkPageTitle:getContent() or ''
	retval = buildItem(talkPageContent, args[1], tamplateAlias, classAlias)

	if args.redirect ~= "follow" then return retval end

	if retval ~= '[['_.._args[1]_.._'|' .. args[1] .. ']]' then return retval end

	if title.isRedirect then
		talkPageContent = title.redirectTarget.talkPageTitle:getContent() or ''
		return buildItem(talkPageContent, args[1], tamplateAlias, classAlias)
	end
end

return p