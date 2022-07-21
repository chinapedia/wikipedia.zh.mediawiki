<includeonly>-{T|zh-cn:模板:电视节目信息框; zh-tw:模板:電視節目資訊框;}-{{High-use|13924}}{{esoteric}}</includeonly><noinclude>{{Template_doc_page_viewed_directly}}</noinclude>-{H|zh-cn:信息; zh-tw:資訊;}--{H|zh-cn:视频; zh-tw:視訊;}--{H|zh-cn:音频; zh-tw:音訊;}--{H|zh-cn:字体颜色;zh-tw:文字顏色;}--{H|zh-cn:默认;zh-tw:預設;}--{H|zh-cn:文件;zh-tw:檔案;}-
<!-- 請在這條線之下編輯模板的說明文件 -->
{{Pnex
| 颜色 = #C6C9FF | 字体颜色 = black | 名称 | 英文名称 | 图片 = Example image not to be used in article namespace.jpg | 尺寸 = 220px | 圖說 | 别名 | 類型 | 格式 | 原作 | 開創 | 開發 | 編劇 | 總導演 | 導演 | 助理導演 | 創意總監 | 主持 | 聯合主持 | 主演 | 評審 | 配音 | 旁白 | 國家 = {{{國家}}}（{{{地區}}}） | 語言 | 字幕 | 標語 | 季數 = {{{季數}}}<br />（{{{集數}}} / {{{系列數}}}） | 集數 | 每集列表 = {{FULLPAGENAME}} | 每集長度 | 配樂 | 主題曲 | 片頭曲 | 作曲 | 作詞 | 演唱 | 片尾曲 | 作曲2 | 作詞2 | 演唱2 | 插曲| 製作年份 | 制片人 | 共同製片人 | 出品人 | 總監制 | 監製 | 執行製作 | 共同執行製作 | 顧問 | 故事 | 編審 | 剪輯 | 外景 | 攝影 | 機位 | 製作公司 | 發行公司 | 發行許可 | 預算 | 電視網 = {{{电视网}}}（{{{电视台}}} / {{{频道}}}） | 图像制式 | 声音制式 | 播出国家 = {{{播出国家}}}<br />（{{{播出地区}}}） | 集数0 | 每集长度0 | 开始 | 结束 = {{{结束}}}<br />（{{{播出日期}}}） | 播出时间 | 电视网1 = {{{电视网1}}}（{{{电视台1}}} / {{{频道1}}}） | 图像制式1 | 声音制式1 | 播出国家1 = {{{播出国家1}}}<br />（{{{播出地区1}}}） | 集数1 | 每集长度1 | 开始1 | 结束1 = {{{结束1}}}<br />（{{{播出日期1}}}） | 播出时间1 | module4 = 上面的数字最多可到6 | 前作 | 续作 | 相关节目 | 中国大陆名称 | 台湾名称 | 港澳名称 | 新加坡名称 | 马来西亚名称 | 日本名称 | 韩国名称 | 泰国名称 | 越南名称 | 官方网站 = http://www.example.com/ | 制作网站 = http://www.example.com/ | imdb_id | tv_com_id 
}}
此模板由原'''{{tl|影集資訊}}'''和'''{{tl|Infobox television}}'''两个模板合并而成，能同时兼容两者的参数，并能直接套用英文维基'''<nowiki>{{</nowiki>[[:en:Template:Infobox television|Infobox television]]<nowiki>}}</nowiki>'''的模板参数。使用时可自由采用[[简体中文]]或[[繁体中文]]，但请不要在同一参数中混用，以避免不能识别的现象发生。例如：
{| style="background: transparent;"
|style="vertical-align:top;"|<pre>{{电视节目-{zh-cn:信息; zh-tw:資訊;}-框
  | -{名称}- = 越狱
  | -{圖片}- = Example.png
  | -{圖说}- = 由於「[[合理使用]]」規範，範例中使用示例图片
  ……
</pre>
|style="vertical-align:top;"|<pre>

//“-{名称}-”二字使用简体中文，正确
//“-{圖片}-”二字使用繁体中文，亦正确
//“-{圖}-”字使用繁体中文，但“-{说}-”字使用了简体中文，这样将无法识别

</pre>
|}

== 实现机理 ==
在2007年8月底，此模板进行了一次更新，修改了原有的识别繁简英参数的实现方法。在新的版本中，模板的核心内容与繁简英参数识别进行了分离。核心内容由'''{{tnull|电视节目信息框/core}}'''处理，繁简英参数识别由此模板进行。

自2012年9月4日起，此模板不再使用'''{{tnull|电视节目信息框/core}}'''，核心内容与繁简英参数识别均由此模板直接进行。

== 使用方式 ==
'''注：本模板适用于电视剧、综艺节目、选秀比赛等在电视上播出的节目，由于参数众多，请将使用不到的参数删去'''
{| style="background:transparent; font-size:9pt"
|style="vertical-align:top;"|<pre>-{zh;zh-hans;zh-hant;zh-cn;zh-tw;zh-hk|{{电视节目信息框
| 颜色      = 
| 字体颜色  = 
| 名称      = 
| 英文名称  = 
| 图片      = 
| 尺寸      = 
| 图说      = 
| 别名      = 
| 类型      = 
| 格式      = 
| 原作      = 
| 开创      = 
| 开发      = 
| 编剧      = 
| 总导演    = 
| 导演      = 
| 助理导演  = 
| 创意总监  = 
| 主持      = 
| 联合主持  = 
| 主演      = 
| 评委      = 
| 配音      = 
| 旁白      = 
| 国家      = 
| 语言      = 
| 字幕      = 
| 标语      = 
| 季数      = 
| 集数      = 
| 每集列表  = 
| 每集长度  = 
| 配乐      = 
| 主题曲    = 
| 片头曲    = 
| 作曲      = 
| 作词      = 
| 演唱      = 
| 片尾曲    = 
| 作曲2     = 
| 作词2     = 
| 演唱2     = 
| 插曲      = 
| 制作年份  = 
| 制片人    = 
| 共同制片人 = 
| 出品人    = 
| 总监制    = 
| 监制      = 
| 执行制作  = 
| 共同执行制作 = 
<!-- | 副制作人  =  -->
| 顾问标签  = 
| 顾问      = 
| 故事标签  = 
| 故事      = 
| 编审      = 
| 剪辑      = 
| 外景      = 
| 摄影      = 
| 机位      = 
| 制作公司  = 
| 发行公司  = 
| 发行许可  = 
| 预算      = 
| 电视网    = 
| 图像制式  = 
| 声音制式  = 
| 播出国家  = 


| 集数0     = 
| 每集长度0 = 
| 开始      = 
| 结束      = 
<!-- | 播出日期  =  -->
| 播出时间  = 
| 电视网1   = 
| 图像制式1 = 
| 声音制式1 = 
| 播出国家1 = 
| 集数1     = 
| 每集长度1 = 
| 开始1     = 
| 结束1     = 
| 播出时间1 = 
| 前作      = 
| 续作      = 
| 相关节目  = 
| 中国大陆名称 = 
| 台湾名称  = 
| 港澳名称  = 
| 新加坡名称  = 
| 马来西亚名称 = 
| 日本名称  = 
| 韩国名称  = 
| 泰国名称  = 
| 越南名称  = 
| 官方网站  = 
| 制作网站  = 
| imdb_id   = 
| tv_com_id = 
}}}-</pre>

|style="vertical-align:top;"|<pre>
-{zh;zh-hans;zh-hant;zh-cn;zh-tw;zh-hk|{{Infobox television
| bgcolour      = 
| colour text   = 
| show_name     = 
| eng_name      = 
| image         = 
| image_size    = 
| caption       = 
| show_name_2   = 
| genre         = 
| format        = 
| based_on      = 
| creator       = 
| developer     = 
| writer        = 
| general_director = 
| director      = 
| assistance_director = 
| creative_director  = 
| presenter     = 
| cohost        = 
| starring      = 
| judges        = 
| voices        = 
| narrated      = 
| country       = 
| language      = 
| subtitle      = 
| slogan        = 
| num_seasons   = 
| num_episodes  = 
| list_episodes = 
| runtime       = 
| theme_music_composer = 
| theme_song    = 
| opentheme     = 
| composer      = 
| lyricist      = 
| singer        = 
| endtheme      = 
| composer_2    = 
| lyricist_2    = 
| singer_2      = 
| interlude     = 
| produce_year  = 
| producer      = 
| co-producer   = 
| program_presenter = 
| senior_producer = 
| supervising_producer = 
| executive_producer = 
| co_exec       = 
<!-- | asst_producer =  -->
| consultant_label = 
| consultant    = 
| story_label   = 
| story         = 
| story_editor  = 
| editor        = 
| location      = 
| cinematography = 
| camera        = 
| company       = 
| distributor   = 
| nrta_id       = 
| budget        = 
| network       = 
| picture_format = 
| audio_format  = 
| first_run     = 


| num_episodes_0 = 
| runtime_0     = 
| first_aired   = 
| last_aired    = 
<!-- | aired  =  -->
| aired_time    = 
| network_1     = 
| picture_format_1 = 
| audio_format_1 = 
| first_run_1   = 
| num_episodes_1 = 
| runtime_1     = 
| first_aired_1 = 
| last_aired_1  = 
| aired_time_1  = 
| preceded_by   = 
| followed_by   = 
| related       = 
| show_name_zh-cn = 
| show_name_zh-tw = 
| show_name_zh-hk = 
| show_name_zh-sg = 
| show_name_zh-my = 
| show_name_zh-jp = 
| show_name_zh-kr = 
| show_name_zh-th = 
| show_name_zh-vi = 
| website       = 
| production_website = 
| imdb_id       = 
| tv_com_id     = 
}}}-</pre>

|style="vertical-align:top;white-space:nowrap;"|<pre>
-{zh;zh-hans;zh-hant;zh-cn;zh-tw;zh-hk|
每栏的背景颜色，使用RGB32位色或标准颜色代码，，亦可写为「背景颜色」
每栏的字体颜色，同上，若不填则使用默认颜色
节目的中文名称，如果没填则会以条目名代替
中文节目的英文名称或非中文节目的外文原名，亦可写为「original_name、原名」。若为拉丁字母文字，建议手动加斜体标示
节目图片，直接填入文件名即可，亦可写为「图像」
图片大小，如250px
图片说明文字
该节目的其他名称，亦可写为「又名」
电视剧的类型，如古装剧、民国剧、都市剧等，亦可写为「分类」
节目的形式，如电视剧、综艺节目、选秀比赛等
節目的原作，如改編來源、電視劇的原著、原著作家等
节目的开创者
节目的开发者，亦可写为「发展」
电视剧的编剧
节目的总导演
节目的导演
节目的助理导演
创意类节目的创意总监
节目的主持人，亦可写为「host」
在节目的主持团中，用来辅助主持人完成主持任务的人员
节目的演出人员，如电视剧的主演、选秀比赛的参赛选手等，亦可写为「演出」
选秀类节目的评委，亦可写为「评判」
节目的配音演员
节目的幕后旁白
制作该节目的国家和地区，由制作、出品公司所在的国家/地区决定，可使用{{CHNML}}等国家模板，亦可写为「地区」
原节目所使用的语言
原节目的字幕文字
节目的标语、宣传语
美剧的季度数目，港剧请写为「num_collections、辑数」，英剧请写为「num_series、系列数」，三选一
节目的集数，亦可写为「original_num_episodes、原集数、原版集数」
详细列出每集节目的列表条目名称，不可在未填写「集数」的情况下使用该参数
每集节目的时间长度，亦可写为「每集长」
主题曲或节目主要配乐的作曲者或製作公司，亦可写为「主题作曲家、配乐作曲」
主题曲或主题音乐名称，亦可写为「theme_music、主题音乐」
节目片头曲名称
片头曲作曲者，亦可写为「composers」
片头曲作词者，亦可写为「填词」
片头曲演唱者，若前面使用了“演唱者《片头曲》”的格式，则可省略该参数，亦可写为「主唱」
节目片尾曲名称
片尾曲作曲者
片尾曲作词者，亦可写为「填词2」
片尾曲演唱者，同上，亦可写为「主唱2」
节目的插曲名称
拍摄、制作该节目的年份，亦可写为「拍摄年份」
节目的制片人，亦可写为「制作人」
节目的共同制片人，亦可写为「共同制作人、联合制片人、联合制作人」
节目的出品人（中国大陸特有的职位，如果为非中国大陸作品则留空）
节目的总监制
节目的监制
节目的执行制片人
节目的共同执行制片人
亦可写为「associate_producer」（由于副制作人的概念有些模糊，故暂时隐藏该参数）
用来显示剧中的亦称
节目的顾问或制作顾问，亦可写为「consulting_producer、制作顾问」
用来显示剧中的亦称
节目的故事创作
故事的编审
节目的剪辑师、剪輯公司，亦可写为「剪接」
节目的外景拍摄地，亦可写为「拍摄地」
节目的摄影指导
摄像的机位，分为单机位和多机位
制作、出品该节目的公司
发行该节目的公司
发行许可证号（中国大陆地区播映之电视剧、动画片、理论文献影视片专用）
节目的预算，包括制作、宣发成本
节目的首播频道，不包括重播、转播或網路同步跟播，亦可写为「TV_station、电视台、channel、频道」
首播频道的图像制式，如黑白、宽屏幕、NTSC 480i、HDTV 1080i等，亦可写为「视频制式」
首播频道的声音制式，如单声道、立体声等，亦可写为「音频制式」
首播频道所在的国家和地区，可使用{{CHNML}}等国家模板，亦可写为「播出地区、首播国家、首播地区」。以下两种情况应省略该参数：
1.节目只在一个国家/地区播出，且与制作国家/地区相同
2.节目虽在多个国家/地区播出，但在频道名称前已经使用了{{CHNML}}之类的国家模板
首播频道的节目集数，若與上方集數相同，則可省略該參數
首播频道的节目时长，若與上方時長相同，則可省略該參數，亦可写为「每集长0」
首播频道的首集播出日期，可使用{{Start date}}模板
首播频道的末集播出日期，可使用{{End date}}模板
对于季播的电视节目或系列电视剧，如节目已播出多季，则应用「播出日期」替代上述两参数
首播频道的播出时间
其他国家和地区的首播频道，亦可写为「TV_station_1、电视台1、channel_1、频道1」，编号最多可到6
其他频道的图像制式，同上，亦可写为「视频制式1」
其他频道的声音制式，同上，亦可写为「音频制式1」
其他频道所在的国家和地区，同上，亦可写为「播出地区1、首播国家1、首播地区1」
其他频道的节目集数，同上
其他频道的节目时长，同上，亦可写为「每集长1」
其他频道的首集播出日期，同上
其他频道的末集播出日期，同上
其他频道的播出时间，同上
系列节目的前作，亦可写为「晚于、后于」
系列节目的续作，亦可写为「早于、先于」
相关的节目，有多个节目时请用<br />换行，亦可写为「相关剧集、相关」
节目的中国大陆名称，繁简转换已经自动消歧义，请不要在文字间插入“-&#123;&#125;-”
节目的台湾名称，同上
节目的港澳名称，同上
节目的新加坡名称，同上
节目的马来西亚名称，同上
节目的日本名称，同上
节目的韩国名称，同上
节目的泰国名称，同上
节目的越南名称，同上
节目的官方网站，仅填入网址即可，亦可写为「网站」
节目的制作网站，仅填入网址即可
节目在IMDb的编号
节目在TV.com的编号

}-</pre>
|}
{{-}}

== 使用範例 ==
{{Infobox Television
| bgcolour                = #EEDFDA
| show_name               = 醉後決定愛上你
| original_name           = ''Love You''<!--SET-->／''While We Were Drunk''<!--TVB-->
| image                   = Poster_not_available.jpg
| caption                 = 基于“合理使用”原则，范例中显示示例图片
| genre                   = [[偶像劇]]
| writer                  = {{Nowrap begin}}陸亦華{{、w}}簡佑玶{{、w}}孫向妘{{、w}}陳泰霖{{Nowrap end}}
| director                = [[陳銘章]]
| starring                = [[張孝全]]、[[楊丞琳]]、[[許瑋甯]]<BR>[[黃鴻升]]、[[白梓軒]]、[[王傳一]]
| country                 = {{ROC-TW}}
| language                = 依劇情混用[[臺灣話|台語]]、[[中華民國國語|國語]]語言
| slogan                  = '''管他誤打又誤撞，我只相信愛最大！'''
| num_episodes            = 18集
| runtime                 = 90分鐘（含廣告）
| list_episodes           = #台視首播收視率
| theme_music_composer    = 席裕龍
| opentheme               = [[MP魔幻力量]]《不按牌理出牌》
| endtheme                = [[嚴爵]]《好的事情》
| producer                = 隋愛朋
| supervising_producer    = 劉思銘、陳泰霖
| executive_producer      = 謝辰陽
| story_label             = 原創故事
| story                   = 蘇麗媚
| editor                  = 林姿嫻、黃郁馨
| location                = {{TWN}}
| cinematography          = 陳世嶧
| company                 = [[夢田文創|夢田影像股份有限公司]]
| channel                 = [[台視主頻|台視]]
| picture_format          = [[標準畫質電視]]
| audio_format            = [[立體聲]]
| first_run               = {{TWN}}
| first_aired             = {{Nowrap end}}{{start date|2011|4|17}}
| last_aired              = {{end date|2011|8|14}}{{Nowrap end}}
| channel_1               = [[三立都會台]]
| picture_format_1        = [[標準畫質電視]]
| audio_format_1          = [[立體聲]]
| first_run_1             = {{TWN}}
| first_aired_1           = {{Nowrap end}}{{start date|2011|4|23}}
| last_aired_1            = {{end date|2011|8|20}}{{Nowrap end}}
| channel_2               = [[星和都會台]]
| picture_format_2        = [[標準畫質電視]]
| runtime_2               = 90分鐘（含廣告）<BR>75分鐘（第13－18集）
| audio_format_2          = [[立體聲]]
| first_run_2             = {{SGP}}
| first_aired_2           = {{Nowrap begin}}{{start date|2011|6|26}}
| last_aired_2            = {{end date|2011|10|23}}{{Nowrap end}}
| channel_3               = [[煲劇1台|無綫劇集台]]
| picture_format_3        = [[標準畫質電視]]
| audio_format_3          = [[立體聲]]
| first_run_3             = {{HKG}}
| num_episodes_3          = 30集
| runtime_3               = 45分鐘
| first_aired_3           = {{Nowrap begin}}{{start date|2011|7|17}}
| last_aired_3            = {{end date|2011|10|23}}{{Nowrap end}}
| channel_4               = [[公視HD台|HiHD頻道]]
| picture_format_4        = [[高清电视|-{zh-tw:高畫質電視;zh-hant:高清電視;zh-hans:高清电视}-]]
| audio_format_4          = [[立體聲]]
| first_run_4             = {{TWN}}
| num_episodes_4          = 30集
| runtime_4               = 60分鐘
| first_aired_4           = {{Nowrap begin}}{{start date|2011|12|26}}
| last_aired_4            = {{end date|2012|2|10}}{{Nowrap end}}
| channel_5               = [[BS富士]]
| picture_format_5        = [[高清电视|-{zh-tw:高畫質電視;zh-hant:高清電視;zh-hans:高清电视}-]]
| audio_format_5          = [[立體聲]]
| first_run_5             = {{JPN}}
| num_episodes_5          = 30集
| runtime_5               = 60分鐘
| first_aired_5           = {{Nowrap begin}}{{start date|2012|2|8}}
| last_aired_5            = {{end date|2012|9|5}}{{Nowrap end}}
| preceded_by             = [[國民英雄]]
| followed_by             = [[小資女孩向前衝]]
| related                 = [[命中注定我愛你]]、[[真心請按兩次鈴]]
| website                 = http://www.ttv.com.tw/drama11/drunk/index.htm 台視
| imdb_id                 = 2473936
}}

{| style="background: transparent;"
<pre style="overflow:auto;">-{zh;zh-hans;zh-hant;zh-cn;zh-tw|
{{電視節目資訊框
| 顏色       = #EEDFDA
| 名稱       = 醉後決定愛上你
| 英文名稱   = ''Love You'／''While We Were Drunk''
| 圖片       = Poster_not_available.jpg
| 圖說       = 基于“合理使用”原则，范例中显示示例图片
| 類型       = [[偶像劇]]
| 編劇       = 陸亦華、簡佑玶、孫向妘、陳泰霖
| 導演       = [[陳銘章]]
| 主演       = [[張孝全]]、[[楊丞琳]]、[[許瑋甯]]<BR>[[黃鴻升]]、[[白梓軒]]、[[王傳一]]
| 國家       = {{ROC-TW}}
| 語言       = 依劇情混用[[臺灣話|台語]]、[[中華民國國語|國語]]語言
| 標語       = '''管他誤打又誤撞，我只相信愛最大！'''
| 集數       = 18集
| 每集長度   = 90分鐘（含廣告）
| 每集列表   = #台視首播收視率
| 配樂       = 席裕龍
| 片頭曲     = [[MP魔幻力量]]《不按牌理出牌》
| 片尾曲     = [[嚴爵]]《好的事情》
| 製作人     = 隋愛朋
| 監製       = 劉思銘、陳泰霖
| 執行製作   = 謝辰陽
| 故事標籤   = 原創故事
| 故事       = 蘇麗媚
| 剪輯       = 林姿嫻、黃郁馨
| 外景       = {{TWN}}
| 攝影       = 陳世嶧
| 製作公司   = [[夢田影像股份有限公司]]
| 頻道       = [[台視]]
| 圖像制式   = [[標準畫質電視]]
| 聲音制式   = [[立體聲]]
| 播出國家   = {{TWN}}
| 開始       = {{start date|2011|4|17}}
| 結束       = {{end date|2011|8|14}}
| 頻道1      = [[三立都會台]]
| 圖像制式1  = [[標準畫質電視]]
| 聲音制式1  = [[立體聲]]
| 播出國家1  = {{TWN}}
| 開始1      = {{start date|2011|4|23}}
| 結束1      = {{end date|2011|8|20}}
| 頻道2      = [[星和都會台]]
| 圖像制式2  = [[標準畫質電視]]
| 每集長度2  = 90分鐘（含廣告）<BR>75分鐘（第13－18集）
| 聲音制式2  = [[立體聲]]
| 播出國家2  = {{SGP}}
| 開始2      = {{start date|2011|6|26}}
| 結束2      = {{end date|2011|10|23}}
| 頻道3      = [[無綫劇集台]]
| 圖像制式3  = [[標準畫質電視]]
| 聲音制式3  = [[立體聲]]
| 播出國家3  = {{HKG}}
| 集數3      = 30集
| 每集長度3  = 45分鐘
| 開始3      = {{start date|2011|7|17}}
| 結束3      = {{end date|2011|10|23}}
| 頻道4      = [[HiHD頻道]]
| 圖像制式4  = [[高畫質電視]]
| 聲音制式4  = [[立體聲]]
| 播出國家4  = {{TWN}}
| 集數4      = 30集
| 每集長度4  = 60分鐘
| 開始4      = {{start date|2011|12|26}}
| 結束4      = {{end date|2012|2|10}}
| 頻道5      = [[BS富士]]
| 圖像制式5  = [[高畫質電視]]
| 聲音制式5  = [[立體聲]]
| 播出國家5  = {{JPN}}
| 集數5      = 30集
| 每集長度5  = 60分鐘
| 開始5      = {{start date|2012|2|8}}
| 結束5      = {{end date|2012|9|5}}
| 前作       = [[國民英雄]]
| 續作       = [[小資女孩向前衝]]
| 相關節目   = [[命中注定我愛你]]、[[真心請按兩次鈴]]
| 官方網站   = http://www.ttv.com.tw/drama11/drunk/index.htm 台視
| imdb_id    = 2473936
}}
}-</pre>
|}

== 模板数据 ==
{{hidden begin|border=#aaa solid 1px;overflow:auto;width:auto;|titlestyle=text-align:center;|title=模板数据|bg=#F0F2F5}}
{{TemplateDataHeader}}
<templatedata>
{
	"description": "提供电视节目基本信息的信息框",
	"format": "block",
	"params": {
		"颜色": {
			"description": "如有特殊需要，可改变各栏标题的背景颜色。使用RGB32位色或标准颜色代码，如果不填则使用默认颜色。",
			"label": "颜色",
			"aliases": [
				"bgcolour",
				"bgcolor",
				"背景颜色",
				"背景顔色",
				"colour",
				"color",
				"顏色"
			],
			"type": "string"
		},
		"字体颜色": {
			"description": "如有特殊需要，可改变各栏标题的字体颜色。使用RGB32位色或标准颜色代码，如果不填则使用默认颜色。",
			"label": "字体颜色",
			"aliases": [
				"colour text",
				"color text",
				"文字顏色"
			],
			"type": "string"
		},
		"名称": {
			"description": "节目的中文名称，请使用官方授权翻译认可之中文名称，如果不填则会以条目名代替。若无官方授权之翻译名称，请使用常见的名称。",
			"label": "名称",
			"aliases": [
				"show_name",
				"名稱"
			],
			"default": "{{PAGENAMEBASE}}",
			"suggested": true,
			"type": "string"
		},
		"英文名称": {
			"description": "中文节目的英文名称，或非中文节目的外文原名。若为拉丁字母文字，建议手动加斜体标示。",
			"label": "英文名称",
			"aliases": [
				"eng_name",
				"英文名稱",
				"original_name",
				"原名"
			],
			"type": "string"
		},
		"图片": {
			"description": "与节目相关的图片，最常使用的是节目片头标志的截图。其他适当的图片包括宣传海报、节目标志等。",
			"label": "图片",
			"aliases": [
				"image",
				"圖片",
				"图像",
				"圖像"
			],
			"type": "wiki-file-name"
		},
		"尺寸": {
			"description": "图片尺寸，填写格式：Npx。N字为一任意整数，不能为负数，意即将图片的宽度设为N像素。默认值为220px。只于有图片时有效，若依默认值缩放则不需填写。",
			"label": "图片尺寸",
			"aliases": [
				"image_size"
			],
			"default": "220px",
			"type": "string"
		},
		"图说": {
			"description": "图片的说明文字，例如：《六人行》的标题卡；或：《长假》的宣传海报。",
			"label": "图片简介",
			"aliases": [
				"caption",
				"圖說"
			],
			"type": "string"
		},
		"别名": {
			"description": "该节目的其他名称。",
			"label": "别名",
			"aliases": [
				"show_name_2",
				"別名",
				"又名"
			],
			"type": "string"
		},
		"类型": {
			"description": "电视剧的类型，如古装剧、民国剧、都市剧等。",
			"label": "类型",
			"aliases": [
				"genre",
				"類型",
				"分类",
				"分類"
			],
			"suggested": true,
			"type": "string"
		},
		"格式": {
			"description": "节目的形式，如电视剧、综艺节目、选秀比赛等。",
			"label": "格式",
			"aliases": [
				"format"
			],
			"type": "string"
		},
		"原作": {
			"description": "节目的原作，如改编来源、电视剧的原著、原著作家等。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "原作",
			"aliases": [
				"based_on",
				"原创者",
				"原創者",
				"原著",
				"原创",
				"原創"
			],
			"type": "string"
		},
		"开创": {
			"description": "节目的开创者。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "开创",
			"aliases": [
				"creator",
				"開創"
			],
			"type": "string"
		},
		"开发": {
			"description": "节目的开发者。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "开发",
			"aliases": [
				"developer",
				"開發",
				"發展",
				"发展"
			],
			"type": "string"
		},
		"编剧": {
			"description": "电视剧的编剧。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "编剧",
			"aliases": [
				"writer",
				"編劇"
			],
			"type": "string"
		},
		"总导演": {
			"description": "节目的总导演。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "总导演",
			"aliases": [
				"general_director",
				"總導演"
			],
			"type": "string"
		},
		"导演": {
			"description": "节目的导演。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "导演",
			"aliases": [
				"director",
				"導演"
			],
			"type": "string"
		},
		"助理导演": {
			"description": "节目的助理导演。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "助理导演",
			"aliases": [
				"assistance_director",
				"助理導演"
			],
			"type": "string"
		},
		"创意总监": {
			"description": "创意类节目的创意总监。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "创意总监",
			"aliases": [
				"creative_director",
				"創意總監"
			],
			"type": "string"
		},
		"主持": {
			"description": "节目的主持人。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "主持人",
			"aliases": [
				"presenter",
				"host"
			],
			"type": "string"
		},
		"联合主持": {
			"description": "在节目的主持团中，用来辅助主持人完成主持任务的人员。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "联合主持",
			"aliases": [
				"cohost",
				"聯合主持"
			],
			"type": "string"
		},
		"主演": {
			"description": "节目的演出人员，如电视剧的主演、选秀比赛的参赛选手等。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "主演",
			"aliases": [
				"starring",
				"演出"
			],
			"type": "string"
		},
		"评委": {
			"description": "选秀类节目的评委。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "评委",
			"aliases": [
				"judges",
				"评判",
				"評判",
				"評委"
			],
			"type": "string"
		},
		"配音": {
			"description": "节目的配音演员。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "配音",
			"aliases": [
				"voices"
			],
			"type": "string"
		},
		"旁白": {
			"description": "节目的幕后旁白。当需列出多个人名时，可使用 Template:Plainlist。",
			"label": "旁白",
			"aliases": [
				"narrated"
			],
			"type": "string"
		},
		"国家": {
			"description": "制作该节目的国家和地区，由制作、出品公司所在的国家/地区决定。",
			"label": "制作国家或地区",
			"aliases": [
				"country",
				"國家",
				"地区",
				"地區"
			],
			"type": "string"
		},
		"语言": {
			"description": "节目所使用的语言，除非必要，请不要在此列出节目在原制作国家或地区外发行时的翻译语言版本。",
			"label": "语言",
			"aliases": [
				"language",
				"語言"
			],
			"type": "string"
		},
		"字幕": {
			"description": "如原始节目播出时有提供字幕（隐藏式字幕（CC）除外），可在此标示字幕所使用的语言，除非必要，请不要在此列出节目在原制作国家或地区外发行时的翻译语言版本。",
			"label": "字幕",
			"aliases": [
				"subtitle"
			],
			"type": "string"
		},
		"标语": {
			"description": "节目的标语、宣传语。",
			"label": "标语",
			"aliases": [
				"slogan",
				"標語"
			],
			"type": "string"
		},
		"季数": {
			"description": "适用于美国电视节目。该节目目前为止所播出的总季数。",
			"label": "季数",
			"aliases": [
				"num_seasons",
				"季數"
			],
			"type": "string"
		},
		"辑数": {
			"description": "适用于香港电视节目。该节目目前为止所播出的总辑数。",
			"label": "辑数",
			"aliases": [
				"num_collections",
				"輯數"
			],
			"type": "string"
		},
		"系列数": {
			"description": "适用于英国电视节目。该节目目前为止所播出的总系列数。",
			"label": "系列数",
			"aliases": [
				"num_series",
				"系列數"
			],
			"type": "string"
		},
		"集数": {
			"description": "节目的集数。",
			"label": "集数",
			"aliases": [
				"num_episodes",
				"集數",
				"原集数",
				"原集數",
				"原版集数",
				"原版集數",
				"original_num_episodes"
			],
			"type": "string"
		},
		"每集列表": {
			"description": "详细列出每集节目的列表条目名称，不可在未填写“集数”的情况下使用该参数。",
			"label": "每集列表",
			"aliases": [
				"list_episodes"
			],
			"type": "string"
		},
		"每集长度": {
			"description": "每集节目的时间长度。若各集节目长度不一，请填入最短和最长的时间，例如“ 30－45分”。",
			"label": "每集长度",
			"aliases": [
				"runtime",
				"每集長度",
				"每集长",
				"每集長"
			],
			"type": "string"
		},
		"配乐": {
			"description": "主题曲或节目主要配乐的作曲者或制作公司。",
			"label": "配乐",
			"aliases": [
				"theme_music_composer",
				"主题作曲家",
				"主題作曲家",
				"配樂",
				"配乐作曲",
				"配樂作曲"
			],
			"type": "string"
		},
		"主题曲": {
			"description": "主题曲或主题音乐名称。",
			"label": "主题曲",
			"aliases": [
				"theme_song",
				"theme_music",
				"主題曲",
				"主题音乐",
				"主題音樂"
			],
			"type": "string"
		},
		"片头曲": {
			"description": "节目片头曲名称。",
			"label": "片头曲",
			"aliases": [
				"opentheme",
				"片頭曲"
			],
			"type": "string"
		},
		"作曲": {
			"description": "使用片头曲参数时适用。片头曲的作曲者。",
			"label": "片头曲作曲者",
			"aliases": [
				"composer",
				"composers"
			],
			"type": "string"
		},
		"作词": {
			"description": "使用片头曲参数时适用。片头曲的作词者。",
			"label": "片头曲作词者",
			"aliases": [
				"lyricist",
				"作詞",
				"填词",
				"填詞"
			],
			"type": "string"
		},
		"演唱": {
			"description": "使用片头曲参数时适用。片头曲的演唱者。若前面使用了“演唱者《片头曲》”的格式，则可省略本参数。",
			"label": "片头曲演唱者",
			"aliases": [
				"singer",
				"主唱"
			],
			"type": "string"
		},
		"片尾曲": {
			"description": "节目片尾曲名称。",
			"label": "片尾曲",
			"aliases": [
				"endtheme"
			],
			"type": "string"
		},
		"作曲2": {
			"description": "使用片尾曲参数时适用。片尾曲的作曲者。",
			"label": "片尾曲作曲者",
			"aliases": [
				"composer_2"
			],
			"type": "string"
		},
		"作词2": {
			"description": "使用片尾曲参数时适用。片尾曲的作词者。",
			"label": "片尾曲作词者",
			"aliases": [
				"lyricist_2",
				"作詞2",
				"填词2",
				"填詞2"
			],
			"type": "string"
		},
		"演唱2": {
			"description": "使用片尾曲参数时适用。片尾曲的演唱者。若前面使用了“演唱者《片尾曲》”的格式，则可省略本参数。",
			"label": "片尾曲演唱者",
			"aliases": [
				"singer_2",
				"主唱2"
			],
			"type": "string"
		},
		"插曲": {
			"description": "节目的插曲名称。建议列出曲名和创作者或演唱者。",
			"label": "插曲",
			"aliases": [
				"interlude"
			],
			"type": "string"
		},
		"制作年份": {
			"description": "拍摄、制作该节目的年份。",
			"label": "制作年份",
			"aliases": [
				"produce_year",
				"製作年份",
				"拍摄年份",
				"拍攝年份"
			],
			"type": "string"
		},
		"制片人": {
			"description": "节目的制片人。",
			"label": "制片人",
			"aliases": [
				"producer",
				"製片人",
				"制作人",
				"製作人"
			],
			"type": "string"
		},
		"共同制片人": {
			"description": "节目的共同制片人。",
			"label": "共同制片人",
			"aliases": [
				"co-producer",
				"共同製片人",
				"共同制作人",
				"共同製作人",
				"联合制片人",
				"聯合製片人",
				"联合制作人",
				"聯合製作人"
			],
			"type": "string"
		},
		"出品人": {
			"description": "中国大陆电视节目作品适用。节目的出品人。",
			"label": "出品人",
			"aliases": [
				"program_presenter"
			],
			"type": "string"
		},
		"总监制": {
			"description": "节目的总监制。",
			"label": "总监制",
			"aliases": [
				"senior_producer",
				"總監製"
			],
			"type": "string"
		},
		"监制": {
			"description": "节目的监制。",
			"label": "监制",
			"aliases": [
				"supervising_producer",
				"監製"
			],
			"type": "string"
		},
		"执行制作": {
			"description": "节目的执行制片人。",
			"label": "执行制片人",
			"aliases": [
				"executive_producer",
				"執行製作"
			],
			"type": "string"
		},
		"共同执行制作": {
			"description": "节目的共同执行制片人。",
			"label": "共同执行制片人",
			"aliases": [
				"co-exec",
				"共同執行製作"
			],
			"type": "string"
		},
		"副制作人": {
			"description": "节目的副制片人。（由于副制片人的概念有些模糊，故暂时隐藏该参数）",
			"label": "副制片人",
			"aliases": [
				"asst_producer",
				"associate_producer",
				"副製作人"
			],
			"deprecated": true,
			"type": "string"
		},
		"顾问标签": {
			"description": "用来显示剧中的亦称。",
			"label": "顾问头衔",
			"aliases": [
				"consultant_label",
				"顧問標籤"
			],
			"type": "string"
		},
		"顾问": {
			"description": "节目的顾问或制作顾问。",
			"label": "顾问",
			"aliases": [
				"consultant",
				"consulting_producer",
				"製作顧問",
				"制作顾问",
				"顧問"
			],
			"type": "string"
		},
		"故事标签": {
			"description": "用来显示剧中的亦称。",
			"label": "故事创作者头衔",
			"aliases": [
				"story_label",
				"故事標籤"
			],
			"type": "string"
		},
		"故事": {
			"description": "节目的故事创作者（与编剧的职位定义不同）。",
			"label": "故事创作",
			"aliases": [
				"story"
			],
			"type": "string"
		},
		"编审": {
			"description": "故事的编审。",
			"label": "编审",
			"aliases": [
				"story_editor",
				"編審"
			],
			"type": "string"
		},
		"剪辑": {
			"description": "节目的剪辑师或剪辑公司。",
			"label": "剪辑",
			"aliases": [
				"editor",
				"剪輯",
				"剪接"
			],
			"type": "string"
		},
		"外景": {
			"description": "节目的拍摄地点。",
			"label": "拍摄地点",
			"aliases": [
				"location",
				"拍摄地",
				"拍攝地"
			],
			"type": "string"
		},
		"摄影": {
			"description": "节目的摄影指导。",
			"label": "摄影指导",
			"aliases": [
				"cinematography",
				"攝影"
			],
			"type": "string"
		},
		"机位": {
			"description": "摄像的机位，分为单机位和多机位。",
			"label": "摄影机位",
			"aliases": [
				"camera",
				"機位"
			],
			"type": "string"
		},
		"制作公司": {
			"description": "制作、出品该节目的公司。",
			"label": "制作公司",
			"aliases": [
				"company",
				"製作公司"
			],
			"type": "string"
		},
		"发行公司": {
			"description": "发行该节目的公司。",
			"label": "发行公司",
			"aliases": [
				"distributor",
				"發行公司"
			],
			"type": "string"
		},
		"发行许可": {
			"description": "适用于在中国大陆地区播映的电视剧、动画片、理论文献纪录片类节目。节目的发行许可证号或播映许可证号。",
			"label": "发行许可证号",
			"aliases": [
				"nrta_id",
				"sarft_id",
				"發行許可"
			],
			"type": "string"
		},
		"预算": {
			"description": "制作该节目的预算金额，不包含营销和宣传费用。若各个预算资料来源之间提供的数字有所冲突，请输入适当的预算范围。",
			"label": "制作预算",
			"aliases": [
				"budget",
				"預算"
			],
			"type": "string"
		},
		"电视网": {
			"description": "节目的首播频道，不包括重播、转播或网络同步跟播。",
			"label": "首播频道",
			"aliases": [
				"network",
				"TV_station",
				"channel",
				"電視網",
				"电视台",
				"電視台",
				"電視臺",
				"频道",
				"頻道"
			],
			"type": "string"
		},
		"图像制式": {
			"description": "首播频道的图像制式，如黑白、宽屏幕、NTSC 480i、HDTV 1080i等。",
			"label": "图像制式",
			"aliases": [
				"picture_format",
				"圖像制式",
				"视频制式",
				"視頻制式",
				"視訊制式"
			],
			"type": "string"
		},
		"声音制式": {
			"description": "首播频道的声音制式，如单声道、立体声等。",
			"label": "声音制式",
			"aliases": [
				"audio_format",
				"聲音制式",
				"音频制式",
				"音頻制式",
				"音訊制式"
			],
			"type": "string"
		},
		"播出国家": {
			"description": "首播频道所在的国家和地区。若节目只在一个国家/地区播出，且与制作国家/地区相同，或在频道名称前使用了国家地区模板时，则此参数应当省略。",
			"label": "播出国家或地区",
			"aliases": [
				"first_run",
				"播出國家",
				"播出地区",
				"播出地區",
				"首播国家",
				"首播國家",
				"首播地区",
				"首播地區"
			],
			"type": "string"
		},
		"集数0": {
			"description": "首播频道的节目集数，若与上方集数相同，则可省略该参数。",
			"label": "播出集数",
			"aliases": [
				"num_episodes_0",
				"集數0"
			],
			"type": "string"
		},
		"每集长度0": {
			"description": "首播频道的节目时长，若与上方时长相同，则可省略该参数。",
			"label": "播出时长",
			"aliases": [
				"runtime_0",
				"每集長度0",
				"每集长0",
				"每集長0"
			],
			"type": "string"
		},
		"开始": {
			"description": "首播频道的首集播出日期，可使用 Template:Start date 模板。",
			"label": "开始日期",
			"aliases": [
				"first_aired",
				"開始"
			],
			"type": "string"
		},
		"结束": {
			"description": "首播频道的末集播出日期，可使用 Template:End date 模板。",
			"label": "结束日期",
			"aliases": [
				"last_aired",
				"結束"
			],
			"type": "string"
		},
		"播出日期": {
			"description": "首播频道的播出日期，即“首集播出日期－末集播出日期”。对于季播的电视节目或系列电视剧，如节目已播出多季，则此参数可被视作“开始”与“结束”的替代参数。请注意，此参数不能与“开始”和“结束”同时使用。使用此参数时，请注意换行及连接符问题。每一季的播出日期请使用&#60;br /&#62;分隔，连接符使用全角连字暨减号（－）。",
			"label": "播出日期",
			"aliases": [
				"aired"
			],
			"type": "string"
		},
		"播出时间": {
			"description": "首播频道的播出时间。",
			"label": "播出时间",
			"aliases": [
				"aired_time",
				"播出時間"
			],
			"type": "string"
		},
		"电视网1": {
			"description": "其他国家和地区的首播频道。",
			"label": "播出频道2",
			"aliases": [
				"network_1",
				"TV_station_1",
				"channel_1",
				"電視網1",
				"电视台1",
				"電視台1",
				"電視臺1",
				"频道1",
				"頻道1"
			],
			"type": "string"
		},
		"图像制式1": {
			"description": "其他频道的图像制式。",
			"label": "图像制式",
			"aliases": [
				"picture_format_1",
				"圖像制式1",
				"视频制式1",
				"視頻制式1",
				"視訊制式1"
			],
			"type": "string"
		},
		"声音制式1": {
			"description": "其他频道的声音制式。",
			"label": "声音制式",
			"aliases": [
				"audio_format_1",
				"聲音制式1",
				"音频制式1",
				"音頻制式1",
				"音訊制式1"
			],
			"type": "string"
		},
		"播出国家1": {
			"description": "其他频道所在的国家和地区。",
			"label": "播出国家或地区",
			"aliases": [
				"first_run_1",
				"播出國家1",
				"播出地区1",
				"播出地區1",
				"首播国家1",
				"首播國家1",
				"首播地区1",
				"首播地區1"
			],
			"type": "string"
		},
		"集数1": {
			"description": "其他频道的节目集数。",
			"label": "播出集数",
			"aliases": [
				"num_episodes_1",
				"集數1"
			],
			"type": "string"
		},
		"每集长度1": {
			"description": "其他频道的节目时长。",
			"label": "播出时长",
			"aliases": [
				"runtime_1",
				"每集長度1",
				"每集长1",
				"每集長1"
			],
			"type": "string"
		},
		"开始1": {
			"description": "其他频道的首集播出日期。",
			"label": "开始日期",
			"aliases": [
				"first_aired_1",
				"開始1"
			],
			"type": "string"
		},
		"结束1": {
			"description": "其他频道的末集播出日期。",
			"label": "结束日期",
			"aliases": [
				"last_aired_1",
				"結束1"
			],
			"type": "string"
		},
		"播出日期1": {
			"description": "其他频道的播出日期。",
			"label": "播出日期",
			"aliases": [
				"aired_1"
			],
			"type": "string"
		},
		"播出时间1": {
			"description": "其他频道的播出时间。",
			"label": "播出时间",
			"aliases": [
				"aired_time_1",
				"播出時間1"
			],
			"type": "string"
		},
		"电视网2": {
			"description": "其他国家和地区的首播频道。",
			"label": "播出频道3",
			"aliases": [
				"network_2",
				"TV_station_2",
				"channel_2",
				"電視網2",
				"电视台2",
				"電視台2",
				"電視臺2",
				"频道2",
				"頻道2"
			],
			"type": "string"
		},
		"图像制式2": {
			"description": "其他频道的图像制式。",
			"label": "图像制式",
			"aliases": [
				"picture_format_2",
				"圖像制式2",
				"视频制式2",
				"視頻制式2",
				"視訊制式2"
			],
			"type": "string"
		},
		"声音制式2": {
			"description": "其他频道的声音制式。",
			"label": "声音制式",
			"aliases": [
				"audio_format_2",
				"聲音制式2",
				"音频制式2",
				"音頻制式2",
				"音訊制式2"
			],
			"type": "string"
		},
		"播出国家2": {
			"description": "其他频道所在的国家和地区。",
			"label": "播出国家或地区",
			"aliases": [
				"first_run_2",
				"播出國家2",
				"播出地区2",
				"播出地區2",
				"首播国家2",
				"首播國家2",
				"首播地区2",
				"首播地區2"
			],
			"type": "string"
		},
		"集数2": {
			"description": "其他频道的节目集数。",
			"label": "播出集数",
			"aliases": [
				"num_episodes_2",
				"集數2"
			],
			"type": "string"
		},
		"每集长度2": {
			"description": "其他频道的节目时长。",
			"label": "播出时长",
			"aliases": [
				"runtime_2",
				"每集長度2",
				"每集长2",
				"每集長2"
			],
			"type": "string"
		},
		"开始2": {
			"description": "其他频道的首集播出日期。",
			"label": "开始日期",
			"aliases": [
				"first_aired_2",
				"開始2"
			],
			"type": "string"
		},
		"结束2": {
			"description": "其他频道的末集播出日期。",
			"label": "结束日期",
			"aliases": [
				"last_aired_2",
				"結束2"
			],
			"type": "string"
		},
		"播出日期2": {
			"description": "其他频道的播出日期。",
			"label": "播出日期",
			"aliases": [
				"aired_2"
			],
			"type": "string"
		},
		"播出时间2": {
			"description": "其他频道的播出时间。",
			"label": "播出时间",
			"aliases": [
				"aired_time_2",
				"播出時間2"
			],
			"type": "string"
		},
		"电视网3": {
			"description": "其他国家和地区的首播频道。",
			"label": "播出频道4",
			"aliases": [
				"network_3",
				"TV_station_3",
				"channel_3",
				"電視網3",
				"电视台3",
				"電視台3",
				"電視臺3",
				"频道3",
				"頻道3"
			],
			"type": "string"
		},
		"图像制式3": {
			"description": "其他频道的图像制式。",
			"label": "图像制式",
			"aliases": [
				"picture_format_3",
				"圖像制式3",
				"视频制式3",
				"視頻制式3",
				"視訊制式3"
			],
			"type": "string"
		},
		"声音制式3": {
			"description": "其他频道的声音制式。",
			"label": "声音制式",
			"aliases": [
				"audio_format_3",
				"聲音制式3",
				"音频制式3",
				"音頻制式3",
				"音訊制式3"
			],
			"type": "string"
		},
		"播出国家3": {
			"description": "其他频道所在的国家和地区。",
			"label": "播出国家或地区",
			"aliases": [
				"first_run_3",
				"播出國家3",
				"播出地区3",
				"播出地區3",
				"首播国家3",
				"首播國家3",
				"首播地区3",
				"首播地區3"
			],
			"type": "string"
		},
		"集数3": {
			"description": "其他频道的节目集数。",
			"label": "播出集数",
			"aliases": [
				"num_episodes_3",
				"集數3"
			],
			"type": "string"
		},
		"每集长度3": {
			"description": "其他频道的节目时长。",
			"label": "播出时长",
			"aliases": [
				"runtime_3",
				"每集長度3",
				"每集长3",
				"每集長3"
			],
			"type": "string"
		},
		"开始3": {
			"description": "其他频道的首集播出日期。",
			"label": "开始日期",
			"aliases": [
				"first_aired_3",
				"開始3"
			],
			"type": "string"
		},
		"结束3": {
			"description": "其他频道的末集播出日期。",
			"label": "结束日期",
			"aliases": [
				"last_aired_3",
				"結束3"
			],
			"type": "string"
		},
		"播出日期3": {
			"description": "其他频道的播出日期。",
			"label": "播出日期",
			"aliases": [
				"aired_3"
			],
			"type": "string"
		},
		"播出时间3": {
			"description": "其他频道的播出时间。",
			"label": "播出时间",
			"aliases": [
				"aired_time_3",
				"播出時間3"
			],
			"type": "string"
		},
		"电视网4": {
			"description": "其他国家和地区的首播频道。",
			"label": "播出频道5",
			"aliases": [
				"network_4",
				"TV_station_4",
				"channel_4",
				"電視網4",
				"电视台4",
				"電視台4",
				"電視臺4",
				"频道4",
				"頻道4"
			],
			"type": "string"
		},
		"图像制式4": {
			"description": "其他频道的图像制式。",
			"label": "图像制式",
			"aliases": [
				"picture_format_4",
				"圖像制式4",
				"视频制式4",
				"視頻制式4",
				"視訊制式4"
			],
			"type": "string"
		},
		"声音制式4": {
			"description": "其他频道的声音制式。",
			"label": "声音制式",
			"aliases": [
				"audio_format_4",
				"聲音制式4",
				"音频制式4",
				"音頻制式4",
				"音訊制式4"
			],
			"type": "string"
		},
		"播出国家4": {
			"description": "其他频道所在的国家和地区。",
			"label": "播出国家或地区",
			"aliases": [
				"first_run_4",
				"播出國家4",
				"播出地区4",
				"播出地區4",
				"首播国家4",
				"首播國家4",
				"首播地区4",
				"首播地區4"
			],
			"type": "string"
		},
		"集数4": {
			"description": "其他频道的节目集数。",
			"label": "播出集数",
			"aliases": [
				"num_episodes_4",
				"集數4"
			],
			"type": "string"
		},
		"每集长度4": {
			"description": "其他频道的节目时长。",
			"label": "播出时长",
			"aliases": [
				"runtime_4",
				"每集長度4",
				"每集长4",
				"每集長4"
			],
			"type": "string"
		},
		"开始4": {
			"description": "其他频道的首集播出日期。",
			"label": "开始日期",
			"aliases": [
				"first_aired_4",
				"開始4"
			],
			"type": "string"
		},
		"结束4": {
			"description": "其他频道的末集播出日期。",
			"label": "结束日期",
			"aliases": [
				"last_aired_4",
				"結束4"
			],
			"type": "string"
		},
		"播出日期4": {
			"description": "其他频道的播出日期。",
			"label": "播出日期",
			"aliases": [
				"aired_4"
			],
			"type": "string"
		},
		"播出时间4": {
			"description": "其他频道的播出时间。",
			"label": "播出时间",
			"aliases": [
				"aired_time_4",
				"播出時間4"
			],
			"type": "string"
		},
		"电视网5": {
			"description": "其他国家和地区的首播频道。",
			"label": "播出频道6",
			"aliases": [
				"network_5",
				"TV_station_5",
				"channel_5",
				"電視網5",
				"电视台5",
				"電視台5",
				"電視臺5",
				"频道5",
				"頻道5"
			],
			"type": "string"
		},
		"图像制式5": {
			"description": "其他频道的图像制式。",
			"label": "图像制式",
			"aliases": [
				"picture_format_5",
				"圖像制式5",
				"视频制式5",
				"視頻制式5",
				"視訊制式5"
			],
			"type": "string"
		},
		"声音制式5": {
			"description": "其他频道的声音制式。",
			"label": "声音制式",
			"aliases": [
				"audio_format_5",
				"聲音制式5",
				"音频制式5",
				"音頻制式5",
				"音訊制式5"
			],
			"type": "string"
		},
		"播出国家5": {
			"description": "其他频道所在的国家和地区。",
			"label": "播出国家或地区",
			"aliases": [
				"first_run_5",
				"播出國家5",
				"播出地区5",
				"播出地區5",
				"首播国家5",
				"首播國家5",
				"首播地区5",
				"首播地區5"
			],
			"type": "string"
		},
		"集数5": {
			"description": "其他频道的节目集数。",
			"label": "播出集数",
			"aliases": [
				"num_episodes_5",
				"集數5"
			],
			"type": "string"
		},
		"每集长度5": {
			"description": "其他频道的节目时长。",
			"label": "播出时长",
			"aliases": [
				"runtime_5",
				"每集長度5",
				"每集长5",
				"每集長5"
			],
			"type": "string"
		},
		"开始5": {
			"description": "其他频道的首集播出日期。",
			"label": "开始日期",
			"aliases": [
				"first_aired_5",
				"開始5"
			],
			"type": "string"
		},
		"结束5": {
			"description": "其他频道的末集播出日期。",
			"label": "结束日期",
			"aliases": [
				"last_aired_5",
				"結束5"
			],
			"type": "string"
		},
		"播出日期5": {
			"description": "其他频道的播出日期。",
			"label": "播出日期",
			"aliases": [
				"aired_5"
			],
			"type": "string"
		},
		"播出时间5": {
			"description": "其他频道的播出时间。",
			"label": "播出时间",
			"aliases": [
				"aired_time_5",
				"播出時間5"
			],
			"type": "string"
		},
		"电视网6": {
			"description": "其他国家和地区的首播频道。",
			"label": "播出频道7",
			"aliases": [
				"network_6",
				"TV_station_6",
				"channel_6",
				"電視網6",
				"电视台6",
				"電視台6",
				"電視臺6",
				"频道6",
				"頻道6"
			],
			"type": "string"
		},
		"图像制式6": {
			"description": "其他频道的图像制式。",
			"label": "图像制式",
			"aliases": [
				"picture_format_6",
				"圖像制式6",
				"视频制式6",
				"視頻制式6",
				"視訊制式6"
			],
			"type": "string"
		},
		"声音制式6": {
			"description": "其他频道的声音制式。",
			"label": "声音制式",
			"aliases": [
				"audio_format_6",
				"聲音制式6",
				"音频制式6",
				"音頻制式6",
				"音訊制式6"
			],
			"type": "string"
		},
		"播出国家6": {
			"description": "其他频道所在的国家和地区。",
			"label": "播出国家或地区",
			"aliases": [
				"first_run_6",
				"播出國家6",
				"播出地区6",
				"播出地區6",
				"首播国家6",
				"首播國家6",
				"首播地区6",
				"首播地區6"
			],
			"type": "string"
		},
		"集数6": {
			"description": "其他频道的节目集数。",
			"label": "播出集数",
			"aliases": [
				"num_episodes_6",
				"集數6"
			],
			"type": "string"
		},
		"每集长度6": {
			"description": "其他频道的节目时长。",
			"label": "播出时长",
			"aliases": [
				"runtime_6",
				"每集長度6",
				"每集长6",
				"每集長6"
			],
			"type": "string"
		},
		"开始6": {
			"description": "其他频道的首集播出日期。",
			"label": "开始日期",
			"aliases": [
				"first_aired_6",
				"開始6"
			],
			"type": "string"
		},
		"结束6": {
			"description": "其他频道的末集播出日期。",
			"label": "结束日期",
			"aliases": [
				"last_aired_6",
				"結束6"
			],
			"type": "string"
		},
		"播出日期6": {
			"description": "其他频道的播出日期。",
			"label": "播出日期",
			"aliases": [
				"aired_6"
			],
			"type": "string"
		},
		"播出时间6": {
			"description": "其他频道的播出时间。",
			"label": "播出时间",
			"aliases": [
				"aired_time_6",
				"播出時間6"
			],
			"type": "string"
		},
		"前作": {
			"description": "若节目为另一节目的续集作品，请在此填写前作的名称，并在全角括号内注明年份。例如：“宫锁心玉（2011年）”。",
			"label": "前作",
			"aliases": [
				"preceded_by",
				"晚于",
				"晚於",
				"后于",
				"後於"
			],
			"type": "string"
		},
		"续作": {
			"description": "若节目有续作，请在此填写该续作的名称，并在全角括号内注明年份。例如：“宫锁连城（2014年）”。",
			"label": "续作",
			"aliases": [
				"followed_by",
				"續作",
				"早于",
				"早於",
				"先于",
				"先於"
			],
			"type": "string"
		},
		"相关节目": {
			"description": "相关的电视节目名称。",
			"label": "相关节目",
			"aliases": [
				"related",
				"相關節目",
				"相关剧集",
				"相關劇集",
				"相关",
				"相關"
			],
			"type": "string"
		},
		"中国大陆名称": {
			"description": "节目的中国大陆名称，请不要在文字间插入“-&#123;&#125;-”。",
			"label": "中国大陆名称",
			"aliases": [
				"show_name_zh-cn",
				"中國大陸名稱"
			],
			"type": "string"
		},
		"台湾名称": {
			"description": "节目的台湾名称，请不要在文字间插入“-&#123;&#125;-”。",
			"label": "台湾名称",
			"aliases": [
				"show_name_zh-tw",
				"台灣名稱",
				"臺灣名稱"
			],
			"type": "string"
		},
		"港澳名称": {
			"description": "节目的港澳名称，请不要在文字间插入“-&#123;&#125;-”。",
			"label": "港澳名称",
			"aliases": [
				"show_name_zh-hk",
				"港澳名稱"
			],
			"type": "string"
		},
		"新加坡名称": {
			"description": "节目的新加坡名称，请不要在文字间插入“-&#123;&#125;-”。",
			"label": "新加坡名称",
			"aliases": [
				"show_name_zh-sg",
				"新加坡名稱"
			],
			"type": "string"
		},
		"马来西亚名称": {
			"description": "节目的马来西亚名称，请不要在文字间插入“-&#123;&#125;-”。",
			"label": "马来西亚名称",
			"aliases": [
				"show_name_zh-my",
				"馬來西亞名稱"
			],
			"type": "string"
		},
		"日本名称": {
			"description": "节目在日本的翻译名称，请不要在文字间插入“-&#123;&#125;-”。",
			"label": "日本名称",
			"aliases": [
				"show_name_zh-jp",
				"日本名稱"
			],
			"type": "string"
		},
		"韩国名称": {
			"description": "节目在韩国的翻译名称，请不要在文字间插入“-&#123;&#125;-”。",
			"label": "韩国名称",
			"aliases": [
				"show_name_zh-kr",
				"韓國名稱"
			],
			"type": "string"
		},
		"泰国名称": {
			"description": "节目在泰国的翻译名称，请不要在文字间插入“-&#123;&#125;-”。",
			"label": "泰国名称",
			"aliases": [
				"show_name_zh-th",
				"泰國名稱"
			],
			"type": "string"
		},
		"越南名称": {
			"description": "节目在越南的翻译名称，请不要在文字间插入“-&#123;&#125;-”。",
			"label": "越南名称",
			"aliases": [
				"show_name_zh-vi",
				"越南名稱"
			],
			"type": "string"
		},
		"官方网站": {
			"description": "节目官方网站的网址。",
			"label": "官方网站",
			"aliases": [
				"website",
				"官方網站",
				"网站",
				"網站"
			],
			"type": "string"
		},
		"制作网站": {
			"description": "第二个官方网站的网址（通常是电视台或制作公司网域中的节目网站）。",
			"label": "制作网站",
			"aliases": [
				"production_website",
				"製作網站"
			],
			"type": "string"
		},
		"imdb_id": {
			"description": "节目在 IMDb 的编号。",
			"label": "IMDb 编号",
			"type": "string"
		},
		"tv_com_id": {
			"description": "节目在 TV.com 的编号。",
			"label": "TV.com 编号",
			"type": "string"
		}
	}
}
</templatedata>
{{hidden end}}

== 微格式 ==
{{UF-hcal}}

== 重定向 ==
以下是重定向到此页的模板名：
*'''{{tl|影集資訊}}'''
*'''{{tl|电视剧集信息框}}'''
*'''{{tl|Infobox television}}'''
*'''{{tl|Infobox Television}}'''
*'''{{tl|電視節目資訊}}'''
*'''{{tl|電視節目}}'''

== 相关模板 ==
以下模板与本模板有一定的关联度，并且大体兼容：
*'''{{tl|系列节目信息框}}'''：季播的电视节目或者系列电视剧可以考虑使用此模板。
*'''{{tl|Infobox reality music competition}}'''：音乐类的真人秀节目可以考虑使用此模板。
*更多模板详见：[[:分类:电视节目信息框模板]]

{{Film and Television related infobox templates}}

<includeonly>
[[Category:電視信息框模板]]
[[Category:电视节目信息框模板| ]]
</includeonly>