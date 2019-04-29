---------------------------------------------------------------------
-- Module:Citation - Lua module for Citation auxiliary templates
---------------------------------------------------------------------
-- For the {{citation}} formatting functions, see: Module:Citation/CS1
--                               (see NOTES at bottom)
--require "mw.text"

local z = {
    wikitext = require("Module:Wikitext"),
    extensiontags = {
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
}

function trim( str )
    if str == nil then
        return nil;
    end
    return str:match( "^%s*(.-)%s*$" );
end

function hideinprint(content)
    return content
end

function onlyinprint(content)
    return ""
end

-- This returns a string with HTML character entities for wikitext markup characters.
function wikiescape(text)
    text = text:gsub( '[&\'%[%]{|}]', {    
            ['&'] = '&',    
            ["'"] = '&#39;',    
            ['['] = '[',    
            [']'] = ']',	
            ['{'] = '{',	
            ['|'] = '|',	
            ['}'] = '}' } );
    return text;
end

function createTag(t, frame)
    local name = t.name or "!-- --"
    local content = t.contents or ""
    local attrs = {}
    if ( z.extensiontags[name] ) then
        -- We have to preprocess these, so that they are properly turned into so-called "strip markers" in the generated wikitext.
        if ( not frame ) then error ("Please supply an extra frame argument to the createTag() function.") end
        local params = {}
        for n,v in pairs(t.params) do
            table.insert(params, "|" .. n .. "=" .. v)
        end
        return frame:preprocess("{{#tag:" .. name .. "|" .. content .. table.concat(params) .. "}}")
    else   
        for n,v in pairs(t.params) do
            if (v) then
                table.insert(attrs, n .. "=\"" .. wikiescape(v) .. "\"")
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

--[[
This is a clone of mw.text.nowiki.  When the mw.text library is installed,
this can be replaced by a call to that library. ]]
function nowiki( s )
    -- string.gsub is safe here, because we're only caring about ASCII chars
    s = string.gsub( s, '["&\'<=>%[%]{|}]', {
        ['"'] = '"',
        ['&'] = '&',
        ["'"] = '&#39;',
        ['<'] = '<',
        ['='] = '=',
        ['>'] = '>',
        ['['] = '[',
        [']'] = ']',
        ['{'] = '{',
        ['|'] = '|',
        ['}'] = '}',
    } )
    s = string.sub( string.gsub( '\n' .. s, '\n[#*:;]', {
        ["\n#"] = "\n#",
        ["\n*"] = "\n*",
        ["\n:"] = "\n:",
        ["\n;"] = "\n;",
    } ), 2 )
    s = string.gsub( s, '://', '://' )
    s = string.gsub( s, 'ISBN ', 'ISBN ' )
    s = string.gsub( s, 'RFC ', 'RFC ' )

    return s
end

function externallinkid(args)
    local sep = args.separator or " "
    args.suffix = args.suffix or ""
    local url_string = args.id
    if args.encode == true or args.encode == nil then
        url_string = mw.uri.encode( url_string );
    end
    
    local t0 = onlyinprint(args.label .. sep .. args.id)
    local t1 = hideinprint("[["_.._args.link_.._"|" .. args.label .. "]]" .. sep .. "[" .. args.prefix .. url_string .. args.suffix .. " " .. nowiki(args.id) .. "]")
    
    return t0 .. t1
end

function doi(id, inactive, nocat)
    local cat = ""
    local text;
    if ( inactive ~= nil ) then 
        text = "[[Digital_object_identifier|doi]]:" .. id;
        cat = cat .. "[[Category:Pages_with_DOIs_inactive_since_"_.._selectyear(inactive)_.._"|Category:Pages with DOIs inactive since " .. selectyear(inactive) .. "]]"
        inactive = " (inactive " .. inactive .. ")" 
    else 
        text = externallinkid({link="Digital object identifier",label="doi",prefix="http://dx.doi.org/",id=id,separator=":"})
        inactive = "" 
    end
    if ( string.sub(id,1,3) ~= "10." ) then
        cat = cat .. "[[Category:含有DOI错误的引用的页面|Category:含有DOI错误的引用的页面]]" .. '<span class="error"> Bad DOI (expected "10." prefix) in code number</span>'
    end
    if ( nocat and nocat ~= "" ) then cat = "" end
    return text .. inactive .. cat    
end

function selectyear( str )
    local lang = mw.getContentLanguage();
    local good, result;
    good, result = pcall( lang.formatDate, lang, 'Y', str )
    if good then 
        return result;
    else
        return '';
    end
end

function anchorid(label, args)
    local P1 = trim(args[1]) or ""
    local P2 = trim(args[2]) or ""
    local P3 = trim(args[3]) or ""
    local P4 = trim(args[4]) or ""
    local P5 = trim(args[5]) or ""
    local anchor = P1 .. P2 .. P3 .. P4 .. P5;
    if anchor ~= '' then  -- See bug description in Citation/CS1
        anchor = mw.uri.anchorEncode( anchor );
    end
    
    return label .. anchor
end

function refid(label, args)
    local p = args.p or ""
    local pp = args.pp or ""
    local loc = args.loc or ""
    return anchorid(label, args) .. p .. pp .. loc    
end

function name(args)
    local P1 = trim(args[1]) or ""
    if ( args[5] ~= nil) then
        return P1 .. " et al."
    else
        local P2 = trim(args[2]) or ""
        local P3 = trim(args[3]) or "" 
        local P4 = trim(args[4]) or ""
        if ( args[4] ~= nil ) then
            P4 = " " .. P4
            P3 = " & " .. P3
            P2 = ", " .. P2
        elseif ( args[3] ~= nil ) then
            P3 = " " .. P3
            P2 = " & " .. P2
        elseif ( args[2] ~= nil ) then
            P2 = " " .. P2            
        end
        return P1 .. P2 .. P3 .. P4
    end 
end

function crossref(frame, label, args)
    local config = frame.args -- the arguments passed BY the template, in the wikitext of the template itself
    local LB = config.BracketLeft or ""
    local RB = config.BracketRight or ""
    local anchor = args.ref or args.Ref or anchorid( label, args)
    local text = name(args)
    local loc = args.loc
    local page
    local pages = args.pp or args.pages
    if pages == nil or pages == '' then
        page = args.p or args.page;
    end 
    if nil == loc then loc = "" else loc = " " .. loc end
    if ( page ~= nil ) then
        local pagesep = config.PageSep or ", p. "
        loc = loc .. pagesep .. page
    end
    if ( pages ~= nil ) then
        local pagessep = config.PagesSep or ", pp. "
        loc = loc .. pagessep .. pages
    end        
    local pagename = args.pagename or ""
    local ps = args.Postscript or ""
    return LB .. "[["_.._pagename_.._"#"_.._anchor_.._"|" .. text .. "]]" .. loc .. RB .. ps
end

function r0(frame, name, group, page)
    if ( name == nil ) then return "" end
    if ( group == nil ) then group = "" end
    local p = ""
    if ( page ~= nil ) then 
        local contents = ":" .. page
        p = createTag({name="sup",contents=contents,params={class="reference",style="white-space:nowrap;"}}) 
    end
    return createTag({name="ref",contents="",params={name=name,group=group}}, frame) .. p
end

function reflist0(frame, config, args)
    local contents = args.refs or ""
    local liststyle = args.liststyle
    local count = args[1]
    local width = args.colwidth
    local group = args.group or config.default_group
    if ( nil == tonumber(count) and nil == width ) then 
        width = count
        count = nil
    end
    if ( nil == liststyle ) then
        if ( "upper-alpha" == group or "lower-alpha" == group or "upper-roman" == group or "lower-roman" == group or "upper-greek" == group or "lower-greek" == group ) then
            liststyle = group
        else
            liststyle = config.default_liststyle
        end
    end
    local params = {}
    params.class = "reflist"    
    params.style = z.wikitext.liststyle(liststyle)
    if ( nil ~= count ) then        
        params.class = params.class .. " references-column-count references-column-count-" .. count
        params.style = params.style .. " " .. z.wikitext.columncountstyle(count)
    end    
    if ( nil ~= width ) then
        params.class = params.class .. " references-column-width"
        params.style = params.style .. " " .. z.wikitext.columnwidthstyle(width)
    end
    local references = createTag({name="references",contents=contents,params={group=group}}, frame)
    return createTag({name="div",contents=references,params=params})
end

function refbegin0(frame, config, args)
    local liststyle = args.liststyle
    local indent = args.indent
    local indentsize = args.indentsize
    local count = args[1]
    local width = args.colwidth
    if ( nil == tonumber(count) and nil == width ) then 
        width = count
        count = nil
    end
    if ( nil == liststyle ) then
        if ( "upper-alpha" == group or "lower-alpha" == group or "upper-roman" == group or "lower-roman" == group or "upper-greek" == group or "lower-greek" == group ) then
            liststyle = group
        else
            liststyle = config.default_liststyle
        end
    end
    local params = {}
    params.class = "refbegin"
    params.style = z.wikitext.liststyle(liststyle)
    if ( nil ~= count ) then        
        params.class = params.class .. " references-column-count references-column-count-" .. count
        params.style = params.style .. " " .. z.wikitext.columncountstyle(count)
    end    
    if ( nil ~= width ) then
        params.class = params.class .. " references-column-width"
        params.style = params.style .. " " .. z.wikitext.columnwidthstyle(width)
    end
    local dlopen
    if ( nil ~= indent ) then
        dlopen = z.wikitext.OpenHTMLTag({name="dl",params={style="text-indent: -" .. (indentsize or "3.2") .. "em;"}})
    else
        dlopen = ""
    end
    return z.wikitext.OpenHTMLTag({name="div",params=params}) .. dlopen
end

function refend0(frame, config, args)
    local indent = args.indent
    local dlclose
    if ( nil ~= indent ) then
        dlclose = "</dl>"
    else
        dlclose = ""
    end
    return dlclose .. "</div>"
end

-- This is used by {{doi}} to create DOI links in the style used in citations.
function z.doi(frame)
    local pframe = frame:getParent()
    local id = pframe.args.id or pframe.args[1] or ""
    return doi(id)
end

-- This is used by {{ISSN}} to create ISSN links in the style used in citations.
function z.ISSN(frame)
    local pframe = frame:getParent()
    local Name = pframe.args[1] or ""
    return hideinprint("[[International_Standard_Serial_Number|ISSN]] [http://www.worldcat.org/search?fq=x0:jrnl&q=n2:" .. Name .. " " .. Name .. "]")
end

-- This is used by templates such as {{SfnRef}} to create the (encoded) anchor name for a Harvard cross-reference hyperlink.
function z.SFNID(frame)
    local pframe = frame:getParent()
    return anchorid('FOOTNOTE', pframe.args)
end

-- This is used by templates such as {{Harvard citation}} to create the Harvard cross-reference text.
function z.Harvard(frame)
    local pframe = frame:getParent()
    return crossref(frame, pframe.args)
end

-- This is used by templates such as {{sfn}} to create the entire cross-reference.
function z.sfn(frame)
    local pframe = frame:getParent()
    pframe.args.Postscript = pframe.args.postscript or pframe.args.ps or ".";
    
    local content = crossref(frame, 'CITEREF', pframe.args)
    local args = { name = refid( 'FOOTNOTE', pframe.args) }
    return createTag({name = "ref", contents = content, params = args}, frame)
end

-- This is used by template {{r}}.
function z.r(frame)
    local pframe = frame:getParent()
    local config = frame.args -- the arguments passed BY the template, in the wikitext of the template itself
    local args = pframe.args -- the arguments passed TO the template, in the wikitext that instantiates the template
    args.page1 = args.page1 or args.page
    local text = ""
    -- This would be shorter using ipairs(), but that doesn't work on an arguments table supplied to a template.
    local index = 1
    while args[index] ~= nil do
        local arg = args[index]
        local t = r0(frame, arg, args.group, args["page" .. index])
        text = text .. t
        index = index + 1
    end
    return text
end

-- This is used by template {{ref label}}.
function z.reflabel(frame)
    local pframe = frame:getParent()
    local config = frame.args -- the arguments passed BY the template, in the wikitext of the template itself
    local args = pframe.args -- the arguments passed TO the template, in the wikitext that instantiates the template
    local P1 = args[1] or ""
    local P2 = args[2] or ""
    local P3 = args[3] or ""
    local id = nil
    local contents = "[[#endnote_"_.._P1_.._P3_.._"|[" .. P2 .. "]]]"
    local params = {}
    params.class="reference"
    if ( args.noid == nil or args.noid == "" ) then params.id = "ref_" .. P1 .. P3 end
    return createTag({name="sup",contents=contents,params=params})
end

-- This is used by template {{note label}}.
function z.notelabel(frame)
    local pframe = frame:getParent()
    local config = frame.args -- the arguments passed BY the template, in the wikitext of the template itself
    local args = pframe.args -- the arguments passed TO the template, in the wikitext that instantiates the template
    local id = args[1] or ""
    local arrow = args[3] or ""
    local postscript = args[4] or ""
    local contents 
    if arrow ~= "" then
        local sup_arrow = createTag({name="sup",contents=arrow,params={}})
        contents = "[[#ref_"_.._id_.._arrow_.._"|<b>" .. sup_arrow .. "</b>]]" .. postscript
        if "none" == arrow then arrow = "^" end -- Change this AFTER using it in the ID parameter and the contents.
    else
        contents = (args[2] or "") .. postscript
    end
    local params = { class="citation wikicite" }
    if id ~= "" and ( args.noid == nil or args.noid == "" ) then 
        params.id = mw.uri.anchorEncode("endnote_" .. id .. arrow)
    end
    return createTag({name="span",contents=contents,params=params})
end

-- This is used by templates {{reflist}} and {{notelist}}.
function z.reflist(frame)
    local pframe = frame:getParent()
    local config = frame.args -- the arguments passed BY the template, in the wikitext of the template itself
    local args = pframe.args -- the arguments passed TO the template, in the wikitext that instantiates the template
    return reflist0(frame, config, args)
end

-- This is used by template {{refbegin}}.
function z.refbegin(frame)
    local pframe = frame:getParent()
    local config = frame.args -- the arguments passed BY the template, in the wikitext of the template itself
    local args = pframe.args -- the arguments passed TO the template, in the wikitext that instantiates the template
    return refbegin0(frame, config, args)
end

-- This is used by template {{refend}}.
function z.refend(frame)
    local pframe = frame:getParent()
    local config = frame.args -- the arguments passed BY the template, in the wikitext of the template itself
    local args = pframe.args -- the arguments passed TO the template, in the wikitext that instantiates the template
    return refend0(frame, config, args)
end

-- This is used by template {{efn}}.
function z.efn(frame)
    local pframe = frame:getParent()
    local config = frame.args -- the arguments passed BY the template, in the wikitext of the template itself
    local args = pframe.args -- the arguments passed TO the template, in the wikitext that instantiates the template
    return createTag({name="ref",contents=(args[1] or ""),params={name=args.name,group=config.default_group}}, frame)
end

return z
---------------------------------------------------------------------
--NOTES
--
-- NOTE A1: This Lua module was originally designed to handle a mix
--      of citation styles, crossing Vancouver style with Wikipedia's
--      local Citation Style 1 (CS1) from {Template:Citation/core}.
--      However, the conflicting positions of parameters, scattered
--      in twisted locations across this module, led to a separate
--      variation just to untangle the CS1 format of citations.
--
-- NOTE D2: The placement of dots and other separators between the
--      displayed parameters has been a continual headache, to keep
--      coordinated with the data in parentheses "(data)". There
--      has been a need to pre-check for the existence of related
--      options, to keep from putting double-dots ".." in some cases.
--      In particular, the omission of the "title=" parameter has led
--      to several cases of a spurious dot ". ." because the original
--      design had treated the title as a mandatory parameter.
--
------------------------------------------------------------------------
--HISTORY:
--18Oct2012 Fixed lead-space in Chapter by omitting " ".
--18Oct2012 Fixed lead-space in Chapter/Title as end " " of Authors/Date/...
--19Oct2012 Put HISTORY comments to log major changes (not typos).
--19Oct2012 Fixed extra dot ".." in Title by omitting at end of "tcommon=...".
--19Oct2012 For pages, put &nbsp in "p. " etc.
--19Oct2012 Enhanced "pages=" to detect lone page as "p." else "pp." prefix.
--19Oct2012 Fixed to show "." after Periodical name (work, newspaper...).
--19Oct2012 Fixed web-link to have spaces "[...  Archived] from the original".
--19Oct2012 Fixed to show ";" between authors & coauthors.
--19Oct2012 Fixed to omit extra "." after coauthors.
--20Oct2012 Fixed COinS data to not urlencode all, as "ctx_ver=Z39.88-2004"
--20Oct2012 Fixed COinS to not end as "&" but use lead "&rft...=" form.
--20Oct2012 Fixed COinS to not url.encode page's "rfr_id=..." pagename.
--20Oct2012 Fixed COinS data when "web" to default to rft.genre "book".
--05Nov2012 Add a span wrapper even when there is no Ref parameter
--15Feb2013 Added Agency for "agency=xx".
--19Feb2013 Put NOTES comments to explain module operation.
--19Feb2013 Copied as Module:Citation/CS1 to alter to match wp:CS1 form.
--19Feb2013 Changed OrigYear to use [__] for CS1 style.
--19Feb2013 Fixed to not show duplicate Publisher/Agency.
--19Feb2013 Moved page-number parameters to after final date.
--19Feb2013 Fixed to not put double-dots after title again.
--20Feb2013 Changed to omit dot "." if already ends with dot.
--20Feb2013 If class "journal" shows Publisher after Periodical/Series.
--20Feb2013 Shifted Format to after Language, and Others after Volume.
--20Feb2013 Set AccessDate + <span class="reference-accessdate">
--20Feb2013 Fixed url when deadurl=no.
--20Feb2013 Added sepc for separator character between parameters.
--20Feb2013 Put "OCLC" for "Online Computer Library Center".
--20Feb2013 Fix empty "authorlink=" as person.link ~= "".
--20Feb2013 Added space after AuthorSep & AuthorNameSep.
--21Feb2013 Added args.contributor (was missing parameter).
--21Feb2013 Fixed EditorSep (was misspelled "EdithorSep").
--21Feb2013 Set OCinSdata.rft_val_fmt = "info:ofi/fmt:kev:mtx:book"
--21Feb2013 Checked to omit blank codes (asin= | doi= etc.).
--21Feb2013 Set enddot to end line if not config.CitationClass "citation".
--21Feb2013 Fixed to show "issn=x" as the ISSN code.
--21Feb2013 Fixed to show "id=x" after Zbl code.
--21Feb2013 Changed to omit double-dot before date when already dot.
--21Feb2013 Order config.CitationClass "citation": Volume, Issue, Publisher.
--21Feb2013 Put warning "Bad DOI (expected "10."..)" in DOI result.
--21Feb2013 Automatically unbolded volume+comma when > 4 long.
--21Feb2013 Changed to allow lowercase "asin-tld".
--22Feb2013 Fixed ref=harv to extract Year from Date.
--22Feb2013 Set Harvard refer. span id if config.CitationClass "citation".
--22Feb2013 Fixed config.CitationClass "citation" as span class="citation".
--22Feb2013 Capitalized "Archived/Retrieved" only when sepc is dot ".".
--23Feb2013 Fixed author editor for "in" or "In" and put space after sepc.
--23Feb2013 Changed to omit dot in "et al." when sepc is "." separator.
--23Feb2013 Fixed "author1-first" to also get args.given or args.given1.
--23Feb2013 Fixed args.article to set Title, after Periodical is Title.
--23Feb2013 Fixed to allow blank Title (such as "contribution=mytitle").
--23Feb2013 Fixed double-dot ".." at end of Editors list
--26Feb2013 Moved "issue=" data to show before "page=".
--26Feb2013 Moved "type=" data to show after "format=".
--26Feb2013 For "pmc=" link, omitted suffix "/?tool=pmcentrez".
--27Feb2013 For coauthors, omitted extra separator after authors.
--27Feb2013 For date, allowed empty date to use month/day/year.
--27Feb2013 Fixed double-dot ".." at end of authors/coauthors list.
--27Feb2013 Reset editor suffix as ", ed." when date exists.
--27Feb2013 Removed duplicate display of "others=" data.
--27Feb2013 Removed parentheses "( )" around "department" TitleNote.
--05Mar2013 Moved Language to follow Periodical or Series.
--05Mar2013 Fixed Edition to follow Series or Volume.
--05Mar2013 Fixed class encyclopaedia to show article as quoted Chapter.
--05Mar2013 Fixed class encyclopaedia to show page as "pp." or "p.".
--07Mar2013 Changed class encyclopaedia to omit "( )" around publisher.
--07Mar2013 Fixed end double-dot by string.sub(idcommon,-1,-1) was "-1,1".
--13Mar2013 Removed enddot "." after "quote=" parameter.
--13Mar2013 Changed config.CitationClass "news" to use "p." page format.
--13Mar2013 Fixed missing "location=" when "web" or "encyclopaedia".
--14Mar2013 Fixed end double-dot after book/work title.
--14Mar2013 Fixed double-dot before "p." or "pp." page number.
--14Mar2013 Fixed config.CitationClass "book" to use p./pp. page.
--
--End