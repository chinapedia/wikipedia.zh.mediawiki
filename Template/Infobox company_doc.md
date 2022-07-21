{{NoteTA
|G1 = IT
|G2 = MediaWiki
}}
{{Documentation subpage}}
{{High-use|11160}}
{{esoteric}}
<!-- 在本行下編輯模板說明 -->
<!-- 以下為本模板的詳細使用說明，請不要刪除，更新模板後請依照您調整的內容，變更以下的說明。 -->
{{Uses Wikidata|P856|P946|P154|P1454|P31|P1365|P1366|P571|P576|P112|P169|P1451|P1546|P452|P2139|P3362|P2295|P2403|P2137|P127|P1128|P2226|P749}}

本模板是用於提供[[公司]]基本資料的信息框模板。
* 在[[Template_talk:Infobox_Company|討論頁]]中討論這個修改—參考他人的回應並且取得共識，決定這個更改是否是正確的決定。如果模板中沒有您需要的欄位，您也許可以加入一個新的欄位。

== 使用方法 ==
如要在條目內使用本模板，請拷貝下方原始碼文字後貼入條目中。

所有參數欄位皆為選填，未填寫的欄位不會出現在儲存編輯後的條目中。

請移除部分參數後方的<code><nowiki><!--</nowiki></code>和<code><nowiki>--></nowiki></code>，以便讓輸入的資料顯示於條目中。
在編輯[[公司]]條目時，請使用公司信息框模板。如果您對這個模板有任何問題，都可以在模板的討論頁提出。

以下是這個模板的原始碼：
<pre>
{{Infobox company 
| name     = 公司名稱
| name_en  = 公司英文名稱（或原文名稱）
| logo     = 公司標誌（圖片）
| type     = 公司類型
| foundation       = 成立地點和時間
| location         = 總部位置
| key_people       = 重要人物
| industry         = 產業類別
| products         = 產品
| revenue          = 年營業額
| operating_income = 稅前盈餘
| net_income       = 淨利
| num_employees    = 員工人數
| parent           = 母公司（控股公司或持股公司）
| divisions        = 主要部門
| subsid           = 子公司
| homepage         = 網址
| footnotes        = 備註
}}
</pre>

=== 精簡版本 ===
{{Parameter names example
|name|name_en|logo|logo_size|logo_caption|image|image_size|image_caption|native_name|native_name_lang|other_name|type|industry|foundation|founder|location|area_served|key_people|products|services|owner|homepage}}

<pre>
{{Infobox company
| name = 
| name_en = 
| logo = 
| logo_size = 
| logo_caption = 
| image =          
| image_size =
| image_caption =
| native_name = 
| native_name_lang = <!-- 公司名称原文语言的ISO 639-1代码。例如填写“ja”表示日语。 -->
| other_name = 
| type = 
| industry = 
| foundation = 
| founder = 
| location = 
| area_served = 
| key_people = 
| products = 
| services = 
| owner = 
| homepage = <!-- {{URL|example.com}} -->
}}
</pre>

=== 完整版本 ===
{{Parameter names example
|name|name_en|logo|logo_size|logo_caption|image|image_size|image_caption|former_name|type|trading_name|native_name|native_name_lang|other_name|traded_as|ISIN|local_code_name|local_code|fate|predecessor|successor|foundation|defunct|location|locations|area_served|founder|key_people|industry|products|services|revenue|operating_income|net_income|net_income_year|aum|assets|equity|owner|num_employees|num_employees_year|parent|divisions|subsid|homepage|slogan|capital|market_value|P/E_ratio|earnings_per_share|net_asset_value|production|accounting_period|major_shareholder|footnotes}}

