<noinclude>{{Documentation subpage}}</noinclude><includeonly>{{Tsh|D|db|Speedy}}
{{Bot use warning|bot=[[User:Jimmy-bot]]、[[User:A2093064-bot]]}}</includeonly>
{{esoteric}}
{{Twinkle standard installation}}
{{lua|Module:Template:Delete|Module:Template:Delete/data}}

== 说明 ==
本模板用来对符合[[Wikipedia:快速刪除的標準|快速刪除標準]]的页面打上删除标记，以便管理员根据删除守则决定是否将其快速删除。

本模板必须用参数1描述被速删的理由，这些理由必须是快速删除标准里所列举的。如果没有填写该参数，最终的模板会在右上角提示出错，单击出错提示会给出相应的详细帮助。

== 用法 ==
:<code>&#123;{Delete|'''快速删除理由'''}&#125;</code>
其中'''快速删除理由'''參數填寫處理描述，也可以用[[Wikipedia:快速刪除|快速刪除標準]]的简化符号。
例如<code><nowiki>{{Delete|G1}}</nowiki></code>顯示為
{{Delete|G1|cat=}}
另外還可以用<code>c1</code>到<code>c10</code>參數附加訊息，這不會列入自動產生的刪除理由，例如<code><nowiki>{{Delete|G1|c1=G1附加訊息}}</nowiki></code>顯示為
{{Delete|G1|c1=G1附加訊息|cat=}}
複合用法：<code><nowiki>{{Delete|G1|c1=*G1附加訊息|c2=**G1的第二個附加訊息|3=G2|c3=*G2附加訊息}}</nowiki></code>顯示為
{{Delete|G1|c1=*G1附加訊息|c2=**G1的第二個附加訊息|3=G2|c3=*G2附加訊息|cat=}}

'''根据[[WP:SD]]操作指引，仍要在页面创建者的用户讨论页添加「{{tls|db-notice|target=页面名称}}--~~<noinclude></noinclude>~~」提醒。'''

