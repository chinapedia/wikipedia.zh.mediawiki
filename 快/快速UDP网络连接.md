{{copyedit|time=2019-04-11T02:51:36+00:00}}
{{noteTA|G1=IT}}
{{网络协议}}

{{refimprove|time=2018-12-14T17:31:40+00:00}}
{{expand|time=2018-12-14T17:31:40+00:00}}

'''快速UDP網路連-{zh-hans:接;zh-hant:線}-'''（{{lang-en|'''Q'''uick '''U'''DP '''I'''nternet '''C'''onnections}}，缩写：'''QUIC'''<ref>[https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=%20&arnumber=7867726 Innovating Transport with QUIC: Design Approaches and Research Challenges]，2017</ref>）是一種實驗性的[[傳輸層|傳輸層]][[網路傳輸協定|網路傳輸協定]]，由[[Google|Google]]開發，在2013年實作。QUIC使用[[用户数据报协议|UDP]]协议，它在兩個端點間建立連線，且支援[[多路複用|多路複用]]連線。<ref>[https://docs.google.com/document/d/1RNHkx_VvKWyWg6Lr8SZ-saqsQx7rFV-ev2jRFUoVD34/mobilebasic?pli=1 MULTIPLEXED STREAM TRANSPORT OVER UDP]，Google</ref>在設計之初，QUIC希望能夠提供等同於[[傳輸層安全協議|SSL/TLS]]層級的網路安全保護，減少資料傳輸及建立連線時的延遲時間，雙向控制頻寬，以避免網路擁塞。Google希望使用這個協定來取代[[传输控制协议|TCP]]協定，使網頁傳輸速度加快，計劃將QUIC提交至網際網路工程任務小組（[[IETF|IETF]]），讓它成為下一代的正式網路規範<ref>[http://www.techbang.com/posts/23287-google-quic-technology-so-online-fast Google推動QUIC新協定，讓網頁瀏覽、影片播放更快速]，T客邦，2015-04-22</ref>。2015 年 6 月，QUIC的{{link-en|网络草案|Internet Draft}}被正式提交至[[互联网工程任务组|互联网工程任务组]]。<ref>{{Cite web|url=https://www.ietf.org/mail-archive/web/i-d-announce/current/msg66052.html|title=I-D Action: draft-tsvwg-quic-protocol-00.txt|accessdate=2018-12-10|work=www.ietf.org}}</ref>2018 年 10 月，互联网工程任务组 HTTP 及 QUIC 工作小组正式将基于 QUIC 协议的 HTTP ({{Lang-en|HTTP over QUIC}}) 重命名为 [[HTTP/3|HTTP/3]] 以为确立下一代规范做准备。<ref>{{Cite web|url=https://www.zdnet.com/article/http-over-quic-to-be-renamed-http3/|title=HTTP-over-QUIC to be renamed HTTP/3|accessdate=2018-12-10|last=Cimpanu|first=Catalin|work=ZDNet|language=en}}</ref>

== 介绍 ==
QUIC旨在提供几乎等同于TCP连接的[[可靠性_(计算机网络)|可靠性]]，但[[來回通訊延遲|延迟]]大大减少。它主要通过两个理解[[HTTP|HTTP]]流量的行为来实现这一点。<ref name='ARSnext'>{{cite web|title=The next version of HTTP won’t be using TCP|first=Peter|last=Bright|url=https://arstechnica.com/gadgets/2018/11/the-next-version-of-http-wont-be-using-tcp/|website=Arstechnica|date=12 November 2018}}</ref>

第一个变化是在连接建立期间大大减少{{Link-en|开销|Overhead (computing)}}。由于大多数HTTP连接都需要[[TLS|TLS]]，因此QUIC使协商[[傳輸層安全性協定#密钥交换和密钥协商|密钥]]和支持的协议成为初始[[握手_(技术)|握手]]过程的一部分。
当客户端打开连接时，[[服务器|服务器]]响应的[[数据包|数据包]]包括将来的数据包[[加密|加密]]所需的数据。这消除了TCP上的先连接并通过附加数据包协商安全协议的需要。其他协议可以以相同的方式进行服务，并将多个步骤组合到一个请求中。
然后，这些数据既可用于初始设置中的后续请求，也可用于未来的请求。<ref name='ARSnext'/>

QUIC使用UDP协议作为其基础，不包括[[丢包|丢失]]恢复。相反，每个QUIC流是单独控制的，并且在QUIC级别而不是UDP级别重传丢失的数据。这意味着如果在一个流中发生错误，[[协议栈|协议栈]]仍然可以独立地继续为其他流提供服务。
这在提高易出错链路的性能方面非常有用，因为在大多数情况下TCP协议通知数据包丢失或损坏之前可能会收到大量的正常数据，但是在纠正错误之前其他的正常请求都会等待甚至重发。
QUIC在修复单个流时可以自由处理其他数据，也就是说即使一个请求发生了错误也不会影响到其他的请求。<ref>{{cite web|last1=Behr|first1=Michael|last2=Swett|first2=Ian|title=Introducing QUIC support for HTTPS load balancing |url=https://cloudplatform.googleblog.com/2018/06/Introducing-QUIC-support-for-HTTPS-load-balancing.html|website=Google Cloud Platform Blog |publisher=Google|accessdate=16 June 2018}}</ref>

QUIC包括许多其他更普通的更改，这些更改也可以优化整体延迟和[[吞吐量|吞吐量]]。例如，每个数据包是单独加密的，因此加密数据时不需要等待部分数据包。
在TCP下通常不可能这样做，其中加密记录在[[字节流|字节流]]中，并且协议栈不知道该流中的更高层边界。这些可以由运行在更上层的协议进行协商，但QUIC旨在通过单个握手过程完成这些。<ref name='IETF QUIC Intro'>{{cite web|url=http://www.ietf.org/proceedings/88/slides/slides-88-tsvarea-10.pdf|title=QUIC: IETF-88 TSV Area Presentation|publisher=Jim Roskind, Google|accessdate=2013-11-07}}</ref>

QUIC的另一个目标是提高网络切换期间的性能，例如当移动设备的用户从[[Wi-Fi|WiFi热点]]切换到[[移动网络|移动网络]]时发生的情况。
当这发生在TCP上时，一个冗长的过程开始了：每个现有连接一个接一个地{{Link-en|超时|Timeout (computing)}}，然后根据需要重新建立。期间存在较高延迟，因为新连接需要等待旧连接超时后才会建立。
为解决此问题，QUIC包含一个连接标识符，该标识符唯一地标识客户端与服务器之间的连接，而无论源[[IP地址|IP地址]]是什么。这样只需发送一个包含此ID的数据包即可重新建立连接，因为即使用户的IP地址发生变化，原始连接ID仍然有效。<ref name='QUICoverview'>{{cite web|url=https://docs.google.com/document/d/1gY9-YNDNAB1eip-RTPbqphgySwSNSDHLq9D5Bty4FSU/edit|title=QUIC at 10,000 feet|website=Chromium}}</ref>

QUIC在{{Link-en|应用程序空间|Application domain}}中实现，而不是在[[内核|操作系统内核]]中实现。当数据在应用程序之间移动时，这通常会由于上下文切换而调用额外的开销。
但是在QUIC下协议栈旨在由单个应用程序使用，每个应用程序使用QUIC在UDP上托管自己的连接。最终差异可能非常小，因为整个[[HTTP/2|HTTP/2]]堆栈的大部分已经存在于应用程序（或更常见的库）中。
将剩余部分放在这些库中，基本上是纠错，对HTTP/2堆栈的大小或整体复杂性几乎没有影响。<ref name='IETF QUIC Intro'/>

QUIC允许更容易地进行未来更改，因为它不需要更改内核就可以进行更新。
QUIC的长期目标之一是添加[[前向纠错|前向纠错]]和改进的[[拥塞控制|拥塞控制]]。<ref name='QUICoverview'/>

关于从TCP迁移到UDP的一个问题是TCP被广泛采用，并且互联网基础设施中的许多中间设备被调整为UDP速率限制甚至阻止UDP。
Google进行了一些探索性实验来描述这一点，发现只有少数连接存在此问题。<ref name='QUIC Design Doc'>{{cite web|url=https://docs.google.com/document/d/1RNHkx_VvKWyWg6Lr8SZ-saqsQx7rFV-ev2jRFUoVD34/edit|title=QUIC: Design Document and Specification Rationale|publisher=Jim Roskind, Chromium Contributor}}</ref>所以Chromium的网络堆栈同时打开QUIC和传统TCP连接，并在QUIC连接失败时以零延迟回退到TCP连接。<ref>{{cite web|url=https://quicwg.org/ops-drafts/draft-ietf-quic-applicability.html|title=Applicability of the QUIC Transport Protocol|date=22 October 2018|website=IETF Network Working Group}}</ref>

=== gGUIC与iQUIC ===
由Google创建并以QUIC的名称提交给IETF的协议与随后在IETF中创建的QUIC完全不同（尽管名称相同）。
最初的Google QUIC（也称为gQUIC）严格来说是通过加密UDP发送HTTP/2帧的协议，而IETF创建的QUIC是通用传输协议，也就是说HTTP以外的其他协议（如[[SMTP|SMTP]]、[[DNS|DNS]]、[[Secure_Shell|SSH]]、[[Telnet|Telnet]]、[[網路時間協定|NTP]]）也可以使用它。重要的是要注意并记住其差异。
自2012年以来，Google在其服务及Chrome中使用的QUIC版本（直到2019年2月）为Google QUIC。随着时间的推移，它正在逐渐变得类似于IETF QUIC（也称为iQUIC）。

== 实现 ==
=== 客户端 ===
[[Google_Chrome|Google Chrome]]于2012年开始开发QUIC协议并且于[[Chromium|Chromium]]版本 29 (2013年8月20日释出) 发布。QUIC协议在当前Chrome版本中被默认开启，活跃的会话列表在<code>''chrome://net-internals/#quic''</code>中可见。

=== 服务端 ===
截至2017年，有三种活跃维护中的实现。谷歌的服务器及谷歌发布的[https://code.google.com/p/chromium/codesearch#chromium/src/net/tools/quic/quic_server.cc 原型服务器]使用Go语言编写的[https://github.com/lucas-clemente/quic-go quic-go]及[[Caddy|Caddy]]的试验性QUIC支持。在2017年7月11日，LiteSpeed科技正式在他们的[[负载均衡|负载均衡]]（[https://www.litespeedtech.com/products/litespeed-web-adc WebADC]）及 LiteSpeed 服务器中支持QUIC。截止 17 年 12 月， 97.5%的使用 QUIC 协议的网站在 LiteSpeed 服务器中运行<ref>{{Cite web|url=https://w3techs.com/technologies/segmentation/ce-quic/web_server|title=Distribution of Web Servers among websites that use QUIC|accessdate=2018-12-10|work=w3techs.com}}</ref>。

另有几种不再维护的社区产品，基于Chromium实现并且减少使用依赖的[https://github.com/devsisters/libquic libquic]、提供libquic的Go语言绑定的[https://github.com/devsisters/goquic goquic]、打包为[[Docker|Docker]]镜像的用来转换为普通HTTP请求的反向代理[https://hub.docker.com/r/devsisters/quic-reverse-proxy/ quic-reverse-proxy]。

== 参见 ==
* [[HTTP/2|HTTP/2]]
* [[SPDY|SPDY]]
* [[流控制传输协议|-{zh-tw:串流控制傳輸協定; zh-cn:流控制传输协议;}-]]
* [[UDT|UDT]]
* {{tsl|en|Datagram Transport Layer Security|數據傳輸層加密}}
* [[握手_(技术)|三方交握]]

==参考资料==
{{reflist}}

== 外部連結 ==
* [[Chromium|Chromium]]: [https://www.chromium.org/quic QUIC, a multiplexed stream transport over UDP]
* [https://docs.google.com/document/d/1RNHkx_VvKWyWg6Lr8SZ-saqsQx7rFV-ev2jRFUoVD34/edit QUIC: Design Document and Specification Rationale], Jim Roskind's original document (2012/2013)
* {{link-en|Daniel Stenberg|Daniel Stenberg}}: [https://http3-explained.haxx.se/en/ HTTP/3 explained]
* [[LWN.net|Linux Weekly News]]: [https://lwn.net/Articles/558826/ Connecting on the QUIC] (2013)
* [https://www.ietf.org/proceedings/88/slides/slides-88-tsvarea-10.pdf QUIC:], IETF-88 TSV Area Presentation (2013-11-07)
* Chromium Blog: [https://blog.chromium.org/2013/06/experimenting-with-quic.html Experimenting with QUIC]  (2013)
* [https://www.youtube.com/watch?v=hQZ-0mXFmk8 QUIC: next generation multiplexed transport over UDP] (Google Developers, 2014)
* [http://c3lab.poliba.it/images/3/3b/QUIC_SAC15.pdf HTTP over UDP: an Experimental Investigation of QUIC]
* [http://www.multipath-quic.org Multipath QUIC] (extension to QUIC)
* [https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=%20&arnumber=7867726 Innovating Transport with QUIC: Design Approaches and Research Challenges] (2017)

[[Category:传输层协议|Category:传输层协议]]
[[Category:网际协议|Category:网际协议]]
[[Category:Google軟體|Category:Google軟體]]