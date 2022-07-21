<includeonly>{{Esoteric}}</includeonly><noinclude>{{template doc page viewed directly}}</noinclude>
<!-- EDIT TEMPLATE DOCUMENTATION BELOW THIS LINE -->
{{Ambox
| image = [[File:Edit-copy purple-wikit.svg|40px]]
| type  = move
| text  = 使用本模板製作大型系譜有機會超過維基媒體制定的[[维基百科:模板限制|允許渲染長度]]導致無法儲存或開啟條目，這時候請改用較為先進的{{tl|Tree chart}}模板。
}}

此模板使用类似[[ASCII艺术]]的句法生成简单[[系谱图]]。它用[[HTML]]表格和[[CSS]]在适当的位置生成文字框和线条以构成家族树，使用者在文本框内可以任意运用维基语法。

此模板基于英语维基上的模板[[:en:Template:Familytree]]，由[[:en:User:Ilmari Karonen|Ilmari Karonen]]用户开发和维护。

==参数==
模板接受至多99个未命名参数，每个参数代表一个“格子”或者一个“框”。

*'''格子'''内含有线状元素，用来生成横纵线条以及各种拐角以连接各个“框”。每一个格子用简单的字符参数来描述，一个特别的例子是'''空格子'''，用一个空格来描述不含任何线条的格子。下面列出模板支持的格子类型：

