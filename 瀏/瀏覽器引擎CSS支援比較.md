{{OftenUpdate}}
{{NoteTA|G1=IT}}
以下的表格顯示一些[[排版引擎|瀏覽器引擎]]對於[[CSS|CSS]]的兼容性與支援的比較。想獲得更多訊息，請參照各產品的項目。此項目不見得包含所有的功能也不見得有最新消息。除非以附註指出特例，這裡以未加裝任何套件或是其他程式的穩定版本進行比較。

<div class="toclimit-2">__TOC__</div>

<!-- 表格圖解 -->
{{瀏覽器引擎命名}}
{{功能成熟度表格圖例}}

== CSS版本支援 ==
想了解各版本的CSS差異，請參考項目[[CSS|CSS]]。<!-- 可能會比此頁面任何部份還新 --> 本表格不以CSS2.0為準，因為存在取代它的CSS2.1。CSS2.1修正了部份CSS2.0的錯誤，刪除了不被CSS社區接受的功能。大部分被刪除的功能將會出現在CSS3。

{| style="width: 95%;" class="wikitable"
|-
! |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|-
! CSS1
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|1.0}}
| {{yes|1.0}}
|-
! CSS2.1
| {{partial|大部分}}
| {{partial|大部分}}
| {{partial|大部分}}
| {{partial|大部分}}
| {{partial|大部分}}
| {{partial|大部分}}
|-
! CSS3
| {{partial|些許}}
| {{partial}}
| {{partial}}
| {{partial|些許}}
| {{partial}}
| {{partial|些許}}
|}

