<!--
G
 Unregistered users:
 If you wish to add a mapping service leave a message on the discussion/talk page
 preferably with instructions on how to format the URL for coordinates.

-->
<div class="toccolours plainlinks" style="font-size:92%;float:right;max-width:60em; ">
{{#ifexpr:{{CURRENTDAY}} mod 8=2 |<div style="background:lightyellow; color:black; border:1px solid #666; padding:0 0.5em; font-size:88%;">
[[File:Imbox notice.png|24px]]&emsp;你是否知道可以點選[[File:Erioll_world.svg|18px|alt=the blue globe|link=|]]開啟[[m:WikiMiniAtlas|WikiMiniAtlas]]而不用離開條目？
</div>|}}
<!-- Input -->
{| style="background:none; text-align:left; width:100%; border-collapse:collapse"
|- style="vertical-align:top;"
! [[WGS84]]
| colspan="3" | <span title="纬度">{latdegabs}°&nbsp;{latminint}′&nbsp;{latsecdec}″&nbsp;{latNS}</span>, <span title="经度">{londegabs}°&nbsp;{lonminint}′&nbsp;{lonsecdec}″&nbsp;{lonEW}</span><br /><span class="geo"><span class="latitude" title="纬度">{latdegdec}</span>, <span class="longitude" title="经度">{londegdec}</span></span>（[https://artoria2e5.github.io/PRCoords/demo?lat={latdegdec}&lon={londegdec} 转换]）
|rowspan="6"|<!-- minimap -->
<div style="position:relative; width:360px; height:180px;">
<div style="position:absolute;">[[File:Earthmap1000x500.jpg|360x180px|alt=|link=]]</div>
<div style="position:absolute; top:97px; left:176px;">
<div style="position:absolute; bottom:{latantipodes}px; left:{longantipodes}px;">[[File:Fairytale undo.png|14x14px|link=http://stable.toolserver.org/geohack/geohack.php?language=zh&pagename={pagename}&params={latantipodes}_N_{longantipodes}_E_scale:10000000_type:{type}&title=相对应于{title}的地方|改变链接到 {title}对应的地方({latantipodes}, {longantipodes})]]</div>
<div style="position:absolute; bottom:{latdegint}px; left:{londegint}px;" title="{title}">[[File:Locator_Dot.png|8x8px|alt=|link=]]</div>
</div>
</div>
|-
! [[通用横轴墨卡托坐标系|UTM]]
| colspan="3" | <span title="投影带">{utmzone}</span> <span title="东向">{utmeasting}</span> <span title="北向">{utmnorthing}</span>
|-
! style="width:3em;" | 放大
| {zoom}
! style="width:3em;" | 比例尺
| ± 1:{scale}
|-
! 地区
| [//zh.wikipedia.org/wiki/ISO_3166-2:{region} {region}]
! 類型
| {type}&nbsp;
|-
! 标题
| colspan="3" | [//zh.wikipedia.org/wiki/{pagename} {title}] <span class="noprint" style="display:none{pagename}">([//zh.wikipedia.org{{SCRIPTPATH}}/index.php?title={pagename}&action=edit 编辑] | [//zh.wikipedia.org{{SCRIPTPATH}}/index.php?title={{ns:1}}:{pagename}&action=edit&section=new&editintro=Template:Geodata-check/report_editintro&preloadtitle=Coordinate%20error&preload=Template:Geodata-check/preload 错误报告])</span>
|-
| colspan="4" style="padding:1em 0 0; width:100%;"| 
{| style="background:none; border-top:solid 1px #bbbbbb; width:100%;"
|- style="vertical-align:top;"
! 目录 __NOTOC__
| [[#全球系统|全球与本地系统]]&nbsp;'''•''' [[#维基百科条目|维基百科条目]]&nbsp;'''•''' [[#照片|照片]]&nbsp;'''•''' [[#其他信息|其他]]&nbsp;'''•''' [http://stable.toolserver.org/geohack/geohack.php?language=zh&pagename={pagename}&params={latdegabs}_{latminint}_{latsecdec}_{latNS}_{londegabs}_{lonminint}_{lonsecdec}_{lonEW}_region:{region}_scale:{scale}_type:{type}_globe:export&title={title} 导出]
|}
|}
</div>
<div class="plainlinks" style="text-align:center;">
<div style="min-width:192px; display:inline-block;"><big>流行选项：</big></div>
<br><div style="min-width:192px; display:inline-block;">
[//www.bing.com/maps/?v=2&cp={latdegdec}~{londegdec}&style=r&lvl={osmzoom}&sp=Point.{latdegdec}_{londegdec}_{titlee}___ <span style="display:inline-block; text-align:center; width:96px;">[[File:Bing favicon.svg|64x64px|link=|alt=]]<br>Bing Maps</span>][//maps.google.com/maps?ll={latdegdec},{londegdec}&q={latdegdec},{londegdec}&hl={language}&t=m&z={osmzoom} <span style="display:inline-block; text-align:center; width:96px;">[[File:Google "G" Logo.svg|64x64px|link=|alt=]]<br>Google Maps</span>]
</div><div style="min-width:192px; display:inline-block;">
[{{fullurl:toollabs:geocommons/earth.kml|latdegdec={latdegdec}&londegdec={londegdec}&scale={scale}&title={titlee}}} <span style="display:inline-block; text-align:center; width:96px;">[[File:Google Earth Icon.png|64x64px|link=|alt=]]<br/>Google Earth</span>]
[//www.openstreetmap.org/?mlat={latdegdec}&mlon={londegdec}&zoom={osmzoom}&layers=M <span style="display:inline-block; text-align:center; width:96px;">[[File:Openstreetmap logo.svg|64x64px|link=|alt=]]<br>OpenStreetMap</span>]
<br>以下列出更多地图来源。
</div></div>
{{-}}
<!-- services -->
{| cellpadding="0" cellspacing="0" style="background:none; border-collapse:collapse; table-layout:fixed; width:100%;" class="plainlinks"
|- style="vertical-align:top;"
| class="directory" style="width:50%;"| <div id="GEOTEMPLATE-GLOBAL">
==全球系統 ==
{|
! 服务商 !! 地圖 !! 衛星 !! 其他
|- style="background:#f5f5f5"
| ACME Mapper
| [http://mapper.acme.com/?ll={latdegdec},{londegdec}&z={osmzoom}&t=M&marker0={latdegdec},{londegdec},{title} 地图]
| [http://mapper.acme.com/?ll={latdegdec},{londegdec}&z={osmzoom}&t=H&marker0={latdegdec},{londegdec},{title} 卫星]
| [http://mapper.acme.com/?ll={latdegdec},{londegdec}&z={osmzoom}&t=R&marker0={latdegdec},{londegdec},{title} 地形],&nbsp;[http://mapper.acme.com/?ll={latdegdec},{londegdec}&z={osmzoom}&t=K&marker0={latdegdec},{londegdec},{title} Mapnik]
|-
| ArcWeb Explorer
| [http://www.arcwebservices.com/awx?c={londegdec}&#124;{latdegdec}&sf={scale}&sp={londegdec}&#124;{latdegdec}&sl=images%2Fgeocoded%5Ficon%2Epng&st={latdegdec},%20{londegdec}&w=fi&#124;10&#124;60 地图]
| [http://www.arcwebservices.com/awx/index.jsp?c={londegdec}&#124;{latdegdec}&sf={scale}&sp={londegdec}&#124;{latdegdec}&sl=images%2Fgeocoded%5Ficon%2Epng&st={latdegdec},%20{londegdec}&w=fi&#124;10&#124;60&ds=ArcWeb:GlobeXplorer.Deluxe_Tiles.World&#124;ArcWeb:TA.Streets_VectorsForHybrid.US&glt=rasterTileGroupLayer&#124;vectorGroupLayer 卫星]
| （需要Flash）
|- style="background:#cad;"
| Bing 地图<sup>流行</sup>
| [http://maps.bing.com/default.aspx?v=2&cp={latdegdec}~{londegdec}&style=r&lvl={osmzoom}&sp=Point.{latdegdec}_{londegdec}_{title}___ 地图]
| [http://maps.bing.com/default.aspx?v=2&cp={latdegdec}~{londegdec}&style=h&lvl={osmzoom}&sp=Point.{latdegdec}_{londegdec}_{title}___ 卫星]
| [http://maps.bing.com/default.aspx?v=2&cp={latdegdec}~{londegdec}&style=o&lvl={osmzoom}&sp=Point.{latdegdec}_{londegdec}_{title}___ 鸟瞰]
|- style="background:#f5f5f5"
| Ayna
| [http://maps.ayna.com/?lang=en&lon={londegdec}&lat={latdegdec}&zoom={osmzoom}&layer=m&marker=1&title={title} 地图]
| [http://maps.ayna.com/?lang=en&lon={londegdec}&lat={latdegdec}&zoom={osmzoom}&layer=s&marker=1&title={title} 卫星]
|
|-
| Blue Marble Navigator
|
| [http://www.blue-marble.de?lon={londegdec}&nlat={latdegdec}&borders&geonames&townnames&zoom&overlay=7&base=14 卫星]
|
|- style="background:#f5f5f5"
| ExploreOurPla.net
|
| [http://exploreourpla.net/explorer/?geoLink=1444&lon={londegdec}&lat={latdegdec}&alt=262144 每天]
|
|-
| Flash Earth
|
| [http://www.flashearth.com/?lat={latdegdec}&lon={londegdec}&z=15&r=0&src=ggl 卫星]
|
|- style="background:#f5f5f5"
| Fourmilab
|
| [http://www.fourmilab.ch/cgi-bin/uncgi/Earth?imgsize=320&opt=-l&lat={latdegdec}&ns=North&lon={londegneg}&ew=West&alt={altitude}&img=nasa.evif 卫星]
|
|-
| GeaBios
|
|[http://www.geabios.com/html/services/maps/PublicMap.htm?lat={latdegdec}&lon={londegdec}&fov={span}&title={title} 卫星]
|
|- style="background:#f5f5f5"
| GeoNames
|
| [http://www.geonames.org/maps/google_{latdegdec}_{londegdec}.html 卫星]
|
|-
| GlobeXplorer
|
| [http://imageatlas.globexplorer.com/ImageAtlas/view.do?group=ImageAtlas&lat={latdegdec}&lon={londegdec}&zoom_level=10 卫星]
|
|- style="background:#f5f5f5"
| Google地球<!-- :en:Template_talk:GeoTemplate/FAQ#Google -->
| [{{fullurl:toollabs:wp-world/earth.php|long={londegdec}&lat={latdegdec}&name={pagenamee}}} 打开]
|
| [{{fullurl:tools:~para/earth.php|latdegdec={latdegdec}&londegdec={londegdec}&scale={scale}&title={title}}} 用 Toolserver 生成精确地标（UTF-8）]
|- style="background:#cad;"
| Google地图<sup>流行</sup>
|[//maps.google.com/maps?ll={latdegdec},{londegdec}&spn={span},{span}&t=m&q={latdegdec},{londegdec} 地图]（[//maps.google.com/maps?q=http%3A//toolserver.org/~para/cgi-bin/kmlexport?project=zh%26article%3D{pagename} 定位]）
| [//maps.google.com/maps?ll={latdegdec},{londegdec}&spn={span},{span}&t=h&q={latdegdec},{londegdec} 卫星]
| [//maps.google.com/maps?ll={latdegdec},{londegdec}&spn={span},{span}&t=p&q={latdegdec},{londegdec} 地形]
|- style="background:#f5f5f5"
| GPS探测仪
| [http://www.gpsvisualizer.com/map_input?special=wikipedia&format=google&bg_map=google_map&sp_width=50km&google_zoom_level={zoom}&form:data=type,name,latitude,longitude%0DW,%22{title}%22,{latdegdec},{londegdec} 地图]
| [http://www.gpsvisualizer.com/map_input?special=wikipedia&format=google&bg_map=google_hybrid&sp_width=50km&google_zoom_level={zoom}&form:data=type,name,latitude,longitude%0DW,%22{title}%22,{latdegdec},{londegdec} 卫星]
| [http://www.gpsvisualizer.com/map_input?special=wikipedia&format=google&bg_map=google_physical&sp_width=50km&google_zoom_level={zoom}&form:data=type,name,latitude,longitude%0DW,%22{title}%22,{latdegdec},{londegdec} 地形]
|-
! scope="row" style="font-weight:normal; text-align:left;" | HERE（诺基亚地图）
| [http://here.com/{latdegdec},{londegdec},{osmzoom},0,0,normal.day 地图]
| [http://here.com/{latdegdec},{londegdec},{osmzoom},0,0,hybrid.day 卫星]
| [http://here.com/{latdegdec},{londegdec},{osmzoom},0,0,terrain.day 地形]、[http://here.com/{latdegdec},{londegdec},{osmzoom},0,60,3d.day 3D地图 (WebGL)]
|-
| Map24
| [http://link2.map24.com/?lid=879d2d1e&maptype=JAVA&wxdd0={londegdec}&wydd0={latdegdec}&name0=Location+display&description0={latdegdec}+N+{londegdec}+E&logo_url0=http://documents.map24.com/wiki.gif&url0=http://www.wikipedia.org 地图]
|
|
|- style="background:#f5f5f5"
| MapQuest
| [http://atlas.mapquest.com/maps/map.adp?searchtype=address&formtype=address&latlongtype=degrees&latdeg={latdegint}&latmin={latminint}&latsec={latsecint}&longdeg={londegint}&longmin={lonminint}&longsec={lonsecint}&zoom={zoom}&title={title} 地图]
|
|
|-
| MapTech
| [http://mapserver.maptech.com/homepage/index.cfm?lat={latdegdec}&lon={londegdec}&scale=24000&zoom=50&type=1 地图]
|
|
|- style="background:#f5f5f5"
| MSN maps
| [http://maps.msn.com/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=2 地图]
|
|
|-
| MultiMap
| [http://www.multimap.com/maps/?lat={latdegdec}&lon={londegdec}&zoom={osmzoom} 地图]
|
|
|- style="background:#f5f5f5"
| NASA World Wind
|
| [worldwind://goto/world=Earth&lat={latdegdec}&lon={londegdec}&view={span} 打开]
|
|-
| NaviTraveler
| [http://www.navitraveler.com/search.php?latlng={latdegdec},{londegdec} 地图]
|
|
|- style="background:#f5f5f5"
| Norkart Virtual Globe
|
| [http://www.virtual-globe.info/VirtualGlobeStarter.php?request=page&dataset=http://www.virtual-globe.info/globe.vgml&lookat={londegdec},{latdegdec},{scale} 卫星]
|
|- style="background:#cad;"
| OpenStreetMap<sup>开放内容</sup>
| [http://www.openstreetmap.org/index.html?mlat={latdegdec}&mlon={londegdec}&zoom={osmzoom}&layers=M 地图]
|
| [http://stable.toolserver.org/geohack/geohack.php?project=osm&pagename={title}&language=zh&params={params} 更多地图]
|- style="background:#f5f5f5"
| Shaded Relief
| [http://www.shaded-relief.com/?gt={latdegdec}&gl={londegdec}&z=9&t=4 地图]
|
|
|-
| TerraServer
|
| [http://www.terraserver.com/view.asp?cx={londegdec}&cy={latdegdec}&proj=4326&mpp=2.5&pic=img 卫星]
|
|- style="background:#f5f5f5"
| USMapServer
| [http://usmapserver.com/WikipediaMap.php?lat={latdegdec}&lon={londegdec}&scale={scale} 地图]
|
|
|-
| ViaMichelin International
| [http://www.viamichelin.com/viamichelin/int/search/Cartes/{londegdec}*{latdegdec}?zoomLevel=9 地图]
|
|
|- style="background:#f5f5f5"
| WikiMapia
| [http://www.wikimapia.org/#lat={latdegdec}&lon={londegdec}&spnx={span}&spny={span}&m=w 地图]
| [http://www.wikimapia.org/#lat={latdegdec}&lon={londegdec}&spnx={span}&spny={span}&m=b 卫星]
| [http://www.wikimapia.org/#lat={latdegdec}&lon={londegdec}&spnx={span}&spny={span}&m=b&v=8 + 老地点]
|-
| WikiMiniAtlas
|  [http://stable.toolserver.org/wma/iframe.html?{latdegdec}_{londegdec}_800_600_en_{zoom}_zh 地图]
|
| 
|- style="background:#f5f5f5"
| Yahoo! Maps
| [http://maps.yahoo.com/broadband/#mvt=m&lat={latdegdec}&lon={londegdec}&mag=6&q1={latdegdec},{londegdec} 地图]
| [http://maps.yahoo.com/broadband/#mvt=h&lat={latdegdec}&lon={londegdec}&mag=6 卫星]
| （需要Flash）
|}
</div>
| class="directory" style="width:50%; vertical-align:top;"| <div id="GEOTEMPLATE-LOCAL">

== 维基媒体地图 ==
<!-- [[MediaWiki:GeoHack.js]] -->
<div class="center">
<div class="thumb tnone">
<div class="thumbinner">
<div id="osmEmbed" class="OSM:{latdegdec}_{londegdec}_{osmzoom}_mapnik" style="background:#aaa; width:100%; height:500px; height:80vh;">未启用JavaScript</div>
</div>
</div>
</div>
</div><!--/GEOTEMPLATE-LOCAL-->

<center>'''[http://stable.toolserver.org/geohack/geohack.php?language=zh&pagename={pagename}&params={latdegabs}_{latminint}_{latsecdec}_{latNS}_{londegabs}_{lonminint}_{lonsecdec}_{lonEW}_region:_scale:{scale}_type:{type}#regional 查看其他所有地区系统]'''</center>
|}

==维基百科条目==
<div class="directory">
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 说明
! 链接
! 服务商
! 更新时间
|-
| 指定经度/纬度的条目
<!-- for [[Category talk:Lines of latitude#Redirects]], [[Category talk:Lines of longitude#Redirects]] -->
| [http://en.wikipedia.org/wiki/Latitude_{latdegabs}_degrees_{latNS} Latitude {latdegabs}° {latNS}] and [http://en.wikipedia.org/wiki/Longitude_{londegabs}_degrees_{lonEW} Longitude {londegabs}° {lonEW}]
| —
| —
|- style="background:#f5f5f5"
| style="overflow:hidden;"| <span style="text-decoration: underline;">{pagename}</span>的精确定位
| [//maps.google.com/maps?q=http%3A//toolserver.org/~para/cgi-bin/kmlexport?project={{CONTENTLANG}}%26article%3D{pagename} Google地图], [http://maps.live.com/?mapurl=http%3A//toolserver.org/~para/cgi-bin/kmlexport?project={{CONTENTLANG}}%26article%3D{pagename} Live Search Maps]
| Para
| 几乎实时
|- style="white-space:nowrap;"
| 图层
| [http://stable.toolserver.org/wma/iframe.html?{latdegdec}_{londegdec}_800_600_en_{zoom}_zh WikiMiniAtlas]
| Dschwen
| 每周1-2次(自2009年3月开始)
|- style="background:#f5f5f5"
| 图层
| [//maps.google.com/maps?ll={latdegdec},{londegdec}&spn={span},{span}&t=m&q={latdegdec},{londegdec}&lci=org.wikipedia.zh Google地图]
| Google
| 2008年07月(自2009年02月开始)
|-
| 图层
| [http://www.geonames.org/maps/wikipedia_{latdegdec}_{londegdec}.html Google地图]
| Geonames
| 2007年12月(自2009年02月开始)
|- style="background:#f5f5f5"
| 图层
| [//maps.google.com/maps?ll={latdegdec},{londegdec}&spn={span},{span}&q=http:%2F%2Ftoolserver.org%2F~kolossos%2Fgeoworld%2FWP-world-maps.php%3Flang%3Dzh Google地图], [{{fullurl:tools:~kolossos/osm/wp-on-osm.php|lat={latdegdec}&lon={londegdec}&zoom={osmzoom}&lang={{CONTENTLANG}}}} Openstreetmap]
| Wikipedia-World
| 2009年05月(自2009年05月开始)
|-
| 图层
| [{{fullurl:tools:~kolossos/wp-world/umkreis.php|la=zh&lon={londegdec}&lat={latdegdec}&rang=50&map=1}} label overlay]
| Wikipedia-World
| 2008年05月(自2009年02月开始)
|- style="background:#f5f5f5"
| 图层
| [http://maps.live.com/default.aspx?v=2&cp={latdegdec}~{londegdec}&style=r&lvl={osmzoom}&explore=sst.0~tag.Wikipedia&sp=Point.{latdegdec}_{londegdec}_{title}___ Live Search Maps]
| Virtual Earth
| 2008年02月(自2009年02月开始)
|-
| 图层
| [http://www.multimap.com/maps/?zoom=14&lat={latdegdec}&lon={londegdec}&p=mm.poi.global.general.wikipedia Multimap]
| Multimap
| 2008年07月(自2009年02月开始)
|- style="background:#f5f5f5"
| 坐标表格
| [{{fullurl:tools:~kolossos/wp-world/umkreis.php|la=zh&submit=Table&lon={londegdec}&lat={latdegdec}&rang=5&map=0&limit=75}} 5,] [{{fullurl:tools:~kolossos/wp-world/umkreis.php|la=zh&submit=Table&lon={londegdec}&lat={latdegdec}&rang=10&map=0&limit=75}} 10,] [{{fullurl:tools:~kolossos/wp-world/umkreis.php|la=zh&submit=Table&lon={londegdec}&lat={latdegdec}&rang=20&map=0&limit=250}} 20,] [{{fullurl:tools:~kolossos/wp-world/umkreis.php|la=zh&submit=Table&lon={londegdec}&lat={latdegdec}&rang=50&map=0&limit=400}} 50,] [{{fullurl:tools:~kolossos/wp-world/umkreis.php|la=zh&submit=Table&lon={londegdec}&lat={latdegdec}&rang=100&map=0&limit=500}} 100,] or [{{fullurl:tools:~kolossos/wp-world/umkreis.php|la=zh&submit=Table&lon={londegdec}&lat={latdegdec}&rang=250&map=0&limit=500}} 250] km away
| Wikipedia-World
| 2008年05月(自2009年02月开始)
|-
| 坐标表格
| [{{fullurl:tools:~dispenser/cgi-bin/locateCoord.py|dbname=coord_zhwiki&lon={londegdec}&lat={latdegdec}&range_km=5}} 5,] [{{fullurl:tools:~dispenser/cgi-bin/locateCoord.py|dbname=coord_zhwiki&lon={londegdec}&lat={latdegdec}&range_km=10}} 10,] [{{fullurl:tools:~dispenser/cgi-bin/locateCoord.py|dbname=coord_zhwiki&lon={londegdec}&lat={latdegdec}&range_km=20}} 20,] [{{fullurl:tools:~dispenser/cgi-bin/locateCoord.py|dbname=coord_zhwiki&lon={londegdec}&lat={latdegdec}&range_km=50}} 50,] [{{fullurl:tools:~dispenser/cgi-bin/locateCoord.py|dbname=coord_zhwiki&lon={londegdec}&lat={latdegdec}&range_km=100}} 100,] or [{{fullurl:tools:~dispenser/cgi-bin/locateCoord.py|dbname=coord_zhwiki&lon={londegdec}&lat={latdegdec}&range_km=250}} 250] km away
| Dispenser
| 每天07:00 UTC
|- style="background:#f5f5f5"
| 坐标表格
| [http://www.geonames.org/maps/wikipedia_{latdegdec}_{londegdec}.html Geonames]
| Geonames
| 2007年12月(自2009年02月开始)
|}
</div>

==照片==
<div class="directory">
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商
! 
|-style="background:#f5f5f5"
| [//maps.google.com/maps?ll={latdegdec},{londegdec}&spn={span},{span}&q=http://toolserver.org/~para/GeoCommons/GeoCommons-simple.kml 共享资源]
| [http://toolserver.org/~para/GeoCommons/proximityrama?latlon={latdegdec},{londegdec} Proximityrama]
|-
| [http://www.flickr.com/map/?fLat={latdegdec}&fLon={londegdec}&zl=5 Flickr地图]
| [http://www.flickr.com/nearby/{latdegdec},{londegdec} Flickr '附近']
|-style="background:#f5f5f5"
| [http://loc.alize.us/#/geo:{latdegdec},{londegdec},14,m/sort:date/ Loc.alize.us]
|
|-
| [http://www.panoramio.com/map/#lt={latdegdec}&ln={londegdec}&z=0&k=0&a=1&tab=2 Panoramio]
|
|-style="background:#f5f5f5"
| [http://www.planeteye.com/maps?refcon=wikipedia&pll={latdegdec},{londegdec}&z={osmzoom}&title={title}&type={type}&scale={scale}&region={region}&sd=photos PlanetEye]
|
|-
| [http://virtualglobetrotting.com/ll/{latdegdec},{londegdec} VirtualGlobetrotting]
|
|-style="background:#f5f5f5"
| [http://whereto.org/search?q={latdegdec},{londegdec}/{span} WhereTo.org]
|
|}
</div>

==其他信息==

<div class="directory">
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 说明
|- style="background:#f5f5f5"
| Geocaching.com
| [//www.geocaching.com/seek/nearest.aspx?origin_lat={latdegdec}&origin_long={londegdec}&dist=20&submit3=Search 地点附近]
|-
| GlobalGuide.org
| [//www.globalguide.org/index.html?lat={latdegdec}&long={londegdec}&zoom=17&title={title} 查看土地使用]
|- style="background:#f5f5f5"
| NASA Weather
| [http://wwwghcc.msfc.nasa.gov/cgi-bin/get-goes?satellite=Global%20Composite&lat={latdegdec}&lon={londegdec}&zoom=1&info=ir&palette=spect.pal&width=600&height=500 天氣衛星影像]
|-
| ExploreOurPla.net
| [http://ExploreOurPla.net/explorer/?geoLink=1444&lat={latdegdec}&lon={londegdec}&alt=262144&nbl=666736,12,10 NASA + METAR (機場)提供的天氣資訊]
|- style="background:#f5f5f5"
| Megalithic Portal
| [http://www.megalithic.co.uk/article.php?long={londegdec}&lat={latdegdec} 附近的史前遺址]
|-
| World Time Engine
| [http://worldtimeengine.com/dotime/{latdegdec},{londegdec}/ 時區]
|- style="background:#f5f5f5"
| Ex :: Natura
| [http://sun.exnatura.org/?longitude={londegdec}&latitude={latdegdec}&resulting=1 日出與日落]
|-
| www.sunrisesunset.com
| [http://www.sunrisesunset.com/calendar.asp?comb_city_info=Long:{londegneg},Lat:{latdegdec};{londegneg};{latdegdec};0;0&month={{CURRENTMONTH}}&year={{CURRENTYEAR}}&time_type=1&use_dst=0&want_twi_civ=1&want_twi_naut=1&want_twi_astro=1&want_mrms=1&want_mphase=1 日出、日落、薄暮、與月出月落]
|- style="background:#f5f5f5"
| Geody
| [http://www.geody.com/geolook.php?world=terra&lat={latdegdec}&lon={londegdec} 資訊]
|-
| Heavens-Above.Com
| [http://www.heavens-above.com/?Loc=Newark&Lat={latdegdec}&Lng={londegdec}&Alt={altitude} 衛星/行星觀測資訊]
|- style="background:#f5f5f5"
| Echolink
| [http://www.echolink.org/links.jsp?sel=latlon&lat_deg={latdegabs}&lat_min={latmindec}&lat_NS={latNS}&lon_deg={londegabs}&lon_min={lonmindec}&lon_EW={lonEW} 可供業餘線上廣播(Radio over IP)網路的當地最靠近的網關]
|-
| Findu.com
| [http://www.findu.com/cgi-bin/near.cgi?lat={latdegdec}&lon={londegdec} 自動封包報導系統(APRS)站台]
|- style="background:#f5f5f5"
| ham.darc.de/echolink
| [http://www.darc.de/echolink-bin/relais.pl?latdegdec={latdegdec}&londegdec={londegdec}&sel=latlondec 於DL3EL資料庫中於該區的中繼器列表]
|-
| Degree Confluence Project
| [http://www.confluence.org/confluence.php?lat={latdeground}&lon={londeground} 資訊]
|- style="background:#f5f5f5"
| OpenPisteMap
| [http://openpistemap.org/?lat={latdegdec}&lon={londegdec}&zoom={osmzoom} 滑雪斜坡]
|-
| Great Circle Mapper
| [http://gc.kls2.com/cgi-bin/gclookup?Q={latdegdecabs}{latNS}++{londegdecabs}{lonEW} 附近機場]
|}
</div>

<!--
==間接==
* [http://plasma.nationalgeographic.com/mapmachine/search.html National Geographic] Diverse maps, including historic maps.
* [http://www.maporama.com/ Maporama] Road maps and driving directions.
* [http://www.m-w.com/maps/moremapsnyt.html Merriam Webster's Atlas]
-->

</div>
<!-- Begin region specific -->
<div id="GEOTEMPLATE-REGIONS" class="directory">

{| id="regional" class="toc plainlinks" summary="其他地区"
! 地区系统:
|
[[#非洲|非洲]]&nbsp;'''•'''
[[#亚洲|亚洲]]&nbsp;'''•'''
[[#大洋洲|大洋洲]]&nbsp;'''•'''
[[#欧洲 A-M|欧洲 (A–M)]]&nbsp;'''•'''
[[#欧洲 N-Z|欧洲 (N–Z)]]&nbsp;'''•'''
[[#北美洲|北美洲]]&nbsp;'''•'''
[[#南美洲|南美洲]]
|}

=北美洲=
<div id="GEOTEMPLATE-CA">
==加拿大==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星 !! 其他
|- style="background:#f5f5f5"
| GPS Visualizer
|
|
| [http://www.gpsvisualizer.com/map_input?special=wikipedia&format=google&bg_map=google_mytopo&sp_width=50km&form:data=type,name,latitude,longitude%0DW,%22{title}%22,{latdegdec},{londegdec} 地形图]
|-
| National Atlas of Canada
|
|
| [http://toolserver.org/~para/EPSG4326to42304.php?lat={latdegdec}&lon={londegdec} 地形图]
|- style="background:#f5f5f5"
| Sympatico / MSN Maps
| [http://en.maps.sympatico.msn.ca/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=0 地圖]
|
|
|-
| TopoQuest
|
|
| [http://www.topoquest.com/map.php?lat={latdegdec}&lon={londegdec}&datum=nad83&zoom=8&map=50k 地形图]
|}
</div>

<div id="GEOTEMPLATE-US">
==美国==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星 !! 其他
|- style="background:#f5f5f5"
| ACME
|
|
| [http://mapper.acme.com/?ll={latdegdec},{londegdec}&z={osmzoom}&t=T&marker0={latdegdec},{londegdec},{title} 地形图] [http://mapper.acme.com/?ll={latdegdec},{londegdec}&z={osmzoom}&t=N&marker0={latdegdec},{londegdec},{title} NEXRAD] [http://mapper.acme.com/?ll={latdegdec},{londegdec}&z={osmzoom}&t=O&marker0={latdegdec},{londegdec},{title} DOQ]
|-
| GPS Visualizer
|
| [http://www.gpsvisualizer.com/map_input?special=wikipedia&format=google&bg_map=usgs_aerial&sp_width=50km&form:data=type,name,latitude,longitude%0DW,%22{title}%22,{latdegdec},{londegdec} USGS 空照圖]
| [http://www.gpsvisualizer.com/map_input?special=wikipedia&format=google&bg_map=google_mytopo&sp_width=50km&form:data=type,name,latitude,longitude%0DW,%22{title}%22,{latdegdec},{londegdec} USGS 地形图]
|- style="background:#f5f5f5"
| MapQuest
| [http://atlas.mapquest.com/maps/map.adp?searchtype=address&formtype=address&latlongtype=degrees&latdeg={latdegint}&latmin={latminint}&latsec={latsecint}&longdeg={londegint}&longmin={lonminint}&longsec={lonsecint}&zoom={zoom}&title={title} 地圖]
| [http://atlas.mapquest.com/maps/map.adp?searchtype=address&formtype=address&latlongtype=degrees&latdeg={latdegint}&latmin={latminint}&latsec={latsecint}&longdeg={londegint}&longmin={lonminint}&longsec={lonsecint}&zoom={zoom}&dtype=h&title={title} 已標記的衛星圖]
|
|-
| MSN Maps USA
| [http://maps.msn.com/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=0&redirect=false 地圖]
|
|
|- style="background:#f5f5f5"
| NASA/MSFC GOES
|
| [http://wwwghcc.msfc.nasa.gov/cgi-bin/get-goes?satellite=GOES-E%20CONUS&lat={latdegdec}&lon={londegdec}&zoom=1&info=ir&palette=spect.pal&width=600&height=500 衛星圖]
|
|-
| 美国国家气象局
|
|
| [http://forecast.weather.gov/MapClick.php?textField1={latdegdec}&textField2={londegdec} 天氣]
|- style="background:#f5f5f5"
| TerraServer-USA
|
| [http://terraserver.microsoft.com/map.aspx?t=1&s=12&lon={londegdec}&lat={latdegdec}&w=600&h=400 空照圖]
| [http://terraserver.microsoft.com/map.aspx?t=2&s=12&lon={londegdec}&lat={latdegdec}&w=600&h=400 地形图]
|-
| TopoQuest
|
|
| [http://www.topoquest.com/map.php?lat={latdegdec}&lon={londegdec}&datum=nad83&zoom=4 地形图]
|- style="background:#f5f5f5"
| Trails.com
|
|
| [http://www.topozone.com/map.asp?lat={latdegdec}&lon={londegdec}&datum=nad83 地形图]
|-
| 美國人口普查局
| [http://tiger.census.gov/cgi-bin/mapgen?lat={latdegdec}&lon={londegdec}&wid={span}&ht={span}&iht=600&iwd=600&mlat={latdegdec}&mlon={londegdec}&msym=bigdot&on=CITIES,GRID,interstate,statehwy,ushwy 地圖]
|
|
|- style="background:#f5f5f5"
| US EPA
|
|
| [http://water.usgs.gov/cgi-bin/pointinhuc.pl?latitude={latdegabs}{latminint}{latsecint}{latNS}&longitude={londegabs}{lonminint}{lonsecint}{lonEW} 流域資訊]
|-
| USGS National Map Viewer
| [http://nmviewogc.cr.usgs.gov/viewer.htm?CenterPoint={latdegdec},{londegdec}&Scale=CITY&Classes=OTHER%20IMAGERY 地圖]
|
|
|}
</div>

=欧洲 A-M=
<div id="GEOTEMPLATE-AT">
==奥地利==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图
|- style="background:#f5f5f5"
| ViaMichelin Austria
| [http://www.viamichelin.at/viamichelin/int/search/Cartes/{londegdec}*{latdegdec}?zoomLevel=12 地圖]
|-
| MSN Karten Österreich
| [http://maps.msn.at/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=1 地圖]
|}
</div>

<div id="GEOTEMPLATE-BG">
==保加利亚==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星
|- style="background:#f5f5f5"
| eMaps.bg
| [http://2cyr.com/emaps-bg.php?q={latdegdec},{londegdec} 地圖]
|
|-
| 360.bg
|
| [http://www.360.bg/index.php?lat={latdegdec}&lon={londegdec} 衛星圖]
|}
<!-- This service would be good to include, but #expr doesn't work as MediaWiki doesn't know the {} parameters, so it needs a GeoHack modification for the offset -->
<!-- *[http://www.emaps.bg/emaps/content.asp?mapSize=1&cboMaps=0&minx={{#expr: {utmeasting}-14425}}&maxx={{#expr: {utmeasting}+14425}}&miny={{#expr: {utmnorthing}-10000}}&maxy={{#expr: {utmnorthing}+10000}} Find this location] on emaps.bg [http://www.emaps.bg/].-->
</div>

<div id="GEOTEMPLATE-CZ">
==捷克==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星 !! 其他
|- style="background:#f5f5f5"
| Mapy.cz
| [http://www.mapy.cz/?st=search&fr=loc:{latdegabs}°{latminint}'{latsecdec}%22{latNS}%20{londegabs}°{lonminint}′{lonsecdec}%22{lonEW}%20dist:{scale}m&omp=ophoto 地圖]
| [http://www.mapy.cz/?mapType=hybrid&query=loc:{latdegabs}°{latminint}'{latsecdec}%22{latNS}%20{londegabs}°{lonminint}′{lonsecdec}%22{lonEW}%20dist:{scale}m 已標記的衛星圖]
| [http://www.mapy.cz/?mapType=army2&query=loc:{latdegabs}°{latminint}'{latsecdec}%22{latNS}%20{londegabs}°{lonminint}′{lonsecdec}%22{lonEW}%20dist:{scale}m 歷史變遷]
|-
| Atlas.cz
| [http://mapy.atlas.cz/?q={latdegabs}%C2%B0{latminint}%27{latsecdec}%22{latNS}%3B%20{londegabs}%C2%B0{lonminint}%27{lonsecdec}%22{lonEW} 地圖]
|
|
|- style="background:#f5f5f5"
| Supermapy.cz
| [http://supermapy-beta.centrum.cz/?ql={latdegabs}%C2%B0{latminint}'{latsecdec}%22{latNS}%20{londegabs}%C2%B0{lonminint}'{lonsecdec}%22{lonEW} 地圖]
|
|
|- style="background:#f5f5f5"
| 1188.cz
| [http://mapy.1188.cz/#pos={latdegdec};{londegdec}@sc={scale}@m=katastralni 地籍圖]
|
|
|}
<!--not work, can found what coor system they use
* [http://beta.mapy.atlas.cz/#appName=atlasof@mapType=2@centerX=-{osgb36easting}@centerY=-{osgb36northing}@mapScale={scale}@geoType=1 Find this location] on Mapy Atlas Beta . [http://beta.mapy.atlas.cz/]
-->
</div>

<div id="GEOTEMPLATE-DK">

==丹麦==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图
|- style="background:#f5f5f5"
| Findvej.dk
| [http://www.findvej.dk/?longitude={londegdec}&latitude={latdegdec} 地圖]
|-
| Findvej.dk with Wikipedia
| [http://www.findvej.dk/wikipedia?template=1&longitude={londegdec}&latitude={latdegdec} 地圖]
|- style="background:#f5f5f5"
| Eniro
| [http://kort.eniro.dk/query?what=map&mapstate={zoom};{londegdec};{latdegdec} 地圖]
|}
===間接===
* Kort & Martikelstyrelsen [http://www.kms.dk/C1256C6200312D33/(AllDocsByDocId)/4CCD2AA92F3C155DC1256CC900553DBF 地形图]
* Krak.dk [http://www.krak.dk/GRIDS/MAINPAGES/map.asp? 地圖] <!-- can be navigated, but needs to be researched -->
</div>

<div id="GEOTEMPLATE-EE">
==爱沙尼亚==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图
|- style="background:#f5f5f5"
| Estonian Land Board
| [http://xgis.maaamet.ee/xgis-latlon.php?lat={latdegdec}&lon={londegdec}&out=xgis Orthophoto/Map]
|}
===間接===
* Delfi - [http://kaart.otsing.delfi.ee/ 地圖]
</div>

<div id="GEOTEMPLATE-FI">
==芬兰==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 其他
|- style="background:#f5f5f5"
| Eniro
| [http://kartat.eniro.fi/query?what=map&mapstate={zoom};{londegdec};{latdegdec} 地圖]
| [http://kartat.eniro.fi/query?what=map&mapstate={zoom};{londegdec};{latdegdec};o Oblique]
|-
| National Land Survey of Finland MapSite
| [http://kansalaisen.karttapaikka.fi/kartanhaku/koordinaattihaku.html?y={latdegdec}&x={londegdec}&scale={scale}&srsName=LATLON:etrs&lang=en-GB 地圖]
|
|- style="background:#f5f5f5"
| 02.fi
| [http://toolserver.org/~para/02.fi-grc.html#latlon={latdegdec},{londegdec} 地圖]
|
|}

=== 本地 ===

{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 其他
|- style="background:#f5f5f5"
| eKarjala
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=0&Iref=0&link=http://kartta.ekarjala.fi/WebEK/Default.aspx?layers=Etel%C3%A4-Karjalan%20Seutukartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|-
| Espoo
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=6600000&Iref=2500000&link=http://kartat.espoo.fi/Web/Default.aspx?layers=Opaskartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|- style="background:#f5f5f5"
| Helsinki
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=6600000&Iref=2500000&link=http://kartta.hel.fi/opas/main/?l=1&m=1&o=1&n={Plocal}&e={Ilocal}}} 地圖]
|
|-
| Hämeenlinna
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=6700000&Iref=2500000&link=http://kartta.hameenlinna.fi/cgi-bin/GifMap.dll?Theme=Opaskartta&West={IlocalW}&South={PlocalS}&East={IlocalE}&North={PlocalN}&Height=600&Width=650&Command=DisplayLink&Language=fin&Info={Plocal},{Ilocal},{title}}} 地圖]
|
|- style="background:#f5f5f5"
| Jyväskylä
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=6890000&Iref=3400000&link=http://kartta.jkl.fi/web/Default.aspx?layers=Opaskartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|-
| Kokkola
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=7000000&Iref=2400000&link=http://ipp.kokkola.fi/cgi-bin/gifmap.dll?Theme=Opaskartta&West={IlocalW}&South={PlocalS}&East={IlocalE}&North={PlocalN}&Height=400&Width=500&Command=DisplayLink_fin&Language=fin&Info={Plocal},{Ilocal},{title}}} 地圖]
|
|- style="background:#f5f5f5"
| Kotka
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=6000000&Iref=3000000&link=http://karttapalvelu.kotka.fi/map/map.php?x={Ilocal}&y={Plocal}&px=1.0&txt={title}}} 地圖]
|
|-
| Kouvola
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=6740000&Iref=3470000&link=http://kartta.kouvola.fi/web/Default.aspx?layers=Opaskartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|- style="background:#f5f5f5"
| Kuopio
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=0&Iref=0&link=http://kartta.kuopionseutu.fi/map/map.php?x={Ilocal}&y={Plocal}&px=1.0&txt={title}}} 地圖]
|
|-
| Lahti
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=840&Iref=-23053970&link=http://kartta.lahti.fi/web/Default.aspx?layers=Opaskartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|- style="background:#f5f5f5"
| Lappeenranta
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=6700000&Iref=3500000&link=http://kartta.lappeenranta.fi/Web/Default.aspx?layers=Opaskartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|-
| Oulu
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&amp;amp;londegdec={londegdec}&Pref=7200000&Iref=2500000&link=http://kartta.ouka.fi/web/Default.aspx?layers=Opaskartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|- style="background:#f5f5f5"
| Pohjois-Karjala
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=0&Iref=0&link=http://pk-kartat.jns.fi/map.php?x={Ilocal}&y={Plocal}&px=1.0&txt={title}}} 地圖]
|
|-
| Pori
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=6800000&Iref=1500000&link=http://kartta.pori.fi/web/Default.aspx?layers=Opaskartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|- style="background:#f5f5f5"
| Rauma
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=0&Iref=1000000&link=http://opaskartta.rauma.fi/Web/Default.aspx?layers=Opaskartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|-
| Rovaniemi
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=0&Iref=0&link=http://kartta.rovaniemi.fi/Web/Default.aspx?layers=Opaskartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|- style="background:#f5f5f5"
| Tampere
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=0&Iref=0&link=http://www.tampere.fi/ytoteto/kartta/map.php?x={Ilocal}&y={Plocal}&px=1.0&txt={title}}} 地圖]
|
|-
| Turku
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=6600000&Iref=1500000&link=http://opaskartta.turku.fi/Web/Default.aspx?layers=Opaskartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|- style="background:#f5f5f5"
| Vaasa
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=6900000&Iref=1500000&link=http://kartta.vaasa.fi/Web/Default.aspx?layers=Opaskartta&cp={Plocal},{Ilocal}&z=2&title={title}}} 地圖]
|
|-
| Vantaa
| [{{fullurl:tools:~para/kkj.php|latdegdec={latdegdec}&londegdec={londegdec}&Pref=0&Iref=0&link=http://kartta.vantaa.fi/Default.aspx?easting={Ilocal}&northing={Plocal}}} 地圖]
|
|}
===間接===
* Retkikartta [http://www.retkikartta.fi/ 地形圖]
</div>

<div id="GEOTEMPLATE-FO">

==法罗群岛==
===間接===
* Føroya Dátusavn [http://www.kagi.fo/html/viewer.asp?Lang=FO 地圖]
</div>

<div id="GEOTEMPLATE-FR">

==法国==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星 !! 其他
|- style="background:#f5f5f5"
| Géoportail
| [http://toolserver.org/~para/geoportail.php?cg=v:1.1*c:metropole*cv:1.0*vv:1.1*xy:{londegdec}%7C{latdegdec}*s:{echelle}*pv:1.0*p:decouverte*l:Scan%7C1%7C100%7C&scale={scale} 地圖]
|[http://toolserver.org/~para/geoportail.php?cg=v:1.1*c:metropole*cv:1.0*vv:1.1*xy:{londegdec}%7C{latdegdec}*s:{echelle}*pv:1.0*p:decouverte*l:Photo%7C1%7C100%7C&scale={scale} 空照圖]
|[http://toolserver.org/~para/geoportail.php?cg=v:1.1*c:metropole*cv:1.0*vv:1.1*xy:{londegdec}%7C{latdegdec}*s:{echelle}*pv:1.0*p:decouverte*l:Parcelles%7C1%7C100%7C&scale={scale} 地籍圖], [http://toolserver.org/~para/geoportail.php?cg=v:1.1*c:metropole*cv:1.0*vv:1.1*xy:{londegdec}%7C{latdegdec}*s:{echelle}*pv:1.0*p:decouverte*l:Geologie%7C1%7C100%7C&scale={scale} 地質圖], [http://toolserver.org/~para/geoportail.php?cg=v:1.1*c:metropole*cv:1.0*vv:1.1*xy:{londegdec}%7C{latdegdec}*s:{echelle}*pv:1.0*p:decouverte*l:Cassini%7C1%7C100%7C&scale={scale} 卡西尼地圖]
|-
| ViaMichelin France
| [http://www.viamichelin.fr/viamichelin/fra/search/Cartes/{londegdec}*{latdegdec}?zoomLevel=12 地圖]
|
| [http://www.viamichelin.fr/viamichelin/fra/search/Trafic/{londegdec}*{latdegdec}?zoomLevel=12 路況圖]
|- style="background:#f5f5f5"
| MSN Cartes France
| [http://maps.msn.fr/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=1 地圖]
|
|
|}
</div>

<div id="GEOTEMPLATE-DE">

==德国==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图
|- style="background:#f5f5f5"
| GoYellow
| [http://www.goyellow.de/map/?lon={londegdec}&lat={latdegdec}&z=15 地圖]
|-
| ViaMichelin Germany
| [http://www.viamichelin.de/viamichelin/int/search/Cartes/{londegdec}*{latdegdec}?zoomLevel=12 地圖]
|- style="background:#f5f5f5"
| MSN Karten Deutschland
| [http://maps.msn.de/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=1 地圖]
|}
</div>

<div id="GEOTEMPLATE-GB">
==英国==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星 !! 其他
|- style="background:#f5f5f5"
| Bing Maps UK
| [http://www.bing.com/maps/?mkt=en-gb&v=2&cp={latdegdec}~{londegdec}&lvl={osmzoom}&sp=Point.{latdegdec}_{londegdec}_{title} 地圖]
| [http://www.bing.com/maps/?mkt=en-gb&v=2&cp={latdegdec}~{londegdec}&lvl=14&sp=Point.{latdegdec}_{londegdec}_{title}&sty=s 英國地形測量局地圖]
| [http://www.bing.com/maps/?mkt=en-gb&v=2&cp={latdegdec}~{londegdec}&lvl={osmzoom}&sp=Point.{latdegdec}_{londegdec}_{title}&sty=h 空照圖]
| [http://www.bing.com/maps/?mkt=en-gb&v=2&cp={latdegdec}~{londegdec}&lvl={osmzoom}&sty=o 鳥瞰視角]
|-
| Multimap
| [http://www.multimap.com/maps/?map={latdegdec},{londegdec}%7C{osmzoom} 地圖]
| [http://www.multimap.com/maps/?map={latdegdec},{londegdec}%7C15%7C4&dp=os 英國地形測量局地圖]
| [http://www.multimap.com/maps/?map={latdegdec},{londegdec}%7C{osmzoom}%7C32 空照圖]
| [http://www.multimap.com/maps/?map={latdegdec},{londegdec}%7C18%7C32 鳥瞰視角]
|- style="background:#f5f5f5"
| StreetMap
| [http://streetmap.co.uk/grid/{osgb36easting}_{osgb36northing}_106 地圖]
| [http://streetmap.co.uk/grid/{osgb36easting}_{osgb36northing}_120 英國地形測量局地圖]
|
|
|-
| 英國地形測量局 Get-a-map 服務
|
| [http://getamap.ordnancesurvey.co.uk/getamap/frames.htm?mapAction=gaz&gazName=g&gazString={osgb36ref} 英國地形測量局地圖]
|
|
|- style="background:#f5f5f5"
| {{abbr|Defra|英國环境、食品与农村事务处（Department for Environment, Food and Rural Affairs）}}之{{abbr|MAGIC|多級機關之鄉村地理資訊（Multi-Agency Geographic Information for the Countryside）}}服務－環境資訊
| [http://www.magic.gov.uk/website/magic/viewer.htm?startTopic=maggb&latlongref={latdegdec},{londegdec} 地圖]
|
|
|
|-
| {{abbr|Elgin|電子化地方政府資訊網（Electronic Local Government<br>Information Network）}}之路況資訊服務
| [http://elgin.gov.uk/index.cfm?api=1&page=map&coord={osgb36easting},{osgb36northing}&scale=5000 地圖]
|
|
|
|- style="background:#f5f5f5"
| ViaMichelin UK
| [http://www.viamichelin.co.uk/viamichelin/gbr/search/Cartes/{londegdec}*{latdegdec}?zoomLevel=12 地圖]
|
|
| [http://www.viamichelin.co.uk/viamichelin/gbr/search/Trafic/{londegdec}*{latdegdec}?zoomLevel=12 路況圖]
|-
| 英國地形測量局舊式地圖
| [http://www.ponies.me.uk/maps/osmap.html?z=14&x={londegdec}&y={latdegdec} 地圖]
|
|
|
|- style="background:#f5f5f5"
| MSN Maps UK
| [http://maps.msn.co.uk/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=1 地圖]
|
|
|
|}

位於[[英國國家格網參考系統]]上的'''{osgb36ref}''' (全數字格式為{osgb36easting} {osgb36northing}) ('''註：'''這不包括[[北爱尔兰]]。該地使用[[愛爾蘭格網參考系統]])

{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 資訊
|- style="background:#f5f5f5"
| [[Geograph British Isles project]]
| [http://www.geograph.org.uk/gridref/{osgb36ref} 該地照片集]
|-
| UKVillages
| [http://www.ukvillages.co.uk/ukvillages.nsf/b!open&s=village%20map&x={osgb36easting}&y={osgb36northing} UKVillages提供之告示板]
|}
</div>

<div id="GEOTEMPLATE-IS">

==冰岛==

{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地圖
|- style="background:#f5f5f5"
| Já.is
| [http://en.ja.is/kort#lat={latdegdec}&lon={londegdec}&z=6&mark=1 地圖]
|-
|}
</div>

<div id="GEOTEMPLATE-IM">

==曼島==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地圖
|- style="background:#f5f5f5"
| Multimap
| [http://www.multimap.com/p/browse.cgi?scale={mmscale}&lon={londegdec}&lat={latdegdec} 地圖]
|-
| StreetMap
| [http://www.streetmap.co.uk/newsearch.srf?mapp=newmap&searchp=newsearch&name={latdegdec},{londegdec}&Submit1=search&type=LatLong 地圖]
|- style="background:#f5f5f5"
| Ordnance Survey Get-a-map
| [http://getamap.ordnancesurvey.co.uk/getamap/frames.htm?mapAction=gaz&gazName=g&gazString={osgb36ref} 地圖]
|-
| MSN Maps UK
| [http://maps.msn.co.uk/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=1 地圖]
|}

位於[[英國國家格網參考系統]]上的'''{osgb36ref}'''
* [http://www.geograph.org.uk/gridref/{osgb36ref} 檢視該地位置的照片]，由[[Geograph British Isles project]]提供
* [http://www.ukvillages.co.uk/ukvillages.nsf/b!open&s=village%20map&x={osgb36easting}&y={osgb36northing} 詢找當地的村和社群]，UKVillages提供
</div>

<div id="GEOTEMPLATE-IT">

==意大利==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 
|- style="background:#f5f5f5"
| myMana
| [http://www.mymana.it/go.php?src=ALL&lat={latdegdec}&lon={londegdec}&zom=14 地圖]
|-
| ViaMichelin Italia
| [http://www.viamichelin.it/viamichelin/int/search/Cartes/{londegdec}*{latdegdec}?zoomLevel=12 地圖]
|- style="background:#f5f5f5"
| MSN Mappe Italia
| [http://maps.msn.it/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=1 地圖]
|}
===間接===
* [http://www.pcn.minambiente.it/viewer/viewer.htm Portale Cartografico Nazionale]
</div>

<div id="GEOTEMPLATE-LI">
==列支敦斯登==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地圖
|- style="background:#f5f5f5"
| Swisstopo
| [http://prod.swisstopogeodata.ch/swisstopo_apps/geodatenviewer/client.php?x={ch1903easting}&y={ch1903northing} 地圖]
|-
| map.search.ch
| [http://map.search.ch/{ch1903easting},{ch1903northing} 地圖]
|- style="background:#f5f5f5"
| MySwitzerland.com
| [http://map.myswitzerland.com/myswitzerland/?x={ch1903easting}.00&y={ch1903northing}.00&lang=en 地圖]
|-
| Mapplus/Tydac
| [http://www.mapplus.ch/frame.php?map=&x={ch1903easting}&y={ch1903northing}&zl=12 地圖]
|}
</div>

<div id="GEOTEMPLATE-LT">

==立陶宛==

===間接===
* Geographic Information portal of Lithuania [http://www.geoportal.lt 地圖與衛星圖]
* DELFI maps [http://maps.delfi.lt/ 地圖]
</div>

=欧洲 N-Z=
<div id="GEOTEMPLATE-NO">
==挪威==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地圖 !! 空照圖 !! 衛星圖
|- style="background:#f5f5f5"
| atlas.no
| [http://www.atlas.no/Default.aspx?x={utm33easting}&y={utm33northing}&zl=0&ms=0 地圖]
| [http://www.atlas.no/Default.aspx?x={utm33easting}&y={utm33northing}&zl=0&ms=1 空照圖]
| [http://www.atlas.no/Default.aspx?x={utm33easting}&y={utm33northing}&zl=0&ms=2 Hybrid]
|-
| Gule Sider
| [http://www.gulesider.no/kart/#lat={utmnorthing}&lon={utmeasting}&zoom={osmzoom}&userLon={utmeasting}&userLat={utmnorthing}&layers=B0000 地圖]
| [http://www.gulesider.no/kart/#lat={utmnorthing}&lon={utmeasting}&zoom={osmzoom}&userLon={utmeasting}&userLat={utmnorthing}&layers=00B00 空照圖]
|
|- style="background:#f5f5f5"
| Inatur
| [http://www.geodataonline.no/inatur/website_no/Kart.aspx?scale={scale}&center={utm33easting}%7c{utm33northing} 地圖]
|
|
|-
| Norkart Virtual Globe
|
|
| [http://www.virtual-globe.info/VirtualGlobeStarter.php?request=page&dataset=http://www.virtual-globe.info/norge-globe-features.vgml&lookat={londegdec},{latdegdec},{scale} 衛星圖]
|}
===間接===
* Norgesglasset [http://ngis2.statkart.no/norgesglasset/default.html 地形图]
* Visveg [http://visveg.no/Visveg 地圖]
* WebAtlas [http://www.webatlas.no/ 地圖]
* Finn.no [http://www.finn.no/kart/ 地圖]
</div>

<div id="GEOTEMPLATE-PL">

==波兰==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 
|- style="background:#f5f5f5"
| Mapa Polski Targeo
| [http://mapa.targeo.pl/{title},,{londegdec},{latdegdec} 地圖]
|-
| Szukacz.pl
| [http://mapa.szukacz.pl/?n={latdegdec}&e={londegdec}&z=3 地圖]
|- style="background:#f5f5f5"
| Zumi
| [http://www.zumi.pl/namapie.html?long={londegdec}&lat={latdegdec}&type=3&scale=3 地圖]
|-
| Autopilot
| [http://mapa.autopilot.pl/?long={londegdec}&lat={latdegdec}&zoom=12 地圖]
|- style="background:#f5f5f5"
| Polish Railways Map
| [http://mapa.kolej.one.pl/index.php?z=11&x={londegdec}&y={latdegdec} 地圖]
|}
===間接===
*Geoportal [http://maps.geoportal.gov.pl/webclient/ 地圖]
</div>

<div id="GEOTEMPLATE-PT">

==葡萄牙==

{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地圖
|- style="background:#f5f5f5"
| rowspan="3" | Instituto<br />Geográfico<br />do Exército 
| [http://www.igeoe.pt/igeoearcweb/igeoesig/ExecCmd.asp?cmd=Center&Lng={londegdec}&Lat={latdegdec}&Scale=25000&SC=WGS84 Continente] (Portuguese mainland) 
| rowspan="3" | (requires<br />Internet Explorer<br />6.0 or above)
|-
| [http://www.igeoe.pt/igeoearcweb/acores/ExecCmd.asp?cmd=Center&Lng={londegdec}&Lat={latdegdec}&Scale=25000&SC=WGS84 Açores]
|-
| [http://www.igeoe.pt/igeoearcweb/madeira/ExecCmd.asp?cmd=Center&Lng={londegdec}&Lat={latdegdec}&Scale=25000&SC=WGS84 Madeira]
|}

</div>

<div id="GEOTEMPLATE-RU">

==俄罗斯==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星
|- style="background:#f5f5f5"
| Yandex Maps
| [http://maps.yandex.ru/?ll={londegdec},{latdegdec}&spn={span},{span}&l=map 地圖]
| [http://maps.yandex.ru/?ll={londegdec},{latdegdec}&spn={span},{span}&l=sat 衛星圖]
|-
| Kosmosnimki
| [http://www.kosmosnimki.ru/index.html#mode=map&x={londegdec}&y={latdegdec}&z=12&fullscreen=true 地圖]
| [http://www.kosmosnimki.ru/index.html#mode=satellite&x={londegdec}&y={latdegdec}&z=12&fullscreen=true 衛星圖]
|}
</div>

<div id="GEOTEMPLATE-SK">
==斯洛伐克==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图
|- style="background:#f5f5f5"
| Mapy.Atlas.sk
| [http://mapy.atlas.sk/GPS%3A{latdegdec}N+{londegdec}E 地圖]
|-
| TuristickaMapa.sk
| [http://www.turistickamapa.sk/?y={latdegdec}&x={londegdec} 地圖]
|}
</div>

<div id="GEOTEMPLATE-SI">
==斯洛文尼亚==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星 !! 其他
|- style="background:#f5f5f5"
| Geopedia
| [http://www.geopedia.si/#L381_T13_b4_c{latdegdec},{londegdec}_s16 地圖]
| [http://www.geopedia.si/#L381_T13_b2_c{latdegdec},{londegdec}_s16 衛星圖]
| [http://www.geopedia.si/#L381_T13_b1-3_c{latdegdec},{londegdec}_s16 Terrain]
|-
| GeaBios
| [http://www.geabios.com/html/services/maps/PublicMap.htm?lat={latdegdec}&lon={londegdec}&fov={span} 地圖]
|
|
|}
===間接===
* Najdi.si [http://zemljevid.najdi.si/search.jsp?tab=maps&x1={latdegdec}&y1={londegdec}&zoom=12000&gx={latdegdec}&gy={londegdec} 地圖]
</div>

<div id="GEOTEMPLATE-ES">
==西班牙==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 覆蓋範圍 !! 地圖
|- style="background:#f5f5f5"
| MSN Mapas España
|align=center| 全區
| [http://maps.msn.es/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=1 地圖]
|-
| Vissir - ICC
| 加泰罗尼亚
| [http://www.icc.cat/vissir2/?etrs89x={londegdec}&etrs89y={latdegdec}&lang=en_UK 地圖]
|- style="background:#f5f5f5"
| Nomecalles
| 馬德里社群
| [http://gestiona.madrid.org/nomecalles/Inicio.icm?idioma=en&utmX={utmeasting}&utmY={utmnorthing}&zoom={altitude} 地圖]
|}
</div>

<div id="GEOTEMPLATE-SE">

==瑞典==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地圖 !! 衛星 !! 其他
|- style="background:#f5f5f5"
| Eniro
| [http://kartor.eniro.se/query?what=map&mapstate={zoom};{londegdec};{latdegdec} 地圖]
| [http://kartor.eniro.se/query?what=map&mapstate={zoom};{londegdec};{latdegdec};h 已標記的衛星圖]
| [http://kartor.eniro.se/query?what=map&mapstate={zoom};{londegdec};{latdegdec};o 鳥瞰圖]
|-
| hitta.se
| [http://toolserver.org/~para/WGS84toRT90.php?lat={latdegdec}&lon={londegdec}&url=http%3A//www.hitta.se/LargeMap.aspx%3Fz%3D3%26mp%3D%3Cpts%3E%3Cpt%20x%3D%22%7Brt90x%7D%22%20y%3D%22%7Brt90y%7D%22%20i%3D%22/images/point.png%22%3E%3Ct%3E{title}%3C/t%3E%3C/pt%3E%3C/pts%3E 地圖]
| [http://toolserver.org/~para/WGS84toRT90.php?lat={latdegdec}&lon={londegdec}&url=http%3A//www.hitta.se/LargeMap.aspx%3FShowSatellite%3Dtrue%26z%3D3%26mp%3D%3Cpts%3E%3Cpt%20x%3D%22%7Brt90x%7D%22%20y%3D%22%7Brt90y%7D%22%20i%3D%22/images/point.png%22%3E%3Ct%3E{title}%3C/t%3E%3C/pt%3E%3C/pts%3E 衛星圖]
|}
===間接===
* Stadskartan [http://www.stadskartan.se/start/lansregister.asp 地圖]
* Kartguiden [http://www.kartguiden.com/ 地圖]
* KartSök och ortnamn [http://www2.lantmateriet.se/ksos/index.html 地圖]
* Historiska kartor [http://historiskakartor.lantmateriet.se/arken/s/search.html 地圖]
</div>

<div id="GEOTEMPLATE-CH">

==瑞士==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! Cantons covered !! 地圖
|- style="background:#f5f5f5"
| Swisstopo
|align=center| all
| [http://prod.swisstopogeodata.ch/swisstopo_apps/geodatenviewer/client.php?x={ch1903easting}&y={ch1903northing} 地圖]
|-
| map.search.ch
|align=center| all
| [http://map.search.ch/{ch1903easting},{ch1903northing} 地圖]
|- style="background:#f5f5f5"
| MySwitzerland.com
|align=center| all
| [http://map.myswitzerland.com/myswitzerland/?x={ch1903easting}.00&y={ch1903northing}.00&lang=en 地圖]
|-
| Mapplus/Tydac
|align=center| all
| [http://www.mapplus.ch/frame.php?map=&x={ch1903easting}&y={ch1903northing}&zl=12 地圖]
|- style="background:#f5f5f5"
| geoportal.ch
| St. Gallen, Appenzell
| [http://www.geoportal.ch/schnittstelle/aufruf.aspx?VERSION=1.0&REQUEST=GetIGis&MAP=94&TOPIC=Coord&ATTRIBUTE1={ch1903easting}&ATTRIBUTE2={ch1903northing}&sign=0&WIDTH=2000 地圖]
|-
| AGISviewer Kanton Aargau
| Aargau
| [http://www.ag.ch/agisviewer/mapFrame.asp?MapWidth=531&MapHeight=492&bitte%20ausw%E4hlen!&Cmd=zoomIn&MinX={ch1903easting}.00001&MinY={ch1903northing}.1&MaxX={ch1903easting}.9&MaxY={ch1903northing}.9 地圖]
|- style="background:#f5f5f5"
| GeoPortal Basel-Stadt
| Basel-City
| [http://www.geo-bs.ch/stadtplan_stadtplan_karte.cfm?X={ch1903easting}&Y={ch1903northing}&Jump=3&Zoom=1000&ZIparkhaeuser=1&ZIspitaeler=1 地圖]
|-
| geoView.BL
| Basel-Country
|[http://www.geo.bl.ch/parzis/automap.jsp?LAYERS=map_3&ZOOM={ch1903easting}.000001%7C{ch1903northing}.000001%7C{ch1903easting}.99%7C{ch1903northing}.99 地圖]
|- style="background:#f5f5f5"
| GéoPortail du Canton de Jura
| Jura
|[http://www.jura.ch/sit/geoportail/IndexRedir.html?Y={ch1903easting}&X={ch1903northing}&echelle=5000&theme=photoaerienne 地圖]
|-
| SITN
| Neuchâtel
|[http://sitn.ne.ch/index.html?x={ch1903easting}&y={ch1903northing}&echelle=25000 地圖]
|- style="background:#f5f5f5"
| GIS Schaffhausen
| Schaffhausen
|[http://www.gis.sh.ch/gis_sh_internet/mapservice.asp?IDProjekt=3&MapServiceUserGroup=1&MapServiceUser=0&MapServiceURL=Nav@g@22@u@West@g@{ch1903easting}@u@Nord@g@{ch1903northing}@u@B@g@1000 地圖]
|-
| GeoShop vs.geo
| Valais
|[http://mapserver3.internetgalerie.ch/vs-geo/vs-geo.php?recenter_bbox={ch1903easting},{ch1903northing} 地圖]
|- style="background:#f5f5f5"
| ZugMap
| Zug
|[http://www.zugmap.ch/bm2_zugmap/mapservice.asp?IDProjekt=1&MapServiceUserGroup=29&MapServiceUser=0&MapServiceURL=Nav@g@22@u@West@g@{ch1903easting}@u@Nord@g@{ch1903northing}@u@B@g@5726&MapServiceDatenauswahl=89@g@94 地圖]
|-
| GIS-Zentrum Kanton Zürich
| Zurich
|[http://www.gis.zh.ch/gb/gb.asp?YKoord={ch1903easting}&XKoord={ch1903northing}&Massstab=10000 地圖]
|}

'''{ch1903easting} / {ch1903northing}''' on the [[Swiss Grid]]
</div>

<div id="GEOTEMPLATE-UA">

==乌克兰==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星
|- style="background:#f5f5f5"
| maps.vlasenko.net
| [http://maps.vlasenko.net/?lat={latdegdec}&lon={londegdec} 地圖]
| [http://maps.vlasenko.net/?lat={latdegdec}&lon={londegdec}&addmap1=space10 衛星圖]
|-
| Visicom Maps
| [http://maps.visicom.ua/#lng={londegdec};lat={latdegdec};z=6;map=ukraine_en;lngm={londegdec};latm={latdegdec}; 地圖]
|
|}
</div>
<!--
==Europe 間接==
* ViaMichelin [http://www.viamichelin.com/viamichelin/int/dyn/controller/mapPerformPage?strCountry=EUR&strAddress=&strMerged={title}&x=0&y=0 地圖]
-->

=大洋洲=
<div id="GEOTEMPLATE-AU">
==澳大利亚==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 其他
|- style="background:#f5f5f5"
| Street-Directory.com.au
| [http://www.street-directory.com.au/sd_new/genmap.cgi?x={londegdec}&y={latdegdec}&sizex=800&sizey=800&level=5&star=6 地圖]
|
|-
| Bonzle Digital Atlas
| [http://maps.bonzle.com/c/a?a=p&x={londegdec}&y={latdegdec} 地圖]
| [http://maps.bonzle.com/c/a?a=p&d=ter&x={londegdec}&y={latdegdec} Terrain Slice]
|-
| NearMap
| 
| [http://www.nearmap.com/?ll={latdegdec},{londegdec}&z={zoom} 空照]
|}
===間接===
* SIX - New South Wales - [http://imagery.maps.nsw.gov.au/ 地形图]
* LIST - Tasmania - [http://www.thelist.tas.gov.au/listmap/listmapstart.jsp 地形图]
</div>

<div id="GEOTEMPLATE-NZ">

==新西兰==
<!-- :<code>{nztmeasting} {nztmnorthing}</code> on NZTM ([[NZGD2000]]) -->
===間接===
* NZTopoOnline [http://www.nztopoonline.linz.govt.nz 地形图]
</div>

=亚洲=
<div id="GEOTEMPLATE-CN">
==中国大陆==
{| class="geoservices" border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !!卫星!!地形
|-
! scope="row" style="font-weight:normal; text-align:left;" |  百度地图
| [https://map.baidu.com/?latlng={latdegdec},{londegdec}&title={titlee}&content={titlee}&autoOpen=true&l= 地图] || ||
|-
! scope="row" style="font-weight:normal; text-align:left;" |  高德地图
| [https://ditu.amap.com/regeo?lng={londegdec}&lat={latdegdec}&name={titlee} 地图] || ||
|-
! scope="row" style="font-weight:normal; text-align:left;" | 腾讯地图
|[https://map.qq.com/?type=marker&isopeninfowin=1&markertype=1&pointx={londegdec}&pointy={latdegdec}&name={titlee}&addr=ADDRESS 地图]
|-
|colspan="4" style="font-size:smaller;background:#f5f5f5"|受[[中华人民共和国测绘限制]]影响，中国地图显示geohack的WGS84坐标会出现一些偏移。可以使用[https://artoria2e5.github.io/PRCoords/demo?lat={latdegdec}&lon={londegdec}#output 这个链接]将Geohack坐标转换到百度地图使用的BD-09坐标和其他地图使用的GCJ-02坐标。
|}

===间接===
* [http://map.sogou.com/ 搜狗地图]
* [http://www.mapabc.com/ mapABC]
* [http://www.mapbar.com/ 图吧]
* [http://www.51ditu.com/ 我要地图]

</div>

<div id="GEOTEMPLATE-IN">

==印度==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星 
|- style="background:#f5f5f5"
| Yahoo! India Maps
| [http://in.maps.yahoo.com/#?lat={latdegdec}&lon={londegdec}&z=5 地圖]
| [http://in.maps.yahoo.com/#?lat={latdegdec}&lon={londegdec}&z=5&mt=h 已標記的衛星圖]
|}
===間接===
* MapMyIndia [http://mapmyindia.com 地圖]
* Maptell [http://www.maptell.com/index.php?option=com_wrapper&Itemid=182 地圖]
</div>

<div id="GEOTEMPLATE-JP">
==日本==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星 !! 其他
|- style="background:#f5f5f5"
| Google Japan
| [//maps.google.co.jp/maps?ll={latdegdec},{londegdec}&spn={span},{span}&q={latdegdec},{londegdec} 地圖]
| [//maps.google.co.jp/maps?ll={latdegdec},{londegdec}&spn={span},{span}&t=h&q={latdegdec},{londegdec} 已標記的衛星圖]
|
|-
| Geographical Survey Institute
|
|
| [http://watchizu.gsi.go.jp/watchizu.html?latitude={latdegdec}&longitude={londegdec} 地形图]
|- style="background:#f5f5f5"
| CyberJapan
|
|
| [http://portal.cyberjapan.jp/denshi/opencjapan.cgi?x={londegdec}&y={latdegdec}&s=10000 地形图]
|-
| Mapion
| [{{fullurl:tools:~para/cgi-bin/wgs2tky|q={latdegdec},{londegdec}&url=http://www.mapion.co.jp/c/f?uc=1&nl={latdegabsjp}/{latminintjp}/{latsecdecjp}&el={londegabsjp}/{lonminintjp}/{lonsecdecjp}&grp=all&scl=250000}} 地圖]
|
|
|- style="background:#f5f5f5"
| MapFan Web
| [{{fullurl:tools:~para/cgi-bin/wgs2tky|q={latdegdec},{londegdec}&url=http://www.mapfan.com/m.cgi?MAP={lonEW}{londegabsjp}.{lonminintjp}.{lonsecdecjp}{latNS}{latdegabsjp}.{latminintjp}.{latsecdecjp}}} 地圖]
|
|
|-
| Yahoo! Japan
| [{{fullurl:tools:~para/cgi-bin/wgs2tky|q={latdegdec},{londegdec}&url=http://map.yahoo.co.jp/pl?lat={latdegabsjp}.{latminintjp}.{latsecdecjp}&lon={londegabsjp}.{lonminintjp}.{lonsecdecjp}}} 地圖]
|
|
|- style="background:#f5f5f5"
| Goo
| [{{fullurl:tools:~para/cgi-bin/wgs2tky|q={latdegdec},{londegdec}&url=http://map.goo.ne.jp/map.php?MAP={lonEW}{londegabsjp}.{lonminintjp}.{lonsecdecjp}{latNS}{latdegabsjp}.{latminintjp}.{latsecdecjp}}} 地圖]
|
|
|-
| Its-mo Guide
| [{{fullurl:tools:~para/cgi-bin/wgs2tky|q={latdegdec},{londegdec}&url=http://www.its-mo.com/z.htm?m={lonEW}{londegabsjp}.{lonminintjp}.{lonsecdecjp}{latNS}{latdegabsjp}.{latminintjp}.{latsecdecjp}&l=8}} 地圖]
|
|
|- style="background:#f5f5f5"
| Livedoor
| [{{fullurl:tools:~para/cgi-bin/wgs2tky|q={latdegdec},{londegdec}&url=http://map.livedoor.com/map/?MAP={lonEW}{londegabsjp}.{lonminintjp}.{lonsecdecjp}{latNS}{latdegabsjp}.{latminintjp}.{latsecdecjp}}} 地圖]
|
|
|}
</div>

<div id="GEOTEMPLATE-LB">
==黎巴嫩==

{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
|-
! 服務商
! 語系
! 型態
|- style="background:#f5f5f5"
| Ayna
| Arabic
| [http://maps.ayna.com/?lang=ar&lon={londegdec}&lat={latdegdec}&zoom=6&layer=m&marker=1&title={title} 地圖]
|-
| Ayna
| English
| [http://maps.ayna.com/?lang=en&lon={londegdec}&lat={latdegdec}&zoom=6&layer=m&marker=1&title={title} 地圖]
|- style="background:#f5f5f5"
| Ayna
| 
| [http://maps.ayna.com/?lang=en&lon={londegdec}&lat={latdegdec}&zoom=6&layer=s&marker=1&title={title} 衛星圖]
|}
</div>


<div id="GEOTEMPLATE-SG">

==新加坡==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 
|- style="background:#f5f5f5"
| Gothere
| [http://gothere.sg/directions#@{latdegdec},{londegdec}: 地圖]
|}
</div>

<div id="GEOTEMPLATE-TW">

==台湾==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 
|- style="background:#f5f5f5"
| Urmap
| [http://www.urmap.com/?qs={londegdec},{latdegdec} 地圖]
|-
| Yahoo!奇摩地圖
| [http://tw.maps.yahoo.com/#lat%01{latdegdec}%02lon%01{londegdec}%02z%012%02pos%01{pagename}%02pok%011%02mrt%010%02pos1%01%02lat1%010%02lon1%010%02pos2%01%02lat2%010%02lon2%010%02shop%01%02sok%010%02sp%010%02slat%010%02slon%010%02rcate%010%02rok%010%02rlat%010%02rlon%010%02lok%010%02llat%010%02llon%010%02mtab%011%02pr%010%02up%010 地圖]
|}
</div>

<div id="GEOTEMPLATE-TH">

==泰国==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 
|- style="background:#f5f5f5"
| PointAsia
| [http://gw.pointasia.com/pointme3/home.aspx?lat={latdegdec}&lon={londegdec} 地圖]
|}
</div>

=南美=
<div id="GEOTEMPLATE-BR">
==巴西==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图
|- style="background:#f5f5f5"
| MSN Maps Brazil
| [http://maps.msn.com/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=4 地圖]
|}
</div>

<div id="GEOTEMPLATE-CL">
==智利==
===間接===
* Office of Territory Studies [http://www.gobernabilidad.cl/cartografia.html 地圖]
</div>

<div id="GEOTEMPLATE-AQ">
==南極洲==
<!--
 add only systems that can display 90 S 0 E etc.
-->
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地圖
|- style="background:#f5f5f5"
| MSN maps
| [http://maps.msn.com/map.aspx?lats1={latdegdec}&lons1={londegdec}&alts1={altitude}&regn1=2 地圖]
|}
</div>

=非洲=
<div id="GEOTEMPLATE-TN">
==突尼斯==
{| border="1" cellpadding="2" style="border:silver 1px solid; border-collapse:collapse;"
! 服务商 !! 地图 !! 卫星
|- style="background:#f5f5f5"
| Ayna 
| [http://maps.ayna.com/?lang=en&lon={londegdec}&lat={latdegdec}&zoom=9&layer=m&marker=1&title={Title} 地圖]
| [http://maps.ayna.com/?lang=en&lon={londegdec}&lat={latdegdec}&zoom=9&layer=s&marker=1&title={Title} 衛星圖]
|}
</div>

<div id="GEOTEMPLATE-XZ">

=國際水域 (XZ)=
No specific resources added yet.
</div>

<!-- End region specific -->
</div>

<!-- Note: Hidden categories show on GeoHack -->
__NOINDEX__

[[Category:地理技术]]
[[Category:外部资源模板|GeoTemplate]]