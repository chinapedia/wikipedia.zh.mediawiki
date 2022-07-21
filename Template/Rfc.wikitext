{{{{{|safesubst:}}}#invoke:Unsubst||$B=<span id="{{#if: {{{rfcid|}}} | rfc_{{{rfcid}}} }}"></span><span id="rfctag"></span>{{Mbox
|image=[[File:Dialog-information on.svg|40px]]
|type=notice
|text={{Userbox
| float  = right
| id     = [[File:Internet-group-chat.svg]]
| id-c   = #d0d0d0
| info   = 請考慮加入[[Wikipedia:回饋請求系統|回饋請求系統]]。
| info-c = #e0e0e0
}}'''某位編輯者請求其他編輯者針對本議題[[Wikipedia:請求評論|進行評論]]。'''{{#if: {{{rfcid|}}} |本頁已經| {{#ifeq:{{{rfcid|¬}}}|¬|在24小時之內，本頁將|[[Category:使用請求評論模板但沒有指定rfcid參數]] <strong class=error>錯誤：如果{{para|rfcid}}為空則必需移除</strong>──本頁將不會}} }}新增至以下列表{{#if:{{{2|}}}||}}：
{{for loop||call=Rfc/topic|{{{1|未分類}}}|{{{2|}}}|{{{3|}}}|{{{4|}}}|{{{5|}}}|{{{6|}}}|{{{7|}}}|{{{8|}}}|{{{9|}}}|{{{10|}}}|skipBlanks=yes}}{{#if:{{{1|}}}{{{2|}}}{{{3|}}}{{{4|}}}{{{5|}}}{{{6|}}}{{{7|}}}{{{8|}}}{{{9|}}}{{{10|}}}||<strong class=error>（錯誤：沒有指定[[WP:RFCCAT|請求評論的分類]]）</strong>}}
當討論結束時，請移除本標籤，將本頁從請求評論列表中移除{{#if:{{{2|}}}||}}。如果本頁也列在其他列表中，也將會在下方得到通知。
}}<includeonly>{{#ifeq:{{FULLPAGENAME}}|Template:Rfc|<!-- Suppress testcase adding category to main template -->|{{#ifeq:{{#switch:{{lc:{{SUBPAGENAME}}}}|sandbox|testcase|testcases=1}}|1|<!-- Don't categorize sandbox, testcase, or testcases pages -->|[[Category:維基百科請求評論]]}}}}</includeonly>}}<noinclude>
{{Documentation}}
</noinclude>