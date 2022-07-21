{{#expr:{{Date.OffsetMinutes|{{{1|0}}}}}+{{Date.OrdinalMinutes|{{#if:{{{2|}}}|{{{2}}}|{{CURRENTTIME}}}}}}}}<noinclude>{{pp-template}}
{{esoteric}}
----
用法：
 <code><nowiki>{{</nowiki>{{PAGENAME}}<nowiki>|时区|UTC时间（省略为当前时间）}}</nowiki></code>
返回UTC时间相对于指定时区零时的分钟数。

[[category:日期计算模板]]
</noinclude>