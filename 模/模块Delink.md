-- This module de-links most wikitext.

p = {}

local function delinkReversePipeTrick(s)
    if mw.ustring.match(s, "^%[%[|.*[|\n]") then -- Check for newlines or multiple pipes.
        return s
    else
        return mw.ustring.match(s, "%[%[|(.*)%]%]")
    end
end

local function delinkPipeTrick(s)
    local linkarea, display = "", ""
    -- We need to deal with colons, brackets, and commas, per [[Help:Pipe_trick|Help:Pipe trick]].
    
    -- First, remove the text before the first colon, if any.
    if mw.ustring.match(s, ":") then
        s = mw.ustring.match(s, "%[%[.-:(.*)|%]%]")
    -- If there are no colons, grab all of the text apart from the square brackets and the pipe.
    else
        s = mw.ustring.match(s, "%[%[(.*)|%]%]")
    end
    
    -- Next up, brackets and commas.
    if mw.ustring.match(s, "%(.-%)$") then -- Brackets trump commas.
        s = mw.ustring.match(s, "(.-) ?%(.-%)$")
    elseif mw.ustring.match(s, ",") then -- If there are no brackets, display only the text before the first comma.
        s = mw.ustring.match(s, "(.-),.*$")
    end
    return s
end

local function delinkWikilink(s)
    local result = s
    -- Deal with the reverse pipe trick.
    if mw.ustring.match(result, "%[%[|") then
        return delinkReversePipeTrick(result)
    end
    
    result = mw.uri.decode(result, "PATH") -- decode percent-encoded entities. Leave underscores and plus signs.
    result = mw.text.decode(result, true) -- decode HTML entities.
    
    -- Check for bad titles. To do this we need to find the
    -- title area of the link, i.e. the part before any pipes.
    local titlearea
    if mw.ustring.match(result, "|") then -- Find if we're dealing with a piped link.
        titlearea = mw.ustring.match(result, "^%[%[(.-)|.*%]%]")
    else
        titlearea = mw.ustring.match(result, "^%[%[(.-)%]%]")
    end
    -- Check for bad characters.
    if mw.ustring.match(titlearea, "[%[%]<>{}%%%c\n]") then
        return s
    end
    
    -- Check for categories, interwikis, and files.
    local colonprefix = mw.ustring.match(result, "%[%[(.-):.*%]%]") or "" -- Get the text before the first colon.
    if mw.language.isKnownLanguageTag(colonprefix)
    or mw.ustring.match(colonprefix, "^[Cc]ategory$")
    or mw.ustring.match(colonprefix, "^[Ff]ile$")
    or mw.ustring.match(colonprefix, "^[Ii]mage$") then
        return ""
    end
    
    -- Remove the colon if the link is using the [[Help:Colon_trick|Help:Colon trick]].
    if mw.ustring.match(result, "%[%[:") then
        result = "[[" .. mw.ustring.match(result, "%[%[:(.*%]%])")
    end
    
    -- Deal with links using the [[Help:Pipe_trick|Help:Pipe trick]].
    if mw.ustring.match(result, "^%[%[[^|]*|%]%]") then
        return delinkPipeTrick(result)
    end
    
    -- Find the display area of the wikilink
    if mw.ustring.match(result, "|") then -- Find if we're dealing with a piped link.
        result = mw.ustring.match(result, "^%[%[.-|(.+)%]%]")
        -- Remove new lines from the display of multiline piped links,
        -- where the pipe is before the first new line.
        result = mw.ustring.gsub(result, "\n", "")
    else
        result = mw.ustring.match(result, "^%[%[(.-)%]%]")
    end

    return result
end

local function delinkURL(s)
    -- Assume we have already delinked internal wikilinks, and that
    -- we have been passed some text between two square brackets [foo].
    
    -- If the text contains a line break it is not formatted as a URL, regardless of other content.
    if mw.ustring.match(s, "\n") then
        return s
    end
    
    -- Check if the text has a valid URL prefix and at least one valid URL character.
    local valid_url_prefixes = {"//", "http://", "https://", "ftp://", "gopher://", "mailto:", "news:", "irc://"} 
    local url_prefix
    for i,v in ipairs(valid_url_prefixes) do
        if mw.ustring.match(s, '^%[' .. v ..'[^"%s].*%]' ) then
            url_prefix = v
            break
        end
    end
    
    -- Get display text
    if not url_prefix then
        return s
    end
    s = mw.ustring.match(s, "^%[" .. url_prefix .. "(.*)%]") -- Grab all of the text after the URL prefix and before the final square bracket.
    s = mw.ustring.match(s, '^.-(["<> ].*)') or "" -- Grab all of the text after the first URL separator character ("<> ).
    s = mw.ustring.match(s, "^%s*(%S.*)$") or "" -- If the separating character was a space, trim it off.
    
    s_decoded = mw.text.decode(s, true)
    if mw.ustring.match(s_decoded, "%c") then
        return s
    else    
        return s_decoded
    end
end

local function delinkLinkClass(s, pattern, delinkFunction)
    if not type(s) == "string" then
        error("Attempt to de-link non-string input.", 2)
    end
    if not ( type(pattern) == "string" and mw.ustring.sub(pattern, 1, 1) == "^" ) then
        error('Invalid pattern detected. Patterns must begin with "^".', 2)
    end
    -- Iterate over the text string, and replace any matched text. using the 
    -- delink function. We need to iterate character by character rather 
    -- than just use gsub, otherwise nested links aren't detected properly.
    local result = ""
    while mw.ustring.len(s) > 0 do
        -- Replace text using one iteration of gsub.
        s = mw.ustring.gsub(s, pattern, delinkFunction, 1)
        -- Append the left-most character to the result string.
        result = result .. mw.ustring.sub(s, 1, 1)
        s = mw.ustring.sub(s, 2, -1)
    end
    return result
end

local function _delink(args)
    local text = args[1] or ""
    if args.refs == "yes" then
        -- Remove any [[Help:Strip_markers|Help:Strip markers]] representing ref tags. In most situations 
        -- this is not a good idea - only use it if you know what you are doing!
        text = mw.ustring.gsub(text, "UNIQ%w*%-ref%-%d*%-QINU", "")
    end
    if not (args.comments == "no") then
        text = mw.ustring.gsub(text, "<!%-%-.-%-%->", "") -- Remove html comments.
    end
    if not (args.wikilinks == "no") then
        text = delinkLinkClass(text, "^%[%[.-%]%]", delinkWikilink) -- De-link wikilinks.
    end
    if not (args.urls == "no") then
        text = delinkLinkClass(text, "^%[.-%]", delinkURL) -- De-link URLs.
    end
    if not (args.whitespace == "no") then
        -- Replace single new lines with a single space, but leave double new lines
        -- and new lines only containing spaces or tabs before a second new line.
        text = mw.ustring.gsub(text, "([^\n \t][ \t]*)\n([ \t]*[^\n \t])", "%1 %2")
        text = mw.ustring.gsub(text, "[ \t]+", " ") -- Remove extra tabs and spaces.
    end
    return text
end

function p.delink(frame)
    local args
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. If the invoking template passed any args, use
        -- them. Otherwise, use the args that were passed into the template.
        args = frame:getParent().args
        for k, v in pairs(frame.args) do
            args = frame.args
            break
        end
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
    return _delink(args)
end

return p