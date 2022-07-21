require('Module:No globals')

local p = {}

-- key is beginning of arg name. value is table with namespace number and link
-- alternatively, a function taking the namespace number and returning a validity
-- can be used
local namespaceCategories = {
	all = { function() return true end },
	main = { 0, '[[Wikipedia:条目|条目]]' },
	help = { 12, '[[wp:帮助页面|帮助]]' },
	portal = { 100, '[[wp:主题|主题]]' },
	talk = { function(n) return n > 0 and n%2 == 1 end, '[[Help:使用讨论页|讨论]]' },
	template = { 10, '[[wp:模板空间|模板]]' },
	wikipedia = { 4, '[[wp:名字空间#计划名字空间|维基百科計畫頁面]]' },
	category = { 14, '[[wp:分类|分类]]' },
	user = { 2, '[[wp:用户页|-{zh-cn:用户;zh-tw:使用者;}-]]' },
}

-- Don't convert blank category to nil
local function valueFunc(key, val)
	if type(val) == 'string' then
		val = val:match('^%s*(.-)%s*$')
		if val == '' and key ~= 'category' and key ~= 'embed' then
			return nil
		end
	end
	return val
end

local function getPrettyName(args)
	for k in pairs(namespaceCategories) do
		if args[k .. ' category'] then
			return  "'''[[:Category:"_.._args[k_.._'_category']_.._"|" .. args.name .. "]]'''："
		end
	end
	return "'''" .. args.name .. "'''："
end

function p.core(frame, args)
	if not args then
		args = require('Module:Arguments').getArgs(frame, {wrappers = 'Template:Redirect template/core', valueFunc = valueFunc})
	end
	local namespace = mw.title.getCurrentTitle().namespace
	local otherCategory = args['other category'] and (args.category or string.format('[[Category:%s|Category:%s]]', args['other category']))
	local embedPossible = args.embed == nil or args.embed == 'yes'

	--- XXX: this is a HORRIBLE HACK. kill it with fire as soon as https://bugzilla.wikimedia.org/show_bug.cgi?id=12974 is fixed
	local beCompatibleWithBug12974 = args.info and (args.info:find('^[:;#*]', 1) == 1 or args.info:find('{|', 1, true) == 1) and '\n' or ''
	
	local retval = string.format('*%s这是%s%s重-{zh-cn:定;zh-tw:新導;}-向。%s%s\n',
		embedPossible and args.name and getPrettyName(args) or '',
		args.from and ( ( args.to and '由' or '') .. args.from .. (args.to and '' or '的' ) ) or '',
		args.to and ( ( args.from and '，' or '') .. '指向'   .. args.to .. '的') or '',
		args.info and beCompatibleWithBug12974 or '',
		args.info or ''
	)
	for k,v in pairs(namespaceCategories) do
		if args[k .. ' category'] then
			if type(v[1]) == 'function' and v[1](namespace) or v[1] == namespace then
				retval = retval .. (args.category or string.format('[[Category:%s|Category:%s]]', args[k .. ' category']))
			elseif args['other category'] then
				retval = retval .. otherCategory
			else
				retval = retval .. frame:expandTemplate{title = '不正确的重-{zh-cn:定;zh-tw:新導;}-向模板', args = {v[2]}}
			end
		end
	end
	return retval
end

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {wrappers = 'Template:Redirect template', valueFunc = valueFunc})
	local retval = p.core(frame, args)
	if mw.title.getCurrentTitle().namespace == 0 then
		if args.printworthy == 'yes' then
			return retval .. (args.category or '[[Category:值得列印的重定向|Category:值得列印的重定向]]')
		elseif args.printworthy == 'no' then
			return retval .. (args.category or '[[Category:不需列印的重定向|Category:不需列印的重定向]]')
		end
	end
	return retval
end

return p