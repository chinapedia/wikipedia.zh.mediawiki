<includeonly></includeonly><noinclude>{{Template doc page viewed directly}}</noinclude>

This template computes the number of the [[Julian day]] starting at noon on the date given in parameter (in the [[Julian calendar]], including after the dates of transition to the [[Gregorian calendar]]).

It ignores the inaccuracies of the Julian calendar which occurred only one year after its creation in [[-44|45 BC]] by ''Julius Caesar'', with different and incorrect rules observed in various locations of the Roman Empire between [[-43|44 BC]] and [[31|31 AD]]. The Julian calendar became then a standard (used during 17 to 19 centuries) only starting in [[32 AD]] after the Roman emperor ''Augustus'' had progressively applied the needed corrections.

So this template consider all years before [[32 AD]] as proleptic Julian years. The result is valid for all proleptic Julian calendar dates starting on March 1, 4801 BC at noon.

; Syntax<nowiki>:</nowiki>
: <tt><nowiki>{{</nowiki>{{PAGENAME}}|</tt>''year''<tt>|</tt>''[month]''<tt>|</tt>''[day]''<tt>|</tt>''[hour]''<tt>|</tt>''[minute]''<tt>|</tt>''[second]''<tt>}}</tt>
* The ''year'' (required) must be astronomical (''year''=1 in [[1|1 AD]] (''[[Anno Domini]]''), ''year''=0 in 1 BC, ''year''=-1 in 2 BC).
* The ''month'' (optional, default value 1) is expressed between 1 et 12 from january to december (but offsets are possible for computing other years).
* The ''year'' and ''month'' are first converted into a number of months, then rounded to the nearest integer to compute the actual year and month used for computing dates.
* The ''day'' (optional, default value 1) is normally between 1 et 31 (but offsets are possible for computing other months). Decimals are possible for fractions of day.
* The ''hour'' (optional, default value 12) is normally between 0 and 23 (but offsets are possible for computing other days). Note that Julian days begin at noon (hour = 12) and thus hours 0-11 of a solar day are one Julian day earlier than hours 12-23. The value may extend outside of the normal range and is considered as additional number of julian days (a Julian day is 24 hours or 86400 seconds exactly, ignoring any adjustment of leap seconds within the UTC calendar). Decimals are possible for fractions of hour.
* The ''minute'' and ''second'' (optional, default value 0) are normally between 0 and 59 (but offsets are possible for computing other hours). Decimals are possible for fractions of minute or second.
* All parameters can be any valid numeric expression which is evaluated before computing.

; Note<nowiki>:</nowiki>
: The julian day, when computed modulo 7, grows from 0 (on monday at noon) to 6 (on sunday at noon)) and falls back to 0 (on next monday). This corresponds to the order of days in the ISO week.

