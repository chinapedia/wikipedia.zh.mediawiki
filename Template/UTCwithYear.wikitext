{{Date.day+nY|{{#expr:
  ({{Date.OrdinalMinutesTZ|{{{1|0}}}|{{{2|{{CURRENTTIME}}}}}}} >= 1440 )
  - ( {{Date.OrdinalMinutesTZ|{{{1|0}}}|{{{2|{{CURRENTTIME}}}}}}}<0 ) 
}}}}{{UTCtime|{{{1|0}}}|{{{2|{{CURRENTTIME}}}}}}}<noinclude>
{{esoteric}}
----
指定时区的时间。

用法：<nowiki>{{</nowiki>{{PAGENAME}}|''时区''|''UTC时间（省略为当前UTC时间）''<nowiki>}}</nowiki>

相关说明见[[Template:UTC]]。

以[[Help:模板|subst:]]方式生成时间，可以参看[[help:模板擴展語法]]的#time。

[[category:日期计算模板]]
[[category:时间显示模板]]
</noinclude>