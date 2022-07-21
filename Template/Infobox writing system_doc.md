{{NoteTA
|G1 = IT
|G2 = MediaWiki
}}
{{Documentation subpage}}
{{esoteric}}
== 语法 ==
Syntax including all possible variables (required parameters marked with asterisk):
<div style="font-size:95%;">
 <nowiki>{{Infobox writing system</nowiki>
 |name        = (*)
 |type        = (*see [[#標題顏色|options below]])
 |typedesc    = (For providing additional info after a general type<!--example?-->)
 |time        = (*Time period during which system was in use)
 |languages   = (Major languages using the writing system)
 |fam1        = (Use famN to specify parent writing system/s.
 |fam2        =  Up to 15 parent writing systems can be listed,
 ...             fam1 being the oldest.)
 |fam15       = 
 |creator     = (Use instead of famN for artificially created writing systems)
 |sisters     = (For sister writing systems here with common origin)
 |children    = (For child writing systems)
 |sample      = (Sample image, WITHOUT "File:" prefix)
 |imagesize   = (Sample image's size)
 |unicode     = (To specify a Unicode range)
 |iso15924    = (To specify an [[ISO 15924]] four-letter code)
 |IPAChartEng = (To provide link to [[Help:IPA]])
 |note        = none (cancels the IPA warning)
 <nowiki>}}</nowiki>
</div>

While it is probably important to always list at least the immediate 'parent' of any writing system it isn't always practical to list all of the 'children' if this number is too large.

== 標題顏色 ==
依照書寫系統（{{Para|type}}）的不同會改變顯示的顏色：
{| style="background:transparent; text-align:center; font-size:120%;" cellspacing="4" cellpadding="3"
|-
| style="background:palegreen;" | [[輔音音素文字]]
| style="background:lightblue;" | [[字母系統]]
| style="background:navajowhite;" | [[元音附標文字]]
| style="background:pink;" | [[音節文字]]
|-
| style="background:violet;" | [[半音節文字]]
| style="background:paleturquoise;"| [[手語文字]]
| style="background:palegoldenrod;"| [[象形文字]]
| style="background:gold;" | [[形意文字]]
|-
| style="background:mistyrose;" | [[語素文字]]
| style="background:turquoise;" | [[速記]]
| style="background:gainsboro;" | [[未解讀文字]]
| style="background:khaki;" | （預設）
|}
<includeonly>{{Sandbox other||
<!-- 本行下加入模板的分類 -->
[[Category:语言信息框模板|W]]
[[Category:文字模板]]
}}</includeonly>