{{Infobox
| bodyclass  = vcard
| bodystyle  = {{#if:{{{box_width|{{{寬度|{{{宽度|}}}}}}}}} |width:{{{box_width|{{{寬度|{{{宽度|}}}}}}}}};}}
| child      = {{lc:{{{embed|{{{嵌入}}}}}}}}

| title      = {{#ifeq:{{lc:{{{embed|{{{嵌入}}}}}}}}|yes|'''寫作生涯'''}}

| above      = 
    {{#if:{{{honorific prefix|{{{honorific_prefix|{{{前綴尊稱|{{{前缀尊称|}}}}}}}}}}}} |<span class="honorific-prefix" style="font-size:small; font-weight:normal;">{{{honorific prefix|{{{honorific_prefix|{{{前綴尊稱|{{{前缀尊称|}}}}}}}}}}}}</span><br/>}}<!--
 --><includeonly><span class="fn">{{{name|{{{姓名|{{PAGENAMEBASE}}}}}}}}</span></includeonly><!--
 -->{{#if:{{{honorific suffix|{{{honorific_suffix|{{{後綴尊稱|{{{后缀尊称|}}}}}}}}}}}} |<br/><span class="honorific-suffix" style="font-size:small; font-weight:normal;">{{{honorific suffix|{{{honorific_suffix|{{{後綴尊稱|{{{后缀尊称|}}}}}}}}}}}}</span>}}

| image      = {{#invoke:InfoboxImage|InfoboxImage |image={{{image|{{{图像|{{{圖像|}}}}}}}}} |size={{{image_size|{{{imagesize|{{{图像大小|{{{圖像大小|}}}}}}}}}}}} |sizedefault=frameless |upright={{{image_upright|1}}} |alt={{{alt|{{{圖像替代|{{{图像替代|}}}}}}}}} |suppressplaceholder=yes}}
| caption    = {{{caption|{{{imagecaption|{{{image_caption|{{{Img_capt|{{{圖片簡介|{{{图片简介|{{{圖像說明|{{{图像说明|}}}}}}}}}}}}}}}}}}}}}}}}

| abovestyle = background-color:{{#if:{{{death_date|{{{deathdate|{{{逝世|}}}}}}}}}|silver|DarkOliveGreen}}; color:{{#if:{{{death_date|{{{deathdate|{{{逝世|}}}}}}}}}|black|white}};
| labelstyle = padding-top:0.225em;line-height:1.1em;padding-right:0.65em;white-space:nowrap;
| datastyle  = line-height:1.4em;

| label1     = 原文名稱
| data1      = {{#if:{{{native_name|{{{original|{{{原文名称|{{{原文名稱|}}}}}}}}}}}} |<span class="nickname" {{#if:{{{native_name_lang|{{{語系|{{{语系|}}}}}}}}}|lang="{{{native_name_lang|{{{語系|{{{语系|}}}}}}}}}"}}>-{{{{native_name|{{{original|{{{原文名称|{{{原文名稱}}}}}}}}}}}}}-</span>}}

| label2     = 日文假名
| data2      = {{#if:{{{kana|{{{日文假名|}}}}}}|{{lang|ja|{{{kana|{{{日文假名|}}}}}}}}}}

| label3     = 羅馬拼音
| data3      = {{{romaji|{{{羅馬拼音|{{{罗马拼音|}}}}}}}}}

| class4     = additional-name
| label4     = 字
| data4      = {{{zi|{{{表字|{{{字|}}}}}}}}}

| class5     = additional-name
| label5     = 號
| data5      = {{{hao|{{{号|{{{號|}}}}}}}}}

| label6     = 出生
| data6      = {{br separated entries
                | 1={{#if:{{{birthname|{{{birth_name|{{{原名|{{{本名|}}}}}}}}}}}}|<span class="nickname">{{{birthname|{{{birth_name|{{{原名|{{{本名|}}}}}}}}}}}}</span>}}
                | 2={{#switch:{{lc:{{{birth_date|{{{birthdate|{{{出生|}}}}}}}}}}}
                   |? |?? |??? |???? |19? |19?? |18?? |17?? |u |unk |unknown = 出生日期不詳
                   | {{{birth_date|{{{birthdate|{{{出生|}}}}}}}}}
                  }}
                | 3={{#if:{{{birth_place|{{{birthplace|{{{出生地點|{{{出生地点|}}}}}}}}}}}}|<span class="birthplace">{{{birth_place|{{{birthplace|{{{出生地點|{{{出生地点|}}}}}}}}}}}}</span>}}
               }}

| label7     = 逝世
| data7      = {{br separated entries
                | 1={{#switch:{{lc:{{{death_date|{{{deathdate|{{{逝世|}}}}}}}}}}}
                   |? |?? |??? |???? |19? |19?? |18?? |17?? |u |unk |unknown = 逝世日期不詳
                   | {{{death_date|{{{deathdate|{{{逝世|}}}}}}}}}
                  }}
                | 2={{#if:{{{death_place|{{{deathplace|{{{逝世地点|{{{逝世地點|}}}}}}}}}}}}|<span class="deathplace">{{{death_place|{{{deathplace|{{{逝世地点|{{{逝世地點|}}}}}}}}}}}}</span>}}
               }}

| class8     = label
| label8     = 墓地
| data8      = {{br separated entries|{{{resting_place|{{{墓地|}}}}}} |{{{resting_place_coordinates|{{{墓地座標|{{{墓地坐标|}}}}}}}}} }}

| class9     = nickname
| label9     = 筆名
| data9      = {{{penname|{{{pseudonym|{{{筆名|{{{笔名|}}}}}}}}}}}}

| class10    = nickname
| label10    = 暱稱
| data10     = {{{nickname|{{{Alias|{{{綽號|{{{绰号|{{{暱稱|{{{昵称|}}}}}}}}}}}}}}}}}}

| class11    = {{#if:{{{resting_place|{{{墓地|}}}}}}||label}}
| label11    = 現居地
| data11     = {{{residence|{{{居处|{{{居處|{{{现居地|{{{現居地|}}}}}}}}}}}}}}}

| class12    = role
| label12    = 職業
| data12     = {{{occupation|{{{職業|{{{职业|}}}}}}}}}

| label13    = 語言
| data13     = {{{language|{{{語言|{{{语言|}}}}}}}}}

| class14    = category
| label14    = 國籍
| data14     = {{{nationality|{{{國籍|{{{国籍|}}}}}}}}}

| class15    = category
| label15    = 永久居留權
| data15     = {{{permanent residency|{{{永久居留權|{{{永久居留權|}}}}}}}}}

| class16    = category
| label16    = 民族
| data16     = {{{ethnicity|{{{種族|{{{种族|{{{民族|}}}}}}}}}}}}

| class17    = category
| label17    = 公民權
| data17     = {{{citizenship|{{{公民權|{{{公民权|}}}}}}}}}

| label18    = 教育程度
| data18     = {{{education|{{{教育程度|}}}}}}

| label19    = 母校
| data19     = {{{alma_mater|{{{母校|}}}}}}

| label20    = 創作時期
| data20     = {{{period|{{{创作时期|{{{創作時期|}}}}}}}}}

| class21    = category
| label21    = 體裁
| data21     = {{{genres|{{{genre|{{{體裁|{{{体裁|}}}}}}}}}}}}

| label22    = 主題
| data22     = {{{subjects|{{{subject|{{{主題|{{{主题|}}}}}}}}}}}}

| label23    = 文學運動
| data23     = {{{movement|{{{文学运动|{{{文學運動|}}}}}}}}}

| label24    = 代表作
| data24     = {{{notable_works|{{{notableworks|{{{notablework|{{{代表作|{{{著名作品|}}}}}}}}}}}}}}}

| class25    = note
| label25    = 獎項
| data25     = {{{awards|{{{奖项|{{{獎項|}}}}}}}}}

| label26    = 活躍年代
| data26     = {{{years active|{{{years_active|{{{yearsactive|{{{活躍年代|{{{活跃年代|}}}}}}}}}}}}}}}

| label27    = 配偶
| data27     = {{{spouses|{{{spouse|{{{配偶|}}}}}}}}}

| label28    = 伴侶
| data28     = {{{partners|{{{partner|{{{伴侣|{{{伴侶|}}}}}}}}}}}}

| label29    = 父母
| data29     = {{{parent|{{{parents|{{{父母|}}}}}}}}}

| label30    = 兒女
| data30     = {{{children|{{{子女|}}}}}}

| label31    = 親屬
| data31     = {{{relatives|{{{relations|{{{親屬|{{{亲属|}}}}}}}}}}}}

| class32    = 
| label32    = 受影響於
| data32     = {{{influences|{{{受影響於|{{{受影响于|}}}}}}}}}

| class33    = 
| label33    = 施影響於
| data33     = {{{influenced|{{{施影响于|{{{施影響於|}}}}}}}}}

| data34     = {{#if:{{{signature|{{{签名|{{{簽名|}}}}}}}}} |<hr/>}}
| label35    = 簽名
| data35     = {{#if:{{{signature|{{{签名|{{{簽名|}}}}}}}}} |[[File:{{{signature|{{{签名|{{{簽名}}}}}}}}}|frameless|upright=0.72|alt={{{signature_alt|{{{签名替代|{{{簽名替代|}}}}}}}}}]]}}

| data36     = {{{misc|{{{module|}}}}}}

| header37   = {{#if:{{{website|{{{homepage|{{{URL|{{{官方网站|{{{官方網站|}}}}}}}}}}}}}}}|官方網站}}
| data38     = {{{website|{{{homepage|{{{URL|{{{官方网站|{{{官方網站|}}}}}}}}}}}}}}}

| data39     = {{#if:{{{portaldisp|{{{顯示主題連結|{{{显示主题链接|}}}}}}}}} |<hr/>'''''{{portal-inline|文學|size=tiny}}'''''}}

}}{{#invoke:Check for unknown parameters | check | ignoreblank = y
| unknown = {{main other|[[Category:使用未知Infobox writer参数的页面|_VALUE_{{PAGENAME}}]]}}
| preview = 页面使用了[[Template:Infobox writer]]的未知参数“_VALUE_”
| Alias | Img_capt | URL | alma_mater | alt | awards | birth_date | birth_name | birth_place | birthdate | birthname | birthplace | box_width | caption | children | citizenship | death_date | death_place | deathdate | deathplace | education | embed | ethnicity | genre | genres | hao | homepage | honorific prefix | honorific suffix | honorific_prefix | honorific_suffix | image | image_caption | image_size | imagecaption | imagesize | image_upright | influenced | influences | kana | language | misc | module | movement | name | nationality | native_name | native_name_lang | nickname | notable_works | notablework | notableworks | occupation | original | parent | parents | partner | partners | penname | period | permanent residency | portaldisp | pseudonym | relations | relatives | residence | resting_place | resting_place_coordinates | romaji | signature | signature_alt | spouse | spouses | subject | subjects | website | years active | years_active | yearsactive | zi | 主題 | 主题 | 亲属 | 代表作 | 著名作品 | 伴侣 | 伴侶 | 体裁 | 公民权 | 公民權 | 出生 | 出生地点 | 出生地點 | 创作时期 | 前綴尊稱 | 前缀尊称 | 創作時期 | 原名 | 原文名称 | 原文名稱 | 受影响于 | 受影響於 | 号 | 后缀尊称 | 国籍 | 图像 | 图像大小 | 图像替代 | 图像说明 | 图片简介 | 國籍 | 永久居留權 | 圖像 | 圖像大小 | 圖像替代 | 圖像說明 | 圖片簡介 | 墓地 | 墓地坐标 | 墓地座標 | 奖项 | 姓名 | 子女 | 字 | 官方網站 | 官方网站 | 宽度 | 寬度 | 居处 | 居處 | 嵌入 | 後綴尊稱 | 教育程度 | 文学运动 | 文學運動 | 施影响于 | 施影響於 | 日文假名 | 昵称 | 显示主题链接 | 暱稱 | 本名 | 母校 | 民族 | 活跃年代 | 活躍年代 | 父母 | 獎項 | 现居地 | 現居地 | 种族 | 種族 | 笔名 | 筆名 | 签名 | 签名替代 | 簽名 | 簽名替代 | 綽號 | 绰号 | 罗马拼音 | 羅馬拼音 | 职业 | 職業 | 號 | 表字 | 親屬 | 語系 | 語言 | 语系 | 语言 | 逝世 | 逝世地点 | 逝世地點 | 配偶 | 顯示主題連結 | 體裁
}}{{main other|
{{#if:{{{pronunciation|}}} |[[Category:使用pronunciation参数的人物信息框]]
}}{{#if:{{{website|{{{homepage|{{{URL|{{{官方网站|{{{官方網站|}}}}}}}}}}}}}}}|{{#switch:{{str left|{{{website|{{{homepage|{{{URL|{{{官方网站|{{{官方網站|}}}}}}}}}}}}}}}|1}}|<=|[=|#default=[[Category:使用裸網址填寫人物傳記模板的網站欄位的條目]]}}}}
}}<noinclude>
{{Documentation}}
</noinclude>