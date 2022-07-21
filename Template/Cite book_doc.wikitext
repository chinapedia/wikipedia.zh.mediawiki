{{Documentation subpage}}
{{high-use|129541}}
{{lua|模块:Citation/CS1}}
<!-- 在以下編輯說明文件 -->
{{Citation Style documentation/cs1}}
本模板是用於在維基百科內[[WP:CITE|引用資料來源]]，特別為引用書籍而設計。

== 使用方式 ==
若以英文填寫，所有欄位名務必為'''[[小寫字母|小寫]]'''。

若要使用請拷貝空白的模板代碼，並用「'''|'''」（直線）字元分開各個欄位。請刪除任何沒有使用到的欄位，以免在編輯視窗中出現空白。

在填寫 [[ISBN]]、[[OCLC]] 和 [[DOI]] 時不需要使用任何模板或魔術字。可使用 <code>編號方式</code> 代替。例如，輸入 <code>isbn=數字</code>，而不要輸入 <code>id=ISBN</code>。

{{csdoc|usage}}

{{csdoc|usage common}}
'''引用一本有作者的書'''
<code><nowiki>{{cite book |last= |first= |date= |title= |url= |location= |publisher= |page= |isbn= |author-link= }}</nowiki></code>

'''引用一本沒有作者的書'''
<code><nowiki>{{cite book |title= |url= |location= |publisher= |page= |date= |isbn= }}</nowiki></code>

'''引用已存檔的在線圖書'''
<code><nowiki>{{cite book |last= |first= |date= |title= |url= |location= |publisher= |isbn= |archiveurl= |archivedate= |dead-url= }}</nowiki></code>

'''引用由外語寫的書'''
<code><nowiki>{{cite book |last= |first= |date= |title= |trans-title= |url= |location= |publisher= |isbn= |language= }}</nowiki></code>

'''To cite and quote an archived, two-author, foreign language book re-published as a PDF on an information aggregation service requiring a subscription'''
<code><nowiki>{{cite book |last1= |first1= |last2= |first2= |date= |title= |trans-title= |url= |format= |location= |publisher= |isbn= |archiveurl= |archivedate= |via= |subscription= |quote= |dead-url= |language= }}</nowiki></code>
{{end}}

{{csdoc|usage full}}
<code><nowiki>{{cite book |last1= |first1= |author-link1= |last2= |first2= |author-link2= |last3= |first3= |author-link3= |last4= |first4= |author-link4= |last5= |first5= |author-link5= |display-authors= |author-mask= |last-author-amp= |date= |year= |orig-year= |chapter= |script-chapter= |trans-chapter= |chapter-url= |chapter-format= |editor1-last= |editor1-first= |editor1-link= |editor2-last= |editor2-first= |editor2-link= |editor3-last= |editor3-first= |editor3-link= |editor4-last= |editor4-first= |editor4-link= |editor5-last= |editor5-first= |editor5-link= |display-editors= |title= |script-title= |trans-title= |url= |dead-url= |format= |type= |series= |language= |volume= |others= |edition= |location= |publisher= |publication-date= |page= |pages= |at= |nopp= |arxiv= |asin= |bibcode= |doi= |doi-broken-date= |isbn= |issn= |jfm= |jstor= |lccn= |mr= |oclc= |ol= |osti= |pmc= |pmid= |rfc= |ssrn= |zbl= |id= |archiveurl= |archivedate= |accessdate= |via= |registration= |subscription= |lay-summary= |lay-source= |lay-date= |quote= |name-list-format= |mode= |postscript= |ref= }}</nowiki></code>
{{end}}

{| class="wikitable"
|+直式排列的全部參數
! 參數 !! 先決條件 !! 簡要說明 !! 直式列表
|-
|| last1 ||  || may also use "last"; for additional authors, "last2", "last3", etc. || rowspan="74" style="vertical-align:top;" | <pre style="margin:0px; border:none;">
{{cite book
|last1=
|first1=
|author-link1=
|author-mask1=
|last2=
|first2=
|display-authors=
|last-author-amp=
|date=
|year=
|orig-year=
|chapter=
|script-chapter=
|trans-chapter=
|chapter-url=
|chapter-format=
|editor1-last=
|editor1-first=
|editor1-link=
|editor1-mask=
|display-editors=
|translator1-last=
|translator1-first=
|translator1-link=
|translator1-mask=
|title=
|script-title=
|trans-title=
|url=
|dead-url=
|format=
|type=
|series=
|language=
|volume=
|others=
|edition=
|location=
|publisher=
|publication-date=
|page=
|pages=
|at=
|nopp=
|arxiv=
|asin=
|bibcode=
|doi=
|doi-broken-date=
|isbn=
|issn=
|jfm=
|jstor=
|lccn=
|mr=
|oclc=
|ol=
|osti=
|pmc=
|pmid=
|rfc=
|ssrn=
|zbl=
|id=
|archiveurl=
|archivedate=
|accessdate=
|via=
|registration=
|subscription=
|lay-summary=
|lay-source=
|lay-date=
|quote=
|name-list-format=
|mode=
|postscript=
|ref=
}}
</pre>
|-
| first1 || last or last1 || may also use "first"; for additional authors, "first2", "first3", etc.
|-
|| author-link1 || last or last1 || may also use "author-link"
|-
|| author-mask1 || last or last1 || may also use "author-mask"
|-
|| last2 || last1 ||
|-
|| first2 || last2 ||
|-
|| display-authors || last or last1 ||
|-
|| last-author-amp ||  last or last1 ||
|-
|| date || ||
|-
|| year || ||
|-
|| orig-year || year or date ||
|-
|| chapter || || do not wikilink "chapter" if "chapterurl" is provided
|-
|| script-chapter || ||
|-
|| trans-chapter || chapter  or script-chapter ||
|-
|| chapter-url || chapter or script-chapter ||
|-
|| chapter-format || chapter-url ||
|-
|| editor1-last ||   || may also use "editor-last"
|-
|| editor1-first ||  editor1-last || may also use 'editor-first"
|-
|| editor1-link ||  editor1-last || may also use "editor-link"
|-
|| editor1-mask ||  editor1-last
|-
|| display-editors || ||
|-
|| title || ||
|-
|| script-title || ||
|-
|| trans-title || title or script-title ||
|-
|| url || title or script-title ||
|-
|| dead-url || ||
|-
|| format || url ||
|-
|| type || ||
|-
|| series || ||
|-
|| language || ||
|-
|| volume || ||
|-
|| others || ||
|-
|| edition || ||
|-
|| location || publisher ||
|-
|| publisher || ||
|-
|| publication-date || ||
|-
|| page || || choose one: "page", "pages", or "at"
|-
|| pages || || choose one: "page", "pages", or "at". Use when content on multiple pages supports the article text.
|-
|| at || || choose one: "page", "pages", or "at"
|-
|| nopp || page or pages || 原用于<code>page=封面</code>时去除“第...页”，中文版本来打算改成去除冒号为句号，实则无效。
|-
|| arxiv || ||
|-
|| asin || ||
|-
|| bibcode || ||
|-
|| doi || ||
|-
|| doi-broken-date ||  doi ||
|-
|| isbn || || '''always include ISBN''', if one has been assigned
|-
|| issn || || 
|-
|| jfm || ||
|-
|| jstor || ||
|-
|| lccn || ||
|-
|| mr || ||
|-
|| oclc || ||
|-
|| ol || ||
|-
|| osti || ||
|-
|| pmc || ||
|-
|| pmid || ||
|-
|| rfc || ||
|-
|| ssrn || ||
|-
|| zbl || ||
|-
|| id || ||
|-
|| archive-url ||  archive-date, url ||
|-
|| archive-date ||  archive-url ||
|-
|| access-date || url ||
|-
|| via || ||
|-
|| registration || ||
|-
|| subscription || ||
|-
|| lay-summary || ||
|-
|| lay-source || lay-summary ||
|-
|| lay-date || lay-summary ||
|-
|| quote || ||
|-
|| name-list-format || || <code>vanc</code>模仿[[溫哥華參考文獻格式]]
|-
|| mode || || <code>cs1</code> or <code>cs2</code>
|-
|| postscript || ||
|-
|| ref || ||
|-
| colspan="4" style="text-align: center " | 如果在'''先決條件'''列中列出了字段名，那麼它就是左側字段的先決條件。
|}

