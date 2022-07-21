{{for2|{{fake}}模板|{{tl|citation needed}}}}
{{translating|time=2012-01-19}}<noinclude>
{{template doc page viewed directly}}
</noinclude>
<!-- EDIT TEMPLATE DOCUMENTATION BELOW THIS LINE -->
{{esoteric}}
{{lua|模块:Citation/CS1}}
'''Citation'''模板是一个多功能模板，可用于引用书籍、期刊、收集工作、专利或网站。此模板的设立目的，是要成为一个可供所有引用用途的模板，其格式为[[哈佛参考文献格式]]。与其他引用模板一样，这个模板既可以用于脚注（用于{{tag|ref}}tag中），又可以用于列出来源的章节中。这个模板使用了与[[Help:引文格式1|引文格式1]]模板相同的[[WP:Lua|Lua]]语言，并且带有将显示的格式变更为[[Help:引文格式2|引文格式2]]的参数。

在使用正确参数的情况下，这个模板将会产生与{{Tl|Cite book}}和{{Tl|Cite web}}等其他引用模板相同的输出，但它和这些模板相比存在一个重大例外：默认情况下，这个引用模板会在引用模板默认使用句点的地方自动使用逗号；任何类型的模板都可以通过使用可选参数选择使用句点或逗号。

无论是使用了哪种引用模板，抑或是没有使用任何引用模板，在被保存并呈现的文本中，一篇文章的所有引用都应该有相同的格式。

