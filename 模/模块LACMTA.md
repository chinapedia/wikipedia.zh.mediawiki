local getArgs = require('Module:Arguments').getArgs
 
local p = {}
 
local function makeInvokeFunction(funcName)
	-- makes a function that can be returned from #invoke, using
	-- [[Module:Arguments|Module:Arguments]].
	return function (frame)
		local args = getArgs(frame, {parentOnly = true})
		return p[funcName](args)
	end
end
 
local function colorbox(color,text,link)
	return '[['..link..'|<span style="border:1px solid darkgray;background-color:'..color..'" title="'..text..'">    </span>]] '
end
 
local t1 = {
	['Harbor Transitway'] = { 'harbor transitway', 'harbor', color='#B8860B', icon='colorbox', },
	['El Monte Busway'] = { 'el monte busway', 'el monte', color='#B8AD93', icon='colorbox', },
	['Regional Connector Transit Corridor'] = { 'regional connector transit corridor', 'regional connector', 'regional', color='#604020', icon='colorbox', },
	['Orange Line'] = { 'orange line', 'orange', icon='img_square', dab=true, },
	['Red Line'] = { 'red line', 'red', icon='img_circle', dab=true, },
	['Purple Line'] = { 'purple line', 'purple', icon='img_circle', dab=true, },
	['Blue Line'] = { 'blue line', 'blue', icon='img_circle', dab=true, },
	['Expo Line'] = { 'expo line', 'expo', icon='img_circle', dab=true, },
	['Green Line'] = { 'green line', 'green', icon='img_circle', dab=true, },
	['Gold Line'] = { 'gold line', 'gold', icon='img_circle', dab=true, },
	['Crenshaw/LAX Line'] = { 'crenshaw/lax line', 'crenshaw/lax', 'crenshaw line', 'crenshaw',  icon='crenshaw', },
	['Silver Line'] = { 'silver line', 'silver', icon='img_square', dab=true, },
}
 
p.icon = makeInvokeFunction('_icon')
 
function p._icon(args)
	local link
	local code = args[1] or ''
	local text = args[2]
	if text then text = '('..text..')' else text = '' end
	local showtext = args.showtext
	for k, v in pairs(t1) do
		for _, name in ipairs(v) do
			if mw.ustring.lower(code) == name then
				if v.dab == true then
					link = k..' (Los Angeles Metro)'
					if showtext then showtext = '[['..link..'|'..k..']] ' else showtext = '' end
				else
					link = k
					if showtext then showtext = '[['..k..'|'..k..']] ' else showtext = '' end
				end
				if v.icon == 'colorbox' then
					return colorbox(v.color,k,k)..showtext..text
				elseif v.icon == 'crenshaw' then
					return '[[File:LACMTA_Circle_Crenshaw_Line.svg|'..(args.size or 17)..'px]] '..showtext..text
				elseif v.icon == 'img_circle' then
					return '[[File:LACMTA_Circle_'..k..'.svg|'..(args.size or 17)..'px]] '..showtext..text
				elseif v.icon == 'img_square' then
					return '[[File:LACMTA_Square_'..k..'.svg|'..(args.size or 17)..'px]] '..showtext..text
				end
			end
		end
	end
	return colorbox('#fff',code..' Line',code..' Line (Los Angeles Metro)')..text
end
 
return p