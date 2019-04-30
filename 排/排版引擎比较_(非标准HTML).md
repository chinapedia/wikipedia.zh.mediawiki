{{HTML}}
下表比较了不赞成使用和专有的[[HTML|HTML]][[HTML元素|元素]]与[[HTML|属性]]对一些[[排版引擎|排版引擎]]的支持和兼容性。请参阅各个产品的条目以获得更多信息。除非脚注中另有规定，比较均基于稳定版本，无任何附加组件、扩展或外部程序。

在[[万维网|万维网]]发展早期，[[网页浏览器|网页浏览器]]和[[网页|网页]]使用的标准还未成熟。[[网景|网景]]、[[微软|微软]]和[[MSN_TV|WebTV]]等供应商相互竞争，提供不同的浏览器与HTML编辑器，它们对如何构造网站都有自己的想法。这些不同的特征导致了网页开发者往往使用仅可被单一浏览器识别的元素为特定的网页浏览器编码。WebTV与IBM的WebExplorer从未被主流浏览器采用。

{{浏览器引擎命名}}
{{功能成熟度表格圖例}}

==不赞成使用的HTML元素==
{| class="wikitable" style="width: 95%; text-align: center;"
|-
! 元素
! 功能
! 率先支持
! 不赞成使用的HTML版本
! 代替方案
! style="width: 10%;" | [[Trident_(排版引擎)|Trident]]
! style="width: 10%;" | [[Gecko|Gecko]]
! style="width: 10%;" | [[WebKit|WebKit]]
! style="width: 10%;" | [[KHTML|KHTML]]
! style="width: 10%;" | [[Presto|Presto]]
|-
| <code>applet</code> || 插入一个小程序 || [[HotJava|HotJava]] || 4<ref>{{citation |title = HTML 4 Changes |publisher = [[World_Wide_Web_Consortium|W3C]] |date = 18 December 1997 |url = http://www.w3.org/TR/REC-html40/appendix/changes.html#h-A.3.1 |accessdate = 2008-05-07}}</ref> || <code>embed</code>、<code>object</code>
| {{IE|4.0}}
| {{Yes|1.7}}
| {{Yes}}
| rowspan="6" {{Yes}}
| {{Yes|1.0}}
|-
| <code>basefont</code> || 设置字体样式 || Internet Explorer || 4 || CSS
| {{IE|3.0}}
| {{No}}<ref name="basefont">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=3875 |title=Bug 3875 - (basefont) deprecated basefont element not supported |publisher=Mozilla}}</ref>
| {{Yes|85}}
| rowspan="4" {{Yes}}
|-
| <code>center</code> || 内容置中 || 网景<ref>{{citation |title = HTML 3.2 Reference Specification |publisher = [[World_Wide_Web_Consortium|W3C]] |date = 14 January 1997 |url = http://www.w3.org/TR/REC-html32.html#center |accessdate = 2008-10-08}}</ref> || 4 || CSS
| rowspan="3" {{Yes|3.1}}
| rowspan="3" {{Yes}}
| rowspan="3" {{Yes}}
|-
| <code>dir</code> || 目录列表 || ? || 4 || <code>ul</code>、<code>ol</code>
|-
| <code>font</code> || 应用字体样式 || 网景|| 4 || CSS
|-
| <code>isindex</code><ref>{{citation |title = Isindex Example |url = http://obscuretags.com/isindex.html |accessdate = 2008-05-07 |deadurl = yes |archiveurl = https://web.archive.org/web/20080405060957/http://obscuretags.com/isindex.html |archivedate = 2008-04-05 }}</ref> || 添加一个搜索栏 || ? || 4 || <code>input type="search"</code>
| {{IE|5.5}}
| rowspan="2" {{Yes|1.7}}
| {{Yes|312}}
| {{Partial}}
|-
| <code>listing</code> || 显示格式化文本 || [[IETF|IETF]] || 2 || <code>pre</code>、<code>samp</code>、<code>code</code>、CSS
| rowspan="3" {{Yes|3.1}}
| {{Yes|125}}
| {{Yes|3.3}}
| rowspan="3" {{Yes}}
|-
| <code>menu</code> || 菜单列表 || ? || 4 || <code>ul</code>、<code>ol</code>
| rowspan="2" {{Yes}}
| rowspan="5" {{Yes}}
| rowspan="5" {{Yes}}
|-
| <code>plaintext</code> || 所有内容按照HTML源代码的方式显示 || ? || 3.2 || The <code>text/plain</code> [[MIME_type|MIME type]]
|-
| <code>s</code> || 删除线 || ? || 4 || <code>del</code>、CSS
| rowspan="3" {{IE|4.0}}
| rowspan="4" {{Yes|1.7}}
| rowspan="4" {{Yes|1.0}}
|-
| <code>strike</code> || 删除线 || ? || 4 || <code>del</code>、CSS
|-
| <code>u</code> || 下划线 || ? || 4 || CSS
|-
| <code>xmp</code> || 与<code>pre和</code><code>plaintext</code>相似，内容按照HTML源代码的方式显示 || ? || 2 || <code>pre</code>、<code>samp</code>、<code>code</code>
| {{IE|3.0}}
| {{Yes|125}}
| {{Yes|3.3}}
|-
|}

==不赞成使用的HTML属性==
{| class="wikitable" style="width: 95%; text-align: center;"
|-
! 属性
! 元素
! 代替方案
! style="width: 10%;" | [[Trident_(排版引擎)|Trident]]
! style="width: 10%;" | [[Gecko|Gecko]]
! style="width: 10%;" | [[WebKit|WebKit]]
! style="width: 10%;" | [[KHTML|KHTML]]
! style="width: 10%;" | [[Presto|Presto]]
|-
| <code>align</code> || <code>caption</code>、<code>div</code>、<code>fieldset</code>、<code>h1</code>、<code>h2</code>、<code>h3</code>、<code>h4</code>、<code>h5</code>、<code>h6</code>、<code>hr</code>、<code>img</code>、<code>input</code>、<code>legend</code>、<code>p</code>、<code>object</code>、<code>table</code> || CSS
| rowspan="6" {{Yes|3.1}}
| rowspan="6" {{Yes}}
| {{Yes}}
| rowspan="18" {{Yes}}
| rowspan="18" {{Yes}}
|-
| <code>alink</code> || <code>body</code> || CSS
| {{No}}
|-
| <code>background</code> || <code>body</code> || CSS
| rowspan="2" {{Yes}}
|-
| <code>bgcolor</code> || <code>body</code>、<code>table</code>、<code>tr</code>、<code>td</code>、<code>th</code> || CSS
|-
| <code>border</code> || <code>img</code>、<code>object</code> || CSS
| {{Partial}}<ref group="注">仅支持<code>img</code>。</ref>
|-
| <code>clear</code> || <code>br</code> || CSS
| rowspan="2" {{No}}
|-
| <code>compact</code> || <code>dl</code>、<code>ul</code>、<code>ol</code> || CSS
| {{No}}
| {{No}}
|-
| <code>color</code> || <code>basefont</code>、<code>font</code> || CSS
| rowspan="11" {{Yes|3.1}}
| {{Partial}}<ref group="注" name="fontonly"/><ref name="basefont"/>
| {{Partial}}<ref group="注" name="fontonly">仅支持<code>font</code>。</ref>
|-
| <code>height</code> || <code>td</code>、<code>th</code> || CSS
| rowspan="2" {{Yes}}
| rowspan="10" {{Yes}}
|-
| <code>hspace</code> || <code>img</code>、<code>object</code> || CSS
|-
| <code>language</code> || <code>script</code> || <code>type</code>属性
| ？
|-
| <code>link</code> || <code>body</code> || CSS
| rowspan="7" {{Yes}}
|-
| <code>noshade</code> || <code>hr</code> || CSS
|-
| <code>nowrap</code> || <code>td</code>、<code>th</code> || CSS
|-
| <code>size</code> || <code>basefont</code>、<code>font</code>、<code>hr</code> || CSS
|-
| <code>start</code> || <code>ol</code> || None
|-
|-
| <code>text</code> || <code>body</code> || CSS
|-
| <code>type</code> || <code>li</code>、<code>ul</code>、<code>ol</code> || CSS
|-
| <code>version</code> || <code>html</code> || [[Document_Type_Declaration|DTD]]
| {{No}}
| {{No}}
| {{No}}
| {{No}}
| {{No}}
|-
| <code>vlink</code> || <code>body</code> || CSS
| rowspan="3" {{Yes}}
| rowspan="3" {{Yes}}
| rowspan="3" {{Yes}}
| rowspan="3" {{Yes}}
| rowspan="3" {{Yes}}
|-
| <code>width</code> || <code>hr</code>、<code>pre</code>、<code>td</code>、<code>th</code> || CSS
|-
| <code>vspace</code> || <code>img</code>、<code>object</code> || CSS
|-
|}

==专有HTML元素==
{| class="wikitable" style="width: 95%; text-align: center;"
! 标签
! 功能
! 引入
! 代替方案
! style="width: 10%;" | [[Trident_(排版引擎)|Trident]]
! style="width: 10%;" | [[Gecko|Gecko]]
! style="width: 10%;" | [[WebKit|WebKit]]
! style="width: 10%;" | [[KHTML|KHTML]]
! style="width: 10%;" | [[Presto|Presto]]
|-
| <code>bgsound</code> || 将声音添加到网站后台 || Internet Explorer || <code>audio</code>
| {{IE|3.0}}
| {{No}}
| {{No}}
| {{No}}
| {{dropped}}<ref>{{Cite web|url=http://my.opera.com/desktopteam/blog/2011/11/28/glyphs-and-plugins|date=28 November 2011|accessdate=28 November 2011|title=Opera Desktop Team - Glyphs and plugins|quote=CORE-34613 Drop support for <bgsound>|author=Tommy A. Olsen}}</ref>
|-
| <code>[[Blink_element|blink]]</code> || 用于显示闪烁的文字 || [[Netscape|网景]] || Javascript、CSS
| {{No}}
| {{dropped}}<ref>{{cite web|title=Mozilla Aurora Notes|url=https://www.mozilla.org/en-US/firefox/23.0a2/auroranotes/|publisher=Mozilla|accessdate=1 June 2013}}</ref>
| {{Yes}}
| {{No}}
| {{Yes|1.0}}
|-
| <code>bq</code> || 用于显示块引用 || WebTV、HTML 3.0 || <code>blockquote</code>
| {{No}}
| {{No}}
| {{No}}
| {{No}}
| {{dropped}}<ref>{{Cite web|url=http://krijnhoetmer.nl/irc-logs/whatwg/20100909#l-756|date=9 September 2010|accessdate=9 September 2010|title=IRC logs: freenode / #whatwg / 2010-09-09|quote=# [17:27] <gsnedders> I know we dropped support for the bq element :P|author=gsnedders}}</ref>
|-
| <code>comment</code> || 用于向HTML文档添加注释 || Internet Explorer、WebTV || <code><!-- ... --></code>
| {{Yes|3.1}}
| {{No}}
| {{No}}
| {{No}}
| {{No}}
|-
| <code>[[Layer_element|ilayer]]</code> || 内嵌层 || 网景（仅版本4） || <code>iframe</code>
| {{No}}
| {{No}}
| {{No}}
| {{Partial}}
| {{No}}
|-
| <code>image</code> || img的同义词 || ? || <code>img</code>
| {{Yes|3.1}}
| {{Yes}}
| {{Yes}}
| {{Yes}}
| {{Yes}}
|-
| <code>[[Layer_element|layer]]</code> || 用于创建多层文本和图像，在给定的顺序下分布在彼此的顶部 || 网景（仅版本4） || CSS、[[Ajax|Ajax]]
| {{No}}
| {{No}}
| {{No}}
| {{Partial}}
| {{No}}
|-
| <code>[[Marquee_element|marquee]]</code> || 用于显示类似滚动字幕的文本 || Internet Explorer、WebTV || JavaScript、CSS3
| {{Yes|3.1}}
| {{Yes|1.7}}
| {{Yes|125}}
| {{Yes|3.3}}
| {{Yes|1.0}}
|-
| <code>nobr</code> || 防止在文本流内产生任何换行符 || 网景<ref name="Complete List of HTML Tags">{{cite web|title=Complete List of HTML Tags|url=http://www.citycat.ru/doc/HTML/IExplorer.30/ie30html.htm|accessdate=10 October 2011}}</ref><ref name="Extensions to HTML">{{Cite web|url=http://home.mcom.com/home/services_docs/html-extensions.html|title=Extensions to HTML|publisher=Netscape|year=1994|accessdate=10 October 2011}}</ref> || CSS
| rowspan="2" {{Yes|3.1}}
| rowspan="2" {{Yes}}
| rowspan="2" {{Yes}}
| rowspan="2" {{Yes}}
| rowspan="2" {{Yes}}
|-
| <code>noembed</code> || 为不承认嵌入标签浏览器显示替代文本 || 网景 || 对象的子元素作为备用
|-
| <code>spacer</code> || 在排版中添加空白 || 网景 || CSS
| {{No}}
| {{Dropped}}<ref>{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=531056 |title=Bug 531056 - {{Bracket|HTML5}} Remove spacer support |publisher=Mozilla}}</ref>
| {{No}}
| {{No}}
| {{No}}
|-
| <code>wbr</code> || 放置在nobr元素中以添加一个换行符 || 网景<ref name="Complete List of HTML Tags"/><ref name="Extensions to HTML"/> || Unicode字符
[[零宽空格|零宽空格]]
（U+200B）
| {{dropped}}{{#tag:ref|Trident在5.0版本中不再支持<code>wbr</code>。<ref>{{citation |url=http://de.selfhtml.org/html/text/zeilenumbruch.htm#erlauben |title=Zeilenumbruch erlauben |language=de |publisher=Impressum}}</ref>|group=注}}
| {{Yes|1.7}}
| {{Yes}}
| {{Yes|3.1}}
| {{No}}
|-
| <code>xml</code><ref>{{citation |url=http://msdn.microsoft.com/en-us/library/ms535918(v=vs.85).aspx |title=<nowiki>XML Element | xml Object</nowiki> |publisher=Microsoft}}</ref> || 限定一个HTML页面中的XML数据岛 || Internet Explorer || ?
| {{Yes|3.1}}
| {{No}}
| {{No}}
| {{No}}
| {{No}}
|}

==专有HTML属性==
{| class="wikitable" style="width: 95%; text-align: center;"
|-
! 属性
! 被废弃
! 功能
! 率先支持
! style="width: 10%;" | [[Trident_(排版引擎)|Trident]]
! style="width: 10%;" | [[Gecko|Gecko]]
! style="width: 10%;" | [[WebKit|WebKit]]
! style="width: 10%;" | [[KHTML|KHTML]]
! style="width: 10%;" | [[Presto|Presto]]
|-
| <code>bgproperties</code> || <code>body</code> || 判定背景图片是否与背景一起滚动 || Internet Explorer
| rowspan="10" {{Yes|3.1}}
| {{No}}
| {{Yes}}
| {{Yes}}
| {{No}}
|-
| <code>bordercolor</code> || <code>body</code> || 在<code>table</code>、<code>td</code>、<code>th</code>与<code>tr</code>元素中设置三维表格边框的颜色 || Internet Explorer
| {{No}}
| {{Yes}}
| {{Yes}}
| {{No}}
|-
| <code>bordercolordark</code> || <code>body</code> || 在<code>table</code>、<code>td</code>、<code>th</code>与<code>tr</code>元素中设置三维表格边框的颜色 || Internet Explorer
| rowspan="2" {{No}}
| rowspan="2" {{No}}
| rowspan="2" {{No}}
| rowspan="2" {{No}}
|-
| <code>bordercolorlight</code> || <code>body</code> || 在<code>table</code>、<code>td</code>、<code>th</code>与<code>tr</code>元素中设置三维表格边框的颜色 || Internet Explorer
|-
| <code>controls</code> || <code>img</code> || 使用<code>img</code>元素放置视频或音频片段 || Internet Explorer
| {{No}}
| {{No}}
| {{No}}
| {{No}}
|-
| <code>dynsrc</code> || <code>img</code> || 使用<code>img</code>元素放置视频或音频片段 || Internet Explorer
| {{No}}
| {{No}}
| {{No}}
| {{No}}
|-
| <code>event</code> || <code>script</code> || 定义一个函数用于调用对象 || Internet Explorer
| {{Partial}}
| ?
| ?
| ?
|-
| <code>for</code> || <code>script</code> || 定义一个对象用于绑定脚本事件 || Internet Explorer
| {{Partial}}
| ?
| ?
| ?
|-
| <code>frame</code> || <code>table</code> || 在table标签中控制表的外边界显示 || Internet Explorer
| {{Yes}}
| ?
| {{Yes}}
| {{No}}
|-
| <code>framespacing</code> || <code>frameset</code> || 设置框架之间空间的多少 || Internet Explorer
| ?
| ?
| {{No}}
| {{No}}
|-
| <code>leftmargin</code> || <code>body</code> || 设置浏览器窗口和网页内容之间的边距 || Internet Explorer
| rowspan="2" {{Yes|3.1}}
| ?
| ?
| {{Yes}}
| {{No}}
|-
| <code>loop</code> || <code>img</code> || 使用<code>img</code>元素放置视频或音频片段 || Internet Explorer
| {{No}}
| {{No}}
| {{No}}
| {{No}}
|-
| <code>rightmargin</code> || <code>body</code> || 设置浏览器窗口和网页内容之间的边距 || Internet Explorer
| rowspan="3" {{Yes|3.1}}
| ?
| ?
| {{No}}
| {{No}}
|-
| <code>start</code> || <code>img</code> || 使用<code>img</code>元素放置视频或音频片段 || Internet Explorer
| {{No}}
| {{No}}
| {{No}}
| {{No}}
|-
| <code>target</code> || <code>form</code> || 为表单的输出指定目标窗口或框架 || Internet Explorer
| {{No}}<ref>{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=207900 |title=Bug 207900 - psychotekk.de - the target attribute in the form element is ignored |publisher=Mozilla}}</ref>
| ?
| {{Yes}}
| {{No}}
|-
| <code>valign</code> || <code>caption</code> || 将表格标题的设置为垂直对齐 || Internet Explorer
| {{Yes|3.1}}
| ?
| ?
| {{No}}
| {{No}}
|}

==参见==
* [[網頁標準|网页标准]]
*[[無線標記語言|无线标记语言]]

==注释==
{{Reflist| group=注}}

== 参考文献 ==
{{Reflist}}
{{refbegin}}
* {{Cite web |url=http://www.devguru.com/technologies/html/quickref/html_other_tags.html |title=DevGuru HTML - Non-standard elements |access-date=2016-02-06 |archive-url=https://web.archive.org/web/20130129131222/http://www.devguru.com/technologies/html/quickref/html_other_tags.html |archive-date=2013-01-29 |dead-url=yes }}
* [https://web.archive.org/web/20080706145821/http://www.seds.org/~spider/os2/webextag.html OS/2 Web Explorer's proprietary HTML elements]
* [http://msdn.microsoft.com/en-us/library/aa242436(VS.60).aspx MSDN Handling Events with HTML elements]
{{refend}}

{{-}}
{{Layout engines}}

[[Category:HTML|Category:HTML]]
[[Category:排版引擎比较|Category:排版引擎比较]]