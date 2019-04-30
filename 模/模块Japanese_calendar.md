-- This module defines an "era" class for processing eras in the Japanese calendar.
-- It also contains functions to export the class properties to #invoke.

local eras = mw.loadData( 'Module:Japanese calendar/data' )
local halfToFull = require( 'Module:Convert character width' ).full -- Converts half-width characters to full-width characters.

--------------------------------------------------------------------
-- Helper functions
--------------------------------------------------------------------

local function yearToEraIndex( year )
    year = tonumber( year )
    if type( year ) ~= 'number' then return end
    for i, t in ipairs( eras ) do
        if year > t.startYear then
            return i
        elseif year == t.startYear then
            if eras[ i + 1 ] and eras[ i + 1 ].startYear == t.startYear then -- This checks for occasions when there were more than two eras in the same year. At the moment, that only applies to the year 686.
                return i + 1
            else
                return i
            end
        end
    end
end

local function textToEraIndex( s )
    if not s or s == '' then return end
    for i, t in ipairs( eras ) do
        if s == t.article or s == t.kanji then
            return i
        end
    end
end

--------------------------------------------------------------------
-- Era class definition
--------------------------------------------------------------------

local era = {}
era.__index = era

function era:new( init )
    init = type( init ) == 'table' and init or {}
    local obj = {}
    
    -- Grab the data from the init table.
    obj.gregorianYear = tonumber( init.year )
    local initText = type( init.era ) == 'string' and init.era or nil
    local initIndex = tonumber( init.index )
    if not ( initIndex and initIndex >= 1 and math.floor( initIndex ) == initIndex and initIndex ~= math.huge ) then -- Check that initIndex is a positive integer.
        initIndex = nil
    end
    
    -- Calculate the era data from the input. First we find the era from the era index, although this is only supposed
    -- to be for internal use. Next we find the era from the era name or the kanji if possible, as this allows us to
    -- specify the last year of one era rather than the first year of the next one, if that is the desired behaviour.
    local eraIndex
    if initIndex then
        eraIndex = initIndex
    elseif initText then
        eraIndex = textToEraIndex( initText )
    elseif obj.gregorianYear then
        eraIndex = yearToEraIndex( obj.gregorianYear )
    end
    
    -- If the data entry was found for the era, process it and add it to the object.
    if not eraIndex then return end
    local eraData = eras[ eraIndex ]
    if not eraData or not eraData.article or eraData.article == '' then return end -- Exit if we are not dealing with a valid era.
    
    obj.startYear = eraData.startYear
    obj.endYear = eraData.endYear
    obj.article = eraData.article
    obj.kanji = eraData.kanji
    obj.label = eraData.label
    
    -- Create a link to the era article if possible.
    if obj.label and obj.article then
        obj.link = mw.ustring.format( '[[%s|%s]]', obj.article, obj.label )
    elseif obj.article then
        obj.link = mw.ustring.format( '[[%s|%s]]', obj.article )
    end
    
    -- Allow matching years to different eras, but only for the first year of the next era. For example, Taisho 15 is also Showa 1, but there is no such thing as Taisho 16.
    -- So, the code era:new{ year = 1926, era = "Taishō" } will return an object with an eraYear of 15, and era:new{ year = 1926 } will return an object with an eraYear of 1.
    local nextEraData = eras[ eraIndex - 1 ]
    local nextStartYear = nextEraData and nextEraData.startYear
    if obj.gregorianYear
        and ( -- If there is a later era, only allow the first year of that era or an earlier year.
            not nextStartYear
            or ( nextStartYear and obj.gregorianYear <= nextStartYear )
        )
        and obj.gregorianYear >= obj.startYear -- Don't allow negative years.
        and obj.article ~= '' -- Don't allow periods between named eras.
        and ( obj.endYear and obj.gregorianYear <= obj.endYear or true ) -- If this era has an end year, don't allow years that are greater than the end year.
        then
        obj.eraYear = obj.gregorianYear - obj.startYear + 1
        if obj.eraYear == 1 then
            obj.eraYearKanji = '元'
        else
            obj.eraYearKanji = halfToFull( obj.eraYear )
        end
    end

    -- Make sure obj.label is available even if it is the same as the article name.
    obj.label = obj.label or obj.article
    
    -- Add methods to get the next and previous eras.
    function obj:getNextEra()
        if not eraIndex then return end       
        return era:new{ index = eraIndex - 1, year = obj.gregorianYear }
    end
    
    function obj:getPreviousEra()
        if not eraIndex then return end            
        return era:new{ index = eraIndex + 1, year = obj.gregorianYear }
    end

    -- Gets the era object for the "old" era. In most cases this is the same as the current era object, but
    -- if the era year for the current object is 1, this method will return the era object for the previous
    -- era. If the method can't find a valid previous era it will return the object for the current era.
    function obj:getOldEra()
        if obj.eraYear == 1 then
            local prevEra = obj:getPreviousEra()
            if prevEra then
                return prevEra
            else
                return obj
            end
        else
            return obj
        end
    end
    
    return setmetatable( obj, {
        __index = self
    })
