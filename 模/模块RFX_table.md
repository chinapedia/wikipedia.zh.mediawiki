-- This module is a replacement for the RfX report bot.

local rfx = require( 'Module:Rfx' )
local colours = mw.loadData( 'Module:RFX report/colour' )

local p = {}

local function makeRow( rfxObject )
    if not ( type( rfxObject ) == 'table' and rfxObject.getTitleObject and rfxObject.getSupportUsers ) then
        return nil
    end
    local style = ''
    local styleInline = ''
    local status = rfxObject:getStatus()
    if status == 'pending closure' then
        style = ' style="background: #f8cdc6;" |'
        styleInline = ' background: #f8cdc6;'
    end
    local page = rfxObject:getTitleObject().prefixedText
    local user = rfxObject.user or rfxObject:getTitleObject().subpageText
    local supports = rfxObject.supports
    local opposes = rfxObject.opposes
    local neutrals = rfxObject.neutrals
    local percent = rfxObject.percent
    local colour
    if percent then
        colour = colours[ rfxObject.type ][ percent ]
    end
    colour = colour or ''
    local votes
    if supports and opposes and neutrals and percent then
        votes = mw.ustring.format( [==[
        
| style="text-align: right;%s" | [[%s#Support|%d]]
| style="text-align: right;%s" | [[%s#Oppose|%d]]
| style="text-align: right;%s" | [[%s#Neutral|%d]]
| style="text-align: right; background: #%s;" | %d]==],
            styleInline, page, supports,
            styleInline, page, opposes,
            styleInline, page, neutrals,
            colour, percent
        )
    else
        votes = '\n| colspan="4" style="background: #f8cdc6;" | Error parsing votes'
    end
    if status then
        status = mw.language.getContentLanguage():ucfirst( status )
        if status == 'Pending closure' then
            status = 'Pending closure...'
        end
        status = mw.ustring.format( '\n| %s %s', style, status )
    else
        status = '\n| style="background: #f8cdc6;" | Error getting status'
    end 
    local endTime = rfxObject.endTime
    local secondsLeft = rfxObject:getSecondsLeft()
    local timeLeft = rfxObject:getTimeLeft()
    local time
    if endTime and timeLeft then
        time = mw.ustring.format( '\n| %s %s\n| %s %s', style, endTime, style, timeLeft )
    else
        time = '\n| colspan="2" style="background: #f8cdc6;" | Error parsing end time'
    end
    local dupes = rfxObject:dupesExist()
    if dupes then
        dupes = "'''yes'''"
    elseif dupes == false then
        dupes = 'no'
    else
        dupes = '--'
    end
    local report = rfxObject:getReport()
    if report then
        report = mw.ustring.format( '\n|%s [%s report]', style, tostring( report ) )
    else
        report = '\n| style="background: #f8cdc6;" | Report not found'
    end
    return mw.ustring.format(
        '\n|-\n|%s [[%s|%s]]%s%s%s\n| style="text-align: center;%s" | %s%s',
        style, page, user, votes, status, time, styleInline, dupes, report
    )
end

local function makeHeading( rfxType )
    if type( rfxType ) ~= 'string' then
        return nil
    end
    return mw.ustring.format(
        '\n|-\n! %s candidate !! S !! O !! N !! S%% !! Status !! Ending (UTC) !! Time left !! Dupes? !! Report',
        rfxType
    )
end

local function getRfxes( args )
    if type( args ) ~= 'table' then
        return nil
    end
    local nums, ret = {}, {}
    for k, v in pairs( args ) do
        if type( k ) == 'number' and k >= 1 and math.floor( k ) == k and k ~= math.huge then
            table.insert( nums, k )
        end
    end
    table.sort( nums )
    for i, v in ipairs( nums ) do
        ret[ i ] = args[ v ]
    end
    return ret
end

local function makeReportRows( args )
    local rfxes = getRfxes( args )
    if not rfxes then
        return nil
    end
    -- Get RfX objects and separate RfAs and RfBs.
    local rfas = {}
    local rfbs = {}
    for i, rfxPage in ipairs( rfxes ) do
        local rfxObject = rfx.new( rfxPage )
        if rfxObject then
            if rfxObject.type == 'rfa' then
                table.insert( rfas, rfxObject )
            elseif rfxObject.type == 'rfb' then
                table.insert( rfbs, rfxObject )
            end
        end
    end
    local ret = {}
    if #rfas > 0 then
        table.insert( ret, makeHeading( 'RfA' ) )
        for i, rfaObject in ipairs( rfas ) do
            table.insert( ret, makeRow( rfaObject ) )
        end
    end
    if #rfbs > 0 then
        table.insert( ret, makeHeading( 'RfB' ) )
        for i, rfbObject in ipairs( rfbs ) do
            table.insert( ret, makeRow( rfbObject ) )
        end
    end
    return table.concat( ret )
end

local function makeReport( args )
    local purgeLink = mw.title.getCurrentTitle():fullUrl( 'action=purge' )
    local header = mw.ustring.format(
        '\n|-\n! colspan="10" style="text-align: center;" | Requests for [[Wikipedia:Requests_for_adminship|adminship]] and [[Wikipedia:Requests_for_bureaucratship|bureaucratship]]<span class="plainlinks" style="float: right;"><small>[%s update]</small></span>',
        purgeLink
    )
    local rows = makeReportRows( args ) or ''
    if rows == '' then
        rows = '\n|-\n| colspan="10" | No current discussions. <small>Recent RfAs: ([[Wikipedia:Successful_requests_for_adminship|successful]], [[Wikipedia:Unsuccessful_adminship_candidacies_(Chronological)|unsuccessful]]) Recent RfBs: ([[Wikipedia:Successful_bureaucratship_candidacies|successful]], [[Wikipedia:Unsuccessful_bureaucratship_candidacies|unsuccessful]])</small>'
    end
    local style = args.style
    if not style then
        local float = args.float or args.align or 'right'
        local clear = args.clear or 'left'
        style = mw.ustring.format(
            'style="white-space:wrap; clear: %s; margin-top: 0em; margin-bottom: .5em; float: %s; padding: .5em 0em 0em 1.4em; background: #ffffff; border-collapse: collapse; border-spacing: 0;"',
            clear, float
        )
    end
    return mw.ustring.format( '\n{| class="wikitable" %s%s%s\n|-\n|}', style, header, rows )
end

function p.main( frame )
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
        v = mw.text.trim( v )
        if v ~= '' then
            args[k] = v
        end
    end
    return makeReport( args )
end

return p