注意：
* 所有参数名称都必须为[[小写字母]]。
* 不可见Unicode空格字符（参见[[:en:Help:CS1 errors#invisible_char|列表]]）将返回错误信息。请删除无意添加的不可见字符，并将有意添加的不可见字符替换为对应HTML实体（如<code>&amp;ZeroWidthSpace;</code>）。

==简单引用==
本章节会介绍这个模板最常用的参数。你可以复制下方的水平表格或垂直表格并从完整列表中添加额外参数。模板中参数的间距和顺序不会影响最终呈现的文本。

<code><nowiki>{{Citation |last= |first= |year= |title= |publisher= |publication-place= |page= |url= |access-date=}}</nowiki></code>

{| class="wikitable"
|-
| <pre>{{Citation
| last        =
| first       =
| year        =
| title       =
| publisher   =
| publication-place =
| page        =
| url         =
| access-date =
}}</pre>
|}
* '''last'''：作者的姓。不要与'''author'''同时使用。
* '''first'''：作者的名。
* '''year'''：出版年份。除非{{para|date}}同时指定了年份和月份，否则必须与[[:Template:Harvard citation]]中的链接同时使用。
* '''title'''：出版物名称。若为网络参考资料则会强制使用。
* '''publisher'''：出版社名称。英文字眼如''Publishers'', ''Co.'', ''Inc.'', ''Ltd.''等应省略，但保留''Books''或''Press''。通常不应填写有维基百科自身文章的期刊，例如《[[告示牌_(雜誌)|告示牌_]]和《[[新闻周刊]]》''。
** '''publication-place'''（或'''place'''、'''location''')：出版城市。如果在标题页出现多个城市，选择第1个城市或出版商的总部所在地。如果出版物的名称指定了出版地点（如《[[纽约时报]]》、《[[印度时报]]》，省略之。）
* '''page'''：用于引用文章的某一页。请在页数前添加“p.”。不要和'''pages'''同时使用。
* '''url'''：项目可被访问的线上位置的[[URL]]。若此url包含双引号，请将之编码为“%22”。
** '''access-date'''：URL被访问的日期<ref group="n" name="dates" />。

===例子===
{| class="wikitable"
|-
| <pre>{{Citation
| last      = Turner
| first     = Orsamus
| title     = History of the pioneer settlement of
Phelps and Gorham's purchase, and Morris' reserve
| publisher = William Alling
| place     = Rochester, New York
| year      = 1851
| ol        = 7120924W
}}
</pre>
| {{Citation
| last      = Turner
| first     = Orsamus
| title     = History of the pioneer settlement of Phelps and Gorham's purchase, and Morris' reserve
| publisher = William Alling
| place     = Rochester, New York
| year      = 1851
| ol        = 7120924W
}}
|}


==Template Data==
{{notice|This template data section needs to be edited. It includes deprecated parameters and does not include parameters that were added in the Lua updates. It also includes a mix of patent and non-patent parameters.}}

{{TemplateDataHeader}}
<templatedata>
{
	"description": "The Citation template generates a citation for a book, periodical, contribution in a collective work, patent, or a web page. It determines the citation type by examining which parameters are used.",
	"params": {
		"1": {
			"label": "1",
			"type": "string",
			"required": false
		},
		"2": {
			"label": "2",
			"type": "string",
			"required": false
		},
		"3": {
			"label": "3",
			"type": "string",
			"required": false
		},
		"last": {
			"label": "author surname",
			"type": "string",
			"description": "surname of the author of the cited material"
		},
		"first": {
			"label": "author given name",
			"type": "string",
			"description": "given name (first name) of the author of the cited material"
		},
		"title": {
			"label": "title of source",
			"type": "string",
			"description": "Title of source; displays in italics."
		},
		"date": {
			"label": "date of source",
			"type": "string",
			"description": "Full date of source being referenced in the same format as other publication dates in the citations.[1] Do not wikilink. Displays after the authors and enclosed in parentheses. If there is no author, then displays after publisher."
		},
		"url": {
			"label": "url of source",
			"type": "string",
			"description": "URL of an online location where the text of the publication can be found."
		},
		"inventor-surname": {
			"label": "inventor-surname",
			"type": "string",
			"required": false
		},
		"inventor1-surname": {
			"label": "inventor1-surname",
			"type": "string",
			"required": false
		},
		"inventor-last": {
			"label": "inventor-last",
			"type": "string",
			"required": false
		},
		"inventor1-last": {
			"label": "inventor1-last",
			"type": "string",
			"required": false
		},
		"inventor": {
			"label": "inventor",
			"type": "string",
			"required": false
		},
		"invent1": {
			"label": "invent1",
			"type": "string",
			"required": false
		},
		"invent-1": {
			"label": "invent-1",
			"type": "string",
			"required": false
		},
		"country-code": {
			"label": "country-code",
			"type": "string",
			"required": false
		},
		"inventor2-surname": {
			"label": "inventor2-surname",
			"type": "string",
			"required": false
		},
		"inventor2-last": {
			"label": "inventor2-last",
			"type": "string",
			"required": false
		},
		"inventor2": {
			"label": "inventor2",
			"type": "string",
			"required": false
		},
		"invent2": {
			"label": "invent2",
			"type": "string",
			"required": false
		},
		"inventor3-surname": {
			"label": "inventor3-surname",
			"type": "string",
			"required": false
		},
		"inventor3-last": {
			"label": "inventor3-last",
			"type": "string",
			"required": false
		},
		"inventor3": {
			"label": "inventor3",
			"type": "string",
			"required": false
		},
		"invent3": {
			"label": "invent3",
			"type": "string",
			"required": false
		},
		"inventor4-surname": {
			"label": "inventor4-surname",
			"type": "string",
			"required": false
		},
		"inventor4-last": {
			"label": "inventor4-last",
			"type": "string",
			"required": false
		},
		"inventor4": {
			"label": "inventor4",
			"type": "string",
			"required": false
		},
		"invent4": {
			"label": "invent4",
			"type": "string",
			"required": false
		},
		"inventor-given": {
			"label": "inventor-given",
			"type": "string",
			"required": false
		},
		"inventor1-given": {
			"label": "inventor1-given",
			"type": "string",
			"required": false
		},
		"inventor-first": {
			"label": "inventor-first",
			"type": "string",
			"required": false
		},
		"inventor1-first": {
			"label": "inventor1-first",
			"type": "string",
			"required": false
		},
		"inventor2-given": {
			"label": "inventor2-given",
			"type": "string",
			"required": false
		},
		"inventor2-first": {
			"label": "inventor2-first",
			"type": "string",
			"required": false
		},
		"inventor3-given": {
			"label": "inventor3-given",
			"type": "string",
			"required": false
		},
		"inventor3-first": {
			"label": "inventor3-first",
			"type": "string",
			"required": false
		},
		"inventor4-given": {
			"label": "inventor4-given",
			"type": "string",
			"required": false
		},
		"inventor4-first": {
			"label": "inventor4-first",
			"type": "string",
			"required": false
		},
		"inventorlink1": {
			"label": "inventorlink1",
			"type": "string",
			"required": false
		},
		"inventorlink": {
			"label": "inventorlink",
			"type": "string",
			"required": false
		},
		"inventorlink2": {
			"label": "inventorlink2",
			"type": "string",
			"required": false
		},
		"inventorlink3": {
			"label": "inventorlink3",
			"type": "string",
			"required": false
		},
		"inventorlink4": {
			"label": "inventorlink4",
			"type": "string",
			"required": false
		},
		"country": {
			"label": "country",
			"type": "string",
			"required": false
		},
		"publication-number": {
			"label": "publication-number",
			"type": "string",
			"required": false
		},
		"patent-number": {
			"label": "patent-number",
			"type": "string",
			"required": false
		},
		"number": {
			"label": "number",
			"type": "string",
			"required": false
		},
		"description": {
			"label": "description",
			"type": "string",
			"required": false
		},
		"status": {
			"label": "status",
			"type": "string",
			"required": false
		},
		"publication-date": {
			"label": "publication-date",
			"type": "string",
			"required": false
		},
		"pubdate": {
			"label": "pubdate",
			"type": "string",
			"required": false
		},
		"issue-date": {
			"label": "issue-date",
			"type": "string",
			"required": false
		},
		"gdate": {
			"label": "gdate",
			"type": "string",
			"required": false
		},
		"year": {
			"label": "year",
			"type": "string",
			"required": false
		},
		"fdate": {
			"label": "fdate",
			"type": "string",
			"required": false
		},
		"pridate": {
			"label": "pridate",
			"type": "string",
			"required": false
		},
		"assign1": {
			"label": "assign1",
			"type": "string",
			"required": false
		},
		"assign2": {
			"label": "assign2",
			"type": "string",
			"required": false
		},
		"ref": {
			"label": "ref",
			"type": "string",
			"required": false
		},
		"separator": {
			"label": "separator",
			"type": "string",
			"required": false
		},
		"quote": {
			"label": "quote",
			"type": "string",
			"required": false
		},
		"postscript": {
			"label": "postscript",
			"type": "string",
			"required": false
		},
		"author-separator": {
			"label": "author-separator",
			"type": "string",
			"required": false
		},
		"author-mask": {
			"label": "author-mask",
			"type": "string",
			"required": false
		},
		"authormask": {
			"label": "authormask",
			"type": "string",
			"required": false
		},
		"surname": {
			"label": "surname",
			"type": "string",
			"required": false
		},
		"last1": {
			"label": "last1",
			"type": "string",
			"required": false
		},
		"surname1": {
			"label": "surname1",
			"type": "string",
			"required": false
		},
		"author1": {
			"label": "author1",
			"type": "string",
			"required": false
		},
		"author": {
			"label": "author",
			"type": "string",
			"required": false
		},
		"authors": {
			"label": "authors",
			"type": "string",
			"required": false
		},
		"last2": {
			"label": "last2",
			"type": "string",
			"required": false
		},
		"surname2": {
			"label": "surname2",
			"type": "string",
			"required": false
		},
		"author2": {
			"label": "author2",
			"type": "string",
			"required": false
		},
		"last3": {
			"label": "last3",
			"type": "string",
			"required": false
		},
		"surname3": {
			"label": "surname3",
			"type": "string",
			"required": false
		},
		"author3": {
			"label": "author3",
			"type": "string",
			"required": false
		},
		"last4": {
			"label": "last4",
			"type": "string",
			"required": false
		},
		"surname4": {
			"label": "surname4",
			"type": "string",
			"required": false
		},
		"author4": {
			"label": "author4",
			"type": "string",
			"required": false
		},
		"last5": {
			"label": "last5",
			"type": "string",
			"required": false
		},
		"surname5": {
			"label": "surname5",
			"type": "string",
			"required": false
		},
		"author5": {
			"label": "author5",
			"type": "string",
			"required": false
		},
		"last6": {
			"label": "last6",
			"type": "string",
			"required": false
		},
		"surname6": {
			"label": "surname6",
			"type": "string",
			"required": false
		},
		"author6": {
			"label": "author6",
			"type": "string",
			"required": false
		},
		"last7": {
			"label": "last7",
			"type": "string",
			"required": false
		},
		"surname7": {
			"label": "surname7",
			"type": "string",
			"required": false
		},
		"author7": {
			"label": "author7",
			"type": "string",
			"required": false
		},
		"last8": {
			"label": "last8",
			"type": "string",
			"required": false
		},
		"surname8": {
			"label": "surname8",
			"type": "string",
			"required": false
		},
		"author8": {
			"label": "author8",
			"type": "string",
			"required": false
		},
		"last9": {
			"label": "last9",
			"type": "string",
			"required": false
		},
		"surname9": {
			"label": "surname9",
			"type": "string",
			"required": false
		},
		"author9": {
			"label": "author9",
			"type": "string",
			"required": false
		},
		"first1": {
			"label": "first1",
			"type": "string",
			"required": false
		},
		"given1": {
			"label": "given1",
			"type": "string",
			"required": false
		},
		"given": {
			"label": "given",
			"type": "string",
			"required": false
		},
		"first2": {
			"label": "first2",
			"type": "string",
			"required": false
		},
		"given2": {
			"label": "given2",
			"type": "string",
			"required": false
		},
		"first3": {
			"label": "first3",
			"type": "string",
			"required": false
		},
		"given3": {
			"label": "given3",
			"type": "string",
			"required": false
		},
		"first4": {
			"label": "first4",
			"type": "string",
			"required": false
		},
		"given4": {
			"label": "given4",
			"type": "string",
			"required": false
		},
		"first5": {
			"label": "first5",
			"type": "string",
			"required": false
		},
		"given5": {
			"label": "given5",
			"type": "string",
			"required": false
		},
		"first6": {
			"label": "first6",
			"type": "string",
			"required": false
		},
		"given6": {
			"label": "given6",
			"type": "string",
			"required": false
		},
		"first7": {
			"label": "first7",
			"type": "string",
			"required": false
		},
		"given7": {
			"label": "given7",
			"type": "string",
			"required": false
		},
		"first8": {
			"label": "first8",
			"type": "string",
			"required": false
		},
		"given8": {
			"label": "given8",
			"type": "string",
			"required": false
		},
		"first9": {
			"label": "first9",
			"type": "string",
			"required": false
		},
		"given9": {
			"label": "given9",
			"type": "string",
			"required": false
		},
		"author-link": {
			"label": "author-link",
			"type": "string",
			"required": false
		},
		"author1-link": {
			"label": "author1-link",
			"type": "string",
			"required": false
		},
		"authorlink": {
			"label": "authorlink",
			"type": "string",
			"required": false
		},
		"authorlink1": {
			"label": "authorlink1",
			"type": "string",
			"required": false
		},
		"author2-link": {
			"label": "author2-link",
			"type": "string",
			"required": false
		},
		"authorlink2": {
			"label": "authorlink2",
			"type": "string",
			"required": false
		},
		"author3-link": {
			"label": "author3-link",
			"type": "string",
			"required": false
		},
		"authorlink3": {
			"label": "authorlink3",
			"type": "string",
			"required": false
		},
		"author4-link": {
			"label": "author4-link",
			"type": "string",
			"required": false
		},
		"authorlink4": {
			"label": "authorlink4",
			"type": "string",
			"required": false
		},
		"author5-link": {
			"label": "author5-link",
			"type": "string",
			"required": false
		},
		"authorlink5": {
			"label": "authorlink5",
			"type": "string",
			"required": false
		},
		"author6-link": {
			"label": "author6-link",
			"type": "string",
			"required": false
		},
		"authorlink6": {
			"label": "authorlink6",
			"type": "string",
			"required": false
		},
		"author7-link": {
			"label": "author7-link",
			"type": "string",
			"required": false
		},
		"authorlink7": {
			"label": "authorlink7",
			"type": "string",
			"required": false
		},
		"author8-link": {
			"label": "author8-link",
			"type": "string",
			"required": false
		},
		"authorlink8": {
			"label": "authorlink8",
			"type": "string",
			"required": false
		},
		"author9-link": {
			"label": "author9-link",
			"type": "string",
			"required": false
		},
		"authorlink9": {
			"label": "authorlink9",
			"type": "string",
			"required": false
		},
		"coauthor": {
			"label": "coauthor",
			"type": "string",
			"required": false
		},
		"coauthors": {
			"label": "coauthors",
			"type": "string",
			"required": false
		},
		"origyear": {
			"label": "origyear",
			"type": "string",
			"required": false
		},
		"month": {
			"label": "month",
			"type": "string",
			"required": false
		},
		"trans_chapter": {
			"label": "trans_chapter",
			"type": "string",
			"required": false
		},
		"trans_title": {
			"label": "trans_title",
			"type": "string",
			"required": false
		},
		"type": {
			"label": "type",
			"type": "string",
			"required": false
		},
		"archiveurl": {
			"label": "archiveurl",
			"type": "string",
			"required": false
		},
		"deadurl": {
			"label": "deadurl",
			"type": "string",
			"required": false
		},
		"series": {
			"label": "series",
			"type": "string",
			"required": false
		},
		"version": {
			"label": "version",
			"type": "string",
			"required": false
		},
		"journal": {
			"label": "journal",
			"type": "string",
			"required": false
		},
		"periodical": {
			"label": "periodical",
			"type": "string",
			"required": false
		},
		"newspaper": {
			"label": "newspaper",
			"type": "string",
			"required": false
		},
		"magazine": {
			"label": "magazine",
			"type": "string",
			"required": false
		},
		"work": {
			"label": "work",
			"type": "string",
			"required": false
		},
		"volume": {
			"label": "volume",
			"type": "string",
			"required": false
		},
		"issue": {
			"label": "issue",
			"type": "string",
			"required": false
		},
		"pages": {
			"label": "pages",
			"type": "string",
			"required": false
		},
		"page": {
			"label": "page",
			"type": "string",
			"required": false
		},
		"at": {
			"label": "at",
			"type": "string",
			"required": false
		},
		"nopp": {
			"label": "nopp",
			"type": "string",
			"required": false
		},
		"chapter": {
			"label": "chapter",
			"type": "string",
			"required": false
		},
		"contribution": {
			"label": "contribution",
			"type": "string",
			"required": false
		},
		"chapter-url": {
			"label": "chapter-url",
			"type": "string",
			"required": false
		},
		"chapterurl": {
			"label": "chapterurl",
			"type": "string",
			"required": false
		},
		"contribution-url": {
			"label": "contribution-url",
			"type": "string",
			"required": false
		},
		"chapter-format": {
			"label": "chapter-format",
			"type": "string",
			"required": false
		},
		"others": {
			"label": "others",
			"type": "string",
			"required": false
		},
		"edition": {
			"label": "edition",
			"type": "string",
			"required": false
		},
		"place": {
			"label": "place",
			"type": "string",
			"required": false
		},
		"location": {
			"label": "location",
			"type": "string",
			"required": false
		},
		"publication-place": {
			"label": "publication-place",
			"type": "string",
			"required": false
		},
		"publisher": {
			"label": "publisher",
			"type": "string",
			"required": false
		},
		"editor-last": {
			"label": "editor-last",
			"type": "string",
			"required": false
		},
		"editor-surname": {
			"label": "editor-surname",
			"type": "string",
			"required": false
		},
		"editor1-last": {
			"label": "editor1-last",
			"type": "string",
			"required": false
		},
		"editor1-surname": {
			"label": "editor1-surname",
			"type": "string",
			"required": false
		},
		"editor1": {
			"label": "editor1",
			"type": "string",
			"required": false
		},
		"editor": {
			"label": "editor",
			"type": "string",
			"required": false
		},
		"editors": {
			"label": "editors",
			"type": "string",
			"required": false
		},
		"editor2-last": {
			"label": "editor2-last",
			"type": "string",
			"required": false
		},
		"editor2-surname": {
			"label": "editor2-surname",
			"type": "string",
			"required": false
		},
		"editor2": {
			"label": "editor2",
			"type": "string",
			"required": false
		},
		"editor3-last": {
			"label": "editor3-last",
			"type": "string",
			"required": false
		},
		"editor3-surname": {
			"label": "editor3-surname",
			"type": "string",
			"required": false
		},
		"editor3": {
			"label": "editor3",
			"type": "string",
			"required": false
		},
		"editor4-last": {
			"label": "editor4-last",
			"type": "string",
			"required": false
		},
		"editor4-surname": {
			"label": "editor4-surname",
			"type": "string",
			"required": false
		},
		"editor4": {
			"label": "editor4",
			"type": "string",
			"required": false
		},
		"editor-first": {
			"label": "editor-first",
			"type": "string",
			"required": false
		},
		"editor-given": {
			"label": "editor-given",
			"type": "string",
			"required": false
		},
		"editor1-first": {
			"label": "editor1-first",
			"type": "string",
			"required": false
		},
		"editor1-given": {
			"label": "editor1-given",
			"type": "string",
			"required": false
		},
		"editor2-first": {
			"label": "editor2-first",
			"type": "string",
			"required": false
		},
		"editor2-given": {
			"label": "editor2-given",
			"type": "string",
			"required": false
		},
		"editor3-first": {
			"label": "editor3-first",
			"type": "string",
			"required": false
		},
		"editor3-given": {
			"label": "editor3-given",
			"type": "string",
			"required": false
		},
		"editor4-first": {
			"label": "editor4-first",
			"type": "string",
			"required": false
		},
		"editor4-given": {
			"label": "editor4-given",
			"type": "string",
			"required": false
		},
		"editor-link": {
			"label": "editor-link",
			"type": "string",
			"required": false
		},
		"editor1-link": {
			"label": "editor1-link",
			"type": "string",
			"required": false
		},
		"editor2-link": {
			"label": "editor2-link",
			"type": "string",
			"required": false
		},
		"editor3-link": {
			"label": "editor3-link",
			"type": "string",
			"required": false
		},
		"editor4-link": {
			"label": "editor4-link",
			"type": "string",
			"required": false
		},
		"language": {
			"label": "language",
			"type": "string",
			"required": false
		},
		"in": {
			"label": "in",
			"type": "string",
			"required": false
		},
		"format": {
			"label": "format",
			"type": "string",
			"required": false
		},
		"arxiv": {
			"label": "arxiv",
			"type": "string",
			"required": false
		},
		"asin": {
			"label": "asin",
			"type": "string",
			"required": false
		},
		"ASIN": {
			"label": "ASIN",
			"type": "string",
			"required": false
		},
		"asin-tld": {
			"label": "asin-tld",
			"type": "string",
			"required": false
		},
		"bibcode": {
			"label": "bibcode",
			"type": "string",
			"required": false
		},
		"doi": {
			"label": "doi",
			"type": "string",
			"required": false
		},
		"DOI": {
			"label": "DOI",
			"type": "string",
			"required": false
		},
		"doi_inactivedate": {
			"label": "doi_inactivedate",
			"type": "string",
			"required": false
		},
		"doi_brokendate": {
			"label": "doi_brokendate",
			"type": "string",
			"required": false
		},
		"isbn": {
			"label": "isbn",
			"type": "string",
			"required": false
		},
		"ISBN": {
			"label": "ISBN",
			"type": "string",
			"required": false
		},
		"issn": {
			"label": "issn",
			"type": "string",
			"required": false
		},
		"ISSN": {
			"label": "ISSN",
			"type": "string",
			"required": false
		},
		"jfm": {
			"label": "jfm",
			"type": "string",
			"required": false
		},
		"JFM": {
			"label": "JFM",
			"type": "string",
			"required": false
		},
		"jstor": {
			"label": "jstor",
			"type": "string",
			"required": false
		},
		"JSTOR": {
			"label": "JSTOR",
			"type": "string",
			"required": false
		},
		"lccn": {
			"label": "lccn",
			"type": "string",
			"required": false
		},
		"LCCN": {
			"label": "LCCN",
			"type": "string",
			"required": false
		},
		"mr": {
			"label": "mr",
			"type": "string",
			"required": false
		},
		"MR": {
			"label": "MR",
			"type": "string",
			"required": false
		},
		"oclc": {
			"label": "oclc",
			"type": "string",
			"required": false
		},
		"OCLC": {
			"label": "OCLC",
			"type": "string",
			"required": false
		},
		"ol": {
			"label": "ol",
			"type": "string",
			"required": false
		},
		"OL": {
			"label": "OL",
			"type": "string",
			"required": false
		},
		"osti": {
			"label": "osti",
			"type": "string",
			"required": false
		},
		"OSTI": {
			"label": "OSTI",
			"type": "string",
			"required": false
		},
		"pmc": {
			"label": "pmc",
			"type": "string",
			"required": false
		},
		"PMC": {
			"label": "PMC",
			"type": "string",
			"required": false
		},
		"pmid": {
			"label": "pmid",
			"type": "string",
			"required": false
		},
		"PMID": {
			"label": "PMID",
			"type": "string",
			"required": false
		},
		"rfc": {
			"label": "rfc",
			"type": "string",
			"required": false
		},
		"RFC": {
			"label": "RFC",
			"type": "string",
			"required": false
		},
		"ssrn": {
			"label": "ssrn",
			"type": "string",
			"required": false
		},
		"SSRN": {
			"label": "SSRN",
			"type": "string",
			"required": false
		},
		"zbl": {
			"label": "zbl",
			"type": "string",
			"required": false
		},
		"id": {
			"label": "id",
			"type": "string",
			"required": false
		},
		"ID": {
			"label": "ID",
			"type": "string",
			"required": false
		},
		"access-date": {
			"label": "access-date",
			"type": "string",
			"required": false
		},
		"accessdate": {
			"label": "accessdate",
			"type": "string",
			"required": false
		},
		"laysummary": {
			"label": "laysummary",
			"type": "string",
			"required": false
		},
		"laysource": {
			"label": "laysource",
			"type": "string",
			"required": false
		},
		"laydate": {
			"label": "laydate",
			"type": "string",
			"required": false
		},
		"author-name-separator": {
			"label": "author-name-separator",
			"type": "string",
			"required": false
		},
		"lastauthoramp": {
			"label": "lastauthoramp",
			"type": "string",
			"required": false
		},
		"display-authors": {
			"label": "display-authors",
			"type": "string",
			"required": false
		},
		"archivedate": {
			"label": "archivedate",
			"type": "string",
			"required": false
		},
		"script-title": {
			"description": "标识引用的原文标题",
			"example": "ja:福原愛",
			"type": "string"
		}
	},
	"maps": {
		"citoid": {
			"title": "title",
			"caseName": "title",
			"nameOfAct": "title",
			"url": "url",
			"label": "publisher",
			"company": "publisher",
			"studio": "publisher",
			"network": "publisher",
			"distributor": "publisher",
			"publisher": "publisher",
			"publicationTitle": "journal",
			"date": "date",
			"issueDate": "date",
			"dateEnacted": "date",
			"dateDecided": "date",
			"accessDate": "accessdate",
			"location": "location",
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
			"firstPage": "pages",
			"codePages": "pages",
			"volume": "volume",
			"reporterVolume": "volume",
			"codeVolume": "volume",
			"series": "series",
			"patentNumber": "patent-number",
			"programTitle": "series",
			"episodeNumber": "issue",
			"billNumber": "issue",
			"publicLawNumber": "issue",
			"docketNumber": "issue",
			"issue": "issue",
			"DOI": "doi",
			"language": "language",
			"interviewee": [
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
			"cartographer": [
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
			"performer": [
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
			"podcaster": [
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
			"director": [
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
			"sponsor": [
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
			"programmer": [
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
			"artist": [
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
				],
				[
					"editor2-first",
					"editor2-last"
				]
			],
			"inventor": [
				[
					"inventor-first",
					"inventor-last"
				],
				[
					"inventor2-first",
					"inventor2-last"
				]
			]
		}
	}
}
</templatedata>

==引用書籍==
===參數（皆為可選）===
{|  border="1"
|-
|<pre>{{Citation
 | last =
 | first =
 | author-link =
 | last2 =
 | first2 =
 | author2-link =
 | date =
 | year =
 | title =
 | edition =
 | volume =
 | place =
 | publisher =
 | id =
 | isbn =
 | doi =
 | oclc =
 | url =
 | accessdate =
}}</pre>
|
* '''last'''（或'''last1'''）：第一位作者的姓。
* '''first'''（或'''first1'''）：第一位作者的名。
* '''author-link'''（或'''author1-link'''）：第一位作者在維基百科中的條目標題（如適用）。
* '''last2'''、'''last3'''、'''last4'''：第二、第三和第四位作者的姓（如適用）。
* '''first2'''、'''first3'''、'''first4'''：第二、第三和第四位作者的名（如適用）。
* '''author2-link'''、'''author3-link'''、'''author4-link'''：第二、第三和第四位作者在維基百科上的條目標題（如適用）。
* '''date'''：出版日期。
* '''year'''：出版年份。
* '''title'''：書名。
* '''edition'''：版次（如果書本不是第1版的話）。例如：edition=2nd（第二版）。
* '''volume'''：多期次書本中的期號。
* '''place'''（或'''location'''）：出版城市。如果在標題頁出現多個城市，選擇第1個城市或出版商的總部所在地。如果該城市不為人所知，必須加上縣、地區或州名。美國州份以2字母縮寫列出，例如：<code>Place=Paris, TX</code>（後面不加句號）。如果出版社在大學，或是該城市是屬於大學城的一部份，不要使用該參數。
* '''publisher'''：出版社名稱。英文字眼如''Publishers''、''Co.''、''Inc.''、''Ltd.''等應省略，但保留''Books''或''Press''。
* '''id'''：識別碼。（當其他專有識別號碼，如國際標準書號不適用時使用。）
* '''isbn''': [[國際標準書號]]（ISBN），如''<nowiki>ISBN 1-111-22222-9</nowiki>''。
* '''doi''': [[DOI|數位物件識別號]]（DOI），如''<nowiki>10.1016/j.coi.2004.08.001</nowiki>''。
* '''oclc''': [[OCLC]]號碼，如''3185581''。
* '''url''': 書本的[[統一資源定位符|網址]]。
* '''accessdate'''：網頁瀏覽日期。
|}

===例子===
{|  border="1"
|-
|僅一位作者
|<pre>
{{ Citation
 | last=Turner
 | first=O.
 | title=History of the Pioneer
Settlement of Phelps and Gorham's
Purchase, and Morris' Reserve
 | publisher=William Alling
 | place=Rochester, New York
 | year=1851
 | url = http://olivercowdery.com/
texts/1851Trn1.htm#turn1851
 }}.
</pre>
|{{ Citation
 | last=Turner
 | first=O.
 | title=History of the Pioneer Settlement of Phelps and Gorham's Purchase, and Morris' Reserve
 | publisher=William Alling
 | place=Rochester, New York
 | year=1851
 | url = http://olivercowdery.com/texts/1851Trn1.htm#turn1851
}}.
|-
|三位作者、一冊書和一位校對者
|<pre>
{{ Citation
 | last1=Lincoln
 | first1=A.
 | last2=Washington
 | first2=G.
 | last3=Adams
 | first3=J.
 | title=All the Presidents' Names
 | publisher=The Pentagon
 | place=Home Base, New York
 | volume=XII
 | edition=2nd
 | year=2007
}}.
</pre>
|{{ Citation
 | last1=Lincoln
 | first1=A.
 | last2=Washington
 | first2=G.
 | last3=Adams
 | first3=J.
 | title=All the Presidents' Names
 | publisher=The Pentagon
 | place=Home Base, New York
 | volume=XII
 | edition=2nd
 | year=2007
}}.
|}

==引用自期刊、報紙、雜誌或其他刊物==
===參數===
{|  border="1"
|-
|<pre>
{{Citation
 | last=
 | first=
 | author-link=
 | year=
 | title=
 | periodical=
 | volume=
 | issue=
 | pages=
 | url=
 | doi=
 | oclc=
}}.
</pre>
|
* '''last'''（或 '''last1'''）：第一位作者的姓。
* '''first'''（或 '''first1'''）：第一位作者的名。
* '''author-link''' (or '''author1-link'''): 第一位作者在維基百科中的條目標題（如適用）。
* '''last2''', '''last3''', '''last4''': 第二、第三和第四位作者的姓（如適用）。
* '''first2''', '''first3''', '''first4''': 第二、第三和第四位作者的名（如適用）。
* '''author2-link''', '''author3-link''', '''author4-link''': 第二、第三和第四位作者在維基百科上的條目標題（如適用）。
* '''date''': 出版日期。
* '''year''': 出版年份。
* '''title''': 標題。
* '''periodical''': 期刊、報章或雜誌的名稱。
* '''volume''': 刊物冊數。
* '''issue''' (or '''number'''): 刊物發行期數。
* '''pages''': 文章頁數（如適用）。
* '''url''': 文章的[[統一資源定位符|網址]]。
* '''doi''': [[DOI|數位物件識別號]]（DOI），如''<nowiki>10.1016/j.coi.2004.08.001</nowiki>''。
* '''oclc''': [[OCLC]]號碼，如''3185581''。
* '''accessdate''': 網頁瀏覽日期。
|}

===例子===
{|  border="1"
|-
|Journal article
|<pre>
{{Citation
 | last=Hill
 | first=Marvin S.
 | title=Joseph Smith and the 1826
Trial: New Evidence and New
Difficulties
 | journal=BYU Studies
 | volume=12
 | issue=2
 | year=1976
 | pages=1&ndash;8
 | url=https://byustudies.byu.edu/
shop/PDFSRC/12.2Hill.pdf
 }}.
</pre>
|{{Citation
 | last=Hill
 | first=Marvin S.
 | title=Joseph Smith and the 1826 Trial: New Evidence and New Difficulties
 | journal=BYU Studies
 | volume=12
 | issue=2
 | year=1976
 | pages=1&ndash;8
 | url=https://byustudies.byu.edu/shop/PDFSRC/12.2Hill.pdf
 }}.
|-
|Newspaper article
|<pre>
{{Citation
 | last=Smith
 | first=Joseph III
 | author-link=Joseph Smith III
 | title=Last Testimony of Sister Emma
 | newspaper=The Saints' Herald
 | volume=26
 | issue=19
 | date=[[October 1]], [[1879]]
 | year=1879
 | month=October
 | page=289
 | url=http://www.sidneyrigdon.com/
dbroadhu/IL/sain1872.htm#100179
 }}.
</pre>
|{{Citation
 | last=Smith
 | first=Joseph III
 | author-link=Joseph Smith III
 | title=Last Testimony of Sister Emma
 | newspaper=The Saints' Herald
 | volume=26
 | issue=19
 | page=289
 | url=http://www.sidneyrigdon.com/dbroadhu/IL/sain1872.htm#100179
 | date=October 1, 1879
 }}.
|}

==引用編輯書或部分編輯書，包括百科全書或百科全書條目==
===參數===
{|  border="1"
|-
|<pre>
{{Citation
 | last=
 | first=
 | author-link=
 | last2=
 | first2=
 | author2-link
 | year=
 | date=
 | publication-date=
 | contribution=
 | contribution-url=
 | editor-last=
 | editor-first=
 | editor-link=
 | editor2-last=
 | editor2-first=
 | editor2-link=
 | title=
 | edition=
 | place=
 | publication-place=
 | publisher=
 | volume=
 | pages=
 | id=
 | doi=
 | oclc=
 | url=
}}.
</pre>
|
* '''last''' (or '''last1'''): The first author's surname or last name.
* '''first''' (or '''first1'''): The first author's first or given name(s).
* '''author-link''' (or '''author1-link'''): Title of an existing Wikipedia article about the first author.
* '''last2''', '''last3''', '''last4''': The second, third, and fourth authors' surname or last name, if applicable.
* '''first2''', '''first3''', '''first4''': The second, third, and fourth authors' first or given name(s), if applicable.
* '''author2-link''', '''author3-link''', '''author4-link''': Title of an existing Wikipedia article about the second, third, and fourth author, if applicable.
* '''year''': Year of authorship or publication. (Mandatory for use with links from [[:Template:Harvard citation]]. In some situations, the template may be able to derive a year from the full date.)
* '''date''': Date of authorship or publication.
* '''publication-date''': Date of publication (if different than ''date'').
* '''contribution''' (or '''chapter'''): Title of the contribution or chapter.
* '''contribution-url''' (or '''chapter-url'''): URL of the contribution or chapter.
* '''editor-last''' (or '''editor1-last'''): The first editor's surname or last name.
* '''editor-first''' (or '''editor2-first'''): The first editor's first or given name(s).
* '''editor-link''' (or '''editor1-link'''): Title of an existing Wikipedia article about the first editor.
* '''editor2-last''', '''editor3-last''', '''editor4-last''': The second, third, and fourth editor' surname or last name, if applicable.
* '''editor2-first''', '''editor3-first''', '''editor4-first''': The second, third, and fourth editors' first or given name(s), if applicable.
* '''editor2-link''', '''editor3-link''', '''editor4-link''': Title of an existing Wikipedia article about the second, third, and fourth editor, if applicable.
* '''title''': Title of the book or compilation.
* '''edition''': Number or name of the edition, if not the first; for example: ''edition''=2nd.
* '''volume''': The volume number of a multi-volume book or compilation.
* '''place''' (or '''location'''): The place where the article, encyclopedia entry, or other included item was created. Usually, this is collective work's city of publication; if not, then use the separate ''publication-place'' parameter. If more than one town/city is listed on the title page, give the first one or the location of the publisher's head office. If the city is not well-known, you may add a county, region, or state. States in the U.S. are denoted by a two-letter code; for example: <code>place=Paris, TX</code> (no period at the end).  Where the publisher is a university and the place or location is included in the name of the university, do not use this parameter.
* '''publication-place'''. The place where the collective work was published (if different from ''place'' or ''location'').
* '''publisher''': The name of the publisher. Omit terms such as ''Publishers'', ''Co.'', ''Inc.'', ''Ltd.'', etc., but retain the words ''Books'' or ''Press''.
* '''id''': Identifier such as ''<nowiki>ISBN 1-111-22222-9</nowiki>''
* '''isbn''': Use this parameter if the book or compilation has an ISBN.
* '''doi''': A [[digital object identifier]] such as ''<nowiki>10.1016/j.coi.2004.08.001</nowiki>''.
* '''oclc''': [[Online Computer Library Center]] ID number, such as ''3185581''
* '''url''': An [[url]] of an online location where the book or compilationcan be found.
* '''accessdate''': Date when the url was accessed.
|}

===例子===
{|  border="1"
|-
|Manuscript published in an edited compilation
|<pre>
{{Citation
 | last=Bidamon
 | first=Emma Smith
 | author-link=Emma Hale Smith
 | chapter=Letter to Emma S. Pilgrim
 | date=1876-03-27
 | editor-surname=Vogel
 | editor-first=Dan
 | title=Early Mormon Documents
 | volume=1
 | publisher=Signature Books
 | publication-date=1996
 | isbn=1-56085-072-8
 }}.
</pre>
|{{Citation
 | last=Bidamon
 | first=Emma Smith
 | author-link=Emma Hale Smith
 | chapter=Letter to Emma S. Pilgrim
 | date= 1876-03-27
 | editor-surname=Vogel
 | editor-first=Dan
 | title=Early Mormon Documents
 | volume=1
 | publisher=Signature Books
 | publication-date=1996
 | isbn=1-56085-072-8
 }}.
|-
|Work with an editor but no author
|<pre>
{{Citation
 | editor-surname=Vogel
 | editor-first=Dan
 | title=Early Mormon Documents
 | volume=1
 | publisher=Signature Books
 | publication-date=1996
 | isbn=1-56085-072-8
 }}.
</pre>
|{{Citation
 | editor-surname=Vogel
 | editor-first=Dan
 | title=Early Mormon Documents
 | volume=1
 | publisher=Signature Books
 | publication-date=1996
 | isbn=1-56085-072-8
 }}.
|-
|Encyclopedia article by a named author
|<pre>
{{Citation
  | last = Kramer
  | first = Martin
  | author-link = Martin Kramer
  | contribution = Bernard Lewis
  | editor-last = Boyd
  | editor-first = Kelley
  | title = Encyclopedia of Historians
and Historical Writing
  | volume = 1
  | pages = 719&ndash;720
  | publisher = Fitzroy Dearborn
  | place = London
  | publication-date = 1999
  | contribution-url = http://
www.geocities.com/martinkramerorg/
BernardLewis.htm
}}.
</pre>
|{{Citation
  | last = Kramer
  | first = Martin
  | author-link = Martin Kramer
  | contribution = Bernard Lewis
  | editor-last = Boyd
  | editor-first = Kelley
  | title = Encyclopedia of Historians and Historical Writing
  | volume = 1
  | pages = 719&ndash;720
  | publisher = Fitzroy Dearborn
  | place = London
  | publication-date = 1999
  | contribution-url = http://www.geocities.com/martinkramerorg/BernardLewis.htm
}}.
|-
|Encyclopedia article with no named author
|<pre>
{{Citation
  | contribution = Bernard Lewis
  | editor-last = Boyd
  | editor-first = Kelley
  | title = Encyclopedia of Historians
and Historical Writing
  | volume = 1
  | pages = 719&ndash;720
  | publisher = Fitzroy Dearborn
  | place = London
  | year = 1999
  | contribution-url = http://
www.geocities.com/martinkramerorg/
BernardLewis.htm
}}.
</pre>
|{{Citation
  | contribution = Bernard Lewis
  | editor-last = Boyd
  | editor-first = Kelley
  | title = Encyclopedia of Historians and Historical Writing
  | volume = 1
  | pages = 719&ndash;720
  | publisher = Fitzroy Dearborn
  | place = London
  | year = 1999
  | contribution-url = http://www.geocities.com/martinkramerorg/BernardLewis.htm
}}.
|}

==Citing contributions, republications, or edited quotations in a periodical article==
===Parameters===
{|  border="1"
|-
|<pre>
{{Citation
 | last=
 | first=
 | author-link=
 | last2=
 | first2=
 | author2-link
 | year=
 | date=
 | publication-date=
 | contribution=
 | contribution-url=
 | editor-last=
 | editor-first=
 | editor-link=
 | editor2-last=
 | editor2-first=
 | editor2-link=
 | title=
 | periodical=
 | volume=
 | issue=
 | pages=
 | place=
 | publication-place=
 | publisher=
 | id=
 | doi=
 | oclc=
 | url=
}}.
</pre>
|
* '''last''' (or '''last1'''): The first author's surname or last name.
* '''first''' (or '''first1'''): The first author's first or given name(s).
* '''author-link''' (or '''author1-link'''): Title of an existing Wikipedia article about the first author.
* '''last2''', '''last3''', '''last4''': The second, third, and fourth authors' surname or last name, if applicable.
* '''first2''', '''first3''', '''first4''': The second, third, and fourth authors' first or given name(s), if applicable.
* '''author2-link''', '''author3-link''', '''author4-link''': Title of an existing Wikipedia article about the second, third, and fourth author, if applicable.
* '''year''': Year of authorship or publication. (Mandatory for use with links from [[:Template:Harvard citation]]. In some situations, the template may be able to derive a year from the full date.)
* '''date''': Date of authorship or publication.
* '''publication-date''': Date of publication (if different than ''date'').
* '''contribution''' (or '''chapter'''): Title of the contribution or chapter.
* '''contribution-url''' (or '''chapter-url'''): URL of the contribution or chapter.
* '''editor-last''' (or '''editor1-last'''): The first editor's surname or last name.
* '''editor-first''' (or '''editor2-first'''): The first editor's first or given name(s).
* '''editor-link''' (or '''editor1-link'''): Title of an existing Wikipedia article about the first editor.
* '''editor2-last''', '''editor3-last''', '''editor4-last''': The second, third, and fourth editor' surname or last name, if applicable.
* '''editor2-first''', '''editor3-first''', '''editor4-first''': The second, third, and fourth editors' first or given name(s), if applicable.
* '''editor2-link''', '''editor3-link''', '''editor4-link''': Title of an existing Wikipedia article about the second, third, and fourth editor, if applicable.
* '''title''': Title of the book or compilation.
* '''periodical''' (or '''journal''', '''newspaper''', '''magazine'''): Name of the periodical.
* '''volume''': The volume number of the journal.
* '''issue''' (or '''number'''): The issue number of the journal.
* '''pages''' (''optional''): The pages in the issue where the article may be found.
* '''place''' (or '''location'''): The place where the article, encyclopedia entry, or other included item was created. Usually, this is collective work's city of publication; if not, then use the separate ''publication-place'' parameter. If more than one town/city is listed on the title page, give the first one or the location of the publisher's head office. If the city is not well-known, you may add a county, region, or state. States in the U.S. are denoted by a two-letter code; for example: <code>place=Paris, TX</code> (no period at the end).  Where the publisher is a university and the place or location is included in the name of the university, do not use this parameter.
* '''publication-place'''. The place where the collective work was published (if different from ''place'' or ''location'').
* '''id''': Identifier such as ''<nowiki>ISBN 1-111-22222-9</nowiki>''
* '''doi''': A [[digital object identifier]] such as ''<nowiki>10.1016/j.coi.2004.08.001</nowiki>''.
* '''oclc''': [[Online Computer Library Center]] ID number, such as ''3185581''
* '''url''': An [[url]] of an online location where the book or compilation can be found.
* '''accessdate''': Date when the url was accessed.
|}

===Examples===

{|  border="1"
|-
|Manuscript edited and published in a journal
|<pre>
{{Citation
 | last=Knight
 | first=Joseph, Sr.
 | year=1833
 | editor-last=Jessee
 | editor-first=Dean
 | title=Joseph Knight's Recollection
of Early Mormon History
 | journal=BYU Studies
 | volume=17
 | issue=1
 | publication-date=1976
 | pages=35
 | url=https://byustudies.byu.edu/
shop/PDFSRC/17.1Jessee.pdf
 }}.</pre>
|{{Citation
 | last=Knight
 | first=Joseph, Sr.
 | year=1833
 | editor-last=Jessee
 | editor-first=Dean
 | title=Joseph Knight's Recollection of Early Mormon History
 | journal=BYU Studies
 | volume=17
 | issue=1
 | publication-date=1976
 | pages=35
 | url=https://byustudies.byu.edu/shop/PDFSRC/17.1Jessee.pdf
 }}.
|-
|Manuscript written at one date and place, then published in a periodical at a different date and place with commentary by the editor.
|<pre>
{{Citation
 | last=Klingensmith
 | first=Philip
 | date=1872-09-05
 | place=Lincoln County, Nevada
 | title=Mountain Meadows Massacre
 | editor-last=Toohy
 | editor-first=Dennis J.
 | journal=Corinne Daily Reporter
 | publication-date=1872-09-24
 | publication-place=Corinne, Utah
 | volume=5
 | issue=252
 | pages=1 
 }}.</pre><!-- 未知錯誤 | contribution=Affidavit | contribution-url=http://udn.lib.utah.edu/u?/corinne,5359 -->

|{{Citation
 | last=Klingensmith
 | first=Philip
 | date= 1872-09-05
 | place=Lincoln County, Nevada
 | title=Mountain Meadows Massacre
 | editor-last=Toohy
 | editor-first=Dennis J.
 | journal=Corinne Daily Reporter
 | publication-date= 1872-09-24
 | publication-place=Corinne, Utah
 | volume=5
 | issue=252
 | pages=1<!--
 | contribution=Affidavit
 | contribution-url=http://udn.lib.utah.edu/u?/corinne,5359-->
 }}.
|}

==Dates==
{{Reflist|group="n"|refs=<ref name="dates" group="n">The format of dates in the references of an article should use consistent and unambiguous styles. Example formats used in Wikipedia citations include:
* ''2009''
* ''2009-09-14'' ([[ISO 8601#Calendar dates|ISO 8601 standard format]]: YYYY-MM-DD)
* ''14 September 2009''
* ''September 14, 2009'' (with comma)
* ''September 2009''

Dates should not be linked (say, to a Wikipedia article of the same name) in references.

Please see [[Wikipedia:Manual of Style (dates and numbers)#Dates|Wikipedia:Manual of Style (dates and numbers) §&nbsp;Dates]] for more guidance about formatting dates.
</ref>}}

==工具==

你可以在[[Wikipedia:列明来源#工具]]看到帮助你以“citation”格式制造参考文献的工具的列表。

<includeonly>
<!-- ADD CATEGORIES BELOW THIS LINE -->
[[Category:引用模板|{{PAGENAME}}]]
[[Category:產生COinS的模板|{{PAGENAME}}]]
[[Category:使用了分析程序的模板|{{PAGENAME}}]]

<!-- ADD INTERWIKIS BELOW THIS LINE -->
</includeonly>