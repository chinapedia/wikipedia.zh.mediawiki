local Text = { serial = "2017-11-01",
               suite  = "Text" }
--[=[
Text utilities
]=]



-- local globals
local PatternCJK        = false
local PatternCombined   = false
local PatternLatin      = false
local PatternTerminated = false
local QuoteLang         = false
local QuoteType         = false
local RangesLatin       = false
local SeekQuote         = false



local function factoryQuote()
    -- Create quote definitions
    QuoteLang = { af        = "bd",
                  ar        = "la",
                  be        = "labd",
                  bg        = "bd",
                  ca        = "la",
                  cs        = "bd",
                  da        = "bd",
                  de        = "bd",
                  dsb       = "bd",
                  et        = "bd",
                  el        = "lald",
                  en        = "ld",
                  es        = "la",
                  eu        = "la",
            --    fa        = "la",
                  fi        = "rd",
                  fr        = "laSPC",
                  ga        = "ld",
                  he        = "ldla",
                  hr        = "bd",
                  hsb       = "bd",
                  hu        = "bd",
                  hy        = "labd",
                  id        = "rd",
                  is        = "bd",
                  it        = "ld",
                  ja        = "x300C",
                  ka        = "bd",
                  ko        = "ld",
                  lt        = "bd",
                  lv        = "bd",
                  nl        = "ld",
                  nn        = "la",
                  no        = "la",
                  pl        = "bdla",
                  pt        = "lald",
                  ro        = "bdla",
                  ru        = "labd",
                  sk        = "bd",
                  sl        = "bd",
                  sq        = "la",
                  sr        = "bx",
                  sv        = "rd",
                  th        = "ld",
                  tr        = "ld",
                  uk        = "la",
                  zh        = "ld",
                  ["de-ch"] = "la",
                  ["en-gb"] = "lsld",
                  ["en-us"] = "ld",
                  ["fr-ch"] = "la",
                  ["it-ch"] = "la",
                  ["pt-br"] = "ldla",
                  ["zh-tw"] = "x300C",
                  ["zh-cn"] = "ld" }
    QuoteType = { bd    = { { 8222, 8220 },  { 8218, 8217 } },
                  bdla  = { { 8222, 8220 },  {  171,  187 } },
                  bx    = { { 8222, 8221 },  { 8218, 8217 } },
                  la    = { {  171,  187 },  { 8249, 8250 } },
                  laSPC = { {  171,  187 },  { 8249, 8250 },  true },
                  labd  = { {  171,  187 },  { 8222, 8220 } },
                  lald  = { {  171,  187 },  { 8220, 8221 } },
                  ld    = { { 8220, 8221 },  { 8216, 8217 } },
                  ldla  = { { 8220, 8221 },  {  171,  187 } },
                  lsld  = { { 8216, 8217 },  { 8220, 8221 } },
                  rd    = { { 8221, 8221 },  { 8217, 8217 } },
                  x300C = { { 0x300C, 0x300D },
                            { 0x300E, 0x300F } } }
    return r
end -- factoryQuote()



local function fiatQuote( apply, alien, advance )
    -- Quote text
    -- Parameter:
    --     apply    -- string, with text
    --     alien    -- string, with language code
    --     advance  -- number, with level 1 or 2
    local r = apply
    local suite
    if not QuoteLang then
        factoryQuote()
    end
    suite = QuoteLang[ alien ]
    if not suite then
        local slang = alien:match( "^(%l+)-" )
        if slang then
            suite = QuoteLang[ slang ]
        end
        if not suite then
            suite = QuoteLang[ "en" ]
        end
    end
    if suite then
        local quotes = QuoteType[ suite ]
        if quotes then
            local space
            if quotes[ 3 ] then
                space = " "
            else
                space = ""
            end
            quotes = quotes[ advance ]
            if quotes then
                r = mw.ustring.format( "%s%s%s%s%s",
                                       mw.ustring.char( quotes[ 1 ] ),
                                       space,
                                       apply,
                                       space,
                                       mw.ustring.char( quotes[ 2 ] ) )
            end
        else
            mw.log( "fiatQuote() " .. suite )
        end
    end
    return r
end -- fiatQuote()



