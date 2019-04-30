{{NoteTA
|G1=IT
}}
{{校对翻译}}
[[File:CGN_IPv4.svg|缩略图]]
'''电信级NAT'''或'''运营商级NAT'''（'''Carrier-grade NAT'''，缩写'''CGN'''），也称'''大规模NAT'''（'''large-scale NAT'''，缩写'''LSN'''）是一种为[[IPv4|IPv4]]网络端点（尤其是住宅网络）设计的方法，通过嵌入在网络运营商网络中的{{tsl|en|Middlebox|中间盒}}[[网络地址转换|网络地址转换]]（NAT）设备，将已配置的[[专用网络|专用网络]]地址翻译到[[IP地址|公网IPv4地址]]，允许许多终端站点共享一个小型公共地址池。这将NAT功能及配置从客户端驻地转移到互联网服务提供商网络。

电信级NAT已被提议作为一种[[IPv4位址枯竭|IPv4位址枯竭]]的缓解方法。<ref>{{Cite web|url=http://tools.ietf.org/html/rfc6264|title=RFC 6264 - An Incremental Carrier-Grade NAT (CGN) for IPv6 Transition}}</ref>

电信级NAT的批评者批评以下几个方面：
* 与任何形式的NAT一样，它损害{{tsl|en|End-to-end principle|端到端原则}}。<ref>{{Cite web|url=http://tools.ietf.org/html/draft-donley-nat444-impacts|title=Assessing the Impact of NAT444 on Network Applications}}</ref>
* 它有显著的安全性、[[可扩展性|可扩展性]]和[[可靠性_(计算机网络)|可靠性]]问题，因为其{{tsl|en|Stateful|有状态}}属性。
* 它使保留记录供执法行动更加困难，除非也记录地址的翻译。
* 它使托管服务变成不可能。
* 当需要公网IP地址时（例如托管Web主机），它不解决IPv4地址耗尽问题。
CGN的一种使用场景可以描述为'''NAT444'''<ref>{{Cite web|url=http://chrisgrundemann.com/index.php/2011/nat444-cgn-lsn-breaks/|title=NAT444 (CGN/LSN) and What it Breaks}}</ref>，因为一些客户与公共服务器的连接将通过三个不同的IPv4寻址域：客户自己的私有网络，运营商的私有网络，以及公共互联网。

另一种CGN场景是[[IPv6转换机制|双栈精简版]]（Dual-Stack Lite，也称DS-Lite），其中运营商的网络使用[[IPv6|IPv6]]，因此只需要两个IPv4寻址域。

== 共享地址空间 ==
如果一个ISP部署CGN并使用RFC 1918地址空间给他们的用户，那么已经使用RFC 1918空间的客户设备存在停止工作的风险。原因是如果网络接口的内部与外部地址相同，路由和NAT将不工作。

这促使一些ISP在{{tsl|en|American Registry for Internet Numbers|ARIN}}内制定策略，为CGN分配新的私有地址空间，但ARIN推迟它，直至[[互联网工程任务组|IETF]]实现策略表明这个问题不是典型的分配但是为技术目的保留（根据RFC 2860）。

IETF创建了RFC 6598，详述了为ISP CGN部署使用的共享地址空间，以及NAT设备可以处理在入站和出站接口上出现的相同地址。ARIN根据此分配的需要将空间返还给[[互联网号码分配局|IANA]]。<ref>{{Cite web|url=http://seclists.org/nanog/2012/Mar/588|title=Re: shared address space... a reality!|accessdate=13 September 2012}}</ref>分配的地址块为<tt>100.64.0.0/10</tt>。<ref>{{Cite web|url=http://chrisgrundemann.com/index.php/2012/100640010/|title=100.64.0.0/10 – Shared Transition Space}}</ref>

=== 问题 ===
* 试图找出IPv4地址是否为公网的设备或软件必须更新以识别新的空间。
* 为NAT设备分配更多私有IPv4地址空间可能会延长到IPv6的过渡。

== 缺点 ==
电信级NAT通常会阻止ISP客户使用[[端口映射|端口映射]]，因为[[网络地址转换|网络地址转换]]（NAT）通常通过将网络中NAT设备的端口映射到外部接口的其他[[通訊埠|端口]]来实现，这样[[路由器|路由器]]才能映射响应到正确的设备。在电信级NAT网络中，即使消费者端的路由器可能已配置为端口转发，ISP处运行CGN的“主路由器”仍将阻止端口转发，因此实际的端口将不是消费者配置的端口。<ref name="ofcom-cgnat">http://stakeholders.ofcom.org.uk/binaries/research/technology-research/2013/cgnat.pdf</ref>为了克服前者的缺点，{{tsl|en|Port Control Protocol|端口控制协议}}（PCP）已在RFC 6887中标准化。

此外，在极少数情况下，可能遇到基于IP地址的封禁问题。以[[维基百科|维基百科]]为例，系统可能封禁发送垃圾信息的用户的IP。如果该用户在一个电信级NAT后面，其他与垃圾发送者共享使用同一公网[[IP地址|IP地址]]的正常用户也将被错误阻止。<ref name="ofcom-cgnat">http://stakeholders.ofcom.org.uk/binaries/research/technology-research/2013/cgnat.pdf</ref>

== 参见 ==
* [[NAT64|NAT64]]

== 参考资料 ==
{{Reflist}}

== 外部链接 ==
* [http://www.networkworld.com/community/node/44989 Understanding Carrier Grade NAT]
* [http://tools.ietf.org/html/draft-ietf-behave-lsn-requirements IETF Internet-Draft: Common requirements for Carrier Grade NAT (CGN)]
* [http://chrisgrundemann.com/index.php/2012/cgn-observations-recommendations/ CGN :: Observations & Recommendations]

* [http://www.c114.net/tech/166/a759847.html CGN在IPv6演进过程中的关键作用]，C114(中国通信网)，2013年4月16日{{zh-cn}}
* [http://www.189.cn/bj/sy_ycgg/90691.html 北京电信宽带部署 CGN 割接的通告]，中国电信，2016年12月29日{{zh-cn}}

[[Category:网络协议|Category:网络协议]]
[[Category:网络地址转换|Category:网络地址转换]]
[[Category:互联网协议|Category:互联网协议]]