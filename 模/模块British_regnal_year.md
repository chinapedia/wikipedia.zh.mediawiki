-- This module implements {{British regnal year}}. It converts a year in the Gregorian
-- calendar to the equivalent English or British regnal year.

local data = mw.loadData( 'Module:British regnal year/data' )

local p = {}

function p.main( frame )
    -- If we are being called from #invoke, then the year is the first positional
    -- argument. If not, it is the frame parameter.
    local inputYear
    if frame == mw.getCurrentFrame() then
        inputYear = frame:getParent().args[ 1 ]
        local frameArgsYear = frame.args[ 1 ]
        if frameArgsYear then
            inputYear = frameArgsYear
        end
    else
        inputYear = frame
    end

    -- Convert the input to an integer if possible. Return "N/A" if the input could
    -- not be converted, or if the converted input is too big or too small.
    if type( inputYear ) ~= 'number' then
        inputYear = tonumber( inputYear )
    end
    if not inputYear then
        return "''N/A''"
    end
    local currentYear = tonumber( mw.language.getContentLanguage():formatDate( 'Y' ) )
    if inputYear < 1066 or inputYear > currentYear then
        return "''N/A''"
    end
    
    -- Find the year in the data page and display the output.
    for _, t in ipairs( data ) do
        local dataYear = t.year
        if inputYear >= dataYear then
            -- Get data values from the data page.
            local startYear = t.startYear
            local currentRegnalYear = inputYear - dataYear + startYear
            local linkCurrent = t.linkCurrent
            local prevEndYear = t.prevEndYear
            local linkPrev = t.linkPrev
            local note = t.note

            if inputYear > dataYear then
                -- Years with the same monarch.
                return mw.ustring.format(
                    '%d %s – %d %s%s',
                    currentRegnalYear - 1, linkCurrent, currentRegnalYear, linkCurrent, note or ''
                )
            elseif inputYear == dataYear and prevEndYear and linkPrev then
                -- Years with a different monarch.
                return mw.ustring.format(
                    '%d %s – %d %s%s',
                    prevEndYear, linkPrev, currentRegnalYear, linkCurrent, note or ''
                )
            else
                -- This should only match the year 1066.
                return mw.ustring.format(
                    '%d %s%s',
                    currentRegnalYear, linkCurrent, note or ''
                )
            end
        end
    end
end

return p