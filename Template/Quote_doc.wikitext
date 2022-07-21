<includeonly></includeonly><noinclude>{{template doc page viewed directly}}</noinclude>
{{noteTA
|1=zh:Enter;zh-cn:回车;zh-tw:確認}}
== 用法 ==

*{{tl|quote|内容}}
*:“内容”为引用。
: '''注意'''：如果引用的文字含有一个或更多“[[等於|=]]”（[[等号]]），那么此模板必须以<nowiki>{{cquote|</nowiki>'''<span style="color:red;">1=</span>'''''引用文字''<nowiki>}}</nowiki>的形式调用。
*{-{}-{quote|height=高度值|内容}}
*:引用内容以固定高度呈现，用来减少大引用所占篇幅，以突出条目。
*{-{}-{quote|width=宽度值|内容}}
*:引用内容以固定k宽度呈现，用来调节过宽文段在排版上的问题。
*{-{}-{quote|align=排列方式|内容}}
*:模板的排列方式（居中请填：center、居右可填：right、居左可填：left）
*{-{}-{quote|width=宽度值|height=高度值|内容}}
*:引用内容以固定高度呈现，用来减少大引用所占篇幅，以突出条目，同时调节过宽文段在排版上的问题。
*{-{}-{quote|内容|人物|来源}}
*:添加了引用来源特性

== 示例 ==

{{tl|quote|这是一个引用。}}

效果：
{{quote|这是一个引用。}}
----
{{tlx|quote|这是一个引用。|作者|出处}}

效果：
{{quote|这是一个引用。|作者|出处}}
----
{{tl|quote|width{{=}}200px{{!}}<-{}-p>这是一个宽度限定的引用。<-{}-/p><-{}-p>目前的宽度是200px。<-{}-/p><-{}-p>所有宽于200px的内容会自动换行。<-{}-/p><-{}-p>注意：<-{}-/p><-{}-p>段落不能通过按二次回车鍵来实现，必须用<-{}-p>或<-{}-br />标签来实现。<-{}-/p>}}

效果：
{{quote|width=200px|<p>这是一个宽度限定的引用。</p><p>目前的宽度是200px。</p><p>所有宽于200px的内容会自动换行。</p><p>注意：</p><p>段落不能通过按二次回车鍵来实现，必须用<-{}-p>或<-{}-br />标签来实现。</p>}}
----
{{tl|quote|height=80px|<-{}-/p>这是一个高度限定的引用。<-{}-/p><-{}-p>目前的高度是120px。<-{}-/p><-{}-p>所有高于120px的内容都可以通过滚动实现浏览。<-{}-/p><-{}-p>注意：<-{}-/p><-{}-p>段落不能通过按二次回车鍵来实现，必须用<-{}-p>或<-{}-br />标签来实现。<-{}-/p><-{}-p>'-{}-'开始：'-{}-'<-{}-/p><-{}-p>……<-{}-/p><-{}-p>……<-{}-/p><-{}-p>……<-{}-/p><-{}-p>……<-{}-/p><-{}-p>……<-{}-/p><-{}-p>'-{}-'结束'-{}-'<-{}-/p>}}

效果：
{{quote|height=80px|<p>这是一个高度限定的引用。</p><p>目前的高度是120px。</p><p>所有高于120px的内容都可以通过滚动实现浏览。</p><p>注意：</p><p>段落不能通过按二次回车鍵来实现，必须用<-{}-p>或<-{}-br />标签来实现。</p><p>''开始：''</p><p>……</p><p>……</p><p>……</p><p>……</p><p>……</p><p>''结束''</p>
}}

==模板數據==
{{TemplateDataHeader}}
<templatedata>{
  "description": "在條目中加入一個引言框。",
  "params": {
    "text": {
      "label": "文字",
      "description": "引言的內文",
      "type": "string",
      "required": false,
      "aliases": [ "1", "quote" ]
    },
    "sign": {
      "label": "作者",
      "description": "引言內容的作者",
      "type": "string",
      "required": false,
      "aliases": [ "2", "cite" ]
    },
    "source": {
      "label": "出處",
      "description": "引言的來源出處",
      "type": "string",
      "required": false,
      "aliases": [ "3" ]
    }
  }
}</templatedata>

==相關模板==
{{Quotation templates}}

<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:格式模板]]
[[Category:引文模板]]
}}</includeonly>