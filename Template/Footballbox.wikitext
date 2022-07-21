<div class="vevent" style="clear:both; background:{{{bg|transparent}}}; width:{{{size|100%}}}" {{#if:{{{id|}}}|id={{#ifeq:{{str sub old|{{{id}}}|0|1}}|" |{{{id|}}}|"{{{id}}}"}} }}>
{{#if:{{{event|}}}|
<div style="text-align:center">'''{{{event}}}'''</div>
}}<span class="summary" style="display:none">{{{team1}}} v {{{team2}}}</span>
{| style="float:left; width:15%; table-layout:fixed"
|<div style="text-align:right">{{{date}}}<br />{{#if:{{{time|}}}|{{{time}}}<br />| }}{{#if:{{{round|}}}|{{{round}}} }}</div>
|}
{| style="float:left; width:61%; table-layout:fixed; text-align:center"
|- style="vertical-align:top"
! style="width:39%; text-align:right" class="vcard attendee" | <span class="fn org">{{{team1}}}</span>
! style="width:22%; text-align:center" | {{#if:{{{score|}}}|{{{score}}}|對 }}<br> {{#if:{{{aet|}}}|<small>（[[加時賽]]）</small>}}
! style="width:39%; text-align:left" class="vcard attendee" | <span class="fn org">{{{team2}}}</span>
|- style="vertical-align:top; font-size:85%"
| style="text-align:right" | {{#ifeq:{{str sub old|{{{goals1}}}|0|1}}|* |{{plainlist|{{{goals1}}}}} |{{{goals1|}}}}}
| style="text-align:center" | {{#ifeq:{{str sub old|{{{report}}}|0|4}}|http |[{{{report}}} 報告] |{{{report|}}}}}{{#if:{{{yellowcard1|}}}{{{yellowcard2|}}}|<br />{{{yellowcard1|0}}} {{yel}} {{{yellowcard2|0}}} }}{{#if:{{{redcard1|}}}{{{redcard2|}}}|<br />{{{redcard1|0}}} {{sent off}} {{{redcard2|0}}} }}{{#if:{{{totalcard1|}}}{{{totalcard2|}}}|<br />{{{totalcard1|0}}} <span style="color:#0AF">═</span> {{{totalcard2|0}}} }}
| style="text-align:left" | {{#ifeq:{{str sub old|{{{goals2}}}|0|1}}|* |{{plainlist|{{{goals2}}}}} |{{{goals2|}}}}}
{{#if:{{{penaltyscore|}}}|
{{!}}-
{{!}} &nbsp;
! style="text-align:center" {{!}} [[互射十二碼|-{zh:互射十二碼;zh-hans:点球大战;zh-hk:互射十二碼;zh-tw:點球大戰;}-]]
{{!}} &nbsp;
{{!}}- style="vertical-align:top; font-size:85%"
{{!}} style="text-align:right" {{!}} {{#ifeq:{{str sub old|{{{penalties1}}}|0|1}}|* |{{plainlist|{{{penalties1}}}}} |{{{penalties1|}}}}}
! style="text-align:center" {{!}} {{{penaltyscore}}}
{{!}} style="text-align:left" {{!}} {{#ifeq:{{str sub old|{{{penalties2}}}|0|1}}|* |{{plainlist|{{{penalties2}}}}} |{{{penalties2|}}}}}
}}
|}
{| style="float:left; width:24%; table-layout:fixed"
|<div style="font-size:85%">{{#if:{{{stadium|}}}|<span class="location">{{{stadium}}}</span> }}{{#if:{{{attendance|}}}|<br />觀眾人數：{{{attendance}}}}}{{#if:{{{referee|}}}|<br />-{zh-cn:裁判;zh-tw:裁判;zh-hk:球證;}-：{{{referee}}} }}</div>
|}{{clear}}
</div><noinclude>
{{Documentation}}
[[Category:足球模板]]
[[Category:體育比賽框模板]]
</noinclude>