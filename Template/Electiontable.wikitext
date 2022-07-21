<noinclude>
== Usage ==
This template marks the beginning of a table and defines borders, margins, background colours, and text alignment within the table. (Default alignment is "right", others must be specified.) Table rows and cells are written as usual, and the table is closed with "<code><nowiki>|}</nowiki></code>"

For example, to have a table as shown below, include the code shown to the right:
{| align="right" style="margin: 0 0 1em 2em;"
|<small><pre>{{electiontable|Table template pagename}}
'''Summary of [[Mars]]ian election results, [[2005]]'''
|- style="background: #E9E9E9;"
! align="left"|Parties
! Votes
! %
! +/-
! Seats
! +/-
|-
| align="left"|The Green Party
| 123,456
| 79.2
| -8.3
| 53
| -8
|-
| align="left"|The Red Party
| 23,697
| 15.2
| +6.6
| 10
| +4
|-
| align="left"|The Sun-Followers' Party
| 8,730
| 5.6
| +1.7
| 4
| +4
|- style="background: #E9E9E9;"
! align="left"|Total
! 155,883
! align="center" colspan="2"|100%
! align="center" colspan="2"|67
|}</pre></small>
|}

{{electiontable|Table template pagename}}'''Summary of [[Mars]]ian election results, [[2005]]'''
|- style="background: #E9E9E9;"
! align="left"|Parties
! Votes
! %
! +/-
! Seats
! +/-
|-
| align="left"|The Green Party
| 123,456
| 79.2
| -8.3
| 53
| -8
|-
| align="left"|The Red Party
| 23,697
| 15.2
| +6.6
| 10
| +4
|-
| align="left"|The Sun-Followers' Party
| 8,730
| 5.6
| +1.7
| 4
| +4
|- style="background: #E9E9E9;"
! align="left"|Total
! 155,883
! align="center" colspan="2"|100%
! align="center" colspan="2"|67
|}</noinclude><includeonly>{| class="wikitable {{#if:{{{collapsed|}}}|collapsible collapsed}} {{#ifeq:{{{sortable|}}}|yes|sortable}}" style="text-align:right; font-size: 95%; {{#if:{{{align|}}}|float:{{{align}}};}}"
{{#if:{{{collapsed|}}}|! colspan=12 style="text-align:center; font-weight:normal;" {{!}}|{{!}}+}} {{#ifeq:{{{editlink|}}}|no||<span style="float:left; align:left; font-size: 75%;" class="editlink noprint plainlinks nourlexpansion">[{{fullurl:{{transclude|{{{1|{{PAGENAME}}}}}}}|action=edit}} 编辑]&nbsp;•&nbsp;[[{{TALKPAGENAME:{{transclude|{{{1|{{PAGENAME}}}}}}}}}|讨论]]</span>&nbsp;}}{{#if:{{{2|}}}|{{{2}}}}}</includeonly><noinclude>

[[Category:政治模板]]
</noinclude>