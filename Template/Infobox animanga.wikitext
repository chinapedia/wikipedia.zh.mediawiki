<noinclude>{{pp-protected|small=yes}}</noinclude>
{{請注意|若對模板結構或參數內容有修改的建議，'''請先至[[{{TALKPAGENAME}}|討論頁]]提出'''。}}
{{TOCright}}
{{clearright}}
此模板是為了能夠將[[電視動畫]]、[[OVA]]、[[漫畫]]、[[電子遊戲]]、[[小說]]、[[廣播劇]]、[[電視劇]]、[[電影]]等各種媒體作品與其他關連項目合併在單一個Infobox中處理所設計的。

完整範例請見[[#記載例與表示例|本頁底部]]，模板示範條目：
* [[秋櫻之空]]
* [[涼宮春日的憂鬱]]

== 模板的構成 ==
;Header與Footer
模板的開頭和最後'''必須'''使用。
* [[:Template:Infobox animanga/Headerofja]]
* [[:Template:Infobox animanga/Footerofja]]
也能夠利用沒有內容物的基本Header。或在和ACG關係疏遠的條目使用純結束表格的Footer。
* [[:Template:Infobox animanga/Header2]]
* [[:Template:Infobox animanga/Footer]]

;name譯名元件
非必須元件。用來整合表示翻譯名稱。
* [[:Template:Infobox animanga/name]]

;各媒體的構成元件
以下是各媒體的模組式構成元件
* [[:Template:Infobox animanga/TVAnime]] - 電視動畫（TVA）
* [[:Template:Infobox animanga/OVA]] - OVA
* [[:Template:Infobox animanga/Manga]] - 漫畫
* [[:Template:Infobox animanga/Game]] - 電子遊戲（Computer Game）
* [[:Template:Infobox animanga/Novel]] - 小說
* [[:Template:Infobox animanga/RadioDrama]] - 廣播劇
* [[:Template:Infobox animanga/TVDrama]] - 電視劇
* [[:Template:Infobox animanga/Radio]] - 廣播
* [[:Template:Infobox animanga/Movie]] - 電影
* [[:Template:Infobox animanga/Cast]] - 卡司
* [[:Template:Infobox animanga/Other]] - 其他
* [[:Template:Infobox animanga/Other2]] - 其他2
如改編多次致段落過長，可使用以下模組摺疊部分段落
* [[:Template:Infobox animanga/MediaMix]] - 模板摺疊Header
* [[:Template:Infobox animanga/MediaMixFooter]] - 模板摺疊Footer
另外还有一个专用于[[世界名作剧场]]的構成元件
* [[:Template:Infobox_animanga/世界名作劇場]]

== 使用方法 ==
*本Infobox，由Header與Footer之間插入一個以上的模組來構成。要將構成元件配置在Infobox的哪個位置交給使用者自行判斷。為了確保整合性，推薦採用媒體頒佈的順序。（例如，涼宮春日：小說→TVA→漫畫）

*為了避免複數國家/語言的記載招致混亂，只有單一國家時應統一使用該地區的發售日期與貨幣等內容。兩個國家以上時建議以原作國家優先記載。
** 一般情況下記述作品名稱時，僅使用[[#Header|Headerofja]]模組即可。
** 作品譯名繁雜時，推薦追加使用[[#翻譯名稱|name]]模組補充詳細資料。
*為了統一性質，Infobox應該置於關連的主題裡。比方說電視動畫與電影存在著不同的條目，電影的構成元件不應該置於電視動畫的條目裡，反之亦然。要提供作品間鏈結的話，使用「Other」是個不錯的選擇。
*各模組中的''標題''參數是屬於'''自由選擇'''填入與否，想要在各個Infobox的頂部表示出不同媒體作品的特定標題時應該採用。不需要填寫時可以省略''標題''參數。
*關於各項構成元件的參數，請參照以下的說明。其中被註明'''「參數名=（必須輸入）」的是必要項目請一定要填寫。'''
*請在「版權／Copyright」欄填入版權持有者名稱（除了「(C)」以外的部分）。
*和譯名有直接關係的動畫、影劇代理及發行商請放在「代理發行」欄位。「其他代理發行」用於歐美等國家。
*和譯名有直接關係的出版社請放在「出版社」欄位。「其他出版社」用於歐美等國家。
*「網路」欄位包括[[網路電視]]、[[寬頻電視]]等。
*相關授權資訊，可搭配{{tl|Licensee‎}}使用。

=== Header ===
請'''一定要'''放在Infobox的開頭。
{| 
|<small><pre>
{{Infobox animanga/Headerofja
|title= 
|image= 
|size= 
|caption= 
|japanese= 
|english= 
|kana= 
|romaji= 
|genre= 
}}</pre></small>
|<small><pre>

標題
圖像
尺寸
說明
日文名稱
英文名稱
假名
羅馬字
類型

</pre></small>
|<small><pre>

第一順位的中文名稱
圖片的檔名xxx.yyy
建議設定在200px～300px之間
圖片解說
作品日文名稱
作品英文名稱
日文名稱的假名標示
日文名稱的羅馬字標示
校園喜劇科幻、冒險遊戲漫畫 等…

</pre></small>
|}
圖像預設大小為200px，建議設定在200px～300px之間，縱長圖像如書籍封面不需填寫（保持預設寬度）。當小於200px的情況時應當註明「圖像尺寸」。除標題以外均為選填。

為了記述的方便性與排版美觀，本模組已設定<nowiki><span lang="ja"></span></nowiki>。'''「日文名稱」與「假名」欄位請省略語言標記'''。

「日文名稱」和「英文名稱」應該'''只有一個'''。對於非英語名稱，可以使用語言標示模板註明，例如：[[魔女獵人]]的<nowiki>{{lang|es|El Cazador de la Bruja}}</nowiki>。

上兩項參數都不會顯示輸入文字以外的敘述，因此非日本作品時省略日文名稱，原名非英文者將名稱填入英文名稱並加上語言標記即可。

=== Header2 ===
這是裡面包含著啟始表格用的wikicode，沒有其他內容的Header。
<pre>
{{Infobox animanga/Header2}}
</pre>

=== Footer ===
請'''一定要'''放在Infobox的最尾端。
<pre>
{{Infobox animanga/Footerofja}}
</pre>

特殊情況： <nowiki>{{Infobox animanga/Footer}}</nowiki> 單純只有結束表格作用，在無關ACG條目利用部分模組整理訊息時可以考慮使用。

=== 翻譯名稱 ===
建議統一用於Headerofja或Header2底下。詳見[[#翻譯名稱模組使用範例|底下範例]]
{| 
|<small><pre>
{{Infobox animanga/name
|original= 
|official= 
|formal= 
|common= 
}}</pre></small>
|<small><pre>

作品原名
官方譯名
正式譯名
常用譯名

</pre></small>
|<small><pre>

使用完整原文名稱，通常在Header處填寫即可
著作權持有者訂定或認可的中文名稱
獲得授權出版、播放或發行的作品翻譯名稱
上述以外來源的常用譯名

</pre></small>
|}
由於一般作品鮮少有官方譯名，該對應欄位請留空或刪除；未有正式譯名而僅有常用譯名時，請於正式譯名處填入「無」。詳細說明見[[維基專題:ACG#譯名命名規則|譯名命名規則]]。

=== 電視動畫 ===
{| 
|<small><pre>
{{Infobox animanga/TVAnime
|標題= 
|圖像= 
|原案= 
|原作= 
|總導演= 
|導演= 
|劇本統籌= 
|編劇= 
|人物原案=
|人物設定= 
|機械設定= 
|音樂= 
|音樂製作= 
|動畫製作= 
|製作= 
|代理發行= 
|其他代理發行= 
|播放電視台= （必須輸入）
|其他電視台= 
|播放開始= （必須輸入）
|播放結束= 
|預定播放= （與「播放開始」二選一）
|網路= （網路首播時填入）
|話數= 
|其他= 
|版權= 
}}</pre></small>
|<small><pre>

電視動畫專有標題
圖片的檔名xxx.yyy
原案
原作所有者
總導演
動畫導演
系列構成
劇本、腳本
#キャラクター原案
キャラクターデザイン
#メカニックデザイン
#
音樂製作公司
動畫公司、工作室
作品製作者
代理發行商
他國代理發行商
電視台
記載多國電視台時使用
首映開始日期
首映結束日期，空白時顯示「播放中」
預定播放之日期或年份
#
播放總集數
備註
版權資訊

</pre></small>
|}
請在''動畫製作''欄填入動畫製作公司。請在''製作''欄填入作品的製作委員會等。

請在'''播放開始'''與'''播放結束'''欄填入主要播放電視台（日本稱為[[:ja:キー局|{{lang|ja|キー局}}]]：[[核心局]]）的播出日程表。如果{{lang|ja|キー局}}不存在的話,請填入最先開始播出此作品之電視台的播出日程表。

和譯名有直接關係的電視台請放在'''播放電視台'''欄位。

=== OVA ===
{| 
|<small><pre>
{{Infobox animanga/OVA
|ONA= 
|標題= 
|原案= 
|原作= 
|總導演= 
|導演= 
|系列構成= 
|劇本= 
|人物原案= 
|人物設定= 
|機械設定= 
|音樂= 
|音樂製作= 
|動畫製作= 
|製作= 
|書籍= 
|出版商= 
|代理發行= 
|其他代理發行=
|網路= （網路首播時填入）
|發售日= 
|開始= 
|結束= 
|上映日期= 
|話數= 
|票房= 
|其他= 
|版權= 
}}</pre></small>
|<small><pre>

設定為原創網絡動畫
OVA專有標題
原案
#原作所有者
總監督
動畫監督
シリーズ構成
#編劇
#キャラクター原案
キャラクターデザイン
メカニックデザイン
#
#音樂製作公司
動畫公司、工作室
作品製作者


代理發行商
他國代理發行商

OVA發售日
首卷發行日期
終卷發行日期
劇場先行上映日期
作品總話數
劇場先行上映票房
備註
版權資訊

</pre></small>
|}

=== 漫畫 ===
{| 
|<small><pre>
{{Infobox animanga/Manga
|標題= 
|作者= 
|作畫= 
|出版社= 
|其他出版社= 
|連載雜誌= 
|label= 
|網路= 
|發售日= 
|開始= 
|結束= 
|開始日= 
|結束日= 
|冊數= 
|話數= 
|其他= 
|版權=
}}</pre></small>
|<small><pre>

漫畫專有標題
漫畫創作者或原作者
有原作者時的漫畫家
原文及中文的單行本出版商
記載其他國家出版社時使用
作品刊載雜誌名稱
叢書（レーベル）
作品刊載網站（網路連載時填入）
單行本發售日期
開始刊載雜誌期號
結束刊載雜誌期號，空白時顯示「連載中」
連載開始日期
連載結束日期，空白時顯示「連載中」
單行本數量
總回數
備註
版權資訊

</pre></small>
|}
''連載雜誌''是漫畫被刊載的雜誌名稱。當作品在雜誌以外的媒體上連載時，也可以用「'''連載於'''」參數替代。'''開始'''與'''結束'''分別填寫連載開始、結束的日期。'''發行日'''主要是構想於全1卷的作品，必要時可以和開始、結束來分開使用。

若是故事與作畫由不同人負責，可以利用''作畫''參數。這時候''作者''參數則填寫原作者（負責故事的人）。'''填寫到作畫欄位的話，作者參數的表示會變成「原作」。'''故事與作畫為同一個人時，請不要在''作畫''欄位填入任何資料。

另外，原作與作畫欄位包括不下、需要記載複數人物時，使用以下的改行標籤。
<pre><nowiki>|作者=山田太郎（人物原案）<br />鈴木花子（漫畫）</nowiki></pre>

=== 電子遊戲 ===
只有街機的遊戲可以考慮使用{{tl|Infobox VG}}
{|
| <small><pre>
{{Infobox animanga/Game
|標題=
|類型=
|使用平台=
|遊戲引擎=
|開發團隊=
|代理商=
|製作人=
|監製=
|腳本=
|程式=
|音樂=
|美術=
|遊戲人數=
|發售日=
|對象年齡=
|結局數=
}}</pre></small>
| <small><pre>

遊戲標題
動作、冒險、模擬 等
遊戲主機名稱 或 Windows 等平台
電腦遊戲用
遊戲製作廠商（開發元）
代理發行廠商（發賣元）
Producer（プロデューサー）
Director（ディレクター）
劇本、編劇
主程式員
音樂製作者
藝術總監，原畫或角色設定
單人或多人
遊戲發售日期
GAL游戏分级，一般游戏不适用
總結局數

</pre></small>
|}

=== 小說 ===
{| 
|<small><pre>
{{Infobox animanga/Novel
|輕小說= 
|標題= 
|原作=
|作者= （必須輸入）
|插圖= 
|出版社= （必須輸入）
|其他出版社= 
|連載雜誌= 
|label= 
|網路= （網路連載時填入）
|發售日= 
|開始= 
|結束= 
|冊數= 
|話數= 
|其他= 
|版權=
}}</pre></small>
|<small><pre>

見下
小說標題

著作者
插畫畫家
原文及中文的小說出版商
記載其他國家出版社時使用
作品刊載雜誌名稱
作品刊載文庫名稱

見下
（連載）開始日期
（連載）結束日期，空白時顯示「連載中」
單行本數量
總回數
備註
版權資訊

</pre></small>
|}
如果作品屬於[[輕小說]]，請在'''輕小說'''欄位裡填入「是」即可。該欄位可刪除。

'''發售日'''主要針對全1卷的作品。依需要可以跟開始・結束分開運用。

=== 廣播劇 ===
{| 
|<small><pre>
{{Infobox animanga/RadioDrama
|媒體= 
|標題= 
|製作= 
|腳本= 
|演出= 
|廣播電台= 
|節目名稱= 
|書籍= 
|出版商= 
|代理商= 
|label= 
|發售日= 
|開始= 
|結束= 
|售價= 
|銷售數量= 
|收聽率= 
|收錄時間= 
|話數= 
|枚數= 
|其他= 
|版權=
}}</pre></small>
|<small><pre>

　
廣播劇標題
製作者
劇本
　
播放電台頻道
　
　
出版廠商
代理廠商
廣播劇CD的發行唱片公司/品牌
　
首卷發行日期
末卷發行日期
銷售定價
銷售量記錄
　
　
　
CD張數
備註
版權資訊

</pre></small>
|}
''媒體''是在更改標題的媒體表示部分時使用，如廣播劇CD之類等。'''省略時會顯示「廣播劇」。'''''書籍''用於如果是雜誌附附錄之類的廣播劇的情況，記載該書籍名稱。

=== 電視劇 ===
{| 
|<small><pre>
{{Infobox animanga/TVDrama
|標題= 
|導演= （必須輸入）
|製作= （必須輸入）
|代理發行= 
|其他代理發行=
|播放電視台= （必須輸入）
|播放開始= （必須輸入）
|播放結束= 
|話數= 
|其他= 
|版權=
}}</pre></small>
|<small><pre>

電視劇標題

製作單位（公司）
代理發行商　
他國代理發行商

首映開始日期
首映結束日期
播放總回數
備註
版權資訊

</pre></small>
|}

=== 廣播 ===
{| 
|<small><pre>
{{Infobox animanga/Radio
|網路=（僅網路廣播需要填入）
|標題=
|暱稱=
|主持人=
|DJ=
|助手=
|節目文案=
|導播=
|製作人=
|混音師=
|腳本=
|演出=
|其他製作人員=
|播放開始=（必須輸入）
|播放結束=
|廣播電台=（必須輸入）
|播放時間=
|播放次數=
|播放形式=
|工作室=
|網路電台=（網路電台）
|廣播聯播網=
|贊助=
|其他=
|版權=
}}
</pre></small>
|<small><pre>


廣播節目名稱
節目暱稱
節目主持人
節目DJ
節目助手
策劃節目構成



編劇


首播日期
結束日期
播放電台
播出日期、時段

收錄後播放、串流...等
錄音製作公司


節目提供商
備註
版權資訊

</pre></small>
|}
請在''播放開始''與''播放結束''欄填入節目首播、結束日期。超過深夜24時的節目播放請記載前一天的日期。
:（例）若於A月1日26時（A月2日2時）播放，則寫為「A月1日」。

''[[廣播聯播網]]''利用方式如「[[全国FM放送協議会|JFN]]38局」。不用於獨立電台。

''網路''僅使用於網路廣播。當此欄位填有參數時，各欄位的「播放」將改變為「配信」。基本上以「網路=1」的方式填寫即可。

當節目為網路廣播時需注意：
*''播放開始''及''播放結束''分別填寫第1次的配信開始日、最終回的配信開始日。''播放結束''不寫配信的最終日期。
*''廣播電台''填寫節目的配信網站。若節目不在專門的網路廣播配信網站播放，而是在獨自簽約的伺服器上配信，可以記載「官方網頁」或「節目網頁」。
*''播放時間''填寫節目的配信日（例：毎週日、毎月25日 等）。
*''播放形式''填寫節目的播放形式。主要有 收錄後播放、串流、隨選、P2P、下載 等，詳細參見[[:ja:インターネットラジオ#放送方式]]。

某些節目會並行地面廣播和網路配信，基本上以最早的播放電台來決定。

=== 電影 ===
{| 
|<small><pre>
{{Infobox animanga/Movie
|標題 = 
|原案 = 
|原作 = 
|總導演 = 
|導演 = （必須輸入）
|編劇 = 
|人物原案 = 
|人物設定 = 
|機械設定 = 
|音樂 = 
|音樂製作 = 
|動畫製作 = 
|製作 = （必須輸入）
|影片發行 = （必須輸入）
|其他影片發行 = 
|代理發行 = 
|其他代理發行 = 
|上映日 = （必須輸入）
|片長 = 
|預算 = 
|票房 =
|網絡 = （網絡首播時填入）
|其他 = 
|版權 = 
}}</pre></small>
|<small><pre>

電影標題
原案
原作所有者

電影導演
編劇
キャラクター原案
キャラクターデザイン
メカニックデザイン

音樂製作公司
動畫公司、工作室
製作委員會
電影的發行公司
他國電影上映的發行公司
影碟的代理發行商
他國影碟的代理發行商
首次上映日期
影片播放時間
影片製作預算
電影的票房總收入
#
備註
版權資訊

</pre></small>
|}

沒有原作或以電影為重的條目可以考慮使用{{tl|Infobox Film}}，例如：[[红猪]]、[[格得战记]]。

和譯名有直接關係的電影上映通路商請放在「影片發行」欄位。「其他影片發行」用於歐美等國家。

===卡司（飾演）===
以下為役名及演出者有4人的情況為例。
{| 
|<small><pre>
{{Infobox animanga/Cast
|人物= 1<br/>2<br/>3<br/>4
|演員= 一<br/>二<br/>三<br/>四
}}</pre></small>
|<small><pre>

主要登場人物
飾演的演員

</pre></small>
|}

動畫或遊戲作品可用下列參數。
{| 
|<small><pre>
{{Infobox animanga/Cast
|角色= 1<br/>2<br/>3<br/>4
|聲優= 一<br/>二<br/>三<br/>四
}}</pre></small>
|<small><pre>

作品主要角色
配音的聲優

</pre></small>
|}

=== 其他 ===
<pre>
{{Infobox animanga/Other
|標題= （必須輸入）
|內容= （必須輸入）
}}
</pre>
在此構成元件使用wiki型式的條列寫法時，必須從''內容''的下一行開始。例如以下範例。
<pre>
{{Infobox animanga/Other
|標題= 
|內容= 
* [[記述內容1]]
* [[記述內容2]]
}}
</pre>
=== 其他2 ===
如果不希望使用条列写法，可以使用更宽松的列项表格写法。
<pre>
{{Infobox animanga/Other2
|标题= 
|key1= <标签名1>
|value1= <标签值1>
.
.
.
|key<n> =
|value<n> =
}}
</pre>

=== 延伸作品 ===
若作品多次[[跨媒體製作]]但沒有獨立條目以至於模板過長，可以考慮將其他媒體的延伸作品包覆於本折疊模組內。

如需將其他媒體作品的模組收合在一個折疊模組內，可使用以下模組：
<pre>
{{Infobox animanga/MediaMix}}
這裡放其他媒體作品的模組
{{Infobox animanga/MediaMixFooter}}
</pre>

如需將其他媒體作品的模組按作品種類分別收合在多個折疊模組內，可使用以下模組：
<pre>
{{Infobox animanga/MediaMix|作品種類}}
這裡放其他媒體作品的模組
{{Infobox animanga/MediaMixFooter}}
</pre>
本模組應該置於Header、name模組、以及原作媒體模組的下方，Footer模組之上。效果參見[[魔法禁書目錄]]（整組包覆）、[[初音島II]]（個別分組）。

== 記載例與表示例 ==
{{請注意|記載內容只是個範例，可能與實際上有出入。}}
{{Infobox animanga/Headerofja
|title= [[Wikipedia:維基娘|維基百科大冒險！]]
|image= Wikipe-tan full length.svg
|size= 200px
|caption= 主角 - 維基娘
|japanese= ウィキペディアの大冒険!
|english= The Adventures of Wikipedia!
|kana= 
|romaji= 
|genre= [[動作]]
}}
{{Infobox animanga/name
|original= 
|official= 維基百科大冒險！
|formal= 维基百科的大冒险！
|common= 维基大冒险
}}
{{Infobox animanga/Manga
|標題= 維基百科大冒險！ THE COMIC
|作者= [[吉米·威爾士]]
|作畫= [[:ja:利用者:Kasuga]]
|出版社= [[维基媒体基金会]]
|連載雜誌= [[Wikipedia]]
|label= [[Wikipedia]]
|發售日= 2001年1月15日
|開始= 2001年1月15日
|結束= 
|冊數= {{NUMBEROFFILES}}卷
|話數= {{NUMBEROFARTICLES}}話
|其他= 
}}
{{Infobox animanga/MediaMix|小说外传}}
{{Infobox animanga/Novel
|輕小說= Y
|標題= [[网络观察基金会与维基百科|维基百科与与英国爱恨缠绵]]
|原作=
|作者= [[维基媒体基金会]]
|插圖= 
|出版社= [[维基媒体基金会]]
|其他出版社= 
|連載雜誌= 
|label= 
|網路= [[维基百科|维基百科网站]]
|發售日= 
|開始= 2008年12月5日
|結束= 2008年12月9日
|冊數= 1
|話數= 4
|其他= 
|版權=
}}
{{Infobox animanga/Novel
|輕小說= 
|標題= [[中国大陆封锁维基媒体事件|中国大陆与维基的大战]]
|原作=
|作者= [[维基媒体基金会]]
|插圖= 
|出版社= [[维基媒体基金会]]
|其他出版社= 
|連載雜誌= 
|label= 
|網路= 
|發售日= 
|開始= 2004年6月3日
|結束= 
|冊數= 15（截至2019年）
|話數= 
|其他= 
|版權=
}}
{{Infobox animanga/MediaMixFooter}}
{{Infobox animanga/TVAnime
|標題= 自由百科 維基百科大冒險！
|導演= [[吉米·威爾士]]
|系列構成= [[吉米·威爾士]]
|人物設定= [[:ja:利用者:Kasuga]]
|機械設定= [[:ja:利用者:Kasuga]]
|動畫製作= [[Wikipedia]]
|製作= [[Wikipedia]]
|播放電視台= [[维基媒体]]电视台
|播放開始= 2001年4月15日
|播放結束= 10月7日
|話數= 全26話
|其他= 
|版權= 2001 Jimmy Production/<br>Wikipedia·wiki Entertainment
}}
{{Infobox animanga/Cast
|角色= 維基娘<br>勇者
|聲優= [[平野綾]]<br>[[森久保祥太郎]]
}}
{{Infobox animanga/OVA
|標題= 新·自由百科 維基百科大冒險！
|導演= [[吉米·威爾士]]
|系列構成= [[吉米·威爾士]]
|人物設定= [[:ja:利用者:Kasuga]]
|機械設定= [[:ja:利用者:Kasuga]]
|動畫製作= [[Wikipedia]]
|製作= [[Wikipedia]]
|發售日= 
|開始= 2002年7月15日
|結束= 2003年7月15日
|話數= 全12話
|其他= 
}}
{{Infobox animanga/Novel
|標題= 維基百科大冒險！ The Side Story
|作者= [[吉米·威爾士]]
|插圖= [[:ja:利用者:Kasuga]]
|出版社= [[维基媒体基金会]]
|連載雜誌= [[Wikipedia]]
|label= [[Wikipedia]]
|發售日= 2001年8月15日
|開始= 2001年8月15日
|結束= 繼續中
|冊數= 目前{{#expr:{{LOCALYEAR}}-2001}}卷
|話數= {{NUMBEROFARTICLES}}話
|其他= 
}}
{{Infobox animanga/Movie
|標題= 維基百科大冒險！ The Movie
|導演= [[吉米·威爾士]]
|制作= [[Wikipedia]]
|製作= wiki製作委員会
|上映日= 2002年11月15日
|片長= 123分
|其他= 
|Copyright= Jimmy Movie Production/<br>Wikipedia·wiki製作委員会
}}
{{Infobox animanga/Cast
|人物= 維基娘<br>勇者
|演員= [[平野綾]]<br>[[森久保祥太郎]]
}}
{{Infobox animanga/Game
|標題=維基百科大冒險！ ONLINE
|類型=[[線上遊戲]]
|使用平台=[[MediaWiki]]
|遊戲引擎=[[MediaWiki]]
|開發團隊=[[Wikimedia]]
|代理商=[[Wikimedia]]
|製作人=[[吉米·威爾士]]
|監製=[[吉米·威爾士]]
|人物設定=[[:ja:利用者:Kasuga]]
|媒體=[[MediaWiki]]
|遊戲人數={{NUMBEROFUSERS}}人
|發售日=2002年6月15日
|對象年齡=全年齡
|結局數=1
|其他=有保護、半保護功能
}}
{{Infobox animanga/Footerofja}}

{| border="0" cellspacing="0" cellpadding="0" style="background: transparent; float: left;"
|<pre>
{{Infobox animanga/Headerofja
|title= [[Wikipedia:維基娘|維基百科大冒險！]]
|image= Wikipe-tan full length.svg
|size= 200px
|caption= 主角 - 維基娘
|japanese= ウィキペディアの大冒険!
|english= The Adventures of Wikipedia!
|kana= 
|romaji= 
|genre= [[動作]]
}}
{{Infobox animanga/name
|original= 
|official= 維基百科大冒險！
|formal= 维基百科的大冒险！
|common= 维基大冒险
}}
{{Infobox animanga/Manga
|標題= 維基百科大冒險！ THE COMIC
|作者= [[吉米·威爾士]]
|作畫= [[:ja:利用者:Kasuga]]
|出版社= [[维基媒体基金会]]
|連載雜誌= [[Wikipedia]]
|label= [[Wikipedia]]
|發售日= 2001年1月15日
|開始= 2001年1月15日
|結束= 
|冊數= {{NUMBEROFFILES}}卷
|話數= {{NUMBEROFARTICLES}}話
|其他= 
}}
{{Infobox animanga/MediaMix|小说外传}}
{{Infobox animanga/Novel
|輕小說= Y
|標題= [[网络观察基金会与维基百科|维基百科与与英国爱恨缠绵]]
|原作=
|作者= [[维基媒体基金会]]
|插圖= 
|出版社= [[维基媒体基金会]]
|其他出版社= 
|連載雜誌= 
|label= 
|網路= [[网络观察基金会与维基百科|维基百科网站]]
|發售日= 
|開始= 2008年12月5日
|結束= 2008年12月9日
|冊數= 1
|話數= 4
|其他= 
|版權=
}}
{{Infobox animanga/Novel
|輕小說= 
|標題= [[中国大陆封锁维基媒体事件]]
|原作=
|作者= [[维基媒体基金会]]
|插圖= 
|出版社= [[维基媒体基金会]]
|其他出版社= 
|連載雜誌= 
|label= 
|網路= 
|發售日= 
|開始= 2004年6月3日
|結束= 
|冊數= 15（截至2019年）
|話數= 
|其他= 
|版權=
}}
{{Infobox animanga/MediaMixFooter}}
{{Infobox animanga/TVAnime
|標題= 自由百科 維基百科大冒險！
|導演= [[吉米·威爾士]]
|系列構成= [[吉米·威爾士]]
|人物設定= [[:ja:利用者:Kasuga]]
|機械設定= [[:ja:利用者:Kasuga]]
|動畫製作= [[Wikipedia]]
|製作= [[Wikipedia]]
|播放電視台= [[维基媒体]]电视台
|播放開始= 2001年4月15日
|播放結束= 10月7日
|話數= 全26話
|其他= 
|版權= 2001 Jimmy Production/<br>Wikipedia·wiki Entertainment
}}
{{Infobox animanga/Cast
|角色= 維基娘<br>勇者
|聲優= [[平野綾]]<br>[[森久保祥太郎]]
}}
{{Infobox animanga/OVA
|標題= 新·自由百科 維基百科大冒險！
|導演= [[吉米·威爾士]]
|系列構成= [[吉米·威爾士]]
|人物設定= [[:ja:利用者:Kasuga]]
|機械設定= [[:ja:利用者:Kasuga]]
|動畫製作= [[Wikipedia]]
|製作= [[Wikipedia]]
|發售日= 
|開始= 2002年7月15日
|結束= 2003年7月15日
|話數= 全12話
|其他= 
}}
{{Infobox animanga/Novel
|標題= 維基百科大冒險！ The Side Story
|作者= [[吉米·威爾士]]
|插圖= [[:ja:利用者:Kasuga]]
|出版社= [[维基媒体基金会]]
|連載雜誌= [[Wikipedia]]
|label= [[Wikipedia]]
|發售日= 2001年8月15日
|開始= 2001年8月15日
|結束= 繼續中
|冊數= 目前{{#expr:{{LOCALYEAR}}-2001}}卷
|話數= {{NUMBEROFARTICLES}}話
|其他= 
}}
{{Infobox animanga/Movie
|標題= 維基百科大冒險！ The Movie
|導演= [[吉米·威爾士]]
|制作= [[Wikipedia]]
|製作= wiki製作委員会
|上映日= 2002年11月15日
|片長= 123分
|其他= 
|Copyright= Jimmy Movie Production/<br>Wikipedia·wiki製作委員会
}}
{{Infobox animanga/Cast
|人物= 維基娘<br>勇者
|演員= [[平野綾]]<br>[[森久保祥太郎]]
}}
{{Infobox animanga/Game
|標題=維基百科大冒險！ ONLINE
|類型=[[線上遊戲]]
|使用平台=[[MediaWiki]]
|遊戲引擎=[[MediaWiki]]
|開發團隊=[[Wikimedia]]
|代理商=[[Wikimedia]]
|製作人=[[吉米·威爾士]]
|監製=[[吉米·威爾士]]
|人物設定=[[:ja:利用者:Kasuga]]
|媒體=[[MediaWiki]]
|遊戲人數={{NUMBEROFUSERS}}人
|發售日=2002年6月15日
|對象年齡=全年齡
|結局數=1
|其他=有保護、半保護功能
}}
{{Infobox animanga/Footerofja}}
</pre>
|}
{{brClear}}

=== 翻譯名稱模組使用範例 ===
一般多個譯名時，接在Header下方。
{{Infobox animanga/Headerofja
|標題=光速蒙面俠21
|日文名稱=アイシールド21
|英文名稱=Eyeshield 21
|類型=[[體育漫畫]]
}}
{{Infobox animanga/name
|original= 
|official= 
|formal= {{flagicon|Taiwan}} 光速蒙面俠21（[[東立出版社]]） <br/> {{flagicon|Hong Kong}} 高速達陣（[[文化傳信]]） <br/> {{flagicon|United States}} Eyeshield 21（[[VIZ Media]]）
|common= 
}}
{{Infobox animanga/Footerofja}}
{| border="0" cellspacing="0" cellpadding="0" style="background: transparent; float: left;"
|<pre>
{{Infobox animanga/Headerofja
|標題=光速蒙面俠21
|日文名稱=アイシールド21
|英文名稱=Eyeshield 21
|類型=[[體育漫畫]]
}}
{{Infobox animanga/name
|formal={{flagicon|Taiwan}} 光速蒙面俠21（[[東立出版社]]） <br/> {{flagicon|Hong Kong}} 高速達陣（[[文化傳信]]） <br/>
 {{flagicon|United States}} Eyeshield 21（{{Tsl|en|VIZ Media|VIZ Media}}）
}}
{{Infobox animanga/Footerofja}}
</pre>
|}

{{Clear}}
某些譯名繁複的作品，可以和Other模組合併使用；將整個name模組放在Other的內容裡。

{{Infobox animanga/Headerofja
|標題= -{zh-hans:哆啦A梦;zh-hk:多啦A夢;zh-tw:哆啦A夢;}-
|日文名稱= ドラえもん‎
|英文名稱= Doraemon
|類型= [[搞笑]]、[[科幻]]漫畫
}}
{{Infobox animanga/Other
|標題= 翻譯名稱
|內容= 
{{Infobox animanga/name
|official= -{zh-hans: 哆啦A梦（中国大陆、台湾）;zh-hant: 哆啦A夢（中國大陸、台灣）}- <br/>-{zh-hans: 多啦A夢（香港）;zh-hant: 多啦A夢（香港）}-
|formal= 叮噹（{{flagicon|Hong Kong}} [[文化傳信]]） <br/> 機器貓小叮噹（{{flagicon|Taiwan}} [[青文出版社]]） <br/> 超能貓小叮噹（{{flagicon|Taiwan}} [[東立出版社]]） <br/> 神奇小叮噹（{{flagicon|Taiwan}} [[大然文化]]）
|common= 萬能小叮噹<br/>機器貓<br/>小叮噹<br/>叮噹
}}
}}
{{Infobox animanga/Footerofja}}
{| border="0" cellspacing="0" cellpadding="0" style="background: transparent; float: left;"
|<pre>
{{Infobox animanga/Headerofja
|標題= -{zh-hans:哆啦A梦;zh-hk:多啦A夢;zh-tw:哆啦A夢;}-
|日文名稱= ドラえもん‎
|英文名稱= Doraemon
|類型= [[搞笑]]、[[科幻]]漫畫
}}
{{Infobox animanga/Other
|標題= 翻譯名稱
|內容= 
{{Infobox animanga/name
|official= -{zh-hans: 哆啦A梦（中国大陆、台湾）;zh-hant: 哆啦A夢（中國大陸、台灣）}- <br/> -{zh-hans: 多啦A夢（香港）;zh-hant: 多啦A夢（香港）}-
|formal= 叮噹（{{flagicon|Hong Kong}} [[文化傳信]]） <br/> 機器貓小叮噹（{{flagicon|Taiwan}} [[青文出版社]]） <br/> 超能貓小叮噹（{{flagicon|Taiwan}} [[東立出版社]]） <br/>
 神奇小叮噹（{{flagicon|Taiwan}} [[大然文化]]）
|common= 萬能小叮噹<br/>機器貓<br/>小叮噹<br/>叮噹
}}
}}
{{Infobox animanga/Footerofja}}
</pre>
|}

[[Category:Infobox animanga| ]]
[[Category:出版品信息框模板|A]]
[[Category:電視信息框模板|A]]