{| style="float: left; margin-left: 1em;"
|+ '''實體線'''
|-
| <big><tt>,</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|,}}{{familytree/end}} || &nbsp;
| <big><tt>.</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|.}}{{familytree/end}} || &nbsp;
| <big><tt>`</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|`}}{{familytree/end}} || &nbsp;
| <big><tt>'</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|'}}{{familytree/end}} || &nbsp;
|-
| <big><tt>^</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|^}}{{familytree/end}} || &nbsp;
| <big><tt>v</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|v}}{{familytree/end}} || &nbsp;
| <big><tt>(</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|(}}{{familytree/end}} || &nbsp;
| <big><tt>)</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|)}}{{familytree/end}} || &nbsp;
|-
| <big><tt>-</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|-}}{{familytree/end}} || &nbsp;
| <big><tt>!</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|!}}{{familytree/end}} || &nbsp;
| <big><tt>+</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|+}}{{familytree/end}} || &nbsp;
| <big><tt> </tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree| }}{{familytree/end}} || &nbsp;
|}
{| style="float: left; margin-left: 1em;"
|+ '''虛線'''
|-
| <big><tt>F</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|F}}{{familytree/end}} || &nbsp;
| <big><tt>7</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|7}}{{familytree/end}} || &nbsp;
| <big><tt>L</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|L}}{{familytree/end}} || &nbsp;
| <big><tt>J</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|J}}{{familytree/end}} || &nbsp;
|-
| <big><tt>A</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|A}}{{familytree/end}} || &nbsp;
| <big><tt>V</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|V}}{{familytree/end}} || &nbsp;
| <big><tt>C</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|C}}{{familytree/end}} || &nbsp;
| <big><tt>D</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|D}}{{familytree/end}} || &nbsp;
|-
| <big><tt>~</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|~}}{{familytree/end}} || &nbsp;
| <big><tt>:</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|:}}{{familytree/end}} || &nbsp;
| <big><tt>%</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|%}}{{familytree/end}} || &nbsp;
|}
{| style="float: left; margin-left: 1em;"
|+ '''混合型'''
|-
| <big><tt>*</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|*}}{{familytree/end}} || &nbsp;
| <big><tt>}</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|}|}}{{familytree/end}} || &nbsp;
| <big><tt>{</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|{|}}{{familytree/end}} || &nbsp;
|-
| <big><tt>#</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|#}}{{familytree/end}} || &nbsp;
| <big><tt>y</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|y}}{{familytree/end}} || &nbsp;
| <big><tt>h</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|h}}{{familytree/end}} || &nbsp;
|-
| <big><tt>]</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|]}}{{familytree/end}} || &nbsp;
| <big><tt>[</tt></big> || style="border: 1px solid gray;" | {{familytree/start}}{{familytree|[}}{{familytree/end}} || &nbsp;
|}
<br clear="left" />

*'''框'''内可以填写任意的维基标记，框内的内容用附加命名变量的方法来加以描述。每一个框为'''三个格子'''宽，并且通常具有2px宽的黑边。附加的变量可以取用任何合法的名字，但是建议不要使用单字符的名字以免与“格子”冲突。

框的外形可以由参数'''border'''和'''boxstyle'''控制，前一个以[[像素]]为单位控制框边的宽度，后者可以为任意[[CSS]]语句，用来修饰框的外观。例如下列代码：

<pre><nowiki>
{{familytree/start}}
{{familytree|border=0|boxstyle=background:#dfd;| | FOO |y| BAR | |FOO=Box 1|BAR=Box 2}}
{{familytree|border=0|boxstyle=background:#dfd;| | |,|-|^|-|.| | }}
{{familytree|border=0|boxstyle=background:#dfd;| | FOO | | BAR | |FOO=Box 3|BAR=Box 4}}
{{familytree/end}}
</nowiki></pre>

产生如下效果：

{{familytree/start}}
{{familytree|border=0|boxstyle=background:#dfd;| | FOO |y| BAR | |FOO=Box 1|BAR=Box 2}}
{{familytree|border=0|boxstyle=background:#dfd;| | |,|-|^|-|.| | }}
{{familytree|border=0|boxstyle=background:#dfd;| | FOO | | BAR | |FOO=Box 3|BAR=Box 4}}
{{familytree/end}}

{{tl|familytree/start}}模板也接受一个可选的'''style'''参数来制定整个表格的格式。

==使用范例==
此范例可能对于第一次使用者有所帮助，当读者掌握相应技巧后，并不需遵循此过程。

步骤一：首先在紙上把家族圖畫好，如下圖：
{{familytree/start}}
{{familytree | | | Mum |y| Dad |Mum=妈妈|Dad=爸爸}}
{{familytree | |,|-|-|-|+|-|-|-|.| | }}
{{familytree | Bro | |  I  | | Sis | Bro=哥哥|I=我|Sis=妹妹}}
{{familytree/end}}


步骤二：考虑将这个图放置在一个长方形中，图形由一个个小的方格子所组成，填满整个长方形（如同在[[拼图]]），每个方格子为以下3种元素之任一：
*连接用的线条，例如{{familytree/start}}{{familytree|y}}{{familytree/end}}每个占用1个方格子，若是较长的线则需要拼接。
*文字与边框，例如{{familytree/start}}{{familytree | bb | bb=&nbsp; &nbsp; &nbsp; &nbsp; 爸爸 &nbsp; &nbsp; &nbsp; &nbsp; }}{{familytree/end}}注意的是文字连同边框一起占用3个方格子，这是固定且不能自行定义的。
*空格，即除以上两种之外的空白处，每个空格即为1个方格子大小的空白。

按照这种方法，以上图形可以用3行11列个方格子来表示，具体分解如下（这一步为关键步骤，如出错会导致图形的偏差）：

 {| class="wikitable" style="text-align:center"
|-
| 空格 || 空格 || colspan="3" |妈妈|| {{familytree/start}}{{familytree|y}}{{familytree/end}} || colspan="3" |爸爸|| 空格 || 空格
|-
| 空格 || {{familytree/start}}{{familytree|,}}{{familytree/end}} || {{familytree/start}}{{familytree|-}}{{familytree/end}} ||  {{familytree/start}}{{familytree|-}}{{familytree/end}} ||  {{familytree/start}}{{familytree|-}}{{familytree/end}}|| {{familytree/start}}{{familytree|+}}{{familytree/end}}  ||  {{familytree/start}}{{familytree|-}}{{familytree/end}} ||  {{familytree/start}}{{familytree|-}}{{familytree/end}} ||  {{familytree/start}}{{familytree|-}}{{familytree/end}} ||  {{familytree/start}}{{familytree|.}}{{familytree/end}} || 空格
|-
| colspan="3" |哥哥|| 空格 || colspan="3" |我|| 空格 || colspan="3" |妹妹
|}
这里特别提醒下对于空格数量的确认，你可能不能一下子看出第一行左侧有2个空格，但是当你整齐地将图形进行排列和划分后，即能发现应该补足的空格数量。


步骤三：换成对应的代码，每个方格子的代码之间使用竖线条 | 来进行分隔：

* 看到连接线，比如 {{familytree/start}}{{familytree|y}}{{familytree/end}} 就是竖线条之间加一个y（请查看参数）
* 看到文字和方框，那就在竖线条之间加入文字（注意文字的方框不需要单独的代码）
* 看到空格，就是竖线条之间为一个空格

以下是替换后的结果，与上列表格一一对应：

<pre><nowiki>
| | | 妈妈 |y| 爸爸 | | |
| |,|-|-|-|+|-|-|-|.| |
| 哥哥 | | 我  | | 妹妹 |
</nowiki></pre>

马上就要成功了，不过文字部分还要稍作处理，对于文字，你需要自行创造一个代码填入该文字应该占据的位置，然后在该行之后说明这种替代关系。

这里比如把妈妈用 “Mum”表示，爸爸用“Dad”表示（当然这是你自己定义的，用爹、粑粑、bb之类的表示均可，但最好使用三个字符，因为使用三个字符时，上下行对齐，容易检查）。在下面，“Mum”和“Dad” 两个代码已经替换了原有文字，而 “Mum=妈妈 | Dad=爸爸”则加在原有语句后面表示这种替代关系，注意，“Mum=妈妈”和“Dad=爸爸”之间是使用一条竖线 | 来进行分隔的，以此类推。

<pre><nowiki>
| | | Mum |y| Dad | | | Mum=妈妈 | Dad=爸爸
</nowiki></pre>


步骤四：按以下格式，即为完整的、可以使用的代码：
<pre><nowiki>
{{familytree/start}}
{{familytree | | | Mum |y| Dad | | |Mum=妈妈|Dad=爸爸}}
{{familytree | |,|-|-|-|+|-|-|-|.| | }}
{{familytree | Bro | |  I  | | Sis |Bro=哥哥|I=我|Sis=妹妹}}
{{familytree/end}}
</nowiki></pre>

下面给出一个更大的家族图与代码，供参考，可以看到文字部分使用了一些维基语法：

{{familytree/start}}
{{familytree | | | | 奶 |~|y|~| 爷 | | 奶=奶奶|爷=爷爷}}
{{familytree | | | | | | | |)|-|-|-|.| }}
{{familytree | | | 妈 |y| 爸 | |叔| 妈=妈妈|爸=爸爸|叔=<s>叔叔</s>}}
{{familytree | |,|-|-|-|+|-|-|-|.| | | }}
{{familytree | 哥 | | 俺 | | 妹 | | | 哥=哥哥|俺='''我'''|妹=[[妹妹]]}}
{{familytree/end}}

<pre><nowiki>
{{familytree/start}}
{{familytree | | | | 奶 |~|y|~| 爷 | | 奶=奶奶|爷=爷爷}}
{{familytree | | | | | | | |)|-|-|-|.| }}
{{familytree | | | 妈 |y| 爸 | |叔| 妈=妈妈|爸=爸爸|叔=<s>叔叔</s>}}
{{familytree | |,|-|-|-|+|-|-|-|.| | | }}
{{familytree | 哥 | | 俺  | | 妹 | | | 哥=哥哥|俺='''我'''|妹=[[妹妹]]}}
{{familytree/end}}
</nowiki></pre>

==相關資料==
*{{tl|Chart}}－可顯示更複雜的家族圖
<includeonly>
[[Category:系譜模板|{{PAGENAME}}]]
</includeonly>