<pre>{{Infobox company
| name = 
| name_en = 
| logo = 
| logo_size = 
| logo_caption = 
| image =          
| image_size =
| image_caption =
| former_name =
| type = 
| trading_name = 
| native_name = 
| native_name_lang = <!-- 公司名稱原文語言的ISO 639-1代碼。例如填寫「ja」表示日語。 -->
| other_name = 
| traded_as = 
| ISIN = 
| local_code_name= <!-- 填写CN/TW/JP或其他自定义文字 -->
| local_code = 
| fate = 
| predecessor = 
| successor = 
| foundation = <!-- {{Start date and age|df=yes|YYYY|MM|DD}} -->
| defunct = <!-- {{End date|YYYY|MM|DD}} -->
| location = 
| locations = 
| area_served = 
| founder = 
| key_people = 
| industry = 
| products = 
| services = 
| revenue = 
| operating_income = 
| net_income = 
| aum = <!-- 僅適用於金融服務類公司。 -->
| assets = 
| equity = 
| owner = 
| num_employees = 
| num_employees_year = 
| parent = 
| divisions = 
| subsid = 
| homepage = <!-- {{URL|example.com/}} -->
| slogan = 
| capital = 
| market_value = 
| P/E_ratio = 
| earnings_per_share = 
| net_asset_value = 
| accounting_period = 
| major_shareholder = 
| footnotes = 
}}
</pre>

==填寫範例==
右邊是「[[聯想集團有限公司]]」條目中的信息框模板，您可能會注意到其中的圖片部份被移除了，這是為了符合維基百科的合理使用規範，不可在相關條目以外的名字空間使用「[[合理使用]]」的圖片。

