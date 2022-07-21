<includeonly>{{Infobox
|name = Infobox train
|bodyclass = vcard hProduct
|bodystyle = width:{{#if:{{{box_width|{{{信息框寬度|}}}}}}|{{{box_width|{{{信息框寬度|}}}}}}|300px}};
|headerstyle = background:#E3E3E3;
|labelstyle = white-space:nowrap
|belowstyle = background:#eee;

|above = {{{車輛名稱|{{{name|{{PAGENAMEBASE}}}}}}}}{{#if:{{{原文名稱|{{{native_name|}}}}}}|<br><span class="nickname" {{#if:{{{原文語言|{{{native_name_lang|}}}}}}|lang="{{{原文語言|{{{native_name_lang}}}}}}"}}><small>{{{原文名稱|{{{native_name}}}}}}</small></span>}}
|abovestyle = background-color:{{ #if: {{{公司色|{{{background_color|}}}}}} | {{{公司色|{{{background_color}}}}}} | white}}; color: {{ #if: {{{標題色|{{{name_color|}}}}}} | {{{標題色|{{{name_color}}}}}} | {{ #if: {{{公司色|{{{background_color|}}}}}} | white | }} }};  padding:5px; line-height:120%;
|aboveclass = fn

|image = {{#invoke:InfoboxImage|InfoboxImage|image={{{圖像|{{{image|}}}}}}|size={{{pxl|{{{image_size|290px}}}}}}|alt={{{圖像替代文字|{{{imagealt|}}}}}}}}
|caption = {{{圖像說明|{{{caption|}}}}}}
|image2 = {{#invoke:InfoboxImage|InfoboxImage|image={{{圖像2|{{{image2|{{{interiorimage|}}}}}}}}}|size={{{pxl2|{{{image_size2|290px}}}}}}|alt={{{圖像替代文字2|{{{imagealt2|{{{interiorimagealt|}}}}}}}}}}}
|caption2 = {{{圖像說明2|{{{caption2|{{{interiorcaption|}}}}}}}}}
|image3 = {{#invoke:InfoboxImage|InfoboxImage|image={{{圖像3|{{{image3|}}}}}}|size={{{pxl3|{{{image_size3|290px}}}}}}|alt={{{圖像替代文字3|{{{imagealt3|}}}}}}}}
|caption3 = {{{圖像說明3|{{{caption3|}}}}}}

|header1 = 概覽

|label2 = 類型
|data2 = {{{類型|{{{traction|}}}}}}

|label3 = 型號
|data3 = {{{型號|{{{diagram|}}}}}}

|label4 = 原產國
|data4 = {{{原產國|{{{origin|}}}}}}

|label5 = 製造
|class5 = brand
|data5 = {{{製造商|{{{製造|{{{manufacturer|}}}}}}}}}

|label6 = 改造
|data6 = {{{改造商|{{{改造|{{{Remodeler|}}}}}}}}}

|label7 = 組裝
|data7 = {{{組裝|{{{assembly|}}}}}}

|label8 = 訂單編號
|data8 = {{{訂單編號|{{{ordernumber|}}}}}}

|label9 = 產量
|data9 = {{{產量|{{{numberbuilt|}}}}}}

|label10 = 車輛總數
|data10 = {{{輛數|{{{車輛總數|{{{numbercar|}}}}}}}}}

|label11 = 車輛編號
|data11 = {{{車輛編號|{{{fleetnumbers|}}}}}}

|label12 = {{nowrap|製造年份}}
|data12 = {{ #if: {{{製造年份|{{{yearconstruction|}}}}}} | {{{製造年份|{{{yearconstruction}}}}}} | {{ #if: {{{投產年份|{{{constructionstart|}}}}}} | {{{投產年份|{{{constructionstart}}}}}}{{ #if: {{{停產年份|{{{constructionend|}}}}}} | －{{{停產年份|{{{constructionend}}}}}} }} }} }} 

|label13 = {{nowrap|改造年份}}
|data13 = {{{改造年份|{{{改造年份|{{{Yearofrenovation|}}}}}}}}}

|label14 = -{zh-hant:投入服務; zh-hans:投入运营;}-
|data14 = {{{投入服務日期|{{{投入服務|{{{yearservice|}}}}}}}}}

|label15 = -{zh-hant:退出服務; zh-hans:退出运营;}-
|data15 = {{{退出服務|{{{yearserviceend|}}}}}}

|label16 = 服务时间
 |data16 = {{{service|}}}

|label17 = 報廢
|data17 = {{{報廢|{{{yearscrapped|}}}}}}

|label18 = 主要用戶
|data18 = {{{用戶|{{{operator|}}}}}}

|label19 = 營運路線
|data19 = {{{路線|{{{lines|}}}}}}

|label20 = 車輛基地
|data20 = {{{車輛基地|{{{depots|}}}}}}

|header30 = 技術數據

|label31 = {{nowrap|列車編組}}
|data31 = {{{列車編組|{{{編組|{{{formation|}}}}}}}}}

|label32 = [[UIC铁路机车轴式分类|UIC軸式]]
|data32 = {{{UIC軸式|{{{uicclass|}}}}}}

|label33 = [[AAR轴式|AAR軸式]]
|data33 = {{{AAR軸式|{{{aarwheels|}}}}}}

|label34 = 編組長度
|data34 = {{ #if: {{{編組長度|{{{trainlength|}}}}}} | {{{編組長度|{{{trainlength}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||m}} }}

|label35 = 車輛長度
|data35 = {{ #if: {{{全長|{{{車輛長度|{{{carlength|}}}}}}}}} | {{{全長|{{{車輛長度|{{{carlength}}}}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||mm}} }}

|label36 = 車體長度
|data36 = {{ #if: {{{車體長度|{{{bodylength|}}}}}} | {{{車體長度|{{{bodylength}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||mm}} }}

|label37 = 車體-{zh-hant:闊度; zh-hans:宽度}-
|data37 = {{ #if: {{{全闊|{{{車輛寬度|{{{width|}}}}}}}}} | {{{全闊|{{{車輛寬度|{{{width}}}}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||mm}} }}

|label38 = 車體高度
|data38 = {{ #if: {{{全高|{{{車輛高度|{{{height|}}}}}}}}} | {{{全高|{{{車輛高度|{{{height}}}}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||mm}} }}

|label39 = -{zh-cn:地板高度; zh-tw:地板高度; zh-hk:地台高度;}-
|data39 = {{ #if: {{{地板高度|{{{地台高度|{{{floorheight|}}}}}}}}} | {{{地板高度|{{{地台高度|{{{floorheight}}}}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||mm}} }}

|label40 = 適應-{zh-cn:站台高度; zh-tw:月台高度; zh-hk:月台高度;}-
|data40 = {{ #if: {{{月台高度|{{{platformheight|}}}}}} | {{{月台高度|{{{platformheight}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||mm}} }}

|label41 = 車輛重量
|data41 = {{ #if: {{{車輛重量|{{{weight|}}}}}} | {{{車輛重量|{{{weight}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||t}} }}

|label42 = 編組重量
|data42 = {{ #if: {{{編組總重量|{{{trainweight|}}}}}} | {{{編組總重量|{{{trainweight}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||t}} }}

|label43 = 軸重
|data43 = {{ #if: {{{軸重|{{{axleload|}}}}}} | {{{軸重|{{{axleload}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||t}} }}

|label44 = [[轴距]]
|data44 = {{ #if: {{{軸距|{{{wheelbase|}}}}}} | {{{軸距|{{{wheelbase}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||mm}} }}

|label45 = [[轨距]]
|data45 = {{ #if: {{{軌距|{{{gauge|}}}}}} | {{{軌距|{{{gauge}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||mm}} }}

|label46 = 輪徑
|data46 = {{ #if: {{{輪徑|{{{wheeldiameter|}}}}}} | {{{輪徑|{{{wheeldiameter}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||mm}} }}

|label47 = {{nowrap|[[最小曲线半径|通過最小曲線半徑]]}}
|data47 = {{ #if: {{{最小曲線半徑|{{{minimumcurve|}}}}}} | {{{最小曲線半徑|{{{minimumcurve}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||m}} }}

|label48 = [[轉向架]]
|data48 = {{{轉向架|{{{bogies|}}}}}}

|label49 = 車體材質
|data49 = {{{車體物料|{{{車身物料|{{{carbody|}}}}}}}}}

|label50 = 車門
|data50 = {{{車門|{{{doors|}}}}}}

|label51 = 車輛-{zh-hant:載客量; zh-hans:定员}-
|data51 = {{{載客量|{{{capacity|}}}}}}

|label52 = 編組-{zh-hant:載客量; zh-hans:定员}-
|data52 = {{{編組載客量|{{{traincapacity|}}}}}}

|label61 = 營運速度
|data61 = {{ #if: {{{營運最高速度|{{{maxspeed|}}}}}} | {{{營運最高速度|{{{maxspeed}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||km/h}} }}

|label62 = 設計最高速度
|data62 = {{ #if: {{{設計最高速度|{{{structuralspeed|}}}}}} | {{{設計最高速度|{{{structuralspeed}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||km/h}} }}

|label63 = 試驗速度
|data63 = {{ #if: {{{試驗最高速度|{{{testspeed|}}}}}} | {{{試驗最高速度|{{{testspeed}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||km/h}} }}

|label64 = 持續速度
|data64 = {{ #if: {{{持續速度|{{{continuousspeed|}}}}}} | {{{持續速度|{{{continuousspeed}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||km/h}} }}

|label65 = 起動加速度
|data65 = {{ #if: {{{起動加速度|{{{acceleration|}}}}}} | {{{起動加速度|{{{acceleration}}}}}}{{wrap}}}}

|label66 = 常用減速度
|data66 = {{ #if: {{{常用減速度|{{{減速度（正常）|{{{deceleration|}}}}}}}}} | {{{常用減速度|{{{減速度（正常）|{{{deceleration}}}}}}}}}{{wrap}}}}

|label67 = 緊急減速度
|data67 = {{ #if: {{{緊急減速度|{{{減速度（緊急）|{{{emergency_deceleration|}}}}}}}}} | {{{緊急減速度|{{{減速度（緊急）|{{{emergency_deceleration}}}}}}}}}{{wrap}}}}

|label68 = [[牵引力]]
|data68 = {{ #if: {{{牽引力|{{{tractiveeffort|}}}}}} | {{{牽引力|{{{tractiveeffort}}}}}}{{wrap}}{{#ifeq:{{{unit|}}}|self||kN}} }}

|label81 = [[電氣化鐵路|供電制式]]
|data81 = {{{電化方式|{{{供電制式|{{{electricsystem|}}}}}}}}}

|label82 = 受流方式
|data82 = {{{受流方式|{{{collectionmethod|}}}}}}

|label83 = 發動機
|data83 = {{{發動機|{{{engine|}}}}}}

|label84 = 發動機功率
|data84 = {{{發動機功率|{{{enginepower|}}}}}}

|label85 = 燃油儲備量
|data85 = {{{燃油量|{{{fuelcapacity|}}}}}}

|label86 = 傳動方式
|data86 = {{{傳動方式|{{{transmission|}}}}}}

|label87 = 傳動裝置
|data87 = {{{傳動裝置|{{{transmissiondevice|}}}}}}

|label88 = 牽引發電機
|data88 = {{{牽引發電機|{{{generator|{{{alternator|}}}}}}}}}

|label89 = {{nowrap|[[牽引電動機]]}}
|data89 = {{{主電動機|{{{電動機|{{{牽引電動機|{{{tractionmotor|}}}}}}}}}}}}

|label90 = 電動機功率
|data90 = {{{電動機輸出|{{{motorpower|}}}}}}

|label91 = 牽引功率
|data91 = {{{編組輸出|{{{trainpower|}}}}}}

|label92 = 傳動比
|data92 = {{{齒輪比|{{{傳動比|{{{gearratio|}}}}}}}}}

|label93 = 控制裝置
|data93 = {{{控制裝置|{{{control|}}}}}}

|label94 = 驅動裝置
|data94 = {{{驅動裝置|{{{驅動方式|{{{drive|}}}}}}}}}

|label95 = 變速段數
|data95 = {{{變速段數|{{{shiftgear|}}}}}}

|label96 = [[车钩|連接器]]
|data96 = {{{連接器|{{{coupling|}}}}}}

|label97 = 制動方式
|data97 = {{{制動方式|{{{brakes|}}}}}}

|label98 = 制動功率
|data98 = {{{制動功率|{{{brakepower|}}}}}}

|label99 = {{nowrap|[[鐵路安全裝置|安全防護系統]]}}
|data99 = {{{保安裝置|{{{safety|}}}}}}

|label100 = 整體控制
|data100 = {{{multipleworking|}}}

|label101 = 車燈類型
|data101 = {{{light|}}}

|label103 = 座位
|data103 = {{{seating|{{{CarSeating|}}}}}}

|label104 = 車型分類
|data104 = {{{stocktype|{{{StockType|}}}}}}

|label105 = [[暖通空調]]
|data105 = {{{hvac|}}}

|label106 = 供电制式
|data106 = {{{powersupply|}}}

|header110 = {{#if:{{{技術平台|{{{family|}}}}}}{{{外形設計|{{{designer|}}}}}}{{{内部設計|{{{interiordesigner|}}}}}}{{{取代了|{{{replaced|}}}}}}{{{暱稱|{{{nickname|}}}}}}{{{備註|{{{note|}}}}}}|其它事项}}

|label111 = 技術平台
|data111 = {{{技術平台|{{{family|}}}}}}

|label112 = 外观設計
|data112 = {{{外形設計|{{{designer|}}}}}}

|label113 = 内饰設計
|data113 = {{{内部設計|{{{interiordesigner|}}}}}}

|label114 = 取代了
|data114 = {{{取代了|{{{replaced|}}}}}}

|label115 = 暱稱
|data115 = {{{暱稱|{{{nickname|}}}}}}

|label116 = 備註
|data116 = {{ #if: {{{備註|{{{note|}}}}}} | <nowiki></nowiki><!-- 為了容許輸入列表而加上 -->{{{備註|{{{note|}}}}}} }}

|below = {{{全寬備註|{{{wide_note|}}}}}}
}}</includeonly><noinclude>{{Documentation}}</noinclude>