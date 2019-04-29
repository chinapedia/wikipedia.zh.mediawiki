{{noteTA|G1=IT}}
'''基于Web的分布式编写和版本控制'''（{{lang|en|'''WebDAV'''}}）是[[超文本传输协议|超文本传输协议]]（HTTP）的扩展，有利于用户间协同编辑和管理存储在[[万维网|万维网]]服务器文档。WebDAV由[[互联网工程任务组|互联网工程任务组]]的工作组在{{IETF RFC|4918}}中定义。

WebDAV协议为用户在[[服务器|服务器]]上创建，更改和移动文档提供了一个框架。WebDAV协议最重要的功能包括维护作者或修改日期的属性、[[命名空间|命名空间]]管理、集合和覆盖保护。维护属性包括创建、删除和查询文件信息等。'''命名空间管理'''处理在服务器名称空间内复制和移动网页的能力。'''集合'''（{{lang|en|Collections}}）处理各种资源的创建、删除和列举。'''覆盖保护'''处理与锁定文件相关的方面。

许多现代[[操作系统|操作系统]]为WebDAV提供了内置的客户端支持。

== 历史 ==
WebDAV始于1996年，当时[[加州大學爾灣分校|加州大學爾灣分校]]博士毕业生[[Jim_Whitehead_(professor)|Jim Whitehead]]与[[万维网联盟|W3C]]共同主办了两场会议，与感兴趣的人讨论万维网上的分布式创作问题。<ref>{{cite web|url= http://lists.w3.org/Archives/Public/w3c-dist-auth/1996AprJun/0002.html|title= Proposed agenda for San Mateo Meeting|year= 1996}}</ref><ref>{{cite web|url= http://lists.w3.org/Archives/Public/w3c-dist-auth/1996JulSep/0095.html|title= Brief mtg. summary|year= 1996}}</ref>
[[蒂姆·伯纳斯-李|蒂姆·伯纳斯-李]]对网络的最初看法是涉及阅读和写作的[[儲存裝置|媒介]]。事实上，Berners Lee的第一个[[网页浏览器|Web浏览器]]（[[WorldWideWeb|WorldWideWeb]]），可以查看和编辑[[網頁|網頁]]；但是，随着网络的成长，对大多数用户来说成为了只读媒介。怀特黑德和其他志同道合的人想超越这个限制。<ref>{{cite web
|url= http://lists.w3.org/Archives/Public/w3c-dist-auth/1996JulSep/0001.html
|title= Re: Updated agenda}}
</ref>

W3C会议决定成立一个[[互联网工程任务组|IETF]]工作组，因为新的工作将导致对[[超文本传输协议|HTTP]]进行扩展，而当时IETF已经开始对HTTP进行标准化。

随着协议的工作开始，很明显，同时处理分布式创作和[[版本控制|版本控制]]将涉及太多的工作，并且任务将不得不分开。WebDAV小组专注于分布式创作，将版本控制留作以后研究。(The [[Delta-V_extension|Delta-V extension]] added versioning later{{snd}} see the Extensions section below.)

在{{le|互联网工程指导组|Internet Engineering Steering Group}}（IESG）接受{{IETF RFC|2518}}的增量更新之后，WebDAV工作组在2007年3月结束了其工作。当时还没有完成的其他扩展，比如{{le|BIND方法|BIND method}}，已经由其独立作者独立于正式工作组完成。

== 实现 ==

WebDAV扩展了[[超文本传输协议#请求信息|request]]方法所允许的标准HTTP谓词和HTTP头。增加的谓词包括：

; COPY
: 将资源从一个[[统一资源标志符|URI]]复制到另一个URI
; LOCK
: [[锁_(计算机科学)|锁定]]一个资源。WebDAV支持共享锁和互斥锁。
; MKCOL
: 创建集合（即[[目录_(文件系统)|目录]]）
; MOVE
: 将资源从一个[[统一资源标志符|URI]]移动到另一个URI
; PROPFIND
: 从{{le|Web资源|web resource}}中检索以[[XML|XML]]格式存储的属性。它也被[[函数重载|重载]]，以允许一个检索远程系统的集合结构（也叫目录层次结构）。
; PROPPATCH
: 在单个{{le|原子性提交|atomic commit|原子性动作}}中更改和删除资源的多个属性
; UNLOCK
: 解除资源的锁定

=== 服务器支持 ===
* [[Apache_HTTP_Server|Apache HTTP Server]]提供基于[[davfs|davfs]]和[[Subversion|Apache Subversion (svn)]]的WebDAV模块。
* [[微软|微软]]的[[網際網路資訊服務|IIS]]也有WebDAV模块。
* [[Nginx|Nginx]]有非常有限的可选WebDav模块<ref>{{cite web|title=Module ngx_http_dav_module|url=http://nginx.org/en/docs/http/ngx_http_dav_module.html|website=nginx website|accessdate=15 July 2016}}</ref>和第三方模块<ref>{{cite web|title=Module nginx-dav-ext-module|url=https://github.com/arut/nginx-dav-ext-module/|website=github.com|accessdate=2 August 2016}}</ref>
* [[SabreDAV|SabreDAV]]是一个PHP应用程序，可以在Apache或Nginx上使用，代替它们的捆绑模块
* [[Nextcloud|Nextcloud]]是一个云存储PHP应用程序，它提供了完整的WebDAV支持<ref>{{cite web|title=Nextcloud 11 User Manual|url=https://docs.nextcloud.com/server/11/user_manual/files/access_webdav.html|website=nextcloud.com|accessdate=19 September 2017}}</ref>
* [[lighttpd|lighttpd]]有一个可选的WebDav模块<ref>{{Cite web|url=http://redmine.lighttpd.net/projects/1/wiki/Docs_ModWebDAV|title=lighttpd mod webdav|last=|first=|date=|website=|archive-url=|archive-date=|dead-url=|access-date=}}</ref>

=== 客户端支持 ===

* [[Git|Git]]支持写入HTTP远端，尽管需要特殊服务器支持的HTTP的“智能”Git协议已经成为WebDAV的首选协议
* [[Linux|Linux]]通过[[GVfs|GVfs]]（包括[[Nautilus檔案瀏覽器|GNOME文件]]）或通过[[KIO|KIO]]（包括[[Konqueror|Konqueror]]和[[Dolphin_(軟體)|Dolphin]]）支持WebDAV
* [[macOS|macOS]]对[[CalDAV|CalDAV]]和[[CardDAV|CardDAV]]有原生支持，其设计基于WebDAV
* [[Microsoft_Windows|Microsoft Windows]]，其[[檔案總管|Explorer]]有原生支持
* [[Microsoft_Office|Microsoft Office]]
* {{le|WebDAV软件比较|Comparison of WebDAV software}}

== 参见 ==
* [[內容管理|內容管理]]
* [[集群文件系统|集群文件系统]]

== 参考文献 ==
{{Reflist|2}}

== 外部链接 ==
* [https://web.archive.org/web/20120626092812/http://webdav.org/ WebDAV Resources]
* [http://savannah.nongnu.org/projects/davfs2 Davfs2 project]
* [http://0pointer.de/lennart/projects/fusedav Fusedav project]
* [http://httpd.apache.org/docs/2.4/mod/mod_dav.html WebDAV Apache modules]
* [https://www.drivehq.com/help/features/webdav.aspx WebDAV Drive Mapping Tool]

{{Authority control}}
[[Category:网际协议|Category:网际协议]]
[[Category:W3C标准|Category:W3C标准]]
[[Category:HTTP|Category:HTTP]]
[[Category:协作软件|Category:协作软件]]
[[Category:网络文件系统|Category:网络文件系统]]