Text.char = function ( apply, again, accept )
    -- Create string from codepoints
    -- Parameter:
    --     apply   -- table (sequence) with numerical codepoints, or nil
    --     again   -- number of repetitions, or nil
    --     accept  -- true, if no error messages to be appended
    -- Returns: string
    local r
    if type( apply ) == "table" then
        local bad   = { }
        local codes = { }
        local s
        for k, v in pairs( apply ) do
            s = type( v )
            if s == "number" then
                if v < 32  and  v ~= 9  and  v ~= 10 then
                    v = tostring( v )
                else
                    v = math.floor( v )
                    s = false
                end
            elseif s ~= "string" then
                v = tostring( v )
            end
            if s then
                table.insert( bad, v )
            else
                table.insert( codes, v )
            end
        end -- for k, v
        if #bad == 0 then
            if #codes > 0 then
                r = mw.ustring.char( unpack( codes ) )
                if again then
                    if type( again ) == "number" then
                        local n = math.floor( again )
                        if n > 1 then
                            r = r:rep( n )
                        elseif n < 1 then
                            r = ""
                        end
                    else
                        s = "bad repetitions: " .. tostring( again )
                    end
                end
            end
        else
            s = "bad codepoints: " .. table.concat( bad, " " )
        end
        if s  and  not accept then
            r = tostring(  mw.html.create( "span" )
                                  :addClass( "error" )
                                  :wikitext( s ) )
        end
    end
    return r or ""
end -- Text.char()



Text.concatParams = function ( args, apply, adapt )
    -- Concat list items into one string
    -- Parameter:
    --     args   -- table (sequence) with numKey=string
    --     apply  -- string (optional); separator (default: "|")
    --     adapt  -- string (optional); format including "%s"
    -- Returns: string
    local collect = { }
    for k, v in pairs( args ) do
        if type( k ) == "number" then
            v = mw.text.trim( v )
            if v ~= "" then
                if adapt then
                    v = mw.ustring.format( adapt, v )
                end
                table.insert( collect, v )
            end
        end
    end -- for k, v
    return table.concat( collect,  apply or "|" )
end -- Text.concatParams()



Text.containsCJK = function ( analyse )
    -- Is any CJK code within?
    -- Parameter:
    --     analyse  -- string
    -- Returns: true, if CJK detected
    local r
    if not patternCJK then
        patternCJK = mw.ustring.char( 91,
                                       13312, 45,  40959,
                                      131072, 45, 178207,
                                      93 )
    end
    if mw.ustring.find( analyse, patternCJK ) then
        r = true
    else
        r = false
    end
    return r
end -- Text.containsCJK()



Text.getPlain = function ( adjust )
    -- Remove wikisyntax from string, except templates
    -- Parameter:
    --     adjust  -- string
    -- Returns: string
    local i = adjust:find( "<!--", 1, true )
    local r = adjust
    local j
    while i do
        j = r:find( "-->",  i + 3,  true )
        if j then
            r = r:sub( 1, i ) .. r:sub( j + 3 )
        else
            r = r:sub( 1, i )
        end
        i = r:find( "<!--", i, true )
    end    -- "<!--"
    r = r:gsub( "(</?%l[^>]*>)", "" )
         :gsub( "'''(.+)'''", "%1" )
         :gsub( "''(.+)''", "%1" )
         :gsub( " ", " " )
    return r
end -- Text.getPlain()



Text.isLatinRange = function ( adjust )
    -- Are characters expected to be latin or symbols within latin texts?
    -- Precondition:
    --     adjust  -- string, or nil for initialization
    -- Returns: true, if valid for latin only
    local r
    if not RangesLatin then
        RangesLatin = { {    7,  687 },
                        { 7531, 7578 },
                        { 7680, 7935 },
                        { 8194, 8250 } }
    end
    if not PatternLatin then
        local range
        PatternLatin = "^["
        for i = 1, #RangesLatin do
            range = RangesLatin[ i ]
            PatternLatin = PatternLatin ..
                           mw.ustring.char( range[ 1 ], 45, range[ 2 ] )
        end    -- for i
        PatternLatin = PatternLatin .. "]*$"
    end
    if adjust then
        if mw.ustring.match( adjust, PatternLatin ) then
            r = true
        else
            r = false
        end
    end
    return r
end -- Text.isLatinRange()



Text.isQuote = function ( ask )
    -- Is this character any quotation mark?
    -- Parameter:
    --     ask  -- string, with single character
    -- Returns: true, if ask is quotation mark
    local r
    if not SeekQuote then
        SeekQuote = mw.ustring.char(   34,       -- "
                                       39,       -- '
                                      171,       -- laquo
                                      187,       -- raquo
                                     8216,       -- lsquo
                                     8217,       -- rsquo
                                     8218,       -- sbquo
                                     8220,       -- ldquo
                                     8221,       -- rdquo
                                     8222,       -- bdquo
                                     8249,       -- lsaquo
                                     8250,       -- rsaquo
                                     0x300C,     -- CJK
                                     0x300D,     -- CJK
                                     0x300E,     -- CJK
                                     0x300F )    -- CJK
    end
    if ask == "" then
        r = false
    elseif mw.ustring.find( SeekQuote, ask, 1, true ) then
        r = true
    else
        r = false
    end
    return r
