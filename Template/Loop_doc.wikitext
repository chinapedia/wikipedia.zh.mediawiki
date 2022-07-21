<includeonly><!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{Documentation subpage}}</noinclude>
<!-- 在本行下編輯模板說明 -->
{{Lua|Module:String}}
此模板透過調用[[Module:String|String模塊]]產生重複的字串，重複次數並無限制。

用法：<code><nowiki>{{loop|重複次數|需重複的字串}}</nowiki></code>

如果字符串包含等号，則必须在字串前加上「<code>2=</code>」。例如:
*<nowiki>{{loop|9|2==}}</nowiki>顯示{{loop|9|2==}}（必须有「<code>2=</code>」）

用例：
*<nowiki>{{loop|4|n}}</nowiki>顯示{{loop|4|n}}
*<nowiki>{{loop|25|test}}</nowiki>顯示{{loop|25|test}}
*<nowiki>{{#expr:2{{loop|50|*2}}}}</nowiki>顯示{{#expr:2{{loop|50|*2}}}}
*<nowiki>{{loop|3|{{CURRENTYEAR}}}}</nowiki>顯示{{loop|3|{{CURRENTYEAR}}}}

== 模板數據 ==
{{TemplateDataHeader}}
<templatedata>
{
	"params": {
		"1": {
			"label": "重複次數",
			"description": "字符串需重複的次數",
			"type": "number",
			"required": true
		},
		"2": {
			"label": "字符串",
			"description": "需重複的字符串",
			"type": "string",
			"required": true
		}
	},
	"description": "此模板用於產生重複的字符串",
	"paramOrder": [
		"1",
		"2"
	]
}
</templatedata>

{{字串模板一覽|IRL}}
<includeonly>
[[Category:輔助模板|{{PAGENAME}}]]
</includeonly>