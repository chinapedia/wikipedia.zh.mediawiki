<noinclude>{|class="wikitable"
|-
||Pos||Num
{{#if:{{{nat|}}} {{!}}{{!}}Nat }}
||Name||Height||Weight||DOB||School
</noinclude>|-
| style="text-align:center;" | {{Bs position|{{{pos|}}}}}
| style="text-align:center;" | {{ifnumber|{{{num|}}}|{{Number table sorting|{{{num|}}}}}|{{{num|}}}}}
{{#if:{{{nat|}}} | {{!}} style="text-align:center;" {{!}} {{sort|1={{{nat|}}}|2={{flagicon|{{{nat|}}}|size=20px|{{{natvar|}}}}} }} }}
| style="text-align:left;" | {{#if:{{{first|}}}{{{last|}}}{{{name|}}}|{{#if:{{{autolink|}}}|{{Autolink|{{{link|{{{name|{{{first}}} {{{last<includeonly>|</includeonly>}}}}}} {{#if:{{{dab|}}}|({{{dab}}})}}}}}|{{{alt|{{{name|{{#if:{{{last<includeonly>|</includeonly>}}}|{{{last}}},}} {{{first}}}}}}}}}}}|[[{{{link|{{{name|{{{first}}}·{{{last<includeonly>|</includeonly>}}}}}} {{#if:{{{dab|}}}|({{{dab}}})}}}}}|{{{alt|{{{name|{{#if:{{{last<includeonly>|</includeonly>}}}|{{{first}}}·}}{{{last}}}}}}}}}]]}}}}{{#if:{{{englink|}}}{{{redlink|}}}|{{le|{{{redlink}}}|{{{englink}}}|{{#if:{{{showname|}}}|{{{showname}}}}}}}}}{{#ifeq:{{{inj|no}}}|yes|&nbsp;[[Image:Cruz Roja.svg|8px|Injured|link=]]}}{{#if:{{{note|}}}|'''（{{{note}}}）'''}}

| style="text-align:right; white-space:nowrap; | {{#if:{{{ft|}}}
     |{{convert|{{{ft|0|}}}|ft|{{#if:{{{in|}}}|{{{in}}}|0}}|in|2|abbr=on|sortable=on}}
     }}
| style="text-align:right; white-space:nowrap; | {{#if:{{{lbs|{{{lbs|}}}}}}
     |{{convert|{{{lbs|{{{lbs|}}}}}}|lb|kg|0|abbr=on}}
     }}
| style="text-align:center;" | {{{DOB|}}}
| style="text-align:left; | {{#if:{{{college<includeonly>|</includeonly>}}} {{{school|}}}
| {{college|{{{college|{{{school|<noinclude>Hard Knocks</noinclude>}}}}}}}}
| {{#if:{{{from|}}}|{{{from}}}}}
}}
|-<noinclude>
|}
{{Documentation|Template:NBA roster doc}}
[[Category:籃球員名單模板]]
</noinclude>