{{ {{{|safesubst:}}}#invoke:Unsubst||$params=old,by,new,note,historical,nocat|date=__DATE__|$B=
{{Ombox
| image     = [[Image:Stop hand nuvola.svg|40px]]
| type      = delete
| text      = [[{{{old|Template:{{{1|{{PAGENAME}}}}}}}}]]已{{#if:{{{by|}}}|被{{{by}}}}}[[已弃用|停用]]{{#if:{{{historical|}}}|，但由于历史原因保留}}。{{#if:{{{new|{{{2<includeonly>|</includeonly>}}}}}}
  |请{{#if:{{{3|}}}
    |使用{{tlx|{{{new|{{{2}}}}}}|{{{3}}}}}代替
    |{{#if:{{{new|}}}
      |参见[[{{{new}}}]]
      |使用[[Template:{{{2}}}]]代替
      }}
    }}。
}}{{{note|}}}{{#if:{{{date|}}}|（{{#time:Y年n月j日|{{{date}}}}}）|{{#if:{{{time|<noinclude>1</noinclude>}}}|（{{#time:Y年n月j日|{{{time<noinclude>|now</noinclude>}}}}}）}}}}
}}{{#ifeq:{{{nocat|}}}|true
   ||{{Template other
      |{{When on basepage<!-- 不将子页面加入分类，如/doc、/sandbox或/testcases -->
         |{{#ifeq:{{PAGENAME}}|{{ucfirst:{{{1|{{PAGENAME}}}}}}}<!-- 只用于停用模板本身 -->
            |<includeonly>{{#if:{{{historical|}}}|[[Category:因历史原因保留的已停用模板]]|[[Category:已停用模板]]}}</includeonly>
          }}
       }}
      |{{#ifeq:{{{old|}}}|{{FULLPAGENAME}}||[[Category:使用已停用模板的页面]]}}
     }}
  }}
}}<noinclude>
{{Documentation}}
<!-- 请将分类添加进/doc子页面，跨语言链接放入维基数据。 -->
</noinclude>