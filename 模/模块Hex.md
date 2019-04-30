local hex = {}
local getArgs = require("Module:Arguments").getArgs
local RESOLUTION = 12 -- I have no idea how many places the floating point is good to, this is just a guess.

-- initialize conversion arrays; these should remain in scope for individual conversions
local d2h = mw.loadData("Module:Hex/data table")

-- functions for other modules to use

-- internal one-byte lookups
hex._d2hbyte = function(val)
    -- assumes decimal is a number
    return d2h[val] or '00'
end

hex._h2dbyte = function(val)
    -- assumes hex is a string
    return tonumber('0x' .. val)
end

-- internal multi-byte lookups
hex._d2h = function(val, integer)
    local negative -- true if number is negative
    if ("string" == type(val)) then
        integer = integer or (not mw.ustring.match(val, "[%.%,]"))
        val = tonumber(val) or error('bad value for Module:hex._d2h')
         -- decimal input can be string, but is required to read as a floating point number for now
         -- as a safeguard, integer as argument or through lack of a "." or "," [not sure if the latter is possible] prevents fractions
    end
    if val<0 then
        val = 0 - val
        negative = true
    end
    local whole = math.floor(val)
    local fraction = val - whole
    local output = "" -- will be made big-endian by adding at the start
    repeat
        local littlest, bigger = whole % 256, math.floor(whole / 256)
        output = hex._d2hbyte(littlest) .. output
        whole = bigger
    until (0 == whole)
    if negative then output = "-" .. output end
    if (not (integer and (fraction > 0))) then
        return output
    end
     -- do fractional conversion to hex
    output = output .. "."
    local count = RESOLUTION -- makes sure it doesn't loop endlessly from hallucinatory floating point data or repeating fraction
    while (fraction > 0) and (count > 0) do
        local shift = fraction * 256
        local biggest, littler = math.floor(shift), (shift) % 1
        output = output .. hex._d2hbyte(biggest)
        fraction = shift
        count = count - 1
    end
    return output
end

local trim = function(text)
    return mw.ustring.gsub(text, "[^0-9A-Fa-f]", "")
end
    
hex._h2d = function(val)
    decwhole = 0
    if ('string' ~= type(val)) then error("hexadecimal value should be text") end
    local whole, fraction = mw.ustring.match(val, "(.-)%.(.-)")
    whole = whole or val
    fraction = fraction or ""
    negative = mw.ustring.match(whole, "%-")
    whole, fraction = trim(whole), trim(fraction)
    if 1 == (#whole % 2) then whole = "0" .. whole end
    if 1 == (#fraction %2) then fraction = fraction .. "0" end
     -- these assume an even number of digits now exist!
    while (#whole > 0) do
        decwhole = decwhole * 256 + hex._h2dbyte(string.sub(whole, 1, 2))
        whole = string.sub(whole, 3, -1)
    end
    local decfraction = 0
    while (#fraction > 0) do
        decfraction = (decfraction + hex._h2dbyte(string.sub(decfraction, -2, -1)))/256
        fraction = string.sub(fraction, 1, -3)
    end
    return ((negative and -1) or 1)*(decwhole + decfraction)
end

hex._even = function(text)
	if (#text % 2 == 1) then
        text = "0" .. text
    end
    return text
end

hex._hexstring = function(text)
    text = mw.text.trim(text)
    text = mw.ustring.gsub(text, "%X", "")
    text = hex._even(text)
    local output = {}
    for i = 1, #text/2 do
        table.insert(output, string.char(hex._h2dbyte(string.sub(text, i*2-1, i*2))))
    end
    return table.concat(output, "")
end

hex._unicode = function(text)
    text = mw.ustring.gsub(text, "%X+", " ")
    text = mw.text.trim(text)
    -- the rule is that any contiguous group of hex digits is one unicode point
    -- so U+2022 +2023 2024 is three chars, but U+20 22 is two chars, sorry
    prowl = string.gmatch(text, "%x+")
    output = {}
    utf = ""
    local prefix
    repeat
        group = prowl()
        if group then
        	-- convert group to UTF8 hex bytes; then hexstring the hex bytes
        	local outgroup = ""
        	local bytes
        	groupval = hex._h2d(group)
        	if (groupval < 128) then
        		prefix = 0
        		bytes = 1
        	elseif (groupval < 2048) then
        		prefix = 192
        		bytes = 2
        	elseif (groupval < 65536) then
        		prefix = 224
        		bytes = 3
        	elseif (groupval < 2097152) then
        		prefix = 240
        		bytes = 4
        	elseif (groupval < 1073741824) then
        		prefix = 248
        		bytes = 5
        	elseif (groupval < 34359738368) then
        		prefix = 252
        		bytes = 6
        	else
        		error ("[[Module:Hex|Module:Hex]] received invalid UTF8")
        	end
        	repeat
        		local outbyte = groupval % 64
        		groupval = math.floor(groupval/64)
        		if (#outgroup == bytes - 1) then
        			outbyte = outbyte + prefix
        		else
        			outbyte = outbyte + 128
        		end
        		outgroup = string.char(outbyte) .. outgroup
        	until (#outgroup >= bytes)
        	table.insert(output, outgroup)

        end
    until not group
    return table.concat(output, "")
end

hex._hexdump = function(text)
    local output = {}
    local stringtable = {string.byte(text, 1, 7500)} -- empirically determined in a sandbox as 7997 to avoid stack error
    for i = 1, #stringtable do
    	local caption = string.sub(text,i,i)
    	if caption == " " then caption = " " end
        table.insert(output, '<div style="position:relative;display:inline;">'..(hex._d2hbyte(stringtable[i]) or "`")..'<span style="position:absolute;color:red;top:-11px;left:3px;font-size:85%;">' .. caption .. '</span></div>')
    end
    return table.concat(output, " ")
end

-- template front doors
hex.d2h = function(frame)
    local args = getArgs(frame)
    return hex._d2h(args.val or args[1], args.integer)
end

hex.h2d = function(frame)
    local args = getArgs(frame)
    return hex._h2d(args.val or args[1])
end

hex.hexstring = function(frame)
    local args = getArgs(frame)
    return hex._hexstring(args.val or args[1])
end

hex.unicode = function(frame)
    local args = getArgs(frame)
    return hex._unicode(args.val or args[1])
end

hex.hexdump = function(frame)
    local args = getArgs(frame)
    local text = args.text or args[1] or ""
    local nowiki = args.nowiki
    if args.transclude then -- you can't just do this in the parameter, or it will evaluate it before sending it!
    	text = "{{" .. text .. "}}"
    end
    if args.preprocess then -- for some transclusions, this will return a strip marker
        text = frame:preprocess(text)
    end
    if args.unstrip then -- and if so, then this will return the HTML that marker would reveal
        text = mw.text.unstrip(text)
    end
    if (not args.plain) then -- as a "control", plain returns the text as it would appear without dump
    	text = hex._hexdump(text or "")
    end
    if nowiki then 
        text = frame:preprocess("<nowiki><pre>" .. text .. "</pre></nowiki>")
    end
    text = "<code>" .. text .. "</code>"
    return text
end

return hex