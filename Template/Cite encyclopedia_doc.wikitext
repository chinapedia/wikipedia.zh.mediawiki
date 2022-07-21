<includeonly>{{lua|模块:Citation/CS1}}<!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{Documentation subpage}}</noinclude>
<!-- 在本行下編輯模板說明 -->
{{Citation Style documentation/cs1}}
引用百科全書的資料時請用本模板。
所有參數'''必須'''為小寫英文字母，可複製一空白版本使用。

==用法==

;常用版本，橫書
<tt><nowiki>{{cite encyclopedia |year= |title = |encyclopedia= |publisher= |location= |id= }}</nowiki></tt>

;詳盡版本，橫書
<tt><nowiki>{{cite encyclopedia |last= |first= |author= |authorlink= |coauthors= |editor= |encyclopedia= |title= |url= |accessdate= |accessyear= |accessmonth= |edition= |date= |year= |month= |publisher= |volume= |location= |id= |doi= |pages= |quote= }}</nowiki></tt>

;詳盡版本，橫書（設定本日日期為存取日期）
<tt><nowiki>{{cite encyclopedia |last= |first= |author= |authorlink= |coauthors= |editor= |encyclopedia= |title= |url= |accessdate=</nowiki>{{CURRENTYEAR}}年{{CURRENTMONTH}}月{{CURRENTDAY}}日<nowiki> |accessyear= |accessmonth= |edition= |date= |year= |month= |publisher= |volume= |location= |id= |doi= |pages= |quote= }}</nowiki></tt>

{| cellpadding="0" cellspacing="6"
! 詳盡版本，橫書 !! 常用版本，直書
|- width="50%"
|
<pre>
{{cite encyclopedia
 | last = 
 | first = 
 | author = 
 | authorlink = 
 | coauthors = 
 | editor = 
 | encyclopedia =
 | title = 
 | url = 
 | accessdate = 
 | accessyear = 
 | accessmonth = 
 | edition = 
 | date = 
 | year = 
 | month = 
 | publisher = 
 | volume =
 | location = 
 | id = 
 | doi =
 | pages = 
 | quote = 
}}
</pre>
| style="vertical-align: top;" |
<pre>
{{cite encyclopedia
 | year = 
 | title = 
 | encyclopedia =
 | publisher = 
 | location = 
 | id = 
}}
</pre>
|}

</pre>
== 欄位變數 ==
===維基連結===
大部分的欄位都可以加入維基內部連結（例如：''title'' = <nowiki>[[條目|百科全書名]]</nowiki>），但建議僅加入維基百科現有條目的內部連結。所有維基連結中'''不應'''包含任何會干擾模板運作的符號，請使用正常的括號 <code>()</code>，而不要使用 <code><nowiki><>[]{}</nowiki></code>。

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
* '''editor'''：書籍的編輯 / 編者姓名。由於本欄位沒有預設的文字，因此使用者必須自行加入「'''（編輯）'''」等附註文字。
* '''encyclopedia'''：書籍的標題。
* '''title'''：書籍的標題。'''這是唯一必填的欄位。'''可以連結至維基百科內已存在的條目。英文書籍可加入斜體符號（<code><nowiki>''book title''</nowiki></code>），中文請勿加入斜體。
* '''url'''：若為線上書籍，請填寫網址。若已在 ''title'' 欄位加入內部連結則無法使用。
** '''format'''：書籍格式，例如：PDF、HTML 等。若無特別的格式則不必填寫。
** '''accessdate'''：造訪線上書籍網址的完整日期。格式為：XXXX年XX月XX日，可自由加上內部連結，例如：[[2007年]][[2月20日]]。若書籍沒有網址則不必填寫。
* '''edition'''：當書籍有特定的版本時使用，例如：1997年6月第二刷。
* '''series'''：當書籍是一系列出版品中的其中一部份時使用。
* '''origdate'''：原始版本的出版日期。格式為：XXXX年XX月XX日，可自由加上內部連結，例如：[[2007年]][[2月20日]]。
** 或：'''origyear'''：原始版本的出版年份，不須加上「年」這個字，只需填寫數字即可。和 '''origmonth'''：原始版本的出版月份，不須加上「月」這個字，只需填寫數字即可。兩個欄位都不可加上內部連結，若是有特定的日期，請改用 ''origdate''。
* '''date'''：引用版本的出版日期。格式為：XXXX年XX月XX日，可自由加上內部連結，例如：[[2007年]][[2月20日]]。
** 或：'''year'''：引用版本的出版年份，不須加上「年」這個字，只需填寫數字即可。和 '''month'''：引用版本的出版月份，不須加上「月」這個字，只需填寫數字即可。兩個欄位都不可加上內部連結，若是有特定的日期，請改用 ''date''。
* '''publisher'''：出版社。請避免加入「出版社」、「公司」、「有限公司」等字樣。
** '''location'''：出版地點。
* '''language'''：書籍的語言。
* '''isbn'''：[[國際標準書號]]（ISBN），例如：''1-111-22222-9''。
* '''unified'''：[[统一书号]]，例如：''7201·85''。
* '''oclc'''：[[線上電腦圖書館中心]]（Online Computer Library Center）編號，例如：''3185581''。
* '''doi'''：[[數位物件識別號]]（digital object identifier，DOI），例如：''<nowiki>10.1016/j.coi.2004.08.001</nowiki>''。
* '''id'''：若以上的欄位不敷使用或不適合，可加入書籍其他的相關認證編號。您必須指定您加入的編號系統名稱，使用相關模板如 {{tl|ISSN}}。
* '''pages'''：''<nowiki>第5&ndash;7頁</nowiki>''：引用頁數的起訖。這是指引用內容所在的頁數，而非整本書的總頁數。
* '''chapter'''：書籍的特定章節。
** '''chapterurl'''：線上書籍的特定章節網址。若有的話必須和 ''url'' 欄位的內容是在同一個網站上。
* '''quote'''：書籍中特定句子的引言。

== 重定向 ==
*{{tl|Cite dictionary}}

<includeonly>
<!-- 本行下加入模板的分類 -->
[[Category:百科全書來源模板|{{PAGENAME}}]]
</includeonly>