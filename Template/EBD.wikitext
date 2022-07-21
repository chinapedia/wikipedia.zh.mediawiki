{{#if: {{{noicon|}}}|<!--empty-->|
   <!--else-->{{#ifeq: {{{wstitle|}}}|<!--eq to empty-->|
               <!--then-->[[File:PD-icon.svg|12px|alt=]]&nbsp;
               |<!--else-->[[File:Wikisource-logo.svg|12px|alt=]]&nbsp;}}<!--endif
-->}}{{{prescript|{{#ifeq: {{{inline|}}} |<!--eq to empty-->|<!--
                      then display-->本條目
                      |<!--else display-->本條目部分或全部内容
                    }}<!-- no white space
      -->出自已經處於[[公有領域]]的：}}}<!-- no white space
-->{{Cite EBD
<!--Fixed parameters entries-->
 |noicon=1
 |ref={{{ref|harv}}}

<!-- this none standard parameter removes from display some of the default parameters -->
 |{{#if:{{{short|}}} |short |HIDE_PARAMETER}}={{{|short}}}

<!--These entries are set by default in Cite EDB-->
 |{{#if:{{{encyclopedia|}}} |encyclopedia |HIDE_PARAMETER1}}={{{|encyclopedia}}}
 |{{#if:{{{year|}}}         |year         |HIDE_PARAMETER2}}={{{|year}}}
 |{{#if:{{{first|}}}        |first        |HIDE_PARAMETER3}}={{{|first}}}
 |{{#if:{{{last|}}}         |last         |HIDE_PARAMETER4}}={{{|last}}}
 |{{#if:{{{authorlink|}}}   |authorlink   |HIDE_PARAMETER5}}={{{|authorlink}}}
 |{{#if:{{{edition|}}}      |edition      |HIDE_PARAMETER6}}={{{edition|}}}
 |{{#if:{{{publisher|}}}    |publisher    |HIDE_PARAMETER7}}={{{publisher|}}}

<!--Check that either title or wstitle is set or display a warning in red -->
 |{{#if:{{{1|}}}       |wstitle   |HIDE_PARAMETER8}}={{{1|}}}
 |{{#if:{{{wstitle|}}} |wstitle   |HIDE_PARAMETER9}}={{{wstitle|}}}
 |{{#if:{{{title|}}}   |title     |HIDE_PARAMETER10}}={{{title|}}}
 |{{#if:{{{url|}}}     |url       |HIDE_PARAMETER11}}={{{url|}}}

<!--These are optional parameters-->
 |{{#if:{{{volume|}}} |volume   |HIDE_PARAMETER12}}={{{volume|}}}
 |{{#if:{{{page|}}}   |page     |HIDE_PARAMETER13}}={{{page|}}}
 |{{#if:{{{pages|}}}  |pages    |HIDE_PARAMETER14}}={{{pages|}}}
}}<includeonly>
[[Category:含有伊斯頓聖經辭典內容的維基百科條目]]</includeonly><noinclude>
{{Documentation}}
</noinclude>