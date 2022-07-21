-- This module implements [[Template:Infobox_tennis_tournament_event/events|Template:Infobox tennis tournament event/events]].
-- [SublimeLinter luacheck-globals:mw]

local p = {}
local getBuffer, print, _ = require('Module:OutputBuffer')()

local STYLES = {
	["singlesdoubles"] = {[=[|-
| [[{prefix}_{year}年{tournament}單打比賽|單打]]
| [[{prefix}_{year}年{tournamentd}雙打比賽|雙打]]]=]},
		["1"] = "singlesdoubles",
		["men"] = "singlesdoubles",
		["mens"] = "singlesdoubles",
		["women"] = "singlesdoubles",
		["womens"] = "singlesdoubles",
	["risingstarsinvitational"] = {[=[|-
| [[{prefix}_{year}年{tournament}單打比賽|單打]]
| [[{prefix}_{year}年{tournamentd}雙打比賽|雙打]]
|-
| colspan="2" | [[{prefix}_{year}年{tournament}新星邀請賽|新星]]]=]},
	["boysgirlssingles"] = {[=[|-
! scope="row" style="font-weight: normal; text-align: right;" | 單打
| [[{prefix}_{year}年{tournament}男子單打比賽|男子]]
| [[{prefix}_{year}年{tournament}女子單打比賽|女子]]
| [[{prefix}_{year}年{tournament}青少年男子單打比賽|青少男]]
| [[{prefix}_{year}年{tournament}青少年女子單打比賽|青少女]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 雙打
| [[{prefix}_{year}年{tournament}男子雙打比賽|男子]]
| [[{prefix}_{year}年{tournament}女子雙打比賽|女子]]]=]},
		["邁阿密大師賽"] = "boysgirlssingles",
	["混合雙打"] = {[=[|-
! scope="row" style="font-weight: normal; text-align: right;" | 單打
| [[{prefix}_{year}年{tournament}男子單打比賽|男子]]
| [[{prefix}_{year}年{tournament}女子單打比賽|女子]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 雙打
| [[{prefix}_{year}年{tournament}男子雙打比賽|男子]]
| [[{prefix}_{year}年{tournament}女子雙打比賽|女子]]
| [[{prefix}_{year}年{tournament}混合雙打比賽|混合]]=]},
		["混合"] = "mixeddoubles",
		["大滿貫"] = "mixeddoubles",
	["mixedandteam"] = {[=[|-
! scope="row" style="font-weight: normal; text-align: right;" | 單打
| [[{prefix}_{year}年{tournament}男子單打比賽|男子]]
| [[{prefix}_{year}年{tournament}女子單打比賽|女子]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 雙打
| [[{prefix}_{year}年{tournament}男子雙打比賽|男子]]
| [[{prefix}_{year}年{tournament}女子雙打比賽|女子]]
| [[{prefix}_{year}年{tournament}混合雙打比賽|混合]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 團隊
| [[{prefix}_{year}年{tournament}男子團隊比賽|男子]]
| [[{prefix}_{year}年{tournament}女子團隊比賽|女子]]]=]},
	["澳洲網球公開賽"] = {[=[|-
! scope="row" style="font-weight: normal; text-align: right;" | 單打
| [[{year}年{tournament}男子單打比賽|男子]]
| [[{year}年{tournament}女子單打比賽|女子]]
|
| [[{year}年{tournament}青少年男子單打比賽|青少男]]
| [[{year}年{tournament}青少年女子單打比賽|青少女]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 雙打
| [[{year}年{tournament}男子雙打比賽|男子]]
| [[{year}年{tournament}女子雙打比賽|女子]]
| [[{year}年{tournament}混合雙打比賽|混合]]
| [[{year}年{tournament}青少年男子雙打比賽|青少男]]
| [[{year}年{tournament}青少年女子雙打比賽|青少女]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 傳奇
| [[{year}年{tournament}男子傳奇雙打比賽|男子]]
| [[{year}年{tournament}女子傳奇雙打比賽|女子]]
| [[{year}年{tournament}傳奇混合雙打比賽|混合]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 輪椅單打
| [[{year}年{tournament}輪椅男子單打比賽|男子]]
| [[{year}年{tournament}輪椅女子單打比賽|女子]]
| [[{year}年{tournament}四輪椅單打比賽|四輪]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 輪椅雙打
| [[{year}年{tournament}輪椅男子雙打比賽|男子]]
| [[{year}年{tournament}輪椅女子雙打比賽|女子]]
| [[{year}年{tournament}四輪椅雙打比賽|四輪]]
]=]},
	["法國網球公開賽"] = {[=[|-
! scope="row" style="font-weight: normal; text-align: right;" | 單打
| [[{year}年{tournament}男子單打比賽|男子]]
| [[{year}年{tournament}女子單打比賽|女子]]
|
| [[{year}年{tournament}青少年男子單打比賽|青少男]]
| [[{year}年{tournament}青少年女子單打比賽|青少女]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 雙打
| [[{year}年{tournament}男子雙打比賽|男子]]
| [[{year}年{tournament}女子雙打比賽|女子]]
| [[{year}年{tournament}混合雙打比賽|混合]]
| [[{year}年{tournament}青少年男子雙打比賽|青少男]]
| [[{year}年{tournament}青少年女子雙打比賽|青少女]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 傳奇
| [[{year}年{tournament}45歲以下傳奇雙打比賽|-45]]
| [[{year}年{tournament}45歲及以上傳奇雙打比賽|45+]]
| [[{year}年{tournament}女子傳奇雙打比賽|女子]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 輪椅單打
| [[{year}年{tournament}輪椅男子單打比賽|男子]]
| [[{year}年{tournament}輪椅女子單打比賽|女子]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 輪椅雙打
| [[{year}年{tournament}輪椅男子雙打比賽|男子]]
| [[{year}年{tournament}輪椅女子雙打比賽|女子]]
]=]},
	["溫布頓網球錦標賽"] = {[=[|-
! scope="row" style="font-weight: normal; text-align: right;" | 單打
| [[{year}年{tournament}男子單打比賽|男子]]
| [[{year}年{tournament}女子單打比賽|女子]]
|
| [[{year}年{tournament}青少年男子單打比賽|青少男]]
| [[{year}年{tournament}青少年女子單打比賽|青少女]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 雙打
| [[{year}年{tournament}男子雙打比賽|男子]]
| [[{year}年{tournament}女子雙打比賽|女子]]
| [[{year}年{tournament}混合雙打比賽|混合]]
| [[{year}年{tournament}青少年男子雙打比賽|青少男]]
| [[{year}年{tournament}青少年女子雙打比賽|青少女]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 傳奇
| [[{year}年{tournament}男子雙打邀請賽|男子]]
| [[{year}年{tournament}女子雙打邀請賽|女子]]
| [[{year}年{tournament}45歲及以上男子雙打邀請賽|45+]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 輪椅雙打
| [[{year}年{tournament}輪椅男子雙打比賽|男子]]
| [[{year}年{tournament}輪椅女子雙打比賽|女子]]
]=]},
	["美國網球公開賽"] = {[=[|-
! scope="row" style="font-weight: normal; text-align: right;" | 單打
| [[{year}年{tournament}男子單打比賽|男子]]
| [[{year}年{tournament}女子單打比賽|女子]]
|
| [[{year}年{tournament}青少年男子單打比賽|青少男]]
| [[{year}年{tournament}青少年女子單打比賽|青少女]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 雙打
| [[{year}年{tournament}男子雙打比賽|男子]]
| [[{year}年{tournament}女子雙打比賽|女子]]
| [[{year}年{tournament}混合雙打比賽|混合]]
| [[{year}年{tournament}青少年男子雙打比賽|青少男]]
| [[{year}年{tournament}青少年女子雙打比賽|青少女]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 傳奇
| [[{year}年{tournament}男子冠軍邀請賽|男子]]
| [[{year}年{tournament}女子冠軍邀請賽|女子]]
| [[{year}年{tournament}混合雙打冠軍邀請賽|混合]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 輪椅單打
| [[{year}年{tournament}輪椅男子單打比賽|男子]]
| [[{year}年{tournament}輪椅女子單打比賽|女子]]
| [[{year}年{tournament}_四輪椅單打比賽|四輪]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 輪椅雙打
| [[{year}年{tournament}輪椅男子雙打比賽|男子]]
| [[{year}年{tournament}輪椅女子雙打比賽|女子]]
| [[{year}年{tournament}四輪椅雙打比賽|四輪]]
]=]},
	["ABN AMRO世界網球賽"] = {[=[|-
| [[{prefix}_{year}年{tournament}單打比賽|單打]]
| [[{prefix}_{year}年{tournamentd}雙打比賽|雙打]]
|-
| [[{prefix}_{year}年{tournament}輪椅單打比賽|輪椅單打]]
| [[{prefix}_{year}年{tournamentd}輪椅雙打比賽|輪椅雙打]]]=]},
	["doublestwotourneys"] = {[=[|-
! scope="row" style="font-weight: normal; text-align: right;" | 單打
| [[{prefix}_{year}年{tournament}單打比賽|男子]]
| [[{prefix}_{year}年{tournamentd}單打比賽|女子]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 雙打
| [[{prefix}_{year}年{tournament}雙打比賽|男子]]
| [[{prefix}_{year}年{tournamentd}雙打比賽|女子]]]=]},
	[""] = {[=[|-
! scope="row" style="font-weight: normal; text-align: right;" | 單打
| [[{prefix}_{year}年{tournament}男子單打比賽|男子]]
| [[{prefix}_{year}年{tournament}女子單打比賽|女子]]
|-
! scope="row" style="font-weight: normal; text-align: right;" | 雙打
| [[{prefix}_{year}年{tournament}男子雙打比賽|男子]]
| [[{prefix}_{year}年{tournament}女子雙打比賽|女子]]]=]}}

local function pullItem(value, default)
	value = value
	if type(STYLES[value]) == "string" then
		value = STYLES[value]
	end
	if STYLES[value] then
		return STYLES[value][1]
	else
		return STYLES[default][1]
	end
end

function p._main(args)
	local default = ""
	if args[2] ~= args[3] then
		default = "doublestwotourneys"
	end

	print('{| style="border-spacing: 0.6em 0; margin: auto; ' ..
		  'text-align: center;"')
	print(string.gsub(pullItem(args.type, default), "{(%a+)}",
		{prefix = args.prefix or "", year = args[1], tournament = args[2],
		 tournamentd = args[3]}))
	print("|}")
	return getBuffer("\n")
end

function p.main(frame)
	local args = require("Module:Arguments").getArgs(frame)
	return p._main(args)
end

return p