<includeonly><!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{Documentation subpage}}</noinclude>
<!-- EDIT TEMPLATE DOCUMENTATION BELOW THIS LINE -->
{{Citation Style documentation/cs1}}
<includeonly>{{esoteric}}</includeonly>

=== Usage summary ===
{{csdoc|usage common}}
:<code><nowiki>{{cite conference |url= |title= |last1= |first1= |author-link1= |last2= |first2= |author-link2= |date= |publisher= |book-title= |pages= |location= |conference= |id= }}</nowiki></code>
{{end}}

==== Full version ====
<pre>
{{cite conference
 | language =
 | first = 
 | last = 
 | authorlink = 
 | coauthors = 
 | date = 
 | year = 
 | month = 
 | title = 
 | conference = 
 | conferenceurl = 
 | booktitle = 
 | editor = 
 | others = 
 | volume = 
 | edition = 
 | publisher = 
 | location = 
 | pages = 
 | url = 
 | format = 
 | accessdate = 
 | doi = 
 | id = 
}}
</pre>

==== Short (common) version ====
<pre>
{{cite conference
 | first = 
 | last = 
 | authorlink = 
 | coauthors = 
 | title = 
 | booktitle = 
 | pages = 
 | publisher = 
 | date = 
 | location = 
 | url = 
 | accessdate = 
 | id = 
}}
</pre>

