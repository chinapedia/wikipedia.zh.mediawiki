local p={
	replace_data = { 
		"%[%[[Cc][Aa][Tt].-%]%]",
		"%[%[分類.-%]%]",
		"%[%[分类.-%]%]",
		"%[%[[Cc]ategory.-%]%]",
		--"其他例外", --直接新增即可
	},
	nullstr = ''
}
local strings = require( 'Module:String' )

--主函數
function p.main(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	
	--__DISAMBIG__
	other_replace = {}
	to_replace = ''
	rep_type = "category"
	for arg_name, arg_value in pairs( get_args ) do
		if arg_name == 1 or arg_name == '1' then
			--要處理的字串
			to_replace = arg_value
		elseif arg_name == "type" then
			rep_type = mw.ustring.lower(arg_value)
		else
			other_replace[arg_name] = arg_value
		end
	end
	if rep_type == "category" then
		return p.delete_category(to_replace, other_replace)
	elseif rep_type == "link" then
		return p.dellink(get_args)
	elseif rep_type == "list_category" or rep_type == "listcategory" or rep_type == "list category" then
		return p.list_category(get_args)
	else
		return to_replace
	end
end

function p.list_category(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	category_list = p.find_category((get_args[1] or get_args['1']) or '')
	format = mw.ustring.gsub((get_args[2] or get_args['2']) or "*{{{1}}}\n", "%{%{%{.-%}%}%}", "%%s" );
	it = mw.ustring.find(format, "%%s", 1)
	if it == nil then format = format .. "%s" end
	format = mw.ustring.gsub(format, "\\n", "\n")

	body = ''
	for i, category in pairs( category_list ) do
		body = body .. mw.ustring.gsub(format, "%%s", category)
	end
	return body
end
function p.deltitle(input)
	str = mw.text.trim(mw.ustring.gsub(input,"\127\'\"`UNIQ%-%-.-QINU`\"\'\127", p.nullstr))

	begin_, end_ = mw.ustring.find(str, "=+", 1)
	if begin_==nil then return input end
	begin_2 = mw.ustring.find(str, "=+ *\n", end_ + 1)
	count = end_ - begin_ + 1

	title_name = mw.text.trim(mw.ustring.sub(str, end_ + 1, begin_2-1 ))
	result = "\n;<span id=\"" .. title_name .. "\" style=\"font-size:" .. (({24,20,18,16,14})[count] or 14) .. "px;\">" .. title_name .. "</span>"

	if count < 1 then return str 
	elseif count < 3 then result = result .. "\n----" end
	return result .. '\n'
end
function p.dellink(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	input = (get_args[1] or get_args['1']) or ''
	input = mw.ustring.gsub(input,"\127\'\"`UNIQ%-%-ref.-QINU`\"\'\127", p.nullstr)
	body = p.delete_category(input, {})
	get_link = mw.ustring.gmatch( body, "%[%[.-%]%]" )
	i = 1 j = 1 while mw.ustring.find(body, "\n=+ *[^\n]* *=+ *\n") and j do
		if i>=10 then j = nil end
		body = mw.ustring.gsub(body, "\n=+ *[^\n]* *=+ *\n", p.deltitle)
		i = i + 1
	end
	
	catbody = mw.ustring.gsub(input,'<',"<")
	catbody = mw.ustring.gsub(catbody,'>',">")
	category_list = p.find_category(catbody)
	
	link_str = get_link()
	while link_str do
		link_url = mw.ustring.sub(link_str, 3, -3)
		--^$()%.[]*+-?
		link_matcher = mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(link_url, 
			"%%", "%%%%"), "%)", "%)"), "%-", "%-"), "%^", "%^"), "%$", "%$"), "%(", "%("), "%.", "%."), "%*", "%*"), "%+", "%+"), "%|", "%|")
		link_matcher = mw.ustring.gsub(mw.ustring.gsub(link_matcher, "%[", "%[") , "%]", "%]") 
		link_matcher = mw.ustring.gsub(mw.ustring.gsub(link_matcher, "%{", "%{") , "%}", "%}")
		first_split = mw.ustring.find(link_url, "%|", 1) or 0
		get_link_inner = mw.ustring.gsub(mw.ustring.sub(link_url, 1, first_split - 1), "%%", "%%%%")

		body = mw.ustring.gsub( body, "%[%[" .. link_matcher .. "%]%]", get_link_inner );
		link_str = get_link()
	end
	body = mw.text.trim(body) .. '\n'
	
	body = mw.ustring.gsub( body, "[Ii][Ss][Bb][Nn]", "ISBN" );
	body = mw.ustring.gsub( body, "__[A-Z]+__", p.nullstr );
	for i, category in pairs( category_list ) do
		body = body .. category .. " "
	end
	return body
