{{Documentation subpage}}
{{Template shortcut|Nts}}
{{Lua|Module:Number table sorting}}
{{mbox
| type = notice
| text = 注意：Adding <code>data-sort-type="number"</code> to the relevant column header solves many numerical sorting problems. See [[Help:Sorting#Forcing a column to have a particular data type|Help:Sorting]].
}}
This template can be useful when building a [[Help:Sorting|sortable table]] in which a column contains both numbers and text. This template should be applied to every number in the column and should not be used outside of sortable tables. 

Currently, the template works for numbers between −10<sup>308</sup> and 10<sup>308</sup>. Numbers outside this range will sort above or below other numbers depending on sign. See the [[#Limitations|Limitations]] section below.

By default the output is displayed using thousands separators. To display numbers as entered, use {{para|format|no}}. 

The template generates a hidden "sort key" in the [[HTML]] markup which forces the [[JavaScript]] [[sorting algorithm]] to sort the column alphabetically. 

===概要===
在兩種情況下，此模板可適用： 
# 當數字後有一些文字
# 當數字前面帶有貨幣符號以外的其他文字

==參數及使用方法==
此模板僅一個參數：不含逗點的實數。以下範例使用了重定向模板{{tl|nts}}：

; 可選參數
* <code>prefix</code>：若想在數字前顯示文字，請使用{{para|prefix|''some prefix''}}
*: <code><nowiki>{{nts|123456789.00123|prefix=approx.&amp;nbsp;}}</nowiki></code> → {{nts|123456789.00123|prefix=approx.&nbsp;}}
* <code>format</code>：不帶逗點輸出，請使用{{para|format|no}}
*: <code><nowiki>{{nts|123456789.00123}}</nowiki></code> → {{nts|123456789.00123}}
*: <code><nowiki>{{nts|123456789.00123|format=no}}</nowiki></code> → {{nts|123456789.00123|format=no}}
* <code>debug</code>：若想顯示排序鍵，請使用{{para|debug|yes}}
*: <code><nowiki>{{nts|123456789.00123|debug=yes}}</nowiki></code> → {{nts|123456789.00123|debug=yes}}
*: <code><nowiki>{{nts|-123456789.00123|debug=yes}}</nowiki></code> → {{nts|-123456789.00123|debug=yes}}

Apart from the added thousands separators the numbers are formatted as supplied (scientific notation or not, leading and trailing zeros, and a zero before the decimal point or not). This formatting does not affect the sorted order except for numbers not satisfying the limitations mentioned below.

{{TemplateDataHeader}}
<templatedata>
{
	"description": "",
	"params": {
		"1": {
			"label": "Number",
			"type": "number",
			"required": true,
			"description": "Your number"
		},
		"format": {
			"label": "Format output?",
			"type": "string",
			"required": false,
			"description": "If you do not wish the output to be formatted (i.e. separated by thousand separators), please put \"no\" in this field. (Without quotation marks.)"
		},
		"debug": {
			"label": "Debug",
			"type": "string",
			"required": false,
			"description": "If set to \"yes\", forces output to include debug data"
		},
		"prefix": {
			"label": "Prefix",
			"type": "string",
			"required": false,
			"description": "The prefix to be displayed before the number. E.g. \"Approx.\" or \"$\""
		}
	}
}
</templatedata>

==排序鍵==
The sort key is a nineteen-digit number.  For numbers within range the first four digits are determined by the number's sign and [[order of magnitude]] and the next fifteen digits are determined by the number's sign and [[significand]].

;Numbers within range
*For numbers between 10<sup>−308</sup> and 10<sup>308</sup> the first four digits are calculated by adding 7000 to the order of magnitude and the next fifteen digits are calculated by multiplying the significand by 10<sup>14</sup>.
*For numbers between −10<sup>−308</sup> and −10<sup>308</sup> the first four digits are calculated by subtracting the order of magnitude from 2999 and the next fifteen digits are calculated by subtracting the significand from 10 multiplying the difference by 10<sup>14</sup>.
*The sort key for 0 is 5000000000000000000.

;Numbers out of range
*Numbers larger than 10<sup>308</sup> are assigned the sort key 9000000000000000000.
*Numbers smaller than −10<sup>308</sup> are assigned the sort key 1000000000000000000.
*Numbers between 10<sup>−308</sup> and 0 or between 0 and −10<sup>−308</sup> are assigned the sort key 5000000000000000000.

==注意事项==
*Any subset of numbers larger than 10<sup>308</sup> are sorted together.
*Any subset of numbers smaller than −10<sup>308</sup> are sorted together.
*Any subset of numbers between 10<sup>−308</sup> and −10<sup>−308</sup> are sorted together.
*If a non-numeric value is given as the first unnamed parameter the results are undefined.
*The hyphen minus sign is converted into a true minus sign; note, though, that this means no more than 12 significant figures are possible.
*A prefix (using the <code>prefix</code> parameter) does not affect the sort order.

==範例==
<code><nowiki>{{nts|123456789.00123}}</nowiki></code> → {{nts|123456789.00123|debug=yes}}

For text which follows a number, <code><nowiki>{{nts|123,456}}</nowiki> as of 2012</code> displays <code>123,456 as of 2012</code> with a numerical sort key of <code>123456</code>. This forces numerical sorting in the cell using this value instead of the default alphabetical sorting.

Below are more examples, some of which illustrate the limitations listed above.

{| class="wikitable sortable"
! 代碼
! 排序鍵和數字
! 錯誤
|-
| <code><nowiki>{{nts|debug=yes}}</nowiki></code> || {{nts|debug=yes}}
|-
| <code><nowiki>{{nts||debug=yes}}</nowiki></code> || {{nts||debug=yes}}
|-
| <code><nowiki>{{nts|2和3之間|debug=yes}}</nowiki></code> || {{nts|2和3之間|debug=yes}}
|-
| <code><nowiki>{{nts|2和3之間|debug=no}}</nowiki></code> || {{nts|2和3之間|debug=no}}
|-
| <code><nowiki>{{nts|10|prefix=約|debug=yes}}</nowiki></code> || {{nts|10|prefix=約|debug=yes}}
|-
| <code><nowiki>{{nts|-5|debug=yes}}</nowiki></code> || {{nts|-5|debug=yes}}
|-
| <code><nowiki>{{nts|-4|debug=yes}}</nowiki></code> || {{nts|-4|debug=yes}}
|-
| <code><nowiki>{{nts|-73|debug=yes}}</nowiki></code> || {{nts|-73|debug=yes}}
|-
| <code><nowiki>{{nts|-67|debug=yes}}</nowiki></code> || {{nts|-67|debug=yes}}
|-
| <code><nowiki>{{nts|-20345678901234567.12345678|debug=yes}}</nowiki></code> || {{nts|-20345678901234567.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|123.456e3|debug=yes}}</nowiki></code> || {{nts|123.456e3|debug=yes}}
|-
| <code><nowiki>{{nts|123.456e2|debug=yes}}</nowiki></code> || {{nts|123.456e2|debug=yes}}
|-
| <code><nowiki>{{nts|20345678901234567.12345678|debug=yes}}</nowiki></code> || {{nts|20345678901234567.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|100345678901234567.12345678|debug=yes}}</nowiki></code> || {{nts|100345678901234567.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|1234567890123456.12345678|debug=yes}}</nowiki></code> || {{nts|1234567890123456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|234567890123456.12345678|debug=yes}}</nowiki></code> || {{nts|234567890123456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|34567890123456.12345678|debug=yes}}</nowiki></code> || {{nts|34567890123456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|4567890123456.12345678|debug=yes}}</nowiki></code> || {{nts|4567890123456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|567890123456.12345678|debug=yes}}</nowiki></code> || {{nts|567890123456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|67890123456.12345678|debug=yes}}</nowiki></code> || {{nts|67890123456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|7890123456.12345678|debug=yes}}</nowiki></code> || {{nts|7890123456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|890123456.12345678|debug=yes}}</nowiki></code> || {{nts|890123456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|90123456.12345678|debug=yes}}</nowiki></code> || {{nts|90123456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|0123456.12345678|debug=yes}}</nowiki></code> || {{nts|0123456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|123456.12345678|debug=yes}}</nowiki></code> || {{nts|123456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|23456.12345678|debug=yes}}</nowiki></code> || {{nts|23456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|3456.12345678|debug=yes}}</nowiki></code> || {{nts|3456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|456.12345678|debug=yes}}</nowiki></code> || {{nts|456.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|56.12345678|debug=yes}}</nowiki></code> || {{nts|56.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|6.12345678|debug=yes}}</nowiki></code> || {{nts|6.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|.12345678|debug=yes}}</nowiki></code> || {{nts|.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|0.12345678|debug=yes}}</nowiki></code> || {{nts|0.12345678|debug=yes}}
|-
| <code><nowiki>{{nts|0.02345678|debug=yes}}</nowiki></code> || {{nts|0.02345678|debug=yes}}
|-
| <code><nowiki>{{nts|0.00345678|debug=yes}}</nowiki></code> || {{nts|0.00345678|debug=yes}}
|-
| <code><nowiki>{{nts|0.00045678|debug=yes}}</nowiki></code> || {{nts|0.00045678|debug=yes}}
|-
| <code><nowiki>{{nts|0.00005678|debug=yes}}</nowiki></code> || {{nts|0.00005678|debug=yes}}
|-
| <code><nowiki>{{nts|0.00000678|debug=yes}}</nowiki></code> || {{nts|0.00000678|debug=yes}}
|-
| <code><nowiki>{{nts|0.00000078|debug=yes}}</nowiki></code> || {{nts|0.00000078|debug=yes}}
|-
| <code><nowiki>{{nts|0.00000008|debug=yes}}</nowiki></code> || {{nts|0.00000008|debug=yes}}
|-
| <code><nowiki>{{nts|.00000008|debug=yes}}</nowiki></code> || {{nts|.00000008|debug=yes}}
|-
| <code><nowiki>{{nts|0|debug=yes}}</nowiki></code> || {{nts|0|debug=yes}}
|}

==參見==
* {{tl|ntsh}} - 與本模板相同，但是不顯示數字
* {{tl|val}} - displays numbers and quantities with various formatting options
* {{tl|Convert}} - 有排版選項
* {{tl|Date table sorting}}
* {{tl|Sort}}
* {{tl|Hidden sort key}}

<includeonly>{{Sandbox other||<!-- 本行下加入模板的分類 -->
[[Category:排序模板|Nts]]
[[Category:Lua模板|Nts]]
}}</includeonly>