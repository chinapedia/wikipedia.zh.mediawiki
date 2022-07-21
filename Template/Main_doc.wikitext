{{NoteTA
|G1=IT
|G2=MediaWiki
}}
{{Documentation subpage}}
{{High-use|34091}}
{{lua|Module:Main}}
<!-- 在本行下編輯模板說明 -->
当[[Wikipedia:什么是条目|维基条目]]很庞大时，它经常会被以[[Wikipedia:摘要格式|摘要格式]]重写。本模板被用在摘要的标题下方，来链接到已经被（或将被）摘要的子条目。

它'''不应当'''被用在条目的顶端来链向它的父主题；取而代之可以在[[WP:序言章節|序言章節]]使用维基链接，并在子条目的讨论页顶端根据需要加上[[Template:Subarticle]]。本模板也'''不用于'''代替内联链接或充当“另见”。它有其特定用途，如上所述。

==用法==
<pre>-{}-
{{Main|条目1}}
</pre>

你也可以引入附加的链接，总数最多为10个。超過10個需使用另一個{{tlx|Main}}。

<pre>-{}-
{{Main
|条目1
|条目2
|条目3
|条目4
|条目5
|条目6
|条目7
|条目8
|条目9
|条目10
}}
</pre>

对于每个链接，你可以选择性地指定一个链接显示名称（<!-- 这是为某些条目设计的， -->一个管道链接将被应用到那些条目）。注意到这些附加参数使用小写的字母<code>[[l]]</code>，例如<code>l1</code>，而'''不是'''<code>11</code>：

<pre>-{}-
{{Main
|条目1
|条目2
|条目3
|条目4
|条目5
|条目6
|条目7
|条目8
|条目9
|条目10
|l1=条目1链接显示名称
|l2=条目2链接显示名称
|l3=条目3链接显示名称
|l4=条目4链接显示名称
|l5=条目5链接显示名称
|l6=条目6链接显示名称
|l7=条目7链接显示名称
|l8=条目8链接显示名称
|l9=条目9链接显示名称
|l10=条目10链接显示名称
}}
</pre>

或者这种形式：

<pre>-{}-
{{Main
|1=主条目1|l1=主条目1显示名称
|2=主条目2|l2=主条目2显示名称
...
|n=主条目n|ln=主条目n显示名称
}}
</pre>

其中<code>n</code>为阿拉伯数字，最大为10。

==范例==
<pre>-{}-
{{Main|条目}}
</pre>

{{Main|条目}}

<pre>-{}-
{{Main|条目1|条目2|条目3}}
</pre>

{{Main|条目1|条目2|条目3}}

<pre>-{}-
{{Main|条目1|条目2|条目3|条目4|条目5}}
</pre>

{{Main|条目1|条目2|条目3|条目4|条目5}}

<pre>-{}-
{{Main|条目|l1=替代标题}}
</pre>

{{Main|条目|l1=替代标题}}

<pre>-{}-
{{Main|条目{{!}}替代标题}}
</pre>

{{Main|条目{{!}}替代标题}}

==重定向==
* {{tlx|主}}
* {{tlx|主条目}}
* {{tlx|Main article}}

==参见==
* 主分類：{{tlx|Maincat}}
* 更详尽的列表：{{tlx|Main list}}
* 参见：{{tlx|See Also}}
* 更多資訊：{{tlx|Further}}
* 此页面分类的主条目是：{{tlx|Catmore}}
* [[Wikipedia:摘要格式]]
* {{Link-en|Wikipedia:長文章布局|Wikipedia:Long article layout}}
* [[m:Help:Template]]
{{Hatnote templates}}

<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:鏈接模板|{{PAGENAME}}]]
[[Category:頁面訊息模板|{{PAGENAME}}]]
[[Category:不顯示於列印版面的模板]]
[[Category:顶注模板]]
}}<templatedata>
{
	"description": "主提示",
	"params": {
		"1": {
			"label": "1",
			"type": "string/wiki-page-name",
			"description": "连接参数，最多可以有13个"
		},
		"l1": {
			"label": "l1",
			"type": "string",
			"description": "连接显示名，与1相等"
		}
	}
}
</templatedata>
</includeonly>