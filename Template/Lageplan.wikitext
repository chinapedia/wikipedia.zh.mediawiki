{{#if: {{{map|}}} | {{{!}} border="0" cellspacing="0" cellpadding="0" style="margin:0 0 0 0; border-style:none; border-width:0px; border-collapse:collapse; empty-cells:show; background:none"
{{!}}{{#ifexpr: {{#expr: ({{{pos_x|-1}}} >= 0) and ({{{pos_x|0}}} <= 100) and ({{{pos_y|-1}}} >= 0) and ({{{pos_y|0}}} <=100) }}
|
<div style="position: relative;"><div style="font-size: {{{markersize|5}}}px; position: absolute; display: block; left:{{#expr: ({{{mapsize_x|140}}}*{{{pos_x|3}}}/100  - {{{markersize|5}}} /2 ) round 0 }}px; top:{{#expr: ({{{mapsize_y|175}}}*{{{pos_y|3}}}/100 - {{{markersize|5}}} /2 ) round 0 }}px; padding:0;">[[File:{{{marker|Reddot.svg}}}|{{{markersize|5}}}px|{{{markertext|}}}]]</div>[[File:{{{map|Karte Deutschland.png}}}|{{{mapsize_x|140}}}px|{{{maptext|}}}]]</div>
|
<span style="color:#ff0000">{{{warning|Error}}}</span>
}}
{{!}}} }}<noinclude>

== Zweck ==
Anzeigen eines Lageplans mit frei wählbarer Karte, Marker, Größe und ''relativer'' Positionierung.

(Achtung: Vor allem der [[Internet Explorer]] reagiert äußerst sensibel auf kleine, vieleicht unscheinbare Änderungen des Quelltextes. Bitte nach dem Bearbeiten unbedingt auch im Internet Explorer testen, da es nach wie vor Benutzer gibt, die ihn einsetzen.)

== Syntax ==
<pre>
{{Lageplan
|marker      = <!-- Symbol zur Markierung, möglichst SVG, z.B. reddot.svg -->
|markersize  = <!-- Größe der Markierung ( < mapsize/3) -->
|markertext  = <!-- Beschriftung -->
|pos_x       = <!-- relative x-Position (0-100)-->
|pos_y       = <!-- relative y-Position (0-100)-->
|map         = <!-- Name der Karte -->
|mapsize_x   = <!-- Größe der Karte in x-Richtung -->
|mapsize_y   = <!-- Größe der Karte in y-Richtung -->
|maptext     = <!-- Beschriftung der Karte -->
|warning     = <!-- Out of range Meldung -->>
}}
</pre>
[[Category:格式模板]]
</noinclude>