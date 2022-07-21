{| class="infobox" style="width: 250px; border-spacing: 2px;"
|- 
! colspan=2 style="background: mediumaquamarine; text-align: center;" | {{{name|{{PAGENAME}}}}}
|-
{{#if:{{{image|}}}|
! colspan=2 style="padding: 20px 0" {{!}} [[Image:{{{image|}}}|center|200px|]]
}}
|-
{{#if:{{{shots_m|}}}{{{olympics_m|}}}{{{worlds_m|}}}{{{abbr_m|}}}
|
! colspan="2" style="background: mediumaquamarine;" {{!}} 男子项目
}}
|-
{{#if:{{{shots_m|}}}|
! style="text-align: left;" {{!}} 射击发数:
{{!}} {{{shots_m|}}}
}}
|-
{{#if:{{{olympics_m|}}}|
! style="text-align: left;" {{!}} 奥运会项目:
{{!}} {{{olympics_m|}}}
}}
|-
{{#if:{{{worlds_m|}}}|
! style="text-align: left;" {{!}} 世界锦标赛:
{{!}} {{{worlds_m|}}}
}}
|-
{{#if:{{{abbr_m|}}}|
! style="text-align: left;" {{!}} 缩写:
{{!}} {{{abbr_m|}}}
}}
|-
{{#if:{{{shots_f|}}}{{{olympics_f|}}}{{{worlds_f|}}}{{{abbr_f|}}}
|
! colspan="2" style="background: mediumaquamarine;" {{!}} 女子项目
}}
|-
{{#if:{{{shots_f|}}}|
! style="text-align: left;" {{!}} 射击发数:
{{!}} {{{shots_f|}}}
}}
|-
{{#if:{{{olympics_f|}}}|
! style="text-align: left;" {{!}} 奥运会项目:
{{!}} {{{olympics_f|}}}
}}
|-
{{#if:{{{worlds_f|}}}|
! style="text-align: left;" {{!}} 世界锦标赛:
{{!}} {{{worlds_f|}}}
}}
|-
{{#if:{{{abbr_f|}}}|
! style="text-align: left;" {{!}} 缩写:
{{!}} {{{abbr_f|}}}
}}
|}<noinclude>

<div style="clear: both"></div>
==Usage==
Copy this code:
<pre>{{ Infobox Shooting sport
|name=
|image=
|shots_m=
|shots_f=
|olympics_m=
|olympics_f=
|worlds_m=
|worlds_f=
|abbr_m=
|abbr_f=
}}</pre>
If anyone of the three "_fem" variables are set, then the infobox will create a two headings separating male and female, else there will be no heading rows.

;name : Remove if page name is same as infobox title
;image : image file name
;shots_m : displayd as '''Number of Shots'''
;shots_f : displayd as '''Number of Shots'''
;olympics_m : displayed as '''Olympics''', it indicates the years during which the sport was offered on the Olympic program
;olympics_f : displayed as '''Olympics''', it indicates the years during which the sport was offered on the Olympic program
;worlds_m : displayed as '''World Championship''', it indicates the years during which the sport was offered at 
the World Championships (ISSF)
;worlds_f : displayed as '''World Championship''', it indicates the years during which the sport was offered at 
the World Championships (ISSF)
;abbr_m: Commonly used abbreviation 
;abbr_f: Commonly used abbreviation 

[[Category:体育信息框模板|项]]

</noinclude>