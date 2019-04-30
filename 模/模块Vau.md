local p = {}

--[[
使用方法:
{{#invoke:Vau|ref|unit=组合名|distinction=识别号码|link=链接目的地|lang=语言代码|add=追加说明|group=ref标签group名}}

unit - 必须
distinction - 任意（默认值 ''）
link - 任意（默认值 ''）
lang - 任意（默认值 ''）
add - 任意（默认值 ''）
group - 任意（默认值 '成员'）
list - 任意（默认值 ''）
]]
function p.ref(frame)
	-- 获得参数
	local unit = frame.args.unit
	local distinction = frame.args.distinction
	local link = frame.args.link
	local lang = frame.args.lang
	local add = frame.args.add
	local list = frame.args.list
	local ref = {name = '', group = frame.args.group}
	
	-- 创建非脚注部分
	local noref = mw.text.nowiki(unit)
	noref = (link == '') and noref or '[['_.._link_..'|' .. noref .. ']]'
	noref = (lang == '') and noref or '<span lang="' .. lang .. '" xml:lang="' .. lang .. '">-{' .. noref .. '}-</span>'
	
	-- 从组合列表中搜索组合名+识别号码
	local search = (distinction == '') and unit or (unit .. '|' .. distinction)
	search = mw.text.unstripNoWiki(frame:expandTemplate{title = 'Vau/组合列表'}):match('(;%s*' .. search:gsub('%p', '%%p') .. '%s*\n.-:%s*.-)%s*\n[:;={]')
	
	local member = '' -- 成员(ref content)
	local error = true
	if search then
		ref.name, member = search:match('.*;%s*(.-)%s+:%s*(.-)%s*[:;={]?$')
		ref.name = (ref.group == '成员' ) and 'vau-' .. ref.name or 'vau-add-' .. ref.name .. add
		if not member:find('<strong class="error">') then
			-- 当成员不是error时：加粗文章的配音演员，添加add
			local bold = frame:preprocess('{{PAGENAME}}')
			local avoid_suffix = {'的作品', '音乐作品', '音乐作品列表', '音樂作品' , '音樂作品列表'}
			for k, v in ipairs(avoid_suffix) do
				bold = bold:gsub(v, '')
			end
			member = member:gsub('%[%[' .. bold .. '|(.-)]]', '<b>%1</b>'):gsub('%[%[' .. bold .. ']]', '<b>' .. bold .. '</b>') .. add
			error = false
		elseif member:find('请在最后添加号码') then
			-- 当避免成员歧义时：添加可视化编辑器的说明
			local d_code, i = {}, 0
			for value in member:gmatch('<code>|(.-)</code>') do
				i = i + 1
				d_code[i] = value
			end
			member = '<dl class="hlist" style="display:inline;"><dt>' .. unit .. '</dt><dd style="white-space:normal;">' .. member:gsub('</strong>$', '<small>如果使用可视编辑器进行编辑，请在“识别号码”字段指定<code>' .. table.concat(d_code, '</code>、<code>') .. '</code>。</small></strong>') .. '</dd></dl>'
		end
	else
		member = '<strong class="error">Vau定义错误: 组合<code>' .. mw.text.nowiki(unit) .. '</code>未定义。详情请参阅[[Template:Vau#发生错误时|Template:Vau#发生错误时]]。</strong>'
	end
	
	-- 列表形式
	if list ~= '' then
		ref = {name = 'vau-list-' .. list .. '-' .. unit, group = ref.group .. '<span style="display:none;">列表' .. list .. '</span>'}
		member = '<dl style="display:inline; margin-left:0;"><dt style="display:inline;"><dfn>' .. mw.text.nowiki(unit) .. '</dfn></dt><dd style="display:inline; margin-left:0;"><span style="padding:0 0.5em;">-</span>' .. member .. '</dd></dl>'
	end
	-- 输出
	if error then
		if frame:preprocess('{{REVISIONID}}') == '' then
			-- 预览
			return member, '<div class="previewnote nomobile" style="position:absolute; top:-2em; left:0;"><strong class="error" style="background:#fff; margin:0 ' .. (#tostring(mw.title.getCurrentTitle()) * 0.6 + 11.8) .. 'em;">[[Template:Vau|<span style="color:#c00;">Template:Vau</span>]]发生了调用错误</strong></div>'
		else
			-- 阅读
			return '<span class="vau-error">' .. noref .. '</span>', '[[Category:模板参数错误的页面/Template:Vau|Category:模板参数错误的页面/Template:Vau]]'
		end
	else
		return '<span class="vau">' .. noref .. frame:extensionTag('ref', member, ref) .. '</span>'
	end
end

return p