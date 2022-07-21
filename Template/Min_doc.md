<noinclude>{{Documentation subpage}}</noinclude>
{{High-use|3021}}
<!-- 請在本行以下編輯模板的說明 -->
{{lua|Module:Math}}
本模板能夠評估並回復數字值的最小值（可填寫多個欄位）。空白的欄位將會被自動忽略。

; 原始碼<nowiki>：</nowiki>
: <tt><nowiki>{{min|</nowiki></tt>[數值1]<tt><nowiki>|</nowiki></tt>[數值2]<tt><nowiki>|</nowiki></tt>[數值3]<tt><nowiki>}}</nowiki></tt>

; 範例<nowiki>：</nowiki>
: <tt><nowiki>{{min}}</nowiki></tt> = {{min}}
: <tt><nowiki>{{min|}}</nowiki></tt> = {{min|}}
: <tt><nowiki>{{min|-7}}</nowiki></tt> = {{min|-7}}
: <tt><nowiki>{{min|-7|}}</nowiki></tt> = {{min|-7|}}
: <tt><nowiki>{{min|7|-5}}</nowiki></tt> = {{min|7|-5}}
: <tt><nowiki>{{min|7|-5|}}</nowiki></tt> = {{min|7|-5|}}
: <tt><nowiki>{{min|7|-5|-8}}</nowiki></tt> = {{min|7|-5|-8}}
: <tt><nowiki>{{min|40*41|300+30}}</nowiki></tt> = {{min|40*41|300+30}}
: <tt><nowiki>{{min|100+10|300+30|200+20}}</nowiki></tt> = {{min|100+10|300+30|200+20}}
: <tt><nowiki>{{min|0|19|118.2|17|-16|15|14|13|1200.5|11|10|9|8|-7|6|5.2|4|3|2|1}}</nowiki></tt> = {{min|0|19|118.2|17|-16|15|14|13|1200.5|11|10|9|8|-7|6|5.2|4|3|2|1}}

; 參見<nowiki>：</nowiki>
* [[Template:Max]]