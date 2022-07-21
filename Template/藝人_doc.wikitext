<includeonly>{{High-use|26560}}{{esoteric}}{{Person infobox header}}{{lua|模組:Infobox|模組:InfoboxImage|模組:Check for unknown parameters}}{{Tracks Wikidata|P18|cat=维基数据图片数据相关分类}}<!--  {{Template doc page transcluded}} --></includeonly><noinclude>{{Template_doc_page_viewed_directly}}</noinclude>
<!-- 此線之下為編輯模板的說明文件 -->
{{NoteTA
|1=zh-hans:文件;zh-hant:檔案;
|2=zh-hans:文件名;zh-hant:檔案名字;
|3=zh-hans:链接;zh-hant:連結;
|4=zh-hans:互联网电影数据库;zh-hant:網路電影資料庫;
|5=zh-hans:戛纳电影节;zh-hant:康城影展;zh-hk:康城影展;zh-mo:康城影展;zh-tw:坎城影展;
|6=zh-cn:金酸莓奖;zh-tw:金酸莓獎;zh-hk:金草莓獎;
|7=zh-hans:格莱美奖;zh-hant:葛萊美獎;zh-cn:格莱美奖;zh-tw:葛萊美獎;zh-hk:格林美獎;zh-mo:格林美獎;
|8=zh-cn:托尼奖;zh-tw:東尼獎;zh-hk:東尼獎;
|9=zh-hans:搜索;zh-hant:搜尋;
|10=zh-hans:支持;zh-hant:支援;
|11=zh-hans:可视化编辑器;zh-hant:視覺化編輯器;
|12=zh-hans:数据;zh-hant:資料;
|13=zh-hans:信息;zh-hant:資訊;
|14=zh-hans:信息框;zh-hant:資訊框;
|15=zh-hans:电影节;zh-hant:影展;
|16=zh-hans:坐标;zh-hant:座標;
|17=zh-hans:模块;zh-hant:模組;
|18=zh-hans:默认;zh-hant:預設;
|19=zh-cn:剪辑;zh-tw:剪輯;zh-hk:剪接;
}}
本模板可使用在提供所有從事不同崗位的'''藝人'''條目的相關摘要資訊（包含歌手、演員、配音員、童星等），由[[Wikipedia:歌手和演员專題]]管理。
* 如該人物為相聲、小品演員，可配合模板{{tl|Crosstalk actor master-apprentice relation module}}。
* 如該人物為[[喜劇演員]]，請使用模板{{tl|Infobox comedian}}。
* 如該人物為古典音樂作曲家，請使用模板{{tl|Infobox classical composer}}。

該模板也可以用作{{tl|Infobox person}}的子模板（嵌入模組）。

請盡量不要將藝人所有的作品列出，可選擇較著名的作品，以保持信息框的意義－「提供摘要」，詳細的作品資訊可留至內文中詳述。
{{Parameter names example
 |前綴尊稱 |姓名 |後綴尊稱 |類型=藝人
 |圖片=Pessoa Neutra.svg |圖片尺寸=220px |補正=no |圖片替代 |圖片簡介
 |本名 |外文名 |外文 |羅馬拼音 |英文名 |暱稱 |其他藝名
 |國籍 |永久居留權 |民族 |籍貫
 |出生名 |出生日期 |出生地點
 |逝世日期 |逝世地點 |死因 |墓地 |墓地座標 |居住地
 |職業 |語言 |教育程度 |母校 |宗教信仰
 |配偶 |兒女 |父母 |親屬
 |音樂類型 |演奏樂器
 |出道地點 |出道日期 |出道作 |代表作
 |著名角色 |活躍年代 |唱片公司 |經紀公司
 |簽名=Example title.svg |簽名大小=150px |簽名替代
 |網站 |相關團體
 |module |module2 |module3=[......] |module6
 |IMDb
 |現任成員 |過往成員 |著名樂器
 |academyawards |cannesfilmawards |afiawards |arielaward |baftaawards
 |cesarawards |emmyawards |filmfareawards |geminiawards |goldenglobeawards
 |goldenraspberryawards |goyaawards |grammyawards |hongkongfilmawards |olivierawards
 |iftaawards |imageaward |nationalfilmawards |sagawards |tonyawards
 |goldenbauhiniaawards |hkfcsawards |asianfilmawards |goldenhorseawards |huabiaoawards
 |goldenroosterawards |hundredflowersawards |goldeneagleawards |flyingapsarasawards |rthktop10goldsongsawards
 |goldenmelodyawards |mtvasiaawards |ntsawards |chinamusicawards |goldenbellawards
 |tvbanniversaryawards |magnoliaawards |asiantvawards |rainbowawards
 |tokyofilmawards |yokohamafilmawards |japanacademyawards |japanesefilmcreticsawards |mainichifilmawards
 |blueribbonawards |hochifilmawards |kinemajunpotop10awards |grandbellawards |bluedragonfilmawards |paeksangartsawards
 |獎項
}}

