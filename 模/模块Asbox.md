--[[
This module was created by User:CodeHydro (Alexander Zhikun He).
User:Jackmcbarn and User:Mr._Stradivarius provided a great deal of assistance in writting p.main()

p.main() draw heavily from the following version of Template:Asbox of the English Wikipedia, authored primarily by User:Rich_Farmbrough
https://en.wikipedia.org/w/index.php?title=Template:Asbox&oldid=619510287

p.templatepage() is derived from the following revision of Template:Asbox/templatepage, authored primarily by User:MSGJ
https://en.wikipedia.org/w/index.php?title=Template:Asbox/templatepage&oldid=632914791

Both templates had significant contributions from numerous others listed in the revision history tab of their respective pages.
--]]
local WRAPPER_TEMPLATE, args = 'Template:Asbox'
local p, Buffer, stubCats = {
	--Prevents dupli-cats... get it? Maybe not?
	cats = setmetatable({}, {__newindex = function(t, i, v)
		if not rawget(t, i) then
			rawset(t, i, v)
			table.insert(t, i)
		end
	end}),
	--initializes variables required by both p.main and p.templatepage
	init = function(self, frame, page)
		args, page = args or require('Module:Arguments').getArgs(frame, {
			wrappers = WRAPPER_TEMPLATE
		}), page or mw.title.getCurrentTitle()
		--Ensures demo parameter will never affect category() output for articles
		self.demo = self.demo or page.namespace ~= 0 and args.demo
		return args, page
	end
}, require('Module:Buffer')

--[[
Formats category links. Stores them until called with cat.done=true
Takes multiple or single categories in the form of 'cat'
or a table of strings and/or tables containing parts. (See below)
]]
local attention, catTag, catKey = Buffer'需要關注的小作品訊息模板', '[[Category:%s|Category:%s]]', '%s|%s%s'
local function category(cat)
	for _, v in ipairs((tostring(cat) == cat or cat.t) and {cat} or cat) do
		--[[
		If v is a table:
			[1] = full category name; defaults to local attention if blank
			k = Category sort key. Prefix before v.t
			t = page.text or args.tempsort#; appended after k (or in its place if omitted). Required if v is not a string
		Basically the same as v = (v[1] or attention) .. ' | ' .. (v.k or '') .. v.t
		]]
		if v and v ~= true then--reject v = nil, false, or true
			p.cats[catTag:format(tostring(v) == v and
				v
				or (v[1] and Buffer(v[1]) or attention):_in(v.k):_(v.t):_str(2, nil, nil, '|')
			)] = true
		end
	end
	return cat.done and table.concat(p.cats, p.demo and ' | ' or nil) or ''
end

--[[
Makes an ombox warning;
Takes table {ifNot = Boolean, text, {cat. sort key, cat. sort name}}
Will return an empty string instead when ifNot evaluates to true 
]]
local function ombox(v)
	if v.ifNot then return end
	p.ombox = p.ombox or require('Module:Message box').ombox
	category{v[2]}
	return p.ombox{
		type = 'content',
		text = v[1]
	}
end

--[[
Unlike original template, module now takes unlimited cats! This function also performs
most stub category error checks except for the ombox for when main |category= is omitted (See p.template())
]]
local function catStub(page, pageDoc)
	stubCats = {missing = {}, v = {}}
	local code
	for k, _ in pairs(args) do
		--Find category parameters and store the number (main cat = '')
		table.insert(stubCats, string.match(k, '^category(%d*)$'))
	end
	table.sort(stubCats)
	for k, v in ipairs(stubCats) do
		--Get category names and, if called by p.templatepage, the optional sort key
		local tsort, cat = args['tempsort' .. v], mw.ustring.gsub(args['category' .. v], '[^%w%p%s]', '')--remove all hidden unicode chars 
		--Do not place template in main category if |tempsort = 'no'. However, DO place articles of that template in the main category.
		table.insert(stubCats.v,
			 page and (--p.templatepage passes page; p.main does not, i.e. articles are categorized without sort keys.
				v=='' and tsort == 'no'--if true, inserts 'true' in table, which category() will reject
				or tsort and {cat, k = ' ', t = tsort}
				or {cat, k = ' *', t = page.text}--note space in front of sort key
			)
			or cat
		)
		--Check category existance only if on the template page (i.e. stub documentation)
		if page then
			if not mw.title.new('Category:' .. cat).exists then
				code = code or mw.html.create'code':wikitext'|category'
				table.insert(stubCats.missing, tostring(mw.clone(code):wikitext(v)))
			end
			--[[
			Checks non-demo stub template for documentation and flags if doc is present.
			All stub cats names are checked and flagged if it does not match 'Category: [] stub'.
			The main stub cat is exempt from the name check if the stub template has its own doc
			(presumably, this doc would have an explanation as to why the main stub cat is non-conforming).
			]]
			table.insert(stubCats.v, v == '' and not p.demo and pageDoc.exists and
				'含有文件子頁面的小作品訊息模板'
				or not cat:match'小作品$' and {k = 'S', t = page.text}
			)
		end
	end
	--Add category names after loop is completed
	category(stubCats.v)
	return #stubCats.missing > 0 and ombox{
		--Changed, original msg:
		--One or more of the stub categories defined in this template do not seem to exist!
		--Please double-check the parameters {{para|category}}, {{para|category1}} and {{para|category2}}.
		'设定的这些小作品类别不存在：' .. mw.text.listToText(stubCats.missing),
		{k = 'N', t = page.text}
	}
