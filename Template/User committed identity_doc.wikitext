<noinclude>{{template doc page viewed directly}}</noinclude>
<!-- EDIT TEMPLATE DOCUMENTATION BELOW THIS LINE -->
{{NoteTA
|G1=IT
|1=zh-cn:选用：用其他冠词取代“一份”（暂未使用）; zh-tw:選用：用其他冠詞取代“一份”（暫未使用）;
}}<!-- 鑒於本頁使用了大量需轉換的術語，且轉換並未用於「模板中」，請勿移除該模板！ -->

== 模板参数 ==

<templatedata>
{
	"params": {
		"1": {
			"label": "散列数值",
			"required": true
		},
		"2": {
			"label": "散列函数",
			"suggested": true,
			"autovalue": "SHA-512"
		},
		"background": {
			"label": "背景颜色",
			"autovalue": "#E0E8FF"
		},
		"border": {
			"label": "边框颜色"
		},
		"border-width": {
			"label": "邊框闊度",
			"autovalue": "1"
		},
		"extra-style": {
			"label": "额外CSS样式"
		},
		"article": {
			"label": "冠词"
		}
	}
}
</templatedata>

== 模板說明 ==

<pre>-{}-
{{User committed identity
|散列值  <!-- 必填。可以使用汉字、英文字母、数字或英文标点符号等 -->
|散列函数  <!-- 選用。預設為SHA-512 -->
|background=  <!-- 選用。背景HTML色彩 -->
|border= <!-- 選用。邊框HTML色彩 -->
|article= <!-- 選用。用其他冠词取代“一份”-->
|border-width= <!-- 選用。框闊度預設為1-->
}}
</pre>

範例如下：

