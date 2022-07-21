{{NoteTA/MediaWiki}}
{{Documentation_subpage}}
{{esoteric}}
用法：
 &#123;&#123;Userboxes
 | bordercolor = 邊框顏色
 | backgroundcolor = 背景色
 | align = 對齊方式
 | toptext = 標題文字，缺省為“''用戶頁面名稱''的[[wikipedia:用戶框|用戶框]]”
 |用户框1|用户框2|用户框3|……|用户框n (最多100个)
 &#125;&#125;
以上的命名参数都可省略。对每一个用户框，都可以加一个参数，参数以该用户框为名的命名参数给出。
#当该用户框参数为&#123;&#123;{1}&#125;&#125;形式时的例子：
#:&#123;&#123;Userboxes|skype|skype=username&#125;&#125;
#当该用户框参数为&#123;&#123;{nameparameter}&#125;&#125;形式时的例子：
#:&#123;&#123;Userboxes|Blog|Blog=<span style="color: red;"><nowiki>BlogUrl=[http://www.example.com 链接标题]</nowiki></span>&#125;&#125;
本模板支持分组，分组可以“|grpX|grpX=分组名称”的参数形式给出，“X”为0-20的阿拉伯数字或空值，但不能重复。加上X為空的情形，也就是说，可支持最多22个分组。

&#123;&#123;Userboxes|grp|grp=语言|zh|en|grp1|grp1=时间|UTC+8|grp2|grp2=即时联系|skype|skype=username|QQ|QQ=888888888&#125;&#125;

== 注意事項 ==
填寫用戶框參數時，如果前面某一參數留空不填，會產生{{tlc|[[Template:User|User ]]|}}（{{User |}}），請確保填入的參數不會有<nowiki>{{Userboxes|box1|box2| |box4}}</nowiki>之類的情形。

== 參看 ==
类似功能模板：
*[[Template:Babel]]
*[[Template:Babel-N]]
*[[Template:Userboxtop]]
*[[Template:Userboxbottom]]
*[[Template:Userboxtop2]]

{{UF-hcard-part}}
<includeonly>
<!-- 請在此線底下增加分類 -->
[[Category:用户框模板]]
<!-- 請在此線底下增加跨語言連結 -->
</includeonly>