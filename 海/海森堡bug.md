{{校对翻译}}
{{NoteTA
|G1=IT
}}
在[[程序设计|程序设计]]术语中，'''海森堡bug'''（{{lang-en|'''heisenbug'''}}）是指在尝试研究它时似乎会消失或者改变行为的[[程序错误|bug]]（程序错误）。<ref name="jarhei">{{Cite web|url=http://catb.org/jargon/html/H/heisenbug.html|title=The Jargon File: heisenbug}}</ref><ref>{{cite journal|title=飘忽无定的海森堡BUG教你搞定幽灵问题|journal=程序员：游戏创造|date=2008年|issue=4|url=http://www.cqvip.com/qk/87226a/200804/27041918.html|accessdate=2017-04-09}}</ref><ref>{{cite web|title=Bug的类型|url=http://www.vaikan.com/types-of-bugs/|website=外刊IT评论|accessdate=2017-04-09}}</ref>该词汇是物理学家[[维尔纳·海森堡|维尔纳·海森堡]]名字的[[双关语|双关语]]，他最先断言了[[量子力学|量子力学]]的[[观察者效应|观察者效应]]——观察系统的行为不可避免地将改变其状态。电子学中的传统用语则是{{tsl|en|Probe effect|探针效应}}，指连接一个{{tsl|en|Test probe|测试探针}}到设备将改变其行为。

类似的词语有'''玻尔bug'''（'''bohrbug'''）、'''曼德博bug'''（'''mandelbug'''）<ref name="jarman">{{Cite web|url=http://catb.org/jargon/html/M/mandelbug.html|title=The Jargon File: Mandelbug|accessdate=2013-09-05|publisher=Catb.org}}</ref><ref>Raymond, Eric S.; [https://books.google.com/books?id=g80P_4v4QbIC&pg=PA295&dq=mandelbug ''The New Hacker's Dictionary''], 3rd edition, 1996</ref><ref>[//en.wikipedia.org/wiki/Arthur_C._Clarke Clarke, Arthur C.], [http://www.google.ca/search?tbm=bks&q=%22The+Mandelbug.+Get+Ada+to+explain+it+to+you+someday.%22 ''The Ghost from the Grand Banks''], Bantam Books, 1990</ref>和'''薛定谔bug'''（'''schrödinbug'''）<ref name="jarsch">{{Cite web|url=http://www.catb.org/jargon/html/S/schroedinbug.html|title=The Jargon File: Schroedinbug|accessdate=2013-09-05|publisher=Catb.org}}</ref><ref>Raymond, Eric S.; [https://books.google.com/books?id=g80P_4v4QbIC&pg=PA397&dq=schroedinbug ''The New Hacker's Dictionary''], 3rd edition, 1996</ref>，它们偶尔被用于指代其他类型的非寻常软件缺陷，但通常以开玩笑的心态使用。<ref>The following article investigates the various definitions of bohrbug, mandelbug and heisenbug proposed in the literature, as well as the statements made about the relationships between these fault types: Grottke, Michael; and Trivedi, Kishor S.; ''Software Faults, Software Aging and Software Rejuvenation'', Journal of the Reliability Engineering Association of Japan, Vol. 27, No. 7, pp. 425-438, 2005.</ref><ref>Grottke, Michael; and Trivedi, Kishor S.; [https://web.archive.org/web/20100327174716/http://www.computer.org/portal/web/csdl/doi/10.1109/MC.2007.55 ''Fighting Bugs: Remove, Retry, Replicate, and Rejuvenate''], IEEE Computer vol. 40, no. 2 (February 2007), pp. 107-109</ref><ref>A February 2012 Google Books search returns about 70 hits for "schroedinbug", 100 for "mandelbug", 400 for "bohrbug" or "heisenbug".</ref>

== 例子 ==
之所以会出现海森堡bug，是因为通常的调试手段，诸如插入[[I/O|输出语句]]或是挂接[[调试工具|调试器]]，往往会修改程序代码，或是更改[[变量|变量]]的[[内存地址|内存地址]]，或是改变其执行时间。这都可能影响程序的行为。如果正好影响到了bug，就有可能产生海森堡bug。

海森堡bug的一个常见情况是，bug只在打开[[編譯器|編譯器]]优化时出现，而关闭优化再编译程序（使用调试器时通常如此）则bug消失。一些在优化后的程序中通常会放入[[寄存器|寄存器]]的值，在调试状态下会放入到主内存。这可能会影响[[浮点数|浮点数]]比较的结果，因为内存中的值可能比寄存器中的值有更小的范围和精度{{fact}}。与此类似，[[C语言|C]]、[[C++|C++]]等语言中使用的运行时[[斷言_(程式)|断言]]的副作用可能导致海森堡bug，因为当生产环境的代码使用<code>[[Assert.h|NDEBUG]]</code>宏关闭断言后，测试表达式不会被執行（eval）。

海森堡bug的其他常见原因是使用未初始化的变量的值（在调试模式下此变量的值可能不同，或者调试系统自动将其初始化），或者使用了{{tsl|en|Fandango on core||无效的}}[[指標_(電腦科學)|指標]]（调试时可能指向了不同的地方）。调试器也经常提供[[断点|监视器]]或其他用户界面，它们也可能导致执行额外的[[源代码|源代码]]（例如属性存取器），从而改变程序的状态。<ref>[http://debuggers.co/java/enterprise/2014/06/17/Kyle-Harr.html "Java toString() override with initialization as a side effect"] {{webarchive|url=https://web.archive.org/web/20141230005029/http://debuggers.co/java/enterprise/2014/06/17/Kyle-Harr.html |date=2014-12-30 }}</ref>

时间也可能是海森堡bug的一个因素，尤其是对于[[多线程|多线程]]应用程序而言。在调试器控制下执行的程序与正常执行的程序在运行时间上会有差异。使用调试器进行逐行单步调试时，时间敏感的bug（例如[[競爭危害|競爭危害]]）可能不会发生。当行为涉及到与不在调试器控制下的实体进行交互时（例如两台计算机之间的网络数据包处理），则更是如此。

海森堡bug可以被视为{{tsl|en|Observer effect (information technology)|信息技术中的观察者效应}}的一个实例。沮丧的程序员可能会幽默或无奈地指责一个海森堡bug是由于[[月相|月相]]<ref>CATB.org, [http://www.catb.org/jargon/html/P/phase-of-the-moon.html "phase of the moon"]</ref>或其他因素，或者猜测它是因为[[Α粒子|Α粒子]]或[[宇宙線|宇宙線]]影响[[计算机硬件|计算机硬件]]而导致的[[軟性錯誤|軟性錯誤]]所致（如果只发生了一次）。

== 相关词汇 ==
词汇“'''bohrbug'''”是海森堡bug的一个反义词，它指良好、稳固的bug。就像确定性的[[玻尔模型|玻尔模型]]一样，它们不改变自己的行为，并且相对容易被检测到。<ref>Goshgarian, Gary; ''Exploring Language'', HarperCollins College Publishers, 1995</ref><ref>"Such transient software failures have been given the whimsical name “Heisenbug” because they disappear when reexamined. </ref>

'''曼德博bug'''（mandelbug，名字取自[[本華·曼德博|本華·曼德博]]的[[曼德博集合|曼德博集合]]）是原因极其复杂而很难修复的bug，其行为看上去[[混沌理论|混乱]]甚至存在[[确定性模型|不确定性]]。它也指程序员检查代码、修复它们时会发现更多bug的bug。{{Fact|date=August 2016}}

'''薛定谔bug'''（schrödinbug，名字取自[[埃尔温·薛定谔|埃尔温·薛定谔]]及他的[[薛定谔猫|薛定谔猫]]）是程序员发现一个永远不应该被触发的情况发生的bug。{{Fact|date=August 2016}}

'''兴登堡bug'''（hindenbug，<ref>{{Cite web|url=http://c2.com/cgi/wiki?HindenBug|title=Hinden Bug}}</ref>{{Better source|date=August 2016}}名字取自[[興登堡號空難|興登堡號空難]]）是具有灾难性行为的bug。

== 词汇历史 ==
该词汇在1985年被[[詹姆斯·尼古拉·格雷|詹姆斯·尼古拉·格雷]]在一篇关于软件故障的论文中使用<ref>{{Cite web|url=http://citeseer.ist.psu.edu/viewdoc/summary?doi=10.1.1.59.6561 <!-- http://www.hpl.hp.com/techreports/tandem/TR-85.7.pdf -->|title=Why Do Computers Stop And What Can Be Done About It?|last=Gray|first=Jim|year=1985|work=Technical Report 85.7|publisher=Tandem Computers}}</ref>，并也在1986年由Jonathan Clark和Zhahai Stewart在邮件列表（之后的[[Usenet|Usenet]]新闻组）{{tsl|en|comp.risks}}中使用。<ref name="risks">(16 December 1986) [https://groups.google.com/group/mod.risks/browse_thread/thread/cc68771824a79d3f RISKS DIGEST 4.30] - (23 December 1986) [https://groups.google.com/group/mod.risks/browse_thread/thread/83a6ad844eda93e0/5e061e6da0c2dbfc?lnk=st&q=heisenbug&rnum=896#5e061e6da0c2dbfc RISKS DIGEST 4.34], moderated by [//en.wikipedia.org/wiki/Peter_G._Neumann Peter G. Neumann]</ref>

供职于[[IBM|IBM]]的研究员{{tsl|en|Bruce Lindsay (IBM Fellow)|Bruce Lindsay}}在2004年的{{tsl|en|ACM Queue}}采访中确认，Heisenbug被最初定义时他在场。<ref>{{Cite web|url=http://queue.acm.org/detail.cfm?id=1036486|title="A Conversation with Bruce Lindsay", ACM Queue vol. 2, no. 8 - November 2004|accessdate=2013-09-05|publisher=Queue.acm.org}}</ref>{{what}}

它于1983年在[[计算机协会|ACM]]的出版物中有更早的出现。<ref>''Proceedings of the ACM SIGSOFT/SIGPLAN Software Engineering Symposium on High-Level Debugging, Pacific Grove, California, March 20–23, 1983'', Association for Computing Machinery, 1983, [http://www.google.ca/search?tbm=bks&q=an+instance+of+such+a+bug+was+called+a+%22Heisenbug%22+by+one+participant Google Books search]:
</ref>

== 解决 ==
Heisenbug通常需要非常仔细地调试才能解决。如果能找出出错代码的近似位置则能更快地找出。在那个位置附近可以检查相关上下文和分析进程转储来寻找解决方案。

另一种方法是检查日志，尤其是由[[lint|lint]]或类lint工具产生的日志。

对于长期、持久的海森堡bug，它可能需要使用诸如[[抽象释义|抽象释义]]等[[靜態程序分析|靜態程序分析]]技术来确定其原因。

== 参见 ==
* [[货物崇拜编程|货物崇拜编程]]
*[[小黄鸭调试法|小黄鸭调试法]]
* {{tsl|en|CHESS model checker|CHESS模型检查器}}—一种用于检测和重现Heisenbug的工具（Windows）
* {{tsl|en|Memory debugger|内存调试器}}
* {{tsl|en|Jinx Debugger|Jinx调试器}}—一种自动探测可能导致Heisenbug的工具。

== 参考资料 ==
{{Reflist|30em}}

== 外部链接 ==
* [http://sourceware.org/gdb/talks/esc-west-1999/ The Heisenberg Debugging Technology]{{en}}
* [https://web.archive.org/web/20101216173357/http://ftp.sunet.se/jargon/html/magic-story.html A Story About Magic]{{en}}
* [https://bugs.launchpad.net/ubuntu/+source/cupsys/+bug/255161 OpenOffice won't print on Tuesdays]{{en}}，一个令人着迷的海森堡bug，花费了将近九个月的时间来解决。
* [http://www.infoq.com/cn/articles/exterminating-heisenbugs 消灭神出鬼没的Heisenbug]{{zh-cn}}

[[Category:调试|Category:调试]]
[[Category:程式錯誤|Category:程式錯誤]]
[[Category:软件测试|Category:软件测试]]