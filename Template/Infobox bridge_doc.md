<includeonly><!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{Documentation subpage}}</noinclude>
<!-- 請在這條線之下編輯模板的說明文件 -->
{{Parameter names example | alt | architect | begin | builder | caption | carries | child | clearance | below | closed | collapsed | complete | contracted_designer | coordinates | cost | crosses | depth | design | designer | electrification | embed | engineering | extra | fabricator | followed | height | heritage | id | image | image_size | image_upright | inaugurated | lanes | length | life | load | country | locale | mainspan | maint | material | name | named_for | native_name | native_name_lang | num_track | number_spans | official_name | open | os_grid_reference | other_name | owner | pierswater | preceded | rebuilt | replaces | replaced_by | structure_gauge | toll | towpath | track_gauge | traffic | traversable | website | width | winner | coordinates={{coord|0|0|type:landmark|display=inline}} }}

==使用方法==
*將以下的模板複製到條目中，在將左列的函數項目複製至條目中之後，就可以將各項的數值填入。
*不使用的函數項目可以刪除，以維護原碼整齊及其易懂性，另並不會對簡介框產生影響。
*有關各項函數解釋請見[[Template:Infobox Bridge#参数描述|下一段落↓]]。
<pre style="overflow:auto">
{{Infobox bridge
| name                = 
| native_name         = 
| native_name_lang    = 
| image               = 
| image_size          = 
| image_upright       = 
| alt                 = 
| caption             = 
| coordinates         = <!-- {{Coord}} -->
| os_grid_reference   = 
| carries             = 
| crosses             = 
| country             =
| locale              = <!-- location = -->
| official_name       = 
| other_name          = 
| named_for           = 
| owner               = 
| maint               = 
| heritage            = 
| id                  = 
| id_type             =
| website             = 
| preceded            = 
| followed            = 
<! -- 设计参数 -->
| design              = 
| material            = 
| length              = 
| width               = 
| height              = 
| depth               = 
| traversable         = 
| towpath             = 
| mainspan            = 
| number_spans        = 
| pierswater          = <!-- piers_in_water = -->
| load                = 
| clearance           = 
| below               = 
| lanes               = 
| exits               = 
| speed_limit         = 
| life                = 
<! -- 轨道特性 -->
| num_track           = 
| track_gauge         = 
| structure_gauge     = 
| electrification     = 
<! -- 历史 -->
| architect           = 
| designer            = 
| contracted_designer = 
| winner              = 
| engineering         = 
| builder             = 
| fabricator          = 
| begin               = 
| complete            = 
| cost                = 
| inaugurated         = 
| open                = 
| rebuilt             = 
| collapsed           = 
| closed              = 
| replaces            = 
| replaced_by         = 
<! -- 统计 -->
| traffic             = 
| toll                = 
<! -- 附加信息 -->
| extra               = <!-- extra = module = embed = -->
}}
</pre>

==参数描述==
{| class="wikitable" border="1"
! 域 !! 描述
|-
| name || 桥名或中文译名
|-
| native_name || 桥梁的本地语言名称
|-
| native_name_lang || 本地语言的ISO代码（如：以“fr”表示法语）；若有一种以上的语言，请使用{{Tl|Lang}}模板输入本地语言名称。
|-
| image || 桥梁图像的档案名称
|-
| image_size || 桥梁图像的宽度数值。只需要输入像素值，px单位已经内建不需输入，默认值为250px
|-
| alt || 桥梁图像的替代文字（参见：[[Wikipedia:圖像的替代文字|WP:ALT]]）
|-
| caption || 图像下方的说明文字
|-
| coordinates || 坐标，请使用{{Tl|Coord}}模板（如：<nowiki>{{Coord|50|01|01|N|90|01|01|W|region:US_type:landmark|display=it}}</nowiki>）。如留空則使用Wikidata的P625值（如有）。
|-
| carries || 承载：通過桥梁的交通路線类型（如：公路、鐵路）、编号及名称，或其他信息
|-
| crosses || 跨越：跨越的水体或其他地理特征（如：河流名称或峡谷名称等）
|-
| country || 國家／地區：桥梁所在國家或地區
|-
| locale || 地点：桥梁所在地名
|-
| official_name || 官方名称：（如果与桥名不同的话）
|-
| other_name || 其他名称：桥梁的别名
|-
| owner || 业主：拥有桥梁所有权的个人或机构
|-
| maint || 维护单位：（如：加利福尼亚交通部）
|-
| heritage || 保护状况：文物古迹的保护状况（如：[[全国重点文物保护单位]]、[[世界遗产]]等）
|-
| id || 官方编号
|-
| id_type || 编号类型。若无特别说明，默认为{{le|美国国家桥梁数据库|National Bridge Inventory}}编号。
|-
| preceded || 上游桥梁：上游桥梁的名称
|-
| followed || 下游桥梁：下游桥梁的名称
|-
| design || 桥型：（如：悬臂桥、桁架桥、斜拉桥等）
|-
| material || 建筑材料：（如：混凝土、钢、石、砖、木等）
|-
| length || 全长：桥梁的总长度，请使用公英制自动转换模板{{tl|Convert}}。
|-
| width || 宽度：桥梁宽度，请使用公英制自动转换模板{{tl|Convert}}。
|-
| height || 高度：桥梁的最大高度，请使用公英制自动转换模板{{tl|Convert}}。
|-
| mainspan || 最大跨度：主跨或最大跨距的长度，请使用公英制自动转换模板{{tl|Convert}}。
|-
| spans || 跨数：桥跨数量
|-
| pierswater || 桥墩数：桥墩数量
|-
| load || 负载限制：桥梁的最大负载重量，请使用公英制自动转换模板{{tl|Convert}}。
|-
| clearance || 桥上净空：桥面以上的通行净空高度
|-
| below || 桥下净空：桥面以下的净空高度
|-
| lanes || 车道数：桥面车道数量（不含非机动车道、人行道） 
|-
| exits || 出口数：桥面车道出口数量 
|-
| speed_limit || 车速限制：桥面车道最高行车限速
|-
| life || 设计寿命：桥梁设计的最大使用年限
|-
| architect || 建筑师：负责桥梁概念设计的第三方建筑师
|-
| designer || 设计师：桥梁设计者或工程师（如：[[伊桑巴德·金德姆·布鲁内尔]]）
|-
| contracted_designer || 首席工程师：合同阶段的首席工程师
|-
| winner || 获得奖项：所获得的奖项
|-
| engineering || 设计单位：负责工程或建筑设计的机构，不同于上述的“designer”。
|-
| builder || 施工单位：桥梁建造者或施工单位
|-
| fabricator || 钢材生产商：所用钢材的生产商
|-
| begin || 开工日：奠基或开工日期
|-
| complete || 完工日：竣工日期
|-
| cost || 总造价：项目总造价或总投资额
|-
| inaugurated || 启用日：举行正式启用典礼的日期
|-
| open || 开通日：实际开通的日期
|-
| rebuilt || 重建日：开始重建的日期
|-
| collapsed || 毁坏日：倒塌或被毁、拆除的日期（如果已倒塌的话）
|-
| closed || 关闭日：关闭或停止使用的日期（如果已关闭的话）
|-
| replaces || 取代：该桥梁替代的原有交通设施（桥梁、隧道或轮渡服务等）
|-
| replaced_by || 被取代：已替代该桥梁的其他交通设施（桥梁、隧道或轮渡服务等）
|-
| traffic || 日交通量：年平均日交通流量
|-
| toll || 通行费：桥梁通行费（如果是收费桥梁的话）
|-
| extra || 其他附加信息
|-
| references || 本信息框的参考资料
|}

==举例==
{{Infobox bridge
| name      = 里翁-安提里翁大桥
| native_name      = Γέφυρα Ρίου-Αντιρρίου
| native_name_lang = el
| image            = C3.00a Brücke Río–Andírio.jpg
| image_size       = 
| caption          = 
| coordinates      = {{Coord|38|19|17|N|21|46|22|E|region:GR_type:landmark|display=inline}}
| carries          = [[File:Autokinetodromos A5 number.svg|x15px]] [[希腊5号高速公路]]<br>人行及自行车道
| crosses          = [[科林斯湾]]
| locale           = {{GRE}}{{le|里翁|Rio, Greece}}－{{le|安提里翁|Antirrio}}
| official_name    = 查理拉奥斯·奇科皮斯大桥<br>{{lang|el|Γέφυρα Χαρίλαος Τρικούπης}}
| owner            = {{le|希腊政府|Government of Greece}}
| maint            = 戈菲拉（{{lang|en|Gefyra SA}}）
| website          = [https://www.gefyra.gr/ 官方网站]（[[希腊语]]）
| design           = [[斜拉桥]]
| material         = [[钢]]、[[混凝土]]
| length           = {{convert|2880|m|ft|0}} 
| width            = {{convert|27.2|m|ft|0}} 
| height           = {{convert|230|m|ft|0}}
| mainspan         = {{convert|560|m|ft|0}}
| spans            = 5
| pierswater       = 4
| load             = 28,000[[吨]]
| clearance        = 
| below            = {{convert|57|m|ft|0}}
| lanes            = 
| life             = 120年
| architect        = {{le|贝吉·米卡利安|Berdj Mikaelian}}
| designer         = 
| contracted_designer = 
| winner           = 
| engineering      = 拉泽尔公司（{{lang|en|Razel}}）
| builder          = 
| fabricator       = {{le|克利夫兰桥梁工程公司|Cleveland Bridge & Engineering Company}}
| begin            = 1998年7月19日
| complete         = 
| cost             = 7.71亿[[欧元]]
| inaugurated      = 2004年8月7日
| open             = 2004年8月12日
| traffic          = 11,000辆
| toll             = 小汽车：13.2欧元<br>摩托车：1.9欧元<br>客车：29.7~64欧元<br>卡车：19.9~41欧元
| references       = 
}}

<pre style="overflow: auto;">
{{Infobox bridge
| name      = 里翁-安提里翁大桥
| native_name      = Γέφυρα Ρίου-Αντιρρίου
| native_name_lang = el
| image            = C3.00a Brücke Río–Andírio.jpg
| image_size       = 
| caption          = 
| coordinates      = {{Coord|38|19|17|N|21|46|22|E|region:GR_type:landmark|display=inline}}
| carries          = [[File:Autokinetodromos A5 number.svg|x15px]] [[希腊5号高速公路]]<br>人行及自行车道
| crosses          = [[科林斯湾]]
| locale           = {{GRE}}{{le|里翁|Rio, Greece}}－{{le|安提里翁|Antirrio}}
| official_name    = 查理拉奥斯·奇科皮斯大桥<br>{{lang|el|Γέφυρα Χαρίλαος Τρικούπης}}
| owner            = {{le|希腊政府|Government of Greece}}
| maint            = 戈菲拉（{{lang|en|Gefyra SA}}）
| website          = [https://www.gefyra.gr/ 官方网站]（[[希腊语]]）
| design           = [[斜拉桥]]
| material         = [[钢]]、[[混凝土]]
| length           = {{convert|2880|m|ft|0}} 
| width            = {{convert|27.2|m|ft|0}} 
| height           = {{convert|230|m|ft|0}}
| mainspan         = {{convert|560|m|ft|0}}
| spans            = 5
| pierswater       = 4
| load             = 28,000[[吨]]
| clearance        = 
| below            = {{convert|57|m|ft|0}}
| lanes            = 
| life             = 120年
| architect        = {{le|贝吉·米卡利安|Berdj Mikaelian}}
| designer         = 
| contracted_designer = 
| winner           = 
| engineering      = 拉泽尔公司（{{lang|en|Razel}}）
| builder          = 
| fabricator       = {{le|克利夫兰桥梁工程公司|Cleveland Bridge & Engineering Company}}
| begin            = 1998年7月19日
| complete         = 
| cost             = 7.71亿[[欧元]]
| inaugurated      = 2004年8月7日
| open             = 2004年8月12日
| traffic          = 11,000辆
| toll             = 小汽车：13.2欧元<br>摩托车：1.9欧元<br>客车：29.7~64欧元<br>卡车：19.9~41欧元
| references       = 
}}
</pre>
{{brClear}}

{{UF-hcard-geo}}

== 追踪分类 ==
* {{clc|Category:使用未知桥梁信息框参数的页面}}

== 参见 ==
* [[Template:Infobox tunnel]]

{{Buildings and structures infobox templates}}
<includeonly>{{Sandbox other||<!-- 本行下加入模板的分類 -->
[[Category:交通信息框模板|桥]]
[[Category:建筑物信息框模板|桥]]
[[Category:桥梁模板]]
[[Category:使用了分析程序的模板|{{PAGENAME}}]]
}}</includeonly>