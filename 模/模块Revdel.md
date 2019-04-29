local rv = {}
function rv.main(frame)
    local args=frame:getParent().args
    local ids = {}
    local article=args["article"]
    local set=args["set"]
    local reason=args["reason"]
    local status=args["status"]
    local statustext=args["statustext"]
    local review=args["review"]

    local i=1
    while true do--frame的args不是完全table实现，无法用#args查表长，只能死循环试探结束。
        t_id=args['id'..i]
        if (t_id~=nil) then         
            table.insert(ids,t_id)
            i=i+1
        else
            break
        end 
    end    
    local code=""
    code=code..'<div class="plainlinks" id="'..article..'">'.."\n"
 
    if(article==nil)then
        article="条目名"
    end
 
    code=code.."* [["..article.."|"..article.."]]"
            .."（["..tostring(mw.uri.fullUrl(article,"action=edit")).." 編輯]"
            .." · [["..tostring(mw.title.makeTitle("",article).talkPageTitle).."|討論]]"
            .." · ["..tostring(mw.uri.fullUrl("Special:Whatlinkshere/"..article,"limit=999")).." 鏈入]"
            .." · ["..tostring(mw.uri.fullUrl(article,"action=history&hilight="..table.concat(ids,","))).." 歷史]"
            .." · ["..tostring(mw.uri.fullUrl(article,"action=watch")).." 監視]"
            .." · ["..tostring(mw.uri.fullUrl("Special:Log","page="..mw.uri.encode(article,"PATH"))).." 日志]）".."\n"
    code=code.."** "..frame:expandTemplate{title="donestatus",args={frame:callParserFunction{name="#if",args={status,status,"处理中"} },statustext,review=review} }.."\n"
 
    local ids_t={}
    for i=1,#ids do
        table.insert(ids_t,"ids["..ids[i].."]=1")
    end
    code=code.."** 请求删除版本（["..tostring(mw.uri.fullUrl(article,"action=revisiondelete&type=revision&"..table.concat(ids_t,"&"))).." 全部删除]）"
    for i=1,#ids do
        code=code..frame:expandTemplate{title="ar-rev",args={article,ids[i]} }
    end
    code=code.."\n"
 
    code=code.."** 刪除內容："..((set~=nil and set)or frame:expandTemplate{title="red",args={"'''请提供所要刪除的內容（編輯內容/編輯者/編輯摘要，可選多於一個）'''"} }).."\n"
             .."** 理由："..((reason~=nil and frame:expandTemplate{title="revdel/core",args={reason} })or frame:expandTemplate{title="red",args={"'''请提供理由'''"} }).."\n"
             .."</div>".."\n"
 
    return code
end
 
return rv