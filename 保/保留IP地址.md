{{NoteTA
|G1=IT
|1=zh-hans:块;zh-hant:網段
}}
在[[互联网|互联网]]寻址结构中，[[互联网工程任务组|互联网工程任务组]]（IETF）和[[互联网号码分配局|互联网号码分配局]]（IANA）保留了许多用于特殊目的的[[网际协议|网际协议]]（IP）地址。

==IPv4==
{| class="wikitable sortable"
|-
!地址块 ([[无类别域间路由|CIDR]])
!范围
!地址数
!效用域
!用途
|-
|0.0.0.0/8
|0.0.0.0 – <br>0.255.255.255
|align="right"|16,777,216
|软件
|用于广播信息到当前主机。<ref>RFC 1700, ''Assigned Numbers'' (1994), page 4</ref>
|-
|10.0.0.0/8
|10.0.0.0 – <br>10.255.255.255
|align="right"|16,777,216
|专用网络
|用于[[专用网络|专用网络]]内的本地通信。<ref name=rfc1918>RFC 1918, ''Address Allocation for Private Internets'' (1996)</ref>
|-
|100.64.0.0/10
|100.64.0.0 – <br>100.127.255.255
|align="right"|4,194,304
|专用网络
|用于在[[电信级NAT|电信级NAT]]环境中服务提供商与其用户通信。<ref>RFC 6598, ''IANA-Reserved IPv4 Prefix for Shared Address Space'' (2012)</ref>
|-
<!-- Note: 14.0.0.0/8, 24.0.0.0/8 and 39.0.0.0/8 are outdated and irrelevant. Do not add them. -->
|127.0.0.0/8
|127.0.0.0 – <br>127.255.255.255
|align="right"|16,777,216
|主机
|用于到本地主机的[[IPv4#环回地址(Loopback_Address)|环回地址]]。<ref>RFC 990, ''Assigned Numbers'' (1986)</ref>
|-
<!-- Note: 128.0.0.0/16 is "no longer needed" and "subject to future allocation" so it is not relevant here. -->
|169.254.0.0/16
|169.254.0.0 – <br>169.254.255.255
|align="right"|65,536
|子网
|用于单链路的两个主机之间的[[本地链路地址|本地链路地址]]，而没有另外指定IP地址，例如通常从[[动态主机设置协议|DHCP]]服务器所检索到的IP地址。<ref>RFC 3927, ''Dynamic Configuration of IPv4 Link-Local Addresses'' (2005)</ref> 
|-
|172.16.0.0/12
|172.16.0.0 – <br>172.31.255.255
|align="right"|1,048,576
|专用网络
|用于专用网络中的本地通信。<ref name=rfc1918 />
|-
<!-- Note: 191.255.0.0/16 and 192.0.0.0/24 is "no longer needed" and "subject to future allocation" so it is not relevant here. -->
|192.0.0.0/24
|192.0.0.0 – <br>192.0.0.255
|align="right"|256
|专用网络
|用于IANA的IPv4特殊用途地址表。<ref name=rfc5736>RFC 5736, ''IANA IPv4 Special Purpose Address Registry'' (2010)</ref>
|-
|192.0.2.0/24
|192.0.2.0 – <br>192.0.2.255
|align="right"|256
|文档
|分配为用于文档和示例中的“TEST-NET”（测试网），它不应该被公开使用。<ref name=rfc5737>RFC 5737, ''IPv4 Address Blocks Reserved for Documentation'' (2010)</ref>
|-
|192.88.99.0/24
|192.88.99.0 – <br>192.88.99.255
|align="right"|256
|互联网
|用于[[6to4|6to4]][[任播|任播]]中继。<ref>RFC 3068, ''An Anycast Prefix for 6to4 Relay Routers'' (2001)</ref>
|-
|192.168.0.0/16
|192.168.0.0 – <br>192.168.255.255
|align="right"|65,536
|专用网络
|用于专用网络中的本地通信。<ref name=rfc1918 />
|-
|198.18.0.0/15
|198.18.0.0 – <br>198.19.255.255
|align="right"|131,072
|专用网络
|用于测试两个不同的子网的网间通信。<ref>RFC 2544, ''Benchmarking Methodology for Network Interconnect Devices'' (1999)</ref>
|-
|198.51.100.0/24
|198.51.100.0 – <br>198.51.100.255
|align="right"|256
|文档
|分配为用于文档和示例中的“TEST-NET-2”（测试-网-2），它不应该被公开使用。<ref name=rfc5737 />
|-
|203.0.113.0/24
|203.0.113.0 – <br>203.0.113.255
|align="right"|256
|文档
|分配为用于文档和示例中的“TEST-NET-3”（测试-网-3），它不应该被公开使用。<ref name=rfc5737 />
|-
<!-- 223.255.255.0/24 presently unused, but subject to future allocation -->
|224.0.0.0/4
|224.0.0.0 – <br>239.255.255.255
|align="right"|268,435,456
|互联网
|用于多播。<ref name=rfc1112>RFC 1112, '' Host Extensions for IP Multicasting'' (1989)</ref>
|-
|240.0.0.0/4
|240.0.0.0 – <br>255.255.255.254
|align="right"|268,435,456
|互联网
|用于将来使用。<ref name=rfc6890>RFC 6890, ''Special-Purpose IP Address Registries'' (2013)</ref>
|-
|255.255.255.255/32
|255.255.255.255
|align="right"|1
|子网
|用于受限广播地址。<ref name=rfc6890 />
|}

==IPv6==
{|class="wikitable"
|-
!地址块（CIDR）
!范围
!地址数
!效用域
!用途
|-
|::/128
|::
|1
|软件
|未指定地址。
|-
|::1/128
|::1
|1
|主机
|用于到本地主机的[[IPv4#环回地址(Loopback_Address)|环回地址]]。
|-
|::ffff:0:0/96
|::ffff:0:0 –<br/>::ffff:ffff:ffff<br/ >(::ffff:0.0.0.0 – <br/>::ffff:255.255.255.255)
|2<sup>32</sup>
|软件
|IPv4映射地址。
|-<!-- Deprecated

|
|
|{{Locality|Local}}
|IPv4 Compatible Addresses (deprecated)
-->
|-
|100::/64
|100:: – <br/>100::ffff:ffff:ffff:ffff 
|2<sup>64</sup>
|
|RFC 6666中废除的前缀。
|-
|64:ff9b::/96
|64:ff9b::<br/>64:ff9b::ffff:ffff<br/>(64:ff9b::0.0.0.0 – <br/>64:ff9b::255.255.255.255)
|2<sup>32</sup>
|全球互联网<ref>RFC 6052 section 3.2</ref>
|用于IPv4/IPv6转换。（RFC 6052）
|-
|2001::/32
|2001:: – <br/>2001::ffff:ffff:ffff:ffff:ffff:ffff
|2<sup>96</sup>
|全局
|用于[[Teredo隧道|Teredo]]通道。
|-
|2001:10::/28
|2001:10:: – <br/>2001:1f:ffff:ffff:ffff:ffff:ffff:ffff
|2<sup>100</sup>
|软件
|已弃用（先前为[[ORCHID|ORCHID]]）。
|-
|2001:20::/28
|2001:20:: – <br/>2001:2f:ffff:ffff:ffff:ffff:ffff:ffff
|2<sup>100</sup>
|软件
|[[ORCHIDv2|ORCHIDv2]]。
|-
|2001:db8::/32
|2001:db8:: – <br/>2001:db8:ffff:ffff:ffff:ffff:ffff:ffff
|2<sup>96</sup>
|文档
|用于文档和示例源代码中的地址。
|-
|2002::/16
|2002:: – <br/>2002:ffff:ffff:ffff:ffff:ffff:ffff:ffff
|2<sup>112</sup>
|全球互联网
|用于[[6to4|6to4]]（已废弃<ref name=rfc7526>{{Cite IETF|rfc=7526|bcp=196|title=Deprecating the Anycast Prefix for 6to4 Relay Routers|author1=O. Troan|editor=B. Carpenter|publisher=[[Internet_Engineering_Task_Force|Internet Engineering Task Force]]|date=May 2015}}</ref>）。
|-
|fc00::/7
|fc00:: – <br/>fdff:ffff:ffff:ffff:ffff:ffff:ffff:ffff
|2<sup>121</sup>
|专用网络
|用于[[唯一区域位址|唯一区域位址]]。
|-
|fe80::/10
|fe80:: – <br/>febf:ffff:ffff:ffff:ffff:ffff:ffff:ffff
|2<sup>118</sup>
|链路
|用於專用網絡中的本地通訊。
|-
|ff00::/8
|ff00:: – <br/>ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff
|2<sup>120</sup>
|全球互联网
|用于[[多播地址|多播地址]]。
|}

==参见==
* {{tsl|en|Martian packet|火星数据包}}

== 参考资料 ==
{{reflist}}

== 外部链接 ==
*[http://www.iana.org/assignments/iana-ipv4-special-registry/iana-ipv4-special-registry.xhtml IANA IPv4 Special-Purpose Address Registry]
*[http://www.iana.org/assignments/iana-ipv6-special-registry/iana-ipv6-special-registry.xhtml IANA IPv6 Special-Purpose Address Registry]

[[Category:IP地址|Category:IP地址]]