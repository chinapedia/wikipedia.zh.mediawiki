<includeonly>{{#ifeq:{{{long|}}}|yes
|[//lccn.loc.gov/{{#if:{{{1|{{{id|}}}}}}|{{{1|{{{id|}}}}}}|Name?{{urlencode:{{PAGENAME}}}}}} {{{2|{{{title|{{{name|{{PAGENAME}}}}}}}}}}}]在美国[[國會圖書館 (美國)|國會圖書館]]的目录记录
|{{LCCN/prepare
|{{{1|{{{id|}}}}}}
|{{#iferror:{{#expr:{{padleft:|2|{{{1|}}} }} }}|2
|{{#ifeq:{{padright:{{{1|}}}|10|x}}|{{{1|}}}|2|0}} }}
|title={{{2|{{{title|{{{name|}}} }}} }}} }}
}}</includeonly><noinclude>
{{documentation}}
<!-- PLEASE ADD CATEGORIES AND INTERWIKIS TO THE /doc SUBPAGE, THANKS -->
</noinclude>