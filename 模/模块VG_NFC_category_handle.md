require('Module:No globals')

local platformAlias = {
	-- Nintendo
	['红白机'] = {'红白机', '紅白機', 'FC', 'Famicom', 'NES', 'Nintendo Entertainment System', 'FC磁碟机', 'FC磁碟機'},
	['超级任天堂'] = {'超级任天堂',  '超級任天堂', '超任', 'SFC', 'Super Famicom', 'SNES'},
	['任天堂64'] = {'任天堂64', 'N64'},
	['任天堂GameCube'] = {'任天堂GameCube', 'GameCube', 'NGC'},
	['Wii'] = {'Wii'},
	['Wii U'] = {'Wii ?U'},
	['任天堂Switch'] = {'任天堂Switch', 'Nintendo Switch', 'NS'},
	['Game Boy'] = {'Game ?Boy', 'GB'},
	['Game Boy Color'] = {'Game Boy Color', 'GBC'},
	['Game Boy Advance'] = {'Game Boy Advance', 'GBA'},
	['任天堂DS'] = {'任天堂DS', 'Nintendo DS', 'NDS'},
	['任天堂3DS'] = {'任天堂3DS', 'Nintendo 3DS', 'N3DS', '3DS'},
	
	-- Sony
	['PlayStation (游戏机)'] = {'PlayStation %(游戏机%)', 'PlayStation %(遊戲機%)', 'PlayStation', 'PS1'},
	['PlayStation 2'] = {'PlayStation 2', 'PS2'},
	['PlayStation 3'] = {'PlayStation 3', 'PS3'},
	['PlayStation 4'] = {'PlayStation 4', 'PS4'},
	['PlayStation Portable'] = {'PlayStation Portable', 'PSP'},
	['PlayStation Vita'] = {'PlayStation Vita', 'PSV', 'PSVita'},
	
	-- Microsoft
	['Xbox'] = {'Xbox %(游戏机%)', 'Xbox %(遊戲機%)', 'Xbox'},
	['Xbox 360'] = {'Xbox? 360', 'X360'},
	['Xbox One'] = {'Xbox? One', 'XOne'},
	
	-- Sega
	['世嘉Master System'] = {'世嘉Master System', 'Sega Master System', 'Master System', 'SMS'},
	['Mega Drive'] = {'Mega ?Drive', 'MD', 'Sega Genesis'},
	['世嘉土星'] = {'世嘉土星', 'Sega Saturn', 'SS'},
	['Dreamcast'] = {'Dreamcast'},
	
	-- Computer
	['Windows'] = {'Windows', 'Microsoft Windows'},
	['MacOS'] = {'macOS', 'Mac OS X', 'OS X'},
	['日本成人游戏'] = {'日本成人游戏', '日本成人遊戲', '十八禁'},

	-- Other
	['街机'] = {'街机', '街機', '大型電玩', 'Arcade'},

}


local getArgs = require('Module:Arguments').getArgs
local p = {}

local function returnCategory(input, property)
	for categoryName, aliases in pairs(platformAlias) do
		for _, k in ipairs(aliases) do
			if string.find(input, '^' .. k .. '$') then
				return '[[Category:'_.._categoryName_.._property_.._'|Category:' .. categoryName .. property .. ']]'
			end
		end
	end

	return '[[Category:'_.._input_.._property_.._'|Category:' .. input .. property .. ']]'
	
end

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	-- Main module code goes here.
	local tab = {}
	for i = 1, 10 do
		if args[i] then
			table.insert(tab, returnCategory(args[i], args.property))
		end
	end
	if table.maxn(tab) == 0 then
		return returnCategory('电子', args.property)
	end
	return table.concat(tab)
end

return p