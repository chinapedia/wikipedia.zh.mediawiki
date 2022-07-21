{{documentation subpage}}
{{high-use|3123}}
{{Intricate template}}
{{Lua|Module:Infobox|Module:InfoboxImage|Module:String|Module:Check for unknown parameters}}
{{Uses Wikidata|P275|P408|P856|P1324}}

== 用法 ==
选择性地複製以下空白原始碼，并将其放在軟體條目頁面的頂端。
{{Parameter names example|_template=|name|logo|logo alt|logo caption|screenshot|screenshot size|screenshot alt|caption|author|developer|released|latest release version|latest release date|latest preview version|latest preview date|programming language|engine|operating system|platform|included with|size|language count|language|language footnote|genre|license|alexa|website|repo|standard|AsOf| other_names |replaces | replaced_by | service_name }}

<syntaxhighlight lang="html" style="overflow: auto;">
{{Infobox software
| name                   = 
| logo                   = <!-- 只填图片名 -->
| logo alt               = 
| logo caption           = 
| screenshot             = <!-- 只填图片名 -->
| screenshot-hans        = <!-- 圖片分為簡繁兩版時，填寫簡體版圖片名 -->
| screenshot-hant        = <!-- 圖片分為繁簡兩版時，填寫繁體版圖片名 -->
| screenshot size        =
| screenshot alt         = 
| caption                = 
| collapsible            = <!-- 填写任意文本均会折叠截图 -->
| author                 = 
| developer              = 
| released               = <!-- {{Start date and age|YYYY|MM|DD|df=yes}} -->
| discontinued           = <!-- 如果软件已停止开发，设为yes，其他文本均会被忽略 -->
| ver layout             = <!-- simple（默认）或 stacked -->
| latest release version = <!-- 若Wikidata有机器人自动维护版本号数据，可使用{{LSR/wikidata}}，并将latest release date留空 -->
| latest release date    = <!-- {{Start date and age|YYYY|MM|DD}} -->
| latest preview version = 
| latest preview date    = <!-- {{Start date and age|YYYY|MM|DD}} -->
| repo                   = <!-- {{URL|example.org}} 如果留空，会自动从wikidata填充 -->
| programming language   = 
| engine                 = <!-- 或 engines 如果留空，会自动从wikidata填充-->
| operating system       = 
| platform               = 
| included with          = 
| size                   = 
| language               = 
| language count         = <!-- 仅数字 -->
| language footnote      = 
| genre                  = 
| license                = <!-- 如果留空，会自动从wikidata填充 -->
| alexa                  = 
| website                = <!-- {{URL|example.org}} 如果留空，会自动从wikidata填充 -->
| standard               = 
| AsOf                   = 
}}
</syntaxhighlight>
{{Clear}}

== 範例 ==
{{Infobox software
| name                   = Example: Yoyodyne
| logo                   = 
| screenshot             = [[File:Yoyo patent 1866.png|200px]]
| caption                = Yoyodyne v0.9 截圖
| developer              = Yoyodyne Industries Inc.
| released               = {{Start date and age|1911}}
| latest release version = 0.9
| latest release date    = {{Start date and age|2006|01|01}}
| latest preview version = 
| latest preview date    = 
| operating system       = [[Unix-like]]
| operating system desc  = 
| size                   = 25&nbsp;[[Megabyte|MB]]
| genre                  = Yoyonics
| license                = [[GNU General Public License]]
| website                = {{URL|www.example.org}}
}}

<pre style="overflow:auto;">
{{Infobox Software
| name                   = Example: Yoyodyne
| logo                   = 
| screenshot             = [[File:Yoyo patent 1866.png|200px]]
| caption                = Yoyodyne v0.9 screenshot
| developer              = Yoyodyne Industries Inc.
| released               = {{Start date|1911}}
| latest release version = 0.9
| latest release date    = {{Start date and age|2006|01|01}}
| latest preview version = 
| latest preview date    = 
| operating system       = [[Unix-like]]
| operating system desc  = 
| size                   = 25&nbsp;[[Megabyte|MB]]
| genre                  = Yoyonics
| license                = [[GNU General Public License]]
| website                = {{URL|www.example.org}}
}}
</pre>

