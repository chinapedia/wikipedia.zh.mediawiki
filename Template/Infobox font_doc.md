<noinclude>{{template doc page viewed directly}}</noinclude>
<!-- 在本行之下编辑此模板说明 -->
{{缺乏使用说明}}
<includeonly>{{esoteric}}</includeonly>
使用<code>'''{{tl|Infobox font}}'''</code>可將[[:Category:信息框模板|信息框]]加入[[字體]]條目中。

== 使用方式 ==
{|
|<pre>{{Infobox font
| name             = 
| familyname       = 
| image            = [[File:{{{name}}} specimen.svg|220px|{{{name}}}]]
| image_size       = 
| alt              = 
| style            = 
| classifications  = 
| creator          = 
| commissioned_by  = 
| foundry          = 
| foundries        = 
| trademark        = 
| creationdate     = 
| releasedate      = 
| characters       = 
| glyphs           = 
| license          = 
| based_on         =
| variations       = 
| aka              = 
| metrically_compatible_with = 
| sample           = File:{{{name}}} sample.svg
| shown_here       =
| sample_fullimage = File:{{{name}}} full sample.svg
| website          = {{url|www.example.com}}
| latest_release_version = 
| latest_release_date    = 
| arabic           = 
| cyrillic         = 
| devangari        = 
| greek            = 
| hebrew           = 
| ipa              = 
| latin            = 
}}</pre>
|}

