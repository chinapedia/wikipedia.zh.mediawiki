{{#ifeq:{{{bottom}}}|yes
| {{ tmbox
| small = {{{small|}}}
| image = none
| style = text-align: center
| text  = '''請在討論頁的底部放置新的討論。'''
}}
}}{{#ifexpr:{{#ifeq:{{NAMESPACE}}|User talk|1|0}}*{{#ifeq:{{{disclaimer|}}}|yes|1|0}}|
{{usertalkpage}}
}}
<table {{#ifexpr:{{#ifeq:{{NAMESPACE}}|User talk|1|0}}*{{#ifeq:{{{disclaimer|}}}|yes|1|0}}
 |style="border: 1px solid #c0c090; border-spacing:3px; background-color: #F8EABA; margin-bottom: 0px; width: 100%"
 |class="tmbox tmbox-notice plainlinks" id="talkheader" style="width: 80%; border-collapse: separate"
}} ><tr>
<th colspan=4 style="border-bottom: 1px solid #c0c090; width: 100%">{{#ifeq:{{NAMESPACE}}|User talk|這裡是[[{{SUBJECTPAGENAME}}|{{PAGENAME}}]]的討論頁，您可以在這向{{PAGENAME}}發送消息和評論。|這是一個[[Wikipedia:討論頁指導方針|討論頁]]，討論關於{{#if:{{{wp|}}}|[[:{{SUBJECTPAGENAME}}|{{PAGENAME}}]]和任何與其目的和任務相關的事項|改善{{pagetype}}[[:{{SUBJECTPAGENAME}}|{{#if:{{{display_title|}}}|{{{display_title}}}|{{PAGENAME}}}}]]}}。<br/> {{#if:{{SUBJECTSPACE}}||這[[Wikipedia:维基百科不是什么#維基百科不是發表創新意念的地方|不是]]一個為討論該條目主題而设的論壇。}}}}</th>
</tr><tr>
<td style="background-color: white; border: 1px solid #c0c090">
* 將新的發言放在舊的發言下，[{{fullurl:{{TALKPAGENAMEE}}|action=edit&section=new}} 點擊這裡開始新的討論]。
* 記得在您發表留言的結尾加上四條半形波浪號（<code><nowiki>~~~~</nowiki></code>）以[[WP:签名|添加簽名]]。
* 請不要隨意更改或刪除別人的留言。
* 維基百科新手？歡迎您，請[[WP:互助客栈/求助|隨時提出問題尋求解答]]。
</td><td>
* 請[[Wikipedia:假定善意|保持善意]]，不要[[WP:不要伤害新手|傷害新人]]
* 請[[Wikipedia:文明|保持禮貌]]，避免[[WP:不要人身攻击|人身攻擊]]
* 遇到爭議時請[[WP:争议的解决|尋求解決方法]]
{{#switch:yes|{{{arpol|}}}|{{#if:{{SUBJECTSPACE}}|no|yes}}=<td style="border-left: 1px solid #c0c090">{{Center|'''條目政策'''}}
* [[Wikipedia:非原创研究|不要原創研究]]
* [[Wikipedia:中立的观点|中立的觀點]]
* [[Wikipedia:可供查證|可供查證]]
</td>
}}{{#if:{{{1|}}}{{{shortcut|}}}{{{shortcut1|}}}{{{sc|}}}{{{sc1|}}}|<td>{{shortcut|{{{1|{{{shortcut|{{{shortcut1|{{{sc|{{{sc1|}}}}}}}}}}}}}}}|{{{2|{{{shortcut2|{{{sc2|}}}}}}}}}|{{{3|{{{shortcut3|{{{sc3|}}}}}}}}}|{{{4|{{{shortcut4|{{{sc4|}}}}}}}}}|{{{5|{{{shortcut5|{{{sc5|}}}}}}}}} }}</td>}}
</tr>
{{#if:{{{noarchive|{{{noarchives|{{{archives|}}}}}}}}}||{{#ifexist:{{FULLPAGENAME}}/存档1|
<tr><td colspan=4 style="border-top: 1px solid #c0c090; padding: 1px 3px">'''[[Help:如何將討論頁存檔|存档]]:''' {{#ifexist:{{FULLPAGENAME}}}/存档目录|[[{{FULLPAGENAME}}/存档目录|存档目录]],&#32;}}{{#ifexist:{{FULLPAGENAME}}/Archive A|{{Archive list alpha|nobr=yes|root={{FULLPAGENAME}}}},&#32;|}}{{Archive list|nobr=yes|root={{FULLPAGENAME}}}}</td>
</tr>
}}
}}
{{#if:{{#ifexist:{{FULLPAGENAME}}/存档1|y}}{{#ifexist:{{FULLPAGENAME}}/Archive A|y}}{{{search|}}}|{{#ifeq:{{{search|}}}|no||
<tr><td colspan=4 style="border-top: 1px solid #c0c090; padding: 0">{{search box|root={{FULLPAGENAME}}|search-break=no|search-width=auto|search-button-label=搜索存档}}</td>
</tr>
}}
}}
</table><noinclude>{{Documentation}}</noinclude>