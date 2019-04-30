w = {};
math_mod = require( "Module:Math" );
wbc = require( "Module:WeatherBoxColors" );  

function checkFlag( flag )
    if flag == nil then
        return nil;
    elseif type( flag ) == 'boolean' then
        return flag;        
    elseif type( flag ) == 'string' then
        flag = flag:lower();
        if flag == '0' or flag == 'false' or
                flag == '' or flag == 'no' or
                flag == 'n' then
            return false;
        else
            return true;
        end
    else
        return error( 'Flag type not valid' );
    end    
end

function w.buildRow( frame )
    local mode = (frame.args.mode or 'basic'):lower();
    local group_name = frame.args.group_name;
    local first_value_string, second_value_string;
    local first_value_number, second_value_number, color_values;
    local color_scheme = frame.args.color_scheme or 't';
    local scale_factor = math_mod._cleanNumber( frame.args.scale_factor) or 1;
    local date_mode = checkFlag( frame.args.date_mode or false );
    local label = frame.args.label or '';
    local annual_mode = (frame.args.annual_mode or 'avg'):lower();
    local include_space = checkFlag( frame.args.include_space or true );
    local second_line = checkFlag( frame.args.second_line ) or false;
    local prefer_cm = checkFlag( frame.args.prefer_cm ) or false;
    local result;

    local pframe = frame:getParent();
    local imperial_first = checkFlag( frame.args['imperial first'] );
    if imperial_first == nil then imperial_first = checkFlag( pframe.args['imperial first'] ); end
        
    local metric_first = checkFlag( frame.args['metric first'] );
    if metric_first == nil then metric_first = checkFlag( pframe.args['metric first'] ); end

    local single_line = checkFlag( frame.args['single line'] );
    if single_line == nil then single_line = checkFlag( pframe.args['single line'] ); end

    if imperial_first == nil and metric_first ~= nil then
        imperial_first = not metric_first;
    else
        imperial_first = true;
    end    

    if mode == 'basic' then
        first_value_string, first_value_number = getInputs( pframe, group_name, 
            nil, include_space );
        second_value_string = nil;
        second_value_number = nil;
    elseif mode == 'temperature' then
        first_value_string, first_value_number = getInputs( pframe, group_name, 
            {'C'}, include_space );
        second_value_string, second_value_number = getInputs( pframe, group_name, 
            {'F'}, include_space );
        first_value_string, first_value_number, second_value_string, second_value_number =
            reconcileTemperature( first_value_string, first_value_number, 
                second_value_string, second_value_number )
    elseif mode == "precipitation" then
        first_value_string, first_value_number, variant = getInputs( pframe, group_name, 
            {'cm', 'mm'}, include_space );
        second_value_string, second_value_number = getInputs( pframe, group_name, 
            {'inch'}, include_space );        
        first_value_string, first_value_number, second_value_string, second_value_number,
            variant =
            reconcilePrecipitation( first_value_string, first_value_number, 
                second_value_string, second_value_number, variant, prefer_cm )
    else
        error( 'Requested mode not recognized' );
    end  
    
    local good = false;
    for i = 1,13 do
        if first_value_string[i] ~= nil and first_value_string[i] ~= '' then
            good = true;
            break;
        end
    end        
    if not good then
        return '';
    end

    if first_value_string[13] == nil or first_value_string[13] == '' then
        first_value_string[13], first_value_number[13] = getAnnualValue( first_value_number, annual_mode );
    end
    if second_value_string ~= nil then
        if second_value_string[13] == nil or second_value_string[13] == '' then
            second_value_string[13], second_value_number[13] = getAnnualValue( second_value_number, annual_mode );
        end
        if mode == 'precipitation' then
            for i = 1,12 do
                if variant[i] ~= 0 then
                    variant[13] = variant[i];
                    break;
                end
            end
        end                        
    end   

    color_scheme = wbc.interpret_color_code( color_scheme );

    color_values = {};
    month_adj = { 31/30, 28/30, 31/30, 1, 31/30, 1, 
        31/30, 31/30, 1, 31/30, 1, 31/30, 12.175 };
    local adj;
    for i = 1,13 do        
        if first_value_number[i] ~= nil and first_value_number[i] ~= -9999 then
            adj = scale_factor;
            if date_mode then 
                adj = adj / month_adj[i];
            end
            if mode == "precipitation" then
                if variant[i] == 1 then
                    adj = adj * 10;
                end
            end
            table.insert( color_values, color_scheme( first_value_number[i] * adj ) );               
        else
            table.insert( color_values, color_scheme( nil ) );
        end
    end
    
    local lang = mw.getContentLanguage();
    for i = 1,13 do
        if first_value_number[i] ~= nil and first_value_number[i] ~= -9999 then
            if math.abs(first_value_number[i]) >= 1000 then
                first_value_string[i] = lang:formatNum( math.abs(first_value_number[i]) );
                if first_value_number[i] < 0 then
                    first_value_string[i] = '−' .. first_value_string[i];
                end
            elseif first_value_number[i] < 0 then
                first_value_string[i] = '−' .. first_value_string[i]:sub(2);
            end
        end
        if second_value_number ~= nil then
            if second_value_number[i] ~= nil and second_value_number[i] ~= -9999 then
                if math.abs(first_value_number[i]) >= 1000 then
                    second_value_string[i] = lang:formatNum( math.abs(second_value_number[i]) );
                    if second_value_number[i] < 0 then
                        second_value_string[i] = '−' .. second_value_string[i];
                    end
                elseif second_value_number[i] < 0 then
                    second_value_string[i] = '−' .. second_value_string[i]:sub(2);
                end
            end
        end
    end              

    if imperial_first and second_value_string ~= nil then
        local t = first_value_string;
        first_value_string = second_value_string;
        second_value_string = t;
    end    

    if not single_line then
        if second_line and second_value_string ~= nil then
            first_value_string = second_value_string;
        end
        second_value_string = nil;
    end

    return makeLine( label, first_value_string, second_value_string, color_values, color_scheme );
