<includeonly>{{#switch:{{NAMESPACE}}
 |User={{#if:{{#rel2abs:..}}
   |[[Category:{{{1}}}/|{{PAGENAME}}]]<!--放入〖目标分类/〗中-->
   |[[Category:{{{1}}}|{{PAGENAME}}]]
  }}
 |Category={{#switch:{{PAGENAME}}
   |{{{1}}}=可能有一些用户在自己的用户页子页中插入了这个用户框。如果您想知道哪些子页上使用了这个用户框，{{#ifexist:{{FULLPAGENAME}}/
     |可以在子分类[[:{{FULLPAGENAME}}/]]中找到。
     |您可以[{{FULLURL:{{FULLPAGENAME}}}}/ 点击这里查看]，如果有兴趣的话还可以[[:{{FULLPAGENAME}}/|为这些子页加上说明]]。
    }}<!--说明-->
   |{{{1}}}/=这里显示的是列出使用了这个用户框的用户页子页。如果您只想知道谁在自己的用户页中使用了这个用户框，请看[[:Category:{{{1}}}]]。[[Category:{{{1}}}| ]]
   |#default=[[Category:{{{1}}}|{{PAGENAME}}]]
  }}
 |Template={{#ifeq:{{#rel2abs:../doc}}|{{FULLPAGENAME}}
   |<!--不要出现在模板文档页-->
   |[[Category:{{{1}}}| ]]
  }}
 |{{NS:Project}}=[[Category:{{{1}}}| ]]
 |#default=[[Category:{{{1}}}|{{PAGENAME}}]]
}}</includeonly><noinclude>{{Documentation}}[[Category:用户框模板]]</noinclude>