<includeonly></includeonly><noinclude>{{template doc page viewed directly}}</noinclude>
<!-- EDIT TEMPLATE DOCUMENTATION BELOW THIS LINE -->
{{lua|Module:Footnotes}}
== 用法 ==

<nowiki>{{harvnb|作者姓氏|发表时间}}</nowiki>

;注释
*作者姓氏和发表时间是两个必要参数。（参数“作者姓氏”，亦可以是中文作者、中文编辑、编辑姓氏，暨 author,editor,editor-last）
*若有合著者，则可使用参数二，三，四（用法同参数一），需注意的是最多只能显示3人（见示例5，6），若使用参数四作者则会显示为"（参数一）等作者"（见示例7）。
*紧随其后的参数代表参考用作品的发表时间。
*参数''loc''用于标识所参考的部分在作品中的所在位置。
*参数''p''用来标识所参考的部分在作品中的具体页数（参见示例2）。
*参数''pp''用来标识所参考的部分在作品中的具体页数范围（参见示例3）。
*参数''ref''用于手动设置生成的链接，需要注意的是，若参数''ref''被设置为''none''(参照示例4)，则该模板不会生成超链接。

== 示例 ==

===代码:===

#<nowiki>{{harvnb|Smith|2006|p=25}}</nowiki>
#<nowiki>{{harvnb|Smith|2006|loc=第100章}}</nowiki>
#<nowiki>{{harvnb|Smith|2006|p=25}}</nowiki>
#<nowiki>{{harvnb|Smith|2006|pp=25-26}}</nowiki>
#<nowiki>{{harvnb|Smith|2006|pp=25-26|Ref=none}}</nowiki>
#<nowiki>{{harvnb|Smith|Jones|2006|p=25}}</nowiki>
#<nowiki>{{harvnb|Smith|Jones|Brown|2006|p=25}}</nowiki>
#<nowiki>{{harvnb|Smith|Jones|Brown|Black|2006|p=25}}</nowiki>
#<nowiki>{{harvnb|Smith|2006|loc=ch.100|p=100}}</nowiki>

===效果:===
====引用====
#{{harvnb|Smith|2006|p=25}}
#{{harvnb|Smith|2006|loc=第100章}}
#{{Harvnb|Smith|2006|p=25}}
#{{Harvnb|Smith|2006|pp=25-26}}
#{{Harvnb|Smith|2006|pp=25-26|Ref=none}}
#{{Harvnb|Smith|Jones|2006|p=25}}
#{{Harvnb|Smith|Jones|Brown|2006|p=25}}
#{{Harvnb|Smith|Jones|Brown|Black|2006|p=25}}
#{{Harvnb|Smith|2006|loc=ch. 100|p=100}}

====文献====
* {{cite book
 | last = Smith | first = John
 | date = 2006
 | title = Smith's Book
 | ref= harv
}}

== 注意事项 ==
1、参数“发表时间”必须添加

2、[[中文维基百科]]目前的模板{{tl|cite book}}需要添加<code>|ref=harv</code>或<code>|ref={{tl|harvid|...}}</code>等参数。

== 参见 ==
* {{tl|Harvard citation text}}
* {{tl|Sfn}}
* [[哈佛参考文献格式]]

<includeonly>
{{esoteric}}

<!-- 请在此线以下添加分类 -->
[[Category:引用模板]]

<!-- 请在此线以下添加跨语言链接 -->
[[ko:틀:Harvnb]]
[[no:Mal:Harvnb]]
</includeonly>