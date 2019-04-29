--require "mw.text"
--require "string"
--require "table"

local z = {
    mw = require "Module:mw"
}

-- This splits a string of name="value" pairs into a table.
-- The common use of this is to parse a single template argument that specifies HTML element attributes all in one lump.
function z.SplitHTMLElementParams(s)
    local params = {}
    for name,value in string.gmatch(s, "([%w_]+)=\"([^\"]*)\"%s*") do
        params[name] = value
    end
    return params
end

-- This returns a string quoted using quotation marks, using HTML character entities for embedded quotation marks and ampersands.
function z.quote(t)
    local chars = {}
    for i=1,#t do
        local char = t:sub(i,i)
        local byte = char:byte()
        if ( byte == 34 or byte == 38 ) then
            table.insert(chars, "&#" .. tostring(byte) .. ";")
        else
            table.insert(chars, char)
        end
    end
    return "\"" .. table.concat(chars) .. "\""
end

function z.CombineHTMLElementParams(params)
    local attrs = {}
    for n,v in pairs(params) do
        table.insert(attrs, n .. "=" .. z.quote(v))
    end
    return table.concat(attrs, " ")
end

function RawOpenHTMLTag(name,params)
    local attr = z.CombineHTMLElementParams(params)
    return "<" .. name .. " " .. attr .. ">"
end

function z.OpenHTMLTag(t)
    local name = t.name or "!-- --"
    if ( "nowiki" == name or "ref" == name or "pre" == name or "gallery" == name or "poem" == name or "references" == name ) then
        error(name .. "：OpenHTMLTag仅适用于非扩展标签。")
    end
    return RawOpenHTMLTag(name,t.params)
end

-- This returns the canonical form of an editor-supplied time, for use in cleanup category names.
function z.canonicalcleanuptime(t)
    return t -- FIXME: This isn't right.
end

-- This returns a list formatted into a (intended to be human-readable) comma-separated form.
function z.oxfordlist(args,separator,ampersand)
    local text = ""
    separator = separator or ","
    ampersand = ampersand or "and"
    for index,arg in ipairs(args) do
        if (index < 2) then 
            -- Add nothing before the first item.
        elseif (args[index + 1] ~= nil) then
            text = text .. separator .. " " 
        elseif (index > 2) then 
            text = text .. separator .. " " .. ampersand .. " "
        else
            text = text .. " " .. ampersand .. " "
        end
        text = text .. arg
    end
    return text
end

-- These return various CSS strings.
function z.columncountstyle(n)
    return "-moz-column-count:" .. n .. "; -webkit-column-count:" .. n .. "; column-count:" .. n .. ";"
end
function z.columnwidthstyle(n)
    return "-moz-column-width:" .. n .. "; -webkit-column-width:" .. n .. "; column-width:" .. n .. ";"
end
function z.liststyle(n)
    return "list-style-type:" .. n .. ";"
end

return z