{{#ifexpr: {{{1|0}}} >= 1........
 | [[File:Yellow card.svg|10px|{{#if: {{{2|<noinclude>-</noinclude>}}} |於{{{2}}}'}}黃牌警告|link=]] <span style="position:relative; left:-5px">}}<!--
-->{{#ifexpr: {{{1|0}}} >= 2
 | [[File:Yellow card.svg|10px|{{#if: {{{3|<noinclude>-</noinclude>}}} |於{{{3}}}'}}第二面黃牌|link=]] <span style="position:relative; left:-5px">}}<!--
-->[[File:Red card.svg|10px|{{#if: {{{3|<noinclude>-</noinclude>}}}
 | 於 {{{3}}}'
 | {{#if: {{{2|<noinclude>-</noinclude>}}}|於{{{2}}}'}}
}}紅牌離場|link=]] <span style="font-size:10px; vertical-align:middle">{{#if: {{{2|<noinclude>-</noinclude>}}} |  {{{2}}}' }}{{#if: {{{3|<noinclude>-</noinclude>}}} | , {{{3}}}'}}</span><!-- 
-->{{#ifexpr: {{{1|0}}} >= 2 |</span>}}<!--
-->{{#ifexpr: {{{1|0}}} >= 1 |</span>}}<noinclude>

==語法==
<code><nowiki>{{sent off|0|min}}</nowiki> -> {{sent off|0}}</code> ''直接出示紅牌''

<code><nowiki>{{sent off|1|ycmin|min}}</nowiki> -> {{sent off|1}}</code> ''第一次出示黃牌，第二次直接出示紅牌''

<code><nowiki>{{sent off|2|ycmin|min}}</nowiki> -> {{sent off|2}}</code> ''兩次收到黃牌警告，紅牌出場''

;''ycmin''
:黃牌的發出時間

;''min''
:紅牌的發出時間


<code><nowiki>{{sent off|0|67}}</nowiki> -> {{sent off|0|67}}</code>

<code><nowiki>{{sent off|1|23|60}}</nowiki> -> {{sent off|1|23|60}}</code>

<code><nowiki>{{sent off|2|23|60}}</nowiki> -> {{sent off|2|23|60}}</code>

==例子==
*<code><nowiki>{{sent off}}</nowiki> -> </code>{{sent off}}
*<code><nowiki>{{sent off|1}}</nowiki> -> </code>{{sent off|1}}
*<code><nowiki>{{sent off|2}}</nowiki> -> </code>{{sent off|2}}
*<code><nowiki>{{sent off|0|27}}</nowiki> -> </code>{{sent off|0|27}}
*<code><nowiki>{{sent off|1|67|88}}</nowiki> -> </code>{{sent off|1|67|88}}
*<code><nowiki>{{sent off|2|23|60}}</nowiki> -> </code>{{sent off|2|23|60}}

==參見==
{{Match report templates}}

[[Category:足球模板]]
</noinclude>