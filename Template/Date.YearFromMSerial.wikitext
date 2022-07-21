{{#expr:{{{2|{{CURRENTYEAR}}}}} 
  - {{#expr:{{{1|{{CURRENTMONTH}}}}}<=0}}
  + {{#expr:{{{1|{{CURRENTMONTH}}}}}>12}}
}}<noinclude>
----
{{esoteric}}
*功能：从月序数返回对应的年份
*用法：
 <nowiki>{{</nowiki>{{PAGENAME}}<nowiki>|月序数|年份}}</nowiki>
参数可省略，默認為當前月份和當前年份。
[[Category:日期计算模板]]
</noinclude>