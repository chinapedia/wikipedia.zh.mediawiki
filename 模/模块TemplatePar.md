--[=[ TemplatePar 2015-02-14
Template parameter utility
* assert
* check
* count
* countNotEmpty
* downcase()
* match
* valid
* verify()
* TemplatePar()
]=]



-- Module globals
local TemplatePar = { }
local MessagePrefix = "lua-module-TemplatePar-"
local L10nDef = {}
L10nDef.en = {
    badPattern  = "#invoke:TemplatePar pattern syntax error",
    dupOpt      = "#invoke:TemplatePar repeated optional parameter",
    dupRule     = "#invoke:TemplatePar conflict key/pattern",
    empty       = "Error in template * undefined value for mandatory",
    invalid     = "Error in template * invalid parameter",
    invalidPar  = "#invoke:TemplatePar invalid parameter",
    minmax      = "#invoke:TemplatePar min > max",
    missing     = "#invoke:TemplatePar missing library",
    multiSpell  = "Error in template * multiple spelling of parameter",
    noMSGnoCAT  = "#invoke:TemplatePar neither message nor category",
    noname      = "#invoke:TemplatePar missing parameter name",
    notFound    = "Error in template * missing page",
    tooLong     = "Error in template * parameter too long",
    tooShort    = "Error in template * parameter too short",
    undefined   = "Error in template * mandatory parameter missing",
    unknown     = "Error in template * unknown parameter name",
    unknownRule = "#invoke:TemplatePar unknown rule"
}
L10nDef.de  = {
    badPattern  = "#invoke:TemplatePar Syntaxfehler des pattern",
    dupOpt      = "#invoke:TemplatePar Optionsparameter wiederholt",
    dupRule     = "#invoke:TemplatePar Konflikt key/pattern",
    empty       = "Fehler bei Vorlage * Pflichtparameter ohne Wert",
    invalid     = "Fehler bei Vorlage * Parameter ungültig",
    invalidPar  = "#invoke:TemplatePar Ungültiger Parameter",
    minmax      = "#invoke:TemplatePar min > max",
    multiSpell  = "Fehler bei Vorlage * Mehrere Parameter-Schreibweisen",
    noMSGnoCAT  = "#invoke:TemplatePar weder Meldung noch Kategorie",
    noname      = "#invoke:TemplatePar Parameter nicht angegeben",
    notFound    = "Fehler bei Vorlage * Seite fehlt",
    tooLong     = "Fehler bei Vorlage * Parameter zu lang",
    tooShort    = "Fehler bei Vorlage * Parameter zu kurz",
    undefined   = "Fehler bei Vorlage * Pflichtparameter fehlt",
    unknown     = "Fehler bei Vorlage * Parametername unbekannt",
    unknownRule = "#invoke:TemplatePar Unbekannte Regel"
}
local Patterns = {
    [ "ASCII" ]    = "^[ -~]*$",
    [ "ASCII+" ]   = "^[ -~]+$",
    [ "ASCII+1" ]  = "^[!-~]+$",
    [ "n" ]        = "^[%-]?[0-9]*$",
    [ "n>0" ]      = "^[0-9]*[1-9][0-9]*$",
    [ "N+" ]       = "^[%-]?[1-9][0-9]*$",
    [ "N>0" ]      = "^[1-9][0-9]*$",
    [ "x" ]        = "^[0-9A-Fa-f]*$",
    [ "x+" ]       = "^[0-9A-Fa-f]+$",
    [ "X" ]        = "^[0-9A-F]*$",
    [ "X+" ]       = "^[0-9A-F]+$",
    [ "0,0" ]      = "^[%-]?[0-9]*,?[0-9]*$",
    [ "0,0+" ]     = "^[%-]?[0-9]+,[0-9]+$",
    [ "0,0+?" ]    = "^[%-]?[0-9]+,?[0-9]*$",
    [ "0.0" ]      = "^[%-]?[0-9]*[%.]?[0-9]*$",
    [ "0.0+" ]     = "^[%-]?[0-9]+%.[0-9]+$",
    [ "0.0+?" ]    = "^[%-]?[0-9]+[%.]?[0-9]*$",
    [ ".0+" ]      = "^[%-]?[0-9]*[%.]?[0-9]+$",
    [ "ID" ]       = "^[A-Za-z]?[A-Za-z_0-9]*$",
    [ "ID+" ]      = "^[A-Za-z][A-Za-z_0-9]*$",
    [ "ABC" ]      = "^[A-Z]*$",
    [ "ABC+" ]     = "^[A-Z]+$",
    [ "Abc" ]      = "^[A-Z]*[a-z]*$",
    [ "Abc+" ]     = "^[A-Z][a-z]+$",
    [ "abc" ]      = "^[a-z]*$",
    [ "abc+" ]     = "^[a-z]+$",
    [ "aBc+" ]     = "^[a-z]+[A-Z][A-Za-z]*$",
    [ "w" ]        = "^%S*$",
    [ "w+" ]       = "^%S+$",
    [ "base64" ]   = "^[A-Za-z0-9%+/]*$",
    [ "base64+" ]  = "^[A-Za-z0-9%+/]+$",
    [ "aa" ]       = "[%a%a].*[%a%a]",
    [ "pagename" ] = string.format( "^[^#<>%%[%%]|{}%c-%c%c]+$",
                                    1, 31, 127 ),
    [ "+" ]        = "%S"
}
local patternCJK = false



