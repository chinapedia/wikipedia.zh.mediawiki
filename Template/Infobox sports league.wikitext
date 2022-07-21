{{infobox
| title     = {{if empty|{{{title|}}}|{{BASEPAGENAME}}}}

| subheader = {{#if: {{{current_season|}}} | '''当前赛季、赛事或届次：'''<br />{{Current sports event icon|sport={{{sport}}}|size=31px}} {{#iferror:{{#expr:{{{current_season}}}}}|[[{{{current_season}}}]]|{{{current_season}}}}} | {{#if: {{{last_season|}}} | '''最近的賽季或賽事：'''<br />{{#iferror:{{#expr:{{{last_season}}}}}|[[{{{last_season}}}]]|{{{last_season}}}}} | {{#if: {{{upcoming_season|}}} | '''即將展開的賽季或賽事：'''<br />{{Current sports event icon|sport={{{sport}}}|size=31px}} {{#iferror:{{#expr:{{{upcoming_season}}}}}|[[{{{upcoming_season}}}]]|{{{upcoming_season}}}}}}} }} }}{{#if: {{{current_season2|}}} | <br/>{{#iferror:{{#expr:{{{current_season2}}}}}|[[{{{current_season2}}}]]|{{{current_season2}}}}}}}
| labelstyle = white-space: nowrap

| image     = {{#invoke:InfoboxImage|InfoboxImage|image={{{logo|}}}|size={{{logo_size|{{{pixels|}}}}}}|sizedefault=200px}}
| caption   = {{{caption|}}}
| label1    = 前身
| data1     = {{if empty|{{{formerly|}}}|{{{Formerly|}}}}}
| label2    = {{#if:{{{game|}}}|游戏|运动}}
| data2     = {{#if:{{{game|}}}|{{{game}}}|{{#switch: {{lc: {{{sport}}}}} | amfootball | americanfootball = [[美式足球|American football]] | aussie rules | australian football = [[澳式足球|Australian rules football]] | squash = [[壁球|Squash]] | soccer = [[足球|Association football]] | {{#ifexist:{{{sport|}}}|[[{{{sport|}}}]]|{{{sport|}}}}} }} }}
| label3    = 創立
| data3     = {{{founded|}}}
| label4    = 创始人
| data4     = {{if empty|{{{founder|}}}|{{{Founder|}}}}}
| label5    = 首賽季
| data5     = {{{inaugural|}}}
| label6    = 中止
| data6     = {{{folded|}}}
| label7    = 取代
| data7     = {{if empty|{{{replaced|}}}|{{{Replaced|}}}}}
| label8    = {{#if:{{{administrator|}}}|管理員|所有者}}
| data8     = {{#if:{{{administrator|}}}|{{{administrator}}}|{{{owner|}}}}}
| label9    = [[首席执行官|CEO]]
| data9     = {{{ceo|}}}
| label10   = [[首席运营官|COO]]
| data10    = {{{coo|}}}
| label11   = 董事
| data11    = {{if empty|{{{director|}}}|{{{Director|}}}}}
| label12   = 董事长
| data12    = {{if empty|{{{chairman|}}}|{{{Chairman|}}}}}
| label13   = 主席
| data13    = {{if empty|{{{president|}}}|{{{President|}}}}}
| label14   = 會長
| data14    = {{if empty|{{{commissioner|}}}|{{{Commissioner|}}}}}
| label15   = 成名原因
| data15    = {{{fame|}}}
| label16   = 格言
| data16    = {{{motto|}}}
| label17   = 分部
| data17    = {{{divisions|}}}
| label18   = 隊伍數
| data18    = {{{teams|}}}
| label19   = 單打參賽者
| data19    = {{{singles|}}}
| label20   = 參賽者
| data20    = {{{competitors|}}}
| label21   = 國家或地區
| data21    = {{if empty|{{{countries|}}}|{{{country|}}}}}
| label22   = 總部
| data22    = {{{headquarters|}}}
| label23   = 場館
| data23    = {{{venue|}}}
| label24   = {{#if:{{{confed|}}}|洲际联盟|洲}}
| data24    = {{if empty|{{{confed|}}}|{{{continents|}}}|{{{continent|}}}}}
| label25   = {{#if: {{{folded|}}} |上届|应届}}冠軍
| data25    = {{if empty|{{{champion|}}}|{{{champions|}}}}}
| label26   = 奪冠最多
| data26    = {{if empty|{{{most_champs|}}}|{{{most successful club|}}}}}
| label27   = 分类
| data27    = {{{classification|}}}
| label28   = 資格
| data28    = {{{qualification|}}}
| label29   = 電視轉播
| data29    = {{{TV|{{{tv|}}}}}}
| label30   = 贊助商
| data30    = {{{sponsor|}}}
| label31   = {{#if:{{{pyramid|}}}|[[{{{pyramid}}}|金字塔]]|金字塔}}等级
| data31    = {{if empty|{{{level|}}}|{{{levels|}}}}}
| label32   = [[升降班制度|升級]]至
| data32    = {{{promotion|}}}
| label33   = [[升降班制度|降級]]至
| data33    = {{{relegation|}}}
| label34   = 國內盃賽
| data34    = {{{domestic_cup|}}}
| label35   = 國際盃賽
| data35    = {{{confed_cup|}}}
| label36   = 相關賽事
| data36    = {{{related_comps|}}}
| label37   = 比赛形式
| data37    = {{{tournament_format|}}}
| label38   = 官方網站
| data38    = {{{website|}}}
| header39  = {{#if:{{{footnotes|}}}|注释}}
| data40    = {{{footnotes|}}}
}}{{#invoke:Check for unknown parameters|check|unknown={{main other|[[Category:使用未知infobox sports league参数的页面|_VALUE_{{PAGENAME}}]]}}|preview=页面使用了[[Template:Infobox sports league]]不存在的参数"_VALUE_"|ignoreblank=y| administrator | caption | ceo | champion | champions | classification | commissioner | Commissioner | competitors | confed | confed_cup | continent | continents | coo | countries | country | current_season | current_season2 | director | Director | divisions | domestic_cup | fame | folded | footnotes | formerly | Formerly | founded | founder | Founder | game | headquarters | inaugural | last_season | level | levels | logo | logo_size | most successful club | most_champs | motto | owner | pixels | chairman | Chairman | president | President | promotion | pyramid | qualification | related_comps | relegation | replaced | Replaced | singles | sponsor | sport | teams | title | tournament_format | tv | TV | upcoming_season | venue | website }}<noinclude>
{{documentation}}
</noinclude>