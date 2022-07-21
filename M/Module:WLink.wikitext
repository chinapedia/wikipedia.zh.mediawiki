local WLink = { suite  = "WLink",
                serial = "2016-10-05" };
--[=[
ansiPercent()
formatURL()
getArticleBase()
getBaseTitle()
getExtension()
getFile()
getFragment()
getLanguage()
getNamespace()
getPlain()
getProject()
getTarget()
getTargetPage()
getTitle()
getWeblink()
isBracketedLink()
isBracketedURL()
isCategorization()
isExternalLink()
isInterlanguage()
isInterwiki()
isMedia()
isTitledLink()
isValidLink()
isWikilink()
wikilink()
failsafe()
]=]



-- local globals
local URLutil = false;



local utilURL = function ()
    -- Attach URLutil library module
    -- Postcondition:
    --     Returns  table, with URLutil library
    --     Throws error, if not available
    if not URLutil then
        local lucky, util = pcall( require, "Module:URLutil" );
        if lucky then
            if type( util ) == "table" then
                URLutil = util.URLutil();
            end
            util = "library URLutil invalid";
        end
        if type( URLutil ) ~= "table" then
            error( util, 0 );
        end
    end
    return URLutil;
end -- utilURL()



local contentExtlink = function ( attempt )
    -- Retrieve span of external link between brackets
    -- Precondition:
    --     attempt  -- string, with presumable link
    --                         the first char is expected to be "["
    -- Postcondition:
    --     Returns  string, number, number
    --                  string including whitespace
    --                  number with index of relevant "["
    --                  number with index after relevant "]"
    --              false if nothing found
    local r1 = false;
    local r2 = false;
    local r3 = attempt:find( "]", 2, true );
    if r3 then
        local s = attempt:sub( 2,  r3 - 1 );
        local i = s:find( "[", 1, true );
        if i then
            r1 = s:sub( i + 1 );
            r2 = i;
        else
            r1 = s;
            r2 = 1;
        end
    else
        r3 = false;
    end
    return r1, r2, r3;
end -- contentExtlink()



local contentWikilink = function ( attempt )
    -- Retrieve span of wikilink between brackets
    -- Precondition:
    --     attempt  -- string, with presumable link
    --                        the first two chars are expected to be "[["
    -- Postcondition:
    --     Returns  string, number, number
    --                  string including whitespace
    --                  number with index of relevant "[["
    --                  number with index after relevant "]]"
    --              false if nothing found
    local r1 = false;
    local r2 = false;
    local r3 = attempt:find( "]]", 3, true );
    if r3 then
        local s = attempt:sub( 3,  r3 - 1 );
        local i = s:find( "[[", 1, true );
        if i then
            r1 = s:sub( i + 2 );
            r2 = i;
        else
            r1 = s;
            r2 = 1;
        end
    end
    return r1, r2, r3;
end -- contentWikilink()



local extractExtlink = function ( attempt )
    -- Retrieve external link
    -- Precondition:
    --     attempt  -- string, with presumable link
    --                        the first char is expected to be "["
    -- Postcondition:
    --     Returns  string, string
    --                  first with target and title
    --                  second result false if not titled
    --              false if nothing found
    local r1 = false;
    local r2 = false;
    local s = contentExtlink( attempt );
    if s then
        local i = s:find( "%s", 1 );
        if i then
            r1 = s:sub( 1,  i - 1 );
            r2 = mw.text.trim( s:sub( i + 1 ) );
            if r2 == "" then
                r2 = false;
            end
        else
            r1 = s;
        end
        if r1 then
            r1 = mw.text.trim( r1 );
            if r1 == ""  or
               not utilURL().isResourceURL( r1 ) then
                r1 = false;
            end
        end
        if not r1 then
            r2 = false;
        end
    end
    return r1, r2;
end -- extractExtlink()



