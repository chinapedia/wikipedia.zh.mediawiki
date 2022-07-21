{{{onright|{{{rhs|}}}}}}
{{Cmbox
| type = notice
| style = padding-bottom:0.5em;
| image = {{#ifeq:{{{type|}}}|module|[[File:Lua-logo-nolabel.svg|44px|Lua 标志|alt=Lua 标志|link=]]|[[File:Curly Brackets.svg|44px|模板括弧|alt=模板括弧|link=]]}}
| text = <div style="width:98%;"><!--

 Container-category message
   -->{{yesno|1={{{container|}}}
       |yes=<div style="font-size:115%;padding:0.5em 0;"> '''注：請勿直接將{{#ifeq:{{{type|}}}|module|-{zh-cn:模块; zh-tw:模組;}-|模板}}加入本分類，正確的做法是將其加入下列子分類之一。'''{{category other|[[Category:容器分类]]}}</div>
      }}<!--

 (type/)topic/description
   -->{{#if:{{{topic|}}}{{{description|}}}
       | <div style="background:#d5e4ed;line-height:1.5em;border:1px solid #aaa;font-size:120%;padding:0.35em;"> <!--
          -->{{#if:{{{topic|}}} |'''與{{{topic}}}有關的{{#switch:{{lc:{{{type}}}}} |navbox|navigation|navigational|infobox|sidebar|stub|={{ucfirst:{{{type}}}}}模板|module=-{zh-cn:模块; zh-tw:模組;}-|#default=模板}}。'''&nbsp;{{{1|}}}{{{description|}}}
              | <div><!--(in case 1/description begins with newline:)--> {{{1|}}}{{{description|}}} </div>
             }} </div>
      }}<!--

 type --><div style="line-height:1.3em;padding-top:0.3em;"> <!--
          -->{{#if:{{{type|}}} <!--
    (then:)-->| <div style="font-size:95%;font-weight:bold;">本[[Help:分类|分类]]的收录对象為<!--
                 -->{{#switch:{{lc:{{{type}}}}}
                     | ambox = [[Wikipedia:条目消息框|条目消息框（ambox）]]模板
                     | category header
                     | category heading
                     | catheader | cat header
                     | cathead = [[Wikipedia:頁面分類|分類]]顶注模板
                     | campaignbox = {{le|Wikipedia:格式手冊/軍事史#戰爭框|Wikipedia:Manual of Style/Military history#Campaignboxes|戰爭框}}模板
                     | conversion = 執行[[Wikipedia:格式手册/日期和数字#单位换算|換算]]操作的模板
                     | external link = [[Wikipedia:外部链接|外部-{zh-hans:链接; zh-hant:連結;}-]]的模板
                     | formatting = 提供特定[[Wikipedia:格式手冊/文字格式|格式]]的模板
                     | function = 函數模板{{nobold|，即生成文字、图像或其他元素的模板}}
                     | infobox = [[Wikipedia:格式手册/信息框|-{zh-hans:信息; zh-hant:資訊;}-框]]模板
                <!-- | message = [[Wikipedia:模板消息|消息]]模板 -->
                     | module = [[Wikipedia:Lua|&nbsp;Lua&nbsp;-{zh-cn:模块; zh-tw:模組;}-]]
                     | meta = {{le|Help:元模板|Help:Metatemplating|元模板}}
                     | navigation |navigational |navbox = [[Wikipedia:导航模板|導航模板]]
                     | sidebar = [[Wikipedia:分類、列表與導航模板#導航模板|側邊欄]]模板
                     | stub = [[Wikipedia:小作品类别列表|小作品]]模板
                     | sub = [[Help:模板#创建并编辑模板|子模板]]{{nobold|，即被另外一個或多個模板所使用的模板}}
                     | timeline = [[Wikipedia:年表|年表]]模板
                     | user
                     | userbox = {{le|Wikipedia:用戶模板|Wikipedia:User templates|用户模板}}，包括[[Wikipedia:用戶框|用户框]]
                     | #default = {{{1|{{{description|}}}}}}
                     | {{{type}}}模板
                    }}。</div><!--

    (else:)-->| <div style="font-size:95%;font-weight:bold;">本[[Help:分类|分类]]的收納對象為[[Help:模板|模板]]。</div>}}
                <div style="font-size:95%;padding:0.15em 0;line-height:1.3em;">本分類是用於[[:Category:維基百科管理|管理維基百科]]的頁面，並非百科全书的一部分。</div> {{#if:{{{ALTTEXT|}}}|<hr/>{{{ALTTEXT}}}<hr/>}}
<!--
 Further template category notes
          --><div class="mw-collapsible mw-collapsed" style="font-size:90%;padding-top:0.25em;line-height:1.3em;">
               <div style="border-bottom:1px solid #aaa;font-weight:bold;">更多-{zh-hans:信息; zh-hant:訊息;}-</div>
               <div class="mw-collapsible-content">
                 <div>本分類專為收納{{#ifeq:{{{type|}}}|module|[[Wikipedia:Lua|-{zh-cn:模块; zh-tw:模組;}-]]|[[Wikipedia:模板命名空间|模板]]}}而建立，不應用於歸類[[Wikipedia:什么是条目|條目]]和其他[[Wikipedia:命名空间|命名空間]]的頁面。</div><br/><!--

                Help subsection
                 -->{{#if:{{{help|}}}{{{2|}}} <!--
                 (then:)-->| {{yesno|{{{help|}}} |no={{#if:{{{2|}}}|<div>{{{2}}}</div><br/>}} |yes=<div>{{{help}}}{{{2|}}}</div><br/>|def=<div>{{{help}}}{{{2|}}}</div><br/>}}<!--
                 (else:)-->| <div>如何將{{#ifeq:{{{type|}}}|module|-{zh-cn:模块; zh-tw:模組;}-|模板}}歸入本分類？</div>
                 {{#ifeq:{{{type|}}}|module|{{Unbulleted list |list_style=padding-left:1.4em; line-height:1.8em;
                | 請在-{zh-cn:模块文档; zh-tw:模組文件;}-頁面（通常名為“Module:''模块名稱''/doc”）底部的 <nowiki><includeonly></nowiki> 標籤之後加入 <kbd>&#91;&#91;{{FULLPAGENAME}}&#93;&#93;</kbd>。
                }}|{{Unbulleted list |list_style=padding-left:1.4em; line-height:1.8em;
                  | 若模板已有-{zh-hans:文档; zh-hant:文件說明;}-頁面（通常名為“Template:''模板名稱''/doc”），請在該頁面底部的 <nowiki><includeonly></nowiki> 標籤之後加入
                  | {{pad}}<kbd>&#91;&#91;{{FULLPAGENAME}}&#93;&#93;</kbd>
                  | 若模板未有-{zh-hans:文档; zh-hant:文件說明;}-頁面，請直接在模板代碼結尾加入
                  | {{pad}}<kbd>&lt;noinclude&gt;&#91;&#91;{{FULLPAGENAME}}&#93;&#93;&lt;/noinclude&gt;</kbd>
                  | 并確保它与模板代碼的最後一個字符位於同一行。
                 }} }} }}
               </div>
             </div> <!--(end "Further template category notes")

      --></div> <!--(end of "type" div)-->

</div> <!--(end containing div)

## Tracking categories
-->{{Category other|<!--
    -->{{#if: {{{topic|}}}{{{description|}}}<!--
        -->|<!-- # We have a topic/description, so all ok
        -->|[[Category:模板：沒有主題或描述的模板分類]]<!--
    -->}}<!--
-->}}
}}<includeonly>{{#ifeq:{{NAMESPACE}}|{{ns:14}}
                | {{{category|[[Category:維基百科模板分類]]}}}
               }}</includeonly><noinclude>
{{Documentation}}
</noinclude>