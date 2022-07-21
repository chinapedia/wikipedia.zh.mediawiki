<includeonly>
{{#ifeq:{{#titleparts:{{PAGENAME}}|1}}|Birth date and age
 | {{Template shortcut|Bda}}
 | {{Template shortcut|Dob}}
}}
{{#ifeq:{{#titleparts:{{PAGENAME}}|1}}|Birth date and age
 | {{High-use|45,000+}} <!--(Template:Birth date and age)-->
 | {{High-use|10,000+}} <!--(Template:Birth date)-->
}}</includeonly><noinclude>{{template doc page viewed directly|{{tl|Birth date and age}}和{{tl|Birth date}}}}</noinclude>
使用模板{{tl|Birth date and age}}將會顯示出生日期，並在其後自動計算並加註今年的年齡。{{tl|Birth date}}是一个用法相似的模板，但不会加注年龄。

如果知道出生日，但只欲顯示出生年份，請使用{{tl|Birth year and age confirmed}}。如果不知道出生日，只知道出生年份，請使用{{tl|Birth year and age}}。

== 使用說明 ==
{| class="plainlinksneverexpand noprint"  style="margin-top:0; width:100%; text-align:center;border:1px #ddd solid;border-radius:5px;"
|-
! style="background:#dfd;border-radius:5px;"|本頁說明全部範例所使用的今天日期是<br>
{{CURRENTYEAR}}年{{CURRENTMONTHNAME}}{{CURRENTDAY}}日
|}

請使用以下原始碼：

: <code><nowiki>{{Birth date|year=|month=|day=}}</nowiki></code>

: <code><nowiki>{{Birth date and age|year=|month=|day=}}</nowiki></code>

其中：
* '''year'''：出生西元年份（請填寫四位數的阿拉伯數字，不須加上「年」）
* '''month'''：出生月份（請填寫阿拉伯數字，不須加上「月」）
* '''day'''：出生日（請填寫阿拉伯數字，不須加上「日」）

== 範例 ==
'''例1'''，使用：
<pre>{{Birth date and age|year=1993|month=2|day=24}}</pre>

页面上显示为：

{{Birth date and age|year=1993|month=2|day=24}}

'''例2'''，也可以省略變數名稱，例如：
<pre>{{Birth date and age|1993|2|24}}</pre>

页面上显示为：

{{Birth date and age|1993|2|24}}

'''例3'''，若使用：
<pre>{{Birth date|1993|02|24}}</pre>

则页面上显示为：

{{Birth date|1993|2|24}}

== 重定向 ==
{{tl|生日和年齡}}重定向至{{tl|Birth date and age}}。

== 参见 ==
* {{tl|Death date and age}}，用于显示某人去世日期与年龄。
* {{tl|Start date and age}}，傳回日期和它距離今天的時間長度。
{{出生、逝世及日期模板|BDA}}

<includeonly>{{Sandbox other||<!-- 本行下加入模板的分類 -->
[[Category:日期计算模板|{{PAGENAME}}]]
[[Category:生卒模板|{{PAGENAME}}]]
}}</includeonly>