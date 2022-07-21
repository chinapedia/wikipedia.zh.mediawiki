<includeonly>{| class="{{#ifeq:{{{metadata|}}}|yes|metadata}} plainlinks mbox-small{{#ifeq:{{lc:{{{position|}}}}}|left|-left}} {{#if:{{{collapsible|}}}|mw-collapsible {{#ifeq:{{{collapsible|}}}|collapsed |mw-collapsed}}}}" style="padding:0.25em 0.5em 0.5em 0.75em;border:1px solid #aaa;background:#f9f9f9;{{{style|}}}"
|-
|colspan="2" style="padding-bottom:0.75em;border-bottom:1px solid #aaa;text-align:center;"| <div style="clear:both;">从维基百科的[[Wikipedia:姊妹计划|姊妹计划]]<br/>了解更多有关<br />“'''{{{display|{{{1|{{PAGENAME}}}}}}}}'''”的内容</div>
|- style="height:25px;"
{{#ifeq:{{{wikt|}}}|no |
 | {{!}}style="padding-top:0.75em;"{{!}} [[File:Wiktionary-logo.svg|25x25px|link={{fullurl:wikt:{{{wikt|Special:Search/{{{1|{{PAGENAME}}}}}}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基词典]]
   {{!}}style="padding-top:0.75em;"{{!}} 维基词典上的[[wikt:{{{wikt|Special:Search/{{{1|{{PAGENAME}}}}}}}}|字词解释]]
}}
|- style="height:25px;"
{{#ifeq:{{{c|{{{commons|}}}}}}|no |
 | {{#ifeq:{{{commonscat|no}}}|yes
    | {{!}} [[File:Commons-logo.svg|25x25px|link={{fullurl:c:Special:Search/Category:{{{c|{{{commons|{{{1|{{PAGENAME}}}}}}}}}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基共享资源]]
      {{!}} 维基共享资源上的[[c:Special:Search/Category:{{{c|{{{commons|{{{1|{{PAGENAME}}}}}}}}}}}|多媒体资源]]
    | {{!}} [[File:Commons-logo.svg|25x25px|link={{fullurl:c:{{{c|{{{commons|Special:Search/{{{1|{{PAGENAME}}}}}}}}}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基共享资源]]
      {{!}} 维基共享资源上的[[c:{{{c|{{{commons|Special:Search/{{{1|{{PAGENAME}}}}}}}}}}}|多媒体资源]]
   }}
}}
|- style="height:25px;"
{{#ifeq:{{{n|}}}|no |
 | {{!}} [[File:Wikinews-logo.svg|25x25px|link={{fullurl:n:Special:Search/{{{1|{{PAGENAME}}}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基新闻]]
   {{!}} 维基新闻上的[[n:Special:Search/{{{1|{{PAGENAME}}}}}|新闻]]
}}
|- style="height:25px;"
{{#ifeq:{{{q|}}}|no |
 | {{!}} [[File:Wikiquote-logo.svg|25x25px|link={{fullurl:q:{{{q|Special:Search/{{{1|{{PAGENAME}}}}}}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基语录]]
   {{!}} 维基语录上的[[q:{{{q|Special:搜索/{{{1|{{PAGENAME}}}}}}}}|名言]]
}}
|- style="height:25px;"
{{#ifeq:{{{s|}}}|no |
 | {{#ifeq:{{{author|no}}}|yes
    | {{!}} [[File:Wikisource-logo.svg|25x25px|link={{fullurl:s:Special:Search/Author:{{{s|{{{1|{{PAGENAME}}}}}}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基文库]]
      {{!}} 维基文库上该作者的[[s:Special:搜索/作者:{{{s|{{{1|{{PAGENAME}}}}}}}}|作品]]
    | {{!}} [[File:Wikisource-logo.svg|25x25px|link={{fullurl:s:{{{s|Special:Search/{{{1|{{PAGENAME}}}}}}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基文库]]
      {{!}} 维基文库上的[[s:{{{s|Special:搜索/{{{1|{{PAGENAME}}}}}}}}|原始文献]]
   }}
}}
|- style="height:25px;"
{{#ifeq:{{{b|}}}|no |
 | {{!}} [[File:Wikibooks-logo.svg|25x25px|link={{fullurl:b:{{{b|Special:Search/{{{1|{{PAGENAME}}}}}}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基教科书]]
   {{!}} 维基教科书上的[[b:{{{b|Special:搜索/{{{1|{{PAGENAME}}}}}}}}|教科书和手册]]
}}
|- style="height:25px;"
{{#ifeq:
   <!-- Show Wikivoyage if the "voy" parameter is anything other than blank, empty or "no" -->
   {{#switch: {{{voy|<noinclude>yes</noinclude>}}}
    | | no     = false
    | #default = true
   }}
 | true
 | {{!}} [[File:Wikivoyage-Logo-v3-icon.svg|25x25px|link={{fullurl:voy:{{{voy|Special:Search/{{{1|{{PAGENAME}}}}}}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-維基導遊]]
   {{!}} 維基導遊上的[[voy:{{{voy|Special:Search/{{{1|{{PAGENAME}}}}}}}}|旅遊{{#if: {{{voy|}}}| 指南| -{zh-cn:信息; zh-tw:資訊}-}}]]
}}
|- style="height:25px;"
{{#ifeq:{{{v|}}}|no |
 | {{!}} [[File:Wikiversity-logo-Snorky.svg|25x25px|link={{fullurl:v:{{{v|Special:Search/{{{1|{{PAGENAME}}}}}}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基学院]]
   {{!}} 维基学院上的[[v:{{{v|Special:Search/{{{1|{{PAGENAME}}}}}}}}|學習资源]]
}}
|- style="height:25px;"
{{#ifeq:{{{d|no}}}|no |
 | {{!}} [[File:Wikidata-logo.svg|25x25px|link={{fullurl:d:{{{d<noinclude>|Special:ItemByTitle/enwiki/{{{1|{{PAGENAME}}}}}</noinclude>}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基数据]]
   {{!}} 维基数据上的[[d:{{{d<noinclude>|{{{1|Special:ItemByTitle/enwiki/{{PAGENAME}}}}}</noinclude>}}}|数据项]]
}}
|- style="height:25px;"
{{#ifeq:{{{species|no}}}|no |
 | {{!}} [[File:Wikispecies-logo.svg|25x25px|link={{fullurl:species:{{{species<noinclude>|Special:Search/{{{1|{{PAGENAME}}}}}</noinclude>}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基物种]]
   {{!}} 维基物种上的[[species:{{{species<noinclude>|Special:Search/{{{1|{{PAGENAME}}}}}</noinclude>}}}|物种信息]]
}}
|- style="height:25px;"
{{#ifeq:{{{species_author|no}}}|no |
 | {{!}} [[File:Wikispecies-logo.svg|25x25px|link={{fullurl:species:{{{species_author<noinclude>|Special:Search/{{{1|{{PAGENAME}}}}}</noinclude>}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-维基物种]]
   {{!}} 维基物种上该物种的[[species:{{{species_author<noinclude>|Special:Search/{{{1|{{PAGENAME}}}}}</noinclude>}}}|{{{species_author<noinclude>|</noinclude>}}}作者]]
}}
|- style="height:25px;"
{{#if:{{{m|}}}|
 {{#switch:{{lc:{{{m}}}}}
   |yes = {{!}}<noinclude>|</noinclude> [[File:Wikimedia Community Logo.svg|25x25px|link={{fullurl:n:Special:Search/{{{1|{{PAGENAME}}}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-元维基]]
   {{!}}<noinclude>|</noinclude> 元维基上的[[m:Special:Search/{{{1|{{PAGENAME}}}}}|讨论]]
   |no =
   |{{!}} [[File:Wikimedia Community Logo.svg|25x25px|link={{fullurl:m:{{{m}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-元维基]]
   {{!}} 元维基上的[[m:{{{m}}}|讨论]]
 }}
}}
|- style="height:25px;"
{{#ifeq:{{{mw|no}}}|no |
 | {{!}} [[File:MediaWiki-2020-small-icon.svg|25x25px|link={{fullurl:mw:{{{mw<noinclude>|Special:Search/{{{1|{{PAGENAME}}}}}</noinclude>}}}}}|-{zh-cn:搜索; zh-tw:搜尋}-MediaWiki]]
   {{!}} MediaWiki上的[[mw:{{{mw<noinclude>|{{{1|Special:Search/{{PAGENAME}}}}}</noinclude>}}}|文档]]
}}
|}</includeonly><noinclude>
{{Documentation}}
</noinclude>