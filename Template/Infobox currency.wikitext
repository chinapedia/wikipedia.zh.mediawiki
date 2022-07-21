{{Infobox
| bodyclass = vevent
| bodystyle = width:25em; font-size:90%;
| labelstyle = text-align:left; white-space: nowrap
| abovestyle = font-size: 115%; background: {{{顏色|{{{颜色|{{{color|lightblue}}}}}}}}};
| headerstyle = font-size: 110%;
| above = <includeonly><span class="fn"><BIG>{{{currency_name|{{{name|{{{货币名称|{{{貨幣名稱|{{{名称|{{{名稱|{{PAGENAME}}}}}}}}}}}}}}}}}}}}</BIG></span></includeonly>

| subheaderstyle = line-height: 1.2em; font-size: 100%; font-weight:bold;
| subheader = {{#if: {{{currency_name_in_local|{{{original_name|{{{当地名称|{{{當地名稱|{{{货币当地名称|{{{貨幣當地名稱|}}}}}}}}}}}}}}}}}} |{{{currency_name_in_local|{{{original_name|{{{当地名称|{{{當地名稱|{{{货币当地名称|{{{貨幣當地名稱|}}}}}}}}}}}}}}}}}} }}

| imagestyle = {{#switch:{{#if:{{{image_1|{{{圖像1|{{{图像1|}}}}}}}}}|1}}{{#if:{{{image_2|{{{圖像2|{{{图像2|}}}}}}}}}|2}}
 | 1 = {{#if:{{{image_background_1|{{{圖像背景1|{{{图像背景1|}}}}}}}}} | background: {{{image_background_1|{{{圖像背景1|{{{图像背景1|}}}}}}}}}}}
 | 2 = {{#if:{{{image_background_2|{{{圖像背景2|{{{图像背景2|}}}}}}}}} | background: {{{image_background_2|{{{圖像背景2|{{{图像背景2|}}}}}}}}}}}
 | 12 = padding: 0.3em 0.6em 0.3em 0.6em
 }}
| image = {{#switch:{{#if:{{{image_1|{{{圖像1|{{{图像1|}}}}}}}}}|1}}{{#if:{{{image_2|{{{圖像2|{{{图像2|}}}}}}}}}|2}}
 | 1 = {{#invoke:InfoboxImage|InfoboxImage|image={{{image_1|{{{圖像1|{{{图像1|}}}}}}}}}|size={{{image_width_1|{{{圖像寬度1|{{{图像宽度1|}}}}}}}}}|sizedefault=252px|alt={{{alt1|}}}}}
 | 2 = {{#invoke:InfoboxImage|InfoboxImage|image={{{image_2|{{{圖像2|{{{图像2|}}}}}}}}}|size={{{image_width_2|{{{圖像寬度2|{{{图像宽度2|}}}}}}}}}|sizedefault=252px|alt={{{alt2|}}}}}
 | 12 = <table class="center" style="display:table; margin:0 auto; background:none"><tr>
<td style="vertical-align: middle;{{#if:{{{image_background_1|{{{圖像背景1|{{{图像背景1|}}}}}}}}} | background: {{{image_background_1|{{{圖像背景1|{{{图像背景1|}}}}}}}}}}}">{{#invoke:InfoboxImage|InfoboxImage|image={{{image_1|{{{圖像1|{{{图像1|}}}}}}}}}|size={{{image_width_1|{{{圖像寬度1|{{{图像宽度1|}}}}}}}}}|sizedefault=126px|alt={{{alt1|}}}}}</td>
<td style="vertical-align: middle;{{#if:{{{image_background_2|{{{圖像背景2|{{{图像背景2|}}}}}}}}} | background: {{{image_background_2|{{{圖像寬度2|{{{图像宽度2|}}}}}}}}}}}">{{#invoke:InfoboxImage|InfoboxImage|image={{{image_2|{{{圖像2|{{{图像2|}}}}}}}}}|size{{{image_width_2|{{{圖像寬度2|{{{图像宽度2|}}}}}}}}}|sizedefault=126px|alt={{{alt2|}}}}}</td>
</tr><tr style="font-size:95%"><td>{{{image_title_1|{{{圖片簡介1|{{{图片简介1|{{{圖像說明1|{{{图像说明1|}}}}}}}}}}}}}}}</td><td>{{{image_title_2|{{{圖片簡介2|{{{图片简介2|{{{圖像說明2|{{{图像说明2|}}}}}}}}}}}}}}}</td>
</tr></table>
 }}
| caption = {{#switch:{{#if:{{{image_1|{{{圖像1|{{{图像1|}}}}}}}}}|1}}{{#if:{{{image_2|{{{圖像2|{{{图像2|}}}}}}}}}|2}}
 | 1 = {{{image_title_1|{{{圖片簡介1|{{{图片简介1|{{{圖像說明1|{{{图像说明1|}}}}}}}}}}}}}}}
 | 2 = {{{image_title_2|{{{圖片簡介2|{{{图片简介2|{{{圖像說明2|{{{图像说明2|}}}}}}}}}}}}}}}
 }}

| header1style = font-size: 110%; background: {{{顏色|{{{颜色|{{{color|lightblue}}}}}}}}};
| header1 = {{#if:{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}} |标准代码}}

| label2 = [[ISO 4217|ISO代码]]
| data2 = {{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}

| label3 = 数字代码
| data3 = {{#if:{{{iso_code_num|{{{ISO数字代码|{{{ISO數字代碼|{{{iso数字代码|{{{iso數字代碼|}}}}}}}}}}}}}}}|{{{iso_code_num|{{{ISO数字代码|{{{ISO數字代碼|{{{iso数字代码|{{{iso數字代碼|}}}}}}}}}}}}}}}}}

| label4 = ISO名称
| data4 = {{#if: {{{ISO_en|{{{iso_en|}}}}}} |{{{ISO_en|{{{iso_en|}}}}}} {{ref-info|英语|国际标准ISO 4217}} }}{{#if: {{{ISO_fr|{{{iso_fr|}}}}}} |<br />{{{ISO_fr|{{{iso_fr|}}}}}} {{ref-info|法语|国际标准ISO 4217}} }}

| label5 = [[ISO 4217|GB]]名称
| data5 = {{#if: {{{gb_name|{{{GB_name|{{{GB_名称|{{{gb_名称|{{{GB名称|{{{gb名称|}}}}}}}}}}}}}}}}}} | {{{gb_name|{{{GB_name|{{{GB_名称|{{{gb_名称|{{{GB名称|{{{gb名称|}}}}}}}}}}}}}}}}}} {{ref-info|简体中文|中华人民共和国国家标准GB 12406}} }}

| label6 = [[ISO 4217|CNS]]名称
| data6 = {{#if: {{{cns_name|{{{CNS_name|{{{CNS_名称|{{{cns_名称|{{{CNS名称|{{{cns名称|}}}}}}}}}}}}}}}}}} | {{{cns_name|{{{CNS_name|{{{CNS_名称|{{{cns_名称|{{{CNS名称|{{{cns名称|}}}}}}}}}}}}}}}}}} {{ref-info|臺灣正體|中華民國國家標準CNS 12873}} }}

<!-- 为其他中文标准预留 -->

| header10style = font-size: 110%; background: {{{顏色|{{{颜色|{{{color|lightblue}}}}}}}}};
| header10 = {{#if:{{{unofficial_users|{{{流通货币|{{{流通貨幣}}}}}}}}}{{{using_countries|{{{法定货币|{{{法定貨幣|{{{使用地|}}}}}}}}}}}}|使用地区}}

| label11 = {{#if:{{{unofficial_users|{{{流通货币|{{{流通貨幣|}}}}}}}}}|法定货币|使用地}}
| data11 = {{{using_countries|{{{法定货币|{{{法定貨幣|{{{使用地|}}}}}}}}}}}}

| label12 = {{nobold|流通货币}}
| data12 = {{{unofficial_users|{{{流通货币|{{{流通貨幣|}}}}}}}}}

| header20style = font-size: 110%; background: {{{顏色|{{{颜色|{{{color|lightblue}}}}}}}}};
| header20 = {{#if:{{{ERM_since|}}}{{{date_of_introduction|{{{始发时间|{{{始發時間|}}}}}}}}}{{{date_of_withdraw|{{{废止时间|{{{廢止時間|}}}}}}}}}{{{currency_before|{{{之前货币|{{{之前貨幣|}}}}}}}}}{{{currency_after|{{{之后货币|{{{之後貨幣|}}}}}}|}}}|发行历史}}

| label21 = 始发时间
| data21 = {{{date_of_introduction|{{{始发时间|{{{始發時間|}}}}}}}}}

| label22 = {{nobold|- 数据来源：}}
| date22 = {{#if:{{{date_of_introduction|{{{始发时间|{{{始發時間|}}}}}}}}}|{{{date_of_introduction_source|{{{始发时间来源|{{{始發時間來源|}}}}}}}}}}}

| label23 = 之前货币
| data23 = {{{currency_before|{{{之前货币|{{{之前貨幣|}}}}}}}}}

| label24 = 废止时间
| data24 = {{{date_of_withdraw|{{{废止时间|{{{廢止時間|}}}}}}}}}

| label25 = {{nobold|- 数据来源：}}
| date25 = {{#if:{{{date_of_withdraw|{{{废止时间|{{{廢止時間|}}}}}}}}}|{{{date_of_withdraw_source|{{{废止时间来源|{{{廢止時間來源|}}}}}}}}}}}

| label26 = 之后货币
| data26 = {{{currency_after|{{{之后货币|{{{之後貨幣|}}}}}}|}}}

| header30 = {{#if:{{{ERM_since|}}}|[[欧洲汇率机制]]}}

| label31 = 加入时间
| data31 = {{{ERM_since|}}}

| label32 = 退出时间
| data32 = {{#if:{{{ERM_since|}}}|{{{ERM_withdraw|}}}}}

| label33 = [[固定汇率制|固定汇率]]启用
| data33 = {{#if:{{{ERM_since|}}}|{{{ERM_fixed_rate_since|}}}}}

| label34 = 非现金被取代
| data34 = {{#if:{{{ERM_since|}}}|{{{euro_replace_non_cash|}}}}}

| label35 = 现金被取代
| data35 = {{#if:{{{ERM_since|}}}|{{{euro_replace_cash|}}}}}

| label36 = [[欧元|欧元汇率]]
| data36 = {{#if:{{{ERM_since|}}}|1 € = {{{ERM_fixed_rate|}}}}}

| label37 = {{nobold|&ensp;Band}}
| data37 = {{#if:{{{ERM_since|}}}|{{{ERM_band|}}}}}

| header40style = font-size: 110%; background: {{{顏色|{{{颜色|{{{color|lightblue}}}}}}}}};
| header40 = {{#if:{{{abbr|{{{缩写|{{{縮寫|}}}}}}}}}{{{symbol|{{{符号|{{{符號|}}}}}}}}}{{{superunit_ratio_1|}}}{{{superunit_ratio_2|}}}{{{superunit_ratio_3|}}}{{{superunit_ratio_4|}}}{{{superunit_ratio_5|}}}{{{subunit_ratio_1|}}}{{{subunit_ratio_2|}}}{{{subunit_ratio_3|}}}{{{subunit_ratio_4|}}}{{{subunit_ratio_5|}}}|货币单位}}

| label41 = {{nobold|&ensp;{{{superunit_ratio_1}}}}}
| data41 = {{#if:{{{superunit_ratio_1|}}}|{{{superunit_name_1}}}{{#if:{{{superunit_inline_note_1|}}}|<br /><small>{{{superunit_inline_note_1}}}</small>}}}}

| label42 = {{nobold|&ensp;{{{superunit_ratio_2}}}}}
| data42 = {{#if:{{{superunit_ratio_2|}}}|{{{superunit_name_2}}}{{#if:{{{superunit_inline_note_2|}}}|<br /><small>{{{superunit_inline_note_2}}}</small>}}}}

| label43 = {{nobold|&ensp;{{{superunit_ratio_3}}}}}
| data43 = {{#if:{{{superunit_ratio_3|}}}|{{{superunit_name_3}}}{{#if:{{{superunit_inline_note_3|}}}|<br /><small>{{{superunit_inline_note_3}}}</small>}}}}

| label44 = {{nobold|&ensp;{{{superunit_ratio_4}}}}}
| data44 = {{#if:{{{superunit_ratio_4|}}}|{{{superunit_name_4}}}{{#if:{{{superunit_inline_note_4|}}}|<br /><small>{{{superunit_inline_note_4}}}</small>}}}}

| label45 = {{nobold|&ensp;{{{superunit_ratio_5}}}}}
| data45 = {{#if:{{{superunit_ratio_5|}}}|{{{superunit_name_5}}}{{#if:{{{superunit_inline_note_5|}}}|<br /><small>{{{superunit_inline_note_5}}}</small>}}}}

| label46 = {{nobold|&ensp;1}}
| data46 = {{#if:{{{superunit_ratio_1|}}}{{{superunit_ratio_2|}}}{{{superunit_ratio_3|}}}{{{superunit_ratio_4|}}}{{{superunit_ratio_5|}}}{{{subunit_ratio_1|}}}{{{subunit_ratio_2|}}}{{{subunit_ratio_3|}}}{{{subunit_ratio_4|}}}{{{subunit_ratio_5|}}}|{{#ifeq: {{{subunit_ratio_1}}} | 1 | |{{#if:{{{unit|{{{单位|{{{單位|}}}}}}}}}|{{{unit|{{{单位|{{{單位|}}}}}}}}}|{{{currency_name|{{{name|{{{货币名称|{{{貨幣名稱|{{{名称|{{{名稱|}}}}}}}}}}}}}}}}}}}}}}}}

| label47 = {{nobold|&ensp;{{{subunit_ratio_1|{{{辅币单位1比率|{{{輔幣單位1比率}}}}}}}}}}}
| data47 = {{#if:{{{subunit_ratio_1|{{{辅币单位1比率|{{{輔幣單位1比率|}}}}}}}}}|{{{subunit_name_1|{{{辅币单位1|{{{輔幣單位1}}}}}}}}}{{#if:{{{subunit_inline_note_1|}}}|<br /><small>{{{subunit_inline_note_1}}}</small>}}}}

| label48 = {{nobold|&ensp;{{{subunit_ratio_2|{{{辅币单位2比率|{{{輔幣單位2比率}}}}}}}}}}}
| data48 = {{#if:{{{subunit_ratio_2|{{{辅币单位2比率|{{{輔幣單位2比率|}}}}}}}}}|{{{subunit_name_2|{{{辅币单位2|{{{輔幣單位2}}}}}}}}}{{#if:{{{subunit_inline_note_2|}}}|<br /><small>{{{subunit_inline_note_2}}}</small>}}}}

| label49 = {{nobold|&ensp;{{{subunit_ratio_3|{{{辅币单位3比率|{{{輔幣單位3比率}}}}}}}}}}}
| data49 = {{#if:{{{subunit_ratio_3|{{{辅币单位3比率|{{{輔幣單位3比率|}}}}}}}}}|{{{subunit_name_3|{{{辅币单位3|{{{輔幣單位3}}}}}}}}}{{#if:{{{subunit_inline_note_3|}}}|<br /><small>{{{subunit_inline_note_3}}}</small>}}}}

| label50 = {{nobold|&ensp;{{{subunit_ratio_4|{{{辅币单位4比率|{{{輔幣單位4比率}}}}}}}}}}}
| data50 = {{#if:{{{subunit_ratio_4|{{{辅币单位4比率|{{{輔幣單位4比率|}}}}}}}}}|{{{subunit_name_4|{{{辅币单位4|{{{輔幣單位4}}}}}}}}}{{#if:{{{subunit_inline_note_4|}}}|<br /><small>{{{subunit_inline_note_4}}}</small>}}}}

| label51 = {{nobold|&ensp;{{{subunit_ratio_5|{{{辅币单位5比率|{{{輔幣單位5比率}}}}}}}}}}}
| data51 = {{#if:{{{subunit_ratio_5|{{{辅币单位5比率|{{{輔幣單位5比率|}}}}}}}}}|{{{subunit_name_5|{{{辅币单位5|{{{輔幣單位5}}}}}}}}}{{#if:{{{subunit_inline_note_5|}}}|<br /><small>{{{subunit_inline_note_5}}}</small>}}}}

| header55 = {{#if:{{{unit|{{{单位|{{{單位}}}}}}}}}{{{subunit_name_1|{{{辅币单位1|{{{輔幣單位1}}}}}}}}}|{{#if:{{{symbol_unit|{{{单位符号|{{{單位符號|}}}}}}}}}{{{symbol_subunit_1|{{{辅币单位1符号|{{{輔幣單位1符號|}}}}}}}}}{{{nickname|{{{别称|{{{別稱|}}}}}}}}}{{{nickname_subunit_1|{{{辅币单位1别称|{{{輔幣單位1別稱|}}}}}}}}}|{{#if:{{{nickname|{{{别称|{{{別稱|}}}}}}}}}{{{nickname_subunit_1|{{{辅币单位1别称|{{{輔幣單位1別稱|}}}}}}}}}、别称}}}}}}

| label61 = [[縮寫|常用缩写]]
| data61 = {{{abbr|{{{缩写|{{{縮寫|}}}}}}}}}

| label62 = [[货币符号]]
| data62 = {{{symbol|{{{符号|{{{符號|}}}}}}}}}

| label63 = {{nobold|&ensp;{{{unit|{{{单位|{{{單位}}}}}}}}}}}
| data63 = {{#if:{{{unit|{{{单位|{{{單位}}}}}}}}}|{{{symbol_unit|{{{单位符号|{{{單位符號|}}}}}}}}}}}

| label64 = {{nobold|&ensp;{{{subunit_name_1|{{{辅币单位1|{{{輔幣單位1}}}}}}}}}}}
| data64 = {{#if:{{{subunit_name_1|{{{辅币单位1|{{{輔幣單位1|}}}}}}}}}|{{{symbol_subunit_1|{{{辅币单位1符号|{{{輔幣單位1符號|}}}}}}}}}}}

| label65 = {{nobold|&ensp;{{{subunit_name_2|{{{辅币单位2|{{{輔幣單位2}}}}}}}}}}}
| data65 = {{#if:{{{subunit_name_2|{{{辅币单位2|{{{輔幣單位2|}}}}}}}}}|{{{symbol_subunit_2|{{{辅币单位2符号|{{{輔幣單位2符號|}}}}}}}}}}}

| label66 = {{nobold|&ensp;{{{subunit_name_3|{{{辅币单位3|{{{輔幣單位3}}}}}}}}}}}
| data66 = {{#if:{{{subunit_name_3|{{{辅币单位3|{{{輔幣單位3|}}}}}}}}}|{{{symbol_subunit_3|{{{辅币单位3符号|{{{輔幣單位3符號|}}}}}}}}}}}

| label67 = {{nobold|&ensp;{{{subunit_name_4|{{{辅币单位4|{{{輔幣單位4}}}}}}}}}}}
| data67 = {{#if:{{{subunit_name_4|{{{辅币单位4|{{{輔幣單位4|}}}}}}}}}|{{{symbol_subunit_4|{{{辅币单位4符号|{{{輔幣單位4符號|}}}}}}}}}}}

| label68 = {{nobold|&ensp;{{{subunit_name_5|{{{辅币单位5|{{{輔幣單位5}}}}}}}}}}}
| data68 = {{#if:{{{subunit_name_5|{{{辅币单位5|{{{輔幣單位5|}}}}}}}}}|{{{symbol_subunit_5|{{{辅币单位5符号|{{{輔幣單位5符號|}}}}}}}}}}}

| label69 = 别称
| data69 = {{{nickname|{{{别称|{{{別稱|}}}}}}}}}

| label70 = {{nobold|&ensp;{{{subunit_name_1|{{{辅币单位1|{{{輔幣單位1}}}}}}}}}}}
| data70 = {{#if:{{{subunit_name_1|{{{辅币单位1|{{{輔幣單位1|}}}}}}}}}|{{{nickname_subunit_1|{{{辅币单位1别称|{{{輔幣單位1別稱|}}}}}}}}}}}

| label71 = {{nobold|&ensp;{{{subunit_name_2|{{{辅币单位2|{{{輔幣單位2}}}}}}}}}}}
| data71 = {{#if:{{{subunit_name_2|{{{辅币单位2|{{{輔幣單位2|}}}}}}}}}|{{{nickname_subunit_2|{{{辅币单位2别称|{{{輔幣單位2別稱|}}}}}}}}}}}

| label72 = {{nobold|&ensp;{{{subunit_name_3|{{{辅币单位3|{{{輔幣單位3}}}}}}}}}}}
| data72 = {{#if:{{{subunit_name_3|{{{辅币单位3|{{{輔幣單位3|}}}}}}}}}|{{{nickname_subunit_3|{{{辅币单位3别称|{{{輔幣單位3別稱|}}}}}}}}}}}

| label73 = {{nobold|&ensp;{{{subunit_name_4|{{{辅币单位4|{{{輔幣單位4}}}}}}}}}}}
| data73 = {{#if:{{{subunit_name_4|{{{辅币单位4|{{{輔幣單位4|}}}}}}}}}|{{{nickname_subunit_4|{{{辅币单位4别称|{{{輔幣單位4別稱|}}}}}}}}}}}

| label74 = {{nobold|&ensp;{{{subunit_name_5|{{{辅币单位5|{{{輔幣單位5}}}}}}}}}}}
| data74 = {{#if:{{{subunit_name_5|{{{辅币单位5|{{{輔幣單位5|}}}}}}}}}|{{{nickname_subunit_5|{{{辅币单位5别称|{{{輔幣單位5別稱|}}}}}}}}}}}

| header80style = font-size: 110%; background: {{{顏色|{{{颜色|{{{color|lightblue}}}}}}}}};
| header80 = {{#if:{{{used_coins|{{{硬幣|{{{硬币|}}}}}}}}}{{{frequently_used_coins|{{{常用硬幣|{{{常用硬币|}}}}}}}}}{{{rarely_used_coins|{{{少用硬幣|{{{少用硬币|}}}}}}}}}{{{used_banknotes|{{{纸币|{{{紙幣|}}}}}}}}}{{{frequently_used_banknotes|{{{常用紙幣|{{{常用纸币|}}}}}}}}}{{{rarely_used_banknotes|{{{少用紙幣|{{{少用纸币|}}}}}}}}}|发行面额}}

| label81 = {{#if:{{{coin_article|}}}|[[{{{coin_article}}}|硬币]]|硬币}}
| data81 = {{{used_coins|{{{硬幣|{{{硬币|}}}}}}}}}{{#if:{{{frequently_used_coins|{{{常用硬幣|{{{常用硬币|}}}}}}}}}{{{rarely_used_coins|{{{少用硬幣|{{{少用硬币|}}}}}}}}}|<nowiki />}}

| label82 = {{nobold|- 常用：}}
| data82 = {{{frequently_used_coins|{{{常用硬幣|{{{常用硬币|}}}}}}}}}

| label83 = {{nobold|- 少用：}}
| data83 = {{{rarely_used_coins|{{{少用硬幣|{{{少用硬币|}}}}}}}}}

| label84 = {{#if:{{{banknote_article|}}}|[[{{{banknote_article}}}|纸币]]|纸币}}
| data84 = {{{used_banknotes|{{{纸币|{{{紙幣|}}}}}}}}}{{#if:{{{frequently_used_banknotes|{{{常用紙幣|{{{常用纸币|}}}}}}}}}{{{rarely_used_banknotes|{{{少用紙幣|{{{少用纸币|}}}}}}}}}|<nowiki />}}

| label85 = {{nobold|- 常用：}}
| data85 = {{{frequently_used_banknotes|{{{常用紙幣|{{{常用纸币|}}}}}}}}}

| label86 = {{nobold|- 少用：}}
| data86 = {{{rarely_used_banknotes|{{{少用紙幣|{{{少用纸币|}}}}}}}}}

| header90style = font-size: 110%; background: {{{顏色|{{{颜色|{{{color|lightblue}}}}}}}}};
| header90 = {{#if:{{{issuing_authority|{{{发行机构|{{{發行機構|}}}}}}}}}{{{printer|}}}{{{mint|}}}|发行制造}}

| label91 = {{nowrap|{{#if:{{{issuing_authority_title|{{{发行机构称谓|{{{發行機構稱謂|}}}}}}}}}|{{{issuing_authority_title|{{{发行机构称谓|{{{發行機構稱謂|}}}}}}}}}|[[中央银行]]}}}}
| data91 = {{{issuing_authority|{{{发行机构|{{{發行機構|}}}}}}}}}

| label92 = {{nobold|- 网址：}}
| data92 = {{#if:{{{issuing_authority|}}}|{{{issuing_authority_website|{{{发行机构网址|{{{發行機構網址|}}}}}}}}}}}

| label93 = {{#if:|{{{printer|}}}|[[造币厂|印钞机构]]}}
| data93 = {{{printer|}}}

| label94 = {{nobold|- 网址：}}
| data94 = {{#if:{{{printer_website|}}}|{{{printer_website|}}}}}

| label95 = {{#if:|{{{mint|}}}|[[造币厂|造币机构]]}}
| data95 = {{{mint|}}}

| label96 = {{nobold|- 网址：}}
| data96 = {{#if:|{{{mint_website|}}}|{{{mint_website|}}}}}

| header100style = font-size: 110%; background: {{{顏色|{{{颜色|{{{color|lightblue}}}}}}}}};
| header100 = {{#if:{{{inflation_rate|{{{通胀率|{{{通脹率|}}}}}}}}}{{{inflation_title|}}}{{{pegged_with|}}}{{{basket_by|}}}{{{pegged_with|}}}{{{pegged_by|}}}|货币估值}}

| label101 = {{#if:{{{inflation_title|}}}|{{{inflation_title}}}|[[通货膨胀|通胀率]]}}
| data101 = {{{inflation_rate|{{{通胀率|{{{通脹率|}}}}}}}}}

| label102 = {{nobold|- 数据来源：}}
| data102 = {{#if:{{{inflation_rate|{{{通胀率|{{{通脹率|}}}}}}}}}|{{{inflation_source_date|{{{通胀率来源|{{{通脹率來源|}}}}}}}}}}}

| label103 = {{nobold|- 测度指数：}}
| data103 = {{#if:{{{inflation_rate|{{{通胀率|{{{通脹率|}}}}}}}}}|{{{inflation_method|}}}}}

| label105 = [[固定汇率制|-{zh-cn:汇率挂靠; zh-hk:匯率掛鈎}-]]
| data105 = {{{pegged_with|}}}

| label106 = [[固定汇率制|-{zh-cn:汇率被挂靠; zh-hk:匯率被掛鈎}-]]
| data106 = {{{pegged_by|}}}

| label107 = [[一篮子货币|汇率参考]]
| data107 = {{{basket_with|}}}

| label108 = [[一篮子货币|汇率被参考]]
| data108 = {{{basket_by|}}}

| header110style = font-size: 110%; background: {{{顏色|{{{颜色|{{{color|lightblue}}}}}}}}};
| header110 = {{#if:{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|Date}}|即期汇率}}

| label111 = <div style="text-align:right;">{{#if:{{{外币量级1|}}}|{{{外币量级1|}}}|1}} {{#if:{{{外币代码1|}}}|{{#if:{{{外币名称1|}}}|[[{{{外币名称1|}}}|{{{外币代码1|}}}]]|{{{外币代码1|}}}}}|[[美元|USD]]}}=</div>
| data111 = {{#if:{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|Date}}|{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|{{#if:{{{外币代码1|}}}|{{{外币代码1|}}}|USD}}|{{#if:{{{外币量级1|}}}|{{{外币量级1|}}}|1}}}} {{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}}}

| label112 = <div style="text-align:right;">{{#if:{{{外币量级2|}}}|{{{外币量级2|}}}|1}} {{#if:{{{外币代码2|}}}|{{#if:{{{外币名称2|}}}|[[{{{外币名称2|}}}|{{{外币代码2|}}}]]|{{{外币代码2|}}}}}|[[欧元|EUR]]}}=</div>
| data112 = {{#if:{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|Date}}|{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|{{#if:{{{外币代码2|}}}|{{{外币代码2|}}}|EUR}}|{{#if:{{{外币量级2|}}}|{{{外币量级2|}}}|1}}}} {{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}}}

| label113 = <div style="text-align:right;">{{#if:{{{外币量级3|}}}|{{{外币量级3|}}}|1}} {{#if:{{{外币代码3|}}}|{{#if:{{{外币名称3|}}}|[[{{{外币名称3|}}}|{{{外币代码3|}}}]]|{{{外币代码3|}}}}}|[[英镑|GBP]]}}=</div>
| data113 = {{#if:{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|Date}}|{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|{{#if:{{{外币代码3|}}}|{{{外币代码3|}}}|GBP}}|{{#if:{{{外币量级3|}}}|{{{外币量级3|}}}|1}}}} {{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}}}

| label114 = <div style="text-align:right;">{{#if:{{{外币量级4|}}}|{{{外币量级4|}}}|1}} {{#if:{{{外币代码4|}}}|{{#if:{{{外币名称4|}}}|[[{{{外币名称4|}}}|{{{外币代码4|}}}]]|{{{外币代码4|}}}}}|[[人民币|CNY]]}}=</div>
| data114 = {{#if:{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|Date}}|{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|{{#if:{{{外币代码4|}}}|{{{外币代码4|}}}|CNY}}|{{#if:{{{外币量级4|}}}|{{{外币量级4|}}}|1}}}} {{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}}}

| label115 = <div style="text-align:right;">{{#if:{{{外币量级5|}}}|{{{外币量级5|}}}|1}} {{#if:{{{外币代码5|}}}|{{#if:{{{外币名称5|}}}|[[{{{外币名称5|}}}|{{{外币代码5|}}}]]|{{{外币代码5|}}}}}|[[日圓|JPY]]}}=</div>
| data115 = {{#if:{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|Date}}|{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|{{#if:{{{外币代码5|}}}|{{{外币代码5|}}}|JPY}}|{{#if:{{{外币量级5|}}}|{{{外币量级5|}}}|1}}}} {{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}}}

| data116 = {{#if:{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|Date}}|{{Small|{{Center|（{{汇率|{{{iso_code|{{{ISO代码|{{{ISO代碼|{{{iso代码|{{{iso代碼|}}}}}}}}}}}}}}}|Date}}）}}}}}}

| below = {{#if:{{{date_of_withdraw|}}}{{{废止时间|}}}{{{廢止時間|}}}{{{euro_replace_non_cash|}}}{{{euro_replace_cash|}}}{{{obsolete_notice|}}}|<div style="font-size:85%; text-align:center;">此信息框显示的是该货币被废止前的最后状态。</div>}}

| data151 = {{#if:{{{footnotes|}}}|<div style="font-size:85%; text-align:left;">{{#if:1|{{{footnotes}}}}}</div>}}
}}{{#if:{{{issuing_authority_website|}}}|{{#ifeq:{{str left|{{{issuing_authority_website}}}|1}}|<||[[Category:带无链接网址的货币信息框]]
}}}}{{#if:{{{printer_website|}}}|{{#ifeq:{{str left|{{{printer_website}}}|1}}|<||[[Category:带无链接网址的货币信息框]]
}}}}{{#if:{{{mint_website|}}}|{{#ifeq:{{str left|{{{mint_website}}}|1}}|<||[[Category:带无链接网址的货币信息框]]
}}}}<noinclude>
{{documentation}}
<!-- 請將跨語言連結與分類加入 /doc 子頁面，而不是加在這裡。 -->
</noinclude>