<code style="word-break: break-all;"><nowiki>{{User committed identity|cf83e1357eefb8bdf1542850d66d8007d620e4050b5715dc83f4a921d36ce9ce47d0d13c5d85f2b0ff8318d2877eec2f63b931bd47417a81a538327af927da3e|SHA-512|background=#E0E8FF|border=#aaa|article=一个|border-width=5}}</nowiki></code>
{{User committed identity|cf83e1357eefb8bdf1542850d66d8007d620e4050b5715dc83f4a921d36ce9ce47d0d13c5d85f2b0ff8318d2877eec2f63b931bd47417a81a538327af927da3e|SHA-512|background=#E0E8FF|border=#aaa|article=一个|border-width=5}}

==说明==
此模板可用于证明您的身份，例如证明账号的相关操作是您本人所为，或者在账号被盗后证明账户的所有权。填入散列值即可使用。

==為何需要？==
本模板的預期作用是用來幫助帳號遭竊取的人，但願這種事情不會發生。

如果您用自己的帳號公开了真实身份，而如果帳號被盗您的身份就可以用来和您的朋友重新建立联系。需要记住的是，这种情况下您并不能通过自己的帳号和朋友建立联系，因为帳號可能被他人控制了。但是，一些维基百科的用户并没有透露自己的真实身份或只透露了一点点，这就很难重新证明自己的身份。

除了拥有一个[[密码强度|強力密碼]]或为您的帳號注册电子邮箱地址外，并没有什么可替代的方法。您仍应尽自己所能来防止帳號被利用，包括使用[[密码强度|強力密碼]]及使用公共电脑时记得退出帳號。如果您能做到的话，公开自己的[[PGP]]公钥也是有一定用处的。但是即使您做得再好，帳號仍然有可能被盗，如通过[[特洛伊木马 (电脑)|特洛伊木马]]或对您的密码进行暴力破解。使用这个模板就可以为您留下最后一线希望。

==如何使用==
本模版主要的概念是使用密碼雜湊技術。您需要先選擇一個只有本人知道的密碼字串，再經由單向的密碼雜湊功能編譯這個密碼字串以得到一組亂碼，最後使用此模板公開此編譯好的密碼字串。由於密碼雜湊技術保證沒有一個人會輕易地將亂碼解譯回自設的密碼字串，因此，未來當遇到帳號被洩漏等不幸事件時，如果您可以提供原先的密碼字串，且此密碼字串經過相同密碼雜湊算法處理後與您之前提供的雜湊值相等，即可十分有力地證明您是此雜湊字串的提供者。

===選擇合適字串===
# 您所使用的字串应该不容易被猜测。如果您并没有公开自己的真实身份，那么任何和您真实身份有关的字串都会是好的字串。如果您'''曾经'''公开过自己是谁，您就需要用更多不容易被猜到的信息。'''如果您使用的字串容易被猜到'''，那么别人也可能会知道您的字串是什么。
# 您的字串应该和您的身份有一定关系。如果这个字串被人知道，您也可以明白地证明您和这个身份的关系。例如，您的字串可以包括您能拿到的电话号码和邮箱地址。
# 不要选择很快就不能证明您身份的字符。例如，当您可能要换电话号码时将现有的号码作为字串就是一个不好的选择。
# 如果您想更换字串，那就换吧。但您应该追溯自己作为密码使用过的老字串。如果您想进一步证实自己的身份，最好把它们全部公开。这就可以证明您是从这个身份一公开就使用自己账号的同一个人。
# 您的字符不应该太短：至少要有15个字符。一个精心的攻击者会使用暴力破解来尝试所有字符，直到他们猜到您用的字串为止。但如果您的字串足够长，攻击也要花费更长的时间。如果您的字串达到15个字符，同样长度的字串会有10<sup>27</sup>个，也就是1[[千秭]]（这还只计算了只带空格和字母的字串）。

* 对于类 UNIX 系统用户，可以使用 [[:en:/dev/random|/dev/urandom]] 之类的随机文件并用 dd 工具截取一部分内容 （例如:<code>dd if=/dev/urandom of='''目标文件''' bs=4096 count=1</code>) 并保存妥当。考虑到内容的杂乱性，这样的字串最好 [[base64]] 后发送给验证者让验证者解密再验证或者干脆直接以文件形式发送。<code>dd</code>在经过[[Root (Android)|Root]]的[[Android]]中安装的[[Busybox]]里一般也可以找到，将命令中<code>dd</code>替换为<code>busybox dd</code>即可使用，亦可通过安装Termux来使用<code>dd</code>，此方法无需root。
* 如果您有一套 [[PGP]] 系统，例如 [[GnuPG]]，您也可以使用公钥指纹，并将公钥放在用户页的子页面处，按照[[#使用PGP]]的方法进行验证。

===取得雜湊===
如果您需要在日后使用，确定您输入模板里的是“精确的字串”。字串容易让自己记住，又很难被人猜出很重要。如果攻击者知道这个字串，那么这个功能就是没有用的。用户名是公开的也容易猜到，而密码也不是好的选择，因为在多数账号被盗的事件中，密码多数已经被猜到了。

* OS X/Linux/Android：在类[[unix]]的系统中，[[GNU核心工具组]]和常常用于微型系统以及[[Android]]的[[Busybox]]都提供了<code>sha224sum</code>、<code>sha256sum</code>、<code>sha384sum</code>和<code>sha512sum</code>的程序（<code>sha1sum</code>、<code>md5sum</code>甚至更差的雜湊极度不建议使用，Busybox 的用法为<code>busybox 内置命令名 命令参数</code>）。这套工具的使用较为简单，可以直接输入命令，键入字符（标准输入），最后换行后 Ctrl-D 结束输入（EOF）。由于最近的密码学研究已经对使用SHA-1的长期可靠性提出了质疑，一般推荐使用SHA-256(224) 或 SHA-512(384)；使用几个散列值对同一份信息进行验证也可能是不错的解决方案。如果没有指定参数，这个模板默认情况下使用[[SHA 家族|SHA-512]]进行加密。如果您并没有 GNU 核心工具或 GnuPG，也可以使用<code>[[OpenSSL|openssl]] sha512 (流/文件名)</code>一类的参数以便用 [[OpenSSL]] 的命令行工具或直接用[http://download.cnet.com/HashCalc/3000-2250_4-10130770.html HashCalc]来获取hash值。为了安全，最好只用本地的可执行程序或客户端执行的[[JavaScript]]来创建hash值。

可以在终端使用以下命令生成散列值（把名字和邮件的部分替换为自己的）：

 <tt>printf 'My name is Joe Schmoe, and I can be contacted at: joe@example.com' | sha512sum</tt>

或者使用openssl：

 <tt>printf 'My name is Joe Schmoe, and I can be contacted at: joe@example.com' | openssl sha512</tt>

* Windows 下可以用 [[PowerShell]] 执行如下代码取得雜湊字段：

 <tt>[bitconverter]::tostring((new-object security.cryptography.sha512managed).computehash([text.encoding]::utf8.getbytes("<font color=red>'''用户信息确认串'''</font>"))).replace("-", "")</tt>

* 线上方式：通过[http://hash.online-convert.com/sha512-generator 这个网站]可以在线取得雜湊。输入字串后点击<code>Convert file</code>后便可生成几组雜湊字串，其中第一组字串即标注着<code>hex:</code>的字串便是您所需要的 SHA-512 雜湊。

===使用===
如果要向别人提交自己的身份并证明自己就是最初开始使用这个账号的人，把最早用来计算的'''准确密码串'''交给一个可靠的用户。他们可以用相同的字串计算得到适当的hash值，并证明您就是自己宣称的那个人。

一旦您证明了自己的身份并建立了新的账号或获得原始账号的控制权，您可能要重新创建一个hash值，并将密码串告诉某个人（可能很多人信任他且您曾经告诉过他密码串）。

===使用PGP===
对于一个 PGP 密钥，需要证明您能够使用所提供公钥对应的私钥，且需要一定时效性保证。PGP 程序的使用方法请参考[[b:GPG|GPG]]。

====声明所有权====
PGP 可以对一个消息进行有时间戳的签名，因此可以有效证明身份。

对于类[[UNIX]]系统用户，可以使用以下命令生成签名（将 <code>${USERNAME}</code> 换成用户名，<code>${DATE}</code>换为出现异常行为的日期）：
<syntaxhighlight lang=bash>echo "此处我（依照 PGP uid 所示的用户）在此声明账号${USERNAME}为我所有，且于${DATE}开始被盗用。" | gpg --clearsign</syntaxhighlight>
PGP 的签名中会带有时间戳，因此并不一定需要指定时间（<code>$(date)</code>）。

如果您使用[[Windows]]，可以创建一个类似内容的文本文件，或者通过[[Cygwin]]等环境处理。

接下来可以将生成的信息通过电子邮件发送。

====验证消息====
如果您之前并没有交换过公钥，可使用 <code>gpg --import</code> 或类似命令导入，但请务必检查这个公钥与被盗用日之前所提供的公钥指纹匹配。

接下来您可以使用 <code>gpg --verify</code> 或类似功能进行校验。请务必确认签名时间正常。除此之外，您也可以每次都额外要求声明者签名您所指定的随机字符串给您，来保证安全性。

<noinclude></noinclude>
<includeonly>
<!-- Categories -->
{{DEFAULTSORT:Committed Identity}}
[[Category:使用了分析程序的模板]]
[[Category:用戶頁模板]]

<!-- Interwikis -->
[[ar:قالب:هوية المستخدم الملزمة]]
[[bn:টেমপ্লেট:User committed identity]]
[[bs:Šablon:Korisnik kovertirani identitet]]
[[de:Vorlage:User committed identity]]
[[en:Template:User committed identity]]
[[fr:Modèle:Utilisateur identifiable]]
[[ja:Template:User committed identity]]
[[no:Mal:Brukeridentitet]]
[[si:සැකිල්ල:User committed identity]]
[[simple:Template:User committed identity]]
[[sr:Шаблон:Корисник ковертирани идентитет]]
[[zh-yue:Template:User committed identity]]
</includeonly>