end -- Text.isQuote()



Text.listToText = function ( args, adapt )
    -- Format list items similar to mw.text.listToText()
    -- Parameter:
    --     args   -- table (sequence) with numKey=string
    --     adapt  -- string (optional); format including "%s"
    -- Returns: string
    local collect = { }
    for k, v in pairs( args ) do
        if type( k ) == "number" then
            v = mw.text.trim( v )
            if v ~= "" then
                if adapt then
                    v = mw.ustring.format( adapt, v )
                end
                table.insert( collect, v )
            end
        end
    end -- for k, v
    return mw.text.listToText( collect )
end -- Text.listToText()



Text.quote = function ( apply, alien, advance )
    -- Quote text
    -- Parameter:
    --     apply    -- string, with text
    --     alien    -- string, with language code, or nil
    --     advance  -- number, with level 1 or 2, or nil
    -- Returns: quoted string
    local mode, slang
    if type( alien ) == "string" then
        slang = mw.text.trim( alien ):lower()
    else
        slang = mw.title.getCurrentTitle().pageLanguage
        if not slang then
            -- TODO FIXME: Introduction expected 2017-04
            slang = mw.language.getContentLanguage():getCode()
        end
    end
    if advance == 2 then
        mode = 2
    else
        mode = 1
    end
    return fiatQuote( mw.text.trim( apply ), slang, mode )
end -- Text.quote()



Text.quoteUnquoted = function ( apply, alien, advance )
    -- Quote text, if not yet quoted and not empty
    -- Parameter:
    --     apply    -- string, with text
    --     alien    -- string, with language code, or nil
    --     advance  -- number, with level 1 or 2, or nil
    -- Returns: string; possibly quoted
    local r = mw.text.trim( apply )
    local s = mw.ustring.sub( r, 1, 1 )
    if s ~= ""  and  not Text.isQuote( s, advance ) then
        s = mw.ustring.sub( r, -1, 1 )
        if not Text.isQuote( s ) then
            r = Text.quote( r, alien, advance )
        end
    end
    return r
end -- Text.quoteUnquoted()



Text.removeDiacritics = function ( adjust )
    -- Remove all diacritics
    -- Parameter:
    --     adjust  -- string
    -- Returns: string; all latin letters should be ASCII
    --                  or basic greek or cyrillic or symbols etc.
    local cleanup, decomposed
    if not PatternCombined then
        PatternCombined = mw.ustring.char( 91,
                                            0x0300, 45, 0x036F,
                                            0x1AB0, 45, 0x1AFF,
                                            0x1DC0, 45, 0x1DFF,
                                            0xFE20, 45, 0xFE2F,
                                           93 )
    end
    decomposed = mw.ustring.toNFD( adjust )
    cleanup    = mw.ustring.gsub( decomposed, PatternCombined, "" )
    return mw.ustring.toNFC( cleanup )
end -- Text.removeDiacritics()



Text.sentenceTerminated = function ( analyse )
    -- Is string terminated by dot, question or exclamation mark?
    --     Quotation, link termination and so on granted
    -- Parameter:
    --     analyse  -- string
    -- Returns: true, if sentence terminated
    local r
    if not PatternTerminated then
        PatternTerminated = mw.ustring.char( 91,
                                             12290,
                                             65281,
                                             65294,
                                             65311 )
                            .. "!%.%?…][\"'%]‹›«»‘’“”]*$"
    end
    if mw.ustring.find( analyse, PatternTerminated ) then
        r = true
    else
        r = false
    end
    return r
end -- Text.sentenceTerminated()



