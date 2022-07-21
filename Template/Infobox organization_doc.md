<noinclude>{{Documentation subpage}}</noinclude>
{{High-use|2461}}
<!-- 请在此线下编辑模板说明文档 -->
{{Esoteric}}
__TOC__
== 模板作用 ==
{{tl|Infobox organization}}是供[[:Category:组织|组织类条目]]使用的信息框模板。

== 使用方法 ==
{{Parameter names example |_display=italics
 |name |full_name |native_name |native_name_lang=es
 |image={{{image}}} |image_size={{{image_size}}} |alt={{{alt}}} |caption
 |logo={{{logo}}} |logo_size={{{logo_size}}} |logo_alt={{{logo_alt}}} |logo_caption
 |map={{{map}}} |map_size={{{map_size}}} |map_alt={{{map_alt}}} |map_caption |map2={{{map2}}} |map2_size={{{map2_size}}} |map2_alt={{{map2_alt}}} |map2_caption
 |abbreviation |nickname |pronounce={{{pronounce}}}&nbsp; |pronounce ref |pronounce comment |pronounce 2 |named_after |motto |predecessor |merged |successor |formation |founder=''founder''&nbsp;{{\}}&nbsp;''founders'' |founding_location
 |dissolved=''dissolved''&nbsp;{{\}}&nbsp;''defunct'' |merger |type |tax_id=''tax_id''&nbsp;{{\}}&nbsp;''vat_id''
 |registration_id |status |purpose |professional_title |headquarters |location_city |location_country |location_city2 |location_country2 |addnl_location_city |addnl_location_country |addnl_location_city2 |addnl_location_country2 |coordinates |origins |region_served=''region_served''&nbsp;{{\}}&nbsp;''region''&nbsp;{{\}}&nbsp;''area_served'' |products=''products''&nbsp;{{\}}&nbsp;''product'' |services |methods=''methods''&nbsp;{{\}}&nbsp;''method'' |fields=''fields''&nbsp;{{\}}&nbsp;''field''
 |membership |membership_year=''_year'' |language =''language''&nbsp;{{\}}&nbsp;''languages'' |owner=''owner''&nbsp;{{\}}&nbsp;''owners'' |sec_gen=''sec_gen''&nbsp;{{\}}&nbsp;''gen_sec''
 |leader_title |leader_name |leader_title2 |leader_name2 |leader_title3 |leader_name3 |leader_title4 |leader_name4
 |board_of_directors |key_people |main_organ =''main_organ''&nbsp;{{\}}&nbsp;''publication'' |parent_organization=''parent_organization''&nbsp;{{\}}&nbsp;''parent_organisation'' |subsidiaries |secessions |affiliations
 |budget |budget_year=''_year'' |revenue |revenue_year=''_year'' |disbursements |expenses |expenses_year=''_year'' |endowment |endowment_year=''_year''
 |staff |staff_year=''_year'' |volunteers |volunteers_year=''_year''
 |students |students_year=''_year''
 |awards |website=<code><nowiki>{{URL|...}}</nowiki></code> |remarks |formerly=''formerly''&nbsp;{{\}}&nbsp;''former_name'' |footnotes |bodystyle
}}
使用时直接将下面的代码复制到文档中，填充相应数据即可，除组织名称外，其余参数都为可选项。请注意参数名首字母是小写的，这是因为本模板直接使用这些参数生成[[hCard]][[微格式]]。

<pre>
{{Infobox organization
|name = <!-- 名称，必需 -->
|original_name = <!-- 原始名称，如果该组织名称非中文，而上一个参数写的是中文时，用来补充说明 -->
|image = <!-- 组织标记图片 -->
|image_border = <!-- 另一个图片，用于分隔上一个参数中图片和下面各项参数 -->
|size = <!-- 图片宽度，默认值：200px -->
|border = <!-- 图片边框，yes为有，默认为无 -->
|caption = <!-- 图片标题 -->
|map = <!-- 地图图片 -->
|msize = <!-- 地图宽度，默认值：250px -->
|mcaption = <!-- 地图标题 -->
|abbreviation = <!-- 简称 -->
|motto = <!-- 组织宣言 -->
|formation = <!-- 成立时间 -->
|founder = <!-- 创始人 -->
|extinction = <!-- 解散时间 -->
|type = <!-- 组织类型（如：政府机构，[[非政府组织]]，政府间国际组织等） -->
|status = <!-- 地位（如：临时机构，特别机构，协会，基金会，隸屬層級等） -->
|purpose = <!-- 组织目標（如：保护环境，促进贸易等） -->
|headquarters = <!-- 总部地点 -->
|location = <!-- 组织所在地 -->
|region_served = <!-- 服务区域 -->
|membership = <!-- 會員數 -->
|language = <!-- 工作语言 -->
|leader_title = <!-- 领导人职位名称（如：主席，秘书长等） -->
|leader_name = <!-- 领导人姓名 -->
|main_organ = <!-- 主要运行机构（如：董事会，办公室等） -->
|parent_organization = <!-- 上级组织 -->
|affiliations = <!-- 附属或分支组织 -->
|num_staff = <!-- 雇员人数 -->
|num_volunteers = <!-- 志愿者人数 -->
|budget = <!-- 预算 -->
|website = <!-- 网站 -->
|remarks = <!-- 注释 -->
}}</pre>

