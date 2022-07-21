{{#if: {{{source|}}}|[[s:{{{source}}}{{#if: {{{version|}}}|&#32;({{{version}}})|}}{{#if: {{{book|}}}|&#47;{{{book}}}|}}&#35;{{#if: {{{chapter|}}}|{{{chapter}}}{{#if:{{{verse|}}}|&#58;|}}|}}{{#if: {{{verse|}}}|{{{verse}}}|}}{{!}}{{#if:{{{showsource|}}}|{{{source}}},&#32;|}}{{{nobook|{{{book|{{{source}}}}}}}}}{{#if: {{{chapter|}}}|&#32;{{{chapter}}}|}}{{#if: {{{verse|}}}|&#58;{{{verse}}}|}}{{#if: {{{range|}}}|{{{range}}}|}}]]|Error on call to [[Template:Sourcetext]]. Parameter '''source''' must be defined.}}<noinclude>

== Description ==

Template for linking to standardised [[Wikisource]] texts.

==Usage==

*'''source''', the source text ('''must''' be defined, or the template will generate an error)
*'''version''', version of the source text (optional, use if there is more than one version of a text, for example, Bible translations, etc)
*'''book''', the book of the source text (optional, use if chapters or books are defined as subpages)
*'''chapter''', the chapter of the book of the source text (chapter/anchor of the book)
*'''verse''', the verse of the chapter of the book of the source text (verse of the book)
*'''range''', specific verse range (optional range, will not link to these verses, will only display)
*'''nobook''', if defined, will not display a book name
*'''showsource''', if defined, will display the title of the sourcetext

==Examples==

Code: ''<nowiki>{{sourcetext|source=Bible|version=King James|book=1 Samuel|chapter=1|verse=10|range=, 18}}, {{sourcetext|source=Bible|version=King James|book=1 Samuel|chapter=3|verse=11|range=-21|nobook=}}</nowiki>''

Renders as: {{sourcetext|source=Bible|version=King James|book=1 Samuel|chapter=1|verse=10|range=, 18}}, {{sourcetext|source=Bible|version=King James|book=1 Samuel|chapter=3|verse=11|range=-21|nobook=}}.

Code: ''<nowiki>{{sourcetext|source=Bible|version=King James|book=Esther|chapter=4|verse=6|range=-10}}</nowiki>''

Renders as: {{sourcetext|source=Bible|version=King James|book=Esther|chapter=4|verse=6|range=-10}}.

Code: ''<nowiki>{{sourcetext|source=The Canterbury Tales: The Wife of Bath's Prologue and Tale|chapter=19}}</nowiki>''

Renders as: {{sourcetext|source=The Canterbury Tales: The Wife of Bath's Prologue and Tale|chapter=19}}

Code: ''<nowiki>{{sourcetext|source=The Man From Snowy River}}</nowiki>''

Renders as: {{sourcetext|source=The Man From Snowy River}}

Code: ''<nowiki>{{sourcetext|source=The Doctrine and Covenants|book=D&C 91|verse=1|range=-12|showsource=y}}</nowiki>''

Renders as: {{sourcetext|source=The Doctrine and Covenants|book=D&C 91|verse=1|range=-12|showsource=y}}

{{esoteric}}

[[Category:姊妹计划链接模板|{{PAGENAME}}]]

</noinclude>