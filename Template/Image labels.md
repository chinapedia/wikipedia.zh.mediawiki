<div style="position: relative; white-space: nowrap; font-size: small; {{{style|}}}">
<span style="display:table-cell; border-collapse:collapse; border: solid 1px #ddd;">{{{image|{{{labels|}}}}}}</span>
<div style="position: absolute; left: {{{labels_x|0}}}px; top: {{{labels_y|0}}}px;">
{{{labels|}}}
</div>
</div><noinclude>
==语法==
{|
|<pre><nowiki>{{Image labels
| style = 
| image = 
| labels = 
| labels_x = 
| labels_y = 
}}
</nowiki></pre>
|<pre>模板头
对于此图文框的CSS代码，可选
图片的链接
一个或多个使用{{Image label}}模板的标签
所有Image label标签向左的位移，单位为px，可选
所有Image label标签向下的位移，单位为px，可选
模板尾
</pre>
|}
==用法==
===基本用法===
<pre>{{Image labels
| image = [[File:Example-zh.jpg]]
| labels = {{Image label|x=50|y=50|text=label 1}}
{{Image label|x=50|y=100|text=label 2}}
{{Image label|x=100|y=50|text=label 3}}
}}</pre>

{{Image labels
| image = [[File:Example-zh.jpg]]
| labels = {{Image label|x=50|y=50|text=label 1}}
{{Image label|x=50|y=100|text=label 2}}
{{Image label|x=100|y=50|text=label 3}}
}}

===使用<code>labels_x</code>参数===

<pre>{{Image labels
| image = [[File:Example-zh.jpg]]
| labels = {{Image label|x=50|y=50|text=labels_x=100}}
| labels_x = 100
}}</pre>

{{Image labels
| image = [[File:Example-zh.jpg]]
| labels = {{Image label|x=50|y=50|text=labels_x=100}}
| labels_x = 100
}}

===使用<code>style</code>参数===

<pre>{{Image labels
| style = border: 1px solid red; color: blue;
| image = [[File:Example-zh.jpg]]
| labels = {{Image label|x=50|y=50|text=style}}
}}</pre>

{{Image labels
| style = border: 1px solid red; color: blue; float: right;
| image = [[File:Example-zh.jpg]]
| labels = {{Image label|x=50|y=50|text=style}}
}}
[[Category:格式模板]]

</noinclude>