local function containsCJK( s )
    -- Is any CJK character present?
    -- Precondition:
    --     s  -- string
    -- Postcondition:
    --     Return false iff no CJK present
    -- Uses:
    --     >< patternCJK
    --     mw.ustring.char()
    --     mw.ustring.match()
    local r = false
    if not patternCJK then
        patternCJK = mw.ustring.char( 91,
                                       13312, 45,  40959,
                                      131072, 45, 178207,
                                      93 )
    end
    if mw.ustring.match( s, patternCJK ) then
        r = true
    end
    return r
end -- containsCJK()



local function facility( accept, attempt )
    -- Check string as possible file name or other source page
    -- Precondition:
    --     accept   -- string; requirement
    --                         file
    --                         file+
    --                         file:
    --                         file:+
    --                         image
    --                         image+
    --                         image:
    --                         image:+
    --     attempt  -- string; to be tested
    -- Postcondition:
    --     Return error keyword, or false
    -- Uses:
    --     Module:FileMedia
    --     FileMedia.isType()
    local r
    if attempt and attempt ~= "" then
        local lucky, FileMedia = pcall( require, "Module:FileMedia" )
        if type( FileMedia ) == "table" then
            FileMedia = FileMedia.FileMedia()
            local s, live = accept:match( "^([a-z]+)(:?)%+?$" )
            if live then
                if FileMedia.isType( attempt, s ) then
                    if FileMedia.isFile( attempt ) then
                        r = false
                    else
                        r = "notFound"
                    end
                else
                    r = "invalid"
                end
            elseif FileMedia.isType( attempt, s ) then
                r = false
            else
                r = "invalid"
            end
        else
            r = "missing"
        end
    elseif accept:match( "%+$" ) then
        r = "empty"
    else
        r = false
    end
    return r
end -- facility()



local function factory( say )
    -- Retrieve localized message string in content language
    -- Precondition:
    --     say  -- string; message ID
    -- Postcondition:
    --     Return some message string
    -- Uses:
    --     >  MessagePrefix
    --     >  L10nDef
    --     mw.language.getContentLanguage()
    --     mw.message.new()
    local c = mw.language.getContentLanguage():getCode()
    local m = mw.message.new( MessagePrefix .. say )
    local r = false
    if m:isBlank() then
        local l10n = L10nDef[ c ]
        if not l10n then
            l10n = L10nDef[ "en" ]
        end
        r = l10n[ say ]
    else
        m:inLanguage( c )
        r = m:plain()
    end
    if not r then
        r = string.format( "(((%s)))", say )
    end
    return r
end -- factory()



local function failsafe( story, scan )
    -- Test for match (possibly user-defined with syntax error)
    -- Precondition:
    --     story  -- string; parameter value
    --     scan   -- string; pattern
    -- Postcondition:
    --     Return nil, if not matching, else non-nil
    -- Uses:
    --     mw.ustring.match()
    return  mw.ustring.match( story, scan )
end -- failsafe()



local function failure( spec, suspect, options )
    -- Submit localized error message
    -- Precondition:
    --     spec     -- string; message ID
    --     suspect  -- string or nil; additional information
    --     options  -- table or nil; optional details
    --                 options.template
    -- Postcondition:
    --     Return string
    -- Uses:
    --     factory()
    local r = factory( spec )
    if type( options ) == "table" then
        if type( options.template ) == "string" then
            if #options.template > 0 then
                r = string.format( "%s (%s)", r, options.template )
            end
        end
    end
    if suspect then
        r = string.format( "%s: %s", r, suspect )
    end
    return r
