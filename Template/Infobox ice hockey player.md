{{infobox3cols
| child = {{{embed|}}}
| bodyclass = vcard
| bodystyle = line-height: 1.4em;
| title = {{#ifeq:{{{embed|}}}|yes|<hr style="background:#efefef; height:3px" />'''冰球生涯'''}}
| above = {{#ifeq:{{{embed|}}}|yes||{{{name<includeonly>|{{PAGENAME}}</includeonly>}}}}}
| aboveclass = fn
| abovestyle = font-size: 125%;

<!-- ###### 名人堂 -->
| subheaderstyle = background: #D0E7FF; font-weight:bold;
| subheader = {{#if: {{{halloffame|}}}|{{{halloffame}}}[[冰球名人堂]]}}

<!-- ###### 圖片 -->
| imagestyle = text-align: center; padding-top: 0.6em; padding-bottom: 0.7em;
| image = {{#invoke:InfoboxImage|InfoboxImage|image={{{image|}}}|size={{{image_size|}}}|sizedefault=frameless|upright=1|alt={{{alt|}}}|suppressplaceholder=yes}}
| caption = {{{caption|}}}

| labelstyle = white-space: nowrap;
| datastyle = white-space: nowrap;

<!-- ###### 出生 -->
| rowcellstyle1 = {{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}}
| label1 = 出生
| data1 = {{br separated entries | {{{birth_date|}}} | {{{birth_place|}}} }}

<!-- ###### 逝世 -->
| label2 = 逝世
| data2 = {{br separated entries | {{{death_date|}}} | {{{death_place|}}} }}

<!-- ###### 身高 -->
| rowcellstyle3 = {{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}}
| label3 = 身高
| data3 = {{#if:{{{height_in|}}}{{{height_ft|}}}
    |{{convert|{{{height_ft|0}}}|ft|{{#if:{{{height_in|}}}|{{{height_in}}}|0}}|in|cm|0|abbr=on}}
    |{{#if:{{{height_m|}}}
       |{{convert|{{{height_m|0}}}|m|ftin|abbr=on}}
       |{{#if:{{{height_cm|}}}| {{convert|{{{height_cm|0}}}|cm|ftin|abbr=on}} }}
     }}
   }}

<!-- ###### 體重 -->
| rowcellstyle4 = {{#if:{{{height_in|}}}{{{height_ft|}}}{{{height_m|}}}{{{height_cm|}}}||{{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}} }}
| label4 = 體重
| data4 =  {{#if:{{{weight_lbs|{{{weight_lb|}}}}}}<!--
  -->|{{convert|{{{weight_lbs|{{{weight_lb|0}}}}}}|lb|kg stlb|abbr=on}}<!--
  -->|{{#if:{{{weight_kg|}}}| {{convert|{{{weight_kg|0}}}|kg|lb stlb|0|abbr=on}} }}<!--
  -->}}

<!-- ###### 位置 -->
| rowcellstyle5 = {{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}}
| label5 = 位置
| class5 = role
| data5 = {{{position|}}}

<!-- ###### 射門 -->
| rowcellstyle6 = {{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}} 
| label6 = 射門
| data6 = {{{shoots|}}}

<!-- ###### 接球 -->
| rowcellstyle7 = {{#if:{{{shoots|}}}||{{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}} }}
| label7 = 接球
| data7 = {{{catches|}}}

<!-- ###### 球隊 -->
| rowcellstyle8 = {{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}}
| label8 = {{#if: {{{team}}}|{{{league}}}球隊}}{{#if: {{{prospect_team|}}}|&nbsp;{{nobold|（P）}}}}{{#if: {{{prospect_team|}}}|<br />效力球隊}}{{#if: {{{former_teams|}}}|<br />前效力球隊}} 
| data8 = {{#if: {{{team|}}}|'''{{{team}}}'''{{#if: {{{prospect_team|}}}|<br />{{{prospect_team|}}}&nbsp;({{{prospect_league|}}})}}{{#if: {{{former_teams|}}}|<br />{{{former_teams|}}}}}}}

<!-- ###### 退役 -->
| rowcellstyle9 = {{#if: {{{team|}}}||{{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}} }}
| label9 = 職業球隊
| data9 = {{{played_for|}}}

<!-- ###### 國際代表 -->
<!-- Set "|sex=f" to use same ntl_team/ntl_team_2/ntl_team_3 parameters to use template {{ihw}}; any other value for "|sex=" or omitting "|sex=" defaults to use template {{ih}} -->
| rowcellstyle10 = {{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}}
| label10 = 國家隊
| data10 = {{#if: {{{ntl_team|}}}{{{ntl_team_2|}}}{{{ntl_team_3|}}}| {{ih{{#ifeq:{{lc:{{{sex|}}}}}|f|w}}|{{{ntl_team|}}}|}}{{#if: {{{ntl_team_2|}}}|&nbsp;<br />{{ih{{#ifeq:{{lc:{{{sex|}}}}}|f|w}}|{{{ntl_team_2}}}|}}}}{{#if: {{{ntl_team_3|}}}|&nbsp;&<br />{{ih{{#ifeq:{{lc:{{{sex|}}}}}|f|w}}|{{{ntl_team_3}}}|}}}}}}

<!-- ###### NHL選秀 -->
| rowcellstyle11 = {{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}}
| label11  = [[{{#if:{{{draft_league|}}}|{{{draft_league}}}|NHL}}選秀]]
|  data11  = {{#if:{{{draftyear|{{{draft_year|}}}}}}|[[{{{draftyear|{{{draft_year}}}}}}年NHL選秀|{{{draftyear|{{{draft_year}}}}}}年]] {{#if:{{{draft|}}}|/ {{{draft}}} | {{#ifexpr:{{str find|{{lc:{{{draftpick|{{{draft_pick}}}}}}}}|territorial}} = -1|/ {{#switch:{{lc:{{{draftround|{{{draft_round|}}}}}}}}||非選秀|[[自由球員|非選秀]]=[[自由球員|非選秀]]|第{{{draftround|{{{draft_round}}}}}}輪<!--end switch-->}}<!--end ifexpr-->}} {{#if:{{{draftpick|{{{draft_pick|}}}}}}|/ 第{{#iferror:{{#ifexpr:{{{draftpick|{{{draft_pick}}}}}} > 0}}|{{{draftpick|{{{draft_pick}}}}}}|{{#ifeq:{{{draftpick|{{{draft_pick}}}}}}|1|[[NHL選秀狀元|1]]|{{{draftpick|{{{draft_pick}}}}}}<!--end ifeq-->}}順位<!--end iferror-->}}<!--end if draft_pick-->}}<!--end if draft-->}} }}
|  data12  = {{#if:{{both|{{{draftyear|{{{draft_year|}}}}}}|{{{draftteam|{{{draft_team|}}}}}}}}|被{{{draftteam|{{{draft_team}}}}}}選中 }}

<!-- ###### WHA選秀 -->
| rowcellstyle13 = {{#if: {{{draft|}}}{{{draft_year|}}}{{{draft_team|}}}|| {{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}} }}
| label13 = WHA選秀
| data13 = {{#if: {{{wha_draft|}}}{{{wha_draft_year|}}}{{{wha_draft_team|}}}| {{#if: {{{wha_draft_year|}}}|[[{{{wha_draft_year}}}年NHL選秀|{{{wha_draft_year}}}]]|}}{{{wha_draft}}}{{#if: {{{wha_draft_team|}}}|{{#if: {{{wha_draft|}}}{{{wha_draft_year|}}}|<br />}}{{{wha_draft_team|}}}|}}}}

<!-- ###### 職業生涯 -->
| rowcellstyle14 = {{#if: {{{draft|}}}{{{draft_year|}}}{{{draft_team|}}}{{{wha_draft|}}}{{{wha_draft_year|}}}{{{wha_draft_team|}}}|| {{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}} }}
| label14 = 職業生涯
| data14 = {{{career_start|{{{draft_year|&#123;&#123;&#123;career_start&#125;&#125;&#125;}}} }}}&ndash;{{#if:{{{career_end|}}} 
  | {{{career_end}}}
  | 至今
  }}

<!-- ###### 網頁 -->
| rowcellstyle15 = {{#ifeq:{{{embed|}}}|yes||border-top:#ccddee 1px solid;}}
| label15 = 網頁
| data15 = {{#if:{{{website|}}}|{{allow wrap|1={{{website|}}}}}}}

| data16 = {{#if:{{{medaltemplates|}}}|
{{Infobox medal templates
  |medals = {{{medaltemplates<includeonly>|</includeonly>}}}
  |expand = {{#ifeq:{{lc:{{{show-medals}}}}}|no||yes}}
  }}
}}

}}<includeonly>{{#ifeq:{{{nationality|+}}}|{{{nationality|-}}}|[[Category:Infobox ice hockey with deprecated parameters]]}}{{#ifeq:{{{nationality_2|+}}}|{{{nationality_2|-}}}|[[Category:Infobox ice hockey with deprecated parameters]]}}{{#ifeq:{{{nationality_3|+}}}|{{{nationality_3|-}}}|[[Category:Infobox ice hockey with deprecated parameters]]}}{{#ifeq:{{{nickname|+}}}|{{{nickname|-}}}|[[Category:Infobox ice hockey with deprecated parameters]]}}{{#ifeq:{{{ntl_team_women|+}}}|{{{ntl_team_women|-}}}|[[Category:Infobox ice hockey with deprecated parameters]]}}{{#ifeq:{{{ntl_team_women_2|+}}}|{{{ntl_team_women_2|-}}}|[[Category:Infobox ice hockey with deprecated parameters]]}}{{#ifeq:{{{ntl_team_women_3|+}}}|{{{ntl_team_women_3|-}}}|[[Category:Infobox ice hockey with deprecated parameters]]}}{{#ifeq:{{{shot|+}}}|{{{shot|-}}}|[[Category:Infobox ice hockey with deprecated parameters]]}}{{#ifeq:{{{caught|+}}}|{{{caught|-}}}|[[Category:Infobox ice hockey with deprecated parameters]]}}{{#if: {{{death_date|}}}{{{death_place|}}}|{{#if:{{{career_end|}}}||[[Category:Infobox ice hockey player with problems|A {{PAGENAME}}]]}}}}{{#if:{{{career_end|}}}||{{#if:{{{shot|}}}{{{caught|}}}|[[Category:Infobox ice hockey player with problems|B {{PAGENAME}}]]}}}}{{#ifeq:{{lc:{{{team|}}}}}|retired|{{#if:{{{career_end|}}}||[[Category:Infobox ice hockey player with problems|C {{PAGENAME}}]]}}}}{{#if:{{{career_start|}}}||[[Category:Infobox ice hockey player with problems|D {{PAGENAME}}]]}}</includeonly><noinclude>{{documentation}}</noinclude>