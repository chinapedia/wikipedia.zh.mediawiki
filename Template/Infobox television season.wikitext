{{Infobox
 | bodyclass      = vevent
 | aboveclass     = summary

 | abovestyle     = background: {{If empty |{{{bg_colour|}}} |{{{bg_color|}}} |{{{bgcolour|}}} |{{{bgcolor|}}} |#CCCCFF }}; color: {{Greater color contrast ratio|{{If empty |{{{bg_colour|}}} |{{{bg_color|}}} |{{{bgcolour|}}} |{{{bgcolor|}}} |#CCCCFF }}|black|white}}; padding: 0.25em 1em; line-height: 1.5em;
 | above          = {{#if: {{{season_name|}}} | {{{season_name|}}} | {{#if: {{{series_name|}}} | {{{series_name|}}} | <includeonly>《{{PAGENAMEBASE}}》</includeonly> }} }}{{#if: {{{season|}}} | {{{season|}}} | {{#if: {{{series|}}} | {{{series|}}} | {{#if: {{{season_number|}}} | 第{{數字轉中文|num={{{season_number|}}}}}季 | {{#if: {{{series_number|}}} | 第{{數字轉中文|num={{{series_number|}}}}}季 }} }} }} }}

 | subheaderstyle = background: {{If empty |{{{bg_colour|}}} |{{{bg_color|}}} |{{{bgcolour|}}} |{{{bgcolor|}}} |#CCCCFF }}; color: {{Greater color contrast ratio|{{If empty |{{{bg_colour|}}} |{{{bg_color|}}} |{{{bgcolour|}}} |{{{bgcolor|}}} |#CCCCFF }}|black|white}}; padding: 0.25em 1em; line-height: 1.8em; font-weight: bold; font-size: 110%;
 | subheader      = {{#if: {{{eng_name|}}} | {{{eng_name|}}} | {{#if: {{{native_name|}}} | {{{native_name|}}} | {{{original_name|}}} }} }}

 | captionstyle   = font-size: 95%; line-height: 1.5em;
 | image          = {{#invoke:InfoboxImage|InfoboxImage|image={{{image|}}}|size={{{image_size|}}}|sizedefault=frameless|upright={{{image_upright|1}}}|alt={{{image_alt|{{{alt|}}}}}}}}
 | caption        = {{{caption|}}}

 | headerclass    = summary
 | headerstyle    = background: {{If empty |{{{bg_colour|}}} |{{{bg_color|}}} |{{{bgcolour|}}} |{{{bgcolor|}}} |#CCCCFF }}; color: {{Greater color contrast ratio|{{If empty |{{{bg_colour|}}} |{{{bg_color|}}} |{{{bgcolour|}}} |{{{bgcolor|}}} |#CCCCFF }}|black|white}}; padding: 0.25em 1em; line-height: 1.5em;

 | labelstyle     = white-space: nowrap

 | label1         = 主演
 | data1          = {{{starring|}}}

 | label4         = 国家／地区
 | data4          = {{{country|}}}

 | label5         = 故事數
 | data5          = {{{num_stories|}}}

 | label6         = 集数
 | data6          = {{{num_episodes|}}}

 | header8        = {{#if:{{{network|}}}{{{first_aired|}}}{{{released|}}}|播映}}

 | label9         = 首播频道
 | data9          = {{{network|}}}

 | label10        = 播出日期
 | data10         = {{#invoke:Infobox/dates|dates|{{{first_aired|{{{released|}}}}}}|{{{last_aired|}}}}}

 | data11         = {{{module|}}}

 | header12       = {{#if:{{{film_start|}}}{{{celebrity_winner|}}}{{{professional_winner|}}}{{{website|}}}|附加信息}}

 | label13        = 拍摄日期
 | data13         = {{#if:{{{film_start|}}}|{{{film_start|}}}－{{{film_end|}}}|}}
 | label14        = 名人赢家
 | data14         = {{{celebrity_winner|}}}
 | label15        = 专业赢家
 | data15         = {{{professional_winner|}}}
 | label16        = 网站
 | data16         = {{{website|}}}

 | header17       = {{#if:
{{{season_name_zh-cn|{{{中国大陆名称|{{{中國大陸名稱|}}}}}}}}}
{{{season_name_zh-hk|{{{港澳名称|{{{港澳名稱|}}}}}}}}}
{{{season_name_zh-my|{{{马来西亚名称|{{{馬來西亞名稱|}}}}}}}}}
{{{season_name_zh-sg|{{{新加坡名称|{{{新加坡名稱|}}}}}}}}}
{{{season_name_zh-tw|{{{台湾名称|{{{台灣名稱|{{{臺灣名稱|}}}}}}}}}}}}
 |各地節目名稱}}

 | label18        = {{nowrap|中国大陆}}
 |data18   = {{#if:{{{season_name_zh-cn|{{{中国大陆名称|{{{中國大陸名稱|}}}}}}}}}|-{<includeonly>zh;zh-hans;zh-hant{{!}}</includeonly>{{{season_name_zh-cn|{{{中国大陆名称|{{{中國大陸名稱|}}}}}}}}}}-}}
 |label19  = {{nowrap|台湾}}
 |data19   = {{#if:{{{season_name_zh-tw|{{{台湾名称|{{{台灣名稱|{{{臺灣名稱|}}}}}}}}}}}}|-{<includeonly>zh;zh-hans;zh-hant{{!}}</includeonly>{{{season_name_zh-tw|{{{台湾名称|{{{台灣名稱|{{{臺灣名稱|}}}}}}}}}}}}}-}}
 |label20  = {{nowrap|港澳}}
 |data20   = {{#if:{{{season_name_zh-hk|{{{港澳名称|{{{港澳名稱|}}}}}}}}}|-{<includeonly>zh;zh-hans;zh-hant{{!}}</includeonly>{{{season_name_zh-hk|{{{港澳名称|{{{港澳名稱|}}}}}}}}}}-}}
 |label21  = {{nowrap|新加坡}}
 |data21   ={{#if:{{{season_name_zh-sg|{{{新加坡名称|{{{新加坡名稱|}}}}}}}}}|-{<includeonly>zh;zh-hans;zh-hant{{!}}</includeonly>{{{season_name_zh-sg|{{{新加坡名称|{{{新加坡名稱|}}}}}}}}}}-}}
 |label22  = {{nowrap|马来西亚}}
 |data22   = {{#if:{{{season_name_zh-my|{{{马来西亚名称|{{{馬來西亞名稱|}}}}}}}}}|-{<includeonly>zh;zh-hans;zh-hant{{!}}</includeonly>{{{season_name_zh-my|{{{马来西亚名称|{{{馬來西亞名稱|}}}}}}}}}}-}}

 | class23        = noprint
 | header23       = {{#if:{{{prev_season|}}}{{{next_season|}}}|季度年表}}{{#if:{{{prev_series|}}}{{{next_series|}}}|系列年表}}

 | rowclass24     = noprint
 | data24         = {{#if:{{{prev_season|}}}{{{prev_series|}}}{{{next_season|}}}{{{next_series|}}} | {{align|left|{{#if:{{{prev_season|}}}{{{prev_series|}}}|←&nbsp;'''前'''<br />{{{prev_season|}}}{{{prev_series|}}}|}} }}{{align|right|{{#if:{{{next_season|}}}{{{next_series|}}}|'''后'''&nbsp;→<br />{{{next_season|}}}{{{next_series|}}}| }} }}
}}
 | belowclass     = noprint
 | below          = {{{episode_list|}}}
}}<noinclude>
{{Documentation}}
</noinclude>