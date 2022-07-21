{{Documentation subpage}}
<!-- Place categories where indicated at the bottom of this page and interwikis at Wikidata (see [[Wikipedia:Wikidata]]) -->

{{deletiontools|all=0|afd=1|merge=1|move=1|transwiki=1}}
{{tsh|mtc}}
{{Twinkle standard installation}}

== 用法 ==
{{Details|Wikipedia:文件转移至共享资源}}

<!-- Keep in sync description with other Template:Copy to Foo -->
本模板主要用於檔案描述頁面。如果本模板用於條目頁面，將會自動偵測出來，並替換為以下樣式：
{{Copy to Wikimedia Commons|demospace=main}}

本模板將會把這類頁面歸類於[[:Category:轉移到維基共享資源]]。 

請不要在本模板使用[[Wikipedia:Subst|替換參照]]（<code>subst:</code>），也不得在目標頁面的編輯摘要中加入「<nowiki>{{...}}</nowiki>」字元，這將會導致在移動編輯歷史至維基共享資源時造成格式問題。本模板須[[Wikipedia:Avoid self-references|避免自我提及]]。

==模板資訊==
{{TemplateData header}}
<TemplateData>
{
        "description": "本模板將會標示應該移動到維基共享資源的檔案。",
        "params": {
                "date": {
                        "label": "年月",
                        "description": "給出建議移動到維基共享資源的日期。",
                        "type": "string",
                        "required": false
                },
                "bot": {
                        "label": "機器人名稱",
                        "description": "大量標記此模板的機器人名稱。",
                        "type": "string/wiki-user-name",
                        "required": false
                },
                 "human": {
                        "label": "複核使用者",
                        "description": "複核該檔案的人類使用者名稱。",
                        "type": "string/wiki-user-name",
                        "required": false
                },
                 "inline": {
                        "label": "Add file to Category:Copy to Wikimedia Commons (inline-identified)",
                        "description": "Puts the file into Category:Copy to Wikimedia Commons (inline-identified) instead of Category:Copy to Wikimedia Commons",
                        "type": "string",
                        "required": false
                }
        }
}
</TemplateData>

==重定向==
{{col-begin|width=auto}}
{{col-break}}
* {{tlx|Commons ok}}
* {{tlx|Copy to commons}}
* {{tlx|Copy to Commons}}
* {{tlx|CtC}}
{{col-break}}
* {{tlx|Movetocommons}}
* {{tlx|MoveToCommons}}
* {{tlx|Move to commons}}
{{col-break}}
* {{tlx|Move to Commons}}
* {{tlx|MTC}}
* {{tlx|To Commons}}
{{col-end}}

==參見==
* {{Tlx|Now Commons}}：標示已移動到維基共享資源，且可以提報刪除的檔案。
* {{Tlx|Do not move to Commons}}：標示不應該移動到維基共享資源的檔案。
* {{Tlx|Deleted on Commons}}：標示曾經遭到維基共享資源刪除的檔案。
* {{Tlx|Incomplete move to Commons}}
* [[Wikipedia:文件轉移至共享資源]]：工作指引
* [[Wikipedia:模板消息/文件名字空间]]
* [[Wikipedia:图像与多媒体专题/共享资源]]

<includeonly>
[[Category:維基百科維護模板|C]]
[[Category:維基共享資源模板‎]]
</includeonly>