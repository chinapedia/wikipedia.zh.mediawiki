{{HTML}}
下表比较了[[XHTML|XHTML]]对一些[[排版引擎|排版引擎]]的支持与兼容性。请参阅各个产品的条目获得更多信息。除非脚注中另有规定，比较均基于稳定版本，无任何附加组件、扩展或外部程序。

本条目只靠路XHTML 1.1。[[XHTML|XHTML 1.1]]基于[[XHTML#XHTML_1.0|XHTML 1.0]]严格版，抛弃了更多的元素与属性。[[XHTML#XHTML_2.0|XHTML 2.0]]是一个工作草案，现未受到任何排版引擎的支持，为支持[[HTML5|HTML5]]和[[XHTML#XHTML5|XHTML5]]的工作，其于2009年被废弃。XHTML 1.0与[[HTML|HTML 4]]（二者均提供<code>text/html</code>）在[[排版引擎比较_(HTML)|排版引擎比较 (HTML)]]中进行了比较。关于XML兼容性的比较请参见[[排版引擎比较_(XML)|排版引擎比较 (XML)]]。

如给出了版本号，则说明自该版本起完全支持该特性。专有扩展不包括在内。

{{浏览器引擎命名}}
{{功能成熟度表格圖例}}

==媒体类型==
格式良好的XHTML文档通过不同的媒体类型送达时会获得响应。注意只有<code>application/xhtml+xml</code>是推荐媒体类型。
{| style="text-align: center; width: 95%;" class="wikitable"
! | [[互联网媒体类型|互联网媒体类型]]
! style="width: 11%;" | [[Trident_(排版引擎)|Trident]]
! style="width: 11%;" | [[Tasman|Tasman]]
! style="width: 11%;" | [[Gecko_(layout_engine)|Gecko]]
! style="width: 11%;" | [[WebKit|WebKit]]
! style="width: 11%;" | [[KHTML|KHTML]]
! style="width: 11%;" | [[Presto|Presto]]
! style="width: 11%;" | [[Prince_XML|Prince XML]]
|-
! style="text-align: left;" | <code>application/atom+xml</code>
| ?
| ?
| ?
| ?
| ?
| {{yes|8.00 beta 2}}<ref group="o">{{citation | url=http://www.opera.com/docs/history/#facts |title=Feature History |publisher=Opera}}</ref><ref group="o">{{cite web | title=Opera Features | work=RSS/Atom | url=http://www.opera.com/features/svg/ | archiveurl=https://web.archive.org/web/20050509013212/http://www.opera.com/features/ | archivedate=2005年5月9日 | deadurl=yes }}</ref>
| ?
|-
! style="text-align: left;" | <code>application/mathml+xml</code>
| {{no}}
| {{no}}
| {{yes|2.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=124709 |title=Bug 124709 - MIME type application/mathml+xml should be supported |publisher=Mozilla}}</ref>
| {{no}}
| {{no}}
| {{yes|9.50 beta 2}}<ref group="o">{{citation | url=http://www.opera.com/docs/history/#facts |title=Feature History |publisher=Opera}}</ref>
| ?
|-
! style="text-align: left;" | <code>application/rss+xml</code>
| ?
| ?
| ?
| ?
| ?
| {{yes|7.50 beta 1}}<ref group="o">{{citation | url=http://www.opera.com/docs/history/#facts |title=Feature History |publisher=Opera}}</ref><ref group="o">{{cite web | title=Opera Features | work=RSS | url=http://www.opera.com/features/svg/ | archiveurl=https://web.archive.org/web/20040802233018/http://www.opera.com/features/ | archivedate=2004年8月2日 | deadurl=yes }}</ref>
| ?
|-
! style="text-align: left;" | <code>application/xhtml+xml</code>
| {{yes|XHTML 5.0}}
| {{no|提示下载}}
| {{yes|XHTML}}
| {{yes|XHTML<br/>125}}
| {{partial|[[#khtml_xhtml|HTML]]}}
| {{yes|XHTML<br/>1.0}}
| ?
|-
! style="text-align: left;" | <code>application/xml</code>
| {{yes|XHTML 5.0}}
| {{no|崩溃}}
| {{yes|XHTML}}
| {{yes|XHTML<br/>125}}
| {{partial|[[#khtml_xml|XML]]}}
| {{yes|XHTML<br/>1.0}}
| ?
|-
! style="text-align: left;" | <code>application/xslt+xml</code>
| ?
| ?
| ?
| ?
| ?
| {{yes|9.00 beta 1}}<ref group="o">{{citation | url=http://www.opera.com/docs/history/#facts |title=Feature History |publisher=Opera}}</ref>
| ?
|-
! style="text-align: left;" | <code>image/svg+xml</code>
| ?
| ?
| {{yes|1.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=160882 |title=Bug 160882 - MIME type image/svg+xml should be supported |publisher=Mozilla}}</ref>
| ?
| ?
| {{yes|9.50}}<ref group="o">{{citation | url=http://www.opera.com/docs/history/#facts |title=Feature History |publisher=Opera}}</ref><ref group="o">{{cite web | title=Opera Features | work=SVG | url=http://www.opera.com/features/svg/ | accessdate=May 1, 2005 | archiveurl=https://web.archive.org/web/20050414082314/http://www.opera.com/features/svg/ | archivedate=2005年4月14日 | deadurl=yes }}</ref>
| ?
|-
! style="text-align: left;" | <code>text/xml</code>
| {{yes|XHTML 5.0}}
| {{no|崩溃}}
| {{yes|XHTML}}
| {{yes|XHTML<br/>125}}
| {{partial|[[#khtml_xml|XML]]}}
| {{yes|XHTML<br/>1.0}}
| ?
|-
! style="text-align: left;" | <code>text/html</code>
| {{yes|HTML}}
| {{yes|HTML}}
| {{yes|HTML}}
| {{yes|HTML}}
| {{yes|HTML}}
| {{yes|HTML}}
| ?
|-
|}

===KHTML媒体类型注释===
# <tt id="khtml_xhtml">application/xhtml+xml</tt> — KHTML支持该媒体类型，但将其视为HTML文档处理。
# <tt id="khtml_xml">application/xml, text/xml</tt> —通过定制DTD定义的HTML实体与自定义实体不被识别。

==联合配置==
通过结合[[XML|XML]]的其他应用程序（不是指使用img/object元素）扩展XHTML。
{| style="text-align: center; width: 95%;" class="wikitable"
! |
! style="width: 11%;" | [[Trident_(排版引擎)|Trident]]
! style="width: 11%;" | [[Tasman|Tasman]]
! style="width: 11%;" | [[Gecko_(layout_engine)|Gecko]]
! style="width: 11%;" | [[WebKit|WebKit]]
! style="width: 11%;" | [[KHTML|KHTML]]
! style="width: 11%;" | [[Presto|Presto]]
! style="width: 11%;" | [[Prince_XML|Prince XML]]
|-
! style="text-align: left;" | [[MathML|MathML]]
| {{no}}
| rowspan="4" {{no}}
| {{yes|1.0}}
| {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=3251 |title=Bug 3251 - Implement MathML (master bug) |publisher=WebKit}}</ref>
| {{no}}
| {{yes|2.1}}
| {{yes|6.0}}
|-
! style="text-align: left;" | [[Scalable_Vector_Graphics|SVG]]
| {{yes|5.0}}
| {{yes|1.8}}
| {{yes|522}}
| {{yes|3.2}}
| {{yes|1.0}}
| {{yes|5.1}}
|-
! style="text-align: left;" | [[XForms|XForms]]
| rowspan="2" {{no}}
| {{no}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=97806 |title=Bug 97806 - (xforms) Implement W3C XForms in browser and composer |publisher=Mozilla}}</ref>
| {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=10048 |title=Bug 10048 - ER: Add support for XForms |publisher=WebKit}}</ref>
| rowspan="2" {{no}}
| {{no}}
| ?
|-
! style="text-align: left;" | [[VoiceXML|VoiceXML]]
| {{no}}
| {{no}}
| {{yes|1.0}}
| {{no}}
|}

==参考来源==

===Gecko参考===
{{Reflist | group=g}}
*{{cite web | title=the mozilla.org projects list | work=MathML in Mozilla | url=http://www.mozilla.org/projects/mathml/ | accessdate=May 1, 2005}}
*{{cite web | title=the mozilla.org projects list | work=Mozilla SVG project | url=http://www.mozilla.org/projects/svg/ | accessdate=May 1, 2005}}
*{{cite web | title=the mozilla.org projects list | work=Mozilla XForms project | url=http://www.mozilla.org/projects/xforms/ | accessdate=May 1, 2005}}

===Opera参考===
{{Reflist | group=o}}

===WebKit参考===
{{Reflist | group=w}}

===其他参考===
*{{reflist}}
*{{cite web | title=W3C | work=XHTML media type test | url=http://www.w3.org/People/mimasa/test/xhtml/media-types/ | accessdate=May 1, 2005}}
*{{cite web | title=Developer's corner | work=Authoring XHTML+Voice | url=http://my.opera.com/community/dev/voice/ | accessdate=May 1, 2005}}

{{Layout engines}}

[[Category:HTML|Category:HTML]]
[[Category:排版引擎比较|Category:排版引擎比较]]