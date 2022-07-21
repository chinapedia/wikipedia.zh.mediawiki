{{#switch:{{uc:{{{1|}}}}}|G8|RM=<span id="delete-reason" style="display:none">{{urlencode:{{#invoke:Template:Delete|input|parent=|deletelink=}}}}</span>{{#ifeq:{{NAMESPACE}}|MediaWiki|[[Category:快速删除候选]]}}|#default=__NOINDEX__
{{mbox
| type  = speedy
| class = ambox-serious
| image = [[File:Icono archivo borrar.png|40px|]]
| text  =
<div style="text-align: right; font-size: smaller; float: right;">
* [[Special:Whatlinkshere/{{FULLPAGENAME}}|链入]]
* [{{fullurl:{{FULLPAGENAME}}|action=history}} 历史]
* <span class="autotrigger">[{{fullurl:{{FULLPAGENAME}}|diff=0&autotrigger_element={{urlencode:.mw-rollback-link a}}}} 最后]</span>
* {{DeleteLink|comment={{#invoke:Template:Delete|input|parent=|deletelink=}}}}<span id="delete-reason" style="display:none">{{urlencode:{{#invoke:Template:Delete|input|parent=|deletelink=}}}}</span>
</div>
<!--

提示 -->{{Hinth|titleStyle=width:12em;|title=<span style="padding: 1px 3px; color: red;" title="單擊可查看本模板的簡化字母參數">{{#if:{{{1|}}}|管理员注意|出错提示}}!</span>}}
{{#if:{{{1|}}}|请对照以下删除理由判断本页是否具备执行快速删除的理据：|标记者没有提供理由，请对照以下删除说明补上合适的参数：
:<code><nowiki>{{Delete|'''快速删除理由'''}}</nowiki></code>
快速删除的理由可以填寫左邊代碼，模板会自动显示相应的理由：}}
{{#invoke:Template:Delete|reasons}}
{{Hintf}}<!-- 提示结束

-->
<strong>{{#if:{{{bot|}}}|[[User:{{{bot}}}|{{{bot}}}]]认为}}本页可能符合[[Wikipedia:快速刪除#準則|快速删除的標準]]而需删除，理由：</strong>
{{IsFile|{{{1|{{PAGENAME}}}}}|2=
*<strong>{{#invoke:Template:Delete|input|F7|{{{1|{{PAGENAME}}}}}}}</strong>
*<strong>本文件已於[[Commons:|維基共享資源]]提供，链接為：[[Commons:File:{{{1|{{PAGENAME}}}}}|File:{{{1|{{PAGENAME}}}}}]]。</strong><includeonly>{{{cat|{{{cate|{{{category|[[Category:与维基共享资源重复的档案|{{FULLPAGENAME}}]][[Category:快速删除候选|共{{PAGENAME}}]]}}}}}}}}}</includeonly>
|3=
<includeonly>{{#invoke:Template:Delete|input|parent=}}</includeonly>
}}

'''請勿移除本模板'''。如有異議，請在'''本模板下方加入{{tlc|hang on|理由}}'''，並儘快{{edit|1={{TALKPAGENAME}}|2=到讨论页闡明理據|section=new|preloadtitle=删除争议|extendurlquerystring=&preload=Template:Hang_on/preload|4=|5=}}。

<small>{{IsFile|{{{1|{{PAGENAME}}}}}|2=
*請[[Wikipedia:管理员|管理员]]注意将[[Special:Whatlinkshere/{{FULLPAGENAME}}|使用该图像的所有条目]]修改为维基共享资源上的图像，然后才能<span class="autotrigger">[{{fullurl:{{FULLPAGENAME}}|action=delete&autotrigger_element=%23mw-filedelete-submit&wpReason={{urlencode:{{#invoke:Template:Delete|input|F7|{{{1|{{PAGENAME}}}}}|deletelink=}}}}}} 删除]。</span>
*|3=}}'''其他'''編者若認為本頁明顯不符合快速删除的标准，{{#switch:{{#invoke:Template:Delete|input|parent=|reasoncode=}}|G10|O1=|#default=或者您已修正存在的問題，}}可去除此模板。</small>
<div id="speedy-delete" class="template-delete"></div>
}}}}<noinclude>
{{Documentation}}
</noinclude>