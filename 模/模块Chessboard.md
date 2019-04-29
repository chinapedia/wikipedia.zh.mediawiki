local p = {}
 
function chessboard(args, size, rev, letters, numbers, header, footer, align, clear)
    function image_square( pc, row, col, size )
        local colornames = { l = '白', d = '黑' }
        local piecenames = { 
            p = '兵', 
            r = '車', 
            n = '馬', 
            b = '象', 
            q = '-{后}-', 
            k = '王', 
            a = 'archbishop',
            c = 'chancelor', 
            z = 'champion', 
            w = 'wizard', 
            t = 'fool', 
            h = '倒兵', 
            m = '倒車', 
            s = '倒馬', 
            f = '倒王',  
            e = '倒象', 
            g = '倒-{后}-',
            }
        local symnames = { 
            xx = '黑叉', 
            ox = '白叉', 
            xo = '黑圈', 
            oo = '白圈',
            ul = '左上', 
            ua = '上', 
            ur = '右上', 
            la = '左', 
            ra = '右',
            dl = '左下', 
            da = '下', 
            dr = '右下', 
            lr = '左右', 
            ud = '上下',
            x0 = '〇', 
            x1 = '一', 
            x2 = '二', 
            x3 = '三', 
            x4 = '四', 
            x5 = '五', 
            x6 = '六', 
            x7 = '七', 
            x8 = '八', 
            x9 = '九',
        }
 
        function colchar( col ) 
            return ( 'abcdefgh' ):sub( col, col ) 
        end
 
        local color = mw.ustring.gsub( pc, '^.*(%w)(%w).*$', '%2' ) or ''
        local piece = mw.ustring.gsub( pc, '^.*(%w)(%w).*$', '%1' ) or ''
        local alt = colchar( col ) .. row .. ' '
        if colornames[color] and piecenames[piece] then
            alt = alt .. colornames[color] .. ' ' .. piecenames[piece]
        else
            alt = alt .. ( symnames[piece .. color] or piece .. ' ' .. color )
        end
 
        return string.format( '[[File:Chess_%s%st45.svg|%dx%dpx]]', piece, color, size, size, alt, alt )
    end
 
    function letters_row( rev, num_lt, num_rt )
        local td = '<td style="padding: 0; vertical-align: inherit;height:18px;width:' .. size .. 'px;">'
        local legends = 'abcdefgh'
        local l = mw.text.split( rev and legends:reverse() or legends, '' )
        return '<tr style="vertical-align:middle">\n' 
                .. ( num_lt and '<td style="vertical-align: inherit; padding: 0"></td>' or '' )
                .. td
                .. table.concat( l, '</td>' .. td ) 
                .. '</td>'
                .. ( num_rt and '<td style="vertical-align: inherit; padding: 0"></td>' or '' )
                .. '\n</tr>'
    end
    local letters_tp = letters:match( 'both' ) or letters:match( 'top' )
    local letters_bt = letters:match( 'both' ) or letters:match( 'bottom' )
    local numbers_lt = numbers:match( 'both' ) or numbers:match( 'left' )
    local numbers_rt = numbers:match( 'both' ) or numbers:match( 'right' )
    local width = 8 * size + 2
    if ( numbers_lt ) then width = width + 18 end
    if ( numbers_rt ) then width = width + 18 end
 
    local b = ''
    local caption = ''
 
    if ( letters_tp ) then b = b .. letters_row( rev, numbers_lt, numbers_rt ) .. '\n' end
    b = b .. '<tr style="vertical-align:middle">'
    if ( numbers_lt ) then b = b .. '<td style="padding: 0; vertical-align: inherit; width:18px;height:' .. size .. 'px">' .. (rev and 1 or 8) .. '</td>' end
    b = b .. '<td colspan=8 rowspan=8 style="padding: 0; vertical-align: inherit;"><div class="chess-board" style="position:relative;">'
    b = b .. string.format( '[[File:Chessboard480.svg|%dx%dpx]]', 8 * size, 8 * size )
    for trow = 1,8 do
        local row = rev and trow or ( 9 - trow )
        for tcol = 1,8 do
            local col = rev and ( 9 - tcol ) or tcol
            local piece = args[8 * ( 8 - row ) + col + 2] or ''
            if piece:match( '%w%w' ) then
               local img = image_square(piece:match('%w%w'), row, col, size )
               b = b .. string.format(
                   '<div style="position:absolute;z-index:3;top:%dpx;left:%dpx;width:' .. size .. 'px;height:' .. size .. 'px;">%s</div>\n', 
                   ( trow - 1 ) * size, ( tcol - 1 ) * size, img )
            end
        end
    end
    b = b .. '</div></td>'
    if ( numbers_rt ) then b = b .. '<td style="width:18px;height:' .. size ..'px;padding:0">' .. (rev and 1 or 8) .. '</td>' end
    b = b .. '</tr>'
    if ( numbers_lt or numbers_rt ) then
       for trow = 2, 8 do
          local row = rev and trow or ( 9 - trow )
          b = b .. '<tr style="vertical-align:middle">'
          if ( numbers_lt ) then b = b .. '<td style="padding: 0; vertical-align: inherit;height:' .. size .. 'px">' .. row .. '</td>' end
          if ( numbers_rt ) then b = b .. '<td style="padding: 0; vertical-align: inherit;height:' .. size .. 'px">' .. row .. '</td>' end
          b = b .. '</tr>\n'
       end
    end
    if ( letters_bt ) then b = b .. letters_row( rev, numbers_lt, numbers_rt ) .. '\n' end
 
    if footer:match( '^%s*$' )
    then
    else    
        caption = '<div class="thumbcaption">' .. footer .. '</div>\n'
    end
 
    --return '<div class="thumb ' .. align .. '" style="clear:' .. clear .. '; text-align:center;">'
    return '<div class="' .. align .. '" style="clear:' .. clear .. '; text-align:center;">'
        .. header .. '\n<div class="thumbinner" style="width:' .. width .. 'px;">\n' 
        .. '<table cellpadding=0 cellspacing=0 style="background:white; font-size:88%; border:1px #b0b0b0 solid; padding:0; '
        .. 'margin:auto;">\n' .. b .. '\n</table>\n' .. caption .. '</div></div>'
