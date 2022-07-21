--<source lang=lua>
--[[
    keywords are used for languages: they are the names of the actual
    parameters of the template
]]

local keywords = {
    barChart = 'bar chart',
    pieChart = 'pie chart',
    width = 'width',
    height = 'height',
    stack = 'stack',
    colors = 'colors',
    group = 'group',
    xlegend = 'x legends',
    tooltip = 'tooltip',
    links = 'links',
    defcolor = 'default color',
    scalePerGroup = 'scale per group',
    unitsPrefix = 'units prefix',
    unitsSuffix = 'units suffix',
    groupNames = 'group names',
    slices = 'slices',
    slice = 'slice',
    radius = 'radius',
    percent = 'percent',

} -- here is what you want to translate

local defColors = require "Module:Plotter/DefaultColors"

local function nulOrWhitespace( s )
    return not s or mw.text.trim( s ) == ''
end

local function createGroupList( tab, legends, cols )
    if #legends > 1 then
        table.insert( tab, mw.text.tag( 'div' ) )
        local list = {}
        local spanStyle = "padding:0 1em;background-color:%s;box-shadow:inset 0 0 1px 1px rgba(0,0,0,0.2);margin-right:1em;" --替换投影。原“box-shadow:2px -1px 4px 0 silver”投影太难看。
        for gi = 1, #legends do
            local span = mw.text.tag( 'span', { style = string.format( spanStyle, cols[gi] ) }, ' ' ) .. ' '..  legends[gi]
            table.insert( list, mw.text.tag( 'li', {}, span ) )
        end
        table.insert( tab,
            mw.text.tag( 'ul',
                {style="width:100%;list-style:none;-webkit-column-width:12em;-moz-column-width:12em;column-width:12em;"},
                table.concat( list, '\n' )
            )
        )
        table.insert( tab, '</div>' )
    end
end

