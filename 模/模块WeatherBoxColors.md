w = {};
convert = require( 'Module:BaseConvert' );
math_mod = require( 'Module:Math' );

function hex( value )
    return convert.convert( { n = value, base = 16, width = 2, precision = 0 } );
end

function format_line( background, text_color )
    return table.concat( {"background:#", background, ";color:#", text_color, ";text-align:center;"} );
end

function range_pos( value, start, stop )
    if start < stop then
        if value < start then
            return 0;
        elseif value > stop then
            return 1;
        else
            return (value - start) / (stop - start);
        end
    else
        if value < stop then
            return 1;
        elseif value > start then
            return 0;
        else
            return (start - value) / (start - stop);
        end
    end        
end        

function w.color_d( frame )
    local val = math_mod._cleanNumber( frame.args[1] );
    return w._days_color( val );
end
function w.color_pastel( frame )
    local val = math_mod._cleanNumber( frame.args[1] );
    return w._pastel_color( val );
end
function w.color_t( frame )
    local val = math_mod._cleanNumber( frame.args[1] );
    return w._temperature_color( val );
end
function w.color_green( frame )
    local val = math_mod._cleanNumber( frame.args[1] );
    return w._green_color( val );
end
function w.color_s( frame )
    local val = math_mod._cleanNumber( frame.args[1] );
    return w._sunshine_color( val );
end
function w.color_h( frame )
    local val = math_mod._cleanNumber( frame.args[1] );
    return w._humidity_color( val );
end
function w.color_p( frame )
    local val = math_mod._cleanNumber( frame.args[1] );
    return w._precipitation_color( val );
end

function w._days_color( val )
    local item, background, text_color;
    
    if val == nil then
        return format_line( "FFFFFF", "000000" );
    end
   
    item = hex( range_pos( val, 20, 0 )*255 );
    background = item .. item;
    
    item = hex( range_pos( val, 40, 20 )*255 );
    background = background .. item;
            
    if val >= 12 then
        text_color = "FFFFFF";
    else
        text_color = "000000";
    end        
   
    return format_line( background, text_color );
end

function w._green_color( val )
    local item1, item2, background, text_color;
    
    if val == nil then
        return format_line( "FFFFFF", "000000" );
    end
   
    item1 = hex( range_pos( val, 165.6, 0 )*255 );
    item2 = hex( range_pos( val, 300, 165.61 )*207 + 48 );
    background = table.concat( { item1, item2, item1 } );   
    if val >= 200 then
        text_color = "FFFFFF";
    else
        text_color = "000000";
    end        
   
    return format_line( background, text_color );
end

function w._temperature_color( val )
    local item, background, text_color;
    
    if val == nil then
        return format_line( "FFFFFF", "000000" );
    end
   
    if val < 4.5 then
        item = range_pos( val, -42.75, 4.5 )*255;
        background = hex( item );
    else      
        item = range_pos( val, 60, 41.5 )*255;
        background = hex( item );
    end
    
    if val <= 4.5 then
        item = range_pos( val, -42.75, 4.5 )*255;
        background = background .. hex( item );
    else
        item = range_pos( val, 41.5, 4.5 )*255;
        background = background .. hex( item );
    end
            
    if val < -42.78 then
        item = range_pos( val, -90, -42.78 )*255;
        background = background .. hex( item );
    else  
        item = range_pos( val, 23, 4.5 )*255;
        background = background .. hex( item );
    end
    
    if val < -23.3 or val >= 37.8 then
        text_color = "FFFFFF";
    else
        text_color = "000000";
    end
   
    return format_line( background, text_color );
end

function w._precipitation_color( val )
    local item, background, text_color;
    
    if val == nil then
        return format_line( "FFFFFF", "000000" );
    end
   
    item = hex( range_pos( val, 165.6, 0 )*255 );
    background = item .. item;
    
    item = hex( range_pos( val, 300, 165.61 )*207 + 48 );
    background = background .. item;
    
    if val > 90 then
        text_color = "FFFFFF";
    else        
        text_color = "000000";
    end

    return format_line( background, text_color );
