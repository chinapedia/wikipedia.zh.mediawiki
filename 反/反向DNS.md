{{expand|time=2019-01-06T07:27:51+00:00}}
{{expert|time=2019-01-06T07:27:51+00:00}}
在[[计算机网络|计算机网络]]中,反向DNS查找或反向DNS解析（rDNS）是查询的域名系统（DNS）来确定相关的域名的IP地址——通常的“转发”的反向DNS查找域名的IP地址。反向的过程解决IP地址使用PTR记录。互联网的反向DNS数据库植根于arpa顶级域名。

虽然信息 [rfc:1912 RFC1912年] (第2.1节)建议，“每一个互联网可访问的主机应该有一个名字”和“为每一个IP地址，应该有一个匹配PTR记录”，这不是一个[[互联网标准|互联网标准]] 要求，并不是所有IP地址中有一个反向记录。

== 历史使用情况 ==
现代“反向DNS查找”不应被混淆<ref name="RFC 3425" />，“反向查询”(IQUERY)机制在RFC 1035中写到：{{Quote|text=Inverse queries take the form of a single [[Resource_record|RR]] in the answer section of the message, with an empty question section.  The owner name of the query RR and its [[Time_to_live|TTL]] are not significant.  The response carries questions in the question section which identify all names possessing the query RR ''which the name server knows''. Since no name server knows about all of the domain name space, the response can never be assumed to be complete.  Thus inverse queries are primarily useful for database management and debugging activities.  Inverse queries are ''not'' an acceptable method of mapping host addresses to host names; use the <code>in-addr.arpa</code> domain instead.<ref name="RFC 1035"></ref>}}IQUERY消息类型总是“可选的”和“从未取得了广泛使用”；“permanently retired”在2002年采用RFC 3425。

== 参考文献 ==
{{Reflist|refs=
<ref name="RFC 1035">{{Cite web|url=https://tools.ietf.org/html/rfc1035|title=RFC 1035 — Domain names - implementation and specification|accessdate=2017-12-28|date=November 1987}}</ref>

<ref name="RFC 3425">{{Cite web|url=https://tools.ietf.org/html/rfc3425|title=RFC 3425 — Obsoleting IQUERY|accessdate=2017-12-28|date=November 2002}}</ref>
}}

[[Category:域名|Category:域名]]
[[Category:信息检索系统|Category:信息检索系统]]