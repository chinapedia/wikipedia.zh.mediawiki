{{Infobox
| bodyclass  = vevent
| bodystyle  = {{{bodystyle|}}}

| titleclass = summary
| title      = {{#if:{{{title|{{{name|}}}}}} |{{{title|{{{name|}}}}}} |<includeonly>{{PAGENAMEBASE}}</includeonly>}}

| image       = {{#invoke:InfoboxImage|InfoboxImage|image={{{logo|}}}|size={{{logo size|{{{logo_size|}}}}}}|sizedefault={{#if:{{{screenshot|}}}|x64px|frameless}}|alt={{{logo alt|{{{logo_alt|}}}}}}}}
| caption     = {{{logo caption|}}}
| image2      = {{#if:{{{collapsible|}}} |{{Hidden begin |title=Screenshot |toggle=left |titlestyle=text-align:left |contentstyle=text-align:center}} }}<!--
                 -->{{#invoke:InfoboxImage|InfoboxImage |image={{{screenshot|}}} |size={{{screenshot_size|{{{screenshot size|}}}}}} |sizedefault=300px |alt={{{screenshot_alt|{{{screenshot alt|}}}}}} }}
| caption2    =      {{{screenshot caption|}}}<!--
            -->{{#if:{{{collapsible|}}} |{{Hidden end}} }}

| headerstyle = background-color: #eee;
| labelstyle = white-space: nowrap

| label1     = [[编程范型|-{zh-hans:编程范型; zh-hant:編程範型;}-]]
| data1      = {{{paradigm|{{{paradigms|}}}}}}

| label2     = 语言家族
| data2      = {{{family|}}}

| label3     = 設計者
| data3      = {{{designer|{{{designers|}}}}}}

| label4     = 實作者
| class4     = organiser
| data4      = {{{developer|{{{developers|}}}}}}

| label5     = -{zh-hans:发行时间;zh-tw:面市時間;zh-hk:釋出時間}-
| data5      = {{{released|{{{year|}}}}}}

| data6    = {{#ifeq:{{{ver layout|simple}}}|stacked
 |{{Infobox software/stacked
  |{{{name|{{PAGENAME}}}}}
  |{{{discontinued|no}}}
  |{{{latest release version|{{{latest_release_version|}}}}}}
  |{{{latest release date   |   {{{latest_release_date|}}}}}}
  |{{{latest preview version|   {{{latest test version|{{{latest_preview_version|{{{latest_test_version|}}} }}} }}} }}}
  |{{{latest preview date   |      {{{latest test date|{{{latest_preview_date   |{{{latest_test_date   |}}} }}} }}} }}}
  }}
 |{{Infobox software/simple
  |{{{name|{{PAGENAME}}}}}
  |{{{discontinued|no}}}
  |{{{latest release version|{{{latest_release_version|}}}}}}
  |{{{latest release date   |   {{{latest_release_date|}}}}}}
  |{{{latest preview version|   {{{latest test version|{{{latest_preview_version|{{{latest_test_version|}}} }}} }}} }}}
  |{{{latest preview date   |      {{{latest test date|{{{latest_preview_date   |{{{latest_test_date   |}}} }}} }}} }}}
  }}
 }}

| label8    = [[類型系統|型態系統]]
| data8     = {{{typing|}}}

| label9    = [[作用域]]
| data9     = {{{scope|}}}

| label10    = 實作語言
| data10     = {{{programming language|{{{programming_language|}}}}}}

| label11    = [[系统平台]]
| data11     = {{{platform|}}}

| label12    = [[作業系統]]
| data12     = {{{operating system|{{{operating_system|}}}}}}

| label13    = [[软件许可证|許可證]]
| data13     = {{{license|}}}

| label14    = [[文件扩展名]]
| data14     = {{{File extensions|{{{file extensions|{{{file ext|{{{file_ext|}}}}}}}}}}}}

| label15    = [[檔案格式]]
| data15     = {{{File format|{{{file format|{{{file_format|{{{fileformat|{{{file formats|}}}}}}}}}}}}}}}

| label16    = 網站
| data16      = {{#if:{{{website|}}}
                  |{{#ifeq:{{{website|}}}|hide||{{{website|}}} }}
                  |{{official url}}
               }}

| header17    = {{#if:{{{implementations|}}}|主要實作產品}}
| data18      = {{{implementations|}}}

| header19    = {{#if:{{{dialects|}}}|衍生副語言}}
| data20      = {{{dialects|}}}

| header21    = {{#if:{{{influenced by|{{{influenced_by|}}}}}}|啟發語言}}
| data22      = {{{influenced by|{{{influenced_by|}}}}}}

| header23    = {{#if:{{{influenced|}}}|影響語言}}
| data24      = {{{influenced|}}}

| belowclass  = hlist
| belowstyle  = border-top: 1px solid #aaa; padding-top: 3px;
| below      =
{{#if:{{{wikibooks|}}}|
* {{wikibooks-inline|{{{wikibooks}}}}}
}}

}}<noinclude>
{{documentation}}
</noinclude>