end    

function makeLine( label, first_value_string, second_value_string, color_values, color_scheme )
    local result, color_str, value_str;
    
    result = {'|- \n! height="16" | ', label,  "\n"}
    for i = 1,13 do
        color_str = color_values[i];

        if i == 13 then
            table.insert( result, table.concat( {'|style="', color_str, ' border-left-width:medium" | '} ) );
        else
            table.insert( result, table.concat( {'|style="', color_str, '" | '} ) );
        end                

        value_str = first_value_string[i];
        if value_str ~= '' and value_str ~= nil then 
            table.insert( result, value_str );
            if second_value_string ~= nil then
                value_str = second_value_string[i];
                if value_str ~= '' and value_str ~= nil then 
                    table.insert( result, "<br /> (" .. value_str .. ")" );
                end    
            end
        else
            table.insert( result, '—' );
        end        
    
        table.insert( result, "\n" ); 
    end
    
    return table.concat( result );
end  

function getInputs( frame, group_name, suffix, include_space )
    local month_names = { 'Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',
        'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec', 'year' };
    local str, str2, val;
    
    local output_string = {};
    local output_value = {};
    local variant = {};
    if suffix == nil then
        for _, mon in ipairs( month_names ) do
            if include_space then
                str = ( frame.args[ mon .. ' ' .. group_name ] or '' );
            else
                str = ( frame.args[ mon .. group_name ] or '' );
            end                
            val, str2 = math_mod._cleanNumber( str );
            if val ~= nil then 
                table.insert( output_string, str2 );
                table.insert( output_value, val );
            else
                table.insert( output_string, str );
                table.insert( output_value, -9999 );
            end                
        end
    else
        local updated = false;
        for _, mon in ipairs( month_names ) do
            updated = false;
            for i, suf in ipairs( suffix ) do
                if include_space then
                    str = frame.args[ mon .. ' ' .. group_name .. ' ' .. suf ];
                else
                    str = frame.args[ mon .. group_name .. ' ' .. suf ];
                end                    
                if str ~= nil and str ~= '' then 
                    val, str2 = math_mod._cleanNumber( str );
                    if val ~= nil then 
                        table.insert( output_string, str2 );
                        table.insert( output_value, val );
                    else
                        table.insert( output_string, str );
                        table.insert( output_value, -9999 );
                    end                
                    table.insert( variant, i );
                    updated = true;
                    break;
                end                
            end
            if not updated then
                table.insert( output_string, '' );
                table.insert( output_value, -9999 );
                table.insert( variant, 0 );
            end            
        end
    end
        
    return output_string, output_value, variant;
