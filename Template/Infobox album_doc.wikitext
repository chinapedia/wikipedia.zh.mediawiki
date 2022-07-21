{{documentation subpage|[[Template:Infobox album]]|[[Template:Infobox album/doc]]}}
{{High-use|7993}}
{{Lua|Module:Infobox|Module:InfoboxImage|Module:Check for unknown parameters}}
-{H|zh-hans:信息;zh-hant:資訊}--{H|zh-hans:信息框;zh-hant:資訊框;}--{H|zh-cn:数字;zh-tw:數位;zh-hk:數碼;}--{H|zh-hans:数据;zh-hant:資料;}--{H|zh-hans:链接;zh-hant:連結;}--{H|zh-hans:文件;zh-hant:檔案;}--{H|zh-cn:上传;zh-tw:上傳;zh-hk:上載;}--{H|zh-hans:文件名;zh-hant:檔案名字;}--{H|zh-cn:视频专辑;zh-tw:視訊專輯;zh-hk:視頻專輯;}-

{{Infobox album
| name       = 某張專輯
| type       = 專輯
| artist     = 某位藝術家
| cover      = Nocover.svg
| alt        = 基於「合理使用」原則，範例中使用示例圖片
| released   = {{Start date|2000|1|1}}
| format     = [[卡式錄音帶]]、[[CD]]
| recorded   = 2000年
| venue      = 
| studio     = 
| genre      = [[華語流行音樂]]
| length     = {{Duration|m=11|s=11}}
| label      = 某唱片公司
| producer   = 製作人A、製作人B、製作人C
| reviews    = 
| prev_title = 前作
| prev_year  = 1990
| next_title = 續作
| next_year  = 2010
}}

'''{{tl|Infobox album}}'''是音樂專輯條目使用的標準[[Wikipedia:格式手册/信息框|信息框]]，右邊的方框就是一個範例。您可以點擊「{{int:viewsource}}」，複製其中的代碼，並將其粘貼至您的條目中，將其中的內容更改為您要編寫的專輯資訊即可。

信息框代碼應放置在條目最頂端，頂註模板和消息框模板的底部。

