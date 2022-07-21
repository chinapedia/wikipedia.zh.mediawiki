-- This module implements {{HK-MTR icon}} and {{HK-MTR color}}.
 
local getArgs = require('Module:Arguments').getArgs
local data = mw.loadData('Module:MTR/data')
 
local p = {}
 
local function makeInvokeFunction(funcName)
	-- makes a function that can be returned from #invoke, using
	-- [[Module:Arguments|Module:Arguments]].
	return function (frame)
		local args = getArgs(frame, {parentOnly = true})
		return p[funcName](args)
	end
end
 
local function getColor(code)
	return data.colors[code] or '000'
end
 
p.colorbyname = makeInvokeFunction('_colorbyname')
 
function p._colorbyname(args)
	local code = args[1] or ''
	code = code:upper()
	return getColor(code)
end
 
p.icon = makeInvokeFunction('_icon')
 
function p._icon(args)
	-- Retrieve arguments
	local code = args[1] or ''
	local link = args[2] or args.link
	local text = args[3] or args.text
 
	-- Fetch data from the data module
	code = code:upper() -- Convert to upper case
	local name = data.names[code]
	if not name then
		-- If we didn't find a name corresponding to the code, exit with a wikitext error.
		return '<strong class="error">Error: "' .. tostring(code) .. '" is not a valid code.</strong>'
	end
	local color = getColor(code)
 
	-- Format the link name
	link = link or name
	if data.needs_dab[link] then
		link = '香港' .. link -- 後備迴避歧義用參數，儘管在中文維基百科用不上，如有必要請到模塊:MTR/data修改。
	end
 
	-- Format the text
	text = text or name .. '轉車站'
 
	-- Build the link
	return '[['_.._link_.._'|<span title="' .. text .. '" style="color:#' .. color .. ';font-size:120%">█</span>]]'
end
 
return p