end

--------------------------------------------------------------------
-- Interface for old Japanese calendar templates
--------------------------------------------------------------------

local function getStartYear( obj )
    return obj.startYear
end

local function getEndYear( obj )
    return obj.endYear
end

local function getEraYear( obj )
    return obj.eraYear
end

local function getEraYearKanji( obj )
    return obj.eraYearKanji
end

local function getArticle( obj )
    return obj.article
end

local function getLabel( obj )
    return obj.label
end

local function getLink( obj )
    return obj.link
end

local function getKanji( obj )
    return obj.kanji
end

local function getLabelAndEraYear( obj, kanji )
    local eraYear = kanji and obj.eraYearKanji or obj.eraYear
    if obj.label and eraYear then
        return mw.ustring.format( '%s %s', obj.label, tostring( eraYear ) )
    end
end

local function getLinkAndEraYear( obj, kanji )
    local eraYear = kanji and obj.eraYearKanji or obj.eraYear
    if obj.link and eraYear then
        return mw.ustring.format( '%s %s', obj.link, tostring( eraYear ) )
    end
end

local function getLabelAndEraYearKanji( obj )
    return getLabelAndEraYear( obj, true )
end

local function getLinkAndEraYearKanji( obj )
    return getLinkAndEraYear( obj, true )
end

-- Process the arguments from #invoke.
local function makeWrapper( func )
    return function( frame )
        -- If called via #invoke, use the args passed into the invoking
        -- template, or the args passed to #invoke if any exist. Otherwise
        -- assume args are being passed directly in from the debug console
        -- or from another Lua module.
        local origArgs
        if frame == mw.getCurrentFrame() then
            origArgs = frame:getParent().args
            for k, v in pairs( frame.args ) do
                origArgs = frame.args
                break
            end
        else
            origArgs = frame
        end
        -- Trim whitespace and remove blank arguments.
        local args = {}
        for k, v in pairs( origArgs ) do
            if type( v ) == 'string' then
                v = mw.text.trim( v )
            end
            if v ~= '' then
                args[k] = v
            end
        end
        
        local myEra
        local otherEraArgs = {}
        table.insert( otherEraArgs, args.next )
        table.insert( otherEraArgs, args.previous )
        table.insert( otherEraArgs, args.old )
        if #otherEraArgs > 1 then
            return '<strong class="error">[[Module:Japanese_calendar|Module:Japanese calendar]] error: you can only specify one parameter out of "next", "previous" and "old".</strong>'
        elseif args.next then
            myEra = era:new( args ):getNextEra()
        elseif args.previous then
            myEra = era:new( args ):getPreviousEra()
        elseif args.old then
            myEra = era:new( args ):getOldEra()
        else
            myEra = era:new( args )
        end
        return myEra and func( myEra ) or ''
    end
end

--------------------------------------------------------------------
-- Return the era class and the template interface
--------------------------------------------------------------------
 
return {
    era = function () return era end, -- Accessor function for getting the era class from other modules.
    baseyear = makeWrapper( getStartYear ),
    endyear = makeWrapper( getEndYear ),
    year = makeWrapper( getEraYear ),
    kanjiyear = makeWrapper( getEraYearKanji ),
    article = makeWrapper( getArticle ),
    label = makeWrapper( getLabel ),
    link = makeWrapper( getLink ),
    kanji = makeWrapper( getKanji ),
    label_year = makeWrapper( getLabelAndEraYear ),
    link_year = makeWrapper( getLinkAndEraYear ),
    label_kanjiyear = makeWrapper( getLabelAndEraYearKanji ),
    link_kanjiyear = makeWrapper( getLinkAndEraYearKanji )
}