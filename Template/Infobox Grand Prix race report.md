{{infobox3cols
| bodyclass = vevent
| bodystyle = width: 27em; line-height: 1.5em;
| titlestyle = font-size: 125%;
| title = <includeonly>{{flagicon|{{{country|{{{Country|none}}}}}}|{{{flag_suffix|{{{Flag_suffix|}}}}}}}}&nbsp;<span class="summary">{{{Year|{{{year}}}}}}年{{{grand prix|{{{Grand Prix}}}大獎賽}}}</span></includeonly>
| abovestyle = font-size:100%; background-color:#efefef;
| above = <includeonly>賽事細節{{{details ref|{{{Details ref|}}}}}}</includeonly>
| subheader = <!--
 -->{{#switch:{{{type|{{{Type}}}}}}
 |F1 = {{#if:{{{race_no|{{{Race_No|}}}}}}|<small class="description">{{#ifexpr:{{{Year|{{{year}}}}}}>1980|[[{{{Year|{{{year}}}}}}年世界一級方程式錦標賽]]|[[{{{Year|{{{year}}}}}}年世界一級方程式錦標賽]]}}共{{{season_no|{{{Season_No}}}}}}站中的第{{{race_no|{{{Race_No}}}}}}站</small>|}}
 |GP = {{#if:{{{race_no|{{{Race_No|}}}}}}|<small class="description">{{#if:{{{description|{{{Description|}}}}}}|{{{description|{{{Description}}}}}}|[[{{{Season|{{{Year|{{{year}}}}}}}}}年大獎賽賽季]]}}</small>|}}
 |EC = {{#if:{{{race_no|{{{Race_No|}}}}}}|<small class="description">[[{{{Year|{{{year}}}}}}年大獎賽賽季|{{{Year|{{{year}}}}}}年歐洲錦標賽]]共{{{season_no|{{{Season_No}}}}}}站中的第{{{race_no|{{{Race_No}}}}}}站</small>|}}
 |WMC = {{#if:{{{race_no|{{{Race_No|}}}}}}|<small class="description">[[{{{Year|{{{year}}}}}}年大獎賽賽季|{{{Year|{{{year}}}}}}年世界製造商錦標賽]]共{{{season_no|{{{Season_No}}}}}}站中的第{{{race_no|{{{Race_No}}}}}}</small>|}}
 |NC = <small class="description">[[{{{Year|{{{year}}}}}}年世界一级方程式锦标赛]]非錦標賽賽事</small>
 |CUST = <small class="description">{{{description|{{{Description}}}}}}</small>
 |#default = 
 }}{{#if:{{{Next_round|}}}{{{Previous_round|}}}<!--
-->|<table style="width: 100%; background: transparent;"><tr><!--
   -->{{#if:{{{Previous_round|}}}<!--
   -->|<td style="text-align:left;">'''←&nbsp;'''[[{{{Previous_round}}}|上一場]]</td><!--
   -->}}{{#if:{{{Next_round|}}}<!--
   -->|<td style="text-align: right;">[[{{{Next_round}}}{{!}}下一場]]'''&nbsp;→'''</td><!--
   -->}}<!--
--></tr></table>}}
| image = {{#invoke:InfoboxImage|InfoboxImage|image={{{Image|{{{image|}}}}}}|size={{{image-size|{{{image_size|}}}}}}|{{#if:{{{Image_Link|{{{image_link|}}}}}}|link|μ1}}=File:{{{Image_Link|{{{image_link|}}}}}}|title={{{caption|{{{Caption|}}}}}}|alt={{{image_alt|{{{image-alt|}}}}}}}}
| caption = {{{caption|{{{Caption|}}}}}}

| labelstyle = width:20%;
| headerstyle = background-color:#efefef;

| label1 = 日期
| data1 = {{#if:{{{Date|{{{date|}}}}}}
 | {{#formatdate:{{{Year|{{{year}}}}}}年{{{Date|{{{date|}}}}}}}}
 | {{{fulldate|{{{Fulldate|}}}}}}
 }}

| label3 = 官方名稱
| data3 = {{{official name|{{{Official name|}}}}}}

| label4 = 舉辦地點
| class4 = location
| data4 = {{{Location|{{{location|}}}}}}

| label5 = 賽道類型
| data5  = {{#if:{{{course_km|{{{Course_km|}}}}}}{{{course_length|{{{Course_length|}}}}}}| {{{course|{{{Course|永久性賽道}}}}}} }}

| label6 = 賽道長度
| data6 = {{#if:{{{course_km|{{{Course_km|}}}}}}
  |{{{course_km|{{{Course_km}}}}}}公里（{{{course_mi|{{{Course_mi}}}}}}英里）
  |{{{course_length|{{{Course_length|}}}}}}
  }}

| label7 = 比賽距離
| data7 = {{#if:{{{distance_km|{{{Distance_km|}}}}}}
          | {{#if:{{{distance_laps|{{{Distance_laps|}}}}}}|{{{distance_laps|{{{Distance_laps}}}}}}圈，}}{{{distance_km|{{{Distance_km}}}}}}公里（{{{distance_mi|{{{Distance_mi}}}}}}英里）
          | {{#if:{{{distance_length|{{{Distance_length|}}}}}}|{{#if:{{{distance_laps|{{{Distance_laps|}}}}}}|{{{distance_laps|{{{Distance_laps}}}}}}圈，}}{{{distance_length|{{{Distance_length}}}}}}}}
          }}

| label8 = 原定賽程
| data8 = {{#if: {{{scheduled_km|{{{Scheduled_km|}}}}}} 
          |{{#if:{{{scheduled_laps|{{{Scheduled_laps|}}}}}}|{{{scheduled_laps|{{{Scheduled_laps}}}}}}圈，}}{{{scheduled_km|{{{Scheduled_km}}}}}}公里（{{{scheduled_mi|{{{Scheduled_mi}}}}}}英里）
          |{{#if: {{{scheduled_length|{{{Scheduled_length|}}}}}} | {{#if:{{{scheduled_laps|{{{Scheduled_laps|}}}}}}|{{{scheduled_laps|{{{Scheduled_laps}}}}}}圈，}}{{{scheduled_length|{{{Scheduled_length}}}}}}}}
          }}

| label9 = 天氣
| data9 = {{{weather|{{{Weather|}}}}}}

| label10 = 觀眾數
| data10 = {{{attendance|{{{Attendance|}}}}}}

| header11 = {{#if: {{{pole_driver|{{{Pole_Driver|}}}}}}| [[桿位]]}}
| label12 = {{#if: {{{pole_driver2|{{{Pole_Driver2|}}}}}}|車手|車手}}
| data12a = {{#if: {{{pole_driver|{{{Pole_Driver|}}}}}}| {{unbulleted list
 | 1 = {{flagicon|{{{pole_country|{{{Pole_Country|none}}}}}}|{{{pole_flag_suffix|{{{Pole_flag_suffix|}}}}}}}} {{{pole_driver|{{{Pole_Driver}}}}}}
 | 2 = {{#if: {{{pole_driver2|{{{Pole_Driver2|}}}}}}|{{flagicon|{{{pole_country2|{{{Pole_Country2|none}}}}}}|{{{pole_flag_suffix2|{{{Pole_flag_suffix2|}}}}}}}} {{{pole_driver2|{{{Pole_Driver2}}}}}} }}
 }} }}
| data12b = {{#if: {{{pole_driver|{{{Pole_Driver|}}}}}}|{{#if: {{{pole_team|{{{Pole_Team|}}}}}}|<small>{{{pole_team|{{{Pole_Team}}}}}}</small>}}}}

| label13 = 時間
| data13 = {{#if: {{{pole_driver|{{{Pole_Driver|}}}}}}| {{{pole_time|{{{Pole_Time|}}}}}} }}
| data14 = {{#if: {{{pole_driver|{{{Pole_Driver|}}}}}}| {{br separated entries
 | 1 = {{#if: {{{grid_from_heats|{{{Grid_from_heats|}}}}}}|'''排位依最佳成績排序'''}}
 | 2 = {{#if: {{{grid_from_ballot|{{{Grid_from_ballot|}}}}}}|'''排位依票數排序'''}}
 | 3 = {{#if: {{{grid_from_number|{{{Grid_from_number|}}}}}}|'''排位依車號排序'''}}
 | 4 = {{#if: {{{grid_from_sprint|{{{Grid_from_sprint|}}}}}}|'''排位依衝刺賽結果排序'''}}
 }} }}

| header15 = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|[[最快圈速|最快單圈]]}}
| label16 = {{#if: {{{fast_driver2|{{{Fast_Driver2|}}}}}}{{{fast_driver3|{{{Fast_Driver3|}}}}}}{{{fast_driver4|{{{Fast_Driver4|}}}}}}{{{fast_driver5|{{{Fast_Driver5|}}}}}}{{{fast_driver6|{{{Fast_Driver6|}}}}}}{{{fast_driver7|{{{Fast_Driver7|}}}}}}|車手|車手}}
| data16a = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver|{{{Fast_Driver|}}}}}} | {{flagicon|{{{fast_country|{{{Fast_Country|none}}}}}}|{{{fast_flag_suffix|{{{Fast_flag_suffix|}}}}}}}} {{{fast_driver|{{{Fast_Driver}}}}}} {{#if: {{{fast_lap|{{{Fast_Lap|}}}}}}| {{#if: {{{fast_driver2|{{{Fast_Driver2|}}}}}}{{{fast_driver3|{{{Fast_Driver3|}}}}}}{{{fast_driver4|{{{Fast_Driver4|}}}}}}{{{fast_driver5|{{{Fast_Driver5|}}}}}}{{{fast_driver6|{{{Fast_Driver6|}}}}}}{{{fast_driver7|{{{Fast_Driver7|}}}}}}|<small>（第{{{fast_lap|{{{Fast_Lap}}}}}}圈）</small>}} }} }} }}
| data16b = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver|{{{Fast_Driver|}}}}}} | <small>{{{fast_team|{{{Fast_Team}}}}}}</small> }} }}
| label17 = <span style="display:none">Fastest lap</span>
| data17a = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver2|{{{Fast_Driver2|}}}}}}| {{flagicon|{{{fast_country2|{{{Fast_Country2|none}}}}}}|{{{fast_flag_suffix2|{{{Fast_flag_suffix2|}}}}}}}} {{{fast_driver2|{{{Fast_Driver2}}}}}} {{#if: {{{fast_lap2|{{{Fast_Lap2|}}}}}}| <small>（第{{{fast_lap2|{{{Fast_Lap2}}}}}}圈）</small>}} }} }}
| data17b = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver2|{{{Fast_Driver2|}}}}}} | <small>{{{fast_team2|{{{Fast_Team2}}}}}}</small> }} }}
| label18 = <span style="display:none">Fastest lap</span>
| data18a = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver3|{{{Fast_Driver3|}}}}}}| {{flagicon|{{{fast_country3|{{{Fast_Country3|none}}}}}}|{{{fast_flag_suffix3|{{{Fast_flag_suffix3|}}}}}}}} {{{fast_driver3|{{{Fast_Driver3}}}}}} {{#if: {{{fast_lap3|{{{Fast_Lap3|}}}}}}| <small>（第{{{fast_lap3|{{{Fast_Lap3}}}}}}圈）</small>}} }} }}
| data18b = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver3|{{{Fast_Driver3|}}}}}} | <small>{{{fast_team3|{{{Fast_Team3}}}}}}</small> }} }}
| label19 = <span style="display:none">Fastest lap</span>
| data19a = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver4|{{{Fast_Driver4|}}}}}}| {{flagicon|{{{fast_country4|{{{Fast_Country4|none}}}}}}|{{{fast_flag_suffix4|{{{Fast_flag_suffix4|}}}}}}}} {{{fast_driver4|{{{Fast_Driver4}}}}}} {{#if: {{{fast_lap4|{{{Fast_Lap4|}}}}}}| <small>（第{{{fast_lap4|{{{Fast_Lap4}}}}}}圈）</small>}} }} }}
| data19b = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver4|{{{Fast_Driver4|}}}}}} | <small>{{{fast_team4|{{{Fast_Team4}}}}}}</small> }} }}
| label20 = <span style="display:none">Fastest lap</span>
| data20a = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver5|{{{Fast_Driver5|}}}}}}| {{flagicon|{{{fast_country5|{{{Fast_Country5|none}}}}}}|{{{fast_flag_suffix5|{{{Fast_flag_suffix5|}}}}}}}} {{{fast_driver5|{{{Fast_Driver5}}}}}} {{#if: {{{fast_lap5|{{{Fast_Lap5|}}}}}}| <small>（第{{{fast_lap5|{{{Fast_Lap5}}}}}}圈）</small>}} }} }}
| data20b = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver5|{{{Fast_Driver5|}}}}}} | <small>{{{fast_team5|{{{Fast_Team5}}}}}}</small> }} }}
| label21 = <span style="display:none">Fastest lap</span>
| data21a = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver6|{{{Fast_Driver6|}}}}}}| {{flagicon|{{{fast_country6|{{{Fast_Country6|none}}}}}}|{{{fast_flag_suffix6|{{{Fast_flag_suffix6|}}}}}}}} {{{fast_driver6|{{{Fast_Driver6}}}}}} {{#if: {{{fast_lap6|{{{Fast_Lap6|}}}}}}| <small>（第{{{fast_lap6|{{{Fast_Lap6}}}}}}圈）</small>}} }} }}
| data21b = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver6|{{{Fast_Driver6|}}}}}} | <small>{{{fast_team6|{{{Fast_Team6}}}}}}</small> }} }}
| label22 = <span style="display:none">Fastest lap</span>
| data22a = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver7|{{{Fast_Driver7|}}}}}}| {{flagicon|{{{fast_country7|{{{Fast_Country7|none}}}}}}|{{{fast_flag_suffix7|{{{Fast_flag_suffix7|}}}}}}}} {{{fast_driver7|{{{Fast_Driver7}}}}}} {{#if: {{{fast_lap7|{{{Fast_Lap7|}}}}}}| <small>（第{{{fast_lap7|{{{Fast_Lap7}}}}}}圈）</small>}} }} }}
| data22b = {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{#if: {{{fast_driver7|{{{Fast_Driver7|}}}}}} | <small>{{{fast_team7|{{{Fast_Team7}}}}}}</small> }} }}

| label23 = 時間
| data23 =  {{#if: {{{fast_time|{{{Fast_Time|}}}}}}|{{{fast_time|{{{Fast_Time}}}}}} {{#if: {{{fast_driver2|{{{Fast_Driver2|}}}}}}{{{fast_driver3|{{{Fast_Driver3|}}}}}}{{{fast_driver4|{{{Fast_Driver4|}}}}}}{{{fast_driver5|{{{Fast_Driver5|}}}}}}{{{fast_driver6|{{{Fast_Driver6|}}}}}}{{{fast_driver7|{{{Fast_Driver7|}}}}}}| |{{#if: {{{fast_lap|{{{Fast_Lap|}}}}}}| 在第{{{fast_lap|{{{Fast_Lap}}}}}}圈 }} }} }}

| header24 = {{#if: {{{first_driver|{{{First_Driver|}}}}}}{{{second_driver|{{{Second_Driver|}}}}}}{{{third_driver|{{{Third_Driver|}}}}}}| [[頒獎台]] }}

| label25 = 第一名
| data25a = {{#if: {{{first_driver|{{{First_Driver|}}}}}}| {{unbulleted list
 |1={{flagicon|{{{first_country|{{{First_Country|none}}}}}}|{{{first_flag_suffix|{{{First_flag_suffix|}}}}}}}} {{{first_driver|{{{First_Driver}}}}}}
 |2={{#if: {{{first_driver2|{{{First_Driver2|}}}}}}| {{flagicon|{{{first_country2|{{{First_Country2|none}}}}}}|{{{first_flag_suffix2|{{{First_flag_suffix2|}}}}}}}} {{{first_driver2|{{{First_Driver2}}}}}} }}
 |3={{#if: {{{first_driver3|{{{First_Driver3|}}}}}}| {{flagicon|{{{first_country3|{{{First_Country3|none}}}}}}|{{{first_flag_suffix3|{{{First_flag_suffix3|}}}}}}}} {{{first_driver3|{{{First_Driver3}}}}}} }}
 }} }}
| data25b = {{#if: {{{first_driver|{{{First_Driver|}}}}}}| <small>{{{first_team|{{{First_Team}}}}}}</small> }}

| label26 = 第二名
| data26a = {{#if: {{{second_driver|{{{Second_Driver|}}}}}}| {{unbulleted list
 |1={{flagicon|{{{second_country|{{{Second_Country|none}}}}}}|{{{second_flag_suffix|{{{Second_flag_suffix|}}}}}}}} {{{second_driver|{{{Second_Driver}}}}}}
 |2={{#if: {{{second_driver2|{{{Second_Driver2|}}}}}}| {{flagicon|{{{second_country2|{{{Second_Country2|none}}}}}}|{{{second_flag_suffix2|{{{Second_flag_suffix2|}}}}}}}} {{{second_driver2|{{{Second_Driver2}}}}}} }}
 |3={{#if: {{{second_driver3|{{{Second_Driver3|}}}}}}| {{flagicon|{{{second_country3|{{{Second_Country3|none}}}}}}|{{{second_flag_suffix3|{{{Second_flag_suffix3|}}}}}}}} {{{second_driver3|{{{Second_Driver3}}}}}} }}
 }} }}
| data26b = {{#if: {{{second_driver|{{{Second_Driver|}}}}}}|<small>{{{second_team|{{{Second_Team}}}}}}</small> }}

| label27 = 第三名
| data27a = {{#if: {{{third_driver|{{{Third_Driver|}}}}}}| {{unbulleted list
 |1= {{flagicon|{{{third_country|{{{Third_Country|none}}}}}}|{{{third_flag_suffix|{{{Third_flag_suffix|}}}}}}}} {{{third_driver|{{{Third_Driver}}}}}}
 |2={{#if: {{{third_driver2|{{{Third_Driver2|}}}}}}| {{flagicon|{{{third_country2|{{{Third_Country2|none}}}}}}|{{{third_flag_suffix2|{{{Third_flag_suffix2|}}}}}}}} {{{third_driver2|{{{Third_Driver2}}}}}} }}
 |3={{#if: {{{third_driver3|{{{Third_Driver3|}}}}}}| {{flagicon|{{{third_country3|{{{Third_Country3|none}}}}}}|{{{third_flag_suffix3|{{{Third_flag_suffix3|}}}}}}}} {{{third_driver3|{{{Third_Driver3}}}}}} }}
 }} }}
| data27b = {{#if: {{{third_driver|{{{Third_Driver|}}}}}}|<small>{{{third_team|{{{Third_Team}}}}}}</small>}}

| belowstyle = background-color:#efefef
| below = {{#if: {{{lapchart|{{{Lapchart|}}}}}}| {{List collapsed|title=<center>領跑者</center>|<center>{{{lapchart|{{{Lapchart}}}}}}</center>}} }}
}}{{#if:<!--
-->{{#ifeq:{{{image_alt|{{{image-alt|}}}}}}|{{{image_alt|}}}{{{image-alt|}}}||1}}{{#if:{{both|{{{image_alt|}}}|{{{image-alt|}}}}}|1}}{{#ifeq:{{{Date|{{{date|}}}}}}|{{{date|{{{Date|}}}}}}{{{date|}}}||1}}{{#if:{{both|{{{date|{{{Date|}}}}}}|{{{date|}}}}}|1}}{{#ifeq:{{{Year|{{{year|}}}}}}|{{{year|{{{Year|}}}}}}{{{year|}}}||1}}{{#if:{{both|{{{year|{{{Year|}}}}}}|{{{year|}}}}}|1}}{{#ifeq:{{{Location|{{{location|}}}}}}|{{{location|{{{Location|}}}}}}{{{location|}}}||1}}{{#if:{{both|{{{location|{{{Location|}}}}}}|{{{location|}}}}}|1}}{{#if:{{both|{{{date|{{{Date|}}}}}}{{{date|}}}|{{{fulldate|{{{Fulldate|}}}}}}}}|1}}{{#if:{{both|{{{course_km|{{{Course_km|}}}}}}|{{{course_length|{{{Course_length|}}}}}}}}|1}}{{#if:{{both|{{{distance_km|{{{Distance_km|}}}}}}|{{{distance_length|{{{Distance_length|}}}}}}}}|1}}<!--
-->|[[Category:使用Infobox Grand Prix race report歧義參數的頁面]]
}}{{#switch:{{{type|{{{Type|}}}}}}|F1|GP|EC|WMC|NC|CUST=|=|#default=[[Category:使用Infobox Grand Prix race report未知比賽類型的頁面]]
}}<!--
-->{{#invoke:Check for unknown parameters|check|unknown={{main other|[[Category:使用Infobox Grand Prix race report未知參數的頁面|_VALUE_{{PAGENAME}}]]}}|preview=本頁面使用[[Template:Infobox Grand Prix race report]]未知參數"_VALUE_"|ignoreblank=y
| Attendance | attendance | Caption | caption | Country | country | Course | course | Course_km | course_km | Course_length | course_length | Course_mi | course_mi | date | Date | Description | description | Details ref | details ref | Distance_km | distance_km | Distance_laps | distance_laps | Distance_length | distance_length | Distance_mi | distance_mi | Fast_Country | fast_country | Fast_Country2 | fast_country2 | Fast_Country3 | fast_country3 | Fast_Country4 | fast_country4 | Fast_Country5 | fast_country5 | Fast_Country6 | fast_country6 | Fast_Country7 | fast_country7 | Fast_Driver | fast_driver | Fast_Driver2 | fast_driver2 | Fast_Driver3 | fast_driver3 | Fast_Driver4 | fast_driver4 | Fast_Driver5 | fast_driver5 | Fast_Driver6 | fast_driver6 | Fast_Driver7 | fast_driver7 | Fast_flag_suffix | fast_flag_suffix | Fast_flag_suffix2 | fast_flag_suffix2 | Fast_flag_suffix3 | fast_flag_suffix3 | Fast_flag_suffix4 | fast_flag_suffix4 | Fast_flag_suffix5 | fast_flag_suffix5 | Fast_flag_suffix6 | fast_flag_suffix6 | Fast_flag_suffix7 | fast_flag_suffix7 | Fast_Lap | fast_lap | Fast_Lap2 | fast_lap2 | Fast_Lap3 | fast_lap3 | Fast_Lap4 | fast_lap4 | Fast_Lap5 | fast_lap5 | Fast_Lap6 | fast_lap6 | Fast_Lap7 | fast_lap7 | Fast_Team | fast_team | Fast_Team2 | fast_team2 | Fast_Team3 | fast_team3 | Fast_Team4 | fast_team4 | Fast_Team5 | fast_team5 | Fast_Team6 | fast_team6 | Fast_Team7 | fast_team7 | Fast_Time | fast_time | First_Country | first_country | First_Country2 | first_country2 | First_Country3 | first_country3 | First_Driver | first_driver | First_Driver2 | first_driver2 | First_Driver3 | first_driver3 | First_flag_suffix | first_flag_suffix | First_flag_suffix2 | first_flag_suffix2 | First_flag_suffix3 | first_flag_suffix3 | First_Team | first_team | Flag_suffix | flag_suffix | Fulldate | fulldate | GP_Suffix | gp_suffix | Grand Prix | grand prix | Grid_from_ballot | grid_from_ballot | Grid_from_heats | grid_from_heats | Grid_from_number | grid_from_number | Grid_from_sprint | grid_from_sprint | image | Image | image_alt | image_link | Image_Link | image_size | image-alt | image-size | Lapchart | lapchart | location | Location | Official name | official name | Pole_Country | pole_country | Pole_Country2 | pole_country2 | Pole_Driver | pole_driver | Pole_Driver2 | pole_driver2 | Pole_flag_suffix | pole_flag_suffix | Pole_flag_suffix2 | pole_flag_suffix2 | Pole_Team | pole_team | Pole_Time | pole_time | Race_No | race_no | Scheduled_km | scheduled_km | Scheduled_laps | scheduled_laps | Scheduled_length | scheduled_length | Scheduled_mi | scheduled_mi | Season | Season_name | Season_No | season_no | Second_Country | second_country | Second_Country2 | second_country2 | Second_Country3 | second_country3 | Second_Driver | second_driver | Second_Driver2 | second_driver2 | Second_Driver3 | second_driver3 | Second_flag_suffix | second_flag_suffix | Second_flag_suffix2 | second_flag_suffix2 | Second_flag_suffix3 | second_flag_suffix3 | Second_Team | second_team | Third_Country | third_country | Third_Country2 | third_country2 | Third_Country3 | third_country3 | Third_Driver | third_driver | Third_Driver2 | third_driver2 | Third_Driver3 | third_driver3 | Third_flag_suffix | third_flag_suffix | Third_flag_suffix2 | third_flag_suffix2 | Third_flag_suffix3 | third_flag_suffix3 | Third_Team | third_team | Type | type | Weather | weather | year | Year | Previous_round | Next_round }}<noinclude>{{documentation}}</noinclude>