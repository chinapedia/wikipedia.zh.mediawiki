{{Infobox
| child = {{{child|}}}
| decat = yes <!--(remove this template from Template:Infobox tracking categories)-->
| titlestyle = font-size:130%; padding-bottom:0.15em;<!--(to avoid title touching box's border)-->
| title = {{#ifeq:{{{child|}}}|yes |'''文件格式详情''' |{{{name|<includeonly>{{PAGENAME}}</includeonly>}}}}}
| image1 = {{#invoke:InfoboxImage|InfoboxImage |image={{{icon|{{{logo|}}}}}} |size={{{icon_size|{{{logo_size|}}}}}} |sizedefault=64px}}
| caption1 = {{{iconcaption|{{{logocaption|}}}}}}
| image2 = {{#invoke:InfoboxImage|InfoboxImage |image={{{screenshot|}}} |size={{{screenshot_size|}}} |sizedefault=300px}}
| caption2 = {{{caption|}}}
| labelstyle = white-space: nowrap;padding:0.2em 0;line-height:1.2em;<!--(modified longitem)--> padding-right:0.65em;<!--(to ensure some gap between (long/unwrapped) label and data on same line)-->
| datastyle = line-height:1.35em;

| label4  = [[扩展名|-{zh-cn:扩展名; zh-tw:副檔名}-]]
|  data4  = {{#if:{{{extension|{{{extensions|}}}}}} |{{#if:{{{_noextcode|}}} |{{{extension|{{{extensions|}}}}}} |<code>-{}-{{{extension|{{{extensions|}}}}}}</code>}} }}
| label5  = [[互联网媒体类型|{{nowrap|-{zh-cn:互联网; zh-tw:網路}-}}{{nowrap|-{zh-cn:媒体类型; zh-tw:媒體型式}-}}]]
|  data5  = {{#if:{{{mime|}}} |{{#if:{{{_nomimecode|}}} |{{{mime}}} |<code>{{{mime}}}</code>}} }}
| label6  = {{le|类型代码|Type code}}
|  data6  = {{{type_code|{{{type code|{{{typecode|}}}}}}}}}
| label7  = [[统一类型标识]]
|  data7  = {{{uniform_type|{{{uniform type|}}}}}}
| label8  = UTI结构
|  data8  = {{{conforms to|{{{conforms_to|}}}}}}
| label9  = [[檔案格式#特征签名|特征签名]]
|  data9  = {{{magic|}}}
| label10 = {{nowrap|开发者}}
|  data10 = {{{developer|{{{owner|}}}}}}
| label11 = {{nowrap|初始版本}}
|  data11 = {{{released|}}}
| label12 = [[软件版本周期|最新版本]]
|  data12 = {{#if:{{{latest_release_version|{{{latest release version|}}}}}} |{{longitem |{{{latest_release_version|{{{latest release version|}}}}}}{{#if:{{{latest_release_date|{{{latest release date|}}}}}}|<br/>{{{latest_release_date|{{{latest release date|}}}}}}}}}} }}
| label13 = 格式类型
|  data13 = {{{type|{{{genre|}}}}}}
| label14 = [[视频文件格式|專門屬]]
|  data14 = {{{container_for|{{{container for|{{{containerfor|}}}}}}}}}
| label15 = 專門由
|  data15 = {{{contained_by|{{{contained by|{{{containedby|}}}}}}}}}
| label16 = -{zh-hant:延伸;zh-hans:扩展}-自
|  data16 = {{{extended_from|{{{extended from|{{{extendedfrom|}}}}}}}}}
| label17 = -{zh-hant:延伸;zh-hans:扩展}-为
|  data17 = {{{extended_to|{{{extended to|{{{extendedto|}}}}}}}}}
| label18 = 标准
|  data18 = {{{standard|{{{standards|}}}}}}
| label19 = {{nowrap|[[自由檔案格式|自由格式]]？}}
|  data19 = {{#switch:{{{free|}}}|Yes|yes=是|No|no=否|#default={{{free|}}}}}
| label20 = 网站
|  data20 = {{{url|}}}

}}<noinclude>{{Documentation}}
</noinclude>