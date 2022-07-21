<includeonly>__NOEDITSECTION__
{{documentation|content=這是'''Template:{{PAGENAME}}'''的說明文件。它是由[[Template:Country showdata]]自動產生的。

<code>Template:{{PAGENAME}}</code>為一系列模板的元模板，亦即本模版將用於構建其他模板，如<code>[[Template:flag|flag]]</code>、<code>[[Template:flagicon|flagicon]]</code>等等。請勿在條目中直接使用此模板。

{{ombox|text=此模板是'''[[WikiProject:紋章及旗幟/旗幟模板|維基百科專題:紋章及旗幟/旗幟模板]]'''的範圍，此專題目的是維護、精進維基百科中的旗幟模板。}}

'''請在對此模板做任何變更後{{purge|重新整理}}此頁面。'''

[[File:{{{flag alias|Flag of None.svg}}}|thumb|{{#if:{{{flag link|}}} | 參見：[[{{{flag link}}}]] | {{#ifexist: Flag of {{{alias}}} | 參見：[[{{{alias}}}旗幟]] | }} }}]]

== 基本參數 ==
<table class="wikitable">
<tr><th>參數名稱</th><th>參數值</th><th>含義</th>
</tr><tr>
<td><code>別名</code></td>
<td>{{#if: {{{alias|}}} | <code>{{{alias}}}</code> | <span style="color:red">'''undefined!'''</span> }}
<td>主條目（[[{{{alias}}}]]）</td>
</tr>
{{#if: {{{name|}}} |
<tr>
<td><code>簡稱</code></td>
<td><code>{{{name}}}</code></td>
<td>（可选）<tt>别名</tt>是一个歧义名称时，显示的维基百科内部链接，如範例所示</td>
</tr>
}}
<tr>
<td><code>旗幟別名</code></td>
<td>{{#if: {{{flag alias|}}} | <code>{{{flag alias}}}</code> | <span style="color:red">'''undefined!'''</span> }}</td>
<td>图片名称（[[:File:{{{flag alias}}}]]，右方圖片）</td>
</tr></table>
{{#if: {{{var1|{{{flag alias-naval|}}}}}} |
== 旗幟變異 ==
{{#if:{{{flag link|}}} | {{details|{{{flag link}}}}} | {{#ifexist: Flag of {{{alias}}} | {{details|Flag of {{{alias}}}}} | }} }}
{{#ifeq:{{{variant|♦}}}|♦|{{red|Note: These variants cannot be used unless the line <code>{{!}} variant {{=}} {{(((}}variant{{!}}{{)))}}</code> is added to this template.}}}}
<table class="wikitable">
<tr><th>標記</th><th>旗幟圖檔 (40px)</th><th>圖片檔案名稱</th></tr>
{{#if: {{{var1|}}} | <tr><td><code>{{{var1}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var1}}}}}}|40px|{{{border-{{{var1}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var1}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var2|}}} | <tr><td><code>{{{var2}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var2}}}}}}|40px|{{{border-{{{var2}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var2}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var3|}}} | <tr><td><code>{{{var3}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var3}}}}}}|40px|{{{border-{{{var3}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var3}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var4|}}} | <tr><td><code>{{{var4}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var4}}}}}}|40px|{{{border-{{{var4}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var4}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var5|}}} | <tr><td><code>{{{var5}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var5}}}}}}|40px|{{{border-{{{var5}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var5}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var6|}}} | <tr><td><code>{{{var6}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var6}}}}}}|40px|{{{border-{{{var6}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var6}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var7|}}} | <tr><td><code>{{{var7}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var7}}}}}}|40px|{{{border-{{{var7}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var7}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var8|}}} | <tr><td><code>{{{var8}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var8}}}}}}|40px|{{{border-{{{var8}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var8}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var9|}}} | <tr><td><code>{{{var9}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var9}}}}}}|40px|{{{border-{{{var9}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var9}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var10|}}} | <tr><td><code>{{{var10}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var10}}}}}}|40px|{{{border-{{{var10}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var10}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var11|}}} | <tr><td><code>{{{var11}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var11}}}}}}|40px|{{{border-{{{var11}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var11}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var12|}}} | <tr><td><code>{{{var12}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var12}}}}}}|40px|{{{border-{{{var12}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var12}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var13|}}} | <tr><td><code>{{{var13}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var13}}}}}}|40px|{{{border-{{{var13}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var13}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var14|}}} | <tr><td><code>{{{var14}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var14}}}}}}|40px|{{{border-{{{var14}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var14}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var15|}}} | <tr><td><code>{{{var15}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var15}}}}}}|40px|{{{border-{{{var15}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var15}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var16|}}} | <tr><td><code>{{{var16}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var16}}}}}}|40px|{{{border-{{{var16}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var16}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var17|}}} | <tr><td><code>{{{var17}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var17}}}}}}|40px|{{{border-{{{var17}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var17}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var18|}}} | <tr><td><code>{{{var18}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var18}}}}}}|40px|{{{border-{{{var18}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var18}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var19|}}} | <tr><td><code>{{{var19}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var19}}}}}}|40px|{{{border-{{{var19}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var19}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var20|}}} | <tr><td><code>{{{var20}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var20}}}}}}|40px|{{{border-{{{var20}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var20}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var21|}}} | <tr><td><code>{{{var21}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var21}}}}}}|40px|{{{border-{{{var21}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var21}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var22|}}} | <tr><td><code>{{{var22}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var22}}}}}}|40px|{{{border-{{{var22}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var22}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var23|}}} | <tr><td><code>{{{var23}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var23}}}}}}|40px|{{{border-{{{var23}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var23}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var24|}}} | <tr><td><code>{{{var24}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var24}}}}}}|40px|{{{border-{{{var24}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var24}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var25|}}} | <tr><td><code>{{{var25}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var25}}}}}}|40px|{{{border-{{{var25}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var25}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var26|}}} | <tr><td><code>{{{var26}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var26}}}}}}|40px|{{{border-{{{var26}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var26}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var27|}}} | <tr><td><code>{{{var27}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var27}}}}}}|40px|{{{border-{{{var27}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var27}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var28|}}} | <tr><td><code>{{{var28}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var28}}}}}}|40px|{{{border-{{{var28}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var28}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var29|}}} | <tr><td><code>{{{var29}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var29}}}}}}|40px|{{{border-{{{var29}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var29}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var30|}}} | <tr><td><code>{{{var30}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var30}}}}}}|40px|{{{border-{{{var30}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var30}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var31|}}} | <tr><td><code>{{{var31}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var31}}}}}}|40px|{{{border-{{{var31}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var31}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var32|}}} | <tr><td><code>{{{var32}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var32}}}}}}|40px|{{{border-{{{var32}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var32}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var33|}}} | <tr><td><code>{{{var33}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var33}}}}}}|40px|{{{border-{{{var33}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var33}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var34|}}} | <tr><td><code>{{{var34}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var34}}}}}}|40px|{{{border-{{{var34}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var34}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var35|}}} | <tr><td><code>{{{var35}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var35}}}}}}|40px|{{{border-{{{var35}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var35}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var36|}}} | <tr><td><code>{{{var36}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var36}}}}}}|40px|{{{border-{{{var36}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var36}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var37|}}} | <tr><td><code>{{{var37}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var37}}}}}}|40px|{{{border-{{{var37}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var37}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var38|}}} | <tr><td><code>{{{var38}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var38}}}}}}|40px|{{{border-{{{var38}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var38}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var39|}}} | <tr><td><code>{{{var39}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var39}}}}}}|40px|{{{border-{{{var39}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var39}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{var40|}}} | <tr><td><code>{{{var40}}}</code></td><td style="text-align:center;">[[File:{{{flag alias-{{{var40}}}}}}|40px|{{{border-{{{var40}}}|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-{{{var40}}}}}}</code></td></tr> }}<!--
-->{{#if: {{{flag alias-naval|}}} | <tr><td><code>naval</code></td><td style="text-align:center;">[[File:{{{flag alias-naval}}}|40px|{{{border-naval|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-naval}}}</code></td></tr> }}<!--
-->{{#if: {{{flag alias-air force|}}} | <tr><td><code>air force</code></td><td style="text-align:center;">[[File:{{{flag alias-air force}}}|40px|{{{border-air force|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-air force}}}</code></td></tr> }}<!--
-->{{#if: {{{flag alias-army|}}} | <tr><td><code>army</code></td><td style="text-align:center;">[[File:{{{flag alias-army}}}|40px|{{{border-army|{{{border|border}}}}}}]]</td><td><code>{{{flag alias-army}}}</code></td></tr> }}<!--
--></table>
}}
{{#if: {{{flag alias-naval|}}}{{{link alias-naval|}}}{{{flag alias-air force|}}}{{{link alias-air force|}}}{{{flag alias-army|}}}{{{link alias-army|}}} |
=== 軍事旗幟 ===
{{#if: {{{flag alias-naval|}}} |
此模板包括海军军旗的变体，可以使用[[Template:Navy]]：
* <code><nowiki>{{navy|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>}}</nowiki></code> → {{navy|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}}}
* <code><nowiki>{{flagicon|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>|naval}}</nowiki></code> → {{flagicon|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}|naval}}
| {{#if: {{{link alias-naval|}}} |
海军旗帜与其国旗相同，因此[[Template:Navy]]产生以下：
* <code><nowiki>{{navy|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>}}</nowiki></code> → {{navy|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}}}
}}}}
{{#if: {{{flag alias-air force|}}} |
此模板包括空军军旗的变体，可以使用[[Template:Air force]]：
* <code><nowiki>{{air force|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>}}</nowiki></code> → {{air force|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}}}
* <code><nowiki>{{flagicon|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>|air force}}</nowiki></code> → {{flagicon|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}|air force}}
| {{#if: {{{link alias-air force|}}} |
空军旗帜与其国旗相同，因此[[Template:Air force]]产生以下：
* <code><nowiki>{{air force|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>}}</nowiki></code> → {{air force|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}}}
}}}}
{{#if: {{{flag alias-army|}}} |
此模板包括陆军军旗的变体，可以使用[[Template:Army]]：
* <code><nowiki>{{army|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>}}</nowiki></code> → {{army|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}}}
* <code><nowiki>{{flagicon|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>|army}}</nowiki></code> → {{flagicon|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}|army}}
| {{#if: {{{link alias-army|}}} |
陆军旗帜与其国旗相同，因此[[Template:Army]]产生以下：
* <code><nowiki>{{army|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>}}</nowiki></code> → {{army|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}}}
}}}} }}
{{#if: {{{redir1|}}} |
== 重定向模板 ==
此模板亦可以以'''別稱'''（其他名稱）使用（以重定向至此模板的方式執行）：<!--
--><table class="wikitable"><!--
--><tr><th>別稱</th><th>{{tlx|flag|''別稱''}}輸出樣貌</th><th>{{tlx|flagicon|''別稱''}}輸出樣貌</th></tr>
{{#if: {{{redir1|}}} | <tr><td><code>{{{redir1}}}</code>（<span class="plainlinks">[{{fullurl:Template:Country data {{{redir1}}}|redirect=no}} 顯示]</span>）</td><td>{{flag|{{{redir1}}}}}</td><td>{{flagcountry|{{{redir1}}}}}</td></tr> }}<!--
-->{{#if: {{{redir2|}}} | <tr><td><code>{{{redir2}}}</code>（<span class="plainlinks">[{{fullurl:Template:Country data {{{redir2}}}|redirect=no}} 顯示]</span>）</td><td>{{flag|{{{redir2}}}}}</td><td>{{flagcountry|{{{redir2}}}}}</td></tr> }}<!--
-->{{#if: {{{redir3|}}} | <tr><td><code>{{{redir3}}}</code>（<span class="plainlinks">[{{fullurl:Template:Country data {{{redir3}}}|redirect=no}} 顯示]</span>）</td><td>{{flag|{{{redir3}}}}}</td><td>{{flagcountry|{{{redir3}}}}}</td></tr> }}<!--
-->{{#if: {{{redir4|}}} | <tr><td><code>{{{redir4}}}</code>（<span class="plainlinks">[{{fullurl:Template:Country data {{{redir4}}}|redirect=no}} 顯示]</span>）</td><td>{{flag|{{{redir4}}}}}</td><td>{{flagcountry|{{{redir4}}}}}</td></tr> }}<!--
-->{{#if: {{{redir5|}}} | <tr><td><code>{{{redir5}}}</code>（<span class="plainlinks">[{{fullurl:Template:Country data {{{redir5}}}|redirect=no}} 顯示]</span>）</td><td>{{flag|{{{redir5}}}}}</td><td>{{flagcountry|{{{redir5}}}}}</td></tr> }}<!--
--></table>
查看[{{fullurl:Special:WhatLinksHere/{{FULLPAGENAMEE}}|hidelinks=1&hidetrans=1}} 全部重定向]。
}}
== 使用範例 ==
* <code><nowiki>{{flag|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>}}</nowiki></code> → {{flag|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}}}
* <code><nowiki>{{flagicon|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>}}</nowiki></code> → {{flagicon|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}}}<!--
-->{{#if: {{{name|}}} |
* <code><nowiki>{{flagcountry|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>}}</nowiki></code> → {{flagcountry|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}}} }}
{{#if: {{{var1|}}} |
=== 使用旗幟變異 ===
* <code><nowiki>{{flag|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>|</nowiki>{{{var1}}}<nowiki>}}</nowiki></code> → {{flag|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}|{{{var1}}}}}
* <code><nowiki>{{flagicon|</nowiki>{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}<nowiki>|</nowiki>{{{var1}}}<nowiki>}}</nowiki></code> → {{flagicon|{{{templatename|{{Str right|{{BASEPAGENAME}}|13}}}}}|{{{var1}}}}}
}}
{{#if: {{{redir1|}}} |
=== 使用重定向模板 ===
* <code><nowiki>{{flagicon|</nowiki>{{{redir1}}}<nowiki>}}</nowiki></code> → {{flagicon|{{{redir1}}}}}
* <code><nowiki>{{flagcountry|</nowiki>{{{redir1}}}<nowiki>}}</nowiki></code> → {{flagcountry|{{{redir1}}}}}
* <code><nowiki>{{flag|</nowiki>{{{redir1}}}<nowiki>}}</nowiki></code> → {{flag|{{{redir1}}}}}
}}
{{#if: {{{related1|}}} |
== 相關模版 ==
请参阅以下相关<code>國家數據</code>模板:
* [[Template:Country data {{{related1}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related1}}}<!-- {{#if:{{{related1param|}}}|{{!}}{{{related1param}}}}} -->}}</span><!--
-->{{#if: {{{related2|}}} |
* [[Template:Country data {{{related2}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related2}}}<!-- {{#if:{{{related2param|}}}|{{!}}{{{related2param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related3|}}} |
* [[Template:Country data {{{related3}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related3}}}<!-- {{#if:{{{related3param|}}}|{{!}}{{{related3param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related4|}}} |
* [[Template:Country data {{{related4}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related4}}}<!-- {{#if:{{{related4param|}}}|{{!}}{{{related4param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related5|}}} |
* [[Template:Country data {{{related5}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related5}}}<!-- {{#if:{{{related5param|}}}|{{!}}{{{related5param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related6|}}} |
* [[Template:Country data {{{related6}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related6}}}<!-- {{#if:{{{related6param|}}}|{{!}}{{{related6param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related7|}}} |
* [[Template:Country data {{{related7}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related7}}}<!-- {{#if:{{{related7param|}}}|{{!}}{{{related7param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related8|}}} |
* [[Template:Country data {{{related8}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related8}}}<!-- {{#if:{{{related8param|}}}|{{!}}{{{related8param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related9|}}} |
* [[Template:Country data {{{related9}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related9}}}<!-- {{#if:{{{related9param|}}}|{{!}}{{{related9param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related10|}}} |
* [[Template:Country data {{{related10}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related10}}}<!-- {{#if:{{{related10param|}}}|{{!}}{{{related10param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related11|}}} |
* [[Template:Country data {{{related11}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related11}}}<!-- {{#if:{{{related11param|}}}|{{!}}{{{related11param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related12|}}} |
* [[Template:Country data {{{related12}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related12}}}<!-- {{#if:{{{related12param|}}}|{{!}}{{{related12param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related13|}}} |
* [[Template:Country data {{{related13}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related13}}}<!-- {{#if:{{{related13param|}}}|{{!}}{{{related13param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related14|}}} |
* [[Template:Country data {{{related14}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related14}}}<!-- {{#if:{{{related14param|}}}|{{!}}{{{related14param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related15|}}} |
* [[Template:Country data {{{related15}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related15}}}<!-- {{#if:{{{related15param|}}}|{{!}}{{{related15param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related16|}}} |
* [[Template:Country data {{{related16}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related16}}}<!-- {{#if:{{{related16param|}}}|{{!}}{{{related16param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related17|}}} |
* [[Template:Country data {{{related17}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related17}}}<!-- {{#if:{{{related17param|}}}|{{!}}{{{related17param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related18|}}} |
* [[Template:Country data {{{related18}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related18}}}<!-- {{#if:{{{related18param|}}}|{{!}}{{{related18param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related19|}}} |
* [[Template:Country data {{{related19}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related19}}}<!-- {{#if:{{{related19param|}}}|{{!}}{{{related19param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related20|}}} |
* [[Template:Country data {{{related20}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related20}}}<!-- {{#if:{{{related20param|}}}|{{!}}{{{related20param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related21|}}} |
* [[Template:Country data {{{related21}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related21}}}<!-- {{#if:{{{related21param|}}}|{{!}}{{{related21param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related22|}}} |
* [[Template:Country data {{{related22}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related22}}}<!-- {{#if:{{{related22param|}}}|{{!}}{{{related22param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related23|}}} |
* [[Template:Country data {{{related23}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related23}}}<!-- {{#if:{{{related23param|}}}|{{!}}{{{related23param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related24|}}} |
* [[Template:Country data {{{related24}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related24}}}<!-- {{#if:{{{related24param|}}}|{{!}}{{{related24param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related25|}}} |
* [[Template:Country data {{{related25}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related25}}}<!-- {{#if:{{{related25param|}}}|{{!}}{{{related25param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related26|}}} |
* [[Template:Country data {{{related26}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related26}}}<!-- {{#if:{{{related26param|}}}|{{!}}{{{related26param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related27|}}} |
* [[Template:Country data {{{related27}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related27}}}<!-- {{#if:{{{related27param|}}}|{{!}}{{{related27param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related28|}}} |
* [[Template:Country data {{{related28}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related28}}}<!-- {{#if:{{{related28param|}}}|{{!}}{{{related28param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related29|}}} |
* [[Template:Country data {{{related29}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related29}}}<!-- {{#if:{{{related29param|}}}|{{!}}{{{related29param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related30|}}} |
* [[Template:Country data {{{related30}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related30}}}<!-- {{#if:{{{related30param|}}}|{{!}}{{{related30param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related31|}}} |
* [[Template:Country data {{{related31}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related31}}}<!-- {{#if:{{{related31param|}}}|{{!}}{{{related31param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related32|}}} |
* [[Template:Country data {{{related32}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related32}}}<!-- {{#if:{{{related32param|}}}|{{!}}{{{related32param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related33|}}} |
* [[Template:Country data {{{related33}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related33}}}<!-- {{#if:{{{related33param|}}}|{{!}}{{{related33param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related34|}}} |
* [[Template:Country data {{{related34}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related34}}}<!-- {{#if:{{{related34param|}}}|{{!}}{{{related34param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related35|}}} |
* [[Template:Country data {{{related35}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related35}}}<!-- {{#if:{{{related35param|}}}|{{!}}{{{related35param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related36|}}} |
* [[Template:Country data {{{related36}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related36}}}<!-- {{#if:{{{related36param|}}}|{{!}}{{{related36param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related37|}}} |
* [[Template:Country data {{{related37}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related37}}}<!-- {{#if:{{{related37param|}}}|{{!}}{{{related37param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related38|}}} |
* [[Template:Country data {{{related38}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related38}}}<!-- {{#if:{{{related38param|}}}|{{!}}{{{related38param}}}}} -->}}</span> }}<!--
-->{{#if: {{{related39|}}} |
* [[Template:Country data {{{related39}}}]]<span style="position:absolute; left:33em;">{{flag|{{{related39}}}<!-- {{#if:{{{related39param|}}}|{{!}}{{{related39param}}}}} -->}}</span> }}<!--
-->}}
{{#ifexist:{{FULLPAGENAME}}/doc |
{{#if:{{Suppress categories|{{{{FULLPAGENAME}}/doc}}}}|
== 其他資訊 ==
}}
{{{{FULLPAGENAME}}/doc|alias={{{alias|}}}|cat={{{cat|}}}}}
}}
[[Category:国家资料模板|{{{alias}}}]]
}}</includeonly><noinclude>
{{documentation}}
</noinclude>