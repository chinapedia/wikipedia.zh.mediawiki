{{documentation subpage}}
<!-- PLEASE ADD CATEGORIES AND INTERWIKIS AT THE BOTTOM OF THIS PAGE -->

这是一个为'''讨论页'''增加「任務清單」列表的模板。该模板本身不含有列出清單具体内容的参数；根据默认设置，实际内容应编写于该页的子页面''/to do'' 。如不存在该子页面，模板将提示列表为空，未经使用的模板将有可能不经提示即被删除。其他具体使用方法见下方[[#用法|用法]]。
*替換引用：{{tl|待辦}}={{tl|todo}}={{tl|To do}}

== 参数 ==
; 基本参数：
<pre>
{{to do
|collapsed=
|for=
|inner=
|list=
|nocats=
|nopreload=
|small=
|target=
}}</pre>

; 元模板参数：
<pre>
{{to do
...
|above=
|below=
|category=
|image=
|inner=
|smallfor= (if the |for= parameter should be displayed when small)
}}</pre>

== 用法 ==
<!-- for the documentation don't subst the result -->
* {{<nowiki/>to do}} — 默认任务列表 
{{to do|nocats=yes}}{{clear}}{{brClear}}

* {{<nowiki/>to do|collapsed=yes}} — 将列表设置为默认合并
{{to do|collapsed=yes}}

* {{<nowiki/>to do|<code>N</code>}} — <tt>N</tt> 是一個1-9的數字，以確定其優先級 (1 代表最高优先级)
{{to do|nocats=yes|9}}{{clear}}{{brClear}}

* {{<nowiki/>to do|inner=列表内容列表内容}} — 使用文字替换默认设置的列表分页（适用于公告）
 {{to do|inner=列表内容列表内容}}{{clear}}{{brClear}}

: '''长内容版本'''：<br>{{<nowiki/>to do|inner=<nowiki><div></nowiki><br><nowiki>
* To Prepare this article for FA status.</nowiki><br><nowiki>
* Addition of pictures and/or photographs to illustrate the relevant topics/sections.</nowiki><br><nowiki></div></nowiki>}}
{{to do|nocats=yes|inner=<div>
* To Prepare this article for FA status.
* Addition of pictures and/or photographs to illustrate the relevant topics/sections.
</div>}}{{clear}}{{brClear}}

* {{<nowiki/>to do|list='''./to do2'''}} — 使用子頁面'''./to do2'''替换默认设置'''./to do'''作为列表分页
{{to do|nocats=yes|list=./to do2}}{{clear}}{{brClear}}

* {{<nowiki/>to do|target=<code>某条目</code>}} — 使用文章「<code>某条目</code>」替换指向的主页面
{{to do|nocats=yes|target=Talk:小甜甜|1}}{{clear}}{{brClear}}

* {{<nowiki/>to do|nocats=yes}} — 不在默认设置的目錄中列出

* {{<nowiki/>to do|nopreload=yes}} — 不自动加載子页面文本

* {{<nowiki/>to do|small=yes}} — 缩小版列表
{{to do|nocats=yes|small=yes}}{{clear}}{{brClear}}

== 另见 ==
* {{tl|task}}
* {{tl|todolist}}
<includeonly>
[[Category:任务列表模板|{{PAGENAME}}]]
[[Category:討論頁模板|{{PAGENAME}}]]

</includeonly>