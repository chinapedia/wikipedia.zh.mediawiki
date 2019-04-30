'''基于融合以太网的RDMA'''（{{lang-en|RDMA over Converged Ethernet}}，缩写'''RoCE'''）是一个网络协议，允许在一个[[以太网|以太网]]网络上使用[[远程直接内存访问|远程直接内存访问]]（RDMA）。RoCE有RoCE v1和RoCE v2两个版本。RoCE v1是一个以太网{{tsl|en|Link layer|链路层}}协议，因此允许同一个以太网[[广播域|广播域]]中的任意两台主机间进行通信。RoCE v2是一个[[网络层|网络层]]协议，因而RoCE v2数据包可以被路由。虽然RoCE协议受益于{{tsl|en|数据中心桥接|Data center bridging|融合以太网网络}}的特征，但该协议也可用于传统或非融合的以太网网络。<ref name="RoCEv1">{{Cite web|url=https://cw.infinibandta.org/document/dl/7148|title=InfiniBand™ Architecture Specification Release 1.2.1 Annex A16: RoCE|date=13 April 2010}}</ref><ref name="RoCEv2">{{Cite web|url=https://cw.infinibandta.org/document/dl/7781|title=InfiniBand™ Architecture Specification Release 1.2.1 Annex A17: RoCEv2|date=2 September 2014}}</ref><ref name=":0">{{cite web|url=https://community.mellanox.com/docs/DOC-1451|title=RoCEv2 Considerations|author=Ophir Maor|date=December 2015|website=Mellanox}}</ref><ref>{{Cite web|url=https://community.mellanox.com/docs/DOC-2283|title=RoCE and Storage Solutions|author=Ophir Maor|date=December 2015|last=Ophir Maor}}</ref>

== 背景 ==
网络密集型应用程序（如网络存储或群集计算）需要具有高带宽且低[[延迟_(工程学)|延迟]]的网络基础架构。RDMA相比其他网络[[应用程序接口|应用程序接口]]（诸如[[Berkeley套接字|Berkeley套接字]]）的优势是更低的延迟、更低的CPU占用，以及更高的带宽。<ref>{{Cite book|title=Virtual Interface Architecture|last=Cameron|first=Don|last2=Regnier|first2=Greg|publisher=Intel Press|year=2002|isbn=978-0-9712887-0-6}}</ref>RoCE协议有着比其前身{{le|iWARP}}协议更低的延迟。<ref>{{Cite web|url=http://archive.hpcwire.com/hpcwire/2010-04-22/roce_an_ethernet-infiniband_love_story.html|title=RoCE: An Ethernet-InfiniBand Love Story|date=22 April 2010|last=Feldman|first=Michael}}</ref>现有的RoCE HCA（主机通道适配器）的延迟低至1.3微秒<ref>{{Cite web|url=http://www.mellanox.com/pdf/applications/SB_EthSolutions_financial.pdf|title=End-to-End Lowest Latency Ethernet Solution for Financial Services|date=March 2011}}</ref><ref>{{Cite web|url=http://www.mellanox.com/pdf/whitepapers/WP_RoCE_vs_iWARP.pdf|title=RoCE vs. iWARP Competitive Analysis Brief|date=9 November 2010}}</ref>，而在2011年已知的最低的iWARP HCA的延迟为3微秒。<ref>{{Cite web|url=http://www.chelsio.com/press-room/2164/|title=Low Latency Server Connectivity With New Terminator 4 (T4) Adapter|date=25 May 2011}}</ref>
[[File:RoCE_Header_format.png|缩略图]]

== RoCE v1 ==
RoCE v1协议是一个以太网链路层协议，Ethertype为0x8915。它要符合以太网协议的帧长度限制：常规[[以太网帧格式|以太网帧]]为1500字节，[[巨型帧|巨型帧]]为9000字节。

== RoCE v2 ==
RoCEv2协议构筑于UDP/IPv4或UDP/IPv6协议之上。UDP目标端口号4791已保留给RoCE v2。<ref>{{Cite web|url=https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml?search=IP+Routable+RocE|title=Service Name and Transport Protocol Port Number Registry|accessdate=14 October 2018|author=Diego Crupnicoff|date=17 October 2014|last=Diego Crupnicoff}}</ref>因为RoCEv2数据包是可路由的，所以RoCE v2协议有时被称为Routable RoCE<ref>{{Cite web|url=http://www.ietf.org/proceedings/88/slides/slides-88-storm-3.pdf|title=RoCE Status and Plans|author=InfiniBand Trade Association|date=November 2013|last=InfiniBand Trade Association}}</ref>或RRoCE。虽然一般不保证UDP数据包的传达顺序，但RoCEv2规范要求，有相同UDP源端口及目标地址的数据包不得改变顺序。除此之外，RoCEv2定义了一种拥塞控制机制，使用IP ECN位用于标记，CNP<ref>{{Cite web|url=https://community.mellanox.com/docs/DOC-2351|title=RoCEv2 CNP Packet Format|author=Ophir Maor|date=December 2015|last=Ophir Maor}}</ref>帧用于送达通知。<ref>{{Cite web|url=https://community.mellanox.com/docs/DOC-2321|title=RoCEv2 Congestion Management|author=Ophir Maor|date=December 2015|last=Ophir Maor}}</ref>软件对RoCE v2的支持在不断涌现。Mellanox OFED 2.3或更高版本支持RoCE v2，Linux内核v4.5也提供支持。<ref>{{Cite web|url=https://git.kernel.org/cgit/linux/kernel/git/davem/net.git/commit/?id=048ccca8c1c8f583deec3367d7df521bb1f542ae|title=Kernel GIT|date=January 2016}}</ref>

== RoCE与InfiniBand相比 ==
RoCE定义了如何在[[以太网|以太网]]上执行RDMA，[[InfiniBand|InfiniBand]]架构规范则定义了如何在一个[[InfiniBand|InfiniBand]]网络上执行RDMA。RoCE预期为将主要面向群集的InfiniBand应用程序带入到一个寻常的以太网融合结构。<ref>{{Cite web|url=http://www.eetimes.com/electronics-news/4088625/New-converged-network-blends-Ethernet-Infiniband|title=New converged network blends Ethernet, InfiniBand|date=19 April 2010|last=Merritt|first=Rick}}</ref>{{who|有人}}认为，InfiniBand将会继续提供比以太网更高的带宽以及更低的延迟。<ref>{{Cite web|url=http://www.enterprisenetworkingplanet.com/nethub/article.php/3879506/InfiniBand-Moving-to-Ethernet.htm|title=InfiniBand Moving to Ethernet ?|date=2 April 2010|last=Kerner|first=Sean Michael}}</ref>

RoCE与InfiniBand协议之间的技术差异：

* 链路级流量控制：InfiniBand使用一个积分算法来保证无损的HCA到HCA通信。RoCE运行在以太网之上，其实现可能需要“无损以太网”以达到类似于InfiniBand的性能特征，无损以太网一般通过[[IEEE_802.3x|以太网流量控制]]或优先流量控制（PFC）配置。配置一个{{tsl|en|Data center bridging|数据中心桥接}}（DCB）以太网网络可能比配置InfiniBand网络更为复杂。<ref>{{Cite web|url=http://ir.mellanox.com/releasedetail.cfm?ReleaseID=851785|title=Mellanox Releases New Automation Software to Reduce Ethernet Fabric Installation Time from Hours to Minutes|author=Mellanox|date=2 June 2014|last=Mellanox}}</ref>
* 拥塞控制：Infiniband定义了基于FECN/BECN标记的拥塞控制，RoCEv2则定义了一个拥塞控制协议，它使用ECN标记在标准交换机中的实现，以及CNP帧用于送达确认。
* 可用的InfiniBand交换机始终有比以太网交换机更低的延迟。一台特定类型以太网交换机的端口至端口延迟为230纳秒<ref>{{Cite web|url=http://www.mellanox.com/page/products_dyn?product_family=115&mtag=sx1036|title=SX1036 - 36-Port 40/56GbE Switch System|accessdate=April 21, 2014}}</ref>，而有相同端口数量的一台InfiniBand交换机为100纳秒<ref>{{Cite web|url=http://www.mellanox.com/page/products_dyn?product_family=91&mtag=is5024|title=IS5024 - 36-Port Non-blocking Unmanaged 40Gb/s InfiniBand Switch System|accessdate=April 21, 2014}}</ref>。

== RoCE与iWARP相比 ==
相比RoCE协议定义了如何使用以太网和UDP/IP帧执行RDMA，iWARP协议定义了如何基于一个面向连接的传输（如[[传输控制协议|传输控制协议]]，TCP）执行RDMA。RoCE v1受限于单个[[广播域|广播域]]，RoCE v2和iWARP封包则可以路由。在大规模数据中心和大规模应用程序（即大型企业、云计算、Web 2.0应用程序等<ref>{{cite conference |last=Rashti |first=Mohammad |url=http://post.queensu.ca/~pprl/papers/HiPC-2010.pdf |title=iWARP Redefined: Scalable Connectionless Communication over High-Speed Ethernet |booktitle=International Conference on High Performance Computing (HiPC) |year=2010}}</ref>）中使用iWARP时，大量连接的内存需求，以及TCP的流量和可靠性控制，将会导致可扩展性和性能问题。此外，RoCE规范中定义了多播，而当前的iWARP规范中没有定义如何执行多播RDMA。<ref>{{Cite web|url=http://tools.ietf.org/html/rfc5041|title=Direct Data Placement over Reliable Transports|accessdate=May 4, 2011|author=H. Shah|date=October 2007|last=H. Shah|work=RFC 5041}}</ref><ref>{{Cite web|url=http://tools.ietf.org/html/rfc5043|title=Stream Control Transmission Protocol (SCTP) Direct Data Placement (DDP) Adaptation|accessdate=May 4, 2011|author=C. Bestler|date=October 2007|last=C. Bestler|work=RFC 5043}}</ref><ref>{{Cite web|url=http://tools.ietf.org/html/rfc5044|title=Marker PDU Aligned Framing for TCP Specification|accessdate=May 4, 2011|author=P. Culley|date=October 2007|last=P. Culley|work=RFC 5044}}</ref>

iWARP中的可靠性由协议本身提供，因为TCP/IP为可靠传输。相比而言，RoCEv2采用UDP/IP，这使它有更小的开销和更好的性能，但不提供固有的可靠性，因此可靠性必须搭配RoCEv2实现。其中一种解决方案是，使用融合以太网交换机使局域网变得可靠。这需要局域网内的所有交换机支持融合以太网，并防止RoCEv2数据包通过诸如互联网等不可靠的广域网传输。另一种解决方案是增加RoCE协议的可靠性（即可靠的RoCE），向RoCE添加握手，通过牺牲性能为代价提供可靠性。

两种协议哪种更好的问题取决于供应商。英特尔和Chelsio建议并独家支持iWARP。Mellanox、Xilinx以及Broadcom推荐并独家支持RoCE/RoCEv2。思科同时支持RoCE<ref>https://www.cisco.com/c/dam/en/us/products/collateral/switches/nexus-9000-series-switches/white-paper-c11-741091.pdf</ref>与自家的VIC RDMA协议。网络行业中的其他供应商则同时提供两种协议的支持，这些供应商如[[Marvell|Marvell]]、[[微软|微软]]、[[Linux|Linux]]和Kazan。<ref>{{Cite web|url=http://sniaesfblog.org/roce-vs-iwarp-the-next-great-storage-debate/|title=RoCE vs. iWARP – The Next “Great Storage Debate”|accessdate=August 22, 2018|author=T Lustig; F Zhang; J Ko,|date=October 2007|last=T Lustig; F Zhang; J Ko,}}</ref>

两种协议都经过了标准化，iWARP是[[互联网工程任务组|IETF]]定义的基于以太网的RDMA，RoCE是{{tsl|en|IBTA|InfiniBand贸易协会}}定义的基于以太网的RDMA  <ref>{{cite web|url=http://sniaesfblog.org/roce-vs-iwarp-the-next-great-storage-debate/|title=RoCE vs. iWARP – The Next “Great Storage Debate”|accessdate=August 22, 2018|author=T Lustig; F Zhang; J Ko,|date=October 2007}}CS1 maint: Multiple names: authors list ([//en.wikipedia.org/wiki/Category:CS1_maint:_Multiple_names:_authors_list link]) 
[[Category:CS1_maint:_Multiple_names:_authors_list|Category:CS1 maint: Multiple names: authors list]]</ref>

== 供应商 ==
支持RoCE的设备的主要供应商包括：

* {{le|Mellanox}}
* {{le|Emulex}}（已被[[博通_(公司)|博通 (公司)]]收购）
* [[博通_(公司)|博通]]（Broadcom）
* {{le|QLogic}}（已被[[凱為半導體|Cavium]]收购）
* [[凱為半導體|凱為半導體]]（Cavium）
* [[华为|华为]]

== 参考文献 ==
{{Reflist|30em}}
[[Category:乙太網路|Category:乙太網路]]
[[Category:操作系统技术|Category:操作系统技术]]
[[Category:并行计算|Category:并行计算]]