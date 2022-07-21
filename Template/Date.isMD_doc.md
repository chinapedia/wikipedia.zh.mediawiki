<includeonly>{{pp-template}}{{esoteric}}</includeonly><noinclude>{{template doc page viewed directly}}</noinclude>
{{tl|Date.isMD|參數1}}判斷參數1是否为一個月份和天數的組合。
== 细节 ==
本模板调用<nowiki>{{#switch:}}</nowiki>函数进行判断，当参数1为类似于以下中文格式的月份或日期时，返回值为“1”：
* 1月
* 1月1日
* 12月31日
为其他值时，返回空串。

== 举例 ==

{| class="wikitable"
! 代码
! 结果
|-
| <code><nowiki>{{Date.isMD|1月}}</nowiki></code>
| {{Date.isMD|1月}}
|-
| <code><nowiki>{{Date.isMD|12月}}</nowiki></code>
| {{Date.isMD|12月}}
|-
| <code><nowiki>{{Date.isMD|12月1日}}</nowiki></code>
| {{Date.isMD|12月1日}}
|-
| <code><nowiki>{{Date.isMD|二月}}</nowiki></code>
| {{Date.isMD|二月}}
|-
| <code><nowiki>{{Date.isMD|二月二日}}</nowiki></code>
| {{Date.isMD|二月二日}}
|-
| <code><nowiki>{{Date.isMD|1}}</nowiki></code>
| {{Date.isMD|1}}
|-
| <code><nowiki>{{Date.isMD|0}}</nowiki></code>
| {{Date.isMD|0}}
|-
| <code><nowiki>{{Date.isMD|0801}}</nowiki></code>
| {{Date.isMD|0801}}
|-
| <code><nowiki>{{Date.isMD|}}</nowiki></code>
| {{Date.isMD|}}
|}
<span style="font-size:smaller;">（注：单元格为空表示输出空串。）</span>

== 参见 ==
* {{tl|Date.IsLeapYear}}，判断某一年份是否为闰年。
* [[Help:模板扩展语法#switch]]
<includeonly>
[[Category:日期计算模板|{{PAGENAME}}]]
</includeonly>