{{#ifexist: Template:Party meta/color/{{{名稱|}}}
    | <!--
     -->{{#if: {{{黨徽|}}}{{{大小|}}}
            | <span style="height:{{#if:{{{大小|}}} | {{{大小}}} | 20px}}; width:{{#if:{{{大小|}}} | {{{大小}}} | 20px}}; display:inline-block; border-radius:10px">[[File:{{#if:{{{黨徽|}}} | {{{黨徽}}} | Stemicoon neutraal.png}} |{{#if: {{{大小|}}} | {{{大小}}} | 20px}}|{{{名稱}}}]]</span>
            | <span style="height:1.4em; width:1.6em; padding-bottom:0.2em; text-align:center; font-size:85%; color:#FFFFF0; display:inline-block; background:-moz-linear-gradient(bottom right, {{Party meta/color/{{{名稱}}}}}, white); background:-webkit-linear-gradient(bottom right, {{Party meta/color/{{{名稱}}}}}, white); background:linear-gradient(to top left, {{Party meta/color/{{{名稱}}}}}, {{#if:{{{顏色|}}} |{{{顏色}}}, {{{顏色}}} 15%,}} {{Party meta/color/{{{名稱}}}}} 33%, white)">&nbsp;</span><!--
     -->}}
    | <!--
     -->{{#if: {{{黨徽|}}}{{{大小|}}} 
            | <span style="height:{{#if:{{{大小|}}} | {{{大小}}} | 20px }}; width:{{#if:{{{大小|}}} | {{{大小}}} | 20px }}; display:inline-block; border-radius:10px">[[File:{{#if:{{{黨徽|}}} | {{{黨徽}}} | Stemicoon neutraal.png}} |{{#if:{{{大小|}}} | {{{大小}}} | 20px}}|{{{名稱}}}]]</span>
            | <span style="height:1.4em; width:1.6em; padding-bottom:0.2em; text-align:center; font-size:85%; color:#FFFFF0; display:inline-block; background:-moz-linear-gradient(bottom right, {{{顏色|gray}}}, white); background:-webkit-linear-gradient(bottom right, {{{顏色|gray}}}, white); background:linear-gradient(to top left, {{{顏色|gray}}}, {{{顏色|gray}}} 33%, white)">&nbsp;</span>
        }}<!--
 -->}}&nbsp;<!--
 -->{{#if: {{{簡稱|}}}
        | [[{{{名稱}}}|{{{簡稱}}}]]
        | {{#ifexist:Template:Party meta/shortname/{{{名稱|}}}
            | [[{{{名稱}}}|{{Party meta/shortname/{{{名稱}}}}}]]
            | {{#if: {{{名稱|}}}
                | [[{{{名稱}}}]]
                | 無黨籍
            }}
        }}
    }}<!--
--><noinclude>
{{Documentation}}
<!-- 請將分類加到 /doc 子頁面 -->
</noinclude>