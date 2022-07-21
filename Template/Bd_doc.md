{{NoteTA
|G1 = IT
|G2 = MediaWiki
}}
{{Documentation subpage|[[Template:Bd]]和[[Template:BD]]}}
<includeonly>{{#ifeq:{{#titleparts:{{PAGENAME}}|1}}|Bd
 | {{High-risk|184959}} <!-- Template:Bd -->
 | {{High-use|13987}} <!-- Template:BD -->
}}</includeonly>
<!-- 在本行下編輯模板說明 -->
{{tlx|bd}}和{{tlx|BD}}模板用于人物条目的首段生卒说明，模板产生一致的生卒日期文字显示（比如标准的连接号），并自动产生相关的生卒日期归类。两个模板用法相同，差别在于后者多输出两侧的小括号“（”与“）”。

两个模板只能用于人物条目正文中，并且只得使用一次。在人物信息框等表格中，请使用{{tlx|birth date and age}}及{{tlx|death date and age}}模板（若出生月日不確定，則使用{{tlx|birth year and age}}及{{tlx|death year and age}}模板）。

== 用法 ==
<pre>{{bd|b1|b2|d1|d2|catIdx=分类索引}}</pre>
其中参数b1、b2、d1、d2分别是出生年、出生月日或自定义日期、逝世年、逝世月日或自定义日期。catIdx定义在分类中的索引，可省略。

#当出生年份确定时，参数b1填“b1年”，b2填月日。自动生成'''b1年出生'''的分类。
#当逝世年份确定时，参数d1填“d1年”，d2填月日。自动生成'''d1年逝世'''的分类。<br/>（以上两种情况，“月日”可以不填，年月日都不能加链接。）
#当出生年份不準確时，参数b1置空，b2填相应的描述。如<code><nowiki>{{bd||约1957年|1989年|3月}}</nowiki></code>
#当逝世年份不準確时，参数d1置空，d2填相应的描述。如<code><nowiki>{{bd|1973年|4月16日||？}}</nowiki></code>
#当出生年份不知道时，参数b1填“？”。如<code><nowiki>{{bd|？||1989年|3月}}</nowiki></code>
#当逝世年份不知道时，参数d1填“？”。如<code><nowiki>{{bd|1973年|4月16日|？|}}</nowiki></code>
#当仍然在世时，参数d1、d2均置空。如<code><nowiki>{{bd|1973年|4月16日||}}</nowiki></code>

== 举例 ==
=== 例一 ===
例如，介绍“[[成吉思汗]]”的生卒时间，可引用{{tlx|bd}}模板：
<pre>'''成吉思汗'''（蒙古语：……，{{bd|1162年|5月31日|1227年|8月25日|catIdx=成}}），……</pre>

页面显示：

'''成吉思汗'''（蒙古语：……，{{bd|1162年|5月31日|1227年|8月25日|catIdx=成}}），……

并且人物被自动归类到[[:Category:1162年出生]]和[[:Category:1227年逝世]]，索引字为“成”。
=== 例二 ===
介绍“[[胡適]]”的生卒时间，可引用{{tlx|BD}}模板，两侧不用再加小括号：
<pre>'''胡適'''{{BD|1891年|12月17日|1962年|2月24日|胡}}，……</pre>

页面显示：

'''胡適'''{{BD|1891年|12月17日|1962年|2月24日|胡}}，……

与上例相似的归类将自动产生。

== 模板數據 ==
<templatedata>
{
  "description": "用於人物條目的首段生卒說明，模板產生一致的生卒日期文字顯示（比如標準的連接號），並自動產生相關的生卒日期歸類。",
  "params": {
    "1": {
      "label": "出生年份",
      "description": "出生年份，並自動加入該年份出生的分類。當出生年份不確定時，請於「出年月日」參數填相應的描述。如{{bd||约1957年}}",
      "example": "1900年",
      "type": "string",
      "required": false
    },
    "2": {
      "label": "出生月日",
      "description": "出生月日，如12月31日",
      "example": "1月1日",
      "type": "string",
      "required": false
    },
    "3": {
      "label": "逝世年份",
      "description": "逝世年份，並自動加入該年份逝世的分類。當逝世年份不確定時，請於「逝世月日」參數填相應的描述。如{{bd|1973年|4月16日||？}}；如仍然在世，請留空",
      "example": "2000年",
      "type": "string",
      "required": false
    },
    "4": {
      "label": "逝世月日",
      "description": "逝世月日；如仍然在世，請留空",
      "example": "12月31日",
      "type": "string",
      "required": false
    },
    "catIdx": {
      "label": "分類索引",
      "description": "填入後，將按照此參數於分類進行索引",
      "example": "陳",
      "type": "string",
      "aliases": ["5"],
      "default": "{{PAGENAME}}",
      "required": false
    }
  }
}
</templatedata>

== 重定向 ==
* {{tl|生卒}}

== 参见 ==
* {{tlx|Birth date and age}}，用于显示出生日期，并自动加注今年的年龄。

<includeonly>{{sandbox other||
<!-- 本行下加入模板的分類，跨維基連結加入Wikidata（參見[[Wikipedia:Wikidata]]） -->
[[Category:生卒模板]]
[[Category:輸入支援模板]]
}}</includeonly>