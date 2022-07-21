{{NoteTA
|G1 = IT
|G2 = MediaWiki
}}
{{Documentation subpage}}
{{High-risk|178790}}
{{lua|Module:Message box}}
{{Mbox templates}}
<!-- 在本行下編輯模板說明 -->
本模板 '''{{tl|ambox}}''' 是條目訊息框的元模板。用於創造文章訊息框模板，如 {{tl|wikify}} 等。此外本模板具有自由選擇不同顏色、顯示特定預設圖片等功能。

'''请注意：'''这个模板只用于在条目名字空间使用的模板，其他名字空间使用的模板请不要使用。

== 常用参数 ==
右側的方框內為 {{tl|ambox}} 模板最常用的參數。每種參數的說明如下：
{| class="wikitable" align="right" style="background:transparent;" width="40%" 
! 常用參數
|-
|<pre style="font-size:90%; ">
{{Ambox
| name  = 
| subst = <includeonly>{{subst:substcheck}}</includeonly>
| small = {{{small|}}}
| type  = 
| image = 
| sect  = {{{1|}}}
| issue = 
| talk  = {{{talk|}}}
| fix   = 
| date  = {{{date|}}}
| time  = {{{time|}}}
| cat   = 
| all   = 
}}
</pre>
|}

=== ''name'' ===
''name'' 参数指定模板的名字，不需要加上模板名字空间前缀。例如 {{tl|Wikify}} 中填入的參數為 {{para|name|Wikify}}。

本參數應該模板被移動時更新。本參數的指定有兩個目的：
* 如果模板被錯誤的替換引用（substituded），這個參數能讓元模板顯示一段警告文字，將可幫助編輯者修復問題。
* 能讓模板在模板頁中更有效地展示，例如在沒有填入日期的情況下自動顯示日期，並能讓模板準確分類。

=== ''subst'' ===
''subst'' 参数讓元模板能检测此模板是否被错误替代引用的，并顯示一段警告文字。同时也会将页面加入 [[:Category:錯誤使用替換引用的頁面]] 分类. 完全复制上述方框中的代码即可。一般情況下，請勿更改本參數內容，直接複製上方的模板代碼即可。

=== ''small'' ===
''small'' 参數可讓編輯者在條目中使用模板時輸入 {{para|small|left}} 來產生一個小型的模板。

{{ambox|nocat=true|small=left|text=這是一個靠左顯示的小型模板。}}

一般情況下本模板的顯示效果如下：

{{ambox|nocat=true|text=這是一個標準的訊息框格式。}}

其他參數設定方式：
* 如果模板「永遠」不應以縮小的方式顯示，請在模板原始碼中使用 {{para|small|no}}。
* 如果模板應「總是」以縮小的方式顯示，請在模板原始碼中使用 {{para|small|left}}。
* 如果模板「預設為縮小顯示」，請在模板原始碼中使用 {{para|small|<nowiki>{{{small|left}}}</nowiki>}}。可讓編輯者在條目中輸入 {{para|small|no}} 參數時無效。

=== ''type'' ===
''type'' 参数能指定的模板預設的左侧直條顏色和图片。本參數的選擇並非依據編輯者對顏色的偏好，而是根據模板內訊息的類型來決定。以下是七種可在「<code>type</code>」參數中填入的值：

{{ambox
| type  = speedy
| text  = type=<u>speedy</u>－请求快速刪除，如 {{tl|delete}}。
}}
{{ambox
| type  = delete
| text  = type=<u>delete</u>－请求删除，如 {{tl|afd}} 与 {{tl|vfd}} 。
}}
{{ambox
| type  = content
| text  = type=<u>content</u>－内容问题，如 {{tl|POV}} 与 {{tl|globalize}} 。
}}
{{ambox
| type  = style
| text  = type=<u>style</u>－格式问题，如 {{tl|cleanup}} 与 {{tl|wikify}}。 
}}
{{ambox
| type  = move
| text  = type=<u>move</u>－合并、拆分及跨维基提议，如 {{tl|split}} 与 {{tl|splitsection}}。
}}
{{ambox
| type  = protection
| text  = type=<u>protection</u>－页面保护，如 {{tl|Protected}}。
}}
{{ambox
| type  = notice
| text  = type=<u>notice</u>－条目注意，如 {{tl|current}} 与 {{tl|inuse}}。 
}}

