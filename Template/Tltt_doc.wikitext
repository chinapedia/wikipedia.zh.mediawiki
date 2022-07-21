<includeonly><!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{Documentation subpage}}</noinclude>

==意思==
'''tltt'''代表'''"template link with [[:en:Tooltip|tooltip]]"'''（即包含[[工具提示]]的模板連結），"tt"亦可代表<nowiki><tt></nowiki>標籤。

==用法==
功能類似{{tl|tl|}}（參見該模板的[[Template:Tl/doc|說明]]），但增加了顯示工具提示的參數。當使用者將滑鼠箭頭指在模板連結上便會顯示工具提示。

代碼：
:<nowiki>{{tltt|模板名稱|工具提示文字}}</nowiki>

範例：
* <nowiki>{{tltt|tl|模板連結}}</nowiki> → {{tltt|tl|模板連結}}
* <nowiki>{{tltt|tltt|包含工具提示的模板連結}}</nowiki> → {{tltt|tltt|包含工具提示的模板連結}}

模板亦允許有最多兩個參數或命名參數：
:代碼：
:<nowiki>{{tltt|模板名稱|工具提示文字|par=1|par2=2}}</nowiki>
:<nowiki>{{tltt|模板名稱|工具提示文字|par=第一參數=1|par2=第二參數=2}}</nowiki>
:效果：
:{{tltt|模板名稱|工具提示文字|par=1|par2=2}}
:{{tltt|模板名稱|工具提示文字|par=第一參數=1|par2=第二參數=2}}

若需要加入更多的參數請利用<nowiki><nowiki></nowiki></nowiki>標籤，即：<nowiki>{{tltt|模板名稱|工具提示文字|par=第一參數=1|par2=第二參數=2</nowiki><nowiki><nowiki>|第三參數=3</nowiki></nowiki><nowiki>}}</nowiki>

==已知問題==
* 在一些作業系統上，工具提示文字只會在用戶將滑鼠箭頭指在[[曲括號]]（'''{}'''）上顯示，而不是連結本身。
* 工具提示文字並不支援西文符號的雙[[引號]]（'''" "'''）。

==相關模板==
* {{tl|Tltt/tip}} - 提示用戶將滑鼠箭頭指在模板連結之上
* {{tl|Tltts}} - 模板名稱前方有「subst:」修飾符

<includeonly>
[[Category:内部链接模板|Tltt]]

[[en:Template:Tltt]]
[[km:ទំព័រគំរូ:Tltt]]
[[ko:틀:Tltt]]
[[ml:ഫലകം:Tltt]]
[[or:ଛାଞ୍ଚ:Tltt]]
[[simple:Template:Tltt]]
</includeonly>