end -- failure()



local function fault( store, key )
    -- Add key to collection string and insert separator
    -- Precondition:
    --     store  -- string or nil or false; collection string
    --     key    -- string or number; to be appended
    -- Postcondition:
    --     Return string; extended
    local r
    local s
    if type( key ) == "number" then
        s = tostring( key )
    else
        s = key
    end
    if store then
        r = string.format( "%s; %s", store, s )
    else
        r = s
    end
    return r
end -- fault()



local function feasible( analyze, options, abbr )
    -- Check content of a value
    -- Precondition:
    --     analyze  -- string to be analyzed
    --     options  -- table or nil; optional details
    --                 options.pattern
    --                 options.key
    --                 options.say
    --     abbr     -- true: abbreviated error message
    -- Postcondition:
    --     Return string with error message as configured;
    --            false if valid or no answer permitted
    -- Uses:
    --     >  Patterns
    --     failure()
    --     mw.text.trim()
    --     facility()
    --     failsafe()
    --     containsCJK()
    local r    = false
    local s    = false
    local show = nil
    local scan = false
    if type( options.pattern ) == "string" then
        if options.key then
            r = failure( "dupRule", false, options )
        else
            scan = options.pattern
        end
    else
        if type( options.key ) == "string" then
            s = mw.text.trim( options.key )
        else
            s = "+"
        end
        if s ~= "*" then
            scan = Patterns[ s ]
        end
        if type( scan ) == "string" then
            if s == "n" or s == "0,0" or s == "0.0" then
                if not analyze:match( "[0-9]" )  and
                   not analyze:match( "^%s*$" ) then
                    scan = false
                    if options.say then
                        show = string.format( "'%s'", options.say )
                    end
                    if abbr then
                        r = show
                    else
                        r = failure( "invalid", show, options )
                    end
                end
            end
        elseif s ~= "*" then
            local op, n, plus = s:match( "([<!=>]=?)([-0-9][%S]*)(+?)" )
            if op then
                n = tonumber( n )
                if n then
                    local i = tonumber( analyze )
                    if i then
                        if op == "<" then
                            i = ( i < n )
                        elseif op == "<=" then
                            i = ( i <= n )
                        elseif op == ">" then
                            i = ( i > n )
                        elseif op == ">=" then
                            i = ( i >= n )
                        elseif op == "==" then
                            i = ( i == n )
                        elseif op == "!=" then
                            i = ( i ~= n )
                        else
                            n = false
                        end
                    end
                    if not i then
                        r = "invalid"
                    end
                elseif plus then
                    r = "undefined"
                end
            elseif s:match( "^image%+?:?$" )  or
                   s:match( "^file%+?:?$" ) then
                r = facility( s, analyze )
                n = true
            elseif s:match( "langW?%+?" ) then
                n = "lang"
-- lang lang+
-- langW langW+
            end
            if not n and not r then
                r = "unknownRule"
            end
            if r then
                if options.say then
                    show = string.format( "'%s' %s", options.say, s )
                else
                    show = s
                end
                if abbr then
                    r = show
                else
                    r = failure( r, show, options )
                end
            end
        end
    end
    if scan then
        local legal, got = pcall( failsafe, analyze, scan )
        if legal then
            if not got then
                if s == "aa" then
                    got = containsCJK( analyze )
                end
                if not got then
                    if options.say then
                        show = string.format( "'%s'", options.say )
                    end
                    if abbr then
                        r = show
                    else
                        r = failure( "invalid", show, options )
                    end
                end
            end
        else
            r = failure( "badPattern",
                         string.format( "%s *** %s", scan, got ),
                         options )
        end
    end
    return r
end -- feasible()



local function fed( haystack, needle )
    -- Find needle in haystack map
    -- Precondition:
    --     haystack  -- table; map of key values
    --     needle    -- any; identifier
    -- Postcondition:
    --     Return true iff found
    local k, v
    for k, v in pairs( haystack ) do
        if k == needle then
            return true
        end
    end -- for k, v
    return false
end -- fed()



