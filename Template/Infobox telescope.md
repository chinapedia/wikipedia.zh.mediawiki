{{infobox
| bodyclass  = vcard
| aboveclass = fn org
| above = {{{name|{{PAGENAME}}}}}
| bodystyle =  {{{#if:{{{table_width|}}}|width: {{{table_width}}}|}}
| headerstyle = background:#ededed

| image   = {{#invoke:InfoboxImage|InfoboxImage|image={{#invoke:Wikidata|getValue|P18|{{{image|FETCH_WIKIDATA}}} }}|size={{{image_size|}}}|sizedefault=frameless|alt={{{alt|}}}}}
| caption = {{{caption|{{#invoke:Wikidata|claim|P18|qualifier=P2096|FETCH_WIKIDATA}}}}}

| header1 = 基本資料  
| label2 = 組織
| data2  = {{#invoke:Wikidata|getValue|P137|{{{organization|{{{organisation|FETCH_WIKIDATA}}}}}}}}

| label3 = 位置
| class3 = label
| data3  = {{#invoke:Wikidata|getValue|P276|{{{location|FETCH_WIKIDATA}}} }}{{#if:{{#Property:P276}}|{{#if:{{#Property:P17}}|{{#if:{{{location|}}}| |, {{#invoke:Wikidata|getValue|P17|FETCH_WIKIDATA}} }} }} }}

| label4 = 坐标
| data4  = {{#if:{{{coords|}}}{{{coordinates|}}} |  {{ifempty|{{{coordinates|}}}|{{{coords|}}}}} | {{#if:{{#Property:P625}} | {{Coord|nosave=1|display=inline,title|format=dms}} }} }}{{#ifeq:{{{refs|no}}}|yes|{{wikidata|references|normal+|{{{qid|}}}|P625}} }}

| label5 = 高度
| data5  = {{#invoke:Wikidata|getValue|P2044|{{{altitude|FETCH_WIKIDATA}}}}}

| label6 = 氣候
| data6  = {{{weather|}}}

| label7 = [[波長]]
| data7  = {{#invoke:Wikidata|getValue|P2808|{{{wavelength|FETCH_WIKIDATA}}}}}

| label8    = 建築
| rowclass8 = 註解
| data8     = {{{built|{{#if:{{#Property:P793}} | {{Start date|{{#invoke:Wikidata|claim|P793|qualifier=P580|FETCH_WIKIDATA}}–{{#invoke:Wikidata|claim|P793|qualifier=P582|FETCH_WIKIDATA}} }} }}}}}

| label9 = [[開光 (天文學)|啟用]]
| data9  = {{#invoke:Wikidata|getDateValue|P729|{{{first_light|FETCH_WIKIDATA}}}|ymd}}

| label10    = 望遠鏡型式
| rowclass10 = 註解
| class10    = 類別
| data10     = {{#invoke:Wikidata|getValue|P31|{{{style|FETCH_WIKIDATA}}}}}

| label11    = 口徑
| rowclass11 = 註解
| data11     = {{#invoke:Wikidata|getValue|P2386|{{{diameter|FETCH_WIKIDATA}}}}}

| label12    = 次鏡直徑
| rowclass12 = 註解
| data12     = {{{diameter2|}}}

| label13    = 第三鏡直徑
| rowclass13 = 註解
| data13     = {{{diameter3|}}}

| label14 = [[角解析度]]
| data14  = {{{angular_resolution|}}}

| label15 = 集光面積
| data15  = {{#invoke:Wikidata|getValue|P2046|{{{area|FETCH_WIKIDATA}}}}}

| label16 = [[焦長]]
| data16  = {{#invoke:Wikidata|getValue|P2151|{{{focal_length|FETCH_WIKIDATA}}}}}

| label17 = [[架台]]
| data17  = {{{mounting|}}}

| label18 = 圓頂
| data18  = {{{dome|}}}

| data19  = {{{website|{{#if:{{#property:P856}}|{{Url|1={{#invoke:Wikidata|getValue|P856|FETCH_WIKIDATA}} }} }} }}}

| header20  = {{{nrhp|{{{embedded|{{{module|}}}}}}}}}

| data21 = {{#if:{{#invoke:Wikidata|getValue|P373|{{{commons|FETCH_WIKIDATA}}} }} | {{icon|Commons}} [[Commons:{{#if:{{{commons|}}} | {{{commons}}} | Category:{{#invoke:Wikidata|getValue|P373|FETCH_WIKIDATA}} }} |维基共享资源]]}}
| below = {{#if:{{{child|}}}||{{EditOnWikidata}}}}

}}<noinclude>
{{documentation}}
</noinclude>