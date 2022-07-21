local ia_more={}
ia_more.main=function(frame)
    local params=frame.args
    local args=frame:getParent().args
    
    local body=""
    local entry={} 
    
    local head_key={}
    local start_key={}
    local end_key={}
    local noend=params["noend"]
    
    for params_count=1,10 do
        t_head_key=params["head"..params_count]
        t_start_key=params["start"..params_count]
        t_end_key=params["end"..params_count]
        
        if (t_head_key~=nil)then
            table.insert(head_key,t_head_key)
        end
        
        if (t_start_key~=nil)then
            table.insert(start_key,t_start_key)
        end
        
        if (t_end_key~=nil)then
            table.insert(end_key,t_end_key)
        end
    end
    
    local i=1
    while true do--frame的args不是完全table实现，无法用#args查表长，只能死循环试探结束。
        local t_head,t_begin,t_end
        for k,v in ipairs(head_key)do
            t_head=args[v..i] or (t_head or nil)
        end
        for k,v in ipairs(start_key)do
            t_begin=args[v..i] or (t_begin or nil)
        end
        for k,v in ipairs(end_key)do
            t_end=args[v..i] or (t_end or nil)
        end
        if t_end == nil or t_end=='' then
            t_end=noend
        end
        --[[t_head=
        t_begin=((args['播放開始'..i] or args['放送開始'..i]) or args['first'..i])
        t_end=((((args['播放完結'..i] or args['播放結束'..i])or args['放送終了'..i])or args['last'..i])or "播放中")]]
 
        if (t_begin~=nil) then   
            t_item={
                    [1]=t_begin,
                    [2]=t_end,
                    [3]=t_head
                    }
            table.insert(entry,t_item)
            i=i+1
        else
            break
        end 
    end    
    
    for k,v in ipairs(entry) do
        head_v=v[3]
        start_v=v[1]
        end_v=v[2]
        
        if(head_v~=nil)then
            head_v=head_v.."："
        else
            head_v=""
        end
        
        body =body .. head_v ..start_v .. " - " .. end_v .. "<br/>"
    end   
 
    local out=body
 
    return out;
end 
 
return ia_more