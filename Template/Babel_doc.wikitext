<!-- 在本行下編輯模板說明 -->
<noinclude>{{template doc page viewed directly}}</noinclude>
{{lua|Module:Babel}}
;Babel: 巴别模板，套入展示用戶語言的用戶框
;格式:<code><nowiki>{{Babel|<box1>|<box2>|<box3>...}}</nowiki></code>
:在任意参数中输入感叹号可以把用户框分列，输入<code>-</code>可以用空行隔开用户框。
;可選項目: 在尾處加上：
:*header=（標題文字，預設是[[維基百科:巴別]]）
:*footer=（尾處文字，預設是[[:Category:用户语言|查看用戶語言]]）
:*color=（背景色，預設為透明。）
:*bordercolor=（邊框色，預設是#99b3ff）
:*align=（排列方位，預設是right）
:*nocat=（取消分类，输入true即可生效）

;標準示例
{{Babel|zh|en-2|cat|nocat=true}}
:<code><nowiki>{{Babel|zh|en-2|cat}}</nowiki></code>
{{Clear}}
{{Babel|zh|null|cat|nocat=true}}
:<code><nowiki>{{Babel|zh|null|cat}}</nowiki></code>
:使用<code>null</code>將不會顯示任何用戶框。
{{Clear}}

;進階示例
{{Babel|zh|en-2|cat|header=進階示例|footer=結束|bordercolor=black|color=green|nocat=true}}
:<code><nowiki>{{Babel|zh|en-2|cat|header=進階示例|footer=結束|bordercolor=black|color=green|nocat=true}}</nowiki></code>
:显示效果如右所示。同时，该用户页也会被自动归类到相关的语言及水平分类下（本例未显示分类效果）。
{{Clear}}

;类似功能模板
:*[[Template:Userboxbottom]]
:*[[Template:Userboxtop]]
:*[[Template:Userboxes]]
:*另请参见[[维基百科:巴别]]

<includeonly>{{Sandbox other||<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:巴别模板]]
}}</includeonly>