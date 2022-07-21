{| class="{{talk other|demospace={{{demospace|}}}|tmbox tmbox-notice|ombox ombox-notice}} {{#ifeq:{{{small|}}}|yes|mbox-small}} {{#ifeq:{{{collapsed|}}}|yes|collapsible collapsed}} t-todo" style="border-collapse:separate; {{{style|}}}" cellspacing="4"
<tr><th class="mbox-text" style="text-align:left; padding:1px;">{{
  #if: {{{inner|}}}
  | <!--nothing-->
  | <span class="noprint plainlinks" style="float:right; text-align:right; font-size:{{#ifeq:{{{small|}}}|yes|100|88}}%; font-weight:normal;">[{{fullurl:{{#rel2abs:{{{list|./to do}}}|{{{target|}}}}}|action=edit{{
    #ifeq: {{{nopreload}}} | yes | | &preload=Template:Tasks/Preload}}
  }} {{
    #ifeq: {{{small|}}} | yes | 编 | 编辑
  }}]{{·}}[{{fullurl:{{#rel2abs:{{{list|./to do}}}|{{{target|}}}}}|action=history}} {{
    #ifeq: {{{small|}}} | yes | 历 | 历史
  }}]{{·}}[{{fullurl:{{#rel2abs:{{{list|./to do}}}|{{{target|}}}}}|action=watch}} {{
    #ifeq: {{{small|}}} | yes | 监 | 监视
  }}]{{·}}[{{fullurl:{{#rel2abs:.}}|action=purge}} {{
    #ifeq: {{{small|}}} | yes | 刷  | 刷新 
  }}]</span>
}}{{
  #ifeq: {{{image|}}} | none
  | <!--nothing-->
  | [[File:{{{image|Stock post message.svg}}}|{{#ifeq:{{{small|}}}|yes|20|25}}px]]
<!-- }} [[Wikipedia:需進行工作列表|任务{{#ifeq:{{{small|}}}|yes||列表}}]]{{ -->
}}{{{for|[[:{{{target|{{SUBJECTPAGENAME}}}}}]]}}}的[[Wikipedia:需進行工作列表|任务{{#ifeq:{{{small|}}}|yes||列表}}]]{{
  #ifeq: {{#ifeq:{{{smallfor|}}}|yes|no|{{{small|}}}}}|yes|| <!--留空 -->
}}:</th><td class="mbox-empty-cell"></td></tr>{{
  #if: {{{above|}}} | <tr class="todo-abovebelow"><td colspan="2">{{{above}}}</td></tr>
}}
|-
| class="todo-box" colspan="2" style="{{talk other|demospace={{{demospace|}}}|background:#fffaef;}} border:1px dotted gray; padding: 2px 4px;" |{{{inner|{{
  #ifexist: {{ #rel2abs: {{{list|./to do}}} | {{{target|}}} }}
  | <!--/to do exists, show it-->{{ {{ #rel2abs: {{{list|./to do}}} | {{{target|}}} }} }}
  | <!--it doesn't--> <small>''该任务列表是空的：请将<nowiki>{{to do}}</nowiki>标签从页面移除，或点击“编辑”添加任务项。''</small>
}}}}}
|-
{{
  #if: {{{below|}}} | <tr class="todo-abovebelow"><td colspan="2">{{{below}}}</td></tr>
}}{{
  #if: {{{1|}}} | <tr class="todo-priority"><td colspan="2" style="text-align:right; font-size:smaller;">'''优先级 {{{1}}} {{ #ifeq: {{{1}}} | 1 | (top) }}'''</td></tr>
}}
|}<includeonly>{{
  #ifeq: {{{nocats}}} | yes | | {{{category|[[Category:含有工作列表的维基页面|{{PAGENAME}}]]}}}{{
    #if: {{{inner|}}} | | {{
      #ifexist: {{#rel2abs:{{{list|./to do}}}|{{{target|}}}}} | [[Category:含有工作列表且使用中的维基页面]]
       }}
    }}
  }}</includeonly><noinclude>
{{Documentation}}
<!-- Please add interwikis to the /doc subpage, not here. -->
</noinclude>