== 使用與重定向 ==
至少有{{PAGESINCATEGORY:呼叫藝人的模板}}個模板[[:Category:呼叫藝人的模板|使用了本模板中的參數]]，[https://zh.wikipedia.org/w/index.php?title=Special:%E9%93%BE%E5%85%A5%E9%A1%B5%E9%9D%A2/Template:%E8%97%9D%E4%BA%BA&hidelinks=1&hidetrans=1 有多個模板重定向至本模板]。

== 實現機理 ==
在2015年7月初，此模板進行了一次更新，修改了原有的識別繁簡英參數及獎項欄位的實現方法。在新的版本中，核心內容、繁簡英參數識別及獎項欄位識別均由此模板進行，不再依賴{{tlc|藝人/core}}與{{tlc|藝人/awards}}兩個模板。同時，新的版本採用標准化的{{tl|Infobox}}模板編寫，更加便於後期的維護。

== 使用方式 ==
本模板分為英文版和中文版，其中中文版用戶可自行選擇繁體中文或簡體中文。要將本模板加入條目中，請複製以下空白原始碼，並貼至條目中即可。只有'''姓名'''和'''類型'''兩個欄位是必須填上。除獎項欄位外，沒有資料的項目可保持空白不用刪除，並不會影響模版的使用。

=== 基本參數空白模板 ===
{| style="border: none; background: transparent;"
|<pre>-{zh;zh-hans;zh-hant|
{{藝人
|姓名 = 
|類型 = 
|圖片 = 
|圖片尺寸 = 
|圖片簡介 = 
|本名 = 
|外文名 = 
|外文 = 
|羅馬拼音 = 
|英文名 = 
|暱稱 = 
|其他藝名 = 
|國籍 = 
|民族 = 
|籍貫 = 
|出生日期 = 
|出生地點 = 
|逝世日期 = 
|逝世地點 = 
|職業 = 
|語言 = 
|教育程度 = 
|母校 = 
|宗教信仰 = 
|配偶 = 
|兒女 = 
|父母 = 
|親屬 = 
|音樂類型 = 
|演奏樂器 = 
|出道地點 = 
|出道日期 = 
|出道作 = 
|代表作 = 
|著名角色 = 
|活躍年代 = 
|唱片公司 = 
|經紀公司 = 
|網站 = 
|相關團體 = 
|IMDb = 
|現任成員 = 
|過往成員 = 
|獎項 = 
}}}-
</pre>
|}

=== 完整參數空白模板 ===
{| style="border: none; background: transparent;"
|<pre>-{zh;zh-hans;zh-hant|
{{藝人
|前綴尊稱 = 
|姓名 = 
|後綴尊稱 = 
|類型 = 
|圖片 = 
|圖片尺寸 = 
|補正 = 
|圖片替代 = 
|圖片簡介 = 
|本名 = 
|外文名 = 
|外文 = 
|羅馬拼音 = 
|英文名 = 
|暱稱 = 
|其他藝名 = 
|國籍 = 
|永久居留權 = 
|民族 = 
|籍貫 = 
|出生名 = 
|出生日期 = 
|出生地點 = 
|逝世日期 = 
|逝世地點 = 
|死因 = 
|墓地 = 
|墓地-{zh-hans:坐;zh-hant:座;}-標 = 
|居住地 = 
|職業 = 
|語言 = 
|教育程度 = 
|母校 = 
|宗教信仰 = 
|配偶 = 
|兒女 = 
|父母 = 
|親屬 = 
|音樂類型 = 
|演奏樂器 = 
|出道地點 = 
|出道日期 = 
|出道作 = 
|代表作 = 
|著名角色 = 
|活躍年代 = 
|唱片公司 = 
|經紀公司 = 
|簽名 = 
|簽名大小 = 
|簽名替代 = 
|網站 = 
|相關團體 = 
|module = 
|module2 = 
|module3 = 
|module4 = 
|module5 = 
|module6 = 
|IMDb = 
|現任成員 = 
|過往成員 = 
|著名樂器 = 
|academyawards = 
|cannesfilmawards = 
|afiawards = 
|arielaward = 
|baftaawards = 
|cesarawards = 
|emmyawards = 
|filmfareawards = 
|geminiawards = 
|goldenglobeawards = 
|goldenraspberryawards = 
|goyaawards = 
|grammyawards = 
|hongkongfilmawards = 
|olivierawards = 
|iftaawards = 
|imageaward = 
|nationalfilmawards = 
|sagawards = 
|tonyawards = 
|goldenbauhiniaawards = 
|hkfcsawards = 
|asianfilmawards = 
|goldenhorseawards = 
|huabiaoawards = 
|goldenroosterawards = 
|hundredflowersawards = 
|goldeneagleawards = 
|flyingapsarasawards = 
|rthktop10goldsongsawards = 
|goldenmelodyawards = 
|mtvasiaawards = 
|ntsawards = 
|chinamusicawards = 
|goldenbellawards = 
|tvbanniversaryawards = 
|magnoliaawards = 
|asiantvawards = 
|rainbowawards = 
|tokyofilmawards = 
|yokohamafilmawards = 
|japanacademyawards = 
|japanesefilmcreticsawards = 
|mainichifilmawards = 
|blueribbonawards = 
|hochifilmawards = 
|kinemajunpotop10awards = 
|grandbellawards = 
|bluedragonfilmawards = 
|paeksangartsawards = 
|獎項 = 
}}}-
</pre>
|<pre>
{{Infobox entertainer
| honorific_prefix          = 
| name                      = 
| honorific_suffix          = 
| type                      = 
| image                     = 
| image_size                = 
| landscape                 = 
| alt                       = 
| caption                   = 
| real_name                 = 
| native_name               = 
| native_name_lang          = 
| romanized_name            = 
| english_name              = 
| nickname                  = 
| other_name                = 
| nationality               = 
| permanent_residency       = 
| people                    = 
| hometown                  = 
| birth_name                = 
| birth_date                = 
| birth_place               = 
| death_date                = 
| death_place               = 
| death_cause               = 
| resting_place             = 
| resting_place_coordinates = 
| residence                 = 
| occupation                = 
| language                  = 
| education                 = 
| alma_mater                = 
| religion                  = 
| spouse                    = 
| children                  = 
| parents                   = 
| relatives                 = 
| music_genre               = 
| instrument                = 
| origin_place              = 
| debut_date                = 
| debut_work                = 
| famous_works              = 
| notable_roles             = 
| years_active              = 
| label                     = 
| agent_company             = 
| signature                 = 
| signature_size            = 
| signature_alt             = 
| website                   = 
| related_group             = 
| module                    = 
| module2                   = 
| module3                   = 
| module4                   = 
| module5                   = 
| module6                   = 
| IMDb                      = 
| current_members           = 
| past_members              = 
| notable_instruments       = 
| academyawards             = 
| cannesfilmawards          = 
| afiawards                 = 
| arielaward                = 
| baftaawards               = 
| cesarawards               = 
| emmyawards                = 
| filmfareawards            = 
| geminiawards              = 
| goldenglobeawards         = 
| goldenraspberryawards     = 
| goyaawards                = 
| grammyawards              = 
| hongkongfilmawards        = 
| olivierawards             = 
| iftaawards                = 
| imageaward                = 
| nationalfilmawards        = 
| sagawards                 = 
| tonyawards                = 
| goldenbauhiniaawards      = 
| hkfcsawards               = 
| asianfilmawards           = 
| goldenhorseawards         = 
| huabiaoawards             = 
| goldenroosterawards       = 
| hundredflowersawards      = 
| goldeneagleawards         = 
| flyingapsarasawards       = 
| rthktop10goldsongsawards  = 
| goldenmelodyawards        = 
| mtvasiaawards             = 
| ntsawards                 = 
| chinamusicawards          = 
| goldenbellawards          = 
| tvbanniversaryawards      = 
| magnoliaawards            = 
| asiantvawards             = 
| rainbowawards             = 
| tokyofilmawards           = 
| yokohamafilmawards        = 
| japanacademyawards        = 
| japanesefilmcreticsawards = 
| mainichifilmawards        = 
| blueribbonawards          = 
| hochifilmawards           = 
| kinemajunpotop10awards    = 
| grandbellawards           = 
| bluedragonfilmawards      = 
| paeksangartsawards        = 
| awards                    = 
}}
</pre>
|}
*請參見「[[#欄位說明|欄位說明]]」以了解每項欄位的意義和建議填寫方式。

== 欄位說明 ==

「粗體」表示的欄位必須填上。

{| style="background: none"
|width="110px" | 前綴尊稱 || 在藝人姓名左側出現的文字。
|-
| '''姓名''' || 藝人的中文姓名或譯名。若沒填，會以條目名代替。請儘量使用中文。
|-
| 後綴尊稱 || 在藝人姓名右側出現的文字。
|-
| '''類型''' || 主要從事的演藝類型，會影響背景顏色（請參照[[#背景顏色|下方的說明]]）。必須填，否則會出現錯誤。詳見：[[:Template:藝人/type return]]
|-
| 圖片 || 藝人的照片檔案名稱（完整檔案名字），例如'''Example.jpg'''。請注意[[Wikipedia:版權資訊#名人的照片|版權問題]]，'''絕大部份從網路上下載的藝人照片均不能在維基使用'''。'''在世人物必須使用自由版權的圖片。'''
|-
| 圖片尺寸 || 圖片尺寸，填寫格式：'''Npx'''。'''N'''字為一任意整數，不能為負數，意即將圖片的宽度设為'''N'''像素。預設值為'''220px'''。只於有圖片時有效，若依預設值縮放則不需填寫。
|-
| 補正 || 在使用較寬、較短的（長方形）圖片時請填入「yes」，圖片的高度會被限制在 200 像素內（只於有圖片時有效）。
|-
| 圖片替代 || 圖片的[[WP:ALT|替代文本]]（只於有圖片時有效）。
|-
| 圖片簡介 || 圖片說明（只於有圖片時有效）。
|-
| 本名 || 真正、正式的名字。'''如果藝人的藝名和本名一樣，則此欄則可以略過'''。多於一個時請用「、」做分隔。
|-
| 外文名 || 根據其國家語系的名字，非拉丁字母系的外文名（如日文，韓文或俄文等）。
|-
| 外文 || 指明外文名之語系，以正確顯示文字（如日文、韓文、俄文等）。只於有外文名時有效。詳見：[[:Template:藝人/lang selector]] '''注意：是 ''ISO-639 語言代碼''，不是中文'''。
|-
| 羅馬拼音 || 非拉丁字母語系（如中文、日文、韓文、俄文等）的拉丁字母拼法。
|-
| 英文名 || 英語名稱，或拉丁字母語系的名字。請留意其與羅馬拼音的不同，如劉德華的英文名是'''Andy Lau'''，而其羅馬拼音則是'''Lau Dak-wa'''。
|-
| 暱稱 || 經常出現在新聞媒體上的暱稱，多個暱稱時請用「、」做分隔，'''最多別超過五個'''。
|-
| 其他藝名 || 曾使用或在外地發展時所使用的藝名。
|-
| 國籍 || 所屬國籍（國家）。若為團體請填寫團體的所屬國籍，'''請勿列出成員的所屬國籍'''。建議使用「{{tlc|國家地區模板}}」。請參照[[Wikipedia:國家及地區標示模板]]。
|-
| 永久居留權 || 永久居留權。'''僅在與國籍不同時填寫。'''
|-
| 民族 || 所屬民族。
|-
| 籍貫 || 家鄉或籍貫。
|-
| 出生名 || 出生名字。'''原則上視同本名，但本名未必是出生名'''。如成龍的出生名是'''陳港生'''，而其本名則是'''房仕龍'''。
|-
| 出生日期 || 出生日期。在世者使用{{tl|Birth date and age}}模板，可自動計算並顯示出歲數。已過世者用{{tl|birth date}}模板。未知完整出生日期者使用「<nowiki>YYYY年MM月DD日</nowiki>」的格式。
|-
| 出生地點 || 出生地。可使用「{{tlc|國家地區模板}} 地區名」的格式，請參照[[Wikipedia:國家及地區標示模板]]。[[維基百科:格式手冊/旗幟]]建議在有新共識前慎重處理出生與死亡地的旗幟，已有國旗的請勿移除，沒有國旗的請勿加入。
|-
| 逝世日期 || 逝世日期。格式同出生日期。使用{{tl|Death date and age}}模板，可自動計算並顯示出歲數。未知出生日期或出生日期不完整者使用{{tl|Death date}}模板。未知完整逝世日期者使用「<nowiki>YYYY年MM月DD日</nowiki>」的格式。
|-
| 逝世地點 || 逝世地點。格式同出生地點。
|-
| 死因 || 逝世原因。
|-
| 墓地 || 死者墓地或葬於、揚骨灰等的地點。
|-
| 墓地座標 || 墓地等的座標，使用{{tl|Coord}}模板。
|-
| 居住地 || 居住地點。格式同出生地點。'''僅在與出生地點不同時填寫。'''
|-
| 職業 || 所從事的演藝工作。'''非演藝相關的職業請勿列入'''。
|-
| 語言 || '''請填寫能流暢溝通的語言或方言'''，多於一個時請用「、」做分隔。
|-
| 教育程度 || 艺人的'''最高'''教育程度。若有多個高等教育學位可用{{tl|Plainlist}}或{{tl|Unbulleted list}}羅列。
|-
| 母校 || 藝人畢業或所就讀的院校，可加括號注明就讀院系、畢業時間等資訊。使用{{tl|Plainlist}}或{{tl|Unbulleted list}}羅列。
|-
| 宗教信仰 || 宗教信仰。
|-
| 配偶 || 配偶姓名，使用{{tl|marriage}}模板。'''請勿填寫只是在交往中，沒有正式婚姻關係者。'''
|-
| 兒女 || 子女姓名。具相關知名度（通常是指有維基條目者）才建議列出。
|-
| 父母 || 父母姓名。具相關知名度（通常是指有維基條目者）才建議列出。
|-
| 親屬 || 兄弟姐妹或其他親屬姓名，並注明與藝人之關係。具相關知名度（通常是指有維基條目者）才建議列出。
|-
| 音樂類型 || 主要演出或創作的音樂類型（適用於從事音樂的藝人）。列出較擅長或演出的類型即可。
|-
| 演奏樂器 || 擅長的樂器（適用於從事音樂的藝人）。列出較擅長或演出的樂器即可。
|-
| 出道地點 || 出道的地點。格式同出生地點。
|-
| 出道日期 || 正式宣佈加入演藝圈的日期，或組合成立的日期。使用「<nowiki>YYYY年MM月DD日</nowiki>」的格式（以官方為準）。
|-
| 出道作 || 首部參與發表的作品、電影、戲劇、或專輯等。
|-
| 代表作 || 最為人熟悉的作品，可以是電影、電視節目、舞台劇或音樂專輯等。'''最多別超過五個'''。
|-
| 著名角色 || 演員演出最為人熟悉的角色（適用於從事電視/電影/舞台劇演出的藝人）。'''最多別超過五個'''。
|-
| 活躍年代 || 活躍年代，即「出道（成立）年份 - 引退（逝世/解散）年份」。
|-
| 唱片公司 || 所属的唱片公司。
|-
| 經紀公司 || 所屬的經紀公司。
|-
| 簽名 || 藝人的簽名檔案名稱（完整檔案名字），例如'''Example.jpg'''。
|-
| 簽名大小 || 簽名尺寸，填寫格式：'''Npx'''。'''N'''字為一任意整數，不能為負數，意即將簽名的宽度设為'''N'''像素。預設值為'''150px'''。只於有簽名時有效，若依預設值縮放則不需填寫。
|-
| 簽名替代 || 簽名的[[WP:ALT|替代文本]]（只於有簽名時有效）。
|-
| 網站 || 由其個人或所屬公司經營、管理之'''一個主要的官方網站'''，其餘連結或是社群網站（如：Twitter、微博等）請放至外部連結。'''填寫格式：{{tlx|URL|www.example.com}}'''。
|-
| 相關團體 || 曾經或現在所屬的組合或團體。
|-
| module<sub>n</sub> || 用於嵌套其他信息框模板（請參照[[#嵌套其他信息框模板|下方的說明]]）。'''n'''字為一任意整數，最多可至6。
|-
| IMDb || 在[[IMDb]]網路電影資料庫的資訊。請輸入藝人的相應 ID 編號，即網址<nowiki>http://www.imdb.com/name/nmXXXXXX/</nowiki>中XXXXXX的數值。
|-
| 現任成員 || 若此條目為團體，請填入現在的成員，請用「<nowiki>*</nowiki>」羅列，可按加入時間依次排序。
|-
| 過往成員 || 若此條目為團體，請填入過往的成員，請用「<nowiki>*</nowiki>」羅列。若該團體已解散，請將所有成員填寫在「過往成員」欄位中，而不要放置在「現任成員」欄位中。
|-
| 著名樂器 || 藝人專屬的特別定做樂器（適用於從事音樂的藝人）。
|}

=== 藝人作品列表欄位 ===
藝人作品列表欄位（音樂專輯、電影、主持節目、電視劇、廣播劇、舞台劇、書籍）已於2015年8月22日從本模板中移除，參見[[Template talk:藝人/存檔9#藝人模板]]。

=== 獎項欄位 ===
* '''本模版可識別西方、華語及日韓娛樂圈具有代表性的演藝獎項，請參照下面的填寫指南將相應的獎項填入對應的欄位中。'''
* '''由於該部分參數眾多，請將沒有資料的獎項欄位刪去，待日後有需要時再添加。'''

{| style="background: none"
|width="120px" | academyawards || 藝人所獲得的[[奧斯卡金像獎]]的獎項。'''填寫格式：{{tlc|獎項|獎項類別|年份|作品|角色}}'''。
|-
| cannesfilmawards || 藝人在[[坎城影展]]上獲得的獎項。填寫格式同「academyawards」。
|-
| afiawards || 藝人所獲得的[[美國電影學會|AFI電影獎]]的獎項。填寫格式同「academyawards」。
|-
| arielaward || 藝人所獲得的{{link-en|阿列爾獎|Ariel Award}}的獎項。填寫格式同「academyawards」。
|-
| baftaawards || 藝人所獲得的[[英國電影學院獎]]的獎項。填寫格式同「academyawards」。
|-
| cesarawards || 藝人所獲得的[[凱撒電影獎]]的獎項。填寫格式同「academyawards」。
|-
| emmyawards || 藝人所獲得的[[艾美獎]]的獎項。填寫格式同「academyawards」。
|-
| filmfareawards || 藝人所獲得的[[印度電影觀眾獎]]的獎項。填寫格式同「academyawards」。
|-
| geminiawards || 藝人所獲得的[[雙子座獎]]的獎項。填寫格式同「academyawards」。
|-
| goldenglobeawards || 藝人所獲得的[[金球獎 (影視獎項)|金球獎]]的獎項。填寫格式同「academyawards」。
|-
| goldenraspberryawards || 藝人所獲得的[[金酸莓獎]]的獎項。填寫格式同「academyawards」。
|-
| goyaawards || 藝人所獲得的[[哥雅獎]]的獎項。填寫格式同「academyawards」。
|-
| grammyawards || 藝人所獲得的[[葛萊美獎]]的獎項。'''填寫格式：{{tlc|獎項|獎項類別|年份|作品}}'''。
|-
| hongkongfilmawards || 藝人所獲得的[[香港電影金像獎]]的獎項。填寫格式同「academyawards」。
|-
| olivierawards || 藝人所獲得的[[勞倫斯·奧利弗獎|勞倫斯奧利弗獎]]的獎項。填寫格式同「academyawards」。
|-
| iftaawards || 藝人所獲得的{{link-en|愛爾蘭電視電影獎|Irish Film & Television Academy}}的獎項。填寫格式同「academyawards」。
|-
| imageaward || 藝人所獲得的[[有色人種促進協會形象獎]]的獎項。填寫格式同「academyawards」。
|-
| nationalfilmawards || 藝人所獲得的[[印度國家電影獎]]的獎項。填寫格式同「academyawards」。
|-
| sagawards || 藝人所獲得的[[美國演員工會獎]]的獎項。填寫格式同「academyawards」。
|-
| tonyawards || 藝人所獲得的[[東尼獎]]的獎項。填寫格式同「academyawards」。
|-
| goldenbauhiniaawards || 藝人所獲得的[[香港電影金紫荊獎]]的獎項。填寫格式同「academyawards」。
|-
| hkfcsawards || 藝人所獲得的[[香港電影評論學會大獎]]的獎項。填寫格式同「academyawards」。
|-
| asianfilmawards || 藝人所獲得的[[亞洲電影大獎]]的獎項。填寫格式同「academyawards」。
|-
| goldenhorseawards || 藝人所獲得的[[金馬獎]]的獎項。填寫格式同「academyawards」。
|-
| huabiaoawards || 藝人所獲得的[[華表獎]]的獎項。填寫格式同「academyawards」。
|-
| goldenroosterawards || 藝人所獲得的[[金雞獎]]的獎項。填寫格式同「academyawards」。
|-
| hundredflowersawards || 藝人所獲得的[[百花獎]]的獎項。填寫格式同「academyawards」。
|-
| goldeneagleawards || 藝人所獲得的[[中國電視金鷹獎|金鷹獎]]的獎項。填寫格式同「academyawards」。
|-
| flyingapsarasawards || 藝人所獲得的[[中國電視劇飛天獎|飛天獎]]的獎項。填寫格式同「academyawards」。
|-
| rthktop10goldsongsawards || 藝人在[[十大中文金曲頒獎音樂會]]上獲得的獎項。填寫格式同「grammyawards」。
|-
| goldenmelodyawards || 藝人所獲得的[[金曲獎]]的獎項。填寫格式同「grammyawards」。
|-
| mtvasiaawards || 藝人所獲得的[[MTV亞洲大獎]]的獎項。填寫格式同「grammyawards」。
|-
| ntsawards || 藝人在[[TVB全球華人新秀歌唱大賽]]上獲得的名次。'''填寫格式：年份 名次（冠軍/亞軍/其他）'''。
|-
| chinamusicawards || 藝人在[[中國歌曲排行榜|中歌榜]]上獲得的獎項。填寫格式同「grammyawards」。
|-
| goldenbellawards || 藝人所獲得的[[金鐘獎]]的獎項。填寫格式同「academyawards」。
|-
| tvbanniversaryawards || 藝人在[[萬千星輝頒獎典禮]]上獲得的獎項。填寫格式同「academyawards」。
|-
| magnoliaawards || 藝人所獲得的[[上海電視節|上海電視節白玉蘭獎]]的獎項。填寫格式同「academyawards」。
|-
| asiantvawards || 藝人所獲得的[[亞洲電視大獎]]的獎項。填寫格式同「academyawards」。
|-
| rainbowawards || 藝人所獲得的[[亞洲彩虹獎電視頒獎禮|亞洲彩虹電視大獎]]的獎項。填寫格式同「academyawards」。
|-
| tokyofilmawards || 藝人在[[東京國際影展]]上獲得的獎項。填寫格式同「academyawards」。
|-
| yokohamafilmawards || 藝人在[[橫濱影展]]上獲得的獎項。填寫格式同「academyawards」。
|-
| japanacademyawards || 藝人所獲得的[[日本電影金像獎]]的獎項。填寫格式同「academyawards」。
|-
| japanesefilmcreticsawards || 藝人所獲得的[[日本電影影評人大獎]]的獎項。填寫格式同「academyawards」。
|-
| mainichifilmawards || 藝人所獲得的[[每日電影獎]]的獎項。填寫格式同「academyawards」。
|-
| blueribbonawards || 藝人所獲得的[[藍絲帶獎 (電影)|藍絲帶獎]]的獎項。填寫格式同「academyawards」。
|-
| hochifilmawards || 藝人所獲得的[[報知電影獎]]的獎項。填寫格式同「academyawards」。
|-
| kinemajunpotop10awards || 藝人所獲得的[[電影旬報十佳獎]]的獎項。填寫格式同「academyawards」。
|-
| grandbellawards || 藝人所獲得的[[大鐘獎]]的獎項。填寫格式同「academyawards」。
|-
| bluedragonfilmawards || 藝人所獲得的[[青龍電影獎]]的獎項。填寫格式同「academyawards」。
|-
| paeksangartsawards || 藝人所獲得的[[百想藝術大賞]]的獎項。填寫格式同「academyawards」。
|-
| 獎項 || 與其範疇相關的其他獎項，'''使用{{tl|獎項}}模板'''。建議只放置全國性或國際性，為權威機構發放，且只與藝術表演有關的獎項。網路票選、搜尋排行、人氣排行、商業活動……等獎項不宜放置於此。
|}

=== 背景顏色 ===
{{main|Template:藝人/color selector}}
*本信息框是使用顏色來分別藝人的類型。使用者並不直接選擇顏色：經由選擇下方的類別、系統會自動判別。如藝人涉及多個類型，請選擇其'''主要'''分類。
{| style="background: transparent; margin-left:1%;"
| bgcolor="{{藝人/color_selector|藝人}}"|藝人||最基本的分類
|-
| bgcolor="{{藝人/color_selector|男藝人}}"|男藝人||最基本的分類，男性
|-
| bgcolor="{{藝人/color_selector|女藝人}}"|女藝人||最基本的分類，女性
|}

==== 電視 / 電影 / 舞台劇演出 ====
{| style="background: transparent; margin-left:1%;"
| bgcolor="{{藝人/color_selector|導演}}"|導演||在戲劇演出、影視製作團隊中，整合全部藝術元素的藝術生產負責人
|-
| bgcolor="{{藝人/color_selector|編劇}}"|編劇||在戲劇演出、影視製作團隊中，負責劇本創作之人
|-
| bgcolor="{{藝人/color_selector|攝影師}}"|攝影師||在戲劇演出、影視製作團隊中，負責攝影攝像之人
|-
| bgcolor="{{藝人/color_selector|剪輯師}}"|剪輯師||在戲劇演出、影視製作團隊中，負責影像剪輯之人
|-
| bgcolor="{{藝人/color_selector|演員}}"|演員||主要從事拍攝電視/電影/舞台劇之藝人
|-
| bgcolor="{{藝人/color_selector|男演員}}"|男演員||主要從事拍攝電視/電影/舞台劇之男藝人
|-
| bgcolor="{{藝人/color_selector|女演員}}"|女演員||主要從事拍攝電視/電影/舞台劇之女藝人
|-
| bgcolor="{{藝人/color_selector|節目主持}}"|節目主持||主要從事節目主持之藝人、DJ、Web J 等
|-
| bgcolor="{{藝人/color_selector|AV女優}}"|AV女優||拍攝 AV 為主的女藝人
|-
| bgcolor="{{藝人/color_selector|童星}}"|童星||未成年之藝人
|-
| bgcolor="{{藝人/color_selector|模特兒}}"|模特兒||主要從事模特兒工作之藝人
|-
| bgcolor="{{藝人/color_selector|配音員}}"|配音員||專負責配音工作的人員
|-
| bgcolor="{{藝人/color_selector|播音員}}"|播音員||專負責播音工作的人員
|-
| bgcolor="{{藝人/color_selector|新聞主播}}"|新聞主播||專負責報導新聞的人員
|-
| bgcolor="{{藝人/color_selector|舞者}}"|舞者||從事舞蹈表演之藝人
|-
| bgcolor="{{藝人/color_selector|魔術師}}"|魔術師||從事魔術表演之藝人
|-
| bgcolor="{{藝人/color_selector|曲藝家}}"|曲藝家||主要從事曲藝表演工作之藝人、相聲演員、小品演員、評書演員等
|-
| bgcolor="{{藝人/color_selector|動作演員}}"|動作演員||主要從事動作特效之藝人
|-
| bgcolor="{{藝人/color_selector|傳媒工作者}}"|傳媒工作者||主要從事媒體工作之藝人
|-
| bgcolor="{{藝人/color_selector|幕後}}"|幕後||所有製作人、歌曲創作、經紀人等幕後人員
|}

==== 音樂 ====
{| style="background: transparent; margin-left:1%;"
| bgcolor="{{藝人/color_selector|歌手}}"|歌手||主要從事歌唱事業之藝人
|-
| bgcolor="{{藝人/color_selector|男歌手}}"|男歌手||主要從事歌唱事業之男藝人
|-
| bgcolor="{{藝人/color_selector|女歌手}}"|女歌手||主要從事歌唱事業之女藝人
|-
| bgcolor="{{藝人/color_selector|組合}}"|組合||樂隊組合，或以一個藝人以上為單位的團體
|-
| bgcolor="{{藝人/color_selector|演奏者}}"|演奏者||從事非聲樂表演之音樂藝人，音樂家亦適用
|-
| bgcolor="{{藝人/color_selector|傳統音樂}}"|傳統音樂||管弦樂相關，其他傳統音樂表演藝人亦適用
|}
*未在上述列表中列出的類型（如「偶像歌手」、「爵士樂樂手」等）將會被自動忽略，相關頁面會被自動添加到[[:分類:缺少或含有無效類型字段的藝人信息框]]中，以方便用戶進行修正。詳見：[[:Template:藝人/tracking]]

{{藝人/範例}}

== 模板資料 ==
{{hidden begin|border=#aaa solid 1px;;width:auto;overflow:auto;|titlestyle=text-align:center;|title=模板資料|bg=#F0F2F5}}
{{TemplateDataHeader}}
<templatedata>
{
	"description": "{{藝人}} 可在特定藝人條目中提供簡要的資訊。",
	"params": {
		"前綴尊稱": {
			"label": "前綴尊稱",
			"type": "string",
			"description": "在藝人姓名左側出現的文字。",
			"aliases": [ "前缀尊称", "honorific_prefix", "honorific prefix" ]
		},
		"姓名": {
			"label": "姓名",
			"type": "string",
			"default": "{{PAGENAMEBASE}}",
			"description": "藝人的中文姓名或譯名。若沒填，會以條目名代替。請儘量使用中文。",
			"aliases": [ "名字", "Name", "name" , "subject_name" ],
                        "required": true
		},
		"後綴尊稱": {
			"label": "後綴尊稱",
			"type": "string",
			"description": "在藝人姓名右側出現的文字。",
			"aliases": [ "后缀尊称", "honorific_suffix", "honorific suffix" ]
		},
		"類型": {
			"label": "從藝類型",
			"type": "string",
			"default": "藝人",
			"description": "主要從事的演藝類型，會影響背景顏色，從「藝人」、「男藝人」、「女藝人」、「導演」、「編劇」、「攝影師」、「剪輯師」、「演員」、「男演員」、「女演員」、「節目主持」、「AV女優」、「童星」、「模特兒」、「配音員」、「播音員」、「新聞主播」、「舞者」、「魔術師」、「曲藝家」、「動作演員」、「傳媒工作者」、「幕後」、「歌手」、「男歌手」、「女歌手」、「組合」、「演奏者」、「傳統音樂」中任選其一。",
			"aliases": [ "类型", "type", "Background", "background", "背景" ],
                        "required": true
		},
		"圖片": {
			"label": "圖片",
			"type": "wiki-file-name",
			"description": "藝人的照片檔案名稱（完整檔案名字），例如Example.jpg。建議使用自由版權圖像。",
			"aliases": [ "图片", "圖像", "图像", "image", "imagename", "image_name", "Img" ]
		},
		"圖片尺寸": {
			"label": "圖片尺寸",
			"type": "string",
			"default": "220px",
			"description": "圖片尺寸，填寫格式：Npx。N字為一任意整數，不能為負數，意即將圖片的寬度設為N像素。預設值為220px。只於有圖片時有效，若依預設值縮放則不需填寫。",
			"aliases": [ "图片尺寸", "圖像大小", "图像大小", "image_size", "imagesize", "Img_size" ]
		},
		"補正": {
			"label": "圖片修正",
			"type": "string",
			"description": "在使用較寬、較短的（長方形）圖片時請填入「yes」，圖片的高度會被限制在 200 像素內（只於有圖片時有效）。",
			"aliases": [ "补正", "landscape", "Landscape" ]
		},
		"圖片替代": {
			"label": "圖片替代文字",
			"type": "string",
			"description": "圖片的替代文本（只於有圖片時有效）。",
			"aliases": [ "图片替代", "圖像替代", "图像替代", "alt", "Img_alt" ]
		},
		"圖片簡介": {
			"label": "圖片簡介",
			"type": "string",
			"description": "圖片說明（只於有圖片時有效）。",
			"aliases": [ "图片简介", "圖像説明", "图像说明", "caption", "image_caption", "imagecaption", "Img_capt" ]
		},
		"本名": {
			"label": "本名",
			"type": "string",
			"description": "真正、正式的名字。如果藝人的藝名和本名一樣，則此欄則可以略過。多於一個時請用「、」做分隔。",
			"aliases": [ "原名", "real_name", "realname", "Real_name", "full name" ]
		},
		"外文名": {
			"label": "外文名",
			"type": "string",
			"description": "根據其國家語系的名字，非拉丁字母系的外文名（如日文，韓文或俄文等）。",
			"aliases": [ "foreign_name", "foreignname", "native_name" ]
		},
		"外文": {
			"label": "外文語系",
			"type": "string",
			"description": "指明外文名之語系，以正確顯示文字（如日文、韓文、俄文等）。只於有外文名時有效。使用 ISO-639 語言代碼。",
			"aliases": [ "fnamelang", "native_name_lang" ]
		},
		"羅馬拼音": {
			"label": "羅馬拼音",
			"type": "string",
			"description": "非拉丁字母語系（如中文、日文、韓文、俄文等）的拉丁字母拼法。",
			"aliases": [ "罗马拼音", "romanized_name", "romanizedname" ]
		},
		"英文名": {
			"label": "英文名",
			"type": "string",
			"description": "英語名稱，或拉丁字母語系的名字。",
			"aliases": [ "english_name", "englishname" ]
		},
		"暱稱": {
			"label": "暱稱",
			"type": "string",
			"description": "經常出現在新聞媒體上的暱稱，多個暱稱時請用「、」做分隔，最多別超過五個。",
			"aliases": [ "昵称", "綽號", "绰号", "nickname", "Alias", "alias" ]
		},
		"其他藝名": {
			"label": "其他藝名",
			"type": "string",
			"description": "曾使用或在外地發展時所使用的藝名。",
			"aliases": [ "其他艺名", "別名", "别名", "other_name", "othername" ]
		},
		"國籍": {
			"label": "國籍",
			"type": "string",
			"description": "所屬國籍（國家）。若為團體請填寫團體的所屬國籍，請勿列出成員的所屬國籍。建議使用「{{國家地區模板}} 」，如{{CHN}}。",
			"aliases": [ "国籍", "nationality", "country" ]
		},
		"永久居留權": {
			"label": "永久居留權",
			"type": "string",
			"description": "永久居留權，僅在與國籍不同時填寫。",
			"aliases": [ "永久居留权", "permanent_residency", "permanent residency" ]
		},
		"民族": {
			"label": "民族",
			"type": "string",
			"description": "所屬民族。",
			"aliases": [ "people", "nation" ]
		},
		"籍貫": {
			"label": "籍貫",
			"type": "string",
			"description": "家鄉或籍貫。",
			"aliases": [ "籍贯", "hometown", "register" ]
		},
		"出生名": {
			"label": "出生名",
			"type": "string",
			"description": "出生名字。原則上視同本名，但本名未必是出生名。",
			"aliases": [ "birth_name", "birthname", "Birth_name" ]
		},
		"出生日期": {
			"label": "出生日期",
			"type": "string",
			"description": "出生日期。在世者使用{{Birth date and age}}模板，可自動計算並顯示出歲數。已過世者用{{birth date}}模板。未知完整出生日期者使用「YYYY年MM月DD日」的格式。",
			"aliases": [ "birth_date", "birthdate", "date_of_birth", "birth date", "Born" ]
		},
		"出生地點": {
			"label": "出生地點",
			"type": "string",
			"description": "出生地。可使用「{{國家地區模板}} 地區名」的格式。",
			"aliases": [ "出生地点", "出生地", "birth_place", "birthplace", "place_of_birth", "location" ]
		},
		"逝世日期": {
			"label": "逝世日期",
			"type": "string",
			"description": "逝世日期。格式同出生日期。",
			"aliases": [ "death_date", "deathdate", "date_of_death", "end date", "Died" ]
		},
		"逝世地點": {
			"label": "逝世地點",
			"type": "string",
			"description": "逝世地點。格式同出生地點。",
			"aliases": [ "逝世地点", "死亡地", "death_place", "deathplace", "place_of_death", "endplace" ]
		},
		"死因": {
			"label": "死因",
			"type": "string",
			"description": "逝世原因。",
			"aliases": [ "death_cause", "deathcause", "cause_of_death" ]
		},
		"墓地": {
			"label": "墓地",
			"type": "string",
			"description": "死者墓地或葬於、揚骨灰等的地點。",
			"aliases": [ "resting_place", "resting place", "restingplace" ]
		},
		"墓地座標": {
			"label": "墓地座標",
			"type": "string",
			"description": "墓地等的座標，使用{{Coord}}模板。",
			"aliases": [ "墓地坐標", "墓地坐标", "resting_place_coordinates", "resting place coordinates", "restingplacecoordinates" ]
		},
		"居住地": {
			"label": "居住地點",
			"type": "string",
			"description": "居住地點。格式同出生地點。僅在與出生地點不同時填寫。",
			"aliases": [ "residence" ]
		},
		"職業": {
			"label": "職業",
			"type": "string",
			"description": "所從事的演藝工作。非演藝相關的職業請勿列入。",
			"aliases": [ "职业", "occupation", "Occupation", "Occupations", "occupations" ]
		},
		"語言": {
			"label": "語言",
			"type": "string",
			"description": "請填寫能流暢溝通的語言或方言，多於一個時請用「、」做分隔。",
			"aliases": [ "语言", "language" ]
		},
		"教育程度": {
			"label": "教育程度",
			"type": "string",
			"description": "藝人的最高教育程度。若有多個高等教育學位可用{{Plainlist}}或{{Unbulleted list}}羅列。",
			"aliases": [ "education", "School_background" ]
		},
		"母校": {
			"label": "母校",
			"type": "string",
			"description": "藝人畢業或所就讀的院校，可加括號註明就讀院系、畢業時間等資訊。使用{{Plainlist}}或{{Unbulleted list}}羅列。",
			"aliases": [ "alma_mater", "almamater", "alma mater" ]
		},
		"宗教信仰": {
			"label": "宗教信仰",
			"type": "string",
			"description": "宗教信仰。",
			"aliases": [ "信仰", "religion" ]
		},
		"配偶": {
			"label": "配偶",
			"type": "string",
			"description": "配偶姓名，使用{{marriage}}模板。請勿填寫只是在交往中，沒有正式婚姻關係者。",
			"aliases": [ "spouse" ]
		},
		"兒女": {
			"label": "兒女",
			"type": "string",
			"description": "子女姓名。具相關知名度（通常是指有維基條目者）才建議列出。",
			"aliases": [ "儿女", "子女", "children", "child" ]
		},
		"父母": {
			"label": "父母",
			"type": "string",
			"description": "父母姓名。具相關知名度（通常是指有維基條目者）才建議列出。",
			"aliases": [ "parents" ]
		},
		"親屬": {
			"label": "親屬",
			"type": "string",
			"description": "兄弟姐妹或其他親屬姓名，並註明與藝人之關係。具相關知名度（通常是指有維基條目者）才建議列出。",
			"aliases": [ "亲属", "relatives", "relations" ]
		},
		"音樂類型": {
			"label": "音樂類型",
			"type": "string",
			"description": "主要演出或創作的音樂類型（適用於從事音樂的藝人）。列出較擅長或演出的類型即可。",
			"aliases": [ "音乐类型", "music_genre", "musicgenre", "Genre", "genre" ]
		},
		"演奏樂器": {
			"label": "演奏樂器",
			"type": "string",
			"description": "擅長的樂器（適用於從事音樂的藝人）。列出較擅長或演出的樂器即可。",
			"aliases": [ "演奏乐器", "instrument", "Instrument", "instruments" ]
		},
		"出道地點": {
			"label": "出道地點",
			"type": "string",
			"description": "出道的地點。格式同出生地點。",
			"aliases": [ "出道地点", "出身地", "origin_place", "originplace", "Origin", "origin" ]
		},
		"出道日期": {
			"label": "出道日期",
			"type": "string",
			"description": "正式宣布加入演藝圈的日期，或組合成立的日期。使用「YYYY年MM月DD日」的格式（以官方為準）。",
			"aliases": [ "debut_date", "debutdate" ]
		},
		"出道作": {
			"label": "出道作品",
			"type": "string",
			"description": "首部參與發表的作品、電影、戲劇、或專輯等。",
			"aliases": [ "出道作品", "debut_work", "debutwork" ]
		},
		"代表作": {
			"label": "代表作品",
			"type": "string",
			"description": "最為人熟悉的作品，可以是電影、電視節目、舞台劇或音樂專輯等。最多別超過五個。",
			"aliases": [ "代表作品", "famous_works", "famousworks", "famous_work", "famouswork" ]
		},
		"著名角色": {
			"label": "著名角色",
			"type": "string",
			"description": "演員演出最為人熟悉的角色（適用於從事電視/電影/舞台劇演出的藝人）。最多別超過五個。",
			"aliases": [ "出名角色", "notable_roles", "notableroles", "notable_role", "notablerole", "notable role" ]
		},
		"活躍年代": {
			"label": "活躍年代",
			"type": "string",
			"description": "活躍年代，即「出道（成立）年份 - 引退（逝世/解散）年份」。",
			"aliases": [ "活跃年代", "活動時期", "活动时期", "years_active", "yearsactive", "Years_active", "year_active", "yearactive", "year" ]
		},
		"唱片公司": {
			"label": "唱片公司",
			"type": "string",
			"description": "所屬的唱片公司。",
			"aliases": [ "label", "Label", "record_label", "recordlabel" ]
		},
		"經紀公司": {
			"label": "經紀公司",
			"type": "string",
			"description": "所屬的經紀公司。",
			"aliases": [ "经纪公司", "agent_company", "agentcompany", "Production" ]
		},
		"簽名": {
			"label": "簽名",
			"type": "wiki-file-name",
			"description": "藝人的簽名檔案名稱（完整檔案名字），例如Example.jpg。",
			"aliases": [ "签名", "signature" ]
		},
		"簽名大小": {
			"label": "簽名大小",
			"type": "string",
			"default": "150px",
			"description": "簽名尺寸，填寫格式：Npx。N字為一任意整數，不能為負數，意即將簽名的寬度設為N像素。預設值為150px。只於有簽名時有效，若依預設值縮放則不需填寫。",
			"aliases": [ "签名大小", "signature_size", "signature size" ]
		},
		"簽名替代": {
			"label": "簽名替代文字",
			"type": "string",
			"description": "簽名的替代文本（只於有簽名時有效）。",
			"aliases": [ "签名替代", "signature_alt", "signature alt" ]
		},
		"網站": {
			"label": "網站",
			"type": "string",
			"description": "由其個人或所屬公司經營、管理之一個主要的官方網站，其餘連結或是社群網站（如：Twitter、微博等）請放至外部連結。填寫格式：{{URL|www.example.com}}。",
			"aliases": [ "网站", "官方網站", "官方网站", "website", "homepage", "URL", "url" ]
		},
		"相關團體": {
			"label": "相關團體",
			"type": "string",
			"description": "曾經或現在所屬的組合或團體。",
			"aliases": [ "相关团体", "related_group", "relatedgroup", "Associated_acts", "associated_acts" ]
		},
		"module": {
			"label": "模組 1",
			"type": "content",
			"description": "用於嵌套其他信息框模板。",
			"aliases": [ "misc", "module1", "misc1" ]
		},
		"module2": {
			"label": "模組 2",
			"type": "content",
			"description": "用於嵌套其他信息框模板。",
			"aliases": [ "misc2" ]
		},
		"module3": {
			"label": "模組 3",
			"type": "content",
			"description": "用於嵌套其他信息框模板。",
			"aliases": [ "misc3" ]
		},
		"module4": {
			"label": "模組 4",
			"type": "content",
			"description": "用於嵌套其他信息框模板。",
			"aliases": [ "misc4" ]
		},
		"module5": {
			"label": "模組 5",
			"type": "content",
			"description": "用於嵌套其他信息框模板。",
			"aliases": [ "misc5" ]
		},
		"module6": {
			"label": "模組 6",
			"type": "content",
			"description": "用於嵌套其他信息框模板。",
			"aliases": [ "misc6" ]
		},
		"IMDb": {
			"label": "IMDb 資訊",
			"type": "string",
			"description": "在IMDb網路電影資料庫的資訊。請輸入藝人的相應 ID 編號，即網址http://www.imdb.com/name/nmXXXXXX/中XXXXXX的數值。",
			"aliases": [ "imdb" ]
		},
		"現任成員": {
			"label": "現任成員",
			"type": "string",
			"description": "若此條目為團體，請填入現在的成員，請用「*」羅列，可按加入時間依次排序。",
			"aliases": [ "现任成员", "current_members", "Current_members", "currentmembers" ]
		},
		"過往成員": {
			"label": "過往成員",
			"type": "string",
			"description": "若此條目為團體，請填入過往的成員，請用「*」羅列。若該團體已解散，請將所有成員填寫在「過往成員」欄位中，而不要放置在「現任成員」欄位中。",
			"aliases": [ "过往成员", "past_members", "Past_members", "pastmembers" ]
		},
		"著名樂器": {
			"label": "著名樂器",
			"type": "string",
			"description": "藝人專屬的特別定做樂器（適用於從事音樂的藝人）。",
			"aliases": [ "著名乐器", "notable_instruments", "Notable_instruments", "notableinstruments" ]
		},
		"academyawards": {
			"label": "奧斯卡金像獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的奧斯卡金像獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"cannesfilmawards": {
			"label": "坎城影展獲獎記錄",
			"type": "string",
			"description": "藝人在坎城影展上獲得的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"afiawards": {
			"label": "AFI電影獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的AFI電影獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"arielaward": {
			"label": "阿列爾獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的阿列爾獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"baftaawards": {
			"label": "英國電影學院獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的英國電影學院獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"cesarawards": {
			"label": "凱撒電影獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的凱撒電影獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"emmyawards": {
			"label": "艾美獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的艾美獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"filmfareawards": {
			"label": "印度電影觀眾獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的印度電影觀眾獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"geminiawards": {
			"label": "雙子座獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的雙子座獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"goldenglobeawards": {
			"label": "金球獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的金球獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"goldenraspberryawards": {
			"label": "金酸莓獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的金酸莓獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"goyaawards": {
			"label": "哥雅獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的哥雅獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"grammyawards": {
			"label": "葛萊美獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的葛萊美獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品}}。"
		},
		"hongkongfilmawards": {
			"label": "香港電影金像獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的香港電影金像獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"olivierawards": {
			"label": "勞倫斯奧利弗獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的勞倫斯奧利弗獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"iftaawards": {
			"label": "愛爾蘭電視電影獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的愛爾蘭電視電影獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"imageaward": {
			"label": "有色人種促進協會形象獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的有色人種促進協會形象獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"nationalfilmawards": {
			"label": "印度國家電影獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的印度國家電影獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"sagawards": {
			"label": "美國演員工會獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的美國演員工會獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。",
			"aliases": [ "screenactorsguildawards", "screenactorguildsawards" ]
		},
		"tonyawards": {
			"label": "東尼獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的東尼獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"goldenbauhiniaawards": {
			"label": "香港電影金紫荊獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的香港電影金紫荊獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"hkfcsawards": {
			"label": "香港電影評論學會大獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的香港電影評論學會大獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"asianfilmawards": {
			"label": "亞洲電影大獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的亞洲電影大獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"goldenhorseawards": {
			"label": "金馬獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的金馬獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"huabiaoawards": {
			"label": "華表獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的華表獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"goldenroosterawards": {
			"label": "金雞獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的金雞獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"hundredflowersawards": {
			"label": "百花獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的百花獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"goldeneagleawards": {
			"label": "金鷹獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的金鷹獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"flyingapsarasawards": {
			"label": "飛天獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的飛天獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"rthktop10goldsongsawards": {
			"label": "十大中文金曲頒獎音樂會獲獎記錄",
			"type": "string",
			"description": "藝人在十大中文金曲頒獎音樂會上獲得的獎項。填寫格式：{{獎項|獎項類別|年份|作品}}。"
		},
		"goldenmelodyawards": {
			"label": "金曲獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的金曲獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品}}。"
		},
		"mtvasiaawards": {
			"label": "MTV亞洲大獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的MTV亞洲大獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品}}。"
		},
		"ntsawards": {
			"label": "TVB全球華人新秀歌唱大賽名次",
			"type": "string",
			"description": "藝人在TVB全球華人新秀歌唱大賽上獲得的名次。填寫格式：年份 名次（冠軍/亞軍/其他）。"
		},
		"chinamusicawards": {
			"label": "中歌榜獲獎記錄",
			"type": "string",
			"description": "藝人在中歌榜上獲得的獎項。填寫格式：{{獎項|獎項類別|年份|作品}}。"
		},
		"goldenbellawards": {
			"label": "金鐘獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的金鐘獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"tvbanniversaryawards": {
			"label": "萬千星輝頒獎典禮獲獎記錄",
			"type": "string",
			"description": "藝人在萬千星輝頒獎典禮上獲得的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"magnoliaawards": {
			"label": "上海電視節白玉蘭獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的上海電視節白玉蘭獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"asiantvawards": {
			"label": "亞洲電視大獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的亞洲電視大獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"rainbowawards": {
			"label": "亞洲彩虹電視大獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的亞洲彩虹電視大獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"tokyofilmawards": {
			"label": "東京國際影展獲獎記錄",
			"type": "string",
			"description": "藝人在東京國際影展上獲得的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"yokohamafilmawards": {
			"label": "橫濱影展獲獎記錄",
			"type": "string",
			"description": "藝人在橫濱影展上獲得的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"japanacademyawards": {
			"label": "日本電影金像獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的日本電影金像獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"japanesefilmcreticsawards": {
			"label": "日本電影影評人大獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的日本電影影評人大獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"mainichifilmawards": {
			"label": "每日電影獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的每日電影獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"blueribbonawards": {
			"label": "藍絲帶獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的藍絲帶獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"hochifilmawards": {
			"label": "報知電影獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的報知電影獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"kinemajunpotop10awards": {
			"label": "電影旬報十佳獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的電影旬報十佳獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"grandbellawards": {
			"label": "大鐘獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的大鐘獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"bluedragonfilmawards": {
			"label": "青龍電影獎獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的青龍電影獎的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"paeksangartsawards": {
			"label": "百想藝術大賞獲獎記錄",
			"type": "string",
			"description": "藝人所獲得的百想藝術大賞的獎項。填寫格式：{{獎項|獎項類別|年份|作品|角色}}。"
		},
		"獎項": {
			"label": "獲得到的其他獎項",
			"type": "string",
			"description": "與其範疇相關的其他獎項，使用{{獎項}}模板。建議只放置全國性或國際性，為權威機構發放，且只與藝術表演有關的獎項。網路票選、搜尋排行、人氣排行、商業活動……等獎項不宜放置於此。",
			"aliases": [ "奖项", "awards", "award" ]
		},
		"嵌入": {
			"label": "嵌入",
			"type": "string",
			"description": "如果要將本模板嵌入到其他信息框中使用，請將此項設為「yes」。",
			"aliases": [ "embed" ]
		}
	},
	"format": "block"
}
</templatedata>
{{hidden end}}

== 微格式 ==
{{UF-hcard-person}}

== 參看 ==
*{{Tl|AV女優}}
*{{Tl|Infobox model}}
*{{Tl|Infobox comedian}}
*{{Tl|配音員}}
*{{Tl|Infobox AKB48 member}}／{{Tl|Infobox Sakamichi-series member}}

=== 支援模板 ===
*{{tl|藝人/color selector}}
*{{tl|藝人/hCard class}}
*{{tl|藝人/lang selector}}
*{{tl|藝人/title return}}
*{{tl|藝人/tracking}}
*{{tl|藝人/type return}}

=== 追蹤分類 ===
使用本模板的條目可從以下隱藏分類追蹤：
*{{clc|使用未知参数的艺人信息框}}－含有未知參數名（如血型、身高、體重、三圍等）的藝人信息框。
*{{clc|缺少或含有无效类型字段的艺人信息框}}－「類型」欄位未填，或填寫了無效值（如「偶像歌手」、「爵士樂樂手」等）的藝人信息框。
*{{clc|网站格式不正确的艺人条目}}－含有錯誤的網站填寫格式的藝人信息框。
*{{clc|在艺人信息框中使用作品列表变量的页面}}－含有已廢除的作品列表欄位（音樂專輯、電影、主持節目、電視劇、廣播劇、舞台劇、書籍）的藝人信息框，可能需要將相應資訊整理到條目中。
*{{clc|使用教育程度参数的艺人信息框}}－含有「教育程度」欄位的藝人信息框，可能需要將其中的部分資訊轉入「母校」欄位。

=== 使用維基數據資源的版本 ===
* {{tl|藝人ii}}
* {{tl|藝人/WD}}
* {{tl|藝人/Wikidata}}

{{Film and Television related infobox templates}}

<includeonly>{{#ifeq:{{SUBPAGENAME}}|sandbox | |
<!-- 請在下面加入模板分類 -->
[[Category:人物信息框模板|文化]]
[[Category:电影信息框模板|人物]]
[[Category:电视信息框模板|人物]]
[[Category:音乐信息框模板|人物]]
}}</includeonly>