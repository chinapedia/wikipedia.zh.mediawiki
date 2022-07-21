<noinclude>{| class="toccolours" style="float: right; clear: right; margin: 0 0 1em 1em; padding: 3px;"
</noinclude><tr><th style="background-color: #FFFFC0; text-align: center;" colspan="2">[[天体测量学|天体测定]]</th></tr><tr><th colspan="2" style="text-align: center">{{{component1<includeonly>|</includeonly>}}}</tr><!--
-->{{#if:{{{radial_v<includeonly>|</includeonly>}}}|<tr valign=top><td>'''[[徑向速度]] <small>(R<sub>v</sub>)</small>'''</td><td>{{{radial_v}}} km/s</td></tr>}}<!--
-->{{#if:{{{prop_mo_ra<includeonly>|</includeonly>}}}{{{prop_mo_dec|}}}|<tr valign=top><td>'''[[自行]] <small>(μ)</small>'''</td><td> 赤经：{{{prop_mo_ra|-}}} [[毫角秒|mas]]/[[年|yr]] <br /> 赤纬：{{{prop_mo_dec|-}}} [[毫角秒|mas]]/[[年|yr]] </td></tr> }}<!--
-->{{#if:{{{parallax<includeonly>|</includeonly>}}}|<tr valign=top><td>'''[[视差]] <small>(π)</small>'''</td><td>{{{parallax}}}{{#if:{{{p_error|}}}|&nbsp;± {{{p_error}}} }}{{#if:{{{parallax_footnote|}}}|{{{parallax_footnote}}} }} [[毫角秒|mas]]</td></tr>}}<!--
-->{{#if:{{{dist_ly<includeonly>|</includeonly>}}}{{{dist_pc|}}}{{{parallax|}}}|<tr valign=top><td>'''[[宇宙距离尺度|距离]]'''</td><!--
--><td><!--
-->{{#if:{{{dist_ly<includeonly>|</includeonly>}}}{{{dist_pc|}}}||{{ErrorBar2|{{#expr: 3261.5638 / {{{parallax}}} }}|{{#if:{{{p_error|}}}|{{#expr: 3261.5638 * {{{p_error}}} / ({{{parallax}}} * {{{parallax}}}) }} }}|0.1}} [[光年|ly]] <br />({{ErrorBar2|{{#expr: 1000.0 / {{{parallax}}} }}|{{#if:{{{p_error|}}}|{{#expr: 1000.0 * {{{p_error}}} / ({{{parallax}}} * {{{parallax}}}) }} }}|0.1}} [[秒差距|pc]])}}<!-- -->{{#if:{{{dist_ly<includeonly>|</includeonly>}}}|{{{dist_ly}}} [[光年|ly]] {{#if:{{{dist_pc|}}}|<br />({{{dist_pc}}} [[秒差距|pc]])}}|{{#if:{{{dist_pc|}}}|{{{dist_pc}}} [[秒差距|pc]]}}}}<!--
--></td></tr>}}<!-- -->{{#if:{{{absmag_v<includeonly>|</includeonly>}}}|<tr valign=top><td>'''[[绝对星等]] <small>(M<sub>V</sub>)</small>'''</td><td>{{{absmag_v}}}</td></tr>}}<!--
--><tr><th colspan="2" style="text-align: center">{{{component2<includeonly>|</includeonly>}}}</th></tr><!--
-->{{#if:{{{radial_v2<includeonly>|</includeonly>}}}|<tr valign=top><td>'''[[徑向速度]] <small>(R<sub>v</sub>)</small>'''</td><td>{{{radial_v2}}} km/s</td></tr>}}<!--
-->{{#if:{{{prop_mo_ra2<includeonly>|</includeonly>}}}{{{prop_mo_dec2|}}}|<tr valign=top><td>'''[[自行]] <small>(μ)</small>'''</td><td> 赤经：{{{prop_mo_ra2|-}}} [[毫角秒|mas]]/[[年|yr]] <br /> 赤纬：{{{prop_mo_dec2|-}}} [[毫角秒|mas]]/[[年|yr]] </td></tr> }}<!--
-->{{#if:{{{parallax2<includeonly>|</includeonly>}}}|<tr valign=top><td>'''[[视差]] <small>(π)</small>'''</td><td>{{{parallax2}}}{{#if:{{{p_error2|}}}|&nbsp;± {{{p_error2}}} }}{{#if:{{{parallax_footnote2|}}}|{{{parallax_footnote2}}} }} [[毫角秒|mas]]</td></tr>}}<!--
-->{{#if:{{{dist_ly2<includeonly>|</includeonly>}}}{{{dist_pc2|}}}{{{parallax2|}}}|<tr valign=top><td>'''[[宇宙距离尺度|距离]]'''</td><!--
--><td><!--
-->{{#if:{{{dist_ly2<includeonly>|</includeonly>}}}{{{dist_pc2|}}}||{{ErrorBar2|{{#expr: 3261.5638 / {{{parallax2}}} }}|{{#if:{{{p_error2|}}}|{{#expr: 3261.5638 * {{{p_error}}} / ({{{parallax2}}} * {{{parallax2}}}) }} }}|0.1}} [[光年|ly]] <br />({{ErrorBar2|{{#expr: 1000.0 / {{{parallax2}}} }}|{{#if:{{{p_error2|}}}|{{#expr: 1000.0 * {{{p_error2}}} / ({{{parallax2}}} * {{{parallax2}}}) }} }}|0.1}} [[秒差距|pc]])}}<!-- -->{{#if:{{{dist_ly<includeonly>|</includeonly>}}}|{{{dist_ly2}}} [[光年|ly]] {{#if:{{{dist_pc2|}}}|<br />({{{dist_pc2}}} [[秒差距|pc]])}}|{{#if:{{{dist_pc2|}}}|{{{dist_pc2}}} [[秒差距|pc]]}}}}<!--
--></td></tr>}}<!-- -->{{#if:{{{absmag_v2<includeonly>|</includeonly>}}}|<tr valign=top><td>'''[[绝对星等]] <small>(M<sub>V</sub>)</small>'''</td><td>{{{absmag_v2}}}</td></tr>}}<noinclude>
|}
{{Documentation}}
</noinclude>