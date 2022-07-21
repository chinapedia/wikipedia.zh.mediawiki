{{#switch: {{{select}}}
| {{{opt1}}} ={{tsSingle
              | type={{{type}}}
              | link={{{link}}}
              | varselect={{{varselect}}}
              | cn={{{cn1|}}}| hk={{{hk1|}}}| tw={{{tw1|}}}| sg={{{sg1|}}}
              }}
| {{{opt2}}} ={{tsSingle
              | type={{{type}}}
              | link={{{link}}}
              | varselect={{{varselect}}}
              | cn={{{cn2|}}}| hk={{{hk2|}}}| tw={{{tw2|}}}| sg={{{sg2|}}}
              }}
| {{{opt3}}} ={{tsSingle
              | type={{{type}}}
              | link={{{link}}}
              | varselect={{{varselect}}}
              | cn={{{cn3|}}}| hk={{{hk3|}}}| tw={{{tw3|}}}| sg={{{sg3|}}}
              }}
| {{{opt4}}} ={{tsSingle
              | type={{{type}}}
              | link={{{link}}}
              | varselect={{{varselect}}}
              | cn={{{cn4|}}}| hk={{{hk4|}}}| tw={{{tw4|}}}| sg={{{sg4|}}}
              }}
|             {{tsSingle
              | type={{{type}}}
              | link={{{link}}}
              | varselect={{{varselect}}}
              | cn={{{cndefault|}}}| hk={{{hkdefault|}}}| tw={{{twdefault|}}}| sg={{{sgdefault|}}}
              }}
}}<noinclude>和[[Template:tsSingle]]相比，這個模板增加了選擇詞語類別的功能，可以用來製作較複雜的繁簡轉換模板，適用於用手動轉換太過麻煩，用自動轉換又嫌使用頻率太低或者容易出錯，同時有多種名稱的詞語（如人名可以分姓、名，國名可以分慣用名、全名、簡稱等）。例如將Template:tsMinervaMc定義為：

<pre>
 {{tsMultiple
  | select = {{{1}}}
  | type = {{{2}}}
  | varselect = {{{3}}}
  | link = 米奈娃·-{麥}-
  | cndefault = 米勒娃·-{麦格}-
  | hkdefault = 米奈娃·-{麥}-
  | sgdefault = 米勒娃·-{麦格}-
  | twdefault = 米奈娃·-{麥}-
  | opt1 = last
  | cn1 = -{麦格}-
  | hk1 = -{麥}-
  | sg1 = -{麦格}-
  | tw1 = -{麥}-
  | opt2 = first
  | cn2 = 米勒娃
  | hk2 = 米奈娃
  | sg2 = 米勒娃
  | tw2 = 米奈娃
 }}
</pre> <!-- 假如真要製作這個模板的話，請把手動轉換標籤拿掉。-->

那麼
<pre>{{tsMinervaMc}}</pre>
在大陸簡體、新加坡簡體中會顯示為-{米勒娃·麦格}-，在港澳繁體、臺灣正體中會顯示為-{米奈娃·麥}-。

opt1、opt2等參數可用來命名不同類別的詞語，如以上將opt1命名為last（姓），將opt2命名為first（名）。和opt1對應的詞語用cn1、hk1、sg1、tw1定義，依此類推。而cndefault、hkdefault、twdefault、sgdefault則在沒有特定選擇任何一種類別的情況下顯示。

詞語類別用<nowiki>tsMinervaMc</nowiki>的第一個參數來選擇，如：
<pre>{{tsMinervaMc|last}}</pre>
在大陸簡體、新加坡簡體中會顯示為-{麦格}-，在港澳繁體、臺灣正體中會顯示為-{麥}-。
<pre>{{tsMinervaMc|first}}</pre>
在大陸簡體、新加坡簡體中會顯示為-{米勒娃}-，在港澳繁體、臺灣正體中會顯示為-{米奈娃}-。

此模板所支持的最高類別數為'''四個'''：opt1、opt2、opt3、opt4。如果需要更多選項的話，請使用支持'''十六個'''類別選項的[[Template:TsMultiple16]]。

以上的範例定義了目前所支持的所有四種中文字體中的詞語。另外還可以省略港澳和新加坡的詞語定義。目前維基百科會自動將未定義的港澳詞語預設成臺灣詞語，將未定義的新加坡詞語預設為大陸詞語。

<pre>
 {{tsMultiple
  | select = {{{1}}}
  | type = {{{2}}}
  | varselect = {{{3}}}
  | link = 米奈娃·-{麥}-
  | cndefault = 米勒娃·-{麦格}-
  | twdefault = 米奈娃·-{麥}-
  | opt1 = last
  | cn1 = -{麦格}-
  | tw1 = -{麥}-
  | opt2 = first
  | cn2 = 米勒娃
  | tw2 = 米奈娃
 }}
</pre> <!-- 假如真要製作這個模板的話，請把手動轉換標籤拿掉。-->

製作好的模板，如<nowiki>{{tsMinervaMc}}</nowiki>，一共有三個參數供文章撰寫者設置。第一個參數用來選擇所顯示的詞語類別，上面已經講過。第二個參數的可設定值有：
<pre>
  T - 轉換文章標題，把條目標題按照用戶設置改成-{米勒娃·麦格}-或-{米奈娃·麥}-，這時<nowiki>{{tsMinervaMc||T}}</nowiki>所在的位置不再顯示任何文字
  A - 通篇轉換，設置之後，條目內其他出現-{米勒娃·麦格}-或-{米奈娃·麥}-的地方，都會自動轉成用戶需要的字體
  L - 增加連接，連接的目標在tsMultiple的link參數中定義
  AL - 以上 A 跟 L 的結合 
</pre>

第三個參數的可設定值有：
<pre>
  cn - 強制顯示大陸字體
  hk - 強制顯示港澳字體
  sg - 強制顯示新加坡字體
  tw - 強制顯示臺灣字體
</pre>

如：

<nowiki>{{tsMinervaMc||A}}</nowiki> - （注意有兩個竪槓）按用戶設置顯示為-{米勒娃·麦格}-或-{米奈娃·麥}-，同時進行通篇轉換

<nowiki>{{tsMinervaMc|||cn}}</nowiki> - （注意有三個竪槓）無論用戶設置是什麼，強制顯示大陸字體

<nowiki>{{tsMinervaMc|first|A}}</nowiki> - 只顯示-{米勒娃}-或-{米奈娃}-，同時進行通篇轉換

<nowiki>{{tsMinervaMc|last||hk}}</nowiki> - （注意有兩個竪槓）強制顯示港澳字體中的-{麥}-

<nowiki>{{tsMinervaMc|first|AL|tw}}</nowiki> - 進行通篇轉換，加上指向-{米奈娃·麥}-的連接，強制顯示臺灣字體中的-{米奈娃}-

注意：
* 假如某種字體中的詞語沒有定義的話，強制使用該字體就會出錯，比如說港澳字體沒有定義，在文章中會預設顯示為臺灣字體，但是假如強制顯示港澳字體的話，就不能正常顯示該詞語。
* 第三個參數假如有設置的話，第二個參數的A（通篇轉換）就會失效，第二個參數的AL就會失去A（通篇轉換）的功能，只剩下L（增加連接）。
* 以下三個參數設置不需要改動，<nowiki>{{tsMinervaMc}}</nowiki>通過這三個參數將自己的三個參數調給<nowiki>{{tsMultiple}}</nowiki>：
<pre>
  | select = {{{1}}}
  | type = {{{2}}}
  | varselect = {{{3}}}
</pre>


[[Category:嵌入式繁簡轉換模板|*]]</noinclude>