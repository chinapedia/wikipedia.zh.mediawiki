<includeonly><div style="text-align: center;">
{{#iferror:{{#expr:1+{{{1|{{PAGENAME}}}}}/ 10}}|<!--
發生錯誤則僅顯示條目名稱-->{{PAGENAME}}|<small>
{{#ifexpr:(1 + {{{1|{{PAGENAME}}}}} / ({{{digit|1}}}*10) - 0.5 round 0) * ({{{digit|1}}}*10) - ({{{digit|1}}}*11) < -1|<!--
取消產生小於負一之整數的連結 (若關注通通過允許建立負二以下之條目可以取消此限制)。-->[[{{{last|负数}}}|<<]] |[[{{{last|{{{modifier|{{{namespace|}}}}}}{{ {{{template|echo}}} | {{{arg|1}}}={{#expr: (1 + {{{1|{{PAGENAME}}}}} / ({{{digit|1}}}*10) - 0.5 round 0) * ({{{digit|1}}}*10) - ({{{digit|1}}}*11)}} }}{{{unit|}}} }}}|<<]]}} <!--
數列本體 -->{{數列|&nbsp;{{{prefix|}}}{{if{{!}}exist{{!}}<!--
檢查條目是否存在 (以數字條目現況通常不存在則代表缺乏關注度，無須顯示紅色連結) -->{{{modifier|{{{namespace|}}}}}}{{#if:{{{template|}}}|{{((}}{{{template}}}{{!}}{{{arg|1}}}{{=}}}}${{#if:{{{template|}}}|{{))}}}}{{{unit|}}}<!--
如果存在則以[[]]包裹住數字條目名稱-->{{!}}[[{{{modifier|{{{namespace|}}}}}}{{#if:{{{template|}}}|{{((}}{{{template}}}{{!}}{{{arg|1}}}{{=}}}}${{#if:{{{template|}}}|{{))}}}}{{{unit|}}}{{!}}{{{modifier|}}}{{#if:{{{template|}}}|{{((}}{{{template}}}{{!}}{{{arg|1}}}{{=}}}}${{#if:{{{template|}}}|{{))}}}}{{{unit|}}}]]{{{postfix|}}}<!--
如果條目不存在則不產生內部連結-->{{!}}{{{modifier| <!--若未加這個會黏一起-->}}}{{#if:{{{template|}}}|{{((}}{{{template}}}{{!}}{{{arg|1}}}{{=}}}}${{#if:{{{template|}}}|{{))}}}}{{{unit|}}}{{{postfix|}}}&zwj;<!--若未加這個會黏一起-->}}|<!--
用高斯符號求出對應於此數區間的下界-->{{#expr: (1 + {{{1|{{PAGENAME}}}}} / ({{{digit|1}}}*10) - 0.5 round 0) * 10 - 10}}|<!--
用高斯符號求出對應於此數區間的上界，並確保下界與上界之間有9個數字-->{{#expr: (1 + {{{1|{{PAGENAME}}}}} / ({{{digit|1}}}*10) - 0.5 round 0) * 10 - 1}}|x*{{{digit|1}}}+{{{tail|0}}}
|preprocess=1}}
[[{{{next|{{{modifier|{{{namespace|}}}}}}{{ {{{template|echo}}} | {{{arg|1}}}={{#expr: (1 + {{{1|{{PAGENAME}}}}} / ({{{digit|1}}}*10) - 0.5 round 0) * ({{{digit|1}}}*10) - 0}} }}{{{unit|}}} }}}|>>]]
</small>
<!--end #iferror-->}}</includeonly><noinclude><table border=0 style="background:#F9F9F9; text-align: center; border-collapse: collapse;" align=center>{{變數|set<!--

在預覽模式下修改demo數值以檢視不同數字的效果
-->|demo=1}}

<tr><td>[[数表]] &mdash; [[整数]]

<tr><td>
{{Numbers digits|{{#iferror:{{變數|get|demo}}|1}}}}
{{Numbers digits|{{#iferror:{{變數|get|demo}}|1}}|digit=10}}
{{Numbers digits|{{#iferror:{{變數|get|demo}}|1}}|digit=100}}
{{Numbers digits|{{解析數字|-{{#iferror:{{變數|get|demo}}|1}}}} }}
{{Numbers digits|{{#iferror:{{變數|get|demo}}|1}}|template=數字轉中文}}
{{Numbers digits|{{#iferror:{{變數|get|demo}}|1}}|namespace=:Category:|template=數字轉中文}}
{{Numbers digits|{{#iferror:{{變數|get|demo}}|1}}|template=LinkForElement}}
{{Numbers digits|{{#iferror:{{變數|get|demo}}|1}}|template=Roman|last=羅馬數字}}
</td></tr>
</table></div>{{Doc}}</noinclude>