{{Infobox 
| bodyclass  = vcard
| aboveclass = fn org
| above= {{{Name|{{{name|{{{名稱|{{{名称|{{{校名|<includeonly>{{PAGENAMEBASE}}</includeonly>}}}}}}}}}}}}}}}
| subheader = {{#if:{{{native_name|{{{本名|{{{外文名|{{{原名|{{{english_name|{{{EnglishName|}}}}}}}}}}}}}}}}}} |<span class="nickname" {{#if:{{{native_name_lang|}}}|lang="{{{native_name_lang}}}"}}>{{{native_name|{{{本名|{{{外文名|{{{原名|{{{english_name|{{{EnglishName}}}}}}}}}}}}}}}}}}</span>}}

|image      = {{#invoke:InfoboxImage|InfoboxImage|image={{{校徽|{{{SealImage|}}}}}}|size={{{校徽大小|{{{SealImage_size|}}}}}}|upright=0.91|alt={{{校徽說明|{{{SealImage_alt|}}}}}}}}
|caption    = {{{校徽說明|{{{SealInfo|}}}}}}

|image2     = {{#invoke:InfoboxImage|InfoboxImage|image={{{image|{{{image_name|{{{图像|{{{圖像|{{{圖像名稱|{{{图像名称|}}}}}}}}}}}}}}}}}} |size={{{圖像大小|{{{图像大小|{{{imagesize|{{{image_size|}}}}}}}}}}}}|upright=1.13|alt={{{圖像説明|{{{图像说明|{{{image_alt|}}}}}}}}}}}
|caption2   = {{{圖像説明|{{{图像说明|{{{caption|{{{image_caption|{{{imagecaption|}}}}}}}}}}}}}}}

| labelstyle = white-space:nowrap;
<!--------------------- Names, motto ---------------------->
| class1     = nickname
| data1      = {{{latin_name|{{{拉丁名称|{{{拉丁名稱|}}}}}}}}}

| label2     = 其他名字
| class2     = nickname
| data2      = {{#if:{{{other_names|}}}|{{{other_names}}}|{{{other_name|}}}}}

| label3     = 老校名
| class3     = nickname
| data3      = {{#if:{{{former_names|}}}|{{{former_names}}}|{{{former_name|{{{老校名|{{{原校名|{{{舊校名|{{{旧校名|}}}}}}}}}}}}}}}}}

| label6     = {{{top_free_label|}}}
| data6      = {{#if:{{{top_free_label|}}} |{{{top_free|}}} }}

| label7     = {{{top_free_label1|}}}
| data7      = {{#if:{{{top_free_label1|}}} |{{{top_free1}}} }}

| label8     = {{{top_free_label2|}}}
| data8      = {{#if:{{{top_free_label2|}}} |{{{top_free2}}} }}

| label12     = <span class="note">[[校训]]</span>
| data12      = {{#if:{{{motto|}}}{{{mottoeng|}}}{{{校训|}}}{{{校訓|}}}{{{Motto|}}}|{{#if:{{{motto_lang|}}}|<span lang="{{{motto_lang|}}}">{{{motto|{{{mottoeng|}}}}}}</span>|{{{motto|{{{mottoeng|{{{校训|{{{校訓|{{{Motto|}}}}}}}}}}}}}}}}}}}

| label13     = <span class="note">中译</span>
| data13      = {{{zhmotto|}}}

| label14     = 创办时间
| data14      = {{{Established|}}}{{{established|}}}{{{建校|}}}{{{創校|}}}

| label15     = 復辦時間
| data15      = {{{Re-established|}}}{{{re-established|}}}{{{复办|}}}{{{復辦|}}}{{{复校|}}}{{{復校|}}}

| label16     = 停办时间
| data16      = {{{Closed|}}}{{{closed|}}}{{{闭校|}}}{{{閉校|}}}

| label17     = 校庆日
| data17      = {{{Anniversary|}}}{{{anniversary|}}}{{{校庆日|}}}{{{校慶日|}}}

<!-- 高等学校代码 -->
| label21 = {{#if:{{{local_code_name|}}} |{{Lpid|{{{local_code_name|}}} }}|机构代码 }}
| data21 =   {{#if:{{{local_code_name|}}} |
{{#if:{{{local_code|}}} | {{Lpid|{{{local_code_name|}}}|{{{local_code|}}} }}
}} }}

| label22     = [[学校标识码]]<!-- 中华人民共和国 -->
| data22      = {{#invoke:Wikidata|getValue|P10472|{{{学校标识码|FETCH_WIKIDATA}}}}}

| label23     = [[學校代碼]]<!-- 中华民国 -->
| data23      = {{#invoke:Wikidata|getValue|P7121|{{{学校代码|{{{學校代碼|FETCH_WIKIDATA}}}}}}}}

| label24     = [[综合高等教育数据系统|IPEDS编码]]<!-- 美国 -->
| data24      = {{#invoke:Wikidata|getValue|P1771|{{{IPEDS|FETCH_WIKIDATA}}}}}

| label25     = {{link-ja|大学与高等专门学校代码|大学・高等専門学校コード|JIS代码}}<!-- 日本 -->
| data25      = {{#invoke:Wikidata|getValue|P7251|{{{JIS|FETCH_WIKIDATA}}}}}

| label26     = {{link-en|唯一参考编号|Unique Reference Number|URN编码}}<!-- 英国 -->
| data26      = {{#invoke:Wikidata|getValue|P2253|{{{URN|FETCH_WIKIDATA}}}}}

| label31     = 学校类型
| class31     = category
| data31      = {{{type|}}}{{{類型|}}}{{{类型|}}}{{{類|}}}{{{Type|}}}

| label32     = 宗教背景
| data32      = {{{religious|}}}{{{宗教背景|}}}

| label33     = [[基金|捐贈基金]]
| data33      = {{{endowment|}}}{{{捐款|}}}

| label34     = 预算
| data34      = {{{budget|}}}

| label41     = 主管官员
| data41      = {{{officer_in_charge|}}}{{{主管官员|}}}{{{主管官員|}}}

| label42    = [[校监]]
| class42    = agent
| data42     = {{{chancellor|}}}{{{Chancellor|}}}{{{校监|}}}{{{校監|}}}

| label43    = [[校監|監督]]
| class43    = agent
| data43     = {{{chancellor2|}}}{{{Chancellor2|}}}{{{监督|}}}{{{監督|}}}

| label44     = {{{chairman_label|}}}{{{董事会主持者头衔|}}}{{{董事會主持者頭銜|}}}
| class44     = agent
| data44      = {{#if:{{{chairman_label|}}}|{{{chairman|}}}}}{{#if:{{{董事会主持者头衔|}}}|{{{董事会主持者|}}}}}{{#if:{{{董事會主持者頭銜|}}}|{{{董事會主持者|}}}}}

| label45    = [[党委书记]]
| class45    = agent
| data45     = {{{书记|}}}{{{党委书记|}}}{{{secretary|}}}{{{Secretary|}}}

| label46    = [[校长]]
| class46    = agent
| data46     = {{{president|}}}{{{校长|}}}{{{校長|}}}{{{President|}}}

| label47    = 监管
| data47     = {{{superintendent|}}}{{{监管|}}}{{{監管|}}}

| label48    = 院長
| data48     = {{{dean|}}}{{{院长|}}}{{{院長|}}}

| label49    = 主管
| data49     = {{{director|}}}

| label50    = 党委副书记
| data50     = {{{vice-secretary|}}}{{{党委副书记|}}}{{{副书记|}}}

| label51    = 副校长
| data51     = {{{vice-president|}}}{{{副校长|}}}{{{副校長|}}}

| label52    = 副院长
| data52     = {{{vice-dean|}}}{{{副院长|}}}{{{副院長|}}}

| label53    = 教務長
| data53     = {{{provost|}}}{{{教务长|}}}{{{教務長|}}}

| label54    = [[校长]]<!-- 英國大學校長頭銜即vice_chancellor，不是副職 -->
| data54     = {{{vice_chancellor|}}}

| label55    = [[校长]]
| data55     = {{{principal|{{{rector|}}}}}}

| label56    = {{{head_label|}}}{{{头衔|}}}{{{頭銜|}}}
| data56     = {{#if:{{{head_label|}}}|{{{head|}}}}}{{#if:{{{头衔|}}}|{{{头衔者|}}}}}{{#if:{{{頭銜|}}}|{{{頭銜者|}}}}}

| label61    = 行政人員
| data61     = {{{administrative_staff|}}}<!-- "staff" for backwards compatibility -->

| label62    = 教师人數
| data62     = {{{academic_staff|}}}{{{faculty|}}}{{{教师|}}}{{{教師|}}}{{{师|}}}{{{師|}}}{{{Faculty|}}}

| label63    = 职工人數
| data63     = {{{staff|}}}{{{职工|}}}{{{職工|}}}{{{员工|}}}{{{員工|}}}{{{職員|}}}{{{Staff|}}}

| label64    = 学生人數
| data64     = {{{students|}}}{{{学生|}}}{{{學生|}}}{{{生|}}}{{{Student|}}}{{{enrollment|}}}

| label65    = -{zh-cn:[[本科生]]; zh-tw:[[大學部]]; zh-hk:[[本科生]];}-人數
| data65     =  {{{undergrad|}}}{{{本科生|}}}{{{大學部|}}}{{{Undergraduate|}}}

| label66    = [[研究生]]人數
| data66     = {{{postgrad|}}}{{{研究生|}}}{{{研究|}}}{{{Postgraduate|}}}

| label67    = [[博士生]]人數
| data67     = {{{doctoral|}}}{{{博士生|}}}

| label68    = [[国防生]]人數
| data68     = {{{国防生|}}}

| label69    = 其他在学人员人數
| data69     = {{{other|}}}{{{其他学生|}}}{{{其他學生|}}}

| label70    = 录取率
| data70    = {{{acceptance_rate|}}}{{{录取率|}}}

| label81    = 校址
| class81    = adr
| data81     = {{#if:{{{location|}}}{{{地址|}}}{{{所在|}}}{{{Location|}}}{{{address|}}}|<span class="extended-address">{{{Location|}}}{{{location|}}}{{{地址|}}}{{{所在|}}}{{{address|}}}</span>|{{#if:{{{country|}}}{{{国家|}}}{{{國家|}}}|<span class="country-name">{{{country|}}}{{{国家|}}}{{{國家|}}}</span>}}{{#if:{{{state|}}}{{{州|}}}|<span class="region">{{{state|}}}{{{州|}}}</span>|{{#if:{{{province|}}}{{{省|}}}|<span class="region">{{{province|}}}{{{省|}}}</span>}}}}{{#if:{{{city|}}}{{{市|}}}|<span class="locality">{{{city|}}}{{{市|}}}</span>}}}}{{#if:{{{coor|}}}{{{coordinates|}}}{{{坐标|}}}{{{坐標|}}}|<br />{{{coor|}}}{{{coordinates|}}}{{{坐標|}}}{{{坐标|}}}}}

| label82    = 校區
| data82     = {{{campus|}}}{{{校园|}}}{{{校區|}}}{{{校園|}}}{{{校园环境|}}}{{{校園環境|}}}{{{Campus|}}}

| label83    = 总面积
| data83     = {{{area|}}}{{{面积|}}}{{{面積|}}}{{{Area|}}}

| label84    = 建筑面积
| data84     = {{{covered_area|{{{建筑面积|{{{建築面積|}}}}}}}}}

| label85    = {{{free_label}}}
| data85     = {{#if:{{{free_label|}}}|{{{free|}}}}}

| label86    = 校隊
| data86    = {{{athletics|}}}

| label87    = 體育聯盟
| data87     = {{{conference|}}}{{{体育联盟|}}}{{{體育聯盟|}}}

| label88    = [[校色|代表色]]
| data88     = {{{Colors|}}}{{{colors|}}}{{{校色|}}}{{{代表色|}}}{{{顏色|}}}{{{colours|}}}

| label89    = 昵称
| data89     = {{{nickname|}}}{{{暱稱|}}}{{{昵称|}}}{{{代號|}}}{{{Nickname|}}}

| label90    = [[吉祥物]]
| data90     = {{{mascot|}}}{{{吉祥物|}}}{{{Mascot|}}}

| label91    = [[校刊]]
| data91     = {{{magazine|}}}{{{校刊|}}}

| label92    = 藏書數量
| data92     = {{{藏書數量|}}}

| label93    = 所屬法人
| data93    = {{{legal_person|}}}{{{所屬法人|}}}{{{所属法人|}}}

| label95    = 隶属
| data95    = {{{affiliations|{{{affiliation|{{{Affiliations|}}}}}}}}}{{{隸屬|{{{隶属|}}}}}}{{{機構成員|}}}

| label96    = [[邮政编码|-{zh-cn:邮政编码; zh-tw:郵遞區號; zh-hk:郵區編號; zh-sg:邮递区号}-]]
| data96     = {{{zip|}}}{{{邮编|}}}{{{郵編|}}}

| label97    = 電話號碼
| data97     = {{{telephone|}}}{{{电话号码|}}}{{{電話號碼|}}}

| label98    = 傳真號碼
| data98     = {{{fax|}}}{{{傳真号码|}}}{{{傳真號碼|}}}

| label99    = 網站
| data99     = {{#if:{{{website|{{{網站|{{{网址|{{{网站|{{{網|{{{网|{{{Website|}}}}}}}}}}}}}}}}}}}}}|{{#ifeq:{{{website|{{{網站|{{{网址|{{{网站|{{{網|{{{网|{{{Website|}}}}}}}}}}}}}}}}}}}}}|hide||{{{website|{{{網站|{{{网址|{{{网站|{{{網|{{{网|{{{Website|}}}}}}}}}}}}}}}}}}}}}}}|{{official url}}}}

| data110     = {{#invoke:InfoboxImage|InfoboxImage |image={{{logo|{{{标志|{{{標誌|{{{纹章|{{{Logo|}}}}}}}}}}}}}}}|size={{{logo_size|}}}|sizedefault=frameless|upright={{{logo_upright|}}}|alt={{{logo_alt|}}}}}

|header111   = {{if empty|{{{nrhp|}}}|{{{embedded|}}}|{{{module|}}}}}

| data112     = {{#if:{{{map_type|}}}{{{Position_map|}}}{{{map_locator|}}}{{wikidata|property|{{{qid|}}}|P625}}|
<table style="border-spacing: 0; width: 100%; min-width: 100%" class="mw-collapsible mw-collapsed">
<tr><th style="text-align: center; background-color: #efefef;"><div style="margin:0 3.5em;">位置</div></th></tr><tr><td style="padding-top: 3px">{{Infobox mapframe
 |zoom={{{mapframe-zoom|}}}
 |frame-width={{{mapframe-width|}}}
 |frame-height={{{mapframe-height|}}}
 |marker={{{mapframe-marker|}}}
 |marker-color={{{mapframe-marker-color|{{{mapframe-marker-colour|}}}}}}
 |frame-lat={{{mapframe-lat|{{{mapframe-latitude|}}}}}}
 |frame-long={{{mapframe-long|{{{mapframe-longitude|}}}}}}
 }}</td></tr>
</table>}}
<!---------------------- Location map ---------------------->
| data113     = {{#if:
 | {{Location map|{{{pushpin_map}}}
   | float    = center
   | caption  = {{#if:{{{pushpin_map_caption|}}}|{{{pushpin_map_caption}}}|位於{{#invoke:Location map| data|{{{pushpin_map}}}|name}}}}
   | border   = infobox
   | width    = {{#if:{{{map_size|}}}|{{{map_size}}}|250}}
   | coordinates = {{if empty|{{{coordinates|}}}|{{{coor|}}}}}
   | position = {{{pushpin_label_position|}}}
   }}
}}

|below      = {{{footnotes|{{{脚注|{{{注释|{{{腳註|{{{註釋|}}}}}}}}}}}}}}}
}}<noinclude>{{documentation}}</noinclude>