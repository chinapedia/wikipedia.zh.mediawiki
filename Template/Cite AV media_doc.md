<noinclude>{{template doc page viewed directly}}</noinclude><!-- EDIT TEMPLATE DOCUMENTATION BELOW THIS LINE -->
{{lua|模块:Citation/CS1}}
__NOTOC__

{{Citation Style documentation/cs1}}

这个[[Help:引文格式1|引文格式1]][[Template:Cite episode|模板]]可用作引用[[影音]]媒體。對於連續劇或連載式的媒體，使用{{tl|cite episode}}或{{tl|cite serial}}。要引用唱片封套上的說明文字（liner notes）及其他配有影音媒體的平面媒體，請使用{{tlx|cite AV media notes}}。 

== 用法 ==
{{csdoc|usage}}

橫向格式：

<code><nowiki>{{cite AV media |people= |date= |year= |title= |trans-title= |medium= |language= |url= |access-date= |archive-url= |archive-date= |format= |time= |location= |publisher= |id= |isbn= |oclc= |quote= |ref= }}</nowiki></code>

縱向格式：
{{pre2|<nowiki>{{cite AV media
 | people =
 | date =
 | year =
 | title =
 | trans-title =
 | medium =
 | language =
 | url =
 | access-date =
 | archive-url =
 | archive-date =
 | format =
 | time =
 | location =
 | publisher =
 | id =
 | isbn =
 | oclc =
 | quote =
 | ref =
}}</nowiki>}}

===範例===
<code><nowiki>{{cite AV media | people=Fouladkar, Assad (Director) | date=May 15, 2003 | title=Lamma hikyit Maryam | trans-title = When Maryam Spoke Out | medium=Motion picture | location=Lebanon | publisher=Fouladkar, Assad | time=12:34}}</nowiki></code>
顯示為

{{cite AV media | people=Fouladkar, Assad (Director) | date=May 15, 2003 | title=Lamma hikyit Maryam | trans-title=When Maryam Spoke Out |medium=Motion picture | location=Lebanon | publisher=Fouladkar, Assad | time=12:34}}

==參數==
===語法===
<div style="font-size: 90%;">
子項可能依靠母項的存在，或取代母項 Nested fields either rely on their parent fields, or replace them:
*''母項 parent''
**''子項 child'' &mdash; 或能與''母項'''''同時使用'''（如子母兩項必須同時使用，而母項未有填寫，子項不會顯示） may be used '''with''' ''parent'' (and is ignored if ''parent'' is not used)
</div>

===說明===
* '''people'''：可以是任何關於影音媒體的人物，請於括號內說明（監製、導演、演員等）。
* '''date'''：影片最初的發佈日期，YYYY-MM-DD格式。先月后日，也可不带日，如5月1日、5月。不能加维基链接。
** '''year'''：影片最初的發佈年份。'''date'''使用後將不會顯示，只知年份而不知道月日時使用。
* '''title'''：影片标题，可以加维基链接。'''这是唯一的必填字段。'''
** '''url'''：与影片相关的外部链接。
** '''format'''：影片的文件格式，如rmvb、avi。
** '''medium'''：被查阅影片的所在媒介。可以是电影、电视、纪录片、DVD等。
* '''publisher'''：出版人或發行商的名稱，如「派拉蒙電影」或「迪士尼」。
** '''location'''：出版人或發行商的實際位置。
* '''accessdate'''：查阅此影片时的日期，应该符合[[ISO 8601]]格式，即YYYY-MM-DD，比如2006-02-17。'''如果填写了url字段，则此字段也需要填写。'''不能加维基链接。
* '''time'''：某一事件在影片中发生的大约的时间点。在列明来源时较有用。

<includeonly>
[[Category:引用模板|{{PAGENAME}}]]
[[Category:多媒体模板]]
</includeonly>
<templatedata>
{
	"params": {
		"title": {
			"label": "標題"
		},
		"url": {
			"label": "網址"
		},
		"date": {
			"label": "發佈日期"
		},
		"publisher": {
			"label": "發行商"
		},
		"accessdate": {
			"label": "查閱日期"
		},
		"time": {
			"label": "時間點"
		},
		"medium": {
			"label": "媒介"
		}
	},
	"description": "這個模板用作引用影音媒體。對於連續劇或連載式的媒體，請使用{{Tl|cite episode}}或{{Tl|cite serial}}。要引用唱片封套上的說明文字（liner notes）及其他配有影音媒體的平面媒體，請使用{{Tl|cite AV media notes}}。",
	"format": "inline"
}
</templatedata>