== 參數 ==
{| class="wikitable"
! 參數
! {{nowrap|選填}}
! 描述
|-
| '''name'''
| {{no}}
| 軟體的名稱，中文名稱優先。注意：请谨慎填写此项<!-- ，因为<code>frequently updated</code>参数可能用到它 -->。
|-
| '''name_ol'''
| {{yes}}
| 軟體的其他名稱（如英文名稱，必须是'''官方'''名稱）
|-
| '''logo'''
| {{yes}}
| 軟體的[[标志]]或[[图标]]（默认宽度设置为64像素，可用{{Para|logo_size}}调整尺寸，{{Para|logo_caption}}、{{Para|logo_alt}}补充说明）
|-
| '''screenshot'''
| {{yes}}
| 屏幕截圖（默认宽度设置为300像素，可用{{Para|screenshot_size}}调整尺寸，{{Para|screenshot_caption}}、{{Para|screenshot_alt}}补充说明）
|-
| '''collapsible'''
| {{yes}}
| 遇到較長垂直截圖的情況下，可以設置為「yes」（可參考[[百度Hi]]例子）
|-
| '''author'''
| {{yes}}
| 軟體的原作者
|-
| '''developer'''
| {{yes}}
| 軟體的開發商
|-
| '''released'''
| {{yes}}
| 1.0版本的發佈日期（或最初版的發佈日期），之後的版本號碼用 <code>latest release date</code>。
|-
| '''ver layout'''
| {{yes}}
| 軟體版本號的顯示方式，遇到多個平臺版本號碼不同的情況時填寫「stacked」，否則填寫「simple」。填寫「stacked」還會生成編輯連結。
|-
| '''latest release version'''
| {{yes}}
| 該程式最新的穩定版本號碼
|-
| '''latest release date'''
| {{yes}}
| 該程式最新的穩定版本的發佈日期 
|-
| '''latest preview version'''
| {{yes}}
| 該程式最新的預覽版本號碼
|-
| '''latest preview date'''
| {{yes}}
| 該程式最新的預覽版本的發佈日期 
|-
| '''programming language'''
| {{yes}}
| 開發的程式語言
|-
| '''operating system'''
| {{no}}
| 软件工作于何[[操作系统]]。请尽可能详细地填写，并避免“[[跨平台]]”之类的表述。例如：
*如果是[[Unix]]、[[Linux]]之类的作業系統，请填写：
**<code><nowiki>[[Unix-like]]</nowiki></code>
*如果是[[Microsoft Windows]]的所有版本，请填写
**<code><nowiki>[[Microsoft Windows]]</nowiki></code>
*如果是不同家族的不同操作系统，可以选择性地将部分列出，并以“等”字结尾，同时在条目中具体叙述。
|-
| '''platform'''
| {{yes}}
| 软件运行于何[[系统平台]]。可以填写以下方面的信息：
* 处理器架构
* 软件框架
|-
| '''engine'''
| {{yes}}
| 軟體引擎
|-
| '''size'''
| {{yes}}
| 软件安装包的大小，仅适用于通过网络下载的软件，不适用于盒装发售的软件。在填写时请注意标明单位，如[[千字节|KB]]、[[百万字节|MB]]和[[吉字节|GB]]。
|-
| '''language'''
| {{yes}}
| 软件的用户界面所采用之自然語言（中文、英文、法文等）。应尽量避免“多语言”之类的模糊表述，除非语言确实过多。
|-
| '''genre'''
| {{no}}
| 程式的種類。应该被链接至条目，如[[地理信息系统]]。
|-
| '''license'''
| {{no}}
| 软件的购买者需依据何种許可協議使用该软件。可以下面两种方式填写：
*填写软件的类型，如：
** [[专有软件]]
** [[免費軟體]]
** [[自由软件]]
*填写授权方案，如：
** [[GNU通用公共许可证]]
** [[BSD许可证]]
|-
| '''repo'''
| {{no}}
| 軟體[[仓库 (版本控制)|代码库]]的網址。
|-
| '''website'''
| {{no}}
| 軟體包的網址。
|}

=== 微格式 ===
{{UF-hcal}}

=== TemplateData ===
{{TemplateDataHeader}}

