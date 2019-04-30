local ilh = {}
local getArgs
local yesno = require('Module:Yesno')

local args
--local frameArgs
local COMMON_TAIL='</span>'
local MODEL={
	 frame_head='<span class="ilh-all %s" data-orig-title="%s" data-lang-code="%s" data-lang-name="%s" data-foreign-title="%s">'
	,frame_tail=COMMON_TAIL
	,page_head='<span class="ilh-page">'
	,page_tail=COMMON_TAIL
	,comment_head='<span class="noprint ilh-comment">（'
	,comment_tail='）'..COMMON_TAIL
	,lang_head='<span class="ilh-lang">'
	,lang_tail=COMMON_TAIL
	,colon='<span class="ilh-colon">：</span>'
	,link_head='<span class="ilh-link">'
	,link_body='-{[[:%s:%s|<span lang="%s" dir="auto">%s</span>]]}-'
	,link_tail=COMMON_TAIL
}
local clazz_pageExist_framehead='ilh-blue'
local TRA_CAT='[[Category:有蓝链却未移除内部链接助手模板的页面|Category:有蓝链却未移除内部链接助手模板的页面]]'

function ilh.main(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	args = getArgs(frame, {parentFirst=true})
	
	return ilh._ilh(arg)
end

function ilh._ilh(arg)
	--frameArgs = getArgs(frame, {frameOnly=true})

	local context={}
	context["isMainPage"]=ilh.isMainPage()
	context["localPage"]=args[1]
	context["foreignPage"]=args[2] or args[1] --如果{{{2}}}不传入的话
	context["displayName"]=ilh.displayName(args)
	context["langCode"]=args["lang-code"]
	context["lang"]=args["lang"]
	context["nocat"]=yesno( args["nocat"] , false )

	context["isExist"]= (args["$exist$"] and args["$exist$"]==1) or ilh.isExist(context["localPage"])
	
	local curPage_obj=mw.title.getCurrentTitle()
	context["isNoCatWithNamespace"]=curPage_obj:inNamespaces(2,828) --User,Module
	--context["curPageNamespace"]=curPage_obj.namespace

	return (context["isMainPage"] and ilh.onlyLink(context)) or ilh.functionLink(context)
end

function ilh.onlyLink(context)
	return ( context["isExist"] and mw.ustring.format( '[[%s|%s]]', context["localPage"], context["displayName"] ) ) or context["displayName"]
end

function ilh.functionLink(context)
	context["_localPage"]=mw.ustring.gsub(context["localPage"],'"','"')
	context["_foreignPage"]=mw.ustring.gsub(context["foreignPage"],'"','"')
	local need_cat=
				   (not context["nocat"])
				   and
				   (not context["isNoCatWithNamespace"])
				   --[[not (
					   context["curPageNamespace"]==2 --User
					or context["curPageNamespace"]==828 --Module
				   )]]
	--mw.log(context["nocat"])
	--mw.log(context["curPageNamespace"])
	--mw.log(need_cat)

	local output_context={}
	table.insert(output_context,
					mw.ustring.format(MODEL.frame_head ,
						 (context["isExist"] and clazz_pageExist_framehead) or ''
						,context["_localPage"]
						,context["langCode"]
						,context["lang"]
						,context["_foreignPage"]
					)
				)
		table.insert(output_context,MODEL.page_head)
			table.insert(output_context,
							mw.ustring.format('[[:%s|%s]]' ,
								context["localPage"],context["displayName"]
							)
						)
		table.insert(output_context,MODEL.page_tail)
		if context["isExist"] then
			if need_cat then
				table.insert(output_context,TRA_CAT)
			end
		else
			table.insert(output_context,MODEL.comment_head)
				table.insert(output_context,MODEL.lang_head)
					table.insert(output_context,context["lang"])
				table.insert(output_context,MODEL.lang_tail)

				table.insert(output_context,MODEL.colon)

				table.insert(output_context,MODEL.link_head)
					table.insert(output_context,
									mw.ustring.format(MODEL.link_body,
										 context["langCode"]
										,(context["foreignPage"] or context["localPage"])
										,context["langCode"]
										,(context["foreignPage"] or context["localPage"])
									)
								)
				table.insert(output_context,MODEL.link_tail)
			table.insert(output_context,MODEL.comment_tail)
		end
	table.insert(output_context,MODEL.frame_tail)

	return table.concat(output_context,"")
end

function ilh.displayName(args)
	local _d=args["d"]
	local _1=args["1"]
	local _3=args["3"]
	local dpN1=_3 or _d
	return (dpN1 and {dpN1} or {_1})[1]
end

--以下需要更高效的实现

--确定主页
--使用mw信息获得主页名
--使用language库获得本站默认语言代码（zh）来确定信息的对应语言，获得全主页名
---因为其他zh分语言只有名，没有命名空间，可以识别出来，但麻烦
--然后判断当前页和主页是否一致
---计划做重定向判断，但没需要
function ilh.isMainPage()
	local mainpage_msgobj=mw.message.new('Mainpage')
	mainpage_msgobj=mainpage_msgobj:inLanguage(mw.getContentLanguage():getCode())
	local mainPage_obj=mw.title.makeTitle(0,mainpage_msgobj:plain())
	local curpage_obj=mw.title.getCurrentTitle()
	--local curpage_redirectFrom_obj=curpage_obj.redirectTarget
	--[[if curpage_redirectFrom_obj ~=false then
		curpage_obj=curpage_redirectFrom_obj
	end]]
	return mw.title.equals(mainPage_obj,curpage_obj) --and curpage_obj.namespace==4
end

--确定页面存在
---exists是高开销方法，需要更高效的实现
--带保护的包装方法
--由于exists和解析器函数ifexist都是高开销方法
--而ifexist达到限制时默认返回结果为false的操作
--而exists会直接抛出错误而中断执行
--所以将相应调用包裹，压制exists的抛错，按照ifexist的理念，返回false
--正常情况下则一切正常
function ilh.isExist(pageName)
	local execStatus,result=pcall(ilh._isExist,pageName)
	
	if execStatus then
		return result
	else
		return false
	end
end
--真实方法
function ilh._isExist(pageName)
	local localPage_obj=mw.title.makeTitle(0,pageName)
	return localPage_obj.exists
end
--end

return ilh