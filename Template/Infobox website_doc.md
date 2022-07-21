{{Documentation subpage}}
<!-- EDIT TEMPLATE DOCUMENTATION AFTER THIS LINE -->
{{Uses Wikidata|P856}}

== 使用 ==
{{Parameter names manual
| name | native_name | native_name_lang  | logo  | logo_size  | logo_alt  | logocaption | screenshot | collapsible | collapsetext | screenshot_size | screenshot_alt | caption | url | commercial | type | registration | language | num_users | content_license | programming_language | owner | author | editor | launch_date | revenue | issn | oclc | current_status | footnotes 
}}

==参数==
{{TemplateData header}}
<templatedata>
{
	"description": "網站介紹的信息框",
	"params": {
		"name": {
			"label": "網站名稱",
			"type": "string",
			"default": "{{PAGENAME}}",
			"description": "網站名稱",
			"aliases": [
				"websitename",
				"company_name"
			]
		},
		"logo": {
			"label": "網站標誌",
			"type": "string",
			"description": "網站標誌",
			"aliases": [
				"websitelogo",
				"company_logo"
			]
		},
		"collapsible": {
			"label": "是否摺疊",
			"type": "string",
			"description": "指定截圖是否摺疊，遇到較長垂直截圖的情況下，可以設定為「yes」，不建議在合理使用的網頁截圖上使用\"collapsible\"參數，詳見Wikipedia:非自由内容使用准则#8"
		},
		"collapsetext": {
			"label": "標題文字",
			"type": "string",
			"default": "截圖",
			"description": "摺疊部分的標題文字"
		},
		"screenshot": {
			"label": "網頁截圖",
			"type": "string",
			"description": "網頁截圖"
		},
		"caption": {
			"label": "截圖說明",
			"type": "string",
			"description": "截圖說明"
		},
		"native_name": {
			"label": "原語言名稱",
			"type": "string",
			"description": "原語言名稱"
		},
		"url": {
			"label": "網址",
			"type": "string",
			"description": "網址，請輸入完整語法。如果留空，会从Wikidata填充。",
			"aliases": [
				"website",
				"homepage"
			]
		},
		"commercial": {
			"label": "商業性質",
			"type": "string",
			"description": "是否為商業性質（請填「是」或「否」）"
		},
		"type": {
			"label": "網站類型",
			"type": "string",
			"description": "網站類型",
			"aliases": [
				"website_type"
			]
		},
		"registration": {
			"label": "需要註冊會員",
			"type": "string",
			"description": "是否需要註冊會員（請填「是」、「否」或「選擇性」）",
			"aliases": [
				"reg"
			]
		},
		"language": {
			"label": "語言",
			"type": "string",
			"description": "語言"
		},
		"content_license": {
			"label": "內容許可",
			"type": "string",
			"description": "內容的版權資訊",
			"aliases": [
				"content_licence",
				"licence",
				"license"
			]
		},
		"owner": {
			"label": "持有者",
			"type": "string",
			"description": "持有者",
			"aliases": [
				"owners"
			]
		},
		"author": {
			"label": "创始人",
			"type": "string",
			"description": "網站的創始人，適用於個人所建立的網站",
			"aliases": [
				"creator",
				"authors",
				"creators"
			]
		},
       "founder": {
			"label": "创立者",
			"type": "string",
			"description": "網站的創辦機構或團體，適用於機構或團體所建立的網站",
			"aliases": [
			]
		},
		"revenue": {
			"label": "收入",
			"type": "string",
			"description": "收入",
			"aliases": [
				"rev"
			]
		},
		"current_status": {
			"label": "現狀",
			"type": "string",
			"description": "現狀，線上、下線、被收購等"
		},
		"location": {
			"label": "總部地點",
			"type": "string",
			"description": "總部地點",
			"aliases": [
				"headquarters"
			]
		},
		"native_name_lang": {
			"label": "原語言名稱語言",
			"description": "原語言名稱語言。若有填寫native_name，該參數必填。",
			"example": "en, ja",
			"type": "string"
		},
		"logo_caption": {
			"aliases": [
				"logocaption"
			],
			"label": "標誌說明",
			"description": "標誌說明",
			"type": "string"
		},
		"logo_size": {
			"label": "標誌大小",
			"description": "標誌大小",
			"example": "150px",
			"type": "string"
		},
		"logo_alt": {
			"label": "標誌替代文字",
			"description": "標誌替代文字。當標誌無法顯示時，替代文字會顯示。",
			"type": "string"
		},
		"screenshot_size": {
			"label": "網頁截圖大小",
			"description": "網頁截圖大小",
			"example": "200px",
			"type": "string"
		},
		"screenshot_alt": {
			"label": "截圖替代文字",
			"description": "截圖替代文字。當截圖無法顯示時，替代文字會顯示。",
			"type": "string"
		},
		"company_type": {
			"label": "公司類型",
			"description": "公司類型",
			"type": "string"
		},
		"language_count": {
			"label": "語言數目",
			"description": "語言數目"
		},
		"language_footnote": {
			"label": "語言脚注",
			"description": "語言脚注",
			"type": "string"
		},
		"traded_as": {
			"label": "股票代號",
			"description": "股票代號"
		},
		"founded": {
			"aliases": [
				"foundation"
			],
			"label": "成立",
			"description": "成立"
		},
		"dissolved": {
			"label": "結束",
			"description": "結束",
			"type": "string"
		},
		"predecessor": {
			"label": "前身",
			"description": "前身",
			"type": "string"
		},
		"successor": {
			"label": "後繼",
			"description": "後繼",
			"type": "string"
		},
		"country_of_origin": {
			"label": "原产地",
			"description": "原产地",
			"type": "string"
		},
		"locations": {
			"label": "營業據點數",
			"description": "營業據點數"
		},
		"area_served": {
			"label": "業務範圍",
			"description": "業務範圍",
			"type": "string"
		},
		"editor": {
			"aliases": [
				"editors"
			],
			"label": "編輯",
			"description": "編輯",
			"type": "string"
		},
		"chairman": {
			"label": "首席",
			"description": "首席",
			"type": "string"
		},
		"chairperson": {
			"label": "董事長",
			"description": "董事長",
			"type": "string"
		},
		"president": {
			"label": "總裁",
			"description": "總裁"
		},
		"CEO": {
			"label": "首席执行官",
			"description": "首席执行官",
			"type": "string"
		},
		"MD": {
			"label": "常務董事",
			"description": "常務董事",
			"type": "string"
		},
		"GM": {
			"label": "總經理",
			"description": "總經理"
		},
		"key_people": {
			"label": "代表人物",
			"description": "代表人物"
		},
		"industry": {
			"label": "产业",
			"description": "产业"
		},
		"products": {
			"label": "产品",
			"description": "产品"
		},
		"services": {
			"label": "服務",
			"description": "服務",
			"type": "string"
		},
		"operating_income": {
			"label": "稅前息前利潤",
			"description": "稅前息前利潤",
			"type": "string"
		},
		"net_income": {
			"label": "净利润",
			"description": "净利润"
		},
		"assets": {
			"label": "总资产",
			"description": "总资产"
		},
		"equity": {
			"label": "总股本",
			"description": "总股本"
		},
		"employees": {
			"aliases": [
				"num_employees"
			],
			"label": "员工",
			"description": "员工"
		},
		"parent": {
			"label": "母公司",
			"description": "母公司"
		},
		"divisions": {
			"label": "部門",
			"description": "部門"
		},
		"subsidiaries": {
			"aliases": [
				"subsid"
			],
			"label": "子公司",
			"description": "子公司"
		},
		"ipv6": {
			"label": "IPv6支持",
			"description": "IPv6支持",
			"example": "是"
		},
		"advertising": {
			"label": "广告",
			"description": "广告"
		},
		"users": {
			"aliases": [
				"num_users"
			],
			"label": "用户",
			"description": "用户"
		},
		"launch_date": {
			"aliases": [
				"date_of_launch",
				"launched"
			],
			"label": "推出時間",
			"description": "推出時間",
			"type": "string",
			"example": "{{start date and age|2000|12|31}}"
		},
		"native_clients": {
			"label": "系统平台",
			"description": "系统平台"
		},
		"programming_language": {
			"label": "編程語言",
			"description": "編程語言"
		},
		"issn": {
			"aliases": [
				"ISSN"
			],
			"label": "国际标准连续出版物号",
			"description": "国际标准连续出版物号"
		},
		"eissn": {
			"aliases": [
				"eISSN"
			],
			"label": "电子国际标准连续出版物号",
			"description": "电子国际标准连续出版物号"
		},
		"oclc": {
			"label": "OCLC号",
			"description": "OCLC号"
		},
		"footnotes": {
			"label": "脚注",
			"description": "脚注",
			"type": "string"
		},
		"location_city": {
			"label": "總部城市",
			"description": "總部城市"
		},
		"location_country": {
			"aliases": [
				"country"
			],
			"label": "總部國家",
			"description": "總部國家"
		},
		"background": {
			"label": "截圖背景顔色",
			"description": "截圖背景顔色"
		}
	},
	"paramOrder": [
		"name",
		"native_name",
		"native_name_lang",
		"logo",
		"logo_size",
		"logo_alt",
		"logo_caption",
		"screenshot",
		"screenshot_size",
		"screenshot_alt",
		"collapsible",
		"collapsetext",
		"background",
		"caption",
		"company_type",
		"type",
		"language",
		"language_count",
		"language_footnote",
		"traded_as",
		"founded",
		"dissolved",
		"predecessor",
		"successor",
		"location",
		"location_city",
		"location_country",
		"country_of_origin",
		"locations",
		"area_served",
		"owner",
		"author",
        "founder",
		"editor",
		"chairman",
		"chairperson",
		"president",
		"CEO",
		"MD",
		"GM",
		"key_people",
		"industry",
		"products",
		"services",
		"revenue",
		"operating_income",
		"net_income",
		"assets",
		"equity",
		"employees",
		"parent",
		"divisions",
		"subsidiaries",
		"url",
		"ipv6",
		"advertising",
		"commercial",
		"registration",
		"users",
		"launch_date",
		"current_status",
		"native_clients",
		"content_license",
		"programming_language",
		"issn",
		"eissn",
		"oclc",
		"footnotes"
	]
}
</templatedata>

