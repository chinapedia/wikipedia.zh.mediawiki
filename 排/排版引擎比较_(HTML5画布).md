{{HTML}}
下表比较了[[HTML5|HTML5]][[Canvas_(HTML元素)|画布元素]]对绘图[[API|API]]的支持及网页浏览器的原生支持程度，无任何[[插件|插件]]、附加组件或[[ECMAScript|ECMAScript]]工作区。

{{浏览器引擎命名}}
{{功能成熟度表格圖例}}

==画布功能==
{| style="text-align: center; width: 95%" class="wikitable"
|-
! |
! style="width: 18%;" | [[Trident_(排版引擎)|Trident]]
! style="width: 18%;" | [[Gecko_(layout_engine)|Gecko]]
! style="width: 18%;" | [[WebKit|WebKit]]
! style="width: 18%;" | [[Presto|Presto]]
|-
! style="text-align: left;" | <code>getContext</code>
| rowspan="2" {{yes|5.0}}
| {{yes|1.8}}
| {{yes}}
| {{yes|2.0}}
|-
! style="text-align: left;" | <code>toDataURL</code>
| {{yes|1.8}}<ref group="g">https://developer.mozilla.org/en/HTML/Element/canvas</ref>
| {{yes}}<ref group="w">{{citation |url=http://developer.apple.com/safari/library/documentation/appleapplications/conceptual/SafariJSProgTopics/Tasks/Canvas.html |title=WebKit DOM Programming Topics: Using the Canvas}}</ref>
| {{yes|2.1}}<ref group="注">Presto 2.0部分支持此属性。</ref>
|}

==支持的上下文==
{| style="text-align: center; width: 95%" class="wikitable"
|-
! |
! style="width: 18%;" | [[Trident_(排版引擎)|Trident]]
! style="width: 18%;" | [[Gecko_(layout_engine)|Gecko]]
! style="width: 18%;" | [[WebKit|WebKit]]
! style="width: 18%;" | [[Presto|Presto]]
|-
! style="text-align: left;" | <code>2d</code>
| {{partial|5.0}}
| {{partial|1.9.1}}
| {{partial}}
| {{partial|2.6}}
|-
! style="text-align: left;" | [[WebGL|WebGL]]
| {{yes|7.0}}<ref group="t">{{cite web |url=http://blogs.msdn.com/b/ie/archive/2013/06/26/introducing-ie11-the-best-way-to-experience-the-web-on-modern-touch-devices.aspx |title=Introducing IE11: The Best Way to Experience the Web on Modern Touch Devices |publisher=Microsoft |accessdate=8 November 2013}}</ref>
| {{depends}}<ref group="g">{{citation |url=https://developer.mozilla.org/en/WebGL |title=WebGL - MDC |publisher=Mozilla}}</ref>
| {{depends}}<ref group="w">{{citation |url=http://webkit.org/blog/603/webgl-now-available-in-webkit-nightlies/ |title=WebGL Now Available in WebKit Nightlies |publisher=Surfin' Safari |first=Chris |last=Marrin |date=2009-10-19}}</ref>
| 2.9.220<ref group="p">{{citation |url=http://my.opera.com/desktopteam/blog/2011/10/13/introducing-opera-12-alpha |title=Opera Desktop Team Blog}}</ref>
|}

==画布2D渲染上下文==

{| style="text-align: center; width: 95%" class="wikitable"
|-
! |
! style="width: 18%;" | [[Trident_(排版引擎)|Trident]]<ref group="t">{{citation |url=http://ie.microsoft.com/testdrive/info/ReleaseNotes/Default.html#WhatsNew |title=Internet Explorer Platform Preview Release Notes |deadurl=yes |archiveurl=https://web.archive.org/web/20100419010701/http://ie.microsoft.com/testdrive/info/ReleaseNotes/Default.html#WhatsNew |archivedate=2010年4月19日 |df= }}</ref>
! style="width: 18%;" | [[Gecko_(layout_engine)|Gecko]]<ref group="g">{{citation |url=https://developer.mozilla.org/en/Canvas_tutorial |title=Canvas tutorial - MDC}}</ref>
! style="width: 18%;" | [[WebKit|WebKit]]<ref group="w">{{citation |url=http://developer.apple.com/safari/library/documentation/appleapplications/Reference/WebKitDOMRef/CanvasRenderingContext2D_idl/Classes/CanvasRenderingContext2D/index.html#//apple_ref/js/cl/CanvasRenderingContext2D |title=WebKit DOM reference - CanvasRenderingContext2D}}</ref>
! style="width: 18%;" | [[Presto|Presto]]<ref group="p">{{citation |url=http://www.opera.com/docs/specs/opera9/canvas/ |title=Opera 9 canvas support}}</ref><ref group="p">{{citation |url=http://www.opera.com/docs/specs/opera95/canvas/ |title=Opera 9.5 canvas support}}</ref>
|-
! colspan="5" | 画布状态
|-
! style="text-align: left;" | <code>save</code>
| rowspan="2" {{yes|5.0}}
| rowspan="2" {{yes|1.8}}
| rowspan="2" {{yes}}
| rowspan="2" {{yes|2.0}}
|-
! style="text-align: left;" | <code>restore</code>
|-
! colspan="5" | 转换
|-
! style="text-align: left;" | <code>scale</code>
| rowspan="5" {{yes|5.0}}
| rowspan="5" {{yes|1.8}}
| rowspan="5" {{yes}}
| rowspan="3" {{yes|2.0}}
|-
! style="text-align: left;" | <code>rotate</code>
|-
! style="text-align: left;" | <code>translate</code>
|-
! style="text-align: left;" | <code>transform</code>
| {{yes|2.6}}<ref group="注" name="presto-dropped-and-recovered">Opera 9.5（Presto 2.1）支持此功能，但Presto 2.1.1至2.5的支持表格表明该属性不被支持。</ref><ref group="p">{{citation |url=http://www.opera.com/docs/specs/presto211/canvas/ |title=Presto 2.1.1 canvas support table}}</ref><ref group="p">{{citation |url=http://www.opera.com/docs/specs/presto25/canvas/ |title=Presto 2.5 canvas support table}}</ref><ref group="p">{{citation |url=http://www.opera.com/docs/specs/presto26/canvas/ |title=Presto 2.6 canvas support table|ref=note}}</ref>
|-
! style="text-align: left;" | <code>setTransform</code>
| {{yes|2.6}}<ref group="注" name="presto-dropped-and-recovered" />
|-
! colspan="5" | 合成
|-
! style="text-align: left;" | <code>globalAlpha</code>
| rowspan="2" {{yes|5.0}}
| rowspan="2" {{yes|1.8}}
| rowspan="2" {{yes}}
| rowspan="2" {{yes|2.0}}
|-
! style="text-align: left;" | <code>globalCompositeOperation</code>
|-
! colspan="5" | 颜色与样式
|-
! style="text-align: left;" | <code>strokeStyle</code>
| rowspan="5" {{yes|5.0}}
| rowspan="5" {{yes|1.8}}
| rowspan="5" {{yes}}
| rowspan="5" {{yes|2.0}}
|-
! style="text-align: left;" | <code>fillStyle</code>
|-
! style="text-align: left;" | <code>createLinearGradient</code>
|-
! style="text-align: left;" | <code>createRadialGradient</code>
|-
! style="text-align: left;" | <code>createPattern</code>
|-
! colspan="5" | 线条样式
|-
! style="text-align: left;" | <code>lineWidth</code>
| rowspan="4" {{yes|5.0}}
| rowspan="4" {{yes|1.8}}
| rowspan="4" {{yes}}
| rowspan="4" {{yes|2.0}}
|-
! style="text-align: left;" | <code>lineCap</code>
|-
! style="text-align: left;" | <code>lineJoin</code>
|-
! style="text-align: left;" | <code>miterLimit</code>
|-
! colspan="5" | 阴影
|-
! style="text-align: left;" | <code>shadowOffsetX</code>
| rowspan="4" {{yes|5.0}}
| rowspan="4" {{yes|1.9.1}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=310682 |title=Bug 310682 - Implement shadows for <html:canvas> |publisher=Mozilla}}</ref>
| rowspan="4" {{yes}}
| rowspan="4" {{yes|2.4}}<ref group="注" name="presto-shadow">Presto 2.4之前仅部分支持此属性。</ref>
<!-- WARNING: Although Presto 2.4 support tables put "Yes" in this property, it is in Yellow. Only in the 2.5 support tables it appears in green. This also applies to the remaining shadow properties.-->
|-
! style="text-align: left;" | <code>shadowOffsetY</code>
|-
! style="text-align: left;" | <code>shadowBlur</code>
|-
! style="text-align: left;" | <code>shadowColor</code>
|-
! colspan="5" | 简单形状
|-
! style="text-align: left;" | <code>clearRect</code>
| rowspan="3" {{yes|5.0}}
| rowspan="3" {{yes|1.8}}
| rowspan="3" {{yes}}
| rowspan="3" {{yes|2.0}}
|-
! style="text-align: left;" | <code>fillRect</code>
|-
! style="text-align: left;" | <code>strokeRect</code>
|-
! colspan="5" | 复杂形状
|-
! style="text-align: left;" | <code>beginPath</code>
| rowspan="13" {{yes|5.0}}
| rowspan="4" {{yes|1.8}}
| rowspan="13" {{yes}}
| rowspan="13" {{yes|2.0}}
|-
! style="text-align: left;" | <code>closePath</code>
|-
! style="text-align: left;" | <code>moveTo</code>
|-
! style="text-align: left;" | <code>lineTo</code>
|-
! style="text-align: left;" | <code>quadraticCurveTo</code>
| {{yes|1.8.1}}<ref group="注">在Gecko 1.8中显示不正确。</ref>
|-
! style="text-align: left;" | <code>bezierCurveTo</code>
| {{yes|1.8}}
|-
! style="text-align: left;" | <code>arcTo</code>
| {{yes|1.8.1}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=333613 |title=Bug 333613 – update canvas on branch |publisher=Mozilla}}</ref>
|-
! style="text-align: left;" | <code>rect</code>
| rowspan="6" {{yes|1.8}}
|-
! style="text-align: left;" | <code>arc</code>
|-
! style="text-align: left;" | <code>fill</code>
|-
! style="text-align: left;" | <code>stroke</code>
|-
! style="text-align: left;" | <code>clip</code>
|-
! style="text-align: left;" | <code>isPointInPath</code>
|-
! colspan="5" | 集中管理
|-
! style="text-align: left;" | <code>drawFocusRing</code>
| {{no}}
| {{yes|28.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=540456 |title=Bug 540456 - Support HTML5 canvas drawFocusRing() |publisher=Mozilla}}</ref>
| {{no}}
| {{no}}
|-
! colspan="5" | 文本
|-
! style="text-align: left;" | <code>font</code>
| rowspan="6" {{yes|5.0}}
| rowspan="6" {{yes|1.9.1}}{{#tag:ref|Gecko在1.9中以不同的名字加入了实验性支持。<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=436904 |title=Bug 436904 - implementing Canvas text spec |publisher=Mozilla}}</ref>|group=注}}
| rowspan="6" {{yes}}
| {{no}}
|-
! style="text-align: left;" | <code>textAlign</code>
| rowspan="5" {{yes|2.6}}
|-
! style="text-align: left;" | <code>textBaseline</code>
|-
! style="text-align: left;" | <code>fillText</code>
|-
! style="text-align: left;" | <code>strokeText</code>
|-
! style="text-align: left;" | <code>measureText</code>
|-
! colspan="5" | 图像
|-
! style="text-align: left;" | <code>drawImage</code>
| rowspan="4" {{yes|5.0}}
| {{yes|1.8}}
| rowspan="4" {{yes}}
| {{yes|2.0}}
|-
! style="text-align: left;" | <code>createImageData</code>
| {{yes|1.9.1}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=433004 |title=Bug 433004 - Support canvas.getContext("2d").createImageData() |publisher=Mozilla}}</ref><ref group="g" name="gecko-pixel-canvas">{{citation |url=https://developer.mozilla.org/en/html/canvas/pixel_manipulation_with_canvas |title=Pixel manipulation with canvas - MDC}}</ref>
| {{yes|2.7}}<ref group="p">{{citation |url=http://www.opera.com/docs/specs/presto27/#changes |title=Web specifications support in Opera Presto 2.7 - Core Milestone additions since Opera Presto 2.6}}</ref>
|-
! style="text-align: left;" | <code>getImageData</code>
| {{yes|1.9}}<ref group="g" name="gecko-pixel-canvas" />
| rowspan="2" {{yes|2.6}}<ref group="注" name="presto-dropped-and-recovered" />
|-
! style="text-align: left;" | <code>putImageData</code>
| {{yes|2.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=498826 |title=Bug 498826 - canvas putImageData doesn't implement optional arguments |publisher=Mozilla}}</ref><ref group="g" name="gecko-pixel-canvas" />
|}

==注释==
{{Reflist|group=注}}

== 参考文献 ==
=== [[Trident|Trident]]参考 ===
{{Reflist | 30em |group = "t" }}

=== [[Gecko|Gecko]]参考 ===
{{Reflist | 30em |group = "g" }}

=== [[Webkit|Webkit]]参考 ===
{{Reflist | 30em |group = "w" }}

=== [[Presto|Presto]]参考 ===
{{Reflist | 30em |group = "p" }}

=== 其他参考 ===
{{Reflist | 30em }}

== 外部链接 ==
* {{cite web |url = http://www.w3.org/TR/2dcontext/ |title = HTML Canvas 2D Context |publisher = [[World_Wide_Web_Consortium|W3C]] |date = 2014-08-21 |accessdate = 2015-01-09 }}

{{-}}
{{Layout engines}}

[[Category:HTML5|Category:HTML5]]
[[Category:排版引擎比较|Category:排版引擎比较]]