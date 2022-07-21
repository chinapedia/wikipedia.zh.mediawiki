{{Infobox
|bodyclass = vcard
|bodystyle = {{#if:{{{infobox_width|}}}|width:{{{infobox_width|23em}}}|}}

|titleclass = fn org
| title = {{{name|{{{bank_name|{{PAGENAMEBASE}}}}}}}}{{#if:{{{native_name|{{{bank_name_in_local|}}}}}}|<br />{{{native_name|{{{bank_name_in_local|}}}}}} }}
| above = {{{other_names|}}}
| image = {{#switch: {{#expr: {{#if:{{{logo|{{{image_1|}}}}}}|1|0}} + {{#if:{{{image|{{{image_2|}}}}}}|2|0}} }}
 |1={{#invoke:InfoboxImage|InfoboxImage|image={{{logo|{{{image_1|}}}}}}|size={{{logo_size|{{{image_width_1|}}}}}}|sizedefault=frameless|upright={{{logo_upright|1.1}}}|alt={{{logo_alt|{{{image_title_1|{{{logo_caption|}}}}}}}}}}}
 |2={{#invoke:InfoboxImage|InfoboxImage|image={{{image|{{{image_2|}}}}}}|size={{{image_size|{{{image_width_2|}}}}}}|sizedefault=frameless|upright={{{image_upright|1.1}}}|alt={{{alt|{{{image_title_2|{{{caption|}}}}}}}}}}}
 |3=<table><tr><td style="text-align:center; vertical-align:middle">{{#invoke:InfoboxImage|InfoboxImage|image={{{logo|{{{image_1|}}}}}}|size={{{logo_size|{{{image_width_1|}}}}}}|sizedefault=frameless|upright={{{logo_upright|.5}}}|alt={{{logo_alt|{{{image_title_1|{{{logo_caption|}}}}}}}}}}}<br />{{{logo_caption|{{{image_title_1|}}}}}}</td><td style="text-align:center; vertical-align:middle">{{#invoke:InfoboxImage|InfoboxImage|image={{{image|{{{image_2|}}}}}}|size={{{image_size|{{{image_width_2|}}}}}}|sizedefault=frameless|upright={{{image_upright|.7}}}|alt={{{alt|{{{image_title_2|{{{logo_caption|}}}}}}}}}}}<br />{{{caption|{{{image_title_2|}}}}}}</td></tr></table>
}}

| captionstyle = border-bottom:#aaa 1px solid
| caption= {{#switch: {{#expr: {{#if:{{{logo|{{{image_1|}}}}}}|1|0}} + {{#if:{{{image|{{{image_2|}}}}}}|2|0}} }}
 |1={{{logo_caption|{{{image_title_1|}}}}}}
 |2={{{caption|{{{image_title_2|}}}}}}
 |3=}}

|headerstyle = border-top:#aaa 1px solid

|rowclass1 = label
| label1 = 總部
|  data1 = {{{headquarters|}}}

| label2 = [[經緯度|坐標]]
|  data2 = {{{coordinates|}}}

| label3 = 成立
|  data3 = {{{established|{{{foundation|}}}}}}

| label4 = 所有者
|  data4 = {{{ownership|}}}

| label5 = 理事機構
|  data5 = {{{governance|}}}

| label6 = {{{executive_title|{{{leader_title|銀行總督}}}}}}
|  data6 = {{#invoke:Wikidata|getValue|P6|{{{executive|{{{president|FETCH_WIKIDATA}}}}}} }}

| label7 = 關鍵人物
|  data7 = {{{key_people|}}}{{{president2|}}}{{{president3|}}}

| label9 = 中央銀行
|  data9 = {{{bank_of|}}}

| label11 = 貨幣
|  data11 = {{{currency|}}}{{#if:{{{currency_iso|}}}|<br />{{{currency_iso|}}}&nbsp;([[ISO 4217]])|}}

| label12 = 儲備
|  data12 = {{{reserves|}}}

| label13 = 儲備要求
|  data13 = {{{reserve_requirements|}}}

| label14 = [[銀行利率]]
|  data14 = {{{borrowing_rate|}}}

| label15 = 利率目標
|  data15 = {{{interest_rate_target|}}}

| label16 = 準備金利息
|  data16 = {{{deposit_rate|}}}

| label17 = 超額準備金利息
|  data17 = {{{IOER|{{{excess_reserves|}}}}}} 

| label21 = 之前是
|  data21 = {{{predecessor|{{{preceded|}}}}}}
| label22 = 繼之後
|  data22 = {{{successor|{{{succeeded|}}}}}}

| label31 = 網站
|  data31 = {{{website|}}}

| belowstyle = border-top:1px solid #aaaaaa;text-align:left;font-size:smaller
| below = {{{footnotes|}}}

|data32 = {{{embed|}}}
}}<noinclude>

{{documentation}}
</noinclude>