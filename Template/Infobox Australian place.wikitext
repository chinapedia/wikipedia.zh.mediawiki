<noinclude>{{noteTA|G1=Unit|G2=Country}}{{Wraps infobox|Infobox settlement|已停用}}</noinclude>
{{Infobox settlement
| name                    = {{{name|<includeonly>{{PAGENAMEBASE}}</includeonly>}}}
| native_name             = {{{native_name|}}}
| native_name_lang        = en
| other_name              = {{#ifeq:{{{type|}}}|protected|{{IUCN banner|{{{iucn_category|}}} }} }}
| image_skyline           = {{{image|}}}
| imagesize               = {{{image_size|{{{imagesize|}}}}}}
| image_alt               = {{{image_alt|{{{alt|}}}}}}
| image_caption           = {{{caption|}}}
| image_blank_emblem      = {{{logo|}}}
| blank_emblem_size       = {{{logosize|}}}
| blank_emblem_alt        = {{{logo_alt|{{{alt|}}}}}}
| image_map1              = {{{image2|}}}
| mapsize1                = {{{image2_size|{{{image2size|}}}}}}
| map_alt1                = {{{image2_alt|{{{alt2|}}}}}}
| map_caption1            = {{{caption2|}}}
| pushpin_map             = {{#if: {{{force_national_map|}}} | Australia | Australia {{ #switch: {{lc:{{{state|}}}}}
  |sa       = South Australia
  |vic      = Victoria
  |nsw      = New South Wales
  |qld      = Queensland
  |nt       = Northern Territory
  |wa       = Western Australia
  |tas      = Tasmania
  |act      = Australian Capital Territory
  |jbt      = Jervis Bay Territory
  |ni       = Norfolk Island
  |#default = 
  }}{{#if:{{{use_lga_map|}}}|_{{{lga|}}}}}}}
| pushpin_label_position  = {{{pushpin_label_position|}}}
| pushpin_map_alt         = {{{map_alt|}}}
| pushpin_mapsize         = {{#if: {{{force_national_map|}}}|270|{{ #switch: {{lc:{{{state|}}} }}
   |sa       = 230
   |qld      = 190
   |nt       = 190
   |wa       = 180
   |tas      = 210
   |act      = 180
   |270
   }} }}
| pushpin_relief          = {{{relief|}}}
| pushpin_map_caption     = {{{pushpin_map_caption|}}}
| coordinates             = {{#if:{{both|{{{latitude|{{{latd|}}}}}}|{{{longitude|{{{longd|}}}}}}}}|
{{Geobox coor|{{#expr:abs({{{latitude|{{{latd|}}}}}})}}|{{{latm|}}}|{{{lats|}}}|S|{{{longitude|{{{longd|}}}}}}|{{{longm|}}}|{{{longs|}}}|E|type:{{#if: {{{coord_type|}}}|{{{coord_type|}}}|{{#ifeq:{{{type|}}}|protected|landmark|city}}}}_region:{{ #switch: {{lc:{{{state|}}} }}
  |sa       = AU-SA
  |vic      = AU-VIC
  |nsw      = AU-NSW
  |qld      = AU-QLD
  |nt       = AU-NT
  |wa       = AU-WA
  |tas      = AU-TAS
  |act      = AU-ACT
  |jbt      = AU-JBT
  |ni       = NF
  |#default = AU
  }}{{#if:{{{map_scale|}}}|_scale:{{{map_scale|}}}|}}|title={{#ifeq:{{{coordinates_display|}}}|inline||1}}}}|{{#if:{{{coordinates|}}}|{{{coordinates}}} }} }}
| subdivision_type        = [[世界政區索引|国家]]
| subdivision_name        = {{AUS}}
| subdivision_type1       = [[澳大利亚行政区划|一级行政区]]
| subdivision_name1       = {{ #switch: {{lc:{{{state|error}}} }}
| sa | 南澳大利亞州 | 南澳州 = [[南澳大利亚州]]
| vic | 維多利亞州 = [[維多利亞州]]
| nsw | 新南威尔士州 | 新南威爾斯州 | 新南威爾士州 = [[新南威爾士州]]
| qld | 昆士蘭州 = [[昆士蘭州]]
| nt | 北領地 = [[北領地]]
| wa | 西澳大利亞州 | 西澳州 = [[西澳大利亚州]]
| act | 澳大利亞首都特區 | 澳洲首都特區 | 澳大利亚首都领地 | 澳洲首都領地 = [[澳大利亚首都领地]]
| tas | 塔斯馬尼亞州 | 塔斯曼尼亞州 = [[塔斯馬尼亞州]]
| jbt | 傑維斯灣領地 = [[傑維斯灣領地]]
| ni | 諾福克島 = [[诺福克岛]]
| au | 澳大利亞 | 澳洲 = 
|{{auto link|{{{state|}}}}}
|error      = 
}}
| subdivision_type2       = {{ #switch: {{lc:{{{state|}}}}}
 | sa  = [[南澳大利亞州地方政府區域|地方政府区域]]
 | vic = [[維多利亞州地方政府區域|地方政府区域]]
 | nsw = [[新南威爾斯州地方政府區域|地方政府区域]]
 | qld = [[昆士蘭州地方政府區域|地方政府区域]]
 | nt  = [[北領地地方政府區域|地方政府区域]]
 | wa  = [[西澳大利亞州地方政府區域|地方政府区域]]
 | tas = [[塔斯马尼亚州地方政府区域|地方政府区域]]
 | act = 区域
 | [[澳大利亞地方政府|地方政府区域]]
  }}
| subdivision_name2       = {{#if:{{{lga|}}}|{{#if: {{{lga2|}}}|<ul style="margin-top: 0px; margin-bottom: 0px;"><li>}} {{auto link|{{{lga}}}}}{{#if: {{{lga2|}}}|<li> {{auto link|{{{lga2}}}}}}}{{#if: {{{lga3|}}}|<li> {{auto link|{{{lga3}}}}}}}{{#if: {{{lga4|}}}|<li> {{auto link|{{{lga4}}}}}}}{{#if: {{{lga5|}}}|<li> {{auto link|{{{lga5}}}}}}}{{#if: {{{lga2|}}}|</ul> }}}}
| subdivision_type3       = [[澳大利亞地區列表|地區]]
| subdivision_name3       = {{#if:{{{region|}}}|{{auto link|{{{region}}}}} }}
| subdivision_type4       = [[澳大利亞土地行政區劃|郡縣]]
| subdivision_name4       = {{#if:{{{county|}}}|{{auto link|{{{county}}}}} }}
| established_title       = 建立
| established_date        = {{{established|{{{est|}}}}}}{{#if:{{{established|{{{est|}}}}}}|{{{established_footnotes|}}}|}}
| extinct_title           = 廢止
| extinct_date            = {{{abolished|}}}
| seat                    = {{{seat|}}}
| leader_title            = {{#if:{{{mayortitle|}}}|{{{mayortitle|}}}|市長}}
| leader_name             = {{#ifeq:{{{type|}}}|lga|{{{mayor|}}} }}
| area_footnotes          = {{{area_footnotes|}}}
| area_total_km2          = {{{area|}}}
| elevation_footnotes     = {{{elevation_footnotes|}}}
| elevation_m             = {{{elevation|}}}
| population_as_of        = {{{pop_year|}}}{{#if:{{{pop2_year|}}}|、{{{pop2_year|}}}}}
| population_footnotes    = {{{pop_footnotes|}}}{{#if:{{{pop2_footnotes|}}}|<br>{{{pop2_footnotes|}}}}}{{#if:{{{density_footnotes|}}}|{{#if:{{{pop_footnotes|}}}{{{pop2_footnotes|}}}|<br>}}{{{density_footnotes|}}}}}
| population_total        = {{{pop|}}}
| population_rank         = {{#if:{{{poprank|}}}|[[澳大利亚城市人口列表|{{{poprank}}}]]}}
| population_density_km2  = {{{density|auto}}}
| population_blank1              = {{{pop2|}}}
| timezone1               = {{{timezone|}}}
| utc_offset1             = {{{utc|}}}
| timezone1_DST           = {{{timezone-dst|}}}
| utc_offset1_DST         = {{{utc-dst|}}}
| postal_code_type        = [[澳大利亞郵政編碼|郵政編碼]]
| postal_code             = {{{postcode|}}}
| blank_name_sec1         = 最近城鎮
| blank_info_sec1         = {{#ifeq:{{{type|}}}|保護|{{auto link|{{{nearest_town_or_city|}}}}} }}
| blank1_name_sec1        = 地圖
| blank1_info_sec1        = {{#if: {{{kml|}}}|
* [https://maps.google.com/maps?q=https://en.wikipedia.org/w/index.php?title=Template:Infobox_Australian_place/KML/{{#if:{{{kml_map|}}}|{{PAGENAMEE:{{{kml_map}}}}}|{{PAGENAMEE}}}}%26action%3Draw Google Maps]
* [http://www.bing.com/maps/default.aspx?mapurl=https://en.wikipedia.org/w/index.php?title=Template:Infobox_Australian_place/KML/{{#if:{{{kml_map|}}}|{{PAGENAMEE:{{{kml_map}}}}}|{{PAGENAMEE}}}}&action=raw Bing Maps]
* [https://en.wikipedia.org/w/index.php?title=Template:Infobox_Australian_place/KML/{{#if:{{{kml_map|}}}|{{PAGENAMEE:{{{kml_map}}}}}|{{PAGENAMEE}}}}&action=raw KML file]
}}
| blank2_name_sec1        = 地名集
| blank2_info_sec1        = {{{gazetted|}}}
| blank3_name_sec1        = 位置
| blank3_info_sec1        = {{#if:{{{dist1|}}}|{{#if:{{{dist2|}}}|<ul style="margin-top: 0px; margin-bottom: 0px;"><li>}}{{convert|{{{dist1|}}}|km|mi}}{{#if:{{{dir1|}}}|<br>（距{{auto link|{{{location1}}}}}{{{dir1}}}）}}{{#if:{{{dist2|}}}|<li>{{convert|{{{dist2|}}}|km|mi}}{{#if:{{{dir2|}}}|<br>（距{{auto link|{{{location2}}}}}{{{dir2}}}）}}}}{{#if:{{{dist3|}}}|<li>{{convert|{{{dist3|}}}|km|mi}}{{#if:{{{dir3|}}}|<br>（距{{auto link|{{{location3}}}}}{{{dir3}}}）}}}}{{#if:{{{dist4|}}}|<li>{{convert|{{{dist4|}}}|km|mi}}{{#if:{{{dir4|}}}|<br>（距{{auto link|{{{location4}}}}}{{{dir4}}}）}}}}{{#if:{{{dist5|}}}|<li>{{convert|{{{dist5|}}}|km|mi}}{{#if:{{{dir5|}}}|<br>（距{{auto link|{{{location5}}}}}{{{dir5}}}）}}}}{{#if:{{{dist2|}}}|</ul>}}}}
| blank4_name_sec1        = 城市
| blank4_info_sec1        = {{#if:{{{city|}}}|{{auto link|{{{city|}}}}}}}
| blank5_name_sec1        = [[教區]]
| blank5_info_sec1        = {{{parish|}}}
| blank6_name_sec1        = {{#ifeq:{{{type|}}}|cadastral|[[Hundred (county division)|Hundred]]}}
| blank6_info_sec1        = {{#ifeq:{{{type|}}}|cadastral|{{{hundred|}}} }}
| blank7_name_sec1        = {{#ifeq:{{{type|}}}|cadastral|[[Hundred (county division)|Hundred (former)]]}}
| blank7_info_sec1        = {{#ifeq:{{{type|}}}|cadastral|{{{former_hundred|}}} }}
| blank_name_sec2         = {{#ifeq:{{{type|}}}|cadastral|[[Lands administrative divisions of New South Wales|Division]]}}
| blank_info_sec2         = {{#ifeq:{{{type|}}}|cadastral|{{{division|}}} }}
| blank1_name_sec2        = [[澳大利亞州暨領地下議院選區|{{#switch:{{lc:{{{state}}}}}|act|nt|jbt= 領地|州}}選區]]
| blank1_info_sec2        = {{#if:{{{stategov|}}}|{{#if: {{{stategov2|}}}|<ul style="margin-top: 0px; margin-bottom: 0px;"><li>}} {{{stategov}}}{{#if: {{{stategov2|}}}|<li> {{{stategov2}}}}}{{#if: {{{stategov3|}}}|<li>{{{stategov3}}}}}{{#if: {{{stategov4|}}}|<li> {{{stategov4}}}}}{{#if: {{{stategov5|}}}|<li> {{{stategov5}}}}}{{#if: {{{stategov2|}}}|</ul> }}}}
| blank2_name_sec2        = [[澳大利亞聯邦下議院選舉分區|聯邦選區]]
| blank2_info_sec2        = {{#if:{{{fedgov|}}}|{{#if: {{{fedgov2|}}}|<ul style="margin-top: 0px; margin-bottom: 0px;"><li>}} {{{fedgov}}}{{#if: {{{fedgov2|}}}|<li> {{{fedgov2}}}}}{{#if: {{{fedgov3|}}}|<li> {{{fedgov3}}}}}{{#if:{{{fedgov4|}}}|<li> {{{fedgov4}}}}}{{#if: {{{fedgov2|}}}|</ul> }}}}
| blank3_name_sec2        = Visitation
| blank3_info_sec2        = {{#ifeq:{{{type|}}}|保護|{{formatnum:{{{visitation_num|}}}}}{{#if: {{{visitation_year|}}}|&nbsp;(in {{{visitation_year|}}}){{#if: {{{visitation_footnotes|}}}|{{{visitation_footnotes|}}}}}}} }}
| blank4_name_sec2        = Managing authorities
| blank4_info_sec2        = {{#ifeq:{{{type|}}}|保護|{{auto link|{{{managing_authorities|}}}}} }}
| blank5_name_sec2        =
| blank5_info_sec2        = {{#if:{{{maxtemp|}}}{{{mintemp|}}}{{{rainfall|}}}|<table cellpadding=4 cellspacing=0 style="width:100%; border: 1px #ddd solid;">
<tr class=mergedrow>
  <td style="background-color:#f0f0ff;border: 1px #FFF solid; text-align:center; width:33%;">'''平均高溫'''{{{maxtemp_footnotes|}}}</td>
  <td style="background-color:#f0f0ff;border: 1px #FFF solid; text-align:center; width:34%;">'''平均低溫'''{{{mintemp_footnotes|}}}</td>
  <td style="background-color:#f0f0ff;border: 1px #FFF solid; text-align:center; width:33%;">'''年降雨量'''{{{rainfall_footnotes|}}}</td>
</tr>
<tr style="border: 1px #FFF  solid" class=mergedrow>
  <td style="padding: 2px 0px; text-align:center; width:33%;"> {{#if: {{{maxtemp|}}}|
    {{{maxtemp}}} °C <br /><sup>{{ #expr: {{{maxtemp}}} * 1.8 + 32 round 0}} °F</sup> | ? }}</td>
  <td style="padding: 2px 0px; text-align:center; width:34%;">{{#if: {{{mintemp|}}}|
    {{{mintemp}}} °C <br /><sup>{{ #expr: {{{mintemp}}} * 1.8 + 32 round 0}} °F</sup> | ?}}</td>
  <td style="padding: 2px 0px; text-align:center; width:33%;">{{#if: {{{rainfall|}}}|
    {{formatnum:{{{rainfall}}}}} mm <br />{{ #expr: {{{rainfall}}} * 0.03937 round 1}} in | ? }}</td>
</tr></td></table> }}
| blank6_name_sec2        =
| blank6_info_sec2        = {{#if:{{{near|}}}{{{near-nw|}}}{{{near-n|}}}{{{near-ne|}}}{{{near-w|}}}{{{near-e|}}}{{{near-sw|}}}{{{near-se|}}}{{{near-s|}}}|<table cellpadding=4 cellspacing=3 style="width:100%; border: 1px #ddd solid;">
<tr class=mergedrow><td colspan=3 style="background-color:#f0f0ff;padding: 2px 0px; text-align:center;">'''{{ #switch: {{lc:{{{type|}}}}}
| cadastral = [[澳大利亞土地行政區劃|土地行政區劃]]
| lga       = [[澳大利亞地方政府|地方政府]]
| suburb    = {{{name|}}}附近的{{#if:{{{city|}}}|{{#ifexist:List of {{{city}}} suburbs| [[{{{city}}}郊區列表|郊區]] | {{ #ifexist:Category:Suburbs of {{{city}}}| [[:Category:{{{city}}}郊區]] | 郊區}}}}|郊區}}
| 附近地區}}'''</td></tr>
<tr class=mergedrow>
  <td style="text-align:center; padding: 3px 0px; width:33%;">{{{near-nw|}}}</td>
  <td style="text-align:center; padding: 3px 0px; width:34%;">{{{near-n|}}}</td>
  <td style="text-align:center; padding: 3px 0px; width:33%;">{{{near-ne|}}}</td>
</tr><tr class=mergedrow>
  <td style="text-align:center; vertical-align: middle; padding: 3px 0px; width:33%;">{{{near-w|}}}</td>
  <td style="text-align:center; vertical-align: middle; padding: 3px 0px; width:34%;">'''{{{near|{{{name}}}}}}'''</td>
  <td style="text-align:center; vertical-align: middle; padding: 3px 0px; width:33%;">{{{near-e|}}}</td>
</tr><tr class=mergedrow>
  <td style="text-align:center; padding: 3px 0px; width:33%;">{{{near-sw|}}}</td>
  <td style="text-align:center; padding: 3px 0px; width:34%;">{{{near-s|}}}</td>
  <td style="text-align:center; padding: 3px 0px; width:33%;">{{{near-se|}}}</td>
</tr></td></table> }}
| blank7_name_sec2        = 參見
| blank7_info_sec2        = {{#ifeq:{{{type|}}}|保護|{{#if:{{both|{{{iucn_category|}}}|{{{state|}}}}}|{{ #switch: {{lc:{{{state|}}} }}
  |sa       = 南澳大利亞州受保護地區
  |vic      = 維多利亞州受保護地區
  |nsw      = 新南威爾士州受保護地區
  |qld      = 昆士蘭州受保護地區
  |nt       = 北領地受保護地區
  |wa       =西澳大利亞州受保護地區
  |tas      = 塔斯瑪尼亞受保護地區
  |act      = 澳大利亞首都領地受保護地區
  }} }} }}
| website                 = {{#if:{{{url|}}}|{{#invoke:URL|url|1={{{url|}}}|2={{{name|}}}}} }}
| footnotes               = {{{footnotes|}}}
}}<!--
-->{{#if:{{{_noautocat|}}}|<!-- [[Category:Australian place articles using missing parameters|N]] -->|{{main other|{{#ifeq:{{{type|}}} | 城鎮| {{ #switch: {{lc:{{{state|}}}}}
| sa  = [[Category:南澳大利亚州城市|{{{name}}}]]
| vic = [[Category:维多利亚州城市|{{{name}}}]]
| nsw = [[Category:新南威尔士州城市|{{{name}}}]]
| qld = [[Category:昆士兰州城市|{{{name}}}]]
| nt  = [[Category:北领地城市|{{{name}}}]]
| wa  = [[Category:西澳大利亚州城市|{{{name}}}]]
| tas = [[Category:塔斯马尼亚州城市|{{{name}}}]]
}} }}{{#ifeq:{{{type|}}} | 城镇 | {{ #switch: {{{state|}}}
| sa  = [[Category:南澳大利亚州城镇|{{{name}}}]]
| vic = [[Category:维多利亚州城镇|{{{name}}}]]
| nsw = [[Category:新南威尔士州城镇|{{{name}}}]]
| qld = [[Category:昆士兰州城镇|{{{name}}}]]
| nt  = [[Category:北领地城镇|{{{name}}}]]
| wa  = [[Category:西澳大利亚州城镇|{{{name}}}]]
| act = [[Category:澳大利亚首都特区城镇|{{{name}}}]]
| tas = [[Category:塔斯马尼亚州城镇|{{{name}}}]]
  }} }}{{#ifeq:{{{type|}}} | 郊區| {{#ifexist:Category:Suburbs of {{{city}}}|[[Category:{{{city}}}郊區|{{{name}}}]]|{{ #switch: {{lc:{{{state|}}}}}
  |sa       = {{#ifexist:Category:Suburbs of {{{city}}}, South Australia|[[Category:南澳大利亞州{{{city}}}郊區|{{{name}}}]]}}
  |vic      = {{#ifexist:Category:Suburbs of {{{city}}}, Victoria|[[Category:維多利亞州{{{city}}}郊區|{{{name}}}]]}}
  |nsw      = {{#ifexist:Category:Suburbs of {{{city}}}, New South Wales|[[Category:新南威爾士州{{{city}}}郊區|{{{name}}}]]}}
  |qld      = {{#ifexist:Category:Suburbs of {{{city}}}, Queensland|[[Category:昆士蘭州{{{city}}}郊區|{{{name}}}]]}}
  |nt       = {{#ifexist:Category:Suburbs of {{{city}}}, Northern Territory|[[Category:北領地{{{city}}}郊區|{{{name}}}]]}}
  |wa       = {{#ifexist:Category:Suburbs of {{{city}}}, Western Australia|[[Category:西澳大利亞洲{{{city}}}郊區|{{{name}}}]]}}
  |tas      = {{#ifexist:Category:Suburbs of {{{city}}}, Tasmania|[[Category:塔斯瑪尼亞{{{city}}}郊區|{{{name}}}]]}}
  |act      = {{#ifexist:Category:Suburbs of {{{city}}}, ACT|[[Category:{{{city}}}郊區|{{{name}}}]]}}
  }} }} }} {{#if:{{{est|}}}|
{{#ifeq:{{{type|}}}|lga|{{#ifexist:Category:Populated places established in {{{est}}}|[[Category:Populated places established in {{{est}}} |{{{name}}}]]}}{{#ifexist:Category:Populated places established in the {{{est}}}|[[Category:Populated places established in the {{{est}}} |{{{name}}}]]}} {{#ifexist:Category:{{{est}}} establishments in Australia|[[Category:{{{est}}} establishments in Australia|{{{name}}}]]}}}}
}} }} }}<noinclude>{{Documentation}}</noinclude>