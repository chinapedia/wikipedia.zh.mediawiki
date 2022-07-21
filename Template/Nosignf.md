{{#ifexpr:
  {{#switch:{{#titleparts:{{FULLPAGENAME}}|2}}
    |Wikipedia:頁面存廢討論/記錄
    |Wikipedia:檔案存廢討論/記錄=1
    |#default=0
  }} and {{#iferror: {{#time:U|{{#titleparts:{{FULLPAGENAME}}|3|3}}}} | 0 | {{#time:U|{{#titleparts:{{FULLPAGENAME}}|3|3}}}} >= 1561766400 }}
  |</div>{{error|根據[[WP:DP|刪除方針]][[Wikipedia_talk:删除方针/存档5#修订删除方针|2018年5月的修訂]]，確立了存廢討論不是投票的原則，請勿再使用投票無效標示相關模板（[[Wikipedia_talk:删除方针/存档5#页面存废讨论还是投票|更多討論]]）。對於沒有簽名的留言，請直接使用{{tl|Unsigned}}補簽名，請移除{{tl|Nosignh}}和{{tl|Nosignf}}。[[Category:存廢討論中使用投票無效標示模板的頁面|I]]}}
  |<noinclude><div></noinclude>{{votevoidf|bordercolor=lightpink|text=↑該用戶{{{1|投票}}}無簽名或不符合{{linkSect|WP:SIGN|签名必须包含的部分}}，{{{1|投票}}}無效，但意見可供參考。如是註冊用戶請以「'''<nowiki>—~~~~</nowiki>'''」補充簽名後移除此標籤。{{#if:{{{sign|}}}| - {{{sign}}}}}}}
}}<noinclude>
{{doc|Template:Votevoidf/doc}}
</noinclude>