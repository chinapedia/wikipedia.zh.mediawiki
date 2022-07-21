<includeonly>{{Infobox
|bodyclass     = geography vcard
|aboveclass    = fn org
|above         = {{#if:{{{conventional_long_name|{{{Name|}}}}}}
                     | {{{conventional_long_name|{{{Name|}}}}}}{{#if:{{{native_name|{{{AltName|}}}}}}|<br /><div class="nickname" style="font-size:78%" {{#if:{{{native_name_lang|}}}|lang="{{{native_name_lang}}}"}}>{{{native_name|{{{AltName|}}}}}}</div>}}
                     | {{#if:{{{native_name|{{{AltName|}}}}}}
                           | {{{native_name|{{{AltName|}}}}}}
                           | {{PAGENAMEBASE}}
                        }}
                 }}

|subheaderstyle= background-color:#cddeff; font-weight:bold;
|subheader     = {{if empty|{{{subdivision_type|}}}|{{#if:{{{status_text|}}}|{{{status_text}}}|{{#if:{{{nation|}}}|{{#ifexist:{{{nation}}}|[[{{{nation}}}]]|{{{nation}}}}}的{{{subdivision|前行政区域}}} }} }} }}
|subheaderclass = category

|subheader2 = {{#if:{{{year_end|}}}| {{#if:{{{life_span|}}}|{{{life_span}}} |{{#ifeq:{{{year_start|}}}|{{{year_end}}}|{{{year_start}}}|{{#if:{{{year_start|}}}|{{{year_start}}}－}}{{{year_end}}}}}}} }}

| image1     = {{#invoke:InfoboxImage|InfoboxImage|image={{{image|{{{Image|}}}}}}|size={{{image size|{{{image_size|{{{imagesize|}}}}}}}}}|sizedefault=frameless|alt={{{alt|}}}|suppressplaceholder=yes}} 
|caption1       = {{{image_caption|}}}

| image2     = {{#if:{{{image_coat|}}}{{{image_symbol|}}}{{{image_flag|}}}{{{image_flag2|}}}
  |{{infobox country/imagetable
    |image1a = {{#invoke:InfoboxImage|InfoboxImage|suppressplaceholder={{main other||no}}|image={{{image_flag|}}}|sizedefault=125px|size={{{flag_width|{{{flag_size|}}}}}}|maxsize=250|border={{yesno |{{{flag_border|}}}|yes=yes|blank=yes}}|alt={{{alt_flag|{{{flag_alt|}}}}}}|title=Flag of {{{common_name|{{{name|{{{linking_name|{{PAGENAME}}}}}}}}}}}}}
    |image1b = {{#invoke:InfoboxImage|InfoboxImage|suppressplaceholder={{main other||no}}|image={{{image_flag2|}}}|sizedefault=125px|size={{{flag_width|}}}|maxsize=250|border={{yesno |{{{flag2_border|}}}|yes=yes|blank=yes}}|alt={{{alt_flag2|{{{flag_alt2|}}}}}}}}
    |caption1= {{#if:{{{flag_caption|}}}|{{{flag_caption}}}|{{#if:{{{flag|}}}|[[{{{flag}}}|{{#if:{{{flag_type|}}}|{{{flag_type}}}|Flag}}]]| {{#ifexist:Flag of {{{common_name}}}|[[Flag of {{{common_name}}}|{{#if:{{{flag_type|}}}|{{{flag_type}}}|Flag}}]]| {{#ifexist:Flag of the {{{common_name}}}|[[Flag of the {{{common_name}}}|{{#if:{{{flag_type|}}}|{{{flag_type}}}|Flag}}]] |{{#if:{{{flag_type|}}}|{{{flag_type}}}|旗帜}}}}}}}}}}
    |image2  = {{#invoke:InfoboxImage|InfoboxImage|suppressplaceholder={{main other||no}}|image={{if empty|{{{image_coat|}}}|{{{image_symbol|}}}}} |size={{{symbol_width|{{{coa_size|}}}}}}|sizedefault=85px|alt={{#if:{{{image_coat|}}}|{{{alt_coat|{{{coat_alt|}}}}}}|{{{alt_symbol|}}}}}|title={{{symbol_type|Coat of arms}}} of {{{common_name|{{{name|{{{linking_name|{{PAGENAME}}}}}}}}}}}}}
    |caption2= {{#if:{{{symbol|}}}|[[{{{symbol}}}|{{#if:{{{symbol_type|}}}|{{{symbol_type}}}|Coat of arms}}]]|{{#ifexist:Coat of arms of {{{common_name}}}|[[Coat of arms of {{{common_name}}}|{{#if:{{{symbol_type|}}}|{{{symbol_type}}}|Coat of arms}}]]|{{#ifexist:Coat of arms of the {{{common_name}}}|[[Coat of arms of the {{{common_name}}}|{{#if:{{{symbol_type|}}}|{{{symbol_type}}}|Coat of arms}}]]|{{#if:{{{symbol_type|}}}|{{{symbol_type}}}|紋章}}}}}}}}
    }} }}

| rowclass1      = mergedtoprow
| class1         = maptable
| data1          = {{#if:{{{flag_image|}}}{{{arms_image|}}}
  |<table style="text-align:center; background: none; width:100%"><tr><!--
-->{{#if:{{{flag_image|}}}|<td style="width: 130px; vertical-align: middle;">{{{flag_image|}}}</td>}}<!--
-->{{#if:{{{arms_image|}}}|<td style="width: 130px; vertical-align: middle;">{{{arms_image|}}}</td>}}<!--
--></tr><tr style="font-size: 83%;"><!--
-->{{#if:{{{flag_image|}}}|<td>{{#if:{{{flag_link|}}}|[[{{{flag_link|}}}|旗幟]]|旗幟}}</td>}}<!--
-->{{#if:{{{arms_image|}}}|<td>{{#if:{{{arms_link|}}}|[[{{{arms_link|}}}|紋章]]|紋章}}</td>}}<!--
--></tr></table>
}}

| data2        = {{#if:{{{Map|{{{image_map|}}}}}} | {{#invoke:InfoboxImage|InfoboxImage|image={{{Map|{{{image_map|}}}}}}|sizedefault=frameless}}<br>{{{map_caption|{{{image_map_caption|}}}}}} }}

| data3        = {{#if:{{{image_map2|}}} | {{#invoke:InfoboxImage|InfoboxImage|image={{{image_map2|}}}|sizedefault=frameless}}<br>{{{image_map2_caption|}}} }}

| header7      = {{#if:{{{anthem|}}}|[[颂歌|区歌]]|{{#if:{{{national_anthem|}}}|[[國歌]]}}}}
| rowclass8    = mergedrow
| data8        = {{if empty|{{{anthem|}}}|{{#ifexist:{{{national_anthem}}}|[[{{{national_anthem}}}]]|{{{national_anthem|}}}}}}}

| rowclass10   = mergedtoprow
| label10      = 首府
| data10       = {{#ifexist:{{{capital}}}|[[{{{capital}}}]]|{{{capital|}}}}}
<!--
| rowclass11   = mergedtoprow
| label11      = [[Demonym]]
| data11       = {{#ifexist:{{{demonym}}}|[[{{{demonym}}}]]|{{{demonym|}}}}}
-->
|rowclass13    = mergedtoprow  
|label13       = 面积
|data13        = {{#if: {{{AreaFirst|}}}{{{AreaSecond|}}}{{{AreaThird|}}}{{{AreaLast|}}}{{{coordinates|}}} |<!--

-->{{ Infobox | child = yes
  | labelstyle = white-space:nowrap;
  | rowclass1  = mergedrow
  | label1     = {{#if: {{{AreaFirstYear|}}} |&nbsp;•&nbsp;{{{AreaFirstYear}}} }}
  | data1      = {{#if: {{{AreaFirst|}}} |{{{AreaFirst}}} }}
  | rowclass2  = mergedrow
  | label2     = {{#if: {{{AreaSecondYear|}}} |&nbsp;•&nbsp;{{{AreaSecondYear}}} }}
  | data2      = {{#if: {{{AreaSecond|}}} |{{{AreaSecond}}} }}
  | rowclass3  = mergedrow 
  | label3     = {{#if: {{{AreaThirdYear|}}} |&nbsp;•&nbsp;{{{AreaThirdYear}}} }}
  | data3      = {{#if: {{{AreaThird|}}} |{{{AreaThird}}} }}
  | rowclass4  = mergedrow
  | label4     = {{#if: {{{AreaLastYear|}}} |&nbsp;•&nbsp;{{{AreaLastYear}}} }}
  | data4      = {{#if: {{{AreaLast|}}} |{{{AreaLast}}} }}
  | rowclass5  = mergedrow
  | label5     = {{#if: {{{coordinates|}}} |&nbsp;•&nbsp;坐标}}
  | data5      = {{#if: {{{coordinates|}}} |{{{coordinates}}} }}
}}
}}{{#if:{{{stat_area2|}}}{{{stat_area3|}}}{{{stat_area4|}}}{{{stat_area5|}}}{{{stat_area1|}}}|&nbsp;}}

|rowclass14     = mergedrow  
|label14        = {{#if: {{{area_gained1|}}}{{{area_lost1|}}} | 地区变更}}
|data14         = {{#if: {{{area_gained1|}}}{{{area_lost1|}}} |<!--

-->{{ Infobox | child = yes
  | labelstyle = font-weight:normal
  | rowclass1  = mergedrow
  | label1     = {{#if: {{{area_gained1|}}} |&nbsp;•&nbsp;{{{area_gained_year1|}}}}}
  | data1      = {{#if: {{{area_gained1|}}} |{{{area_gained1|}}} {{#if: {{{gained_from1|}}} |从{{{gained_from1|}}}}} }}
  | rowclass2  = mergedrow
  | label2     = {{#if: {{{area_lost1|}}} |&nbsp;•&nbsp;{{{area_lost_year1|}}}}}
  | data2      = {{#if: {{{area_lost1|}}} |{{{area_lost1|}}} {{#if: {{{lost_to1|}}} |至{{{lost_to1|}}}}} }}
  | rowclass3  = mergedrow
  | label3     = {{#if: {{{area_gained2|}}} |&nbsp;•&nbsp;{{{area_gained_year2|}}} }}
  | data3      = {{#if: {{{area_gained2|}}} |{{{area_gained2|}}} {{#if: {{{gained_from2|}}} |从{{{gained_from2|}}}}} }}
  | rowclass4  = mergedrow
  | label4     = {{#if: {{{area_lost2|}}} |&nbsp;•&nbsp;{{{area_lost_year2|}}} }}
  | data4      = {{#if: {{{area_lost2|}}} |{{{area_lost2|}}} {{#if: {{{lost_to2|}}} |至{{{lost_to2|}}}}} }}
  | rowclass5  = mergedrow
  | label5     = {{#if: {{{area_gained3|}}} |&nbsp;-&nbsp;{{{area_gained_year3|}}} }}
  | data5      = {{#if: {{{area_gained3|}}} |{{{area_gained3|}}} {{#if: {{{gained_from3|}}} |从{{{gained_from3|}}}}} }}
  | rowclass6  = mergedrow
  | label6     = {{#if: {{{area_lost3|}}} |&nbsp;•&nbsp;{{{area_lost_year3|}}} }}
  | data6      = {{#if: {{{area_lost3|}}} |{{{area_lost3|}}} {{#if: {{{lost_to3|}}} |至{{{lost_to3|}}}}} }}
}}
}}

| rowclass17 = {{#if:{{{stat_area2|}}}{{{stat_area3|}}}{{{stat_area4|}}}{{{stat_area5|}}}|mergedrow|mergedbottomrow}}
| label17 = <div style="text-indent:-0.9em;margin-left:1.2em;font-weight:normal;">•&nbsp;{{{stat_year1|}}}{{{ref_area1|}}}</div>
| data17 = {{#if: {{{stat_area1|}}} | {{convinfobox|{{{stat_area1|}}}|km2||sqmi}} }}

| rowclass18 = {{#if:{{{stat_area3|}}}{{{stat_area4|}}}{{{stat_area5|}}}|mergedrow|mergedbottomrow}}
| label18 = <div style="text-indent:-0.9em;margin-left:1.2em;font-weight:normal;">•&nbsp;{{{stat_year2|}}}{{{ref_area2|}}}</div>
| data18 = {{#if: {{{stat_area2|}}} | {{convinfobox|{{{stat_area2|}}}|km2||sqmi}} }}

| rowclass19 = {{#if:{{{stat_area4|}}}{{{stat_area5|}}}|mergedrow|mergedbottomrow}}
| label19 = <div style="text-indent:-0.9em;margin-left:1.2em;font-weight:normal;">•&nbsp;{{{stat_year3|}}}{{{ref_area3|}}}</div>
| data19 = {{#if: {{{stat_area3|}}} | {{convinfobox|{{{stat_area3|}}}|km2||sqmi}} }}

| rowclass20 = {{#if:{{{stat_area5|}}}|mergedrow|mergedbottomrow}}
| label20 = <div style="text-indent:-0.9em;margin-left:1.2em;font-weight:normal;">•&nbsp;{{{stat_year4|}}}{{{ref_area4|}}}</div>
| data20 = {{#if: {{{stat_area4|}}} | {{convinfobox|{{{stat_area4|}}}|km2||sqmi}} }}

| rowclass21 = mergedbottomrow
| label21 = <div style="text-indent:-0.9em;margin-left:1.2em;font-weight:normal;">•&nbsp;{{{stat_year5|}}}{{{ref_area5|}}}</div>
| data21 = {{#if: {{{stat_area5|}}} | {{convinfobox|{{{stat_area5|}}}|km2||sqmi}} }}


|rowclass25     = mergedtoprow  
|label25        = {{#if: {{{PopulationFirst|}}}{{{PopulationSecond|}}}{{{PopulationThird|}}}{{{PopulationLast|}}}{{{stat_pop1|}}}{{{stat_pop2|}}}{{{stat_pop3|}}}{{{stat_pop4|}}}{{{stat_pop5|}}} | 人口}}
|data25         = {{#if: {{{PopulationFirst|}}}{{{PopulationSecond|}}}{{{PopulationThird|}}}{{{PopulationLast|}}} |<!--

-->{{ Infobox | child = yes
  | labelstyle = font-weight:normal
  | rowclass1  = mergedrow
  | label1     = {{#if: {{{PopulationFirstYear|}}} |&nbsp;•&nbsp;{{{PopulationFirstYear}}} }}
  | data1      = {{#if: {{{PopulationFirst|}}} |{{{PopulationFirst}}} }}
  | rowclass2  = mergedrow
  | label2     = {{#if: {{{PopulationSecondYear|}}} |&nbsp;•&nbsp;{{{PopulationSecondYear}}} }}
  | data2      = {{#if: {{{PopulationSecond|}}} |{{{PopulationSecond}}} }}
  | rowclass3  = mergedrow 
  | label3     = {{#if: {{{PopulationThirdYear|}}} |&nbsp;•&nbsp;{{{PopulationThirdYear}}} }}
  | data3      = {{#if: {{{PopulationThird|}}} |{{{PopulationThird}}} }}
  | rowclass4  = mergedrow
  | label4     = {{#if: {{{PopulationLastYear|}}} |&nbsp;•&nbsp;{{{PopulationLastYear}}} }}
  | data4      = {{#if: {{{PopulationLast|}}} |{{{PopulationLast}}} }}
}}|{{#if:{{{stat_pop1|}}}{{{stat_pop2|}}}{{{stat_pop3|}}}{{{stat_pop4|}}}{{{stat_pop5|}}}|&nbsp;}}
}}

| rowclass34= mergedrow
| data34= {{#if:{{{stat_pop1|}}}{{{stat_pop2|}}}{{{stat_pop3|}}}{{{stat_pop4|}}}{{{stat_pop5|}}}|{{infobox country/multirow|{{{stat_year1|}}}{{{ref_pop1|}}} |{{{stat_pop1|}}}|{{{stat_year2|}}}{{{ref_pop2|}}} |{{{stat_pop2|}}}|{{{stat_year3|}}}{{{ref_pop3|}}} |{{{stat_pop3|}}}|{{{stat_year4|}}}{{{ref_pop4|}}} |{{{stat_pop4|}}}|{{{stat_year5|}}}{{{ref_pop5|}}} |{{{stat_pop5|}}} }} }}

|rowclass36     = mergedrow  
|label36        = {{#if: {{{DensityFirst|}}}{{{DensitySecond|}}}{{{DensityThird|}}}{{{DensityLast|}}} | 密度 }}
|data36         = {{#if: {{{DensityFirst|}}}{{{DensitySecond|}}}{{{DensityThird|}}}{{{DensityLast|}}} |<!--

-->{{ Infobox | child = yes
  | labelstyle = font-weight:normal
  | rowclass1  = mergedrow
  | label1     = {{#if: {{{DensityFirstYear|}}} |&nbsp;•&nbsp;{{{DensityFirstYear}}} }}
  | data1      = {{#if: {{{DensityFirst|}}} |{{{DensityFirst}}} }}
  | rowclass2  = mergedrow
  | label2     = {{#if: {{{DensitySecondYear|}}} |&nbsp;•&nbsp;{{{DensitySecondYear}}} }}
  | data2      = {{#if: {{{DensitySecond|}}} |{{{DensitySecond}}} }}
  | rowclass3  = mergedrow 
  | label3     = {{#if: {{{DensityThirdYear|}}} |&nbsp;•&nbsp;{{{DensityThirdYear}}} }}
  | data3      = {{#if: {{{DensityThird|}}} |{{{DensityThird}}} }}
  | rowclass4  = mergedrow
  | label4     = {{#if: {{{DensityLastYear|}}} |&nbsp;•&nbsp;{{{DensityLastYear}}} }}
  | data4      = {{#if: {{{DensityLast|}}} |{{{DensityLast}}} }}
}}
}}

|rowclass37     = mergedtoprow  
|label37        = 歷史
|data37         = <!--
  
-->{{ Infobox | child = yes
  | labelstyle = font-weight:normal
  | rowclass1  = mergedrow  
  | label1     = &nbsp;•&nbsp;前任
  | data1      = {{{preceded_by|}}}
  | rowclass2  = mergedrow  
  | label2     = &nbsp;•&nbsp;起源
  | data2      = {{{Origin|}}}
  | rowclass3  = mergedrow  
  | label3     = &nbsp;•&nbsp;創立
  | data3      = {{{Start|}}}
  | rowclass4  = mergedrow  
  | label4     = &nbsp;•&nbsp;廢除
  | data4      = {{{End|}}}
  | rowclass5  = mergedrow  
  | label5     = &nbsp;•&nbsp;繼任
  | data5      = {{{Replace|}}}
}}

|rowclass38     = mergedtoprow  
|label38        = 地位
|data38         = {{{Status|}}}

|rowclass39     = mergedrow
|label39        = {{#if: {{{CodeName|}}} |{{nowrap|{{{CodeName|}}}}} }}
|data39         = {{#if: {{{Code|}}} |{{{Code}}} }}

|rowclass40    = {{#if:{{{govern|{{{Government|}}}}}}{{{year_leader1|}}}{{{year_deputy1|}}}{{{Motto|}}}{{{motto|}}}{{{national_motto|}}} | mergedtoprow | mergedrow }} 
|label40       = {{#if:{{{govern|{{{Government|}}}}}}{{{year_leader1|}}}{{{year_deputy1|}}}{{{Motto|}}}{{{motto|}}}{{{national_motto|}}} |政府}}
|data40        = {{{govern|{{{Government|}}}}}}<!--

-->{{ Infobox | child = yes
  | labelstyle = font-weight:normal
  | rowclass1  = mergedrow
  | label1     = &nbsp;•&nbsp;类型
  | data1      = {{#ifexist:{{{government_type}}}|[[{{{government_type}}}]]|{{{government_type|}}}}}
  | rowclass2  = mergedrow
  | label2     = &nbsp;•&nbsp;[[行政中心]]
  | data2      = {{{HQ|}}}
  | rowclass3  = mergedrow
  | label3     = &nbsp;•&nbsp;[[座右銘]]
  | data3      = {{if empty|{{{motto|}}}|{{{Motto|}}}|{{{national_motto|}}}}}

  | rowclass41    = mergedrow
  | label41       = '''{{#if:{{{title_leader|}}}
    |{{#ifexist:{{{title_leader}}}|[[{{{title_leader}}}]]|{{{title_leader|}}}}}
    |{{#switch:{{{government_type}}}
      |君主制=[[{{#ifexist:{{{common_name}}}君主
                 |{{{common_name}}}君主
                 |君主
               }}}}|君主]]
      |君主立憲制|君主立宪制=[[{{#ifexist:{{{common_name}}}君主
                               |{{{common_name}}}君主
                               |君主
                              }}}}|君主]]
      |[[{{#ifexist:{{{common_name}}}总统
         |{{{common_name}}}总统
         |{{#ifexist:{{{common_name}}}總統
              |{{{common_name}}}總統
              |總統
       }}}}|總統]]
      }}
    }}'''
  | data41        = {{#if:{{{year_leader1|}}}|&nbsp;}}
  | rowclass42    = mergedrow
  | data42        = {{#if:{{{year_leader1|}}} | {{Infobox country/multirow|{{{year_leader1|}}} |{{{leader1|}}} |{{{year_leader2|}}} |{{{leader2|}}} |{{{year_leader3|}}} |{{{leader3|}}} |{{{year_leader4|}}} |{{{leader4|}}} |{{{year_leader5|}}} |{{{leader5|}}} |{{{year_leader6|}}} |{{{leader6|}}} |{{{year_leader7|}}} |{{{leader7|}}} |{{{year_leader8|}}} |{{{leader8|}}} |{{{year_leader9|}}} |{{{leader9|}}} |{{{year_leader10|}}} |{{{leader10|}}} |{{{year_leader11|}}} |{{{leader11|}}}|{{{year_leader12|}}} |{{{leader12|}}}|{{{year_leader13|}}} |{{{leader13|}}}|{{{year_leader14|}}} |{{{leader14|}}}|{{{year_leader15|}}} |{{{leader15|}}} }} }}

  | rowclass43    = mergedrow
  | label43       = '''{{#if:{{{title_deputy|}}}|{{#ifexist:{{{title_deputy}}}|[[{{{title_deputy}}}]]|{{{title_deputy}}}}}|[[{{#ifexist:{{{common_name}}}首相|{{{common_name}}}首相|{{#ifexist:Prime minister of the {{{common_name}}}|Prime minister of the {{{common_name}}}|{{#ifexist:Prime Minister of {{{common_name}}}|Prime Minister of {{{common_name}}}|{{#ifexist:Prime Minister of the {{{common_name}}}|Prime Minister of the {{{common_name}}}|Prime minister}}}}}}}}|首相]]}}'''
  | data43        = {{#if:{{{year_deputy1|}}}|&nbsp;}}
  | rowclass44    = mergedrow
  | data44        = {{#if:{{{year_deputy1|}}}|{{Infobox country/multirow|{{{year_deputy1|}}} |{{{deputy1|}}} |{{{year_deputy2|}}} |{{{deputy2|}}} |{{{year_deputy3|}}} |{{{deputy3|}}} |{{{year_deputy4|}}} |{{{deputy4|}}} |{{{year_deputy5|}}} |{{{deputy5|}}} |{{{year_deputy6|}}} |{{{deputy6|}}}|{{{year_deputy7|}}} |{{{deputy7|}}}|{{{year_deputy8|}}} |{{{deputy8|}}}|{{{year_deputy9|}}} |{{{deputy9|}}}|{{{year_deputy10|}}} |{{{deputy10|}}}|{{{year_deputy11|}}} |{{{deputy11|}}}|{{{year_deputy12|}}} |{{{deputy12|}}}|{{{year_deputy13|}}} |{{{deputy13|}}}|{{{year_deputy14|}}} |{{{deputy14|}}}|{{{year_deputy15|}}} |{{{deputy15|}}} }} }}

  | rowclass54  = mergedtoprow
  | data54      = {{#if:{{{Arms|}}} | {{{Arms}}}<br>{{{arms_caption|}}} }}
  | rowclass55  = {{#if:{{{Arms|}}} | mergedrow | mergedtoprow }}
  | data55      = {{#if:{{{Civic|}}} | {{{Civic}}}<br>{{{civic_caption|}}} }}
}}

| rowclass45    = mergedtoprow
| label45       = [[立法機關]]
| data45        = {{#if:{{{legislature|}}}|{{{legislature|}}}|{{#if:{{{house1|}}}{{{house2|}}}|&nbsp;}}}}
| rowclass46    = mergedrow
| label46       = <div style="text-indent:-0.9em;margin-left:1.2em;font-weight:normal;">•&nbsp;{{#if:{{{type_house1|}}}|{{{type_house1|}}}|上議院}}</div>
| data46        = {{{house1|}}}
| rowclass47    = mergedrow
| label47       = <div style="text-indent:-0.9em;margin-left:1.2em;font-weight:normal;">•&nbsp;{{#if:{{{type_house2|}}}|{{{type_house2|}}}|下議院}}</div>
| data47        = {{{house2|}}}

| label48       = {{nowrap|{{#if:{{{era|}}}|歷史時期|歷史}}}}
| data48        = {{#if:{{{era|}}}|{{{era}}}|{{#if:{{{date_start|}}}{{{year_start|}}}|&nbsp;}}}}
| rowclass49    = mergedrow
| data49        = {{#if:{{{date_start|}}}{{{year_start|}}}|{{Infobox country/multirow |{{{event_pre|}}} |{{{date_pre|}}}  |{{if empty|{{{event_start|}}}|{{nowrap|成立}}}} |{{{year_start|}}}{{{date_start|}}}|{{{event1|}}} |{{{date_event1|}}}  |{{{event2|}}} |{{{date_event2|}}}  |{{{event3|}}} |{{{date_event3|}}}  |{{{event4|}}} |{{{date_event4|}}}  |{{{event5|}}} |{{{date_event5|}}}  |{{{event6|}}} |{{{date_event6|}}}|{{{event7|}}} |{{{date_event7|}}}|{{{event8|}}} |{{{date_event8|}}}|{{{event9|}}} |{{{date_event9|}}}|{{{event10|}}} |{{{date_event10|}}}  |{{if empty|{{{event_end|}}}|{{nowrap|废除}}}} |{{{year_end|}}}{{{date_end|}}}|{{{event_post|}}} |{{{date_post|}}} }} }}


|rowclass51     = {{#if:{{{membership_title1|}}} | mergedtoprow |  mergedrow }}  
|label51        = {{#if:{{{membership_title1|}}} | 包含于 }}
|data51         = <!--
  
-->{{ Infobox | child = yes
  | labelstyle = font-weight:normal
  | rowclass1  = mergedrow  
  | label1     = &nbsp;•&nbsp;{{{membership_title1|}}}
  | data1      = {{{membership1|}}}
  | rowclass2  = mergedrow  
  | label2     = &nbsp;•&nbsp;{{{membership_title2|}}}
  | data2      = {{{membership2|}}}
  | rowclass3  = mergedrow  
  | label3     = &nbsp;•&nbsp;{{{membership_title3|}}}
  | data3      = {{{membership3|}}}
  | rowclass4  = mergedrow  
  | label4     = &nbsp;•&nbsp;{{{membership_title4|}}}
  | data4      = {{{membership4|}}}
  | rowclass5  = mergedrow  
  | label5     = &nbsp;•&nbsp;{{{membership_title5|}}}
  | data5      = {{{membership5|}}}
}}

| rowclass52   = mergedtoprow
| label52      = [[貨幣]]
| data52       = {{#ifexist:{{{currency|}}}|[[{{{currency}}}]]|{{{currency|}}}}}

|rowclass53     = {{#if:{{{Divisions|}}} | mergedtoprow |  mergedrow }}  
|label53        = {{#if:{{{Divisions|}}} | 分區 }}
|data53         = <!--

-->{{ Infobox | child = yes
  | labelstyle = font-weight:normal
  | rowclass1  = mergedrow
  | label1     = &nbsp;•&nbsp;類型
  | data1      = {{{Divisions|}}}
  | rowclass2  = mergedrow
  | label2     = &nbsp;•&nbsp;單元
  | data2      = {{{DivisionsNames|}}}
  | rowclass3  = mergedrow
  | data3      = {{#if:{{{DivisionsMap|}}} | {{{DivisionsMap}}}<br>{{{divisions_map_caption|}}} }}
}}

| rowclass54   = 
| label54      = 行政分區
| data54       = {{{political_subdiv|}}}

| data55 = {{#if:{{{p1|}}}{{{s1|}}}
              |{{Infobox country/formernext|flag_p1={{{flag_p1|}}}|image_p1={{{image_p1|}}}|p1={{{p1|}}}|border_p1={{{border_p1|}}}|flag_p2={{{flag_p2|}}}|image_p2={{{image_p2|}}}|p2={{{p2|}}}|border_p2={{{border_p2|}}}|flag_p3={{{flag_p3|}}}|image_p3={{{image_p3|}}}|p3={{{p3|}}}|border_p3={{{border_p3|}}}|flag_p4={{{flag_p4|}}}|image_p4={{{image_p4|}}}|p4={{{p4|}}}|border_p4={{{border_p4|}}}|flag_p5={{{flag_p5|}}}|image_p5={{{image_p5|}}}|p5={{{p5|}}}|border_p5={{{border_p5|}}}|flag_p6={{{flag_p6|}}}|image_p6={{{image_p6|}}}|p6={{{p6|}}}|border_p6={{{border_p6|}}}|flag_p7={{{flag_p7|}}}|image_p7={{{image_p7|}}}|p7={{{p7|}}}|border_p7={{{border_p7|}}}|flag_p8={{{flag_p8|}}}|image_p8={{{image_p8|}}}|p8={{{p8|}}}|border_p8={{{border_p8|}}}|flag_p9={{{flag_p9|}}}|image_p9={{{image_p9|}}}|p9={{{p9|}}}|border_p9={{{border_p9|}}}|flag_p10={{{flag_p10|}}}|image_p10={{{image_p10|}}}|p10={{{p10|}}}|border_p10={{{border_p10|}}}|flag_p11={{{flag_p11|}}}|image_p11={{{image_p11|}}}|p11={{{p11|}}}|border_p11={{{border_p11|}}}|flag_p12={{{flag_p12|}}}|image_p12={{{image_p12|}}}|p12={{{p12|}}}|border_p12={{{border_p12|}}}|flag_p13={{{flag_p13|}}}|image_p13={{{image_p13|}}}|p13={{{p13|}}}|border_p13={{{border_p13|}}}|flag_p14={{{flag_p14|}}}|image_p14={{{image_p14|}}}|p14={{{p14|}}}|border_p14={{{border_p14|}}}|flag_p15={{{flag_p15|}}}|image_p15={{{image_p15|}}}|p15={{{p15|}}}|border_p15={{{border_p15|}}}|flag_p16={{{flag_p16|}}}|image_p16={{{image_p16|}}}|p16={{{p16|}}}|border_p16={{{border_p16|}}}|flag_p17={{{flag_p17|}}}|image_p17={{{image_p17|}}}|p17={{{p17|}}}|border_p17={{{border_p17|}}}|flag_p18={{{flag_p18|}}}|image_p18={{{image_p18|}}}|p18={{{p18|}}}|border_p18={{{border_p18|}}}|flag_p19={{{flag_p19|}}}|image_p19={{{image_p19|}}}|p19={{{p19|}}}|border_p19={{{border_p19|}}}|flag_p20={{{flag_p20|}}}|image_p20={{{image_p20|}}}|p20={{{p20|}}}|border_p20={{{border_p20|}}}|flag_p21={{{flag_p21|}}}|image_p21={{{image_p21|}}}|p21={{{p21|}}}|border_p21={{{border_p21|}}}|flag_s1={{{flag_s1|}}}|image_s1={{{image_s1|}}}|s1={{{s1|}}}|border_s1={{{border_s1|}}}|flag_s2={{{flag_s2|}}}|image_s2={{{image_s2|}}}|s2={{{s2|}}}|border_s2={{{border_s2|}}}|flag_s3={{{flag_s3|}}}|image_s3={{{image_s3|}}}|s3={{{s3|}}}|border_s3={{{border_s3|}}}|flag_s4={{{flag_s4|}}}|image_s4={{{image_s4|}}}|s4={{{s4|}}}|border_s4={{{border_s4|}}}|flag_s5={{{flag_s5|}}}|image_s5={{{image_s5|}}}|s5={{{s5|}}}|border_s5={{{border_s5|}}}|flag_s6={{{flag_s6|}}}|image_s6={{{image_s6|}}}|s6={{{s6|}}}|border_s6={{{border_s6|}}}|flag_s7={{{flag_s7|}}}|image_s7={{{image_s7|}}}|s7={{{s7|}}}|border_s7={{{border_s7|}}}|flag_s8={{{flag_s8|}}}|image_s8={{{image_s8|}}}|s8={{{s8|}}}|border_s8={{{border_s8|}}}|flag_s9={{{flag_s9|}}}|image_s9={{{image_s9|}}}|s9={{{s9|}}}|border_s9={{{border_s9|}}}|flag_s10={{{flag_s10|}}}|image_s10={{{image_s10|}}}|s10={{{s10|}}}|border_s10={{{border_s10|}}}|flag_s11={{{flag_s11|}}}|image_s11={{{image_s11|}}}|s11={{{s11|}}}|border_s11={{{border_s11|}}}|flag_s12={{{flag_s12|}}}|image_s12={{{image_s12|}}}|s12={{{s12|}}}|border_s12={{{border_s12|}}}|flag_s13={{{flag_s13|}}}|image_s13={{{image_s13|}}}|s13={{{s13|}}}|border_s13={{{border_s13|}}}|flag_s14={{{flag_s14|}}}|image_s14={{{image_s14|}}}|s14={{{s14|}}}|border_s14={{{border_s14|}}}|flag_s15={{{flag_s15|}}}|image_s15={{{image_s15|}}}|s15={{{s15|}}}|border_s15={{{border_s15|}}}|flag_s16={{{flag_s16|}}}|image_s16={{{image_s16|}}}|s16={{{s16|}}}|border_s16={{{border_s16|}}}|flag_s17={{{flag_s17|}}}|image_s17={{{image_s17|}}}|s17={{{s17|}}}|border_s17={{{border_s17|}}}|flag_s18={{{flag_s18|}}}|image_s18={{{image_s18|}}}|s18={{{s18|}}}|border_s18={{{border_s18|}}}|flag_s19={{{flag_s19|}}}|image_s19={{{image_s19|}}}|s19={{{s19|}}}|border_s19={{{border_s19|}}}|flag_s20={{{flag_s20|}}}|image_s20={{{image_s20|}}}|s20={{{s20|}}}|border_s20={{{border_s20|}}}|flag_s21={{{flag_s21|}}}|image_s21={{{image_s21|}}}|s21={{{s21|}}}|border_s21={{{border_s21|}}}}}
}}

| label63  = {{nowrap|今属于}}
| data63   = {{{today|}}}

| data72 = {{{footnotes|}}}
}}</includeonly><!-- End of template
-->{{#ifeq: {{NAMESPACE}} | {{ns:0}}
| {{#if: {{{_noautocat|}}}
  |
  | <!-- Start Established Categories
-->{{#if:{{{year_start|}}}<!--
-->|{{#ifexist:Category:{{{year_start}}}建立的行政區劃<!--
    -->|[[Category:{{{year_start}}}建立的行政區劃|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
    -->|{{#ifexist:Category:{{{year_start}}}建立的行政區劃<!--
       -->|[[Category:{{{year_start}}}建立的行政區劃|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
       -->|{{#ifeq:{{Str find| {{{year_start}}} |BC}}|-1<!--
          -->|{{#ifexist:Category:States and territories established in the {{#expr: {{{year_start}}}-{{{year_start}}}mod10}}s<!--
             -->|[[Category:States and territories established in the {{#expr: {{{year_start}}}-{{{year_start}}}mod10}}s|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
             -->|{{#ifexist:Category:States and territories established in the {{Ordinal|{{#expr: ({{{year_start}}}-{{{year_start}}}mod100)/100+1}}}} century<!--
                -->|[[Category:States and territories established in the {{Ordinal| {{#expr: ({{{year_start}}}-{{{year_start}}}mod100)/100+1}}}} century|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
                -->|[[Category:需要整理的历史国家条目|Y1]]<!--
                -->}}<!--
             -->}}<!--
          -->|{{#ifexist:Category:States and territories established in the {{#expr: {{Str mid| {{{year_start}}}||{{#expr: {{Str find|{{{year_start}}} |BC}}-1}} }}-{{Str mid| {{{year_start}}}||{{#expr: {{Str find|{{{year_start}}} |BC}}-1}} }}mod10}}s BC<!--
             -->|[[Category:States and territories established in the {{#expr: {{Str mid| {{{year_start}}}||{{#expr: {{Str find|{{{year_start}}} |BC}}-1}} }}-{{Str mid| {{{year_start}}}||{{#expr: {{Str find|{{{year_start}}} |BC}}-1}} }}mod10}}s BC|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
             -->|{{#ifexist:Category:States and territories established in the {{Ordinal| {{#expr: ({{Str mid| {{{year_start}}}||{{#expr: {{Str find|{{{year_start}}} |BC}}-1}} }} - {{Str mid| {{{year_start}}}||{{#expr: {{Str find|{{{year_start}}} |BC}}-1}} }}mod100)/100+1}}}} century BC<!--
                -->|[[Category:States and territories established in the {{Ordinal|{{#expr: ({{Str mid| {{{year_start}}}||{{#expr: {{Str find|{{{year_start}}} |BC}}-1}} }} - {{Str mid| {{{year_start}}}||{{#expr: {{Str find|{{{year_start}}} |BC}}-1}} }}mod100)/100+1}}}} century BC|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
                -->|[[Category:需要整理的历史国家条目|Y1]]<!--
                -->}}<!--
             -->}}<!--
          -->}}<!--
     -->}}<!--
  -->}}<!--
-->|[[Category:需要整理的历史国家条目|D1]]<!--
-->}}<!-- End Established Categories
-->
<!-- Start Disestablished Categories
-->{{#if:{{{year_end|}}}<!--
-->|{{#ifexist:Category:{{{year_end}}}廢除的行政區劃<!--
    -->|[[Category:{{{year_end}}}廢除的行政區劃|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
    -->|{{#ifexist:Category:{{{year_end}}}廢除的行政區劃<!--
       -->|[[Category:{{{year_end}}}廢除的行政區劃|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
       -->|{{#ifeq:{{Str find| {{{year_end}}} |BC}}|-1<!--
          -->|{{#ifexist:Category:States and territories disestablished in the {{#expr: {{{year_end}}}-{{{year_end}}}mod10}}s<!--
             -->|[[Category:States and territories disestablished in the {{#expr: {{{year_end}}}-{{{year_end}}}mod10}}s|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
             -->|{{#ifexist:Category:States and territories disestablished in the {{Ordinal|{{#expr: ({{{year_end}}}-{{{year_end}}}mod100)/100+1}}}} century<!--
                -->|[[Category:States and territories disestablished in the {{Ordinal| {{#expr: ({{{year_end}}}-{{{year_end}}}mod100)/100+1}}}} century|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
                -->|[[Category:需要整理的历史国家条目|Y2]]<!--
                -->}}<!--
             -->}}<!--
          -->|{{#ifexist:Category:States and territories disestablished in the {{#expr: {{Str mid| {{{year_end}}}||{{#expr: {{Str find|{{{year_end}}} |BC}}-1}} }}-{{Str mid| {{{year_end}}}||{{#expr: {{Str find|{{{year_end}}} |BC}}-1}} }}mod10}}s BC<!--
             -->|[[Category:States and territories disestablished in the {{#expr: {{Str mid| {{{year_end}}}||{{#expr: {{Str find|{{{year_end}}} |BC}}-1}} }}-{{Str mid| {{{year_end}}}||{{#expr: {{Str find|{{{year_end}}} |BC}}-1}} }}mod10}}s BC|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
             -->|{{#ifexist:Category:States and territories disestablished in the {{Ordinal|{{#expr: ({{Str mid| {{{year_end}}}||{{#expr: {{Str find|{{{year_end}}} |BC}}-1}} }} - {{Str mid| {{{year_end}}}||{{#expr: {{Str find|{{{year_end}}} |BC}}-1}} }}mod100)/100+1}}}} century BC<!--
                -->|[[Category:States and territories disestablished in the {{Ordinal|{{#expr: ({{Str mid| {{{year_end}}}||{{#expr: {{Str find|{{{year_end}}} |BC}}-1}} }} - {{Str mid| {{{year_end}}}||{{#expr: {{Str find|{{{year_end}}} |BC}}-1}} }}mod100)/100+1}}}} century BC|{{#if:{{{common_name|}}}|{{{common_name}}}|{{PAGENAME}}}}]]<!--
                -->|[[Category:需要整理的历史国家条目|Y2]]<!--
                -->}}<!--
             -->}}<!--
          -->}}<!--
     -->}}<!--
  -->}}<!--
-->|[[Category:需要整理的历史国家条目|D2]]<!--
-->}}<!-- End Disestablished Categories
-->{{#if: {{{subdivision|}}}
    | {{#ifexist: Category:{{{nation}}}行政區劃
      | {{#switch: {{{nation|}}}
        | Poland = <!-- disabled -->
        | #default = [[Category:{{{nation}}}行政區劃]]
        }}
      }}
    }}<!--
    -->
  }}
}}<includeonly>{{#ifeq:{{{child|}}}|yes||{{Wikidata image|1={{{image_map|}}}|2={{{nocat_wdimage|}}}}}}}</includeonly>{{#invoke:Check for unknown parameters|check|unknown={{main other|[[Category:使用未知infobox former subdivision参数的页面|_VALUE_{{PAGENAME}}]]}}|preview=页面使用了[[Template:Infobox former subdivision]]不存在的参数"_VALUE_"|ignoreblank=y| _noautocat | alt | alt_coat | alt_flag | alt_flag2 | alt_symbol | AltName | anthem | area_gained_year1 | area_gained_year2 | area_gained_year3 | area_gained1 | area_gained2 | area_gained3 | area_lost_year1 | area_lost_year2 | area_lost_year3 | area_lost1 | area_lost2 | area_lost3 | AreaFirst | AreaFirstYear | AreaLast | AreaLastYear | AreaSecond | AreaSecondYear | AreaThird | AreaThirdYear | Arms | arms_caption | arms_image | arms_link | border_p1 | border_p10 | border_p11 | border_p12 | border_p13 | border_p14 | border_p15 | border_p16 | border_p17 | border_p18 | border_p19 | border_p2 | border_p20 | border_p21 | border_p3 | border_p4 | border_p5 | border_p6 | border_p7 | border_p8 | border_p9 | border_s1 | border_s10 | border_s11 | border_s12 | border_s13 | border_s14 | border_s15 | border_s16 | border_s17 | border_s18 | border_s19 | border_s2 | border_s20 | border_s21 | border_s3 | border_s4 | border_s5 | border_s6 | border_s7 | border_s8 | border_s9 | currency | capital | child | Civic | civic_caption | coa_size | coat_alt | Code | CodeName | common_name | conventional_long_name | coordinates | date_end | date_event1 | date_event10 | date_event2 | date_event3 | date_event4 | date_event5 | date_event6 | date_event7 | date_event8 | date_event9 | date_post | date_pre | date_start | demonym | DensityFirst | DensityFirstYear | DensityLast | DensityLastYear | DensitySecond | DensitySecondYear | DensityThird | DensityThirdYear | deputy1 | deputy10 | deputy11 | deputy12 | deputy13 | deputy14 | deputy15 | deputy2 | deputy3 | deputy4 | deputy5 | deputy6 | deputy7 | deputy8 | deputy9 | Divisions | divisions_map_caption | DivisionsMap | DivisionsNames | End | era | event_end | event_post | event_pre | event_start | event1 | event10 | event2 | event3 | event4 | event5 | event6 | event7 | event8 | event9 | flag | flag_alt | flag_alt2 | flag_border | flag_caption | flag_image | flag_link | flag_p1 | flag_p10 | flag_p11 | flag_p12 | flag_p13 | flag_p14 | flag_p15 | flag_p16 | flag_p17 | flag_p18 | flag_p19 | flag_p2 | flag_p20 | flag_p21 | flag_p3 | flag_p4 | flag_p5 | flag_p6 | flag_p7 | flag_p8 | flag_p9 | flag_s1 | flag_s10 | flag_s11 | flag_s12 | flag_s13 | flag_s14 | flag_s15 | flag_s16 | flag_s17 | flag_s18 | flag_s19 | flag_s2 | flag_s20 | flag_s21 | flag_s3 | flag_s4 | flag_s5 | flag_s6 | flag_s7 | flag_s8 | flag_s9 | flag_size | flag_type | flag_width | flag2_border | footnotes | gained_from1 | gained_from2 | gained_from3 | govern | Government | government_type | house1 | house2 | HQ | Image | image | image size | image_caption | image_coat | image_flag | image_flag2 | image_map | image_map_caption | image_map2 | image_map2_caption | image_p1 | image_p10 | image_p11 | image_p12 | image_p13 | image_p14 | image_p15 | image_p16 | image_p17 | image_p18 | image_p19 | image_p2 | image_p20 | image_p21 | image_p3 | image_p4 | image_p5 | image_p6 | image_p7 | image_p8 | image_p9 | image_s1 | image_s10 | image_s11 | image_s12 | image_s13 | image_s14 | image_s15 | image_s16 | image_s17 | image_s18 | image_s19 | image_s2 | image_s20 | image_s21 | image_s3 | image_s4 | image_s5 | image_s6 | image_s7 | image_s8 | image_s9 | image_size | image_symbol | imagesize | leader1 | leader10 | leader11 | leader12 | leader13 | leader14 | leader15 | leader2 | leader3 | leader4 | leader5 | leader6 | leader7 | leader8 | leader9 | legislature | life_span | linking_name | lost_to1 | lost_to2 | lost_to3 | Map | map_caption | membership_title1 | membership_title2 | membership_title3 | membership_title4 | membership_title5 | membership1 | membership2 | membership3 | membership4 | membership5 | Motto | motto | Name | name | national_motto | nation | native_name | native_name_lang | nocat_wdimage | Origin | p1 | p10 | p11 | p12 | p13 | p14 | p15 | p16 | p17 | p18 | p19 | p2 | p20 | p21 | p3 | p4 | p5 | p6 | p7 | p8 | p9 | political_subdiv | PopulationFirst | PopulationFirstYear | PopulationLast | PopulationLastYear | PopulationSecond | PopulationSecondYear | PopulationThird | PopulationThirdYear | preceded_by | ref_area1 | ref_area2 | ref_area3 | ref_area4 | ref_area5 | ref_pop1 | ref_pop2 | ref_pop3 | ref_pop4 | ref_pop5 | Replace | s1 | s10 | s11 | s12 | s13 | s14 | s15 | s16 | s17 | s18 | s19 | s2 | s20 | s21 | s3 | s4 | s5 | s6 | s7 | s8 | s9 | Start | stat_area1 | stat_area2 | stat_area3 | stat_area4 | stat_area5 | stat_pop1 | stat_pop2 | stat_pop3 | stat_pop4 | stat_pop5 | stat_year1 | stat_year2 | stat_year3 | stat_year4 | stat_year5 | Status | status_text | subdivision | subdivision_type | symbol | symbol_type | symbol_width | title_deputy | title_leader | today | type_house1 | type_house2 | year_deputy1 | year_deputy10 | year_deputy11 | year_deputy12 | year_deputy13 | year_deputy14 | year_deputy15 | year_deputy2 | year_deputy3 | year_deputy4 | year_deputy5 | year_deputy6 | year_deputy7 | year_deputy8 | year_deputy9 | year_end | year_leader1 | year_leader10 | year_leader11 | year_leader12 | year_leader13 | year_leader14 | year_leader15 | year_leader2 | year_leader3 | year_leader4 | year_leader5 | year_leader6 | year_leader7 | year_leader8 | year_leader9 | year_start }}<noinclude>
{{documentation}}</noinclude>