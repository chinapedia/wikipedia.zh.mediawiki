<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->

}}</includeonly>

<includeonly><!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{Documentation subpage}}</noinclude>
<!-- Place categories where indicated at the bottom of this page and interwikis at Wikidata -->
<includeonly>{{esoteric}}</includeonly>

== 參數及使用方法 ==
此模板能在[[唱片公司]]條目中加入[[m:Infobox|信息框]]。模板代码应该位于页面的最上方，文章之前（参见：[[Wikipedia:格式手冊/序言章節]]），但要在消歧义提示之下（参见：[[Wikipedia:管理员不是什么]]）。

== 範例 ==
如果你已知哪些字段该填写哪个，下面这个空白示例可以直接复制粘贴到你的文章并立刻填充内容，不必去删除备注。
{{Parameter names manual
| name | image | image_name | image_size | image_alt | caption | parent | founded | defunct | founder | status | distributor | genre | country | location | website
}}

=== 字段 ===

所有的字段均为可选填（不填写不会引起显示错误），但推荐您去填写尽量多的又来源的信息，特别是<code>founded</code> 和<code>country</code>两个字段。空白的<nowiki>{{Infobox record label}}</nowiki> 只会生成文章名的蓝色标题。

; name : （默认为文章名）显示在信息框标题出的厂牌名。
; image : 厂牌徽标，如<code>LABEL-LOGO.jpg</code>。
; image_size: 推荐100到200像素的宽度，基于照片的竖向或横向长度，默认为180像素。
; image_alt : [[Wikipedia:圖像的替代文字|描述图像的替代文字]]。
; caption : 图片的说明。
; parent : 母公司，如<code><nowiki>[[華納音樂集團]]</nowiki></code>。
; founded : 4位数建立年份，使用{{Tl|Start date}}。
; founder : 创立者，使用逗号或者<code><nowiki><br /></nowiki></code>分开。
; defunct : 4位数停业年份，使用{{tl|end date}}。
; status : 除了<code>Inactive</code>（不活跃）情况之外，均留空。
; distributor : 发行者者，使用逗号或者<code><nowiki><br /></nowiki></code>分开。
; genre : <code>比如<nowiki>[[World music|World]]</nowiki></code>或者<code>Various</code>，使用逗号或者<code><nowiki><br /></nowiki></code>分开。 .
; country : 起源地区，如<code><nowiki>U.S.</nowiki></code> 或者 <code><nowiki>{{Flag|土耳其}}</nowiki></code>.
; location : 总部所在国家及地区。
; website {{nobold|or}} url : 使用<nowiki>{{[[Template:URL|URL}}</nowiki>来指向唱片公司的官方网站，如： <br /> <code><nowiki>{{URL|www.atlanticrecords.com}}</nowiki></code> （简洁版） <br /> <code><nowiki>{{URL|www.kalan.com/english/scripts|Kalan.com}}</nowiki></code> （完整版）

Additional field not provided by default:

; bgcolor : （以弃用，默认为"{{Colors|black|LightBlue|LightBlue}}"）资料框标题背景色，除非有合理需要否则不应使用。

== 示例 ==

{{Infobox record label <!-- See Wikipedia:WikiProject_Music -->
| name        = Republic Records
| image_name  = Wikipedia-logo-v2-en.svg
| image_size  = 100px
| parent      = [[Universal Music Group]]
| founded     = {{Start date|1995}}
| founder     = {{ubl| [[Monte Lipman]] | Avery Lipman }}
| distributor = {{ubl| Universal Music Group (Worldwide) | [[Virgin EMI Records]] (in the UK) }}
| genre       = Various
| country     = United States
| location    = New York City
| website     = {{URL|www.republicrecords.com}}
}}

<pre style="overflow:auto">
{{Infobox record label <!-- See Wikipedia:WikiProject_Music -->
| name        = Republic Records
| image_name  = Wikipedia-logo-v2-en.svg
| image_size  = 100px
| parent      = [[Universal Music Group]]
| founded     = {{Start date|1995}}
| founder     = {{ubl| [[Monte Lipman]] | Avery Lipman }}
| distributor = {{ubl| Universal Music Group (Worldwide) | [[Virgin EMI Records]] (in the UK) }}
| genre       = Various
| country     = United States
| location    = New York City
| website     = {{URL|www.republicrecords.com}}
}}
</pre>

上方代码即为右侧信息框的源码。

* 由于合理使用的限制，实际徽标不应显示在此文档页面上（只能用于阐述有关其的文章）。此处维基百科的图像是用于阐述如何使用徽标的。 
* 请注意在<code>distributor</code>字段，你可以在 <code><nowiki><br /></nowiki></code>的中间隐藏新一行以换行。这么做并非必须 （<code>founder</code> 字段并不使用），且版本不影响输出信息，但可以使得在长分项内容中的维基代码更有可读及可修改性。
* 这里删除了两项字段：<code>image_bg</code> （因为默认色是白色）和<code>status</code> （因为此公司既不为非活跃状态也非停业，而且并近期没有必要使用此字段的迹象）。

{{Clear}}<!--PREVENTS INFOBOX OVERFLOWING NEXT SECTION-->

== 分类 ==

此模板不创建任何文章的自动分类。你需要自己添加你的文章到相关的分类，以下是推荐的分类（和它们的子分类）：

* [[:Category:各國唱片公司]]

== 微格式 ==
{{UF-hcard-org}}

== 参见 ==
<!-- self-listing for quick access on edit history -->

* {{Lts|{{BASEPAGENAME}}}}
* <!-- links to relevant pages -->
* {{Lts|Infobox album}}
* {{Lts|Infobox musical artist}}
** 为独立艺术家或乐队所打造。

== 模板数据 ==
{{collapse top|TemplateData}}
{{TemplateData header}}
<templatedata>
{
	"params": {
		"bgcolor": {
			"label": "Background color",
			"description": "Used to change the background color. It is not required and recommended UNLESS a logical and justified reason is given.",
			"type": "string",
			"default": "LightBlue."
		},
		"name": {
			"label": "Name",
			"description": "The name of the record label. Must not be linked or formatted. ",
			"example": "ex. Modular Recordings",
			"type": "string",
			"required": true
		},
		"image": {
			"label": "Image",
			"description": "The logo image for the record label."
		},
		"image_size": {
			"label": "Image size",
			"description": "The size of the image. \"px\" must not be added; only the numerical value given.",
			"example": "ex. 64",
			"default": "100px"
		},
		"image_alt": {
			"label": "Image alternative text",
			"description": "The alternative text used to describe the image given for visually-impaired readers.",
			"type": "string"
		},
		"caption": {
			"label": "Image caption",
			"description": "A caption for the image.",
			"example": "Ex. The official logo for Big Beat Records.",
			"type": "string"
		},
		"parent": {
			"label": "Parent company",
			"description": "The parent company that owns the record label. Must be linked and have its own separate article.",
			"example": "ex. [[Sony Music Entertainment]]",
			"type": "string"
		},
		"founded": {
			"label": "Founded",
			"description": "The foundation year in which the record label was established. Must only be the year and must use the {{start date and age}} if possible.",
			"example": "ex. {{start date and age|1887}}",
			"type": "string",
			"suggested": true
		},
		"defunct": {
			"label": "Defunct",
			"description": "The year in which the record company was officially dissolved. Must have the {{end date}} template.",
			"example": "ex. {{end date|1953}}"
		},
		"founder": {
			"label": "Founder",
			"description": "The person or people who founded the company. If possible, must be linked to its article.",
			"example": "ex. Pete Doraine",
			"type": "string"
		},
		"status": {
			"label": "Status",
			"description": "The current status of the company.",
			"deprecated": "According to the documentation: \" The company is neither inactive nor defunct, and currently unlikely to require the field in the near future.\" DO NOT USE"
		},
		"distributor": {
			"label": "Distributor",
			"description": "The company or companies that distribute the licensed work of the company. If possible, must be linked to its article.",
			"example": "ex. Sony Music",
			"type": "string"
		},
		"genre": {
			"label": "Genre",
			"description": "The genre(s) that are most common for the record label. Must be used with the {{hlist}} template if there are more than one.",
			"example": "ex. {{hlist|[[Rock music|Rock]]|[[electronica]]|[[electropop]]|[[neo-psychedelia]]|[[psychedelic rock]]}}",
			"type": "string",
			"suggested": true
		},
		"country": {
			"label": "Country of origin",
			"description": "The record label's country of origin, where it is headquartered. The country MUST NOT be linked.",
			"example": "ex. Japan",
			"type": "string"
		},
		"location": {
			"label": "Location",
			"description": "The official city in which the record label is headquartered in it's country of origin. The exact address is NOT ALLOWED as only the city is.",
			"example": "ex. [[Dortmund]]",
			"type": "string"
		},
		"url": {
			"label": "Website",
			"description": "The official website for the record label. It must be used in accordance with the {{URL}} template so as to be printer-friendly.",
			"example": "ex. {{URL|defjam.com}}",
			"type": "string"
		}
	},
	"description": "An infobox used to describe a record label, it's general and corporate information, as well as location and official website.",
	"format": "block"
}
</templatedata>
{{collapse bottom}}

{{Organization infoboxes}}
<includeonly>{{Sandbox other||<!-- 本行下加入模板的分類 -->
[[Category:音樂信息框模板|Record label]]
[[Category:企業信息框模板|Record label]]
[[Category:唱片公司|*<!--STAR-->Infobox record label]]
}}</includeonly>