end

function p.delete_category(source_str, other)
	local body = source_str
	for i, categorys in pairs( p.replace_data ) do
		body = mw.ustring.gsub( body, categorys, p.nullstr );	   
	end
	for i, categorys in pairs( other ) do
		body = mw.ustring.gsub( body, categorys, p.nullstr );	   
	end
	--Category:使用ISBN魔術連結的頁面
	body = mw.ustring.gsub( body, "[Ii][Ss][Bb][Nn]", "ISBN" );
	body = mw.text.trim(body) --消除多餘空行
	return body
end

function p.find_category(source_str)
	local body = ''
	input = mw.ustring.gsub(source_str,'<',"<")
	input = mw.ustring.gsub(input,'>',">")
	cat_counting = {}
	for i, category_matcher in pairs( p.replace_data ) do
		get_cat = mw.ustring.gmatch( input, category_matcher )
		cat_str = get_cat()
		while cat_str do
			cat_name_it = mw.ustring.find(cat_str, ':', 1, false)
			first_split = mw.ustring.find(cat_str, "%|", 1) or -2
			
			category = mw.ustring.sub(cat_str, cat_name_it + 1, first_split - 1)
			cat_counting[category] = category
			cat_str = get_cat()
		end
	end
	if mw.ustring.find(body, "[Ii][Ss][Bb][Nn]") then category_list["使用ISBN魔術連結的頁面"] = "使用ISBN魔術連結的頁面" end
	cat_list = {}
	i=1
	for _, category_name in pairs( cat_counting ) do
		cat_list[i] = "Category:" .. category_name

		i = i + 1
	end	
	return cat_list
end

