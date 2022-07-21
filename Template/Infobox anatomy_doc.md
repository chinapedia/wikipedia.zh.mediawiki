{{Documentation subpage}}
<!-- Place categories where indicated at the bottom of this page and interwikis at Wikidata (see [[Wikipedia:Wikidata]]) -->
{{lua|Module:Check for unknown parameters}}

本文件為'''Template:Infobox anatomy'''的使用方法，使用此模板時，不必將所有資訊全部填滿才可以使用，任何一樣正確的資訊都相當重要。

== 用法 ==
當您的條目是有關解剖學的構造時，您可以將以下的文本複製到條目的最頂端：

<pre>
{{Infobox anatomy
| Name          = 
| Pronunciation = 
| Synonyms      = 
| Image         = 
| Caption       = 
| Width         = 
| Image2        = 
| Caption2      = 
| Width2        = 
| Latin         = 
| Greek         = 
| Precursor     = 
| System        = 
| Artery        = 
| Vein          = 
| Nerve         = 
| Lymph         = 
}}
</pre>

===基本参数===
{{Infobox anatomy/doc/transcludetable}}
所有的空格都是選填的，模板會依你的填入資訊而調整。

All fields are optional.  Field labels are case-sensitive.

* '''Name''': The title at top of infobox, which should usually match the name of page, and will default to this if it is not filled out.
* '''Image''' and '''Caption''': Up to two images can be included in the infobox.Ideally, the images should be appropriate and useful both to newcomers and to experts. To this end, try to pick a first image that helps orient the user to the region of the body, and pick one where the user doesn't need to click on the image to figure out where the structure is. Then, pick a second image that provides more detail. Alternatively, two images can show the same structure from two different angles. In either case, allowing the user to view more than one image, at the same time, allows them to better visualize the object of attention. Of course, there aren't perfect images for each article.
** If able, include useful information in the caption, such as a general orientation to where the structure is.
** '''Width''' is an optional parameter for the image width, in pixels (omit "px"). If the picture is far too big, then specify a custom width (in pixels) like this: {{para|width|325}}. When no Width parameter is specified, it defaults to a width of 190 pixels.
** [[:en:Help:Pictures#Image maps|Image maps]] can be included using the image parameter. For example: <pre> | Image = {{Inner ear map|Cochlea|Inline=1}}</pre>
** Only two images can be included in the infobox, but there is no restriction on the number of images on the article; other images can be placed in sections, or at the end in an "Additional images" section. 

;细节
Some fields are grouped together as "details", relating to the anatomy of a structure
* '''Precursor''': This refers to the embryological precursor from which the structure derives
* '''System''': Circulatory system, respiratory system, etc.
* '''Artery''': Arteries supplying the structure. Note that there may be more than one artery (as in the [[腎上腺]]). If there is not yet an article for the artery, consider also including a less specific artery that does have an article
* '''Vein''': Vein(s) draining the structure
* '''Nerve''': Nerve(s) to the structure
* '''Lymph''': Lymphatic drainage from the structure

;识别标示
Some fields visible to the reader are automatically inserted from [[维基数据]], and should be edited there. These are: [[解剖學術語|TA]], TE, TH, [[解剖学基础模型|FMA]] and [[医学主题词|MeSH]].

For terms and links that relate to how the structure is identified anatomically
* '''Latin''': Especially important to support interwikification. Good sources for the Latin are online medical dictionaries, such as [http://www.emedicine.com/asp/dictionary.asp?keyword=lung eMedicine],{{dead link|date=December 2012}} [http://www.stedmans.com/ Stedman's], and [http://www.mercksource.com/pp/us/cns/cns_hl_dorlands.jspzQzpgzEzzSzppdocszSzuszSzcommonzSzdorlandszSzdorlandzSzdmd-a-b-000zPzhtm Dorlands]. The letters "TA" stand for [[解剖學術語]], and it is the closest thing to an international naming standard presently in existence. If there are multiple Latin names available, put the TA first.
* '''Greek''': Refers to [[古希臘語]] and as with Latin, may be found in medical dictionaries. Use only where term is in wide use, and not the same as the Latin term, ''e.g.'', [[脾脏]]: Greek: ''σπλήν—splḗn'' ; Latin: ''lien''. Also useful when the Greek root is widely used, such as καρδία–kardía ; root of cardiac, cardiology etc.

;链接
All templates in this series provide a link to the relevant [[:en:Anatomical terminology]] articles, ''e.g.'', [[:en:Anatomical terms of bone]] for [[:Template:Infobox bone]], etc.

===参数===
{{TemplateData header}}
<templatedata>
{
	"params": {
		"Image": {
			"label": "图像",
			"description": "第一幅图像",
			"suggested": true
		},
		"Name": {
			"label": "名称",
			"description": "结构的中文名称",
			"suggested": true
		},
		"Width": {
			"label": "宽度",
			"description": "第一幅图像的宽度",
			"default": "250"
		},
		"Caption": {
			"label": "说明",
			"description": "第一幅图像的说明文字",
			"suggested": true
		},
		"Image2": {
			"label": "图像2",
			"description": "第二幅图像",
			"suggested": true
		},
		"Width2": {
			"label": "宽度2",
			"description": "第二幅图像的宽度",
			"default": "250"
		},
		"Caption2": {
			"label": "说明2",
			"description": "第二幅图像的说明文字",
			"suggested": true
		},
		"System": {
			"label": "系统",
			"description": "结构相关的机体系统",
			"example": "循环系统",
			"suggested": true
		},
		"Latin": {
			"label": "拉丁文",
			"description": "结构的拉丁文名称",
			"suggested": true
		},
		"Greek": {
			"label": "希腊文",
			"description": "结构的希腊文名称"
		},
		"Acronym": {
			"label": "缩写",
			"description": "结构名称的常用缩写"
		},
		"Precursor": {
			"label": "发育自"
		},
		"GivesRiseTo": {
			"label": "发育为"
		},
		"Artery": {
			"label": "动脉"
		},
		"Vein": {
			"label": "静脉"
		},
		"Nerve": {
			"label": "神经"
		},
		"Lymph": {
			"label": "淋巴"
		}
	},
	"paramOrder": [
		"Name",
		"Image",
		"Width",
		"Caption",
		"Image2",
		"Width2",
		"Caption2",
		"System",
		"Latin",
		"Greek",
		"Acronym",
		"Precursor",
		"GivesRiseTo",
		"Artery",
		"Vein",
		"Nerve",
		"Lymph"
	],
	"description": "解剖学信息框模板",
	"format": "block"
}
</templatedata>

== 相关模板 ==
{{collapse top|title=[[:Template:Infobox bone]]代码}}
<pre>
{{Infobox bone
| Name          = 
| synonyms      =
| Latin         = 
| Greek         =
| Image         = 
| Width         = 
| Caption       = 
| Image2        = 
| Width2        = 
| Caption2      = 
| System        = 
| Origins       = 
| Insertions    = 
| Articulations = 
| Precursor     = 
| Acronym       = 
| Pronunciation = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox artery]]代码}}
<pre>
{{Infobox artery
| Name        = 
| Latin       = 
| Image       = 
| Width       = 
| Caption     = 
| Image2      = 
| Width2      = 
| Caption2    = 
| BranchFrom  = 
| BranchTo    = 
| Vein        = 
| Precursor   = 
| Supplies    = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox vein]]代码}}
<pre>
{{Infobox vein
| Name        = 
| Latin       = 
| Image       = 
| Caption     = 
| Image2      = 
| Caption2    = 
| DrainsFrom  =
| DrainsTo    =
| Artery      = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox lymph]]代码}}
<pre>
{{Infobox lymph
| name          =
| image         =
| alt           =
| caption       =
| image2        =
| alt2          =
| caption2      =
| Latin         =
| drains_from   =
| source        =
| drains_to     =
| Acronym       = 
| Pronunciation = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox muscle]]代码}}
<pre>
{{Infobox muscle
| Name          = 
| Image         = 
| Width         = 
| Caption       = 
| Image2        = 
| Width2        = 
| Caption2      = 
| Latin         = 
| Greek         = 
| System        = 
| Origin        = 
| Insertion     = 
| Artery        = 
| Nerve         = 
| Vein          = 
| Action        = 
| Antagonist    = 
| Pronunciation = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox ligament]]代码}}
<pre>
{{Infobox ligament
| Name          = 
| Image         = 
| Caption       = 
| Image2        = 
| Caption2      = 
| Latin         = 
| From          = 
| To            = 
| Pronunciation = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox nerve]]代码}}
<pre>
{{Infobox nerve
| Name        = 
| Latin       = 
| Image       = 
| Caption     = 
| Image2      = 
| Caption2    = 
| Innervates  = 
| BranchFrom  = 
| BranchTo    = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox neuron]]代码}}
<pre>
{{Infobox neuron
| name             =  
| image            =  
| caption          =  
| location         =  
| function         =  
| neurotransmitter =
| morphology       = 
| afferents        = 
| efferents        = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox brain]]代码}}
<pre>
{{Infobox brain
| name            = 
| Latin           = 
| image           = 
| caption         = 
| image2          = 
| caption2        = 
| part_of         =
| components      =
| artery          = 
| vein            =
| acronym         =
| Function        = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox tract]]代码}}
<pre>
{{Infobox tract
| Name            = 
| Synonyms        =
| Latin           = 
| Image           = 
| Caption         = 
| Image2          = 
| Caption2        = 
| PartOf          =
| Components      =
| Acronym         =
| Function        = 
| Decussation     = 
| From            =
| To              = 
| System          = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox cell]]代码}}
<pre>
{{Infobox cell
| Name          = 
| Image         = 
| Caption       = 
| Image2        = 
| Caption2      = 
| System        =
| Precursor     =
| Function      =
| Pronunciation = 
| Location      =
| Acronym       = 
| Latin         = 
| Greek         = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox microanatomy]]代码}}
<pre>
{{Infobox microanatomy
| Name          = 
| Image         = 
| Caption       = 
| Image2        = 
| Caption2      = 
| System        =
| Precursor     =
| Function      =
| Pronunciation = 
| Location      =
| Acronym       = 
| Latin         = 
| Greek         = 
}}
</pre>
{{collapse bottom}}
{{collapse top|title=[[:Template:Infobox embryology]]代码}}
<pre>
{{Infobox embryology
| Name          = 
| Image         = 
| Width         = 
| Caption       = 
| Image2        = 
| Width2        = 
| Caption2      = 
| Latin         = 
| CarnegieStage = 
| Days          = 
| System        = 
| Precursor     = 
| GivesRiseTo   = 
| Acronym       = 
| Pronunciation =
}}
</pre>
{{collapse bottom}}

