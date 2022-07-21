{{Infobox
| child      = {{{embed|}}}
| abovestyle = background-color: #CEDEFF;
| above      = {{{name|{{{river_name|<includeonly>{{PAGENAMEBASE}}</includeonly>}}}}}}{{#if:{{{native_name|{{{name_native|}}}}}}|<br /><span class="nickname" {{#if:{{{native_name_lang|{{{name_native_lang|}}}}}}|lang="{{{native_name_lang|{{{name_native_lang}}}}}}"}}>-{{{{native_name|{{{name_native}}}}}}}-</span>}}
| headerstyle= background-color: #CEDEFF;

| image      = {{#invoke:InfoboxImage|InfoboxImage|image={{#invoke:WikidataIB |getPreferredValue |P18 |name=image |qid={{{qid|}}} |suppressfields={{{suppressfields|}}} |fetchwikidata={{{fetchwikidata|ALL}}} |onlysourced=no |noicon=yes|{{{image|{{{image_name|}}}}}}}}|size={{#if:{{{image_size|}}}|{{{image_size|}}}|250px}}|sizedefault=frameless|upright={{{image_upright|1}}}|alt={{{image_alt|}}}|suppressplaceholder=yes}}
| caption    = {{#if:{{{image|{{{image_name|}}}}}}|{{{image_caption|{{{caption|}}}}}}|{{{image_caption|{{#invoke:Wikidata|getImageLegend|FETCH_WIKIDATA}}}}}}}

| image2     = {{#invoke:InfoboxImage|InfoboxImage|image={{{map|{{{image_map|}}}}}}|size={{{map_size|}}}|sizedefault=frameless|alt={{{map_alt|}}}}}
| caption2   = {{{map_caption|}}}

| image3     = {{#if:{{both|{{{pushpin_map|}}}|{{{mouth_coordinates|}}}{{#property:P625}}}}|{{location map|{{{pushpin_map}}}
               |border      =infobox
               |alt         ={{{pushpin_map_alt|}}}
               |float       =center
               |width       ={{{pushpin_map_size|}}}
               |coordinates ={{{mouth_coordinates|}}}
               |relief      ={{if empty|{{{pushpin_map_relief|}}}|1}}
               |caption     ={{{pushpin_map_caption|}}} }} }}

| label2     = 别名
| data2      = {{{name_other|{{{other_name|}}}}}}

| label3     = 词源
| data3      = {{{etymology|}}}

| label4     = {{{subdivision_type1|{{{country_type|[[世界政區索引|國家]]}}}}}}
| data4      = {{{subdivision_name1|{{{country|}}}}}}

| label5     = {{{subdivision_type2|{{{state_type|州}}}}}}
| data5      = {{{subdivision_name2|{{{state|}}}}}}

| label6     = {{{subdivision_type3|{{{region_type|地區}}}}}}
| data6      = {{{subdivision_name3|{{{region|}}}}}}

| label7     = {{{subdivision_type4|{{{district_type|區}}}}}}
| data7      = {{{subdivision_name4|{{{district|}}}}}}

| label8     = {{{subdivision_type5|{{{municipality_type|市}}}}}}
| data8      = {{{subdivision_name5|{{{municipality|}}}}}}

| header15    = {{#if:{{{river_system|}}}{{{progression|}}}{{{source1_location|}}}{{{source1_lat_d|}}}{{{source1_lat_m|}}}{{{source1_lat_s|}}}{{{source1_lat_NS|}}}{{{source1_long_d|}}}{{{source1_long_m|}}}{{{source1_long_s|}}}{{{source1_long_EW|}}}{{{source1_elevation|}}}{{{source1_coordinates|}}}{{{mouth_location|}}}{{{mouth_lat_d|}}}{{{mouth_lat_m|}}}{{{mouth_lat_s|}}}{{{mouth_lat_NS|}}}{{{mouth_long_d|}}}{{{mouth_long_m|}}}{{{mouth_long_s|}}}{{{mouth_long_EW|}}}{{{mouth_elevation|}}}{{{altitude_difference|}}}{{{basin_size|}}}{{{basin_countries|}}}{{{basin_states|}}}{{{basin_cities|}}}{{{basin_landmarks|}}}{{{basin_population|}}}|流域}}

| label16    = [[流域|水系]]
| data16     = {{{river_system|}}}

| label17    = 流向
| data17     = {{{progression|}}}

| rowstyle18 = display:none;
| data18     = {{Infobox river/source|source={{{source1|}}} |loc={{{source1_location|{{{origin|}}}}}} |elev={{{source1_elevation|}}}<!-- 以下是舊版參數 -->{{#if:{{{elevation_m|}}}|{{#if:{{{elevation_ft|}}}|{{formatnum:{{{elevation_m}}}&nbsp;m ({{{elevation_ft}}}&nbsp;ft)}}|{{convert|{{{elevation_m}}}|m|abbr=on}} }}|{{#if:{{{elevation_ft|}}}|{{convert|{{{elevation_ft}}}|ft|abbr=on}} }} }}{{{elevation|}}} |coord={{#if:{{both|{{{source1_lat_d|{{{origin_lat_d|}}}}}}|{{{source1_long_d|{{{origin_long_d|}}}}}}}} | {{geobox coor|{{{source1_lat_d|{{{origin_lat_d|}}}}}}|{{{source1_lat_m|{{{origin_lat_m|}}}}}}|{{{source1_lat_s|{{{origin_lat_s|}}}}}}|{{{source1_lat_NS|{{{origin_lat_NS|}}}}}}|{{{source1_long_d|{{{origin_long_d|}}}}}}|{{{source1_long_m|{{{origin_long_m|}}}}}}|{{{source1_long_s|{{{origin_long_s|}}}}}}|{{{source1_long_EW|{{{origin_long_EW|}}}}}}|{{#if:{{{source1_coord_region|}}}|region:{{{source1_coord_region}}}_}}type:river|format={{{source1_coord_format|}}}|wrap=true|name={{{source1_coord_name|Primary source of {{{name|{{PAGENAMEBASE}}}}}}}}}} }}<!-- 或 -->{{{origin_coordinates|}}}<!-- 或 -->{{{source1_coordinates|}}} |len={{{source1_length|}}} |coord_ref={{{source1_coord_ref|}}} }}

| rowstyle19 = display:none;
| data19     = {{Infobox river/source|第2源头|source={{{source2|}}} |loc={{{source2_location|}}} |elev={{{source2_elevation|}}} |coord={{{source2_coordinates|}}} |len={{{source2_length|}}} |coord_ref={{{source2_coord_ref|}}} }}

| rowstyle20 = display:none;
| data20     = {{Infobox river/source|第3源头|source={{{source3|}}} |loc={{{source3_location|}}} |elev={{{source3_elevation|}}} |coord={{{source3_coordinates|}}} |len={{{source3_length|}}} |coord_ref={{{source3_coord_ref|}}} }}

| rowstyle21 = display:none;
| data21     = {{Infobox river/source|第4源头|source={{{source4|}}} |loc={{{source4_location|}}} |elev={{{source4_elevation|}}} |coord={{{source4_coordinates|}}} |len={{{source4_length|}}} |coord_ref={{{source4_coord_ref|}}} }}

| rowstyle22 = display:none;
| data22     = {{Infobox river/source|第5源头|source={{{source5|}}} |loc={{{source5_location|}}} |elev={{{source5_elevation|}}} |coord={{{source5_coordinates|}}} |len={{{source5_length|}}} |coord_ref={{{source5_coord_ref|}}} }}

| label24    = 河口
| data24     = {{#if:{{{mouth|}}}|{{{mouth}}}|{{#if:{{{mouth_location|}}}{{{mouth_coordinates|}}}{{{mouth_elevation|}}}{{{mouth_elevation_m|}}}{{{mouth_elevation_ft|}}}|&nbsp;}}}}

| label25    = <div style="display:inline;font-weight:normal">&nbsp;-&nbsp;{{nowrap|位置}}</div>
| data25     = {{{mouth_location|}}}

| label26    = <div style="display:inline;font-weight:normal">&nbsp;-&nbsp;{{nowrap|坐標}}</div>
| data26     = {{#if:{{both|{{{mouth_lat_d|}}}|{{{mouth_long_d|}}}}} | {{geobox coor|{{{mouth_lat_d|}}}|{{{mouth_lat_m|}}}|{{{mouth_lat_s|}}}|{{{mouth_lat_NS|}}}|{{{mouth_long_d|}}}|{{{mouth_long_m|}}}|{{{mouth_long_s|}}}|{{{mouth_long_EW|}}}|{{#if:{{{mouth_coord_region|}}}|region:{{{mouth_coord_region}}}_}}type:river|format={{{mouth_coord_format|}}}|wrap=true|name={{{mouth_coord_name|Mouth of {{PAGENAMEBASE}}}}}|title=y}} }}<!-- 或 -->{{{mouth_coordinates|}}}<!-- 參考 -->{{{mouth_coord_ref|}}}

| label27    = <div style="display:inline;font-weight:normal">&nbsp;-&nbsp;海拔</div>
| data27     = {{{mouth_elevation|}}}<!-- 或 -->{{#if:{{{mouth_elevation_m|}}}|{{#if:{{{mouth_elevation_ft|}}}|{{formatnum:{{{mouth_elevation_m}}}&nbsp;m ({{{mouth_elevation_ft}}}&nbsp;ft)}}|{{convert|{{{mouth_elevation_m}}}|m|abbr=on}} }}|{{#if:{{{mouth_elevation_ft|}}}|{{convert|{{{mouth_elevation_ft}}}|ft|abbr=on}} }} }}

| label28    = 落差
| data28     = {{{altitude_difference|}}}

| label29    = 流域面積<!-- TEMP/FOR COMPATIBILITY -->
| data29     = {{#if:{{{watershed_km2|}}}|{{#if:{{{watershed_sqmi|}}}|{{formatnum:{{{watershed_km2}}}&nbsp;km<sup>2</sup> ({{{watershed_sqmi}}}&nbsp;sq&nbsp;mi)}}|{{convert|{{{watershed_km2}}}|km2|abbr=on}} }}|{{#if:{{{watershed_sqmi|}}}|{{convert|{{{watershed_sqmi}}}|sqmi|abbr=on}} }} }}

| label30    = 面積
| data30     = {{{basin_size|{{{watershed|}}}}}}

| label31    = {{nowrap|流經国家}}
| data31     = {{{basin_countries|}}}

| label32    = {{nowrap|流經州份}}
| data32     = {{{basin_states|}}}

| label33    = {{#if:{{{basin_cities|}}}|城市|位置}}
| data33     = {{if empty|{{{basin_cities|}}}|{{{location|}}}}}

| label34    = 地標
| data34     = {{{basin_landmarks|}}}

| label35    = 人口
| data35     = {{{basin_population|}}}

| header44   = {{#if:{{{length|}}}{{{width_min|}}}{{{width_avg|}}}{{{width_max|}}}{{{depth_min|}}}{{{depth_avg|}}}{{{depth_max|}}}{{{discharge1_location|}}}{{{discharge1_min|}}}{{{discharge1_avg|}}}{{{discharge1_max|}}}|本貌}}

| label45     = 長度<!-- TEMP/FOR COMPATIBILITY -->
| data45      = {{#if:{{{length_km|}}}|{{#if:{{{length_mi|}}}|{{formatnum:{{{length_km}}}&nbsp;km ({{{length_mi}}}&nbsp;mi)}}|{{convert|{{{length_km}}}|km|abbr=on}} }}|{{#if:{{{length_mi|}}}|{{convert|{{{length_mi}}}|mi|abbr=on}} }} }}

| label46    = 長度
| data46     = {{{length|}}}

| label47    = 寬度
| data47     = {{#if:{{{width_min|}}}{{{width_avg|}}}{{{width_max|}}}|{{plainlist|
{{#if:{{{width_min|}}}|
* '''最小寬度：'''<br>{{{width_min|}}}}}
{{#if:{{{width_avg|}}}|
* '''平均寬度：'''<br>{{{width_avg|}}}}}
{{#if:{{{width_max|}}}|
* '''最大寬度：'''<br>{{{width_max|}}}}}}}
}}

| label48    = 深度
| data48     = {{#if:{{{depth_min|}}}{{{depth_avg|}}}{{{depth_max|}}}|{{plainlist|
{{#if:{{{depth_min|}}}|
* '''最小深度：'''<br>{{{depth_min|}}}}}
{{#if:{{{depth_avg|}}}|
* '''平均深度：'''<br>{{{depth_avg|}}}}}
{{#if:{{{depth_max|}}}|
* '''最大深度：'''<br>{{{depth_max|}}}}}}}
}}

| label49     = 平均流量 <!-- TEMP/FOR COMPATIBILITY -->
| data49      = {{#if:{{{discharge_m3/s|}}}{{{discharge_cuft/s|}}}|{{#if:{{{discharge_m3/s|}}}|{{#if:{{{discharge_cuft/s|}}}|{{formatnum:{{{discharge_m3/s}}}&nbsp;[[cubic metres per second|m<sup>3</sup>/s]] ({{{discharge_cuft/s}}}&nbsp;[[cubic feet per second|cu&nbsp;ft/s]])}}|{{convert|{{{discharge_m3/s}}}|m3/s|abbr=on}} }}|{{#if:{{{discharge_cuft/s|}}}|{{convert|{{{discharge_cuft/s}}}|cuft/s|abbr=on}} }} }} }}{{{discharge|}}}

| label50    = 流量
| data50     = {{#if:{{{discharge1_location|}}}{{{discharge1_min|}}}{{{discharge1_avg|}}}{{{discharge1_max|}}}|{{plainlist|
{{#if:{{{discharge1_location|}}}|
* '''地點：'''<br>{{{discharge1_location|}}}}}
{{#if:{{{discharge1_min|}}}|
* '''最低速率：'''<br>{{{discharge1_min|}}}}}
{{#if:{{{discharge1_avg|}}}|
* '''平均速率：'''<br>{{{discharge1_avg|}}}}}
{{#if:{{{discharge1_max|}}}|
* '''最高速率：'''<br>{{{discharge1_max|}}}}}}}
}}

| label51    = 流量<br>（位置2）
| data51     = {{#if:{{{discharge2_location|}}}{{{discharge2_min|}}}{{{discharge2_avg|}}}{{{discharge2_max|}}}|{{plainlist|
{{#if:{{{discharge2_location|}}}|
* '''地點：'''<br>{{{discharge2_location|}}}}}
{{#if:{{{discharge2_min|}}}|
* '''最低速率：'''<br>{{{discharge2_min|}}}}}
{{#if:{{{discharge2_avg|}}}|
* '''平均速率：'''<br>{{{discharge2_avg|}}}}}
{{#if:{{{discharge2_max|}}}|
* '''最高速率：'''<br>{{{discharge2_max|}}}}}}}
}}

| label52    = 流量<br>（位置3）
| data52     = {{#if:{{{discharge3_location|}}}{{{discharge3_min|}}}{{{discharge3_avg|}}}{{{discharge3_max|}}}|{{plainlist|
{{#if:{{{discharge3_location|}}}|
* '''地點：'''<br>{{{discharge3_location|}}}}}
{{#if:{{{discharge3_min|}}}|
* '''最低速率：'''<br>{{{discharge3_min|}}}}}
{{#if:{{{discharge3_avg|}}}|
* '''平均速率：'''<br>{{{discharge3_avg|}}}}}
{{#if:{{{discharge3_max|}}}|
* '''最高速率：'''<br>{{{discharge3_max|}}}}}}}
}}

| label53    = 流量<br>（位置4）
| data53     = {{#if:{{{discharge4_location|}}}{{{discharge4_min|}}}{{{discharge4_avg|}}}{{{discharge4_max|}}}|{{plainlist|
{{#if:{{{discharge4_location|}}}|
* '''地點：'''<br>{{{discharge4_location|}}}}}
{{#if:{{{discharge4_min|}}}|
* '''最低速率：'''<br>{{{discharge4_min|}}}}}
{{#if:{{{discharge4_avg|}}}|
* '''平均速率：'''<br>{{{discharge4_avg|}}}}}
{{#if:{{{discharge4_max|}}}|
* '''最高速率：'''<br>{{{discharge4_max|}}}}}}}
}}

| label54    = 流量<br>（位置5）
| data54     = {{#if:{{{discharge5_location|}}}{{{discharge5_min|}}}{{{discharge5_avg|}}}{{{discharge5_max|}}}|{{plainlist|
{{#if:{{{discharge5_location|}}}|
* '''地點：'''<br>{{{discharge5_location|}}}}}
{{#if:{{{discharge5_min|}}}|
* '''最低速率：'''<br>{{{discharge5_min|}}}}}
{{#if:{{{discharge5_avg|}}}|
* '''平均速率：'''<br>{{{discharge5_avg|}}}}}
{{#if:{{{discharge5_max|}}}|
* '''最高速率：'''<br>{{{discharge5_max|}}}}}}}
}}

| header65   = {{#if:{{{tributaries_left|}}}{{{tributaries_right|}}}{{{waterbodies|{{{water_bodies|}}}}}}{{{waterfalls|}}}{{{bridges|}}}{{{ports|}}}{{{custom_label|}}}{{{custom_data|}}}|特徵}}

| label66    = 支流
| data66     = {{#if:{{{tributaries_left|{{{left_tribs|}}}}}}{{{tributaries_right|{{{right_tribs|}}}}}}|{{plainlist|
{{#if:{{{tributaries_left|{{{left_tribs|}}}}}}|
* '''左：'''<br>{{{tributaries_left|{{{left_tribs|}}}}}}
}}{{#if:{{{tributaries_right|{{{right_tribs|}}}}}}|
* '''右：'''<br>{{{tributaries_right|{{{right_tribs|}}}}}}}}
}} }}

| label67    = 水體
| data67     = {{{waterbodies|{{{water_bodies|{{{lakes|}}}}}}}}}

| label68    = 瀑布
| data68     = {{{waterfalls|}}}

| label69    = 橋樑
| data69     = {{{bridges|}}}

| label70    = 內陸港
| data70     = {{{ports|}}}

| label71    = {{{custom_label|{{{blank_name|}}}}}}
| data71     = {{{custom_data|{{{blank_info|}}}}}}

| below      = {{{extra|}}}

}}<noinclude>{{documentation}}<!-- place category on the /doc page --></noinclude>