--[[
this module is meant for language-dependant time calculations.
ATM it exports a single function: sumHMS, which accepts unnamed (aka "order based")
arguments in the form ssss (any number of digits) or "mm:ss" or "hh:mm:ss:,
converts them all to seconds, sums them up, and returns the output string 
describing the total duration, using mw.getContentLanguage():formatDuration()
an optional paramter, "units" tells the formatting function which units to use:
e.g. {{invoke:Duration | sumHMS | 7211 | units = minutes, seconds}} will return "120 minutes and 11 seconds".
{{invoke:Duration|sumHMS| 1:0:11 | 1:00:00 | units= seconds}} will return "7211 seconds"
]]


local function sumHMS( args )
    local total = 0
    
    function oneMore( st )
        if type( st ) ~= 'string' then return end
        local t, ar = 0, { st:match( "^%s*(%d*):?(%d*):?(%d*)%s*$" ) }
        for _, v in ipairs( ar ) do
            local n = tonumber( v )
            if n then t = t * 60 + n end
        end
        total = total + t
    end

    for _, v in ipairs( args ) do oneMore( v ) end
    local units
    if args.units then 
        units = {}
        for unit in mw.ustring.gmatch( args.units, "%w+" ) do -- this silliness should be replaced with mw.text.split("%W+") once mw.text is available. 
            table.insert( units, unit ) 
        end
    end
    return mw.language.getContentLanguage():formatDuration( total, units )
end

return {
    sumHMS = function( frame ) return sumHMS( frame.args ) end,
}