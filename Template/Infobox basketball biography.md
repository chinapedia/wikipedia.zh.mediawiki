{{infobox
| child = {{Yesno|{{{embed|no}}}}}
| bodyclass = vcard
| bodystyle = {{#if:{{{wide|}}}|width:{{{wide|}}}|width:26em}}

| titleclass = fn summary
| title    = {{#ifeq:{{Yesno|{{{embed|no}}}}}|yes|'''籃球生涯'''|{{{name|<includeonly>{{PAGENAMEBASE}}</includeonly>}}}}}

| image    = {{#invoke:InfoboxImage|InfoboxImage|image={{{image|}}}|size={{if empty|{{{image_size|}}}|{{{width|}}}}}|sizedefault=frameless|upright=1|alt={{{alt|}}}|suppressplaceholder=yes}}
| caption  = {{{caption|}}}

| headerstyle = {{Infobox basketball biography/style|{{delink|{{{team|}}}}}|border=2.5}}
| header1  = {{#if:{{{team|}}}
   |{{#if:{{{number|}}}|No. {{{number}}}&#32;–&#32;}}{{delink|{{{team}}}}}}}

| label2   = 位置
|  data2   = {{#if:{{{team|}}}|{{{position|}}}}}
| class2   = role

| label3   = 聯盟
|  data3   = {{#if:{{{team|}}}|{{{league|}}}}}

| header5  = {{#if:{{{birth_date|}}}{{{birth_place|}}}{{{death_date|}}}{{{death_place|}}}{{{nationality|}}}{{{height_ft|}}}{{{height_in|}}}{{{height_m|}}}{{{height_cm|}}}{{{height|}}}{{{weight_lbs|}}}{{{weight_lb|}}}{{{weight_kg|}}}{{{weight|}}}{{{college_class|}}}|個人資料}}

| label6   = 出生
|  data6   = {{br separated entries|{{{birth_date|}}}|{{{birth_place|}}}}}

| label7   = 逝世
|  data7   = {{br separated entries|{{{death_date|}}}|{{{death_place|}}}}}

| label8   = 國籍
|  data8   = {{{nationality|}}}{{#if: {{both|{{{nationality|}}}|{{{nationality_2|}}}}} |&#32;/&#32;}}{{{nationality_2|}}}

| label9   = 登錄身高
|  data9   = {{#if:{{{height_ft|}}}
     |{{convert|{{{height_ft|0|}}}|ft|{{if empty|{{{height_in|}}}|0}}|in|m|2|abbr=on|order={{{height_order|}}}}}{{{height_footnote|}}}
     |{{#if:{{{height_cm|}}}
       |{{convert|{{if empty|{{{height_cm|}}}|0}}|cm|ftin|0|abbr=on|order={{{height_order|}}}}}{{{height_footnote|}}}
       |{{#if:{{{height_m|}}}
         |{{convert|{{if empty|{{{height_m|}}}|0}}|m|ftin|0|abbr=on|order={{{height_order|}}}}}{{{height_footnote|}}}
         |{{#if:{{{height|}}}|{{Infobox person/height|{{{height}}}}}}}{{{height_footnote|}}}
         }}
       }}
     }}

| label10  = 登錄體重
|  data10  = {{#if:{{{weight_lbs|}}}{{{weight_lb|}}}
     |{{convert|{{if empty|{{{weight_lbs|}}}|{{{weight_lb|}}}}}|lb|kg|0|abbr=on|order={{{weight_order|}}}}}{{{weight_footnote|}}}
     |{{#if:{{{weight_kg|}}}
       |{{convert|{{if empty|{{{weight_kg|}}}|0}}|kg|lb|0|abbr=on|order={{{weight_order|}}}}}{{{weight_footnote|}}}
       |{{#if:{{{weight|}}}|{{Infobox person/weight|{{{weight}}}}}}}{{{weight_footnote|}}}
       }}
     }}

| header12 = {{#if:{{{highschool|}}}{{{high_school|}}}{{{high school|}}}{{{college|}}}{{{pro_club|}}}{{{draftyear|}}}{{{draft_year|}}}{{{draftteam|}}}{{{draft_team|}}}{{{draftyearpba|}}}{{{draft_year_pba|}}}{{{draftpba|}}}{{{draft_pba|}}}{{{debutyear|}}}{{{career_start|}}}{{{draft_year|}}}|職業資料}}

| label13  = 高中
|  data13  = {{if empty|{{{highschool|}}}|{{{high_school|}}}|{{{high school|}}}}}
| class13 = plainlist

| label14  = 大學
|  data14  = {{{college|}}}
| class14 = plainlist

| label15  = 選秀前俱樂部
|  data15  = {{{pro_club|}}}

| label16  = [[{{if empty|{{{draft_league|}}}|NBA}}選秀]]
|  data16  = {{#if:{{{draftyear|{{{draft_year|}}}}}}|[[{{{draftyear|{{{draft_year}}}}}}年{{#if:{{{draft_league|}}}|{{{draft_league}}}|NBA}}選秀|{{{draftyear|{{{draft_year}}}}}}年]] {{#if:{{{draft|}}}|/ {{{draft}}} | {{#ifexpr:{{str find|{{lc:{{{draftpick|{{{draft_pick}}}}}}}}|territorial}} = -1|/ {{#switch:{{lc:{{{draftround|{{{draft_round|}}}}}}}}||undrafted|選秀落選|[[選秀落選自由球員|選秀落選]]=[[選秀落選自由球員|選秀落選]]|<!-- Round:XX -->輪次：{{{draftround|{{{draft_round}}}}}}}}}} {{#if:{{{draftpick|{{{draft_pick|}}}}}}|/ <!--  Pick: XXth overall -->總順位：{{#iferror:{{#ifexpr:{{{draftpick|{{{draft_pick}}}}}} > 0}}|{{{draftpick|{{{draft_pick}}}}}}|{{#ifeq:{{{draftpick|{{{draft_pick}}}}}}|1|[[{{if empty|{{{draft_league|}}}|NBA}}選秀狀元|1<!-- first overall picks -->]]|{{{draftpick|{{{draft_pick}}}}}}}}}}}}}}}}
|  data17  = {{#if:{{both|{{{draftyear|}}}{{{draft_year|}}}|{{{draftteam|}}}{{{draft_team|}}}}}|被{{if empty|{{{draftteam|}}}|{{{draft_team}}}}}選中}}

| label18  = [[{{{draft_league2|}}}選秀]]<!-- 2021年臺灣選秀 -->
|  data18  = {{#if:{{{draftyear2|{{{draft_year2|}}}}}}|[[{{{draftyear2|{{{draft_year2}}}}}}年{{#if:{{{draft_league2|}}}|{{{draft_league2}}}|NBA}}選秀|{{{draftyear2|{{{draft_year2}}}}}}年]] {{#if:{{{draft2|}}}|/ {{{draft2}}} | {{#ifexpr:{{str find|{{lc:{{{draftpick2|{{{draft_pick2}}}}}}}}|territorial}} = -1|/ {{#switch:{{lc:{{{draftround2|{{{draft_round2|}}}}}}}}||undrafted|選秀落選|[[選秀落選自由球員|選秀落選]]=[[選秀落選自由球員|選秀落選]]|<!-- Round:XX -->輪次：{{{draftround2|{{{draft_round2}}}}}}}}}} {{#if:{{{draftpick2|{{{draft_pick2|}}}}}}|/ <!--  Pick: XXth overall -->總順位：{{#iferror:{{#ifexpr:{{{draftpick2|{{{draft_pick2}}}}}} > 0}}|{{{draftpick2|{{{draft_pick2}}}}}}|{{#ifeq:{{{draftpick2|{{{draft_pick2}}}}}}|1|[[{{{draft_league2|}}}選秀狀元|1<!-- first overall picks -->]]|{{{draftpick2|{{{draft_pick2}}}}}}}}}}}}}}}}
|  data19  = {{#if:{{both|{{{draftyear2|}}}{{{draft_year2|}}}|{{{draftteam2|}}}{{{draft_team2|}}}}}|被{{if empty|{{{draftteam2|}}}|{{{draft_team2}}}}}選中}}

| label20  = [[{{{draft_league3|}}}選秀]]<!-- 2021年臺灣選秀 -->
|  data20  = {{#if:{{{draftyear3|{{{draft_year3|}}}}}}|[[{{{draftyear3|{{{draft_year3}}}}}}年{{#if:{{{draft_league3|}}}|{{{draft_league3}}}|NBA}}選秀|{{{draftyear3|{{{draft_year3}}}}}}年]] {{#if:{{{draft3|}}}|/ {{{draft3}}} | {{#ifexpr:{{str find|{{lc:{{{draftpick3|{{{draft_pick3}}}}}}}}|territorial}} = -1|/ {{#switch:{{lc:{{{draftround3|{{{draft_round3|}}}}}}}}||undrafted|選秀落選|[[選秀落選自由球員|選秀落選]]=[[選秀落選自由球員|選秀落選]]|<!-- Round:XX -->輪次：{{{draftround3|{{{draft_round3}}}}}}}}}} {{#if:{{{draftpick3|{{{draft_pick3|}}}}}}|/ <!--  Pick: XXth overall -->總順位：{{#iferror:{{#ifexpr:{{{draftpick3|{{{draft_pick3}}}}}} > 0}}|{{{draftpick3|{{{draft_pick3}}}}}}|{{#ifeq:{{{draftpick3|{{{draft_pick3}}}}}}|1|[[{{{draft_league3|}}}選秀狀元|1<!-- first overall picks -->]]|{{{draftpick3|{{{draft_pick3}}}}}}}}}}}}}}}}
|  data21  = {{#if:{{both|{{{draftyear3|}}}{{{draft_year3|}}}|{{{draftteam3|}}}{{{draft_team3|}}}}}|被{{if empty|{{{draftteam3|}}}|{{{draft_team3}}}}}選中}}

| label22  = 職業生涯
|  data22  = {{#if:{{{debutyear|}}}{{{career_start|}}}|{{if empty|{{{debutyear|}}}|{{{career_start|}}}}}–{{if empty|{{{finalyear|}}}|{{{career_end|}}}|至今}}}}

| label23  = 位置
|  data23  = {{if empty|{{{career_position|}}}|{{#if:{{{team|}}}||{{{position|}}}}}}}

| label24  = 號碼
|  data24  = {{if empty|{{{career_number|}}}|{{#if:{{{team|}}}||{{{number|}}}}}}}

| label25  = 教練生涯
|  data25  = {{#if:{{{coach_start|}}}|{{{coach_start}}}–{{if empty|{{{coach_end|}}}|至今}}}}

| label26  = 裁判生涯
|  data26  = {{#if:{{{referee_start|}}}|{{{referee_start}}}–{{if empty|{{{referee_end|}}}|至今}}}}

| header27 = {{#if:{{{former_teams|}}}{{{teams|}}}{{{coach|}}}{{{years1|}}}{{{cyears1|}}}{{{team1|}}}{{{cteam1|}}}
 |{{#invoke:sports career|main
   | title = 生涯歷史
   | pheader = {{#if:{{{cyears1|}}}{{{cteam1|}}}|球員時期：}}
   | cheader = 教練時期：
   | pmax = 40 | pmaxcat = {{main other|[[Category:Pages using infobox basketball biography with long career|P]]}}
   | cmax = 30 | cmaxcat = {{main other|[[Category:Pages using infobox basketball biography with long career|C]]}}
   }}
 }}

| header28 = {{#if:{{{awards|}}}{{{highlights|}}}
 |{{Infobox|child = yes
   | decat   = yes <!-- remove from template:infobox tracking categories -->
   | datastyle = text-align: left;
   | title     = 生涯焦點與獎項

   |  data1= {{if empty|{{{awards|}}}|{{{highlights|}}}}}

   }}
 }}

| header29 = {{#if:{{both|{{{stat1label|}}}|{{{career_end|}}}{{{finalyear|}}}}}
 |{{Infobox|child = yes
   | decat   = yes <!-- remove from template:infobox tracking categories -->
   | labelstyle = text-align: right; line-height: 1.2em
   | datastyle  = line-height: 1.2em
   | title      = {{{stats_league|}}}生涯數據

   | label1 = {{{stat1label}}}
   |  data1 = {{#if:{{{stat1label|}}}|{{{stat1value|}}} }}
   | label2 = {{{stat2label}}}
   |  data2 = {{#if:{{{stat2label|}}}|{{{stat2value|}}} }}
   | label3 = {{{stat3label}}}
   |  data3 = {{#if:{{{stat3label|}}}|{{{stat3value|}}} }}
   }}
 }}
 
|  data30  = {{#if:{{{nbanew|}}}{{#property:P3647}}
  |<span style="font-weight:bold">{{#if:{{{nbanew|}}}
       | NBA.com上的[https://www.nba.com/player/{{{nbanew}}} 資料]
       | NBA.com上的[https://www.nba.com/player/{{#property:P3647}} 資料]{{EditAtWikidata|nbsp=y|pid=P3647}}
    }}</span>}}

| data31  = {{#if:{{{wnba_profile|}}}|<span style="font-weight:bold">WNBA.com上的[https://www.wnba.com/player/{{#invoke:String|replace|source={{lc:{{{wnba_profile}}}}}|pattern=_ |replace=-}} 資料]</span>}}

|  data32  = {{#if:{{{bbr|}}}|<span style="font-weight:bold">Basketball-Reference.com上的[https://www.basketball-reference.com/players/{{#if:{{{letter|}}}|{{{letter}}}|{{Str left|{{{bbr}}}|1}}}}/{{{bbr}}}.html 資料]</span>
   | {{#if:{{#property:P2685}}|<span style="font-weight:bold">Basketball-Reference.com上的[https://www.basketball-reference.com/players/{{#property:P2685}}.html 資料]{{EditAtWikidata|nbsp=y|pid=P2685}}</span>
       }}
   }}

|  data33  = {{#if:{{{bbr_wnba|}}}|<span style="font-weight:bold">Basketball-Reference.com上的[https://www.basketball-reference.com/wnba/players/{{#if:{{{letter|}}}|{{{letter}}}|{{Str left|{{{bbr_wnba}}}|1}}}}/{{{bbr_wnba}}}.html 資料]</span>}}

| header34 = {{#if:{{both|{{{cstats_league1|}}}|{{{coach_end|}}}}}
 |{{Infobox|child = yes
   | decat   = yes <!-- remove from template:infobox tracking categories -->
   | labelstyle = text-align: right; line-height: 1.2em
   | datastyle  = line-height: 1.2em
   | title      = 生涯執教紀錄

   | label1 = {{{cstats_league1}}}
   |  data1 = {{#if:{{{cstats_league1|}}}|{{Winning percentage|{{#if:{{{cwin1|}}}|{{{cwin1}}}|0}}|{{#if:{{{closs1|}}}|{{{closs1}}}|0}}|record=y}}}}
   | label2 = {{{cstats_league2}}}
   |  data2 = {{#if:{{{cstats_league2|}}}|{{Winning percentage|{{#if:{{{cwin2|}}}|{{{cwin2}}}|0}}|{{#if:{{{closs2|}}}|{{{closs2}}}|0}}|record=y}}}}
   | label3 = {{{cstats_league3}}}
   |  data3 = {{#if:{{{cstats_league3|}}}|{{Winning percentage|{{#if:{{{cwin3|}}}|{{{cwin3}}}|0}}|{{#if:{{{closs3|}}}|{{{closs3}}}|0}}|record=y}}}}
   | label4 = {{{cstats_league4}}}
   |  data4 = {{#if:{{{cstats_league4|}}}|{{Winning percentage|{{#if:{{{cwin4|}}}|{{{cwin4}}}|0}}|{{#if:{{{closs4|}}}|{{{closs4}}}|0}}|record=y}}}}
   | label5 = {{{cstats_league5}}}
   |  data5 = {{#if:{{{cstats_league5|}}}|{{Winning percentage|{{#if:{{{cwin5|}}}|{{{cwin5}}}|0}}|{{#if:{{{closs5|}}}|{{{closs5}}}|0}}|record=y}}}}
   }}
 }}

|  data35  = {{#if:{{{HOF|}}}{{{HOF_player|}}}{{{HOF_coach|}}}{{{WomensHOF}}}{{{FIBA_HOF_player|}}}{{{CBBASKHOF_year|}}}
 |{{infobox|child=yes
   | datastyle = font-weight:bold; background-color: #DCDCDC;
   |  data1= {{#if:{{{HOF|}}}|[http://www.hoophall.com/hall-of-famers/{{{HOF}}} 篮球名人堂]}}
   |  data2= {{#if:{{{HOF_player|}}}|[http://www.hoophall.com/hall-of-famers/{{{HOF_player}}} 作为球员入选篮球名人堂]}}
   |  data3= {{#if:{{{HOF_coach|}}}|[http://www.hoophall.com/hall-of-famers/{{{HOF_coach}}} 作为教练入选篮球名人堂]}}
   |  data4= {{#if:{{{WBHOF|}}}{{{womensHOF|}}}|{{wbhoflink|{{{WBHOF|}}}{{{womensHOF|}}}|女士篮球名人堂}}}}
   |  data5= {{#if:{{{FIBA_HOF_player|}}}|[http://halloffame.fiba.com/pages/eng/hof/indu/play/2007/p/lid_17904_newsid/{{{FIBA_HOF_player}}}/bio.html 國際籃球總會球員名人堂]}}
   |  data6= {{#if:{{{CBBASKHOF_year|}}}|大学篮球名人堂<br />于{{{CBBASKHOF_year}}}年入选 }}

   }}
 }}
| belowstyle = {{Infobox basketball biography/style|{{{team}}}}}
| below = {{#if:{{{medal_templates|}}}{{{medaltemplates|}}}|{{Infobox medal templates
   | title      = 獎牌
   | titlestyle = background-color: #DCDCDC; color: #000000;
   | medals     = {{if empty|{{{medal_templates|}}}|{{{medaltemplates|}}}}}
   | expand     = {{if empty|{{{medal_templates-expand|}}}|{{{medaltemplates-expand|}}}|{{#ifeq:{{lc:{{{show-medals}}}}}|no||yes}}}}
   }}
 }}

}}<!--
-->{{#invoke:Check for unknown parameters|check|unknown={{user other||[[Category:在籃球類模板使用未知參數的頁面|_VALUE_{{PAGENAME}}]]}}|preview = 頁面上 [[Template:Infobox basketball biography]] 使用了未知的參數 "_VALUE_"|ignoreblank=y
| regexp1 = years[%d][%d]* | regexp2 = team[%d][%d]* | regexp3 = cyears[%d][%d]* | regexp4 = cteam[%d][%d]*
| embed| wide| name| image| image_size| width| alt| caption| team| number| position| league| birth_date| birth_place| nationality| death_date| death_place| height_ft| height_in| height_m| height_cm| weight_lbs| weight_lb| weight_kg| college_class| nationality_2| height_order| height_footnote| height| weight_order| weight_footnote| weight| highschool| high_school| high school| college| pro_club| draftyear| draft_year| draftteam| draft_team| debutyear| career_start| draft_league| draft| draftpick| draft_pick| draftround| draft_round| draftyear2| draft_year2| draftteam2| draft_team2| debutyear2| career_start2| draft_league2| draft2| draftpick2| draft_pick2| draftround2| draft_round2| draftyear3| draft_year3| draftteam3| draft_team3| debutyear3| career_start3| draft_league3| draft3| draftpick3| draft_pick3| draftround3| draft_round3| finalyear| career_end| career_position| career_number| coach_start| coach_end| awards| highlights| stat1label| stats_league| stat1value| stat2label| stat2value| stat3label| stat3value| nbanew| wnba_profile| bbr| letter| bbr_wnba| cstats_league1| cwin1| closs1| cstats_league2| cwin2| closs2| cstats_league3| cwin3| closs3| cstats_league4| cwin4| closs4| cstats_league5| cwin5| closs5| HOF| HOF_player| HOF_coach| WBHOF| womensHOF| FIBA_HOF_player| CBBASKHOF_year| medal_templates| medaltemplates| medal_templates-expand| medaltemplates-expand| show-medals 
}}<!--
-->{{#if:{{{team|}}}|{{#ifexpr:{{#ifeq:{{str left|{{{team}}}|2}}|{{str left|[[link]]|2}}|1|0}}+{{#ifeq:{{str left|{{{team}}}|2}}|{{str left|'''[[link]]'''|2}}|1|0}}|{{#if:{{Infobox_basketball_biography/team_parameter_linked}}}} }}<!--
-->}}<noinclude>
{{documentation}}
</noinclude>