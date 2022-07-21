<includeonly><!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{Documentation subpage}}</noinclude>
<!-- 在本行下編輯模板說明 -->

{{缺乏中文说明}}
{{template shortcut|sm|aut|scap}}
==Usage==
{{COinS safe|n}}

<CODE><NOWIKI>{{Smallcaps|Your Text}}</NOWIKI></CODE> will display the lowercase part of {{Smallcaps|Your Text}} as typographical {{Smallcaps|[[small caps]]}}. Your source text is not altered (a copy-paste will give it in its original form), only the way it is displayed. You can most especially use this template for names/surnames disambiguation and all-caps words or pronounceable [[acronym]]s.

[[Diacritic]]s (å, ç, é, ğ, ı, ñ, ø, ş, ü, etc.) are handled. However, because the job is performed by each reader's browser, inconsistencies in [[CSS]] implementations can lead to some browsers not converting certain rare diacritics.

Use of this template does not generate any automatic categorization. As with most templates, if the argument contains an <TT>=</TT> sign, the argument should be prefixed with <TT>1=</TT>. And for wikilinks, you need to use piping. There is a parsing problem with MediaWiki which causes unexpected behavior when a template with one style is used within a template with another style. 

Technically, the templates wraps the standard {{Nowrap|<CODE><NOWIKI><SPAN STYLE="font-variant:small-caps;">Your Text</SPAN></NOWIKI></CODE>}}.

==Code examples==

{| CLASS="wikitable"
|-
! !! Code !! Gives
|-
|Y|| <nowiki>{{Smallcaps|The ''Name'' of the 2<SUP>nd</SUP> Game}}</nowiki> || {{Smallcaps|The ''Name'' of the 2<SUP>nd</SUP> Game}}
|-
|Y|| <nowiki>Leonardo {{Smallcaps|DiCaprio}} (born 1974)</nowiki> || Leonardo {{Smallcaps|DiCaprio}} (born 1974)
|-
|Y|| <nowiki>{{Smallcaps|Nesbø, Vågen, Louÿs, Zúñiga, Kabaağaçlı}}</nowiki> || {{Smallcaps|Nesbø, Vågen, Louÿs, Zúñiga, Kabaağaçlı}}
|-
|COLSPAN=3 ALIGN=CENTER| ''When your text uses an = sign:''
|-
|N|| <nowiki>{{Smallcaps|2+2=4}}</nowiki> || {{Smallcaps|2+2=4}}
|-
|Y|| <nowiki>{{Smallcaps|1=2+2=4}}</nowiki> || {{Smallcaps|1=2+2=4}}
|-
|COLSPAN=3 ALIGN=CENTER| ''When your text uses a template:''
|-
|N|| <nowiki>{{Smallcaps|Being {{Green|Green}} is Easy}}</nowiki> || {{Smallcaps|Being {{Green|Green}} is Easy}}
|-
|N|| <nowiki>{{Smallcaps|Being {{Green{{!}}Green}} is Easy}}</nowiki> || {{Smallcaps|Being {{Green{{!}}Green}} is Easy}}
|-
|Y|| <nowiki>{{Smallcaps|1=Being {{Green|Green}} is Easy}}</nowiki> || {{Smallcaps|1=Being {{Green|Green}} is Easy}}
|-
|Y|| <nowiki>{{Green|1=Being {{Smallcaps|Green}} is Easy}}</nowiki> || {{Green|1=Being {{Smallcaps|Green}} is Easy}}
|-
|Y|| <nowiki>{{Colors|green|yellow|3=Being {{Smallcaps|Green}} is Easy}}</nowiki> || {{Colors|green|yellow|3=Being {{Smallcaps|Green}} is Easy}}
|-
|COLSPAN=3 ALIGN=CENTER| ''When your text uses a {{!}} pipe:''
|-
|N|| <nowiki>{{Smallcaps|Before|afteR}}</nowiki> || {{Smallcaps|Before|afteR}}
|-
|N|| <nowiki>{{Smallcaps|1=Before{{!}}afteR}}</nowiki> || {{Smallcaps|1=Before{{!}}afteR}}
|-
|Y|| <nowiki>{{Smallcaps|1=Before&amp;#124;afteR}}</nowiki> || {{Smallcaps|1=Before&#124;afteR}}
|-
|COLSPAN=3 ALIGN=CENTER| ''When your text uses a link:''
|-
|N|| <nowiki>[[{{Smallcaps|Mao}} Zedong]]</nowiki> || [[{{Smallcaps|Mao}} Zedong]]
|-
|Y|| <nowiki>[[Mao Zedong|{{Smallcaps|Mao}} Zedong]]</nowiki> || [[Mao Zedong|{{Smallcaps|Mao}} Zedong]]
|}

==Reasons to use==

This template is useful for typographical uses including:

* To lighten ALL-CAPS words or pronounceable [[acronym]]s, such as:
** The biblical "[[The LORD|{{Smallcaps|Lord}}]]" (instead of LORD or Lord) or "Lord {{Smallcaps|God}}" as written in some Bibles
** The acronyms [[UNESCO|{{Smallcaps|Unesco}}]] (instead of UNESCO or Unesco) or [[UNICEF|{{Smallcaps|Unicef}}]]
** The trademark [[時代 (雜誌)|{{Smallcaps|Time}}]] (instead of TIME or Time)
* To lighten ALL-CAPS surnames mandated by some referencing styles:
** Piccadilly has been compared to a Parisian boulevard ({{Smallcaps|Dickens}} 1879).
** [[Charles Dickens, Jr|{{Smallcaps|Dickens}}, C., Jr]] (1879). "Piccadilly" in ''Dickens's Dictionary of London''.
* To disambiguate Western names and surnames at a glance:
** Many Spanish names are tricky to decompose:
*** [[Jorge Luis Borges|Jorge Luis {{Smallcaps|Borges}}]], but [[Adolfo Bioy Casares|Adolfo {{Smallcaps|Bioy Casares}}]] (both filed under "B")
* To disambiguate Eastern surnames and names at a glance:
** Most Chinese names retain their surname-first order:
*** [[Mao Zedong|{{Smallcaps|Mao}} Zedong]] vs. [[Chiang Kai-shek|{{Smallcaps|Chiang}} Kai-shek]]
** Most Japanese names are reversed in the West:
*** [[Akira Kurosawa|Akira {{Smallcaps|Kurosawa}}]] or [[Motojirō Kajii|Motojirō {{Smallcaps|Kajii}}]] (usually reversed)
*** But [[江戸川乱步|{{Smallcaps|Edogawa}} Ranpo]] (kept due to wordplay "EdgarA–llanPoe) vs. [[江戸川乱步|Ranpo {{Smallcaps|Edogawa}}]] (some modern uses)

==See also==

Templates that change the display (copy-paste will get the original text):

* {{tl|Nocaps}}    – lower case display
* {{tl|Smallcaps}} – small caps display
* {{tl|Allcaps}}   – upper case display

[[Help:魔术字#格式|Magic words]] that rewrite the output (copy-paste will get the text as displayed):

* <NOWIKI>{{</NOWIKI>lc:}}      – lower case output of the full text
* <NOWIKI>{{</NOWIKI>uc:}}      – upper case output of the full text
* <NOWIKI>{{</NOWIKI>lcfirst:}} – lower case output of the first character only
* <NOWIKI>{{</NOWIKI>ucfirst:}} – upper case output of the first character only

<includeonly>
<!-- PLEASE ADD CATEGORIES BELOW THIS LINE, THANKS. -->
[[Category:格式模板|{{PAGENAME}}]]
</includeonly>