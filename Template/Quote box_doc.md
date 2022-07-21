<includeonly><!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{Documentation subpage}}</noinclude>
<!-- 請在這條線之下編輯模板的說明文件 -->{{Uses TemplateStyles|Template:Quote box/styles.css}}
== 用法 ==
'''Quote box''' 模板可以容易地加上一個有關的引用和一個小的藍色圖像，可以加上你想要的圖像。

== 參數 ==
=== 參數說明 ===
==== 基本參數 ====
* <code>title</code> = 文字標題
* <code>quote</code> = 引用內容
* <code>source</code> = 來源

==== 主要參數 ====
* <code>align</code> - 方框放置位置，可選參數為：left、right、center、none，默認為居右。
* <code>width</code> - 方框寬度，默認滿數為100%。
* <code>border</code> - 方框邊框線大小。默認為1px，可以設置，單位為“[[像素|px]]”或“[[em (字体排印学)|em]]”。
* <code>fontsize</code> - 文本字體的大小，默認為88%。
* <code>bgcolor</code> - 方框文字的背景色，默認是灰色，#F9F9F9。
* <code>style</code> - CSS風格。

==== 標題參數 ====
* <code>title_bg</code> - 標題背景色，默認是灰色，#F9F9F9。
* <code>title_fnt</code> - 標題字體顏色，默認是黑色，black。
* <code>tstyle</code> - 標題CSS風格。

==== 引用內容參數 ====
* <code>qalign</code> - 引用內容的位置，可選參數為：left、right、center。默認是居左，left。
* <code>qstyle</code> - 引用內容的CSS風格。
* <code>quoted</code> - 引用內容是否顯示引號，可選參數為：“1”。

==== 來源參數 ====
* <code>salign</code> - 來源的顯示位置，可選參數為：left、right、center，默認結果同引用內容參數“qalign”一樣。
* <code>sstyle</code> - 來源自的CSS風格。

=== 常用參數 ===
<pre>-{}-
{{Quote_box
| width =（寬度）
| align =（排列）
| quote =（引語）
| source =（出處）
|}}
</pre>

=== 全部參數 ===
<PRE>
{{Quote box
 |title = 
 |quote = 
 |source = 
 |align = 
 |width = 
 |border = 
 |fontsize = 
 |bgcolor = 
 |style = 
 |title_bg = 
 |title_fnt = 
 |tstyle = 
 |qalign = 
 |qstyle = 
 |quoted = 
 |salign = 
 |sstyle = 
}}
</PRE>

== 示例 ==
以下為基本的常用方式，詳情參見： [[Template:Quote_box/examples]]。

'''文段和來源'''
<PRE>
{{Quote box
 |quote  = 桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
}}
</PRE>

{{Quote box
 |quote  = 桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
}}
{{Clear}}

'''文段、來源、寬度和顯示位置居右'''
<pre>
{{Quote_box
| width = 45%
| align = right
| quote = 桃李不言，下自成蹊，此言雖小，可以諭大也。
| source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
|}}
</pre>

{{Quote_box
| width = 45%
| align = right
| quote = 桃李不言，下自成蹊，此言雖小，可以諭大也。
| source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
|}}
{{Clear}}

'''文段、來源、寬度和顯示位置居左'''
<PRE>
{{Quote box
 |quote  = 桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
 |width  = 50%
 |align  = left
}}
</PRE>

{{Quote box
 |quote  = 桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
 |width  = 50%
 |align  = left
}}
{{Clear}}

'''文段、來源、寬度和顯示位置居中'''

<PRE>
{{Quote box
 |quote  = 桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
 |width  = 50%
 |align  = center
}}
</PRE>

{{Quote box
 |quote  = 桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
 |width  = 50%
 |align  = center
}}
{{brClear}}

== 結合其他模板 ==

'''結合大引號'''
<PRE>
{{Quote box
 |quote  = 桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
 |quoted = 1
}}
</PRE>

{{Quote box
 |quote  = 桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
 |quoted = 1
}}
{{brClear}}

'''標題居中'''
<PRE>
{{Quote box
 |title = Centered quote
 |quote  = 桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
 |qalign = center
}}
</PRE>

{{Quote box
 |title = Centered quote
 |quote  = 桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source =  [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
 |qalign = center
}}
{{brClear}}

'''標題居左，文段居右'''
<PRE>
{{Quote box
 |title = Left title, right quote
 |tstyle = text-align: left;
 |quote  = 桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
 |qalign = right
}}
</PRE>

{{Quote box
 |title = Left title, right quote
 |tstyle = text-align: left;
 |quote  =桃李不言，下自成蹊，此言雖小，可以諭大也。
 |source = [[司馬遷]]，《[[史記]]》，卷109，《李將軍列傳》。
 |qalign = right
}}
{{brClear}}

===相關模板===
{{Quotation templates}}

<includeonly>{{#ifeq:{{SUBPAGENAME}}|sandbox | |
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:引文模板]]
}}</includeonly>