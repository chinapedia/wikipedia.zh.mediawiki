{{NoteTA
|G1 = IT
|G2 = MediaWiki
}}
{{Documentation subpage}}
{{High-use|6308}}
{{Lua|Module:Nihongo}}
{{TOCright}}

本模板提供簡便一致的方式來記述中文、日文及附註事項，並給予日文正確的語言標記（[[Template:Lang#使用理由]]）。

== 使用方法 ==

=== 语法 ===
{| class="wikitable"
! !!输入!!输出
|-
|使用<code>lead=yes</code>参数
||<code><nowiki>{{nihongo|中文|日本漢字/假名|romaji=romaji|第三语言|extra|extra2|lead=yes}}</nowiki></code>
||{{nihongo|中文|日本漢字/假名|romaji=romaji|第三语言|extra|extra2|lead=yes}}
|-
|不使用<code>lead=yes</code>参数
||<code><nowiki>{{nihongo|中文|日本漢字/假名|romaji=romaji|第三语言|extra|extra2}}</nowiki></code>
||{{nihongo|中文|日本漢字/假名|romaji=romaji|第三语言|extra|extra2}}
|}

=== 参数 ===
* <code>|1=</code>（推荐）－中文：填写日文的翻译名称。
* <code>|2=</code>（推荐）－日语汉字/假名：填写日文原文，可能是日本汉字、假名或其他格式。
* <code>|romaji=</code>（可选）－罗马字：填写日文对应的平文式罗马字。適用條目序言，一般僅需記載漢字/假名。
* <code>|lead=</code>（可选）－yes：用于条目导言，填写参数后模板会标记出文字说明。
* <code>|3=</code>（可选）－第三语言：可用于填写主题的第三种语言；如日文名是转写自英文，这里也可填写英文原词。
* <code>|extra=</code>（可选）－extra：填写其他注释。
* <code>|extra2=</code>（可选）－extra2：其他信息

參數3僅供第三語種如英語、德語等使用，請勿用來記載羅馬字。romaji參數應使用在條目序言，或有明顯合理目的时少量使用（例如标示日语发音有助于理解条目）。不要在列舉項目如角色列表，用任何方式標示羅馬字。我們是在寫百科全書，[[Wikipedia:维基百科不是什么|不是語言教學書]]。

請不要在模板內使用[[旁註標記]]語法或模板（如{{tl|ruby}}），這會妨礙其他編者維護內容及檢查錯誤，並且可能在未支援的瀏覽器上呈現ruby編者未預期的糟糕結果。複製一段文字可以很容易了解未支援瀏覽器將如何呈現，{{red|錯誤範例}}：[[Special:diff/30860915/31168834|魍魉之匣]]，第一位人物的結果為『中禪寺 秋彥（中禅寺ちゅうぜんじ 秋彦あきひこ，Chuuzenji Akihiko）』，若使用ruby模板（有設定替代文字）會呈現『中禪寺 秋彥（中禅寺（ちゅうぜんじ） 秋彦（あきひこ），Chuuzenji Akihiko）』之結果。應以[[Special:diff/34458897/34459170|如此方式]]修正。

== 範例 ==

; 條目序言
{| class="wikitable"
|-
! 源码
| <code><nowiki>{{nihongo|'''和歌山縣'''|和歌山県|romaji=Wakayama-ken}}</nowiki></code>
|-
! 显示
| {{nihongo|'''和歌山縣'''|和歌山県|romaji=Wakayama-ken}}
|}

; 使用<code>lead=yes</code>
{| class="wikitable"
|-
! 源码
| <code><nowiki>{{nihongo|'''和歌山縣'''|和歌山県|romaji=Wakayama-ken|lead=yes}}</nowiki></code>
|-
! 显示
| {{nihongo|'''和歌山縣'''|和歌山県|romaji=Wakayama-ken|lead=yes}}
|}

; 一般用法
{| class="wikitable"
|'''原碼''' ||
<code><nowiki>{{nihongo|'''勇者鬥惡龍'''|ドラゴンクエスト|Dragon Quest}}</nowiki></code>
|-
|'''顯示'''||
{{nihongo|'''勇者鬥惡龍'''|ドラゴンクエスト|Dragon Quest}}
|}

; 使用<code>extra</code>参数
{| class="wikitable"
|'''原碼''' ||<code><nowiki>{{nihongo|'''安康天皇'''|安康天皇|romaji=Ank&#x14d; Tenn&#x14d;|extra=约出生於[[401年]]，[[456年]][[8月9日]]被刺杀}}</nowiki></code>
|-
|'''顯示'''||               {{nihongo|'''安康天皇'''|安康天皇|romaji=Ank&#x14d; Tenn&#x14d;|extra=约出生於[[401年]]，[[456年]][[8月9日]]被刺杀}}
|}

; 使用<code>extra2</code>
{| class="wikitable"
|'''原碼''' ||
<code><nowiki>; {{nihongo|拉克絲·克萊因|ラクス・クライン|Lacus Clyne||extra2=聲優：[[田中理惠]]}}</nowiki></code><br />
<code><nowiki>: 拉克絲·克萊因被稱為Z.A.F.T.的歌姬和「粉色的公主」、「白色的皇后」。札夫特議會原議長西蓋爾·克萊因之女。</nowiki></code>
|-
|'''顯示'''||
; {{nihongo|拉克絲·克萊因|ラクス・クライン|Lacus Clyne||extra2=聲優：[[田中理惠]]}}
: 拉克絲·克萊因被稱為Z.A.F.T.的歌姬和「粉色的公主」、「白色的皇后」。札夫特議會原議長西蓋爾·克萊因之女。
|}

; 不使用<code>extra2</code>
{| class="wikitable"
|'''原碼''' ||
<code><nowiki>; {{nihongo|拉克絲·克萊因|ラクス・クライン|Lacus Clyne}}聲優：[[田中理惠]]</nowiki></code><br />
<code><nowiki>: 拉克絲·克萊因被稱為Z.A.F.T.的歌姬和「粉色的公主」、「白色的皇后」。札夫特議會原議長西蓋爾·克萊因之女。</nowiki></code>
|-
|'''顯示'''||
<!--       -->; {{nihongo|拉克絲·克萊因|ラクス・クライン|Lacus Clyne}}聲優：[[田中理惠]]
<!--       -->: 拉克絲·克萊因被稱為Z.A.F.T.的歌姬和「粉色的公主」、「白色的皇后」。札夫特議會原議長西蓋爾·克萊因之女。
|}

; 若要在另外和另外2使用語言標記的話，必須指定extra參數。
{| class="wikitable"
|'''原碼''' ||
<code><nowiki>; {{nihongo|日本國|日本国|romaji=Nippon-koku|extra={{lang|ja|にほんこく}}|extra2={{lang|ja|ニホンコク}}}}</nowiki></code>
|-
|'''顯示'''||
; {{nihongo|日本國|日本国|romaji=Nippon-koku|extra={{lang|ja|にほんこく}}|extra2={{lang|ja|ニホンコク}}}}
|}

; 原始式樣
{| class="wikitable"
|'''原碼''' ||<code><nowiki>{{nihongo|1|2|romaji=romaji|3|4|5}}</nowiki></code>
|-
|'''顯示'''||               {{nihongo|1|2|romaji=romaji|3|4|5}}
|}

== 用戶樣式 ==
登入用戶可以在[[Special:Mypage/common.css|common.css]]加入如下的原始碼以客製化[[Help:用户样式|用戶樣式]]

<syntaxhighlight lang="css">
@media screen, tv {
	*[lang="ja"] {
		color: green;
	}
}</syntaxhighlight>

或是

<syntaxhighlight lang="css">
@media screen, tv {
	.t_nihongo_kanji {
		color: green;
	}
}
</syntaxhighlight>

== 模板数据 ==

<templatedata>
{
	"params": {
		"1": {
			"description": "中文",
			"type": "string",
			"suggested": true
		},
		"2": {
			"description": "日文汉字或日文假名",
			"type": "string",
			"suggested": true
		},
		"3": {
			"description": "除日文以外的外文",
			"type": "string"
		},
		"4": {
			"aliases": [
				"extra"
			],
			"label": "第一个扩展注释",
			"type": "string"
		},
		"5": {
			"aliases": [
				"extra2"
			],
			"label": "第二个扩展注释",
			"type": "string",
			"description": "注释于括号外"
		},
		"romaji": {
			"description": "日文罗马字",
			"type": "string"
		},
		"lead": {
			"example": "yes",
			"type": "boolean",
			"description": "标记为yes时，显示日文和罗马音的语言文字说明"
		}
	},
	"description": "本模板提供简便一致的方式来记述中文、日文及附注事项，并给予日文正确的语言标记。",
	"format": "inline"
}
</templatedata>

== 參見 ==
*{{tl|Nihongo title}}
*{{tl|Japanese}}
*{{tl|Jpn}}
*{{tl|Jp}}，{{tl|Jpn}}和本模板的合成版本
*[[Wikipedia:格式手册 (日本相关条目)]]
*[[維基專題:ACG]]

<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:日語模板|{{PAGENAME}}]]
[[Category:人物模板]]
[[Category:虚构角色模板]]
}}</includeonly>