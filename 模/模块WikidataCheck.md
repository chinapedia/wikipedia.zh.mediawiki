local p = {}

function p.wikidatacheck(frame)
    local pframe = frame:getParent()
    local config = frame.args -- the arguments passed BY the template, in the wikitext of the template itself
    local args = pframe.args -- the arguments passed TO the template, in the wikitext that transcludes the template
    
    local property = config.property
    local value = config.value or ""
    local catbase = config.category
    local namespaces = config.namespaces
    local ok = false -- one-way flag to check if we're in a good namespace
    local ns = mw.title.getCurrentTitle().namespace
    for v in mw.text.gsplit( namespaces, ",", true) do
        if tonumber(v) == ns then
            ok = true
        end
    end
    if not ok then -- not in one of the approved namespaces
        return ""
    end
    local entity = mw.wikibase.getEntityObject()
    if not entity then -- no Wikidata item (根本找不到对应的维基数据页)
        return "[[Category:不在維基數據的"_.._catbase_.._"|Category:不在維基數據的" .. catbase .. "]]"
    end
  	if value == "" then
       	return nil -- Using Wikidata (检索维基数据页)
	end
    local claims = entity.claims or {}
    local hasProp = claims[property]
    if not hasProp then -- no claim of that property (在维基数据页的各条信息项都中没有对应的信息)
        return "[[Category:不在維基數據的"_.._catbase_.._"|Category:不在維基數據的" .. catbase .. "]]" -- bad. Bot needs to add the property (这不是好事,但可以由机器人完成对应项的添加)
    end
    for i, v in ipairs(hasProp) do	-- Now we try to iterate over all possible values? (将要检查的模板参数与多条信息记录逐个取值比对)
    	propValue = v.mainsnak.datavalue.value
    	if propValue == value then
        	return "[[Category:與維基數據相同的"_.._catbase_.._"|Category:與維基數據相同的" .. catbase .. "]]" -- yay! (这是好结果,表示调用模板时填写的信息参数和wikidata中填写的信息能对得上号,万事大吉)
    	end
	end
    return "[[Category:與維基數據不同的"_.._catbase_.._"|Category:與維基數據不同的" .. catbase .. "]]" -- needs human review :( (此结果表示虽然wikidata中有对应的信息项,但是与调用模板时填写的参数不匹配,需要人工查证)
end

return p