{| width="100%" style="font-size: smaller; "
|
| align="center"| [[香港歷史]] | [[香港歷史年表]]
|-
| '''[[世紀]]：'''
| align="center" | [[{{#expr: ({{{1|{{CURRENTYEAR}}}}} - 1) / 100 - 0.5 round 0 }}世紀香港]] | '''[[{{#expr: (({{{1|{{CURRENTYEAR}}}}} - 1) / 100 - 0.5 round 0) + 1 }}世紀香港]]''' | [[{{#expr: (({{{1|{{CURRENTYEAR}}}}} - 1) / 100 - 0.5 round 0) + 2 }}世紀香港]]
|-
| '''[[年代]]：'''
| align="center" | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 - 30 }}年代香港]] | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 - 20 }}年代香港]] | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 - 10 }}年代香港]] | '''[[{{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 }}年代香港]]''' | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 + 10 }}年代香港]] | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 + 20 }}年代香港]] | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 + 30 }}年代香港]]
|-
| '''[[年|年份]]：'''
| align="center" | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} - 4 }}年香港]] | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} - 3 }}年香港]] | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} - 2 }}年香港]] | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} - 1 }}年香港]] | '''[[{{{1|{{CURRENTYEAR}}}}}年香港]]''' | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} + 1 }}年香港]] | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} + 2 }}年香港]] | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} + 3 }}年香港]] | [[{{#expr: {{{1|{{CURRENTYEAR}}}}} + 4 }}年香港]]
|-
| '''[[紀年]]：'''
| align="center" | '''[[{{YearInSexagenaryCycle|{{{1|{{CURRENTYEAR}}}}}|2}}]]年'''（'''[[生肖|{{YearInSexagenaryCycle|{{{1|{{CURRENTYEAR}}}}}|1}}年]]'''）{{#ifexpr: {{{1|{{CURRENTYEAR}}}}} >= 1841 |、'''[[香港開埠初期歷史|香港開埠]]{{#expr: {{{1|{{CURRENTYEAR}}}}} - 1841}}周年'''}}{{#ifexpr: {{{1|{{CURRENTYEAR}}}}} >= 1945 and {{{1|{{CURRENTYEAR}}}}} <= 1997 |、'''[[香港重光]]{{#expr: {{{1|{{CURRENTYEAR}}}}} - 1945}}周年'''{{{2|}}}}}{{#ifexpr: {{{1|{{CURRENTYEAR}}}}} >= 1997 |、'''[[香港回歸]]{{#expr: {{{1|{{CURRENTYEAR}}}}} - 1997}}周年'''{{{2|}}}}}
|}<noinclude>

== 功能 ==

從「年份數」（預設為「 <nowiki>{{CURRENTYEAR}}</nowiki>」）返回對應的年份索引

== 用法 ==

<nowiki>{{HKYearTOC|年份数|其他纪年}} </nowiki>

{{esoteric}}

[[Category:日历模板|{{PAGENAME}}]]
[[Category:香港模板]]

</noinclude>