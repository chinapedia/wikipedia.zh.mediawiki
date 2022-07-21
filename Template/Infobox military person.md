{{Infobox
| child         = {{lc:{{{embed}}}}}

| bodyclass     = vcard
| bodystyle     = {{WPMILHIST Infobox style|{{#switch:{{{width_style|}}}|narrow|person|auto=main_box_raw_auto_width|wide|military|#default=main_box_raw}}}}

| title         = {{#ifeq:{{lc:{{{embed}}}}}|yes|{{if empty|{{{embed_title|}}}|'''军事生涯'''}}}}
| decat         = yes <!-- remove from template:infobox tracking categories -->

| above         = {{br separated entries
 |1={{#if:{{{honorific prefix|{{{honorific_prefix|}}}}}}|<span class="honorific-prefix" style="font-size: small; font-weight: normal">{{{honorific prefix|{{{honorific_prefix|}}}}}}</span>}}
 |2={{#if:{{{name|{{{姓名|<includeonly>{{PAGENAMEBASE}}</includeonly>}}}}}}|<span class="fn">{{{name|{{{姓名|{{PAGENAMEBASE}}}}}}}}</span>}}
 |3={{#if:{{{honorific suffix|{{{honorific_suffix|}}}}}}|<span class="honorific-suffix" style="font-size: small; font-weight: normal">{{{honorific suffix|{{{honorific_suffix|}}}}}}</span>}}
 }}
| abovestyle    = {{WPMILHIST Infobox style|header_color}}
| headerstyle   = {{WPMILHIST Infobox style|header_color}}

| image         = {{#if:{{{image|{{{image name|{{{图像|{{{圖像|}}}}}}}}}}}}|{{#ifeq:{{Str left | {{{image|{{{image name|{{{图像|{{{圖像|}}}}}}}}}}}} | 1 }}|[|[[Category:需要更新图片参数的军事人物信息框]]}}{{#invoke:InfoboxImage|InfoboxImage|image={{{image|{{{image name|{{{图像|{{{圖像|}}}}}}}}}}}}|size={{{width|{{{image_size|{{{Img_size|{{{圖片尺寸|{{{图片尺寸|{{{圖像大小|{{{图像大小|}}}}}}}}}}}}}}}}}}}}}|sizedefault=frameless|alt={{{alt|}}}|suppressplaceholder=yes}} }}
| imagestyle    = border-bottom: {{WPMILHIST Infobox style|section_border}}; line-height: 1.5em

| caption       = {{{caption|{{{imagecaption|{{{image_caption|{{{Img_capt|{{{圖片簡介|{{{图片简介|{{{圖像說明|{{{图像说明|}}}}}}}}}}}}}}}}}}}}}}}}
| captionstyle  = font-size: 95%

| labelstyle    = white-space: nowrap

| data1         = 
{{Infobox officeholder/office|color=#B0C4DE
| office = {{{job|}}}
| term = {{{period|}}}
}}
{{Infobox officeholder/office|color=#B0C4DE
| office = {{{job-1|}}}
| term = {{{period-1|}}}
}}
{{Infobox officeholder/office|color=#B0C4DE
| office = {{{job-2|}}}
| term = {{{period-2|}}}
}}
{{Infobox officeholder/office|color=#B0C4DE
| office = {{{job-3|}}}
| term = {{{period-3|}}}
}}
{{Infobox officeholder/office|color=#B0C4DE
| office = {{{job-4|}}}
| term = {{{period-4|}}}
}}
{{Infobox officeholder/office|color=#B0C4DE
| office = {{{job-5|}}}
| term = {{{period-5|}}}
}}
{{Infobox officeholder/office|color=#B0C4DE
| office = {{{job-6|}}}
| term = {{{period-6|}}}
}}

| header15      = {{#if:{{{job|}}}{{{period|}}}{{{job-1|}}}{{{period-1|}}}{{{job-2|}}}{{{period-2|}}}{{{job-3|}}}{{{period-3|}}}{{{job-4|}}}{{{period-4|}}}{{{job-5|}}}{{{period-5|}}}{{{job-6|}}}{{{period-6|}}}|{{#if:{{{native_name|{{{native name|{{{foreign_names|{{{外文名|}}}}}}}}}}}}{{{birth_name|{{{birth name|{{{birthname|{{{原名|{{{本名|}}}}}}}}}}}}}}}{{{romaji|}}}{{{english_names|{{{english_name|{{{英文名|}}}}}}}}}{{{courtesy name|{{{courtesy_name|}}}}}}{{{other_name|{{{other_names|{{{別名|{{{别名|}}}}}}}}}}}}{{{nickname|}}}{{{gender|{{{Sex|{{{sex|{{{性別|{{{性别|}}}}}}}}}}}}}}}{{{birth_date|{{{born|{{{date of birth|{{{出生日期|}}}}}}}}}}}}{{{birth_place|{{{placeofbirth|{{{place of birth|{{{出生地点|{{{出生地點|}}}}}}}}}}}}}}}{{{Native place|{{{native place|{{{籍貫|{{{籍贯|}}}}}}}}}}}}{{{death_date|{{{died|{{{date of death|{{{逝世日期|}}}}}}}}}}}}{{{death_place|{{{placeofdeath|{{{place of death|{{{逝世地點|{{{逝世地点|}}}}}}}}}}}}}}}{{{placeofburial|}}}{{{placeofburial_coordinates|}}}{{{nationality|{{{国籍|{{{國籍|}}}}}}}}}{{{residence|{{{居住地|{{{现居地|{{{現居地|}}}}}}}}}}}}{{{languages|{{{language|{{{语言|{{{語言|}}}}}}}}}}}}{{{party|{{{政党|{{{政黨|}}}}}}}}}{{{allegiance|}}}{{{alma mater|{{{alma_mater|}}}}}}{{{branch|}}}{{{kind|}}}{{{serviceyears|}}}{{{rank|{{{軍銜|{{{军衔|}}}}}}}}}{{{servicenumber|}}}{{{unit|{{{force|{{{軍隊|{{{军队|}}}}}}}}}}}}{{{commands|}}}{{{battles|}}}{{{awards|}}}{{{memorials|}}}{{{spouse|{{{配偶|}}}}}}{{{relations|{{{relatives|{{{亲属|{{{親屬|}}}}}}}}}}}}{{{otherwork|{{{laterwork|}}}}}}|个人资料}}}}

| label16       = 原文名
| data16        = {{#if: {{{native_name_lang|{{{外文|}}}}}} | {{lang|{{{native_name_lang|{{{外文|}}}}}}|{{{native_name|{{{native name|{{{foreign_names|{{{外文名|}}}}}}}}}}}} }}|{{{native_name|{{{native name|{{{foreign_names|{{{外文名|}}}}}}}}}}}}}}

| label17       = 本名
| data17        = {{{birth_name|{{{birth name|{{{birthname|{{{原名|{{{本名|}}}}}}}}}}}}}}}
| class17       = nickname

| label18       = 罗马拼音
| data18        = {{{romaji|}}}

| label19       = 英文名
| data19        = {{#if:{{{english_names|{{{english_name|{{{英文名|}}}}}}}}}|{{lang|en|{{{english_names|{{{english_name|{{{英文名|}}}}}}}}} }}}}

| label20       = 字号
| data20        = {{{courtesy name|{{{courtesy_name|}}}}}}

| label21       = 别名
| data21        = {{{other_name|{{{other_names|{{{別名|{{{别名|}}}}}}}}}}}}
| class21       = nickname

| label22       = 昵称
| data22        = {{{nickname|}}}
| class22       = nickname

| label23       = 性别
| data23        = {{{gender|{{{Sex|{{{sex|{{{性別|{{{性别|}}}}}}}}}}}}}}}

| label24       = 出生
| data24        = {{br separated entries | {{{birth_date|{{{born|{{{date of birth|{{{出生日期|}}}}}}}}}}}} | {{{birth_place|{{{placeofbirth|{{{place of birth|{{{出生地点|{{{出生地點|}}}}}}}}}}}}}}} }}

| label25       = 籍贯
| data25        = {{{Native place|{{{native place|{{{籍貫|{{{籍贯|}}}}}}}}}}}}

| label26       = 逝世
| data26        = {{br separated entries | {{{death_date|{{{died|{{{date of death|{{{逝世日期|}}}}}}}}}}}} | {{{death_place|{{{placeofdeath|{{{place of death|{{{逝世地點|{{{逝世地点|}}}}}}}}}}}}}}} }}

| label27       = {{#if:{{{placeofburial_label|}}}|{{{placeofburial_label}}}|墓地}}
| data27        = {{#if:{{{placeofburial|}}}{{{placeofburial_coordinates|}}}|<span class="label">{{{placeofburial|}}}</span> {{#if:{{{placeofburial_coordinates|}}}|({{{placeofburial_coordinates}}})}}}}

| label28       = 国籍
| data28        = {{{nationality|{{{国籍|{{{國籍|}}}}}}}}}

| label29       = 居住地
| data29        = {{{residence|{{{居住地|{{{现居地|{{{現居地|}}}}}}}}}}}}

| label30       = 语言
| data30        = {{{languages|{{{language|{{{语言|{{{語言|}}}}}}}}}}}}

| label31       = 政党
| data31        = {{{party|{{{政党|{{{政黨|}}}}}}}}}

| label32       = 效命
| data32        = {{{allegiance|}}}

| label33       = [[母校]]
| data33        = {{{alma mater|{{{alma_mater|}}}}}}

| label34       = 军种
| data34        = {{{branch|}}}

| label35       = 兵科
| data35        = {{{kind|}}}

| label36       = 服役年份
| data36        = {{{serviceyears|}}}

| label37       = 军衔
| data37        = {{{rank|{{{軍銜|{{{军衔|}}}}}}}}}

| label38       = {{Link-en|军籍号码|Service number}}<!-- Service number -->
| data38        = {{{servicenumber|}}}

| label39       = 部队
| data39        = {{{unit|{{{force|{{{軍隊|{{{军队|}}}}}}}}}}}}

| label40       = 统率
| data40        = {{{commands|}}}

| label41       = {{#if:{{{battles_label|}}}|{{{battles_label|}}}|参与战争}}
| data41        = {{{battles|}}}

| label42       = 获得勋章
| data42        = {{{awards|}}}

| label43       = 纪念建筑
| data43        = {{{memorials|}}}

| label44       = 配偶
| data44        = {{{spouse|{{{配偶|}}}}}}

| label45       = 亲属
| data45        = {{{relations|{{{relatives|{{{亲属|{{{親屬|}}}}}}}}}}}}

| label46       = 其他工作
| data46        = {{{otherwork|{{{laterwork|}}}}}}

| label47       = 签名
| data47        = {{#invoke:InfoboxImage|InfoboxImage|image={{{signature|}}}|size={{{signature_size|}}}|sizedefault=100px|alt={{{signature alt|{{{signature_alt|}}}}}}}}

| label48       = {{#if:{{{website|{{{homepage|{{{URL|}}}}}}}}}|网站}}
| data48        = {{{website|{{{homepage|{{{URL|}}}}}}}}}

<!-- 兼容 {{军人}} -->

| data49        = {{#if:{{{educate|}}}{{{学历|}}}{{{學歷|}}}|{{Collapsible list
 | title = 学历
 | title_style = text-align:center; {{WPMILHIST Infobox style|header_color}} 
 | frame_style = border: none; padding: 0;
 | 1 = {{Infobox|child=yes
  | datastyle = font-size:90%; text-align:left
  | data1 = {{{educate|{{{学历|{{{學歷|}}}}}}}}}
  }}
 }}
}}

| data50        = {{#if:{{{job2|}}}{{{目前职务|}}}{{{目前職務|}}}|{{Collapsible list
 | title = 目前职务
 | title_style = text-align:center; {{WPMILHIST Infobox style|header_color}} 
 | frame_style = border: none; padding: 0;
 | 1 = {{Infobox|child=yes
  | datastyle = font-size:90%; text-align:left
  | data1 = {{{job2|{{{目前职务|{{{目前職務|}}}}}}}}}
  }}
 }}
}}

| data51        = {{#if:{{{past|}}}{{{經歷|}}}{{{经历|}}}|{{Collapsible list
 | title = 经历
 | title_style = text-align:center; {{WPMILHIST Infobox style|header_color}} 
 | frame_style = border: none; padding: 0;
 | 1 = {{Infobox|child=yes
  | datastyle = font-size:90%; text-align:left
  | data1 = {{{past|{{{經歷|{{{经历|}}}}}}}}}
  }}
 }}
}}

| data52        = {{#if:{{{work|}}}{{{主要作品|}}}|{{Collapsible list
 | title = 代表作
 | title_style = text-align:center; {{WPMILHIST Infobox style|header_color}} 
 | frame_style = border: none; padding: 0;
 | 1 = {{Infobox|child=yes
  | datastyle = font-size:90%; text-align:left
  | data1 = {{{work|{{{主要作品|}}}}}}
  }}
 }}
}}

| data53        = {{#if:{{{award|}}}{{{勳章獎章|}}}{{{勋章奖章|}}}|{{Collapsible list
 | title = 勋章奖章
 | title_style = text-align:center; {{WPMILHIST Infobox style|header_color}} 
 | frame_style = border: none; padding: 0;
 | 1 = {{Infobox|child=yes
  | datastyle = font-size:90%; text-align:left
  | data1 = {{{award|{{{勳章獎章|{{{勋章奖章|}}}}}}}}}
  }}
 }}
}}

| data54        = {{#if:{{{rankrecord|}}}{{{軍銜記錄|}}}{{{军衔记录|}}}|{{Collapsible list
 | title = 军衔记录
 | title_style = text-align:center; {{WPMILHIST Infobox style|header_color}} 
 | frame_style = border: none; padding: 0;
 | 1 = {{Infobox|child=yes
  | datastyle = font-size:90%; text-align:left
  | data1 = {{{rankrecord|{{{軍銜記錄|{{{军衔记录|}}}}}}}}}
  }}
 }}
}}

| data55        = {{{module|}}}  

}}<includeonly>{{Wikidata image|1={{{image|}}}{{{image name|}}}{{{图像|}}}{{{圖像|}}} }}</includeonly><noinclude>{{documentation}}</noinclude>