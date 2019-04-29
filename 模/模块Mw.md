local extensiontags = {
    nowiki = true,
    ref = true,
    gallery = true,
    pre = true,
    source = true,
    categorytree = true,
    charinsert = true,
    hiero = true,
    imagemap = true,
    inputbox = true,
    math = true,
    poem = true,
    ref = true,
    references = true,
    syntaxhighlight = true,
    timeline = true,
}

local text = {
    -- This returns a string with HTML character entities for wikitext markup characters.
    -- FIXME: Space at the start of a line isn't handled.
    escape = function (text)
        text = text:gsub( '[&\'%[%]{|}]', {    
                ['&'] = '&',    
                ["'"] = '&#39;',	
                ['['] = '[',	
                [']'] = ']',	
                ['{'] = '{',	
                ['|'] = '|',	
                ['}'] = '}' } );
        return text;
    end,
}

text.tag = function (t, frame)
    local name = t.name or "!-- --"
    local content = t.contents or ""
    if ( extensiontags[name] ) then
        -- We have to preprocess these, so that they are properly turned into so-called "strip markers" in the generated wikitext.
        if ( not frame ) then error ("请提供一个额外的框架参数以执行 mw.text.tag() 功能。") end
        local params = {}
        for n,v in pairs(t.params) do
            table.insert(params, "|" .. n .. "=" .. v)
        end
        return frame:preprocess("{{#tag:" .. name .. "|" .. content .. table.concat(params) .. "}}")
    else
        -- Everything else we can just generate directly, without calling the preprocessor.
        local attrs = {}
        for n,v in pairs(t.params) do
            if (v) then
                table.insert(attrs, n .. "=\"" .. text.escape(v) .. "\"")
            else
                table.insert(attrs, n)
            end
        end
        if ("" == content) then
            return "<" .. name .. " " .. table.concat(attrs, " ") .. "/>"
        else
            return "<" .. name .. " " .. table.concat(attrs, " ") .. ">" .. content .. "</" .. name .. ">"
        end
    end
end

-- FIXME: How much of the below is obsolete now that we have the mw.uri module?
local url = {
    server = "zh.wikipedia.org",
    -- Return a string encoded for use in a URL, equivalent to the parser function {{urlencode:}}.
    --   0-9A-Za-z --> no change
    --   -._       --> no change
    --   ' ' --> '+'
    --   '*' --> '%XX' where XX is hex value of character '*' other than those above
    encode = function (t)
        return mw.uri.encode( t );
    end,
    -- This returns a string encoded for use in a URL, equivalent to the parser function {{anchorencode:}}.
    encodeAnchor = function (t)
        return mw.uri.anchorEncode( t );
    end,
}

url["local"] = function (title, query)
    return "/w/index.php?title=" .. url.encode(title) .. "&" .. query
end
url.full = function (title, query)
    return "//" .. url.server .. "/w/index.php?title=" .. url.encode(title) .. "&" .. query
end

-- Insert as the global functions if they haven't been supplied by Scribunto.
-- FIXME: I'm told this doesn't work. If not, take it out.
if ( nil == mw ) then mw = {} end
if ( nil == mw.text ) then mw.text = text end
if ( nil == mw.url ) then mw.url = url end

-- Return our replacement functions as this module's own exported function table.
return { url = url, text = text }