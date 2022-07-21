{{Infobox
| bodyclass = vcard
| bodystyle = {{#if:{{{infoboxwidth|{{{width|}}}}}} |width:{{{infoboxwidth|{{{width}}}}}} }}
| headerstyle = background-color: #eee;
| labelstyle = white-space:nowrap;
| titleclass = fn org
| title = {{{name|{{{名称|{{{名稱|{{PAGENAME}}}}}}}}}}}
| subheader = {{#if:{{{native_name|{{{其他名称|{{{其他名稱|}}}}}}}}}|<span class="nickname" {{#if:{{{native_name_lang|}}}|lang="{{{native_name_lang|}}}" xml:lang="{{{native_name_lang|}}}"}}>'''{{{native_name|{{{其他名称|{{{其他名稱|}}}}}}}}}'''</span>}}
| image1 = {{#invoke:InfoboxImage|InfoboxImage|image={{{logo|{{{标志|{{{標誌|}}}}}}}}}|sizedefault=frameless|maxsize=300|size={{{logo_size|}}}|upright={{{logo_upright|1}}}|alt={{{logo_alt|}}}}}
| caption1 = {{{logo_caption|}}}
| image2 = {{#invoke:InfoboxImage|InfoboxImage|image={{{image|{{{图像|{{{圖像|}}}}}}}}}|sizedefault=frameless|maxsize=300|size={{{image_size|{{{imagesize|}}}}}}|upright={{{image_upright|1}}}|alt={{{alt|}}}}}
| caption2 = {{{caption|{{{图像说明|{{{圖像說明|}}}}}}}}}
| image3 = {{#if:{{{pushpin_map|{{{map_type|}}}}}}|{{Location map|{{{pushpin_map|{{{map_type}}}}}}
 | border = infobox
 | caption = {{#if:{{{map_caption|}}}|{{{map_caption}}}|在{{#invoke:Location map|data|{{{pushpin_map|{{{map_type}}}}}}|name}}的位置}}
 | float = center
 | width = {{#if:{{{map_size|}}}|{{{map_size}}}|220}}
 | relief = {{{pushpin_relief|{{{map_relief|}}}}}}
 | coordinates = {{{coordinates|{{{坐标|{{{坐標|}}}}}}}}}
 | label = {{{map dot label|}}}
 | lat_deg = {{#if:{{{coordinates|{{{坐标|{{{坐標|}}}}}}}}}||{{{lat_deg|}}}}}
 | lat_min = {{{lat_min|}}}
 | lat_sec = {{{lat_sec|}}}
 | lat_dir = {{{lat_dir|}}}
 | lon_deg = {{#if:{{{coordinates|{{{坐标|{{{坐標|}}}}}}}}}||{{{lon_deg|}}}}}
 | lon_min = {{{lon_min|}}}
 | lon_sec = {{{lon_sec|}}}
 | lon_dir = {{{lon_dir|}}}
 | lat = {{#if:{{{coordinates|{{{坐标|{{{坐標|}}}}}}}}}||{{{latitude|}}}}}
 | long = {{#if:{{{coordinates|{{{坐标|{{{坐標|}}}}}}}}}||{{{longitude|}}}}}
 }}}}
| image4 = {{If declined|{{{mapframe|}}}||{{Infobox mapframe
 |zoom={{{mapframe-zoom|}}}
 |frame-width={{{mapframe-width|}}}
 |frame-height={{{mapframe-height|}}}
 |stroke-color={{{mapframe-stroke-color|{{{mapframe-stroke-colour|}}}}}}
 |stroke-width={{{mapframe-stroke-width|1}}}
 |marker={{{mapframe-marker|museum}}}
 |marker-color={{{mapframe-marker-color|{{{mapframe-marker-colour|}}}}}}
 |frame-lat={{{mapframe-lat|{{{mapframe-latitude|}}}}}}
 |frame-long={{{mapframe-long|{{{mapframe-longitude|}}}}}}
 }}
}}
| caption4 = {{If declined|{{{mapframe|}}}||{{{mapframe-caption|}}}}}

| label1 = 舊名
| data1 = {{{former_name|}}}
| class1 = 暱稱

| label2 = 成立日期
| data2 = {{{established|{{{成立时间|{{{成立時間|{{{成立日期|}}}}}}}}}}}}

| label3 = 关闭日期
| data3 = {{{dissolved|{{{关闭时间|{{{關閉時間|{{{关闭日期|{{{關閉日期|}}}}}}}}}}}}}}}

| label4 = 地址
| data4 = {{{location|{{{地址|}}}}}}
| rowclass4 = adr
| class4 = locality

| label5 = [[經緯度]]
| data5 = {{#if:{{{coordinates|{{{坐标|{{{坐標|}}}}}}}}}|{{{coordinates|{{{坐标|{{{坐標}}}}}}}}}|{{#if:{{Both|{{{latitude|{{{lat_deg|}}}}}}|{{{longitude|{{{lon_deg|}}}}}}}}|
{{Geobox coor|{{{latitude|{{{lat_deg|}}}}}}|{{{lat_min|}}}|{{{lat_sec|}}}|{{{lat_dir|}}}|{{{longitude|{{{lon_deg|}}}}}}|{{{lon_min|}}}|{{{lon_sec|}}}|{{{lon_dir|}}}|{{#if:{{{coordinates_type|}}}|{{{coordinates_type}}}|type:landmark}}{{#if: {{{coordinates_region|}}}|_region:{{{coordinates_region}}}}}|{{#if:{{{coordinates_display|}}}|title|μ}}={{{coordinates_display|}}}|format={{{coordinates_format|}}}}}}}}}

| label6 = 類型
| data6 = {{{type|{{{类型|{{{類型|}}}}}}}}}

| label7 = 认证
| data7 = {{{accreditation|{{{委派经营|{{{委派經營|}}}}}}}}}

| label8 = 重要藏品
| data8 = {{{key_holdings|}}}

| label9 = 館藏
| data9 = {{{collections|{{{馆藏|{{{館藏|}}}}}}}}}

| label10 = 館藏規模
| data10 = {{{collection|{{{collection_size|{{{collection size|{{{馆藏规模|{{{館藏規模|}}}}}}}}}}}}}}}

| label11 = 参观人數
| data11 = {{{visitors|{{{参观人数|{{{參觀人數|}}}}}}}}}

| label12 = 建立者
| data12 = {{{founder|{{{建立者|}}}}}}
| class12 = agent

| label13 = {{#if:{{{leader_type|}}}|{{{leader_type}}}|Manager}}
| data13 = {{{leader|}}}
| class13 = agent

| label14 = 館長
| data14 = {{{director|{{{馆长|{{{館長|}}}}}}}}}
| class14 = agent

| label15 =館長
| data15 = {{{president|}}}
| class15 = agent

| label16 = 館長
| data16 = {{{chairperson|}}}
| class16 = agent

| label17 = 策展人
| data17 = {{{curator|{{{策展人|}}}}}}
| class17 = agent

| label18 = Historian
| data18 = {{{historian|}}}
| class18 = agent

| label19    = 建築師
| data19      = {{{architect|{{{建築師|}}}}}}
| class19     = agent

| label20 = 所有者
| data20= {{{owner|{{{所有者|}}}}}}
| class20 = agent

| label21 = 公共交通
| data21 = {{{publictransit|{{{公共交通|}}}}}}

| label22 = 附近{{#if:{{{parking|}}}|停車場|停車場}}
| data22 = {{#if:{{{parking|}}}|{{{parking}}}|{{{car_park|}}}}}

| label23 = 網站
| data23 = {{#if:{{{website|{{{官方网站|{{{官方網站|{{{网站|{{{網站|}}}}}}}}}}}}}}}|{{#ifeq:{{{website|{{{官方网站|{{{官方網站|{{{网站|{{{網站|}}}}}}}}}}}}}}}|hide||{{{website|{{{官方网站|{{{官方網站|{{{网站|{{{網站|}}}}}}}}}}}}}}}}}|{{official url}}}}

| header24 = {{#if:{{{network|}}}|{{Infobox museum/{{{network}}} network|header}} }}
| data25 = {{#if:{{{network|}}}|{{Infobox museum/{{{network}}} network|data}} }}

| header26 = {{{nrhp|{{{embedded|}}}}}}

|label27 = 地图
|data27  = {{{备注|{{{備註|}}}}}}

}}<noinclude>
{{documentation}}
</noinclude>