{{mbox
| type = notice
| image = [[File:Historical.svg|30px|alt=|link=WP:HISPAGES]]
| imageright = {{#if:{{{1<includeonly>|</includeonly>}}}|{{Ombox/shortcut|{{{1|}}}|{{{2|}}}|{{{3|}}}|{{{4|}}}|{{{5|}}}}}}}
| text = {{#switch:{{NAMESPACE}}
|User|User talk = '''此使用者{{#ifeq:{{BASEPAGENAME}}|{{PAGENAME}}||子}}頁面目前處於閒置狀態，僅為供歷史參考而保留。'''<br/><span style="font-size:90%">此頁面最後更新於{{{last|{{{date|{{#time:Y年n月j日 (D) H:i (T)|{{REVISIONTIMESTAMP}}}}}}}}}}。若希望重啟討論，您可嘗試[[User talk:{{ROOTPAGENAME}}|聯繫此使用者]]，或至[[Wikipedia:互助客栈|互助客棧]]尋求更廣泛的意見。</span>
| #default = {{#switch:{{{type}}}
| policy = '''此[[Wikipedia:方針與指引|維基百科方針]]已經廢止，僅為供歷史參考而保留。'''
| guideline = '''此[[Wikipedia:方針與指引|維基百科指引]]已經廢止，僅為供歷史參考而保留。'''
| woundup = '''此頁面已基於[[Wikipedia:共识|社群共識]]同意關閉，僅為供歷史參考而保留。'''<br/><span style="font-size:90%">若您希望重啟討論，請至[[Wikipedia:互助客栈|互助客棧]]尋求更廣泛的意見。</span>
| section = '''此章節目前處於閒置狀態，僅為供歷史參考而保留。'''
| #default = '''此頁面目前處於閒置狀態，僅為供歷史參考而保留。'''{{#if:{{{brief|}}}||<br/><span style="font-size:90%">此頁面最後更新於{{{last|{{{date|{{#time:Y年n月j日 (D) H:i (T)|{{REVISIONTIMESTAMP}}}}}}}}}}。此頁面的內容可能已無明確的共識支持，或是不再與討論的主題相關。若您希望重啟討論，請至[[Wikipedia:互助客栈|互助客棧]]尋求更廣泛的意見。</span>
}}}}}}<span style="font-size: 90%">{{{comment|{{{reason|{{{result|}}}}}}}}}</span>
}}<includeonly>{{#switch:{{NAMESPACE}}|User|User talk=|#default={{#ifeq:{{{category}}}|no||[[Category:维基百科存档|{{PAGENAME}}]]}}}}</includeonly><noinclude>{{documentation}}</noinclude>