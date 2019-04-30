{{NoteTA
|G1=IT
}}
{{校对翻译}}
{{更新|1=|time=2016-12-15T22:51:48+00:00}}
'''复合TCP'''（{{lang-en|'''Compound TCP'''}}，简称'''CTCP'''）是[[微软|微软]]自[[Windows_Vista|Windows Vista]]及Window Server 2008开始在[[传输控制协议|TCP]]栈中引入的一个算法。它旨在积极调整发送方的{{tsl|en|Congestion window|拥塞窗口}}，以在不损害{{tsl|en|Fairness measure||公平原则}}的基础上（[[高速TCP|HSTCP]]同样遵循）优化TCP对高[[带宽时延积|带宽时延积]]连接的表现。该方案还可在Linux、Windows XP以及Windows Server 2003上使用。<ref>[http://support.microsoft.com/kb/949316 A hotfix that adds Compound TCP (CTCP) support to computers that are running Windows Server 2003 or Windows XP is available]</ref>

== 操作原理 ==
类似{{tsl|en|FAST TCP}}和{{tsl|en|TCP Vegas}}，复合TCP采用估算排队延迟来度量拥塞；如果排队延迟小，则假设链路上没有拥塞，并迅速增加其速率。但不同于FAST和Vegas，它不追求维护恒定数量的数据包队列。

复核TCP维护两个拥塞窗口：一个常规的{{tsl|en|Additive increase/multiplicative decrease||AIMD}}窗口，以及一个基于延迟的窗口。最终实际使用的滑动窗口大小是这两个窗口的和。AIMD窗口与{{tsl|en|TCP Reno}}的增加方式相同。如果延迟小，基于延迟的窗口将迅速增加以提高网络的利用率。一旦经历了排队，延迟窗口将逐渐减小以补偿增加的AIMD窗口。这样的目的是保持两者的总和大致恒定，使算法估计[[带宽时延积|带宽时延积]]的路径。具体来说，当检测到排队时，基于时延的窗口因估计的队列大小而减少，以避免FAST和Vegas报告的“持续拥塞”。因此，不同于{{tsl|en|TCP-Illinois}}及其前身{{tsl|en|TCP Africa}}，复合TCP可以减少其窗口以避免响应延迟。这增加了它对于Reno的公平性。{{Fact|date=April 2013}}

== 支持平台 ==

=== Windows 2003和XP x64 ===
有一个热修复补丁可以为64位Windows XP和Windows Server 2003添加CTCP支持。<ref name="CTCPDownlevel">[http://support.microsoft.com/kb/949316 A hotfix that adds Compound TCP (CTCP) support to computers that are running Windows Server 2003 or Windows XP is available]</ref>

将下列注册表键设为'''1'''则为启用，设为'''0'''则为禁用：
 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\TCPCongestionControl

=== Windows Vista/2008/7 ===
CTCP在Beta版的Windows Server 2008中被默认启用，在Windows Vista和7上被默认禁用。 

可以使用下列命令启用CTCP：
 netsh interface tcp set global congestionprovider=ctcp 
下列命令禁用CTCP：
 netsh interface tcp set global congestionprovider=none
显示当前的CTCP设置：
 netsh interface tcp show global
“附加拥塞控制提供程序”（Add-On Congestion Control Provider）参数为“none”表示CTCP已禁用，为“ctcp”表示它已启用。

=== Windows 8 / 8.1 ===
Windows 8/8.1需使用[[Windows_PowerShell|PowerShell]]命令（见 https://web.archive.org/web/20131029184023/http://technet.microsoft.com/en-us/library/hh826132.aspx%3Cnowiki/%3E%EF%BC%89%E4%BF%AE%E6%94%B9%E6%8B%A5%E5%A1%9E%E6%8E%A7%E5%88%B6%E7%AE%97%E6%B3%95。

=== Linux ===
除了Windows支持，CTCP还被Angelo P. Castellani移植到了[[Linux|Linux]]。Caltech开发的一个补丁包含了CTCP's TUning By Emulation (TUBE)。此补丁由于[[软件专利|软件专利]]而仅供研究人员使用。该模块已不兼容内核2.6.17及以上版本，将由于内核API变更而编译失败。<ref>{{cite web |url=http://netlab.caltech.edu/lachlan/ctcp/ |title=存档副本 |accessdate=2011-01-04 |0=2008-08-02 |deadurl=yes |archiveurl=https://web.archive.org/web/20080802222857/http://netlab.caltech.edu/lachlan/ctcp/ |archivedate=2008-08-02 }}</ref>

== 参见 ==
* {{tsl|en|TCP congestion avoidance algorithm|TCP拥塞避免算法}}
* [[显式拥塞通知|显式拥塞通知]]
* [[传输控制协议#發展過程|传输控制协议（TCP） - 发展过程]]

== 参考资料 ==
{{reflist|2}}

== 外部链接 ==
* [http://tools.ietf.org/html/draft-sridharan-tcpm-ctcp Compound TCP Internet-Draft]
* [http://research.microsoft.com/research/pubs/view.aspx?type=Technical%20Report&id=940 "A Compound TCP Approach for High-speed and Long Distance Networks"] July 2005
* [https://web.archive.org/web/20060506095853/http://www.microsoft.com/technet/community/columns/cableguy/cg1105.mspx Performance Enhancements in the Next Generation TCP/IP Stack], The Cable Guy
* [http://research.microsoft.com/en-us/projects/ctcp/ The Compound TCP for High-speed and Long Distance Networks], Microsoft Research publication
* [http://www.networkperformancedaily.com/2006/12/vistas_tcpip_promises_and_peri.html Vista's TCP/IP Promises and Perils], Article at Network Performance Daily
* [https://web.archive.org/web/20080802222857/http://netlab.caltech.edu/lachlan/ctcp/ Caltech's Compound TCP patch for Linux]
* Enabling CTCP on 2003/XP x64: [http://blog.tiensivu.com/aaron/archives/1537-KB-949316-Add-Compound-TCP-CTCP-support-to-XP-and-Server-2003.html],[http://blog.tiensivu.com/aaron/archives/901-Compound-TCP-congestion-control-algorithm-in-Vista-can-make-lossyhigh-latency-connections-behave-better..html]
* [http://www.hamilton.ie/net/delay_tests_final.pdf Report on experimental evaluation of Compound TCP] [http://www.hamilton.ie Hamilton Institute] and [http://netlab.caltech.edu Caltech], March 2008.
* [http://www.comp.nus.edu.sg/~wuxiucha/research/reactive/publication/ctcp_study.pdf A simulation-based study of Compound TCP] {{Dead link|date=May 2016}} July 14, 2008
* [http://blog.sina.com.cn/s/blog_4caedc7a0100gd8f.html CTCP进驻Windows的故事]，[[微软亚洲研究院|微软亚洲研究院]]的博客，2009年10月27日 {{zh-cn}}

[[Category:TCP拥塞控制|Category:TCP拥塞控制]]