end

--Shows population of categories found by catStub(). Outputs demo values if none
local function population()
	local wikitext, base = {}, '* [[:Category:%s|:Category:%s]]（页面数：%s）\n'
	if not args.category and stubCats[1] ~= false then
		table.insert(stubCats, 1, false)
	end
	for _, v in ipairs(stubCats) do
		table.insert(wikitext, base:format(
			v and args['category' .. v] or '{{{category}}}',
			v and mw.site.stats.pagesInCategory(args['category' .. v], 'all') or 0
		))
	end
	return table.concat(wikitext)
end

--Includes standard stub documention and flags stub templates with bad parameter values.
function p.templatepage(frame, page)
	args, page = p:init(frame, page)
	local tStubDoc = mw.title.new'Template:Stub documentation'
	local pageDoc = page:subPageTitle('doc')
	--Reorganization note: Original Asbox alternates between outputting categories and checking on params |category#=.
	--Rather than checking multiple times and switching tasks, all stub category param operations have been rolled into catStub()
	return Buffer(
		ombox{--Show ombox warnings for missing args.
			ifNot = args.category,
			'未設置<code>|category</code>參數。請加入一個適當的小作品分類。',
			{k = 'C', t = page.text}
		})
		:_(ombox{
			ifNot = args.subject or args.article or args.qualifier,
			'This stub template contains no description! At least one of the parameters <code>|subject</code>, <code>|article</code> or <code>|qualifier</code> must be defined.',
			{k = 'D', t = page.text}
		})
		:_(catStub(page, pageDoc))--catStub() may also return an ombox if there are non-existing categories
		:_(category{
			done = p.demo ~= 'doc',--Outputs categories if not doc demo
			'小作品訊息模板',
			'Exclude in print',
			args.icon and
				'使用圖示參數的小作品訊息模板'
				or args.image and (
					mw.title.new('Media:' .. mw.text.split(args.image, '|')[1]).exists--do nothing if exists. category() will reject true
					or {k = 'B', t = page.text}
				)
				or '沒有圖像的小作品訊息模板',
			args.imagealt and {k = 'I', t = page.text},
		})
		:_((not p.demo or p.demo == 'doc') and--Add standard stub template documentation
			require('Module:Documentation').main{
				content = Buffer(page.text ~= 'Stub' and--This comparison performed in {{Asbox/stubtree}} before it invokes Module:Asbox stubtree
						require('Module:Asbox stubtree').subtree{args = {pagename = page.text}}
					)
					:_in'\n== 關於本模板 ==\n本模板適用':_(args.qualifier):_'的':_(args.subject):_'小作品中':_out''--space
					:_'。其使用了{{[[Template:Asbox|asbox]]}}元模板建立。\n=== 使用方式 ===\n在條目中輸入'
					:_(mw.html.create'code'
						:wikitext('{{', page.text == 'Stub' and 'stub' or page.text, '}}')
					)
					:_'將會自動生成最上方所示的小作品訊息，並將條目自動加入以下頁面分類中'
					:_'：\n'
					:_(population())
					:_(pageDoc.exists and--transclusion of /doc if it exists
						frame:expandTemplate{title = pageDoc.text}
					)
					:_'\n== 通用說明 ==\n'
					:_(frame:expandTemplate{title = tStubDoc.text})
					:_'\n\n'(),
				['link box'] = Buffer'本文档由[[Module:Asbox|Module:Asbox]]自动生成。'
					:_in'通用信息嵌入自[[Template:Stub_documentation|Template:Stub documentation]]。'
						:_(mw.html.create'span'
							:cssText'font-size:smaller;font-style:normal;line-height:130%'
							:node(('([%s 编辑] | [%s 历史])'):format(
								tStubDoc:fullUrl('action=edit', 'relative'),
								tStubDoc:fullUrl('action=history', 'relative')
							))
						)
						:_out()
					:_(page.protectionLevels.edit and page.protectionLevels.edit[1] == 'sysop' and
						"This template is [[WP:PROTECT|fully protected]] and any [[WP:CAT|categories]] should be added to the template's ["
						.. pageDoc:fullUrl('action=edit&preload=Template:Category_interwiki/preload', 'relative')
						.. '| /doc] subpage, which is not protected.'
					)' <br/>'
			}
		)()
