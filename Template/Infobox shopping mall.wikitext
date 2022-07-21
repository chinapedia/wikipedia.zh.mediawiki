{{Infobox
|child = {{#ifeq:{{{embed|}}}|yes|yes}}
|bodyclass  = vcard
|titleclass = fn org
| labelstyle = white-space: nowrap;
| headerstyle = {{#ifeq:{{{embed|}}}|yes||background-color:#efefef}}

| title      = {{#ifeq:{{{embed|}}}|yes|'''商业建筑详情'''}}
| above      = {{#if:{{{name|{{{shopping_mall_name|}}}}}}{{{名稱|}}}{{{度假村名字|}}}{{{casino|}}}{{{zoo_name|}}}{{{retail_market_name|}}}{{{company_name|}}}|{{{name|{{{shopping_mall_name|}}}}}}{{{名稱|}}}{{{度假村名字|}}}{{{casino|}}}{{{zoo_name|}}}{{{retail_market_name|}}}{{{company_name|}}}|<includeonly>{{PAGENAMEBASE}}</includeonly>}}
|subheader  = {{#if:{{{native_name|}}}{{{company_name_en|}}}{{{原文名稱|}}}{{{英文名稱|}}}|<span class="nickname" {{#if:{{{native_name_lang|}}}|lang="{{{native_name_lang}}}"}}{{#if:{{{company_name_en|}}}{{{英文名稱|}}}|lang="en"}}>{{{native_name|}}}{{{company_name_en|}}}{{#if:{{{英文名稱|}}}|{{{原文名稱|}}}<br>{{{英文名稱|}}}|{{{原文名稱|}}}}}</span>}}

|image      = {{#invoke:InfoboxImage|InfoboxImage|image={{{logo|}}}{{{company_logo|}}}|alt={{{logo_alt|}}}{{{name|{{{shopping_mall_name|<includeonly>{{PAGENAMEBASE}}</includeonly>}}}}}} logo|size={{{logo_size|}}}{{{logo_width|{{{logodimensions|{{{logo_dimensions|}}}}}}}}}|sizedefault=frameless}}
| caption = {{{logo_caption|}}}
|image2     = {{#invoke:InfoboxImage|InfoboxImage|image={{{image|}}}|alt={{{image_alt|}}}|size={{{image_width|{{{imagedimensions|{{{image_dimensions|}}}}}}}}}|sizedefault=frameless}}
|caption2   = {{{caption|}}}{{{image_caption|}}}
|image3     = {{#invoke:InfoboxImage|InfoboxImage|image={{{company_image|}}}{{{圖片|}}}{{{代表圖像|}}}|alt={{{image_alt|}}}|size={{{image_size|}}}{{{image_width|{{{imagedimensions|{{{image_dimensions|}}}}}}}}}{{{圖片尺寸|}}}|sizedefault=frameless}}
|caption3   = {{{圖片說明|}}}

| label1    = 全称
| data1     = {{{official_company_name|}}}{{{正式名稱|}}}
| label2    = 建筑物名称
| data2     ={{{建物名稱|}}}
| label3    = 简称
| data3     = {{{abbreviated_name|}}}
| label4    = 旧称
| data4     = {{{previous_names|}}}{{{names_pre|}}}
| label5    = 词源
| data5    = {{#invoke:Wikidata|getValue|P138|{{{etymology|FETCH_WIKIDATA}}}}}

| header10 = 概要
| label11    = 类型
| data11     = {{#invoke:Wikidata|getValue|P31|{{{type|{{{casino_type|FETCH_WIKIDATA}}}}}}}}
| label12    = 国家／地区
| data12     = {{#if:{{{address|{{{location|{{{所在地|{{{地址|}}}}}}}}}}}}{{{street-address|}}}|{{{country|}}}|{{#invoke:Wikidata|getValue|P17|{{{country|FETCH_WIKIDATA}}}}}}}
| label13   = 行政区
| data13   = {{#if:{{{address|{{{location|}}}}}}{{{street-address|}}}|{{{state|}}}{{{county|}}}{{{city|}}}{{{location_city|}}}{{{location_town|}}}|{{#invoke:Wikidata|getValue|P131|{{{location_town|{{{location_city|FETCH_WIKIDATA}}}}}}}}|}}
| label14    = 地址
| data14     = {{#invoke:Wikidata|getValue|P6375|{{{street-address|{{{address|{{{location|{{{所在地|{{{地址|FETCH_WIKIDATA}}}}}}}}}}}}}}}}}
|class14    = label
| label15    = [[经纬度|坐标]]
| data15     = {{#if:{{{coordinates|}}}|{{#invoke:Coordinates|coordinsert|{{{coordinates|}}}|type:landmark|{{#if:{{{country|}}}|region:{{Country abbreviation|{{{country}}}}}}}}}|{{#if:{{#property:P625}}|{{#invoke:Coordinates|coord|format=dms}}}}}}
| label16    = [[邮政编码|-{zh-cn:邮政编码; zh-tw:郵遞區號;}-]]
| data16     = {{#if: {{{所在地郵遞區號|}}}|{{color|red|〒}}{{{所在地郵遞區號|}}}|{{#invoke:Wikidata|getValue|P281|{{{zip|{{{postcode|{{{zip_code|FETCH_WIKIDATA}}}}}}}}}}}}}
| label21    = 前身
| data21     = {{{前身|}}}{{{營地前身|}}}
| label22   = 建成日期
| data22    = {{{建成日期|}}}
| label23   = 预计开业日期
| data23    = {{{date_opening|}}}
| label24   = 开业日期
| data24    = {{#invoke:Wikidata|getValue|P1329|{{{established|{{{opening_date|{{{open_date|{{{開業日|{{{date_opened|FETCH_WIKIDATA}}}}}}}}}}}}}}}}}
| label25   = 翻修日期
| data25    = {{{renovations|}}}
| label26   = 关闭日期
| data26    = {{{closing_date|}}}{{{閉店日|}}}{{{date_closed|}}}
| label27   = 后继
| data27     = {{{後繼|}}}
| label28   = -{zh-cn:开发商; zh-hk:發展商; zh-tw:開發商}-
| data28    = {{{developer|}}}
| label29   = 经营者
| data29    = {{{operator|}}}
| label30   = 管理者
| data30    = {{{manager|}}}{{{設施管理者|}}}{{{管理者|}}}
| label31   = 所有者
| data31    = {{#invoke:Wikidata|getValue|P127|{{{current-owner|{{{owner|{{{設施所有者|FETCH_WIKIDATA}}}}}}}}}}}
| label32   = 营业执照持有人
| data32    ={{{license_holder|}}}
| label33   = 地主
| data33    ={{{土地所有者|}}}
| label34   = 托建人
| data34   = {{#invoke:Wikidata|getValue|P88|{{{client|FETCH_WIKIDATA}}}}}
| label40   = 代表人物
| data40    = {{{key_people|}}}{{{director|}}}{{{general_manager|}}}
| label41   = 主要股东
| data41    = {{{major_shareholder|}}}
| label42   = [[控股公司|母公司]]
| data42    = {{{parent|}}}
| label43   = 主厨
| data43    = {{{head-chef|}}}
| label44   = 厨师
| data44    = {{{chef|}}}

| header60 = {{#if: {{{company_slogan|}}}{{{slogan|}}}{{{入營類別|}}}{{{theme|}}}{{{營業時間|}}}{{{season|}}}{{{normal_market_days|}}}{{{number_of_stores|}}}{{{店鋪數|}}}{{{number_of_tenants|}}}{{{number_of_anchors|}}}{{{核心店鋪|}}}{{{num_employees|}}}{{{rooms|}}}{{{宿位數目|}}}{{{shows|}}}{{{food-type|}}}{{{dress-code|}}}{{{rating|}}}{{{seating-capacity|}}}{{{reservations|}}}{{{environment_type|}}}{{{goods_sold|}}}{{{annual_visitors|}}}{{{visitors|}}}{{{revenue|}}}|营业-{zh-hant:資訊;zh-hans:信息;}-}}
| label61   = 标语口号
| data61    = {{{company_slogan|}}}{{{slogan|}}}
| label62   = 服务类型
| data62    = {{{入營類別|}}}
| label63   = 主题
| data63    = {{{theme|}}}
| label64   = 营业时间
| data64    = {{{營業時間|}}}{{{season|}}}{{{normal_market_days|}}}
| label65   = 商户数
| data65    = {{{number_of_stores|}}}{{{店鋪數|}}}{{{number_of_tenants|}}}
|class65   = note
| label66   = 主力商戶数
| data66    = {{{number_of_anchors|}}}{{{核心店鋪|}}}
| label67   = 员工数
| data67    = {{{num_employees|}}}
| label68   = 房间数
| data68    = {{{rooms|}}}
<!-- 度假村/野营地兼容参数 -->
| label69   = -{zh-cn:营位数; zh-hk:宿位数}-
| data69    = {{{宿位數目|}}}
<!-- 赌场兼容参数 -->
| label70   = 常驻表演
| data70    = {{{shows|}}}
<!-- 餐厅兼容参数 -->
| label71   = 食品类型
| data71    = {{#invoke:Wikidata|getValue|P2012|{{{food-type|}}}}}
| label72   = 服装特色
| data72    = {{{dress-code|}}}
| label73   = 评分
| data73    = {{{rating|}}}
| label74   = 座位数
| data74    = {{{seating-capacity|}}}
| label75   = 预约服务
| data75    = {{{reservations|}}}
<!--跳蚤市场兼容参数 -->
| label76   = 市场环境
| data76    = {{{environment_type|}}}
| label77   = 贩售商品
| data77    = {{{goods_sold|}}}
| label91   = 年客流数
| data91    = {{{annual_visitors|}}}{{{visitors|}}}
| label92   = 年营业额
| data92    = {{{revenue|}}}
| label93   = 结算期
| data93    = {{{accounting_period|}}}
| data94    = {{{nrhp2|}}}
<!-- 餐厅兼容参数 -->

| header100 = {{#if:{{{architect|}}}{{{architecture_firm|{{{施工|}}}}}}{{{設計者|}}}{{{structural_engineer|}}}{{{architectural_style|{{{style|}}}}}}{{{architectural_style|{{{style|}}}}}}{{{material|}}}{{{material|}}}{{{floors|}}}{{{建地面積|}}}{{{area|}}}{{{floor_area|}}}{{{建築面積|}}}{{{floorspace|}}}{{{樓板面積|}}}{{{商業設施面積|}}}{{{space_gaming|}}}{{#property:P84}}{{#property:P193}}|建筑-{zh-hant:資訊;zh-hans:信息;}-}}
| label101  = 建筑风格
| data101   = {{#invoke:Wikidata|getValue|P149|{{{architectural_style|{{{style|FETCH_WIKIDATA}}}}}}}}
| label102   = 建筑师
| data102   = {{#invoke:Wikidata|getValue|P84|{{{architect|FETCH_WIKIDATA}}}}}
| label103  = 建筑商
| data103   = {{#invoke:Wikidata|getValue|P193|{{{architecture_firm|{{{施工|FETCH_WIKIDATA}}}}}}}}
| label104  = 建筑设计师
| data104   ={{{設計者|}}}
| label105  = 结构工程师
| data105  = {{#invoke:Wikidata|getValue|P631|{{{structural_engineer|FETCH_WIKIDATA}}}}}
| label106   = 建筑材料
| data106   = {{#invoke:Wikidata|getValue|P186|{{{material|FETCH_WIKIDATA}}}}}
| label107  = {{#if:{{{floor_below|}}}{{#property:P1139}}|地上}}层数
| data107   = {{#invoke:Wikidata|getValue|P1101|{{{floors|FETCH_WIKIDATA}}}}}
| label108  = 地下层数
| data108  = {{#invoke:Wikidata|getValue|P1139|{{{floor_below|FETCH_WIKIDATA}}}}}
| label109  = 电梯数
| data109  = {{#invoke:Wikidata|getValue|P1301|{{{elevator_count|FETCH_WIKIDATA}}}}}
| label110  = 高度
| data110   = {{#invoke:Wikidata|getValue|P2048|{{{height|FETCH_WIKIDATA}}}}}
| label111  = 占地面积
| data111   ={{{建地面積|}}}{{{area|}}}
| label112  = 建筑面积
| data112   = {{{floor_area|}}}{{{建築面積|}}}{{{floorspace|}}}
| label113  = 楼面面积
| data113   = {{{樓板面積|}}}
| label114  = 营业面积
| data114   = {{{商業設施面積|}}}
| label115  = 总博弈面积
| data115   = {{{space_gaming|}}}
| label116   = 建筑造价
| data116   = {{#invoke:Wikidata|getValue|P2130|{{{construct_cost|{{{cost|FETCH_WIKIDATA}}}}}}}}
| label117    = 保护情况
| data117    = {{#invoke:Wikidata|getValue|P1435|{{{designations|FETCH_WIKIDATA}}}}}

| header120 = {{#if: {{{商圈人口|}}}{{{parking|}}}{{{停車位數|}}}{{{publictransit|}}}{{{最近車站|}}}{{{最近交流道|}}}{{{attractions|}}}{{{notable_restaurants|}}}{{{members|}}}{{{website|}}}{{{homepage|}}}{{{外部連結|}}}{{{telephone_no|}}}|其他-{zh-hant:資訊;zh-hans:信息;}-}}
| label121  = 商圈人口
| data121   = {{{商圈人口|}}}
| label122  = 停车场
| data122   = {{{parking|}}}{{{停車位數|}}}
| label123  = 公共交通
| data123   = {{{publictransit|}}}
| label124  = 最近车站
| data124   = {{{最近車站|}}}
| label125  = 最近立交桥
| data125   ={{{最近交流道|}}}
| label126  = 著名景点
| data126   ={{{attractions|}}}
| label127  = 著名餐厅
| data127   = {{{notable_restaurants|}}}
| label128  = 其他分店
| data128   = {{{other-locations|}}}
| label129  = 其他-{zh-hant:資訊;zh-hans:信息;}-
| data129   = {{{other-information|}}}
| label130  = 网站
| data130   = {{#if:{{{website|}}}{{{homepage|}}}{{{外部連結|}}}|{{{website|}}}{{{homepage|}}}{{{外部連結|}}}|{{#if:{{#property:P856}}|{{URL|{{#property:P856}}}}}}}}
| label131  = 电话
| data131   = {{#invoke:Wikidata|getValue|P1329|{{{telephone_no|FETCH_WIKIDATA}}}}}

| data141    = {{{nrhp|}}}
| data142   ={{{embedded|}}}
| data143   ={{{module|}}}

| header150 = {{yesno|{{{mapframe|yes}}}
  |yes = {{#if: {{#property:P625}}| {{{map_label|位置图}}} }}
  |no  = {{#if:{{{location_map|}}} | {{{map_label|map}}} }}
  }}
| data151    = {{#if:{{{pushpin_map|}}} |
  {{Location map |{{{pushpin_map|}}}
  | coordinates = {{{coordinates|}}}
  | label    = {{#ifeq:{{lc:{{{pushpin_label_position|}}}}}|none | |{{{casino|{{{name}}}}}} }}
  | alt      = {{{pushpin_map_alt|}}}
  | float    = center
  | mark     = Red pog.svg
  | marksize = 8
  | border   = infobox
  | position = {{#if:{{{pushpin_label_position|}}} |{{{pushpin_label_position|}}} |none}}
  | width    = {{#if:{{{pushpin_mapsize|}}} |{{{pushpin_mapsize|}}} |250}}
  | caption  = {{if empty|{{{pushpin_map_caption|}}} |{{{map_caption|}}} }}
  }}
}}

| data161     = {{If declined|{{{mapframe|}}}||{{Infobox mapframe
 |zoom={{{mapframe-zoom|}}}
 |frame-width={{{mapframe-width|}}}
 |frame-height={{{mapframe-height|}}}
 |marker={{{mapframe-marker|}}}
 |marker-color={{{mapframe-marker-color|{{{mapframe-marker-colour|}}}}}}
 |frame-lat={{{mapframe-lat|{{{mapframe-latitude|}}}}}}
 |frame-long={{{mapframe-long|{{{mapframe-longitude|}}}}}}
 }}
}}
| data162 = {{If declined|{{{mapframe|}}}||{{{mapframe-caption|}}}}}

|belowstyle = {{{belowstyle|}}}
|below      = {{{footnotes|}}}
}}<!--
-->{{#invoke:Check for unknown parameters|check|unknown=[[Category:使用infobox_shopping_mall含有未知參數的頁面|_VALUE_{{PAGENAME}}]]|preview = 頁面使用了[[Template:Infobox shopping mall]]不存在的參數"_VALUE_" |ignoreblank=y
| abbreviated_name | accounting_period | address | annual_visitors | architect | architectural_style | architecture_firm | area | attractions | belowstyle | caption | casino | casino_type | chef | city | client | closing_date | company_image | company_logo | company_name | company_name_en | company_slogan | construct_cost | coordinates | cost | country | county | current-owner | date_closed | date_opened | date_opening | designations | developer | director | dress-code | elevator_count | embed | embedded | environment_type | established | etymology | floors | floorspace | floor_area | floor_below | food-type | footnotes | general_manager | goods_sold | head-chef | height | homepage | image | imagedimensions | image_alt | image_caption | image_dimensions | image_size | image_width | key_people | license_holder | location | location_city | location_map | location_town | logo | logodimensions | logo_alt | logo_caption | logo_dimensions | logo_size | logo_width | major_shareholder | manager | mapframe | mapframe-caption | mapframe-height | mapframe-lat | mapframe-latitude | mapframe-long | mapframe-longitude | mapframe-marker | mapframe-marker-color | mapframe-marker-colour | mapframe-width | mapframe-zoom | map_caption | map_label | material | members | module | name | names_pre | native_name | native_name_lang | normal_market_days | notable_restaurants | nrhp | nrhp2 | number_of_anchors | number_of_stores | number_of_tenants | num_employees | official_company_name | opening_date | open_date | operator | other-information | other-locations | owner | parent | parking | postcode | previous_names | publictransit | pushpin_label_position | pushpin_map | pushpin_mapsize | pushpin_map_alt | pushpin_map_caption | rating | renovations | reservations | retail_market_name | revenue | rooms | season | seating-capacity | shopping_mall_name | shows | slogan | space_gaming | state | street-address | structural_engineer | style | telephone_no | theme | type | visitors | website | zip | zip_code | zoo_name | 代表圖像 | 停車位數 | 入營類別 | 前身 | 原文名稱 | 名稱 | 商圈人口 | 商業設施面積 | 圖片 | 圖片尺寸 | 圖片說明 | 土地所有者 | 地址 | 外部連結 | 宿位數目 | 店鋪數 | 度假村名字 | 建地面積 | 建成日期 | 建物名稱 | 建築面積 | 後繼 | 所在地 | 所在地郵遞區號 | 施工 | 最近交流道 | 最近車站 | 核心店鋪 | 樓板面積 | 正式名稱 | 營地前身 | 營業時間 | 管理者 | 英文名稱 | 設施所有者 | 設施管理者 | 設計者 | 閉店日 | 開業日
}}<noinclude>
{{Documentation}}
</noinclude>