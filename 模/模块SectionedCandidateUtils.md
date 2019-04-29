local parser = require( 'Module:ParsePage' )

local z = {}

function getCandidates( frame )
    text, sections = parser.getSections( frame:expandTemplate{ title = frame.args.title }, tonumber( frame.args.level ) )
    for i = 1, #sections - 1 do
        sections[i] = mw.text.trim( mw.ustring.gsub( sections[i + 1], 'UNIQ.-QINU', '' ) )
    end
    sections[#sections] = nil
    return sections
end

function z.count( frame )
    return #getCandidates( frame )
end

function z.list( frame )
    list = getCandidates( frame )
    if frame.args.linkprefix then
        linkprefix = mw.text.trim( mw.ustring.gsub( frame.args.linkprefix, 'UNIQ.-QINU', '' ) )
    else
        linkprefix = nil
    end
    for i = 1, #list do
        if linkprefix then
            sections[i] = '[[:'_.._linkprefix_.._sections[i]_.._'|' .. sections[i] .. ']]'
        else
            sections[i] = '[[:'_.._sections[i]_.._'|:' .. sections[i] .. ']]'
        end
    end
    if #list > 0 then
        return table.concat( list, '－' )
    else
        return '暂无'
    end
end

return z