== 語法與規則 ==
{| style="width: 95%;" class="wikitable"
|-
! colspan="3" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|-
! rowspan="6" | CSS2
! <code>!important</code>
| 重要程度增加
| {{yes|[[#trident-important-bug|7.0]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|1.0}}
| {{yes}}
|-
! <code>/*Comment*/</code>
| 註解
| {{yes|3.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|1.0}}
| {{yes}}
|-
! <code>@import</code>
| 匯入樣式
| {{yes|[[#trident-import-bug|8.0]]}}
| {{yes|1.0}}
| {{yes}}
| {{yes}}
| {{yes|[[#presto_at-import|1.0]]}}
| {{yes|2.1}}
|-
! <code>@charset</code>
| 字元編碼
| {{yes|5.5}}
| {{yes|1.0}}
| {{yes|0}}
| {{yes|4.2.3}}
| {{yes|1.0}}
| {{yes}}
|-
! <code>@media</code>
| 媒體特定
| {{yes|5.5}}
| {{yes|1.0}}
| {{yes}}
| {{yes}}
| {{yes|1.0}}
| {{yes|5.1}}
|-
! <code>@page</code>
| 換頁媒體
| {{yes|8.0}}
| {{no}}<ref group="g" name="moz-page">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=115199 |title=Bug 115199 - CSS2中的「@page」無實作 |publisher=Mozilla}}</ref>
| {{no}}<ref group="w" name="webkit-page">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=15548 |title=Bug 15548 - 支援CSS3《CSS3換頁媒體模組》(@page) |publisher=Webkit}}</ref>
| {{no}}
| {{yes|1.0}}
| {{yes|6.0}}
|-
! rowspan="24" | CSS3
! <code>@namespace</code>
| 命名空間宣告
| {{yes|9.0}}<ref group="t" name="ie9-preview">{{citation |url=http://msdn.microsoft.com/en-us/ie/ff468705.aspx |title=給開發者的Internet Explorer 9 Beta導覽 |publisher=Microsoft}}</ref>
| {{yes|1.0}}
| {{yes}}
| {{yes}}
| {{yes|1.0}}
| {{yes|5.0}}
|-
! <code>@document</code>
| Restriction by URLs
| {{no}}
| {{yes|6.0}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>@keyframes</code>
| 动画关键帧
| {{yes|10.0}}<ref group="t">{{citation |url=http://msdn.microsoft.com/en-US/library/ie/hh772747.aspx |title=@keyframes rule (Internet Explorer) |publisher=Microsoft}}</ref>
| {{yes|16.0}}
| {{table-experimental}}
| {{no}}
| {{yes|2.12}}
| {{no}}
|-
! <code>@font-face</code>
| 定義字型
| {{yes|[[#trident_at-font-face|4.0]]}}
| {{yes|1.9.1}}
| {{yes|525}}
| {{yes|4.3}}
| {{yes|2.2}}
| {{yes|6.0}}
|-
! <code>@supports</code>
| 有条件的规则
| {{no}}
| {{depends| 17.0}}
| {{nightly }}
| {{no}}
| {{yes|2.12}}
| {{no}}
|-
! <code>@phonetic-alphabet</code>
| 發音
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>@region</code>
| Region flow segment
| {{no}}
| {{no}}
| {{nightly}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>@counter-style</code>
| 自定义计数器样式
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>@top-left-corner</code>
| rowspan="16" | Margin boxes <ref group="spec">{{citation |url=http://dev.w3.org/csswg/css3-page/#margin-boxes |title=CSS Paged Media Module Level 3 - Margin Boxes |publisher=W3C}}</ref>
| rowspan="16" {{no}}
| rowspan="16" {{no}}
| rowspan="16" {{no}} <ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=85062 |title= Bug 85062 - Support CSS 3 Paged Media Margin Boxes  |publisher=WebKit}}</ref>
| rowspan="16" {{no}}
| rowspan="16" {{no}}
| rowspan="16" {{no}}
|-
! <code>@top-left</code>
|-
! <code>@top-center</code>
|-
! <code>@top-right</code>
|-
! <code>@top-right-corner</code>
|-
! <code>@bottom-left-corner</code>
|-
! <code>@bottom-left</code>
|-
! <code>@bottom-center</code>
|-
! <code>@bottom-right</code>
|-
! <code>@bottom-right-corner</code>
|-
! <code>@left-top</code>
|-
! <code>@left-middle</code>
|-
! <code>@left-bottom</code>
|-
! <code>@right-top</code>
|-
! <code>@right-middle</code>
|-
! <code>@right-bottom</code>
|-
! colspan="3" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|}

=== Trident語法與規則附註 ===
# <tt id="trident-important-bug">!important</tt> — 7.0之前，<code>!important</code>並不會蓋掉在同一個宣告區的後面的規則。
# <tt id="trident-import-bug">@import</tt> —  8.0之前，不支援媒體形態。使用<code>@import <URL> <MEDIA></code>，則IE會要求此URL：「<code><URL> <MEDIA></code>」，包括<code>url()</code>及URL裡的引號。無法匯入超過35的樣式表。


=== Presto語法與規則附註 ===
# <tt id="presto_at-import">@import</tt> — 儘管Gecko、WebKit及iCab會立即下載所有樣式表，Opera只下載媒體名為「handheld」、「print」、「projection」、「screen media」、「speech」（當聲音功能在啟動狀態）、「tv」（電視裝置）。文字瀏覽器模擬模式僅為一個使用者樣式表而不用媒體形態「tty」。這是符合不支援CSS的老舊文字瀏覽器的。

== 選擇器 ==
{| style="width: 95%;" class="wikitable"
|-
! colspan="3" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|-
! colspan="9" | 元素選擇器<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-selectors/ |title=CSS選擇器等級3 |publisher=W3C}}</ref>
|-
! rowspan="4" | CSS2
! <code><nowiki>*</nowiki></code>
| 全域
| {{yes|[[#trident_universal|7.0]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| rowspan="5" {{yes|1.0}}
| {{yes}}
|-
! <code>E</code>
| 元素
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>E.class</code>
| 類別
| {{yes|[[#trident_class|7.0]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>E#id</code>
| ID
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! CSS3
! <code><nowiki>ns|E</nowiki></code>
| 命名空間
| {{yes|9.0}}
| {{yes|1.0}}
| {{yes}}
| {{yes}}
| {{yes}}
|-
! colspan="9" | 關係選擇器
|-
! rowspan="3" | CSS2
! <code>E F</code>
| 後裔
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| rowspan="3" {{yes|1.0}}
| {{yes}}
|-
! <code>E > F</code>
| 子元素
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>E + F</code>
| 直接相連
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! CSS3
! <code>E ~ F</code>
| 間接相連
| {{yes|7.0}}
| {{yes|1.7}}
| {{yes|412}}
| {{yes|3.3.2}}
| {{yes|2.0}}
| {{yes}}
|-
! rowspan="2" | CSS4
! <code>E /for/ F</code>
| Reference combinators
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>E! > F</code>
| Subject
| {{no}}
| {{no}}<ref group="g">{{Citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=418039 |title=Bug 418039 - CSS parent (has-child) and ancestor (has-descendant) selectors (:subject) |publisher=Mozilla}}</ref>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! colspan="9" | 屬性選擇器
|-
! rowspan="4" | CSS2
! <code>E[attr]</code>
| 存在
| {{yes|[[#trident_attr|7.0]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| rowspan="4" {{yes|1.0}}
| {{yes}}
|-
! <code>E[attr="value"]</code>
| 相等
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes}}
| {{yes}}
| {{yes}}
|-
! <code>E[attr~="value"]</code>
| 含有（以空白相隔）
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes}}
| {{yes}}
| {{yes}}
|-
! <code><nowiki>E[attr|="value"]</nowiki></code>
| 含有（以連字號相隔）
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes}}
| {{yes}}
| {{yes}}
|-
! rowspan="4" | CSS3
! <code>E[attr^="value"]</code>
| 以……開頭
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes}}
| {{yes|3.4}}
| {{yes|1.0}}
| {{yes}}
|-
! <code>E[attr$="value"]</code>
| 以……結尾
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes}}
| {{yes|3.4}}
| rowspan="3" {{yes|2.0}}
| {{yes}}
|-
! <code>E[attr*="value"]</code>
| 含有子字串
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes}}
| {{yes|3.4}}
| {{yes}}
|-
! <code><nowiki>E[ns|attr]</nowiki></code>
| 命名空間
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes}}
| {{yes|3.4}}
| {{no}}
|-
! colspan="9" | 擬類別
|-
! rowspan="10" | CSS2
! <code>E:link</code>
| 未開過連結
| {{yes|3.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| rowspan="10" {{yes|1.0}}
| {{yes|6.0}}
|-
! <code>E:visited</code>
| 開過連結
| {{yes|3.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>E:active</code>
| 啟動中
| {{yes|[[#trident_active|8.0]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>E:hover</code>
| 滑鼠置上
| {{yes|[[#trident_hover|7.0]]}}
| {{yes|1.0}}
| {{yes|419.3}}
| {{yes}}
| {{yes}}
|-
! <code>E:focus</code>
| 集中點
| {{yes|8.0}}
| {{yes|1.0}}
| {{yes}}
| {{yes}}
| {{yes}}
|-
! <code>E:first-child</code>
| 第一子元素
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>E:lang()</code>
| 語言
| {{yes|8.0}}
| {{yes|1.2}}
| {{yes|[[#webcore_lang|525]]}}
| {{yes|3.4}}
| {{yes}}
|-
! <code>@page:first</code>
| 第一頁
| rowspan="3" {{yes|8.0}}
| rowspan="3" {{no}}<ref group="g" name="moz-page"/>
| rowspan="3" {{nightly}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=38731 |title= Bug 38731 - 讓CSS Parser無錯誤地處理頁面專用擬類別 |publisher=WebKit}}</ref>
| rowspan="3" {{no}}
| rowspan="3" {{yes}}
|-
! <code>@page:left</code>
| 左頁
|-
! <code>@page:right</code>
| 右頁
|-
! rowspan="26" | CSS3
! <code>E:root</code>
| 根
| rowspan="17" {{yes|9.0}}
| rowspan="2" {{yes|1.0}}
| rowspan="2" {{yes|85}}
| rowspan="16" {{yes|3.4}}
| rowspan="12" {{yes|2.1}}
| rowspan="12" {{yes}}
|-
! <code>E:not()</code>
| 逆
|-
! <code>E:empty</code>
| 空元素
| {{yes|1.8}}
| {{yes|412}}
|-
! <code>E:first-of-type</code>
| 第一個名為……的子元素
| {{yes|1.9.1}}
| rowspan="13" {{yes|525}}
|-
! <code>E:last-child</code>
| 最後子元素
| {{yes|1.0}}
|-
! <code>E:last-of-type</code>
| 最後一個名為……的子元素
| {{yes|1.9.1}}
|-
! <code>E:only-child</code>
| 唯一子元素
| {{yes|1.8}}
|-
! <code>E:only-of-type</code>
| 唯一個名為……的子元素
| {{yes|1.9.1}}
|-
! <code>E:nth-child</code>
| 第N個子元素
| {{yes|1.9.1}}
|-
! <code>E:nth-last-child</code>
| 第N個子元素（倒過來數）
| {{yes|1.9.1}}
|-
! <code>E:nth-of-type</code>
| 第N個名為……的子元素
| {{yes|1.9.1}}
|-
! <code>E:nth-last-of-type</code>
| 第N個名為……的子元素（倒過來數）
| {{yes|1.9.1}}
|-
! <code>E:target</code>
| 目標
| {{yes|1.3}}
| {{yes|[[#presto_target|2.5]]}}
| rowspan="14" {{no}}
|-
! <code>E:enabled</code>
| 啟動狀態
| {{yes|1.8}}
| rowspan="3" {{yes|2.0}}
|-
! <code>E:disabled</code>
| 未啟動狀態
| {{yes|1.8}}
|-
! <code>E:checked</code>
| 被選取狀態
| {{yes|1.0}}
|-
! <code>E:indeterminate</code>
| 中間狀態
| {{yes|1.9.2}}
| {{yes|522}}
| {{no}}
| {{no}}
|-
! <code>E:default</code>
| 預設
| {{no}}
| {{yes|1.9}}
| {{yes}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=27458 |title=Bug 27458 - Support :default HTML5 CSS selector |publisher=Webkit}}</ref>
| {{yes|4.3}}
| rowspan="7" {{yes|2.0}}
|-
! <code>E:valid</code>
| 合格
| {{yes|10.0}}<ref group=t>{{cite web|title=:valid pseudo-class (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/hh772727|publisher=Microsoft|accessdate=17 November 2012}}</ref>
| rowspan="4" {{yes|1.8}}
| rowspan="2" {{yes}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=27357 |title=Bug 27357 - Support :valid/:invalid CSS selectors |publisher=Webkit}}</ref>
| rowspan="6" {{no}}
|-
! <code>E:invalid</code>
| 不合格
| {{yes|10.0}}<ref group=t>{{cite web|title=:invalid pseudo-class (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/hh772367|publisher=Microsoft|accessdate=17 November 2012}}</ref>
|-
! <code>E:in-range</code>
| 範圍內
| {{no}}
| rowspan="2" {{yes}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=29071 |title=Bug 29071 - Support for :in-range and :out-of-range CSS selectors |publisher=Webkit}}</ref>
|-
! <code>E:out-of-range</code>
| 範圍外
| {{no}}
|-
! <code>E:required</code>
| 必需
| {{yes|10.0}}<ref group=t>{{cite web|title=:required pseudo-class (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/hh772720|publisher=Microsoft|accessdate=17 November 2012}}</ref>
| rowspan="2" {{yes|2.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=506554 |title=Bug 506554 - Implement the CSS3 pseudo-classes :required and :optional |publisher=Mozilla}}</ref>
| rowspan="2" {{yes}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=25551 |title=Bug 25551 - Support for HTML5 Forms "required" attribute |publisher=Webkit}}</ref>
|-
! <code>E:optional</code>
| 非必需
| {{yes|10.0}}<ref group=t>{{cite web|title=:optional pseudo-class (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/hh772709|publisher=Microsoft|accessdate=17 November 2012}}</ref>
|-
! <code>E:read-only</code>
| 唯讀
| {{no}}
| rowspan="2" {{table-experimental|[[#gecko_-moz-|Experimental]]}}<ref group="g">{{Citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=312971 |title=Bug 312971 - Support :read-only and :read-write pseudoclasses |publisher=Mozilla}}</ref>
| rowspan="2" {{no}}
| rowspan="2" {{incorrect|[[#general_rw|Incorrect]]}}
| rowspan="2" {{incorrect|[[#general_rw|Incorrect]]}}
|-
! <code>E:read-write</code>
| 讀寫
| {{no}}
|-
! rowspan="19" | CSS4
! <code>E:not(s1, s2)</code>
| 否定
| rowspan="19" {{no}}
|{{no}}
| rowspan="19" {{no}}
| rowspan="19" {{no}}
| rowspan="19" {{no}}
| rowspan="19" {{no}}
|-
! <code>E:matches(s1, s2)</code>
| 匹配其中任意一个
| {{no}} <ref group="g">{{Citation |url= https://bugzilla.mozilla.org/show_bug.cgi?id=561154 |title=Bug 561154 - fix specificity of :-moz-any() |publisher=Mozilla}}</ref>
|-
! <code>E[foo="bar" i]</code>
| 大小写敏感性
| {{no}}
|-
! <code>E:dir(ltr)</code>
| 方向性
| {{table-experimental|[[#gecko_-moz-|17]]}}<ref group="g">{{Citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=562169 |title=Bug 562169 - Implement the :dir(rtl/ltr) selector to select on HTML directionality |publisher=Mozilla}}</ref>
|-
! <code>E:lang(zh, *-hant)</code>
| (多种) 语言
| rowspan="4" {{no}}
|-
! <code>E:any-link</code>
| 超链接
|-
! <code>E:local-link</code>
| 本地链接
|-
! <code>E:local-link(0)</code>
| 本地链接
|-
! <code>E:scope</code>
| Contextual reference
|  {{table-experimental|[[#gecko_-moz-|20]]}}<ref group="g">{{Citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=648722 |title=Bug 648722 - Add support for :scope as :-moz-scope |publisher=Mozilla}}</ref>
|-
! <code>E:current</code>
| Time-dimensional : current
| rowspan="10" {{no}}
|-
! <code>E:current(s)</code>
| Time-dimensional : current
|-
! <code>E:past</code>
| Time-dimensional : past
|-
! <code>E:future</code>
| Time-dimensional : future
|-
! <code>E:indeterminate</code>
| Indeterminate-value 
|-
! <code>E:nth-match(n of selector)</code>
| N<sup>th</sup> child of
|-
! <code>E:nth-last-match(n of selector)</code>
| N<sup>th</sup> last child of
|-
! <code>E:column(selector)</code>
| 分栏
|-
! <code>E:nth-column(n)</code>
| 第 n 个分栏
|-
! <code>E:nth-last-column(n)</code>
| 倒数第 n 个分栏
|-
! colspan="9" | 擬元素
|-
! rowspan="4" | CSS2
! <code>E:first-letter</code>
| 第一字節
| rowspan="2" {{yes|9.0}}
| rowspan="2" {{yes|1.0}}
| {{yes|85}}
| rowspan="4" {{yes}}
| rowspan="4" {{yes|1.0}}
| {{yes|5.0}}
|-
! <code>E:first-line</code>
| 第一行
| {{partial|[[#webcore_first-line|部份]]}}
| {{no}}<ref group="r" name="prince">{{citation |url=http://www.princexml.com/doc/7.0/css21/ |title=Prince: 未支援的CSS 2.1機能 |publisher=YesLogic}}</ref>
|-
! <code>E:before</code>
| 之前
| rowspan="2" {{yes|8.0}}
| rowspan="2" {{yes|[[#gecko_gencon|1.9.1]]}}
| rowspan="2" {{partial|[[#webcore_pseudo-elements|部份]]}}
| rowspan="2" {{yes}}
|-
! <code>E:after</code>
| 之後
|-
! rowspan="7" | CSS3
! <code>E::before</code>
| 雙冒號語法
| rowspan="5" {{yes|9.0}}
| rowspan="2" {{yes|[[#gecko_gencon|1.9.1]]}}
| rowspan="2" {{partial|[[#webcore_pseudo-elements|部份]]}}
| rowspan="5" {{yes|3.4}}
| rowspan="4" {{yes|1.0}}
| rowspan="3" {{yes}}
|-
! <code>E::after</code>
| 雙冒號語法
|-
! <code>E::first-letter</code>
| 雙冒號語法
| rowspan="2" {{yes|1.5}}
| {{yes|85}}
|-
! <code>E::first-line</code>
| 雙冒號語法
| {{partial|[[#webcore_first-line|部份]]}}
| {{no}}<ref group="r" name="prince"/>
|-
! <code>E::selection</code>
| 選取
| {{table-experimental|[[#gecko_-moz-|實驗性質]]}}
| {{yes|412}}
| {{yes|2.1}}
| {{no}}
|-
! <code>E::marker</code> <ref>http://www.w3.org/TR/css3-lists/</ref>
| 列表标记
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>E::value</code>
| 数据本身選取
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! colspan="3" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|}

=== 一般選擇器附註 ===
# <tt id="general_rw">:read-only</tt>與<tt>:read-write</tt> — Presto與KHTML皆不正確地處理有<code>contenteditable</code>屬性的元素。

=== Trident選擇器附註 ===
# <tt id="trident_active">:active</tt> — 8.0之前，Trident僅支援超連結元素。
# <tt id="trident_hover">:hover</tt> — 7.0之前，Trident僅支援超連結元素。
# <tt id="trident_class">.one.two</tt> — 7.0之前，被當成<code>.two</code>類別選擇器處理。
# <tt id="trident_universal">*</tt> — 7.0之前這代表「一個或是沒有元素」。
# <tt id="trident_attr">[attr]</tt> — 當屬性是<code>colspan</code>的時候，選出所有表格內的<code>td</code>元素及<code>th</code>元素（有沒有之的有<code>colspan</code>屬性都一樣）。<ref group="t">{{citation |url=https://connect.microsoft.com/IE/feedback/ViewFeedback.aspx?FeedbackID=446817 |title=（選有「colspan」屬性的TD、TH）屬性選擇器會選出所有TD、TH |last=Hopkins |first=James}}</ref>這可能不是一個bug，因規格存在模稜兩可的解釋。<ref group="t">{{citation |url=http://www.webdevout.net/tidings/2009/03/23/ie-8-css-21-support-results/#comment-4168 |title=《IE 8 CSS 2.1支援測試結果》之評論 |last=Hammond |first=David}}</ref>
# <tt id="trident_first-letter">:first-letter</tt>、<tt>:first-line</tt> — 在6.0，<code>:first-letter</code>與其他rules一起使用的時候可能有問題。<ref group="t">{{citation |url=http://haslayout.net/css/-first-letter-Ignore-Bug |title=臭蟲 - 忽略「:first-letter」 |publisher=hasLayout.net |deadurl=yes |archiveurl=https://web.archive.org/web/20100302152332/http://haslayout.net/css/-first-letter-Ignore-Bug |archivedate=2010-03-02 }}</ref>在8.0，在<code>:first-line</code>與<code>:first-letter</code>宣告內的有<code>!important</code>的rules會被省略。<ref group="t">{{citation |url=https://connect.microsoft.com/IE/feedback/details/478138/declaration-which-includes-important-keyword-is-ignored-when-used-within-a-first-letter-or-first-line-rule |title=有用!important的屬性質宣告在:first-letter或:first-line裡會被省略 |last=Hopkins |first=James}}</ref>

=== Gecko選擇器附註 ===
# <tt id="gecko_gencon">(:):before, (:):after</tt> — 在1.9.1之前，有些屬性不能使用（這是CSS2.0的過期解釋）。<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=237119 |title=Bug 237119 - 「display」屬性在生成內容上會被省略 |publisher=Mozilla}}</ref>

=== WebKit選擇器附註 ===
# <tt id="webcore_lang">:lang()</tt> — 只對寫上<code>lang</code>屬性的元素有效，屬性不繼承。
# <tt id="webcore_first-line">(:):first-line</tt> — <code>text-transform</code>不在此擬元素上作用。<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=3409 |title=Bug 3409 - CSS1: Safari 忽略在「first-line」CSS rules裡的「text-transform」屬性 |publisher=Webkit}}</ref>
# <code id="webcore_pseudo-elements">(:):before/after</code> — 有些樣式無法使用於<code>:before</code>與<code>:after</code>擬元素之上，如動畫與轉變。<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=23209 |title=Bug 23209 - [RFE] CSS生成內容不轉變 |publisher=Webkit}}</ref>

=== Presto選擇器附註 ===
# <tt id="presto_target">:target</tt> — 在2.5之前，樣式在以向前向後按鈕瀏覽的時候不作用。

== 屬性 ==
{| style="width: 95%;" class="wikitable"
|-
! colspan="2" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|-
! colspan="8" | {{Anchor|Box}}盒子模型(@@翻譯)<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-box/ |title=CSS 3 盒子模型(@@翻譯)模組 |publisher=W3C}}</ref>
|-
! rowspan="14" | CSS2
! <code>margin</code>
| {{incorrect|[[#trident_margin|4.0]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| rowspan="13" {{yes|1.0}}
| {{yes}}
|-
! <code>padding</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>width</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>height</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>float</code>
| {{yes|5.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>clear</code>
| {{yes|5.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>display</code>
| {{yes|[[#trident_display|8.0]]}}
| {{partial|[[#gecko_display|部份]]}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>min-width</code>
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes|416}}
| {{yes}}
| {{yes|5.0}}
|-
! <code>max-width</code>
| {{yes|7.0}}
| {{yes|1.0}}
| {{yes|416}}
| {{yes}}
| {{yes|5.0}}
|-
! <code>min-height</code>
| {{yes|7.0}}
| {{yes|1.7}}
| {{yes|416}}
| {{yes|3.3.2}}
| {{yes|5.0}}
|-
! <code>max-height</code>
| {{yes|7.0}}
| {{yes|1.7}}
| {{yes|416}}
| {{yes|3.3.2}}
| {{yes|5.0}}
|-
! <code>clip</code>
| {{yes|[[#trident_rect|8.0]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|5.0}}
|-
! <code>overflow</code>
| {{incorrect|[[#trident_overflow|不正確]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes|3.2}}
| {{yes|5.0}}
|-
! <code>visibility</code>
| {{incorrect|[[#trident_visibility|不正確]]}}
| {{yes|[[#gecko_visibility|1.8]]}}
| {{partial|[[#webcore_visibility|部份]]}}
| {{partial|[[#khtml_visibility|部份]]}}
| {{yes|[[#presto_visibility|2.5]]}}
| {{partial|[[#prince-visibility|部份]]}}
|-
! rowspan="2" | CSS3
! <code>overflow-x</code>
| rowspan="2" {{incorrect|[[#trident_overflow|不正確]]}}
| rowspan="2" {{yes|1.8}}
| rowspan="2" {{yes|525}}
| rowspan="2" {{yes|3.5.6}}
| rowspan="2" {{yes|2.1}}
| rowspan="2" {{yes|5.0}}
|-
! <code>overflow-y</code>
|-
! colspan="8" | {{Anchor|Border}}邊框<ref group="spec" name="spec-back-borders">{{citation |url=http://www.w3.org/TR/css3-background/ |title=CSS 3 背景與邊框模組 |publisher=W3C}}</ref>
|-
! rowspan="8" | CSS2
! <code>border</code>
| {{yes|4.0}}
| rowspan="8" {{yes|1.0}}
| rowspan="8" {{yes|85}}
| rowspan="8" {{yes}}
| rowspan="8" {{yes|1.0}}
| rowspan="8" {{yes|3.0}}
|-
! <code>border-color</code>
| {{yes|[[#trident_border-color|7.0]]}}
|-
! <code>border-style</code>
| {{yes|[[#trident_border-style|8.0]]}}
|-
! <code>border-width</code>
| {{yes|4.0}}
|-
! <code>border-top</code>
| rowspan="4" {{yes|5.5}}
|-
! <code>border-right</code>
|-
! <code>border-bottom</code>
|-
! <code>border-left</code>
|-
! rowspan="9" | CSS3
! <code>border-radius</code>
| {{nightly|9.0}}<ref group="t" name="ie9-preview" />
| {{table-experimental|[[#gecko_border-radius|實驗性質 (2.0)]]}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=451134 |title=Bug 451134 - 把「-moz-border-radius*」的屬性名改成css3-background的名字 |publisher=Mozilla}}</ref>
| {{yes|533}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=27578 |title=Bug 27578 - 拿掉border-radius屬性的前輟 |publisher=Webkit}}</ref>
| {{table-experimental|[[#khtml_-khtml-|實驗性質]]}}
| {{yes|2.5}}
| {{yes|6.0}}
|-
! <code>border-image</code>
| rowspan="6" {{no}}
| {{yes|15.0}}<ref group="g">{{Citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=378217 |title=Bug 378217 - implement css3 'border-image' property |publisher=Mozilla}}</ref>
| {{table-experimental}}
| rowspan="6" {{no}}
| {{yes|2.5}}
| rowspan="6" {{no}}
|-
! <code>border-image-source</code>
| rowspan="5" {{yes|15.0}}<ref group="g">{{Citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=497995 |title=Bug 497995 - Implement border-image revisions in latest css3-background |publisher=Mozilla}}</ref>
| rowspan="5" {{no}}
| rowspan="5" {{no}}
|-
! <code>border-image-slice</code>
|-
! <code>border-image-width</code>
|-
! <code>border-image-outside</code>
|-
! <code>border-image-repeat</code>
|-
! <code>box-shadow</code>
| {{nightly|[[#trident_box-shadow|9.0]]}}
| {{table-experimental|實驗性質 (2.0)}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=590039 |title=Bug 590039 - 修正模糊半徑的計算並把「-moz-box-shadow」改至「box-shadow」 |publisher=Mozilla}}</ref>
| {{table-experimental}}
| {{no}}
| {{yes|2.5}}
| {{no}}
|-
! <code>box-decoration-break</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{yes|2.7}}<ref group="p">{{Cite web|url=http://my.opera.com/ODIN/blog/first-browser-to-11-unless-chrome-gets-there-first |title=第一個到11的瀏覽器（除非Chrome先到） |first=David |last=Storey |date=2010-11-23 |accessdate=2010-11-23 |publisher=Opera |archiveurl=https://web.archive.org/web/20101208233126/http://my.opera.com/ODIN/blog/first-browser-to-11-unless-chrome-gets-there-first |archivedate=2010-12-08 |deadurl=yes }}</ref>
| {{no}}
|-
! colspan="2" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|-
! colspan="8" | {{Anchor|Linebox}}行排版<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-linebox/ |title=CSS 3 行模組 |publisher=W3C}}</ref>
|-
! rowspan="2" | CSS2
! <code>line-height</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| rowspan="2" {{yes|1.0}}
| {{yes|5.0}}
|-
! <code>vertical-align</code>
| {{yes|8.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|6.0}}
|-
! colspan="8" | {{Anchor|Positioning}}定位
|-
! rowspan="6" | CSS2
! <code>position</code>
| {{yes|[[#trident_position|7.0]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| rowspan="6" {{yes|1.0}}
| {{yes|5.0}}
|-
! <code>top</code>
| {{yes|8.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|6.0}}
|-
! <code>right</code>
| {{yes|8.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|6.0}}
|-
! <code>bottom</code>
| {{yes|8.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|6.0}}
|-
! <code>left</code>
| {{yes|8.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|6.0}}
|-
! <code>z-index</code>
| {{yes|[[#trident_z-index|8.0]]}}
| {{yes|[[#gecko_z-index|1.9]]}}
| {{yes|85}}
| {{yes}}
| {{yes|6.0}}
|-
! colspan="8" | {{Anchor|Content}}生成內容與取代內容(@@翻譯)<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-content/ |title=CSS 3 生成內容與取代內容模組 |publisher=W3C}}</ref>
|-
! rowspan="4" | CSS2
! <code>quotes</code>
| {{yes|8.0}}
| {{yes|[[#gecko_quotes|1.8]]}}
| {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=3234 |title=Bug 3234 - CSS2: 提高引用支援（q標籤） |publisher=Webkit}}</ref>
| {{yes|3.4}}
| {{yes|1.0}}
| {{no}}
|-
! <code>content</code>
| {{partial|[[#trident_content|部份]]}}
| {{yes|[[#gecko_content|1.9]]}}
| {{partial|[[#webkit_content|部份]]}}
| {{yes}}
| {{partial|[[#presto_content|部份]]}}
| {{partial|[[#prince-content|部份]]}}
|-
! <code>counter-increment</code>
| {{yes|8.0}}
| {{yes|1.8}}
| {{yes|525}}
| {{yes|3.4}}
| rowspan="2" {{yes|[[#presto_counter|1.0]]}}
| {{yes|5.0}}
|-
! <code>counter-reset</code>
| {{yes|8.0}}
| {{yes|1.8}}
| {{yes|525}}
| {{yes|3.4}}
| {{yes|5.0}}
|-
! colspan="8" | {{Anchor|Lists}}列<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-lists/ |title=CSS 3 列模組 |publisher=W3C}}</ref>
|-
! rowspan="4" | CSS2
! <code>list-style</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| rowspan="4" {{yes|1.0}}
| {{yes|6.0}}
|-
! <code>list-style-image</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|6.0}}
|-
! <code>list-style-position</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|6.0}}
|-
! <code>list-style-type</code>
| {{yes|[[#trident_list-style-type|8.0]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes|3.4}}
| {{partial|[[#prince-list-style|部份]]}}
|-
! colspan="8" | {{Anchor|Color}}色彩<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-color/ |title=CSS 3 色彩模組 |publisher=W3C}}</ref>
|-
! rowspan="1" | CSS2
! <code>color</code>
| {{yes|3.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|1.0}}
| {{yes|5.0}}
|-
! rowspan="1" | CSS3
! <code>opacity</code>
| {{nightly|[[#trident_opacity|9.0]]}}<ref group="t" name="ie9-preview" />
| {{yes|1.7}}
| {{yes|125}}
| {{yes|4.0}}
| {{yes|2.0}}
| {{yes|6.0}}
|-
! colspan="2" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|-
! colspan="8" | {{Anchor|Backgroud}}背景<ref group="spec" name="spec-back-borders"/>
|-
! rowspan="6" | CSS2
! <code>background</code>
| {{yes|4.0}}
| rowspan="6" {{yes|1.0}}
| rowspan="6" {{yes|85}}
| rowspan="6" {{yes}}
| rowspan="6" {{yes|1.0}}
| {{yes|6.0}}
|-
! <code>background-attachment</code>
| {{yes|[[#trident_background-attachment|7.0]]}}
| {{yes|5.0}}
|-
! <code>background-color</code>
| {{yes|4.0}}
| {{yes|3.1}}
|-
! <code>background-image</code>
| {{yes|[[#trident_background-image|8.0]]}}
| {{yes|6.0}}
|-
! <code>background-position</code>
| {{yes|[[#trident_background-position|8.0]]}}
| {{yes|3.1}}
|-
! <code>background-repeat</code>
| {{yes|4.0}}
| {{yes|3.1}}
|-
! rowspan="4" | CSS3
! <code>background (多重)</code>
| rowspan="4" {{nightly|9.0}}<ref name="ie9-preview" group="t" />
| {{yes|1.9.2}}
| {{yes|312}}
| {{yes|3.5}}
| rowspan="4" {{yes|2.5}}
| rowspan="4" {{no}}
|-
! <code>background-clip</code>
| rowspan="3" {{table-experimental|實驗性質 (2.0)}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=549809 |title=Bug 549809 - 將「background-origin」與「background-clip」屬性及取值更名至css3-background |publisher=Mozilla}}</ref>
| rowspan="3" {{table-experimental|[[#webcore_-webkit-|實驗性質]]}}
| rowspan="3" {{table-experimental|[[#khtml_-khtml-|實驗性質]]}}
|-
! <code>background-origin</code>
|-
! <code>background-size</code>
|-
! colspan="8" | {{Anchor|Fonts}}字型<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-fonts/ |title=CSS 3 字型模組 |publisher=W3C}}</ref>
|-
! rowspan="6" | CSS2
! <code>font</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{incorrect|[[#presto_font|不正確]]}}
| {{yes}}
|-
! <code>font-family</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| rowspan="4" {{yes|1.0}}
| {{yes}}
|-
! <code>font-size</code>
| {{yes|3.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|3.1}}
|-
! <code>font-style</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>font-variant</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|125}}
| {{yes}}
| {{yes}}
|-
! <code>font-weight</code>
| {{yes|[[#trident_font-weight|8.0]]}}
| {{partial|[[#gecko_font-weight|部份]]}}
| {{partial|[[#webcore_font-weight|部份]]}}
| {{yes}}
| {{Incorrect|[[#presto_font-weight|部份]]}}
| {{yes}}
|-
! rowspan="13" | CSS3
! <code>font-size-adjust</code>
| {{yes|10.0}}<ref group=t>{{cite web|title=font-size-adjust property (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/jj127323|publisher=Microsoft|accessdate=17 November 2012}}</ref>
| {{yes|[[#gecko_font-size-adjust|1.9]]}}
| {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=15257 |title=Bug 15257 - Support CSS 3 font-size-adjust |publisher=Webkit}}</ref>
| {{no}}
| {{no}}
| {{no}}
|-
! <code>font-stretch</code>
| {{yes|9.0}}<ref name="ie9-preview" group="t" />
| {{yes|9.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=3512 |title=Bug 3512 - (font-stretch) Implement font-stretch property |publisher=Mozilla}}</ref>
| {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=12530 |title=Bug 12530 - CSS3: Support the font-stretch property |publisher=Webkit}}</ref>
| {{no}}
| {{no}}
| {{yes|6.0}}
|-
! <code>font-feature-settings</code>
| {{yes|10.0}}<ref group=t>{{cite web|title=font-feature-settings property (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/hh869409|publisher=Microsoft|accessdate=17 November 2012}}</ref>
| {{yes|34.0}}
| {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=63796 |title=Bug 63796 - Master: Support CSS3 font feature properties |publisher=Webkit}}</ref>
| {{no}}
| {{no}}
| {{no}}
|-
! <code>font-kerning</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>font-language-override</code>
| {{no}}
| {{yes|34.0}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>font-synthesis</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|- 
! <code>font-variant-alternates </code>
| rowspan="6" {{no}}
| rowspan="6" {{no}}
| rowspan="6" {{no}}
| rowspan="6" {{no}}
| rowspan="6" {{no}}
| rowspan="6" {{no}}
|-
! <code>font-variant-caps </code>
|-
! <code>font-variant-east-asian </code>
|-
! <code>font-variant-ligatures</code>
|-
! <code>font-variant-numeric</code>
|-
! <code>font-variant-position </code>
|-
! <code>unicode-range</code>
| {{yes|9.0}}<ref group=t>{{cite web|title=@font-face rule (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/ms530757|publisher=Microsoft|accessdate=17 November 2012}}</ref>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! colspan="8" | {{Anchor|Text}}文字<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-text/ |title=CSS 3 文字模組 |publisher=W3C}}</ref>
|-
! rowspan="7" | CSS2
! <code>text-align</code>
| {{yes|[[#trident_text-align|4.0]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| rowspan="6" {{yes|1.0}}
| {{yes}}
|-
! <code>text-decoration</code>
| {{yes}}
| {{incorrect|[[#general_text-decoration|不正確]]}}
| {{incorrect|[[#general_text-decoration|不正確]]}}
| {{yes}}
| {{yes|3.1}}
|-
! <code>text-indent</code>
| {{yes|3.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes}}
|-
! <code>text-transform</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|6.0}}
|-
! <code>letter-spacing</code>
| {{yes|4.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|5.0}}
|-
! <code>word-spacing</code>
| {{yes|8.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|5.0}}
|-
! <code>white-space</code>
| {{yes|[[#trident_white-space|8.0]]}}
| {{yes|[[#gecko_white-space|1.9.1]]}}
| {{yes|[[#webcore_white-space|522]]}}
| {{yes}}
| {{yes|2.1}}
| {{yes|6.0}}
|-
! rowspan="9" | CSS3
! <code>text-overflow</code>
| {{partial|Partial}}
| {{yes|7.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=312156 |title=Bug 312156 - implement text-overflow: ellipsis from CSS3 text |publisher=Mozilla}}</ref>
| {{partial|Partial}}
| {{partial|3.5.6}}
| {{table-experimental|Experimental (Nightly)}}<ref group="p">{{citation|url=http://my.opera.com/desktopteam/blog/2010/08/09/new-10-70-snapshot-with-more-presto-updates |title=New 10.70 snapshot with more Presto updates |date=2010-08-09 |publisher=Opera |author=Haavard |archiveurl=https://web.archive.org/web/20100819082335/http://my.opera.com/desktopteam/blog/2010/08/09/new-10-70-snapshot-with-more-presto-updates |archivedate=2010-08-19 |deadurl=yes }}</ref>
| {{no}}
|-
! <code>word-break</code>
| {{partial|Partial}}
| {{yes|15.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=249159 |title=Bug 249159 - implement 'word-break' properties of CSS3 |publisher=Mozilla}}</ref>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>text-wrap</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>word-wrap</code>
| {{yes|5.0}}
| {{yes|1.9.1}}
| {{yes|85}}
| {{yes|4.3}}
| {{yes|2.5}}
| {{no}}
|-
! <code>text-align-last</code>
| {{partial}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{partial}}
|-
! <code>text-justify</code>
| {{yes|5.5}}
| {{no}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=276079 |title=Bug 276079 - 實作「text-justify」屬性（只弄「auto」、「inter-word」、「inter-ideograph」及「distribute」） |publisher=Mozilla}}</ref>
| {{no}}
| {{no}}
| {{no}}
| {{yes|6.0}}
|-
! <code>punctuation-trim</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>text-outline</code>
| {{no}}
| {{no}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=470547 |title=Bug 470547 - CSS3 text-outline尚未支援 |publisher=Mozilla}}</ref>
| {{table-experimental|[[#webcore_-webkit-|Nightly Build]]}}<ref group="w">{{citation |url=http://webkit.org/blog/85/introducing-text-stroke/ |title=Text-Stroke介紹 |publisher=Surfin’ Safari |first=Dave |last=Hyatt |date=2006-12-21}}</ref><ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=9475 |title=Bug 9475 - CSS3: 增加font-effect: outline支援 |publisher=WebKit}}</ref>
| {{no}}
| {{no}}
| {{no}}
|-
! <code>hanging-punctuation</code>
| {{no}}
| {{no}}
| {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=18109 |title=Bug 18109 - 實作懸吊標點（@@暫翻） |publisher=Webkit}}</ref>
| {{no}}
| {{no}}
| {{no}}
|-
! rowspan="5" | CSS 4
! <code>hyphenate-character</code>
| {{no}}
| rowspan="5" {{no}}
| rowspan="5" {{no}}
| rowspan="5" {{no}}
| rowspan="5" {{no}}
| rowspan="5" {{no}}
|-
! <code>hyphenate-limit-zone</code>
| {{table-experimental|10.0}}<ref group=t>{{cite web|title=-ms-hyphenate-limit-zone property (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/hh771869|publisher=Microsoft|accessdate=17 November 2012}}</ref>
|-
!<code>hyphenate-limit-chars</code>
| {{table-experimental|10.0}}<ref group=t>{{cite web|title=-ms-hyphenate-limit-chars property (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/hh771865|publisher=Microsoft|accessdate=17 November 2012}}</ref>
|-
! <code>hyphenate-limit-lines</code>
| {{table-experimental|10.0}}<ref group=t>{{cite web|title=-ms-hyphenate-limit-lines property (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/hh771867|publisher=Microsoft|accessdate=17 November 2012}}</ref>
|-
! <code>hyphenate-limit-last</code>
| {{no}}
|-
! colspan="2" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|-
! colspan="8" | {{Anchor|Text-decoration}}文本装饰<ref group="spec">{{citation |url=http://www.w3.org/TR/css-text-decor-3/ |title=CSS Text Decoration Module Level 3 |publisher=W3C}}</ref>
|-
! rowspan="10" | CSS 3
! <code>text-shadow</code>
| {{yes|10.0}}<ref group=t>{{cite web|title=text-shadow property (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/hh771872|publisher=Microsoft|accessdate=17 November 2012}}</ref>
| {{yes|1.9.1}}
| {{yes}}
| {{yes|3.4}}
| {{yes|2.1}}
| {{no}}
|-
! <code>text-decoration-style</code>
| {{no}}
| rowspan="3" {{table-experimental|6.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=59109 |title=Bug 59109 - implement CSS3 text module's text-decoration-style and text-decoration-color |publisher=Mozilla}}</ref><ref group="g">{{citation |url= https://developer.mozilla.org/en/Firefox_6_for_developers |title=Firefox 6 for developers |publisher=Mozilla}}</ref>
| rowspan="4" {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=58491 |title=Bug 58491 - <nowiki>[css3-text]</nowiki> Support text-decoration-* properties from CSS3 Text  |publisher=Webkit}}</ref>
| {{no}}
| {{no}}
| {{no}}
|-
! <code>text-decoration-color</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>text-decoration-line</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>text-decoration-skip</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>text-underline-position</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>text-emphasis-style</code>
| rowspan="4" {{no}}
| rowspan="4" {{yes|46.0}}
| rowspan="4" {{yes}}
| rowspan="4" {{no}}
| rowspan="4" {{no}}
| rowspan="4" {{no}}
|-
! <code>text-emphasis-color</code>
|-
! <code>text-emphasis</code>
|-
! <code>text-emphasis-position</code>
|- 
! colspan="8" | {{Anchor|Writing-modes}}書寫模式<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-writing-modes/ |title=CSS 3 書寫模式模組 |publisher=W3C}}</ref>
|- 
! rowspan="4" | CSS3
! <code>direction</code>
| {{yes|5.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| rowspan="2" {{yes|1.0}}
| {{yes|7.0}}
|-
! <code>unicode-bidi</code>
| {{yes|5.0}}
| {{yes|1.0}}
| {{yes|525}}
| {{yes}}
| {{yes|7.0}}
|-

! <code>writing-mode</code>
| {{incorrect|[[#trident_writing-mode|不正確]]}}
| {{yes|41.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=145503 |title=Bug 145503 - (writing-mode) CSS3 writing-mode （豎排） |publisher=Mozilla}}</ref>
| {{yes|[[#webcore_-webkit-|Nightly Build]]}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=46123 |title=Bug 46123 - 增加所有排版機制的writing-mode支援（主bug） |publisher=WebKit}}</ref>
| {{no}}
| {{no}}
| {{no}}
|-
! <code>text-combine</code>
| {{no}}
| {{no}}
| {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=48538 |title=Bug 48538 - 支援CSS「text-combine」屬性 |publisher=WebKit}}</ref>
| {{no}}
| {{no}}
| {{no}}
|-
! colspan="8" | {{Anchor|Table}}表格
|-
! rowspan="5" | CSS2
! <code>border-collapse</code>
| {{yes|8.0}}
| {{yes|1.0}}
| {{yes|125}}
| {{yes}}
| rowspan="5" {{yes|1.0}}
| {{yes|5.1}}
|-
! <code>border-spacing</code>
| {{yes|8.0}}
| {{yes|1.0}}
| {{yes|125}}
| {{yes}}
| {{yes|6.0}}
|-
! <code>caption-side</code>
| {{yes|8.0}}
| {{yes|1.4}}
| {{yes|85}}
| {{yes}}
| {{yes|5.0}}
|-
! <code>empty-cells</code>
| {{yes|8.0}}
| {{yes|1.0}}
| {{yes|125}}
| {{yes}}
| {{yes|5.0}}
|-
! <code>table-layout</code>
| {{yes|5.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|6.0}}
|-
! colspan="8" | {{Anchor|UI}}使用者界面<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-ui/ |title=CSS 3 基本使用者界面模組 |publisher=W3C}}</ref>
|-
! rowspan="5" | CSS2
! <code>cursor</code>
| {{yes|[[#trident_cursor|5.5]]}}
| {{yes|[[#trident_cursor|1.8]]}}
| {{yes|125}}
| {{yes}}
| {{partial|[[#presto_cursor|部份]]}}
| {{yes}}
|-
! <code>outline</code>
| {{yes|8.0}}
| {{yes|1.8}}
| {{yes|125}}
| {{yes}}
| rowspan="4" {{yes|1.0}}
| {{no}}
|-
! <code>outline-color</code>
| {{yes|8.0}}
| {{yes|1.8}}
| {{yes|125}}
| {{yes}}
| {{no}}
|-
! <code>outline-style</code>
| {{yes|8.0}}
| {{yes|1.8}}
| {{yes|125}}
| {{yes}}
| {{no}}
|-
! <code>outline-width</code>
| {{yes|8.0}}
| {{yes|1.8}}
| {{yes|125}}
| {{yes}}
| {{no}}
|-
! rowspan="10" | CSS3
! <code>outline-offset</code>
| {{no}}
| {{yes|1.8}}
| {{yes|125}}
| {{yes|3.5}}
| {{yes|2.1}}
| {{no}}
|-
! <code>box-sizing</code>
| {{yes|8.0}}
| {{table-experimental|[[#gecko_-moz-|實驗性質]]}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=243412 |title=實作「box-sizing」（丟掉「-moz-」前輟） |publisher=Mozilla}}</ref>
| {{table-experimental|[[#webcore_-webkit-|實驗性質]]}}
| {{yes|3.3.2}}
| {{yes|1.0}}
| {{yes|7.0}}
|-
! <code>resize</code>
| {{no}}
| {{nightly|2.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=553576 |title=Bug 553576 - 實作css 「resize」屬性的功能 |publisher=Mozilla}}</ref>
| {{yes|525}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>appearance</code>
| {{no}}
| {{table-experimental|[[#gecko_-moz-|實驗性質]]}}
| {{table-experimental|[[#webcore_-webkit-|實驗性質]]}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>icon</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>nav-index</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| rowspan="5" {{yes|2.1}}
| {{no}}
|-
! <code>nav-up</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>nav-right</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>nav-down</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>nav-left</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! colspan="2" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|-
! colspan="8" | {{Anchor|Page}}換頁媒體<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-page/ |title=CSS 3 換頁媒體模組 |publisher=W3C}}</ref>
|-
! rowspan="5" | CSS2

! <code>page-break-before</code>
| rowspan="2" {{yes|4.0}}
| rowspan="2" {{partial|[[#gecko_page-break-before-after|部份]]}}
| rowspan="2" {{partial|[[#webcore_page-break-before-after|部份]]}}
| rowspan="5" {{yes|3.5}}
| rowspan="5" {{yes|1.0}}
| {{yes|6.0}}
|-
! <code>page-break-after</code>
| {{yes|6.0}}
|-
! <code>page-break-inside</code>
| rowspan="3" {{yes|8.0}}
| {{no}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=132035 |title=Bug 132035 - 實作缺少的CSS 2.1功能 - 「page-break-*」  |publisher=Mozilla}}</ref>
| rowspan="3" {{yes|312}}
| {{yes|6.0}}
|-
! <code>orphans</code>
| rowspan="2" {{no}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=137367 |title=Bug 137367 - 實作「orphans」及「widows」 |publisher=Mozilla}}</ref>
| {{yes|6.0}}
|-
! <code>widows</code>
| {{yes|6.0}}
|-
! rowspan="5" | CSS3
! <code>page</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{yes}}
|-
! <code>size</code>
| {{no}}
| {{no}}
| {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=10894 |title=Bug 10894 - CSS 「size」屬性尚未支援 |publisher=Webkit}}</ref>
| {{no}}
| {{yes|1.0}}
| {{yes|6.0}}
|-
! <code>image-orientation</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>object-fit</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| rowspan="2" {{yes|2.7}}<ref group="p">{{citation|url=http://my.opera.com/desktopteam/blog/2010/08/03/presto-update |title=Opera 10.70 - Presto更新 |author=Haavard |date=2010-08-03 |publisher=Opera |archiveurl=https://web.archive.org/web/20100806103943/http://my.opera.com/desktopteam/blog/2010/08/03/presto-update |archivedate=2010-08-06 |deadurl=yes }}</ref>
| {{no}}
|-
! <code>object-position</code>
| {{no}}
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! colspan="8" | {{Anchor|Speech}}語音<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-speech/ |title=CSS 3 語音模組 |publisher=W3C}}</ref>
|-
! rowspan="8" | CSS2
! <code>cue</code>
| rowspan="23" {{no}}
| rowspan="23" {{no}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=47159 |title=Bug 47159 - 在getComputedStyle支援《css3-speech》（之前的聽覺樣式表）屬性 |publisher=Mozilla}}</ref>
| rowspan="6" {{no}}
| rowspan="23" {{no}}
| rowspan="8" {{yes|1.0}}
| rowspan="23" {{no}}
|-
! <code>cue-after</code>
|-
! <code>cue-before</code>
|-
! <code>pause</code>
|-
! <code>pause-after</code>
|-
! <code>pause-before</code>
|-
! <code>speak</code>
| {{nightly}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=46827 |title=Bug 46827 - AX: 實作CSS3 Speech 「speak」 |publisher=WebKit}}</ref>
|-
! <code>voice-family</code>
| rowspan="16" {{no}}
|-
! rowspan="15" | CSS3
! <code>voice-balance</code>
| rowspan="9" {{table-experimental|[[#presto_-xv-|實驗性質]]}}
|-
! <code>voice-duration</code>
|-
! <code>voice-pitch</code>
|-
! <code>voice-pitch-range</code>
|-
! <code>voice-rate</code>
|-
! <code>voice-stress</code>
|-
! <code>voice-volume</code>
|-
! <code>interpret-as</code>
|-
! <code>phonemes</code>
|-
! <code>rest</code>
| rowspan="6" {{no}}
|-
! <code>rest-after</code>
|-
! <code>rest-before</code>
|-
! <code>mark</code>
|-
! <code>mark-after</code>
|-
! <code>mark-before</code>
|-
! colspan="2" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|-
! colspan="8" | {{Anchor|Mediaqueries}}媒體查詢<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-mediaqueries/ |title=媒體查詢 |publisher=W3C}}</ref>
|-
! rowspan="13" | CSS3
! <code>width</code>
| rowspan="13" {{nightly|9.0}}<ref group="t" name="ie9-preview" />
| rowspan="11" {{yes|1.9.1}}
| rowspan="8" {{yes|525}}
| rowspan="9" {{yes|4.1}}
| rowspan="5" {{yes|2.0}}
| ?
|-
! <code>height</code>
| ?
|-
! <code>device-width</code>
| ?
|-
! <code>device-height</code>
| ?
|-
! <code>device-aspect-ratio</code>
| ?
|-
! <code>color</code>
| rowspan="4" {{yes|2.5}}
| ?
|-
! <code>color-index</code>
| ?
|-
! <code>monochrome</code>
| ?
|-
! <code>resolution</code>
| rowspan="5" {{no}}
| ?
|-
! <code>orientation</code>
| rowspan="2" {{yes|4.2.1}}
| {{no}}
| ?
|-
! <code>aspect-ratio</code>
| {{yes|2.1}}
| ?
|-
! <code>grid</code>
| rowspan="2" {{no}}
| rowspan="2" {{yes|4.1}}
| rowspan="2" {{yes|2.5}}
| ?
|-
! <code>scan</code>
| ?
|-
! colspan="8" | {{Anchor|Ruby}}Ruby字元<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-ruby/ |title=CSS 3 Ruby模組 |publisher=W3C}}</ref>
|-
! rowspan="4" | CSS3
! <code>ruby-position</code>
| rowspan="3" {{yes|5.0}}
| rowspan="4" {{yes|38.0}}<ref group="g">{{citation |url=https://developer.mozilla.org/en-US/docs/Web/CSS/ruby-position |title=ruby-position - CSS |publisher=Mozilla Developer Network}}</ref>
| rowspan="4" {{no}}
| rowspan="4" {{no}}
| rowspan="4" {{no}}
| rowspan="4" {{no}}
|-
! <code>ruby-align</code>
|-
! <code>ruby-overhang</code>
|-
! <code>ruby-span</code>
| {{no}}
|-
! colspan="8" | {{Anchor|Multicol}}多欄排版<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-multicol/ |title=CSS 3 多欄排版模組 |publisher=W3C}}</ref>
|-
! rowspan="10" | CSS3
! <code>column-count</code>
| rowspan="10" {{yes|10.0}}<ref group=t>{{cite web|title=Multi-column Layout (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/hh771877|publisher=Microsoft|accessdate=17 November 2012}}</ref>
| rowspan="4" {{table-experimental|[[#gecko_-moz-|实验性质]]}}<ref group="g" name="moz-multicol">{{Citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=684062 |title=Bug 684062 - Compare spec and implement CSS multi-column support |publisher=Mozilla}}</ref>
| rowspan="5" {{table-experimental|[[#webcore_-webkit-|实验性质]]}}
| rowspan="10" {{no}}
| rowspan="10" {{yes|2.8}}<ref group="p">{{Cite web |url=http://www.opera.com/docs/specs/presto28/css/multicolumnlayout/ |title=CSS Multi-column Layout Module support in Opera Presto 2.8 |date=2011-03-06 |accessdate=2011-03-06 |publisher=Opera}}</ref>
| rowspan="5" {{yes}}
|-
! <code>column-width</code>
|-
! <code>column-gap</code>
|-
! <code>column-rule</code>
|-
! <code>columns</code>
| {{table-experimental|9.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=446569 |title=Bug 446569 - Implement CSS3 columns shorthand |publisher=Mozilla}}</ref>
|-
! <code>break-before</code>
| rowspan="3" {{no}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=549114 |title=Bug 549114 - Support Column Breaks|publisher=Mozilla}}</ref>
| rowspan="2" {{table-experimental|[[#webcore_-webkit-|实验性质]]}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=15552 |title= Bug 15552 - Support CSS3 column-break-before and column-break-after |publisher=WebKit}}</ref>
| rowspan="4" {{yes|6.0}}
|-
! <code>break-after</code>
|-
! <code>break-inside</code>
| rowspan="1" {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=39498#c7 |title= Bug 39498 - [CSS3 Multi-column] Floating elements are rendered below the columns |publisher=WebKit}}</ref>
|-
! <code>column-fill</code>
| {{table-experimental|14.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=695222 |title=Bug 695222 - Implement column-fill |publisher=Mozilla}}</ref>
| {{no}}
|-
! <code>column-span</code>
| {{no}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=616436 |title=Bug 616436 - column-span not implemented (css3 multicolumn) |publisher=Mozilla}}</ref>
| {{table-experimental|[[#webcore_-webkit-|实验性质]]}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=15550 |title=Bug 15550 - WebKit does not support CSS3 column-span: |publisher=Webkit}}</ref>
| {{no}}
|-
! colspan="2" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|-
! colspan="8" | {{Anchor|Animation}}動畫<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-animations/ |title=CSS 3 動畫模組 |publisher=W3C}}</ref>
|-
! rowspan="10" | CSS3
|-
! <code>animation</code>
| rowspan="9" {{yes|10.0}}<ref group=t>{{cite web|title=Animations (Internet Explorer)|url=http://msdn.microsoft.com/en-us/library/ie/hh771874|publisher=Microsoft|accessdate=17 November 2012}}</ref>
| rowspan="9" {{yes|16.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=435442 |title=Bug 435442 - Implement Webkit's CSS Animation proposal |publisher=Mozilla}}</ref>
| rowspan="9" {{table-experimental|[[#webcore_-webkit-|实验性质]]}}
| rowspan="9" {{no}}
| rowspan="9" {{yes|2.12}}
| rowspan="9" {{no}}
|-
! <code>animation-delay</code>
|-
! <code>animation-direction</code>
|-
! <code>animation-duration</code>
|-
! <code>animation-iteration-count</code>
|-
! <code>animation-name</code>
|-
! <code>animation-play-state</code>
|-
! <code>animation-timing-function</code>
|-
! <code>animation-fill-mode</code>
|-
! colspan="8" | {{Anchor|Transform}}2D變換<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-2d-transforms/ |title=CSS 3 2D變換模組 |publisher=W3C}}</ref>
|-
! rowspan="3" | CSS3
|-
! <code>transform</code>
| rowspan="2" {{nightly|實驗性質}}<ref group="t" name="ie9-preview" />
| rowspan="2" {{table-experimental|[[#gecko_-moz-|實驗性質]]}}
| rowspan="2" {{table-experimental|[[#webcore_-webkit-|實驗性質]]}}
| rowspan="2" {{no}}
| rowspan="2" {{table-experimental}}
| rowspan="2" {{no}}
|-
! <code>transform-origin</code>
|-
! colspan="2" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]}
|-
! colspan="8" | {{Anchor|3D-transform}}3D變換<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-3d-transforms/ |title=CSS 3 3D變換模組 |publisher=W3C}}</ref>
|-
! rowspan="7" | CSS3
|-
! <code>transform</code>
| rowspan="6" {{no}}
| rowspan="6" {{no}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=505115 |title=Bug 505115 - CSS3 3D變換 |publisher=Mozilla}}</ref>
| rowspan="6" {{table-experimental|[[#webcore_-webkit-|實驗性質]]}}
| rowspan="6" {{no}}
| rowspan="6" {{no}}
| rowspan="6" {{no}}
|-
! <code>transform-origin</code>
|-
! <code>transform-style</code>
|-
! <code>perspective</code>
|-
! <code>perspective-origin</code>
|-
! <code>backface-visibility</code>
|-
! colspan="8" | {{Anchor|Transitions}}轉變<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-transitions/ |title=CSS 3 轉變模組 |publisher=W3C}}</ref>
|-
! rowspan="6" | CSS3
|-
! <code>transition-property</code>
| rowspan="5" {{no}}
| rowspan="5" {{nightly|2.0 (實驗性質)}}<ref group="g" name="moz-trans">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=537142 |title=Bug 435441 - 把CSS轉變弄到可以釋出的程度 |publisher=Mozilla}}</ref>
| rowspan="5" {{table-experimental|[[#webcore_-webkit-|實驗性質]]}}
| rowspan="5" {{no}}
| rowspan="5" {{table-experimental}}
| rowspan="5" {{no}}
|-
! <code>transition-duration</code>
|-
! <code>transition-timing-function</code>
|-
! <code>transition-delay</code>
|-
! <code>transition</code>
|-
! colspan="8" | {{Anchor|Flexbox}}彈性盒排版(@@翻譯)<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-flexbox/ |title=CSS3 彈性盒排版(@@翻譯)模組 |publisher=W3C}}</ref>
|-
! rowspan="9" | CSS3
|-
! <code>box-align</code>
| rowspan="8" {{no}}
| rowspan="4" {{table-experimental|[[#gecko_-moz-|實驗性質]]}}
| rowspan="8" {{table-experimental|[[#webcore_-webkit-|實驗性質]]}}
| rowspan="8" {{no}}
| rowspan="8" {{no}}
| rowspan="8" {{no}}
|-
! <code>box-direction</code>
|-
! <code>box-flex</code>
|-
! <code>box-flex-group</code>
|-
! <code>box-lines</code>
| {{no}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=562073 |title=Bug 562073 - 實作css3-flexbox的「box-lines」屬性 |publisher=Mozilla}}</ref>
|-
! <code>box-ordinal-group</code>
| rowspan="3" {{table-experimental|[[#gecko_-moz-|實驗性質]]}}
|-
! <code>box-orient</code>
|-
! <code>box-pack</code>
|-
! colspan="8" | {{Anchor|Marquee}}彈幕(@@翻譯xd)<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-marquee/ |title=CSS 3 彈幕模組 |publisher=W3C}}</ref>
|-
! rowspan="6" | CSS3
|-
! <code>marquee-direction</code>
| rowspan="5" {{no}}
| rowspan="5" {{no}}
| rowspan="4" {{table-experimental|[[#webcore_-webkit-|實驗性質]]}}<ref group="w">{{citation |url=http://ajnaware.wordpress.com/2008/08/14/scrolling-text-with-webkit-marquee/ |title=以「-webkit-marquee」轉動文字 |date=2008-08-14 |publisher=Ajnaware}}</ref>
| rowspan="5" {{no}}
| rowspan="5" {{no}}
| rowspan="5" {{no}}
|-
! <code>marquee-play-count</code>
|-
! <code>marquee-speed</code>
|-
! <code>marquee-style</code>
|-
! <code>overflow-style</code>
| {{no}}
|-
! colspan="2" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|}

=== 一般屬性附註 ===
# <code id="general_text-decoration">text-decoration</code> — Gecko或Webkit的底線有可能會畫過行級(@@inline翻譯)取代元素（例如圖片）。

=== Trident屬性附註 ===
# <tt id="trident_margin">margin</tt> — <code>inherit</code>繼承未計算值然後再計算一次而不是直接繼承計算後的值。<ref group="t">{{citation |url=https://connect.microsoft.com/IE/feedback/ViewFeedback.aspx?FeedbackID=344787 |title=用「inherit」繼承的邊界(margin) - 應該繼承計算後的值 |last=Talbot}}</ref>
# <tt id="trident_display">display</tt> — 7.0之前，支援無誤的只有<code>none</code>、<code>block</code>、<code>inline</code>、<code>table-header-group</code>及<code>table-footer-group</code>。8.0之前，沒支援<code>run-in</code>與<code>table</code>，而<code>inline-block</code>僅支援在行級元素上。 
# <tt id="trident_overflow">overflow</tt> — 7.0之前，<code>overflow: visible;</code>支援的不正確。在8.0，<code>scroll</code>將該元素的高度調至<code>max-height</code>，就算內容並沒有這麼高。<ref group="t">{{citation |url=https://connect.microsoft.com/IE/feedback/ViewFeedback.aspx?FeedbackID=408759 |title=「Overflow: scroll」讓一個元素永遠用它的「max-height」 |last=Groot |first=Sven}}</ref>
# <tt id="trident_visibility">visibility</tt> — 8.0之前，未支援「<code>visibility: collapse;</code>」。在8.0，<code>visibility: hidden;</code>的塊元素(@@block翻譯)中「<code>visibility: visible;</code>」的行級元素不被顯示。<ref group="t">{{citation |url=https://connect.microsoft.com/IE/feedback/ViewFeedback.aspx?FeedbackID=442805 |title=用「visibility:visible」的行級元素不蓋掉從它母元素（塊元素）被繼承的「visibility:hidden」 |last=Hopkins |first=James}}</ref>
# <tt id="trident_content">content</tt> — 在8.0，<code>attr()</code>的算後值不在屬性(attribute)變更時被更新。<ref group="t">{{citation |url=https://connect.microsoft.com/IE/feedback/ViewFeedback.aspx?FeedbackID=434925 |title=「content: attr(x)」不在屬性值更改時被更新}}</ref>
# <tt id="trident_border-color">border-color</tt> — 7.0之前，不支援<code>transparent</code>。
# <tt id="trident_border-style">border-style</tt> — 8.0之前，不支援<code>hidden</code>。
# <tt>border-style</tt> — 7.0之前，<code>dotted</code>被顯示成<code>dashed</code>。
# <tt id="trident_box-shadow">box-shadow</tt> — 9.0之前，trident支援自從5.5就有的類似的專有屬性「Shadow」<ref group="t">{{citation |url=http://msdn.microsoft.com/en-us/library/ms533086(VS.85).aspx |title=Shadow過濾器 |publisher=Microsoft}}</ref>及「DropShadow」<ref group="t">{{citation |url=http://msdn.microsoft.com/en-us/library/ms532985(VS.85).aspx |title=DropShadow過濾器 |publisher=Microsoft}}</ref>過濾器。
# <tt id="trident_position">position</tt> — 7.0之前，未支援固定配置。7.0跟之後版本只在標準模式的時候支援。
# <tt id="trident_z-index">z-index</tt> —  8.0之前，僅部份支援<code>z-index</code>。<ref group="t">{{citation |url=http://msdn.microsoft.com/en-us/library/cc351024(VS.85).aspx#positioning |title=配置 |publisher=}}</ref>在8.0，除了整數以外也支持浮點數。<ref group="t">{{citation |url=https://connect.microsoft.com/IE/feedback/details/386914/illegal-parsing-of-a-z-index-decimal-value-instead-of-an-integer |title=「z-index」的語法分析不合法 - 分析為小數而非整數 |last=Hopkins |first=James}}</ref>
# <tt id="trident_list-style-type">list-style-type</tt> — 8.0之前，不支援<code>armenian</code>、<code>decimal-leading-zero</code>、<code>georgian</code>、<code>lower-greek</code>、<code>lower-latin</code>、<code>upper-latin</code>。
# <tt id="trident_opacity">opacity</tt> — 9.0之前，Trident支援一個專有的替代屬性。<ref group="t">{{citation |url=http://msdn.microsoft.com/en-us/library/ms532967(VS.85).aspx |title=Alpha過濾器 |publisher=Microsoft}}</ref>
# <tt id="trident_background-image">background-image</tt> — 8.0之前，背景圖片在某些情況下被處理的很糟。<ref group="t">{{citation |url=http://css-class.com/test/bugs/ie/escaping-background-image-bug1.htm |title=IE7-/背景圖片跑不見 - Demo 1 |deadurl=yes |archiveurl=https://web.archive.org/web/20100103170233/http://css-class.com/test/bugs/ie/escaping-background-image-bug1.htm |archivedate=2010-01-03 }}</ref><ref group="t">{{citation |url=http://css-class.com/test/bugs/ie/escaping-background-image-bug2.htm |title=IE7-/背景圖片跑不見 - Demo 2 |deadurl=yes |archiveurl=https://web.archive.org/web/20100422123501/http://css-class.com/test/bugs/ie/escaping-background-image-bug2.htm |archivedate=2010-04-22 }}</ref>
# <tt id="trident_background-attachment">background-attachment</tt> — 7.0之前，<code>fixed</code>只被允許使用在<code>body</code>元素上。
# <tt id="trident_background-position">background-position</tt> — 8.0之前，不支援固定配置。
# <tt id="trident_font-weight">font-weight</tt> — 8.0之前，當取值為600顯示不正確。<ref group="t">{{citation |url=http://www.quirksmode.org/css/tests/iewin_fontweight.html |title=IE Windows與Opera - 「font-weight: 600」 vs. 「bold」 |last=Koch |first=Peter-Paul |publisher=QuirksMode}}</ref>
# <tt id="trident_text-align">text-align</tt> — 在8.0，<code>text-align</code>不被<code>:before</code>及<code>:after</code>擬元素繼承。<ref group="t">{{citation |url=https://connect.microsoft.com/IE/feedback/ViewFeedback.aspx?FeedbackID=454985 |title=「text-align」的值不被擬元素「:before」與「:after」繼承 |last=Hopkins |first=James}}</ref>
# <tt id="trident_white-space">white-space</tt> — 6.0之前，不支援<code>pre</code>。8.0之前，僅部份支援<code>white-space</code>：不支援<code>pre-line</code>及<code>pre-wrap</code>。<ref group="t">{{citation |url=http://msdn.microsoft.com/en-us/library/cc351024#font |title=自型與文字 |publisher=Microsoft}}</ref>
# <tt id="trident_writing-mode">writing-mode</tt> — Trident支援過期的取值<code>lr-tb</code>、<code>tb-rl</code>、<code>tb-lr</code>等等。<ref group="t">{{citation |url=http://msdn.microsoft.com/en-us/library/ms531187.aspx |title=「writingMode」屬性 |publisher=Microsoft}}</ref>這些取值作用在<code>direction</code>上。這是與Webkit不同的行為。
# <tt id="trident_cursor">cursor</tt> — 仍作用於沒前輟的瀏覽器擴充。

=== Gecko屬性附註 ===
# <tt id="gecko_display">display</tt> — 不支援<code>run-in</code>。<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=2056 |title=Bug 2056 - 「display: run-in」尚無實作 |publisher=Mozilla}}</ref>1.9之前，不支援「<code>inline-table</code><ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=18217 |title=Bug 18217 - 「display: inline-table」無實作 |publisher=Mozilla}}</ref>」與「<code>inline-block</code><ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=9458 |title=Bug 9458 - (inline-block)實作「inline-block」 |publisher=Mozilla}}</ref>」。
# <tt id="gecko_z-index">z-index</tt> — 1.9之前負數的支援情況不佳。
# <tt id="gecko_quotes">quotes</tt> — 1.8之前不支援巢狀引用。<ref group="g">{{citation |url=http://www.mozilla.org/projects/deerpark/new-web-dev-features.html |title=Deer Park Alpha 1中給Web Developer的新功能 |publisher=Mozilla}}</ref>
# <tt id="gecko_content">content</tt> — 1.9之前不支援「<code>none</code>」。此屬性不作用在一般元素（非擬元素），不符合《CSS 3 生成內容與取代內容模組》。
# <tt id="gecko_background-position">background-position</tt> — 1.7以前的版本使用CSS2語法，非CSS2.1的擴充語法。
# <tt id="gecko_font-size-adjust">font-size-adjust</tt> — 1.9之前，僅在視窗版支援。
# <tt id="gecko_font-weight">font-weight</tt> — 就算裝了一個字型的Light或Heavy/Black[[字模|字模]]，除非使用Gecko 2.0在Windows 7或Windows Vista的DirectWrite，僅Regular與Bold會被使用。
# <tt id="gecko_white-space">white-space</tt> — 1.9.1之前不支援<code>pre-line</code>。1.9之前，以<code>-moz-pre-wrap</code>實驗性地支援<code>pre-wrap</code>的功能。
# <tt id="gecko_visibility">visibility</tt> — 1.8之前不支援<code>collapse</code>。
# <tt id="gecko_border-radius">border-radius</tt> — 1.9.1之前，邊框的曲線是圓形而不是同現在CSS3草案記載的橢圓曲線，短宣告<code>border-radius</code>的順序是「左上 右上 右下 左下」而不是W3C的「右上 右下 左下 左上」。當邊框的樣式是點線(dotted)破折線(dashed)，曲線總是顯示實線為。<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=382721 |title=Bug 382721 - 點線/破折線的「-moz-border-radius」邊框顯示為實線 |publisher=Mozilla}}</ref>
# <tt id="gecko_page-break-before-after">page-break-before; page-break-after</tt> — 僅支援「<code>always</code>」與「<code>auto</code>」。

=== WebKit屬性附註 ===
# <tt id="webcore_font">font</tt> — 不支援讓設計師根據使用者作業系統呈現結果的系統字型關鍵字。
# <tt id="webcore_font-weight">font-weight</tt> — 就算裝了一個字型的Light或Heavy/Black[[字模|字模]]，僅Regular與Bold會被使用。
# <tt id="webcore_page-break-before-after">page-break-before; page-break-after</tt> — 僅支援「<code>always</code>」與「<code>auto</code>」。
# <tt id="webcore_white-space">white-space</tt> — 522之前，不支援「<code>pre-line</code>」與「<code>pre-wrap</code>」。
# <tt id="webcore_visibility">visibility</tt> — 522之前不支援「<code>collapse</code>」，這個值的實作跟「<code>hidden</code>」一樣，因此不合標準。<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=8735 |title=Bug 8735 - CSS 2.1 「visibility: collapse」顯示為「visibility: hidden」 |publisher=Webkit}}</ref>
# <tt id="webkit_content">content</tt> — 不支援「<code>none</code>」、「<code>open-quote</code>」、「<code>close-quote</code>」、「<code>no-open-quote</code>」、「<code>no-close-quote</code>」及「<code>normal</code>」，且此屬性不作用在一般元素（非擬元素），不符合《CSS 3 生成內容與取代內容模組》。
# <tt>font-size</tt> — 「<code>font-size</code>」屬性不見得吃0這個值，就算用「font-size: 0px」，文字還是看得見。

=== KHTML屬性附註 ===
# <tt id="khtml_overflow">overflow</tt> — 不支援取值「<code>scroll</code>」與「<code>auto</code>」。
# <tt id="khtml_page-break-before-after">page-break-before; page-break-after</tt> — 3.5之前僅支援「<code>always</code>」與「<code>auto</code>」。
# <tt id="khtml_visibility">visibility</tt> — 支援所有的屬性，但「<code>collapse</code>」這個值的實作跟「<code>hidden</code>」一樣，因此不合標準。

=== Presto屬性附註 ===
# <tt id="presto_counter">counter-increment, counter-reset</tt> — 使用推薦標準版本(CSS2)的演算法。
# <tt id="presto_background-position">background-position</tt> — Presto在Opera 8.0以前的版本使用CSS2語法，非CSS2.1的擴充語法。
# <tt id="presto_font-weight">font-weight</tt> — 當取值為600顯示不正確，與以Trident為對象設計的網站兼容。
# <tt id="presto_visibility">visibility</tt> — 2.5之前，在表格列裡不支援「<code>collapse</code>」這個值，在表格行裡，這個值呈現與「<code>hidden</code>」同樣的效果因此不合標準。
# <tt id="presto_cursor">cursor</tt> — 「<code>cursor</code>」不支援動態擬類別，且不支援自定游標。
# <tt id="presto_content">content</tt> — 不支援取值「<code>none</code>」。<ref group="p">{{citation |url=http://www.quirksmode.org/css/beforeafter_content.html |title=「:before/:after」與「content」 |publisher=Quirksmode |first=Peter-Paul |last=Koch}}</ref>
# <tt id="presto_font">font</tt> — 不應該吃「<code>inherit</code>」跟一個「font-size」取值的情形，這應該被當作語法錯誤並丟棄，但Opera接受這種狀況。

=== Prince XML屬性附註 ===
# <tt id="prince-visibility">visibility</tt> — 不支援取值「<code>collapse</code>」。<ref group="r" name="prince"/>
# <tt id="prince-list-style">list-style</tt> — 不支援取值「<code>armenian</code>」與「<code>georgian</code>」。<ref group="r" name="prince"/>
# <tt id="prince-content">content</tt> — 不支援取值「<code>open-quote</code>」與「<code>close-quote</code>」。<ref group="r" name="prince"/>

== 取值與單位 ==
{| style="width: 95%;" class="wikitable"
|-
! colspan="3" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|-
! colspan="9" | 數<ref group="spec">{{citation |url=http://www.w3.org/TR/css3-values/ |title=CSS 3 取值與單位模組 |publisher=W3C}}</ref>
|-
! rowspan="4" | CSS2
! <code><number></code>
| [[浮點數|浮點數]]
| rowspan="4" {{yes|3.0}}
| rowspan="4" {{yes|1.0}}
| rowspan="4" {{yes|85}}
| rowspan="4" {{yes}}
| rowspan="4" {{yes|[[#presto_float|1.0]]}}
| rowspan="4" {{yes|6.0}}
|-
! <code><length></code>
| <number>接單位
|-
! <code><percentage></code>
| <number>接'''%'''
|-
! <code><integer></code>
| [[整數|整數]]
|-
! rowspan="4" | CSS3
! <code><angle></code>
| <number>接角度單位
| rowspan="2" {{nightly|9.0}}<ref group="t" name="ie9-preview" />
| {{partial|[[#general_angle|部份]]}}
| {{partial|[[#general_angle|部份]]}}
| {{partial|[[#general_angle|部份]]}}
| {{partial|[[#general_angle|部份]]}}
| rowspan="4" {{no}}
|-
! <code><time></code>
| <number>接長度單位
| {{nightly|2.0}}<ref group="g" name="moz-trans"/>
| rowspan="2" {{yes}}
| rowspan="2" {{yes}}
| {{yes|2.5}}
|-
! <code><frequency></code>
| <number>接頻率單位
| rowspan="2" {{no}}
| rowspan="2" {{no}}
| rowspan="2" {{no}}
|-
! <code><fraction></code>
| 剩餘空間
| {{no}}
| {{no}}
|-
! colspan="9" | 字串
|-
! rowspan="2" | CSS2
! <code><string></code>
| String
| {{yes|3.0}}
| rowspan="2" {{yes|1.0}}
| rowspan="2" {{yes|85}}
| rowspan="2" {{yes}}
| rowspan="2" {{yes|1.0}}
| rowspan="2" {{yes}}
|-
! <code>\code</code>
| Unicode轉意
| {{yes|6.0}}
|-
! colspan="9" | 型
|-
! CSS2
! <code>rect()</code>
| 長方型
| {{yes|[[#trident_rect|8.0]]}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|1.0}}
| {{yes}}
|-
! colspan="9" | 函數
|-
! rowspan="3" | CSS2
! <code>url()</code>
| [[URI|URI]]
| {{yes|3.0}}
| rowspan="3" {{yes|1.0}}
| rowspan="3" {{yes|85}}
| rowspan="3" {{yes}}
| rowspan="3" {{yes|1.0}}
| rowspan="3" {{yes}}
|-
! <code>counter()</code>
|
| rowspan="2" {{yes|8.0}}
|-
! <code>attr()</code>
| 屬性標示符
|-
! CSS3
! <code>calc()</code>
|
| {{nightly|9.0}}<ref group="t" name="ie9-preview" />
| {{nightly|2.0 (實驗性質)}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=363249 |title=Bug 363249 - 實作css3-values的「calc()」 |publisher=Mozilla}}</ref>
| {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=16662 |title=Bug 16662 - CSS3: 實作「calc()」 |publisher=Webkit}}</ref>
| {{no}}
| {{no}}
| {{no}}
|-
! colspan="9" | 顏色
|-
! rowspan="4" | CSS2
! HTML4顏色關鍵字
| 16個預定義[[網頁顏色模式|網頁顏色]]
| rowspan="2" {{yes|3.0}}
| rowspan="4" {{yes|1.0}}
| rowspan="4" {{yes|85}}
| rowspan="4" {{yes}}
| rowspan="4" {{yes|1.0}}
| rowspan="4" {{yes}}
|-
! <code>#rrggbb或#rgb</code>
| [[十六進位|十六進位]]記法
|-
! <code>rgb(r, g, b)</code>
| [[三原色光模式|RGB]]記法
| {{yes|4.0}}
|-
! <code>系統顏色</code><ref group="spec">{{citation |url=http://www.w3.org/TR/CSS21/ui.html#system-colors |title=系統顏色 |publisher=W3C}}</ref>
| 28預定義系統顏色
| {{yes|3.0}}
|-
! rowspan="6" | CSS3
! SVG顏色關鍵字
|
| {{yes|8.0}}
| {{yes}}
| {{yes}}
| {{yes}}
| {{yes}}
| {{?}}
|-
! <code>currentColor</code>
| <code>color</code>屬性的值
| rowspan="4" {{nightly|9.0}}<ref name="ie9-preview" group="t" />
| {{yes|1.8}}
| {{yes|528}}
| {{yes}}
| {{yes|2.1}}
| {{?}}
|-
! <code>rgba(r, g, b, a)</code>
| [[RGBA|RGBA]]記法
| {{yes|1.9}}
| rowspan="4" {{yes|525}}
| {{yes|4.0}}
| {{yes|2.2}}
| {{yes|6.0}}
|-
! <code>hsl(h, s, l)</code>
| [[HSL和HSV色彩空間|HSL]]記法
| {{yes|1.5}}
| {{yes|3.5.5}}
| {{yes|2.1}}
| rowspan="2" {{no}}
|-
! <code>hsla(h, s, l, a)</code>
| [[HSL和HSV色彩空間|HSLA]]記法
| {{yes|1.9}}
| {{yes|3.5.5}}
| {{yes|2.2}}
|-
! <code>[[#general_transparent|transparent]]</code>
| 全[[透明|透明]]
| {{partial|[[#trident_transparent|部份]]}}
| {{yes|1.9}}
| {{yes|4.0}}
| {{partial|[[#presto_transparent|部份]]}}
| {{partial}}
|-
! colspan="9" | 圖像值<ref group="spec">{{citation |url=http://dev.w3.org/csswg/css3-images/ |title=CSS 3 圖像值模組 |publisher=W3C}}</ref>
|-
! CSS2
! <code><url></code>
| rowspan="5" | 圖像形態
| {{yes|3.0}}
| {{yes|1.0}}
| {{yes|85}}
| {{yes}}
| {{yes|1.0}}
| {{yes}}
|-
! rowspan="8"| CSS3
! <code><sprite></code>
| rowspan="8" {{no}}
| rowspan="2" {{no}}
| rowspan="2" {{no}}
| rowspan="8" {{no}}
| rowspan="8" {{no}}
| rowspan="8" {{no}}
|-
! <code><image-list></code>
|-
! <code><linear-gradient></code>
| rowspan="6" {{table-experimental|[[#gecko_-moz-|實驗性質]]}}
| rowspan="4" {{table-experimental}}
|-
! <code><radial-gradient></code>
|-
! <code>linear-gradient()</code>
| rowspan="4" | 漸層
|-
! <code>radial-gradient()</code>
|-
! <code>repeating-linear-gradient()</code>
| rowspan="2" {{no}}
|-
! <code>repeating-radial-gradient()</code>
|-
! colspan="9" | 關鍵字
|-
! rowspan="2"| CSS2
! <code>auto</code>
| 自動
| {{yes|[[#trident_auto|6.0]]}}
| rowspan="2" {{yes|1.0}}
| rowspan="2" {{yes|85}}
| rowspan="2" {{yes}}
| rowspan="2" {{yes|1.0}}
| rowspan="2" {{yes}}
|-
! <code>inherit</code>
| 從母元素繼承
| {{yes|8.0}}
|-
! CSS3
! <code>initial</code>
|
| {{no}}
| {{table-experimental|[[#gecko_-moz-|實驗性質]]}}
| {{yes|125}}
| {{no}}
| {{no}}
| {{no}}
|-
! colspan="9" | 單位
|-
! rowspan="9" | CSS2
! <code>px</code>
| [[像素|像素]]
| rowspan="9" {{yes|3.0}}
| rowspan="9" {{yes|1.0}}
| rowspan="9" {{yes|85}}
| rowspan="9" {{yes}}
| rowspan="9" {{yes|1.0}}
| rowspan="9" {{yes}}
|-
! <code>pt</code>
| [[點_(印刷)|點]]
|-
! <code>pc</code>
| [[倍卡|倍卡]]
|-
! <code>cm</code>
| [[公分|公分]]
|-
! <code>mm</code>
| [[公釐|公釐]]
|-
! <code>in</code>
| 英尺
|-
! <code>em</code>
| [[正方|正方]]
|-
! <code>ex</code>
| [[X字高|X字高]]
|-
! <code>%</code>
| [[百分比|百分比]]
|-
! rowspan="18" | CSS3
! <code>deg</code>
| [[角度|度]]
| rowspan="6" {{nightly|9.0}}<ref name="ie9-preview" group="t" />
| rowspan="3" {{yes|1.9.1}}
| rowspan="3" {{yes}}
| rowspan="3" {{yes}}
| rowspan="3" {{yes|2.5}}
| rowspan="18" {{no}}
|-
! <code>grad</code>
| [[梯度_(角)|梯度]]
|-
! <code>rad</code>
| [[弧度|弧度]]
|-
! <code>turn</code>
| [[轉_(角)|轉]]
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>ms</code>
| [[毫秒|毫秒]]
| rowspan="2" {{nightly|2.0}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=435441 |title=Bug 435441 - 實作Webkit的《CSS Transitions》提案 |publisher=Mozilla}}</ref>
| rowspan="4" {{yes}}
| rowspan="4" {{yes}}
| rowspan="2" {{yes|2.5}}
|-
! <code>s</code>
| 秒
|-
! <code>Hz</code>
| [[赫茲|赫茲]]
| rowspan="7" {{no}}
| rowspan="2" {{no}}
| rowspan="2" {{no}}
|-
! <code>kHz</code>
| [[千赫|千赫]]
|-
! <code>dpi</code>
| [[dpi|dpi]]
| rowspan="2" {{yes|1.9.1}}
| rowspan="2" {{no}}
| rowspan="2" {{yes|4.1}}
| rowspan="2" {{yes|2.5}}
|-
! <code>dpcm</code>
| [[dpi|dpcm]]
|-
! <code>dppx</code>
| [[dppx|dppx]]
| {{no}}
| {{no}}
| {{?}}
| {{no}}
|-
! <code>gd</code>
| 網格數
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>fr</code>
| 剩餘空間分配數
| {{no}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>rem</code>
| 根原素字型大小
| rowspan="5" {{nightly|9.0}}<ref name="ie9-preview" group="t" />
| {{yes|1.9.2}}
| {{no}}
| {{no}}
| {{no}}
|-
! <code>vw</code>
| [[視口|視口]]的寬度
| rowspan="3" {{no}}<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=503720 |title=Bug 503720 - 實作《CSS 3 取值與單位模組》的 vw/vh/vm（視口大小） |publisher=Mozilla}}</ref>
| rowspan="3" {{no}}<ref group="w">{{citation |url=https://bugs.webkit.org/show_bug.cgi?id=27160 |title=Bug 27160 - 實作《CSS 3 取值與單位模組》的 vw/vh/vm（視口大小 |publisher=Webkit}}</ref>
| rowspan="3" {{no}}
| rowspan="3" {{no}}
|-
! <code>vh</code>
| [[視口|視口]]的高度
|-
! <code>vm</code>
| [[視口|視口]]高度跟寬度小的那個
|-
! <code>ch</code>
| 從字型中抽出的該大小的「0」(ZERO, U+0030)的[[字形|字形]]寬度
| {{yes|[[#gecko_ch|1.9.1]]}}
| {{no}}
| {{no}}
| {{no}}
|-
! colspan="3" |
! style="width: 12%" | [[Trident_(排版引擎)|Trident]]
! style="width: 12%" | [[Gecko|Gecko]]
! style="width: 12%" | [[WebKit|WebKit]]
! style="width: 12%" | [[KHTML|KHTML]]
! style="width: 12%" | [[Presto|Presto]]
! style="width: 12%" | [[Prince_XML|Prince XML]]
|}

===取值與單位一般附註===
# <tt id="general_transparent">transparent</tt> — <blockquote cite="http://www.w3.org/TR/2008/WD-css3-color-20080721/#transparent">CSS1引入了「transparent」當作「background-color」的一個值。 CSS2開始允許「border-color」使用「transparent」。《Open eBook(tm) Publication Structure 1.0.1》[OEB101]擴張了「color」屬性使其也吃關鍵字「transparent」。CSS3擴張了顏色的取值使其包含關鍵字「transparent」，使得所有吃<value>的屬性都可以使用這個值，這也簡化了這些屬性在CSS3的定義。</blockquote>
# <tt id="general_angle"><angle></tt> — 不支援 <code>turn</code>。

===取值與單位Trident附註===
# <tt id="trident_rect">rect()</tt> — 8.0之前，不支援用逗號的正確語法。
# <tt id="trident_auto">auto</tt> — 在 [[Quirks_mode|Quirks mode]]（IE5模擬模式），<code>auto</code>不作用在除了表格元素之外的<code>margin</code>屬性上。
# <tt id="trident_transparent">transparent</tt> — 設<code>color</code>屬性為<code>transparent</code>則字會呈現為黑色。
# <tt>transparent</tt> — 7.0之前，不支援在邊框上的<code>transparent</code>（呈現為實心黑色），且在PNG圖像上被省略。

===取值與單位Gecko附註===
# <tt id="gecko_ch"><ch></tt> — 版本1.9.1之前，用「M」的[[字形|字形]]寬度 而非「0」的字形寬度。<ref group="g">{{citation |url=https://bugzilla.mozilla.org/show_bug.cgi?id=282126 |title=Bug 282126 - 長度單位「ch」要怎麼辦？（Mozilla專有擴張） |publisher=Mozilla}}</ref>

===取值與單位Presto附註===
# <tt id="presto_float"><number></tt> — 2.1之前，對於大於20.47的值曾有一個[[非交換幾何|量子化]]錯誤（不只是<tt>em</tt>，其他非像素單位也一樣）。<ref group="p">{{citation|url=http://www.brunildo.org/test/emarg.pl |title=Opera 7-9.2的「em」值的量子化錯誤 |archiveurl=https://web.archive.org/web/20080321205550/http://www.brunildo.org/test/emarg.pl |archivedate=2008-03-21 |deadurl=yes }}</ref>
# <tt id="presto_transparent">transparent</tt> — 當使用屬性 <tt>outline-color</tt>時此關鍵字會被忽略。版本2.2之前，同樣的情形也發生在屬性<tt>color</tt>及<tt>text-shadow</tt>。

== 一般附註 ==
=== 一般Trident附註 ===
# <code id="trident_-ms-">-ms-</code> — 所有實驗中的選取器、屬性、值都有「-ms-」作為前輟。例如：是<code>-ms-interpolation-mode</code>而不是<code>interpolation-mode</code>。

=== 一般Gecko附註===
# <code id="gecko_-moz-">-moz-</code> — 所有實驗中的選取器、屬性、值都有「-moz-」作為前輟。例如：是<code>::-moz-selection</code>而不是<code>::selection</code>。

=== 一般WebKit附註 ===
# <code id="webcore_-webkit-">-webkit-</code> — 所有實驗中的選取器、屬性、值都有「-webkit-」作為前輟。例如：是<code>-webkit-box-shadow</code>而不是<code>box-shadow</code>。

=== 一般KHTML附註===
# <code id="khtml_-khtml-">-khtml-</code> — 所有實驗中的選取器、屬性、值都有「-khtml-」作為前輟。例如：是<code>-khtml-opacity</code>而不是<code>opacity</code>。


=== 一般Presto附註===
# <code id="presto_-o-">-o-</code> — 所有實驗中的選取器、屬性、值都有「-o-」作為前輟。例如：是<code>-o-transition-property</code>而不是<code>transition-property</code>。
# <code id="presto_-xv-">-xv-</code> — 所有實驗中的《CSS3口說模組(@@翻譯)》選取器、屬性、值都有「-o-」作為前輟。例如：是<code>-xv-voice-rate</code>而不是<code>voice-rate</code>。


=== 瀏覽器自定樣式的DOM表現 ===
# 實驗中的CSS瀏覽器自定屬性的對照DOM屬性沒有連字號，且第一個字母為大寫。例如：<code>element.style.MozBorderRadius</code>對應於<code>-moz-border-radius</code>屬性、<code>element.style.OTransform</code>對應於<code>-o-transform</code>屬性。

== 參見 ==
=== 規格 ===
{{Reflist | group=spec | 2}}

=== Trident相關 ===
{{Reflist | group=t | 2}}

=== Gecko相關 ===
{{Reflist | group=g | 2}}

=== Webkit相關 ===
{{Reflist | group=w | 2}}

=== Presto相關 ===
{{Reflist | group=p | 2}}

=== Prince XML相關 ===
{{Reflist |group=r | 2}}
=== 其他參見 ===
{{Reflist | 2}}
{{Refbegin}}
* {{cite web | title=W3C | work=CSS 1 test suite | url=http://www.w3.org/Style/CSS/Test/CSS1/current/ | accessdate=May 1, 2005}}
* {{cite web | title=W3C | work=CSS 2.1 test suite | url=http://www.w3.org/Style/CSS/Test/CSS2.1/current/ | accessdate=May 1, 2005}}
* {{cite web | title=mozilla.org Bugzilla | work=Bug 281960 - [devmo] Mozilla CSS support chart | url=https://bugzilla.mozilla.org/show_bug.cgi?id=281960 | accessdate=July 13, 2005}}
* {{cite web | title=Mozilla Developer Center | work=Mozilla CSS support chart | url=http://developer.mozilla.org/en/docs/Mozilla_CSS_support_chart | accessdate=May 21, 2006}}
* {{cite web | title=Opera Documentation | work=Web Specifications Supported in Opera - CSS | url=http://www.opera.com/docs/specs/css/ | accessdate=May 1, 2005}}
* {{cite web | title=Internet & Web - Safari | work=CSS Support in Safari | url=http://developer.apple.com/internet/safari/safari_css.html | accessdate=July 13, 2005}}
* {{cite web | title=Konqueror Homepage | work=CSS 2.1 & 3 Support in KHTML 3.4 | url=http://www.konqueror.org/css/ | accessdate=July 13, 2005}}
* {{cite web | title=Apple Developer Connection | work=Safari CSS Reference | url=http://developer.apple.com/documentation/AppleApplications/Reference/SafariCSSRef/ | accessdate=July 14, 2005}}
* {{cite web | title=Prince XML | work=Release Changelog | url=http://www.princexml.com/releases/}}
* {{cite web | title=Prince XML| work=Unsupported CSS2.1 features | url=http://www.princexml.com/doc/6.0/css21/ }}
* {{cite web | title=Microsoft MSDN | work=CSS Compatibility and Internet Explorer | url=http://msdn.microsoft.com/en-us/library/cc351024(VS.85).aspx | accessdate=Sep 29, 2009}}
{{Refend}}

== 外部連結 ==
* [http://www.webdevout.net/browser-support-css WebDevout]——以視窗瀏覽器的臭蟲測試為主要導向。
* [http://caniuse.com/ Can I Use]——展示各大浏览器对HTML5、CSS3的支持程度。
* [http://css3test.com/ The CSS3 Test]——测试各大浏览器对CSS3的支持程度。
* [https://developer.mozilla.org/en-US/docs/Web/CSS Mozilla Developer Network上面的CSS相关资料]

[[Category:軟件比較|Category:軟件比較]]