{{Documentation subpage}}
<!-----------------------------------------------------------------------------
     Place categories where indicated at the bottom of this page, please!
 ------------------------------------------------------------------------------>
{{tl|Template category}}应该放置于归类模板页面及相关子页面的分类的顶端。

{{TOC limit|3}}

==用法==

===完整语法===
<pre style="overflow:auto;">
{{Template category
| type = 
| topic = 
| description = 
| rhs = 
| container = 
| help = 
}}
</pre>

===参数===
本模板可以不设参数直接使用，即使用代码<code><nowiki>{{Template category}}</nowiki></code>。
{{Hidden begin |showhide=left |title=不设参数 |bodystyle=font-size:105%;}}
{{Template category}}
{{Hidden end}}

下面是可用于使本模板提供更多实用信息的参数：

====''type''====
<hr/>
: 设置''type''为（目前的）十一个值之一，会显示分类用于归类的模板类型的预设说明。这些值有：
:: '''{{hlist |ambox |campaignbox |conversion |external link |formatting |function |meta |navbox|navigation |sidebar |stub |timeline |userbox}}'''
: 若''type''设置为了不是这些值的其他内容，默认的说明“在本分类中列出的页面为模板”会原样显示。
{{Hidden begin |showhide=left |title=只设''type'' |bodystyle=font-size:105%;}}
<pre>{{Template category |type=sidebar}}</pre>
{{Template category |type=sidebar}}
{{Hidden end}}
: 更多''type''的输出示例请见下面的示例。

====''topic''====
<hr/>
: 添加默认说明“与''topic''相关的模板”，其中''topic''通常为与分类相关的主条目的[[wikilink]]。（如[[美国]]与[[:Category:美国模板]]）
{{Hidden begin |showhide=left |title=只设''topic'' |bodystyle=font-size:105%;}}
<pre>{{Template category |topic=[[美国]]}}</pre>
{{Template category |topic=[[美国]]}}
{{Hidden end}}
{{Hidden begin |showhide=left |title=''type''，''topic'' |bodystyle=font-size:105%;}}
<pre>{{Template category |type=infobox |topic=[[美国]]}}</pre>
{{Template category |type=infobox |topic=[[美国]]}}
{{Hidden end}}

====''description''====
<hr/>
: Use this if a customised description is needed instead of&nbsp;– or, if ''topic'' also used, to follow&nbsp;– the default description above.
{{Hidden begin |showhide=left |title=''type'', ''topic'', ''description'' |bodystyle=font-size:105%;}}
<pre style="overflow:auto;">
{{Template category
| type = navbox
| topic = [[China]]
| description = <br/>{{small|For templates relating specifically to the [[People's Republic of China|People's Republic of China (PRC)]] or the current [[Republic of China|Republic of China (ROC, "Taiwan")]], see, respectively, {{c|People's Republic of China templates}} and {{c|Republic of China (Taiwan) templates}}.}}
}}
</pre>
{{Template category
| type = navbox
| topic = [[China]]
| description = <br/>{{small|For templates relating specifically to the [[People's Republic of China|People's Republic of China (PRC)]] or the current [[Republic of China|Republic of China (ROC, "Taiwan")]], see, respectively, {{c|People's Republic of China templates}} and {{c|Republic of China (Taiwan) templates}}.}}
}}
{{Hidden end}}
{{Hidden begin |showhide=left |title=只设''description'' |bodystyle=font-size:105%;}}
<pre>{{Template category |description=This text is supplied by the ''description'' parameter.}}</pre>
{{Template category |description=This text is supplied by the ''description'' parameter.}}
{{Hidden end}}

====''onright'' / ''rhs''====
<hr/>
: Use this to place right-aligned boxes beside the template, such as {{tl|portal}} (to provide a link or links to related portal or portals) and/or {{tl|Commons category}} (to provide a link to the same or a similarly-named category at the Commons). If more than one box is included, ensure the widest one appears first (see example below) otherwise overlapping may occur.
{{Hidden begin |showhide=left |title=''topic'', ''rhs'' |bodystyle=font-size:105%;}}
<pre>
{{Template category
| topic = [[美国]]
| rhs = {{Commons category|United States|美国}}{{portal|美国}}
}}
</pre>
{{Template category
| topic = [[美国]]
| rhs = {{Commons category|United States|美国}}{{portal|美国}}
}}
{{Hidden end}}

====''container''====
<hr/>
: Set ''container'' to "true" (without quotemarks) to identify the category as a [[Wikipedia:Container category|container category]], i.e. a category meant to contain only subcategories. A note requesting that no templates are added to the template category is then included.
{{Hidden begin |showhide=left |title=只设''container'' |bodystyle=font-size:105%;}}
<pre>{{Template category |container=true}}</pre>
{{Template category |container=true}}
{{Hidden end}}

: An alternative to using ''container'' is to place {{tl|Parent category}} after the {{tl|Template category}} template:
{{Hidden begin |showhide=left |title={{braces|Parent category}}跟随{{braces|Template category}} |bodystyle=font-size:105%;}}
<pre>
{{Template category
| type = ''type''
| topic = ''[[topic]]''
| description = 这是''description''参数提供的文字。
}}
{{Parent category}}
</pre>
{{Template category
| type = ''type''
| topic = ''[[topic]]''
| description = 这是''description''参数提供的文字。
}}
{{Parent category}}
{{Hidden end}}

====''help''====
<hr/>
: Use this to replace the default instructions as to how to add a template to the category (see the "Further template category notes" section) or, if set to nothing, remove them.

==参见==
{{Other category-header templates}}

<includeonly>
{{#ifeq:{{SUBPAGENAME}}|sandbox | |
<!----------请在本行下设置分類------------>
[[Category:分類頁模板]]
}}
</includeonly>