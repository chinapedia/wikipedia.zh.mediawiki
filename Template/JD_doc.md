<includeonly></includeonly><noinclude>{{template doc page viewed directly}}</noinclude>

This template converts date elements, or date and time elements, into a [[Julian date]] timestamp.
It interprets all dates starting at [[15 October]] [[1582]] in the [[Gregorian calendar]], otherwise it uses the [[Julian calendar]] that was valid until [[04 October]] [[1582]].

; Syntax<nowiki>:</nowiki>
: <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|</nowiki></tt>''year''<tt><nowiki>|</nowiki></tt>''[month]''<tt><nowiki>|</nowiki></tt>''[day]''<tt><nowiki>|</nowiki></tt>''[hour]''<tt><nowiki>|</nowiki></tt>''[minute]''<tt><nowiki>|</nowiki></tt>''[second]''<tt><nowiki>}}</nowiki></tt>
: <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>}}</nowiki></tt>
* If the ''year'' parameter is missing, all other parameters are ignored, and their default is the current UTC date and time, as set on the server.
* Otherwise, all parameters for the date and time must be specified as valid numeric expressions.
* The default ''day'' and ''month'' are 1.
* The computed ''year'' and ''month'' parameters are first converted into a rounded number of months since 01 December 1 AD and then converted to the actual ''year'' and ''month''. For this prior computing, the ''day'' parameter and time parameters are ignored.
* The default ''hour'' is 12 (for noon). Note that 24-hours format is used, so an ''hour'' parameter lower than 12 indicates the previous day in the old Julian day counting system, where days started at noon.
* The default ''minute'' or ''second'' is 0.
* Any date whose actual ''month'' and ''year'' are before October 1582, or are October 1582 but the computed ''day'' parameter is before the 15th at noon, will be interpreted as dates in the Julian calendar.

; Example<nowiki>:</nowiki>
* It is JD {{ {{BASEPAGENAME}}}} now.
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}|1582|10|05|11|59|59<nowiki>}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1582|10|05|11|59|59}} (this is the last valid instant of a Julian date before the Gregorian change, before noon, so actually it is still October 4 with the old date counting where days start at noon).
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}|1582|10|15|12|00|00<nowiki>}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1582|10|15|12|00|00}} (this is the first instant of a Gregorian date, on October 15 at noon, i.e. October 5 at noon in the previous Julian calendar).
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}|1582|10|15|11|59|59<nowiki>}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1582|10|15|11|59|59}} (this is still a date of the Julian calendar ''after'' the Gregorian change, and it is actually still the 14th of October before noon with the Julian calendar and the old Julian day counting system, or the 24th of October before noon with the proleptic Gregorian calendar and the old Julian day counting system where dates still changed at noon).
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}|1582|10|25|11|59|59<nowiki>}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1582|10|15|11|59|59}} (this is still the same instant in the Gregorian calendar).

''Note'': the results may seem wrong, but they are not. The interpretation is given by comparing the Julian and Gregorian dates, so read twice the description of the third example; the exact calendar shift occurred between examples 1 and 2, and the 4th example is unambiguously in the Gregorian calendar.''

; See also<nowiki>:</nowiki>
* [[Template:JULIANDAY]] (version taking a date in the Gregorian calendar only)
* [[Template:JULIANDAY.JULIAN]] (version taking a date in the Julian calendar only)

<includeonly>
[[Category:日期计算模板|{{PAGENAME}}]]
</includeonly>