<noinclude>{{template doc page viewed directly}}</noinclude>
'''此模板'''（{{tl|templatesnotice}}）應置於列在[[Wikipedia:模板消息/用戶討論名字空間]]的[[:Category:用戶警告模板|用戶警告模板]]裡。

==捷徑==
此模板可顯示最多三個的模板捷徑：即位於[[:Category:用戶警告模板的重定向模板]]的模板，例如{{tl|uw-t1}}。要加入模板捷徑，只需填上模板的名稱便可（省去「Template:」字樣）。
 <nowiki>{{templatesnotice|s1=模板捷徑1|s2=模板捷徑2|s3=模板捷徑3}}</nowiki>

此功能使用{{tl|template shortcut}}模板。

==模板系列==
為了方便瀏覽同系列的用戶警告模板，本模板嵌入了{{tl|Warning set}}模板。模板提供了3個參數來設定{{tl|Warning set}}模板：「series」、「max」和「escalate」參數。代碼：
 &#123;{templatesnotice|series=模板系列名稱|max=系列內模板的總數目|escalate=警告升級}}
*「series」參數是指該模板系列的名稱，即用戶警告模板名稱的前綴。例子有「uw-vandalism」、「uw-test」、「uw-spam」、「uw-agf」等。
*「max」參數是指該系列內模板的總數目。以「uw-own」系列為例，它包含了{{tl|uw-own1}}、{{tl|uw-own2}}和 {{tl|uw-own3}}，所以「max」參數應填上3了。如果該系列含有所有層級的模板（包括層級4im），「max」參數便應填上5了。
*「escalate」參數是指模板系列的層級4模板是否升級至{{tl|uw-vandalism4}}。以「uw-test」系列為例，它包含了{{tl|uw-test1}}、{{tl|uw-test2}}及{{tl|uw-test3}}，而到層級4時則需轉用{{tl|uw-vandalism4}}（警告升級），因{{tl|uw-vandalism4}}模板不是屬於「uw-test」系列，所以「max」參數應填上3，並且需將「escalate」參數填上「yes」。  將「escalate」參數填上「no」、「false」 等的參數或將其留空則不會將層級4轉成{{tl|uw-vandalism4}}模板。

此功能使用{{tl|Warning set}}模板，並使用了複雜的分析程序代碼。

==捷徑及系列==
使用以下代碼便能將以上兩個功能結合使用：
 &#123;{templatesnotice|series = 模板系列名稱|max = 系列內模板的總數目|s1 = 模板捷徑1|s2 = 模板捷徑2|s3 = 模板捷徑3|escalate = 警告升級}}

==非[[WP:TW|Twinkle]]模板==
使用<code>|notwinkle=yes</code>去除{{tl|Twinkle standard installation}}

<includeonly>
[[Category:使用了分析程序的模板]]

[[bn:টেমপ্লেট:Templatesnotice]]
[[en:Template:Templatesnotice]]
[[gl:Modelo:Documentación dos avisos de usuario]]
[[or:ଛାଞ୍ଚ:Templatesnotice]]
[[simple:Template:Multi notice]]
[[sl:Predloga:Templatesnotice]]
[[vi:Bản mẫu:Templatesnotice]]
</includeonly>