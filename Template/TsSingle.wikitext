{{#switch: {{{type}}}
| L
| AL =[
}}{{#switch: {{{type}}}
| L
| AL =[{{{link}}}{{!}}
}}-{{{#switch: {{{type}}}
| T=T{{!}}
| AL
| A=A{{!}}
}}{{#switch: {{{varselect}}}
| cn = {{{cn}}}
| hk = {{{hk}}}
| sg = {{{sg}}}
| tw = {{{tw}}}
| {{#if: {{{cn|}}}
  |zh-hans:{{{cn}}};
  |
  }} {{#if: {{{hk|}}}
  |zh-hk:{{{hk}}};
  |
  }} {{#if: {{{sg|}}}
  |zh-sg:{{{sg}}};
  |
  }} {{#if: {{{tw|}}}
  |zh-hant:{{{tw}}};
  |
  }}
}}}-{{#switch: {{{type}}}
| L
| AL=]]
}}<noinclude>這個模板可以用來製作簡單的繁簡轉換模板，適用於用手動轉換太過麻煩，用自動轉換又嫌使用頻率太低或者容易出錯的案例。例如將Template:tsVoldemort定義為：

<pre>
 {{tsSingle
  | type = {{{1}}}
  | varselect = {{{2}}}
  | link = 伏地魔
  | cn = 伏地魔
  | hk = 佛地魔
  | tw = 佛地魔
  | sg = 伏地魔
 }}
</pre>

那麼
<pre>{{tsVoldemort}}</pre>
在大陸簡體、新加坡簡體中會顯示為-{伏地魔}-，在港澳繁體、臺灣正體中會顯示為-{佛地魔}-。

以上的範例定義了目前所支持的所有四種中文字體中的詞語。另外還可以省略港澳和新加坡的詞語定義。目前維基百科會自動將未定義的港澳詞語預設成臺灣詞語，將未定義的新加坡詞語預設為大陸詞語。

<pre>
 {{tsSingle
  | type = {{{1}}}
  | varselect = {{{2}}}
  | link = 伏地魔
  | cn = 伏地魔
  | tw = 佛地魔
 }}
</pre>

製作好的模板，如<nowiki>{{tsVoldemort}}</nowiki>，一共有兩個參數供文章撰寫者設置。第一個參數的可設定值有：
<pre>
  T - 轉換文章標題，把條目標題按照用戶設置改成-{伏地魔}-或-{佛地魔}-，這時<nowiki>{{tsVoldemort|T}}</nowiki>所在的位置不再顯示任何文字
  A - 通篇轉換，設置之後，條目內其他出現-{伏地魔}-或-{佛地魔}-的地方，都會自動轉成用戶需要的字體
  L - 增加連接，連接的目標在tsSingle的link參數中定義
  AL - 以上 A 跟 L 的結合 
</pre>

第二個參數的可設定值有：
<pre>
  cn - 強制顯示大陸字體
  hk - 強制顯示港澳字體
  sg - 強制顯示新加坡字體
  tw - 強制顯示臺灣字體
</pre>


如：

<nowiki>{{tsVoldemort|A}}</nowiki> - 按用戶設置顯示為-{伏地魔}-或-{佛地魔}-，同時進行通篇轉換

<nowiki>{{tsVoldemort||cn}}</nowiki> - （注意有兩個竪槓）無論用戶設置是什麼，強制顯示大陸字體

<nowiki>{{tsVoldemort|AL|tw}}</nowiki> - 進行通篇轉換，加上指向-{佛地魔}-的連接，強制顯示臺灣字體

注意：
* 假如某種字體中的詞語沒有定義的話，強制使用該字體就會出錯，比如說港澳字體沒有定義，在文章中會預設顯示為臺灣字體，但是假如強制顯示港澳字體的話，就不能正常顯示該詞語。
* 第二個參數假如有設置的話，第一個參數的A（通篇轉換）就會失效，第一個參數的AL就會失去A（通篇轉換）的功能，只剩下L（增加連接）。
* 以下兩個參數設置不需要改動，<nowiki>{{tsVoldemort}}</nowiki>通過這兩個參數將自己的兩個參數調給<nowiki>{{tsSingle}}</nowiki>：
<pre>
  | type = {{{1}}}
  | varselect = {{{2}}}
</pre>


[[Category:嵌入式繁簡轉換模板|*]]</noinclude>