Text.ucfirstAll = function ( adjust )
    -- Capitalize all words
    -- Precondition:
    --     adjust  -- string
    -- Returns: string with all first letters in upper case
    local r = " " .. adjust
    local i = 1
    local c, j, m
    if adjust:find( "&" ) then
        r = r:gsub( "&",      "&" )
             :gsub( "<",       "<" )
             :gsub( ">",       ">" )
             :gsub( " ",    " " )
             :gsub( " ", " " )
             :gsub( "‌",   "‌" )
             :gsub( "‍",    "‍" )
             :gsub( "‎",    "‎" )
             :gsub( "‏",    "‏" )
        m = true
    end
    while i do
        i = mw.ustring.find( r, "%W%l", i )
        if i then
            j = i + 1
            c = mw.ustring.upper( mw.ustring.sub( r, j, j ) )
            r = string.format( "%s%s%s",
                               mw.ustring.sub( r, 1, i ),
                               c,
                               mw.ustring.sub( r, i + 2 ) )
            i = j
        end
    end -- while i
    r = r:sub( 2 )
    if m then
        r = r:gsub(     "&", "&" )
             :gsub(     "<", "<" )
             :gsub(     ">", ">" )
             :gsub(    " ", " " )
             :gsub(   " ", " " )
             :gsub(   "‌", "‌" )
             :gsub(   "‍", "‍" )
             :gsub(   "‎", "‎" )
             :gsub(   "‏", "‏" )
             :gsub( "&#X(%x+);", "&#x%1;" )
    end
    return r
end -- Text.ucfirstAll()



Text.uprightNonlatin = function ( adjust )
    -- Ensure non-italics for non-latin text parts
    --     One single greek letter might be granted
    -- Precondition:
    --     adjust  -- string
    -- Returns: string with non-latin parts enclosed in <span>
    local r
    Text.isLatinRange()
    if mw.ustring.match( adjust, PatternLatin ) then
        -- latin only, horizontal dashes, quotes
        r = adjust
    else
        local c
        local j    = false
        local k    = 1
        local m    = false
        local n    = mw.ustring.len( adjust )
        local span = "%s%s<span dir='auto' style='font-style:normal'>%s</span>"
        local flat = function ( a )
                  -- isLatin
                  local range
                  for i = 1, #RangesLatin do
                      range = RangesLatin[ i ]
                      if a >= range[ 1 ]  and  a <= range[ 2 ] then
                          return true
                      end
                  end    -- for i
              end -- flat()
        local focus = function ( a )
                  -- char is not ambivalent
                  local r = ( a > 64 )
                  if r then
                      r = ( a < 8192  or  a > 8212 )
                  else
                      r = ( a == 38  or  a == 60 )    -- '&' '<'
                  end
                  return r
              end -- focus()
        local form = function ( a )
                return string.format( span,
                                      r,
                                      mw.ustring.sub( adjust, k, j - 1 ),
                                      mw.ustring.sub( adjust, j, a ) )
              end -- form()
        r = ""
        for i = 1, n do
            c = mw.ustring.codepoint( adjust, i, i )
            if focus( c ) then
                if flat( c ) then
                    if j then
                        if m then
                            if i == m then
                                -- single greek letter.
                                j = false
                            end
                            m = false
                        end
                        if j then
                            local nx = i - 1
                            local s  = ""
                            for ix = nx, 1, -1 do
                                c = mw.ustring.sub( adjust, ix, ix )
                                if c == " "  or  c == "(" then
                                    nx = nx - 1
                                    s  = c .. s
                                else
                                    break -- for ix
                                end
                            end -- for ix
                            r = form( nx ) .. s
                            j = false
                            k = i
                        end
                    end
                elseif not j then
                    j = i
                    if c >= 880  and  c <= 1023 then
                        -- single greek letter?
                        m = i + 1
                    else
                        m = false
                    end
                end
            elseif m then
                m = m + 1
            end
        end    -- for i
        if j  and  ( not m  or  m < n ) then
            r = form( n )
        else
            r = r .. mw.ustring.sub( adjust, k )
        end
    end
    return r
end -- Text.uprightNonlatin()



Text.test = function ( about )
    local r
    if about == "quote" then
        factoryQuote()
        r = { }
        r.QuoteLang = QuoteLang
        r.QuoteType = QuoteType
    end
    return r
end -- Text.test()



-- Export
local p = { }

function p.char( frame )
    local params = frame:getParent().args
    local story = params[ 1 ]
    local codes, lenient, multiple
    if not story then
        params = frame.args
        story  = params[ 1 ]
    end
    if story then
        local items = mw.text.split( story, "%s+" )
        if #items > 0 then
            local j
            lenient  = ( params.errors == "0" )
            codes    = { }
            multiple = tonumber( params[ "*" ] )
            for k, v in pairs( items ) do
                if v:sub( 1, 1 ) == "x" then
                    j = tonumber( "0" .. v )
                elseif v == "" then
                    v = false
                else
                    j = tonumber( v )
                end
                if v then
                    table.insert( codes,  j or v )
                end
            end -- for k, v
        end
    end
    return Text.char( codes, multiple, lenient )
