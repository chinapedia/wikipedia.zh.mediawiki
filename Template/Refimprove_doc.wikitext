<noinclude>{{template doc page viewed directly}}</noinclude>
{{Twinkle standard installation}}
{{high-use|26180}}
== 用法 ==

这个模板用于指出需要更多参考资料的条目。如何在条目中放置这个模板在现在还没有一致的共识。这个模板是一个[[Wikipedia:避免自我提及|自我提及]]，是维基百科项目的一部分，而非百科全书的内容，[[打印]]时不会出现。

这个模板也包括了对日期参数的支持。加上日期参数可以让条目被分入[[:Category:需补充来源的条目]]的子分类中，这样有助于编辑者区分出较早的问题以优先解决。

下面列出的两种使用方式都是正确的：

<code>
<!-- 
<nowiki>
{{refimprove}}
</nowiki>

<nowiki>
{{refimprove|</nowiki>{{CURRENTYEAR}}年{{CURRENTMONTHNAME}}<nowiki>}}
</nowiki>
-->
<nowiki>
{{refimprove|date=</nowiki>{{CURRENTYEAR}}年{{CURRENTMONTHNAME}}<nowiki>}}
</nowiki>

<nowiki>
{{refimprove|time=</nowiki>{{#time:Y-m-d}}<nowiki>}}
</nowiki>

</code>

本模板支持自动参数生成，因此可以用[[Help:替换引用|替换引用]]的方式引入时间：

<code><nowiki>{{subst:refimprove/auto}}</nowiki></code>

使用變數recommendation= 來加上建議或訊息。

|recommendation= 參考...

{{Refimprove|recommendation=參考...|time=2017-04-23}}

如只是某一章节没有来源，請使用:

{{tl|Refimprove section}}

== 与其他相似模板的不同 ==

=== 与{{tl|Unreferenced}}的区别 ===

* {{tl|Refimprove}}适用于条目中有一定的参考或来源但不足的情况，{{tl|Unreferenced}}则用于条目中完全没有参考或来源的情况。

* {{tl|Refimprove}}允许使用者直接输入日期参数，而可以忽略「date=」字符。

=== 与{{tl|Primarysources}}的区别 ===

* {{tl|Primarysources}}用于条目中缺少第二手来源的情况。

=== 与{{tl|Fact}}的区别 ===

* {{tl|Refimprove}}适用于条目的全局标记，而{{tl|Fact}}则用于标记单独的语句。

* 与{{tl|Fact}}不同的是，{{tl|Refimprove}}会在条目中添加上一个醒目的横幅。

==={{tl|Medref}}===
* 使用於醫學、藥學、心理學、神經科學等領域的條目。
{{Delcat|{{Medref}}}}

==重定向==
*{{tl|More references}}
*{{tl|Moreref}}
*{{tl|增加来源}}
*{{tl|補充来源}}
*{{tl|改善来源}}
*{{tl|Verify}}

==参见==
* {{tl|Refimprovesect}}
* {{tl|Unreferenced}}
* {{tl|Primarysources}}
* {{tl|Citation style}}
* [[Wikipedia:模板消息/条目来源]]
* [[Wikipedia:模板消息/清理]]
{{Citation and verifiability article maintenance templates}}
<includeonly>
<!-- ADD CATEGORIES BELOW THIS LINE -->
[[Category:引用與查證維護模板|{{PAGENAME}}]]

[[ar:قالب:مصادر أكثر]]
[[as:Template:Refimprove]]
[[cy:Nodyn:GwellaCyfeiriadau]]
[[en:Template:Refimprove]]
[[es:Plantilla:Referencias adicionales]]
[[fa:الگو:بهبود منبع]]
[[hy:Կաղապար:Refimprove]]
[[ja:Template:未検証]]
[[mk:Шаблон:Малку извори]]
[[ml:ഫലകം:Not verified]]
[[no:Mal:Refforbedre]]
[[pt:Predefinição:S-fontes]]
[[ro:Format:Refimprove]]
[[ru:Шаблон:Refimprove]]
[[simple:Template:More sources]]
[[sl:Predloga:Več sklicev]]
[[sv:Mall:Fler källor]]
[[uk:Шаблон:Refimprove]]
[[vi:Bản mẫu:Chú thích trong bài]]
</includeonly>