end
 
function convertFenToArgs( fen )
    -- converts FEN notation to 64 entry array of positions, offset by 2
    local res = { ' ', ' ' }
    -- Loop over rows, which are delimited by /
    for srow in string.gmatch( "/" .. fen, "/%w+" ) do
        -- Loop over all letters and numbers in the row
        for piece in srow:gmatch( "%w" ) do
            if piece:match( "%d" ) then -- if a digit
                for k=1,piece do
                    table.insert(res,' ')
                end
            else -- not a digit
                local color = piece:match( '%u' ) and 'l' or 'd'
                piece = piece:lower()
                table.insert( res, piece .. color )
            end
        end
    end
 
    return res
end
 
function convertArgsToFen( args, offset )
    function nullOrWhitespace( s ) return not s or s:match( '^%s*(.-)%s*$' ) == '' end
    function piece( s ) 
        return nullOrWhitespace( s ) and 1
        or s:gsub( '%s*(%a)(%a)%s*', function( a, b ) return b == 'l' and a:upper() or a end )
    end
 
    local res = ''
    offset = offset or 0
    for row = 1, 8 do
        for file = 1, 8 do
            res = res .. piece( args[8*(row - 1) + file + offset] )
        end
        if row < 8 then res = res .. '/' end
    end
    return mw.ustring.gsub(res, '1+', function( s ) return #s end )
end
 
function p.board(frame)
    local args = frame.args
    local pargs = frame:getParent().args
    local size = args.size or pargs.size or '26'
    local reverse = ( args.reverse or pargs.reverse or '' ):lower() == "true"
    local letters = ( args.letters or pargs.letters or 'both' ):lower() 
    local numbers = ( args.numbers or pargs.numbers or 'both' ):lower() 
    local header = args[2] or pargs[2] or ''
    local footer = args[67] or pargs[67] or ''
    local align = ( args[1] or pargs[1] or 'tright' ):lower()
    local clear = args.clear or pargs.clear or ( align:match('tright') and 'right' ) or 'none'
    local fen = args.fen or pargs.fen
 
    size = mw.ustring.match( size, '[%d]+' ) or '26' -- remove px from size
    if (fen) then
        align = args.align or pargs.align or 'tright'
        clear = args.clear or pargs.clear or ( align:match('tright') and 'right' ) or 'none'
        header = args.header or pargs.header or ''
        footer = args.footer or pargs.footer or ''
        return chessboard( convertFenToArgs( fen ), size, reverse, letters, numbers, header, footer, align, clear )
    end
    if args[3] then
        return chessboard(args, size, reverse, letters, numbers, header, footer, align, clear)
    else
        return chessboard(pargs, size, reverse, letters, numbers, header, footer, align, clear)
    end
end
 
function p.fen2ascii(frame)
    -- {{#invoke:Chessboard|fen2ascii|fen=...}}
    local b = convertFenToArgs( frame.args.fen )
    local res = '|=\n'
    local offset = 2
    for row = 1,8 do
        local n = (9 - row)
        res = res .. n .. ' |' .. 
            table.concat(b, '|', 8*(row-1) + 1 + offset, 8*(row-1) + 8 + offset) .. '|=\n'
    end
    res = mw.ustring.gsub( res,'\| \|', '|  |' )
    res = mw.ustring.gsub( res,'\| \|', '|  |' )
    res = res .. '   a  b  c  d  e  f  g  h'
    return res
end
 
function p.ascii2fen( frame )
    -- {{#invoke:Chessboard|ascii2fen|kl| | |....}}
    return convertArgsToFen( frame.args, frame.args.offset or 1 )
end
 
return p