end

function p.concatParams( frame )
    local args
    local template = frame.args.template
    if type( template ) == "string" then
        template = mw.text.trim( template )
        template = ( template == "1" )
    end
    if template then
        args = frame:getParent().args
    else
        args = frame.args
    end
    return Text.concatParams( args,
                              frame.args.separator,
                              frame.args.format )
end

function p.containsCJK( frame )
    return Text.containsCJK( frame.args[ 1 ] or "" ) and "1" or ""
end

function p.getPlain( frame )
    return Text.getPlain( frame.args[ 1 ] or "" )
end

function p.isLatinRange( frame )
    return Text.isLatinRange( frame.args[ 1 ] or "" ) and "1" or ""
end

function p.isQuote( frame )
    return Text.isQuote( frame.args[ 1 ] or "" ) and "1" or ""
end



function p.listToFormat(frame)
    local lists = {}
    local pformat = frame.args["format"]
    local sep = frame.args["sep"] or ";"

    -- Parameter parsen: Listen
    for k, v in pairs(frame.args) do
        local knum = tonumber(k)
        if knum then lists[knum] = v end
    end

    -- Listen splitten
    local maxListLen = 0
    for i = 1, #lists do
        lists[i] = mw.text.split(lists[i], sep)
        if #lists[i] > maxListLen then maxListLen = #lists[i] end
    end

    -- Ergebnisstring generieren
    local result = ""
    local result_line = ""
    for i = 1, maxListLen do
        result_line = pformat
        for j = 1, #lists do
            result_line = mw.ustring.gsub(result_line, "%%s", lists[j][i], 1)
        end
        result = result .. result_line
    end

    return result
end



function p.listToText( frame )
    local args
    local template = frame.args.template
    if type( template ) == "string" then
        template = mw.text.trim( template )
        template = ( template == "1" )
    end
    if template then
        args = frame:getParent().args
    else
        args = frame.args
    end
    return Text.listToText( args, frame.args.format )
end



function p.quote( frame )
    local slang = frame.args[2]
    if type( slang ) == "string" then
        slang = mw.text.trim( slang )
        if slang == "" then
            slang = false
        end
    end
    return Text.quote( frame.args[ 1 ] or "",
                       slang,
                       tonumber( frame.args[3] ) )
end



function p.quoteUnquoted( frame )
    local slang = frame.args[2]
    if type( slang ) == "string" then
        slang = mw.text.trim( slang )
        if slang == "" then
            slang = false
        end
    end
    return Text.quoteUnquoted( frame.args[ 1 ] or "",
                               slang,
                               tonumber( frame.args[3] ) )
end



function p.removeDiacritics( frame )
    return Text.removeDiacritics( frame.args[ 1 ] or "" )
end

function p.sentenceTerminated( frame )
    return Text.sentenceTerminated( frame.args[ 1 ] or "" ) and "1" or ""
end

function p.ucfirstAll( frame )
    return Text.ucfirstAll( frame.args[ 1 ] or "" )
end

function p.uprightNonlatin( frame )
    return Text.uprightNonlatin( frame.args[ 1 ] or "" )
end



function p.zip(frame)
    local lists = {}
    local seps = {}
    local defaultsep = frame.args["sep"] or ""
    local innersep = frame.args["isep"] or ""
    local outersep = frame.args["osep"] or ""

    -- Parameter parsen
    for k, v in pairs(frame.args) do
        local knum = tonumber(k)
        if knum then lists[knum] = v else
            if string.sub(k, 1, 3) == "sep" then
                local sepnum = tonumber(string.sub(k, 4))
                if sepnum then seps[sepnum] = v end
            end
        end
    end
    -- sofern keine expliziten Separatoren angegeben sind, den Standardseparator verwenden
    for i = 1, math.max(#seps, #lists) do
        if not seps[i] then seps[i] = defaultsep end
    end

    -- Listen splitten
    local maxListLen = 0
    for i = 1, #lists do
        lists[i] = mw.text.split(lists[i], seps[i])
        if #lists[i] > maxListLen then maxListLen = #lists[i] end
    end

    local result = ""
    for i = 1, maxListLen do
        if i ~= 1 then result = result .. outersep end
        for j = 1, #lists do
            if j ~= 1 then result = result .. innersep end
            result = result .. (lists[j][i] or "")
        end
    end
    return result
end



function p.failsafe()
    return Text.serial
end



p.Text = function ()
    return Text
end -- p.Text

return p