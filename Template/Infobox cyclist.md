{{Infobox
|bodyclass    = vcard
| child       = {{{embed|{{{child|}}}}}}

|title        = {{#ifeq:{{{embed|{{{child|}}}}}}|yes|'''自行车生涯'''|{{{name|{{{ridername|<includeonly>{{PAGENAMEBASE}}</includeonly>}}}}}}}}
|titleclass   = fn
|image        = {{#invoke:InfoboxImage|InfoboxImage|image={{{image|{{#invoke:Wikidata|claim|P18}}}}}|size={{{image_size|{{{size|}}}}}}|sizedefault=frameless|upright={{{image_upright|1}}}|alt={{{alt|}}}|suppressplaceholder=yes}}
|caption      = {{{caption|}}}
|headerstyle  = {{#ifeq:{{{child|{{{embed|}}}}}}|yes||background:#ADDFAD;}}
|labelstyle   = white-space:nowrap;

|header1  = {{#if:{{{full_name|}}}{{{fullname|}}}{{{nickname|}}}{{{birth_date|}}}{{{date_of_birth|}}}{{{birth_place|}}}{{{place_of_birth|}}}{{{death_date|}}}{{{date_of_death|}}}{{{death_place|}}}{{{place_of_death|}}}{{{height|}}}{{{weight|}}}|個人資料}}
|label2   = 全名                        |data2    = {{{full_name|{{{fullname|}}}}}}
|label3   = 綽號                        |data3    = {{{nickname|}}}     |class3  = nickname
|label4   = 出生                        |data4    = {{br separated entries|{{{birth_name|}}}|{{{birth_date|{{{date_of_birth|}}}}}}|{{{birth_place|{{{place_of_birth|}}}}}} }} 
|label5   = 逝世                        |data5    = {{br separated entries|{{{death_date|{{{date_of_death|}}}}}}|{{{death_place|{{{place_of_death|}}}}}} }} 
|label9   = 身高                        |data9    = {{#if: {{{height|}}} | {{Infobox person/height|{{{height}}}}} }}
|label10  = 體重                        |data10   = {{#if: {{{weight|}}} | {{Infobox person/weight|{{{weight}}}}} }}

|header11 = {{#if: {{{currentteam|}}} {{{discipline|}}} {{{role|}}} {{{ridertype|}}} | 車隊資料}}
|label12  = 目前效力車隊                 |data12   = {{{currentteam|}}}  |class12 = note
|label13  = 環境                        |data13   = {{{discipline|}}}
|label14  = 角色                        |data14   = {{{role|}}}         |class14 = role
|label15  = 類型                        |data15   = {{{ridertype|}}}

|header16 = {{#if:{{{amateuryears1|}}}{{{amateuryears|}}}{{{amateurteam1|}}}{{{amateurteams|}}}
  |{{infobox|child=yes
  | decat  = yes <!-- remove from template:infobox tracking categories -->
  | title  = 業餘車隊經歷
  | labelstyle = white-space:nowrap; line-height:1.2em;
  | datastyle  = white-space:nowrap; line-height:1.2em;
  | label1  = {{{amateuryears1|}}}{{#if:{{{amateuryears|}}}|<div style="line-height:1.7em">
{{{amateuryears|}}}</div>}} | data1 = {{{amateurteam1|}}}{{#if:{{{amateurteams|}}}|<div style="line-height:1.7em">
{{{amateurteams|}}}</div>}}
  | label2  = {{{amateuryears2|}}}  | data2  = {{{amateurteam2|}}}
  | label3  = {{{amateuryears3|}}}  | data3  = {{{amateurteam3|}}}
  | label4  = {{{amateuryears4|}}}  | data4  = {{{amateurteam4|}}}
  | label5  = {{{amateuryears5|}}}  | data5  = {{{amateurteam5|}}}
  | label6  = {{{amateuryears6|}}}  | data6  = {{{amateurteam6|}}}
  | label7  = {{{amateuryears7|}}}  | data7  = {{{amateurteam7|}}}
  | label8  = {{{amateuryears8|}}}  | data8  = {{{amateurteam8|}}}
  | label9  = {{{amateuryears9|}}}  | data9  = {{{amateurteam9|}}}
  | label10 = {{{amateuryears10|}}} | data10 = {{{amateurteam10|}}}
  | label11 = {{{amateuryears11|}}} | data11 = {{{amateurteam11|}}}
  | label12 = {{{amateuryears12|}}} | data12 = {{{amateurteam12|}}}
  | label13 = {{{amateuryears13|}}} | data13 = {{{amateurteam13|}}}
  | label14 = {{{amateuryears14|}}} | data14 = {{{amateurteam14|}}}
  | label15 = {{{amateuryears15|}}} | data15 = {{{amateurteam15|}}}
  }}
 }}

|header18 = {{#if:{{{proyears1|}}}{{{proyears|}}}{{{proteam1|}}}{{{proteams|}}}
  |{{infobox|child=yes
  | decat  = yes <!-- remove from template:infobox tracking categories -->
  | title  = 職業車隊經歷
  | labelstyle = white-space:nowrap; line-height:1.2em;
  | datastyle  = white-space:nowrap; line-height:1.2em;
  | label1  = {{{proyears1|}}}{{#if:{{{proyears|}}}|<div style="line-height:1.7em">
{{{proyears|}}}</div>}} | data1 = {{{proteam1|}}}{{#if:{{{proteams|}}}|<div style="line-height:1.7em">
{{{proteams|}}}</div>}}
  | label2  = {{{proyears2|}}}  | data2  = {{{proteam2|}}}
  | label3  = {{{proyears3|}}}  | data3  = {{{proteam3|}}}
  | label4  = {{{proyears4|}}}  | data4  = {{{proteam4|}}}
  | label5  = {{{proyears5|}}}  | data5  = {{{proteam5|}}}
  | label6  = {{{proyears6|}}}  | data6  = {{{proteam6|}}}
  | label7  = {{{proyears7|}}}  | data7  = {{{proteam7|}}}
  | label8  = {{{proyears8|}}}  | data8  = {{{proteam8|}}}
  | label9  = {{{proyears9|}}}  | data9  = {{{proteam9|}}}
  | label10 = {{{proyears10|}}} | data10 = {{{proteam10|}}}
  | label11 = {{{proyears11|}}} | data11 = {{{proteam11|}}}
  | label12 = {{{proyears12|}}} | data12 = {{{proteam12|}}}
  | label13 = {{{proyears13|}}} | data13 = {{{proteam13|}}}
  | label14 = {{{proyears14|}}} | data14 = {{{proteam14|}}}
  | label15 = {{{proyears15|}}} | data15 = {{{proteam15|}}}
  | label16 = {{{proyears16|}}} | data16 = {{{proteam16|}}}
  | label17 = {{{proyears17|}}} | data17 = {{{proteam17|}}}
  | label18 = {{{proyears18|}}} | data18 = {{{proteam18|}}}
  | label19 = {{{proyears19|}}} | data19 = {{{proteam19|}}}
  | label20 = {{{proyears20|}}} | data20 = {{{proteam20|}}}
  | label21 = {{{proyears21|}}} | data21 = {{{proteam21|}}}
  | label22 = {{{proyears22|}}} | data22 = {{{proteam22|}}}
  | label23 = {{{proyears23|}}} | data23 = {{{proteam23|}}}
  | label24 = {{{proyears24|}}} | data24 = {{{proteam24|}}}
  | label25 = {{{proyears25|}}} | data25 = {{{proteam25|}}}
  }}
 }}

|header20 = {{#if:{{{manageyears1|}}}{{{manageyears|}}}{{{manageteam1|}}}{{{manageteams|}}}
  |{{infobox|child=yes
  | decat  = yes <!-- remove from template:infobox tracking categories -->
  | title  = Managerial team(s)
  | labelstyle = white-space:nowrap; line-height:1.2em;
  | datastyle  = white-space:nowrap; line-height:1.2em;
  | label1  = {{{manageyears1|}}}{{#if:{{{manageyears|}}}|<div style="line-height:1.7em">
{{{manageyears|}}}</div>}} | data1 = {{{manageteam1|}}}{{#if:{{{manageteams|}}}|<div style="line-height:1.7em">
{{{manageteams|}}}</div>}}
  | label2  = {{{manageyears2|}}}  | data2  = {{{manageteam2|}}}
  | label3  = {{{manageyears3|}}}  | data3  = {{{manageteam3|}}}
  | label4  = {{{manageyears4|}}}  | data4  = {{{manageteam4|}}}
  | label5  = {{{manageyears5|}}}  | data5  = {{{manageteam5|}}}
  | label6  = {{{manageyears6|}}}  | data6  = {{{manageteam6|}}}
  | label7  = {{{manageyears7|}}}  | data7  = {{{manageteam7|}}}
  | label8  = {{{manageyears8|}}}  | data8  = {{{manageteam8|}}}
  | label9  = {{{manageyears9|}}}  | data9  = {{{manageteam9|}}}
  | label10 = {{{manageyears10|}}} | data10 = {{{manageteam10|}}}
  | label11 = {{{manageyears11|}}} | data11 = {{{manageteam11|}}}
  | label12 = {{{manageyears12|}}} | data12 = {{{manageteam12|}}}
  | label13 = {{{manageyears13|}}} | data13 = {{{manageteam13|}}}
  | label14 = {{{manageyears14|}}} | data14 = {{{manageteam14|}}}
  | label15 = {{{manageyears15|}}} | data15 = {{{manageteam15|}}}
  | label16 = {{{manageyears16|}}} | data16 = {{{manageteam16|}}}
  | label17 = {{{manageyears17|}}} | data17 = {{{manageteam17|}}}
  | label18 = {{{manageyears18|}}} | data18 = {{{manageteam18|}}}
  | label19 = {{{manageyears19|}}} | data19 = {{{manageteam19|}}}
  | label20 = {{{manageyears20|}}} | data20 = {{{manageteam20|}}}
  | label21 = {{{manageyears21|}}} | data21 = {{{manageteam21|}}}
  | label22 = {{{manageyears22|}}} | data22 = {{{manageteam22|}}}
  | label23 = {{{manageyears23|}}} | data23 = {{{manageteam23|}}}
  | label24 = {{{manageyears24|}}} | data24 = {{{manageteam24|}}}
  | label25 = {{{manageyears25|}}} | data25 = {{{manageteam25|}}}
  }}
 }}

|header22 = {{#if:{{{majorwins|}}}
  |{{infobox|child=yes
  | decat  = yes <!-- remove from template:infobox tracking categories -->
  | title  = 主要戰績
  | datastyle = text-align:left;
  | data1  = 
{{{majorwins|}}}
  }}
 }}

|header24 = {{Infobox medal templates
  | title = 獎牌紀錄<!-- default is "Medal record" -->
  | medals = {{{medaltemplates|}}}
  | expand = {{{show-medals|}}}
 }}

|belowstyle  = color:darkslategray; font-size:82%
|below = {{#if:{{{updated|}}}|最近一次更新<br />{{{updated|}}}}}
}}<noinclude>{{Documentation}}

[[Category:体育人物信息框模板]]</noinclude>