local extractWikilink = function ( attempt )
    -- Retrieve wikilink
    -- Precondition:
    --     attempt  -- string, with presumable link
    --                        the first two chars are expected to be "[["
    -- Postcondition:
    --     Returns  string, string
    --                  first with target
    --                  second result title, or false if not piped
    --              false if nothing found
    local r1 = false;
    local r2 = false;
    local s = contentWikilink( attempt );
    if s then
        local i = s:find( "|", 1, true );
        if i then
            r1 = s:sub( 1,  i - 1 );
            r2 = s:sub( i + 1 );
        else
            r1 = s;
        end
        r1 = mw.text.trim( r1 );
        if r1 == "" then
            r1 = false;
        else
            r1 = r1:gsub( "_",        " " )
                   :gsub( " ",   " " )
                   :gsub( " ", " " )
                   :gsub( " ",   " " )
                   :gsub( " ",  " " )
                   :gsub( "  +",      " " );
            r1 = mw.text.decode( r1 );
        end
    end
    return r1, r2;
end -- extractWikilink()



local prefix = function ( ask, ahead )
    -- Interprete prefix of language or project type
    -- Precondition:
    --     ask    -- string, with presumable prefix
    --     ahead  -- true, if first segment
    -- Postcondition:
    --     Returns  string,string or nil
    --                     first  string one of "lead", "lang", "project"
    --                     second string is formatted value
    --                       type is one of "lead", "lang", "project"
    --              nil if nothing found
    local r1, r2;
    local prefixes = { b           = true,
                       c           = "commons",
                       d           = true,
                       commons     = true,
                       m           = "meta",
                       mediawiki   = "mw",
                       mw          = true,
                       meta        = true,
                       n           = true,
                       q           = true,
                       s           = true,
                       simple      = false,
                       v           = true,
                       voy         = true,
                       w           = true,
                       wikibooks   = "b",
                       wikidata    = "d",
                       wikinews    = "n",
                       wikipedia   = "w",
                       wikiquote   = "q",
                       wikisource  = "s",
                       wikiversity = "v",
                       wikivoyage  = "voy",
                       wikt        = true,
                       wiktionary  = "wikt"
                     };
    local s = mw.text.trim( ask );
    if s == "" then
        if ahead then
            r1 = "lead";
            r2 = true;
        end
    else
        local p;
        s = s:lower();
        p = prefixes[ s ];
        if p == true then
            r1 = "project";
            r2 = s;
        elseif p then
            r1 = "project";
            r2 = p;
        elseif p == false then
            r1 = "lang";
            r2 = s;
        elseif s:match( "^%l%l%l?$" )
               and  mw.language.isSupportedLanguage( s ) then
            r1 = "lang";
            r2 = s;
        end
    end
    return r1, r2;
end -- prefix()



local target = function ( attempt, lonely )
    -- Retrieve first target (wikilink or URL), or entire string
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    --     lonely   -- remove fragment, if true
    -- Postcondition:
    --     Returns  string, number
    --                  string, with detected link target, or entire
    --                  number, with number of brackets, if found, or 2
    local r1, r2 = WLink.getTarget( attempt );
    if not r1 then
        r1 = mw.text.trim( attempt );
        r2 = 2;
    end
    if lonely then
        local i = r1:find( "#", 1, true );
        if i == 1 then
            r1 = "";
        elseif i then
            r1 = r1:sub( 1, i - 1 );
        end
    end
    return r1, r2;
end -- target()



function WLink.ansiPercent( attempt, alter )
    -- Convert string by ANSI encoding rather than UTF-8 encoding
    -- Precondition:
    --     attempt  -- string, with presumable ANSI characters
    --     alter    -- string or nil, to use for spaces instead of %20
    -- Postcondition:
    --     Returns  string, encoded
    local k, s;
    local r = attempt;
    if alter then
        r = r:gsub( " ", alter );
    end
    for i = mw.ustring.len( r ), 1, -1 do
        k = mw.ustring.codepoint( r, i, i );
        if k <= 32  or  k > 126 then
            if k > 255 then
                s = mw.ustring.sub( r, i, i );
                if k > 2047 then
                    s = string.format( "%%%2X%%%2X%%%2X",
                                       s:byte( 1, 1 ),
                                       s:byte( 2, 2 ),
                                       s:byte( 3, 3 ) );
                else
                    s = string.format( "%%%2X%%%2X",
                                       s:byte( 1, 1 ),
                                       s:byte( 2, 2 ) );
                end
            else
                s = string.format( "%%%2X", k );
            end
            r = string.format( "%s%s%s",
                               mw.ustring.sub( r,  1,  i - 1 ),
                               s,
                               mw.ustring.sub( r,  i + 1 ) );
        end
    end -- for --i
    r = mw.ustring.gsub(r, '^%*', '%%2A')
    return r;
