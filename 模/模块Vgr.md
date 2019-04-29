local labels = {
	-- South Korea and Japan
	{'KR', '-{zh-cn:韩国; zh-tw:南韓;}-'},
	{'JP', '日本'},
	
	-- Western
	{'WW', '全球'},
	{'NA', '北美'},
	{'PAL', '[[PAL区|PAL]]'},
	{'EU', '欧洲'},
	{'UK', '英国'},
	{'AU', '澳-{}-洲'},
	{'AUS', '澳-{}-洲'},
	
	-- Chinese-speaking world
	{'CN', '<abbr title="中国大陆">大陆</abbr>'},
	{'TWHK', '臺港'},
	{'TW', '臺灣'},
	{'HK', '香港'},
	{'MO', '澳门'},
	
	-- Southeast Asia
	{'SEA', '东南亚'},
	{'SG', '新加坡'},
	{'MY', '<abbr title="马来西亚">大马</abbr>'},
	
	-- Others
	{'?', '未知'},
}

require('Module:No globals')
local getArgs = require('Module:Arguments').getArgs
local list = require('Module:List').unbulleted
local yesno = require('Module:Yesno')
local lc = require('Module:WikitextLC').converted
local cd = require('Module:Chinese date')._main

local p = {}

local function getLabelName(input)
	if input == nil then
		return ''
	end
	
	for key, value in ipairs(labels) do
		if input == value[1] then
			return value[2] .. '：'
		end
	end
	
	return input .. '：'
end

local function itemBuilder(args, para1, para2)

	para1 = getLabelName(para1)
	
	if para2 == nil then
		para2 = ''
	elseif yesno(args.nocc) then
		para2 = lc(para2, {'zh-hans', 'zh-hant'})
	else
		para2 = cd{para2, ['error']='ignore', ['suf']='yes'}
	end
	
	return (para1 .. para2 == '' and nil or para1 .. para2)

end

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	-- Main module code goes here.
	local tab = {}
	local maxIndex = 20 -- [[WP:VG/GL|专题指引]]不鼓励在信息框列出过多地区的发售信息，故将此数限制在20以内，即最多列出10个地区
	
	for i = 1, maxIndex, 2 do
		table.insert(tab, itemBuilder(args, args[i], args[i+1]))
	end

	return list(tab)
end

return p