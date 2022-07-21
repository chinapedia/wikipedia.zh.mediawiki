{{Infobox
| bodyclass = vcard
| bodystyle = {{#if:{{{infoboxwidth|{{{width|}}}}}} |width:{{{infoboxwidth|{{{width}}}}}} }}
| titlestyle = padding-bottom:0.2em;
| above = {{{圖書名稱|{{{name|{{{書名|{{{书名|{{{title|{{PAGENAMEBASE}}}}}}}}}}}}}}}}}
| abovestyle = background:#cedeff;

| imagestyle = {{#if:{{{圖書封面|{{{image|{{{图像|{{{圖像|{{{圖片|{{{图片|}}}}}}}}}}}}}}}}}}||display:none}}
| image = {{#if:{{{圖書封面|{{{image|{{{图像|{{{圖像|{{{圖片|{{{图片|}}}}}}}}}}}}}}}}}}|{{#ifeq:{{Str left | {{{圖書封面|{{{image|{{{图像|{{{圖像|{{{圖片|{{{图片|}}}}}}}}}}}}}}}}}} | 1 }}|[|[[Category:需要更新图片参数的图书信息框]]}}{{#invoke:InfoboxImage|InfoboxImage|image={{{圖書封面|{{{image|{{{图像|{{{圖像|{{{圖片|{{{图片|FETCH_WIKIDATA}}}}}}}}}}}}}}}}}}|size={{{圖書封面尺寸|{{{image_size|{{{圖片大小|{{{图片大小|}}}}}}}}}}}}|sizedefault=frameless|alt={{{alt|{{{圖片替代|{{{图片替代|}}}}}}}}}|border={{{border|}}}|suppressplaceholder=yes}}|{{main other|{{#property:P18}}[[Category:缺少封面的圖書]]}}}}
| caption = {{{caption|{{{image_caption|{{{图像说明|{{{圖像說明|{{{圖片簡介|{{{图片简介|{{{圖片說明|{{{图片说明|}}}}}}}}}}}}}}}}}}}}}}}}

| subheader = {{#if:{{{全名|}}}|全名：{{{全名|}}}}}

| labelstyle = white-space:nowrap;

| label4 = 副标题
| data4 = {{#invoke:Wikidata|getValue|P1680|{{{副書名|FETCH_WIKIDATA}}}}}

| label5 = 其他名称
| data5 = {{{altnames|{{{別名|{{{别名|}}}}}}}}}

| label6 = 原名
| data6 = {{{title_orig|{{{原名|}}}}}}

| label7 = 中文名
| data7 = {{{chinese_name|{{{中文书名|{{{中文書名|}}}}}}}}}

| label8 = 外文名
| data8 = {{{外文名|}}}{{#if:{{{假名|}}}|{{#if:{{{外文名|}}}|<br>}}假名：{{lang|ja|{{{假名}}}}}}}{{#if:{{{諺文|{{{谚文|}}}}}}|{{#if:{{{假名|}}}{{{外文名|}}}|<br>}}谚文：{{lang|ko|{{{諺文|{{{谚文}}}}}}}}}}{{#if:{{{羅馬拼音|{{{罗马拼音|}}}}}}|{{#if:{{{諺文|{{{谚文|}}}}}}{{{假名|}}}{{{外文名|}}}|<br>}}羅馬拼音：{{lang|en|{{{羅馬拼音|{{{罗马拼音}}}}}}}}}}

| label11 = 作者
| data11 = {{{撰者|{{{authors|{{{author|{{{creator|{{{作者|
 {{#if:{{#property:P50}}|
 {{#ifexist:{{#property:P50}}|[[{{#property:P50}}]]|{{#property:P50}}}}
 }}
}}}}}}}}}}}}}}}{{#if:{{{託名作者|{{{托名作者|}}}}}}|{{#if:{{{撰者|{{{authors|{{{author|{{{creator|{{{作者|
 {{#if:{{#property:P50}}|
 {{#ifexist:{{#property:P50}}|[[{{#property:P50}}]]|{{#property:P50}}}}
 }}
}}}}}}}}}}}}}}}|<br>}}託名：{{{託名作者|{{{托名作者|}}}}}}}}

| label12 = 编者
| data12 = {{{editors|{{{编者|{{{編者|{{{編集者|{{{编集者|}}}}}}}}}}}}}}}{{#if:{{{輯錄者|{{{辑录者|}}}}}}|{{#if:{{{editors|{{{编者|{{{編者|{{{編集者|{{{编集者|}}}}}}}}}}}}}}}|<br>}}輯錄者：{{{輯錄者|{{{辑录者|}}}}}}}}

{{#if:{{{註解者|{{{注解者|}}}}}}|{{#if:{{{輯錄者|{{{辑录者|}}}}}}{{{editors|{{{编者|{{{編者|{{{編集者|{{{编集者|}}}}}}}}}}}}}}}|<br>}}{{{註解者|{{{注解者|}}}}}}}}

| label13 = 译者
| data13 = {{#invoke:Wikidata|getValue|P655|{{{translators|{{{translator|{{{译者|{{{譯者|}}}}}}}}}}}}}}

| label14 = 创作时间
| data14 = {{{創作時間|{{{创作时间|}}}}}}

| label15 = 类型
| data15 = {{#if:{{#property:P466}}|{{#invoke:Wikidata|getValue|P136|{{{genres|{{{genre|{{{类型|{{{類型|{{{分類|{{{分类|FETCH_WIKIDATA}}}}}}}}}}}}}}}}}}}}|{{#invoke:Wikidata|getValue|P31|{{{genres|{{{genre|{{{类型|{{{類型|{{{分類|{{{分类|FETCH_WIKIDATA}}}}}}}}}}}}}}}}}}}}}}

| label16 = 系列
| data16 = {{#invoke:Wikidata|getValue|P179|{{{series|{{{系列|FETCH_WIKIDATA}}}}}}}}

| label17 = 学科
| data17 = {{{discipline|{{{学科|{{{學科|}}}}}}}}}

| label18 = 语言
| data18 = {{#invoke:Wikidata|getValue|P407|{{{language|{{{语言|{{{語言|FETCH_WIKIDATA}}}}}}}}}}}{{#if:{{{文字|}}}|{{#if:{{#invoke:Wikidata|getValue|P407|{{{language|{{{语言|{{{語言|FETCH_WIKIDATA}}}}}}}}}}}|<br>文字：}}{{{文字|}}}}}

| label19 = 版本
| data19 = {{{版本|}}}

| label20 = 成书年代
| data20 = {{{成書年代|{{{成书年代|}}}}}}

| label21 = 亡佚年代
| data21 = {{{亡佚年代|}}}

| label22 = 伪托年代
| data22 = {{{偽託年代|{{{伪托年代|}}}}}}

| label23 = 主题
| data23 = {{#invoke:Wikidata|getValue|delimiter=、|P921|{{{subject|{{{subjects|{{{题材|{{{題材|FETCH_WIKIDATA}}}}}}}}}}}}}}

| label24 = 故事时代背景
| data24 = {{#invoke:Wikidata|getValue|P2408|{{{period|FETCH_WIKIDATA}}}}}

| label25 = 故事背景地
| data25 = {{#invoke:Wikidata|getValue|P840|{{{narrative location|FETCH_WIKIDATA}}}}}

| headerstyle = background:#cedeff;
| header30 = {{#if:{{{總編輯|}}}{{{editors|{{{editor|}}}}}}{{{社長|}}}{{{illustrator|{{{插图|{{{插圖|}}}}}}}}}{{{cover_artist|{{{封面设计|{{{封面設計|}}}}}}}}}{{{published|}}}{{{publisher|{{{出版者|{{{出版商|}}}}}}}}}{{{publisher2|}}}{{{發行商|}}}{{{發行人|}}}{{{language|{{{语言|{{{語言|}}}}}}}}}{{{首次刊载|}}}{{{country|{{{出版地|{{{出版國家或地區|{{{出版国家或地区|}}}}}}}}}}}}{{{發行地區|}}}{{{pub_date|{{{release_date|{{{出版時間|{{{發行時間|{{{出版日期|{{{發行日期|}}}}}}}}}}}}}}}}}}{{{chinese_pub_date|{{{chinese_release_date|{{{中文版|}}}}}}}}}{{{chinese_publisher|}}}{{{media_type|{{{媒介|}}}}}}{{{pages|{{{页数|{{{頁數|}}}}}}}}}{{{format|{{{开本|{{{開本|}}}}}}}}}{{{number_of_books|}}}{{{售價|}}}{{{銷售量|}}}{{{awards|{{{award|}}}}}}|發行-{zh-hans:信息; zh-hant:情況;}-}}

| label31 = 连载状态
| data31 = {{{status|{{{current|}}}}}}{{#if:{{{篇數|{{{篇数|}}}}}}|{{#if:{{{status|{{{current|}}}}}}|<br>}}篇数：{{{篇數|{{{篇数|}}}}}}}}{{#if:{{{原書篇數|{{{原书篇数|}}}}}}|{{#if:{{{status|{{{current|}}}}}}{{{篇數|{{{篇数|}}}}}}|<br>}}原書篇數：{{{原書篇數|{{{原书篇数|}}}}}}}}{{#if:{{{今本篇數|{{{今本篇数|}}}}}}|{{#if:{{{status|{{{current|}}}}}}{{{原書篇數|{{{原书篇数|}}}}}}{{{篇數|{{{篇数|}}}}}}|<br>}}今本篇數：{{{今本篇數|{{{今本篇数|}}}}}}}}{{#if:{{{卷數|{{{卷数|}}}}}}|{{#if:{{{status|{{{current|}}}}}}{{{原書篇數|{{{原书篇数|}}}}}}{{{篇數|{{{篇数|}}}}}}{{{今本篇數|{{{今本篇数|}}}}}}|<br>}}卷數：{{{卷數|{{{卷数|}}}}}}}}{{#if:{{{原書卷數|{{{原书卷数|}}}}}}|{{#if:{{{status|{{{current|}}}}}}{{{卷數|{{{卷数|}}}}}}{{{原書篇數|{{{原书篇数|}}}}}}{{{篇數|{{{篇数|}}}}}}{{{今本篇數|{{{今本篇数|}}}}}}|<br>}}原書卷數：{{{原書卷數|{{{原书卷数|}}}}}}}}{{#if:{{{今本卷數|{{{今本卷数|}}}}}}|{{#if:{{{status|{{{current|}}}}}}{{{原書卷數|{{{原书卷数|}}}}}}{{{卷數|{{{卷数|}}}}}}{{{原書篇數|{{{原书篇数|}}}}}}{{{篇數|{{{篇数|}}}}}}{{{今本篇數|{{{今本篇数|}}}}}}|<br>}}今本卷數：{{{今本卷數|{{{今本卷数|}}}}}}}}{{#if:{{{章回|}}}|{{#if:{{{status|{{{current|}}}}}}{{{今本卷數|{{{今本卷数|}}}}}}{{{原書卷數|{{{原书卷数|}}}}}}{{{卷數|{{{卷数|}}}}}}{{{原書篇數|{{{原书篇数|}}}}}}{{{篇數|{{{篇数|}}}}}}{{{今本篇數|{{{今本篇数|}}}}}}|<br>}}章回：{{{章回|}}}}}

| label32 = 首次刊载处
| data32 = {{#invoke:Wikidata|getValue|P1433|{{{首次刊载|FETCH_WIKIDATA}}}}}

| label33 = 收录于
| data33 = {{{published_in|{{{released_in|{{{最初著錄|{{{最初著录|}}}}}}}}}}}}

| label34 = 收录小说类型
| data34 = {{{publication_type|}}}

| labe35 = 总编辑
| dat35 = {{{總編輯|{{{总编辑|}}}}}}

| label36 = 編輯
| data36 = {{#invoke:Wikidata|getValue|P98|{{{editors|{{{editor|FETCH_WIKIDATA}}}}}}}}

| label37 = 社長
| data37 = {{{社長|{{{社长|}}}}}}

| label38 = 封面設計
| data38 = {{{cover_artist|{{{封面设计|{{{封面設計|}}}}}}}}}

| label39 = 插圖
| data39 = {{#invoke:Wikidata|getValue|P110|{{{illustrator|{{{插图|{{{插圖|FETCH_WIKIDATA}}}}}}}}}}}

| label40 = 出版
| data40 = {{{published|}}}

| label41 = 出版机构
| data41 = {{#invoke:Wikidata|getValue|P123|{{{出版社|{{{publisher|{{{出版者|{{{出版商|FETCH_WIKIDATA}}}}}}}}}}}}}}{{#if:{{{publisher2|}}}|、{{{publisher2}}}}}

| label42 = 发行机构
| data42 = {{{發行商|{{{发行机构|}}}}}}{{{syndicate|}}}

| label43 = 发行人
| data43 = {{{發行人|{{{发行人|}}}}}}

| label44 = 连载开始日期
| data44 = {{{began|{{{first|}}}}}}

| label45 = 连载结束日期
| data45 = {{{ended|{{{last|}}}}}}

| label46 = 出版時間
| data46 = {{If then show|{{{pub_date|{{{release_date|{{{出版時間|{{{發行時間|{{{出版日期|{{{發行日期|}}} }}} }}} }}} }}} }}} | {{#invoke:WikidataIB |getValue|P577|fwd=ALL |osd=no}} }}

| label47 = 出版地
| data47 = {{{country|{{{出版地|{{{出版國家或地區|{{{出版国家或地区|{{{發行地區|{{{國家|{{{国家|}}}}}}}}}}}}}}}}}}}}}

| label48 = 中譯本出版日期
| data48 = {{{chinese_pub_date|{{{chinese_release_date|{{{中文版|}}}}}}}}}

| label49 = 中譯本出版機構
| data49 = {{{chinese_publisher|}}}

| label51 = 媒介
| data51 = {{{media_type|{{{媒介|}}}}}}

| label52 = 開本
| data52 = {{{format|{{{开本|{{{開本|}}}}}}}}}

| label53 = 页数
| data53 = {{#invoke:Wikidata|getValue|P1104|{{{pages|{{{页数|{{{頁數|FETCH_WIKIDATA}}}}}}}}}}}

| label54 = 数量
| data54 = {{{number_of_books|}}} {{#if:{{{list_books|}}}|（[[{{{list_books}}}|列表]]）}}

| label55 = 售价
| data55 = {{{售價|{{{售价|}}}}}}

| label56 = 销量
| data56 = {{{銷售量|{{{销售量|}}}}}}

| label57 = 所获奖项
| data57 = {{#invoke:Wikidata|getValue|P166|{{{rating|{{{awards|{{{award|FETCH_WIKIDATA}}}}}}}}}}}

| label58 = 網站
| data58 = {{{website|{{{homepage|{{{URL|{{{url|{{{官方網站|{{#ifeq:{{{website|{{{homepage|{{{URL|{{{url|{{{官方網站|}}}}}}}}}}}}}}}
 | FETCH_WIKIDATA
 | {{#if:{{#property:P856}}|{{Url|1={{#invoke:Wikidata|getValue|P856|FETCH_WIKIDATA}} }} }}
 |}}}}}}}}}}}}}}}}}{{#if:{{{rss|}}}|<br />{{RSS|1={{{rss}}} RSS web feed}} }}{{#if:{{{atom|}}}|<br />{{atom|1={{{atom}}} Atom web feed}} }}

| header60 = {{#if:{{{books|}}}{{#property:P527}}|系列作品}}
| data61 = {{#invoke:Wikidata|getValue|P527|{{{books|FETCH_WIKIDATA}}}}}

| label62 = 上一部作品
| data62 = {{#invoke:Wikidata|getValue|P155|{{{preceded_by|{{{preceded by|{{{上一部作品|FETCH_WIKIDATA}}}}}}}}}}}

| label63 = 下一部作品
| data63 = {{#invoke:Wikidata|getValue|P156|{{{followed_by|{{{followed by|{{{下一部作品|FETCH_WIKIDATA}}}}}}}}}}}

| label64 = 引用
| data64 = {{{citing|{{{引用|}}}}}}

| label65 = 被引用
| data65 = {{{cited|{{{被引用|}}}}}}

| header70 = {{{nrhp|{{{embedded|}}}}}}
| data71 = {{{module|}}}

| label72 = {{longitem|原始文本}}
| data72 = {{#if:{{{native_wikisource|}}} <!--
 then:-->| 《{{lang|{{{orig_lang_code|}}}
                  |[[s:{{#if:{{{orig_lang_code|}}}|{{{orig_lang_code|}}}:}}{{{native_wikisource|}}}|{{{title_orig|{{{name|{{PAGENAME}}}}}}}}]]<!--
 -->}}》（出自<!--
 -->{{#ifeq:{{#language:{{{orig_lang_code}}}}}|{{{orig_lang_code}}} |
                  | {{iso2lang|{{{orig_lang_code}}}}}<!--
 -->}}[[維基文庫]]）<!--
 -->{{main other|[[Category:連往外語維基文庫的條目]]}} <!--(create hidden category to be monitored by WikiProject:Wikisource)
 else:-->| {{#if:{{{native_external_url|}}}
 | ''{{lang |{{{orig_lang_code|}}}
                     | [{{{native_external_url|}}} {{{title_orig|{{{name|{{PAGENAME}}}}}}}}]<!--
 -->}}'' <!--
 -->{{#if:{{{native_external_host|}}} |見{{{native_external_host|}}} |在線}}
 }} }}

| label73 = {{#if:{{{native_wikisource|}}} |譯本|{{#if:{{{native_external_url|}}}|譯本|文本}} }}
| data73 = {{#if:{{{wikisource|}}} <!--
 then:-->| [[s:{{{wikisource|}}}|{{{name|{{PAGENAME}}}}}]]在<!--
 -->{{#if:{{{native_wikisource|}}} |Wikisource |[[维基文库]]上的版本}}<!--
 -->{{main other|[[Category:連往維基文庫的條目]]}} <!--(create hidden category to be monitored by WikiProject:Wikisource)
 else:-->| {{#if:{{{external_url|}}}
 | ''[{{{external_url|}}} {{{name|{{PAGENAME}}}}}]'' <!--
 -->{{#if:{{{external_host|}}} |見{{{external_host|}}} |在線}}
 }} }}


| header90 = {{#if:{{{isbn|}}}{{{ISBN|}}}{{{oclc|{{{OCLC|}}}}}}{{{dewey|{{{杜威十进制图书分类法|{{{杜威十進制圖書分類法|}}}}}}}}}{{{congress|{{{美国国会图书馆图书分类法|{{{美國國會圖書館圖書分類法|}}}}}}}}}{{#property:P212}}{{#property:P5331}}|[[權威控制|规范控制]]}}
| label91 = <span class=type>[[国际标准书号|ISBN]]</span>
| data91 ={{#if:{{{isbn|}}}{{{ISBN|}}} | {{#iferror: {{#expr:{{{isbn}}}}}
 | {{{ISBN|{{{isbn|}}}}}} | <span class=value>[[Special:网络书源/{{{ISBN|{{{isbn|}}}}}}|{{{ISBN|{{{isbn|}}}}}}]]</span> }} |{{#property:P212}}}} {{{isbn_note|{{{ISBN_note|}}}}}}

| label92 = [[统一书号|CSBN]]
| data92 = {{{csbn|{{{统一书号|{{{統一書號|}}}}}}}}}

| label93 = <span class="type">[[OCLC|{{abbr|OCLC|联机计算机图书馆中心号}}]]</span>
| data93 = {{#if:{{{oclc|{{{OCLC|}}}}}}{{#property:P5331}}| <span class=value>[//www.worldcat.org/oclc/{{urlencode:{{#invoke:Wikidata|getValue|P5331|{{{oclc|{{{OCLC|FETCH_WIKIDATA}}}}}}}}}} {{#invoke:Wikidata|getValue|P5331|{{{oclc|{{{OCLC|FETCH_WIKIDATA}}}}}}}}]</span> }}

| label94 = [[杜威十进制图书分类法|杜威分类法]]
| data94 = {{{dewey|{{{杜威十进制图书分类法|{{{杜威十進制圖書分類法|}}}}}}}}}

| label95 = <span class="type">[[美国国会图书馆图书分类法|LC分类法]]</span>
| data95 = {{{congress|{{{美国国会图书馆图书分类法|{{{美國國會圖書館圖書分類法|}}}}}}}}}

| belowstyle = border-top:1.5px solid #aaa; text-align:left;
| below = {{{notes|{{{note|{{{備註|}}}}}}}}}
}}{{#invoke:Check for unknown parameters|check|unknown={{main other|[[Category:使用未知书籍信息框参数的页面|_VALUE_{{PAGENAME}}]]}}|preview=页面使用了[[Template:Infobox book]]不存在的参数"_VALUE_"|ignoreblank=y | infoboxwidth | width | 圖書名稱 | name | 書名 | 书名 | title | 圖書封面 | image | 图像 | 圖像 | 圖片 | 图片 | 圖書封面尺寸 | image_size | 圖片大小 | 图片大小 | alt | 圖片替代 | 图片替代 | border | caption | image_caption | 图像说明 | 圖像說明 | 圖片簡介 | 图片简介 | 圖片說明 | 图片说明 | 全名 | 副書名 | altnames | 別名 | 别名 | title_orig | 原名 | chinese_name | 中文书名 | 中文書名 | 外文名 | 假名 | 諺文 | 谚文 | 羅馬拼音 | 罗马拼音 | 撰者 | authors | author | creator | 作者 | 託名作者 | 托名作者 | editors | 编者 | 編者 | 編集者 | 编集者 | 輯錄者 | 辑录者 | 註解者 | 注解者 | translator | translators |译者 | 譯者 | 創作時間 | 创作时间 | genres | genre | 类型 | 類型 | 分類 | 分类 | series | 系列 | discipline | 学科 | 學科 | language | 语言 | 語言 | 文字 | 版本 | 成書年代 | 成书年代 | 亡佚年代 | 偽託年代 | 伪托年代 | subject | subjects | 题材 | 題材 | period | narrative location | 總編輯 | editor | 社長 | illustrator | 插图 | 插圖 | cover_artist | 封面设计 | 封面設計 | published | publisher | 出版者 | 出版商 | publisher2 | 發行商 | 發行人 | 首次刊载 | country | 出版地 | 出版國家或地區 | 出版国家或地区 | 發行地區 | pub_date | release_date | 出版時間 | 發行時間 | 出版日期 | 發行日期 | chinese_pub_date | chinese_release_date | 中文版 | chinese_publisher | media_type | 媒介 | pages | 页数 | 頁數 | format | 开本 | 開本 | number_of_books | 售價 | 銷售量 | awards | award | status | current | 篇數 | 篇数 | 原書篇數 | 原书篇数 | 今本篇數 | 今本篇数 | 卷數 | 卷数 | 原書卷數 | 原书卷数 | 今本卷數 | 今本卷数 | 章回 | published_in | released_in | 最初著錄 | 最初著录 | publication_type | 总编辑 | 社长 | 发行机构 | syndicate | 发行人 | began | first | ended | last | 國家 | 国家 | list_books | 售价 | 销售量 | rating | website | homepage | URL | url | 官方網站 | rss | atom | books | preceded_by | preceded by | 上一部作品 | followed_by | followed by | 下一部作品 | citing | 引用 | cited | 被引用 | nrhp | embedded | module | native_wikisource | orig_lang_code | native_external_url | native_external_host | wikisource | external_url | external_host | isbn | ISBN | oclc | OCLC | dewey | 杜威十进制图书分类法 | 杜威十進制圖書分類法 | congress | 美国国会图书馆图书分类法 | 美國國會圖書館圖書分類法 | isbn_note | ISBN_note | notes | note | 備註 | csbn | 统一书号 | 統一書號 }}<noinclude>
{{documentation}}
</noinclude>