Implements the mathematical [[ceil function]], i.e. returns the input value if it’s an integer, otherwise returns the lowest integer which is still greater than the input value.

For negative numbers, it will truncate the displayed decimals. For positive numbers, the decimals will be dropped and the integer part of the value displayed is incremented (unless the input is already an integer). This is the mathematical definition of the IEEE rounding mode ''toward plus infinite''.

; Usage<nowiki>:</nowiki>
: <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}|</tt>''value''<tt><nowiki>}}</nowiki></tt>

; Examples<nowiki>:</nowiki>
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>3.9<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|3.9}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>3.5<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|3.5}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>3.1<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|3.1}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>3.0<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|3.0}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>1.0<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|1.0}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>0.9<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|0.9}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>0.5<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|0.5}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>0.1<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|0.1}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>0.0<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|0.0}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>-0.1<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|-0.1}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>-0.5<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|-0.5}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>-0.9<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|-0.9}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>-1.0<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|-1.0}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>-3.0<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|-3.0}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>-3.2<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|-3.2}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>-3.5<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|-3.5}}.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki>-3.9<nowiki>}}</nowiki></tt> = {{{{BASEPAGENAME}}|-3.9}}.

; See also<nowiki>:</nowiki>
* [[Template:Floor]]

<includeonly>
[[Category:使用了分析程序的模板|{{PAGENAME}}]]
[[Category:函数模板|{{PAGENAME}}]]

[[eo:Ŝablono:Supren]]
[[nl:Sjabloon:Ceil]]
[[fi:Malline:Ceil]]
[[zh-classical:Template:Math.ceil]]
</includeonly>