end -- WLink.ansiPercent()



function WLink.formatURL( adjust )
    -- Create bracketed link, if not yet
    -- Precondition:
    --     adjust  -- string, with URL or domain/path or bracketed link
    -- Postcondition:
    --     Returns  string, with bracketed link
    --              false on invalid format
    local r;
    if type( adjust ) == "string" then
        if WLink.isBracketedLink( adjust ) then
            r = adjust;
        else
            local url = mw.text.trim( adjust );
            local host;
            utilURL();
            host = URLutil.getHost( adjust );
            if not host then
                url  = "http://" .. adjust;
                host = URLutil.getHost( url );
            end
            if host then
                local path = URLutil.getRelativePath( url );
                local show;
                if path == "/" then
                    if not url:match( "/$" ) then
                        url = url .. "/";
                    end
                    show = host;
                else
                    local i = path:find( "#" );
                    if i then
                        path = path:sub( 1,  i - 1 );
                    end
                    show = host .. path;
                end
                r = string.format( "[%s %s]", url, show );
            else
                r = adjust;
            end
        end
    else
        r = false;
    end
    return r;
end -- WLink.formatURL()



function WLink.getArticleBase( attempt )
    -- Retrieve generic article title, no fragment nor brackets
    -- Precondition:
    --     attempt  -- string, with wikilink or page title
    --                         current page title, if missing
    -- Postcondition:
    --     Returns  string, with identified lemma, or all
    --              false on invalid format
    local r;
    if attempt then
        local m;
        r, m = target( attempt, true );
        if m ~= 2 then
            r = false;
        end
    else
        r = mw.title.getCurrentTitle().text;
    end
    if r then
        local sub = r:match( "^(.*%S) *%(.+%)$" );
        if sub then
            r = sub;
        end
    end
    return r;
end -- WLink.getArticleBase()



function WLink.getBaseTitle( attempt )
    -- Retrieve last segment in subpage, no fragment
    -- Precondition:
    --     attempt  -- string, with wikilink or page title
    -- Postcondition:
    --     Returns  string, with identified segment, or all
    local r;
    local s, m = target( attempt, true );
    if m == 2 then
        local sub = s:match( "/([^/]+)$" );
        if sub then
            r = sub;
        else
            r = s;
        end
    else
        r = false;
    end
    return r;
end -- WLink.getBaseTitle()



function WLink.getExtension( attempt )
    -- Retrieve media extension
    -- Precondition:
    --     attempt  -- string, with wikilink (media link) or page title
    --                         if URL, PDF may be detected
    -- Postcondition:
    --     Returns  string, with detected downcased media type
    --              false if no extension found
    local r = false;
    local s, m = target( attempt );
    if m == 2 then
        s = s:match( "%.(%a+)$" );
        if s then
            r = s:lower();
        end
    elseif s:upper():match( "[%./](PDF)%W?" ) then
        r = "pdf";
    end
    return r;
end -- WLink.getExtension()