end

function w._humidity_color( val )
    local item, background, text_color;
    
    if val == nil then
        return format_line( "FFFFFF", "000000" );
    end
   
    item = hex( range_pos( val, 66.67, 0 )*255 );
    background = item .. item;
    
    item = hex( range_pos( val, 133.33, 66.667 )*255 );
    background = background .. item;
    
    if val >= 40 then
        text_color = "FFFFFF";
    else        
        text_color = "000000";
    end

    return format_line( background, text_color );
end

function w._sunshine_color( val )
    local item, background, text_color;
    
    if val == nil then
        return format_line( "FFFFFF", "000000" );
    end
   
    if val < 90 then
        item = hex( range_pos( val, 0, 90 )*170 );
    elseif val < 180 then
        item = hex( range_pos( val, 90, 180 )*42.5 + 170 );
    else
        item = hex( range_pos( val, 180, 360 )*42.5 + 212.5 );
    end 
    background = item .. item;
    
    if val < 90 then
        item = hex( range_pos( val, 0, 90 )*170 );
    elseif val < 270 then
        item = hex( range_pos( val, 150, 90 )*170 );
    else
        item = hex( range_pos( val, 270, 720 )*255 );
    end 
    background = background .. item;
    
    if val < 80 then
        text_color = "FFFFFF";
    else        
        text_color = "000000";
    end

    return format_line( background, text_color );
end

function w._pastel_color( val )
    local item, background, text_color;
    
    if val == nil then
        return format_line( "FFFFFF", "000000" );
    end

    if val < -15 or val >= 39 then
        text_color = "FFFFFF";
    else        
        text_color = "000000";
    end
    
    if val >= 51 then
        background = 'EE2200';
    else
        val = math_mod._round( (val + 25.5)/3, 0 );
        if val == 1 then
            background = 'BB00CC';         
        elseif val == 2 then
            background = 'CC00EE';
        elseif val == 3 then
            background = 'CC33EE';
        elseif val == 4 then
            background = 'CC55EE';
        elseif val == 5 then
            background = 'DD66EE';
        elseif val == 6 then
            background = 'DD77EE';
        elseif val == 7 then
            background = 'DD99EE';
        elseif val == 8 then
            background = 'DDAAEE';
        elseif val == 9 then
            background = 'DDBBEE';
        elseif val == 10 then
            background = 'EECCFF';
        elseif val == 11 then
            background = 'FFDDFF';
        elseif val == 12 then
            background = 'F1F1F1';
        elseif val == 13 then
            background = 'FFEEBB';
        elseif val == 14 then
            background = 'FFFFCC';
        elseif val == 15 then
            background = 'FFFFBB';
        elseif val == 16 then
            background = 'FFFFAA';
        elseif val == 17 then
            background = 'FFFF88';
        elseif val == 18 then
            background = 'FFCC33';
        elseif val == 19 then
            background = 'FFBB33';
        elseif val == 20 then
            background = 'FF9900';
        elseif val == 21 then
            background = 'FF8844';
        elseif val == 22 then
            background = 'FF6633';
        elseif val == 23 then
            background = 'FF5522';
        elseif val == 24 then
            background = 'FF4422';
        elseif val == 25 then
            background = 'EE4400';
        else
            background = 'AA00AA'
        end
    end  

    return format_line( background, text_color );
end

function w._none_color( val )
    return format_line( "FAFAFA", "000000" );
end

function w.interpret_color_code( code )
    code = code:lower();
    if code == 't' then
        return w._temperature_color;
    elseif code == 'pastel' then
        return w._pastel_color;
    elseif code == 'green' then
        return w._green_color;
    elseif code == 'h' then
        return w._humidity_color;
    elseif code == 's' then
        return w._sunshine_color;
    elseif code == 'p' then
        return w._precipitation_color;
    elseif code == 'd' then
        return w._days_color;
    elseif code == 'none' then
        return w._none_color;
    else
        error( 'Unknown color scheme option' );
    end    
end

return w;