function p.test(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	
	text = mw.ustring.gsub( ((get_args[1] or get_args['1']) or ''), '\n', "\n ")
	
	input = mw.ustring.gsub(text,'<',"<")
	input = mw.ustring.gsub(input,'>',">")

	--return mw.ustring.gsub( input .. "\n*匹配數:", "\127\'\"`UNIQ%-%-ref.-QINU`\"\'\127", p.nullstr );
	input = mw.ustring.gsub( input, "\127\'\"`", p.nullstr );
	return mw.ustring.gsub( input, "`\"\'\127", p.nullstr );
end
function p.get_title(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	for arg_name, arg_value in pairs( get_args ) do
		if arg_name == 1 or arg_name == '1' then
			--要處理的字串
			input = arg_value
		elseif arg_name == "title" or  arg_name == "2" or arg_name == 2 then
			title = arg_value
		elseif arg_name == "keep" or arg_name == "keep_title" or arg_name == "keep title" or
			arg_name == "3" or arg_name == 3 then
				keep_title = mw.ustring.lower(arg_value)
		end
	end
	return p.find_title(input or '', title or '', keep_title)
end
function p.get_chapter(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	input = (get_args[1] or get_args['1']) or ''

	chapter_begin, chapter_end = mw.ustring.find(input, '#', 1)
	if chapter_begin ~= nil then
		return mw.ustring.sub(input, chapter_begin + 1)
	end
	
	return ''
end
function p.find_title(str, title, keep_title)
	if title == nil then return '' end
	if title == '' then return str end
	settion_data_begin, settion_data_end = mw.ustring.find(title, "_[0-9]+$", 1)
	
	find_count = 1
	if settion_data_begin ~= nil then 
		cutted_title = mw.ustring.sub(title, 1, settion_data_begin - 1)
		find_count = tonumber(mw.ustring.sub(title, settion_data_begin + 1, settion_data_end))
	else
		cutted_title = title
	end
	if find_count < 1 then 
		find_count = 1
		cutted_title = title 
	end
	show_t = true
	if keep_title ~= nil then
		if yesno == nil then yesno = require('Module:Yesno') end
		if keep_title == "hide" then show_t = false end
		keep_t = yesno(keep_title)
	else
		keep_t = false
	end
	
	str = '\n'..mw.text.trim(mw.ustring.gsub(str,"\127\'\"`UNIQ%-%-h%-.-QINU`\"\'\127", p.nullstr))

	--^$()%.[]*+-?
	title_matcher = mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(title, 
		"%%", "%%%%"), "%)", "%)"), "%-", "%-"), "%^", "%^"), "%$", "%$"), "%(", "%("), "%.", "%."), "%*", "%*"), "%+", "%+"), "%|", "%|")
	title_matcher = mw.ustring.gsub(mw.ustring.gsub(title_matcher, "%[", "%[") , "%]", "%]") 
	title_matcher = mw.ustring.gsub(mw.ustring.gsub(title_matcher, "%{", "%{") , "%}", "%}")

	cutted_title_matcher = mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(cutted_title, 
		"%%", "%%%%"), "%)", "%)"), "%-", "%-"), "%^", "%^"), "%$", "%$"), "%(", "%("), "%.", "%."), "%*", "%*"), "%+", "%+"), "%|", "%|")
	cutted_title_matcher = mw.ustring.gsub(mw.ustring.gsub(cutted_title_matcher, "%[", "%[") , "%]", "%]") 
	cutted_title_matcher = mw.ustring.gsub(mw.ustring.gsub(cutted_title_matcher, "%{", "%{") , "%}", "%}")

	cutted_title_matcher = "\n=+ *" .. cutted_title_matcher .. " *=+ *\n"
	title_matcher = "\n=+ *" .. title_matcher .. " *=+ *\n"
	
	finded_title_begin, finded_title_end = mw.ustring.find(str, title_matcher, 1)
	if finded_title_begin == nil then
		finded_title_begin, finded_title_end = mw.ustring.find(str, cutted_title_matcher, 1)
		for index = 2, find_count do
			if finded_title_end ~= nil then
				finded_title_begin, finded_title_end = mw.ustring.find(str, cutted_title_matcher, finded_title_end + 1)
			end
		end
	end

	if title == "__FIRST_SECTION__" then finded_title_begin = -1 end
	if finded_title_begin ~= nil then
		if title == "__FIRST_SECTION__" then
			finded_title = ''
			count = 99999
			finded_title_end = 1
		else
			finded_title = mw.ustring.sub(str, finded_title_begin, finded_title_end)
			
			begin_, end_ = mw.ustring.find(finded_title, "=+", 1)
			begin_2, end_2 = mw.ustring.find(finded_title, "=+ *\n", end_ + 1)
			count = end_ - begin_ + 1
			
		end
		next_title_matcher = "\n=+ *[^=\n]* *=+ *\n"
		next_title_find_begin, next_title_find_end = mw.ustring.find(str, next_title_matcher, finded_title_end + 1)
		flag = true while next_title_find_begin and flag do
			next_title_find = mw.ustring.sub(str, next_title_find_begin, next_title_find_end)
			find_begin_, find_end_ = mw.ustring.find(next_title_find, "=+", 1)
			find_count = find_end_ - find_begin_ + 1
			if find_count <= count then 
				next_title_begin = next_title_find_begin
				next_title_end = next_title_find_end
				flag = nil
			end
			next_title_find_begin, next_title_find_end = mw.ustring.find(str, next_title_matcher, next_title_find_end + 1)
		end
		
		--title_name = mw.text.trim(mw.ustring.sub(str, end_ + 1, begin_2-1 ))
		if next_title_begin == nil then next_title_begin = 0 end
		
		body = mw.ustring.sub(str, finded_title_end + 1, next_title_begin - 1)
		i = 1 j = 1 while mw.ustring.find(body, "\n=+ *[^\n]* *=+ *\n") and j do if i>=10 then j = nil end
			body = mw.ustring.gsub(body, "\n=+ *[^\n]* *=+ *\n", p.deltitle)
			i = i + 1
		end

		if show_t then if keep_title then body = finded_title .. body else body = p.deltitle(finded_title) .. body end end
		return  mw.text.trim(body)
	end
	return ''
end

return p