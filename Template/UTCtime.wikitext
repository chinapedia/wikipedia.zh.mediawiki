{{#ifexpr:{{Date.HourFromSerial|{{Date.OrdinalMinutesTZ|{{{1|0}}}|{{{2|{{CURRENTTIME}}}}}}}}}<10
  |0}}{{Date.HourFromSerial|{{Date.OrdinalMinutesTZ|{{{1|0}}}|{{{2|{{CURRENTTIME}}}}}}}
}}:{{#ifexpr:{{Date.MinuteFromSerial|{{Date.OrdinalMinutesTZ|{{{1|0}}}|{{{2|{{CURRENTTIME}}}}}}}}}<10
  |0}}{{Date.MinuteFromSerial|{{Date.OrdinalMinutesTZ|{{{1|0}}}|{{{2|{{CURRENTTIME}}}}}}}
}}<noinclude>{{pp-template}}
{{esoteric}}
----
用法：
 <code><nowiki>{{</nowiki>{{PAGENAME}}<nowiki>|时区|UTC时间（省略为当前UTC时间）}}</nowiki></code>
返回参数“hh:mm”中的分钟数，参数错误时返回空值。

以[[Help:模板|subst:]]方式生成时间，可以参看[[help:模板擴展語法]]的#time。

[[Category:时间显示模板]]
[[category:日期计算模板]]
</noinclude>