function pieChart( frame )
    local res, imslices, args = {}, {}, frame.args
    local radius
    local values, colors, names, legends, links = {}, {}, {}, {}, {}
    local delimiter = args.delimiter or ':'
    local lang = mw.getContentLanguage()

    function getArg( s, def, subst, with )
        local result = args[keywords[s]] or def or ''
        if subst and with then result = mw.ustring.gsub( result, subst, with ) end
        return result
    end

    function analyzeParams()
        function addSlice( i, slice )
            local value, name, color, link = unpack( mw.text.split( slice, '%s*' .. delimiter .. '%s*' ) )
            values[i] = tonumber( lang:parseFormattedNumber( value ) )
                or error( string.format( 'Slice %d: "%s", first item("%s") could not be parsed as a number', i, value or '', sliceStr ) )
            colors[i] = not nulOrWhitespace( color ) and color or defColors[i * 2]
            names[i] = name or ''
            links[i] = link
        end
        
        radius = getArg( 'radius', 150 )
        local slicesStr = getArg( 'slices' )
        local prefix = getArg( 'unitsPrefix', '', '_', ' ' )
        local suffix = getArg( 'unitsSuffix', '', '_', ' ' )
        local percent = args[keywords.percent]
        local sum = 0
        local i, value = 0
        for slice in mw.ustring.gmatch( slicesStr or '', "%b()" ) do
            i = i + 1
            addSlice( i, mw.ustring.match( slice, '^%(%s*(.-)%s*%)$' ) )
        end
        
        for k, v in pairs(args) do
            local ind = mw.ustring.match( k, '^' .. keywords.slice .. '%s+(%d+)$' )
            if ind then addSlice( tonumber( ind ), v ) end
        end
        
        for _, val in ipairs( values ) do sum = sum + val end
        for i, value in ipairs( values ) do
            local addprec = percent and string.format( ' (%0.1f%%)', value / sum * 100 ) or ''
            legends[i] = mw.ustring.format( '%s: %s%s%s%s', names[i], prefix, lang:formatNum( value ), suffix, addprec )
            links[i] = mw.text.trim( links[i] or mw.ustring.format( '[[#noSuchAnchor|%s]]', legends[i] ) )
        end
    end

    function addRes( ... )
        for _, v in pairs( { ... } ) do
            table.insert( res, v )
        end
    end

    function createImageMap()
        addRes( '{{#tag:imagemap|', 'Image:Circle frame.svg{{!}}' .. ( radius * 2 ) .. 'px' )
        addRes( unpack( imslices ) )
        addRes( 'desc none', '}}' )
    end

    function drawSlice( i, q, start )
        local color = colors[i]
        local angle = start * 2 * math.pi
        local sin, cos = math.abs( math.sin( angle ) ), math.abs( math.cos( angle ) )
        local wsin, wcos = sin * radius, cos * radius
        local s1, s2, w1, w2, w3, w4, width, border
        local style
        if q == 1 then
            border = 'left'
            w1, w2, w3, w4 = 0, 0, wsin, wcos
            s1, s2 = 'bottom', 'left'
        elseif q == 2 then
            border = 'bottom'
            w1, w2, w3, w4 = 0, wcos, wsin, 0
            s1, s2 = 'bottom', 'right'
        elseif q == 3 then
            border = 'right'
            w1, w2, w3, w4 = wsin, wcos, 0, 0
            s1, s2 = 'top', 'right'
        else
            border = 'top'
            w1, w2, w3, w4 = wsin, 0, 0, wcos
            s1, s2 = 'top', 'left'
        end

        local style = string.format( 'position:absolute;%s:%spx;%s:%spx;width:%spx;height:%spx', s1, radius, s2, radius, radius, radius )
        if start <= ( q - 1 ) * 0.25 then
            style = string.format( '%s;border:0;background-color:%s', style, color )
        else
            style = string.format( '%s;border-width:%spx %spx %spx %spx;border-%s-color:%s', style, w1, w2, w3, w4, border, color )
        end
        addRes( mw.text.tag( 'div', { class = 'transborder', style = style }, '' ) )
    end

    function createSlices()
        function coordsOfAngle( angle )
            return ( 100 + math.floor( 100 * math.cos( angle ) ) ) .. ' ' .. ( 100 - math.floor( 100 * math.sin( angle ) ) )
        end

        local sum, start = 0, 0
        for _, value in ipairs( values ) do sum = sum + value end
        for i, value in ipairs(values) do
            local poly = { 'poly 100 100' }
            local startC, endC =  start / sum, ( start + value ) / sum
            local startQ, endQ = math.floor( startC * 4 + 1 ), math.floor( endC * 4 + 1 )
            for q = startQ, math.min( endQ, 4 ) do drawSlice( i, q, startC ) end
            for angle = startC * 2 * math.pi, endC * 2 * math.pi, 0.02 do
                table.insert( poly,  coordsOfAngle( angle ) )
            end
            table.insert( poly, coordsOfAngle( endC * 2 * math.pi ) .. ' 100 100 ' .. links[i] )
            table.insert( imslices, table.concat( poly, ' ' ) )
            start = start + values[i]
        end
    end

    analyzeParams()
    if #values == 0 then error( "no slices found - can't draw pie chart" ) end
    addRes( mw.text.tag( 'div', { style = string.format( "max-width:%spx", radius * 2 ) } ) )
    addRes( mw.text.tag( 'div', { style = string.format( 'position:relative;min-width:%spx;min-height:%spx;max-width:%spx;overflow:hidden;', radius * 2, radius * 2, radius * 2 ) } ) )
    createSlices()
    addRes( mw.text.tag( 'div', { style = string.format( 'position:absolute;min-width:%spx;min-height:%spx;overflow:hidden;', radius * 2, radius * 2 ) } ) )
    createImageMap()
    addRes( '</div>' ) -- close "position:relative" div that contains slices and imagemap.
    addRes( '</div>' ) -- close "position:relative" div that contains slices and imagemap.
    createGroupList( res, legends, colors ) -- legends
    addRes( '</div>' ) -- close containing div
    return frame:preprocess( table.concat( res, '\n' ) )
end


