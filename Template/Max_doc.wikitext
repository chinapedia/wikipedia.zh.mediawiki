<includeonly><!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{Documentation subpage}}</noinclude>
<!-- 請在本行以下編輯模板的說明 -->
{{lua|Module:Math}}
本模板能夠評估並回復數字值的最大值（可填寫多個欄位）。空白的欄位將會被自動忽略。

== 用法 ==
: <tt><nowiki>{{max|</nowiki></tt>數值1<tt><nowiki>|</nowiki></tt>數值2<tt><nowiki>|</nowiki></tt>數值3<tt><nowiki>}}</nowiki></tt>

== 範例 ==
: <tt><nowiki>{{max}}</nowiki></tt> = {{max}}
: <tt><nowiki>{{max|}}</nowiki></tt> = {{max|}}
: <tt><nowiki>{{max|-7}}</nowiki></tt> = {{max|-7}}
: <tt><nowiki>{{max|-7|}}</nowiki></tt> = {{max|-7|}}
: <tt><nowiki>{{max|-7|5}}</nowiki></tt> = {{max|-7|5}}
: <tt><nowiki>{{max|-7|5|}}</nowiki></tt> = {{max|-7|5|}}
: <tt><nowiki>{{max|-7|5|8}}</nowiki></tt> = {{max|-7|5|8}}
: <tt><nowiki>{{max|40*41|300+30}}</nowiki></tt> = {{max|40*41|300+30}}
: <tt><nowiki>{{max|100+10|300+30|200+20}}</nowiki></tt> = {{max|100+10|300+30|200+20}}
: <tt><nowiki>{{max|2000.1|-7|5|8|-199.9}}</nowiki></tt> = {{max|2000.1|-7|5|8|-199.9}}
: <tt><nowiki>{{max|0|19|118.2|17|-16|15|14|13|1200.5|11|10|9|8|-7|6|5.2|4|3|2|1}}</nowiki></tt> = {{max|0|19|118.2|17|-16|15|14|13|1200.5|11|10|9|8|-7|6|5.2|4|3|2|1}}

== 參見 ==
* [[:Template:Min]]<includeonly>
<!-- 頁面分類 -->
[[Category:函数模板]]
</includeonly>