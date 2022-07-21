<noinclude>{{template doc page viewed directly}}</noinclude>
{{Twinkle standard installation}}
<!-- EDIT TEMPLATE DOCUMENTATION BELOW THIS LINE -->
{{high-use|61398}}

* 这个模板会将被标示的'''主名字空间'''（条目）页面置入[[:Category:缺少来源的条目]]的子分类中。
* 这个[[{{SITENAME}}:模板|模板]]是[[{{SITENAME}}:避免自我提及|自我提及]]，是维基计划的一部分，而非百科全书的内容，[[打印]]时不会出现。
* 这个模板无法[[Help:替换引用|替换引用]]。
* 这个模板在条目中的位置现在还没有一致的共识；可以将这个模板放在条目的最顶端或最底端，也可以是条目中某一节的顶端，还可以是条目的讨论页中。
* 这个模板是否应使用于[[{{SITENAME}}:小作品|小作品]]现在还没有一致的共识。从理论上讲，包括小作品在内的所有条目都应该列明来源；但意见在小作品上存在分歧：有人认为小作品的标记已能通知编辑者改善其条目，也有人认为需要通过本标记作出进一步的通知。<!--参见英文维基上的投票-->

==用法==
{{tl|Unreferenced}}使用于完全没有来源的条目。另一个模板{{tl|Refimprove}}适用于那些来源不充足的条目。

*使用时，需要为模板指定时间参数。
**您可以从此处复制当前的时间：
***<code><nowiki>{{Unreferenced |time=</nowiki>{{#time:c}} }}</code>
**或者使用[[help:替换引用|替换引用]]功能：
***<code><nowiki>{{Unreferenced |time={{subst:#time:c}}</nowiki> }}</code>
**甚至您还可以使用：
***{{tls|Unreferenced/auto}}
**加上时间参数可以让条目被分入[[:Category:缺少来源的条目]]的子分类中，这样有助于编辑者区分出较早的问题以优先解决。未加时间参数会让条目被归类到[[:Category:模板参数错误的页面]]中去。

*这个模板还有一些可选择的参数，允许使用者表明哪部分内容需要述及来源。作为一项建议，当整篇条目都需要列明来源时，使用者可以输入<code><nowiki>{{unreferenced}}</nowiki></code>；如果使用者需要为文章中的特定章节请求来源时，使用者可以输入<code><nowiki>{{unreferenced|条目中的“儿童”一节}}</nowiki></code>或使用{{tlg|Unreferenced section}}。

==重定向==
*{{tl|需要來源}}
*{{tl|缺乏来源}}
*{{tl|沒有來源}}
*{{tl|No references}}
*{{tl|Noref}}
*{{tl|Unref}}
*{{tl|Unsourced}}
**使用提示：不同於 {{tl|請求來源}}。

==参见==
* {{tl|Citation needed}}（{{tl|来源请求}}）：对应的内文维护模板
*下列的模板应当在条目内已具有'''一些'''来源的时候使用，所以'''这些模板不能用于标注没有来源的条目'''：
** {{tl|Unreferencedsect}}：用於某一段落或章節沒有參考來源。
** {{tl|Refimprove}}：用於需要補充一些參考或來源。
** {{tl|Verify}}：雖有來源，但是其真實性受到懷疑而需要查證。
** {{tl|Primarysources}}：條目过于依赖第一手來源，需要可靠、公開、第三方的參考來源。
** {{tl|No footnotes}}：条目包含参考来源或外部链接，但缺少內文脚注。
** {{tl|Citation style}}：參考資料需要進行清理，以符合正確的引用、腳注或外部連結格式。
** {{tl|BLPsources}}：在世人物需补充参考文献的条目。
** {{tl|Verify source}}：需要查證的文字。
*相關模板列表：
** [[Wikipedia:模板消息/条目来源]]
***{{tl|BLP unsourced}}：在世人物未有列出任何參考文獻的條目
** [[Wikipedia:模板消息/清理]]

{{Citation and verifiability article maintenance templates}}
<includeonly>
<!-- ADD CATEGORIES BELOW THIS LINE -->
[[Category:引用與查證維護模板|{{PAGENAME}}]]
</includeonly>