end

function p.main(frame, page)
	args, page = p:init(frame, page)
	local output = mw.html.create'table'
		:addClass'metadata plainlinks stub'
		:css{background = 'transparent'}
		:attr{role = 'presentation'}
		:tag'tr'
			:node((args.icon or args.image) and
				mw.html.create'td'
					:wikitext(args.icon or ('[[File:%s|%spx]]'):format(
						args.image or '',
						args.pix or '40x30',
						args.imagealt or '小作品圖示'
					))
			)
			:tag'td'
				:css{['font-size'] = 'smaller'}
				:tag''
				:wikitext(
					Buffer'这是一篇':_(args.qualifier):_(args.qualifier and '的'):_(args.subject)'',--space
					'[[Wikipedia:小作品|小作品]]。你可以-{zh-hant:透過; zh-hans:通过;}-[',
					page:fullUrl('action=edit', 'relative'),
					' 编辑或修订]扩充其内容。'
					)
				:done()
				:node(args.name and
					require'Module:Navbar'._navbar{
						args.name,
						mini = 'yes',
						style = 'position: absolute; right: 15px; display: none;'
					}
				)
				:node(args.note and
					mw.html.create()
						:tag'br':done()
						:tag'span'
							:css{['font-style'] = 'normal', ['font-size'] = 'smaller'}
							:wikitext(args.note)
						:done()
				)
		:allDone()
	--[[
	Stub categories for templates include a sort key (Otherwise all will be indexed under the letter 'T' for 'Template:[] stubs')
	Articles using the template do not need a sort key since they have unique names.
	When p.demo equals 'doc', the demo stub categories will appear as those for a stub template.
	Otherwise, any non-nil p.demo will emulate article space categories (plus any error cats unless set to 'art')
	]]
	if page.namespace == 0 then -- Main namespace
		category'全部小作品'
		catStub()
	elseif p.demo then
		if p.demo ~= 'doc' then catStub() end
		--Unless p.demo is set to 'art', it will also include error categories normally only shown on
		--the template but not in the article. The elseif after namespace == 0 means demo cats will never show in article space.
		p.demodoc = p.demo ~= 'art' and p.templatepage(frame, page)
		output = mw.html.create()
			:node(output)
			:tag'small':wikitext(
				'Demo categories: ',
				(category{done = true}:gsub('(%[%[)(Category:)([^|%]]-)(%|)', '%1%2%3|%2%3%4'):gsub('(%[%[)(Category:)', '%1:%2'))
			):done()
			:wikitext(p.demo == 'doc' and p.demodoc or nil)
	else
		--Checks for valid name; emulates original template's check using {{FULLPAGENAME:{{{name|}}}}}
		local normalizedName = mw.title.new(args.name or '')
		if normalizedName and normalizedName.fullText == page.fullText then
			output = mw.html.create():node(output):wikitext(p.templatepage(frame, page))
		elseif not page.isSubpage and page.namespace == 10 then-- Template namespace and not a subpage
			category{{k = args.name and 'E' or 'W', t = page.text}}
		end
	end
	return output:wikitext(not p.demo and category{done = true} or nil)
end

return p