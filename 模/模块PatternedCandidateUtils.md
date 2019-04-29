local z = {}

function getCandidates( frame )
    local page = mw.title.new( frame.args.title ):getContent()
    local matches = {}
    local black = {}
    if frame.args.black then
        for b in mw.text.gsplit( frame.args.black, '|', true ) do
            black[b] = true
        end
    end
    for m in mw.ustring.gmatch( page, frame.args.pattern ) do
        if not black[m] and not ( frame.args.blackregex and mw.ustring.match( m, frame.args.blackregex ) ) then
            table.insert( matches, m )
        end
    end
    return matches
end

function z.count( frame )
    return #getCandidates( frame )
end

function z.list( frame )
    local list = getCandidates( frame )
    local linkprefix = frame.args.linkprefix
    for i = 1, #list do
        if linkprefix then
            list[i] = '[[:'_.._linkprefix_.._list[i]_.._'|' .. list[i] .. ']]'
        else
            list[i] = '[[:'_.._list[i]_.._'|:' .. list[i] .. ']]'
        end
    end
    if #list > 0 then
        return table.concat( list, '－' )
    else
        return '暂无'
    end
end

return z