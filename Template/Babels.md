{{#ifeq:{{NAMESPACE}}|Category
  |{{Babel
    |{{#ifexist:Template:User {{{1|zh}}}|{{{1|zh}}}|null}}
    |{{#ifexist:Template:User {{{1|zh}}}-5|{{{1|zh}}}-5|null}}
    |{{#ifexist:Template:User {{{1|zh}}}-4|{{{1|zh}}}-4|null}}
    |{{#ifexist:Template:User {{{1|zh}}}-3|{{{1|zh}}}-3|null}}
    |{{#ifexist:Template:User {{{1|zh}}}-2|{{{1|zh}}}-2|null}}
    |{{#ifexist:Template:User {{{1|zh}}}-1|{{{1|zh}}}-1|null}}
    |{{#ifexist:Template:User {{{1|zh}}}-0|{{{1|zh}}}-0|null}}|nocat=true}}
 |<div style="clear:both;"></div>}}
<!--當wikipedia參數為none時或語言代碼為zh時不顯示該語言的維基百科連接-->
{{#ifeq:{{{wikipedia|}}}|none||{{#ifeq:{{{1|}}}|zh||<div style="float: right; padding: 0.3em; border: 1px solid #999; font-size: 0.9em; padding: 0.4em;"><span class="Unicode">➠</span> {{#ifeq:{{{wikipedia|}}}|{{ns:0}}|[[:{{{1}}}:|{{{zhname}}}{{#if:{{{zhname2|}}}|／{{{zhname2}}}}}维基百科]]|[[:{{{wikipedia}}}:|{{{zhname}}}维基百科]]}}</div>}}}}
<div style="margin: 1em; padding: 1em 0 0.17em 0; font-size: 133%;">
<span id="anchorage_{{{1|zh}}}" style="font-weight:bold; padding:0.3em; border:1px solid #999; font-family: monospace; background:#faf9ec" lang="en">{{{1|zh}}}</span> – <span lang="{{{1|zh}}}">{{{nativename|{{#language:{{{1|zh}}}}}}}}</span>&#8206;（[[{{{zhname}}}]]{{#if:{{{zhname2|}}}|／[[{{{zhname2}}}]]}}）</div>
<!--*參考：'''[[:Category:其他语言的维基百科典范条目 ({{{zhname}}}{{#if:{{{zhname2|}}}|／[[{{{zhname2}}}]]}})]]'''-->
<!--以連結不同語言的特色條目分類中，吸引更多熟習該語言的維基人進行釋譯-->
{|cellpadding="2" cellspacing="0" style="margin: 2em; width: 70%;"
|+ 分類：'''[[:Category:{{{1|zh}}} 使用者]]'''
|-　valign="top"
|style="padding-right:2em;border-bottom:1px solid #ddd;"|熟練度
|style="padding-right:2em;border-bottom:1px solid #ddd;"|模板
|style="border-bottom:1px solid #ddd;"|相關分類
|-valign="top"
|style="padding-right:2em;"|母語
|style="padding-right:2em;"|<nowiki>{{</nowiki>[[Template:User {{{1|zh}}}|User {{{1|zh}}}]]<nowiki>}}</nowiki>
|[[:Category:{{{1|zh}}} 母語使用者]]
|-valign="top"
|style="padding-right:2em;"|专业
|style="padding-right:2em;"|<nowiki>{{</nowiki>[[Template:User {{{1|zh}}}-5|User {{{1|zh}}}-5]]<nowiki>}}</nowiki>
|[[:Category:{{{1|zh}}}-5 使用者]]
|-valign="top"
|style="padding-right:2em;"|接近母語
|style="padding-right:2em;"|<nowiki>{{</nowiki>[[Template:User {{{1|zh}}}-4|User {{{1|zh}}}-4]]<nowiki>}}</nowiki>
|[[:Category:{{{1|zh}}}-4 使用者]]
|-valign="top"
|style="padding-right:2em;"|高級
|style="padding-right:2em;"|<nowiki>{{</nowiki>[[Template:User {{{1|zh}}}-3|User {{{1|zh}}}-3]]<nowiki>}}</nowiki>
|[[:Category:{{{1|zh}}}-3 使用者]]
|-valign="top"
|style="padding-right:2em;"|中級
|style="padding-right:2em;"|<nowiki>{{</nowiki>[[Template:User {{{1|zh}}}-2|User {{{1|zh}}}-2]]<nowiki>}}</nowiki>
|[[:Category:{{{1|zh}}}-2 使用者]]
|-valign="top"
|style="padding-right:2em;"|初級
|style="padding-right:2em;"|<nowiki>{{</nowiki>[[Template:User {{{1|zh}}}-1|User {{{1|zh}}}-1]]<nowiki>}}</nowiki>
|[[:Category:{{{1|zh}}}-1 使用者]]
{{#ifeq:{{{zero|{{#ifexist:Template:User {{{1|zh}}}-0|0|}}}}}case|0case|
{{!}}- valign="top"
{{!}}style="padding-right:2em;"{{!}}完全不會{{!}}{{!}}style="padding-right:2em;"{{!}}<nowiki>{{</nowiki>[[Template:User {{{1|zh}}}-0|User {{{1|zh}}}-0]]<nowiki>}}</nowiki>{{!}}{{!}}[[:Category:{{{1|zh}}}-0 使用者]]}}
|}<noinclude>
{{Documentation}}
</noinclude>