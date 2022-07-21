{{ infobox
| abovestyle = background-color: {{#switch:{{lc:{{{type|}}} }}
| islam|islamic|伊斯蘭教|伊斯兰教                        = lightgreen
| judaism|juda|jewish|jew|猶太教|犹太教              = lightskyblue
| buddhism|buddhist|buddha|佛教             = palegoldenrod
| christian|christ|christianity|基督教|天主教        = lavender
| asian festival|asian|亞洲節日|亚洲节日                 = rosybrown
| secular|世俗                              = darkgray
| national|international|local|group|国家|国内|國際|本地|国际   = #ddccff
| historical|cultural|patriotic|ethnic|歷史|文化|历史 = lightsalmon
| pagan|其他                                = darkkhaki
| commercial|商業|商业                           = yellow
| hindu|hinduism                       = orange
| shinto|shintoism                     = red
| default                              = lightsteelblue
| transparent }}
| aboveclass = hd
| bodyclass = vevent
| above        = {{{holiday_name|<includeonly>{{PAGENAME}}</includeonly>}}}
| image        = {{#invoke:InfoboxImage|InfoboxImage|image={{{image|}}}|size={{{image_size|{{{imagesize|}}}}}}|sizedefault=frameless|upright=1.1|alt={{{alt|}}}}}                  
| caption      = {{{caption|}}}
| captionstyle = caption
| labelstyle   = white-space: nowrap;

| label1     = 正式名稱
| data1      = {{{official_name|}}}
| label2     = 别名
| data2      = {{{nickname|}}}
| label3     = 参与者
| data3      = {{{observedby|}}}
| label4     = 礼仪颜色
| data4      = {{{litcolor|}}}
| label5     = 類型
| data5      = {{{longtype|{{ucfirst:{{{type|}}}}}}}}
| class6     = summary
| label6     = 意义
| data6      = {{{significance|}}}
| label7     = 活動
| data7      = {{{celebrations|}}}
| label8     = 风俗
| data8      = {{{observances|}}}

| label9    = 日期
| data9     = {{{date|}}}

| label10    = 開始日期
| data10     = {{{begins|}}}
| label11    = 結束日期
| data11     = {{{ends|}}}

| label18    = 时长
| data18     = {{#ifeq:{{{duration|}}}|1 day||{{#if:{{{duration|}}}|{{#ifexist:Category:Holidays and observances by duration ({{{duration}}})|[[:Category:Holidays and observances by duration ({{{duration}}})|{{{duration}}}]]|{{{duration}}} }} }} }}

| label19    = 频率
| data19     = {{#if:{{{frequency|}}}|{{#ifexist:Category:Holidays and observances by frequency ({{{frequency}}})|[[:Category:Holidays and observances by frequency ({{{frequency}}})|{{{frequency}}}]]|{{{frequency}}} }} }}

| label20    = 首次时间
| data20     = {{{firsttime|}}}

| label21    = 末次时间
| data21     = {{{lasttime|}}}

| label22    = 起始
| data22     = {{{startedby|}}}

| label23     = 相關節日
| data23      = {{{relatedto|}}}

| label24     = 網站
| data24      = {{{website|}}}

}}<includeonly>{{#if:{{{color1|}}}{{{color2|}}}{{{color3|}}}|[[Category:Non-standard holiday infoboxes|{{PAGENAME}}]]}}</includeonly><noinclude>
{{documentation}}
</noinclude>