-- Simple Module that passes all arguments in the parent frame to a specified template
pa = {};

function pa.run( frame )
    local template = frame.args.template or frame.args[1];
    local pframe = frame:getParent();
    local exclude = frame.args.exclude or '';
    local exclude_list = {};
    for val in string.gmatch( exclude, '[^,]*' ) do
        table.insert( exclude_list, val );
    end
    
    local result;
    args = {};
    for k,v in pairs( pframe.args ) do
        local good = true;
        for _, v2 in ipairs( exclude_list ) do
            if k == v2 then
                good = false;
            end
        end
        if good then
            args[k] = v;
        end        
    end
    
    result = frame:expandTemplate( { title=template, args = args } );
    
    return result;
end

function pa.list( frame )
    local template = frame.args.template or frame.args[1];
    local pframe = frame:getParent();
    local exclude = frame.args.exclude or '';
    local exclude_list = {};
    for val in string.gmatch( exclude, '[^,]*' ) do
        table.insert( exclude_list, val );
    end
    
    local result;
    args = {};
    for k,v in pairs( pframe.args ) do
        local good = true;
        for _, v2 in ipairs( exclude_list ) do
            if k == v2 then
                good = false;
            end
        end
        if good then
            table.insert( args, k .. '=' .. v );
        end        
    end
    
    result = '{{ ' .. template .. ' | ' .. table.concat( args, ' | ' ) .. ' }}';
    
    return result;
end

return pa