== 代碼 ==
對於大多數條目而言，通常只需要填寫以下欄位即可（請參見「[[#高級用法|高級用法]]」以獲取完整的參數列表）。沒有資料的項目請保持空白不必刪除，並不會影響模板的使用。請注意，參數名稱區分大小寫。

<pre style="overflow:auto">
-{zh;zh-hans;zh-hant;|{{subst:Infobox album
| name       = 
| type       = 
| artist     = 
| cover      = 
| alt        = 
| released   = <!-- {{Start date|||}} -->
| format     = 
| recorded   = 
| venue      = 
| studio     = 
| genre      = <!-- 請勿添加無來源的音樂類型 -->
| length     = 
| label      = 
| producer   = 
| reviews    = 
| prev_title = 
| prev_year  = 
| next_title = 
| next_year  = 
}}
}-</pre>

== 說明 ==
嘗試盡可能多地填寫詳細資訊。如果某些資訊未知，請將該部分內容保持空白。請在適當的地方建立維基連結，但請務必檢查您的連結，並相應地修正其中的[[Wikipedia:消歧义|消歧義連結]]。

=== name ===
專輯名稱應使用文字標識，而不是徽標。

=== {{Anchors|顏色|類型與顏色}} type ===
{{para|type}}欄位指的是音樂專輯的總體類型。輸入下表中展示的代碼，該類型將以適當的顏色顯示。如果類型未知，則保持此欄空白即可。

{{Infobox album/doc/type}}

=== {{Anchor|專輯封面}} cover ===
此處應採用首版專輯的官方封面圖片。如果沒有首版，則可以使用再版版本的封面代替。

專輯封面圖片檔案可源於掃描，或從[http://www.allmusic.com Allmusic]、[http://www.amazon.com 亞馬遜網路書店]等網站下載。請注意，無論是從上述任何一種方式獲取的圖片檔案，在上傳時請務必使用適當的檔案名字，降低原图的[[解析度]]至300像素左右，並遵守[[Wikipedia:合理使用|合理使用方針]]。如果沒有適合的封面圖片，請將此欄設為<code>blank</code>。

如果此欄留空，則該條目將被自動添加至「[[:分类:损坏的宣传品图像的链接的页面]]」中。

=== alt ===
專輯封面的視覺替代文字，適用於有視覺障礙的讀者。參見「[[Wikipedia:圖像的替代文字|維基百科:圖像的替代文字]]」以獲取更多資訊。

=== released ===
請參照[[Wikipedia:格式手册/日期和数字#时间|日期格式手冊]]填入首版專輯的發行日期，可使用{{tl|Start date}}模板。

=== format ===
填入專輯的發行方式，例如[[黑膠唱片]]、[[CD]]、[[卡式錄音帶]]、[[數位音樂下載]]（註釋出渠道連結）等。通常情況下，再版版本的發行方式應當記錄於條目中。

=== recorded ===
填入歌曲的錄製時間。當有多個日期時，建議使用月份或月份範圍（例如：2016年1月－3月）進行總結。請於{{para|studio}}或{{para|venue}}欄位記錄錄音的地點。

=== studio ===
如果收錄的歌曲在'''錄音室'''錄製，請填入錄音室的名稱和位置，並為其建立維基連結，除非該錄音室位於不知名的國家、政區或城市（參見「[[WP:OVERLINK]]」以獲取更多資訊）。如果錄音室名稱中出現了「錄音室」或「Studios」字樣，請將它們從錄音室名稱中移除。例如「<nowiki>[[Sound City Studios|Sound City]]</nowiki>」，而不是「<nowiki>[[Sound City Studios]]</nowiki>」。

=== venue ===
對於'''現場錄製'''的音樂專輯，請填入場地名稱（如音樂廳、體育館等）和位置。適當時請建立連結。

=== genre ===
該欄位應填入最能描述總體風格的音樂類型，資料應當來自可靠來源，並於條目正文中說明和引用，請勿填入個人觀點或原創研究。內容應當建立連結。

=== length ===
專輯內容的長度應當以分鐘和秒為單位表示，長度超過一小時亦同，例如「74:23」。可使用{{tl|Duration}}模板。

請列出首版、標準版或最普遍版本專輯的時長。

=== label ===
此欄僅需填入最初發行專輯的[[唱片公司]]即可。如果該專輯在不同地區由不同的唱片公司負責發行，則應當記錄于正文的「發行歷史」小節下。請將其中的「唱片」或「Records」字樣移除（例如<code>{{nowrap|<nowiki>[[福茂唱片|福茂]]</nowiki>}}</code>，而不是<code>{{nowrap|<nowiki>[[福茂唱片]]</nowiki>}}</code>）。

=== producer ===
通常情況下，正文的曲目表中會列出全部收錄歌曲的'''[[音樂製作人|製作人]]'''名單，此處無需再次全部列出，僅需填入'''主要的'''製作人即可。

=== reviews ===
專業評分，僅用於向後兼容，請在新條目中以{{tl|Album ratings}}代替。

== 專輯年表 ==
填入該歌手已發行專輯的年表。

{{para|prev_title}}和{{para|prev_year}}應填入上一張專輯的名稱和發行年份。如果當前專輯是該歌手的處女作，則保持此欄空白即可。

{{para|next_title}}和{{para|next_year}}應填入下一張專輯的名稱和發行年份。如果當前專輯是該歌手的最新作品，則保持此欄空白即可。

== 高級用法 ==
{{Infobox album
| name          = 專輯A
| original_name = {{lang|en|''Album A''}}
| type          = 專輯
| artist        = 藝術家A、藝術家B
| cover         = Nocover.svg
| alt           = 基於「合理使用」原則，範例中使用示例圖片
| border        = yes
| caption       = 首版封面
| released      = {{Start date|2000|1|1}}
| format        = [[卡式錄音帶]]、[[CD]]
| recorded      = 2000年
| venue         = 
| studio        = 錄音室A
| genre         = [[流行 (音樂類型)|流行]]
| length        = {{Duration|m=11|s=11}}
| language      = 英語
| label         = 唱片公司A
| producer      = 制作人A、制作人B、制作人C
| reviews       = 
| chronology    = 藝人A
| prev_title    = 前作
| prev_year     = 1990
| next_title    = 續作
| next_year     = 2010
| misc          = 
 {{Extra chronology
 | artist       = 藝人B專輯
 | type         = 專輯
 | prev_title   = 前作
 | prev_year    = 1990
 | title        = 專輯A
 | year         = 2000
 | next_title   = 續作
 | next_year    = 2010
 }}
 {{Extra album cover
 | header  = 再版封面
 | type    = 專輯
 | cover   = Nocover.svg
 | alt     = 示例文字
 | border  = yes
 | caption = 再版封面
 }}
 {{Singles
 | name        = 專輯A
 | type        = 專輯
 | single1     = 曲目A
 | single1date =  
 | single2     = 曲目B
 | single2date = 
 }}
}}
在某些特殊情況下，可能會用到模板中的其他欄位，未被使用的欄位可保持空白或刪除。
<pre style="line-height:1.2em;">
-{zh;zh-hans;zh-hant;|{{subst:Infobox album
| name           = 
| original_name  = 
| type           = 
| longtype       = 
| artist         = 
| cover          = 
| border         = 
| alt            = 
| caption        = 
| released       = 
| format         = 
| recorded       = 
| venue          = 
| studio         = 
| genre          = 
| length         = 
| language       = <!-- 適用於非國語專輯 -->
| label          = 
| director       = 
| producer       = 
| compiler       = 
| reviews        = 
| chart_position = 
| certification  = 
| chronology     = 
| prev_title     = 
| prev_year      =
| year           = 
| next_title     = 
| next_year      = 
| misc           = 
}}
}-</pre>

=== original_name ===
中文專輯的官方英文名稱，或非中文專輯的原文名稱。根據[[Wikipedia:格式手册/亲和力|網頁親和力格式手冊]]，此欄建議使用{{tl|lang}}模板填寫。如果為拉丁字母文字，建議手動加註斜體標示。

=== longtype ===
附加的專輯類型資訊，例如原聲帶所指向的作品類型（電視劇、電影或電子遊戲）和名稱，或者致敬專輯的致敬對象，該項資訊顯示在{{para|type}}欄位的後方，建議手動加註括號標示。

=== border ===
將此欄設為「yes」可在封面圖片周圍添加寬度為1像素的灰色邊框，適用於封面圖片和背景混淆在一起的情況。

=== caption ===
如果專輯有不同版本的封面，則應在此處註明封面所指的版本。

=== language ===
請填入專輯的[[歌詞]]在演唱時所使用的[[語言]]，適當時請建立連結。例如，「<code>-{zh;zh-hans;zh-hant;|國語、粵語}-</code>」表示專輯的歌詞是國語和粵語，國語專輯可不必填寫。如果{{para|genre}}欄位中填入了包含語言資訊的音樂類型（例如「[[華語流行音樂]]」或「[[粵語流行音樂]]」），則此欄亦可不必填寫。

=== director ===
該欄位僅用於[[音樂錄影帶|視訊專輯]]，請填入條目中提及的導演姓名。

=== compiler ===
僅用於[[合輯]]，填入負責合輯的編選人。

=== chart_position ===
記錄在各主要排行榜的最高名次。

=== certification ===
填入認證銷量及認證單位。

=== chronology ===
填入歌手姓名，將顯示「（内容）專輯年表」。

=== misc ===
有許多可用在'''misc'''欄位的模板，例如{{tl|Extra album cover}}、{{tl|Extra chronology}}、{{tl|Singles}}和{{tl|Audiosample}}。

==== {{Anchor|Template:Extra chronology}} Template:Extra chronology ====
附加的專輯年表通常用于{{tsl|en|split album|合發專輯}}、合作專輯和專輯系列。
<pre style="overflow:auto">
{{Infobox album
...
| misc       = {{Extra chronology 
 | artist     = 
 | type       = 
 | prev_title = 
 | prev_year  = 
 | title      = 
 | year       = 
 | next_title = 
 | next_year  = 
 }}
}}
</pre>

==== {{Anchor|Template:Extra album cover}} Template:Extra album cover ====
如果该专辑在发行时有不同的专辑封面，可以使用此模板将它们添加到信息框中。然而，根据[[WP:NFCC#3]]，非自由内容的使用应是最小限度的，如果一个项目可以传达同等重要的信息，就不要使用。一个与原版有明显不同的、且被广泛传播的和/或取代原版的替代性封面通常被认为是符合这一标准的。此外，作为具体（来源）批评评论的主题的替代性封面也通过了列入标准。本质上相似但在颜色、设计、文字等方面存在差异的封面不应列入。
<pre style="overflow:auto">
-{zh;zh-hans;zh-hant;|{{Infobox album
...
| misc    = {{subst:Extra album cover
 | header  = 
 | type    = 專輯
 | cover   = 
 | border  = <!-- 選填參數，將此欄設為「yes」可在封面圖片周圍添加寬度為1像素的灰色邊框 -->
 | alt     = 
 | caption = 
}}
}}}-</pre>

==== Template:Singles ====
<pre style="overflow:auto">
{{Infobox album
...
| misc       = {{Singles
 | name        = 
 | type        = 
 | single1     = 
 | single1date = 
 | single2     = 
 | single2date = 
 | single3     = 
 | single3date = 
 | single4     = 
 | single4date = 
 }}
}}
</pre>

== 微格式 ==
{{UF-hcal}}

== 參見 ==
* {{tlx|Infobox song}}

<includeonly>{{sandbox other||
[[Category:音樂信息框模板|A]]
}}</includeonly>