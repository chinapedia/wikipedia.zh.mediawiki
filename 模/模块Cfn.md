--based on [[en:Module:Footnotes|en:Module:Footnotes]]

f = {
    args_default = {
        page = "",
        location = "",
        year = "",
        month = "",
        day = "",
        vol = "",
        ref = "",
        group = "",
        ref = "",
        P1 = "",
        P2 = "",
        P3 = "",
        P4 = "",
        url = "",
    }
};

function trim( str )
    if str == nil then
        return nil;
    end
    return str:match( "^%s*(.-)%s*$");
end    

function core( args )
    local result;
 
    if args.P4 ~= "" then
        result = args.P1 .. '等作者';
    elseif args.P3 ~= "" then
        result = args.P1 .. '，' .. args.P2 .. ' & ' .. args.P3;
    elseif args.P2 ~= "" then
        result = args.P1 .. ' & ' .. args.P2
    else
        result = args.P1;
    end
    
    if args.year ~= "" then
        result = result .. '（' .. args.year .. '年';
        if args.month ~= "" then
            result = result .. args.month .. '月';
            if args.day ~= "" then
                result = result .. args.day .. '日'
            end
        end
        result = result .. '）'
    end
 
    if args.ref ~= 'none' then
        if args.ref ~= "" then
            result = "[[#"_.._args.ref_.._"|" .. result .. "]]";
        else
            result = "[[#CITEREF" .. args.P1 .. args.P2 .. args.P3 .. args.P4 .. args.vol .. 
                args.year .. args.month .. args.day .. "|" .. result .. "]]";
        end
    end
 
     if args.vol ~= "" then
        result = result .. '，' .. args.vol;
    end
 
    if args.page ~= "" then
    	if args.url ~= "" then
    		result = result .. '，' .. '[' .. args.url .. ' ' ..  '第' .. args.page .. '页' .. ']';
    	else
    		result = result .. '，' .. '第' .. args.page .. '页';
    	end
    end      
 
    if args.location ~= "" then
        result = result .. "，" .. args.location;
    end
 
    return result;
end
 
function f.cfn( frame )
    local args = f.args_default;
    pframe = frame:getParent();
 
    args.page = pframe.args.p or pframe.args.pp or "";
    args.location = pframe.args.loc or "";
    args.year = pframe.args.y or "";
    args.month = pframe.args.m or "";
    args.day= pframe.args.d or "";
    args.ref = pframe.args.ref or pframe.args.Ref or "";
    args.group = pframe.args.group or pframe.args.g or "";
    args.vol = pframe.args.v or pframe.args.vol or pframe.args.volume or "";
    args.P1 = trim( pframe.args[1] ) or "";
    args.P2 = trim( pframe.args[2] ) or "";
    args.P3 = trim( pframe.args[3] ) or "";
    args.P4 = trim( pframe.args[4] ) or "";
    args.url = pframe.args.url or pframe.args.u or "";
 
    local result = core( args );
    local name = "FOOTNOTE" .. args.P1 .. args.P2 ..  args.P3 .. args.P4 .. args.vol .. 
        args.year .. args.month .. args.day .. args.page .. args.location;
 
    result = frame:extensionTag{ name = "ref", args = {name=name, group=args.group}, content=result };
 
    return result;
end
 
return f;