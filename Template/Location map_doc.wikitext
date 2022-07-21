<noinclude>{{template doc page viewed directly}}</noinclude>
{{Notchinese|time=2008-09-04}}
{{lua|Module:Location map}}
基于现有采用[[:en:equirectangular projection|-{A|zh-hans:等距圆柱投影; zh-hant:正距圓筒圖法;}-]]的地图来创建一幅地理位置图作为[[m:Help:composite images|自创图像]]，同时可以在其上进行标示并选择性地叠加标签。需要注意的是:
:* 使用“caption=xxx”可以给地图加上外边框（缺省的“caption=”则保留地图的无边框状态）
:* 标示和标签不会去检查经度和纬度的有效性，并且有可能被置于页面的任何位置，甚至超越页面底部
:* 要忽略标示，可以设置marksize=1，即1个像素的宽度
:* 地图需要设置宽度，例如“width=250”（省略输入“px”），否则图像将会拉伸至整个页面
:* 要放置多个标示和标签，请''[[#See also|参看]]''
:* 要沿着汇合的经线做映射，请参考：''[[Template:Location_map_skew]]''

== 使用方法 ==
{{Location map
| USA
| relief = 1
| width = 320
| lat = 44.6
| long = -110.5
| caption = 黃石公園在美國西北部的位置
}}

{|
! 十進制度
!
! 度、分、秒
|- 
| style="vertical-align:top;" |
<pre style="overflow: auto; margin-right: 5px;">
{{Location map
| {{{1}}}
| width      = 
| float      = 
| border     = 
| caption    = 
| alt        = 
| relief     = 
| AlternativeMap = 
| overlay_image = 
| label      = 
| label_size = 
| position   = 
| background = 
| mark       = 
| marksize   = 
| link       = 
| lat_deg    = 
| lon_deg    = 
}}
</pre>
| width="20px" |
| style="vertical-align:top;" |
<pre style="overflow: auto; margin-right: 5px;">
{{Location map
| {{{1}}}
| width      = 
| float      = 
| border     = 
| caption    = 
| alt        = 
| relief     = 
| AlternativeMap = 
| overlay_image = 
| label      = 
| label_size = 
| position   = 
| background = 
| mark       = 
| marksize   = 
| link       = 
| lat_deg    = 
| lat_min    = 
| lat_sec    = 
| lat_dir    = 
| lon_deg    = 
| lon_min    = 
| lon_sec    = 
| lon_dir    = 
}}
</pre>
|}

== 可用地圖 ==
模版&#123;{Template:Location map location}&#125;的列表（省略了前缀“Template:”）：
{{Special:Prefixindex/Template:Location_map_}}

'''说明：'''若需要更多列表，请前往[[Special:PrefixIndex/Template:Location_map_]]并点击右上角的“下一页”。

同时可以参阅[[:Category:地理位置圖模板]]（现时还很不完整，但对于一些子类很有用）。

== 建立新地圖步驟 ==

# 找到一幅合适的使用[[:en:equirectangular projection|等距圆柱投影]]的空白地图
# 以「Template:Location map ''location''」的名稱建立模板（可從其他地圖模板複製過來，並輸入相關數據）

參見：[[模板:Location map/Creating a new map template|創建一個新地圖模版]]

== 範例 ==
=== 带默认说明的地图（度／分） ===
{{Location map | Croatia
| alt     = 位於島上的帕格
| lat_deg = 44 | lat_min = 26
| lon_deg = 15 | lon_min = 3
}}
<pre style="width: 40em;">
{{Location map | Croatia
| alt     = 位於島上的帕格
| lat_deg = 44 | lat_min = 26
| lon_deg = 15 | lon_min = 3
}}

</pre>
{{clear}}

=== 带默认说明的地图（十进制坐标） ===
{{Location map | Croatia
| alt     = 位於島上的帕格
| lat_deg = 44.44
| lon_deg = 15.05
}}
<pre style="width: 40em;">
{{Location map | Croatia
| alt     = 位於島上的帕格
| lat_deg = 44.44
| lon_deg = 15.05
}}
</pre>

=== 带默认说明和替代文字的地图 ===
{{Location map | Croatia
| width = 200
| float = right
| alt = 位於島上的帕格
| label = 帕格
| position = right
| mark = Green pog.svg <!--绿色标示点-->
| lat_deg = 44 | lat_min = 26 <!-- default: lat_dir = N -->
| lon_deg = 15 | lon_min = 3  <!-- default: lon_dir = E -->
}}
<pre style="width: 40em;">
{{Location map | Croatia
| width = 200
| float = right
| alt = 位於島上的帕格
| label = 帕格
| position = right
| mark = Green pog.svg <!--绿色标示点-->
| lat_deg = 44 | lat_min = 26 <!-- default: lat_dir = N -->
| lon_deg = 15 | lon_min = 3  <!-- default: lon_dir = E -->
}}
</pre>
{{clear}}

=== 标示和标签位于地图之外 ===
{{Location map | Croatia
| width    = 200
| float    = right
| caption  =
| alt      = 里米尼在意大利的位置（地圖之外）
| lat_deg  = 44.05
| lon_deg  = 12.57 <!--outside map's left border at 13.1-->
| outside  = 1 <!-- we're aware the point is outside the map, so suppress the warning category -->
| label    = 里米尼
| position = right
}}
<pre style="width: 60em;">
{{Location map | Croatia
| width    = 200
| float    = right
| caption  =
| alt      = 里米尼在意大利的位置（地圖之外）
| lat_deg  = 44.05
| lon_deg  = 12.57 <!--outside map's left border at 13.1-->
| outside  = 1 <!-- we're aware the point is outside the map, so suppress the warning category -->
| label    = 里米尼
| position = right
}}
</pre>
{{clear}}

=== 带自定义说明和文字背景的地图 ===
{| width=100%
| width=60% valign=top | '''Imotski'''
 <nowiki>{{Location map
 |Croatia
 |label=Imotski
 |lat=43.44
 |long=17.21
 |position=right
 |width=300
 |float=right
 |background=#FFFFDD
 |caption=Imotski&nbsp;在克罗地亚的位置
 }}</nowiki>
| width="300" align="center" | {{Location map|Croatia|label=Imotski|lat=43.44|long=17.21|position=right|width=300|float=right|background=#FFFFDD|caption=Imotski在克罗地亚的位置}}
|}

=== 標示和標簽都放大了的地圖 ===
{{Location map | Italy
| width      = 200
| float      = right
| caption    = 里米尼在意大利的位置
| alt        = 意大利的地圖，標記顯示里米尼的位置
| label      = 里米尼
| label_size = 150 <!--150% of normal size-->
| position   = bottom
| background = orange
| mark       = Orange_pog.svg
| marksize   = 12 <!--size in pixels-->
| lat_deg    = 44.05
| lon_deg    = 12.57
}}
<pre style="width: 40em;">
{{Location map | Italy
| width      = 200
| float      = right
| caption    = 里米尼在意大利的位置
| alt        = 意大利的地圖，標記顯示里米尼的位置
| label      = 里米尼
| label_size = 150 <!--150% of normal size-->
| position   = bottom
| background = orange
| mark       = Orange_pog.svg
| marksize   = 12 <!--size in pixels-->
| lat_deg    = 44.05
| lon_deg    = 12.57
}}
</pre>
{{clear}}

{{anchor|Using Alternative Map}}<!--former section name for links from other pages-->

=== 不带说明的地图 ===
{| width=100%
| width=60% valign=top | '''Brčko（波斯尼亚和黑塞哥维那）'''
 <nowiki>{{Location map
 |Bosnia
 |label=Brčko
 |position=left
 |width=150
 |lat=44.87
 |long=18.81
 |float=right
 |caption=
 }}</nowiki>
| width="250" | {{Location map|Bosnia|label=Brčko|position=left|width=150|lat=44.87|long=18.81|float=right|caption=}}
|}

{{anchor|Relief}}<!--former section name for links from other pages-->
=== 地形图参数 ===
Also demonstrates automatic positioning of label to the left, due to far right position of mark.
{{Location map | Nepal
| relief = yes
| caption = Location of Biratnagar Airport in Nepal
| alt = Biratnagar Airport is located in southeastern Nepal
| label = Biratnagar
| mark = Airplane silhouette.svg
| marksize = 10
| lat_deg = 26 | lat_min = 28 | lat_sec = 53 | lat_dir = N
| lon_deg = 87 | lon_min = 15 | lon_sec = 50 | lon_dir = E
}}
<pre style="width: 40em;">
{{Location map | Nepal
| relief = yes
| caption = Location of Biratnagar Airport in Nepal
| alt = Biratnagar Airport is located in southeastern Nepal
| label = Biratnagar
| mark = Airplane silhouette.svg
| marksize = 10
| lat_deg = 26 | lat_min = 28 | lat_sec = 53 | lat_dir = N
| lon_deg = 87 | lon_min = 15 | lon_sec = 50 | lon_dir = E
}}
</pre>
{{clear}}

{{Location map | Nepal
| relief = 
| caption = Location of Biratnagar Airport in Nepal
| alt = Biratnagar Airport is located in southeastern Nepal
| label = Biratnagar
| mark = Airplane silhouette.svg
| marksize = 10
| lat_deg = 26 | lat_min = 28 | lat_sec = 53 | lat_dir = N
| lon_deg = 87 | lon_min = 15 | lon_sec = 50 | lon_dir = E
}}
<pre style="width: 40em;">
{{Location map | Nepal
| relief = 
| caption = Location of Biratnagar Airport in Nepal
| alt = Biratnagar Airport is located in southeastern Nepal
| label = Biratnagar
| mark = Airplane silhouette.svg
| marksize = 10
| lat_deg = 26 | lat_min = 28 | lat_sec = 53 | lat_dir = N
| lon_deg = 87 | lon_min = 15 | lon_sec = 50 | lon_dir = E
}}
</pre>
{{clear}}

{{anchor|Alternative style of map}}<!--former section name for links from other pages-->

=== 置换成其它地图的参数（AlternativeMap） ===
{{Location map | Italy
| AlternativeMap = Italy location map.svg
| width   = 200
| float   = right
| caption = 羅馬在意大利的位置
| alt     = 意大利的地圖，標記顯示羅馬的位置
| label   = 羅馬
| lat_deg = 41.9
| lon_deg = 12.5
}}
<pre style="width: 40em;">
{{Location map | Italy
| AlternativeMap = Italy location map.svg
| width   = 200
| float   = right
| caption = 羅馬在意大利的位置
| alt     = 意大利的地圖，標記顯示羅馬的位置
| label   = 羅馬
| lat_deg = 41.9
| lon_deg = 12.5
}}
</pre>
{{clear}}

{{anchor|Relief}}<!--former section name for links from other pages-->

=== 在不同地图显示同一坐标 ===
{{Location map | Scotland
| relief = 1
| width = 180
| float = right
| caption = Lockerbie in Scotland, UK
| alt = Lockerbie is in southern Scotland.
| label = Lockerbie
| mark = Blue_pog.svg
| marksize = 9
| lat_deg = 55 | lat_min = 07 | lat_sec = 16 | lat_dir = N
| lon_deg = 03 | lon_min = 21 | lon_sec = 19 | lon_dir = W
}}
<pre style="width: 40em;">
{{Location map | Scotland
| relief = 1
| width = 180
| float = right
| caption = Lockerbie in Scotland, UK
| alt = Lockerbie is in southern Scotland.
| label = Lockerbie
| mark = Blue_pog.svg
| marksize = 9
| lat_deg = 55 | lat_min = 07 | lat_sec = 16 | lat_dir = N
| lon_deg = 03 | lon_min = 21 | lon_sec = 19 | lon_dir = W
}}
</pre>
{{clear}}

{{Location map | United Kingdom
| relief = 1
| width = 180
| float = right
| caption = Lockerbie in Scotland, UK
| alt = Lockerbie is in southern Scotland.
| label = Lockerbie
| mark = Blue_pog.svg
| marksize = 9
| lat_deg = 55 | lat_min = 07 | lat_sec = 16 | lat_dir = N
| lon_deg = 03 | lon_min = 21 | lon_sec = 19 | lon_dir = W
}}
<pre style="width: 40em;">
{{Location map | United Kingdom
| relief = 1
| width = 180
| float = right
| caption = Lockerbie in Scotland, UK
| alt = Lockerbie is in southern Scotland.
| label = Lockerbie
| mark = Blue_pog.svg
| marksize = 9
| lat_deg = 55 | lat_min = 07 | lat_sec = 16 | lat_dir = N
| lon_deg = 03 | lon_min = 21 | lon_sec = 19 | lon_dir = W
}}
</pre>
{{clear}}

=== 西半球 ===
{{Location map many | United Kingdom
| width = 180
| float = right
| caption = 蘇格蘭的洛克比
| label = 洛克比
| position = right
| lat_deg = 55 | lat_min=07 | lat_sec=16 | lat_dir=N
| lon_deg = 3 | lon_min=21 | lon_sec=19 | lon_dir=W
}}
<pre style="width: 40em;">
{{Location map many | United Kingdom
| width = 180
| float = right
| caption = 蘇格蘭的洛克比
| label = 洛克比
| position = right
| lat_deg = 55 | lat_min=07 | lat_sec=16 | lat_dir=N
| lon_deg = 3 | lon_min=21 | lon_sec=19 | lon_dir=W
}}
</pre>
{{clear}}

=== 幅员超过180°经度的国家 ===
{{Location map | Fiji
| width      = 180
| float      = right
| label      = 蘇瓦
| position   = right
| background = yellow
| mark       = Locator_Dot.png
| marksize   = 7
| lat_deg =  18 | lat_min =  8 | lat_sec = 0 | lat_dir = S
| lon_deg = 178 | lon_min = 26 | lon_sec = 0 | lon_dir = E
}}
<pre style="width: 40em;">
{{Location map | Fiji
| width      = 180
| float      = right
| label      = 蘇瓦
| position   = right
| background = yellow
| mark       = Locator_Dot.png
| marksize   = 7
| lat_deg =  18 | lat_min =  8 | lat_sec = 0 | lat_dir = S
| lon_deg = 178 | lon_min = 26 | lon_sec = 0 | lon_dir = E
}}
</pre>
{{clear}}
=== 用户选择多个地图===
需使用用户工具[[Wikipedia:用戶工具#輔助閱讀|显示地图切换按钮]]才能使本功能生效。
{{Location map | UK Scotland#UK
| relief = 1
| width = 180
| float = right
| caption = Lockerbie in Scotland, UK
| alt = Lockerbie is in southern Scotland.
| label = Lockerbie
| mark = Blue_pog.svg
| marksize = 9
| lat_deg = 55 | lat_min = 07 | lat_sec = 16 | lat_dir = N
| lon_deg = 03 | lon_min = 21 | lon_sec = 19 | lon_dir = W
}}
<pre style="width: 40em;">
{{Location map | UK Scotland#UK
| relief = 1
| width = 180
| float = right
| caption = Lockerbie in Scotland, UK
| alt = Lockerbie is in southern Scotland.
| label = Lockerbie
| mark = Blue_pog.svg
| marksize = 9
| lat_deg = 55 | lat_min = 07 | lat_sec = 16 | lat_dir = N
| lon_deg = 03 | lon_min = 21 | lon_sec = 19 | lon_dir = W
}}
</pre>
{{Clear}}

===“coordinates”與“lat_deg”“lat”===
如果“coordinates”參數與“lat_deg”參數同時使用，只有“coordinates”的值會生效。
{{Location map | Croatia
| coordinates = {{Coord|42|26|N|14|3|E}}
| lat_deg = 44 | lat_min = 26
| lon_deg = 15 | lon_min = 3
| caption = “coordinates”參數優先於“lat_deg”（“lat_deg”等參數所示位置位於克羅地亞海岸）
}}
<pre style="width:40em;">
{{Location map | Croatia
| coordinates = {{Coord|42|26|N|14|3|E}}
| lat_deg = 44 | lat_min = 26
| lon_deg = 15 | lon_min = 3
}}
</pre>

如果“coordinates”參數與“lat”參數同時使用，只有“coordinates”的值會生效。
{{Location map | Croatia
| coordinates = {{Coord|42|26|N|14|3|E}}
| lat = 44.4333
| long = 15.05
| caption = “coordinates”參數優先於“lat”（“lat”等參數所示位置位於克羅地亞海岸）
}}
<pre style="width:40em;">
{{Location map | Croatia
| coordinates = {{Coord|42|26|N|14|3|E}}
| lat = 44.4333
| long = 15.05
| caption = “coordinates”參數優先於“lat”（“lat”等參數所示位置位於克羅地亞海岸）
}}
</pre>

== 全部参数 ==
<table class="wikitable">
 <th>参数</th>
 <th>默认值</th>
 <th>描述</th>
 <tr>
  <th>{1}</th>
  <td> </td>
  <td> </td>
 </tr>
 <tr>
  <th>AlternativeMap=</th>
  <td>Location map {1}|image</td>
  <td><nowiki>[[</nowiki>File: {}]]</td>
 </tr>
 <tr>
  <th>background=</th>
  <td> </td>
  <td>background-color: {};</td>
 </tr>
 <tr>
  <th>border=</th>
  <td>#CCCCCC</td>
  <td>border: {};</td>
 </tr>
 <tr>
  <th>caption=</th>
  <td> </td>
  <td> </td>
 </tr>
 <tr>
  <th>float=</th>
  <td> </td>
  <td>float: {}; clear: {};</td>
 </tr>
 <tr>
  <th>label=</th>
  <td>{PAGENAME}</td>
  <td> </td>
 </tr>
 <tr>
  <th>lat=</th>
  <td>0</td>
  <td> </td>
 </tr>
 <tr>
  <th>lat_deg=</th>
  <td>0</td>
  <td> </td>
 </tr>
 <tr>
  <th>lat_dir=</th>
  <td> </td>
  <td> </td>
 </tr>
 <tr>
  <th>lat_min=</th>
  <td>0</td>
  <td> </td>
 </tr>
 <tr>
  <th>lat_sec=</th>
  <td>0</td>
  <td> </td>
 </tr>
 <tr>
  <th>long=</th>
  <td>0</td>
  <td> </td>
 </tr>
 <tr>
  <th>lon_deg=</th>
  <td>0</td>
  <td> </td>
 </tr>
 <tr>
  <th>lon_dir=</th>
  <td> </td>
  <td> </td>
 </tr>
 <tr>
  <th>lon_min=</th>
  <td>0</td>
  <td> </td>
 </tr>
 <tr>
  <th>lon_sec=</th>
  <td>0</td>
  <td> </td>
 </tr>
 <tr>
  <th>mark=</th>
  <td>Red pog.svg</td>
  <td><nowiki>[[</nowiki>File: {}]]</td>
 </tr>
 <tr>
  <th>marksize=</th>
  <td>8</td>
  <td><nowiki>[[</nowiki>File: {}px]]<br/>font-size: {}px;</td>
 </tr>
 <tr>
  <th>position=</th>
  <td>right</td>
  <td> </td>
 </tr>
 <tr>
  <th>width=</th>
  <td>240</td>
  <td>File: {}px<br/>width: ({}+2)px;</td>
 </tr>
</table>

== 另請參見 ==
* [[Template:Location map many]] – 放置多个标示和标签
* [[Template:Location map+]] – 放置标示和标签的长列表
* [[Template:Location map skew]] – 沿着汇合的经线做映射（非等距圆柱投影）
* [[commons:Category:Map pointers]]

<includeonly>
[[Category:地理位置圖模板| ]] 
</includeonly>
<templatedata>
{
	"params": {
		"width": {
			"description": "以像素为单位确定贴图的宽度，覆盖任何默认值；不包括px。例如，使用| width=300，而不是| width=300px。"
		},
		"default_width": {
			"description": "以像素为单位确定地图的默认宽度，供模板使用，例如放置信息框；默认值为240。不包括px。该值将乘以各个地图模板中指定的defaultscale参数（如果存在），以获得垂直地图的适当大小。例如，如果给定| default_width=200，将显示宽度为200×0.57=114像素的泰国地图（如模块：Location map/data/Thailand中所述）。"
		},
		"max_width": {
			"description": "地图的最大大小（以像素为单位）。供模板使用，例如放置信息框。不包括px。"
		},
		"float": {
			"description": "指定地图在页面上的位置；有效值包括left, right, center 和none。默认值是right"
		},
		"border": {
			"description": "指定1px地图边框的颜色；默认值为浅灰色（请参见网页颜色）。如果设置为“无”，则不会生成边框。这个参数很少使用。"
		},
		"caption": {
			"description": "地图下方显示的标题文本；指定标题将使地图显示一个框架。如果定义了| caption=但未指定值，则地图将不加边框，也不会显示任何标题。如果未定义| caption=，则不会对地图进行框显，并生成默认标题。默认标题是根据地图定义模板中的| label=参数（如果|label=未定义，则为当前页面名称）和|name=参数创建的。当以##分隔时，可以显示多个标题（即两个）。"
		},
		"alt": {
			"description": "Alt text for map; used by screen readers. See WP:ALT."
		},
		"relief": {
			"description": "任何非空值（1、yes等）都会导致模板将地图定义模板中指定的地图显示为image1，这通常是一张地形图；请参见[[模板:Location map+/relief]]上的示例。"
		}
	}
}
</templatedata>