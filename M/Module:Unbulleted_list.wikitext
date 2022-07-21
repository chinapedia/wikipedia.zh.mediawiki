-- This module implements {{unbulleted list}} and {{hlist}}.

local function getListItem( data, style, itemStyle )
    if not data then
        return nil
    end
    if style or itemStyle then
        style = style or ''
        itemStyle = itemStyle or ''
        return mw.ustring.format(
            '<li style="%s%s">%s</li>',
            style, itemStyle, data
        )
    else
        return mw.ustring.format(
            '<li>%s</li>',
            data
        )
    end
end

local function getArgNums( args )
    -- Returns an array containing the keys of all positional arguments
    -- that contain data (i.e. non-whitespace values).
    local nums = {}
    for k, v in pairs( args ) do
        if type( k ) == 'number' and 
            k >= 1 and 
            math.floor( k ) == k and 
            mw.ustring.match( v, '%S' ) then
                table.insert( nums, k )
        end
    end
    table.sort( nums )
    return nums
end

local function getClass( listType, class )
    local classes = {}
    if listType == 'hlist' then
        table.insert( classes, 'hlist' )
    else
        table.insert( classes, 'plainlist' )
    end
    table.insert( classes, class )
    local ret
    if #classes == 0 then
        return nil
    end
    return mw.ustring.format( ' class="%s"', table.concat( classes, ' ' ) )
end

local function getStyle( listType, indent, style )
    local styles = {}
    if listType == 'hlist' then
        indent = indent and tonumber( indent )
        indent = tostring( ( indent and indent * 1.6 ) or 0 )
        table.insert( styles, 'margin-left: ' .. indent .. 'em;' )
    end
    table.insert( styles, style )
    if #styles == 0 then
        return nil
    end
    return mw.ustring.format( ' style="%s"', table.concat( styles, ' ' ) )
end

local function buildList( args, listType )
    local listItems = {}
    local argNums = getArgNums( args )
    for i, num in ipairs( argNums ) do
        local item = getListItem(
            args[ num ],
            args.li_style,
            args[ 'li_style' .. tostring( num ) ]
        )
        table.insert( listItems, item )
    end
    if #listItems == 0 then
        return ''
    end
    local class = getClass( listType, args.class ) or ''
    local style = getStyle( listType, args.indent, args.style ) or ''
    local ulStyle = ( args.ul_style and ( ' style="' .. args.ul_style .. '"' ) ) or ''
    return mw.ustring.format( 
        '<div%s%s><ul%s>%s</ul></div>',
        class, style, ulStyle, table.concat( listItems )
    )
end

local function makeWrapper( listType )
    return function( frame )
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
        
        local args = {}
        for k, v in pairs( origArgs ) do
            if type( k ) == 'number' or v ~= '' then
                args[ k ] = v
            end
        end
        return buildList( args, listType )
    end
end

return {
    hlist = makeWrapper( 'hlist' ),
    unbulleted = makeWrapper( 'unbulleted' )
}