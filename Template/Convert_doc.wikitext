<includeonly>{{lua|Module:Convert}}{{High-use|52176}}{{esoteric}}</includeonly><noinclude>{{template doc page viewed directly}}</noinclude>
<!-- 在本行下編輯模板說明 -->

本模板提供一般數學及科學单位轉換功能。请注意，根据[[WP:MOS#时间、数字、度量衡|格式手册]]，度量衡一般应采用国际单位制，因此建议'''仅在必要时使用本模板'''。

=== 用法 ===
这个模板主要显示计量单位数值，并可将一数据自动转换成两个不同计量单位，可实现功能有数值四舍五入，计量单位的维基内部链接、计量单位简写、包括各种分隔符：括号“（&nbsp;）”，“or”，连字符，逗号，“to”或破折号。可以帮助用户生成正确的转换，从一个计量单位转换成另一个测量，尤其是对于更复杂的单位。转换遵循[[WP:MOSNUM|格式手册]]。模板生成的内容与普通文本没有什么不同。

样式包括: 距离“{{convert|32|m|ft}}”和“{{convert|32|m|ft|disp=or}}”；温度“{{convert|18|°C|°F}}”；质量 “{{convert|55.0|kg|lb|abbr=on}}”及“{{convert|65|to|80|kg|lb|abbr=on}}”。

{|
|- bgcolor="#FAFEFF" valign=top
| width="80px"|选项包括：||[[Template:Convert/doc#lk_in|<code>lk=in</code>]], [[Template:Convert/doc#abbr_on|<code>abbr=on</code>]], [[Template:Convert/doc#abbr_on|<code>abbr=off</code>]], [[Template:Convert/doc#disp_or|<code>disp=x</code>]], [[Template:Convert/doc#disp_table|<code>disp=table</code>]] 和 [[Template:Convert/doc#sortable_on|<code>sortable=on</code>]] （下面详细解释）。默认情况下，输出[[Template:Convert/doc#Rounding|四舍五入]]到匹配的输入精度；备选方案包括：<code>sigfig=3</code>或使用最终参数，如“<code>&#124;1</code>”显示小数点后一位或“<code>&#124;-2</code>”，显示百位整数等。
|}

====模板數據====
{{TemplateDataHeader}}

<templatedata>{
"description": "換算數學單位到另一個單位",
"params": {
"1": {
  "label": "數值",
  "description": "被換算的數值",
  "type": "number"
},
"2": {
  "label": "原單位",
  "description": "被換算的（輸入）單位",
  "type": "string/line"
},
"3": {
  "label": "目標單位",
  "description": "換算成哪一種（輸出）單位",
  "type": "string/line"
},
"4": {
  "label": "小數位或後綴",
  "description": "小數點後的精準度，如果輸入負數就會變成顯示10的次方。（重要！不提供舊版的「precision」命名參數重定向！）",
  "type": "number"
},
"lk": {
  "label": "單位條目鏈接",
  "description": "「on」對全部單位提供條目鏈接、 「in」只鏈接原輸入單位、 「out」只鏈接輸出單位、「off」不提供鏈接。（重要！新版不提供「link」重定向參數！所有「link」參數必須移除或改成「lk」!）",
  "default": "off",
  "type": "string/line"
},
"abbr": {
  "label": "略稱",
  "description": "「on」將單位變成略稱，大部分為拉丁字母略稱、 「off」全部單位顯示全名，大部分已經翻譯為中文、「in」只縮略輸入單位、「out」只縮略輸出單位、「values」隱藏所有單位。",
  "default": "off",
  "type": "string/line"
},
"disp": {
  "label": "顯示方式",
  "description": "「b」以圓括號包圍輸出顯示、「x」使用方括號、「or」以「或」字取代括號鏈接輸入和輸出顯示、「table」或「tablecen」以維基列表代碼分隔和令每一格靠右或置中、「output only」只顯示輸出結果、「output number only」只顯示輸出數字不提供單位、「flip」調換輸入輸出位置、「unit」只顯示輸入單位名、輸入數字的場合下視作「小數位或後綴」參數。",
  "default": "b",
  "type": "string/line"
},
"sigfig": {
  "label": "精準度",
  "description": "輸入數字改變多少位化整為零。",
  "type": "number"
},
"sortable": {
  "label": "排序開關",
  "description": "「on」 會在顯示結果前生成一個隱藏的數據方便在使用了sortable class的列表中排序。",
  "type": "string/line"
},
"sp": {
  "label": "美制",
  "description": "「us」顯示US，此為英文版痕跡參數，中文版不要使用。",
  "type": "string/line"
},
"adj": {
  "label": "形容詞句式",
  "description": "英文版痕跡參數，「on」顯示形容詞句式（連字符接著單數格單位名），「mid」增加一個新的string參數顯示在輸入單位後，使用「mid」和新string參數的場合下必須提供輸出單位，就算是使用預設輸出單位。",
  "type": "string/line"
}
}}</templatedata>

====单个值====
 <tt><nowiki>{{</nowiki>convert|值|输入单位|输出单位|四舍五入位数<nowiki>|...}}</nowiki></tt>

'''范围是两个值，或三个值''' （见下面清单“范围”选项）:
<tt>
 {&#123;convert|值1|范围|值2 |输入单位|输出单位|四舍五入位数|...}}
 {&#123;convert|值1|范围|值2|修辞|值3|输入单位|输出单位|四舍五入位数|...}}</tt>

* 数值必须是标准格式（无分隔符）。模板的输出值将被格式化，并在适当情况下显示负号。要指定用逗号，改变格式<nowiki>{{formatnum:9,000,500|R}}</nowiki>（变成 9000500）。
* 可选参数，在下面的例子中，单位缩写（abbr=on），或单词美国拼法（sp=us 例如''meter''，中文无效），或断字（adj=on）等。
* 此模板进行多层次的调用，分析起来很麻烦。可以借助[[Special:ExpandTemplates|展开模板]]查看工具分析。
* 模板的[[量纲分析]]能力有限。因此需要由编者确认输入和输出单位的配对及兼容。不要做如下使用：尝试'''桶'''到'''吨'''的转换（参见 {{tl|bbl to t}}）。也请注意有类似名称的单位：代码<code>oz</code>盎司质量单位，如果要标识液体盎司就不要使用这个符号。代码<code>lb</code>代表质量镑，如果要使用力学单位镑力使用<code>lbf</code>符号。
* 试图转换一个单元本身，例如公里转公里，将导致模板陷入死循环。
* 各单位范围内的功能没有充分验证，需要不断的试验。
* 这个文档页面与模板功能不匹配。有关详细信息，请参见讨论页和其档案。

===举例说明===
====单个值====
{| class="wikitable"
! 输入 !! 显示效果
|-
|<nowiki>{{convert|3.21|kg|lb}}</nowiki>||{{convert|3.21|kg|lb}}
|-
|<nowiki>{{convert|3.21|kg|lb|0}}</nowiki>||{{convert|3.21|kg|lb|0}}
|-
|<nowiki>{{convert|10|kg|lb|disp=or}}</nowiki>||{{convert|10|kg|lb|disp=or}}
|-
|<nowiki>{{convert|6|ft|5|in|m}}</nowiki>||{{convert|6|ft|5|in|m}}
<!--This is currently broken, see talk page
|-
|<nowiki>{{convert|2|m|ftin}}</nowiki>||{{convert|2|m|ftin}}
-->
|-
|<nowiki>{{convert|10|mi}}</nowiki>||{{convert|10|mi}}
|-
|<nowiki>{{convert|100|mpgus}}</nowiki>||{{convert|100|mpgus}}
|-
|<nowiki>{{convert|120|km/h}}</nowiki>||{{convert|120|km/h}}
|-
|<nowiki>{{convert|18|°C|°F}}</nowiki>||{{convert|18|°C|°F}}
|-
| <nowiki>{{convert|1250|sqft|m2|lk=in|sigfig=2}}</nowiki> ||{{convert|1250|sqft|m2|lk=in|sigfig=2}}<br/>注“lk=in”只输入单位有链接。这个例子是仅用于说明，常见的度量单位不应有链接。参见：[[Wikipedia:格式手册 (链接)|Wp:格式手册 (链接)]]。
|- 
|<nowiki>{{convert|20.5|m3|cuyd|lk=out|abbr=on}}</nowiki>||{{convert|20.5|m3|cuyd|lk=out|abbr=on}}<br/>注“lk=in”只输出单位有链接, [[cu yd]].
|-
|<nowiki>{{convert|641|acre|ha sqmi|lk=on}}</nowiki>||{{convert|641|acre|ha sqmi|lk=on}}<br/>注“lk=on”全部单位有链接。指引，共用单位没有链接，参见： [[Wikipedia:格式手册 (链接)|Wp:格式手册 (链接)]]。
|-
|<nowiki>{{convert|641|acre|ha sqmi|2|lk=on}}</nowiki>||{{convert|641|acre|ha sqmi|2|lk=on}}<br/>虽然640英亩等于1平方英里；四舍五入到小数点后两位641英亩等于1.00平方公里。
|}

====两个值====
:''注：不是所有单位都能使用此效果''
{| class="wikitable"
! 输入 !! 显示效果
|-
|<nowiki>{{convert|60|and|170|kg|lb}}</nowiki>||{{convert|60|and|170|kg|lb}}
|-
|<nowiki>{{convert|60|to|170|kg|lb}}</nowiki>||{{convert|60|to|170|kg|lb}}
|-
|<nowiki>{{convert|60|to(-)|170|kg|lb}}</nowiki>||{{convert|60|to(-)|170|kg|lb}}
|-
|<nowiki>{{convert|60|-|170|kg|lb}}</nowiki>||{{convert|60|-|170|kg|lb}}
|-
|<nowiki>{{convert|41|to|50|F|C}}</nowiki>||{{convert|41|to|50|F|C}}
|-
|<nowiki>{{convert|41|-|50|F|K}}</nowiki>||{{convert|41|-|50|F|K}}
|-
|<nowiki>{{convert|60|x|120|m|ft}}</nowiki>||{{convert|60|x|120|m|ft}}
|-
|<nowiki>{{convert|60|+/-|10|m|ft}}</nowiki>||{{convert|60|+/-|10|m|ft}}
|-
|<nowiki>{{convert|19|to|27|L|USgal}}</nowiki>||{{convert|19|to|27|L|USgal}}
|-
|<nowiki>{{convert|5|to|7|L|USgal|abbr=mos}}</nowiki>||{{convert|5|to|7|L|USgal|abbr=mos}}
|-
|<nowiki>{{convert|4|-|9|L|USgal|abbr=off}}</nowiki>||{{convert|4|-|9|L|USgal|abbr=off}}
|-
|}<!--NOTE: rows require "nowiki", using &#123;{ disappears. -->

目前数值在以下范围的不提供转换：
*部分英制单位和美国加仑为基础的单位。
*除英里每加仑“mpg”和升每百公里“L100km”，以外的其他燃料消费的单位。
*大型单位（e3，e6，e9）.
*由于转换太复杂，组合为基础的单位(ft&in, st&lb, lb&oz)（英/尺，吨/磅，磅/盎司）。

====三个值====
:''注：不是所有单位都能使用此效果''
{| class="wikitable"
! 输入 !! 显示效果
|-
|<nowiki>{{convert|2|x|4|x|6|m|ft}}</nowiki>||{{convert|2|x|4|x|6|m|ft}}
|-
|<nowiki>{{convert|2|x|4|x|6|m|ft|abbr=on}}</nowiki>||{{convert|2|x|4|x|6|m|ft|abbr=on}}
|-
|<nowiki>{{convert|60|-|70|-|80|kg|lb}}</nowiki>||{{convert|60|-|70|-|80|kg|lb}}
|-
|<nowiki>{{convert|60|-|70|-|80|kg|lb|abbr=on}}</nowiki>||{{convert|60|-|70|-|80|kg|lb|abbr=on}}
|-
|<nowiki>{{convert|60|to|80|or|85|m|ft}}</nowiki>||{{convert|60|to|80|or|85|m|ft}}
|-
|<nowiki>{{convert|60|to|80|or|85|m|ft|abbr=on}}</nowiki>||{{convert|60|to|80|or|85|m|ft|abbr=on}}
|-
|<nowiki>{{convert|41|to|50|to|60|F|C}}</nowiki>||{{convert|41|to|50|to|60|F|C}}
|-
|<nowiki>{{convert|41|to|50|to|60|F|C|abbr=on}}</nowiki>||{{convert|41|to|50|to|60|F|C|abbr=on}}
|}

===参数===
{| class="wikitable"
|-
! colspan="2" | 参数
|-
| {{anchor|lk_in}}单位添加 [[Wikipedia:格式手册_(链接)|链接]] 
| 附上 <code><nowiki>|lk=on</nowiki></code> 所有单位开 (默认: <tt>lk=off</tt>)<br /> 附上 <code><nowiki>|lk=in</nowiki></code> 输入单位有链接<br /> 附上 <code><nowiki>|lk=out</nowiki></code> 输出单位有链接<br />（[[Wikipedia:格式手册_(链接)|格式手册]]建议常见的测量单位不应该链接）
|-
| 单位英文符号, 或不 
| {{anchor|abbr_on}}附上 <code><nowiki>|abbr=on</nowiki></code> 显示单位符号<br /> 附上 <code><nowiki>|abbr=off</nowiki></code> 显示完所有单位整的名称，显示中文名称（中文模板默认设置）<br /> 附上 <code><nowiki>|abbr=in</nowiki></code> 缩写输入单位<br /> 附上 <code><nowiki>|abbr=out</nowiki></code> 缩写输出单位<br /> 附上 <code><nowiki>|abbr=values</nowiki></code> 不显示单位只显示数字。所以 <nowiki>{{convert|6|mi|abbr=values}}</nowiki> 显示: {{convert|6|mi|abbr=values}}。
|-
| {{anchor|disp_or}}改变“（）”显示其他分隔 
| 附上 <code>&#124;disp=comma</code> 显示逗号, 不显示方括号/圆括号<br /> 附上 <code>&#124;disp=or</code> 单位之间添加“或”（or）。<br /> 默认值是：disp=b 显示方括号/圆括号。
|-
| 改变“（）”自定义分隔符
| 附上 <code>&#124;disp=x&#124; (begin &#124; end)</code> 显示 "xx (begin yy end)" 参见：例1<br /> 附上 <code>&#124;disp=x&#124;;</code> 显示 "xx; yy" 参见：例2<br /> 附上 <code>&#124;disp=x&#124; (same as &#124;)</code> 显示 "xx (same as yy)". 参见：例3<br />例1: {{nowrap|<nowiki>{&#123;convert|9|km|mi|disp=x| [|]}}</nowiki>}}  显示为：{{convert|9|km|mi|disp=x| [|]}} （注意前<nowiki>[|</nowiki>）空格。<br />例2: {{nowrap|<nowiki>{&#123;convert|9|km|mi|disp=x|；}}</nowiki>}}  显示为：{{convert|9|km|mi|disp=x|：}}<br />例3: {{nowrap|<nowiki>{&#123;convert|10|km|mi|disp=x|（大约|）}}</nowiki>}}  显示为：{{convert|10|km|mi|disp=x| (大约|)}} （使用代码时注意空格）。
|-
| 仅显示输出
| 附上 <code>&#124;disp=output only</code> 只显示结果的数量及单位<br /> 附上 <code>&#124;disp=output number only</code> 只显示数量<br />注：当使用“disp=output only”，单位名义仍然显示中文abbr=off或有链接lk=on。
|-
| 前后顺序颠倒显示数据
| 附上 <code>&#124;disp=flip</code> 顺序颠倒同时显示单位单元。<br />如, <nowiki>{{convert|6|km|disp=flip}}</nowiki> 显示“{{convert|6|km|disp=flip}}”。<br />为得到符号“mi”使用abbr=in，缩写输入单元（左侧单位）。
|-
| 只显示单位名称 
| 附上 <code>&#124;disp=unit</code> 显示单位名称为符号<br />输入不为1的数值显示完整的中文单位名。 <nowiki>{{convert|2|cuyd|disp=unit}}</nowiki>显示“{{convert|2|cuyd|disp=unit}}”。
|-
| {{anchor|disp_table}}显示为表格代码
| 附上 <tt>&#124;disp=table</tt> (or <tt>&#124;disp=tablecen</tt>)注：表中的使用，模板必须开始一个新行。 只有数字将显示，除非设置<code><nowiki>|abbr=on</nowiki></code>，<code><nowiki>|lk=on</nowiki></code>，<code><nowiki>|lk=in</nowiki></code>或<code><nowiki>|lk=out</nowiki></code>。例：[[:en:Phnom_Penh#Highways|here]]
|-
| 四舍五入到[[有效数字]]指定的数 
| 附上 <code><nowiki>|sigfig={大于零的整数}</nowiki></code>。在摄氏或华氏温度的情况下，这是指以绝对零度的温度差异。例如，在室温下显著两个数字意味着四舍五入到几十度。
|-
| 数值修约到5 
| 附上 <tt>&#124;disp=5</tt> 输出值将被数值修约到5的倍数。不能使用其他选项。（输出数值的个位数，二舍八入，三七做五）
|-
|让''Convert''决定默认输出单位|| 跳过精确参数 (第三和第四个参数不输入) 例如：<code><nowiki>{{convert|100|km|mi}}</nowiki></code>显示{{convert|100|km|mi}}和<code><nowiki>{{convert|100|km}}</nowiki></code>显示{{convert|100|km}}。
|-
|显示输入值分数
| <nowiki>{{convert|3/8|in|mm|3|abbr=on}}</nowiki>显示{{convert|3/8|in|mm|3|abbr=on}}或<nowiki>{{convert|11+1/4|in|cm|2|abbr=on}}</nowiki>显示{{convert|11+1/4|in|cm|2|abbr=on}}
为负数金额，使用两个减号（连字符）：-11-1/4。
|-
|{{anchor|sortable_on}}生成一个[[:en:Help:Sorting#Sorting with hidden sortkey|隐藏的排序键]]用于[[:en:Help:Sorting|表格排序]]
| 附上 <code><nowiki>|sortable=on</nowiki></code> 生成一个隐藏的排序键，这样的排序表将正确排序。使用{{tp|ntsh}}产生的第一个数值的排序键。它忽略任何附加值，即，如果使用<code>6|ft|2|in</code>的值，它只会使用排序键6。这将导致数值排序中的数字顺序，即：5，10，15，而不是10，15，5。
|}

====仍在建设中的参数====
{| class="wikitable"
|-
! colspan="2" | 仍在建设中的参数,可能无法在所有情况下正常工作
|-
| disp=5<ref name=temp group=note>这是有限的，暂时的选项，直到替代功能全部实施.</ref> || 输出值将被数值修约到5的倍数。不能使用其他选项。
|-
|disp=tablecen<ref name=temp group=note/>||除了显示列和数值，与disp=table类似
|-
|disp=comma<ref name=temp group=note/>||首先看重的是括号内的内容，这两个值将用逗号分隔。
|-
|abbr=in||只缩写只输出单位。
|-
|abbr=out||只缩写只输出单位。
|-
|abbr=comma<ref name=temp group=note/>||"缩写"(删除)逗号.
|-
|abbr=mos||在一定范围, 输入单位缩写重复两次。不要混淆与[[Wikipedia:格式手册_(日期和数字)|数字格式手册]].
|-
|disp=br||这强制换行符分开输入和输出单位。在横向宽度受限空间表格有效果。
|-
|disp=sqbr||输出显示[[括号]]“[&nbsp;]” 而不是括号“(&nbsp;)”。 例如：55公里[89公里]。此选项可以使用直接引号，显示在编辑括号参数。见：代入<code>&#124;disp=x&#124;[&#124;]</code>，上面为显示括号“[ ]”的另一种方式。
|}
{{reflist|group=note}}

===数值修约（四舍五入）===
''Convert'' 支持四种类型四舍五入。
;四舍五入到一个给定的精度
:指定需要的精度用第四个未命名参数（如果“转换”参数被省略，第三无名参数；如果指定的范围，或是第五个未命名的参数；如果被指定范围和“转换”参数被省略，或第四个未命名参数；必要时要“精确”命名参数）取代。转换四舍五入采用精确位置数值{{frac|10}}来判断。例如，如果数值是8621，参数是'-2'，其结果将是8600。如果数值是234.0283043和参数为'0'，结果将是234。

;四舍五入到一个给定的数量[[有效数字]]
:指定所需数量的有效数字 <code><nowiki>|sigfig={大于1的整数}</nowiki></code>如上所述。

;默认的四舍五入
:如果没有特殊指定，将参考输入值可比精度四舍五入（小数点后的数位或一些非重大零负之前增加一个转换，如果是0.02和0.2之间的精度加1，如果是0.2和2之间不变，如果它是2和20之间精度减1，等等），或最精确的两个有效数字。温度例外，将四舍五入转换输入值。

{| class="wikitable"
|-
! colspan="3" | 默认四舍五入的例子
|-
|'''输入'''||'''显示为'''||'''说明'''
|-
|<nowiki>{{convert|550|ft|m|0}}</nowiki>||{{convert|550|ft|m|0}}  || 近似值167.64米
|-
|<nowiki>{{convert|550|ft|m}}</nowiki>||{{convert|550|ft|m}} || 近似值167.64米，四舍五入到170
|-
|<nowiki>{{convert|500|ft|m|0}}</nowiki>||{{convert|500|ft|m|0}}  ||  近似值152.4米
|-
|<nowiki>{{convert|500|ft|m}}</nowiki>||{{convert|500|ft|m}}  ||   近似值152.4米，四舍五入到150
|}<!--NOTE: rows require "nowiki", using &#123;{ disappears. -->

=== 支持單位 ===
参见[[Module:Convert/documentation/conversion data/doc]]

===除錯===
如果使用本模板時因為提供錯誤的參數值或參數值不足等而得出類似這樣的提示字眼：{{convert|abbr=bogus}}，條目就會被加入隱藏分類「[[:Category:未獲Convert模塊承認的單位或選項]]」（條目以外的名字空間不受影響），將鼠標移到提示句子上顯示彈出信息框並按其指示除錯。

===參見===
* {{Tl|Convinfobox}} for use in infoboxes
* {{Tl|Bbl to t}} for converting barrel of oil to tonnes
* {{Tl|CwtQtrLb to kg}} for converting long hundred weights, quarters and pounds into kilograms
* {{Tl|Decdeg}} for converting degrees, minutes and seconds to [[decimal degrees]]
* {{Tl|HMS2Deg}} for converting [[hour angle]]s, given in hours, minutes and seconds, to decimal degrees
* {{Tl|Miles-chains}} for converting miles and chains to kilometres linking "chains"
* {{Tl|Pop density}} for converting a population and area to a density
* {{Tl|Inflation}} for calculating inflation of Consumer Price Index related prices
* {{Tl|Metricate}}
* {{Tl|RailGauge}} for converting rail (track) gauges
* {{Tl|Convert/scale}} with custom formula for converting any linearly related units
* [[bugzilla:235|Bug 235]]: Auto unit conversion 

<includeonly>
[[Category:换算模板]]

</includeonly>