=== CSS 及 Javascript 頁面 ===
{{main|Template:Special_wikitext/doc#特殊頁面放置方法}}
{{Special wikitext/放置方法|1=<nowiki>{{Delete|O1}}</nowiki>|2=如用戶欲請求刪除其位於 User: 命名空間的[[CSS]]、[[JavaScript]]或[[JSON]]頁面（名稱以'''.css'''、'''.js'''或'''.json'''結尾），可使用以下格式
|JSON=JSON頁面<br/><span style="font-size:0.7em;">（名稱以'''.json'''結尾）</span>
|JavaScript=JavaScript頁面<br/><span style="font-size:0.7em;">（名稱以'''.js'''結尾）</span>
|CSS=CSS頁面<br/><span style="font-size:0.7em;">（名稱以'''.css'''結尾）</span>
|Lua=Module:名字空間的頁面
}}

== 不允許非管理員使用G8準則提刪 ==
根據[[Wikipedia:快速删除方针#G8|快速刪除方針G8準則]]：
: 解封使用者後刪除使用者頁面：作為解封程序的一部分，應直接予以刪除。
: 因使用者奪取而刪除：作為重命名使用者程序的一部分，應直接予以刪除。
: 刪除無用的MediaWiki頁面：由於技術限制，不適宜進行提刪，應直接予以刪除。
: 因移動請求而刪除頁面、以覆寫刪除重新導向：根據[[Wikipedia:移動請求]]，應以移動請求程序處理，而非以速刪程序處理。
由於以上原因，(1) 該準則所涵蓋的所有刪除皆不需要非管理員提刪，(2) 該準則僅作為刪除摘要使用而非實務上的提刪準則，再加上 (3) 不少使用者混淆移動請求程序與G8速刪準則，或 (4) 濫用速刪程序來誘使管理員處理無關速刪的問題，故不允許非管理員使用G8準則提刪。

==模板數據==
{{templatedataheader}}
{{HideH|templatedata}}
<templatedata>
{
	"params": {
		"1": {
			"description": "刪除理由",
			"example": "G1",
			"required": true,
			"type": "string",
			"suggestedvalues": [
				"G1", "G2", "G3", "G10", "G11", "G12", "G13", "G14", "G15", "G16", "G17",
				"A1", "A2", "A3", "A5", "A6",
				"R2", "R3", "R5", "R6", "R7", "R8",
				"F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8", "F9", "F10",
				"O1", "O3", "O4", "O7", "O8"
			]
		},
		"2": {
			"description": "刪除理由",
			"example": "G1",
			"type": "string",
			"suggestedvalues": [
				"G1", "G2", "G3", "G10", "G11", "G12", "G13", "G14", "G15", "G16", "G17",
				"A1", "A2", "A3", "A5", "A6",
				"R2", "R3", "R5", "R6", "R7", "R8",
				"F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8", "F9", "F10",
				"O1", "O3", "O4", "O7", "O8"
			]
		},
		"3": {
			"description": "刪除理由",
			"example": "G1",
			"type": "string",
			"suggestedvalues": [
				"G1", "G2", "G3", "G10", "G11", "G12", "G13", "G14", "G15", "G16", "G17",
				"A1", "A2", "A3", "A5", "A6",
				"R2", "R3", "R5", "R6", "R7", "R8",
				"F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8", "F9", "F10",
				"O1", "O3", "O4", "O7", "O8"
			]
		},
		"4": {
			"description": "刪除理由",
			"example": "G1",
			"type": "string",
			"suggestedvalues": [
				"G1", "G2", "G3", "G10", "G11", "G12", "G13", "G14", "G15", "G16", "G17",
				"A1", "A2", "A3", "A5", "A6",
				"R2", "R3", "R5", "R6", "R7", "R8",
				"F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8", "F9", "F10",
				"O1", "O3", "O4", "O7", "O8"
			]
		},
		"5": {
			"description": "刪除理由",
			"example": "G1",
			"type": "string",
			"suggestedvalues": [
				"G1", "G2", "G3", "G10", "G11", "G12", "G13", "G14", "G15", "G16", "G17",
				"A1", "A2", "A3", "A5", "A6",
				"R2", "R3", "R5", "R6", "R7", "R8",
				"F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8", "F9", "F10",
				"O1", "O3", "O4", "O7", "O8"
			]
		},
		"6": {
			"description": "刪除理由",
			"example": "G1",
			"type": "string",
			"suggestedvalues": [
				"G1", "G2", "G3", "G10", "G11", "G12", "G13", "G14", "G15", "G16", "G17",
				"A1", "A2", "A3", "A5", "A6",
				"R2", "R3", "R5", "R6", "R7", "R8",
				"F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8", "F9", "F10",
				"O1", "O3", "O4", "O7", "O8"
			]
		},
		"7": {
			"description": "刪除理由",
			"example": "G1",
			"type": "string",
			"suggestedvalues": [
				"G1", "G2", "G3", "G10", "G11", "G12", "G13", "G14", "G15", "G16", "G17",
				"A1", "A2", "A3", "A5", "A6",
				"R2", "R3", "R5", "R6", "R7", "R8",
				"F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8", "F9", "F10",
				"O1", "O3", "O4", "O7", "O8"
			]
		},
		"8": {
			"description": "刪除理由",
			"example": "G1",
			"type": "string",
			"suggestedvalues": [
				"G1", "G2", "G3", "G10", "G11", "G12", "G13", "G14", "G15", "G16", "G17",
				"A1", "A2", "A3", "A5", "A6",
				"R2", "R3", "R5", "R6", "R7", "R8",
				"F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8", "F9", "F10",
				"O1", "O3", "O4", "O7", "O8"
			]
		},
		"9": {
			"description": "刪除理由",
			"example": "G1",
			"type": "string",
			"suggestedvalues": [
				"G1", "G2", "G3", "G10", "G11", "G12", "G13", "G14", "G15", "G16", "G17",
				"A1", "A2", "A3", "A5", "A6",
				"R2", "R3", "R5", "R6", "R7", "R8",
				"F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8", "F9", "F10",
				"O1", "O3", "O4", "O7", "O8"
			]
		},
		"10": {
			"description": "刪除理由",
			"example": "G1",
			"type": "string",
			"suggestedvalues": [
				"G1", "G2", "G3", "G10", "G11", "G12", "G13", "G14", "G15", "G16", "G17",
				"A1", "A2", "A3", "A5", "A6",
				"R2", "R3", "R5", "R6", "R7", "R8",
				"F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8", "F9", "F10",
				"O1", "O3", "O4", "O7", "O8"
			]
		},
		"c1": {
			"description": "針對第1個理由的附加訊息",
			"example": "因為...所以符合G1",
			"type": "string"
		},
		"c2": {
			"description": "針對第2個理由的附加訊息",
			"example": "因為...所以符合G1",
			"type": "string"
		},
		"c3": {
			"description": "針對第3個理由的附加訊息",
			"example": "因為...所以符合G1",
			"type": "string"
		},
		"c4": {
			"description": "針對第4個理由的附加訊息",
			"example": "因為...所以符合G1",
			"type": "string"
		},
		"c5": {
			"description": "針對第5個理由的附加訊息",
			"example": "因為...所以符合G1",
			"type": "string"
		},
		"c6": {
			"description": "針對第6個理由的附加訊息",
			"example": "因為...所以符合G1",
			"type": "string"
		},
		"c7": {
			"description": "針對第7個理由的附加訊息",
			"example": "因為...所以符合G1",
			"type": "string"
		},
		"c8": {
			"description": "針對第8個理由的附加訊息",
			"example": "因為...所以符合G1",
			"type": "string"
		},
		"c9": {
			"description": "針對第9個理由的附加訊息",
			"example": "因為...所以符合G1",
			"type": "string"
		},
		"c10": {
			"description": "針對第10個理由的附加訊息",
			"example": "因為...所以符合G1",
			"type": "string"
		}
	},
	"description": "本模板用来对符合快速刪除標準的页面打上删除标记，以便管理员根据删除守则决定是否将其快速删除。",
	"paramOrder": [
		"1",
		"c1",
		"2",
		"c2",
		"3",
		"c3",
		"4",
		"c4",
		"5",
		"c5",
		"6",
		"c6",
		"7",
		"c7",
		"8",
		"c8",
		"9",
		"c9",
		"10",
		"c10"
	]
}
</templatedata>
{{HideF}}

== 參见 ==
* [[Wikipedia:快速刪除]]
* [[:Category:快速删除候选]]
* [[Special:Log/delete]] - 刪除日誌
* 模板重定向 {{tl|Delete}} = {{tl|D}} = {{tl|速删}}
* 快速刪除通知 {{tl|Db-notice}}
<includeonly>
<!-- 請在此線底下增加分類 -->
[[Category:快速刪除模板]]
</includeonly>