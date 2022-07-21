<noinclude>{{template doc page viewed directly}}</noinclude>
{{Nosubst}}<includeonly>{{esoteric}}</includeonly>

==用法==
請把所有內文換成以下內容：

<nowiki>{{Copyvio|url=来源url|OldRevision=具有侵权文本的版本号|sign=~~~~|date=提報日期(X月X日)}}</nowiki>

如果有多于一个的来源，可以采用这种形式把所有內文換成以下內容（URL參數'''不能'''以搜尋器結果當參數）：

<pre><nowiki>{{Copyvio
|url=
*http://url1
*http://url2
*http://url3
}}</nowiki></pre>

如果掛上模板時觸發垃圾連結黑名單，請將<code>http</code>換成<code>&amp;#104;ttp</code>，或移除<code>http://</code>。

若頁面已掛上{{tl|Copyvio}}時，表示維基百科已收到（或預計收到）著作權人或其代理人根據[[數位千禧年著作權法]]要求刪除頁面的通知或被發現著作權人或其代理人的作品所使用的著作權授權條款不符合[[Wikipedia:CC BY-SA 3.0协议文本]]規定（包括但不限於''複製到授權條款規定禁止商業利用的內容''、''複製到授權條款規定禁止改做的內容''或''複製到授權條款使用[https://creativecommons.org/licenses/by-sa/4.0/deed.zh_TW CC BY-SA 4.0]的文字內容''），請勿編輯掛有<nowiki>{{Copyvio}}</nowiki>的頁面，以避免觸發[[Special:滥用过滤器/79|79號]][[Wikipedia:防滥用过滤器|防濫用過濾器]]。

本模板支持[[Wikipedia:模板自动参数模式|自动参数]]。使用{{tls|Copyvio/auto|url{{=}}来源}}獲得自動签名的调用，參看[[Wikipedia:模板自动参数模式]]。

模板中的OldRevision用于保证“先前的文本”指向正确的地方，可以省略，省略时“先前的文本”連結至頁面歷史。

本模板會自動將所使用的文章加入'''[[:Category:怀疑侵犯版权页面]]'''分類中。

*模板重定向 {{tl|Copyvio}} = {{tl|侵权}}

== TemplateData ==
{{TemplateDataHeader}}
<templatedata>
{
	"params": {
		"url": {
			"label": "網址",
			"example": "* http://example.com/",
			"required": true,
			"description": "侵權來源網址"
		},
		"OldRevision": {
			"label": "舊版本ID",
			"description": "在張貼侵權模板前的版本ID，設定「原文本」連結的目標舊版本，若不提供則會連結到歷史頁面",
			"example": "12345",
			"type": "number",
			"suggested": true
		},
		"date": {
			"label": "日期",
			"description": "提報侵權的日期，控制Wikipedia:頁面存廢討論/疑似侵權的連結錨點",
			"example": "1月1日",
			"type": "string",
			"suggested": true
		},
		"sign": {
			"label": "簽名",
			"description": "提報者的簽名",
			"required": true
		}
	}
}
</templatedata>

<includeonly>
<!-- 在此线下放置分类-->
[[Category:維基百科維護模板|C]]
</includeonly>