{{#if:{{{bwx|}}}|
<tr style="font-size: 90%; text-align:center">
<td style="vertical-align:middle;{{#if:{{{isnotlast|}}}|border-bottom:{{WPMILHIST Infobox style|internal_border}} }}">{{Infobox firearm cartridge/convert|{{{bwx|}}}|gr|g|round={{#if:{{{bwround|}}}|{{{bwround}}}|0}}|flip={{#ifeq:{{{bwunit|}}}|gram|yes}}}} {{{btypex|}}}</td>
<td style="{{#if:{{{isnotlast|}}}|border-bottom:{{WPMILHIST Infobox style|internal_border}} }}">{{Infobox firearm cartridge/convert|{{{velx|}}}|ft/s|m/s|flip={{{is_SI_ballistics|}}}}}</td>
<td colspan=2 style="{{#if:{{{isnotlast|}}}|border-bottom:{{WPMILHIST Infobox style|internal_border}} }}">{{Infobox firearm cartridge/convert|{{{enx|}}}|ft.lbf|J|flip={{{is_SI_ballistics|}}}}}</td>
</tr>
}}<noinclude>{{documentation|content=
This subtemplate of {{tl|Infobox firearm cartridge}} is used to create the rows in the ballistics table.  It should not be used directly

== Usage ==
<pre style="overflow:auto">
<table class="infobox">
<tr>
<th colspan=4 style="text-align:center">{{infobox firearm cartridge/ballistics header}}
{{infobox firearm cartridge/ballistics|bwx=1.0|bwunit=gr|btypex=foo|velx=1.0|enx=1.0}}
{{infobox firearm cartridge/ballistics|bwx=1.0|bwunit=gram|btypex=foo|velx=1.0|enx=1.0|is_SI_ballistics=yes}}
{{infobox firearm cartridge/ballistics|bwx=1.0|bwunit=gr|bwround=1|btypex=foo|velx=1.0|enx=1.0}}
{{infobox firearm cartridge/ballistics|bwx=1.0|bwunit=gram|bwround=1|btypex=foo|velx=1.0|enx=1.0|is_SI_ballistics=yes}}
</table>
</pre>
<table class="infobox">
<tr>
<th colspan=4 style="text-align:center">{{infobox firearm cartridge/ballistics header}}
{{infobox firearm cartridge/ballistics|bwx=1.0|bwunit=gr|btypex=foo|velx=1.0|enx=1.0}}
{{infobox firearm cartridge/ballistics|bwx=1.0|bwunit=gram|btypex=foo|velx=1.0|enx=1.0|is_SI_ballistics=yes}}
{{infobox firearm cartridge/ballistics|bwx=1.0|bwunit=gr|bwround=1|btypex=foo|velx=1.0|enx=1.0}}
{{infobox firearm cartridge/ballistics|bwx=1.0|bwunit=gram|bwround=1|btypex=foo|velx=1.0|enx=1.0|is_SI_ballistics=yes}}
</table>

}}
[[Category:武器信息框模板|F]]
</noinclude>