local function fetch( light, options )
    -- Return regular table with all parameters
    -- Precondition:
    --     light    -- true: template transclusion;  false: #invoke
    --     options  -- table; optional details
    --                 options.low
    -- Postcondition:
    --     Return table; whitespace-only values as false
    -- Uses:
    --     TemplatePar.downcase()
    --     mw.getCurrentFrame()
    --     frame:getParent()
    local g, k, v
    local r = { }
    if options.low then
        g = TemplatePar.downcase( options )
    else
        g = mw.getCurrentFrame()
        if light then
            g = g:getParent()
        end
        g = g.args
    end
    if type( g ) == "table"  then
        r = { }
        for k, v in pairs( g ) do
            if type( v ) == "string" then
                if v:match( "^%s*$" ) then
                    v = false
                end
            else
                v = false
            end
            if type( k ) == "number" then
                k = tostring( k )
            end
            r[ k ] = v
        end -- for k, v
    else
        r = g
    end
    return r
end -- fetch()



local function figure( append, options )
    -- Extend options by rule from #invoke strings
    -- Precondition:
    --     append   -- string or nil; requested rule
    --     options  --  table; details
    --                  ++ .key
    --                  ++ .pattern
    -- Postcondition:
    --     Return sequence table
    local r = options
    if type( append ) == "string" then
        local story = mw.text.trim( append )
        local sub   = story:match( "^/(.*%S)/$" )
        if type( sub ) == "string" then
            sub             = sub:gsub( "%%!", "|" )
            sub             = sub:gsub( "%%%(%(", "{{" )
            sub             = sub:gsub( "%%%)%)", "}}" )
            options.pattern = sub
            options.key     = nil
        else
            options.key     = story
            options.pattern = nil
        end
    end
    return r
end -- figure()



local function fill( specified )
    -- Split requirement string separated by '='
    -- Precondition:
    --     specified  -- string or nil; requested parameter set
    -- Postcondition:
    --     Return sequence table
    -- Uses:
    --     mw.text.split()
    local r
    if specified then
        local i, s
        r = mw.text.split( specified, "%s*=%s*" )
        for i = #r, 1, -1 do
            s = r[ i ]
            if #s == 0 then
                table.remove( r, i )
            end
        end -- for i, -1
    else
        r = { }
    end
    return r
end -- fill()



local function finalize( submit, options, frame )
    -- Finalize message
    -- Precondition:
    --     submit   -- string or false or nil; non-empty error message
    --     options  -- table or nil; optional details
    --                 options.format
    --                 options.preview
    --                 options.cat
    --                 options.template
    --     frame    -- object, or false
    -- Postcondition:
    --     Return string or false
    -- Uses:
    --     factory()
    local r = false
    if submit then
        local opt, s
        local lazy = false
        local show = false
        if type( options ) == "table" then
            opt  = options
            show = opt.format
            lazy = ( show == ""  or  show == "0"  or  show == "-" )
            s    = opt.preview
            if type( s ) == "string"  and
                s ~= ""  and  s ~= "0"  and  s ~= "-" then
                if lazy then
                    show = ""
                    lazy = false
                end
                if not frame then
                    frame = mw.getCurrentFrame()
                end
                if frame:preprocess( "{{REVISIONID}}" ) == "" then
                    if s == "1" then
                        show = "*"
                    else
                        show = s
                    end
                end
            end
        else
            opt = { }
        end
        if lazy then
            if not opt.cat then
                r = string.format( "%s %s",
                                   submit,  factory( "noMSGnoCAT" ) )
            end
        else
            r = submit
        end
        if r  and  not lazy then
            local i
            if not show  or  show == "*" then
                show = "<span class=\"error\">@@@</span>"
            end
            i = show:find( "@@@", 1, true )
            if i then
                -- No gsub() since r might contain "%3" (e.g. URL)
                r = string.format( "%s%s%s",
                                   show:sub( 1,  i - 1 ),
                                   r,
                                   show:sub( i + 3 ) )
            else
                r = show
            end
        end
        s = opt.cat
        if type( s ) == "string" then
            if opt.errNS then
                local ns = mw.title.getCurrentTitle().namespace
                local st = type( opt.errNS )
                if st == "string" then
                    local space  = string.format( ".*%%s%d%%s.*", ns )
                    local spaces = string.format( " %s ", opt.errNS )
                    if spaces:match( space ) then
                        opt.errNS = false
                    end
                elseif st == "table" then
                    for i = 1, #opt.errNS do
                        if opt.errNS[ i ] == ns then
                            opt.errNS = false
                            break    -- for i
                        end
                    end -- for i
                end
            end
            if opt.errNS then
                r = ""
            else
                if not r then
                   r = ""
                end
                if s:find( "@@@" ) then
                    if type( opt.template ) == "string" then
                        s = s:gsub( "@@@", opt.template )
                    end
                end
                local i
                local cats = mw.text.split( s, "%s*#%s*" )
                for i = 1, #cats do
                    s = mw.text.trim( cats[ i ] )
                    if #s > 0 then
                        r = string.format( "%s[[Category:%s|Category:%s]]", r, s )
                    end
                end -- for i
            end
        end
    end
    return r
