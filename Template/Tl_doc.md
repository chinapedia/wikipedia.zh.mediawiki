{{NoteTA
|G1 = IT
|G2 = MediaWiki
}}
{{Documentation subpage}}
{{High-risk|188844| all-pages = yes }}
<!-- 在本行下編輯模板說明 -->
本模板可以用来创建一个到[[Help:模板|模板]]的带有大括号的链接，以便于使用者复制或查看相关[[Help:模板|模板]]介绍。

== 舉例 ==
=== 目標模板無參數時 ===
<pre>
{{tl|hideH}}
</pre>

{{tl|hideH}}

=== 目標模板只有一個參數時 ===
<pre>-{}-
{{tl|hideH|标题}}
</pre>

{{tl|hideH|标题}}

=== 目標模板有多個參數或命名參數時 ===
==== 無繁簡轉換 ====
<pre>
{{tl|hideH|&lt;nowiki>Head=标题|FrameStyle=整个框架的格式&lt;/nowiki>}}
</pre>

{{tl|hideH|<nowiki>Head=标题|FrameStyle=整个框架的格式</nowiki>}}

==== 可繁簡轉換 ====
<pre>-{}-
{{tl|hideH|Head{{=}}标题{{!}}FrameStyle=整个框架的格式}}
</pre>

{{tl|hideH|Head{{=}}标题{{!}}FrameStyle{{=}}整个框架的格式}}

== 重定向 ==
* {{tlx|t1}}，错字重定向

== 参见 ==
* {{tlx|tls}}，与本模板相似，生成的模板名称前带有“subst:”字样。
* {{tlx|tlx}}，与本模板相似，但可以用管道符“|”方式引入最多11个参数。
* {{tlx|tnull}}，与本模板相似，生成的模板名称不带链接，且可以用管道符“|”方式引入最多7个参数。

<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:维基数据]]） -->
[[Category:鏈接模板|Tl]]
[[Category:輸入支援模板|{{PAGENAME}}]]
}}</includeonly>