function barChart( frame )
    local res = {}
    local args = frame.args -- can be changed to frame:getParent().args
    local values, xlegends, colors, tooltips, yscales = {}, {}, {}, {} ,{}, {}, {}
    local groupNames, unitsSuffix, unitsPrefix, links = {}, {}, {}, {}
    local width, height, stack, delimiter = 500, 350, false, ':'
    local chartWidth, chartHeight, defcolor, scalePerGroup


    local numGroups, numValues
    local scaleWidth

    function validate()
        function asGroups( name, tab, toDuplicate, emptyOK )
            if #tab == 0 and not emptyOK then
                error( "must supply values for " .. keywords[name] )
            end
            if #tab == 1 and toDuplicate then
                for i = 2, numGroups do tab[i] = tab[1] end
            end
            if #tab > 0 and #tab ~= numGroups then
                error ( keywords[name] .. ' should contain the same number of items as the number of groups (' .. numGroups .. ')')
            end
        end

        -- do all sorts of validation here, so we can assume all params are good from now on.
        -- among other things, replace numerical values with mw.language:parseFormattedNumber() result


        chartHeight = height - 80
        numGroups = #values
        numValues = #values[1]
        defcolor = defcolor or 'blue'
        colors[1] = colors[1] or defcolor
        scaleWidth = scalePerGroup and 80 * numGroups or 100
        chartWidth = width -scaleWidth
        asGroups( 'unitsPrefix', unitsPrefix, true, true )
        asGroups( 'unitsSuffix', unitsSuffix, true, true )
        asGroups( 'colors', colors, true, true )
        asGroups( 'groupNames', groupNames, false, false )
        if stack and scalePerGroup then
            error( string.format( 'Illegal settings: %s and %s are incompatible.', keyword.stack, keyword.scalePerGroup ) )
        end
        for gi = 2, numGroups do
            if #values[gi] ~= numValues then error( keywords.group .. " " .. gi .. " does not have same number of values as " .. keywords.group .. " 1" ) end
        end
        if #xlegends ~= numValues then error( 'Illegal number of ' .. keywords.xlegend .. '. Should be exatly ' .. numValues ) end
    end

    function extractParams()
        function testone( keyword, key, val, tab )
            i = keyword == key and 0 or key:match( keyword .. "%s+(%d+)" )
            if not i then return end
            i = tonumber( i ) or error("Expect numerical index for key " .. keyword .. " instead of '" .. key .. "'")
            if i > 0 then tab[i] = {} end
            for s in mw.text.gsplit( val, '%s*' .. delimiter .. '%s*' ) do
                table.insert( i == 0 and tab or tab[i], s )
            end
            return true
        end

        for k, v in pairs( args ) do
            if k == keywords.width then
                width = tonumber( v )
                if not width or width < 200 then
                    error( 'Illegal width value (must be a number, and at least 200): ' .. v )
                end
            elseif k == keywords.height then
                height = tonumber( v )
                if not height or height < 200 then
                    error( 'Illegal height value (must be a number, and at least 200): ' .. v )
                end
            elseif k == keywords.stack then stack = true
            elseif k == keywords.scalePerGroup then scalePerGroup = true
            elseif k == keywords.defcolor then defcolor = v
            else
                for keyword, tab in pairs( {
                    group = values,
                    xlegend = xlegends,
                    colors = colors,
                    tooltip = tooltips,
                    unitsPrefix = unitsPrefix,
                    unitsSuffix = unitsSuffix,
                    groupNames = groupNames,
                    links = links,
                    } ) do
                        if testone( keywords[keyword], k, v, tab )
                            then break
                        end
                end
            end
        end
    end

    function roundup( x ) -- returns the next round number: eg., for 30 to 39.999 will return 40, for 3000 to 3999.99 wil return 4000. for 10 - 14.999 will return 15.
        local ordermag = 10 ^ math.floor( math.log10( x ) )
        local normalized = x /  ordermag
        local top = normalized >= 1.5 and ( math.floor( normalized + 1 ) ) or 1.5
        return ordermag * top, top, ordermag
    end

    function calcHeightLimits() -- if limits were passed by user, use ithem, otherwise calculate. for "stack" there's only one limet.
        if stack then
            local sums = {}
            for _, group in pairs( values ) do
                for i, val in ipairs( group ) do sums[i] = ( sums[i] or 0 ) + val end
            end
            local sum = math.max( unpack( sums ) )
            for i = 1, #values do yscales[i] = sum end
        else
            for i, group in ipairs( values ) do yscales[i] = math.max( unpack( group ) ) end
        end
        for i, scale in ipairs( yscales ) do yscales[i] = roundup( scale ) end
        if not scalePerGroup then for i = 1, #values do yscales[i] = math.max( unpack( yscales ) ) end end
    end

    function tooltip( gi, i, val )
        if tooltips and tooltips[gi] and not nulOrWhitespace( tooltips[gi][i] ) then return tooltips[gi][i], true end
        local groupName = not nulOrWhitespace( groupNames[gi] ) and groupNames[gi] .. ': ' or ''
        local prefix = unitsPrefix[gi] or unitsPrefix[1] or ''
        local suffix = unitsSuffix[gi] or unitsSuffix[1] or ''
        return mw.ustring.gsub(groupName .. prefix .. mw.getContentLanguage():formatNum( tonumber( val ) or 0 ) .. suffix, '_', ' '), false
    end

    function calcHeights( gi, i, val )
        local barHeight = math.floor( val / yscales[gi] * chartHeight + 0.5 ) -- add half to make it "round" insstead of "trunc"
        local top, base = chartHeight - barHeight, 0
        if stack then
            local rawbase = 0
            for j = 1, gi - 1 do rawbase = rawbase + values[j][i] end -- sum the "i" value of all the groups below our group, gi.
            base = math.floor( chartHeight * rawbase / yscales[gi] ) -- normally, and especially if it's "stack", all the yscales must be equal.
        end
        return barHeight, top - base
    end

    function groupBounds( i )
        local setWidth = math.floor( chartWidth / numValues )
        local setOffset = ( i - 1 ) * setWidth
        return setOffset, setWidth
    end

    function calcx( gi, i )
        local setOffset, setWidth = groupBounds( i )
        if stack then
            local barWidth = math.min( 38, math.floor( 0.8 * setWidth ) )
            return setOffset + (setWidth - barWidth) / 2, barWidth
        end
        setWidth = 0.85 * setWidth
        local barWidth = math.floor( 0.75 * setWidth / numGroups )
        local left = setOffset + math.floor( ( gi - 1 ) / numGroups * setWidth )
        return left, barWidth
    end

    function drawbar( gi, i, val )
        local color, tooltip, custom = colors[gi] or defcolor or 'blue', tooltip( gi, i, val )
        local left, barWidth = calcx( gi, i )
        local barHeight, top = calcHeights( gi, i, val )
        local style = string.format("position:absolute;left:%spx;top:%spx;height:%spx;min-width:%spx;max-width:%spx;background-color:%s;overflow:hidden;",--删投影。
                        left, top, barHeight, barWidth, barWidth, color)
        local link = links[gi] and links[gi][i] or ''
        local img = not nulOrWhitespace( link ) and mw.ustring.format( '[[File:Transparent.png|1000px]]', link, custom and tooltip or '' ) or ''
        table.insert( res, mw.text.tag( 'div', { style = style, title = tooltip, }, img ) )
    end


    function drawYScale()
        function drawSingle( gi, color, width, single )
            local yscale = yscales[gi]
            local _, top, ordermag = roundup( yscale * 0.999 )
            local numnotches = top <= 1.5 and top * 4
                    or top < 4  and top * 2
                    or top
            local valStyleStr =
                single and 'position:absolute;height=20px;text-align:right;vertical-align:middle;width:%spx;top:%spx;padding:0 2px'
                or 'position:absolute;height=20px;text-align:right;vertical-align:middle;width:%spx;top:%spx;left:3px;background-color:%s;color:white;font-weight:bold;text-shadow:-1px -1px 0 #000,1px -1px 0 #000,-1px 1px 0 #000,1px 1px 0 #000;padding:0 2px'
            local notchStyleStr = 'position:absolute;height=1px;min-width:5px;top:%spx;left:%spx;border:1px solid %s;'
            for i = 1, numnotches do
                local val = i / numnotches * yscale
                local y = chartHeight - calcHeights( gi, 1, val )
                local div = mw.text.tag( 'div', { style = string.format( valStyleStr, width - 10, y - 10, color ) }, mw.getContentLanguage():formatNum( tonumber( val ) or 0 ) )
                table.insert( res, div )
                div = mw.text.tag( 'div', { style = string.format( notchStyleStr, y, width - 4, color ) }, '' )
                table.insert( res, div )
            end
        end

        if scalePerGroup then
            local colWidth = 80
            local colStyle = "position:absolute;height:%spx;min-width:%spx;left:%spx;border-right:1px solid %s;color:%s"
            for gi = 1, numGroups do
                local left = ( gi - 1 ) * colWidth
                local color = colors[gi] or defcolor
                table.insert( res, mw.text.tag( 'div', { style = string.format( colStyle, chartHeight, colWidth, left, color, color ) } ) )
                drawSingle( gi, color, colWidth )
                table.insert( res, '</div>' )
            end
        else
            drawSingle( 1, 'black', scaleWidth, true )
        end
    end

    function drawXlegends()
        local setOffset, setWidth
        local legendDivStyleFormat = "position:absolute;left:%spx;top:10px;min-width:%spx;max-width:%spx;text-align:center;veritical-align:top;"
        local tickDivstyleFormat = "position:absolute;left:%spx;height:10px;width:1px;border-left:1px solid black;"
        for i = 1, numValues do
            if not nulOrWhitespace( xlegends[i] ) then
                setOffset, setWidth = groupBounds( i )
                -- setWidth = 0.85 * setWidth
                table.insert( res, mw.text.tag( 'div', { style = string.format( legendDivStyleFormat, setOffset - 5, setWidth - 10, setWidth - 10 ) }, xlegends[i] or '' ) )
                table.insert( res, mw.text.tag( 'div', { style = string.format( tickDivstyleFormat, setOffset + setWidth / 2 ) }, '' ) )
            end
        end
    end

    function drawChart()
        table.insert( res, mw.text.tag( 'div', { style = string.format( 'max-width:%spx;', width ) } ) )
        table.insert( res, mw.text.tag( 'div', { style = string.format("position:relative;min-height:%spx;min-width:%spx;max-width:%spx;", height, width, width ) } ) )

        table.insert( res, mw.text.tag( 'div', { style = string.format("float:right;position:relative;min-height:%spx;min-width:%spx;max-width:%spx;border-left:1px black solid;border-bottom:1px black solid;", chartHeight, chartWidth, chartWidth ) } ) )
        for gi, group in pairs( values ) do
            for i, val in ipairs( group ) do
                drawbar( gi, i, val )
            end
        end
        table.insert( res, '</div>' )
        table.insert( res, mw.text.tag( 'div', { style = string.format("position:absolute;height:%spx;min-width:%spx;max-width:%spx;", chartHeight, scaleWidth, scaleWidth, scaleWidth ) } ) )
        drawYScale()
        table.insert( res, '</div>' )
        table.insert( res, mw.text.tag( 'div', { style = string.format( "position:absolute;top:%spx;left:%spx;width:%spx;", chartHeight, scaleWidth, chartWidth ) } ) )
        drawXlegends()
        table.insert( res, '</div>' )
        table.insert( res, '</div>' )
        createGroupList( res, groupNames, colors )
        table.insert( res, '</div>' )
    end

    extractParams()
    validate()
    calcHeightLimits()
    drawChart()
    return table.concat( res, "\n" )
end

return {
    ['bar-chart'] = barChart,
    [keywords.barChart] = barChart,
    [keywords.pieChart] = pieChart,
}
--</source>