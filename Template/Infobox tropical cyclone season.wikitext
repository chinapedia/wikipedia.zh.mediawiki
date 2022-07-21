<includeonly>{{Infobox
| bodyclass = vevent
| headerstyle = background-color: #CFCFCF;
| labelstyle   = white-space:nowrap;
| aboveclass = summary
| above = {{{Name|{{{name|{{PAGENAMEBASE}}}}}}}}

| image = {{#invoke:InfoboxImage|InfoboxImage|image={{{Track|}}}|size={{{Track size|300px}}}|alt={{{Track alt|}}}}}
| caption = {{{Track caption|氣旋季總結圖}}}

| header1 = 氣旋季長度
| label2 = 首-{}-個系統形成
| data2 = {{{First system formed|{{{First storm formed}}}}}} 
| label3 = 末個系統消散
| data3 = {{{Last system dissipated|{{{Last storm dissipated}}}}}}

| header4 = {{#if:{{{Strongest storm name|}}}|最強風暴}}
| data5 = {{#if:{{{Strongest storm name|}}}|{{Infobox|child=yes
  | label1 = 名稱
  | data1 = {{{Strongest storm name|}}}
  | label2 = &nbsp;•&nbsp;最高風速
  | data2 = {{#if:{{{Strongest storm winds|}}}|{{#switch:{{{Basin}}}|Atl|EPac={{#expr:((1.151*{{{Strongest storm winds}}})/5 round 0)*5}} mph（{{#expr:((1.852*{{{Strongest storm winds}}})/5 round 0)*5}} km/h）|{{#expr:((1.852*{{{Strongest storm winds}}})/5 round 0)*5}} km/h（{{#expr:((1.151*{{{Strongest storm winds}}})/5 round 0)*5}} mph）}}{{#if:{{{Average wind speed|}}}|<br>（<small>{{{Average wind speed}}}分鐘平均風速</small>）}}}}
  | label3 = &nbsp;•&nbsp;最低氣壓
  | data3 = {{#if:{{{Strongest storm pressure|}}}|{{#switch:{{{Basin}}}|Atl|EPac= {{{Strongest storm pressure}}} [[巴|mbar]]（[[帕斯卡|hPa]]；{{#expr:{{{Strongest storm pressure}}}/33.8635 round 2}} [[英寸汞柱|inHg]]）| {{{Strongest storm pressure}}} [[帕斯卡|hPa]]（[[巴|mbar]]）}}}}
}}}}

| header6 = {{#if:{{{Strongest CPac name|}}}|最強風暴}}
| data7 = {{#if:{{{Strongest CPac name|}}}|{{Infobox|child=yes
  | label1 = 名稱
  | data1 = {{{Strongest CPac name|}}}
  | label2 = &nbsp;•&nbsp;最高風速
  | data2 = {{#if:{{{Strongest CPac winds|}}}|{{#if:{{{Strongest CPac name|}}}|{{#expr:((1.151*{{{Strongest CPac winds}}})/5 round 0)*5}} mph（{{#expr:((1.852*{{{Strongest CPac winds}}})/5 round 0)*5}} km/h）|}}{{#if:{{{Average wind speed|}}}|<br>（<small>{{{Average wind speed}}}分鐘平均風速</small>）}}}}
  | label3 = &nbsp;•&nbsp;最低氣壓
  | data3 = {{#if:{{{Strongest CPac pressure|}}}|{{{Strongest CPac pressure}}} [[巴|mbar]]（[[帕斯卡|hPa]]；{{#expr:{{{Strongest storm pressure}}}/33.8635 round 2}} [[英寸汞柱|inHg]]）}}
}}}}

| header8 = 氣旋季統計
| label9 = {{#switch:{{{Basin}}}|NIO=低氣壓數|Atl|EPac=潛在熱帶氣旋數|WPac|SHem|SWI|Aus|SPac=熱帶擾動數}}
| data9 = {{{Total disturbances|}}}
| label10 = {{#switch:{{{Basin}}}|Atl|EPac=熱帶低氣壓數|WPac|SHem|SWI=熱帶低氣壓數|Aus=熱帶低氣壓數|NIO=強低氣壓數|SPac=熱帶低氣壓數}}
| data10 = {{{Total depressions|}}}
| label11 = {{#switch:{{{Basin}}}|Atl|EPac|WPac|SHem|SWI=風暴數|NIO=氣旋風暴數|Aus|SPac=熱帶氣旋數}}
| data11 = {{{Total storms|}}}
| label12 = {{#switch:{{{Basin}}}|Atl|EPac=颶風數|WPac=颱風數|NIO=強烈氣旋風暴數|熱帶氣旋數}}
| data12 = {{{Total hurricanes|}}}

| label13 = {{#switch:{{{Basin}}}|Atl|EPac=大型颶風數<br>（[[萨菲尔-辛普森飓风风力等级|三級+]]）|WPac=超級颱風數|Aus|SHem|SPac=強烈熱帶氣旋數|NIO=特強氣旋風暴數|SWI=強烈熱帶氣旋數}}
| data13 = {{{Total intense|}}}
| label14 = {{#switch:{{{Basin}}}|Atl|EPac=大型颶風數<br>（[[萨菲尔-辛普森飓风风力等级|三級+]]）|WPac=超級颱風數|Aus|SHem|SPac=強烈熱帶氣旋數|NIO=超級氣旋風暴數|SWI=特強熱帶氣旋數}}
| data14 = {{{Total super|}}}

| label15 = 死亡人數
| data15 = {{#if:{{{Fatalities|}}}|{{{Fatalities}}}|不明}}
| label16 = 財產損失
| data16 = {{#ifeq:{{{Damages}}}|None|無|{{#if:{{{Damages|}}}|{{#if:{{{Damagespre|}}}|{{{Damagespre}}}|}}${{#ifexpr:{{{Damages}}}<0.01|{{#expr:{{{Damages}}}*1000000}}|{{#ifexpr:{{{Damages}}}<100|{{#expr:{{{Damages}}}*100}}萬|{{#expr:{{{Damages}}}/100}}億}}}}（{{{Year}}}年[[美元]]）|不明}}<!--
-->{{#if:{{{Inflated|}}}|<br/>{{#if:{{{Damagespre|}}}|{{{Damagespre}}}|}}${{#ifexpr:({{{Damages}}}{{Inflation/US|{{{Year}}}|{{Inflation/year|US}}}})<1|{{#expr:({{{Damages}}}{{Inflation/US|{{{Year}}}|{{Inflation/year|US}}}})*1000 round {{{Inflated}}}}},000|{{#ifexpr:({{{Damages}}}{{Inflation/US|{{{Year}}}|{{Inflation/year|US}}}})<100|{{#expr:({{{Damages}}}{{Inflation/US|{{{Year}}}|{{Inflation/year|US}}}}) round {{{Inflated}}}}}百萬|{{#expr:({{{Damages}}}{{Inflation/US|{{{Year}}}|{{Inflation/year|US}}}})/100 round {{{Inflated}}}}}億}}}}美元（計入美元通脹，換算為{{Inflation/year|US}}年）|}}}}{{#if:{{{Damagespost|}}}|<br /><small>（{{{Damagespost}}}）</small>|}}<!-- Template:Inflation/US前面不需要*號 -->

| header17 = {{#ifexpr:{{#if:{{{Season stats|}}}|1|0}}+{{#if:{{{Season list|}}}|1|0}}+{{#if:{{{Season timeline|}}}|1|0}}+{{#if:{{{Atlantic season|}}}|1|0}}+{{#if:{{{East Pacific season|}}}|1|0}}+{{#if:{{{West Pacific season|}}}|1|0}}+{{#if:{{{North Indian season|}}}|1|0}}+{{#if:{{{Australian season|}}}|1|0}}+{{#if:{{{South Indian season|}}}|1|0}}+{{#if:{{{South Pacific season|}}}|1|0}}>0| 相關條目{{#ifexpr:{{#if:{{{Season stats|}}}|1|0}}+{{#if:{{{Season list|}}}|1|0}}+{{#if:{{{Season timeline|}}}|1|0}}+{{#if:{{{Atlantic season|}}}|1|0}}+{{#if:{{{East Pacific season|}}}|1|0}}+{{#if:{{{West Pacific season|}}}|1|0}}+{{#if:{{{North Indian season|}}}|1|0}}+{{#if:{{{Australian season|}}}|1|0}}+{{#if:{{{South Indian season|}}}|1|0}}+{{#if:{{{South Pacific season|}}}|1|0}}=1||}}}}

| data18=<div style="text-align: left;"> {{#if:{{{Season stats|}}}|
* [[{{{Season stats|}}}]]}}{{#if:{{{Season list|}}}|
* [[{{{Season list|}}}]]}}{{#if:{{{Season timeline|}}}|
* [[{{{Season timeline|}}}]]}}{{#if:{{{Atlantic season|}}}|
* [[{{{Atlantic season|}}}]]}}{{#if:{{{East Pacific season|}}}|
* [[{{{East Pacific season|}}}]]}}{{#if:{{{West Pacific season|}}}|
* [[{{{West Pacific season|}}}]]}}{{#if:{{{North Indian season|}}}|
* [[{{{North Indian season|}}}]]}}{{#if:{{{Australian season|}}}|
* [[{{{Australian season|}}}]]}}{{#if:{{{South Indian season|}}}|
* [[{{{South Indian season|}}}]]}}{{#if:{{{South Pacific season|}}}|
* [[{{{South Pacific season|}}}]]}}</div>

| belowclass   = hlist noprint nowrap
| belowstyle   = border-top: 1px solid #aaa; padding-top: 3px;
| below = {{autolink|{{#switch:{{{Basin}}}|Atl=大西洋颶風|EPac=太平洋颶風|WPac=太平洋颱風|NIO=北印度洋氣旋|Aus=澳洲地區熱帶氣旋|SWI=西南印度洋熱帶氣旋|SPac=南太平洋熱帶氣旋}}|{{#switch:{{{Basin}}}|Atl=大西洋颶風|EPac=太平洋颶風|WPac=太平洋颱風|NIO=北印度洋氣旋|Aus=澳洲地區熱帶氣旋|SWI=西南印度洋熱帶氣旋|SPac=南太平洋熱帶氣旋}}季}}{{#if:{{{five seasons|}}}|<br>{{{five seasons}}}}}
}}{{#ifeq:{{NAMESPACE}}|User||[[Category:不完整的热带气旋信息框]]}}</includeonly><noinclude>
{{documentation}}
</noinclude>