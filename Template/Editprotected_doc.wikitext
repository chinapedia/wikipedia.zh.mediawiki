{{Documentation subpage}}<includeonly>
{{Bot use warning|bot=[[User:A2093064-bot]]}}</includeonly>
{{Template shortcut|EP}}
==使用方法==
這個[[Wikipedia:模板消息|模板]]將會把頁面加入[[:Category:維基百科編輯被保護頁面請求]]。請注意這個模板是一個<includeonly>[[Category:自我提及模板]]</includeonly>[[Wikipedia:避免自我提及|自我提及]]，是維基百科計劃的一部份，而不是百科全書內容。

{{tl|Editprotected}}應該在[[Wikipedia:討論頁|討論頁]]中輸入。請盡量清楚並具體地述說請求的內容，包含了修改的理由。有可能的話也請提供語法。當應回絕一些受爭議的請求，譬如不符合維基百科方針和／或社群共識的編輯。

禁止把本模板用於主頁面未受保護的討論頁（具有[[WP:COI|利益衝突]]的編輯者請改用{{tl|Request edit}}並等侯[[WP:NPOV|中立]]的編輯者回覆），如主頁面的保護狀態：{{int:restriction-edit}}{{int:colon-separator}}{{int:protect-default}}{{int:restriction-move}}{{int:colon-separator}}{{int:protect-default}}。

受請求的頁面將會被分類到[[:分類:維基百科編輯被保護頁面請求]]。管理員將會檢查這個分類並處理編輯請求。

如果完成，可將{{tl|Editprotected}}改為<nowiki>{{Editprotected|ok=1|sign=--~~~~}}</nowiki>，如果拒绝，可将{{tl|Editprotected}}改成<nowiki>{{Editprotected|no=1|sign=--~~~~}}</nowiki>，頁面都會歸類到[[:分類:已處理的維基百科編輯被保護頁面請求]]。

== 高级方法 ==
在本模板后面添加patch参数，将可以把您想要修改的页面存储至一个临时页面内，您可以进行您想要的修改，并将临时页面名填入patch参数以供管理员检查。

==模板数据==
{{TemplateDataHeader}}
<templatedata>
{
	"params": {
		"ok": {
			"description": "請求已處理",
			"example": "1",
			"type": "unknown",
			"autovalue": ""
		},
		"sign": {
			"description": "簽名"
		},
		"no": {
			"description": "請求已拒絕",
			"example": "1",
			"autovalue": ""
		},
		"patch": {
			"description": "修改範例",
			"suggested": true,
			"example": "Draft:頁面名"
		},
		"conflict": {}
	},
	"description": "編輯請求",
	"paramOrder": [
		"ok",
		"no",
		"sign",
		"patch",
		"conflict"
	]
}
</templatedata>
<includeonly>
[[Category:討論頁模板]]
[[Category:請求模板]]
</includeonly>