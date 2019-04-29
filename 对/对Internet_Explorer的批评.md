{{original research|time=2014-08-31}}
{{update|time=2014-08-31}}
{{noteTA
|G1=IT
|G2=Windows
|1=zh-hans:网上; zh-tw:網路上;
|2=zh-hans:单词; zh-tw:單字;
|3=zh-hans:站点; zh-tw:網站;
}}

'''[[Internet_Explorer|Internet Explorer]]'''是一款招致了许多批评的[[网页浏览器|网页浏览器]]。大部分批评都集中在其[[电脑安全|安全]]架构以及对[[开放标准|开放标准]]的支持程度上。

== 对其安全性的批评 ==
Internet Explorer 的安全性已被来自[[電腦安全|電腦安全]]研究社群全面审查，部分原因是因为市场被其独占。Internet Explorer 的[[安全漏洞|安全漏洞]]已经使得其成为[[网页浏览器列表|主流浏览器]]中較不安全的一个。

2005年6月20日，安全咨询网站[[Secunia|Secunia]]列出了 Internet Explorer 6 的20个无补丁的安全漏洞{{noteTag|[http://secunia.com/product/11/ 20个无补丁的安全漏洞列表。]}}，在每一个安全级别中，绝大部分漏洞存在的时间都比[[网页浏览器比较#一般資料|其他浏览器]]的时间长，但其中的一些漏洞只會影响特定版本的 Windows 上的某些 Internet Explorer 或是在与某些其他应用程序结合时才会暴露。

另一安全咨询网站SecurityFocus列出了存在于 Windows XP Service Pack 2 的 Internet Explorer 6 中 27个无补丁安全漏洞<ref group="參" >[http://securityfocus.com/cgi-bin/index.cgi?l=30&c=12&vendor=Microsoft&version=6.0%20SP2&title=Internet%20Explorer Internet Explorer 6 中 27个无补丁安全漏洞]</ref>。在 Windows XP SP2 上的早期 Windows 中存在更多。

2004年6月23日，一个目的在于大公司 [[IIS|IIS]] 服务器的攻击即是通过使用 Internet Explorer 中两个先前未发现的漏洞，借以在不知情的大量最终用户的浏览器中插入[[垃圾邮件|垃圾邮件]]发送软件而成{{refTag|[http://news.zdnet.com/2100-1009_22-5247187.html Researchers warn of infectious Web sites], [[May_12|May 12]], 2005.}}{{refTag|1=[http://isc.incidents.org/diary.php?isc=79fcd38fcac%20d616798ba716ac6e99ca1 Handler's Diary May 11th 2005], [[May_12|May 12]], 2005.}}{{refTag|[http://62.131.86.111/analysis.htm An analysis of the Ilookup Trojan], [[May_12|May 12]], 2005.}}。该[[恶意软件|恶意软件]]被定名为[[Download.ject|Download.ject]]，它会在用户浏览网页时偷偷电脑中安装[[后门|后门]]以及一个[[鍵盤監聽|键盘击键记录软件]]。被感染的电脑包括许多金融網站。

Art Manion 是[[美国电脑紧急相应小组|美国电脑紧急相应小组]]（US-CERT）的一名代表，他指出 Internet Explorer 6 SP1 的许多设计使得 Internet Explorer 6 天生就不可能安全，他说道：

{{cquote|在IE安全区域模块的技术中存在大量严重漏洞，本地文件系统（本机区域）被设计为信任动态HTML(DHTML)文档对象模块（特别的，DHTML所特有的功能）、HTML帮助系统、MIME类别定义、图形用户介面（GUI）以及ActiveX……另一方面IE又被设计为整合进Windows以至于IE的漏洞经常被骇客当作对操作系统的进行攻击的一个重要途径。{{noteTag|[http://www.kb.cert.org/vuls/id/713878 美国电脑紧急相应小组 Internet Explorer 6 SP1 的資料]}}}}

Manion随后声名他的讲话大部分是相对于2004年发布 SP2 前的，并且其他浏览器也开始在上述CERT文件中面临类似的问题{{noteTag|1=http://news.com.com/A+safe+browser+No+longer+in+the+lexicon/2010-1071_3-5777036.html?part=rss&tag=5777036&subj=news}}。

值得注意的是XP SP2所提供的一些功能对于先前版本的Windows并不可用，它们包括 Windows 9x，NT 和 2000。

另外，一些与Internet Explorer相关的安全漏洞也令需要的Windows用户突破安全权限。一个例子是，在Windows XP中，缺省时系统是不允许普通用户组（User用户组）的用户以管理员组（Administrator用户组）权限进行特权操作的。但实际上，这种情况下骇客可以运行一个专用代码实现对电脑操作系统的完全控制。这种破解行为也将导致任何浏览器以不受限的特权状态运行。对于其他系统普通用户的日常操作来说，使用[[超级用户|超级用户]]（Power User用户组）进行日常操作是不明智的，但攻击者可以依赖于Windows系统中这个处于不适当级别的浏览器进程。然而，也有许多Windows中的程式离开管理员特权无法运行或效果变差，所以其他系统中的正常操作可能对于Windows用户来说是不切实际。

许多的安全分析者指出IE经常爆出严重漏洞是因为它独占市场份额，所以骇客把其优先作为攻击目标。然而，也有许多批评指出这种说法是不全面的；[[Apache|Apache]]网络服务器的市场份额比微软IIS要高，但Apache几乎没有安全漏洞，就算有也相较IIS说是很轻微{{noteTag|http://www.dwheeler.com/oss_fs_why.html}}。微软的Craig{{dead link|date=2017年12月 |bot=InternetArchiveBot |fix-attempted=yes }} Mundie曾经承认微软公司的产品「对常态而言是不安全的」而这是因为微软「设计时更注重功能而非安全」{{noteTag|http://www.vnunet.com/news/1135763}}。{{dead link|date=2017年12月 |bot=InternetArchiveBot |fix-attempted=yes }}

结果这样导致许多问题，一些安全专家，包括[[Bruce_Schneier|Bruce Schneier]] {{refTag|[http://www.schneier.com/blog/archives/2004/12/safe_personal_c.html Safe Personal Computing], [[May_12|May 12]], 2005.}}以及[[开源|开源]]倡导者[[David_A._Wheeler|David A. Wheeler]] {{refTag|[http://www.dwheeler.com/essays/securing-windows.html Securing Microsoft Windows (for Home and Small Business Users)], [[May_12|May 12]], 2005.}}，推荐广大用户停止使用Internet Explorer作为日常浏览器，而转换其他浏览器作为替代。一些技术专栏作家也建议过类似的话{{refTag|[http://ptech.wsj.com/archive/ptech-20040916.html How to Protect Yourself From Vandals, Viruses If You Use Windows], [[May_12|May 12]], 2005.}} {{refTag|[http://www.eweek.com/article2/0,1759,1617931,00.asp Internet Explorer Is Too Dangerous to Keep Using], [[May_12|May 12]], 2005.}}。2004年6月6日，US-CERT发布的漏洞报告建议立即停止使用IE而该用其他，尤其是访问非信任站点时更应如此{{noteTag|http://www.kb.cert.org/vuls/id/713878}}。2004年12月，宾夕法尼亚大学发布的一篇文章告诫学生和员工马上丢弃使用IE并改用其他浏览器{{noteTag|1=http://www.informationweek.com/story/showArticle.jhtml?articleID=55301109}}。

===组件对象模块===
许多的IE安全问题皆与[[组件对象模块|组件对象模块]]（COM）相关。IE通过[[ActiveX|ActiveX]]或[[浏览器帮助对象|浏览器帮助对象]]（Browser Helper Object）将COM深植其中。这种功能的结合为[[电脑病毒|电脑病毒]]、[[特洛伊木马_(电脑)|特洛依木马程序]]以及[[间谍软件|间谍软件]]的进入大开方便之门。

这些[[恶意软件|恶意软件]]的攻击与传遍通常皆要利用ActiveX。微软早已经认识到这一问题，1996年Charles Fitzgerald－微软的Java团队程序负责人曾说，「如果你想在『-{zh-hans:网上; zh-tw:網路上;}-』安全，请关掉你的电脑。我们从来没有准备让ActiveX安全。{{noteTag|http://www.javaworld.com/javaworld/jw-03-1997/jw-03-component.web97.html}}」{{dead link|date=2017年12月 |bot=InternetArchiveBot |fix-attempted=yes }}

ActiveX控件，一旦运行，即可获得用户特权而非像其竞争技术（如Java与JavaScript）那样被限制的运行。ActiveX控件一如既往的是一个非标准的不可在非Windows平台上移植的技术。一份[[普林斯頓大學|普林斯頓大學]]教授[[Edward_Felten|Edward Felten]]的文章[http://www.cs.princeton.edu/sip/java-vs-activex.html 指出]:

{{cquote|ActiveX的安全依赖于个人的判断力。ActiveX程序可以附带程序厂商或其他任何人的数字签名。ActiveX的主要危险之处在于你可能对是否接受一个程序作出错误的判断。在最危险的情况下，这个程序被你所不了解的某个人加上数字签名，而你又确实想知道程序运行的结果，但是如果你拒绝它你将不可能看见结果。惟一可以避免这样情况的方法是拒绝所有程序，而不管上面写的如何有趣如何好玩儿，除非这个程序来自少数你真正了解的发布方。{{noteTag|http://www.cs.princeton.edu/sip/java-vs-activex.html}}}}

ActiveX的安全依赖于安全区域的设置和数字签名，而没有类似[[沙盒_(计算机安全)|沙盒]]以及元政策的指导{{noteTag|http://www.mozilla.org/projects/security/components/same-origin.html}}。在O'Reilly的书中有这样的解释恶意移动代码：{{dead link|date=2017年12月 |bot=InternetArchiveBot |fix-attempted=yes }}

{{cquote|ActiveX最大的问题在于它标记对脚本安全的方法不对。已经有一些email蠕虫攻击使用这种方法，这种类型的漏洞还会持续发现。如果微软都不能正确决定自己系统控件的安全级别设定，第三方程序提供商更不可能做到。接下来的问题就是未签署代码使用的增长。数字签名过程是一项技术并且昂贵。大部分网上的ActiveX控件都未曾加以签名。被签名程序中的大部分又是过期的证书签署的。我很少看见一个正确有效的控件签名。如果ActiveX的执行在于最终用户是否选择执行它，那么数字签名技术一定要更广泛传播。如果ActiveX成为世界范围内网站的标准，那么可以想见的是，我们将会看见使用ActiveX的恶意代码的剧增。{{noteTag|1=http://www.groklaw.net/article.php?story=20050127222737475}}}}

ActiveX的安全问题首次被发现是在1997年，[[混沌電腦俱樂部|混沌電腦俱樂部]]（Chaos Computer Club）这家机构展示了一个可以与用户手持设备中[[Intuit|Intuit]]的[[Quicken|Quicken]]金融软件自动进行连接的ActiveX控件，这个程序会自动将用户帐号上的钱转移至CCC的银行帐号{{noteTag|1=http://news.com.com/2100-1023-268947.html?legacy=cnet}}。

[[美国国防部|美国国防部]](DoD)已经将ActiveX定义为1类（最危险）的移动代码技术，并严格限制ActiveX在DoD系统内的使用{{noteTag|http://www.defenselink.mil/nii/org/cio/doc/mobile-code11-7-00.html}}。

也有专家认为ActiveX的风险被过分夸张了，而其实ActiveX是有安全机制的。eWeek的Larry Seltzer指出：

{{cquote|显然的没有足够证据证明ActiveX是不安全的，有很多反对的声音是无根据传说或是不值一驳的谣言。实际上Sun公司花钱雇人编写恶意ActiveX控件。我在JavaOne的时候，他们演示了（我想是1997年）它。测试系统显示的是一系列你通常见到的警示对话框，但Sun的雇员竟然有胆量编写了那种使警示对话框迅速关闭以使人们忽略其存在的软件。同时，他们同样也没有提及即使是签名过的Java小程序也可能会执行一些危险的特权操作，这些操作应当提供类似的警示对话框。大部分针对ActiveX的批评是简单而又非正式的，这个例子却指出了伪善者的不诚实。{{noteTag|http://www.eweek.com/article2/0,1759,1785769,00.asp}}}}

已发布的[[Windows_Defender|Windows Defender]]可以监视Windows 2000，XP and Server 2003下IE中的BHO，并对欲新安装BHO对用户作出警告。

===补丁===
很多人批评IE常常在发现问题很长时间後才发布对应的补丁，而且发布的补丁常常不能完全修复漏洞。如微软在2003年2月发布初始报告後200天才发布出补丁（而不是30-60天），Marc Maifrett，[[eEye_Digital_Security|eEye Digital Security]]的Hacking部门主管说过：“如果它们真的需要花费如此长的时间来修复(以及测试)，那么他们还有别的问题。这不是一个软件公司的运作常态。{{noteTag|http://news.com.com/2102-1002_3-5158625.html}}”[[The_Register|The Register]]则批评Maifrett公布的安全漏洞导致了[[CodeRed|CodeRed]]在那年的流行，也有人认为：「如果他们没有发现引起公众慌乱、ida漏洞或是他们的SecureIIS产品有能力防卫，红色代码蠕虫就不会感染数千台系统。{{noteTag|http://www.theregister.co.uk/2001/07/20/internet_survives_code_red/}}

微软将他们的延期归咎于区域测试。公司对Internet Explorer进行测试的软件是复杂而完全的。IE浏览器以26种不同语种发布在不同的Windows平台上。因此，对每个补丁的测试估计需要进行[http://blogs.msdn.com/ie/archive/2004/08/17/216080.aspx 最少237次安装]。

虽然安全补丁持续在不同平台上发布，但现今大部分补丁只针对Windows XP发布。

===间谍软件·广告软件与Windows XP SP2===
[[间谍软件|间谍软件]]与[[广告软件|广告软件]]，如同其他的[[恶意软件|恶意软件]]一样，通常把目标对准Windows/Internet Explorer为基础的作业系统。较旧的间谍软件对系统的危害已经因为Windows XP SP2的安全增强而有所缓解，但对IE新型的攻击会在SP2上安装间谍软件。微软不建议在已经感染间谍软件的系统上安装SP2，因为这可能导致不能自举：

{{cquote|於安裝SP2前，清除間諜軟件及廣告軟件失敗可導致問題產生及在一些情形中，你會難以重新啟動電腦。你甚至可能不知道間諜軟件或廣告軟件已經於你的系統上安裝。一些間諜軟件或廣告軟件可能不會與SP2構成嚴重問題，但在安裝SP2前，最好執行間諜軟件及廣告軟件的移除程式。{{noteTag|http://www.microsoft.com/windowsxp/using/security/expert/russel_installsp2.mspx}}}}

視已安裝的間碟軟件而定，在SP2更新準備工作中，我們可透過反間諜工具移除間碟軟件或在一些嚴重情形中，需要手動修改[[登錄檔|登錄檔]]（Windows Registry）。 然而，保安專家普遍建議安裝Service Pack 2。

==對其不支援開放標準的批評==
[[File:Box-model-bug.png|right]] in quirks mode]]

在1990年代的[[瀏覽器戰爭|瀏覽器戰爭]]時代，Internet Explorer與[[Netscape_Navigator|Netscape Navigator]]都不得不致力於在瀏覽器中添加非標準功能。這與近來以[[web標準|web標準]]設計的瀏覽器形成鮮明對比。在版本號5後，IE的[[Trident_(排版引擎)|Trident]][[渲染引擎|渲染引擎]]幾乎沒有進行過重大修改。結果在2005年，IE在支持標準上已經大大落後。

雖然每一個版本的IE都會改善基本支援，包括在版本6中引採用的「符合標準模式」，其中用來建立網頁（[[HTML|HTML]]和[[串接樣式表|CSS]]）的核心標準卻仍然是以不完全且不正確的方式來實作的。舉例來說，它不支援<tt><nowiki><abbr></nowiki></tt> 元素，但這是HTML 4.01 標準的一部份，而且它對CSS1標準中的float-margin部分的實作有缺陷。[[Internet_Explorer盒模型错误|Internet Explorer盒模型错误]]是Internet Explorer對CSS標準的實作中，最為人熟知的缺陷之一。

由於它在市場上的主導地位，使得某些網頁開發人員只用Internet Explorer來測試他們的網站。某些開發人員也使用Internet Explorer所提供的非標準擴充套件。這導致網頁無法被其他瀏覽器正確地解讀。最糟糕的情況下，它可能會阻擋其他瀏覽器的使用者存取這些開發人員所建立的網站。

雖然[[Netscape|Netscape]]已經停止開發[[Netscape_Navigator|Netscape Navigator]]，微軟的Internet Explorer因而取得了非常大的市場佔有率，而後開發[[Netscape_Navigator|Netscape Navigator]]的程式員與一些不滿Internet Explorer的技術人員創立了[[Mozilla基金會|Mozilla組織]]並以[[Netscape_Navigator|Netscape Navigator]]作基礎開發了[[Mozilla_Application_Suite|Mozilla Application Suite]]與[[Mozilla_Firefox|Mozilla Firefox]]。

===圖像標準===
由於IE不支援[[PNG|PNG]]圖像的[[阿爾法通道|Alpha 通道]]，導致PNG[[圖像格式|圖像格式]]在网上使用率的減少。雖然只是一個可選的特性，[[阿爾法通道|Alpha 通道]]卻是把PNG與其他像[[GIF|GIF]]或者[[JPEG|JPEG]]這樣的格式相區別的一個特色。 在Internet瀏覽器中，透明的部分的形象將被顯示作為灰色，白或者其他顏色。

隔行或漸進顯示對於過去大量使用的[[撥號上網|撥號上網]]而[[頻寬|頻寬]]非常有限的用戶非常有用。不過，Internet Explorer的圖像不支持於未完成下載時開啟。但由於[[宽带因特网连接|宽带因特网连接]]的引進，現在這問題已沒那麼重要。

===XHTML===
=== HTTP與MIME ===
不像其他瀏覽器，Internet Explorer不允許MIME在Content-Type[[信頭|信頭]]段中定義MIME類型。比如一個純文本格式的檔內包含了HTML樣式的標記就會被識別為HTML文檔，而不是純文本文檔。但在這種情況下，可以通過手動修改註冊表的方式強行改變執行行為。

===JavaScript與DOM===
微軟擴展了原先網景的JavaScript並專稱其為JScript，JScript是Internet Explorer的缺省腳本語言。與Netscape's JavaScript有相似的implementation, JScript supports the full specification of [[ECMAScript|ECMAScript]], the only standardised scripting language on the Web.

最大的不同在於與[[JScript|JScript]]綁定的[[文档对象模型|文档对象模型]](DOM)。

===Unicode===
{{main|Unicode與HTML}}

Internet Explorer對多語言文本支援[[Unicode|Unicode]]標準，因此其理論上有能力顯示任何已經安裝[[字體|字體]]的[[圖像|字元]]。但實際上，Internet Explorer不會對混和Unicode文本自動選擇字體。這種情況下字元可能會以一個空格結束或顯示為問號。

網頁設計者必須猜測在用戶電腦上顯示哪種字體最為合適，如果需要改變就需要對每個Unicode塊進行手動改變。而對其他瀏覽器卻可以自動完成這個操作。

以Unicode之中的英文的音標為例，當網頁中，欲顯示的音標字串的前後有使用<nowiki><font name="Lucida Sans Uinicode"></nowiki>與<nowiki></font></nowiki>所包起來時。IE6以前的版本，無法正常顯示出英文的音標。但IE7則已修正了此Bug。

==其他批评==
随着版本的更新，Internet Explorer的下载大小也显著增大。对于[http://www.microsoft.com/windows/ie/downloads/critical/ie6sp1/ Internet Explorer 6 Service Pack 1]（包括[[Outlook_Express|Outlook Express]]）来说，其典型安装时的下载大小已经接近25[[megabyte|MB]]s。它的大小从11[[megabyte|MB]]s（最简安装）到75[[megabyte|MB]]s（完全安装）不等。这大大超过了一另一些网络浏览套装（Internet suites）的大小，例如（基于Windows installer）Opera 8.0 (3.6MB)、Mozilla Suite 1.7.8 (11MB)、Mozilla Firefox 1.5.0.6(4.9MB)和SeaMonkey 1.0.4(12MB)。<!--Internet suites are used as downloading IE typically also download OE. Standalone browsers should not be listed here to be fair.-->

一个较小但似乎很有意思的批评是软件名称中[[Internet|Internet]]这个单词的使用。严格地说，Internet Explorer是为万维网（[[World_Wide_Web|World Wide Web]]）而不是为整个包含了[[電郵|電郵]], [[Usenet|Usenet]], [[telnet|telnet]]和[[Internet_Relay_Chat|IRC]]等的因特网（[[Internet|Internet]]）而设计的。由于这种以因特网（Internet）来代替万维网（World Wide Web）的误导性使用，许多对因特网没有足够了解的用户可能会认为使用Internet Explorer是进入因特网的唯一途径。

==註解==
<!-- Dead note "PNGAlphaChannelIssue": [http://support.microsoft.com/kb/294714/en PNG Files Do Not Show Transparency in Internet Explorer], [[February_13|February 13]], 2005. -->
<!-- Dead note "PNGAlphaChannelWorkaround": [http://blogs.msdn.com/dmassy/archive/2004/08/05/209428.aspx Transparent PNG Support], [[May_12|May 12]], 2005. -->
<!-- Dead note "PNGDisappear": [http://support.microsoft.com/kb/822071/en Cannot View Some PNG Images], [[May_12|May 12]], 2005. -->
<!-- Dead note "ProgressiveJPEGIssue": [http://php.oregonstate.edu/manual/en/function.imageinterlace.php#41582 PHP: imageinterlace], [[May_12|May 12]], 2005. -->
<!-- Dead note "ForceIEToShowXHTML": [http://lists.w3.org/Archives/Public/www-html/2002Dec/0176.html Forcing IE to Show Application/xhtml+xml pages], [[May_12|May 12]], 2005. -->
<!-- Dead note "SendingXHTMLAsHTMLConsideredHarmful": [http://hixie.ch/advocacy/xhtml Sending XHTML as text/html Considered Harmful], [[February_13|February 13]], 2005. -->
<!-- Dead note "IE7Hack": [http://dean.edwards.name/IE7/ /IE7/], [[May_12|May 12]], 2005. -->
<div class="references-small">{{noteFoot}}</div>

==參考資料==

{{reflist}}
<div class="references-small">{{refFoot}}</div>

==参见==
*[[Internet_Explorer|Internet Explorer]]
*[[Common_criticisms_of_Microsoft|Common criticisms of Microsoft]]

==外部链接==
*[http://secunia.com/product/11/ Secunia - Vulnerability Report - Microsoft Internet Explorer 6.x]
*[http://www.positioniseverything.net/explorer.html Explorer Exposed!]
*[http://www.positioniseverything.net/ie-primer.html Internet Explorer vs. the Standards]
*[http://www.tbray.org/ongoing/When/200x/2003/07/17/BrowserDream The Door Is Ajar] — An "anti-IE" article by a [[Sun_Microsystems|Sun Microsystems]] technology director [[Tim_Bray|Tim Bray]].
*[http://www.lockergnome.com/news/2004/06/15/why-you-should-dump-internet-explorer/ Why You Should Dump Internet Explorer] — An "anti-IE" article by a [[MCSE|MCSE]] Daniel Miessler.
*[http://www.stopie.com StopIE] — An "anti-IE" campaign by a web developer Stephen O'Brien
*[http://www.browsehappy.com Browse Happy] — An "anti-IE" campaign by the Web Standards Project
*[https://web.archive.org/web/20050723082947/http://jgwebber.blogspot.com/2005/05/drip-ie-leak-detector.html Drip] — A utility to detect and measure IE's memory leaks.

{{Internet Explorer}}
[[Category:Internet_Explorer|Internet Explorer]]
[[Category:針對微軟的批評與爭議|Category:針對微軟的批評與爭議]]

[[en:Criticism_of_Internet_Explorer|en:Criticism of Internet Explorer]]