== 追踪分类 ==
* {{clc|使用過時參數的醫學信息模板}} (via [[Module:Check for unknown parameters]])
* {{clc|使用GraySubject或GrayPage參數的醫學信息框模板}}——参数信息已移至维基数据
* {{clc|使用Dorlands參數的醫學信息框模板}}——参数决定移除，请参考[[:en:Wikipedia_talk:WikiProject_Anatomy/Archive_11#Infobox_parameters_to_remove|WikiProject_Anatomy]]
* {{clc|使用BrainInfoType或BrainInfoNumber參數的醫學信息框模板}}——参数信息已移至维基数据
* {{clc|使用NeuroLex或NeuroLexID參數的醫學信息框模板}}——参数信息已移至维基数据
* {{clc|使用Mesh參數的醫學信息框模板}}——参数信息已移至维基数据
* {{clc|使用BamsSlug參數的醫學信息框模板}}——参数决定移除，请参考[[:en:Wikipedia_talk:WikiProject_Anatomy/Archive_11#Infobox_parameters_to_remove|WikiProject_Anatomy]]

<includeonly>{{#ifeq:{{SUBPAGENAME}}|sandbox | |
<!-- Categories below this line, interwikis at Wikidata -->
[[Category:解剖學信息框模板| ]]
[[Category:使用维基数据信息的模板]]
}}</includeonly>