end -- finalize()



local function finder( haystack, needle )
    -- Find needle in haystack sequence
    -- Precondition:
    --     haystack  -- table; sequence of key names, downcased if low
    --     needle    -- any; key name
    -- Postcondition:
    --     Return true iff found
    local i
    for i = 1, #haystack do
        if haystack[ i ] == needle then
            return true
        end
    end -- for i
    return false
end -- finder()



local function fix( valid, duty, got, options )
    -- Perform parameter analysis
    -- Precondition:
    --     valid    -- table; unique sequence of known parameters
    --     duty     -- table; sequence of mandatory parameters
    --     got      -- table; sequence of current parameters
    --     options  -- table or nil; optional details
    -- Postcondition:
    --     Return string as configured; empty if valid
    -- Uses:
    --     finder()
    --     fault()
    --     failure()
    --     fed()
    local k, v
    local r = false
    for k, v in pairs( got ) do
        if not finder( valid, k ) then
            r = fault( r, k )
        end
    end -- for k, v
    if r then
        r = failure( "unknown",
                     string.format( "'%s'", r ),
                     options )
    else -- all names valid
        local i, s
        for i = 1, #duty do
            s = duty[ i ]
            if not fed( got, s ) then
                r = fault( r, s )
            end
        end -- for i
        if r then
            r = failure( "undefined", r, options )
        else -- all mandatory present
            for i = 1, #duty do
                s = duty[ i ]
                if not got[ s ] then
                    r = fault( r, s )
                end
            end -- for i
            if r then
                r = failure( "empty", r, options )
            end
        end
    end
    return r
end -- fix()



local function flat( collection, options )
    -- Return all table elements with downcased string
    -- Precondition:
    --     collection  -- table; k=v pairs
    --     options     -- table or nil; optional messaging details
    -- Postcondition:
    --     Return table, may be empty; or string with error message.
    -- Uses:
    --     mw.ustring.lower()
    --     fault()
    --     failure()
    local k, v
    local r = { }
    local e = false
    for k, v in pairs( collection ) do
        if type ( k ) == "string" then
            k = mw.ustring.lower( k )
            if r[ k ] then
                e = fault( e, k )
            end
        end
        r[ k ] = v
    end -- for k, v
    if e then
        r = failure( "multiSpell", e, options )
    end
    return r
end -- flat()



local function fold( options )
    -- Merge two tables, create new sequence if both not empty
    -- Precondition:
    --     options  -- table; details
    --                 options.mandatory   sequence to keep unchanged
    --                 options.optional    sequence to be appended
    --                 options.low         downcased expected
    -- Postcondition:
    --     Return merged table, or message string if error
    -- Uses:
    --     finder()
    --     fault()
    --     failure()
    --     flat()
    local i, e, r, s
    local base   = options.mandatory
    local extend = options.optional
    if #base == 0 then
        if #extend == 0 then
            r = { }
        else
            r = extend
        end
    else
        if #extend == 0 then
            r = base
        else
            e = false
            for i = 1, #extend do
                s = extend[ i ]
                if finder( base, s ) then
                    e = fault( e, s )
                end
            end -- for i
            if e then
                r = failure( "dupOpt", e, options )
            else
                r = { }
                for i = 1, #base do
                    table.insert( r, base[ i ] )
                end -- for i
                for i = 1, #extend do
                    table.insert( r, extend[ i ] )
                end -- for i
            end
        end
    end
    if options.low  and  type( r ) == "table" then
        r = flat( r, options )
    end
    return r
end -- fold()



local function form( light, options, frame )
    -- Run parameter analysis on current environment
    -- Precondition:
    --     light    -- true: template transclusion;  false: #invoke
    --     options  -- table or nil; optional details
    --                 options.mandatory
    --                 options.optional
    --     frame    -- object, or false
    -- Postcondition:
    --     Return string with error message as configured;
    --            false if valid
    -- Uses:
    --     fold()
    --     fetch()
    --     fix()
    --     finalize()
    local duty, r
    if type( options ) == "table" then
        if type( options.mandatory ) ~= "table" then
            options.mandatory = { }
        end
        duty = options.mandatory
        if type( options.optional ) ~= "table" then
            options.optional = { }
        end
        r = fold( options )
    else
        options = { }
        duty    = { }
        r       = { }
    end
    if type( r ) == "table" then
        local got = fetch( light, options )
        if type( got ) == "table" then
            r = fix( r, duty, got, options )
        else
            r = got
        end
    end
    return finalize( r, options, frame )
