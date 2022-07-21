{| class="wikitable {{#if:{{{collapsed|}}}|collapsible collapsed}}" style="{{#if:{{{collapsed|}}}|width:100%;}}text-align:center" {{#if:{{{id|}}}|id={{{id}}}}}
|-
{{#if:{{{title|}}}|! colspan=10 {{!}} {{{title}}} }}
|-
!{{#ifeq:{{{1<includeonly>|</includeonly>}}}|index|!!|}} style="text-align:center; width:{{#if:{{{team-width|}}}|{{{team-width}}}|250px}}"|{{#if:{{{team1|}}}|{{{team1}}}|第一隊}}
! style="width:{{#if:{{{score-width|}}}|{{{score-width}}}|100px}}"|{{#if:{{{agg-score|}}}|{{{agg-score}}}|總比數}}
! style="text-align:center; width:{{#if:{{{team-width|}}}|{{{team-width}}}|250px}}"|{{#if:{{{team2|}}}|{{{team2}}}|第二隊}}
! style="width:{{#if:{{{score-width|}}}|{{{score-width}}}|90px}}"|首回合
! style="width:{{#if:{{{score-width|}}}|{{{score-width}}}|90px}}"|次回合<!--
-->{{#ifexpr: {{{legs|0}}} > 2|!! style="width:{{#if:{{{score-width|}}}|{{{score-width}}}|90px}}"{{!}}第三回合|}}<!--
-->{{#ifexpr: {{{legs|0}}} > 3|!! style="width:{{#if:{{{score-width|}}}|{{{score-width}}}|90px}}"{{!}}第四回合|}}<!--
-->{{#if: {{{extra|}}} |!! style="width:{{#if:{{{score-width|}}}|{{{score-width}}}|90px}}"{{!}}{{{extra}}}}}<!--
--><noinclude>
[[Category:足球模板|{{PAGENAME}}]]
</noinclude>