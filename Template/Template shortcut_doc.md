{{NoteTA
|G1 = IT
|G2 = MediaWiki
}}
{{Documentation subpage}}
{{tsh|tsh}}
{{缺乏中文說明}}
<!-- 在本行下編輯模板說明 -->

== 用法 ==
本模板能夠在模板的說明頁中顯示模板的{{#if:{{{redirect|}}} |重定向 |-{zh-hans:快捷方式; zh-hant:捷徑;}-}}。

==範例==
===基本===
For one template shortcut named {{tl|uw-v1}}: 

<pre>
{{template shortcut|uw-v1}}
</pre>

{{template shortcut|uw-v1}}
{{clear}}

To indicate that {{tl|uw-vandalism1}} has three shortcuts named: {{tl|uw-v1}}, {{tl|uw-vand1}}, and {{tl|uw-vandal1}}; then the following code may be used:

<pre>
{{template shortcut|uw-v1|uw-vand1|uw-vandal1}}
</pre>

{{template shortcut|uw-v1|uw-vand1|uw-vandal1}}
{{clear}}

=== With additional parameters ===
Using {{para|float|<var>left</var>}} makes this template flow to the left of the page:

<pre>
{{template shortcut|float=left|uw-v1}}
</pre>

{{template shortcut|float=left|uw-v1}}
{{clear}}

Using {{para|pre2|<var>subst:</var>}} and {{para|pre3|<var>subst:</var>}} will show "subst:" before the shortcut links, but within the braces. For example: 
<pre>
{{template shortcut|uw-v1|pre2=subst:|uw-vand1|pre3=subst:|uw-vandal1}}
</pre>

{{template shortcut|uw-v1|pre2=subst:|uw-vand1|pre3=subst:|uw-vandal1}}
{{clear}}

== 重定向 ==
* {{tl|tsh}}

== 參見 ==
* {{tl|shortcut}}, the standard shortcut notice.
** {{tl|shortcut-l}} for a left-aligned standard shortcut notice.
* {{tl|policy shortcut}} for shortcuts to sections of policy pages.

<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:消歧義模板]]
[[Category:模板文件]]
}}</includeonly>