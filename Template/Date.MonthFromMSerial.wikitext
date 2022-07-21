{{#expr:{{{1|{{CURRENTMONTH}}}}} 
  + {{#expr:{{{1|{{CURRENTMONTH}}}}}<=0}}*12
  - {{#expr:{{{1|{{CURRENTMONTH}}}}}>12}}*12
}}<noinclude>
----
{{esoteric}}
*功能：从月序数返回对应的月份
*用法：
 <nowiki>{{</nowiki>{{PAGENAME}}<nowiki>|月序数}}</nowiki>
参数可省略，默認為當前月。
[[Category:日期计算模板]]
</noinclude>