== 欄位變數 ==
===維基連結===
大部分的欄位都可以加入維基內部連結（例如：''title'' = <nowiki>[[條目|書名]]</nowiki>），但建議僅加入維基百科現有條目的內部連結。所有維基連結中'''不應'''包含任何會干擾模板運作的符號，請使用正常的括號 <code>()</code>，而不要使用 <code><nowiki><>[]{}</nowiki></code>。

===說明欄位===
====<small>欄位變數</small>====
<div style="font-size：90%;">
以下的欄位說明中，部份欄位有親子連動關係，親子欄位必須搭配使用才會正常顯示：
*親欄位
**子欄位 &mdash; 必須和親欄位'''同時'''使用（若親欄位沒有填寫則可忽略）
**或：''子欄位2'' &mdash; 可以取代親欄位使用（若已使用親欄位則可忽略）
</div>

====說明====
* '''author'''：作者姓名，適合使用在作者的姓名（或翻譯後姓名）為中文的時候，例如：張愛玲、喬治·華盛頓。可填寫下方的 ''authorlink'' 欄位加入內部連結。
* '''last'''：作者姓氏，由於與名字中間有空格，建議使用在以原文（通常是英文）表現作者姓氏時。例如：Johnson。請不要直接加入維基連結，改用 ''authorlink'' 欄位。
** '''first'''：作者名字，由於與姓氏中間有空格，建議使用在以原文（通常是英文）表現作者名字時。例如：Jack。也可加入中間姓名（middle name）。請不要直接加入維基連結，改用 ''authorlink'' 欄位。
*** ''last'' 和 ''first'' 僅適合用在用英文（或其他類似語言）書寫的作者姓名，中文或翻譯姓名請改用 ''author'' 欄位。
** '''authorlink'''：維基百科中關於作者的條目名稱。請僅輸入已存在的條目。請不要獨立使用這個欄位，務必僅在 ''author'' 或 ''first'' 和 ''last'' 有填寫時使用。
** '''coauthors'''：其他合作作者的完整姓名，使用頓號（、）分開。（例如：王大明、李小華；或：Joe Bloggs、John F. Kennedy、H. R. Dent）
* '''editor'''：書籍的編輯 / 編者姓名。會自動在姓名後加上「'''(編)'''」。
* '''translator'''：書籍的譯者 / 譯者姓名。。
* '''others'''：其他書籍的貢獻者，例如：由王大明翻譯；或：插圖由李小華繪製。
* '''title'''：書籍的標題。'''這是唯一必填的欄位。'''可以連結至維基百科內已存在的條目。英文書籍可加入斜體符號（<code><nowiki>''book title''</nowiki></code>），中文請勿加入斜體。
* '''url'''：若為線上書籍，請填寫網址。若已在 ''title'' 欄位加入內部連結則無法使用。
** '''format'''：書籍格式，例如：PDF、HTML 等。若無特別的格式則不必填寫。
** '''accessdate'''：造訪線上書籍網址的完整日期。格式為：XXXX年XX月XX日或YYYY-MM-DD<s>，可自由加上內部連結，例如：[[2007年]][[2月20日]]</s><small>（根据2014年[[WP:格式手册]]的'''新规定'''，不再对日期添加链接）</small>。若書籍沒有網址則不必填寫。
* '''edition'''：當書籍有特定的版本時使用，例如：1997年6月第二刷。
* '''series'''：當書籍是一系列出版品中的其中一部份時使用。
* '''origdate'''：原始版本的出版日期。格式為：XXXX年XX月XX日或YYYY-MM-DD<s>，可自由加上內部連結，例如：[[2007年]][[2月20日]]</s><small>（根据2014年[[WP:格式手册]]的'''新规定'''，不再对日期添加链接）</small>。
** 或：'''origyear'''：原始版本的出版年份，不須加上「年」這個字，只需填寫數字即可。和 '''origmonth'''：原始版本的出版月份，不須加上「月」這個字，只需填寫數字即可。兩個欄位都不可加上內部連結，若是有特定的日期，請改用 ''origdate''。
* '''date'''或'''year'''：引用版本的出版年、出版年月或出版年月日。格式為：XXXX年XX月XX日或YYYY-MM-DD<s>，可自由加上內部連結，例如：[[2007年]][[2月20日]]</s><small>（根据2014年[[WP:格式手册]]的'''新规定'''，不再对日期添加链接）</small>。
** <s>或：'''year'''：引用版本的出版年份，不須加上「年」這個字，只需填寫數字即可。和 '''month'''：引用版本的出版月份，不須加上「月」這個字，只需填寫數字即可。兩個欄位都不可加上內部連結，若是有特定的日期，請改用 ''date''。</s><small>（'''month'''已棄用，系統無法辨識，若要填寫出版年月或出版年月日，請改用'''year'''或'''date'''）</small>
* '''publisher'''：出版社。請避免加入「出版社」、「公司」、「有限公司」等字樣。
** '''location'''：出版地點。
* '''language'''：書籍的語言，以[[ISO 639-1代碼表]]來標示語言，一書多語（比方說中英對照）可用半形逗號區隔並增加語言，例如：''en, zh''。
* '''isbn'''：[[國際標準書號]]（ISBN），例如：''1-111-22222-9''。
* '''unified'''：[[统一书号]]，例如：''7201·85''。
* '''oclc'''：[[線上電腦圖書館中心]]（Online Computer Library Center）編號，例如：''3185581''。
* '''doi'''：[[數位物件識別號]]（digital object identifier，DOI），例如：''<nowiki>10.1016/j.coi.2004.08.001</nowiki>''。
* '''id'''：若以上的欄位不敷使用或不適合，可加入書籍其他的相關認證編號。您必須指定您加入的編號系統名稱，使用相關模板如 {{tl|ISSN}}、{{tl|NLC}}、{{tl|NCID}}、{{tl|NDL}}等，可多选。
* '''pages'''：''<nowiki>第5&ndash;7頁</nowiki>''：引用頁數的起訖。這是指引用內容所在的頁數，而非整本書的總頁數。
* '''chapter'''：書籍的特定章節。
** '''chapterurl'''：線上書籍的特定章節網址。若有的話必須和 ''url'' 欄位的內容是在同一個網站上。
* '''quote'''：書籍中特定句子的引言。