end -- form()



local function format( analyze, options )
    -- Check validity of a value
    -- Precondition:
    --     analyze  -- string to be analyzed
    --     options  -- table or nil; optional details
    --                 options.say
    --                 options.min
    --                 options.max
    -- Postcondition:
    --     Return string with error message as configured;
    --            false if valid or no answer permitted
    -- Uses:
    --     feasible()
    --     failure()
    local r = feasible( analyze, options, false )
    local show
    if options.min  and  not r then
        if type( options.min ) == "number" then
            if type( options.max ) == "number" then
                if options.max < options.min then
                    r = failure( "minmax",
                                 string.format( "%d > %d",
                                                options.min,
                                                options.max ),
                                 options )
                end
            end
            if #analyze < options.min  and  not r then
                show = " <" .. options.min
                if options.say then
                    show = string.format( "%s '%s'", show, options.say )
                end
                r = failure( "tooShort", show, options )
            end
        else
            r = failure( "invalidPar", "min", options )
        end
    end
    if options.max  and  not r then
        if type( options.max ) == "number" then
            if #analyze > options.max then
                show = " >" .. options.max
                if options.say then
                    show = string.format( "%s '%s'", show, options.say )
                end
                r = failure( "tooLong", show, options )
            end
        else
            r = failure( "invalidPar", "max", options )
        end
    end
    return r
end -- format()



local function formatted( assignment, access, options )
    -- Check validity of one particular parameter in a collection
    -- Precondition:
    --     assignment  -- collection
    --     access      -- id of parameter in collection
    --     options     -- table or nil; optional details
    -- Postcondition:
    --     Return string with error message as configured;
    --            false if valid or no answer permitted
    -- Uses:
    --     mw.text.trim() 
    --     format()
    --     failure()
    local r = false
    if type( assignment ) == "table" then
        local story = assignment.args[ access ] or ""
        if type( access ) == "number" then
            story = mw.text.trim( story ) 
        end
        if type( options ) ~= "table" then
            options = { }
        end
        options.say = access
        r = format( story, options )
    end
    return r
end -- formatted()



local function furnish( frame, action )
    -- Prepare #invoke evaluation of .assert() or .valid()
    -- Precondition:
    --     frame    -- object; #invoke environment
    --     action   -- "assert" or "valid"
    -- Postcondition:
    --     Return string with error message or ""
    -- Uses:
    --     form()
    --     failure()
    --     finalize()
    --     TemplatePar.valid()
    --     TemplatePar.assert()
    local options = { mandatory = { "1" },
                      optional  = { "2",
                                    "cat",
                                    "errNS",
                                    "low",
                                    "max",
                                    "min",
                                    "format",
                                    "preview",
                                    "template" },
                      template  = string.format( "#invoke:%s|%s|",
                                                 "TemplatePar",
                                                 action )
                    }
    local r       = form( false, options, frame )
    if not r then
        local s
        options = { cat      = frame.args.cat,
                    errNS    = frame.args.errNS,
                    low      = frame.args.low,
                    format   = frame.args.format,
                    preview  = frame.args.preview,
                    template = frame.args.template
                  }
        options = figure( frame.args[ 2 ], options )
        if type( frame.args.min ) == "string" then
            s = frame.args.min:match( "^%s*([0-9]+)%s*$" )
            if s then
                options.min = tonumber( s )
            else
                r = failure( "invalidPar",
                             "min=" .. frame.args.min,
                             options )
            end
        end
        if type( frame.args.max ) == "string" then
            s = frame.args.max:match( "^%s*([1-9][0-9]*)%s*$" )
            if s then
                options.max = tonumber( s )
            else
                r = failure( "invalidPar",
                             "max=" .. frame.args.max,
                             options )
            end
        end
        if r then
            r = finalize( r, options, frame )
        else
            s = frame.args[ 1 ] or ""
            r = tonumber( s )
            if ( r ) then
                s = r
            end
            if action == "valid" then
                r = TemplatePar.valid( s, options, frame )
            elseif action == "assert" then
                r = TemplatePar.assert( s, "", options )
            end
        end
    end
    return r or ""
