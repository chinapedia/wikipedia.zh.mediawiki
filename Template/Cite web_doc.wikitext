{{NoteTA
|G1=IT
|G2=MediaWiki
}}
{{Documentation subpage}}
{{High-risk|513635|all-pages = no}}
{{lua|Module:Citation/CS1}}
<!-- 在本行下編輯模板說明 -->
{{Citation Style documentation/cs1}}

==模板簡介==
描写维基条目时经常需要参考网络上的各种资源，因此更多地使用这个模板可以将所参考的来源记录下来，以便浏览者以及之后的编写者找到这些来源资料。

本模板是用來列明維基條目中'''非新聞來源'''（參見[[Wikipedia:列明来源|列明來源]]的關於維基條目列明的一般注意事項，並參見{{tlx|Cite news}}以學習如何列明'''新聞來源'''）。<br />此模板用来取代過時的'''{{tlx|Web reference}}'''。它的參數<span style="color: red;">僅允許小寫</span>。

==模板用法==
{{Citation Style documentation|usage}}

有作者的參考
:<code><nowiki>{{cite web |url= |title= |last= |first= |date= |website= |publisher= |accessdate= |quote= }}</nowiki></code>

沒有作者的參考
:<code><nowiki>{{cite web |url= |title= |date= |website= |publisher= |accessdate= |quote= }}</nowiki></code>

