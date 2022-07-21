{{NoteTA
|G1 = IT
|G2 = MediaWiki
}}
{{Documentation subpage}}
{{High-use|12367}}
<!-- 在本行下編輯模板說明 -->

本模板显示“模板文档”框，就像您现在看到的这样。

起初用于为模板自动从/doc子页面中显示文档，但也用于显示内联文档。

==用法==
# {{tlx|Documentation subpage}}
# {{tlx|Documentation subpage|页面名称}}

* '''页面名称'''为指向文档页的名称，用來产生在框顶部右侧<code>-{}-[查看]</code>和<code>-{}-[编辑]</code>的特定按鈕。
* 參數1和參數2皆須被連結，如{{code|[[參數]]}}。

本模板应被放在“/doc”页面顶端。根据被调用的位置的不同，它会显示不同的消息：
* 在“/doc”页上，它会显示一个文本框，提示这是一个模板说明文档，并提供指向模板本身的链接。
* 在其他页面上（即[[Wikipedia:嵌入包含|嵌入包含]]「/doc」页的页面），它会该提示说明文档是从一个子页面嵌入包含而来的。

==功能==
除了提示消息之外，本模板亦将页面分到[[:Category:模板說明文件]]或相似（根据主体空间命名）的分类下，但仅针对拥有子页面功能的名字空间里的说明文档。本模板还会把模板的[[m:Help:Categories#Sort order|排序关键字]]根据不带名字空间名称时的页面名称作相应变动（例如根据“Foo”，“Template:Foo”在分类中会被当做“F”开头的模板排序）。

==参见==
* [[Wikipedia:模板文件页模式]]

<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:模板說明文件| {{PAGENAME}}]]
[[Category:模板頁的模板]]
}}</includeonly>