end -- furnish()



TemplatePar.assert = function ( analyze, append, options )
    -- Perform parameter analysis on a single string
    -- Precondition:
    --     analyze  -- string to be analyzed
    --     append   -- string: append error message, prepending <br />
    --                 false or nil: throw error with message
    --     options  -- table; optional details
    -- Postcondition:
    --     Return string with error message as configured;
    --            false if valid
    -- Uses:
    --     format()
    local r = format( analyze, options )
    if ( r ) then
        if ( type( append ) == "string" ) then
            if ( append ~= "" ) then
                r = string.format( "%s<br />%s", append, r )
            end
        else
            error( r, 0 )
        end
    end
    return r
end -- TemplatePar.assert()



TemplatePar.check = function ( options )
    -- Run parameter analysis on current template environment
    -- Precondition:
    --     options  -- table or nil; optional details
    --                 options.mandatory
    --                 options.optional
    -- Postcondition:
    --     Return string with error message as configured;
    --            false if valid
    -- Uses:
    --     form()
    return form( true, options, false )
end -- TemplatePar.check()



TemplatePar.count = function ()
    -- Return number of template parameters
    -- Postcondition:
    --     Return number, starting at 0
    -- Uses:
    --     mw.getCurrentFrame()
    --     frame:getParent()
    local k, v
    local r = 0
    local t = mw.getCurrentFrame():getParent()
    local o = t.args
    for k, v in pairs( o ) do
        r = r + 1
    end -- for k, v
    return r
end -- TemplatePar.count()



TemplatePar.countNotEmpty = function ()
    -- Return number of template parameters with more than whitespace
    -- Postcondition:
    --     Return number, starting at 0
    -- Uses:
    --     mw.getCurrentFrame()
    --     frame:getParent()
    local k, v
    local r = 0
    local t = mw.getCurrentFrame():getParent()
    local o = t.args
    for k, v in pairs( o ) do
        if not v:match( "^%s*$" ) then
            r = r + 1
        end
    end -- for k, v
    return r
end -- TemplatePar.countNotEmpty()



TemplatePar.downcase = function ( options )
    -- Return all template parameters with downcased name
    -- Precondition:
    --     options  -- table or nil; optional messaging details
    -- Postcondition:
    --     Return table, may be empty; or string with error message.
    -- Uses:
    --     mw.getCurrentFrame()
    --     frame:getParent()
    --     flat()
    local t = mw.getCurrentFrame():getParent()
    return flat( t.args, options )
end -- TemplatePar.downcase()



TemplatePar.valid = function ( access, options, frame )
    -- Check validity of one particular template parameter
    -- Precondition:
    --     access   -- id of parameter in template transclusion
    --                 string or number
    --     options  -- table or nil; optional details
    --     frame    -- object; #invoke environment
    -- Postcondition:
    --     Return string with error message as configured;
    --            false if valid or no answer permitted
    -- Uses:
    --     mw.text.trim()
    --     TemplatePar.downcase()
    --     frame:getParent()
    --     formatted()
    --     failure()
    --     finalize()
    local r = type( access )
    if r == "string" then
        r = mw.text.trim( access )
        if #r == 0 then
            r = false
        end
    elseif r == "number" then
        r = access
    else
        r = false
    end
    if r then
        local params
        if type( options ) ~= "table" then
            options = { }
        end
        if options.low then
            params = TemplatePar.downcase( options )
        else
            params = frame:getParent()
        end
        r = formatted( params, access, options )
    else
        r = failure( "noname", false, options )
    end
    return finalize( r, options, frame )
end -- TemplatePar.valid()



TemplatePar.verify = function ( options )
    -- Perform #invoke parameter analysis
    -- Precondition:
    --     options  -- table or nil; optional details
    -- Postcondition:
    --     Return string with error message as configured;
    --            false if valid
    -- Uses:
    --     form()
    return form( false, options, false )
end -- TemplatePar.verify()



-- Provide external access
local p = {}



function p.assert( frame )
    -- Perform parameter analysis on some single string
    -- Precondition:
    --     frame  -- object; #invoke environment
    -- Postcondition:
    --     Return string with error message or ""
    -- Uses:
    --     furnish()
    return furnish( frame, "assert" )
end -- .assert()