空白模板：

<pre>
{{Infobox organization
| name                = <!-- defaults to {{PAGENAME}}, if not provided -->
| full_name           = 
| native_name         = <!-- organization's name in its local language -->
| native_name_lang    = <!-- required ISO 639-1 code of the above native language -->
| logo                = 
| logo_size           = 
| logo_alt            = 
| logo_caption        = 
| image               = 
| image_size          = 
| alt                 = <!-- see [[WP:ALT]] -->
| caption             = 
| map                 = <!-- map image -->
| map_size            = <!-- defaults to 250px -->
| map_alt             = 
| map_caption         = 
| map2                = <!-- 2nd map image, if required -->
| map2_size           = 
| map2_alt            = 
| map2_caption        = 
| abbreviation        = 
| nickname            = 
| pronounce           = 
| pronounce ref       = 
| pronounce comment   = 
| pronounce 2         = 
| named_after         = 
| motto               = 
| predecessor         = 
| merged              = <!-- any other organization(s) which it was merged into -->
| successor           = 
| formation           = <!-- or |established = --><!-- use {{start date and age|YYYY|MM|DD}} -->
| founder             = <!-- or |founders = -->
| founding_location   = 
| dissolved           = <!-- or |defunct = --><!-- use {{end date and age|YYYY|MM|DD}} -->
| merger              = <!-- other organizations (if any) merged with, to constitute the new organization -->
| type                = <!-- e.g., [[Nonprofit organization|Nonprofit]], [[Non-governmental organization|NGO]], etc. -->
| tax_id              = <!-- or |vat_id = (for European organizations) -->
| registration_id     = <!-- for non-profits -->
| status              = <!-- legal status or description (company, charity, foundation, etc.) -->
| purpose             = <!-- or |focus = --><!-- humanitarian, activism, peacekeeping, etc. -->
| professional_title  = <!-- for professional associations -->
| headquarters        = 
| location_city       = 
| location_country    = 
| location_city2      = 
| location_country2   = 
| addnl_location_city = 
| addnl_location_country = 
| addnl_location_city2 = 
| addnl_location_country2 = 
| coordinates         = <!-- {{coord|LAT|LON|display=inline,title}} -->
| origins             = 
| region_served       = <!-- or |area_served = or |region = -->
| products            = <!-- or |product = -->
| services            = 
| methods             = <!-- or |method = -->
| fields              = <!-- or |field = -->
| membership          = <!-- number of members -->
| membership_year     = <!-- year to which membership numbers/data apply -->
| language            = <!-- or |languages = --><!-- any official language or languages used -->
| owner               = <!-- or |owners = -->
| sec_gen             = <!-- or |gen_sec for General Secretary -->
| leader_title        = <!-- defaults to "Leader" -->
| leader_name         = 
| leader_title2       = 
| leader_name2        = 
| leader_title3       = 
| leader_name3        = 
| leader_title4       = 
| leader_name4        = 
| board_of_directors  = 
| key_people          = 
| main_organ          = <!-- or |publication = --><!-- organization's principal body (assembly, committee, board, etc.) or publication -->
| parent_organization = <!-- or |parent_organisation = -->
| subsidiaries        = 
| secessions          = 
| affiliations        = 
| budget              = 
| budget_year         = 
| revenue             = 
| revenue_year        = 
| disbursements       = 
| expenses            = 
| expenses_year       = 
| endowment           = 
| endowment_year      = 
| funding             = <!-- source of funding e.g. for "think tanks" -->
| staff               = 
| staff_year          = 
| volunteers          = 
| volunteers_year     = 
| students            = 
| students_year       = 
| awards              = 
| website             = <!-- {{URL|example.com}} -->
| remarks             = 
| formerly            = <!-- or |former_name = -->
| footnotes           = 
| bodystyle           = 
}}
</pre>

{{Organization infoboxes}}
<includeonly>{{Sandbox other||<!-- 本行下加入模板的分類 -->
[[Category:组织机构信息框模板| ]]
}}</includeonly>