function WLink.getFile( attempt )
    -- Retrieve media page identifier
    -- Precondition:
    --     attempt  -- string, with wikilink (media link) or page title
    -- Postcondition:
    --     Returns  string, with detected file title
    --                      no namespace nor project
    --              false if no file found
    local r = false;
    local s, m = target( attempt );
    if m == 2 then
        local slow    = ":" .. s:lower();
        local find = function ( a )
                         local seek = string.format( ":%s:().+%%.%%a+$",
                                                     a:lower() );
                         local join = slow:find( seek );
                         local ret;
                         if join then
                             ret = s:sub( join + #a + 1 );
                         end
                         return ret;
                     end;
        r = find( "file" );
        if not r then
            local trsl = mw.site.namespaces[6];
            r = find( trsl.name );
            if not r then
                trsl = trsl.aliases;
                for k, v in pairs( trsl ) do
                    r = find( v );
                    if r then
                        break; -- for k, v
                    end
                end -- for k, v
            end
        end
    end
    return r;
end -- WLink.getFile()



function WLink.getFragment( attempt )
    -- Retrieve fragment
    -- Precondition:
    --     attempt  -- string, with presumable fragment
    -- Postcondition:
    --     Returns  string, with detected fragment
    --              false if no address found
    local r = false;
    local s, m = target( attempt );
    if s then
        local i = s:find( "#", 1, true );
        if i then
            if i > 1 then
                s = s:sub( i - 1 );
                i = 2;
            end
            if s:find( "&#", 1, true ) then
                s = mw.text.decode( s );
                i = s:find( "#", 1, true );
                if not i then
                   s = "";
                   i = 0;
                end
            end
            s = s:sub( i + 1 );
            r = mw.text.trim( s );
            if r == "" then
                r = false;
            elseif m == 2 then
                r = r:gsub( "%.(%x%x)", "%%%1" )
                     :gsub( "_", " " );
                r = mw.uri.decode( r, "PATH" );
            end
        end
    end
    return r;
end -- WLink.getFragment()



function WLink.getLanguage( attempt )
    -- Retrieve language project identifier
    -- Precondition:
    --     attempt  -- string, with wikilink or page title
    -- Postcondition:
    --     Returns  string, with detected downcased language identifier
    --              false if no project language found
    local r = false;
    local s, m = WLink.getTarget( attempt );
    if m == 2 then
        local w = WLink.wikilink( s );
        if w  and  w.lang then
            r = w.lang;
        end
    end
    return r;
end -- WLink.getLanguage()



function WLink.getNamespace( attempt )
    -- Retrieve namespace number
    -- Precondition:
    --     attempt  -- string, with wikilink or page title
    -- Postcondition:
    --     Returns  number, of detected namespace
    --              false if no namespace found
    local r = false;
    local s, m = WLink.getTarget( attempt );
    if m == 2 then
        local w = WLink.wikilink( s );
        if w  and  not w.lang  and  not w.project  and  w.ns then
            r = w.ns;
        end
    end
    return r;
end -- WLink.getNamespace()



function WLink.getPlain( attempt )
    -- Retrieve text with all links replaced by link titles
    -- Precondition:
    --     attempt  -- string, with wikitext
    -- Postcondition:
    --     Returns  string, with modified wikitext without links
    local r = attempt;
    local i = 1;
    local j, k, n, lean, s, shift, space, suffix;
    while ( true ) do
        j = r:find( "[", i, true );
        if j then
            suffix = r:sub( j );
            i      = j + 1;
            lean   = ( r:byte( i, i ) == 91 );
            if lean then
                s, k, n = contentWikilink( suffix );
            else
                s, k, n = contentExtlink( suffix );
            end
            if s then
                if k > 1 then
                    n      = n - k;
                    i      = j + k;
                    j      = i - 1;
                    suffix = r:sub( j );
                end
                if lean then
                    s, shift = extractWikilink( suffix );
                    if s then
                        space = s:match( "^([^:]+):" );
                        if space then
                            space = mw.site.namespaces[ space ];
                            if space then
                                space = space.id;
                            end
                        end
                        if space == 6  or  space == 14 then
                            shift = "";
                        elseif not shift then
                            shift = s;
                        end
                    else
                        s     = "";
                        shift = "";
                    end
                else
                    s, shift = extractExtlink( suffix );
                    if not s then
                        s = "";
                    end
                    if not shift then
                        shift = "";
                    end
                    i = i - 1;
                end
                if j > 1 then
                    s = r:sub( 1, j - 1 );
                else
                    s = "";
                end
                r = string.format( "%s%s%s",
                                   s,  shift,  r:sub( n + i ) );
                i = i + #shift;
            else
                break; -- while true
            end
        else
            break; -- while true
        end
    end -- while true
    return r;
end -- WLink.getPlain()



function WLink.getProject( attempt )
    -- Retrieve wikifarm project identifier
    -- Precondition:
    --     attempt  -- string, with wikilink or page title
    -- Postcondition:
    --     Returns  string, with detected downcased project identifier
    --              false if no project identifier found
    local r = false;
    local s, m = WLink.getTarget( attempt );
    if m == 2 then
        local w = WLink.wikilink( s );
        if w  and  w.project then
            r = w.project;
        end
    end
    return r;
end -- WLink.getProject()



function WLink.getTarget( attempt )
    -- Retrieve first target (wikilink or URL)
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  string, number
    --                  string, with first detected link target
    --                  number, with number of brackets, if found
    --              false if nothing found
    local r1 = false;
    local r2 = false;
    local i  = attempt:find( "[", 1, true );
    if i then
        local m;
        r1 = attempt:sub( i );
        if r1:byte( 2, 2 ) == 91 then
            m  = 2;
            r1 = extractWikilink( r1 );
        else
            m  = 1;
            r1 = extractExtlink( r1 );
        end
        if r1 then
            r2 = m;
        end
    else
        r1 = attempt:match( "%A?([hf]t?tps?://%S+)%s?" );
        if r1 then
            if utilURL().isResourceURL( r1 ) then
                r2 = 0;
            else
                r1 = false;
            end
        else
            r1 = false;
        end
    end
    return r1, r2;
end -- WLink.getTarget()



function WLink.getTargetPage( attempt )
    -- Retrieve first target page (page name or URL of page)
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  string, with first detected linked page
    --              false if nothing found
    local r1, r2 = WLink.getTarget( attempt );
    if r1 then
        local i = r1:find( "#", 1, true );
        if i then
            if i == 1 then
                r1 = false;
            else
                r1 = mw.text.trim( r1:sub( 1,  i - 1 ) );
            end
        end
    end
    return r1, r2;
end -- WLink.getTargetPage()



function WLink.getTitle( attempt )
    -- Retrieve first link title (wikilink or URL), or wikilink target
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  string, with first detected link target
    --              false if nothing found
    local r = false;
    local i = attempt:find( "[", 1, true );
    if i then
        local s1, s2;
        r = attempt:sub( i );
        if r:byte( 2, 2 ) == 91 then
            s1, s2 = extractWikilink( r );
            if s2 then
                r = s2;
            else
                r = s1;
            end
        else
            s1, r = extractExtlink( r );
        end
    end
    return r;
end -- WLink.getTitle()



function WLink.getWeblink( attempt, anURLutil )
    -- Retrieve bracketed link from resource URL
    -- Precondition:
    --     attempt    -- string, with URL, or something different
    --     anURLutil  -- library module object, or nil
    -- Postcondition:
    --     Returns  string, with first detected link target
    --              false if nothing found
    local second = ".ac.co.go.gv.or.";
    local r;
    if type( anURLutil ) == "table" then
        URLutil = anURLutil;
    else
        utilURL();
    end
    if URLutil.isResourceURL( attempt ) then
        local site = URLutil.getAuthority( attempt );
        local show;
        if #attempt == #site then
           site = site .. "/";
        end
        show = URLutil.getTop3domain( "//" .. site );
        if show then
            local scan   = "[%./](%a+)(%.%l%l%.)(%a+)$";
            local search = "." .. show;
            local s1, s2, s3 = search:match( scan );
            if s2 then
                if not second:find( s2, 1, true ) then
                    show = string.format( "%s.%s", s2, s3 );
                end
            else
                show = false;
            end
        end
        if not show then
            show = URLutil.getTop2domain( "//" .. site );
            if not show then
                show = URLutil.getHost( "//" .. site );
            end
        end
        r = string.format( "[%s %s]", attempt, show );
    else
        r = attempt;
    end
    return r;
end -- WLink.getWeblink()



function WLink.isBracketedLink( attempt )
    -- Does attempt match a bracketed link?
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  boolean
    local r = false;
    local i = attempt:find( "[", 1, true );
    if i then
        local s = attempt:sub( i );
        if s:byte( 2, 2 ) == 91 then
            s = extractWikilink( s );
        else
            s = extractExtlink( s );
        end
        if s then
            r = true;
        end
    end
    return r;
end -- WLink.isBracketedLink()



function WLink.isBracketedURL( attempt )
    -- Does attempt match a bracketed URL?
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  boolean
    local s, r = WLink.getTarget( attempt );
    return ( r == 1 );
end -- WLink.isBracketedURL()



function WLink.isCategorization( attempt )
    -- Does attempt match a categorization?
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  boolean
    local r = false;
    local s, m = WLink.getTarget( attempt );
    if m == 2 then
        local w = WLink.wikilink( s );
        if w  and  w.ns == 14
              and  not ( w.lead or w.lang or w.project )
              and  w.title ~= "" then
            r = true;
        end
    end
    return r;
end -- WLink.isCategorization()



function WLink.isExternalLink( attempt )
    -- Does attempt match an external link?
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  boolean
    local s, r = WLink.getTarget( attempt );
    if r then
        r = ( r < 2 );
    end
    return r;
end -- WLink.isExternalLink()



function WLink.isInterlanguage( attempt )
    -- Does attempt match an interlanguage link?
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  boolean
    local r = false;
    local s, m = WLink.getTarget( attempt );
    if m == 2 then
        local w = WLink.wikilink( s );
        if w and w.lang and not w.project and not w.lead
             and  w.title ~= "" then
            r = true;
        end
    end
    return r;
end -- WLink.isInterlanguage()



function WLink.isInterwiki( attempt )
    -- Does attempt match an interwiki link within wikifarm?
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  boolean
    local r = false;
    local s, m = WLink.getTarget( attempt );
    if m == 2 then
        local w = WLink.wikilink( s );
        if w  and  ( w.lang or w.project )  and  w.title ~= "" then
            r = true;
        end
    end
    return r;
end -- WLink.isInterwiki()



function WLink.isMedia( attempt )
    -- Does attempt match a media translusion?
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  boolean
    local r = false;
    local s, m = WLink.getTarget( attempt );
    if m == 2 then
        local w = WLink.wikilink( s );
        if w  and  w.ns == 6
           and  not ( w.lead or w.lang or w.project )
           and  w.title ~= ""
           and  WLink.getExtension( w.title ) then
            r = true;
        end
    end
    return r;
end -- WLink.isMedia()



function WLink.isTitledLink( attempt )
    -- Does attempt match a titled link?
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  boolean
    local r = false;
    local i = attempt:find( "[", 1, true );
    if i then
        local c, n;
        local s = attempt:sub( i );
        if s:byte( 2, 2 ) == 91 then
            n = s:find( "%]%]", 5 );
            c = "|";
        else
            n = s:find( "%]", 8 );
            c = "%s%S";
        end
        if n then
            local m = s:find( c, 2 );
            if m  and  m + 1 < n  and  WLink.getTarget( attempt ) then
                r = true;
            end
        end
    end
    return r;
end -- WLink.isTitledLink()



function WLink.isValidLink( attempt )
    -- Does attempt match a link?
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  boolean
    local s, r = WLink.getTarget( attempt );
    if r then
        r = true;
    end
    return r;
end -- WLink.isValidLink()



function WLink.isWikilink( attempt )
    -- Does attempt match a wikilink?
    -- Precondition:
    --     attempt  -- string, with presumable link somewhere
    -- Postcondition:
    --     Returns  boolean
    local s, m = WLink.getTarget( attempt );
    return ( m == 2 );
end -- WLink.isWikilink()



function WLink.wikilink( attempt )
    -- Retrieve wikilink components
    -- Precondition:
    --     attempt  -- string, with presumable link
    --                         expected to be enclosed in "[["_"|" "]]"
    --                         else wikilink
    -- Postcondition:
    --     Returns  table or false
    --              table of assignments with { type, value}
    --                       type is one of "lead",
    --                          "project", "lang",
    --                          "ns", "space", "title"
    --              false if nothing found
    local s = contentWikilink( attempt );
    local got, n, r;
    if not s then
        s = attempt;
    end
    i = s:find( "|", 1, true );
    if i then
        s = s:sub( 1, i - 1 );
    end
    got = mw.text.split( s, ":" );
    n   = table.maxn( got );
    if n == 1 then
        r = { title = mw.text.trim( s ) };
    else
        local j, k, o, v;
        r = { title = "" };
        if n > 4 then
            k = 4;
        else
            k = n - 1;
        end
        j = k;
        for i = 1, j do
            s = mw.text.trim( got[ i ] );
            if s ~= "" then
                o = mw.site.namespaces[ mw.text.trim( got[ i ] ) ];
                if o then
                    r.ns    = o.id;
                    r.space = o.name;
                    k = i + 1;
                    j = i - 1;
                    break; -- for i
                end
            end
        end -- for i
        for i = 1, j do
            o, v = prefix( got[ i ],  ( i == 1 ) );
            if o then
                if r[ o ] then
                    k = i;
                    break; -- for i
                else
                    r[ o ] = v;
                end
            else
                k = i;
                break; -- for i
            end
        end -- for i
        for i = k, n do
            r.title = r.title .. got[ i ];
            if i < n then
                r.title = r.title .. ":";
            end
        end -- for i
    end
    if r.lead and
       ( r.project  or  not r.title  or
         ( not r.lang  and  r.ns ~= 6  and  r.ns ~= 14 ) ) then
        r.lead = false;
    end
    return r;
end -- WLink.wikilink()



function WLink.failsafe( assert )
    -- Retrieve versioning and check for compliance
    -- Precondition:
    --     assert  -- string, with required version, or false
    -- Postcondition:
    --     Returns  string with appropriate version, or false
    local r;
    if assert  and  assert > WLink.serial then
        r = false;
    else
        r = WLink.serial;
    end
    return r
end -- WLink.failsafe()



local function Template( frame, action, leave, lone )
    -- Run actual code from template transclusion
    -- Precondition:
    --     frame   -- object
    --     action  -- string, with function name
    --     leave   -- true: keep whitespace around
    --     lone    -- true: permit call without parameters
    -- Postcondition:
    --     Return string; might be error message
    local lucky = true;
    local s = false;
    local r = false;
    local space;
    for k, v in pairs( frame.args ) do
        if k == 1 then
            if leave then
                s = v;
            else
                s = mw.text.trim( v );
            end
        elseif action == "ansiPercent"  and  k == "space" then
            if v ~= "" then
                space = v;
            end
        elseif k ~= "template" then
            lucky = false;
            if r then
                r = r .. "|";
            else
                r = "Unknown parameter: ";
            end
            r = string.format( "%s%s=", r, k );
        end
    end -- for k, v
    if lucky then
        if s or lone then
            lucky, r = pcall( WLink[ action ],  s,  space );
        else
            r = "Parameter missing";
            lucky = false;
        end
    end
    if lucky then
        if type( r ) == "boolean" then
            if r then
                r = "1";
            else
                r = "";
            end
        end
    else
        r = string.format( "<span class=\"error\">%s</span>", r );
    end
    return r;
end -- Template()



-- Export
local p = { };

p.ansiPercent = function ( frame )
    return Template( frame, "ansiPercent" );
end
p.formatURL = function ( frame )
    return Template( frame, "formatURL" );
end
p.getArticleBase = function ( frame )
    return Template( frame, "getArticleBase", false, true );
end
p.getBaseTitle = function ( frame )
    return Template( frame, "getBaseTitle" );
end
p.getExtension = function ( frame )
    return Template( frame, "getExtension" );
end
p.getFile = function ( frame )
    return Template( frame, "getFile" );
end
p.getFragment = function ( frame )
    return Template( frame, "getFragment" );
end
p.getInterwiki = function ( frame )
    return Template( frame, "getInterwiki" );
end
p.getLanguage = function ( frame )
    return Template( frame, "getLanguage" );
end
p.getNamespace = function ( frame )
    return tostring( Template( frame, "getNamespace" ) );
end
p.getPlain = function ( frame )
    return Template( frame, "getPlain" );
end
p.getProject = function ( frame )
    return Template( frame, "getProject" );
end
p.getTarget = function ( frame )
    return Template( frame, "getTarget" );
end
p.getTargetPage = function ( frame )
    return Template( frame, "getTargetPage" );
end
p.getTitle = function ( frame )
    return Template( frame, "getTitle" );
end
p.getWeblink = function ( frame )
    return Template( frame, "getWeblink" );
end
p.isBracketedLink = function ( frame )
    return Template( frame, "isBracketedLink" );
end
p.isBracketedURL = function ( frame )
    return Template( frame, "isBracketedURL" );
end
p.isCategorization = function ( frame )
    return Template( frame, "isCategorization" );
end
p.isExternalLink = function ( frame )
    return Template( frame, "isExternalLink" );
end
p.isInterlanguage = function ( frame )
    return Template( frame, "isInterlanguage" );
end
p.isInterwiki = function ( frame )
    return Template( frame, "isInterwiki" );
end
p.isMedia = function ( frame )
    return Template( frame, "isMedia" );
end
p.isTitledLink = function ( frame )
    return Template( frame, "isTitledLink" );
end
p.isValidLink = function ( frame )
    return Template( frame, "isValidLink" );
end
p.isWeblink = function ( frame )
    return Template( frame, "isWeblink" );
end
p.isWikilink = function ( frame )
    return Template( frame, "isWikilink" );
end
p.failsafe = function ( frame )
    local since = frame.args[ 1 ];
    if since then
        since = mw.text.trim( since );
        if since == "" then
            since = false;
        end
    end
    return WLink.failsafe( since ) or "";
end
p.WLink = function ()
    return WLink;
end

return p;