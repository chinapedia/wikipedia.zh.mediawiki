<includeonly>{{#ifeq:{{{Twinkle|}}}|no||{{Twinkle standard installation}}}}</includeonly>
本模板是基於[[Wikipedia:專題/用戶警告]]的指引而設計的。

請在使用用戶警告模板前參閱[[WP:UTM|用戶警告模板的索引頁]]。選擇最適合的用戶警告模板能減少用戶對你所留下訊息的困惑。

'''注意：'''只有[[WP:ADMIN|管理員]]才能封禁用戶，在用戶討論頁裡加入一個封禁模板並不會構成封禁行動，參見[[WP:RFAA|Wikipedia:請求管理員幫助]]以建立一個用戶封禁請求。

=== 用法 ===
請謹記要使用{{tls|{{PAGENAME}}}}代碼來[[Help:替換引用|替代]]本模板，而不是直接使用{{tl|{{lcfirst:{{PAGENAME}}}}}}代碼。

要指明一個短暫性的封禁，請使用代碼：<code><nowiki>{{subst:</nowiki>{{PAGENAME}}{{!}}time=封禁時間<nowiki>}}</nowiki></code>，否則將顯示預設文字「暫時'''[[WP:封禁方针|禁止]]'''」。要指明一個無限期的封禁，請使用代碼<code><nowiki>{{subst:</nowiki>{{PAGENAME}}{{!}}indef=yes<nowiki>}}</nowiki></code>

要為您的訊息提供更多資訊，您可以指定：封禁對象是否匿名用戶、封禁時間、原因、是否允許編輯對話頁、用戶編輯的頁面、是否自動包含您的簽名。
:<code><nowiki>{{subst:</nowiki>{{PAGENAME}}{{#ifeq:{{{allow anon|yes}}}|yes|{{!}}'''anon'''=yes}}{{!}}<span style="color:#c00;">'''time'''</span>=封禁時間{{!}}<span style="color:#c00;">'''reason'''</span>=封禁原因{{#ifeq:{{{allow notalk|yes}}}|yes|{{!}}'''notalk'''=yes}}{{!}}'''admin'''=執行封禁的管理員{{!}}<span style="color:#c00;">'''page'''</span>=用戶編輯的頁面{{!}}'''sig'''=yes{{{extra params|}}}<nowiki>}}</nowiki></code>

{{Block templates}}
[[Category:封禁模板]]