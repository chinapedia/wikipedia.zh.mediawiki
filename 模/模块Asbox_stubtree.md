local i = {}

function i.exists(pagename)
    local t = mw.title.new(pagename, "Template")
    return t.exists
end

function i.pcase(word)
   return mw.ustring.upper(mw.ustring.sub(word,1,1)) .. mw.ustring.sub(word,2)
end

function i._subtree(pagename)
    local finalresult
    local out = {"",pagename}
    local tt
    local temppage
    local temppageexists
    local r = 0
    local t = {}
    local removeditem1 = ""
    local removeditem2 = ""
    
    -- split items on dash into table
    for token in mw.ustring.gmatch(pagename, "[^-]+") do
        -- don't add numbered items to list
        if tonumber(mw.ustring.sub(token,1,1)) == nil then
            table.insert(t,token)
        else
            r = 1
        end
    end
    table.remove(t, #t)

    while (#t > 1) do
        if r == 1 then
            r = 0
        else
            -- Remove 1st item from list
            removeditem1 = t[1]
            table.remove(t, 1)
        end

        temppage = table.concat(t, "-") .. "-stub"
        temppageexists = i.exists(temppage)
        if temppageexists == true then
            table.insert(out,"[[Template:"_.._temppage_.._"|" .. i.pcase(temppage) .. "]]")
        else
            -- If template with first item does not exist, try removing last item
            removeditem2 = t[#t]
            table.remove(t, #t)
            temppage = removeditem1 .. "-" .. table.concat(t, "-") .. "-stub"
            if #t == 0 then
                temppage = removeditem1 .. "-stub"
            end
            temppageexists = i.exists(temppage)
            if temppageexists == true then
                -- if exists then add first item back to list
                table.insert(t,1,removeditem1)
                table.insert(out,"[[Template:"_.._temppage_.._"|" .. i.pcase(temppage) .. "]]")
            else
                -- if exists then add last item back to list
                table.insert(t,removeditem2)
            end
        end
    end

    finalresult = '<div style="float:right; border-style:dotted; border-width:2px; padding:5px; margin:5px;">'
    finalresult = finalresult .. '<span title="顯示本小作品訊息模板與其他相關模板的從屬關係。" style="font-size:125%; font-weight:bold;">相關小作品類別從屬關係</span>'
    finalresult = finalresult .. table.concat(out, "\n* ")
    finalresult = finalresult .. '\n* [[Template:Stub|Stub]]'
    finalresult = finalresult .. '\n</div>'
    return finalresult
end

function i.subtree(frame)
    return i._subtree(frame.args["pagename"])
end

return i