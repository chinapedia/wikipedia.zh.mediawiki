<includeonly>{{#if:{{{2|}}}|{{#ifexpr: {{{2}}} > {{{1}}} * {{{3}}}|大约{{#expr: {{{1}}} round {{Sigfigs|{{{2}}}}}}}|{{#expr: {{{1}}} round {{Sigfigs|{{{2}}}}} }} &plusmn; {{#expr: {{{2}}} round {{Sigfigs|{{{2}}}}} }} }} |{{{1}}} }}</includeonly><noinclude>

This template is used to display a correctly rounded uncertain quantity and its uncertainty, except that if
the uncertainty exceeds a threshold times the quantity, the uncertainty is not displayed and it is merely
indicated that the quantity is uncertain.

Its syntax is

<nowiki>{{ErrorBar2|</nowiki>''uncertain-quantity''|''uncertainty''|''threshold''}}.

For example:
* <nowiki>{{ErrorBar2|1573.614|687.9|0.1}}</nowiki> yields ''{{ErrorBar2|1573.614|687.9|0.1}}''.
* <nowiki>{{ErrorBar2|1573.614|187.9|0.1}}</nowiki> yields ''{{ErrorBar2|1573.614|187.9|0.1}}''.
* <nowiki>{{ErrorBar2|1573.614|123.4|0.1}}</nowiki> yields ''{{ErrorBar2|1573.614|123.4|0.1}}''.
* <nowiki>{{ErrorBar2|1573.614|47.9|0.1}}</nowiki> yields ''{{ErrorBar2|1573.614|47.9|0.1}}''.
* <nowiki>{{ErrorBar2|1573.614|0.873|0.1}}</nowiki> yields ''{{ErrorBar2|1573.614|0.873|0.1}}''.
* <nowiki>{{ErrorBar2|1573.614|0.007|0.1}}</nowiki> yields ''{{ErrorBar2|1573.614|0.007|0.1}}''.
[[Category:天文学模板]]
</noinclude>