== 範例 ==
{{Infobox website
| name                 = 維基百科
| native_name          = Wikipedia
| native_name_lang     = en
| logo                 = [[File:Wikipedia-logo-v2.svg|frameless|150px]]<br />[[File:Wikipedia wordmark.svg|200px|Wikipedia的文字標誌]]
| logo_caption         = [[维基百科标志]]，各种[[文字]]组成的球状符号，大多数为字母[[W]]或Wi的发音。
| screenshot           = Www.wikipedia_screenshot_(2021).png
| screenshot_size      = 250px
| collapsible          = yes
| collapsetext         = 截圖
| caption              = 維基百科多語言入口網站的截圖。
| url                  = [https://www.wikipedia.org/ www.wikipedia.org]
| type                 = [[网络百科全书|網路百科全書]]
| language             = 301種語言
| registration         = 可選（但在編輯受保護的頁面或者上傳圖片等操作时需要登录账户）
| owner                = [[維基媒體基金會]]
| author               = [[吉米·威爾斯]]、[[拉里·桑格]]<ref name="Jonathan Sidener">{{Cite web |title=Everyone's Encyclopedia |url=http://www.utsandiego.com/uniontrib/20041206/news_mz1b6encyclo.html |accessdate=2012年8月3日 |author=Jonathan Sidener |date=2004年12月6日 |publisher=《[[聖地牙哥聯合論壇報]]》（U-T San Diego） |language=en |archiveurl=https://web.archive.org/web/20121004092019/http://www.utsandiego.com/uniontrib/20041206/news_mz1b6encyclo.html |archivedate=2012年10月4日 |deadurl=no}}</ref>
| launch_date          = {{Start_date_and_age|2001|1|15}}
| current_status       = 活跃
| content_license      = {{clear}}
* 條目採用[[创作共用|知识共享 署名-相同方式共享 3.0协议]]
** 大多數內容也同時雙向對應[[GNU自由文档许可证|GNU自由文件授權條款]]的內容
* 多媒體部分則依照不同性質而採用各種授權協議
}}

<pre style="overflow:auto;">
{{Infobox website
| name                 = 維基百科
| native_name          = Wikipedia
| native_name_lang     = en
| logo                 = [[File:Wikipedia-logo-v2.svg|frameless|150px]]<br />[[File:Wikipedia wordmark.svg|200px|Wikipedia的文字標誌]]
| logo_caption         = [[维基百科标志]]，各种[[文字]]组成的球状符号，大多数为字母[[W]]或Wi的发音。
| screenshot           = Www.wikipedia.org_screenshot_2018.png
| screenshot_size      = 250px
| collapsible          = yes
| collapsetext         = 截圖
| caption              = 維基百科多語言入口網站的截圖。
| url                  = [https://www.wikipedia.org/ www.wikipedia.org]
| type                 = [[网络百科全书|網路百科全書]]
| language             = 301種語言
| registration         = 可選（但在編輯受保護的頁面或者上傳圖片等操作时需要登录账户）
| owner                = [[維基媒體基金會]]
| author               = [[吉米·威爾斯]]、[[拉里·桑格]]<ref name="Jonathan Sidener">{{Cite web |title=Everyone's Encyclopedia |url=http://www.utsandiego.com/uniontrib/20041206/news_mz1b6encyclo.html |accessdate=2012年8月3日 |author=Jonathan Sidener |date=2004年12月6日 |publisher=《[[聖地牙哥聯合論壇報]]》（U-T San Diego） |language=en |archiveurl=https://web.archive.org/web/20121004092019/http://www.utsandiego.com/uniontrib/20041206/news_mz1b6encyclo.html |archivedate=2012年10月4日 |deadurl=no}}</ref>
| launch_date          = {{Start_date_and_age|2001|1|15}}
| current_status       = 活跃
| content_license      = {{clear}}
* 條目採用[[创作共用|知识共享 署名-相同方式共享 3.0协议]]
** 大多數內容也同時雙向對應[[GNU自由文档许可证|GNU自由文件授權條款]]的內容
* 多媒體部分則依照不同性質而採用各種授權協議
}}
</pre>

=== 参考文献 ===
{{Reflist}}
{{Clear}}

== 跟踪模板 ==
*{{clc|使用未知Infobox website参数的页面}}
*{{clc|使用冗余Infobox website参数的页面}}——模板输出时只显示一个
*{{clc|在网站信息框没有并用native_name和native_name_lang的页面}}——如果没有并用，native_name不会显示出来

{{Organization infoboxes}}
<includeonly>{{Sandbox other||<!-- 本行下加入模板的分類 -->
[[Category:電腦信息框模板|W]]
[[Category:網站模板| ]]
}}</includeonly>