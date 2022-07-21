{{#expr: {{Date.DaysBeforeMonth
    | {{{2|{{CURRENTMONTH}}}}}
    | {{{3|{{CURRENTYEAR}}}}}
  }} + {{{1|{{CURRENTDAY}}}}}
}}<noinclude>{{pp-template}}
----
{{esoteric}}
用法：
 <nowiki>{{</nowiki>{{PAGENAME}}<nowiki>|日|月|年}}</nowiki>
参数可由後依次省略，默認為當前年月日。
[[Category:日期计算模板]]
</noinclude>