function p.check( frame )
    -- Check validity of template parameters
    -- Precondition:
    --     frame  -- object; #invoke environment
    -- Postcondition:
    --     Return string with error message or ""
    -- Uses:
    --     form()
    --     fill()
    local options = { optional  = { "all",
                                    "opt",
                                    "cat",
                                    "errNS",
                                    "low",
                                    "format",
                                    "preview",
                                    "template" },
                      template  = "#invoke:TemplatePar|check|"
                    }
    local r = form( false, options, frame )
    if not r then
        options = { mandatory = fill( frame.args.all ),
                    optional  = fill( frame.args.opt ),
                    cat       = frame.args.cat,
                    errNS     = frame.args.errNS,
                    low       = frame.args.low,
                    format    = frame.args.format,
                    preview   = frame.args.preview,
                    template  = frame.args.template
                  }
        r       = form( true, options, frame )
    end
    return r or ""
end -- .check()



function p.count( frame )
    -- Count number of template parameters
    -- Postcondition:
    --     Return string with digits including "0"
    -- Uses:
    --     TemplatePar.count()
    return tostring( TemplatePar.count() )
end -- .count()



function p.countNotEmpty( frame )
    -- Count number of template parameters which are not empty
    -- Postcondition:
    --     Return string with digits including "0"
    -- Uses:
    --     TemplatePar.countNotEmpty()
    return tostring( TemplatePar.countNotEmpty() )
end -- .countNotEmpty()



function p.match( frame )
    -- Combined analysis of parameters and their values
    -- Postcondition:
    --     Return string with error message or ""
    -- Uses:
    --     mw.text.trim()
    --     mw.ustring.lower()
    --     failure()
    --     form()
    --     TemplatePar.downcase()
    --     figure()
    --     feasible()
    --     fault()
    --     finalize()
    local r = false
    local options = { cat      = frame.args.cat,
                      errNS    = frame.args.errNS,
                      low      = frame.args.low,
                      format   = frame.args.format,
                      preview  = frame.args.preview,
                      template = frame.args.template
                    }
    local k, v, s
    local params = { }
    for k, v in pairs( frame.args ) do
        if type( k ) == "number" then
            s, v = v:match( "^ *([^=]+) *= *(%S.*%S*) *$" )
            if s then
                s = mw.text.trim( s )
                if s == "" then
                    s = false
                end
            end
            if s then
                if options.low then
                    s = mw.ustring.lower( s )
                end
                if params[ s ] then
                    s = params[ s ]
                    s[ #s + 1 ] = v
                else
                    params[ s ] = { v }
                end
            else
                r = failure( "invalidPar",  tostring( k ),  options )
                break -- for k, v
            end
        end
    end -- for k, v
    if not r then
        s = { }
        for k, v in pairs( params ) do
            s[ #s + 1 ] = k
        end -- for k, v
        options.optional = s
        r = form( true, options, frame )
    end
    if not r then
        local errMiss, errValues, lack, rule
        local targs = frame:getParent().args
        options.optional = nil
        if options.low then
            targs = TemplatePar.downcase()
        else
            targs = frame:getParent().args
        end
        errMiss   = false
        errValues = false
        for k, v in pairs( params ) do
            options.say = k
            errValue    = false
            s = targs[ k ]
            if s then
                if s == "" then
                    lack = true
                else
                    lack = false
                end
            else
                s    = ""
                lack = true
            end
            for r, rule in pairs( v ) do
                options = figure( rule, options )
                r       = feasible( s, options, true )
                if r then
                    if lack then
                        if errMiss then
                            errMiss = string.format( "%s, '%s'",
                                                     errMiss, k )
                        else
                            errMiss = string.format( "'%s'", k )
                        end
                    elseif not errMiss then
                        errValues = fault( errValues, r )
                    end
                    break -- for r, rule
                end
            end -- for s, rule
        end -- for k, v
        r = ( errMiss or errValues )
        if r then
            if errMiss then
                r = failure( "undefined", errMiss, options )
            else
                r = failure( "invalid", errValues, options )
            end
            r = finalize( r, options, frame )
        end
    end
    return r or ""
end -- .match()



function p.valid( frame )
    -- Check validity of one particular template parameter
    -- Precondition:
    --     frame  -- object; #invoke environment
    -- Postcondition:
    --     Return string with error message or ""
    -- Uses:
    --     furnish()
    return furnish( frame, "valid" )
end -- .valid()



function p.TemplatePar()
    -- Retrieve function access for modules
    -- Postcondition:
    --     Return table with functions
    return TemplatePar
end -- .TemplatePar()



return p