<templatedata>
{
	"description": "在计算机软件中使用的信息框。",
	"params": {
		"title": {
			"label": "title",
			"description": "软件标题。若未指定，则使用‘name’参数或 PAGENAME。该参数应该是普通文本，即不包含内部链接、超链接或图像。",
			"type": "string/line",
			"required": false
		},
		"name": {
			"label": "name",
			"description": "标题未指定时使用的名称。内部也与 Template:Latest stable software release/'name' 联合使用。该参数应该是普通文本，即不包含内部链接、超链接或图像。",
			"default": "PAGENAME",
			"type": "string/line",
			"required": false
		},
		"logo": {
			"label": "logo",
			"description": "图像的文件名，如‘File:The GIMP icon - gnome.svg’",
			"type": "wiki-page-name",
			"required": false
		},
		"logo_size": {
			"label": "logo_size",
			"description": "标志的尺寸。",
			"default": "64px",
			"type": "string/line",
			"required": false
		},
		"logo_alt": {
			"label": "logo_alt",
			"description": "标志的替代文本。",
			"type": "string/line",
			"required": false
		},
		"logo caption": {
			"label": "logo caption",
			"description": "标志的标题。如果只是简单的‘X 的标志’，那么直接留空更好。保留用于特殊情况，如说明一些必要的情况或用于插入 {{ffdc}}  或 {{deletable image-caption}}。",
			"type": "string",
			"required": false
		},
		"screenshot": {
			"label": "screenshot",
			"description": "截图的文件名",
			"type": "wiki-page-name",
			"required": false,
			"example": "GIMP_screenshot.png"
		},
		"screenshot_size": {
			"label": "screenshot_size",
			"description": "截图的尺寸",
			"default": "300px",
			"type": "string",
			"required": false
		},
		"screenshot_alt": {
			"label": "screenshot_alt",
			"description": "截图的替代文本",
			"type": "string",
			"required": false
		},
		"caption": {
			"label": "caption",
			"description": "截图的标题。",
			"type": "string",
			"required": false
		},
		"collapsible": {
			"label": "collapsible",
			"description": "当本截图默认隐藏时，设为‘yes’以在可折叠区域中显示截图",
			"type": "string/line",
			"required": false
		},
		"author": {
			"label": "author",
			"description": "软件的原始作者或发布者名。可以是个人或组织机构名。多数情况下指定了开发者字段后才会用到该参数。",
			"type": "string",
			"required": false
		},
		"developer": {
			"label": "developer",
			"description": "软件目前的开发者名。可以是个人或组织机构名称。",
			"type": "string",
			"required": false
		},
		"released": {
			"label": "released",
			"description": "在软件开发到正式发布（RTM）阶段时发布 1.0 版本（或最接近版本）的日期。如果条目是有关某个主流版本的内容（如 Internet Explorer 8 或 Microsoft Office 2007），则该字段应包含该主流版本正式发布（即到达 RTM 阶段）的日期。如果软件仍在开发中且尚未正式发布，请忽略该字段，即不要使用该字段指定首个预览版或测试版的发布日期，因为已经存在该用途的参数。该字段的格式应类似：{{Start date and age|year|month|day}}。如果条目使用 DMY 的日期格式，请相应替换为：{{Start date and age|year|month|day|df=yes}} 。如果您不确定日期格式，请参考 WP:MOSDATES。",
			"type": "string",
			"required": false
		},
		"discontinued": {
			"label": "discontinued",
			"description": "软件不再开发时，把信息框中的‘Latestrelease’字段设为‘Discontinued’。由于技术原因，该参数中使用任意内容也具有相同效果，如‘yes’、‘no’或其他。要取消此参数，把它去除就行了。",
			"type": "string",
			"required": false
		},
		"ver layout": {
			"label": "ver layout",
			"description": "软件版本号的显示方式，有 simple 和 stacked 两种选项。",
			"type": "string",
			"aliases": [
				"ver layout"
			],
			"required": false
		},
		"latest release version": {
			"label": "latest release version",
			"description": "该软件最新发布的版本号，如‘v1.5’、‘2008 (v12.2)’",
			"type": "string",
			"aliases": [
				"latest_release_version"
			],
			"required": false
		},
		"latest release date": {
			"label": "latest release date",
			"description": "最新版本的发布日期。如果软件首次发布后尚未更新，请忽略该字段，填写 released 字段就够了。该字段的格式应类似：{{Start date and age|year|month|day}}",
			"type": "string",
			"aliases": [
				"latest_release_date"
			],
			"required": false
		},
		"latest preview version": {
			"label": "latest preview version",
			"description": "最新预览版或开发分支的版本号。只有在软件的新版本（比 latest release version 中更新的版本）在开发中才应使用。请参考上面 latest release version 中的说明以更好理解该参数的含义。",
			"type": "string",
			"aliases": [
				"latest_preview_version"
			],
			"required": false
		},
		"latest preview date": {
			"label": "latest preview date",
			"description": "最新预览版或开发分支的发布日期。只有在软件的新版本（比 latest release version 中更新的版本）在开发中才应使用。请参考上面 latest release version 中的说明以更好理解该参数的含义。",
			"type": "string",
			"aliases": [
				"latest_preview_date"
			],
			"required": false
		},
		"programming language": {
			"label": "programming language",
			"description": "编写软件的语言。如果该语言在维基百科中有相应条目，请加上链接，如 [[C++]]、[[Python]]。",
			"type": "string",
			"aliases": [
				"programming_language"
			],
			"required": false
		},
		"operating system": {
			"label": "operating system",
			"description": "软件适用的操作系统。请尽可能准确指明（同时也注意长度）、避免模糊的表达，如跨平台、多平台。对于可运行于 unix/linux 所有版本的软件可使用‘[[Unix-like]]’，对于适用 Windows 平台的则可使用‘[[Microsoft Windows]]’、‘[[Windows]]’或‘[[Windows XP]] 及更高版本’。如果软件是与操作系统无关的网页程序，则忽略此参数。",
			"type": "string",
			"aliases": [
				"operating_system"
			],
			"required": false
		},
		"platform": {
			"label": "platform",
			"description": "软件运行的计算平台。可以指定处理器，如‘[[IA-32]]’（i386）、‘[[x86-64]]’、‘Itanium’、‘ARM’或‘MIPS’。",
			"type": "string",
			"required": false
		},
		"size": {
			"label": "size",
			"description": "安装包大小。只适用于可下载的软件。如‘{{Nowrap|48 MB}}’。",
			"type": "string",
			"required": false
		},
		"language": {
			"label": "language",
			"description": "软件用户界面支持的自然语言列表。不要使用‘多语言’或类似的模糊说法。",
			"type": "string",
			"required": false
		},
		"language count": {
			"label": "language count",
			"description": "软件用户界面支持的自然语言数。",
			"type": "number",
			"required": false
		},
		"language footnote": {
			"label": "language footnote",
			"description": "该参数用于提供可用翻译的引文。",
			"type": "string",
			"required": false
		},
		"genre": {
			"label": "genre",
			"description": "程序类型。应该内部链接到其他条目，如‘[[桌面搜索]]’。更多信息请参考软件分类列表。",
			"type": "wiki-page-name",
			"required": false
		},
		"license": {
			"label": "license",
			"description": "允许消费者使用软件的许可证类型。如‘[[专有软件|专有]] [[商业软件]]’、‘[[免费软件]]’、‘[[自由软件]]’、‘[[GNU通用公共许可证]]’、‘[[GNU宽通用公共许可证]]’、‘[[BSD许可证]]’。",
			"type": "string",
			"required": false
		},
		"licence": {
			"label": "licence",
			"description": "Alternative to license for articles using Commonwealth English.",
			"type": "string",
			"required": false
		},
		"alexa": {
			"label": "alexa",
			"description": "网站的当前 Alexa 排名。请参阅主文档了解自动更新的细节。",
			"type": "string",
			"required": false
		},
		"repo": {
			"label": "repo",
			"description": "软件[[仓库 (版本控制)|代码库]]的網址。格式：{{URL|http://www.example.com/repo}}。",
			"type": "string",
			"required": false
		},
		"website": {
			"label": "website",
			"description": "软件包网站的网址。格式：{{URL|http://www.example.com}}。",
			"type": "string",
			"required": false
		},
		"standard": {
			"label": "standard",
			"description": "软件的技术标准。",
			"type": "string",
			"required": false
		},
		"AsOf": {
			"label": "AsOf",
			"description": "Month Year.",
			"type": "string",
			"required": false
		},
		"bodystyle": {
			"label": "bodystyle",
			"description": "应用于信息框整体的 CSS 样式",
			"type": "string",
			"required": false
		},
		"screenshot-hans": {
			"label": "screenshot-hans",
			"description": "简体版截图的文件名",
			"example": "GIMP_screenshot_(zh-hans).png",
			"type": "wiki-file-name"
		},
		"screenshot-hant": {
			"label": "screenshot-hant",
			"description": "繁体版截图的文件名",
			"example": "GIMP_screenshot_(zh-hant).png",
			"type": "wiki-file-name"
		}
	},
	"format": "block",
	"paramOrder": [
		"title",
		"name",
		"logo",
		"logo_size",
		"logo_alt",
		"logo caption",
		"screenshot",
		"screenshot-hans",
		"screenshot-hant",
		"screenshot_size",
		"screenshot_alt",
		"caption",
		"collapsible",
		"author",
		"developer",
		"released",
		"discontinued",
		"ver layout",
		"latest release version",
		"latest release date",
		"latest preview version",
		"latest preview date",
		"programming language",
		"operating system",
		"platform",
		"size",
		"language",
		"language count",
		"language footnote",
		"genre",
		"license",
		"licence",
		"alexa",
		"repo",
		"website",
		"standard",
		"AsOf",
		"bodystyle"
	]
}
</templatedata>

== 微格式 ==
{{UF-hcal}}

== 追踪模板 ==
* {{clc|使用未知软件信息框参数的页面}}

== 參見 ==
* {{tl|Infobox OS}}：操作系統專用
* {{tl|Infobox VG}}：電子遊戲專用

== 參考 ==
<references />

<includeonly>
<!-- ADD CATEGORIES BELOW THIS LINE -->
[[Category:软件信息框模板|{{PAGENAME}}]]
</includeonly>