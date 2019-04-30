local fs={}
local getArgs
local KW_LIMIT=5

function fs.linkbuilder(args,url_model,split,url_other,firstword_show,split_show)
    local qw={}
    for i=1,KW_LIMIT do
        local val=args[i]
        val = (i==1 and val==nil) and args["subpagename"] or val
        if val~=nil then
            val=tostring(mw.uri.encode(i==1 and '"'..val..'"' or val))
            if i~=1 then table.insert(qw,split) end
            table.insert(qw,val)
        else
            break
        end
    end
    local url=mw.ustring.format(url_model,table.concat(qw,""))
    url = (url_other~=nil and url..url_other) or url
    
    local shower_url=nil
    if firstword_show == nil then
        local sw={}
        for i=1,KW_LIMIT do
            local val=args[i]
            val = (i==1 and val==nil) and args["subpagename"] or val
            if val~=nil then                
                if i==1 then
                    table.insert(sw,'"'..val..'"')
                else
                    table.insert(sw,split_show)
                    table.insert(sw,val)
                end
            else
                break
            end
        end
        shower_url=table.concat(sw,"")
    else
        shower_url=firstword_show
    end
    return '['..url..' '..shower_url..']'
end

function fs._main(args)
	if args["namespacenum"]==0 then
		return '<span class="error">請勿在條目使用findsources模板！</span>'
	end
    
    local out='来源搜-{zh-cn:索;zh-tw:尋;}-：<span class="plainlinks">'
    --
    ..'-{ '..fs.linkbuilder(args,'//www.google.com/search?&as_eq=wikipedia&q=%s','+',nil,nil,' ')..' }-'..'—'
    --
    ..'Google：'
    ..fs.linkbuilder(args,'//www.google.com/search?q=%s','+',nil,'网页')..'、'
    ..fs.linkbuilder(args,'//www.google.com/search?tbm=nws&as_src=-newswire+-wire+-presswire+-PR+-press+-release+-wikipedia&q=%s','+',args['free']=='yes' and '&as_price=p1' or nil,'新闻')..'、'
    ..fs.linkbuilder(args,'//scholar.google.com/scholar?&q=%s','+',nil,'学术')..'、'    
    ..fs.linkbuilder(args,'//www.google.com/search?tbo=p&tbm=bks&q=%s','+',nil,'图书')..'、'
    ..fs.linkbuilder(args,'//www.google.com/search?tbm=isch&safe=off&q=%s','+',nil,'图片')..'；'
    --
    ..'百度：'
    ..fs.linkbuilder(args,'//www.baidu.com/s?ie=utf-8&wd=%s','+',nil,'网页')..'、'
    ..fs.linkbuilder(args,'http://news.baidu.com/ns?ie=utf-8&cl=2&rn=20&tn=news&word=%s','+',nil,'新闻')..'、'
    ..fs.linkbuilder(args,'http://xueshu.baidu.com/s?ie=utf-8&wd=%s','+',nil,'学术')..'、'
    ..fs.linkbuilder(args,'http://image.baidu.com/i?ie=utf-8&tn=baiduimage&word=%s','+',nil,'图片')..'；'
    --
    ..fs.linkbuilder(args,'http://gongjushu.cnki.net/refbook/basicsearch.aspx?kw=%s','+',nil,'知网工具书')
    --
    ..'</span>'
    ..'<span style="display:none">'
    ..fs.linkbuilder(args,'//abusefilter.invalid/ReportedPage?page=%s','+',nil,'Report')
    ..'</span>'
    
    return out
end

function fs.main(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	local args = getArgs(frame, {parentFirst=true})
	local curPage_obj=mw.title.getCurrentTitle()
	args["subpagename"]= curPage_obj.subpageText
	args["namespacenum"]= curPage_obj.namespace
	
	return fs._main(args)
end

return fs