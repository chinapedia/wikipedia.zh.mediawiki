<noinclude>{{pp-template}}</noinclude>{{not year|{{{1|0}}}}}
{| width="100%" style="font-size:small; background: none;"
| style="white-space:nowrap;" |'''[[千纪]]：'''
| align="center" | '''[[{{CalcBcDate| {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} > 0 | {{#expr: (({{{1|{{CURRENTYEAR}}}}} - 0.9) / 1000 - 0.5 round 0) + 1 }} | {{#expr: (({{{1|{{CURRENTYEAR}}}}} + 0.9) / 1000 + 0.5 round 0) - 1 }} }} | 0 | m }}千纪]]'''
|-
| style="white-space:nowrap;" |'''[[世纪]]：'''
| align="center" | [[{{CalcBcDate| {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} > 0 | {{#expr: (({{{1|{{CURRENTYEAR}}}}} - 0.9) / 100 - 0.5 round 0) + 1 }} | {{#expr: (({{{1|{{CURRENTYEAR}}}}} + 0.9) / 100 + 0.5 round 0) - 1 }} }} | -1 }}世纪]] | '''[[{{CalcBcDate| {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} > 0 | {{#expr: (({{{1|{{CURRENTYEAR}}}}} - 0.9) / 100 - 0.5 round 0) + 1 }} | {{#expr: (({{{1|{{CURRENTYEAR}}}}} + 0.9) / 100 + 0.5 round 0) - 1 }} }} | 0 }}世纪]]''' | [[{{CalcBcDate| {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} > 0 | {{#expr: (({{{1|{{CURRENTYEAR}}}}} - 0.9) / 100 - 0.5 round 0) + 1 }} | {{#expr: (({{{1|{{CURRENTYEAR}}}}} + 0.9) / 100 + 0.5 round 0) - 1 }} }} | 1 }}世纪]]
|-
| style="white-space:nowrap;" |'''[[年代]]：'''
| align="center" | [[{{CalcBcDate| {{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 }} | {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} < 0 and {{{1|{{CURRENTYEAR}}}}} > -10 | -40 | -30 }} | d }}年代]] | [[{{CalcBcDate| {{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 }} | {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} < 0 and {{{1|{{CURRENTYEAR}}}}} > -10 | -30 | -20 }} | d }}年代]] | [[{{CalcBcDate| {{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 }} | {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} < 0 and {{{1|{{CURRENTYEAR}}}}} > -10 | -20 | -10 }} | d }}年代]] | '''[[{{CalcBcDate| {{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 }} | {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} < 0 and {{{1|{{CURRENTYEAR}}}}} > -10 | -10 | 0 }} | d }}年代]]''' | [[{{CalcBcDate| {{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 }} | {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} < 0 and {{{1|{{CURRENTYEAR}}}}} > -10 | 0 | 10 }} | d }}年代]] | [[{{CalcBcDate| {{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 }} | {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} < 0 and {{{1|{{CURRENTYEAR}}}}} > -10 | 10 | 20 }} | d }}年代]] | [[{{CalcBcDate| {{#expr: {{{1|{{CURRENTYEAR}}}}} - {{{1|{{CURRENTYEAR}}}}} mod 10 }} | {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} < 0 and {{{1|{{CURRENTYEAR}}}}} > -10 | 20 | 30 }} | d }}年代]]
|- 
| style="white-space:nowrap;" |'''[[年|年份]]：'''
| align="center" | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | -5 }}年]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | -4 }}年]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | -3 }}年]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | -2 }}年]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | -1 }}年]] | '''{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年''' | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | +1 }}年]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | +2 }}年]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | +3 }}年]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | +4 }}年]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | +5 }}年]]
|- 
| style="white-space:nowrap;" |'''[[纪年]]：'''
| align="center" | {{#ifexpr: {{{1|{{CURRENTYEAR}}}}} > 84 | '''[[{{YearInSexagenaryCycle|{{{1|{{CURRENTYEAR}}}}}|2}}]]年'''（'''[[生肖|{{YearInSexagenaryCycle|{{{1|{{CURRENTYEAR}}}}}|1}}年]]'''）{{#if: {{{2|}}} |；|}}|}}{{{2|}}}
|- 
| style="white-space:nowrap;" |'''[[月|月份]]：'''
| align="center" | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年1月|1月]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年2月|2月]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年3月|3月]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年4月|4月]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年5月|5月]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年6月|6月]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年7月|7月]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年8月|8月]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年9月|9月]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年10月|10月]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年11月|11月]] | [[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年12月|12月]]
|}
{{#ifexpr:{{{1|{{CURRENTYEAR}}}}}>1582
|{{HideH|[[{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}年]]日曆表{{#ifexpr:{{{1|{{CURRENTYEAR}}}}}<1919|（[[格里曆]]）|}}}}
{{格里曆年曆|{{CalcBcDate| {{{1|{{CURRENTYEAR}}}}} | 0 }}}}
{{HideF}}
|}}
<noinclude>{{Documentation}}</noinclude>