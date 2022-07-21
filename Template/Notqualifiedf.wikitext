{{#ifexpr:
  {{#switch:{{#titleparts:{{FULLPAGENAME}}|2}}
    |Wikipedia:頁面存廢討論/記錄
    |Wikipedia:檔案存廢討論/記錄=1
    |#default=0
  }} and {{#iferror: {{#time:U|{{#titleparts:{{FULLPAGENAME}}|3|3}}}} | 0 | {{#time:U|{{#titleparts:{{FULLPAGENAME}}|3|3}}}} >= 1561766400 }}
  |</div>{{error|根據[[WP:DP|刪除方針]][[Wikipedia_talk:删除方针/存档5#修订删除方针|2018年5月的修訂]]，確立了存廢討論不是投票的原則，請勿再使用投票無效標示相關模板（[[Wikipedia_talk:删除方针/存档5#页面存废讨论还是投票|更多討論]]）。請移除{{tl|Notqualifiedh}}和{{tl|Notqualifiedf}}。[[Category:存廢討論中使用投票無效標示模板的頁面|Q]]}}
  |<noinclude><div></noinclude>{{votevoidf|bordercolor=green|text=↑該用戶不符合{{#if:{{{rfa|}}}|[[Wikipedia:人事任免投票資格|人事任免投票資格]]|資格，投票者必须在本討論發起時已为[[Wikipedia:自動確認用戶|自動確認用戶]]{{#if:{{{expect|}}} |（{{{expect|}}}除外）| {{#switch:{{#titleparts:{{FULLPAGENAME}}|1|}}
|Wikipedia:頁面存廢討論|Wikipedia:檔案存廢討論=（原作者或上傳者除外）
|#default=
}}}}}}，所以投票無效，但意見仍可供參考。{{#if:{{{sign|}}}|{{{sign}}}}}}}
}}<noinclude>
{{doc|Template:Votevoidf/doc}}
</noinclude>