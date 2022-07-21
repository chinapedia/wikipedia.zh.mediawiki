{{Infobox settlement
<!-- See Template:Infobox settlement for additional fields and descriptions -->
| name                    = {{raise|0.2em|{{#if:{{both|{{{自治體名|}}}|{{{町村|}}}}}|{{{自治體名|}}}{{{町村|}}}|{{PAGENAMEBASE}}}}}}
| native_name             = {{lower|0.1em|{{nobold|{{lang|ja|{{{日文原名|{{wikidata|property|P1705}}}}}}}}}}}
| native_name_lang        = ja
| settlement_type         = [[{{#if:{{{町村|}}}|{{#ifeq:{{{町村|}}}|村|村 (日本){{!}}村|町}}|{{#ifeq:{{str rightmost|{{{自治體名}}}|1}}|村|村 (日本){{!}}村|{{str rightmost|{{{自治體名}}}|1}}}}}}]]
<!-- transliteration(s) -------->
| translit_lang1          = {{{{{|safesubst:}}}#if:{{{日文原名|}}}{{{羅馬字拼音|{{{羅馬拼音|}}}}}}{{{平假名|}}}|日文}}
| translit_lang1_type     = {{{{{|safesubst:}}}#if:{{{日文原名|}}}|[[日文]]}}
| translit_lang1_info     = {{lang|ja|{{{日文原名|{{wikidata|property|P1705}}}}}}}
| translit_lang1_type1    = {{{{{|safesubst:}}}#if:{{{平假名|}}}|[[平假名]]}}
| translit_lang1_info1    = {{lang|ja|{{{平假名|{{wikidata|property|P1814}}}}}}}
| translit_lang1_type2    = {{{{{|safesubst:}}}#if:{{{羅馬字拼音|{{{羅馬拼音|}}}}}}|[[日语罗马字|罗马字]]}}
| translit_lang1_info2    = {{{羅馬字拼音|{{{羅馬拼音|}}}}}}
<!-- images, nickname, motto -->
| image_skyline           = {{{圖像|}}}
| imagesize               = {{{圖像大小|}}}
| image_caption           = {{{圖像說明|}}}
| image_flag              = {{{町村旗|{{{旗|{{wikidata|property|raw|P41}}}}}}}}
| flag_link               = 市町村旗
| flag_type               = {{#if:{{{町村|}}}|{{{町村|}}}|{{str rightmost|{{{自治體名}}}|1}}}}旗
| image_shield            = {{{町村章|{{wikidata|property|raw|P94}}}}}
| shield_type             = {{#if:{{{圖章類型|}}}|{{{圖章類型}}}|{{#if:{{{町村|}}}|{{{町村|}}}|{{str rightmost|{{{自治體名}}}|1}}}}章}}
| shield_size             = 70px
| nickname                = 
| motto                   = 
<!-- maps and coordinates -->
| image_map               = {{{地圖|{{wikidata|property|raw|P242}}}}}
| mapsize                 = {{{地圖大小|}}}
| map_caption             = {{{{{|safesubst:}}}#if:{{both|{{{自治體名|}}}|{{{町村|}}}}}|{{{自治體名}}}{{{町村|}}}在{{{都道府縣}}}的位置}}
| image_map1              = 
| map_caption1            = 
| pushpin_map             = #Japan
| pushpin_relief          = 
| pushpin_label_position  = <!-- position of the pushpin label: left, right, top, bottom, none -->
| pushpin_map_alt         = 
| pushpin_map_caption     = {{PAGENAME}}在日本的位置
| coordinates             = {{#if:{{{座標|{{{coordinates|{{{Coordinates|{{{坐标|}}}}}}}}}}}}|{{#invoke:Coordinates|coordinsert|{{{座標|{{{coordinates|{{{Coordinates|{{{坐标|}}}}}}}}}}}}|region:JP|type:city}}}}
| coordinates_footnotes   = <!-- for references: use <ref> tags -->
<!-- location -->
| subdivision_type        = [[世界政區索引|国家]]
| subdivision_name        = {{JPN}}
| subdivision_type1       = [[日本地理分区|地方]]
| subdivision_name1       = {{地方區分{{{都道府縣}}}}}
| subdivision_type2       = [[日本行政區劃|都道府縣]]
| subdivision_name2       = {{#if:{{{都道府縣|}}}|[[{{{都道府縣}}}]]}}{{#if:{{{支廳|}}}|[[{{#if:{{{支廳連結|}}}|{{{支廳連結}}}{{!}}}}{{{支廳}}}]]}}
| subdivision_type3       = [[郡 (日本)|郡]]
| subdivision_name3       = {{#if:{{{郡|}}}|[[{{#if:{{{郡連結|}}}|{{{郡連結}}}{{!}}}}{{{郡}}}]]}}
| subdivision_type4       = {{nowrap|接鄰行政區}}
| subdivision_name4       = {{{自治體|}}}
<!-- established -->
| established_title       = 
| established_date        = 
| extinct_title           = 
| extinct_date            = 
| founder                 = 
| named_for               =
<!-- government type, leaders -->
| government_footnotes    = <!-- for references: use <ref> tags -->
| leader_party            = 
| leader_title            = {{#if:{{{町村|}}}|{{{町村|}}}|{{str rightmost|{{{自治體名}}}|1}}}}長
| leader_name             = {{{首長|}}}{{#if:{{{卸任日期|}}}|<br /><small>（現任任期至：{{{卸任日期}}}）</small>}}
| leader_title1           = 
| leader_name1            = <!-- etc., up to leader_title4 / leader_name4 -->
<!-- display settings  -->
| total_type              = <!-- to set a non-standard label for total area and population rows -->
| unit_pref               = metric_only<!-- 使单位仅显示公制 -->
<!-- area -->
| area_magnitude          = <!-- use only to set a special wikilink -->
| area_footnotes          = {{{面積註腳|}}}<!-- for references: use <ref> tags -->
| area_total_km2          = {{{面積|}}}
| area_land_km2           = 
| area_note               = {{#switch:{{{邊界未定|}}}|有=<span style="font-size:80%;">（部份邊界未確定）</span> | }}
<!-- population -->
| population_footnotes    = <!-- for references: use <ref> tags -->
| population_total        = {{{人口|}}}
| population_as_of        = {{{統計時間|}}}
| population_density_km2  = {{#if:{{{人口密度|}}}|{{{人口密度|}}}|{{#ifexpr:0={{解析數字|1={{#if:{{{人口|}}}|{{{人口}}}|{{#if:{{#property:P1082}}|{{#property:P1082}}}}}}|default=0}} or 0={{解析數字|1={{{面積}}}|default=0}}||{{Infobox 日本的市/round|{{Infobox 日本的市/round|{{#invoke:TemplateParameters|getNumberValue|1={{解析數字|1={{#if:{{{人口|}}}|{{{人口}}}|{{#if:{{#property:P1082}}|{{#property:P1082}}}}}}|default=0}}} }} }}/{{Infobox 日本的市/round|{{解析數字|1={{{面積}}}|default=0}} }} }} }} }}
| population_note         = 
<!-- time zone(s) -->
| timezone1               = [[日本標準時間]]
| utc_offset1             = +9
<!-- postal codes, area code -->
| area_code_type          = [[全國地方公共團體編號|{{#if:{{{町村|}}}|{{{町村|}}}|{{str rightmost|{{{自治體名}}}|1}}}}編號]]
| area_code               = {{{編號|}}}
<!-- Demographics -->
| demographics_type1      = {{{{{|safesubst:}}}#if:{{{樹|}}}{{{花|}}}{{{鳥|}}}{{{魚|}}}{{{歌|}}}{{{其他象徵|}}}|象徵}}
| demographics1_title1    = {{#if:{{{町村|}}}|{{{町村|}}}|{{str rightmost|{{{自治體名}}}|1}}}}樹
| demographics1_info1     = {{{樹|}}}
| demographics1_title2    = {{#if:{{{町村|}}}|{{{町村|}}}|{{str rightmost|{{{自治體名}}}|1}}}}花
| demographics1_info2     = {{{花|}}}
| demographics1_title3    = {{#if:{{{町村|}}}|{{{町村|}}}|{{str rightmost|{{{自治體名}}}|1}}}}鳥
| demographics1_info3     = {{{鳥|}}}
| demographics1_title4    = {{{其他象徵物|}}}
| demographics1_info4     = {{{其他象徵|}}}
<!-- blank fields (section 1) -->
| blank_name_sec1        = {{{{{|safesubst:}}}#if:{{{郵遞區號|}}}|[[郵遞區號|-{zh-cn:邮政编码; zh-tw:郵遞區號; zh-hk:郵區編號; zh-sg:邮递区号;}-]]}}
| blank_info_sec1         = {{color|red|〒}}{{{郵遞區號|}}}
| blank1_name_sec1        = {{#if:{{{町村|}}}|{{{町村|}}}|{{str rightmost|{{{自治體名}}}|1}}}}役場地址
| blank1_info_sec1        = {{#if:{{{所在地|}}}|{{{都道府縣}}}{{{所在地|}}}}}
| blank2_name_sec1        = 電話號碼
| blank2_info_sec1        = {{#if:{{{電話號碼|}}}|+81-{{{電話號碼|}}}}}
| blank3_name_sec1        = {{#if:{{{町村|}}}|{{{町村|}}}|{{str rightmost|{{{自治體名}}}|1}}}}議員數
| blank3_info_sec1        = {{{議員數|}}}
| blank4_name_sec1        = [[法人番號]]
| blank4_info_sec1        = {{#if:{{#property:P3225}}|[http://www.houjin-bangou.nta.go.jp/henkorireki-johoto.html?selHouzinNo={{#property:P3225}} {{#property:P3225}}]}}
<!-- website, footnotes -->
| website                 = {{{外部連結|}}}
| footnotes               = {{{註記|}}}
}}<includeonly>{{#ifeq:{{NAMESPACE}}|{{ns:0}}|{{#ifexpr:{{#if:{{{外部連結|}}}|0|1}}+{{#if:{{{都道府縣|}}}|0|1}}+{{#if:{{{面積|}}}|0|1}}+{{#if:{{{郡|}}}|0|1}}+{{#if:{{{編號|}}}|0|1}}+{{#if:{{{自治體|}}}|0|1}}+{{#if:{{{自治體名|}}}|0|1}}+{{#if:{{{町村|}}}|0|1}}+{{#if:{{{郵遞區號|}}}|0|1}}+{{#if:{{{所在地|}}}|0|1}}+{{#if:{{{日文原名|}}}|0|1}}+{{#if:{{{平假名|}}}|0|1}}>0|[[Category:缺少必要參數的日本行政區條目]]}}}}[[Category:{{PAGENAME}}{{!}} ]] [[Category:{{{都道府縣}}}的市町村|{{{羅馬字拼音}}}]]</includeonly><noinclude>{{Documentation}}</noinclude>