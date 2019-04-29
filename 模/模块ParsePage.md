--[[

This module is a collection of functions to assist in extracting information
from full Wikipedia pages.

It is not intended to be a full parser, or anything like that, merely a simple
system for grabbing a few relevant details.  These functions are not intended 
to be called directly from templates, but rather these functions would be 
included and referenced in other Lua modules that examine page text.

]]

p = {}

p.getUsers = 
function ( text, sort, unique )    
    sort = sort or false;
    unique = unique or false;
    local user_table = {};
    local search_re, link;
    
    -- Note, mw.ustring.gmatch is relatively slow.  Should switch to 
    -- string once the string.gmatch bug is resolved.
    if not sort then 
        search_re = '()%[%[User:([^/]-)[|%]#]';
        for ind, name in string.gmatch( text, search_re ) do
            link = table.concat( {'[[User:',_name,_'|', name, ']]'} );
            table.insert( user_table, {ind, name, link} );
        end
        search_re = '()%[%[User talk:([^/]-)[|%]#]';
        for ind, name in string.gmatch( text, search_re ) do
            if string.match( name, '^%d-%.%d-%.%d-%.%d-$' ) or string.match( name, '^[%dA-F]-:[%dA-F]-:[%dA-F]-:[%dA-F]-:[%dA-F]-:[%dA-F]$' ) then
                link = table.concat( {'[[Special:Contributions/',_name,_'|', name, ']]'} );
                table.insert( user_table, {ind, name, link} );
            else       
                link = table.concat( {'[[User:',_name,_'|', name, ']]'} );
                table.insert( user_table, {ind, name, link} );
            end            
        end
        table.sort( user_table, p._comp1 );
    else
        search_re = '%[%[User:([^/]-)[|%]#]';
        for name in string.gmatch( text, search_re ) do
            link = table.concat( {'[[User:',_name,_'|', name, ']]'} );
            table.insert( user_table, {0, name, link} );
        end
        search_re = '%[%[User talk:([^/]-)[|%]#]';
        for name in string.gmatch( text, search_re ) do
            if string.match( name, '^%d-%.%d-%.%d-%.%d-$' ) or string.match( name, '^[%dA-F]-:[%dA-F]-:[%dA-F]-:[%dA-F]-:[%dA-F]-:[%dA-F]$' ) then
                link = table.concat( {'[[Special:Contributions/',_name,_'|', name, ']]'} );
                table.insert( user_table, {0, name, link} );
            else       
                link = table.concat( {'[[User:',_name,_'|', name, ']]'} );
                table.insert( user_table, {0, name, link} );
            end            
        end    
        local comp = function( a, b )
            return a[2] < b[2];
        end    
        table.sort( user_table, comp );
    end
           
    if unique then
        user_table = p._makeUniqueTable( user_table, 2, sort );
    end      

    local name_table = {};
    local last;
    for _, v in ipairs( user_table ) do
        if v[2] ~= last then
            table.insert( name_table, {v[2], v[3]} );
        end
        last = v[2];
    end    

    return name_table;
end

p.getSections =
function( text, header_level )
    local head_item = '^' .. string.rep( '=', header_level ) .. '[^=]';
    local head_filter = table.concat( { '^',  string.rep( '=', header_level ),
        '%s*(.*)%s*' .. string.rep( '=', header_level ) } );
    
    local pos, last_pos, total_len;
    local new_table = {};
        
    local line_group = {};
    local headings = { '' };
    
    for line in string.gmatch( text, "\n([^\n]*)" ) do
        if string.match( line, head_item ) then
            table.insert( new_table, table.concat( line_group, "\n" ) );
            table.insert( headings, mw.ustring.match( line, head_filter ) );
            
            line_group = { line };
        else
            table.insert( line_group, line );
        end
    end    
    table.insert( new_table, table.concat( line_group ) );
    
    return new_table, headings;
end

p.getTimestamps = 
function ( text )    
    local time_table = {};
    local lang = mw.getContentLanguage();
    local val;
    
    -- 01:02, 28 February 2013 (UTC)
    for ts in string.gmatch( text, '%d%d:%d%d, %d%d? %w- %d%d%d%d %(UTC%)' ) do
        val = tonumber( lang:formatDate( 'U', ts ) );  
        table.insert( time_table, {ts, val} );
    end
    return time_table;
end

p.formatSectionLink =
function( root, text )
    local frame = mw.getCurrentFrame();
    local link = text;
    
    link = string.gsub( link, '%b<>', '' );
    link = string.gsub( link, '%[%[', '' );
    link = string.gsub( link, '%]%]', '' );
        
    return table.concat( {'[[', root, '#', frame:preprocess( '{{anchorencode:' .. text .. '}}' ), 
        '|' .. link .. ']]' } );    
end

p.formatDateDiff = 
function( date_diff )
    if date_diff < 60*60 then
        return tonumber( math.floor(date_diff/6)/10 ) .. ' minutes';
    elseif date_diff < 60*60*24 then
        return tonumber( math.floor(date_diff/(6*60))/10 ) .. ' hours';
    else
        return tonumber( math.floor(date_diff/(6*60*24))/10 ) .. ' days';
    end
end

p.getExcerpt = 
function( text, length )
    length = length or 200;
    text = '\n' .. text .. '\n';
    text = string.gsub( text, '\n=+[^=]-=+', '\n' ); --headings
    text = string.gsub( text, '%[%[File:[^%]]*%]%]', '' ); --files
    text = string.gsub( text, '%[%[Image:[^%]]*%]%]', '' ); --images
    text = mw.ustring.match( text, '%s*(%S.*%S)%s*' ); --trim
    text = string.gsub( text, '|', "|" ); --table
    text = string.gsub( text, '%b<>', "" ); --tags
    text = string.gsub( text, '{', "{" ); --tags
    text = string.gsub( text, '{', "}" ); --tags
    
    if mw.ustring.len( text ) < length then
        return text;
    else
        return mw.ustring.sub( text, 1, length ) ..
            mw.ustring.match( text, '%S*', length+1 ) .. '...';
    end
end


function p._compKey( a, b, key )
    return a[key] < b[key];
end

function p._comp1( a, b )
    return p._compKey( a, b, 1 );
end

function p._makeUniqueTable( t, key, sort )    
    sort = sort or false;
    local comp;
    
    if key then 
        comp = function( a, b )
            return p._compKey( a, b, key );
        end
    else
        comp = nil;
    end    
    
    if sort then            
        if comp then
            table.sort( t, comp );
        else
            table.sort( t );
        end  
        
        local new_table, last;
        new_table = {};
        
        last = ''

        for k, v in ipairs( t ) do            
            if key then
                if v[key] ~= last then
                    table.insert( new_table, v );
                    last = v[key];
                end
            else
                if v ~= last then
                    table.insert( new_table, v );
                    last = v;
                end
            end
        end
        return new_table;
    else
        local simple_table = {};
        local new_table = {};
        for _, item in ipairs( t ) do  
            if key then
                if not simple_table[item[key]] then
                    table.insert( new_table, item )
                end                
                simple_table[item[key]] = true;
            else
                if not simple_table[item] then
                    table.insert( new_table, item )                    
                end                
                simple_table[item] = true;
            end            
        end
                    
        return new_table;               
    end
end

return p;