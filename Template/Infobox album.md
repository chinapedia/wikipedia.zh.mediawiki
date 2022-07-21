{{{{{|safesubst:}}}#invoke:Unsubst-infobox||$params=name,original_name,type,longtype,artist,cover,border,alt,caption,released,format,recorded,venue,studio,genre,length,language,label,director,producer,compiler,reviews,chart_position,certification,chronology,prev_title,prev_year,year,next_title,next_year,misc|$extra=original_name,longtype,border,caption,language,director,compiler,chart_position,certification,chronology,year,misc|$aliases=Name>name,Original_name>original_name,Type>type,image>cover,Cover>cover,Border>border,Alt>alt,Caption>caption,Longtype>longtype,Artist>artist,Released>released,Format>format,Recorded>recorded,Venue>venue,Studio>studio,Genre>genre,Length>length,Language>language,Label>label,Director>director,Producer>producer,Compiler>compiler,Reviews>reviews,Chart position>chart_position,Certification>certification,Chronology>chronology,Misc>misc|prev_title={{{{{|safesubst:}}}if empty|{{{prev_title|}}}|{{{{{|safesubst:}}}#if:{{{last_album|{{{Last album|}}}}}}|{{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{last_album|{{{Last album|}}}}}}|2=^([^<]+)%s*< ?/? ?[Bb][Rr] ?/? ?>|nomatch={{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{last_album|{{{Last album|}}}}}}|2=^<div class="plainlist"><ul><li>([^<]+)</li>}}}}}}}}|prev_year={{{{{|safesubst:}}}if empty|{{{prev_year|}}}|{{{{{|safesubst:}}}#if:{{{last_album|{{{Last album|}}}}}}|{{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{last_album|{{{Last album|}}}}}}|2=< ?/? ?[Bb][Rr] ?/? ?>%s*%（(%d+)%年）|nomatch={{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{last_album|{{{Last album|}}}}}}|2=<li>%（(%d+)%年）</li></ul></div>}}}}}}}}|next_title={{{{{|safesubst:}}}if empty|{{{next_title|}}}|{{{{{|safesubst:}}}#if:{{{next_album|{{{Next album|}}}}}}|{{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{next_album|{{{Next album|}}}}}}|2=^([^<]+)%s*< ?/? ?[Bb][Rr] ?/? ?>|nomatch={{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{next_album|{{{Next album|}}}}}}|2=^<div class="plainlist"><ul><li>([^<]+)</li>}}}}}}}}|next_year={{{{{|safesubst:}}}if empty|{{{next_year|}}}|{{{{{|safesubst:}}}#if:{{{next_album|{{{Next album|}}}}}}|{{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{next_album|{{{Next album|}}}}}}|2=< ?/? ?[Bb][Rr] ?/? ?>%s*%（(%d+)%年）|nomatch={{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{next_album|{{{Next album|}}}}}}|2=<li>%（(%d+)%年）</li></ul></div>}}}}}}}}|released={{{{{|safesubst:}}}if empty|{{{released|{{{Released|}}}}}}|{{{{{|safesubst:}}}#if:{{{this_album|{{{This album|}}}}}}|{{{{{|safesubst:}}}#if:{{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1=x{{{chronology|{{{Chronology|}}}}}}|2=[ ]recordings?$|nomatch=}}||{{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{this_album|{{{This album|}}}}}}|2=< ?/? ?[Bb][Rr] ?/? ?>%s*%（(%d+)%年）|nomatch={{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{this_album|{{{This album|}}}}}}|2=<li>%（(%d+)%年）</li></ul></div>}}}}}}}}}}|year={{{{{|safesubst:}}}#ifeq:{{{{{|safesubst:}}}#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|{{{released|{{{Released|}}}}}}|%d%d%d+}}|{{{year|}}}||{{{year|}}}}}|length={{{{{|safesubst:}}}#if:{{{length|{{{Length|}}}}}}|{{{{{|safesubst:}}}#invoke:String|replace|error_category=String模块出错的音乐信息框{{!}}A|1={{{{{|safesubst:}}}#invoke:String|replace|error_category=String模块出错的音乐信息框{{!}}A|1={{{{{|safesubst:}}}#invoke:String|replace|error_category=String模块出错的音乐信息框{{!}}A|1={{{{{|safesubst:}}}#invoke:String|replace|error_category=String模块出错的音乐信息框{{!}}A|1={{{length|{{{Length|}}}}}}|2=^([0-9][0-9]?)分?%.?,?:? ?([0-9])秒?%.?$|3=%1:0%2|plain=false}}|2=^([0-9][0-9]?)分?%.?,?:? ?([0-9][0-9]?)秒?%.?$|3=%1:%2|plain=false}}|2=^([0-9][0-9]?)分[钟鐘]?,?:? ?([0-9])秒?%.?$|3=%1:0%2|plain=false}}|2=^([0-9][0-9]?)分[钟鐘]?,?:? ?([0-9][0-9]?)秒?%.?$|3=%1:%2|plain=false}}}}|$flags=override|$B=<templatestyles src="ShareCSS/infobox.css" />{{infobox
| bodyclass   = vevent haudio

| aboveclass  = summary album
| abovestyle  = background-color: {{#ifeq:{{Infobox album/color|{{{type|{{{Type|}}}}}}}}|khaki|{{Infobox album/color}}|{{Infobox album/color|{{{type|{{{Type|}}}}}} }} }}
| above       = {{Br separated entries
 | 1 = {{#if:{{{name|{{{Name|}}}}}}|{{{name|{{{Name}}}}}}|<includeonly>无题</includeonly>}}
 | 2 = {{#if:{{{original_name|{{{Original_name|}}}}}}|<span style="font-size:small; font-weight:normal;">{{{original_name|{{{Original_name|}}}}}}</span>}}
}}

| image       = {{#invoke:InfoboxImage|InfoboxImage|image={{#switch:{{{image|{{{cover|{{{Cover|}}}}}}}}}|blank=|???=Nocover (zh).png|#default={{{image|{{{cover|{{{Cover|}}}}}}}}}}}|border={{{border|{{{Border|}}}}}}|alt={{{alt|{{{Alt|}}}}}}}}
| caption     = {{{caption|{{{Caption|}}}}}}

| headerstyle = background-color: {{#ifeq:{{Infobox album/color|{{{type|{{{Type|}}}}}}}}|khaki|{{Infobox album/color}}|{{Infobox album/color|{{{type|{{{Type|}}}}}}}}}}
| headerclass = description

| labelstyle  = white-space: nowrap;

| header1     = {{#if:{{{artist|{{{Artist|}}}}}}|<span class="contributor">{{{artist|{{{Artist}}}}}}</span>的}}{{Infobox album/link|{{{type|{{{Type|}}}}}} }}{{#if:{{{longtype|{{{Longtype|}}}}}}|{{{longtype|{{{Longtype}}}}}}}}
| label2      = 发行日期
| data2       = {{if empty|{{{released|{{{Released|}}}}}}|{{#if:{{{this_album|{{{This album|}}}}}}|{{#if:{{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1=x{{{chronology|{{{Chronology|}}}}}}|2=[ ]recordings?$|nomatch=}}||{{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{this_album|{{{This album|}}}}}}|2=< ?/? ?[Bb][Rr] ?/? ?>%s*%（(%d+)%年）|nomatch={{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{this_album|{{{This album|}}}}}}|2=<li>%（(%d+)%年）</li></ul></div>}}}}}}}}}}
| class2      = published
| label3      = 格式
| data3       = {{{format|{{{Format|}}}}}}
| class3      = hlist
| label4      = 录制时间
| data4       = {{{recorded|{{{Recorded|}}}}}}
| class4      = plainlist
| label5      = 场地
| data5       = {{{venue|{{{Venue|}}}}}}
| label6      = 录音室
| data6       = {{{studio|{{{Studio|}}}}}}
| class6      = plainlist
| label7      = [[音乐类型|类型]]
| data7       = {{{genre|{{{Genre|}}}}}}
| class7      = category hlist
| label8      = 时长
| data8       = {{#invoke:hms|main|duration={{{length|{{{Length|}}}}}}}}
| label9      = 语言
| data9       = {{{language|{{{Language|}}}}}}
| class9      = category
| label10     = [[唱片公司]]
| data10      = {{{label|{{{Label|}}}}}}
| class10     = hlist
| label11     = [[電影導演|导演]]
| data11      = {{{director|{{{Director|}}}}}}
| class11     = hlist
| label12     = [[音樂製作人|-{zh-cn:制作人;zh-tw:製作人;zh-hk:監製;}-]]
| data12      = {{{producer|{{{Producer|}}}}}}
| class12     = hlist
| label13     = 编选
| data13      = {{{compiler|{{{Compiler|}}}}}}
| class13     = hlist
| header14    = {{#if:{{{reviews|{{{Reviews|}}}}}}|评价}}
| data15      = {{#if:{{{reviews|{{{Reviews|}}}}}}|<div style="text-align: left; padding: 0; margin: 0">
{{{reviews|{{{Reviews|}}}}}}
</div>
}}
| header16    = {{#if:{{{chart_position|{{{Chart position|}}}}}}|排行榜最高名次}}
| data17      = {{#if:{{{chart_position|{{{Chart position|}}}}}}|<div style="text-align: left; padding: 0; margin: 0">
{{{chart_position|{{{Chart position|}}}}}}
</div>
}}
| header18    = {{#if:{{{certification|{{{Certification|}}}}}}|销量认证}}
| data19      = {{#if:{{{certification|{{{Certification|}}}}}}|<div style="text-align: left; padding: 0; margin: 0">
{{{certification|{{{Certification|}}}}}}
</div>
}}
| header20    = {{#if:{{{last_album|{{{Last album|}}}}}}{{{next_album|{{{Next album|}}}}}}{{{prev_title|}}}{{{next_title|}}}|{{#if:{{{chronology|{{{Chronology|}}}}}}|{{{chronology|{{{Chronology|}}}}}}|{{{artist|{{{Artist}}}}}}}}{{#ifeq:{{Infobox album/color|{{{type|{{{Type|}}}}}}}}|&#35;99CCFF|录像带|专辑}}年表}}
| data21      = {{#if:{{{last_album|{{{Last album|}}}}}}{{{next_album|{{{Next album|}}}}}}{{{prev_title|}}}{{{next_title|}}}|
{{(!}} style="background: transparent; width: 100%; min-width: 100%; border-collapse: collapse"
{{!}}- style="line-height: 1.4em;"
{{!}} style="width: 33%; text-align: center; vertical-align: top; padding: .2em .1em .2em 0" {{!}} {{#if:{{{prev_title|}}}|{{{prev_title}}}{{#if:{{{prev_year|}}}|<br />（{{{prev_year}}}年）}}|{{{last_album|{{{Last album|}}}}}}<span style="display:none">{{#if:{{{last_album|{{{Last album|}}}}}}|{{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{last_album|{{{Last album|}}}}}}|2=^([^<]+)%s*< ?/? ?[Bb][Rr] ?/? ?>|nomatch={{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{last_album|{{{Last album|}}}}}}|2=^<div class="plainlist"><ul><li>([^<]+)</li>}}}}{{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{last_album|{{{Last album|}}}}}}|2=< ?/? ?[Bb][Rr] ?/? ?>%s*%（(%d+)%年）|nomatch={{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{last_album|{{{Last album|}}}}}}|2=<li>%（(%d+)%年）</li></ul></div>}}}}}}</span> }}
{{!}} style="width: 33%; text-align: center; vertical-align: top; padding: .2em .1em" {{!}} {{{this_album|{{{This album|'''{{{name|{{{Name|{{PAGENAMEBASE}} }}}}}}'''{{#if:{{{next_year|}}}{{{prev_year|}}}|<br />（{{{year|{{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|{{{released|{{{Released|}}}}}}|%d%d%d+}}}}}年）}}}}}}}}
{{!}} style="width: 33%; text-align: center; vertical-align: top; padding: .2em 0 .2em .1em" {{!}} {{#if:{{{next_title|}}}|{{{next_title}}}{{#if:{{{next_year|}}}|<br />（{{{next_year}}}年）}}|{{{next_album|{{{Next album|}}}}}}<span style="display:none">{{#if:{{{next_album|{{{Next album|}}}}}}|{{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{next_album|{{{Next album|}}}}}}|2=^([^<]+)%s*< ?/? ?[Bb][Rr] ?/? ?>|nomatch={{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{next_album|{{{Next album|}}}}}}|2=^<div class="plainlist"><ul><li>([^<]+)</li>}}}}{{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{next_album|{{{Next album|}}}}}}|2=< ?/? ?[Bb][Rr] ?/? ?>%s*%（(%d+)%年）|nomatch={{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{next_album|{{{Next album|}}}}}}|2=<li>%（(%d+)%年）</li></ul></div>}}}}}}</span> }}
{{!)}}
}}

| below       = {{{misc|{{{Misc|}}}}}}
}}{{category handler
 |main={{#ifeq:{{Infobox album/color|{{{type|{{{Type|}}}}}}|Test}}|Test
  |[[Category:不標準的唱片信息框]]
 }}{{#ifeq:{{Infobox album/color|{{{type|{{{Type|}}}}}}}}|khaki
  |[[Category:不標準的唱片信息框]][[Category:應為單曲信息框的唱片信息框]]
 }}[[Category:嵌入hAudio微格式的條目]]{{#switch:{{lc:{{{image|{{{cover|{{{Cover|}}}}}}}}}}}
  |
  |???
  |nocover (zh).png = [[Category:損壞的宣傳品圖像的鏈接的頁面|唱片]]
 }}
}}<!--

-->{{#if:{{#ifeq:{{str left|{{{last_album|{{{Last album|}}}}}}|22}}|<div class="plainlist"|1|}}{{#ifeq:{{str left|{{{this_album|{{{This album|}}}}}}|22}}|<div class="plainlist"|1|}}{{#ifeq:{{str left|{{{next_album|{{{Next album|}}}}}}|22}}|<div class="plainlist"|1|}}|[[Category:在信息框的年表参数中使用无项目符号列表项的页面]]
}}<!--

-->{{#ifeq:{{{type|}}}{{{Type|}}}||[[Category:含有空白类型参数的唱片信息框]]}}<!--

-->{{#invoke:Check for unknown parameters|check|unknown={{main other|[[Category:在唱片信息框中使用未知参数的页面|_VALUE_{{PAGENAME}}]]}}|preview=页面使用了[[Template:Infobox album]]的未知参数“_VALUE_”|ignoreblank=y|type|Type|name|Name|original_name|Original_name|image|cover|Cover|border|Border|alt|Alt|caption|Caption|longtype|Longtype|artist|Artist|released|Released|format|Format|recorded|Recorded|venue|Venue|studio|Studio|genre|Genre|length|Length|language|Language|label|Label|director|Director|producer|Producer|compiler|Compiler|reviews|Reviews|chart_position|Chart position|certification|Certification|last_album|Last album|next_album|Next album|chronology|Chronology|this_album|This album|prev_title|prev_year|next_title|next_year|year|misc|Misc}}<!--

-->{{#if:{{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{{prev_title|}}}{{{last_album|}}}{{{Last album|}}}{{{prev_year|}}}{{{next_title|}}}{{{next_album|}}}{{{Next album|}}}{{{next_year|}}}{{{type|}}}{{{Type|}}}{{{name|}}}{{{Name|}}}{{{original_name|}}}{{{Original_name|}}}{{{image|}}}{{{cover|}}}{{{Cover|}}}{{{border|}}}{{{Border|}}}{{{alt|}}}{{{Alt|}}}{{{caption|}}}{{{Caption|}}}{{{longtype|}}}{{{Longtype|}}}{{{artist|}}}{{{Artist|}}}{{{released|}}}{{{Released|}}}{{{format|}}}{{{Format|}}}{{{recorded|}}}{{{Recorded|}}}{{{venue|}}}{{{Venue|}}}{{{studio|}}}{{{Studio|}}}{{{genre|}}}{{{Genre|}}}{{{length|}}}{{{Length|}}}{{{language|}}}{{{Language|}}}{{{label|}}}{{{Label|}}}{{{director|}}}{{{Director|}}}{{{producer|}}}{{{Producer|}}}{{{compiler|}}}{{{Compiler|}}}{{{reviews|}}}{{{Reviews|}}}{{{chart_position|}}}{{{Chart position|}}}{{{certification|}}}{{{Certification|}}}{{{chronology|}}}{{{Chronology|}}}{{{this_album|}}}{{{This album|}}}{{{year|}}}x|2=</?t[drh][ >]|nomatch=}}|[[Category:含有畸形表格对象的音乐信息框|A]]}}<!--

使用以下所列的參數會被加入[[Category:在音乐信息框中使用过时参数的页面|A]]
-->{{#if:{{{Name|}}}{{{Original name|}}}{{{Type|}}}{{{Cover|}}}{{{Border|}}}{{{Alt|}}}{{{Caption|}}}{{{Longtype|}}}{{{Artist|}}}{{{Released|}}}{{{Format|}}}{{{Recorded|}}}{{{Venue|}}}{{{Studio|}}}{{{Genre|}}}{{{Length|}}}{{{Language|}}}{{{Label|}}}{{{Director|}}}{{{Producer|}}}{{{Compiler|}}}{{{Reviews|}}}{{{Chart position|}}}{{{Certification|}}}{{{Chronology|}}}{{{Misc|}}}{{{last_album|}}}{{{Last album|}}}{{{this_album|}}}{{{This album|}}}{{{next_album|}}}{{{Next album|}}}|[[Category:在音乐信息框中使用过时参数的页面|A]]}}<!--

-->{{main other|{{#if:{{{length|{{{Length|}}}}}}|{{#if:{{#invoke:String|match|error_category=String模块出错的音乐信息框{{!}}A|1={{#invoke:hms|main|duration={{{length|{{{Length|}}}}}}}}|2=class="duration"|plain=true|nomatch=}}|[[Category:嵌入hAudio微格式的條目]]}}}}}}<!--

end of #invoke:Unsubst-infobox
-->}}<noinclude>
{{Documentation}}
<!-- Add categories to the /doc subpage, not here. -->
</noinclude>