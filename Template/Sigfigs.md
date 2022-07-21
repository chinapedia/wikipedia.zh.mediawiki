<includeonly>{{#ifexpr:{{{1|0}}} < 0.0001|5|{{#ifexpr:{{{1|}}} < 0.001|4|{{#ifexpr:{{{1|}}} < 0.01|3|{{#ifexpr:{{{1|}}} < 0.1|2|{{#ifexpr: {{{1|}}} < 1.0|1|{{#ifexpr: {{{1|}}} < 10.0|0|{{#ifexpr: {{{1|}}} < 100.0|-1|{{#ifexpr: {{{1|}}} < 1000.0|-2|-3}} }} }} }} }} }} }} }}</includeonly><noinclude>
This template is used to determine the number of figures after the decimal point of an uncertain quantity
to display.  Its syntax is:

<nowiki>{{Sigfigs|</nowiki> ''uncertainty-value''}}.

For example:
* <nowiki>{{Sigfigs|0.0002}}</nowiki> is 4,
* <nowiki>{{Sigfigs|0.005}}</nowiki> is 3,
* <nowiki>{{Sigfigs|50.0}}</nowiki> is -1,
and so on.
</noinclude>