; Examples<nowiki>:</nowiki>
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|-4800|3|1|11|59|59}}</nowiki></tt> returns {{{{BASEPAGENAME}}|-4800|2|29|11|59|59}} (''proleptic'') (in ''year 4801 BC''), '''last''' Julian date where the result is '''wrong''', and too large of 365 days
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|-4800|3|1|12|0|0}}</nowiki></tt> returns {{{{BASEPAGENAME}}|-4800|3|1|12|0|0}} (''proleptic'') (in ''year 4801 BC''), first Julian date where the result is correct
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|-4800|3|2}}</nowiki></tt> returns {{{{BASEPAGENAME}}|-4800|3|2}} (''proleptic'') (in ''year 4801 BC''), 1 day increment test
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|-4712|1|1}}</nowiki></tt> returns {{{{BASEPAGENAME}}|-4712|1|1}} (''proleptic'') (in ''year 4713 BC'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|0|1|1}}</nowiki></tt> returns {{{{BASEPAGENAME}}|0|1|1}} (in ''year 1 BC'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|0|12|25}}</nowiki></tt> returns {{{{BASEPAGENAME}}|0|12|25}}
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|0|12|31}}</nowiki></tt> returns {{{{BASEPAGENAME}}|0|12|31}}
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|1|1|1}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1|1|1}} (Julian ''[[Anno Domini]]'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|1|1|3}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1|1|3}} (Gregorian ''[[Anno Domini]]'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|200|2|29}}</nowiki></tt> returns {{{{BASEPAGENAME}}|200|2|29}} (last day in the leap Julian year 200 AD, not leap in the proleptic Gregorian calendar)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|200|3|1}}</nowiki></tt> returns {{{{BASEPAGENAME}}|200|3|1}} (first day where the Julian and proleptic Gregorian calendars are '''equivalent''')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|300|2|28}}</nowiki></tt> returns {{{{BASEPAGENAME}}|300|2|28}} (last day where the Julian and proleptic Gregorian calendars are '''equivalent''')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|300|2|29}}</nowiki></tt> returns {{{{BASEPAGENAME}}|300|2|29}} (first day of difference between the Julian and proleptic Gregorian calendars, in leap Julian year 300 AD, not leap in the proleptic Gregorian calendar)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|325|3|21}}</nowiki></tt> returns {{{{BASEPAGENAME}}|325|3|21}} (spring equinox observed at the christian [[First Council of Nicaea]], taken as a reference for aligning the Julian calendar to the proleptic Gregorian calendar)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|1782|10|4}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1782|10|4}} (last day of the Julian calendar before the transition to the Gregorian calendar)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|1782|10|5}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1782|10|5}} (''proleptic'') (actually the 15th of october in the new Gregorian calendar)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|1858|11|4|12}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1858|11|4|12}} (''proleptic'') (start of epoch for the [[Julian day#Alternatives|Reduced Julian Day]], RJD)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|1858|11|5|0}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1858|11|5|0}} (''proleptic'') (start of epoch for the [[Julian day#Alternatives|Modified Julian Day]], MJD)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|1968|5|11|0}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1968|5|11|0}} (''proleptic'') (start of epoch for the [[NASA]]'s [[Julian day#Alternatives|Truncated Julian Day]], TJD)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|1995|9|27|0}}</nowiki></tt> returns {{{{BASEPAGENAME}}|1995|9|27|0}} (''proleptic'') (start of epoch for the current [[NIST]]'s [[Julian day#Alternatives|Truncated Julian Day]], TJD mod 10000)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2000|1|1}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2000|1|1}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2000|1|2}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2000|1|2}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2000|2|1}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2000|2|1}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2000|2|29}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2000|2|29}} (''proleptic'') (this leap day in the Julian calendar actually occurs on the 13th of March in the Gregorian calendar, whose leap day also occurred that year, but 13 days before)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2000|3|1}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2000|3|1}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2000|12|31}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2000|12|31}} (''proleptic'') (last day of the [[2nd millennium]] and of the [[20th century]] in the Julian calendar, remember that this is not the new Year's evening in the Gregorian calendar, but already the 13th of January)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2001|1|1}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2001|1|1}} (''proleptic'') (first day of the [[3rd millennium]] and of the [[21st century]] in the Julian calendar, the 14th of January in the Gregorian calendar)
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2001|12|31}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2001|12|31}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2002|12|31}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2002|12|31}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2003|12|31}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2003|12|31}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|2|1}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|2|1}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|3|1}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|3|1}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|3|31}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|3|31}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|4|30|0|0|0}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|4|30|0|0|0}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|4|30|01|35|48}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|4|30|01|35|48}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|4|30|11|59|60}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|4|30|11|59|60}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|4|30|12.0}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|4|30|12.0}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|4|30}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|4|30}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|4|30|23|59|59}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|4|30|23|59|59}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|5|1|00|00|00}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|5|1|00|00|00}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|5|1|12|00|00}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|5|1|12|00|00}} (''proleptic'')
* <tt><nowiki>{{</nowiki>{{BASEPAGENAME}}<nowiki>|2006|5|1}}</nowiki></tt> returns {{{{BASEPAGENAME}}|2006|5|1}} (''proleptic'')

; See also<nowiki>:</nowiki>
* [[Template:JULIANDAY]] (version taking a date in the Gregorian calendar)
* [[Template:JD]] (automatic Julian or Gregorian calendar determination)
* [[Template:JULIANDAY.JULIAN.YEAR]] (returns the year from a JD, in the Julian calendar)
* [[Template:JULIANDAY.JULIAN.MONTH]] (returns the month from a JD ,in the Julian calendar)
* [[Template:JULIANDAY.JULIAN.DAY]] (returns the day of month from a JD, in the Julian calendar)
* [[Template:JULIANDAY.YEAR]] (returns the year from a JD, in the Gregorian calendar)
* [[Template:JULIANDAY.MONTH]] (returns the month from a JD, in the Gregorian calendar)
* [[Template:JULIANDAY.DAY]] (returns the day of month from a JD, in the Gregorian calendar)
* [[Template:JULIANDAY.HOUR]] (returns the hour from a JD)
* [[Template:JULIANDAY.MINUTE]] (returns the minute from a JD)
* [[Template:JULIANDAY.SECOND]] (returns the second from a JD)
* [[Template:YEARCC]]
* [[Template:YEARYY]]
* [[Template:CENTURY]]
* [[Template:ISLEAPYEAR]]
* [[Template:WEEKDAY]]
* [[Template:ISOYEAR]]
* [[Template:CURRENTJULIANDAY]]