<includeonly>{{#if:{{{system|}}}|<!-- 

    以是否输入了system参数判断编者试图调用的是本地版本还是英文版版本的s-line。
    以下为英文版s-line，更新于2017年

--><tr>
{{#if:{{{hide1|}}}||<td rowspan="{{{rows1|1}}}" style="text-align: center; vertical-align: middle; {{#ifexist:Template:{{{system}}} style|{{#switch:{{{{{system}}} style|export}}|AUS|CRR=border: 3px #{{{{{system}}} color|{{{line}}}}} solid;|#default=border-left: 0px none; border-bottom: 0px none; border-right: 1px #aaa solid; border-top: 1px #aaa solid;}}|border-left: 0px none; border-bottom: 0px none; border-right: 1px #aaa solid; border-top: 1px #aaa solid;}}">{{S-line/side cell|through={{{through1|}}}|state={{{state1|}}}|branch={{{branch|}}}|next={{{previous|}}}|system={{{system|}}}|line={{{line|}}}|note={{{note|}}}|type={{{type|}}}|oneway={{{oneway1|}}}|round={{{round1|}}}|circular={{#if:{{{circular|}}}|1|{{{circular1|}}}}}|side=left}}</td>
}}{{#if:{{{hidemid|}}}||{{#ifexist:Template:{{{system}}} style|{{#ifeq:{{{{{system}}} style|export}}|AUS||<td rowspan="{{{rowsmid|1}}}" style="text-align: center; border-left: 0px none; border-bottom: 0px none; border-right: 0px none; border-top: 1px #aaa solid; width: 1px; background-color: #{{{{{system}}} color|{{{line}}}}}"></td>}}|<td rowspan="{{{rowsmid|1}}}" style="text-align: center; border-left: 0px none; border-bottom: 0px none; border-right: 0px none; border-top: 1px #aaa solid; width: 1px; background-color: #{{{{{system}}} color|{{{line}}}}}"></td>}}
}}{{#if:{{{hidemid|}}}||<td rowspan="{{{rowsmid|1}}}" {{#ifexist:Template:{{{system}}} style|{{#switch:{{{{{system}}} style|export}}|CRR=style="text-align: center; vertical-align: middle; border: 3px #{{{{{system}}} color|{{{line}}}}} solid;"|AUS=colspan="3" style="text-align: center; vertical-align: middle; font-weight: bold; color: #{{{{{system}}} color|{{{line|}}}|font}}; border: 3px #{{{{{system}}} color|{{{line}}}}} solid; background-color: #{{{{{system}}} color|{{{line}}}}};"|#default=style="text-align: center; vertical-align: middle; border-bottom: 0px none;"}}|style="text-align: center; vertical-align: middle; border-bottom: 0px none;"}}>{{#ifexist:Template:{{{system}}} style|{{#ifeq:{{{{{system}}} style|export}}|AUS|<span style="color: #{{{{{system}}} color|{{{line}}}|font}};">}}}}{{#ifeq:{{{line}}}|{{{{{system}}} lines|{{{line}}}}}|{{{line}}}|{{{{{system}}} lines|{{{line}}}}}}}{{#ifexist:Template:{{{system}}} style|{{#ifeq:{{{{{system}}} style|export}}|AUS|</span>}}}}{{#if:{{{branch|}}}|<div style="font-size:smaller">{{#ifexist:Template:{{{system}}} lines/branches|{{{{{system}}} lines/branches|branch={{{branch|}}}|system={{{system|}}}|line={{{line|}}}}}|{{{branch}}}}}</div>}}{{#if:{{{notemid|}}}|<div style="font-size:smaller">{{{notemid|}}}</div>}}{{#if:{{{transfer|}}}|<div style="font-size:smaller">''Transfer at: {{{{{system}}} stations|line={{{line}}}|station={{{transfer}}}}}''</div>}}</td>
}}{{#if:{{{hidemid|}}}||{{#ifexist:Template:{{{system}}} style|{{#ifeq:{{{{{system}}} style|export}}|AUS||<td rowspan="{{{rowsmid|1}}}" style="text-align: center; border-left: 0px none; border-bottom: 0px none; border-right: 0px none; border-top: 1px #aaa solid; width: 1px; background-color: #{{{{{system}}} color|{{{line}}}}}"></td>}}|<td rowspan="{{{rowsmid|1}}}" style="text-align: center; border-left: 0px none; border-bottom: 0px none; border-right: 0px none; border-top: 1px #aaa solid; width: 1px; background-color: #{{{{{system}}} color|{{{line}}}}}"></td>}}}}{{#if:{{{hide2|}}}||<td rowspan="{{{rows2|1}}}" style="text-align: center; vertical-align: middle; {{#ifexist:Template:{{{system}}} style|{{#switch:{{{{{system}}} style|export}}|AUS|CRR=border: 3px #{{{{{system}}} color|{{{line}}}}} solid;|#default=border-left: 1px #aaa solid; border-bottom: 0px none; border-right: 0px none; border-top: 1px #aaa solid;}}|border-left: 1px #aaa solid; border-bottom: 0px none; border-right: 0px none; border-top: 1px #aaa solid;}}">{{S-line/side cell|through={{{through2|}}}|state={{{state2|}}}|branch={{{branch|}}}|next={{{next|}}}|system={{{system|}}}|line={{{line|}}}|note={{{note2|}}}|type={{{type2|}}}|oneway={{{oneway2|}}}|round={{{round2|}}}|circular={{#if:{{{circular|}}}|1|{{{circular2|}}}}}|side=right}}</td>}}
</tr><!--

    英文版s-line结束

-->|<!--

    以下为本地原版s-line

-->{{#if:{{{sup|}}}|{{#ifeq:{{{sup|}}}|0|{{Terminus|{{{rowssup|rows={{{rows|1}}}}}}}}|{{#if:{{{supm|}}}|{{s-abandoned|{{{sup}}}|rows={{{rowssup|{{{rows|1}}}}}}}}|{{#if:{{{supn|}}}|{{s-unbuilt|{{{sup}}}|rows={{{rowssup|{{{rows|1}}}}}}}}|{{s-inop|{{{sup}}}|rows={{{rowssup|{{{rows|1}}}}}}}}}}}}}}}}
{{!}} width="1px" style="border-left: 0px none; border-bottom: 0px none; border-right: 0px none; border-top: 1px #aaa solid; background:{{{3|#0008BD}}}; nboexaq:如果您看到这行字，请在<nowiki>{{s-line}}</nowiki>前面换行; " rowspan="{{{rowsup|{{{rows|1}}}}}}"{{!}}
{{!}} width="177px" align="center" style="vertical-align: middle; border-bottom: 0px none; text-align: center; white-space:nowrap;" rowspan="{{{rows|1}}}"{{!}}{{#if:{{{1|}}}|'''{{{1}}}'''}}{{#if:{{{1|}}}|{{#if:{{{2|}}}|<br />}}}}{{#if:{{{2|}}}|{{{2}}}}}
{{!}} width="1px" style="border-left: 0px none; border-bottom: 0px none; border-right: 0px none; border-top: 1px #aaa solid; background:{{{4|{{{3|#0008BD}}}}}};" rowspan="{{{rowsdown|{{{rowsup|{{{rows|1}}}}}}}}}"{{!}}
{{#if:{{{sdown|}}}|{{#ifeq:{{{sdown|}}}|0|{{Terminus|rows={{{rowssdown|{{{rowssup|{{{rows|1}}}}}}}}}}}|{{#if:{{{sdownm|}}}|{{s-abandoned|{{{sdown}}}|rows={{{rowssdown|{{{rowssup|{{{rows|1}}}}}}}}}}}|{{#if:{{{sdownn|}}}|{{s-unbuilt|{{{sdown}}}|rows={{{rowssdown|{{{rowssup|{{{rows|1}}}}}}}}}}}|{{s-inop|{{{sdown}}}|rows={{{rowssdown|{{{rowssup|{{{rows|1}}}}}}}}}}}}}}}}}}}
{{#if:{{{5|}}}|{{!}}-
{{!}} width="1px" style="background:{{{5}}};" rowspan="{{{rowsup2|{{{rowsdown|{{{rowsup|{{{rows|1}}}}}}}}}}}}"{{!}}
{{!}} width="1px" style="background:{{{6|{{{5}}}}}};" rowspan="{{{rowsdown2|{{{rowsup2|{{{rowsdown|{{{rowsup|{{{rows|1}}}}}}}}}}}}}}}"{{!}}}}
{{#if:{{{7|}}}|{{!}}-
{{!}} width="1px" style="background:{{{7}}};" rowspan="{{{rowsup3|{{{rowsdown|{{{rowsup|{{{rows|1}}}}}}}}}}}}"{{!}}
{{!}} width="1px" style="background:{{{8|{{{7}}}}}};" rowspan="{{{rowsdown3|{{{rowsup3|{{{rowsdown|{{{rowsup|{{{rows|1}}}}}}}}}}}}}}}"{{!}}}}<!--

    本地原版s-line结束

-->}}</includeonly><noinclude>
{{Documentation}}
</noinclude>