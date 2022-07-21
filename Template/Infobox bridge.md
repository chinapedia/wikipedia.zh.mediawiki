<includeonly>
{{Infobox
| child = {{#ifeq:{{{embed|}}}|yes|yes}}
| bodyclass = vcard
| titleclass = fn org
| above = {{#ifeq:{{{embed|}}}|yes||{{if empty|{{{name|}}}|{{{Name|}}}|{{{bridge_name|}}}|{{{aqueduct_name|}}}|{{PAGENAMEBASE}}}}}}

| subheader = {{#if:{{{ANAME|}}}|{{{ANAME|}}}{{#if:{{{native_name|}}}|<br>}}}}{{#if:{{{native_name|}}}|{{lang|{{{native_name_lang}}}|{{{native_name}}}}}}}

| image = {{#invoke:InfoboxImage|InfoboxImage|image={{{image|{{{Image|}}}}}}|size={{{image_size|250px}}}|upright={{{image_upright|1.1}}}|alt={{{alt|}}}}}
| caption = {{{caption|{{{ImageTitle|}}}}}}

| headerstyle = background-color: #efefef
| labelstyle = white-space:nowrap;

| label1 = [[地理坐标系|-{zh-hans:坐标; zh-hant:座標;}-]]
| data1 = {{#if:{{{coordinates|}}} 
 | {{#invoke:Coordinates|coordinsert|{{{coordinates}}}|type:landmark}}
 | {{#if:{{#Property:P625}} 
 | {{Nowrap| {{Coord|nosave=1|display=inline,title|format=dms}}{{wikidataOI|references|normal+|{{{qid|}}}|P625|fetch={{{refs|yes}}}}} }}
 }}
 }}
| class1 = coordinates

| label2 = [[英國國家格網參考系統|OS格网参考]]
| data2 = {{#if:{{{os_grid_reference|}}}|<span class="plainlinksneverexpand">{{Gbmaprim|{{{os_grid_reference}}}|{{{os_grid_reference}}}}}</span>}}

| label3 = 承載
| data3 = {{{carries|}}}

| label4 = 跨越
| data4 = {{{crosses|}}}

| label5 = 國家／地區
| data5 = {{{country|}}}

| label6 = 地點
| data6 = {{{locale|{{{location|}}}}}}{{#if:{{both|{{{Start|{{{start|}}}}}}|{{{End|{{{end|}}}}}}}}|{{#if:{{{locale|{{{location|}}}}}}|<br>}}起於{{{Start|{{{start|}}}}}}，終於{{{End|{{{end|}}}}}}}}
| class6 = label

| label7 = 官方名稱
| data7 = {{{official_name|}}}
| class7 = nickname

| label8 = 其他名稱
| data8 = {{{other_name|{{{also_known_as|}}}}}}
| class8 = nickname

| label9 = 命名自
| data9 = {{{named_for|}}}

| label10 = 业主
| data10 = {{{owner|}}}

| label11 = 维护单位
| data11 = {{{maint|{{{maintained|}}}}}}

| label12 = 保護狀況
| data12 = {{{heritage|}}}
| class12 = category

| label13 = {{#if:{{{id_type|}}}|{{{id_type}}}|{{tsl|en|National Bridge Inventory|美國國家橋樑數據庫|编号}}}}
| data13 = {{{id|}}}

| label14 = 網站
| data14 = {{{website|}}}

| label15 = 上游桥梁
| data15 = {{#if:{{{preceded|}}}|{{{preceded|}}}|{{{upstream|}}}}}

| label16 = 下游桥梁
| data16 = {{#if:{{{followed|}}}|{{{followed|}}}|{{{downstream|}}}}}

| header17 = {{#if:{{{design|}}}{{{material|}}}{{{material1|}}}{{{material2|}}}{{{length|}}}{{{width|}}}{{{height|}}}{{{depth|}}}{{{traversable|{{{passable|}}}}}}{{{towpath|}}}{{{mainspan|}}}{{{number_spans|{{{spans|}}}}}}{{{piers_in_water|{{{pierswater|}}}}}}{{{load|}}}{{{clearance_above|{{{clearance|}}}}}}{{{clearance_below|{{{below|}}}}}}{{{lanes|}}}{{{life|}}}
 |设计参数}}

| label18 = 桥型
| data18 = {{{design|}}}
| class18 = category

| label19 = 建筑材料
| data19 = {{{material|}}}
| class19 = category

| label22 = 全长
| data22 = {{{length|{{{Long|}}}}}}

| label23 = -{zh-cn:宽;zh-tw:寬;zh-hk:闊;}-度
| data23 = {{{width|}}}

| label24 = 高度
| data24 = {{{height|}}}

| label25 = 水深
| data25 = {{{depth|}}}

| label26 = 可通过
| data26 = {{{traversable|{{{passable|}}}}}}

| label27 = {{le|纤路|Towpath}}
| data27 = {{{towpath|}}}

| label28 = 最大跨度
| data28 = {{{mainspan|}}}

| label29 = 跨數
| data29 = {{{number_spans|{{{spans|}}}}}}

| label30 = 橋墩数
| data30 = {{{piers_in_water|{{{pierswater|}}}}}}

| label31 = 负载限制
| data31 = {{{load|}}}

| label32 = 桥上淨空
| data32 = {{{clearance_above|{{{clearance|}}}}}}

| label33 = 桥下净空
| data33 = {{{clearance_below|{{{below|}}}}}}

| label34 = -{zh-cn:[[車道|车道]]数;zh-tw:[[車道]]數;zh-hk:[[車道|行車線]]數量;}-
| data34 = {{{lanes|}}}

| label35 = 出口数
| data35 = {{{exit|{{{exits|{{{Exit|{{{Exits|}}}}}}}}}}}}

| label36 = 車速限制
| data36 = {{{speed_limit|}}}

| label37 = 設計壽命
| data37 = {{{life|}}}

| header41 = {{#if:{{{num_track|{{{notrack|}}}}}}{{{track_gauge|{{{gauge|}}}}}}{{{structure_gauge|}}}{{{electrification|}}}|轨道特性}}

| label42 = [[鐵路軌道|轨道]]数
| data42 = {{{num_track|{{{notrack|}}}}}}

| label43 = [[轨距]]
| data43 = {{{track_gauge|{{{gauge|}}}}}}

| label44 = {{link-en|構造物限界|Structure gauge}}
| data44 = {{{structure_gauge|}}}

| label45 = [[電氣化鐵路|电气化]]
| data45 = {{{electrification|}}}

| header51 = {{#if:{{{architect|}}}{{{designer|}}}{{{winner|}}}{{{contracted_designer|}}}{{{engineering|}}}{{{builder|}}}{{{fabricator|}}}{{{begin|}}}{{{complete|}}}{{{cost|}}}{{{open|}}}{{{inaugurated|}}}{{{rebuilt|}}}{{{collapsed|}}}{{{closed|}}}{{{replaces|}}}{{{replaced_by|}}}|历史}}

| label52 = 建築師
| data52 = {{{architect|}}}

| label53 = 設計师
| data53 = {{{designer|}}}

| label54 = 首席工程师
| data54 = {{{contracted_designer|}}}

| label55 = 获得奖项
| data55 = {{{winner|}}}

| label56 = 设计单位
| data56 = {{{engineering|}}}

| label57 = 施工單位
| data57 = {{{builder|}}}

| label58 = 钢材生产商
| data58 = {{{fabricator|}}}

| label59 = 开工日
| data59 = {{{begin|}}}

| label60 = 完工日
| data60 = {{{complete|}}}

| label61 = 总造价
| data61 = {{{cost|}}}

| label62 = 启用日
| data62 = {{if empty|{{{dedicated|}}}|{{{inaugurated|}}}}}

| label63 = 开通日
| data63 = {{if empty|{{{opening|}}}|{{{open|}}}|{{{opened|}}}|{{{Open|}}}}}

| label64 = 重建日
| data64 = {{{rebuilt|}}}

| label65 = 毀壞日
| data65 = {{{collapsed|}}}

| label66 = 關閉日
| data66 = {{{closed|}}}

| label67 = 取代
| data67 = {{{replaces|}}}

| label68 = 被取代
| data68 = {{{replaced_by|}}}

| header71 = {{#if:{{{traffic|}}}{{{toll|}}}|统计}}

| label72 = 日交通量
| data72 = {{{traffic|}}}

| label73 = 通行费
| data73 = {{{toll|}}}

| header96 = {{{extra|}}}

| header97 = {{yesno|{{{mapframe|yes}}}
 |yes = {{#if: {{#property:P625}}{{{coordinates|}}} | {{{map_label|地圖}}} }}
 |no = {{#if:{{{location_map|}}} | {{{map_label|Map}}} }}
 }}
| data98 = {{yesno|{{{mapframe|yes}}}
 |no = {{#if:{{both|{{{location_map|}}}|{{{coordinates|{{{坐标|{{{座標|}}}}}}}}}{{#property:P625}}}}|{{Location map|{{{location_map}}}
 |alt = {{{map_alt|}}}
 |coordinates = {{{coordinates|{{{坐标|{{{座標|}}}}}}}}}
 |float = center
 |label = {{if empty| {{{map dot label|}}} | {{{map_dot_label|}}} }}
 |relief = {{{relief|}}}
 |border = infobox
 |caption = {{If empty|{{{map_caption|}}}|{{#invoke:Location map|data|{{{location_map}}}|name}}的位置}}
 |width = {{{map_size|}}}
 }}}}
 |yes = {{Infobox mapframe
 |id = {{{id|}}}
 |coord = {{{coordinates|{{{坐标|{{{座標|}}}}}}}}}
 |zoom = {{{mapframe-zoom|}}}
 |frame-width = {{{mapframe-width|{{{map_size|}}}}}}
 |frame-height = {{{mapframe-height|}}}
 |marker = {{{mapframe-marker|}}}
 |marker-color = {{{mapframe-marker-color|{{{mapframe-marker-colour|}}}}}}
 |frame-coordinates = {{{mapframe-coordinates|{{{mapframe-coord|}}}}}}
 |stroke-color = {{{mapframe-stroke-color|{{{mapframe-stroke-colour|}}}}}}
 |geomask = {{yesno|{{{mapframe-geomask|}}}
 |no= |blank=<!-- no geomask -->
 |yes=P276<!-- Location (P276) from Wikidata -->
 |def={{{mapframe-geomask|}}}<!-- User-supplied P- or Q-number -->
 }}
 }}
 }}
| data99 = {{yesno|{{{mapframe|yes}}} |no=<!-- no mapframe map --> |yes={{{map_caption| {{yesno|{{{mapframe-geomask|}}}
 |no= |blank=<!-- no geomask -->
 |yes={{#if:{{#property:P276}}|{{wikidata|property|{{{id|}}}|P276}}的位置}}
 |def={{#switch:{{Str left|{{{mapframe-geomask|}}}|1}}
 |P|p= {{#if: {{#property:{{{mapframe-geomask|}}}}} | {{wikidata|property|{{{id|}}}|{{{mapframe-geomask|}}}}}的位置 }}
 |Q|q= {{#if: {{Label|{{{mapframe-geomask|}}}}} | {{Label|{{{mapframe-geomask|}}}}}的位置 }}
 }}<!-- end #switch -->
 }}<!-- end inner yesno --> }}}<!-- end map_caption param -->
}}<!-- end outer yesno -->

| header100 = {{{module|}}}

| below = {{#if:{{{references|}}}|參考資料：}}{{{references|}}}
| belowstyle = border-top:1px solid #aaaaaa; text-align:left
}}{{#invoke:Check for unknown parameters|check|unknown={{main other|[[Category:使用未知桥梁信息框参数的页面|_VALUE_{{PAGENAME}}]]}}|preview=页面使用了[[Template:Infobox bridge]]不存在的参数"_VALUE_"|ignoreblank=y| also_known_as | alt | aqueduct_name | architect | begin | below | bridge_name | builder | caption | carries | child | clearance | clearance_above | clearance_below | closed | collapsed | complete | contracted_designer | coordinates | cost | crosses | dedicated | depth | design | designer | downstream | electrification | embed | engineering | extra | fabricator | followed | gauge | height | heritage | id | id_type | image | image_caption | image_size | image_upright | inaugurated | lanes | length | life | load | locale | location | mainspan | maint | maintained | map dot label | map_alt | map_caption | map_dot_label | map_label | map_size | material | material1 | material2 | name | named_for | native_name | native_name_lang | notrack | num_track | number_spans | official_name | open | opened | opening | os_grid_reference | other_name | owner | passable | piers_in_water | pierswater | preceded | rebuilt | references | replaced_by | replaces | spans | structure_gauge | toll | towpath | track_gauge | traffic | traversable | upstream | website | width | winner | mapframe | id | mapframe-zoom | mapframe-width | mapframe-height | mapframe-marker | mapframe-marker-color | mapframe-marker-colour | mapframe-coordinates | mapframe-coord | mapframe-stroke-color | mapframe-stroke-colour | mapframe-geomask }}{{Main other|
{{#if:{{{clearance|}}}|[[Category:使用Template:Infobox bridge的clearance參數的頁面]]}}
{{#if:{{{extra|}}}|[[Category:使用Infobox bridge的extra參數的頁面]]}}
}}</includeonly><noinclude>
{{Documentation}}<!-- PLEASE ADD THIS TEMPLATE'S CATEGORIES TO THE /doc SUBPAGE, THANKS -->
</noinclude>