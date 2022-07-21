<includeonly><!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{template doc page viewed directly}}</noinclude>
== 使用方法 ==
<code><nowiki>{{標音|字= |繁= |简= |拼音= |注音= |粤拼= |臺羅= |中古= |南京= |上古= |反切= |同音字= }}</nowiki></code>

所有欄位均為選用，至少應填寫一項標音方有意義。

{| class="wikitable" 
!參數||說明
|-
| <code>字</code>、<code>char</code>|| 若僅標註之前詞語中的一個字，用此標明，不必區分繁簡
|-
| <code>繁</code>、<code>t</code>|| 需要注音的漢字的繁体字型。若聯係上文很清楚，可留空
|-
| <code>-{简}-</code>、<code>-{簡}-</code>、<code>s</code>|| 需要注音的漢字的简化字型。若聯係上文很清楚，可留空
|-
| <code>拼音</code>、<code>pinyin</code>、<code>pin</code>|| [[汉语拼音方案]]
|-
| <code>注音</code>、<code>zhuyin</code>、<code>zhu</code>|| [[注音符號]]
|-
| <code>南京官話</code>、<code>南京官话</code>、<code>南京</code>、<code>langjin</code>|| [[南京話拉丁化方案#輸入法方案]]
|-
| <code>-{粤拼}-</code>、<code>-{粵拼}-</code>、<code>jyutping</code>、<code>jyut</code>|| [[香港語言學學會粵語拼音方案]]
|-
| <code>-{臺羅}-</code>、<code>-{臺羅}-</code>、<code>tailo</code>、<code>台羅</code>|| [[中華民國教育部|中華民國（臺灣）教育部]]
|-
|<code>中古</code>||中古漢語擬音，請附上擬音版本跟來源
|-
|<code>上古</code>||上古漢語擬音，請附上擬音版本跟來源
|-
|<code>反切</code>||[[反切]]，不要把“切”字寫出
|-
|<code>同音字</code>||標註的同音字最好普通話和中古音都和被標註字同音，非多音字，且常用
|-
|<code>括</code>、<code>br</code>|| 若設為<code>yes</code>，則所有文字前後加括號
|-
| <code>-{链}-</code>、<code>-{連}-</code>、<code>link</code>|| 若設為<code>no</code>，則不為各拼音方法添上內部連結
|-
|-
|<code>fs</code>||字号
|}
<!-- 也可使用<nowiki>{{subst:標音/auto}}</nowiki> -->

== 使用範例 ==

{| class="wikitable"
|+
! 代碼!! 效果
|-
| <code><nowiki>{{標音|繁=數|简=数|拼音=shù|注音=ㄕㄨˋ|粤拼=sou3|中古=sryoh|反切=色句|同音字=㡏}}</nowiki></code>
|| {{標音|繁=數|简=数|拼音=shù|注音=ㄕㄨˋ|粤拼=sou3|中古=sryoh|反切=色句|同音字=㡏}}
|-
| <code><nowiki>尚書{{標音|字=尚|拼音=shàng|注音=ㄕㄤˋ|中古=zjang|反切=市羊|同音字=上|br=yes}}</nowiki></code>
|| 尚書{{標音|字=尚|拼音=shàng|注音=ㄕㄤˋ|中古=zjang|反切=市羊|同音字=上|br=yes}}
|}

==參見==
* {{tl|pron-zh}}，重定向至此
* {{tl|lang-pinyin}}，用於顯示漢語拼音
* {{tl|lang-zhuyin}}，用於顯示注音符號
<includeonly>
[[Category:多语言支持模板]]
[[Category:漢語標音模板]]
</includeonly>