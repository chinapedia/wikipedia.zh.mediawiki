<includeonly><!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{Documentation subpage}}</noinclude>
<!-- EDIT TEMPLATE DOCUMENTATION BELOW THIS LINE -->

== 關於本模板 ==
本模板是為了告知，在討論頁裡提出了關於條目內容的詢問或提案，而貼在條目文章的開頭用的模板。主要用於以下的情況。
* 在討論頁裡提出了詢問或提案，但過了一段時間後仍沒有回應。
* 對於在討論頁裡提出的詢問或提案，想早點得到意見的時候。
* 討論頁的議論停擺的時候。
* {{tl|seetalk}}、{{tl|参见讨论页}}重定向至此。

== 使用方法與範例 ==
在條目文章的開頭記述<code><nowiki>{{SeeTalk}}</nowiki></code>

=== 簡單的用法 ===
 <code><nowiki>{{</nowiki>SeeTalk|提案|更改分類如何}}</code>
會變成以下：
{{SeeTalk|提案|更改分類如何}}

=== 使用多個參數的方法 ===
 <code><nowiki>{{</nowiki>SeeTalk
  |notice-type=提案
  |notice-summary=關於本模板
  |section=關於模板
  |image=File:Nuvola apps edu languages.png
  |image-size=50px
 }}</code>
結果如下：
{{SeeTalk
  |notice-type=提案
  |notice-summary=關於本模板
  |section=關於模板
  |image=File:Nuvola apps edu languages.png
  |image-size=50px
 }}

=== 參數 ===
依指定的參數，能夠變更顯示內容。不指定任何參數時，將變成上面的形式。
;<code>notice-type</code>
:記述「詢問」「提案」等欲告知的類型。未指定時將顯示「詢問」。
;<code>notice-summary</code>
:記述投稿至討論頁內容的要旨。未指定時將不會顯示要旨。需要[[:Wikipedia:在討論頁上簽名|簽名]]時請在在要旨的最後加上<nowiki>~~~或~~~~</nowiki>。
;<code>section</code>
:鏈結目標有小節時，記述該小節名稱。不需要「#」。未指定時將被忽略。
;<code>image</code>
:指定要顯示的圖像。不需要<code>[[]]</code>（內部鏈結）。未指定時將顯示[[:File:Help-browser.svg]]。
;<code>image-size</code>
:指定圖像大小。未指定時預設為「40px」。

由於從上而下為 <nowiki>{{{1}}} 至 {{{5}}}</nowiki> 的參數，也能夠不指定參數名，像「[[#簡單的用法]]」一樣橫列式指定。「[[#使用多個參數的方法]]」也是同樣地，能夠用 <nowiki>{{SeeTalk|提案|關於本模板|關於模板|File:Nuvola apps edu languages.png|50px}}</nowiki> 的寫法。

== 提示與注意事項 ==
* 在討論頁想要告知的投稿項目有複數件的時候，可以不使用<code>section</code>而以<code>notice-summary</code>直接貼上目標各小節的內部鏈結來處理。
* 可以用來表示的圖像在[[commons:Category:Icons]]。
* '''依照投稿於討論頁的內容不同，可能有更適合的模板。'''這時候請使用該適切模板。詳細請看[[:Wikipedia:模板消息]]。
* '''詢問或提案解決後，請儘速將本模板除去。'''
<!--
* <code><nowiki>{{Seetalk}}</nowiki></code>、<code><nowiki>{{SeeNote}}</nowiki></code>、<code><nowiki>{{Seenote}}</nowiki></code>も同じ働きをしますが、これらは<code><nowiki>{{SeeTalk}}</nowiki></code>へのリダイレクトですのでなるべく<code><nowiki>{{SeeTalk}}</nowiki></code>を使用してください。
-->
<noinclude></noinclude>
<includeonly>
[[Category:頁面訊息模板|* SeeTalk]]
[[Category:維基百科討論]]
[[ja:Template:SeeTalk]]
</includeonly>