==範例==
;僅有書名：
:<code><nowiki>* {{cite book | title=神祕之書 }}</nowiki></code>

:* {{cite book | title = 神祕之書 }}

;年份和書名
:<code><nowiki>* {{cite book | title=神祕之書 | year=1901 }}</nowiki></code>

:* {{cite book | title = 神祕之書 | year = 1901 }}

;基本樣式（英文書籍）：
:<code><nowiki>* {{cite book |first=Joe |last=Bloggs |authorlink=Joe Bloggs |year=1974 |title=Book of Bloggs }}</nowiki></code>

:* {{cite book |first=Joe |last=Bloggs |authorlink=Joe Bloggs |year=1974 |title=Book of Bloggs }}

;基本樣式（中文書籍）：
:<code><nowiki>* {{cite book |author=張愛玲 |authorlink=張愛玲 |year=1948 |title=半生緣 }}</nowiki></code>

:* {{cite book |author=張愛玲 |authorlink=張愛玲 |year=1948 |title=半生緣 }}

;基本樣式，包含網址
:<code><nowiki>* {{cite book |last=Bloggs |first=Joe |authorlink=Joe Bloggs |year=1974 |title=Book of Bloggs |edition=1st |url=http://en.wikipedia.org/ |accessdate=[[2006年]][[2月17日]] }}</nowiki></code>

:* {{cite book |last=Bloggs |first=Joe |authorlink=Joe Bloggs |year=1974 |title=Book of Bloggs |edition=1st |url=http://en.wikipedia.org/ |accessdate=2006年2月17日 }}

;三位作者、書名、維基內部連結、書籍版本
:<code><nowiki>* {{cite book |last=Bloggs |first=Joe |authorlink=Joe Bloggs | author12=John Smith | author2=Jim Smythe |title=[[A Thousand Acres|1000 Acres]] |edition=第二版 }}</nowiki></code>

:* {{cite book |last=Bloggs |first=Joe |authorlink=Joe Bloggs | author12=John Smith | author2=Jim Smythe |title=[[A Thousand Acres|1000 Acres]] |edition=第二版 }}

;三種語言、書名、作者、出版社、出版日期
:<code><nowiki>* {{cite book |author=谷學 |title=全球論語：中英日對照讀本 |publisher=上海譯文 |date=2007-08-01 |language=zh, en, ja |isbn=9787532743360 }}</nowiki></code>

:* {{cite book |author=谷學 |title=全球論語：中英日對照讀本 |publisher=上海譯文 |date=2007-08-01 |language=zh, en, ja |isbn=9787532743360 }}

;不含日的日期、書名和出版社的維基內部連結、編號、頁數、出版地點
:<code><nowiki>* {{cite book | author1=Bruce R. Cordell | author2=Jeff Grubb | author3=David Noonan | title=[[Manual of the Planes]] | publisher=[[Wizards of the Coast]] | location=Timbuktu | isbn=0786918500 | pages=第134-137頁 |date=2001年9月}}</nowiki></code>

:* {{cite book | author1=Bruce R. Cordell | author2=Jeff Grubb | author3=David Noonan | title=[[Manual of the Planes]] | publisher=[[Wizards of the Coast]] | location=Timbuktu | isbn=0786918500 | pages=第134-137頁 |date=2001年9月}}

;初版（原版）的日期、其他語言、插畫家
:<code><nowiki>* {{cite book | last=Bloggs | first=Joe | origyear=1463 | year=1974 | title=Book of Bloggs | edition=初版 | others=由 Smith 繪製插畫 | language=de | url=http://en.wikipedia.org/ | accessdate=2006年2月17日 }}</nowiki></code>

:* {{cite book | last=Bloggs | first=Joe | origyear=1463 | year=1974 | title=Book of Bloggs | edition=初版 | others=由 Smith 繪製插畫 | language=de | url=http://en.wikipedia.org/ | accessdate=2006年2月17日 }}

;使用[[數位物件識別號|DOI]]
:<code><nowiki>*{{cite book
|last=Mumford
|first=David
|authorlink=David Mumford
|year=1999
|title=The Red Book of Varieties and Schemes: Includes the Michigan Lectures (1974) on Curves and Their Jacobians
|edition=第二版
|publisher=Springer-Verlag
|doi=10.1007/b62130
|isbn=354063293X
}}</nowiki></code>

:*{{cite book
|last=Mumford
|first=David
|authorlink=David Mumford
|year=1999
|title=The Red Book of Varieties and Schemes: Includes the Michigan Lectures (1974) on Curves and Their Jacobians
|edition=第二版
|publisher=Springer-Verlag
|doi=10.1007/b62130
|isbn=354063293X
}}

==測試==
參見 [[Template:cite book/regression tests]]。
==工具==
*http://www.ottobib.com/ --输入ISBN号，即可获得完整的cite book信息。
==引用格式指南==
一些英文中合作作者的引用格式指南，僅供參考：
* [[MLA格式手册]]
* [[APA格式]]
* [http://www.liunet.edu/cwis/cwp/library/workshop/citchi.htm Chicago Manual of Style]
* [http://www.liunet.edu/cwis/cwp/library/workshop/cittur.htm Turabian].
* [[哈佛参考文献格式]]
* [[文后参考文献著录规则|GB/T 7714]]

==模板数据==
{{TemplateDataHeader}}
<templatedata>
{
	"description": "本模板是用於在維基百科內引用資料來源，特別為引用書籍而設計。",
	"params": {
		"url": {
			"label": "URL",
			"description": "若為線上書籍，請填寫網址。若已在 ''title'' 欄位加入內部連結則無法使用。",
			"type": "string",
			"aliases": [
				"URL"
			]
		},
		"title": {
			"label": "標題",
			"description": "書籍的標題。'''這是唯一必填的欄位。'''可以連結至維基百科內已存在的條目。英文書籍可加入斜體符號（''book title''），中文請勿加入斜體。",
			"type": "string",
			"required": true
		},
		"last": {
			"label": "作者/姓氏",
			"description": "作者姓氏，由於與名字中間有空格，建議使用在以原文（通常是英文）表現作者姓氏時。例如：Johnson。請不要直接加入維基連結，改用 ''authorlink'' 欄位。",
			"aliases": [
				"author",
				"  author1",
				"  authors",
				"  last1"
			],
			"suggested": true
		},
		"first": {
			"label": "名字",
			"description": "作者名字，由於與姓氏中間有空格，建議使用在以原文（通常是英文）表現作者名字時。例如：Jack。也可加入中間姓名（middle name）。請不要直接加入維基連結，改用 ''authorlink'' 欄位。",
			"aliases": [
				"first1"
			],
			"suggested": true
		},
		"authorlink": {
			"label": "作者條目",
			"description": "維基百科中關於作者的條目名稱。請僅輸入已存在的條目。請不要獨立使用這個欄位，務必僅在 ''author'' 或 ''first'' 和 ''last'' 有填寫時使用。",
			"type": "wiki-page-name",
			"aliases": [
				"authorlink1"
			]
		},
		"last2": {
			"label": "第二作者姓氏",
			"description": "第二作者姓氏。如須加入維基連結，請用 ''authorlink2'' 欄位。",
			"aliases": [
				"author2"
			]
		},
		"first2": {
			"label": "第二作者名字",
			"description": "第二作者名字或名字首字母縮寫。如須加入維基連結，請用 ''authorlink2'' 欄位。"
		},
		"authorlink2": {
			"label": "第二作者條目",
			"description": "維基百科中關於第二作者的條目名稱。請僅輸入已存在的條目。請不要獨立使用這個欄位，務必僅在 ''author2'' 或 ''first2'' 和 ''last2'' 有填寫時使用。",
			"type": "wiki-page-name"
		},
		"last3": {
			"label": "第三作者姓氏",
			"description": "第三作者姓氏。如須加入維基連結，請用 ''authorlink3'' 欄位。",
			"aliases": [
				"author3"
			]
		},
		"first3": {
			"label": "第三作者名字",
			"description": "第三作者名字或名字首字母縮寫。如須加入維基連結，請用 ''authorlink3'' 欄位。"
		},
		"authorlink3": {
			"label": "第三作者條目",
			"description": "維基百科中關於第三作者的條目名稱。",
			"type": "wiki-page-name",
			"aliases": [
				"author3-link"
			]
		},
		"last4": {
			"label": "第四作者姓氏",
			"description": "第四作者姓氏。如須加入維基連結，請用 ''authorlink4'' 欄位。",
			"aliases": [
				"author4"
			]
		},
		"first4": {
			"label": "第四作者名字",
			"description": "第四作者名字或名字首字母縮寫。如須加入維基連結，請用 ''authorlink4'' 欄位。"
		},
		"authorlink4": {
			"label": "第四作者條目",
			"description": "維基百科中關於第四作者的條目名稱。",
			"type": "wiki-page-name",
			"aliases": [
				"author4-link"
			]
		},
		"last5": {
			"label": "第五作者姓氏",
			"description": "第五作者姓氏。如須加入維基連結，請用 ''authorlink5'' 欄位。",
			"aliases": [
				"author5"
			]
		},
		"first5": {
			"label": "第五作者名字",
			"description": "第五作者名字或名字首字母縮寫。如須加入維基連結，請用 ''authorlink5'' 欄位。"
		},
		"authorlink5": {
			"label": "第五作者條目",
			"description": "維基百科中關於第五作者的條目名稱。",
			"type": "wiki-page-name",
			"aliases": [
				"author5-link"
			]
		},
		"last6": {
			"label": "第六作者姓氏",
			"description": "第六作者姓氏。如須加入維基連結，請用 ''authorlink6'' 欄位。",
			"aliases": [
				"author6"
			]
		},
		"first6": {
			"label": "第六作者名字",
			"description": "第六作者名字或名字首字母縮寫。如須加入維基連結，請用 ''authorlink6'' 欄位。",
			"aliases": [
				"author6-link"
			]
		},
		"authorlink6": {
			"label": "第六作者條目",
			"description": "維基百科中關於第六作者的條目名稱。",
			"type": "wiki-page-name"
		},
		"last7": {
			"label": "第七作者姓氏",
			"description": "第七作者姓氏。如須加入維基連結，請用 ''authorlink7'' 欄位。",
			"aliases": [
				"author7"
			]
		},
		"first7": {
			"label": "第七作者名字",
			"description": "第七作者名字或名字首字母縮寫。如須加入維基連結，請用 ''authorlink7'' 欄位。"
		},
		"authorlink7": {
			"label": "第七作者條目",
			"description": "維基百科中關於第七作者的條目名稱。",
			"type": "wiki-page-name",
			"aliases": [
				"author7-link"
			]
		},
		"last8": {
			"label": "第八作者姓氏",
			"description": "第八作者姓氏。如須加入維基連結，請用 ''authorlink8'' 欄位。",
			"aliases": [
				"author8"
			]
		},
		"first8": {
			"label": "第八作者名字",
			"description": "第八作者名字或名字首字母縮寫。如須加入維基連結，請用 ''authorlink8'' 欄位。"
		},
		"authorlink8": {
			"label": "第八作者條目",
			"description": "維基百科中關於第八作者的條目名稱。",
			"type": "wiki-page-name",
			"aliases": [
				"author8-link"
			]
		},
		"last9": {
			"label": "第九作者姓氏",
			"description": "第九作者姓氏。如須加入維基連結，請用 ''authorlink9'' 欄位。",
			"aliases": [
				"author9"
			]
		},
		"first9": {
			"label": "第九作者名字",
			"description": "第九作者名字或名字首字母縮寫。如須加入維基連結，請用 ''authorlink9'' 欄位。"
		},
		"authorlink9": {
			"label": "第九作者條目",
			"description": "維基百科中關於第九作者的條目名稱。",
			"type": "wiki-page-name",
			"aliases": [
				"author9-link"
			]
		},
		"date": {
			"label": "出版日期",
			"description": "引用版本的出版日期。格式為：YYYY-MM-DD，根據2014年[[WP:格式手册]]的'''新规定'''，請勿加上內部連結。",
			"type": "string"
		},
		"work": {
			"label": "作品",
			"description": "引用書籍文本所出現的作品標題",
			"type": "string"
		},
		"publisher": {
			"label": "出版社",
			"description": "出版社。請避免加入「出版社」、「公司」、「有限公司」等字樣。",
			"type": "string",
			"suggested": true
		},
		"accessdate": {
			"label": "URL訪問日期",
			"description": "原URL的訪問日期。",
			"type": "string"
		},
		"others": {
			"label": "其他",
			"description": "其他書籍的貢獻者，例如：由王大明翻譯；或：插圖由李小華繪製。",
			"type": "string"
		},
		"year": {
			"label": "出版年份",
			"description": "引用版本的出版年份，不須加上「年」這個字，只需填寫數字即可。",
			"type": "string",
			"suggested": true
		},
		"origyear": {
			"label": "原出版年份",
			"description": "原始版本的出版年份，不須加上「年」這個字，只需填寫數字即可。",
			"type": "string"
		},
		"isbn": {
			"label": "ISBN",
			"description": "[[國際標準書號]]（ISBN），例如：''1-111-22222-9''。",
			"type": "string",
			"suggested": true
		},
		"editor-last": {
			"label": "編輯姓氏",
			"description": "編輯姓氏。如須加入維基連結，請用 ''editor-link'' 欄位。",
			"aliases": [
				"editor",
				"  editor1-last",
				"  editors"
			]
		},
		"editor-first": {
			"label": "編輯名字",
			"description": "編輯名字或名字首字母縮寫。如須加入維基連結，請用 ''editor-link'' 欄位。",
			"aliases": [
				"editor1-first"
			]
		},
		"editor-link": {
			"label": "編輯條目",
			"description": "維基百科中關於編輯的條目名稱。",
			"aliases": [
				"editor1-link"
			],
			"type": "wiki-page-name"
		},
		"editor2-last": {
			"label": "第二編輯姓氏",
			"description": "第二編輯姓氏。如須加入維基連結，請用 ''editor-link2'' 欄位。",
			"type": "string"
		},
		"editor2-first": {
			"label": "第二編輯名字",
			"description": "第二編輯名字或名字首字母縮寫。如須加入維基連結，請用 ''editor-link2'' 欄位。",
			"type": "string"
		},
		"editor2-link": {
			"label": "第二編輯條目",
			"description": "維基百科中關於第二編輯的條目名稱。",
			"type": "wiki-page-name"
		},
		"editor3-last": {
			"label": "第三編輯姓氏",
			"description": "第三編輯姓氏。如須加入維基連結，請用 ''editor-link3'' 欄位。",
			"type": "string"
		},
		"editor3-first": {
			"label": "第三編輯名字",
			"description": "第三編輯名字或名字首字母縮寫。如須加入維基連結，請用 ''editor-link3'' 欄位。",
			"type": "string"
		},
		"editor3-link": {
			"label": "第三編輯條目",
			"description": "維基百科中關於第三編輯的條目名稱。",
			"type": "wiki-page-name"
		},
		"editor4-last": {
			"label": "第四編輯姓氏",
			"description": "第四編輯姓氏。如須加入維基連結，請用 ''editor-link4'' 欄位。",
			"type": "string"
		},
		"editor4-first": {
			"label": "第四編輯名字",
			"description": "第四編輯名字或名字首字母縮寫。如須加入維基連結，請用 ''editor-link4'' 欄位。",
			"type": "string"
		},
		"editor4-link": {
			"label": "第四編輯條目",
			"description": "維基百科中關於第四編輯的條目名稱。",
			"type": "wiki-page-name"
		},
		"editor5-last": {
			"label": "第五編輯姓氏",
			"description": "第五編輯姓氏。如須加入維基連結，請用 ''editor-link5'' 欄位。",
			"type": "string"
		},
		"editor5-first": {
			"label": "第五編輯名字",
			"description": "第五編輯名字或名字首字母縮寫。如須加入維基連結，請用 ''editor-link5'' 欄位。",
			"type": "string"
		},
		"editor5-link": {
			"label": "第五編輯條目",
			"description": "維基百科中關於第五編輯的條目名稱。",
			"type": "wiki-page-name"
		},
		"editor6-last": {
			"label": "第六編輯姓氏",
			"description": "第六編輯姓氏。如須加入維基連結，請用 ''editor-link6'' 欄位。",
			"type": "string"
		},
		"editor6-first": {
			"label": "第六編輯名字",
			"description": "第六編輯名字或名字首字母縮寫。如須加入維基連結，請用 ''editor-link6'' 欄位。",
			"type": "string"
		},
		"editor6-link": {
			"label": "第六編輯條目",
			"description": "維基百科中關於第六編輯的條目名稱。",
			"type": "wiki-page-name"
		},
		"editor7-last": {
			"label": "第七編輯姓氏",
			"description": "第七編輯姓氏。如須加入維基連結，請用 ''editor-link7'' 欄位。",
			"type": "string"
		},
		"editor7-first": {
			"label": "第七編輯名字",
			"description": "第七編輯名字或名字首字母縮寫。如須加入維基連結，請用 ''editor-link7'' 欄位。",
			"type": "string"
		},
		"editor7-link": {
			"label": "第七編輯條目",
			"description": "維基百科中關於第七編輯的條目名稱。",
			"type": "wiki-page-name"
		},
		"editor8-last": {
			"label": "第八編輯姓氏",
			"description": "第八編輯姓氏。如須加入維基連結，請用 ''editor-link8'' 欄位。",
			"type": "string"
		},
		"editor8-first": {
			"label": "第八編輯名字",
			"description": "第八編輯名字或名字首字母縮寫。如須加入維基連結，請用 ''editor-link8'' 欄位。",
			"type": "string"
		},
		"editor8-link": {
			"label": "第八編輯條目",
			"description": "維基百科中關於第八編輯的條目名稱。",
			"type": "wiki-page-name"
		},
		"editor9-last": {
			"label": "第九編輯姓氏",
			"description": "第九編輯姓氏。如須加入維基連結，請用 ''editor-link9'' 欄位。",
			"type": "string"
		},
		"editor9-first": {
			"label": "第九編輯名字",
			"description": "第九編輯名字或名字首字母縮寫。如須加入維基連結，請用 ''editor-link9'' 欄位。",
			"type": "string"
		},
		"editor9-link": {
			"label": "第九編輯條目",
			"description": "維基百科中關於第九編輯的條目名稱。",
			"type": "wiki-page-name"
		},
		"edition": {
			"label": "版本",
			"description": "當書籍有特定的版本時使用，例如：1997年6月第二刷。",
			"type": "string"
		},
		"series": {
			"label": "系列編號",
			"description": "當書籍是一系列出版品中的其中一部份時使用。",
			"aliases": [
				"version"
			],
			"type": "string"
		},
		"volume": {
			"label": "卷號",
			"description": "當書籍是一系列書卷的其中一卷時使用。",
			"type": "string"
		},
		"location": {
			"label": "出版地點",
			"description": "出版地點。",
			"aliases": [
				"place"
			],
			"type": "string",
			"suggested": true
		},
		"publication-place": {
			"label": "出版地點",
			"description": "如果同時指定 ''location'' （或 ''place''）及 ''publication-place'' 欄位，則前者會移到標題前，並標上「寫於」。",
			"type": "string"
		},
		"publication-date": {
			"label": "出版日期",
			"description": "當出版日期和著作日期不同時使用。",
			"type": "string"
		},
		"page": {
			"label": "頁數",
			"description": "第5–7頁：引用頁數的起訖。這是指引用內容所在的頁數，而非整本書的總頁數。",
			"type": "string"
		},
		"pages": {
			"label": "頁數",
			"description": "5–7：引用頁數的起訖。這是指引用內容所在的頁數，而非整本書的總頁數。",
			"type": "string",
			"suggested": true
		},
		"nopp": {
			"label": "無pp",
			"description": "原用于“page=封面”时去除“第...页”，中文版本来打算改成去除冒号为句号，实则无效。",
			"type": "string"
		},
		"at": {
			"label": "書內部分",
			"description": "當頁數（''page'' 或 ''pages''）不適用時使用。",
			"type": "string"
		},
		"translator-last": {
			"label": "譯者姓氏",
			"description": "編輯姓氏。如須加入維基連結，請用 ''translator-link'' 欄位。",
			"aliases": [
				"translator",
				"  translator1-last",
				"  translator-last1"
			]
		},
		"translator-first": {
			"label": "譯者名字",
			"description": "譯者名字或名字首字母縮寫。如須加入維基連結，請用 ''translator-link'' 欄位。",
			"aliases": [
				"translator1-first"
			]
		},
		"translator-link": {
			"label": "譯者條目",
			"description": "維基百科中關於譯者的條目名稱。",
			"aliases": [
				"translator1-link",
				"translator-link1"
			],
			"type": "wiki-page-name"
		},
		"translator2-last": {
			"label": "第二譯者姓氏",
			"description": "第二譯者姓氏。如須加入維基連結，請用 ''translator-link2'' 欄位。",
			"type": "string"
		},
		"translator2-first": {
			"label": "第二譯者名字",
			"description": "第二譯者名字或名字首字母縮寫。如須加入維基連結，請用 ''translator-link2'' 欄位。",
			"type": "string"
		},
		"translator2-link": {
			"label": "第二譯者條目",
			"description": "維基百科中關於第二譯者的條目名稱。",
			"type": "wiki-page-name"
		},
		"translator3-last": {
			"label": "第三譯者姓氏",
			"description": "第三譯者姓氏。如須加入維基連結，請用 ''translator-link3'' 欄位。",
			"type": "string"
		},
		"translator3-first": {
			"label": "第三譯者名字",
			"description": "第三譯者名字或名字首字母縮寫。如須加入維基連結，請用 ''translator-link3'' 欄位。",
			"type": "string"
		},
		"translator3-link": {
			"label": "第三譯者條目",
			"description": "維基百科中關於第三譯者的條目名稱。",
			"type": "wiki-page-name"
		},
		"translator4-last": {
			"label": "第四譯者姓氏",
			"description": "第四譯者姓氏。如須加入維基連結，請用 ''translator-link4'' 欄位。",
			"type": "string"
		},
		"translator4-first": {
			"label": "第四譯者名字",
			"description": "第四譯者名字或名字首字母縮寫。如須加入維基連結，請用 ''translator-link4'' 欄位。",
			"type": "string"
		},
		"translator4-link": {
			"label": "第四譯者條目",
			"description": "維基百科中關於第四譯者的條目名稱。",
			"type": "wiki-page-name"
		},
		"translator5-last": {
			"label": "第五譯者姓氏",
			"description": "第五譯者姓氏。如須加入維基連結，請用 ''translator-link5'' 欄位。",
			"type": "string"
		},
		"translator5-first": {
			"label": "第五譯者名字",
			"description": "第五譯者名字或名字首字母縮寫。如須加入維基連結，請用 ''translator-link5'' 欄位。",
			"type": "string"
		},
		"translator5-link": {
			"label": "第五譯者條目",
			"description": "維基百科中關於第五譯者的條目名稱。",
			"type": "wiki-page-name"
		},
		"translator6-last": {
			"label": "第六譯者姓氏",
			"description": "第六譯者姓氏。如須加入維基連結，請用 ''translator-link6'' 欄位。",
			"type": "string"
		},
		"translator6-first": {
			"label": "第六譯者名字",
			"description": "第六譯者名字或名字首字母縮寫。如須加入維基連結，請用 ''translator-link6'' 欄位。",
			"type": "string"
		},
		"translator6-link": {
			"label": "第六譯者條目",
			"description": "維基百科中關於第六譯者的條目名稱。",
			"type": "wiki-page-name"
		},
		"translator7-last": {
			"label": "第七譯者姓氏",
			"description": "第七譯者姓氏。如須加入維基連結，請用 ''translator-link7'' 欄位。",
			"type": "string"
		},
		"translator7-first": {
			"label": "第七譯者名字",
			"description": "第七譯者名字或名字首字母縮寫。如須加入維基連結，請用 ''translator-link7'' 欄位。",
			"type": "string"
		},
		"translator7-link": {
			"label": "第七譯者條目",
			"description": "維基百科中關於第七譯者的條目名稱。",
			"type": "wiki-page-name"
		},
		"translator8-last": {
			"label": "第八譯者姓氏",
			"description": "第八譯者姓氏。如須加入維基連結，請用 ''translator-link8'' 欄位。",
			"type": "string"
		},
		"translator8-first": {
			"label": "第八譯者名字",
			"description": "第八譯者名字或名字首字母縮寫。如須加入維基連結，請用 ''translator-link8'' 欄位。",
			"type": "string"
		},
		"translator8-link": {
			"label": "第八譯者條目",
			"description": "維基百科中關於第八譯者的條目名稱。",
			"type": "wiki-page-name"
		},
		"translator9-last": {
			"label": "第九譯者姓氏",
			"description": "第九譯者姓氏。如須加入維基連結，請用 ''translator-link9'' 欄位。",
			"type": "string"
		},
		"translator9-first": {
			"label": "第九譯者名字",
			"description": "第九譯者名字或名字首字母縮寫。如須加入維基連結，請用 ''translator-link9'' 欄位。",
			"type": "string"
		},
		"translator9-link": {
			"label": "第九譯者條目",
			"description": "維基百科中關於第九譯者的條目名稱。",
			"type": "wiki-page-name"
		},
		"language": {
			"label": "語言",
			"description": "書籍的語言。",
			"type": "string"
		},
		"script-title": {
			"label": "外文標題",
			"description": "當標題為非拉丁文字或非漢字時使用（如阿拉伯文字、希伯來文字等），有助瀏覽器顯示外文字形。格式為：ISO639-1標準中的二字母代碼，後加半形冒號，之後是原外文標題。例如，「|script-title=ar:」後寫出阿拉伯字母標題。",
			"type": "string"
		},
		"trans-title": {
			"label": "翻譯標題",
			"description": "中文標題。如果引用的是外文出版物，建議使用 ''language'' 欄位指定語言。",
			"type": "string"
		},
		"chapter": {
			"label": "章節",
			"description": "書籍的特定章節。",
			"type": "string"
		},
		"trans-chapter": {
			"label": "翻譯章節標題",
			"description": "中文章節標題名稱。如果引用的是外文出版物，建議使用 ''language'' 欄位指定語言。",
			"type": "string"
		},
		"chapterurl": {
			"label": "章節URL",
			"description": "線上書籍的特定章節網址。若有的話必須和 ''url'' 欄位的內容是在同一個網站上。",
			"aliases": [
				"chapter-url"
			],
			"type": "string"
		},
		"type": {
			"label": "類別",
			"description": "關於出版物媒介類別的額外訊息。",
			"type": "string"
		},
		"format": {
			"label": "格式",
			"description": "''url'' 欄位所指向的檔案格式，例如PDF、DOC、XLS等。無須指定HTML。",
			"type": "string"
		},
		"arxiv": {
			"label": "arXiv識別號",
			"description": "科學論文電子預印本在arXiv上的識別號",
			"type": "string"
		},
		"asin": {
			"label": "ASIN",
			"description": "Amazon Standard Identification Number; 10 characters",
			"type": "string"
		},
		"asin-tld": {
			"label": "ASIN TLD",
			"description": "ASIN top-level domain for Amazon sites other than the US",
			"type": "string"
		},
		"bibcode": {
			"label": "Bibcode",
			"description": "Bibliographic Reference Code (REFCODE); 19 characters",
			"type": "string"
		},
		"citeseerx": {
			"label": "CiteSeerX",
			"description": "CiteSeerX identifier; found after the 'doi=' query parameter",
			"type": "string"
		},
		"doi": {
			"label": "DOI",
			"description": "[[數位物件識別號]]（digital object identifier，DOI），例如：''10.1016/j.coi.2004.08.001</nowiki>''。",
			"type": "string"
		},
		"doi_brokendate": {
			"label": "DOI無效日期",
			"description": "DOI被發現無效時的日期",
			"type": "string"
		},
		"issn": {
			"label": "ISSN",
			"description": "International Standard Serial Number，共8個字符，可分為兩組，各4個字符，用短橫分隔。",
			"type": "string"
		},
		"jfm": {
			"label": "jfm編碼",
			"description": "Jahrbuch über die Fortschritte der Mathematik分類編號",
			"type": "string"
		},
		"jstor": {
			"label": "JSTOR",
			"description": "JSTOR識別號",
			"type": "string"
		},
		"lccn": {
			"label": "LCCN",
			"description": "Library of Congress Control Number",
			"type": "string"
		},
		"mr": {
			"label": "MR",
			"description": "Mathematical Reviews識別號",
			"type": "string"
		},
		"oclc": {
			"label": "OCLC",
			"description": "[[線上電腦圖書館中心]]（Online Computer Library Center）編號，例如：''3185581''。",
			"type": "string"
		},
		"ol": {
			"label": "OL",
			"description": "Open Library識別號",
			"type": "string"
		},
		"osti": {
			"label": "OSTI",
			"description": "Office of Scientific and Technical Information識別號",
			"type": "string"
		},
		"pmc": {
			"label": "PMC",
			"description": "PubMed Center條目號",
			"type": "string"
		},
		"pmid": {
			"label": "PMID",
			"description": "PubMed Unique識別號",
			"type": "string"
		},
		"rfc": {
			"label": "RFC",
			"description": "Request for Comments number",
			"type": "string"
		},
		"ssrn": {
			"label": "SSRN",
			"description": "Social Science Research Network",
			"type": "string"
		},
		"zbl": {
			"label": "Zbl",
			"description": "Zentralblatt MATH期刊識別號",
			"type": "string"
		},
		"id": {
			"label": "id",
			"description": "若以上的欄位不敷使用或不適合，可加入書籍其他的相關認證編號。您必須指定您加入的編號系統名稱，使用相關模板如 {{tl|ISSN}}。",
			"type": "string"
		},
		"archiveurl": {
			"label": "存檔URL",
			"description": "網頁存檔的URL，在原URL無效或目標內容已改變時使用。須同時指定 ''archivedate''",
			"type": "string"
		},
		"archivedate": {
			"label": "存檔日期",
			"description": "原URL存檔日期",
			"type": "string"
		},
		"deadurl": {
			"label": "無效URL",
			"description": "設為 ''no'' 時會調整標題格式。當URL已存檔但原目標仍有效時使用",
			"type": "string"
		},
		"quote": {
			"label": "引文",
			"description": "書籍中特定句子的引文。",
			"type": "string"
		},
		"ref": {
			"label": "Ref",
			"description": "錨點識別號。在正文中可用維基連結指向具有此識別號的完整參考訊息。''harv'' 是特殊值，配合harv模板使用",
			"type": "string"
		},
		"separator": {
			"label": "分隔符",
			"description": "分隔多個作者、編者等所用的標點符號。如須使用半形空格，請用&#32;。切勿使用星號、冒號或井號。",
			"type": "string",
			"default": "."
		},
		"postscript": {
			"label": "結尾符",
			"description": "參考引用的結尾標點符號。此項在 ''quote'' 已指定時會被忽略。",
			"type": "string",
			"default": "."
		},
		"layurl": {
			"label": "外行概要URL",
			"description": "對引用出版物的非專業概要或述評的URL連結",
			"aliases": [
				"laysummary"
			],
			"type": "string"
		},
		"laysource": {
			"label": "外行概要標題",
			"description": "非專業概要的標題，須配合 ''layurl'' 使用。",
			"type": "string"
		},
		"laydate": {
			"label": "外行概要日期",
			"description": "非專業概要的日期。",
			"type": "string"
		},
		"author-mask": {
			"label": "作者掩碼",
			"description": "把第一作者的姓名改為連接號或其他文字。要改為 ''n'' 個連接號，設此項為 ''n''；要改為文字並去除緊接其後的作者分隔符，設此項為所需文字。",
			"type": "string"
		},
		"author-name-separator": {
			"label": "作者姓名分隔符",
			"description": "指定作者姓氏與名字之間的分隔符，默認為半形逗號加半形空格。如須使用半形空格，請用&#32;。切勿使用星號、冒號或井號。",
			"type": "string",
			"default": ", "
		},
		"author-separator": {
			"label": "作者分隔符",
			"description": "指定作者和作者之間的分隔符，默認為半形分號加半形空格。如須使用半形空格，請用&#32;。切勿使用星號、冒號或井號。",
			"type": "string",
			"default": "; "
		},
		"display-authors": {
			"label": "顯示的作者數目",
			"description": "顯示的作者數目。例如，如果已指定6名作者的姓名而此項設為3，那麼將只會顯示首3名作者的姓名，並在其後加上「等」一字。",
			"type": "number",
			"aliases": [
				"displayauthors"
			],
			"default": "8"
		},
		"lastauthoramp": {
			"label": "最後作者分隔符",
			"description": "指定最後兩個作者姓名之間的分隔符。",
			"type": "string"
		},
		"unified": {
			"label": "统一书号",
			"description": "中华人民共和国原国内统一书号（CSBN）。",
			"example": "7201·85",
			"type": "string"
		}
	},
	"maps": {
		"citoid": {
			"edition": "edition",
			"title": "chapter",
			"bookTitle": "title",
			"publicationTitle": "title",
			"series": "series",
			"url": "url",
			"publisher": "publisher",
			"date": "date",
			"place": "location",
			"ISSN": [
				"issn"
			],
			"ISBN": [
				"isbn"
			],
			"PMCID": "pmc",
			"PMID": "pmid",
			"oclc": "oclc",
			"pages": "pages",
			"volume": "volume",
			"DOI": "doi",
			"language": "language",
			"contributor": [
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
				]
			]
		}
	},
	"format": "inline"
}
</templatedata>

== 參見 ==
* [[WP:CITE]]: 格式指南
* [[Wikipedia:列明来源]]：格式指引
* [[Wikipedia:模板消息/条目来源]]：相關模板
* [[Template:Cite web]]：引用來源為網頁時
* [[Template:Cite news]]：引用來源為新聞時
* [[Template:Cite journal]]：引用來源為期刊時
* [[:Category:引用模板]]：其他的引用模板
* [[Template:Cite isbn]]
* [[Template:Rp]]：几处引用了同一本书籍的不同页码时可用此模板标注页码。
* {{tl|Harvtxt}}或{{tl|Harvnb}}（{{tl|sfn}}或{{tl|cfn}}透過{{tl|Harvtxt}}或{{tl|Harvnb}}可正常與{{tl|cite book}}等對應）<!-- 例如[[人工智能]]，追查結果 -->
* {{tl|clref}}（{{tl|sfn}}或{{tl|cfn}}透過{{tl|clref}}包覆{{tl|cite book}}等，可正常對應）

<includeonly>
<!-- 頁面分類 -->
[[Category:引用模板|{{PAGENAME}}]]
</includeonly>