=== Description of parameters ===
* '''language''':Lauguage of this conference use.
* '''author''': Author
** '''last''' works with '''first''' to produce <code>last, first</code>
** '''authorlink''' works either with '''author''' or with '''last''' & '''first''' to link to the appropriate article
** '''coauthors''': allows additional authors
* '''date''': Full date of publication, in [[ISO 8601]] YYYY-MM-DD format, eg. ''2006-02-17''. (Not automatically wikified.)
** OR:  '''year''': Year of publication, and '''month''': Name of the month of publication. If you also have the day, use ''date'' instead.
* '''title''': 文献标题。 '''''必填参数'''''。
* '''conference''': 会议名称。
* '''conferenceurl''': 会议网址。
* '''booktitle''': 会议论文集标题。'''''必填参数'''''。 ''eg:'' "Proceedings of the ''conference organizer''"
* '''editor''': No text is added, so labels such as "(ed.)" has to be supplied by user.
* '''others''': For uses such as "illustrated by Smith" or "trans. Smith".
* '''volume''': If the proceedings are part of a series.
* '''edition''': When the book has more than one edition. ''eg:'' "2nd edition".
* '''pages''': ''1&amp;ndash;2'': first page, and optional last page (put an &[[dash#En dash|ndash]]; for the range).
* '''publisher''': Publisher should not include corporate designation such is "Ltd" or "Inc".
** '''location''': Place of publication (and ''not'' conference place). Produces ''location: publisher'' (ignored if the publisher field is ''not'' used).
* '''doi''': The [[Digital Object Identifier]].
* '''id''': Identifier such as ''<nowiki>ISBN 1-111-22222-9</nowiki>'' or ''<nowiki>{{</nowiki>[[:Template:LCC|LCC]]|Z253.U69}}'' or ''<nowiki>{{</nowiki>[[:Template:ISSN|ISSN]]|1111-2220}}''
* '''url''': url of the online article or proceedings.
** '''format''': Format, e.g. PDF.  HTML implied if not specified.
** '''accessdate''': Full date when item was accessed, in [[ISO 8601]] YYYY-MM-DD format, eg. ''2006-02-17''. (Automatically wikified.)

===Examples===
{| class="wikitable"
!Wikitext !! Result
|-
|<pre> {{cite conference
 | first = FIRST
 | last = LAST
 | authorlink = Example
 | coauthors = COAUTHORS
 | date = 1996-11-29
 | year = 
 | month = 
 | title = TITLE
 | conference = CONFERENCE
 | conferenceurl = http://www.wikipedia.org/
 | booktitle = BOOKTITLE
 | editor = EDITOR
 | others = OTHERS
 | volume = 1
 | edition = EDITION
 | publisher = PUBLISHER
 | location = LOCATION
 | pages = PAGES
 | url = http://www.wikipedia.org/
 | accessdate = 2006-04-07
 | doi = 10.1234/5678
 | id = ISBN 1-111-22222-9
 }}</pre> 
| 
{{cite conference
 | first = FIRST
 | last = LAST
 | authorlink = Example
 | coauthors = COAUTHORS
 | date = 1996-11-29
 | year = 
 | month = 
 | title = TITLE
 | conference = CONFERENCE
 | conferenceurl = http://www.wikipedia.org/
 | booktitle = BOOKTITLE
 | editor = EDITOR
 | others = OTHERS
 | volume = 1
 | edition = EDITION
 | publisher = PUBLISHER
 | location = LOCATION
 | pages = PAGES
 | url = http://www.wikipedia.org/
 | accessdate = 2006-04-07
 | doi = 10.1234/5678
 | id = ISBN 1-111-22222-9
 }}
|-
|
<pre> {{cite conference
 | author = AUTHOR
 | authorlink = Example
 | year = 2006
 | month = January
 | title = TITLE
 | booktitle = BOOKTITLE
 | url = http://www.wikipedia.com
 | accessdate = 2006-04-07
 | id = ISBN 1-111-22222-9
 }}</pre>
|
* {{cite conference
 | author = AUTHOR
 | authorlink = Example
 | title = TITLE
 | booktitle = BOOKTITLE
 | url = http://www.wikipedia.com
 | accessdate = 2006-04-07
 | id = ISBN 1-111-22222-9
 |date=January 2006}}
|}

==TemplateData==
{{TemplateData header}}
<templatedata>
{
	"description": "This template formats a citation to published conference proceedings.",
	"params": {
		"url": {
			"label": "URL",
			"description": "The URL of the online location where the text of the publication can be found. Requires schemes of the type \"http://...\" or maybe even the &nbsp;protocol relative scheme \"//...\"",
			"type": "line",
			"aliases": [
				"URL"
			],
			"suggested": true,
			"example": "https://www.nytimes.com/..."
		},
		"title": {
			"label": "标题",
			"description": "The title of the article; can be wikilinked to an existing Wikipedia article or url may be used to add an external link, but not both. Displays in quotes.",
			"type": "content",
			"required": true
		},
		"last": {
			"label": "作者/姓氏",
			"description": "The surname of the author; don't wikilink, use 'author-link'; can suffix with a numeral to add additional authors",
			"aliases": [
				"author",
				"author1",
				"authors",
				"last1"
			],
			"type": "line",
			"suggested": true
		},
		"first": {
			"label": "名字",
			"description": "Given or first name, middle names, or initials of the author; don't wikilink, use 'author-link'; can suffix with a numeral to add additional authors",
			"aliases": [
				"first1"
			],
			"type": "line",
			"suggested": true
		},
		"last2": {
			"label": "Last name 2",
			"description": "The surname of the second author; don't wikilink, use 'author-link2'.",
			"aliases": [
				"author2"
			],
			"type": "line"
		},
		"first2": {
			"label": "First name 2",
			"description": "Given or first name, middle names, or initials of the second author; don't wikilink.",
			"type": "line"
		},
		"date": {
			"label": "日期",
			"description": "Date of the source; do not wikilink. As listed in the publication",
			"type": "date",
			"suggested": true,
			"example": "Summer 2017"
		},
		"publisher": {
			"label": "出版社",
			"description": "Name of the publisher; displays after title",
			"type": "content"
		},
		"issue": {
			"label": "期号",
			"description": "Issue identifier when the source is part of a series that is published periodically",
			"type": "line"
		},
		"doi": {
			"label": "DOI",
			"description": "Digital Object Identifier; begins with '10.'",
			"type": "string"
		},
		"doi-broken-date": {
			"label": "DOI broken date",
			"description": "The date that the DOI was determined to be broken",
			"type": "date"
		},
		"others": {
			"label": "其他贡献者",
			"description": "Used to record other contributions to the work, such as 'Illustrated by John Smith' or 'Translated by John Smith'",
			"type": "content"
		},
		"year": {
			"label": "出版年",
			"description": "Year of the source being referenced; recommended only when date parameter format is YYYY-MM-DD and a CITEREF disambiguator is needed",
			"type": "number"
		},
		"orig-date": {
			"label": "Original date",
			"description": "Original date of publication; provide specifics",
			"type": "number"
		},
		"editor-last": {
			"label": "Editor last name",
			"description": "The surname of the editor; don't wikilink, use 'editor-link'; can suffix with a numeral to add additional editors; alias of 'editor1-last', 'editor'",
			"aliases": [
				"editor1-last"
			],
			"type": "line"
		},
		"editor-first": {
			"label": "Editor first name",
			"description": "Given or first name, middle names, or initials of the editor; don't wikilink, use 'editor-link'; can suffix with a numeral to add additional editors; alias of 'editor1-first'",
			"aliases": [
				"editor1-first"
			],
			"type": "line"
		},
		"editor-link": {
			"label": "Editor link",
			"description": "Title of existing Wikipedia article about the editor; can suffix with a numeral to add additional editors; alias of 'editor1-link'",
			"type": "wiki-page-name"
		},
		"series": {
			"label": "Series",
			"description": "Series identifier when the source is part of a series, such as a book series or a journal; alias of 'version'",
			"type": "content",
			"aliases": [
				"version"
			]
		},
		"location": {
			"label": "Location of publication",
			"description": "Geographical place of publication; usually not wikilinked; omit when the publication name includes place; alias of 'place'",
			"type": "string"
		},
		"publication-place": {
			"label": "Place of publication",
			"description": "Publication place shows after title; if 'place' or 'location' are also given, they are displayed before the title prefixed with 'written at'",
			"type": "content"
		},
		"publication-date": {
			"label": "Publication date",
			"description": "Date of publication when different from the date the work was written; do not wikilink",
			"type": "date"
		},
		"edition": {
			"label": "Edition",
			"description": "When the publication has more than one edition; for example: '2nd', 'Revised' etc.; suffixed with ' ed.'",
			"type": "line"
		},
		"volume": {
			"label": "Volume",
			"description": "For one publication published in several volumes",
			"type": "line",
			"suggested": true
		},
		"page": {
			"label": "Page",
			"description": "Page in the source that supports the content; displays after 'p.'",
			"type": "line"
		},
		"pages": {
			"label": "Pages",
			"description": "Pages in the source that support the content (not an indication of the number of pages in the source; displays after 'pp.'",
			"type": "line",
			"suggested": true
		},
		"no-pp": {
			"label": "No pp",
			"description": "Set to 'y' to suppress the 'p.' or 'pp.' display with 'page' or 'pages' when inappropriate (such as 'Front cover')",
			"type": "line"
		},
		"at": {
			"label": "At",
			"description": "May be used instead of 'page' or 'pages' where a page number is inappropriate or insufficient",
			"type": "line"
		},
		"language": {
			"label": "Language",
			"description": "The language in which the source is written, if not English; use the full language name; do not use icons or templates",
			"type": "content"
		},
		"script-title": {
			"label": "Script title",
			"description": "For titles in languages that do not use a Latin-based alphabet (Arabic, Chinese, Cyrillic, Greek, Hebrew, Japanese, Korean, Vietnamese, etc). Prefix with two-character ISO639-1 language code followed by a colon. For Japanese use: |script-title=ja:...",
			"type": "line"
		},
		"trans-title": {
			"label": "Translated title",
			"description": "An English language title, if the source cited is in a foreign language; 'language' is recommended",
			"type": "content"
		},
		"type": {
			"label": "Type",
			"description": "Additional information about the media type of the source; format in sentence case",
			"type": "content"
		},
		"format": {
			"label": "Format",
			"description": "Format of the work referred to by 'url' ('url' is required when using 'format'); examples: PDF, DOC, XLS; do not specify HTML",
			"type": "content"
		},
		"arxiv": {
			"label": "arXiv identifier",
			"description": "An identifier for arXive electronic preprints of scientific papers",
			"type": "line"
		},
		"asin": {
			"label": "ASIN",
			"description": "Amazon Standard Identification Number; 10 characters",
			"type": "line"
		},
		"asin-tld": {
			"label": "ASIN TLD",
			"description": "ASIN top-level domain for Amazon sites other than the US",
			"type": "line"
		},
		"bibcode": {
			"label": "Bibcode",
			"description": "Bibliographic Reference Code (REFCODE); 19 characters",
			"type": "line"
		},
		"biorxiv": {
			"label": "biorXiv",
			"description": "biorXiv identifier; 6 digits",
			"type": "line"
		},
		"citeseerx": {
			"label": "CiteSeerX",
			"description": "CiteSeerX identifier; found after the 'doi=' query parameter",
			"type": "line"
		},
		"isbn": {
			"label": "ISBN",
			"description": "International Standard Book Number; use the 13-digit ISBN where possible",
			"type": "line"
		},
		"issn": {
			"label": "ISSN",
			"description": "International Standard Serial Number; 8 characters; may be split into two groups of four using a hyphen",
			"type": "line"
		},
		"jfm": {
			"label": "jfm code",
			"description": "Jahrbuch über die Fortschritte der Mathematik classification code",
			"type": "line"
		},
		"jstor": {
			"label": "JSTOR",
			"description": "JSTOR identifier",
			"type": "line"
		},
		"lccn": {
			"label": "LCCN",
			"description": "Library of Congress Control Number",
			"type": "line"
		},
		"mr": {
			"label": "MR",
			"description": "Mathematical Reviews identifier",
			"type": "line"
		},
		"oclc": {
			"label": "OCLC",
			"description": "Online Computer Library Center number",
			"type": "number"
		},
		"ol": {
			"label": "OL",
			"description": "Open Library identifier",
			"type": "line"
		},
		"osti": {
			"label": "OSTI",
			"description": "Office of Scientific and Technical Information identifier",
			"type": "line"
		},
		"pmc": {
			"label": "PMC",
			"description": "PubMed Center article number",
			"type": "number"
		},
		"pmid": {
			"label": "PMID",
			"description": "PubMed Unique Identifier",
			"type": "line"
		},
		"rfc": {
			"label": "RFC",
			"description": "Request for Comments number",
			"type": "number"
		},
		"ssrn": {
			"label": "SSRN",
			"description": "Social Science Research Network",
			"type": "line"
		},
		"zbl": {
			"label": "Zbl",
			"description": "Zentralblatt MATH journal identifier",
			"type": "line"
		},
		"id": {
			"label": "id",
			"description": "A unique identifier used where none of the specialized ones are applicable",
			"type": "line"
		},
		"quote": {
			"label": "Quote",
			"description": "Relevant text quoted from the source; displays last, enclosed in quotes; needs to include terminating punctuation",
			"type": "content"
		},
		"ref": {
			"label": "Ref",
			"description": "An anchor identifier; can be made the target of wikilinks to full references; special value 'harv' generates an anchor suitable for the harv and sfn templates",
			"type": "line"
		},
		"postscript": {
			"label": "Postscript",
			"description": "The closing punctuation for the citation; ignored if 'quote' is defined; to suppress use reserved keyword 'none'",
			"type": "line",
			"default": "."
		},
		"last3": {
			"label": "Last name 3",
			"description": "The surname of the third author; don't wikilink, use 'author-link3'.",
			"aliases": [
				"author3"
			],
			"type": "line"
		},
		"first3": {
			"label": "First name 3",
			"description": "Given or first name, middle names, or initials of the third author; don't wikilink.",
			"type": "line"
		},
		"last4": {
			"label": "Last name 4",
			"description": "The surname of the fourth author; don't wikilink, use 'author-link4'.",
			"aliases": [
				"author4"
			],
			"type": "line"
		},
		"first4": {
			"label": "First name 4",
			"description": "Given or first name, middle names, or initials of the fourth author; don't wikilink.",
			"type": "line"
		},
		"last5": {
			"label": "Last name 5",
			"description": "The surname of the fifth author; don't wikilink, use 'author-link5'.",
			"aliases": [
				"author5"
			],
			"type": "line"
		},
		"first5": {
			"label": "First name 5",
			"description": "Given or first name, middle names, or initials of the fifth author; don't wikilink.",
			"type": "line"
		},
		"last6": {
			"label": "Last name 6",
			"description": "The surname of the sixth author; don't wikilink, use 'author-link6'.",
			"aliases": [
				"author6"
			],
			"type": "line"
		},
		"first6": {
			"label": "First name 6",
			"description": "Given or first name, middle names, or initials of the sixth author; don't wikilink.",
			"type": "line"
		},
		"last7": {
			"label": "Last name 7",
			"description": "The surname of the seventh author; don't wikilink, use 'author-link7'.",
			"aliases": [
				"author7"
			],
			"type": "line"
		},
		"first7": {
			"label": "First name 7",
			"description": "Given or first name, middle names, or initials of the seventh author; don't wikilink.",
			"type": "line"
		},
		"last8": {
			"label": "Last name 8",
			"description": "The surname of the eighth author; don't wikilink, use 'author-link8'.",
			"aliases": [
				"author8"
			],
			"type": "line"
		},
		"first8": {
			"label": "First name 8",
			"description": "Given or first name, middle names, or initials of the eighth author; don't wikilink.",
			"type": "line"
		},
		"last9": {
			"label": "Last name 9",
			"description": "The surname of the ninth author; don't wikilink, use 'author-link9'. If nine authors are defined, then only eight will show and 'et al.' will show in place of the last author.",
			"aliases": [
				"author9"
			],
			"type": "line"
		},
		"first9": {
			"label": "First name 9",
			"description": "Given or first name, middle names, or initials of the ninth author; don't wikilink.",
			"type": "line"
		},
		"editor2-last": {
			"label": "Editor last name 2",
			"description": "The surname of the second editor; don't wikilink, use 'editor2-link'.",
			"aliases": [
				"editor2"
			],
			"type": "line"
		},
		"editor2-first": {
			"label": "Editor first name 2",
			"description": "Given or first name, middle names, or initials of the second editor; don't wikilink.",
			"type": "line"
		},
		"editor3-last": {
			"label": "Editor last name 3",
			"description": "The surname of the third editor; don't wikilink, use 'editor3-link'.",
			"aliases": [
				"editor3"
			],
			"type": "line"
		},
		"editor3-first": {
			"label": "Editor first name 3",
			"description": "Given or first name, middle names, or initials of the third editor; don't wikilink.",
			"type": "line"
		},
		"editor4-last": {
			"label": "Editor last name 4",
			"description": "The surname of the fourth editor; don't wikilink, use 'editor4-link'.",
			"aliases": [
				"editor4"
			],
			"type": "line"
		},
		"editor4-first": {
			"label": "Editor first name 4",
			"description": "Given or first name, middle names, or initials of the fourth editor; don't wikilink.",
			"type": "line"
		},
		"editor5-last": {
			"label": "Editor last name 5",
			"description": "The surname of the fifth editor; don't wikilink, use 'editor5-link'.",
			"aliases": [
				"editor5"
			],
			"type": "line"
		},
		"editor5-first": {
			"label": "Editor first name 5",
			"description": "Given or first name, middle names, or initials of the fifth editor; don't wikilink.",
			"type": "line"
		},
		"editor6-last": {
			"label": "Editor last name 6",
			"description": "The surname of the sixth editor; don't wikilink, use 'editor6-link'.",
			"aliases": [
				"editor6"
			],
			"type": "line"
		},
		"editor6-first": {
			"label": "Editor first name 6",
			"description": "Given or first name, middle names, or initials of the sixth editor; don't wikilink.",
			"type": "line"
		},
		"editor7-last": {
			"label": "Editor last name 7",
			"description": "The surname of the seventh editor; don't wikilink, use 'editor7-link'.",
			"aliases": [
				"editor7"
			],
			"type": "line"
		},
		"editor7-first": {
			"label": "Editor first name 7",
			"description": "Given or first name, middle names, or initials of the seventh editor; don't wikilink.",
			"type": "line"
		},
		"editor8-last": {
			"label": "Editor last name 8",
			"description": "The surname of the eighth editor; don't wikilink, use 'editor8-link'.",
			"aliases": [
				"editor8"
			],
			"type": "line"
		},
		"editor8-first": {
			"label": "Editor first name 8",
			"description": "Given or first name, middle names, or initials of the eighth editor; don't wikilink.",
			"type": "line"
		},
		"editor9-last": {
			"label": "Editor last name 9",
			"description": "The surname of the ninth editor; don't wikilink, use 'editor9-link'.",
			"aliases": [
				"editor9"
			],
			"type": "line"
		},
		"editor9-first": {
			"label": "Editor first name 9",
			"description": "Given or first name, middle names, or initials of the ninth editor; don't wikilink.",
			"type": "line"
		},
		"author-mask": {
			"label": "Author mask",
			"description": "Replaces the name of the first author with em dashes or text; set to a numeric value 'n' to set the dash 'n' em spaces wide; set to a text value to display the text without a trailing author separator; for example, 'with' instead",
			"type": "string"
		},
		"author-link": {
			"label": "Author link",
			"description": "Title of existing Wikipedia article about the author; can suffix with a numeral to add additional authors",
			"type": "wiki-page-name",
			"aliases": [
				"author-link1",
				"author1-link"
			]
		},
		"author-link2": {
			"label": "Author link 2",
			"description": "Title of existing Wikipedia article about the second author.",
			"type": "wiki-page-name",
			"aliases": [
				"author2-link"
			]
		},
		"access-date": {
			"label": "URL access date",
			"description": "The full date when the original URL was accessed; do not wikilink",
			"type": "date"
		},
		"archive-url": {
			"label": "Archive URL",
			"description": "The URL of an archived copy of a web page, if or in case the URL becomes unavailable; requires 'archivedate'",
			"type": "line"
		},
		"archive-date": {
			"label": "Archive date",
			"description": "Date when the original URL was archived; do not wikilink",
			"type": "date"
		},
		"author-link3": {
			"label": "Author link 3",
			"description": "Title of existing Wikipedia article about the third author.",
			"type": "wiki-page-name",
			"aliases": [
				"author3-link"
			]
		},
		"author-link4": {
			"label": "Author link 4",
			"description": "Title of existing Wikipedia article about the fourth author.",
			"type": "wiki-page-name",
			"aliases": [
				"author4-link"
			]
		},
		"author-link5": {
			"label": "Author link 5",
			"description": "Title of existing Wikipedia article about the sixth author.",
			"type": "wiki-page-name",
			"aliases": [
				"author5-link"
			]
		},
		"author-link6": {
			"label": "Author link 6",
			"description": "Title of existing Wikipedia article about the sixth author.",
			"type": "wiki-page-name",
			"aliases": [
				"author6-link"
			]
		},
		"author-link7": {
			"label": "Author link 7",
			"description": "Title of existing Wikipedia article about the seventh author.",
			"type": "wiki-page-name",
			"aliases": [
				"author7-link"
			]
		},
		"author-link8": {
			"label": "Author link 8",
			"description": "Title of existing Wikipedia article about the eighth author.",
			"type": "wiki-page-name",
			"aliases": [
				"author8-link"
			]
		},
		"author-link9": {
			"label": "Author link 9",
			"description": "Title of existing Wikipedia article about the ninth author.",
			"type": "wiki-page-name",
			"aliases": [
				"author9-link"
			]
		},
		"editor2-link": {
			"label": "Editor link 2",
			"description": "Title of existing Wikipedia article about the second editor.",
			"type": "wiki-page-name",
			"aliases": [
				"editor2link",
				"editorlink2"
			]
		},
		"editor3-link": {
			"label": "Editor link 3",
			"description": "Title of existing Wikipedia article about the third editor.",
			"type": "wiki-page-name",
			"aliases": [
				"editor3link",
				"editorlink3"
			]
		},
		"editor4-link": {
			"label": "Editor link 4",
			"description": "Title of existing Wikipedia article about the fourth editor.",
			"type": "wiki-page-name",
			"aliases": [
				"editor4link",
				"editorlink4"
			]
		},
		"editor5-link": {
			"label": "Editor link 5",
			"description": "Title of existing Wikipedia article about the fifth editor.",
			"type": "wiki-page-name",
			"aliases": [
				"editor5link",
				"editorlink5"
			]
		},
		"editor6-link": {
			"label": "Editor link 6",
			"description": "Title of existing Wikipedia article about the sixth editor.",
			"type": "wiki-page-name",
			"aliases": [
				"editor6link",
				"editorlink6"
			]
		},
		"editor7-link": {
			"label": "Editor link 7",
			"description": "Title of existing Wikipedia article about the seventh editor.",
			"type": "wiki-page-name",
			"aliases": [
				"editor7link",
				"editorlink7"
			]
		},
		"editor8-link": {
			"label": "Editor link 8",
			"description": "Title of existing Wikipedia article about the eighth editor.",
			"type": "wiki-page-name",
			"aliases": [
				"editor8link",
				"editorlink8"
			]
		},
		"editor9-link": {
			"label": "Editor link 9",
			"description": "Title of existing Wikipedia article about the ninth editor.",
			"type": "wiki-page-name",
			"aliases": [
				"editor9link",
				"editorlink9"
			]
		},
		"display-authors": {
			"label": "Display authors",
			"description": "number of authors to display before 'et al.' is used;",
			"type": "number"
		},
		"via": {
			"label": "Content deliverer (i.e. Database)",
			"description": "Provider of the article (not the publisher), usually an aggregator of journal articles or a repository",
			"example": "JSTOR, Project MUSE, Elsevier Science Direct",
			"type": "string",
			"suggested": true
		},
		"url-access": {
			"label": "URL access level",
			"description": "Classification of the access restrictions on the URL ('registration', 'subscription' or 'limited')",
			"type": "string"
		},
		"bibcode-access": {
			"label": "Bibcode access level",
			"description": "If the full text is available from ADS via this Bibcode, type 'free'.",
			"type": "string"
		},
		"doi-access": {
			"label": "DOI access level",
			"description": "If the full text is free to read via the DOI, type 'free'.",
			"type": "string"
		},
		"hdl-access": {
			"label": "HDL access level",
			"description": "If the full text is free to read via the HDL, type 'free'.",
			"type": "string"
		},
		"jstor-access": {
			"label": "Jstor access level",
			"description": "If the full text is free to read on Jstor, type 'free'.",
			"type": "string"
		},
		"ol-access": {
			"label": "OpenLibrary access level",
			"description": "If the full text is free to read on OpenLibrary, type 'free'.",
			"type": "string"
		},
		"osti-access": {
			"label": "OSTI access level",
			"description": "If the full text is free to read on OSTI, type 'free'.",
			"type": "string"
		},
		"conference": {
			"label": "Conference",
			"description": "Name of the conference, may include location if different from location and date if different from date or year.",
			"type": "content",
			"required": true
		},
		"conference-url": {
			"aliases": [
			],
			"label": "Conference URL",
			"description": "URL of conference proceedings, if different from url.",
			"type": "url"
		}
	},
	"paramOrder": [
		"last",
		"first",
		"author-link",
		"last2",
		"first2",
		"author-link2",
		"last3",
		"first3",
		"author-link3",
		"last4",
		"first4",
		"author-link4",
		"last5",
		"first5",
		"author-link5",
		"last6",
		"first6",
		"author-link6",
		"last7",
		"first7",
		"author-link7",
		"last8",
		"first8",
		"author-link8",
		"last9",
		"first9",
		"author-link9",
		"display-authors",
		"author-mask",
		"date",
		"year",
		"orig-date",
		"editor-last",
		"editor-first",
		"editor-link",
		"editor2-last",
		"editor2-first",
		"editor2-link",
		"editor3-last",
		"editor3-first",
		"editor3-link",
		"editor4-last",
		"editor4-first",
		"editor4-link",
		"editor5-last",
		"editor5-first",
		"editor5-link",
		"editor6-last",
		"editor6-first",
		"editor6-link",
		"editor7-last",
		"editor7-first",
		"editor7-link",
		"editor8-last",
		"editor8-first",
		"editor8-link",
		"editor9-last",
		"editor9-first",
		"editor9-link",
		"others",
		"title",
		"script-title",
		"trans-title",
		"url",
		"format",
		"conference",
		"type",
		"series",
		"language",
		"edition",
		"location",
		"publisher",
		"publication-place",
		"publication-date",
		"volume",
		"issue",
		"page",
		"pages",
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
		"conference-url"
	],
	"maps": {
		"citoid": {
			"title": "title",
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
			"pages": "pages",
			"volume": "volume",
			"series": "series",
			"seriesNumber": "volume",
			"issue": "issue",
			"DOI": "doi",
			"oclc": "oclc",
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

<!--
==See also==
* [[Wikipedia:Cite sources]]: Style guide
* [[Wikipedia:Template messages/Sources of articles/Generic citations]]: Related templates
* [[Wikipedia:WikiProject Wikicite]]
* [[Wikipedia:Citing sources#Tools]] for a list of tools which can help create a reference in the 'cite conference' format.
-->

<includeonly>
<!-- ADD CATEGORIES BELOW THIS LINE -->
[[Category:引用模板|{{PAGENAME}}]]

<!-- ADD INTERWIKIS BELOW THIS LINE -->
[[cs:Šablona:Citace konference]]
[[en:Template:Cite conference]]
[[es:Plantilla:Cita conferencia]]
[[ja:Template:Cite conference]]
[[sl:Predloga:Navedi konferenco]]

</includeonly>