end

function getAnnualValue( values, mode )
    local total = 0;
    local val = 0;
    
    if mode == 'avg' or mode == 'sum' then
        local p1, p2;
        p1 = 0;
        for i = 1, 12 do
            val = values[i];
            if val == -9999 then
                return '', -9999;
            end            
            
            p2 = math_mod._precision( val );
            if p2 > p1 then
                p1 = p2;
            end
            
            total = total + val;
        end
        if mode == 'avg' then
            total = math_mod._round( total / 12, p1 + 1 );
        end
        return tostring( total ), total;
    elseif mode == 'min' then
        local min_val = nil;
        for i = 1, 12 do
            val = values[i];
            if val ~= -9999 then
                if min_val == nil or val < min_val then
                    min_val = val;
                end                
            end            
        end
        return tostring( min_val ), min_val;
    elseif mode == 'max' then
        local max_val = nil;
        for i = 1, 12 do
            val = values[i];
            if val ~= -9999 then
                if max_val == nil or val > max_val then
                    max_val = val;
                end                
            end            
        end
        return tostring(max_val), max_val;
    else
        error( 'Unrecognized Annual Mode' );
    end
end        

function reconcileTemperature( C_degree_strings, C_degree_values, F_degree_strings, F_degree_values )
    local p;
    for i = 1,13 do
        if C_degree_strings[i] == '' then
            if F_degree_values[i] ~= -9999 then
                p = math.max( 0, math_mod._precision( F_degree_strings[i] ) );
                C_degree_values[i] = math_mod._round( (F_degree_values[i] - 32)*5/9, p );
                C_degree_strings[i] = tostring( C_degree_values[i] );
            end            
        elseif F_degree_strings[i] == '' then
            if C_degree_values[i] ~= -9999 then
                p = math.max( 0, math_mod._precision( C_degree_strings[i] ) );
                F_degree_values[i] = math_mod._round( C_degree_values[i]*9/5 + 32, p );
                F_degree_strings[i] = tostring( F_degree_values[i] );
            end                        
        end        
    end
    return C_degree_strings, C_degree_values, F_degree_strings, F_degree_values;
end    

function reconcilePrecipitation( M_degree_strings, M_degree_values, 
        I_degree_strings, I_degree_values, variant, prefer_cm )
    local p;
    
    local v_class = 0;
    for i = 1,13 do
        if variant[i] == 1 then
            v_class = 1;
        elseif variant[i] == 2 then
            v_class = 2;
        end
    end
    if v_class == 0 then
        if prefer_cm then
            v_class = 1;
        else
            v_class = 2;
        end        
    end
    for i = 1,13 do
        if M_degree_strings[i] == '' then
            if I_degree_values[i] ~= -9999 then
                if v_class == 1 then 
                    p = math.max( 0, math_mod._precision( I_degree_strings[i] ) );
                    M_degree_values[i] = math_mod._round( I_degree_values[i]*2.54, p );
                    variant[i] = v_class;
                else 
                    p = math.max( 0, math_mod._precision( I_degree_strings[i] ) ) - 1;
                    M_degree_values[i] = math_mod._round( I_degree_values[i]*25.4, p );
                    variant[i] = v_class;
                end                
                M_degree_strings[i] = tostring( M_degree_values[i] );
            end            
        elseif I_degree_strings[i] == '' then
            if M_degree_values[i] ~= -9999 then
                if variant[i] == 1 then
                    p = math.max( 0, math_mod._precision( M_degree_strings[i] ) ) + 1;
                    I_degree_values[i] = M_degree_values[i]/2.54;
                else
                    p = math.max( 0, math_mod._precision( M_degree_strings[i] ) ) + 2;
                    I_degree_values[i] = M_degree_values[i]/25.4;
                end                    
                I_degree_values[i] = math_mod._round( I_degree_values[i], p );
                I_degree_strings[i] = tostring( I_degree_values[i] );
            end                        
        end  
    end
    return M_degree_strings, M_degree_values, I_degree_strings, I_degree_values, variant;
end    

return w;