;直式排列的最常用參數
<!-- Please synchronize this list with the corresponding one at the overview page [[Wikipedia:Citation templates#Examples]] -->
<pre style="margin:0px; border:none; white-space:pre;">
{{cite web
| url =
| title =
| author=
| last =
| first =
| date =
| website =
| publisher =
| access-date =
| quote = }}
</pre>
{{csdoc|usage full}}
:<code><nowiki>{{cite web |url= |title= |last= |first= |author= |author-link= |last2= |first2= |author2= |author-link2= |date= |year= |editor-last= |editor-first= |editor= |editor-link= |editor2-last= |editor2-first= |editor2-link= |editors= |department= |website= |series= |publisher= |location= |page= |pages= |at= |language= |script-title= |trans-title= |type= |format= |arxiv= |asin= |bibcode= |doi= |doi-broken-date= |isbn= |issn= |jfm= |jstor= |lccn= |mr= |oclc= |ol= |osti= |pmc= |pmid= |rfc= |ssrn= |zbl= |id= |archiveurl= |archivedate= |deadurl= |accessdate= |quote= |ref= |postscript= |subscription= |registration= }}</nowiki></code>
{{end}}
;直式排列的全部參數
<pre style="margin:0px; border:none; white-space:pre;">
{{cite web
| url =
| title =
| last =
| first =
| author=
| author-link =
| last2 =
| first2 =
| author2= 
| author-link2 =
| date =
| year =
| editor-last =
| editor-first =
| editor-link =
| editor2-last =
| editor2-first =
| editor2-link =
| department =
| website =
| series =
| publisher =
| via =
| location =
| page =
| pages =
| at =
| language =
| script-title =
| trans-title =
| type =
| format =
| arxiv =
| asin =
| bibcode =
| doi =
| doi-broken-date =
| isbn =
| issn =
| jfm =
| jstor =
| lccn =
| mr =
| oclc =
| ol =
| osti =
| pmc =
| pmid =
| rfc =
| ssrn =
| zbl =
| id =
| archive-url =
| archive-date =
| dead-url =
| access-date =
| quote =
| ref =
| postscript =
| subscription =
| registration = }}
</pre>

====必填参数（<span style="color: red;">否则会报错</span>）====
*'''title''': 引用项的标题（原文）。
** '''script-title'''：外语文献（特别字形与中文差异较大的日文）建议使用该参数代替，开头需用<code>ja:</code>等形式标示语言。
*'''url''': 引用项的网址。开头必须带有通讯协议 例如<nowiki>http://或https://</nowiki>。

====选填参数====
*'''accessdate''': 查阅日期。可使用[[ISO 8601]]中规定的YYYY-MM-DD格式，例如"accessdate= {{CURRENTYEAR}}-{{CURRENTMONTH}}-{{CURRENTDAY2}}"。
*'''trans_title'''：標題的中文翻譯
*'''author''': 作者的名字（通常用于中文名）
**'''last''' 与 '''first'''：一起使用，产生效果如<code>姓, 名. </code>（主要用于英文人名名字在前，姓氏在后的情况），不要使用维基链接，作者的条目链接请填入'''authorlink'''。
**'''authorlink'''：有关作者的现有维基百科条目的标题，不要使用维基链接。
<!--**'''coauthors''': 在此处可以添加另外的共同作者。-->
*'''date''': 原文出版或发表的日期，请使用包括年、月、日的完整日期格式并与所写条目风格保持一致。如果是与使用[[ISO 8601]]中规定的YYYY-MM-DD格式时，例如是''2006-02-17''，<s>则不需要在输入日期时加上维基链接，它会自动被系统加上</s><small>（根据2014年[[WP:格式手册]]的'''新规定'''，不再对日期添加链接，原有的“<nowiki>[[2015年]][[10月21日]]</nowiki>”等内文链接也逐步被[[User:Yinweichen-bot]]等人移除）</small>。
**或者使用另一种组合: '''year''': 出版年份和'''month''': 出版月份。如果你有详细的日子，请使用''date''参数。不要加上维基链接。
*'''language''': 引用项使用的语言，以[[ISO 639-1]]代码表来标示（使用多種語言時可以用","隔開）。
*'''format''': 文件格式，例如PDF文件。此项为空则被缺省认为是HTML格式。
*'''work''': 网站的名称，可以使用维基链接。
**等效参数：'''journal''', '''newspaper''', '''magazine''', '''periodical''', '''website'''
*'''pages''': ''5–7'': 引用项所在的页数或者是所在的起始页和终止页，而不是在此写明所引用书籍的总页数。此项在引用项为PDF文件时特别有用。<!-- COmmentedout:notimplemented in the template!  This is especially useful for [[PDF]] format, where the page can be linked to with the <code>#page=''number''</code> anchor tagged on the end of the URL:
*:<code><nowiki>pages = [http://www.example.org/file.pdf#page=123 p. 123]</nowiki></code>-->
*'''publisher''': 如果存在出版者--例如这个网站是由某个政府服务部门、教育机构或公司来提供运作，则可以在此输入。
*'''via''': 非出版者--例如社群或信息网站是由某个人、部门机构或公司发布消-{}-息，则可以在此输入（例如[[Twitter]]，[[新浪微博]]等）。
* '''doi''': 有关文档的[[DOI|数位物件识别号]]，例如''<nowiki>10.1038/news070508-7</nowiki>''
**'''Doilabel''': 如果此DOI包括一些必须要进行[[URL编码]]的字符，请使用"Doilabel}}"参数表明为进行URL编码的版本。参见{{tlx|doi}}: "id"等同于"doi"而"label"等同于"doilabel"
*'''archiveurl''': 重要的网页可以被类似[[WebCite]]这样的网站[[网络存档]]，这时候这个参数应该是这个存档副本的网页网址（需要同时使用'''archivedate'''参数）。
*'''archivedate''': 此文档存档的日期（需要同时使用'''archiveurl'''参数），请使用[[ISO 8601]]YYYY-MM-DD格式，例如''2006-02-17''。不要加上维基链接。
*'''dead-url''': 标记源链接是否为失效链接。填<code>yes</code>表示失效链接，此时会以存档链接为显示主体；填<code>no</code>表示未失效链接，此时存档仅为备份作用，并以未失效的源链接为显示主体。（需要同时使用'''archiveurl'''和'''archivedate'''参数）
*'''quote''': 被引用的相关原文。

==举例说明==
===一些常见用法===
*<code><nowiki>{{Cite web
|author=Doe, John
|title=My favorite things part II
|publisher=Open Publishing
|date=2005-04-30
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2005-07-06
}}</nowiki></code><br/>→ <span style="background:white">{{Cite web
|author=Doe, John
|title=My favorite things part II
|publisher=Open Publishing
|date=2005-04-30
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2005-07-06
}}</span>

*<code><nowiki>{{Cite web
|author=Doe, John
|title=My favorite things part II
|date=2005-04-30
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2005-07-06
}}</nowiki></code><br/>→ <span style="background:white">{{Cite web
|author=Doe, John
|title=My favorite things part II
|date=2005-04-30
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2005-07-06
}}</span>

*<code><nowiki>{{Cite web
|author=Doe, John
|title=My favorite things part II
|date=2005-04-30
|url=http://www.example.org/
|accessdate=2005-07-06
}}</nowiki></code><br/>→ <span style="background:white">{{Cite web
|author=Doe, John
|title=My favorite things part II
|date=2005-04-30
|url=http://www.example.org/
|accessdate=2005-07-06
}}</span>

*<code><nowiki>{{Cite web
|author=Doe, John
|title=My favorite things part II
|url=http://www.example.org/
|accessdate=2005-07-06
}}</nowiki></code><br/>→ <span style="background:white">{{Cite web
|author=Doe, John
|title=My favorite things part II
|url=http://www.example.org/
|accessdate=2005-07-06
}}</span>

*<code><nowiki>{{Cite web
|title=My favorite things part II
|url=http://www.example.org/
|accessdate=2005-07-06
}}</nowiki></code><br/>→ <span style="background:white">{{Cite web
|title=My favorite things part II
|url=http://www.example.org/
|accessdate=2005-07-06
}}</span>

*<code><nowiki>{{Cite web
|url=http://www.nfl.com/fans/
|title=Digest of rules
|publisher= National Football League
|accessdate=2005-07-06
}}</nowiki></code><br />→ <span style="background:white">{{Cite web
|url=http://www.nfl.com/fans/
|title=Digest of rules
|publisher= National Football League
|accessdate=2005-07-06
}}</span>

===使用format参数===
*<code><nowiki>{{Cite web 
|title=List of psychotropic substances under international control
|publisher=International Narcotics Control Board
|url=http://www.incb.org/pdf/e/list/green.pdf
|format=PDF
|accessdate=2005-07-06
}}</nowiki></code><br/> → <span style="background:white">{{Cite web 
|title=List of psychotropic substances under international control
|publisher=International Narcotics Control Board
|url=http://www.incb.org/pdf/e/list/green.pdf
|format=PDF
|accessdate=2005-07-06
}}</span>

===使用language参数===
*<code><nowiki>{{Cite web
|author=Joliet, François
|title=Honnit soit qui mal y pense
|date=2005-04-30
|url=http://www.example.org/
|accessdate=2005-07-06
|language= Fr,zh,ja
}}</nowiki></code><br/>→ <span style="background:white">{{Cite web
|author=Joliet, François
|title=Honnit soit qui mal y pense
|date=2005-04-30
|url=http://www.example.org/
|accessdate=2005-07-06
|language= Fr,zh,ja
}}</span><!--

===使用coauthors参数===
*<code><nowiki>{{Cite web
|first=John
|last=Doe
|coauthors=Smith, Peter; Smythe, Jim
|title=My favorite things part II
|publisher=Open Publishing
|date=2005-04-30
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2006-05-16 
}}</nowiki></code><br/>→ <span style="background:white">{{Cite web
|first=John
|last=Doe
|coauthors=Smith, Peter; Smythe, Jim
|title=My favorite things part II
|publisher=Open Publishing
|date=2005-04-30
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2006-05-16 
}}</span>
<br />-->

===使用authorlink参数===
*<code><nowiki>{{Cite web
|url= http://www.ceo.gov.hk/chi/press/oped.htm
|title= 「大市場 小政府」── 我們恪守的經濟原則
|accessdate= 2008-08-08
|author= 曾蔭權
|authorlink= 曾蔭權
|date= 2006-9-18
|work= 香港特別行政區行政長官網頁
|publisher= 香港特別行政區政府新聞處
|language= zh-hant
|quote= 對於私營界別可以自己做的事，政府不應對市場作任何干預
}}</nowiki></code><br/>→ <span style="background:white">{{Cite web
|url= http://www.ceo.gov.hk/chi/press/oped.htm
|title= 「大市場 小政府」── 我們恪守的經濟原則
|accessdate= 2008-08-08
|author= 曾蔭權
|authorlink= 曾蔭權
|date= 2006-09-18
|work= 香港特別行政區行政長官網頁
|publisher= 香港特別行政區政府新聞處
|language= zh-hant
|quote= 對於私營界別可以自己做的事，政府不應對市場作任何干預
}}</span>

===不使用author参数===
*<code><nowiki>{{Cite web
|title=My favorite things part II
|publisher=Open Publishing
|date=2005-04-30
|work=Encyclopedia of things
|url=http://www.example.org/ | accessdate=2006-05-16 
}}</nowiki></code><br/>→ <span style="background:white">{{Cite web
|title=My favorite things part II
|publisher=Open Publishing
|date=2005-04-30
|work=Encyclopedia of things
|url=http://www.example.org/ | accessdate=2006-05-16 
}}</span>

===不使用author和publisher参数===
*<code><nowiki>{{Cite web
|title=My favorite things part II
|date=2005-04-30
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2005-07-06
}}</nowiki></code></br>→ <span style="background:white">{{Cite web
|title=My favorite things part II
|date=2005-04-30
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2005-07-06
}}</span>

*<code><nowiki>{{Cite web
|title=My favorite things part II
|date=2005-04-30
|url=http://www.example.org/
|accessdate=2005-07-06}}</nowiki></code><br/>→ <span style="background:white">{{cite web
|title=My favorite things part II
|date=2005-04-30
|url=http://www.example.org/
|accessdate=2005-07-06}}</span>

*<code><nowiki>{{Cite web 
|title=List of psychotropic substances under international control
|date=2005-04-30
|url=http://www.incb.org/pdf/e/list/green.pdf
|format=PDF
|accessdate=2005-07-06
|language= el 
}}</nowiki></code><br/> → <span style="background:white">{{Cite web 
|title=List of psychotropic substances under international control
|date=2005-04-30
|url=http://www.incb.org/pdf/e/list/green.pdf
|format=PDF
|accessdate=2005-07-06
|language= el 
}}</span>

===使用参数archiveurl和archivedate及url-status（可选）添加存档网页===
*<code><nowiki>{{Cite web
|title=List of psychotropic substances under international control
|date=2005-04-30
|url=http://www.incb.org/pdf/e/list/green.pdf
|format=PDF
|accessdate=2005-07-06
|archiveurl=http://www.archive.org/2005-09-11/www.incb.org/pdf/e/list/green.pdf
|archivedate=2005-09-11
}}</nowiki></code><br/> → <span style="background:white">{{Cite web
|title=List of psychotropic substances under international control
|date=2005-04-30
|url=http://www.incb.org/pdf/e/list/green.pdf
|format=PDF
|accessdate=2005-07-06
|archiveurl=http://www.archive.org/2005-09-11/www.incb.org/pdf/e/list/green.pdf
|archivedate=2005-09-11
}}</span>

*<code><nowiki>{{Cite web
|url=http://joanjettbadrep.com/cgi-bin/fullStory.cgi?archive=currnews&story=20060405-01shore.htm
|title=Interview with Maggie Downs
|date=2006-03-31
|publisher=The Desert Sun
|archiveurl=http://72.14.207.104/search?q=cache:JAxf4v-pQmgJ:joanjettbadrep.com/cgi-bin/fullStory.cgi%3Farchive%3Dcurrnews%26story%3D20060405-01shore.htm
|archivedate=2006-04-26
}}</nowiki></code><br/> → <span style="background:white">{{Cite web
|url=http://joanjettbadrep.com/cgi-bin/fullStory.cgi?archive=currnews&story=20060405-01shore.htm
|title=Interview with Maggie Downs
|date=2006-03-31
|publisher=The Desert Sun
|archiveurl=http://72.14.207.104/search?q=cache:JAxf4v-pQmgJ:joanjettbadrep.com/cgi-bin/fullStory.cgi%3Farchive%3Dcurrnews%26story%3D20060405-01shore.htm
|archivedate=2006-04-26
}}</span>

===使用quote参数===
*<code><nowiki>{{Cite web
|title=My favorite things part II
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2005-07-06
|quote=Lorem ipsum dolor.
}}</nowiki></code><br/>→ <span style="background:white">{{Cite web
|title=My favorite things part II
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2005-07-06
|quote=Lorem ipsum dolor.
}}</span>

===忘记填写title参数而导致的错误===
*<code><nowiki>{{Cite web
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2005-07-06
|quote=Lorem ipsum dolor.
}}</nowiki></code><br/>→ <span style="background:white">{{Cite web
|work=Encyclopedia of things
|url=http://www.example.org/
|accessdate=2005-07-06
|quote=Lorem ipsum dolor.
}}</span>

==注意事項==
某些外文標點符號（-{“　”　‘　’}-）在「繁體」模式時會錯誤轉換為引號，如在location和quote參數填入的文字有該等標點，使用<nowiki>-{... }-</nowiki>即可強制該等標點不轉換。

如果網頁標題含有以下字符，請在填寫title參數時依下表替換。

{| class="wikitable" style="text-align:center;"
! 網頁標題原有字符 !! 替換為
|-
| <nowiki> | </nowiki>
| &amp;#124;
|-
| colspan=2 align=left | 以下為以往引致錯誤的字符，已於2016年修復問題，<br/>可直接於title填「|title=[文字...] 文字...」，繼續依下表轉換亦可
|-
| <nowiki><</nowiki>
| &amp;#60;
|-
| <nowiki>[</nowiki>
| &amp;#91;
|-
| <nowiki>]</nowiki>
| &amp;#93;
|-
|}

測試：<nowiki>{{Cite web |url=https://zh.wikipedia.org |title=一<二[三]四 | 五 }}</nowiki>，顯示為：{{Cite web |url=https://zh.wikipedia.org |title=一<二[三]四 | 五 }}

請勿使用{{Tl|!}}顯示標題中的「|」，因為在<nowiki>{{!}}</nowiki>前面的文字將不會顯示，如<nowiki>{{Cite web |url=https://zh.wikipedia.org |title=前面{{!}}後面}}</nowiki>顯示為：

{{Cite web |url=https://zh.wikipedia.org |title=前面{{!}}後面}}

請改用「&amp;#124;」。

加入<code>language=en</code>（或ja、es之類）關閉轉換的方法於2015年12月以後失效。

==模板數據==
{{templatedataheader}}
== 模板数据 ==
<templatedata>
{
	"description": "该模板使用所提供的来源信息（如期刊名称、作者、标题、期数、URL）和各种格式选项，对网页进行格式化引用。",
	"params": {
		"url": {
			"label": "网址",
			"description": "该出版物的线上版本的URL。需要“http://...”一类的协议头",
			"type": "line",
			"aliases": [
				"URL"
			],
			"suggested": true,
			"example": "https://www.nytimes.com/..."
		},
		"title": {
			"label": "标题",
			"description": "文章的标题",
			"type": "content",
			"required": true
		},
		"last": {
			"label": "姓",
			"description": "作者的姓氏（仅英文人名）；不要加入条目链接，如有条目请使用'author-link'；中文人名请使用'author'",
			"aliases": [
				"last1"
			],
			"type": "line",
			"suggested": true
		},
		"first": {
			"label": "名",
			"description": "作者的名（仅英文人名）；不要加入条目链接，如有条目请使用'author-link'；中文人名请使用'author'",
			"aliases": [
				"first1"
			],
			"type": "line",
			"suggested": true
		},
		"last2": {
			"label": "姓2",
			"description": "第2名作者的姓氏（仅英文人名）；不要加入条目链接，如有条目请使用'author-link2'；",
			"type": "line"
		},
		"first2": {
			"label": "名2",
			"description": "第2名作者的名（仅英文人名）；不要加入条目链接，如有条目请使用'author-link2'；",
			"type": "line"
		},
		"date": {
			"label": "来源日期",
			"description": "来源的发表日期，使用YYYY-MM-DD格式（例如“2020-09-23”）",
			"type": "date",
			"suggested": true
		},
		"publisher": {
			"label": "出版者",
			"description": "出版商的名称，可以加入条目链接",
			"type": "content",
			"example": "[[芝加哥大学出版社]]",
			"suggested": true
		},
		"doi": {
			"label": "DOI",
			"description": "数字对象识别符；以'10.'开始",
			"type": "string",
			"suggested": true
		},
		"doi-broken-date": {
			"label": "DOI损坏日期",
			"description": "DOI损坏的日期",
			"type": "date"
		},
		"others": {
			"label": "其它人物",
			"description": "其他贡献该作品的人物，如“由约翰·史密斯插图”",
			"type": "content",
			"example": "由约翰·史密斯插图"
		},
		"year": {
			"label": "来源年份",
			"description": "来源年份，一般不推荐使用；仅当日期参数格式为YYYY-MM-DD且需要使用sfn类模板时才推荐。",
			"type": "number"
		},
		"orig-year": {
			"label": "原始日期",
			"description": "原始出版日期。为清晰起见，请提供具体细节：例如“1859年首次出版”、“1904年创作”",
			"type": "number",
			"example": "1859年首次出版"
		},
		"editor-last": {
			"label": "编者的姓",
			"description": "编者的姓（仅英文人名）。不要加入条目链接，如有条目请使用'editor-link'；中文人名请使用'editor'",
			"aliases": [
				"editor1-last"
			],
			"type": "line"
		},
		"editor-first": {
			"label": "编者的名",
			"description": "编者的名（仅英文人名）。不要加入条目链接",
			"aliases": [
				"editor1-first"
			],
			"type": "line"
		},
		"editor-link": {
			"label": "编者条目链接",
			"description": "关于编者的现有维基百科条目的标题",
			"type": "wiki-page-name"
		},
		"series": {
			"label": "系列",
			"description": "系列标识符，当来源是一个系列的一部分时",
			"type": "content",
			"aliases": [
				"version"
			]
		},
		"department": {
			"label": "Department",
			"description": "Department within the periodical",
			"type": "string",
			"deprecated": true
		},
		"location": {
			"label": "地点",
			"description": "写作的地点，通常是出版的地点。若两者不同，则在此处填入写作的地点，并使用publication-place填入出版的地点。否则只需填写出版商的地点即可",
			"type": "string",
			"example": "美国芝加哥"
		},
		"publication-place": {
			"label": "出版地点",
			"description": "出版地点，仅在出版地点与写作地点不同时使用，显示在标题之后。若使用了'place'或'location'参数，则显示在标题之前，前缀为”写在”。",
			"type": "content"
		},
		"publication-date": {
			"label": "出版日期",
			"description": "出版日期，仅在出版日期与作品的写作日期不同时使用，不要加入条目链接。",
			"type": "date"
		},
		"edition": {
			"label": "版本",
			"description": "出版物的版本，如：第2版、修订版",
			"type": "line",
			"example": "第2版"
		},
		"page": {
			"label": "页码",
			"description": "文章所在的页码，多个页码使用例如“22-26”",
			"type": "line",
			"example": "22-26",
			"aliases": [
				"pages"
			]
		},
		"no-pp": {
			"label": "No pp",
			"description": "Set to 'y' to suppress the 'p.' or 'pp.' display with 'page' or 'pages' when inappropriate (such as 'Front cover')",
			"type": "line",
			"deprecated": "直接删除即可"
		},
		"at": {
			"label": "位于",
			"description": "如页码不适用，在此填入文章在作品中的位置",
			"type": "line"
		},
		"language": {
			"label": "语言",
			"description": "来源的语言，使用ISO 639-1语言代码。例如：en、ja",
			"type": "content",
			"example": "ja"
		},
		"script-title": {
			"label": "外文标题",
			"description": "非中文标题。开头使用ISO 639-1语言代码加上一个英文冒号。例如日语标题为：ja:标题名称。使用本字段则无需使用title字段。",
			"type": "line",
			"example": "ja:ウィキペディア"
		},
		"trans-title": {
			"label": "翻译标题",
			"description": "非中文标题的中文翻译",
			"type": "content"
		},
		"type": {
			"label": "类型",
			"description": "关于来源的媒体类型的附加信息（不常用）。例如：论文、小册子",
			"type": "content"
		},
		"format": {
			"label": "格式",
			"description": "网址链接到的文件的格式（使用'format'时需要'url'）；例如：PDF, DOC, XLS；一般的HTML格式不用填写",
			"type": "content"
		},
		"arxiv": {
			"label": "arXiv标识符",
			"description": "arXiv标识符，例如“0706.0001”",
			"type": "line",
			"example": "0706.0001"
		},
		"asin": {
			"label": "ASIN",
			"description": "亚马逊标准识别号码，10个数字组成。如有其它标识符则不建议使用。",
			"type": "line"
		},
		"asin-tld": {
			"label": "ASIN顶级域名",
			"description": "该ASIN在亚马逊网站顶级域名（即amazon.XX），例如：us、jp",
			"type": "line",
			"example": "jp"
		},
		"bibcode": {
			"label": "Bibcode",
			"description": "Bibliographic Reference Code (REFCODE)；19个字符组成。",
			"type": "line",
			"example": "1924MNRAS..84..308E"
		},
		"biorxiv": {
			"label": "biorXiv",
			"description": "biorXiv标识符；完整的doi",
			"type": "line"
		},
		"citeseerx": {
			"label": "CiteSeerX",
			"description": "CiteSeerX识别符",
			"type": "line"
		},
		"isbn": {
			"label": "ISBN",
			"description": "国际标准书号；尽可能使用13位ISBN",
			"type": "line",
			"example": "978-0-8126-9593-9"
		},
		"issn": {
			"label": "ISSN",
			"description": "国际标准连续出版物号（印刷）；8个字符；通常用连字符分成两组，每组4个字符，例如：2049-3630",
			"type": "line",
			"example": "2049-3630"
		},
		"eissn": {
			"label": "eISSN",
			"description": "国际标准连续出版物号（电子）；8个字符；通常用连字符分成两组，每组4个字符，例如：2049-3630",
			"type": "line"
		},
		"cn": {
			"label": "CN",
			"description": "中国国内统一连续出版物号",
			"type": "line"
		},
		"jfm": {
			"label": "jfm编码",
			"description": "Jahrbuch über die Fortschritte der Mathematik classification code",
			"type": "line",
			"example": "53.0144.01"
		},
		"hdl": {
			"label": "HDL",
			"description": "HDL标识符",
			"type": "line"
		},
		"jstor": {
			"label": "JSTOR",
			"description": "JSTOR标识符",
			"type": "line"
		},
		"lccn": {
			"label": "LCCN",
			"description": "美国国会图书馆控制号",
			"type": "line"
		},
		"mr": {
			"label": "MR",
			"description": "《数学评论》标识符",
			"type": "line"
		},
		"oclc": {
			"label": "OCLC",
			"description": "联机计算机图书馆中心号码",
			"type": "number"
		},
		"ol": {
			"label": "OL",
			"description": "开放图书馆标识符",
			"type": "line"
		},
		"osti": {
			"label": "OSTI",
			"description": "Office of Scientific and Technical Information标识符",
			"type": "line"
		},
		"pmc": {
			"label": "PMC",
			"description": "PubMed Center文章编号",
			"type": "number"
		},
		"pmid": {
			"label": "PMID",
			"description": "PubMed Unique Identifier",
			"type": "line"
		},
		"rfc": {
			"label": "RFC",
			"description": "Request for Comments编号",
			"type": "number"
		},
		"s2cid": {
			"label": "S2CID",
			"description": "S2CID标识符",
			"type": "line"
		},
		"ssrn": {
			"label": "SSRN",
			"description": "Social Science Research Network",
			"type": "line"
		},
		"zbl": {
			"label": "Zbl",
			"description": "Zentralblatt MATH期刊标识符",
			"type": "line"
		},
		"id": {
			"label": "id",
			"description": "其它标识符，可自由填入多个",
			"type": "line"
		},
		"quote": {
			"label": "引文",
			"description": "从来源处引用的相关文本",
			"type": "content"
		},
		"ref": {
			"label": "Ref",
			"description": "锚点的标识符，可使该引用能成为维基链接的目标；填入“harv”可生成适合harv和sfn模板的锚点。",
			"type": "line"
		},
		"postscript": {
			"label": "结尾标点",
			"description": "引用的结尾标点符号；如要移除标点，填入“none”。如果填写了'quote'参数，则忽略该参数",
			"type": "line",
			"default": "."
		},
		"last3": {
			"label": "姓3",
			"description": "第3名作者的姓氏（仅英文人名）；不要加入条目链接，如有条目请使用'author-link3'；",
			"type": "line"
		},
		"first3": {
			"label": "名3",
			"description": "第2名作者的名（仅英文人名）；不要加入条目链接，如有条目请使用'author-link2'；",
			"type": "line"
		},
		"last4": {
			"label": "姓4",
			"description": "第4名作者的姓氏（仅英文人名）；不要加入条目链接，如有条目请使用'author-link4'；",
			"type": "line"
		},
		"first4": {
			"label": "名4",
			"description": "第4名作者的名（仅英文人名）；不要加入条目链接，如有条目请使用'author-link4'；",
			"type": "line"
		},
		"last5": {
			"label": "姓5",
			"description": "第5名作者的姓氏（仅英文人名）；不要加入条目链接，如有条目请使用'author-link5'；",
			"type": "line"
		},
		"first5": {
			"label": "名5",
			"description": "第5名作者的名（仅英文人名）；不要加入条目链接，如有条目请使用'author-link5'；",
			"type": "line"
		},
		"last6": {
			"label": "姓6",
			"description": "第6名作者的姓氏（仅英文人名）；不要加入条目链接，如有条目请使用'author-link6'；",
			"type": "line"
		},
		"first6": {
			"label": "名6",
			"description": "第6名作者的名（仅英文人名）；不要加入条目链接，如有条目请使用'author-link6'；",
			"type": "line"
		},
		"last7": {
			"label": "姓7",
			"description": "第7名作者的姓氏（仅英文人名）；不要加入条目链接，如有条目请使用'author-link7'；",
			"type": "line"
		},
		"first7": {
			"label": "名7",
			"description": "第7名作者的名（仅英文人名）；不要加入条目链接，如有条目请使用'author-link7'；",
			"type": "line"
		},
		"last8": {
			"label": "姓8",
			"description": "第8名作者的姓氏（仅英文人名）；不要加入条目链接，如有条目请使用'author-link8'；",
			"type": "line"
		},
		"first8": {
			"label": "名8",
			"description": "第8名作者的名（仅英文人名）；不要加入条目链接，如有条目请使用'author-link8'；",
			"type": "line"
		},
		"last9": {
			"label": "姓9",
			"description": "第9名作者的姓氏（仅英文人名）；不要加入条目链接，如有条目请使用'author-link9'；",
			"type": "line"
		},
		"first9": {
			"label": "名9",
			"description": "第9名作者的名（仅英文人名）；不要加入条目链接，如有条目请使用'author-link9'；",
			"type": "line"
		},
		"last10": {
			"label": "姓10",
			"description": "第10名作者的姓氏（仅英文人名）；不要加入条目链接，如有条目请使用'author-link10'；",
			"type": "line"
		},
		"first10": {
			"label": "名10",
			"description": "第10名作者的名（仅英文人名）；不要加入条目链接，如有条目请使用'author-link10'；",
			"type": "line"
		},
		"last11": {
			"label": "姓11",
			"description": "第11名作者的姓氏（仅英文人名）；不要加入条目链接，如有条目请使用'author-link11'；",
			"type": "line"
		},
		"first11": {
			"label": "名11",
			"description": "第11名作者的名（仅英文人名）；不要加入条目链接，如有条目请使用'author-link11'；",
			"type": "line"
		},
		"editor2-last": {
			"label": "编者的姓2",
			"description": "第2名编者的姓（仅英文人名）。不要加入条目链接，如有条目请使用'editor-link2'；中文人名请使用'editor2'",
			"type": "line"
		},
		"editor2-first": {
			"label": "编者的名2",
			"description": "第2名编者的名（仅英文人名）。不要加入条目链接。",
			"type": "line"
		},
		"editor3-last": {
			"label": "编者的姓3",
			"description": "第3名编者的姓（仅英文人名）。不要加入条目链接，如有条目请使用'editor-link3'；中文人名请使用'editor2'",
			"type": "line"
		},
		"editor3-first": {
			"label": "编者的名3",
			"description": "第3名编者的名（仅英文人名）。不要加入条目链接。",
			"type": "line"
		},
		"editor4-last": {
			"label": "编者的姓4",
			"description": "第4名编者的姓（仅英文人名）。不要加入条目链接，如有条目请使用'editor-link4'",
			"type": "line"
		},
		"editor4-first": {
			"label": "编者的名4",
			"description": "第4名编者的名（仅英文人名）。不要加入条目链接。",
			"type": "line"
		},
		"editor5-last": {
			"label": "编者的姓5",
			"description": "第5名编者的姓（仅英文人名）。不要加入条目链接，如有条目请使用'editor-link5'",
			"type": "line"
		},
		"editor5-first": {
			"label": "编者的名5",
			"description": "第5名编者的名（仅英文人名）。不要加入条目链接。",
			"type": "line"
		},
		"editor6-last": {
			"label": "编者的姓6",
			"description": "第6名编者的姓（仅英文人名）。不要加入条目链接，如有条目请使用'editor-link6'",
			"type": "line"
		},
		"editor6-first": {
			"label": "编者的名6",
			"description": "第6名编者的名（仅英文人名）。不要加入条目链接。",
			"type": "line"
		},
		"editor7-last": {
			"label": "编者的姓7",
			"description": "第7名编者的姓（仅英文人名）。不要加入条目链接，如有条目请使用'editor-link7'",
			"type": "line"
		},
		"editor7-first": {
			"label": "编者的名7",
			"description": "第7名编者的名（仅英文人名）。不要加入条目链接。",
			"type": "line"
		},
		"editor8-last": {
			"label": "编者的姓8",
			"description": "第8名编者的姓（仅英文人名）。不要加入条目链接，如有条目请使用'editor-link8'",
			"type": "line"
		},
		"editor8-first": {
			"label": "编者的名8",
			"description": "第8名编者的名（仅英文人名）。不要加入条目链接。",
			"type": "line"
		},
		"editor9-last": {
			"label": "编者的姓9",
			"description": "第9名编者的姓（仅英文人名）。不要加入条目链接，如有条目请使用'editor-link9'",
			"type": "line"
		},
		"editor9-first": {
			"label": "编者的名9",
			"description": "第9名编者的名（仅英文人名）。不要加入条目链接。",
			"type": "line"
		},
		"author-mask": {
			"label": "作者替代",
			"description": "用破折号或文本替换第1名作者的姓名。填入数字值X可将破折号设置为X em空格宽；填入文本值可显示无尾部作者分隔符的文本（例如“with”）",
			"type": "string"
		},
		"author-link": {
			"label": "作者条目链接",
			"description": "关于作者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"author-link1",
				"author1-link"
			]
		},
		"author-link2": {
			"label": "作者条目链接2",
			"description": "关于第2名作者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"author2-link"
			]
		},
		"access-date": {
			"label": "网址访问日期",
			"description": "最后一次访问原始网址的日期",
			"type": "date",
			"suggested": true
		},
		"archive-url": {
			"label": "存档网址",
			"description": "网页的存档副本的网址，需要与“archive-date”参数一同使用",
			"type": "line"
		},
		"archive-date": {
			"label": "存档日期",
			"description": "网页的存档日期",
			"type": "date",
			"example": "2021-02-08"
		},
		"url-status": {
			"label": "网址状态",
			"description": "如网址有效，填入“live”；如网址失效，填入“dead”",
			"type": "line",
			"example": "dead"
		},
		"author-link3": {
			"label": "作者条目链接3",
			"description": "关于第3名作者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"author3-link"
			]
		},
		"author-link4": {
			"label": "作者条目链接4",
			"description": "关于第4名作者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"author4-link"
			]
		},
		"author-link5": {
			"label": "作者条目链接5",
			"description": "关于第5名作者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"author5-link"
			]
		},
		"author-link6": {
			"label": "作者条目链接6",
			"description": "关于第6名作者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"author6-link"
			]
		},
		"author-link7": {
			"label": "作者条目链接7",
			"description": "关于第7名作者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"author7-link"
			]
		},
		"author-link8": {
			"label": "作者条目链接8",
			"description": "关于第8名作者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"author8-link"
			]
		},
		"author-link9": {
			"label": "作者条目链接9",
			"description": "关于第9名作者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"author9-link"
			]
		},
		"editor2-link": {
			"label": "编者条目链接2",
			"description": "关于第2名编者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"editor-link2"
			]
		},
		"editor3-link": {
			"label": "编者条目链接3",
			"description": "关于第3名编者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"editor-link3"
			]
		},
		"editor4-link": {
			"label": "编者条目链接4",
			"description": "关于第4名编者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"editor-link4"
			]
		},
		"editor5-link": {
			"label": "编者条目链接5",
			"description": "关于第5名编者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"editor-link5"
			]
		},
		"editor6-link": {
			"label": "编者条目链接6",
			"description": "关于第6名编者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"editor-link6"
			]
		},
		"editor7-link": {
			"label": "编者条目链接7",
			"description": "关于第7名编者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"editor-link7"
			]
		},
		"editor8-link": {
			"label": "编者条目链接8",
			"description": "关于第8名编者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"editor-link8"
			]
		},
		"editor9-link": {
			"label": "编者条目链接9",
			"description": "关于第9名编者的现有维基百科条目的标题",
			"type": "wiki-page-name",
			"aliases": [
				"editor-link9"
			]
		},
		"name-list-style": {
			"label": "姓名列表样式",
			"description": "填入“amp”可将名字列表上最后两个人之间的分隔符分别改为“&”；设置为'vanc'可以以温哥华风格显示名字列表（需填写'vauthors'）",
			"type": "string",
			"deprecated": true
		},
		"chapter": {
			"label": "章节",
			"description": "来源的章节标题（显示效果不佳，不建议使用）",
			"type": "string"
		},
		"via": {
			"label": "内容提供者（如：数据库）",
			"description": "文章的提供者（不是出版商），通常是期刊文章的聚合者或资源库",
			"example": "JSTOR, Project MUSE, Elsevier Science Direct",
			"type": "string",
			"suggested": true
		},
		"url-access": {
			"label": "网址访问级别",
			"description": "对网址的访问限制进行分类（“registration”，“subscription”或“limited”）",
			"type": "string"
		},
		"bibcode-access": {
			"label": "Bibcode访问级别",
			"description": "如果全文可通过此Bibcode从ADS获得，请输入“free”。",
			"type": "string"
		},
		"doi-access": {
			"label": "DOI访问级别",
			"description": "如果通过DOI可以免费阅读全文，请输入“free”。",
			"type": "string"
		},
		"hdl-access": {
			"label": "HDL访问级别",
			"description": "如果通过HDL可以免费阅读全文，请输入“free”。",
			"type": "string"
		},
		"jstor-access": {
			"label": "JSTOR访问级别",
			"description": "如果通过JSTOR可以免费阅读全文，请输入“free”。",
			"type": "string"
		},
		"ol-access": {
			"label": "OpenLibrary访问级别",
			"description": "如果通过OpenLibrary可以免费阅读全文，请输入“free”。",
			"type": "string"
		},
		"osti-access": {
			"label": "OSTI访问级别",
			"description": "如果在OSTI上可以免费阅读全文，请输入“free”。",
			"type": "string"
		},
		"s2cid-access": {
			"label": "S2CID访问级别",
			"description": "如果通过S2CID可以免费阅读全文，请输入“free”。",
			"type": "string"
		},
		"vauthors": {
			"label": "温哥华风格作者",
			"description": "以逗号分隔的温哥华风格的作者姓名列表；将公司或机构的作者姓名放在双括号“(())”内。",
			"type": "line"
		},
		"display-authors": {
			"label": "显示作者量",
			"description": "显示的作者数量，默认全部显示；超过显示数量将以“et al.”代替",
			"type": "number"
		},
		"author-link10": {
			"aliases": [
				"author10-link"
			],
			"label": "作者条目链接10",
			"description": "关于第10名作者的现有维基百科条目的标题"
		},
		"author-link11": {
			"aliases": [
				"author11-link"
			],
			"label": "作者条目链接11",
			"description": "关于第11名作者的现有维基百科条目的标题"
		},
		"author": {
			"aliases": [
				"author1"
			],
			"label": "姓名",
			"description": "作者的姓名（适用于中文人名）；不要加入条目链接，如有条目请使用'author-link'；"
		},
		"author2": {
			"label": "姓名2",
			"description": "第2名作者的姓名（适用于中文人名）；不要加入条目链接，如有条目请使用'author-link2'；"
		},
		"author3": {
			"label": "姓名3",
			"description": "第3名作者的姓名（适用于中文人名）；不要加入条目链接，如有条目请使用'author-link3'；"
		},
		"author4": {
			"label": "姓名4",
			"description": "第4名作者的姓名（适用于中文人名）；不要加入条目链接，如有条目请使用'author-link4'；"
		},
		"author5": {
			"label": "姓名5",
			"description": "第5名作者的姓名（适用于中文人名）；不要加入条目链接，如有条目请使用'author-link5'；"
		},
		"author6": {
			"label": "姓名6",
			"description": "第6名作者的姓名（适用于中文人名）；不要加入条目链接，如有条目请使用'author-link6'；"
		},
		"author7": {
			"label": "姓名7",
			"description": "第7名作者的姓名（适用于中文人名）；不要加入条目链接，如有条目请使用'author-link7'；"
		},
		"author8": {
			"label": "姓名8",
			"description": "第8名作者的姓名（适用于中文人名）；不要加入条目链接，如有条目请使用'author-link8'；"
		},
		"author9": {
			"label": "姓名9",
			"description": "第9名作者的姓名（适用于中文人名）；不要加入条目链接，如有条目请使用'author-link9'；"
		},
		"author10": {
			"label": "姓名10",
			"description": "第10名作者的姓名（适用于中文人名）；不要加入条目链接，如有条目请使用'author-link10'；"
		},
		"author11": {
			"label": "姓名11",
			"description": "第11名作者的姓名（适用于中文人名）；不要加入条目链接，如有条目请使用'author-link11'；"
		},
		"translator": {
			"label": "译者",
			"description": "作品的译者"
		},
		"editor": {
			"label": "编者姓名",
			"description": "编者的姓名（支持中文人名）。不要加入条目链接，如有条目请使用'editor-link'"
		},
		"editor2": {
			"label": "编者姓名2",
			"description": "第2名编者的姓名（支持中文人名）。不要加入条目链接，如有条目请使用'editor-link2'"
		},
		"editor3": {
			"label": "编者姓名3",
			"description": "第3名编者的姓名（支持中文人名）。不要加入条目链接，如有条目请使用'editor-link3'"
		},
		"editor4": {
			"label": "编者姓名4",
			"description": "第4名编者的姓名（支持中文人名）。不要加入条目链接，如有条目请使用'editor-link4'"
		},
		"editor5": {
			"label": "编者姓名5",
			"description": "第5名编者的姓名（支持中文人名）。不要加入条目链接，如有条目请使用'editor-link5'"
		},
		"editor6": {
			"label": "编者姓名6",
			"description": "第6名编者的姓名（支持中文人名）。不要加入条目链接，如有条目请使用'editor-link6'"
		},
		"editor7": {
			"label": "编者姓名7",
			"description": "第7名编者的姓名（支持中文人名）。不要加入条目链接，如有条目请使用'editor-link7'"
		},
		"editor8": {
			"label": "编者姓名8",
			"description": "第8名编者的姓名（支持中文人名）。不要加入条目链接，如有条目请使用'editor-link8'"
		},
		"editor9": {
			"label": "编者姓名9",
			"description": "第9名编者的姓名（支持中文人名）。不要加入条目链接，如有条目请使用'editor-link9'"
		},
		"website": {
			"aliases": [
				"work"
			],
			"label": "网站名称",
			"description": "来源网站的名称，可以加入条目链接",
			"example": "[[维基百科]]",
			"type": "content",
			"suggested": true
		}
	},
	"paramOrder": [
		"last",
		"first",
		"author",
		"author-link",
		"last2",
		"first2",
		"author2",
		"author-link2",
		"last3",
		"first3",
		"author3",
		"author-link3",
		"last4",
		"first4",
		"author4",
		"author-link4",
		"last5",
		"first5",
		"author5",
		"author-link5",
		"last6",
		"first6",
		"author6",
		"author-link6",
		"last7",
		"first7",
		"author7",
		"author-link7",
		"last8",
		"first8",
		"author8",
		"author-link8",
		"last9",
		"first9",
		"author9",
		"author-link9",
		"last10",
		"first10",
		"author10",
		"author-link10",
		"last11",
		"first11",
		"author11",
		"author-link11",
		"display-authors",
		"author-mask",
		"name-list-style",
		"vauthors",
		"date",
		"year",
		"orig-year",
		"editor-last",
		"editor-first",
		"editor",
		"editor-link",
		"editor2-last",
		"editor2-first",
		"editor2",
		"editor2-link",
		"editor3-last",
		"editor3-first",
		"editor3",
		"editor3-link",
		"editor4-last",
		"editor4-first",
		"editor4",
		"editor4-link",
		"editor5-last",
		"editor5-first",
		"editor5",
		"editor5-link",
		"editor6-last",
		"editor6-first",
		"editor6",
		"editor6-link",
		"editor7-last",
		"editor7-first",
		"editor7",
		"editor7-link",
		"editor8-last",
		"editor8-first",
		"editor8",
		"editor8-link",
		"editor9-last",
		"editor9-first",
		"editor9",
		"editor9-link",
		"translator",
		"others",
		"title",
		"script-title",
		"trans-title",
		"url",
		"url-status",
		"format",
		"department",
		"website",
		"chapter",
		"type",
		"series",
		"language",
		"edition",
		"location",
		"publisher",
		"publication-place",
		"publication-date",
		"page",
		"at",
		"no-pp",
		"arxiv",
		"asin",
		"asin-tld",
		"bibcode",
		"biorxiv",
		"citeseerx",
		"doi",
		"doi-broken-date",
		"isbn",
		"issn",
		"eissn",
		"cn",
		"hdl",
		"jfm",
		"jstor",
		"lccn",
		"mr",
		"oclc",
		"ol",
		"osti",
		"pmc",
		"pmid",
		"rfc",
		"s2cid",
		"ssrn",
		"zbl",
		"id",
		"url-access",
		"archive-url",
		"archive-date",
		"access-date",
		"quote",
		"postscript",
		"ref",
		"via",
		"bibcode-access",
		"doi-access",
		"hdl-access",
		"jstor-access",
		"ol-access",
		"osti-access",
		"s2cid-access"
	],
	"maps": {
		"citoid": {
			"title": "title",
			"url": "url",
			"subject": "title",
			"publicationTitle": "website",
			"blogTitle": "website",
			"forumTitle": "website",
			"seriesTitle": "website",
			"websiteTitle": "website",
			"publisher": "publisher",
			"date": "date",
			"PMCID": "pmc",
			"PMID": "pmid",
			"oclc": "oclc",
			"series": "series",
			"accessDate": "access-date",
			"DOI": "doi",
			"language": "language",
			"contributor": "others",
			"author": [
				[
					"first",
					"last"
				],
				[
					"first2",
					"last2"
				],
				[
					"first3",
					"last3"
				],
				[
					"first4",
					"last4"
				],
				[
					"first5",
					"last5"
				],
				[
					"first6",
					"last6"
				],
				[
					"first7",
					"last7"
				],
				[
					"first8",
					"last8"
				],
				[
					"first9",
					"last9"
				]
			],
			"editor": [
				[
					"editor-first",
					"editor-last"
				],
				[
					"editor2-first",
					"editor2-last"
				],
				[
					"editor3-first",
					"editor3-last"
				],
				[
					"editor4-first",
					"editor4-last"
				],
				[
					"editor5-first",
					"editor5-last"
				],
				[
					"editor6-first",
					"editor6-last"
				],
				[
					"editor7-first",
					"editor7-last"
				],
				[
					"editor8-first",
					"editor8-last"
				],
				[
					"editor9-first",
					"editor9-last"
				]
			]
		}
	},
	"format": "{{_ |_=_}}"
}
</templatedata>

==參見==
* [[Wikipedia:列明来源]]：格式指引
* [[Wikipedia:模板消息/条目来源]]：相關模板
* [[Template:Cite_news]]：引用來源為新聞時
* [[Template:Cite_book]]：引用來源為書籍時
* [[Template:Cite_journal]]：引用來源為期刊時
* [[Help:引文格式1错误]]：因為填寫參數有問題而產生紅字提示的解答指南
* [[:Template:Citation Style documentation/deprecated]]：如果在Cite web模板內使用某些「舊」參數，條目會被自動加入「[[:Category:含有过时参数的引用的页面]]」，改用建議的參數名稱後就不會被加入該分類。

<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:頁面訊息模板|{{PAGENAME}}]]
[[Category:引用模板]]
}}</includeonly>