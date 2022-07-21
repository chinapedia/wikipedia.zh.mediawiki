<includeonly>{{Infobox
| bodyclass = ib-uk-place vcard
| templatestyles = Infobox UK place/styles.css

| aboveclass = fn org nowrap
| above = {{{official_name|{{PAGENAMEBASE}}}}}{{Unbulleted list|class=ib-uk-place-other-names
|{{#if:{{{gaelic_name|}}}  |{{lang-gd|{{{gaelic_name}}}}}}}
|{{#if:{{{scots_name|}}}   |{{lang-sco|{{{scots_name}}}}}}}
|{{#if:{{{cornish_name|}}} |{{lang-kw|{{{cornish_name}}}}}}}
|{{#if:{{{welsh_name|}}}   |{{lang-cy|{{{welsh_name}}}}}}}
|{{#if:{{{irish_name|}}}   |{{lang-ga|{{{irish_name}}}}}}}
|{{#if:{{{manx_name|}}}    |{{lang-gv|{{{manx_name}}}}}}}
|{{#if:{{{other_language_name|}}} |[[{{{other_language}}}|{{{other_language_name}}}]]}}
|{{#if:{{{local_name|}}}   |{{{local_name}}}}}
}}<!--

***** Type *****-->
| subheader ={{#if:{{{type|}}}|<span class="category">{{#switch:{{lc:{{{type|}}}}} |civil parish=Civil parish |#default={{{type|}}}}}</span>}}<!--

***** Static image/s *****-->
| rowclass1 = mergedtoprow
| data1 = {{#invoke:InfoboxImage|InfoboxImage|image={{#if:{{{static_image|}}}|{{{static_image}}}|{{{static_image_name|}}}}} |size={{{static_image_width|}}}|sizedefault=240px|alt={{{static_image_alt|}}}}}{{#if:{{{static_image|}}}{{{static_image_name|}}}|{{#if:{{{static_image_caption|}}} |<br/>{{{static_image_caption|}}} }} }}
| rowclass2 = mergedbottomrow
| data2 = {{#invoke:InfoboxImage|InfoboxImage|image={{#if:{{{static_image_2|}}}|{{{static_image_2}}}|{{{static_image_2_name|}}}}} |size={{{static_image_2_width|}}}|sizedefault=240px|alt={{{static_image_2_alt|}}}}}{{#if:{{{static_image_2|}}}{{{static_image_2_name|}}}|{{#if:{{{static_image_2_caption|}}} |<br/>{{{static_image_2_caption|}}} }} }}<!--

***** Map *****-->
| data3 = {{#switch:{{{map_type}}}
  | nomap = 
  | UK = {{Location map
                  |{{#if:{{{pushpin_map|}}}|{{{pushpin_map}}}#}}United Kingdom
                  |width=240 |float=center|marksize=6 | coordinates = {{{coordinates|}}}
                  |relief={{{map_relief|}}} |alt={{{map_alt|}}}
                  |label={{nowrap|{{PAGENAMEBASE}}}} |position={{{label_position|}}}
                  |border=infobox
                  |caption={{#if:{{{pushpin_map|}}}||{{#if:{{{coordinates|}}}|{{PAGENAME}}在{{#switch:{{{country}}}
              | England | 英格蘭 | 英格兰 = {{Infobox UK place/local  |level1=England  |level2={{{region}}}  |level3={{#if:{{{london_borough|}}}|Greater London |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_county}}} |{{#if:{{{shire_county|}}}|{{{shire_county}}} |{{#if:{{{lieutenancy_england|}}}|{{{lieutenancy_england}}} |{{{unitary_england}}} }} }} }} }}  |level4={{#if:{{{london_borough|}}}|{{{london_borough}}} |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_borough}}} |{{#if:{{{shire_county|}}}|{{{shire_district}}} |{{{unitary_england}}} }} }} }}  |retrieve=maptitle}}
              | Northern Ireland | 北愛爾蘭 | 北爱尔兰 = {{Infobox UK place/local |level1=Northern Ireland |level2={{{lieutenancy_northern_ireland}}} |retrieve=maptitle}}
              | Scotland | 蘇格蘭 | 苏格兰 = {{Infobox UK place/local  |level1=Scotland  |level2={{{unitary_scotland}}}  |level3={{#if:{{{map_type|}}}|{{{map_type|}}} |{{#if:{{{shire_district|}}}|{{{shire_district|}}} |{{{lieutenancy_scotland|}}} }} }}  |retrieve=maptitle}}
              | Wales | 威爾斯 | 威尔士 = {{Infobox UK place/local |level1=Wales |level2={{{unitary_wales}}} |retrieve=maptitle}}
              | #default = {{#ifeq:{{{crown_dependency}}}|Isle of Man |{{Infobox UK place/local|level1=Isle of Man|retrieve=maptitle}} |[[英国]]{{Infobox UK place/NoLocalMap}} }} }}的位置
}} }} }}
  | #default = {{#if:{{{coordinates|}}}
    |{{Location map
      |{{#if:{{{pushpin_map|}}}|{{{pushpin_map}}}#}}{{#switch:{{{country}}}
        | England | 英格蘭 | 英格兰 = {{Infobox UK place/local  |level1=England  |level2={{{region}}}  |level3={{#if:{{{london_borough|}}}|Greater London |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_county}}} |{{#if:{{{shire_county|}}}|{{{shire_county}}} |{{#if:{{{lieutenancy_england|}}}|{{{lieutenancy_england}}} |{{{unitary_england}}} }} }} }} }}  |level4={{#if:{{{london_borough|}}}|{{{london_borough}}} |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_borough}}} |{{#if:{{{shire_county|}}}|{{{shire_district}}} |{{{unitary_england}}} }} }} }}  |retrieve=map}}
        | Northern Ireland | 北愛爾蘭 | 北爱尔兰 = {{Infobox UK place/local |level1=Northern Ireland |level2={{{lieutenancy_northern_ireland}}} |retrieve=map}}
        | Scotland | 蘇格蘭 | 苏格兰 = {{Infobox UK place/local  |level1=Scotland  |level2={{{unitary_scotland}}}  |level3={{#if:{{{map_type|}}}|{{{map_type|}}} |{{#if:{{{shire_district|}}}|{{{shire_district|}}} |{{{lieutenancy_scotland|}}} }} }}  |retrieve=map}}
        | Wales | 威爾斯 | 威尔士 = {{Infobox UK place/local |level1=Wales |level2={{{unitary_wales}}} |retrieve=map}}
        | #default = {{#ifeq:{{{crown_dependency}}}|Isle of Man |{{Infobox UK place/local|level1=Isle of Man|retrieve=map}} |United Kingdom}}
      }}<!-- switch -->
      |width=240 |float=center|marksize=6 | coordinates = {{{coordinates|}}}
      |relief={{{map_relief|}}} |alt={{{map_alt|}}}
      |label={{nowrap|{{PAGENAMEBASE}}}} |position={{{label_position|}}}
      |border=infobox
      |caption={{#if:{{{pushpin_map|}}}|{{{pushpin_map_caption|}}}##}}{{#if:{{{coordinates|}}}|{{PAGENAME}}在{{#switch:{{{country}}}
              | England | 英格蘭 | 英格兰 = {{Infobox UK place/local  |level1=England  |level2={{{region}}}  |level3={{#if:{{{london_borough|}}}|Greater London |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_county}}} |{{#if:{{{shire_county|}}}|{{{shire_county}}} |{{#if:{{{lieutenancy_england|}}}|{{{lieutenancy_england}}} |{{{unitary_england}}} }} }} }} }}  |level4={{#if:{{{london_borough|}}}|{{{london_borough}}} |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_borough}}} |{{#if:{{{shire_county|}}}|{{{shire_district}}} |{{{unitary_england}}} }} }} }}  |retrieve=maptitle}}
              | Northern Ireland | 北愛爾蘭 | 北爱尔兰 = {{Infobox UK place/local |level1=Northern Ireland |level2={{{lieutenancy_northern_ireland}}} |retrieve=maptitle}}
              | Scotland | 蘇格蘭 | 苏格兰 = {{Infobox UK place/local  |level1=Scotland  |level2={{{unitary_scotland}}}  |level3={{#if:{{{map_type|}}}|{{{map_type|}}} |{{#if:{{{shire_district|}}}|{{{shire_district|}}} |{{{lieutenancy_scotland|}}} }} }}  |retrieve=maptitle}}
              | Wales | 威爾斯 | 威尔士 = {{Infobox UK place/local |level1=Wales |level2={{{unitary_wales}}} |retrieve=maptitle}}
              | #default = {{#ifeq:{{{crown_dependency}}}|Isle of Man |{{Infobox UK place/local|level1=Isle of Man|retrieve=maptitle}} |[[英国]]{{Infobox UK place/NoLocalMap}} }} }}的位置
}} }} }} }}
<!--

***** Area *****-->
| rowclass5 = mergedtoprow
| label5 = {{#if:{{{area_total_sq_mi|}}}{{{area_total_km2|}}}{{{area_footnotes|}}}|面積 }}
| data5 = {{#if:{{{area_total_sq_mi|}}}  |{{Infobox UK place/area|type=mile|top={{{area_total_sq_mi|}}}}}
              | {{#if:{{{area_total_km2|}}} |{{Infobox UK place/area|type=km|top={{{area_total_km2|}}}}} }}
             }}{{#if:{{{area_footnotes|}}} |&nbsp;{{{area_footnotes}}} }} <!--

***** Population/Density *****-->
| label6 = 人口
| data6 = {{#if:{{{population|}}} | {{#iferror: {{#expr:{{formatnum:{{{population}}}|R}}}}
                 | <strong class="error">表達式錯誤！“{{{population}}}”必須是數字</strong>
                 | {{formatnum: {{formatnum:{{{population}}}|R}} }}<!--([space to avoid leading-space if only population_ref supplied?])-->
             }} }}{{#if:{{{population_ref|}}} |{{{population_ref|}}} }}

| rowclass7 = mergedrow
| label7 = {{#if:{{{population|}}}
           | {{#iferror: {{#expr:{{formatnum:{{{population}}}|R}} }} |
              | {{#if:{{{area_total_sq_mi|}}}{{{area_total_km2|}}}{{{population_density|}}}|
                 •&nbsp;[[人口密度]] }}}}}}

| data7 = {{#if:{{{population|}}}
           | {{#iferror: {{#expr:{{formatnum:{{{population}}}|R}} }} |
              | {{#if:{{{area_total_sq_mi|}}}{{{area_total_km2|}}}{{{population_density|}}}|
              {{#if:{{{population_density|}}} |{{{population_density|}}}
                    | {{#if:{{{area_total_sq_mi|}}} |{{Infobox UK place/dens|type=mile|top={{{population}}}|bottom={{{area_total_sq_mi}}}}}
                       | {{Infobox UK place/dens|type=km|top={{{population}}}|bottom={{{area_total_km2}}}}}
                   }} }} }}}}}}

| rowclass8 = mergedrow
| label8 = {{{statistic_title|}}}
| data8 = {{{statistic|}}}

| rowclass9 = mergedrow
| label9 = {{{statistic_title1|}}}
| data9 = {{{statistic1|}}}

| rowclass10 = mergedrow
| label10 = {{{statistic_title2|}}}
| data10 = {{{statistic2|}}}<!--

***** Population demonym *****-->
| rowclass11 = mergedtoprow
| label11 = [[区域居民称谓词|居民称谓]]
| data11 = {{{population_demonym|}}}<!--

***** Language/s *****-->
| label12 = [[語言]]
| data12 = {{{language|}}}{{#if:{{{language1|}}}|<br/>{{{language1|}}}}}{{#if:{{{language2|}}}|<br/>{{{language2|}}}}}<!--

***** OS / Irish grid ref *****-->
| rowclass13 = mergedtoprow
| label13 = {{nowrap|[[英國國家格網參考系統|OS&nbsp;格網參考]]}}
| data13 = {{#if:{{{os_grid_reference|}}}|<span class="plainlinks nourlexpansion">{{Gbm4ibx|{{{os_grid_reference}}}}}{{{os_grid_reference_note|}}}</span>}}

| rowclass14 = mergedtoprow
| label14 = [[愛爾蘭格網參考系統|愛爾蘭格網參考]]
| data14 = {{#if:{{{irish_grid_reference|}}}|<span class="plainlinks nourlexpansion">{{iem4ibx|{{{irish_grid_reference}}}}}{{{irish_grid_reference_note|}}}</span>}}<!--

***** City distances *****-->
| rowclass15 = mergedrow
| label15 = {{#if:{{{belfast_distance|}}}{{{belfast_distance_mi|}}}{{{belfast_distance_km|}}}|•&nbsp;[[贝尔法斯特]]}}
| data15 ={{#if:{{{belfast_distance_mi|}}}|{{Infobox UK place/dist|type=mile|distance={{{belfast_distance_mi}}}}}
             | {{#if:{{{belfast_distance_km|}}} |{{Infobox UK place/dist|type=km|distance={{{belfast_distance_km}}}}} }}
            }}{{{belfast_distance|}}}{{#if:{{{belfast_direction|}}}|&nbsp;[[罗盘方位{{!}}{{{belfast_direction}}}]]}}

| rowclass16 = mergedrow
| label16 ={{#if:{{{cardiff_distance|}}}{{{cardiff_distance_mi|}}}{{{cardiff_distance_km|}}}|•&nbsp;[[加的夫|-{zh-hans:加的夫; zh-hk:卡迪夫; zh-mo:加地夫; zh-tw:卡地夫;}-]]}}
| data16 ={{#if:{{{cardiff_distance_mi|}}}|{{Infobox UK place/dist|type=mile|distance={{{cardiff_distance_mi}}}}}
             | {{#if:{{{cardiff_distance_km|}}} |{{Infobox UK place/dist|type=km|distance={{{cardiff_distance_km}}}}} }}
            }}{{{cardiff_distance|}}}{{#if:{{{cardiff_direction|}}}|&nbsp;[[罗盘方位{{!}}{{{cardiff_direction}}}]]}}

| rowclass17 = mergedrow
| label17 ={{#if:{{{douglas_distance|}}}{{{douglas_distance_mi|}}}{{{douglas_distance_km|}}}|•&nbsp;[[道格拉斯 (马恩岛)|道格拉斯 (马恩岛)]]}}
| data17 ={{#if:{{{douglas_distance_mi|}}}|{{Infobox UK place/dist|type=mile|distance={{{douglas_distance_mi}}}}}
             | {{#if:{{{douglas_distance_km|}}} |{{Infobox UK place/dist|type=km|distance={{{douglas_distance_km}}}}} }}
            }}{{{douglas_distance|}}}{{#if:{{{douglas_direction|}}}|&nbsp;[[罗盘方位{{!}}{{{douglas_direction}}}]]}}

| rowclass18 = mergedrow
| label18 = {{#if:{{{dublin_distance|}}}{{{dublin_distance_mi|}}}{{{dublin_distance_km|}}}|•&nbsp;[[都柏林]]}}
| data18 ={{#if:{{{dublin_distance_mi|}}}|{{Infobox UK place/dist|type=mile|distance={{{dublin_distance_mi}}}}}
             | {{#if:{{{dublin_distance_km|}}} |{{Infobox UK place/dist|type=km|distance={{{dublin_distance_km}}}}} }}
            }}{{{dublin_distance|}}}{{#if:{{{dublin_direction|}}}|&nbsp;[[罗盘方位{{!}}{{{dublin_direction}}}]]}}

| rowclass19 = mergedrow
| label19 ={{#if:{{{edinburgh_distance|}}}{{{edinburgh_distance_mi|}}}{{{edinburgh_distance_km|}}}| •&nbsp;[[愛丁堡]] }}
| data19 ={{#if:{{{edinburgh_distance_mi|}}}|{{Infobox UK place/dist|type=mile|distance={{{edinburgh_distance_mi}}}}}
             | {{#if:{{{edinburgh_distance_km|}}} |{{Infobox UK place/dist|type=km|distance={{{edinburgh_distance_km}}}}} }}
            }}{{{edinburgh_distance|}}}{{#if:{{{edinburgh_direction|}}}|&nbsp;[[罗盘方位{{!}}{{{edinburgh_direction}}}]]}}

| rowclass20 = mergedbottomrow
| label20 = {{#if:{{{london_distance|}}}{{{london_distance_mi|}}}{{{london_distance_km|}}}|•&nbsp;[[伦敦]]}}
| data20 ={{#if:{{{london_distance_mi|}}}|{{Infobox UK place/dist|type=mile|distance={{{london_distance_mi}}}}}
             | {{#if:{{{london_distance_km|}}} |{{Infobox UK place/dist|type=km|distance={{{london_distance_km}}}}} }}
            }}{{{london_distance|}}}{{#if:{{{london_direction|}}}|&nbsp;[[罗盘方位{{!}}{{{london_direction}}}]]}}

| rowclass21 = mergedbottomrow
| label21 = {{#if:{{{charingX_distance|}}}{{{charingX_distance_mi|}}}{{{charingX_distance_km|}}}|•&nbsp;[[查令十字]]}}
| data21 ={{#if:{{{charingX_distance_mi|}}}|{{Infobox UK place/dist|type=mile|distance={{{charingX_distance_mi}}}}}
             | {{#if:{{{charingX_distance_km|}}} |{{Infobox UK place/dist|type=km|distance={{{charingX_distance_km}}}}} }}
            }}{{{charingX_distance|}}}{{#if:{{{charingX_direction|}}}|&nbsp;[[罗盘方位{{!}}{{{charingX_direction}}}]]}}<!--

***** Administrative divisions (except constituencies) *****
    ***** Parish (level 5) *****-->
| label22 = [[民政教區]]
| data22 ={{Unbulleted list|{{{civil_parish|}}}|{{{civil_parish1|}}}|{{{civil_parish2|}}}}}

| rowclass23 = mergedtoprow
| label23 = [[威尔士行政区划#社區|社區]]
| data23 = {{Unbulleted list|{{{community_wales|}}}|{{{community_wales1|}}}|{{{community_wales2|}}}|{{{community_wales3|}}}}}

| rowclass24 = mergedtoprow
| label24 = [[社區議會]]
| data24 = {{Unbulleted list|{{{community_scotland|}}}|{{{community_scotland1|}}}|{{{community_scotland2|}}}|{{{community_scotland3|}}}}}<!--


    ***** District (level 4) *****-->
| rowclass25 = mergedrow
| label25 = [[威尔士行政区划|主要地區]]
| data25 = {{Unbulleted list|{{{unitary_wales|}}}|{{{unitary_wales1|}}}|{{{unitary_wales2|}}}|{{{unitary_wales3|}}}}}

| rowclass26 = mergedrow
| label26 ={{#if:{{{london_borough|}}}|{{Infobox UK place/local |level1=England |level2={{{region}}} |level3={{{london_borough}}} |level4={{{london_borough}}} |retrieve=boroughhead}} }}
| data26 ={{Unbulleted list| {{#if:{{{london_borough|}}}|{{Infobox UK place/local |level1=England |level2={{{region}}} |level3={{{london_borough}}} |level4={{{london_borough}}} |retrieve=borough}}}}|{{#if:{{{london_borough1|}}}|{{Infobox UK place/local |level1=England |level2={{{region}}} |level3={{{london_borough}}} |level4={{{london_borough1}}} |retrieve=borough}}}}|{{#if:{{{london_borough2|}}}|{{Infobox UK place/local |level1=England |level2={{{region}}} |level3={{{london_borough}}} |level4={{{london_borough2}}} |retrieve=borough}}}}|{{#if:{{{london_borough3|}}}|{{Infobox UK place/local |level1=England |level2={{{region}}} |level3={{{london_borough}}} |level4={{{london_borough3}}} |retrieve=borough}}}}|{{#if:{{{london_borough4|}}}|{{Infobox UK place/local |level1=England |level2={{{region}}} |level3={{{london_borough}}} |level4={{{london_borough4}}} |retrieve=borough}}}}}}

| rowclass27 = mergedrow
| label27 = [[區 (英格蘭)|都會自治市]]
| data27 = {{Unbulleted list|{{{metropolitan_borough|}}}|{{{metropolitan_borough1|}}}|{{{metropolitan_borough2|}}}|{{{metropolitan_borough3|}}}}}

| rowclass28 = mergedrow
| label28 = [[區 (英格蘭)|區]]
| data28 = {{Unbulleted list|{{{shire_district|}}}|{{{shire_district1|}}}|{{{shire_district2|}}}|{{{shire_district3|}}}}}

| rowclass29 = mergedrow
| label29 = [[區 (英格蘭)|單一管理區]]
| data29 = {{Unbulleted list|{{{unitary_england|}}}|{{{unitary_england1|}}}|{{{unitary_england2|}}}|{{{unitary_england3|}}}}}

| rowclass30 = mergedrow
| label30 = [[苏格兰行政区划|議會區]]
| data30 = {{Unbulleted list|{{{unitary_scotland|}}}|{{{unitary_scotland1|}}}|{{{unitary_scotland2|}}}|{{{unitary_scotland3|}}}}}

| rowclass31 = mergedrow
| label31 = [[北爱尔兰行政区划|區]]
| data31 = {{Unbulleted list|{{{unitary_northern_ireland|}}}|{{{unitary_northern_ireland1|}}}|{{{unitary_northern_ireland2|}}}|{{{unitary_northern_ireland3|}}}}}

| rowclass32 = mergedrow
| label32 = [[堂區長|堂區]]
| data32 = {{{manx_parish|}}}<!--

    ***** County (level 3) *****-->
| rowclass33 = mergedrow
| label33 = [[威尔士的保留郡|名譽郡]]
| data33 = {{Unbulleted list|{{{lieutenancy_wales|}}}|{{{lieutenancy_wales1|}}}|{{{lieutenancy_wales2|}}}|{{{lieutenancy_wales3|}}}}}

| rowclass34 = mergedrow
| label34 = {{Infobox UK place/local |level1=England |level2={{{region}}} |level3={{{london_borough}}} |level4={{{london_borough1}}} |retrieve=countyhead}} 
| data34 = {{#if:{{{london_borough|}}}| [[大倫敦]] }}

| rowclass35 = mergedrow
| label35 = [[英格蘭的都會郡和非都會郡|郡份]]
| data35 = {{Unbulleted list|{{{shire_county|}}}|{{{shire_county1|}}}|{{{shire_county2|}}}|{{{shire_county3|}}}}}

| rowclass36 = mergedrow
| label36 = [[英格蘭的都會郡和非都會郡|-{zh-cn:都市郡; zh-hk:都市郡; zh-tw:都會郡;}-]]
| data36 = {{Unbulleted list|{{{metropolitan_county|}}}|{{{metropolitan_county1|}}}|{{{metropolitan_county2|}}}|{{{metropolitan_county3|}}}}}

| rowclass37 = mergedrow
| label37 = [[英格蘭的名譽郡|名譽郡]]
| data37 = {{Unbulleted list|{{{lieutenancy_england|}}}|{{{lieutenancy_england1|}}}|{{{lieutenancy_england2|}}}|{{{lieutenancy_england3|}}}}}

| rowclass38 = mergedrow
| label38 =[[蘇格蘭的郡尉轄區|郡尉轄區]]
| data38 = {{Unbulleted list|{{{lieutenancy_scotland|}}}|{{{lieutenancy_scotland1|}}}|{{{lieutenancy_scotland2|}}}|{{{lieutenancy_scotland3|}}}}}

| rowclass39 = mergedrow
| label39 = [[郡 (北愛爾蘭)|郡]]
| data39 = {{Unbulleted list|{{{lieutenancy_northern_ireland|}}}|{{{lieutenancy_northern_ireland1|}}}|{{{lieutenancy_northern_ireland2|}}}}}

| rowclass40 = mergedrow
| label40 = [[曼島的地方政府|行政區]]
| data40 = {{{manx_sheading|{{{manx_shedding|}}}}}}<!--

   ***** Regional (level 2) *****-->
| rowclass41 = mergedrow
| label41 = [[區域 (英格蘭)|-{zh-hant:區域; zh-cn:大区; zh-sg:区域;}-]]
| data41 = {{Unbulleted list|{{Infobox UK place/local |level1=England |level2={{{region}}} |retrieve=region}}|{{Infobox UK place/local |level1=England |level2={{{region1}}} |retrieve=region}}}}<!--

   ***** Country (level 1) *****-->
| rowclass42 = mergedrow adr
| label42 = [[英國的構成國|國家]]
| data42 = {{#if:{{{country|}}}|<span class="country-name">{{Auto link|{{{country}}}}}</span>}}{{#if:{{{country1|}}}|<br/>{{Auto link|{{{country1|}}}}}}}

| rowclass43 = mergedrow adr
| label43 = [[英國皇家屬地|皇家屬地]]
| data43 = {{Auto link|{{{crown_dependency|}}}}}

| rowclass44 = mergedrow
| label44 = [[主权国家列表|主權國家]]
| data44 = {{#if:{{{country|}}}|[[英国]]}}<!--

***** Historic county *****
| rowclass45 = mergedtoprow
| label45 = {{#switch:{{{country}}}
        | England = [[英格蘭歷史上的郡|歷史上的郡]]
        | Northern Ireland = [[郡 (北愛爾蘭)|歷史上的郡]]
        | Scotland = [[郡 (蘇格蘭)|歷史上的郡]]
        | Wales = [[威尔士历史上的郡|歷史上的郡]]
        | #default = [[英國歷史上的郡|歷史上的郡]]
  }}
| data45 = {{#if:{{{historic_county|}}}|{{Unbulleted list|{{{historic_county|}}}|{{{historic_county1|}}}}}}}<!--

***** Post town/s *****-->
| rowclass46 = mergedtoprow
| label46 = [[郵鎮]]
| data46 = {{#if:{{{post_town|}}}|{{#switch:{{{post_town}}}|London|倫敦|伦敦|[[London postal district|London]]|[[London postal district|倫敦]]|[[倫敦郵區|倫敦]]|LONDON=[[倫敦郵區|倫敦]] |{{{post_town}}}={{{post_town}}}}}|{{Infobox UK place/NoPostCode}}}}

| rowclass47 = mergedrow
| label47 = [[英國郵區編號|郵區]]
| data47 = {{#if:{{{postcode_area|}}}|[[{{{postcode_area}}} 郵區|{{#if:{{{postcode_district|}}}|{{{postcode_district}}}|{{{postcode_area}}}}}]]|{{Infobox UK place/NoPostCode}}}}<!--

    ***** Post town 1 ***** -->
| rowclass48 = mergedrow
| label48 = 郵鎮
| data48 = {{#if:{{{post_town1|}}}|{{#switch:{{{post_town1}}}|London|倫敦|伦敦|[[London postal district|London]]|[[London postal district|倫敦]]|[[倫敦郵區|倫敦]]|LONDON=[[倫敦郵區|倫敦]]|{{{post_town1}}}={{{post_town1}}}}}}}

| rowclass49 = mergedrow
| label49 = 郵區
| data49 = {{#if:{{{postcode_area1|}}}|[[{{{postcode_area1}}} 郵區|{{{postcode_district1}}}]]}}<!--

    ***** Post town 2 ***** -->
| rowclass50 = mergedrow
| label50 = Post&nbsp;town
| data50 = {{#if:{{{post_town2|}}}|{{#switch:{{{post_town2}}}|London|倫敦|伦敦|[[London postal district|London]]|[[London postal district|倫敦]]|[[倫敦郵區|倫敦]]|LONDON=[[倫敦郵區|倫敦]]|{{{post_town2}}}={{{post_town2}}}}}}}

| rowclass51 = mergedrow
| label51 = Postcode&nbsp;district
| data51 = {{#if:{{{postcode_area2|}}}|[[{{{postcode_area2}}} 郵區|{{{postcode_district2}}}]]}}<!--

***** Dialling code/s ***** -->

| rowclass52 = mergedrow
| label52 = [[英國電話號碼|電話區號]]
| data52 = {{#if:{{{dial_code|}}}|{{#switch:{{{dial_code}}}|0203|0207|0208|020 3|020 7|020 8|020=[[020]]  |02380|02392|023 80|023 92|023=023  |02476|024 76=024  |{{{dial_code}}}={{{dial_code}}}}} | {{Infobox UK place/NoDialCode}}}}{{#if:{{{dial_code1|}}}|<br/>{{{dial_code1}}}}}{{#if:{{{dial_code2|}}}|<br/>{{{dial_code2}}}}}<!--

***** ISO code *****-->

| rowclass53 = mergedrow
| label53 = {{nowrap|[[ISO 3166|ISO&nbsp;3166]]代碼}}
| data53 = {{#if:{{{iso_code|}}}|{{{iso_code}}}|<!--{{Infobox UK place/NoISOCode}}-->}}<!--

***** Emergency services ***** -->
| rowclass54 = mergedtoprow
| data54 = {{#if:{{{hide_services|}}}|<!--(then omit the following)
  -->|{{Infobox| child=yes | <!--

          ***** Police *****-->
      | rowclass1 = mergedrow
      | label1 = [[英国执法机构列表|警察]]
      | data1 = {{#switch:{{{country}}}
            | England | 英格蘭 | 英格兰 = {{Infobox UK place/local  |level1=England  |level2={{{region}}}  |level3={{#if:{{{london_borough|}}}|{{{london_borough}}} |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_county}}} |{{#if:{{{shire_county|}}}|{{{shire_county}}} |{{#if:{{{lieutenancy_england|}}}|{{{lieutenancy_england}}} |{{{unitary_england}}} }} }} }} }}  |level4={{#if:{{{london_borough|}}}|{{{london_borough}}} |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_borough}}} |{{#if:{{{shire_county|}}}|{{{shire_district}}} |{{{unitary_england}}} }} }} }}  |retrieve=police}}
            | Northern Ireland | 北愛爾蘭 | 北爱尔兰 = {{Infobox UK place/local |level1=Northern Ireland |retrieve=police}}
            | Scotland | 蘇格蘭 | 苏格兰 = {{Infobox UK place/local |level1=Scotland |level2={{{unitary_scotland}}} |retrieve=police}}
            | Wales | 威爾斯 | 威尔士 = {{Infobox UK place/local |level1=Wales |level2={{{unitary_wales}}} |retrieve=police}}
            | #default = {{#ifeq:{{{crown_dependency}}}|Isle of Man |{{Infobox UK place/local|level1=Isle of Man|retrieve=police}} |&nbsp;}}
           }} 
      | rowclass2 = mergedrow
      | label2 = &nbsp;
      | data2 = {{Unbulleted list|{{#if:{{{shire_county3|}}}|{{Infobox UK place/local |level1=England |level2={{{region1}}} |level3={{{shire_county3}}} |retrieve=police}}}}|{{#if:{{{metropolitan_county3|}}}|{{Infobox UK place/local |level1=England |level2={{{region1}}} |level3={{{metropolitan_county3}}} |retrieve=police}}}}|{{#if:{{{unitary_england3|}}}|{{Infobox UK place/local |level1=England |level2={{{region1}}} |level3={{{unitary_england3}}} |retrieve=police}}}}|{{#if:{{{unitary_scotland3|}}}|{{Infobox UK place/local |level1=Scotland |level2={{{unitary_scotland3}}} |retrieve=police}}}}|{{#if:{{{unitary_wales3|}}}|{{Infobox UK place/local |level1=Wales |level2={{{unitary_wales3}}} |retrieve=police}}}}}} <!--

          ***** Fire *****-->
      | rowclass3 = mergedrow
      | label3 = [[英国消防机构|消防]]
      | data3 = {{#switch:{{{country}}}
                | England | 英格蘭 | 英格兰 = {{Infobox UK place/local  |level1=England  |level2={{{region}}}  |level3={{#if:{{{london_borough|}}}|{{{london_borough}}} |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_county}}} |{{#if:{{{shire_county|}}}|{{{shire_county}}} |{{#if:{{{lieutenancy_england|}}}|{{{lieutenancy_england}}} |{{{unitary_england}}} }} }} }} }}  |level4={{#if:{{{london_borough|}}}|{{{london_borough}}} |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_borough}}} |{{#if:{{{shire_county|}}}|{{{shire_district}}} |{{{unitary_england}}} }} }} }}  |retrieve=fire}}
                | Northern Ireland | 北愛爾蘭 | 北爱尔兰 = {{Infobox UK place/local |level1=Northern Ireland |retrieve=fire}}
                | Scotland | 蘇格蘭 | 苏格兰 = {{Infobox UK place/local |level1=Scotland |level2={{{unitary_scotland}}} |retrieve=fire}}
                | Wales | 威爾斯 | 威尔士 = {{Infobox UK place/local |level1=Wales |level2={{{unitary_wales}}} |retrieve=fire}}
                | #default = {{#ifeq:{{{crown_dependency}}}|Isle of Man |{{Infobox UK place/local|level1=Isle of Man|retrieve=fire}} |&nbsp;}}
               }}
      | rowclass4 = mergedrow
      | label4 = &nbsp;
      | data4 = {{Unbulleted list|{{#if:{{{shire_county3|}}}|{{Infobox UK place/local |level1=England |level2={{{region1}}} |level3={{{shire_county3}}} |retrieve=fire}}}}|{{#if:{{{metropolitan_county3|}}}|{{Infobox UK place/local |level1=England |level2={{{region1}}} |level3={{{metropolitan_county3}}} |retrieve=fire}}}}|{{#if:{{{unitary_england3|}}}|{{Infobox UK place/local |level1=England |level2={{{region1}}} |level3={{{unitary_england3}}} |retrieve=fire}}}}|{{#if:{{{unitary_scotland3|}}}|{{Infobox UK place/local |level1=Scotland |level2={{{unitary_scotland3}}} |retrieve=fire}}}}|{{#if:{{{unitary_wales3|}}}|{{Infobox UK place/local |level1=Wales |level2={{{unitary_wales3}}} |retrieve=fire}}}}}}
      | rowclass5 = mergedrow
      | label5 = {{#if:{{{country|}}} |[[英國緊急醫療機構|救護]] |Ambulance}} 
      | data5 = {{#switch:{{{country}}}
                    | England | 英格蘭 | 英格兰 = {{Infobox UK place/local  |level1=England  |level2={{{region}}}  |level3={{#if:{{{london_borough|}}}|{{{london_borough}}} |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_county}}} |{{#if:{{{shire_county|}}}|{{{shire_county}}} |{{#if:{{{lieutenancy_england|}}}|{{{lieutenancy_england}}} |{{{unitary_england}}} }} }} }} }}  |level4={{#if:{{{london_borough|}}}|{{{london_borough}}} |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_borough}}} |{{#if:{{{shire_county|}}}|{{{shire_district}}} |{{{unitary_england}}} }} }} }}  |ambulance={{{ambulance_service}}}  |official_name={{#if:{{{official_name|}}}|{{{official_name}}}|{{PAGENAMEBASE}}}}  |postcode={{{postcode_district}}}  |retrieve=ambulance}}
                    | Northern Ireland | 北愛爾蘭 | 北爱尔兰 = {{Infobox UK place/local |level1=Northern Ireland |retrieve=ambulance}}
                    | Scotland | 蘇格蘭 | 苏格兰 = {{Infobox UK place/local |level1=Scotland |level2={{{unitary_scotland}}} |retrieve=ambulance}}
                    | Wales | 威爾斯 | 威尔士 = {{Infobox UK place/local |level1=Wales |level2={{{unitary_wales}}} |retrieve=ambulance}}
                    | #default = {{#ifeq:{{{crown_dependency}}}|Isle of Man |{{Infobox UK place/local|level1=Isle of Man|retrieve=ambulance}} |&nbsp;}}
                   }} 

      | rowclass6 = mergedrow
      | label6 = &nbsp;
      | data6 = {{#if:{{{region1|}}}|{{Infobox UK place/local  |level1=England  |level2={{{region1}}}  |level3={{#if:{{{london_borough3|}}}|Greater London |{{#if:{{{metropolitan_county3|}}}|{{{metropolitan_county3}}} |{{#if:{{{shire_county3|}}}|{{{shire_county3}}} |{{#if:{{{lieutenancy_england3|}}}|{{{lieutenancy_england3}}} |{{{unitary_england3}}} }} }} }} }}  |level4={{#if:{{{london_borough3|}}}|{{{london_borough3}}} |{{#if:{{{metropolitan_county3|}}}|{{{metropolitan_borough3}}} |{{#if:{{{shire_county3|}}}|{{{shire_district3}}} |{{{unitary_england3}}} }} }} }}  |ambulance={{{ambulance_service1}}}  |postcode={{{postcode_district}}}  |retrieve=ambulance}}}}
    }}
  }}<!--
***** Constituencies *****

   ***** UK Parliament *****-->
| rowclass55 = mergedtoprow
| label55 = [[英國國會選區]]
| data55 = {{Unbulleted list|{{{constituency_westminster|}}}|{{{constituency_westminster1|}}}|{{{constituency_westminster2|}}}|{{{constituency_westminster3|}}}|{{{constituency_westminster4|}}}|{{{constituency_westminster5|}}}|{{{constituency_westminster6|}}}|{{{constituency_westminster7|}}}|{{{constituency_westminster8|}}}}}<!--

   ***** Scottish Parliament *****-->
| rowclass56 = mergedrow
| label56 = [[蘇格蘭議會選區]]
| data56 =   {{Unbulleted list|{{{constituency_scottish_parliament|}}}|{{{constituency_scottish_parliament1|}}}|{{{constituency_scottish_parliament2|}}}|{{{constituency_scottish_parliament3|}}}|{{{constituency_scottish_parliament4|}}}|{{{constituency_scottish_parliament5|}}}|{{{constituency_scottish_parliament6|}}}|{{{constituency_scottish_parliament7|}}}|{{{constituency_scottish_parliament8|}}}|{{{constituency_scottish_parliament9|}}}|{{{constituency_scottish_parliament10|}}}}}<!--

    ***** London Assembly ***** -->
| rowclass57 = mergedrow
| label57 = [[倫敦議會選區列表|倫敦議會選區]]
| data57 = {{Unbulleted list|{{#if:{{{london_borough|}}}|{{Infobox UK place/local |level1=England |level2={{{region}}} |level3={{{london_borough}}} |level4={{{london_borough}}} |retrieve=assembly}}}}|{{#if:{{{london_borough1|}}}|{{Infobox UK place/local |level1=England |level2={{{region}}} |level3={{{london_borough1}}} |level4={{{london_borough1}}} |retrieve=assembly}}}}|{{#if:{{{london_borough2|}}}|{{Infobox UK place/local |level1=England |level2={{{region}}} |level3={{{london_borough2}}} |level4={{{london_borough2}}} |retrieve=assembly}}}}}}<!--

    ***** Welsh Assembly *****-->
| rowclass58 = mergedrow
| label58 = [[威尔士议会选区]]
| data58 = {{Unbulleted list|{{{constituency_welsh_assembly|}}}|{{{constituency_welsh_assembly1|}}}|{{{constituency_welsh_assembly2|}}}}}<!--

    ***** Isle of Man (House of Keys) *****-->
| rowclass59 = mergedrow
| label59 = [[曼島下議院選區]]
| data59 = {{{constituency_manx_parliament|}}}<!--

    ***** Northern Ireland Assembly ***** -->
| rowclass60 = mergedrow
| label60 = [[北愛爾蘭議會選區列表|北愛爾蘭議會選區]]
| data60 = {{Unbulleted list|{{{constituency_ni_assembly|}}}|{{{constituency_ni_assembly1|}}}|{{{constituency_ni_assembly2|}}}|{{{constituency_ni_assembly3|}}}}}<!--

    ******Councillors (merged from {{infobox UK ward}}****** -->

| rowclass61 = mergedrow
| label61 = 議員
| data61 = {{{councillors|}}}

| rowclass62 = mergedrow
| label62 = 議員
| data62 = {{Unbulleted list|{{{councillor1|}}}{{#if:{{{party1|}}}|&#x20;({{{party1|}}})}}|{{{councillor2|}}}{{#if:{{{party2|}}}|&#x20;({{{party2|}}})}}|{{{councillor3|}}}{{#if:{{{party3|}}}|&#x20;({{{party3|}}})}}|{{{councillor4|}}}{{#if:{{{party4|}}}|&#x20;({{{party4|}}})}}|{{{councillor5|}}}{{#if:{{{party5|}}}|&#x20;({{{party5|}}})}}}}<!--

***** Website *****-->
| rowclass63 = mergedtoprow
| label63 = 網站
| data63 = {{{website|}}}

| data70 = {{{embedded|}}}<!--

***** Footer *****-->
| belowclass = hlist noprint nowrap
| below =; {{nobold|地區列表}} {{#switch:{{{country}}}
| England | 英格蘭 | 英格兰 =
: [[英國地區列表|英國]]
: [[英格蘭地區列表|英格蘭]]
: {{Infobox UK place/local  |level1=England  |level2={{{region}}}  |level3={{#if:{{{london_borough|}}}|Greater London |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_county}}} |{{#if:{{{shire_county|}}}|{{{shire_county}}} |{{#if:{{{lieutenancy_england|}}}|{{{lieutenancy_england}}} |{{{unitary_england}}} }} }} }} }}  |level4={{#if:{{{london_borough|}}}|{{{london_borough}}} |{{#if:{{{metropolitan_county|}}}|{{{metropolitan_borough}}} |{{#if:{{{shire_county|}}}|{{{shire_district}}} |{{{unitary_england}}} }} }} }}  |retrieve=footer}}
| Scotland | 蘇格蘭 | 苏格兰 =
: [[英國地區列表|英國]]
: [[蘇格蘭地區列表|蘇格蘭]]
: {{Infobox UK place/local |level1=Scotland |level2={{{unitary_scotland}}} |retrieve=footer}}
| Wales | 威爾斯 | 威尔士 =
: [[英國地區列表|英國]]
: [[威尔士地区列表|威尔士]]
: {{Infobox UK place/local |level1=Wales |level2={{{unitary_wales}}} |retrieve=footer}}
| Northern Ireland | 北愛爾蘭 | 北爱尔兰 =
: [[英國地區列表|英國]]
: [[北愛爾蘭]]
: {{Infobox UK place/local |level1=Northern Ireland |level2={{{lieutenancy_northern_ireland}}} |retrieve=footer}}
| #default =
: {{#ifeq:{{{crown_dependency}}}|Isle of Man |{{Infobox UK place/local|level1=Isle of Man|retrieve=footer}} |[[英國地區列表|英國]]}}
}}<!--

***** Co-ordinates for top of page ***** -->
{{#if:{{{coordinates|}}}|{{#invoke:Coordinates|coordinsert|{{{coordinates}}}|region:{{#ifeq:{{{crown_dependency|}}}|Isle of Man|IM|GB}}|type:city{{#iferror:{{#expr:{{formatnum:{{{population}}}|R}}*1}}||({{formatnum:{{{population}}}|R}})}}}} 
|}}
}}</includeonly>{{#invoke:Check for unknown parameters|check|unknown={{main other|[[Category:含有未知参数的英国地区信息框|_VALUE_{{PAGENAME}}]]}}|preview=[[Template:Infobox UK place]] 含有未知参数“_VALUE_”|ignoreblank=y| ambulance_service | ambulance_service1 | area_footnotes | area_total_km2 | area_total_sq_mi | belfast_direction | belfast_distance | belfast_distance_km | belfast_distance_mi | cardiff_direction | cardiff_distance | cardiff_distance_km | cardiff_distance_mi | charingX_direction | charingX_distance | charingX_distance_km | charingX_distance_mi | civil_parish | civil_parish1 | civil_parish2 | community_scotland | community_scotland1 | community_scotland2 | community_scotland3 | community_wales | community_wales1 | community_wales2 | community_wales3 | constituency_manx_parliament | constituency_ni_assembly | constituency_ni_assembly1 | constituency_ni_assembly2 | constituency_ni_assembly3 | constituency_scottish_parliament | constituency_scottish_parliament1 | constituency_scottish_parliament10 | constituency_scottish_parliament2 | constituency_scottish_parliament3 | constituency_scottish_parliament4 | constituency_scottish_parliament5 | constituency_scottish_parliament6 | constituency_scottish_parliament7 | constituency_scottish_parliament8 | constituency_scottish_parliament9 | constituency_welsh_assembly | constituency_welsh_assembly1 | constituency_welsh_assembly2 | constituency_westminster | constituency_westminster1 | constituency_westminster2 | constituency_westminster3 | constituency_westminster4 | constituency_westminster5 | constituency_westminster6 | constituency_westminster7 | constituency_westminster8 | coordinates | cornish_name | councillor1 | councillor2 | councillor3 | councillor4 | councillor5 | councillors | country | country1 | crown_dependency | dial_code | dial_code1 | dial_code2 | douglas_direction | douglas_distance | douglas_distance_km | douglas_distance_mi | dublin_direction | dublin_distance | dublin_distance_km | dublin_distance_mi | edinburgh_direction | edinburgh_distance | edinburgh_distance_km | edinburgh_distance_mi | embedded | gaelic_name | hide_services | irish_grid_reference | irish_grid_reference_note | irish_name | iso_code | label_position | language | language1 | language2 | lieutenancy_england | lieutenancy_england1 | lieutenancy_england2 | lieutenancy_england3 | lieutenancy_northern_ireland | lieutenancy_northern_ireland1 | lieutenancy_northern_ireland2 | lieutenancy_scotland | lieutenancy_scotland1 | lieutenancy_scotland2 | lieutenancy_scotland3 | lieutenancy_wales | lieutenancy_wales1 | lieutenancy_wales2 | lieutenancy_wales3 | local_name | london_borough | london_borough1 | london_borough2 | london_borough3 | london_borough4 | london_direction | london_distance | london_distance_km | london_distance_mi | manx_name | manx_parish | manx_sheading | manx_shedding | map_alt | map_relief | map_type | metropolitan_borough | metropolitan_borough1 | metropolitan_borough2 | metropolitan_borough3 | metropolitan_county | metropolitan_county1 | metropolitan_county2 | metropolitan_county3 | official_name | os_grid_reference | os_grid_reference_note | other_language | other_language_name | party1 | party2 | party3 | party4 | party5 | population | population_demonym | population_density | population_ref | post_town | post_town1 | post_town2 | postcode_area | postcode_area1 | postcode_area2 | postcode_district | postcode_district1 | postcode_district2 | pushpin_map | region | region1 | scale | scots_name | shire_county | shire_county1 | shire_county2 | shire_county3 | shire_district | shire_district1 | shire_district2 | shire_district3 | static_image | static_image_2 | static_image_2_alt | static_image_2_caption | static_image_2_name | static_image_2_width | static_image_alt | static_image_caption | static_image_name | static_image_width | statistic | statistic_title | statistic_title1 | statistic_title2 | statistic1 | statistic2 | type | unitary_england | unitary_england1 | unitary_england2 | unitary_england3 | unitary_northern_ireland | unitary_northern_ireland1 | unitary_northern_ireland2 | unitary_northern_ireland3 | unitary_scotland | unitary_scotland1 | unitary_scotland2 | unitary_scotland3 | unitary_wales | unitary_wales1 | unitary_wales2 | unitary_wales3 | website | welsh_name |pushpin_map_caption }}<noinclude>
{{Documentation}}
</noinclude>