如果没有指定 ''type'' 参数，默认为 {{para|type|notice}}。

=== ''image'' ===
您可以使用 ''image'' 參數來指定模板中顯示的圖片。圖片的指定語法與維基百科放置圖片的預設語法相同（參見：[[Help:图像|如何放置圖片]]）。一般來說，圖片的寬度約為 40-50px。範例如下：

* {{tl|POV}} 中參數設定為 {{para|image|<nowiki>[[File:Unbalanced scales.svg|40px|link=|alt=]]</nowiki>}}，其顯示效果如下：
{{POV|time={{#time:c}}|nocat=true}}

* {{tl|wikify}} 中參數設定為 {{para|image|<nowiki>[[File:Wikitext.svg|50px|link=|alt=]]</nowiki>}}，其顯示效果如下：
{{Wikify|time={{#time:c}}|nocat=true}}

請注意：
* 如果沒有指定圖片，模板將會配合「type」參數的內容選擇適當的圖片（參見：[[#type]]）
* 如果參數設定為 {{para|image|none}} 時將不會顯示任何圖片，訊息框內將僅顯示文字。
* 如果圖片僅為裝飾功能，並屬於[[公共领域]]，可如在參數中加上 "{{para|link}}'' 以產生連往圖片描述頁的連結，以及 ''{{para|alt}}" 來產生替代文字；以上兩種做法可提升[[Wikipedia:格式手冊/親和力|頁面親和力]]。

=== ''sect'' ===
许多条目訊息模板开头文字为「'''此条目⋯⋯'''」，如果此模板用于章节，则应该更适当地使用「'''此章节⋯⋯'''」。其他可能性包括「'''此列表⋯⋯'''」和「'''此人物傳記⋯⋯'''」。

为了实现这个功能。请使用 {{para|sect|<nowiki>{{{1|}}}</nowiki>}} 參數。這將使編輯者能在第一個無名的參數中輸入「'''章節''''」來改變模板所指的條目部分。例如：{{tlx|Advert|章节}} 將會顯示：
{{Advert|章节|time={{#time:c}}}}

在使用这个功能時，在模板原始碼中应移除开头的几个字（例如：本条目），否则会造成重复显示。

=== ''issue'' & ''fix'' ===
''issue'' 参数用于描述条目的问题。請儘量保持文字敘述簡潔有力（約在 10-20 個字內），並包含一個連結至有關的[[Wikipedia:方針與指引|方針與指引]]頁面。

''fix'' 参数包含描述如何改进条目的指导文字。文字內容可比 ''issue'' 參數中所填入的字數多，在大多數情況下，請保持在兩句話內敘述完畢。

當模板以整合狀態（例如放置在 {{tl|multiple issues}} 中）或小型狀態（使用 {{para|small|left}} 參數）顯示時，只有 ''issue'' 參數中的文字會顯示。例如在 {{tl|citation style}} 模板中的參數設定為：

* <code>|issue = <nowiki>本條目的'''引用需要进行清理。'''</nowiki></code>
* <code>| fix = <nowiki>参考文献应符合正确的[[Wikipedia:列明来源|引用]]、[[Wikipedia:脚注|脚注]]及[[Wikipedia:外部链接|外部链接]]格式。</nowiki></code>

當單獨使用時顯示效果如下：
{{Citation style}}

但當與 {{tl|article issues}} 模板整合使用或以小型模式（{{para|small|left}}）顯示時，效果則如下：
{{Multiple issues <!-- Even though there's only one "issue", please don't remove this {{Multiple issues}} template. It is a demonstration of the formatting. --> |{{Citation style}}}}
{{Citation style|small=left}}

=== ''talk'' ===
某些條目訊息框模板包含了一個通往其討論頁的連結，並讓編輯者能指定相關議題所在的章節位置。如要達成這項功能，請使用 ''talk'' 參數，使用方式為 {{para|talk|<nowiki>{{{talk|}}}</nowiki>}}。

這項參數將可被編輯者以下述方式使用：
* {{para|talk|章節標題}} - 連結可通往條目討論頁中的特定章節。例如：{{para|talk|西瓜}}
* {{para|talk|完整頁面名稱}} - 連結將通往指定的頁面。例如：{{para|talk|Talk:香蕉#西瓜}}

請注意：
* 當模板中使用本參數時，模板本身將會顯示一個通往討論頁的連結（為了顯示支援此功能），但僅有在參數被確實定義時才會在條目中的模板內顯示。
* 如果要讓模板永遠顯示一個通往討論頁的連結，請使用 {{para|talk|<nowiki>{{{talk|#}}}</nowiki>}} 參數。
* 如果討論頁面不存在，無論參數設定為何，都將不會顯示任何連結。

=== ''date'' ===
將 ''date'' 直接傳送至元模板可讓編輯者（或[[WP:bot|機器人]]）自行輸入模板被放置在條目中的日期。日期將會以較小的字體在主要文字後顯示。

在 ''cat'' 參數同時獲得定義時，將 ''date'' 參數傳送至元模板可實現將條目自動[[:Category:按月分类的维基百科维护分类|按月分類]]的功能。
=== ''time'' ===
''time''和''date''用法差不多，但是time可以配合<nowiki>{{#time:c}}</nowiki>，例如：

<nowiki>{{ambox|issue=内容|fix=附加文字|date={{subst:#time:c}}}}</nowiki>会显示为：{{ambox|issue=内容|fix=附加文字|date={{#time:c}}}}

<nowiki>{{ambox|issue=内容|fix=附加文字|time={{subst:#time:c}}}}</nowiki>会显示为：{{ambox|issue=内容|fix=附加文字|time={{#time:c}}}}

=== ''cat'' ===
這個參數定義了清理分類的名稱。使用 {{para|cat|CATEGORY}} 參數：

* 並同時使用 {{para|date|DATE}}，則條目會被自動分類至 '''Category:自DATE起CATEGORY''' 中。
* 若無指定日期，條目會被自動分類至 '''Category:CATEGORY''' 中。

=== ''all'' ===
''all'' 參數可用來指定所有包含模板之條目的分類。

== 其他參數 ==
右側方框內展示了此模版的所有參數。由於幾乎不可能同時用到所有參數，因此不建議複製此處的空白模版。
{| class="wikitable" align="right" style="background:transparent; width=40%" 
!完整的所有參數
|-
|<pre style="font-size:90%; width=40%">
{{Ambox
| name        = 
| subst       = <includeonly>{{subst:substcheck}}</includeonly>
| small       = {{{small|}}}
| type        = 
| image       = 
| imageright  = 
| smallimage  = 
| smallimageright = 
| class       = 
| style       = 
| textstyle   = 
| sect        = {{{1|}}}
| issue       = 
| talk        = {{{talk|}}}
| fix         = 
| date        = {{{date|}}}
| time        = {{{time|}}}
| text        = 
| smalltext   = 
| cat         = 
| all         = 
| cat2        = 
| all2        = 
| cat3        = 
| all3        = 
}}<noinclude>
{{Documentation}}
</noinclude>
</pre>
|}

=== ''imageright'' ===
在訊息框右側顯示圖片。填入方式與 ''image'' 參數相同，預設為不顯示任何圖片。

=== ''smallimage'' & ''smallimageright'' ===
可在此參數指定模板縮小顯示後所使用的圖片。僅在定義 {{para|small|left}} 時有效。

=== ''class'' ===
可自行定义使用在訊息框的[[Cascading Style Sheets|CSS]]型別選擇器（Class）。

=== ''style'' & ''textstyle'' ===
可選擇定義CSS樣式，不需加上引號 <code>" "</code>，但必須在結尾加上分號 <code>;</code>。
* ''style'' 為套用至整個訊息框的樣式
* ''textstyle'' 為僅套用在文字上的樣式

=== ''text'' & ''smalltext'' ===
除了指定 ''issue'' 和 ''fix'' 參數外，也可使用 ''text'' 參數來定義要顯示的文字（不建议使用''text''，不支持移动版）

''smalltext'' 則用來定義要以較小字體顯示的文字

=== 其他分類相關參數 ===
* ''cat2'' 和 ''cat3'' 可增加按月分類時所用的分類名稱，用法與 ''[[#cat]]'' 參數相同。
* ''all2'' 和 ''all3'' 可增加所有包含模板之條目的分類名稱，用法與 ''[[#all]]'' 參數相同。

== 技術細節 ==
如果你需要在text参数中使用一些特殊字符的话，那么就需要像这样将它们换码：

<pre>
{{ambox
| text  = 
等号 = 与前后大括号{ }可以正常地使用。
但是管道符{{!}}与两个连着的后大括号<nowiki><nowiki>}}</nowiki></nowiki>则不能直接使用。
一起用同样要带nowiki标记<nowiki><nowiki>|}}</nowiki></nowiki>。
}}
</pre>

{{ambox
| text  = 
等号 = 与前后大括号{ }可以正常地使用。
但是管道符{{!}}与两个连着的后大括号<nowiki>}}</nowiki>则不能直接使用。
一起用同样要带nowiki标记<nowiki>|}}</nowiki>。
}}

此模板使用CSS类来确定显示风格，因此可被更换到其他风格。

在此元模板内使用了HTML的表格标示法，而没有使用维基式的表格标示法。在制作元模板时这是一个常见的方法，因为维基式标示法存在一些缺陷。譬如，维基式标示法会加大[[Help:模板扩展语法|模板扩展语法]]及参数中特殊字符使用的难度。

此元模板所用的缺省图片用的是png格式的，而不是svg格式。其主要原因是在处理MediaWiki为svg图片所渲染的透明背景时，一些老版本的网络浏览器会遇到一些麻烦。这里的png格式图片有手工优化过的透明背景颜色，因而在所有的浏览器中它们看上去都是好的。请注意，svg图标只会在一些老版本的浏览器中看上去有点不对头，因此只有那些非常广泛使用的图标才值得费些功夫去做那种手工优化。

更多的技术细节参见[[{{TALKPAGENAME}}|讨论页]]以及下方的[[#參見]]一节。

== 參見 ==
其他屬於 {{tl|mbox}} 家族的系列模板：
* {{tl|ambox}} – 用于条目消息框。
* {{tl|tmbox}} – 用于讨论页消息框。
* {{tl|imbox}} – 用于图像页消息框。
* {{tl|cmbox}} – 用于分类消息框。
* {{tl|ombox}} – 用于其他页面消息框。
* {{tl|fmbox}} – 用于页眉和页脚消息框。
* {{tl|mbox}} – 有名字空间探测功能。某些消息框会用在几类页面并因此需要依据所用在的页面来改变风格，这种情况下的消息框可以用此元模板。

其他页面：
<!--* [[Wikipedia:条目消息框的型別選擇器]]－描述如何在[[Help:表格|维基表格]]和HTML表格中直接使用条目消息框的CSS型別選擇器（CSS Class）。-->
* [[Wikipedia:条目消息框]]－（提議中）创建条目消息框时应遵循的格式指引。
* [[Wikipedia talk:条目消息框]]－讨论相关的事宜。

<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:維基百科元模板|Ambox]]
[[Category:條目訊息模板|Ambox]]
}}</includeonly>