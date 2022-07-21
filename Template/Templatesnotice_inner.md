<includeonly>{{#if: {{{notwinkle|}}} || {{Twinkle standard installation}} }}
{{substituted|auto={{#ifeq:{{FULLPAGENAME}}|Template:Templatesnotice|no|yes}}}}
</includeonly>
== 用法 ==
* <code>{{tls|{{#ifeq:{{NAMESPACE}}|Template||{{NAMESPACE}}:}}{{PAGENAME}}}}</code>
* <code>{{tls|{{#ifeq:{{NAMESPACE}}|Template||{{NAMESPACE}}:}}{{PAGENAME}}|原因}}</code> 指明一個特定的原因
* <code>{{tls|{{#ifeq:{{NAMESPACE}}|Template||{{NAMESPACE}}:}}{{PAGENAME}}|原因<nowiki>|附加文字</nowiki>}}</code> {{#ifeq:{{{param2}}}|yes||刪去訊息最後的「謝謝」字眼，}}在後加入附加文字。
{{#if:{{{s1|}}}|{{template shortcut|{{{s1}}}|{{{s2|}}}|{{{s3|}}}|{{{s4|}}}}}}}
* 此標準化模板符合[[Wikipedia:用戶警告專題|用戶警告專題]]的指南，您可以在[[Wikipedia talk:用戶警告專題|用戶警告專題討論頁]]討論這些標準化模板的視覺外觀（例如左上角的圖像）。
* 在用戶討論頁上使用任何模板之前，請參閱[[Wikipedia:模板消息/用戶討論名字空間|模板消息的索引]]以警告用戶。應用最符合您的目的的模板有助於減少您發送消息的混淆。
* 當使用多層級模板時，在某些情況下，您不需要從層級1警告開始。查看[[Wikipedia:模板消息/用戶討論名字空間#多層級模板]]。
* 請記得使用<code>{{tls|{{#ifeq:{{NAMESPACE}}|Template||{{NAMESPACE}}:}}{{PAGENAME}}}}</code>而不是{{tlc|{{lcfirst:{{#ifeq:{{NAMESPACE}}|Template||{{NAMESPACE}}:}}{{PAGENAME}}}}}}來[[Help:替换引用|替換]]模板。
* 此模板使用[[mw:Help:Extension:ParserFunctions|分析器功能]]。要更詳細地說明您的信息，您可以將頁面和一些其他文字添加到模板的尾端。{{#if:{{{extra usage|}}}|{{{extra usage}}}}}

{{#if:{{{series|}}}<!--
---->|{{#switch:{{{max|5}}}<!--
------>|1={{user-warning set|{{{series|}}}<!--
-------->|1|{{#ifeq:{{{escalate|}}}|yes|uw-{{#if:{{{escalate_to|}}}|{{{escalate_to}}}|vandalism}}2|uw-{{#if:{{{escalate_to|}}}|{{{escalate_to}}}|vandalism}}3|uw-{{#if:{{{escalate_to|}}}|{{{escalate_to}}}|vandalism}}4|||}}|}}<!-- 
------>|2={{user warning set|series={{{series|}}}<!--
-------->|1|2|{{#ifeq:{{{escalate|}}}|yes|uw-{{#if:{{{escalate_to|}}}|{{{escalate_to}}}|vandalism}}3|uw-{{#if:{{{escalate_to|}}}|{{{escalate_to}}}|vandalism}}4||}}|}}<!-- 
------>|3={{user warning set|series={{{series|}}}<!--
-------->|1|2|3|{{#ifeq:{{{escalate|}}}|yes|uw-{{#if:{{{escalate_to|}}}|{{{escalate_to}}}|vandalism}}4}}|}}<!--  
------>|4={{user warning set|series={{{series|}}}|1|2|3|4|}}<!--
------>|#default={{user warning set|series={{{series|}}}|1|2|3|4|4im}}<!--
---->}}<!--
-->}}<noinclude>
{{Documentation}}</noinclude>