<div style="text-align: center;"></div><includeonly>{{lua|模块:Coordinates}}</includeonly><noinclude>{{template doc page viewed directly}}</noinclude>
<!-- 請在此線底下編輯模板的說明文件 -->
<!-- {{过期翻译|time=2008-05-01T14:34:32}} -->
<!-- {{shortcut|[[WP:COORD]]}} -->{{TOCright}}
{{noteTA
|1=zh-cn:内联;zh-tw:內嵌;
}}
{{High-risk|259154}}
{{tl|coord}}模板根基于地理坐标及其他参数，生成一个前往地图资源清单的链接，并提供一个标准化的坐标表示法。
{{#switch: {{FULLPAGENAME}} | Template:Coord | Template:Coord/doc = {{Uses Wikidata|P625}} {{Tracks Wikidata|P625|cat=维基数据坐标数据相关分类}} }}

此模板要用[[地球]]上的[[WGS84]]地理坐标（[[经度]]、[[纬度]]），坐标可以使用适当的精确度以十进位计数法（小数）输入，或者用[[角度|度]]/[[角分|分]]/[[角秒|秒]]参数输入。本模板链接到https://tools.wmflabs.org/geohack//geohack.php?language=zh&pagename=Template:Coord&params=xxx ，并显示坐标值。点击其中的蓝色星球[[File:Erioll_world.svg|18px]]会激活[[:meta:WikiMiniAtlas|WikiMiniAtlas]]地图显示（需要Javascript）。

'''注意：'''中国大陆地区的商业地形图坐标都加了偏移，建议优先使用OpenStreetMap坐标。（右键“显示地址”即可读出。）如要使用Google或Bing的数据，请使用卫星地图中的坐标。百度地图和Google.cn的卫星图也都有偏移，应避免使用。地形图中的坐标由于使用的是来自于中国大陆厂商提供的坐标数据，已经[[中华人民共和国测绘限制|根据中国政府的要求]]人工偏移。要将这类坐标修正为WGS84，可以使用[[User:Artoria2e5/Gadget-PRCoords.js]]小工具或[https://artoria2e5.github.io/PRCoords/demo 其线上版本]（请使用带cai的高精度解）；其中大部分地图使用的是[[GCJ-02]]偏移算法，百度地图用的则是[[BD-09]]。 

{{Coord how-to}}

若使用其他的角度單位，請參看以下转换表：
{{相同角度的轉換表}}

本模板的输出数据以下列形式提供：
* 度/分/秒（“DMS”，精确度是度、或度/分、或度/分/秒，基于输入值）。一些从十进制（小数的）度到度分秒的换算需要修正（参见[[:en:Template_talk:Coord/doc#template:Coord/dec2dms/dms|英文讨论]]）。
* 小数（精确度由小数位数确定，基于输入值）。
* [[Geo|地理信息]]。

[[Google地球]]等不少程序都会解析维基百科的数据库转储文件，寻找{{tl|coord}}中的坐标信息。'''为了确认坐标被正确地解析，一定要使用<code>display=title</code>。'''参见[//earth.google.com/userguide/v4/geoweb_faq.html 如何让我的维基百科条目出现在谷歌地球地理网络层？]'''。一定不要'''未经预先讨论就匆忙修改本模板。

另请参见[[:en:Wikipedia:WikiProject Geographical coordinates|地理坐标专题]]{{en icon}}。
<!-- 
This template, {{tl|coord}}, produces a link to a list of map sources, based on the geographical coordinates and other parameters, and provides a standardized notation for the coordinates.

The template is for [[WGS84]] geographical coordinates ([[latitude]];[[longitude]]) on [[Earth]], which can be entered in either decimal notation, or degrees/minutes/seconds parameters, with the appropriate precision.

It links to {{Coor URL}}, then displays the coordinates.

The template outputs data in:
* Degree/minutes/seconds ("DMS", precision is degrees, or degrees/minutes, or degrees/minutes/seconds, based on input)
* Decimal (precision by number of decimal places, based on input)
**  A computer-readable [[Geo (microformat)|Geo microformat]].

{{tl|coord}} will imminently be used by tools which parse the raw Wikipedia database dumps, such as [[Google Earth]]. The template '''must not''' be modified without reference to that project ([[User talk:Gmaxwell#The benefit of hindsight|link needed]]).

See also [[Wikipedia:WikiProject Geographical coordinates]].
-->

== 取代對象 ==
这个单一的模板將取代以下模板：
* {{tl|coor dms}}
* [//zh.wikipedia.org/w/index.php?title=Special:PrefixIndex&from=Geolinks&namespace=10 Geolinks]模板
* [//zh.wikipedia.org/w/index.php?title=Special:PrefixIndex&from=Mapit&namespace=10 Mapit]模板

所有参数能够像以前一样使用，参见[[#用法|用法]]。

举例：
{| class="wikitable"
|-
!模板編碼||被取代模板編碼
|-
| <nowiki>{{coord|12|N|45|W|display=title}}</nowiki> || <nowiki>{{coor title d|12|N|45|W}}</nowiki>
|-
| <nowiki>{{coord|12|34|N|45|33|W|display=title}}</nowiki> || <nowiki>{{coor title dm|12|34|N|45|33|W}}</nowiki>
|-
| <nowiki>{{coord|12|34|56|N|45|33|22|W|display=title}}</nowiki> || <nowiki>{{coor title dms|12|34|56|N|45|33|8|W}}</nowiki>
|-
| <nowiki>{{coord|12|34|12|N|45|33|45|W|display=inline,title}}</nowiki> || <nowiki>{{coor at dms|12|34|12|N|45|33|45|W}}</nowiki> 
|-
| <nowiki>{{coord|10.2|-20.3|display=inline}}</nowiki> 或 <br /> <nowiki>{{coord|10.2|-20.3}}</nowiki> || <nowiki>{{coor d|10.2|N|-20.3|E}}</nowiki>
|-
| <nowiki>{{coord|44.4|-111.1|type:city_region:US|display=inline,title}}</nowiki> || <nowiki>{{Geolinks-US-cityscale|44.4|-111.1}}</nowiki>
|-
| <nowiki>{{coord|51.01234|-1.56789|type:landmark_region:GB|display=inline,title}}</nowiki> || <nowiki>{{Geolinks-UK-buildingscale|51.01234|-1.56789}}</nowiki>
|-
| <nowiki>{{coord|-35.5|150.1|type:landmark_region:AU|display=inline,title}}</nowiki> || <nowiki>{{Mapit-AUS-suburbscale|lat=-35.5|long=150.1}}</nowiki>
|-
| <nowiki>{{coord|12|34|12|N|45|33|45|W|display=title}}</nowiki> || <nowiki>{{CoorHeader|12|34|12|N|45|33|45|W}}</nowiki>
|}

<!-- 
==Superseded templates==

This single template supersedes {{tl|coor d}}, {{tl|coor dm}}, {{tl|coor dms}}, {{tl|coor at d}}, {{tl|coor at dm}}, {{tl|coor at dms}}, {{tl|coor title d}}, {{tl|coor title dm}}, and {{tl|coor title dms}}. All parameters can be used as before - see [[#Usage|Usage]].

Examples:
<table class="prettytable">
<tr><td>&#123;{coord|12|34|N|45|33|W|'''display=title'''}&#125;</td><td>Replaces &#123;{coor '''title''' dm|12|34|N|45|67|W}&#125;</td></tr>
<tr><td>&#123;{coord|12|34|12|N|45|33|45|W|'''display=inline,title'''}&#125;</td><td>Replaces &#123;{coor '''at''' dms|12|34|12|N|45|33|45|W}&#125;</td></tr>
<tr><td>&#123;{coord|10.2|-20.3|'''display=inline'''}&#125; or &#123;{coord|10.2|-20.3}&#125;</td><td>Replaces &#123;{coor d|10.2|N|-20.3|E}&#125;</td></tr>
</table>
 -->
== 用法 ==

 &#123;{coord|''latitude''|''longitude''|''坐标参数''|''模板参数''}&#125;
 &#123;{coord|''dd''|''N/S''|''dd''|''E/W''|''坐标参数''|''模板参数''}&#125;
 &#123;{coord|''dd''|''mm''|''N/S''|''dd''|''mm''|''E/W''|''坐标参数''|''模板参数''}&#125;
 &#123;{coord|''dd''|''mm''|''ss''|''N/S''|''dd''|''mm''|''ss''|''E/W''|''坐标参数''|''模板参数''}&#125;

有两类参数，都是可选的：
* 坐标参数：以地图服务器识别，以''参数:值''的格式给出，并且藉由下划线字符“_”互相隔开。常见的坐标参数包括''type''、''region''、和''scale''。参见[[#坐标参数|坐标参数]]查看全面的列表。
* 模板参数：為模板自身所使用，以''参数=值''的格式给出，并且由管道符“|”互相隔开。支持的模板参数有''display''、''name''和''format''。
** ''display''可以为下列之一：
*** <code>display=inline</code> — 内联（inline）显示坐标（缺省值）
*** <code>display=title</code> — 显示坐标在条目标题旁边（取代{{tl|coor title dms}}模板家族），快捷方式为<code>display=t</code>
*** <code>display=inline,title</code> — 同时内联显示和在标题处显示坐标（取代{{tl|coor at dms}}模板家族）<br />注意：使用title属性表明坐标适用于该条目，而不只是适用于条目中提及的某一个地点（可能提及了许多地点）——因此该属性只能在后一种情形下才应当省略。<code>display=title,inline</code>也是有效的。快捷方式为<code>display=it</code>
** ''format''可以用来强制显示dec或dms坐标给所有读者。
** ''name''可以用来注释内联坐标，用于在地图服务或其他外部用途中的显示。它不应用到条目标题旁，或顯示於一个信息框内部的那些坐标，由于在那些情况下条目标题就是隐含的名称。
** ''notes''可以用来指定紧接在坐标后的文字。主要用于给标题旁的坐标添加脚注。
** ''qid''可以用来指定显示哪个数据项的坐标。主要用于使用维基数据的信息框。

== 举例 ==
{| class="prettytable"
| <code><nowiki>{{coord|43.651234|-79.383333}}</nowiki></code>
| {{coord|43.651234|-79.383333}}
| 多伦多 - 全小数 - N & W<!-- Toronto - Fully decimal - N & W -->
|-
| <code><nowiki>{{coord|43.65|-79.38}}</nowiki></code>
| {{coord|43.65|-79.38}}
| 多伦多 - 更小精确度<!-- Toronto - less precise -->
|-
| <code><nowiki>{{coord|43.6500|-79.3800}}</nowiki></code>
| {{coord|43.6500|-79.3800}}
| 多伦多 - 中等精确度，带尾随零<!-- Toronto - medium precision with trailing zeroes -->
|-
| <code><nowiki>{{coord|43.651234|N|79.383333|W}}</nowiki></code>
| {{coord|43.651234|N|79.383333|W}}
| 多伦多 - 小数，带北向纬度差与西向经度差（N & W）<!-- Toronto - decimal with Northing & Westing -->
|-
| <code><nowiki>{{coord|43|29|N|79|23|W}}</nowiki></code>
| {{coord|43|29|N|79|23|W}}
| 多伦多 - 度数与分数<!-- Toronto - degrees & minutes -->
|-
| <code><nowiki>{{coord|43|29|4|N|79|23|0|W}}</nowiki></code>
| {{coord|43|29|4|N|79|23|0|W}}
| 多伦多 - 度数、分数与秒数<!-- Toronto - degrees, minutes & seconds -->
|-
| <code><nowiki>{{coord|43|29|4.5|N|79|23|0.5|W}}</nowiki></code>
| {{coord|43|29|4.5|N|79|23|0.5|W}}
| 多伦多 - 度数、分数与秒数（小数）<!-- Toronto - degrees, minutes, seconds & fractions of seconds -->
|-
| <code><nowiki>{{coord|55.752222|N|37.615556|E}}</nowiki></code>
| {{coord|55.752222|N|37.615556|E}}
| 莫斯科 - N & E<!-- Moscow - N & E -->
|-
| <code><nowiki>{{coord|55.752222|N|37.615556|E|format=dms}}</nowiki></code>
| {{coord|55.752222|N|37.615556|E|format=dms}}
| 转换至dms格式<!-- Convert to dms format -->
|-
| <code><nowiki>{{coord|39.098095|-94.587307|format=dms}}</nowiki></code>
| {{coord|39.098095|-94.587307|format=dms}}
| 十进制转换，不带N/S/E/W<!-- Decimal conversion without N/S/E/W -->
|-
| <code><nowiki>{{coord|55.752222|N|37.615556|E|&#8203;format=dec|name=Moscow}}</nowiki></code>
| {{coord|55.752222|N|37.615556|E|format=dec|name=Moscow}}
| 转换至十进制，并在某些地图上贴上标签<!-- Convert to decimal and label on some maps -->
|-
| <code><nowiki>{{coord|33|55|S|18|25|E}}</nowiki></code>
| {{coord|33|55|S|18|25|E}}
| 开普敦 - S & E<!-- Cape Town - S & E -->
|-
| <code><nowiki>{{coord|35|00|N|105|00|E}}</nowiki></code>
| {{coord|35|00|N|105|00|E}}
| 中华人民共和国<!-- China, People's Republic of -->
|-
| <code><nowiki>{{coord|22|54|30|S|43|14|37|W}}</nowiki></code>
| {{coord|22|54|30|S|43|14|37|W}}
| 里奥（Rio） - S & W<!-- Rio - S & W -->
|-
| <code><nowiki>{{coord|22|S|43|W}}</nowiki></code>
| {{coord|22|S|43|W}}
| 一处[[经纬汇合工程|经纬汇合]]<!-- A [[Degree Confluence Project|degree confluence]] -->
|-
| <code><nowiki>{{coord|52|28|59|N|1|53|37|W|&#8203;display=inline,title|region:GB_type:city}}</nowiki></code>
| {{coord|52|28|59|N|1|53|37|W|display=inline,title|region:GB_type:city}}
| 伯明翰(英国) - 带显示及参数设定；注意在本页的标题处也会显示<!-- （英文模板目前已实现） --><!-- Birmingham - with display and parameter settings; note display also in title of this page. -->
|}

== 坐标参数 ==
跟随地理坐标之后，更多参数可能选择性地提供，它们由下划线分隔。这会帮助找到适当的地图资源，当[[meta:Category:Wikimaps|Wikimaps]]变得完全泛函化（become fully functional）时这一点也会变得更加重要。
<!-- 
Following the geographical coordinate, further parameters can optionally be supplied, separated by underscores. This will help in finding suitable map resources, and will become more important when the [//meta.wikimedia.org/wiki/Category:Wikimaps Wikimaps] become fully functional.
-->
===== type:''T'' =====
设定这个位置的类型，它将用于小数点的反向映射（the reverse mapping of the points）。类型也将设定缺省地图比例。如果缺省地图比例不适当，可考虑添加一个''[[#scale:N|scale:N]]''参数。类型有：
<!-- 
Sets the type of this location, which will be used for the reverse mapping of the points. Type will also set default map scale. If the default map scale is not appropriate, consider adding a ''[[#scale:N|scale:N]]'' parameter. Types are:
-->

{| align="center" class="wikitable"
! 类型（Type）
! 描述（Description）
! 比例尺（Scale）
|-
| '''country'''
| (例如<!-- e.g. --> "type:country")
|align="right" | 1:10,000,000
|-
| '''satellite'''
| 地球同步卫星<!-- geo-stationary satellites -->
|align="right" | (1:10,000,000)
|-
| '''adm1st''' 
| 国家行政区划，第一级（省、州），参见<!-- Administrative unit of country, 1st level (province, state), see  -->[[:en:Table of administrative_country_subdivisions_by_country#Table|table]]，例如[[美国州份]]<!-- , e.g. [[U.S. state]]s -->
|align="right" | 1:1,000,000
|-
| '''adm2nd'''
| 国家行政区划，第二级，参见<!-- Administrative unit of country, 2nd level, see  -->[[:en:Table of administrative_country_subdivisions_by_country#Table|table]]，例如[[县 (美国)]]<!-- , e.g. [[County (United States)]] -->
|align="right" | 1:300,000
|-
| '''city('''''pop''''')'''
| 市、镇或村，带指定的人口。''pop''中的逗号会受到忽略。不能有空白。<!-- City, town or village with specified population. Commas will be ignored in ''pop''. There should be no blanks. -->
|align="right" | 1:30,000 ... 1:300,000
|-
| '''city'''
| 市、镇或村，未特别指定人口。会被当作一个较小的城市。<!-- City, town or village, unspecified population. Will be treated as a minor city. -->
|align="right" | 1:100,000
|-
| '''airport'''
| 机场
|align="right" | 1:30,000
|-
| '''mountain'''
| 山峰、山脉<!-- peaks, mountain ranges -->
|align="right" | 1:100,000
|-
| '''isle'''
| 岛、岛屿<!-- Isles, islands -->
|align="right" | 1:100,000
|-
| '''waterbody'''
| 湾、海湾、湖、水库、池塘、港湾、瀉湖、河口湾、内海……<!-- Bays, fjords, lakes, reservoirs, ponds, lochs, loughs, meres, lagoons, estuaries, inland seas... -->
|align="right" | 1:100,000
|-
| '''forest'''
| 森林、林地<!-- Forests and woodlands -->
|align="right" | 1:50,000
|-
| '''river'''
| 江河、运河<!-- Rivers and canals -->
|align="right" | 1:100,000
|-
| '''glacier'''
| 冰川、冰冠<!-- Glaciers, ice caps -->
|align="right" | 1:50,000
|-
| '''edu'''
| 学校、学院、大学<!-- Schools, colleges, universities -->
|align="right" | 1:10,000
|-
| '''pass'''
| 山口<!-- mountain passes -->
|align="right" | 1:10,000
|-
| '''railwaystation'''
| 轨道、列车、铁路、地铁、高速交通、遂道、高架铁道，等等<!-- stations and stops of railway, train, railroad, metro, rapid transit, underground, subway, elevated railway, etc. --> 
|align="right" | 1:10,000
|-
| '''landmark'''
| 文化地标、特别有趣的建筑、游览胜地及其他有趣的地点<!-- Cultural landmark, building of special interest, tourist attraction and other points of interest. -->
|align="right" | 1:10,000
|-
| 
| ''缺省比例尺：如果没有使用type参数，或者此type在geohack扩展中未定义。''<!-- ''Default scale: if no type is used or the type is not defined in the geohack extension'' -->
|align="right" | 1:300,000
|}

圆括号中的比例尺在geohack扩展中尚未定义。type:state已从列表中撤出。
<!-- 
Scales in parentheses aren't defined yet in the geohack extension. type:state was withdrawn from the list.
-->

示例：
* <code><nowiki>{{coord|46|43|N|7|58|E|type:mountain}}</nowiki></code> 给出 {{coord|46|43|N|7|58|E|type:mountain}}

===== scale:''N'' =====
设定想要的地图[[比例尺]]为1:''N''。这会覆盖由[[#type:T|type:''T'']]参数确定的比例尺。若未定义type和scale参数，则使用扩展中的缺省的比例尺（1:300,000）。
''scale:''为可选参数。
<!-- 
Sets the desired map [[scale (map)|scale]] as 1:''N''. This will override the scale determined by the [[#type:T|type:''T'']] parameter. If no type and scale parameters are defined, the default scale of the extension will be used (1:300,000).

The ''scale:'' parameter can be omitted.
-->

{| class="wikitable"
|+ 示例<!-- Samples -->
!align=right| 比例尺<!-- Scale -->
! 标记<!-- Markup -->
! 结果<!-- Result -->
|-
|align=right|1:1000
|<nowiki>{{coord|51.500611|N|0.124611|W|scale:1000}}</nowiki> 
|{{coord|51.500611|N|0.124611|W|scale:1000}}
|-
|align=right|1:10,000
|<nowiki>{{coord|51.500611|N|0.124611|W|scale:10000}}</nowiki> 
|{{coord|51.500611|N|0.124611|W|scale:10000}}
|-
|align=right|1:100,000
|<nowiki>{{coord|51.500611|N|0.124611|W|scale:100000}}</nowiki> 
|{{coord|51.500611|N|0.124611|W|scale:100000}}
|-
|align=right|1:1,000,000
|<nowiki>{{coord|51.500611|N|0.124611|W|scale:1000000}}</nowiki> 
|{{coord|51.500611|N|0.124611|W|scale:1000000}}
|}

若前往地图站点的链接在{{tl|GeoTemplate}}中正确配置，并且某个地图在该比例尺下是可用的，则一个对应的地图可能显示出来。
<!-- 
If the links to the map sites are correctly configured on [[Template:GeoTemplate|GeoTemplate]] and a map is available for the scale, a corresponding map may be displayed.
-->

===== region:''R'' =====
设置首选的地图区域覆盖范围，用于为该地区选择适当的地图资源。若未提供region参数，geohack扩展会尝试从坐标值来确定它。

区域应当以下列形式给出：一个双字符的[[ISO 3166-1]]国家代码，或者一个[[ISO 3166-2]]区域代码。例如：
<!-- 
Sets the preferred map region of coverage, used in selecting appropriate map resources for the area. If no region parameter is supplied, the geohack extension attempts to determine it from the coordinates.

The region should be supplied as either a two character [[ISO 3166-1 alpha-2]] country code, or an [[ISO 3166-2]] region code. E.g:
-->

<table><tr><td>
* '''US''' [[美国]]
* '''US-NY''' 美国纽约
* '''CA''' [[加拿大]]
* '''DE''' [[德国]]
* '''DE-TH''' 德国[[图林根]]
* '''CH''' [[瑞士]]
* '''FR''' [[法国]]
* '''CN''' [[ISO_3166-2:CN|中国]]
</td><td>
* '''GB''' [[英国]]
* '''IN''' [[印度]]
* '''BR''' [[巴西]]
* '''AU''' [[澳大利亚]]
* '''NO-03''' [[挪威]][[奥斯陆]]
* '''NL''' [[荷兰]]
* '''LK''' [[斯里蘭卡]]
* '''TW-TPE''' [[台北市]]
</td></tr></table>

示例：
* <nowiki>{{coord|46.9524|N|7.4396|E|region:CH}}</nowiki> 聚焦于瑞士区域，在<!-- focuses the section for Switzerland at --> {{coord|46.9524|N|7.4396|E|region:CH}}。
* <nowiki>{{coord|52.5164|N|13.3775|E|region:DE-BB}}</nowiki> 聚焦于德国区域，在<!-- focuses the section for Germany at --> {{coord|52.5164|N|13.3775|E|region:DE-BB}}。

特种码：
* XZ用于国际海域之内/之上的对象（类似于[[:en:UN/LOCODE|UN/LOCODE]]）
* ZZ用于示例中
<!-- 
Specific code:
*XZ is used for objects in/above international waters (similar to [[UN/LOCODE]]).
*ZZ is used in samples
-->

===== globe:''G'' =====
指定除了[[地球]]（Earth）之外的其他[[行星]]，例如[[月球]]（Moon）、[[火星]]（Mars）、[[金星]]（Venus）、[[水星]]（Mercury）。

Geohack扩展的大部分特性对于其他星球来说不是很理想的。
<!-- 
Specifies other worlds than [[Earth]], such as ''[[Moon]]'', ''[[Mars]]'', ''[[Venus]]'', ''[[Mercury (planet)|Mercury]]''.

Most features of the geohack extension are not made for other globes.
-->

===== source:''S'' =====
指定（此处出现的）数据源和数据源格式/数据，并且可以选择性地在括号中显示原始数据。这最初主要是为地理标签机器人的应用而准备的，以便数据不被盲目地从格式到格式、从Wikipedia到Wikipedia重复拷贝，那会逐步丧失精度与归属性。

举例：
* 一个源于[[英國地形測量局]]（Ordnance Survey）[[英國國家格網參考系統]]（British national grid reference system）NM 435 355，其数据发现于英语维基百科，这样的经/纬地理标签应当标记为“source:enwiki-osgb36(NM435355)”。
* 一个源于取自德语维基百科的数据的经度-纬度位置，应当标记为“source:dewiki”。对于其他语言代码也类似。
* 一个源于公众领域[[:en:GEOnet Names Server|地理网络名称服务器]]数据库的位置应标记为“source:GNS”。数据或格式信息不是必需的，因为缺省情况下所有维基百科坐标都是以基于[[WGS84]]数据的经度/纬度格式存在。类似地，源于相似的公众领域[[:en:Geographic Names Information System|GNIS]]数据库的美国位置应当标记为“source:GNIS”。
<!-- 
Specifies, where present, the data source and data source format/datum, and optionally the original data, presented in parentheses. This is initially primarily intended for use by geotagging robots, so that data is not blindly repeatedly copied from format to format and Wikipedia to Wikipedia, with progressive loss of precision and attributability.

Examples:
* A lat/long geotag derived from a [[Ordnance Survey]] [[British national grid reference system|National Grid Reference]] NM 435 355 found in the English-language Wikipedia would be tagged as "source:enwiki-osgb36(NM435355)"
* A latitude-longitude location sourced from data taken from the German-language Wikipedia would be tagged as "source:dewiki" -- and so on, for other language codes;
* A location sourced from the public domain [[GEOnet Names Server|GeoNet Names Server]] database would be tagged as "source:GNS". No datum or format information is needed, since by default all Wikipedia coordinates are in latitude/longitude format based on the [[World Geodetic System|WGS84]] datum. Similarly, U.S. locations sourced from the similar public domain [[Geographic Names Information System|GNIS]] database would be tagged as "source:GNIS".
-->

== 显示 ==
缺省情况下坐标以那些指定的格式显示。

若要总是显示坐标为度分秒值，添加以下代码到[[Special:Mypage/common.css|你的common.css]]：
:<code>.geo-default { display: inline } .geo-nondefault { display: inline } <br />.geo-dec { display: none }   .geo-dms { display: inline }</code>

若要总是显示坐标为十进制值，添加以下代码到你的monobook.css：
:<code>.geo-default { display: inline } .geo-nondefault { display: inline }<br />.geo-dec { display: inline } .geo-dms { display: none }</code>

若要同时以两种格式显示坐标，添加以下代码到你的monobook.css：
:<code>.geo-default { display: inline } .geo-nondefault { display: inline }<br />.geo-dec { display: inline }   .geo-dms { display: inline }<br />.geo-multi-punct { display: inline }</code>

如果CSS遭到禁用，或者你有一个被缓存的旧版[[MediaWiki:Common.css]]，你将同时看到两种格式。（Common.css的缓存需要31天到期。你可以清空你的缓存，或者手动刷新这个URL：[//zh.wikipedia.org/w/index.php?title=MediaWiki:Common.css&usemsgcache=yes&action=raw&ctype=text/css&smaxage=2678400]。）

另见[[:en:Wikipedia:Manual of Style (dates and numbers)#Geographical coordinates]]。
<!-- 
==Display==

By default coordinates are displayed in the format in which they are specified.

To always display coordinates as DMS values, add this to [[Special:Mypage/monobook.css|your monobook.css]]:
:<code>.geo-default { display: inline } .geo-nondefault { display: inline } <br />.geo-dec { display: none }   .geo-dms { display: inline }</code>

To always display coordinates as decimal values, add this to [[Special:Mypage/monobook.css|your monobook.css]]:
:<code>.geo-default { display: inline } .geo-nondefault { display: inline }<br />.geo-dec { display: inline } .geo-dms { display: none }</code>

To display coordinates in both formats, add this to [[Special:Mypage/monobook.css|your monobook.css]]:
:<code>.geo-default { display: inline } .geo-nondefault { display: inline }<br />.geo-dec { display: inline }   .geo-dms { display: inline }<br />.geo-multi-punct { display: inline }</code>

If CSS is disabled, or you have an old copy of [[MediaWiki:Common.css]] cached, you will see both formats.  (The cache for Common.css takes 31 days to expire, and the changes were made 2007-04-04.  You can either clear your cache or manually refresh this URL: [//en.wikipedia.org/w/index.php?title=MediaWiki:Common.css&usemsgcache=yes&action=raw&ctype=text/css&smaxage=2678400].)

See also [[Wikipedia:Manual of Style (dates and numbers)#Geographical coordinates]].
-->
<!-- 
== Usage ==
 &#123;{coord|''latitude''|''longitude''|''parameters''|display=''display''}&#125;
 &#123;{coord|''dd''|''N/S''|''dd''|''E/W''|''parameters''|display=''display''}&#125;
 &#123;{coord|''dd''|''mm''|''N/S''|''dd''|''mm''|''E/W''|''parameters''|display=''display''}&#125;
 &#123;{coord|''dd''|''mm''|''ss''|''N/S''|''dd''|''mm''|''ss''|''E/W''|''parameters''|display=''display''}&#125;

* ''parameters'', which are optional, can be any ''type:'', ''region:'', or ''scale:'' setting which is recognised by the map server, such as the popular <code>type:city</code> and <code>type:landmark options</code>. See [[Wikipedia:WikiProject Geographical coordinates#Parameters]] for a comprehensive list.

* ''display'', which is optional, can be one of the following:
** <code>inline</code> (default): display the coordinate inline
** <code>title</code>: display the coordinate by the article title, right-justified (replaces {{tl|coor title dms}} family)
** <code>inline,title</code>: display both inline and at title (replaces {{tl|coor at dms}} family)

Note: using the <code>title</code> attribute indicates that the coordinates apply to the article, and not just one of (perhaps many) places mentioned in it &mdash; so it should only be omitted in the latter case. It will be used to add the article to services such as Google Earth layers.
 -->
<!-- 
== Examples ==
(These are live geo-microformats and should be detected on this page by parsers)
<table class="prettytable">
{{template example row|43.651234|-79.383333|notes=Toronto - Fully decimal - N & W }}
{{template example row|43.65|-79.38|notes=Toronto - less precise}}
{{template example row|43.6500|-79.3800|notes=Toronto - medium precision with trailing zeroes}}
{{template example row|43.651234|N|79.383333|W|notes=Toronto - decimal with Northing & Westing}}
{{template example row|43|29|N|79|23|W|notes=Toronto - degrees & minutes}}
{{template example row|43|29|4|N|79|23|0|W|notes=Toronto - degrees, minutes & seconds}}
{{template example row|43|29|4.5|N|79|23|0.5|W|notes=Toronto - degrees, minutes, seconds & fractions of seconds}}
{{template example row|55.752222|N|37.615556|E|notes=Moscow - N & E}}
<tr><td><code><nowiki>{{coord|55.752222|N|37.615556|E|format=dms}}</nowiki></code></td> <td>{{coord|55.752222|N|37.615556|E|format=dms}}</td> <td></td></tr>
<tr><td><code><nowiki>{{Coord|39.098095|-94.587307|format=dms}}</nowiki></code></td><td>{{Coord|39.098095|-94.587307|format=dms}} </td><td>Decimal conversion without N/S/E/W</td></tr>
<tr><td><code><nowiki>{{coord|55.752222|N|37.615556|E|format=dec}}</nowiki></code></td> <td>{{coord|55.752222|N|37.615556|E|format=dec}}</td> <td></td></tr>
{{template example row|33|55|S|18|25|E|notes=Capetown - S & E}}
{{template example row|22|54|30|S|43|14|37|W|notes=Rio - S & W}}
{{template example row|22|S|43|W|notes=A [[Degree Confluence Project|degree confluence]]}}
<tr><td><code><nowiki>{{coord|52|28|59|N|1|53|37|W
|display=inline,title|region:GB_type:city}}</nowiki></code></td> <td>{{coord|52|28|59|N|1|53|37|W|display=inline,title|region:GB_type:city}}</td> <td>Birmingham - with display and parameter settings; note display also in title of this page.</td></tr>
</table>
-->

== 错误使用维护 ==
本模板有几个内建的输入检查。基本的错误会显示{{tl|Coord/input/error2}}中的信息。参见[[:Category:需要修復的經緯模板引用]]查看需要修复的页面。

== 子模板 ==
参见[[:Category:經緯模板]]以及本模板的[[Template_talk:Coord|讨论页]]。

{|
! 名称<!-- name -->
! 功能<!-- function -->
|-
| [[Template:Coord/input/d|Coord/input/d]]
| 对以度格式输入的坐标进行转换<!-- converts coordinates from input in degrees format  --><nowiki>{{coord|12|N|12|W}}</nowiki>
|-
| [[Template:Coord/input/dm|Coord/input/dm]]
| 对以度/分格式输入的坐标进行转换<!-- converts coordinates from input in degrees/minutes format  --><nowiki>{{coord|12|12|N|12|12|W}}</nowiki>
|-
| [[Template:Coord/input/dms|Coord/input/dms]]
| 对以度/分/秒格式输入的坐标进行转换<!-- converts coordinates from input in degrees/minutes/seconds format  --><nowiki>{{coord|12|12|12|N|12|12|12|W}}</nowiki>
|-
| [[Template:Coord/display/inline|Coord/display/inline]]
| 创建以内联形式显示坐标的输出<!-- creates output to display coordinates inline -->
|-
| [[Template:Coord/display/title|Coord/display/title]]
| 创建在条目上方显示坐标的输出（通常在条目标题的右侧）<!-- creates output to display above the article (generally to the right of the article's title) -->
|-
| [[Template:Coord/display/inline,title|Coord/display/inline,title]]
| 创建以内联形式显示同时在条目上方显示坐标的输出<!-- （英文模板已实现） --><!-- creates output to display coordinates inline and above the article -->
|}

== 类名 ==
类名'''geo'''、'''latitude'''和'''longitude'''用来生成微格式，并且'''一定不要'''更改。

== 模板数据 ==
This template uses overloading which does not work well with the [[Wikipedia:TemplateData|VisualEditor/TemplateData]]. Consider using "Edit source" instead of the visual editor until this defect is corrected. To facilitate visual editing in the mean time, consider using {{tl|coordDec}} for signed decimal degrees, {{tl|coordDMS}} when degrees minutes and seconds are specified, and {{tl|coordDM}} when just degrees and minutes are given.

{{TemplateData header}}
<templatedata>{
	"description": "用于提供一个地点的经纬度坐标，提供该地点的地图链接。This template does not work well with the Visual Editor, consider using {{coordDec}} for signed decimal degrees, {{coordDMS}} when degrees minutes and seconds are specified {{coordDM}} when only degrees and minutes are specified. To use this template you will need to use positional parameter following one of these schemes: {{coord | D | M | S | NS | D | M | S | EW | geo | opts}}, {{coord | D | M | NS | D | M | EW | geo | opts}}, {{coord | D| NS | D| EW | geo | opts}} {{coord | sD | sD | geo | opts}} where D is degrees, M is minutes, S seconds, sD signed decimal degrees, NS is N or S, EW is E or W, opts are named parameter and geo are the coordinate parameters described on the main doc page.",
	"params": {
		"1": {
			"label": "1",
			"description": "Either degrees latitude or a signed decimal degrees latitude",
			"type": "number",
			"required": false,
			"suggested": true
		},
		"2": {
			"label": "2",
			"description": "Either: minutes latitude, signed decimal degrees longitude or 'N' or 'S'.",
			"type": "string",
			"required": false,
			"suggested": true
		},
		"3": {
			"label": "3",
			"description": "Either: second latitude, degrees longitude, 'N' or 'S' or GeoHack parameters",
			"type": "string",
			"required": false
		},
		"4": {
			"label": "4",
			"description": "Either: degrees longitude, 'N', 'S', 'E' or 'W' or GeoHack parameters",
			"type": "string",
			"required": false
		},
		"5": {
			"label": "5",
			"description": "Either: degrees longitude, minutes longitude or GeoHack parameters",
			"type": "string",
			"required": false
		},
		"6": {
			"label": "6",
			"description": "Either: minutes longitude, 'E' or 'W' or GeoHack parameters",
			"type": "string",
			"required": false
		},
		"7": {
			"label": "7",
			"description": "Either second longitude, or GeoHack parameters",
			"type": "string",
			"required": false
		},
		"8": {
			"label": "8",
			"description": "'E' or 'W'.",
			"type": "string",
			"required": false
		},
		"9": {
			"label": "9",
			"description": "GeoHack parameters. Example: dim:30_region:US-WI_type:event",
			"type": "string",
			"required": false
		},
		"qid": {
			"label": "维基数据项目",
			"description": "从WikiData项目而不是从该模板的参数中检索坐标",
			"type": "line",
			"required": false,
			"example": "Q513"
		},
		"display": {
			"label": "顯示方式",
			"description": "显示的位。可填写：'inline'，即在条目中；'title'，即在条目顶端；'inline,title'，两者兼有",
			"type": "line",
			"default": "inline",
			"suggested": true,
			"required": false
		},
		"name": {
			"label": "名稱",
			"description": "要放置在地图上的标签（默认为页面名）",
			"type": "string",
			"required": false
		},
		"notes": {
			"label": "注释",
			"description": "在坐标后面显示的文本",
			"type": "string",
			"required": false
		},
		"format": {
			"label": "格式",
			"description": "坐标格式，'dec'或'dms'",
			"type": "line",
			"required": false
		}
	},
	"format": "inline"
}</templatedata>

== 外部链接 ==
* [https://support.google.com/earth/answer/2395280?hl=zh-Hant 如何让我的维基百科条目出现在谷歌地球地理网络层？]——关于Google如何使用维基百科的坐标信息的FAQ
<!-- 
==Class names==
The class names '''geo''', '''latitude''' and '''longitude''' are used to generate the microformat and '''MUST NOT''' be changed.

==External links==
* [//earth.google.com/userguide/v4/geoweb_faq.html Google Earth Geographic Web Layer FAQ] &ndash; Information on how Google uses Wikipedia's coordinate information.
-->
{{Organization infoboxes|state=collapsed}}
<includeonly>{{Sandbox other||<!-- 本行下加入模板的分類 -->
[[Category:經緯模板|{{PAGENAME}}]]
<!--
[[Category:Protected templates|{{PAGENAME}}]]
[[Category:Templates generating Geo|{{PAGENAME}}]] 
-->
}}</includeonly>