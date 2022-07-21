{{ombox
 |image = [[File:{{{image|{{#switch: {{lc:{{{status}}}}}
  |active
  |approved   = Crystal Clear accepted bot.png
  |trial      = Crystal Clear question bot.svg
  |inactive   = Crystal Clear inactive bot2.png
  |unapproved = Crystal Clear denied bot.png
  |#default   = Crystal Clear action run.png
 }}}}}|75px|{{{caption|This is a bot account.}}}|alt={{{alt|}}}]]
 |text  = '''此為[[Wikipedia:Bot policy|機械人帳號]]{{#if:{{{codebase|}}}
  |，使用{{{codebase}}}
  |{{#ifeq: {{lc:{{{awb}}}}}|yes
    |，使用[[WP:AWB|自動維基瀏覽器]]
  }}}}，操作者為{{{by|[[:{{#if:{{{site|}}}
  |{{{site}}}
  |zh
 }}:User:{{Trim|{{{1}}}}}|{{Trim|{{{1}}}}}]]（[[:{{#if:{{{site|}}}
  |{{{site}}}
  |zh
 }}:User talk:{{{talklink|{{Trim|{{{1}}}}}}}}|討論]]）{{#if:{{Trim|{{{2|}}}}}
  |{{#if:{{Trim|{{{3|}}}}}
   |、
   |及
  }}[[:zh:User:{{Trim|{{{2}}}}}|{{Trim|{{{2}}}}}]]（[[:zh:User talk:{{{talklink|{{Trim|{{{2}}}}}}}}|討論]]）
 }}{{#if:{{Trim|{{{3|}}}}}
  |及[[:zh:User:{{Trim|{{{3}}}}}|{{Trim|{{{3}}}}}]]（[[:en:User talk:{{{talklink|{{Trim|{{{3}}}}}}}}|討論]]）
 }}}}}，'''屬[[WP:SOCK#LEGIT|合規附屬帳戶]]，以半自動或全自動方式協助用戶處理繁瑣而重複的工作。{{#switch: {{lc:{{{status}}}}}
  |active
  |approved   = {{#if:{{{globalbot|}}}
|此為[{{fullurl:Special:GlobalUsers/Global_bot|limit=1&username={{urlencode:{{{username|{{BASEPAGENAME}}}}}}}}} 全域機械人]，主要依據[[:meta:Bot_policy#Global_bots|元維基機械人方針]]處理跨語言連結或整理雙重重定向，現時在用。{{#if:{{{overridebrfa|}}}|另外，此帳戶亦會處理其他本地事務或者得到本地許可，詳請[[{{{overridebrfa}}}|見此]]。|{{#ifexist:Wikipedia:机器人/申请/{{ifempty|{{{brfa|}}}|{{BASEPAGENAME}}}}|另外，此帳戶得到本地許可，詳情[[Wikipedia:机器人/申请/{{ifempty|{{{brfa|}}}|{{BASEPAGENAME}}}}|見此]]。|}}}}
|{{#ifeq:{{{approvalneeded|}}}|no
 | 此機械人在用，而所處理事務毋須事先取得[[WP:BRFA|許可]]。
 | 此機械人已得到許可，亦正在運作中。{{#if:{{{overridebrfa|}}}|[[WP:BRFA|申請存檔]][[{{{overridebrfa}}}|見此]]|{{#ifexist:Wikipedia:机器人/申请/{{ifempty|{{{brfa|}}}|{{BASEPAGENAME}}}}|[[WP:BRFA|申請存檔]][[Wikipedia:机器人/申请/{{ifempty|{{{brfa|}}}|{{BASEPAGENAME}}}}|見此]]|{{{nocat|[[Category:無指明申請許可而在用維基百科機械人]]}}}}}}}
}}
}}{{{nocat|[[Category:在用維基百科機械人]]}}}
  |inactive   = {{#ifeq:{{{approvalneeded|}}}|no
| 此機械人現時不在用，而之前所負責事務毋須事先得到許可。
| 此機械人現時不在用，然而仍保有{{#if:{{{globalbot|}}}|全域|}}社群[[{{#if:{{{overridebrfa|}}}|{{{overridebrfa}}}|Wikipedia:机器人/申请/{{ifempty|{{{brfa|}}}|{{BASEPAGENAME}}}}}}|許可]]。{{{nocat|[[Category:不在用維基百科機械人]]}}}
}}
  |trial      = 此機械人獲得[[Wikipedia:機械人審核小組|機械人審核小組]]批准有限度試行。{{{nocat|[[Category:未批准維基百科機械人]]}}}
  |unapproved = 此機械人並未獲得社群批准運作，或其操作許可已被撤銷，是故不應進行大規模操作，亦請勿在缺乏操作者監察下運作，操作者及机器人用戶空間除外。{{{nocat|[[Category:未批准維基百科機械人]]}}}
  |#default = {{{nocat|<includeonly>[[Category:未知狀態維基百科機械人]]</includeonly>}}}
 }}{{{more|}}}<br/><small>{{#ifeq:{{lc:{{{awb}}}}}|yes
  |如要使此機械人停止運作直至操作者重啟，請編輯[[User talk:{{PAGENAME}}|機械人討論頁]]。如果討論頁為重定向，請直接編輯重定向本身，而非所指向的頁面。
 }} <span class="sysop-show">'''管理員︰若然此機械人{{#ifeq: {{lc:{{{status}}}}}|unapproved
   |進行大規模操作或相信在缺乏監察下運作，而且所編輯區域並非操作者或機械人用戶名字空間
   |{{#ifeq:{{lc:{{{awb}}}}}|yes
    |在收到提醒或警告訊息後繼續作出有問題編輯
    |失靈或作出有問題編輯
   }}
  }}，請[{{fullurl:Special:Block|wpTarget={{PAGENAMEE}}&wpExpiry=indefinite&wpHardBlock=1&wpAutoBlock=0&wpCreateAccount=0&wpReason=機器人發生故障並必須緊急停止}} 施予封禁]{{#ifeq:{{lc:{{{awb}}}}}|yes
  |或者移除其[[Wikipedia:AutoWikiBrowser/CheckPage|自動維基瀏覽器使用權]]
 }}。'''</span></small>
 |imageright={{#ifeq: {{lc:{{{awb}}}}}|yes
  |[[File:AWB_logo_draft.png|75px]]{{{nocat|[[Category:自动维基浏览器使用者]]}}}
 }}<includeonly>{{{nocat|[[Category:所有維基百科機器人]]{{#if:{{{globalbot|}}}|[[Category:全域維基百科機械人]][[Category:跨語言連接機械人]]|}}}}}</includeonly>
}}<noinclude>
{{documentation}}
</noinclude>