=== 欄位變數 ===
==== 必填 ====
;name: 字體的名稱。如有必要，可加入格式變體（例如：粗體、斜體、窄體等）。
;style: 字體的樣式：有襯線、無襯線、哥德式字體（Blackletter）、書法、符號等
==== 選填 ====
非必須填寫，但建議填寫能使模板更為詳實。
;familyname: 字體所屬的家族名稱，例如 '''Arial Black''' 就屬於 [[Arial]] 家族的字體。
;classifications: 更精確的樣式定義，例如現代、手寫或幾何（Geometric）
;image: 字體名稱的圖片，以該字體表示。這和下列的「'''sample'''」欄位不同。推薦使用 [[SVG]] 格式的圖片。
;imagesize: 显示图片的宽度（默认为300px）。
;based_on: 字體設計的參考對象。與複製的字體不同，若是不同的稱呼請使用「aka」欄位。
;creationdate: 字體創建的年份或日期。<br />请使用 <code><nowiki>{{release date and age|YYYY|MM|DD}}</nowiki></code> 标注日期。
;releasedate: 字體首次發行的年份，與創建日期不同。<br />请使用 <code><nowiki>{{release date and age|YYYY|MM|DD}}</nowiki></code> 标注日期。
;creator: 字體設計 / 創造者的姓名，若無法得知，可留空並填寫字體發行公司（foundry）欄位。
;commissioned_by: 原始委託創建字形的團體機構或個人名稱。
;foundry: 字體的原始發行者和版權持有者（公司）。
;foundries: 以不同形態（例如數位字體）重新發行字體的公司名稱。
;glyphs: 字体内的[[字形]]数量（即字体内含有多少不同的形态），若无便提供大致数量。
;characters: 字体内的[[字符_(计算机科学)|字符]]数量（即多少可正常输出的字），若不是[[Unicode]]则请注明字符编码系统。
;license: 该字体发布使用的[[授權 (法律)|许可]]，如 “[[SIL开源字体授权|OFL]]”，“[[知识共享许可协议|CC0]]”，或者“[[专有软件|专有字体]]”
;trademark: 字體名稱的擁有者或字體名稱持有者的註冊商標。
;variations: 列出其他字体发行商的其他变体名称，如“[[Garamond]]”，“Adobe Garamond”和“ITC Garamond”虽然是不同名称，但是都基于相同的字体设计。
;aka: 其他相似或参考该字体的其他字体，例如Swiss 721是[[Bitstream]]旗下所发布的类[[Helvetica]]字体。
;sample: 字體的範例，以單一的大型字元（g）作為顯示，以及一組字元（A-Z、a-z、0-9）。推薦使用 [[SVG]] 格式。
;shown here: 信息框中所展示的样本字体的名称。
;sample_fullimage: 字體的大型範例圖片，展示完整的字元組。推薦使用 [[SVG]] 格式。
;website: 字体的网页链接（如有）。<br />请使用 <code><nowiki>{{URL|http://www.example.com}}</nowiki></code> 标注网址。
;latest_release_version: 该字体的最新发布版本编号。
;latest_release_date: 该字体最新发布版的日期。<br />请使用 <code><nowiki>{{release date and age|YYYY|MM|DD}}</nowiki></code> 标注日期。

=== 字符覆盖范围 ===
;arabic: 如果该字体含有[[阿拉伯字母]]，则设为''yes''。
;cyrillic: 如果该字体含有[[西里尔字母]]，则设为''yes''。
;devangari: 如果该字体含有[[天城文#字母|天城文字母]]，则设为''yes''。
;greek: 如果该字体含有[[希腊字母]]，则设为''yes''。
;hebrew: 如果该字体含有[[希伯来字母]]，则设为''yes''。
;ipa: 如果该字体含有[[国际音标]]字符，则设为''yes''。
;latin: 如果该字体含有[[拉丁字母]]，则设为''yes''。
;emoji: <!-- Set the emoji-Version number 4, 5, or 11 ???-->''目前待议。''


== 範例 ==
=== 一般語法 ===
{{Infobox font
| name    = Bookman
| image   = [[File:Bookman font.svg|220px|Bookman]]
| style   = [[有襯線體]]
| classifications = [[Slab serif]]
| date    = 1860年
| creator = [[Alexander Phemister]]
| foundry = [[國際字體公司|ITC]]
| sample  = [[File:Bookman_sample.svg|220px|Bookman 範例文字]]
| sample_fullimage = Bookman.png
}}

<div style="width:50%;">
<pre><nowiki>{{Infobox font
| name    = Bookman
| image   = [[File:Bookman font.svg|220px|Bookman]]
| style   = [[襯線體]]
| classifications = [[粗襯線體]]
| date    = 1860年
| creator = [[Alexander Phemister]]
| foundry = [[國際字體公司|ITC]]
| sample  = [[File:Bookman_sample.svg|220px|Bookman 範例文字]]
| sample_fullimage = Bookman.png
}}</nowiki></pre>
</div>

{{brClear}}
=== 最精簡語法 ===
{{Infobox font
| name  = 微軟雅黑
| style = [[無襯線體]]
}}

<div style="width:50%;">
<pre><nowiki>{{Infobox font
| name  = 微軟雅黑
| style = [[無襯線體]]
}}</nowiki></pre>
</div>

{{brClear}}

=== 選填語法 ===
{{Infobox font
| name = Helvetica
| familyname = Helvetica
| image = [[File:Helvetica font.svg|220px|Helvetica]]
| style = [[無襯線體]]
| date = [[1957年]]
| creator = 馬克斯·米耶丁格
| foundry = [[Haas Typefoundry]]<br />[[Linotype]]
| origin = [[瑞士]][[蘇黎世]]
| variations = [[Helvetica Neue]]<br />[[Helvetica Rounded]]<br />[[Nimbus Sans]]
| sample = [[File:Helvetica sample.svg|220px|Helvetica 範例文字]]
}}

<div style="width:50%;">
<pre><nowiki>{{Infobox font
| name = Helvetica
| familyname = Helvetica
| image = [[File:Helvetica font.svg|220px|Helvetica]]
| style = [[無襯線字體]]
| aka = [[瑞士字體]]
| date = [[1957年]]
| creator = 馬克斯·米耶丁格
| foundry = [[Haas Typefoundry]]<br />[[Linotype]]
| origin = [[瑞士]][[蘇黎世]]
| variations = [[Helvetica Neue]]<br />[[Helvetica Rounded]]<br />[[Nimbus Sans]]
| sample = [[File:Helvetica sample.svg|220px|Helvetica 範例文字]]
}}</nowiki></pre>
</div>
{{brClear}}
<includeonly>
{{Film and Television related infobox templates}}
[[Category:文化信息框模板|F]]
[[Category:電腦信息框模板|F]]
</includeonly>