{{Infobox Company 
| company_name     = 聯想集團有限公司
| company_name_en  = Lenovo
| company_logo     = [[File:Branding lenovo-logo lenovologoposred low res.png|center|200px]]
| company_type     = 上市公司（[[香港證交所]]）
| foundation       = [[中國]]（1984年）
| location         = [[紐約]]
| key_people       = [[柳傳志]] - 控股總裁<br />[[楊元慶]] - 董事局主席<br />[[史蒂夫·沃德]] - 首席運營官
| industry         = [[IT]]產業<br />風險投資<br />房地產
| products         = [[個人電腦]]<br />[[手提電腦]]<br />[[伺服器]]<br />[[掌上電腦]]<br />[[印表機]]<br />[[超級伺服器]]等
| revenue          = 130億[[美元]]（2005年）
| operating_income = 8,481萬[[美元]]（2006年）
| net_income       = 
| num_employees    = 19,000人（2004年）
| parent           = 
| subsid           = 
| homepage         = {{URL|http://www.lenovo.com}}
| footnotes        = 
}}

以下是右上方的「[[聯想集團有限公司]]」公司信息框模板的原始代碼：

<pre>
{{Infobox Company 
| company_name     = 聯想集團有限公司
| company_name_en  = Lenovo
| company_logo     = [[File:Branding lenovo-logo lenovologoposred low res.png|center|200px]]
| company_type     = 上市公司（[[香港證交所]]）
| foundation       = [[中國]]（1984年）
| location         = [[紐約]]
| key_people       = [[柳傳志]] - 控股總裁<br />[[楊元慶]] - 董事局主席<br />[[史蒂夫·沃德]] - 首席運營官
| industry         = [[IT]]產業<br />風險投資<br />房地產
| products         = [[個人電腦]]<br />[[手提電腦]]<br />[[伺服器]]<br />[[掌上電腦]]<br />[[印表機]]<br />[[超級伺服器]]等
| revenue          = 130億[[美元]]（2005年）
| operating_income = 8,481萬[[美元]]（2006年）
| net_income       = 
| num_employees    = 19,000人（2004年）
| parent           = 
| subsid           = 
| homepage         = {{URL|http://www.lenovo.com}}
| footnotes        = 
}}
</pre>


<!-- 以上為本模板的詳細使用說明，請不要刪除，更新模板後請依照您調整的內容，變更上方的說明。 -->

== 參數說明 ==
{| class="wikitable" 
|-
! 参数名
! 显示名
! {{nowrap|必填项}}
! 描述
|-
! name
||公司名稱
|{{rh}}|'''是'''
||公司稱呼，若公司登記與實際名稱有出入者，請分行或於條目中做詳細說明。
|-
! name_en
||公司英文名稱
||否
||该公司的英文稱呼。
|-
! logo
||公司商標
||否
||公司商標圖片，已使用[[模块:InfoboxImage]]，與格式<code><nowiki>[[File:文件名]]</nowiki></code>相容，可自行指定大小。
|-
! logo_size
||公司商標大小
||否
||公司商標圖片大小，仅适用於logo参数只填写文件名时。
|-
! logo_alt
||公司商標替代文字
||否
||公司商標圖片[[alt屬性|替代文字]]，仅适用於logo参数只填写文件名时。
|-
! logo_caption
||公司商標说明
||否
||对公司商标的说明。
|-
! image
||公司建筑物
||否
||公司建筑物圖片，同商標圖片說明。如原格式<code><nowiki>[[File:文件名]]</nowiki></code>有設定位置參數，請刪除。
|-
|-
! image_size
||公司建筑图片大小
||否
||公司建筑图片大小，仅适用於image参数只填写文件名时。
|-
! image_alt
||公司建筑图片替代文字
||否
||公司建筑图片[[alt屬性|替代文字]]，仅适用於image参数只填写文件名时。
|-
|-
! image_caption
||公司建筑图片说明
||否
||对公司建筑物图片的说明。
|-
! native_name
||原文名稱
||否
||非英語系公司原文名稱，與舊參數original_text相容，建議配合相關模版使用。公司名稱為中文时無需使用此參數。
|-
|-
! other_name
||其他名稱
||否
||公司的其他名稱。
|-
! former_name
||曾用名
||否
||公司曾经用过的名稱。
|-
! type
||公司類型
||否
||公司類型，只適用於國有企業、私人公司、上市公司、子公司、事業部制，上市公司可附上相關交易所資料。不適用於公司法定類型，如有限公司、株式會社等。
|-
! traded_as
||股票代號
||否
||market_information證券市場資料，公司公開發行股票證券資訊。<br />上市公司的股票代號，伴隨使用股票代號模板。<br />範例：<nowiki>{{nasdaq|MSFT}}、{{nyse|CAT}}或{{twse|2317}}</nowiki> <br />可用的股票代號模板列表可參見[[:Category:股票代码模板]]。
|-
! ISIN
||國際證券識別碼
||否
||國際證券識別碼共有十二個字符組成，含字母及數字，能統一識別證券，並無金融工具的特徵資訊。國際證券識別碼，依據國際標準化組織ISO 6166訂明之結構組成。
|-
! local_code_name
||依填入参数而定
||否
||公司在本地区注册时的代码。填写“CN”为中华人民共和国境内注册机构的代码；“TW”为中華民國境內各營利事業機構（含公司）的統一編號（英譯：{{lang|en|Unified Business Number}}），由[[經濟部商業司]]負責製發；“JP”为日本境內各註冊[[法人]]（含[[公法人]]與一般公司）所使用之識別編號，由[[國稅廳]]負責編製。其他地区代码请自定义或加入[[Template:Lpid]]中。
|-
! local_code
||地区代码
||否
||依local_code_name填写地区代码
|-
! fate*
||公司結局
||否
||公司停止營業的原因。例如收購，破產，解散，合併。
|-
! predecessor
||機構前身
||否
||公司的前身機構組織。
|-
! successor*
||後繼組織
||否
||公司解散後的後繼機構組織。
|-
! foundation
||成立地點和時間
||建議
||公司成立地點和時間。
|-
! defunct*
||結束於
||否
||公司解散的時間。
|-
! location
||總部位置
|{{rh}}|'''是'''
||公司總部位置
|-
! locations
||廠（店）數
||否
||公司擁有實體廠房或店面的數量。用數字來表示，並加上建物的類型，以及在括號內填入適用的年份。
|-
! area_served
||服務範圍
||否
||公司服務範圍
|-
! founder
||創始人
||建議
||公司創辦人
|-
! chairman
||董事長
||否
||公司負責人（该参数已暂停使用；请改用<code>key_people</code>）
|-
! president
||總裁
||否
||公司領導人（该参数已暂停使用；请改用<code>key_people</code>）
|-
! key_people
||重要人物
||否
||公司主要人物
|-
! industry
||產業類別
||否
||公司產業類別
|-
! products
||產品
||否
||公司相關產品
|-
! services
||服務
||否
||公司相關服務
|-
! revenue
||年營業額
||否
||公司年營業額
|-
! operating_income
||稅前盈餘
||否
||總[[除稅及利息前盈利]]，每年公司扣除掉利息支出與法律規定應繳稅額之前所得盈利。在括號內加入年份。
|-
! net_income
||稅後純利
||否
||淨利或[[利潤]]（profit），每年公司盈餘扣除掉利息支出與應繳稅額之後的實際利潤。在括號內加入年份。
|-
! aum 
||資產管理規模
||否
||此欄只給有金融服務的公司使用。公司的總資產管理規模（assets under management）。
|-
! assets
||總資產
||否
||公司持有資產
|-
! equity
||總資產淨值
||否
||公司持有的總資產淨值，也稱為[[股東權益]]。
|-
! owner
||所有權人
||否
||公司持有股東
|-
! num_employees
||員工人數
||否
||公司聘任人數
|-
! parent
||母公司
||否
||控股公司或持股公司，公司所屬事業群。
|-
! divisions
||主要部門
||否
||公司主要事業部門
|-
! subsid
||主要子公司
||否
||公司另行開設事業中的主要事業
|-
! |homepage
||網址
||否
||公司架設網際網路站點
|-
! capital
||實收資本額
||否
||公司實收資本額，注意不是資本總額。
|-
! slogan
||口號
||否
||公司於平面媒體或公司內部所使用宣傳口號。
|-
! market_value
||市值
||否
||
|-
! P/E_ratio
||市盈率
||否
||-
|-
! earnings_per_share
||每股盈利
||否
||公司公開發行股票所含盈利。
|-
! net_asset_value
||每股資產淨值
||否
||公司公開發行股票所含資產淨值。
|-
! accounting_period
||結算期
||否
||公司營業年度結算時間
|-
! major_shareholder
||主要股東
||否
||公司持有股東
|-
! footnotes
||備註
||否
||其他需補充注意事項
|-
|}

== 模板数据 ==
<includeonly>
{{TemplateDataHeader}}
<templatedata>
{
	"description": "提供公司基本資訊的信息框",
	"params": {
		"name": {
			"label": "公司名稱",
			"description": "公司的正式完整名稱。公司的完整名稱可能與條目標題所使用的名稱不同。",
			"aliases": [
				"company_name"
			],
			"default": "{{PAGENAME}}",
			"required": true,
			"type": "string"
		},
		"width": {
			"label": "寬度",
			"description": "信息欄寬度",
			"default": "300px",
			"required": false,
			"type": "string"
		},
		"name_en": {
			"label": "公司英文名稱",
			"description": "公司的英文名稱。",
			"aliases": [
				"company_name_en"
			],
			"type": "string"
		},
		"native_name": {
			"description": "公司在所屬國家使用的正式完整原文名稱。",
			"label": "公司原文名稱",
			"type": "string"
		},
		"native_name_lang": {
			"description": "公司在所屬國家使用的正式完整原文名稱的語言。",
			"label": "公司原文名稱語言",
			"type": "string"
		},
		"other_name": {
			"description": "公司的其他名稱。",
			"label": "公司其他名稱",
			"aliases": [
				"other_text"
			],
			"type": "string"
		},
		"former_name": {
			"label": "公司的曾用名",
			"description": "公司曾经用过的名稱。",
			"type": "string"
		},
		"logo": {
			"description": "公司目前主要使用的商標或標誌。請使用條目主題之公司的商標；公司的商標可能與消費者產品上所使用的商標不同，特別是在條目與母公司或控股公司有關時。注意：將註冊商標或標誌上傳到維基共享資源可能導致檔案被刪除。",
			"label": "公司商標",
			"aliases": [
				"company_logo"
			],
			"example": "logo.png",
			"type": "string"
		},
		"logo_size": {
			"description": "公司商標圖片大小。若不指定，將使用預設圖片大小數值。",
			"label": "公司商標大小",
			"example": "250px",
			"type": "string"
		},
		"logo_alt": {
			"description": "公司商標的描述文字，適用於純文字瀏覽器和視覺不便的使用者。",
			"label": "公司商標替代文字",
			"aliases": [
				"alt"
			],
			"example": "第一公司的商標。",
			"type": "string"
		},
		"logo_caption": {
			"description": "如有需要，可填寫公司商標的說明。通常較少使用。",
			"label": "公司商標說明",
			"aliases": [
				"caption"
			],
			"example": "1960年至1982年間使用的商標。",
			"type": "string"
		},
		"image": {
			"description": "公司的次要圖片（非商標）。",
			"label": "次要圖片",
			"example": "Headquarter.jpg ",
			"type": "string"
		},
		"image_size": {
			"description": "公司次要圖片的大小。若不指定，將使用預設圖片大小數值。",
			"label": "次要圖片大小",
			"example": "250px",
			"type": "string"
		},
		"image_alt": {
			"description": "公司次要圖片的描述文字，適用於純文字瀏覽器和視覺不便的使用者。。",
			"label": "次要圖片替代文字",
			"example": "第一公司的總部大樓外觀。",
			"type": "string"
		},
		"image_caption": {
			"description": "如有需要，可填寫公司次要圖片的說明。通常較少使用。",
			"label": "次要圖片说明",
			"example": "第一公司位於紐約市的總部大樓。",
			"type": "string"
		},
		"type": {
			"description": "公司類型，並請加入維基連結。對於私有公司，如有需要，可使用「所有權人」（owner）參數來列出各所有權人的持有佔比。",
			"label": "公司類型",
			"aliases": [
				"company_type"
			],
			"example": "[[上市公司]] 或 [[私人公司]]",
			"type": "wiki-page-name"
		},
		"traded_as": {
			"description": "上市公司的股市交易代號，請使用股票代號模板模板。若公司屬於主要市場指數，也可在此填入公司目前的狀態。若有一個以上的股市交易代號，請使用 {{unbulleted list}} 模板。股票代號模板可在 [[分類:股票代碼模板]] 中找到。",
			"label": "股票代號",
			"type": "string"
		},
		"local_code_name": {
			"description": "公司在本地区注册时的代码。填写“CN”为中华人民共和国境内注册机构的代码；“TW”为中华民国境内各营利事业机构（含公司）的统一编号（英译：Unified Business Number），由[[經濟部商業司|经济部商业司]]负责制发；“JP”为日本境内各注册[[法人]]（含[[公法人]]与一般公司）所使用之识别编号，由[[國稅廳|国税厅]]负责编制。其他地区代码请自定义或加入模板。",
			"label": "地區代碼",
			"type": "string"
		},
		"local_code": {
			"description": "依local_code_name填写地区代码",
			"label": "注冊代碼",
			"type": "string"
		},
		"predecessor": {
			"description": "公司或機構前身的正式完整名稱。若條目主題的公司是由一個或多個機構合併而成，請使用 {{unbulleted list}} 模板列出所有機構名稱。",
			"label": "公司前身",
			"type": "string"
		},
		"successor": {
			"description": "後繼公司或機構的正式完整名稱。若有一個以上的後繼機構，請使用 {{unbulleted list}} 模板列出所有機構名稱。",
			"label": "後繼公司",
			"type": "string"
		},
		"foundation": {
			"description": "公司或機構成立的日期和地點。請使用 {{Start date}} 模板標記日期。地點建議使用「[[國家]][[省份/州份]][[城市]]」的格式，或簡單表記為「[[省份/州份]][[城市]]」。請不要使用國家或地區旗幟模板；國家或地區的旗幟造成不必要的國籍強調。",
			"label": "成立日期和地點",
			"type": "string"
		},
		"founder": {
			"description": "公司或機構的創辦人。若有一位以上的創辦人，請使用 {{unbulleted list}} 模板。若創辦人在維基百科內有獨立的條目，或具有顯著性時，可加入維基連結。",
			"label": "創辦人",
			"type": "string"
		},
		"defunct": {
			"description": "公司或機構中止營運或法定解散的日期。使用 {{End date}} 模板來標記解散日期。",
			"label": "結束日期和地點",
			"example": "{{End date|2000}} 或 {{End date|2000|06|30}}",
			"type": "string"
		},
		"fate": {
			"description": "公司結束營運、解散或變更類型的原因，以及收購或合併此公司的法人全名。",
			"label": "公司結局",
			"example": "「被蘋果電腦收購」或「破產」或「解散」或「與湯普森公司合併」",
			"type": "string"
		},
		"location": {
			"description": "公司總部所在位置。建議使用「[[國家]][[省份/州份]][[城市]]」的格式，或簡單表記為「[[省份/州份]][[城市]]」。請不要使用國家或地區旗幟模板；國家或地區的旗幟造成不必要的國籍強調。",
			"label": "總部位置",
			"type": "string"
		},
		"locations": {
			"description": "公司或機構實體營業據點的數量，以數字表示，後方加上據點類型，並在括號內加註數字適用的年份。",
			"label": "據點數量",
			"example": "200間分店（2016年）",
			"type": "string"
		},
		"area_served": {
			"description": "公司營運的地理範圍。請標示最大的地理範圍，例如某間公司營運範圍包括加拿大的所有省份，請在此項填寫「加拿大」，而不要列出所有省份的名稱。若列出的地名已在先前的參數中出現過，請勿重複添加維基連結。若有一個以上的地點，請使用 {{unbulleted list}} 模板。",
			"label": "服務範圍",
			"type": "string"
		},
		"key_people": {
			"description": "與公司或機構有緊密連結的人物，最多列出四人。若列出一位以上的重要人物，請使用 {{unbulleted list}} 模板。以職位或角色重要性排序列出的人物，並在人名後方以括號加註職銜。若創辦人已在「創辦人」參數中記載，請勿重複在此列出該人物為創辦人；若創辦人在公司內有其他職位（例如董事長、總裁⋯⋯等），可在此列出。請僅列出擔任關鍵重要職位的人物，例如副董事長、執行長、營運長、產品設計副總裁⋯⋯等，請不要列出擔任部門總主管以下職位且不具顯著性的人物。若擔任最高管理階層的人物本身並無重要性，則仍可在此列出，但無須加入維基連結。若列出的人物在維基百科內有獨立條目，請在此以該人物為人熟知的名字標記。若特定人物在公司或機構的歷史發展上扮演重要角色，也可在此列出。若公司或機構已經結束營運，請僅列出最後一任的管理階層人物。",
			"label": "重要人物",
			"type": "string"
		},
		"industry": {
			"description": "公司主要的營運產業類別。若公司的產業類別超過一項以上，請使用 {{unbulleted list}} 模板。",
			"label": "產業類別",
			"example": "家電製造 或 {{unbulleted list|電子產品設計|電子產品銷售|娛樂}}",
			"type": "string"
		},
		"products": {
			"description": "公司具代表性且知名的產品名稱，可包括現行產品與過去的產品。若產品超過一項以上，請使用 {{unbulleted list}} 模板。",
			"label": "產品",
			"example": "{{unbulleted list|[[Microsoft Office]]|[[Microsoft Windows]]}} 或 {{unbulleted list|[[可口可樂]]|[[雪碧]]|[[芬達]]}}",
			"type": "string"
		},
		"services": {
			"description": "公司具代表性且知名的服務名稱，可包括現行服務與過去曾提供過的服務。若服務超過一項以上，請使用 {{unbulleted list}} 模板。",
			"label": "服務",
			"example": "{{unbulleted list|[[金融服務|金融]]|[[保險]]}}",
			"type": "string"
		},
		"revenue": {
			"description": "在最近期的一年，公司從營業行為所獲得的全部收入。營業額通常是來自銷售貨品或服務給顧客，金額以年為單位計算，請在金額後方以括號標註年份。請在貨幣符號加入維基連結。",
			"label": "年營業額",
			"type": "string"
		},
		"operating_income": {
			"description": "每年公司扣除掉利息支出與法律規定應繳稅額之前所得盈利，請在金額後方以括號標註年份。",
			"label": "稅前盈餘",
			"type": "string"
		},
		"net_income": {
			"description": "每年公司盈餘扣除掉利息支出與應繳稅額之後的實際利潤，請在金額後方以括號標註年份。",
			"label": "稅後純利",
			"aliases": [
				"profit"
			],
			"type": "string"
		},
		"aum": {
			"description": "適用於提供金融服務之公司使用。公司的總資產管理規模（assets under management），請在金額後方以括號標註年份。",
			"label": "資產管理規模",
			"type": "string"
		},
		"assets": {
			"description": "在最近期的一年，公司所持有的總資產價值金額，請在金額後方以括號標註年份。",
			"label": "總資產",
			"type": "string"
		},
		"equity": {
			"description": "公司持有的總資產淨值，也稱為股東權益。請在金額後方以括號標註年份。",
			"label": "總資產淨值",
			"example": "{{unbulleted list|{{increase}}NT$32,016,008,004（2011年）|NT$29,752,528,004（2010年）}}",
			"type": "string"
		},
		"owner": {
			"description": "列出持有此私人公司的人物或合資企業。若為公開上市公司，請勿使用本欄位。列出所有權人時請使用完整的正式名稱。若列出項目為一個以上，請使用 {{unbulleted list}} 模板。",
			"label": "所有權人",
			"type": "string"
		},
		"num_employees": {
			"description": "公司聘任人數。",
			"label": "員工人數",
			"type": "string"
		},
		"parent": {
			"description": "控股公司或持股公司，公司所屬事業群。",
			"label": "母公司",
			"type": "string"
		},
		"divisions": {
			"description": "公司主要事業部門。",
			"label": "主要部門",
			"type": "string"
		},
		"subsid": {
			"description": "公司另行開設事業中的主要事業。",
			"label": "主要子公司",
			"type": "string"
		},
		"capital": {
			"description": "公司實收資本額，注意不是資本總額。",
			"label": "實收資本額",
			"type": "string"
		},
		"market_value": {
			"description": "市值。",
			"label": "市值",
			"type": "string"
		},
		"P/E_ratio": {
			"description": "市盈率。",
			"label": "市盈率",
			"type": "string"
		},
		"earnings_per_share": {
			"description": "公司公開發行股票所含盈利。",
			"label": "每股盈利",
			"type": "string"
		},
		"net_asset_value": {
			"description": "公司公開發行股票所含資產淨值。",
			"label": "每股資產淨值",
			"type": "string"
		},
		"accounting_period": {
			"description": "公司營業年度結算時間。",
			"label": "結算期",
			"type": "string"
		},
		"major_shareholder": {
			"description": "公司持有股東。",
			"label": "主要股東",
			"type": "string"
		},
		"slogan": {
			"description": "公司於平面媒體或公司內部所使用宣傳口號。",
			"label": "口號",
			"aliases": [
				"company_slogan"
			],
			"type": "string"
		},
		"homepage": {
			"description": "公司官方網站的最上級網址。請使用 {{URL}} 模板。請勿包含前綴的 www.，除非該網站必須加入前綴才可連結。",
			"label": "官方網站",
			"example": "{{URL|caterpillar.com}}",
			"type": "string"
		},
		"footnotes": {
			"label": "備註",
			"description": "可在此列出信息框內各欄位的時間、名稱和數字的資料來源。",
			"type": "string",
			"default": "default value"
		}
	},
	"format": "block"
}
</templatedata>
</includeonly>

== 注意 ==
{{UF-hcard-org}}

使用本模板的条目可能还需要添加字词转换组。

==追踪分类==
*{{clc|使用未知公司信息框参数的页面}}
*{{clc|公司信息框使用额外地区代码参数的页面}}

== 重定向 ==
* {{tl|公司}}

{{Organization infoboxes}}
<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:公司信息框模板| ]]
[[Category:企業信息框模板|C]]
}}</includeonly>