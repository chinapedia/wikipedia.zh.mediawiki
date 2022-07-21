{{NoteTA
|G1 = IT
|G2 = MediaWiki
}}
{{Documentation subpage}}
{{High-use|719405|all-pages=yes}}
{{Esoteric}}
<!-- 在本行下編輯模板說明 -->
使用本模板可在條目中顯示註腳（{{tag|ref}}）列表。其涵盖了{{tag|references|s}}的所有功能。

==参数解说 ==

{{tlc|1=Reflist|2=欄位數/欄位寬度|3=group=组别|4=refs=列表內容|5=liststyle=|6=list=}}

本模板所有参数均为可选

; 无名参数1
: 按固定寬度分欄（填入[[em (字体排印学)|em]]等排印单位）：如{{tlc|Reflist|25em}}，瀏覽器會依照這個數值和當前的視窗大小，自動調整欄位數目。
: 按列数分欄（填入自然数；此機制不建議使用）：如{{tlc|Reflist|2}}將會創造出一個兩欄式的的注釋列表，而{{tlc|Reflist|3}}會產生一個三欄式的列表。視窗大小可变，请慎重定义列数。
: 不填任何内容默认为1。 
; <code>group</code>
: 参见[[#分組註釋|分组注释]]
; <code>refs</code>
: 将脚注内容集中到一起存放，参见[[#统一存放参考信息集]]
; <code>liststyle</code>
:
; <code>list</code>
: 手工列出一般参考资料，使用此参数时，模板原本列出{{tag|references|s}}的功能会无效化。可用{{tl|ReflistH}}/{{tl|ReflistF}}模板替代。

=== 过时参数 ===
; <code>colwidth</code>
: 已合并到无名参数1

== 用法 ==

{{markup|title=只使用内文注释
|<nowiki>一條青龍一氣通<ref>參考1</ref>，二盤連莊二本場<ref>參考2</ref>。

==參考資料==
{{Reflist}}</nowiki>
|一條青龍一氣通<ref>參考1</ref>，二盤連莊二本場<ref>參考2</ref>。

{{fake heading|參考資料}}
{{Reflist}}
}}

{{markup|title=只使用一般注释
|<nowiki>一條青龍一氣通，二盤連莊二本場。

==參考資料==
{{Reflist|list=
* 书目a
* 书目b
}}</nowiki>
|一條青龍一氣通，二盤連莊二本場。

{{fake heading|參考資料}}
{{Reflist|list=
* 书目a
* 书目b
}}
}}

{{markup|title=内文与一般注释混合使用
|<nowiki>一條青龍一氣通<ref>參考1</ref>，二盤連莊二本場<ref>參考2</ref>。

==參考資料==
{{Reflist}}

{{Reflist|list=
* 书目a
* 书目b
}}</nowiki>
|一條青龍一氣通<ref>參考1</ref>，二盤連莊二本場<ref>參考2</ref>。

{{fake heading|參考資料}}
{{Reflist}}

{{Reflist|list=
* 书目a
* 书目b
}}
}}

=== 分栏 ===

{{Rellink|不支持Internet Explorer 9、Firefox 1.0、Safari 2、Opera 11.0及更低版本，这些浏览器只会显示为单行}}

複數欄位是使用 [[CSS|CSS3]] 作為基礎，目前使用[[Gecko]]（如[[Mozilla Firefox]]等）与[[Kestrel]]（[[Opera]]9.5及以上版本）作排版引擎的瀏覽器會得到較佳的效果{{efn-ur|1={{cite web|url=http://www.stuffandnonsense.co.uk/archives/css3_multi-column_thriller.html|title=CSS3 Multi-Column Thriller|accessdate=2006年11月24日|date=2005年12月30日}}}}，但由於 CSS 是網頁上的標準之一，因此日後將能適用在更多的瀏覽器{{efn-ur|1={{cite web|url=http://www.w3.org/TR/css3-multicol|title=CSS3 module: Multi-column layout|publisher=[[World Wide Web Consortium|W3C]]|date=2005年12月15日|accessdate=2006年11月24日}}}}。

按宽度分栏（例如<code><nowiki>{{Reflist|30em}}</nowiki></code>）会让浏览器在给定最小宽度的前提下（如宽度至少为30 em），显示尽可能多的栏目。宽度单位支持em, ex, in, cm, mm, pt, pc, px，但是通常使用em。数字和单位之间不能有空格。不支持使用百分比。

根据参考内容的宽度选择合适的宽度：

* 30em：当有大量参考文献且参考条目有一页宽时适用。例如：{{oldid|張伯苓|71040939#参考文献}}
* 20em：当有宽度较短的[[哈佛参考文献格式]]（如{{t1|Template:Sfn}}）时适用。例如：{{oldid|南方十字 (无字小说)|71611463#脚注}}.

{{markup|title=分为2栏
|<nowiki>一條青龍一氣通<ref>參考1</ref>，二盤連莊二本場<ref>參考2</ref>。

==參考資料==
{{Reflist|2}}</nowiki>
|一條青龍一氣通<ref>參考1</ref>，二盤連莊二本場<ref>參考2</ref>。

{{fake heading|參考資料}}
{{Reflist|2}}
}}

{{markup|title=按30em宽度分栏
|<nowiki>一條青龍一氣通<ref>參考1</ref>，二盤連莊二本場<ref>參考2</ref>。

==參考資料==
{{Reflist|30em}}</nowiki>
|一條青龍一氣通<ref>參考1</ref>，二盤連莊二本場<ref>參考2</ref>。

{{fake heading|參考資料}}
{{Reflist|30em}}
}}

=== 分組註釋 ===

於2008年6月開始，腳註系統支援了把註釋分成不同組合。這允許組合註釋、參考以及其他。請參閱 {{en icon}}[[:en:Wikipedia:Footnotes#Separating reference lists and explanatory notes|Wikipedia:Footnotes#Separating reference lists and explanatory notes]]。

標籤的原始碼为{{tag|ref group&#61;''"groupname"''|open}}，对应註腳列表的原始碼，{{tlx|Reflist|group&#61;''"groupname"''}}。而其中的「groupname」是組合的名稱，如「注」、「参」或「标签」。注意groupname对简繁体敏感。

部分分组会显示特殊效果，如{{tag|ref|params=group="upper-alpha"}}的生成的脚注为{{dummy ref|A}}，{{tag|ref|params=group="lower-alpha"}}生成的为{{dummy ref|a}}。

{{markup | title = 按“注释”和“参考”分组
|<nowiki>三元兼四喜，滿貫<ref group="注释">注释1</ref>遇全么<ref group="参考">参考1</ref>。

花<ref group="注释">注释2</ref>自槓頭髮，月從海底撈<ref group="参考">参考2</ref>。

==注释和参考资料==
===注释===
{{Reflist|group=注释}}

===参考===
{{Reflist|group=参考}}</nowiki>
|三元兼四喜，滿貫<ref group="注释">注释1</ref>遇全么<ref group="参考">参考1</ref>。

花<ref group="注释">注释2</ref>自槓頭髮，月從海底撈<ref group="参考">参考2</ref>。

{{fake heading|注释和参考资料}}
{{fake heading|sub=3|注释}}
{{Reflist|group=注释}}
{{fake heading|sub=3|参考}}
{{Reflist|group=参考}}
}}
=== 统一存放参考信息集 ===
<!-- As of September 2009, references may be defined within {{tl|Reflist}} using {{para|refs}} and invoked within the content. There are new error messages associated with this update, documented at [[Help:Cite errors]]. -->
从2014年2月开始，该模板可以通过{{para|refs}}统一存放注脚信息来方便管理。此次更新的相關引用错误问题的提示文件見[[:en:Help:Cite errors]]。

{{markup | title = 示例
|<nowiki>这是参考A<ref name="refname1" />。

这是参考B<ref name="refname2" />。

==参考资料==
{{Reflist|refs=
<ref name="refname1">内容1</ref>
<ref name="refname2">内容2</ref>
}}</nowiki>
|这是参考A<ref name="refname1" group=upper-alpha/>。

这是参考B<ref name="refname2" group=upper-alpha/>。

{{fake heading|参考资料}}
{{Reflist|group=upper-alpha|refs=
<ref name="refname1">内容1</ref>
<ref name="refname2">内容2</ref>
}}
}}

==模板數據==
{{templatedataheader}}
<templatedata>
{
  "description": "在條目中加入一個使用較小字級顯示的註腳列表。",
  "params": {
    "colwidth": {
      "label": "欄位的寬度",
      "description": "瀏覽器會依照這個數值和當前的視窗大小自動調整欄位數目，請依照該頁面中注釋的平均寬度來填寫欄位的寬度數值。填入後參數「1」將被忽略。",
      "type": "string/line",
      "required": false
    },
    "1": {
      "label": "欄位的數目",
      "description": "欄位的數目，填入2將創造一個兩欄式的的注釋列表，如此類推。",
      "type": "number",
      "default": "1",
      "required": false
    },
    "list": {
      "label": "自定義註釋內容",
      "description": "自定義註釋內容。",
      "default": "<references />",
      "type": "string",
      "required": false
    },
    "refs": {
      "type": "string",
      "required": false
    },
    "group": {
      "label": "註腳組別名稱",
      "description": "註腳組別的名稱，即在插入參考文獻時「使用此組」輸入的名稱。",
      "type": "string/line",
      "required": false
    }
  }
}
</templatedata>

==参考文献==
{{notelist-ur}}

==參見==
* {{tlx|ReferencesWithExtra}}
* {{tlx|Notelist}}
* {{tlx|Template reference list}}
* 在討論頁顯示參考文獻請用{{tlx|Reflist-talk}}
* [[Help:脚注]]
* [[Wikipedia:列明来源]]
<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:引用模板| ]]
[[Category:頁面訊息模板|註]]
}}</includeonly>