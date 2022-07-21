<includeonly><!-- protection template here --></includeonly><noinclude>{{template doc page viewed directly}}</noinclude>
<!-- 請在此線底下編輯模板的說明文件 -->

可以用本模板产生没有编辑按钮的标题。

产生没有编辑按钮的标题的另一方法是使用&lt;h<var>x</var>&gt;HTML标签，其中<var>x</var>为1至6的数字。区别在于：使用此模板的段落的编辑按钮被隐藏（但被识别为一个可编辑的段落），而使用HTML标签的段落在编辑时视为上一段落的一部分。

== 用法 ==
产生二级标题：
 '''&#123;&#123;{{PAGENAME}}|== 标题名称 ==&#125;&#125;'''
产生三级标题：
 '''&#123;&#123;{{PAGENAME}}|=== 标题名称 ===&#125;&#125;'''
管道符“|”后面的参数同正常标题的wiktext语法一致。

对于不需要编辑首段（导论）的页面，可在用不带参数的本模板。

若要全頁都不要编辑按鈕，請改用魔術字「 '''<code><nowiki>__NOEDITSECTION__</nowiki></code>''' 」。
;原始碼：:
<pre>-{}-
====示例：正常====
<h4>示例：h4</h4>
'''<big>示例：大号字</big>'''
{{NoEdit|====示例：NoEdit====}}
</pre>
;結果：:
====示例：正常====
<h4>示例：h4</h4>
'''<big>示例：大号字</big>'''
{{NoEdit|====示例：NoEdit====}}
'''请注意，如果是可视化编辑的话，需要将字段名称设为空值，然后里面输入<code>===内容===</code>。'''

== 備註 ==
本模板只针对标题本身设置不出现编辑按钮，如果想对一大段文字的所有标题都设定不出现编辑按钮，可以使用 '''{{tl|noEditH}} {{tl|noEditF}}''' 模板对。

==參見==
*[[Template:NoNewSection]]
<includeonly>

[[Category:辅助模板]]
</includeonly>