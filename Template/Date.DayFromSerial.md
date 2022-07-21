{{#ifexpr:{{{1|1}}}<1
	|{{#expr: 31+{{{1|1}}} }}
	|{{#ifexpr:{{{1|1}}} > ( 365+{{Date.IsLeapYear|{{{2|{{CURRENTYEAR}}}}}}} )
		|{{#expr: {{{1|1}}}-365-{{Date.IsLeapYear|{{{2|{{CURRENTYEAR}}}}}}} }}
		|{{#expr: {{{1|1}}}-{{Date.DaysBeforeMonth|{{Date.MonthFromSerial|{{{1|1}}}|{{{2|{{CURRENTYEAR}}}}}}}|{{{2|{{CURRENTYEAR}}}}}}} }}
	}}
}}<noinclude>{{pp-template}}
{{esoteric}}
[[Category:日期计算模板]]
</noinclude>