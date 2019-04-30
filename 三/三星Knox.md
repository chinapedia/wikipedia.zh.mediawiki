{{noteTA
|G1=IT
}}
{{orphan|time=2018-02-20T14:58:25+00:00}}
{{roughtranslation|time=2018-02-20T14:58:25+00:00}}
{{Infobox software
| name = 三星Knox
| title = 三星Knox
| logo = Samsung_Knox.png
| logo caption =
| screenshot = <!-- [[File:|File:]] -->
| caption =
| collapsible =
| author =
| developer = [[三星集团|三星集团]]
| released = <!-- {{Start date|YYYY|MM|DD|df=yes}} -->
| discontinued =
| latest release version = 2.9
| latest release date = {{Start date and age|2017|08|28|df=yes}}<ref>{{cite web|url=https://www.samsungknox.com/en/blog/whats-new-in-knox-29 |title=What’s new in Knox 2.9? |publisher=Samsung Knox |date=28 August 2017}}</ref>
| latest preview version =
| latest preview date = <!-- {{Start date and age|YYYY|MM|DD|df=yes}} -->
| frequently updated = <!-- DO NOT include this parameter unless you know what it does -->
| status = 活跃
| programming language =
| operating system = [[Android|Android]]及[[Tizen|Tizen]]
| platform =
| size =
| language = 
| language count = <!-- DO NOT include this parameter unless you know what it does -->
| language footnote =
| genre =
| license =
| alexa =
| website = {{URL|http://www.samsungknox.com/en|samsungknox.com}}
| standard =
| AsOf =
}}
'''三星Knox'''是一款预装于大多数三星智能手机、平板电脑和[[可穿戴設備|可穿戴设备]]上的[[企业级软件|企业级]]{{tsl|en|mobile computing|掌上计算|掌上设备}}{{tsl|en|mobile security|手持设备安全|安全}}软件。

== 服务 ==
相同掌上设备的功能。用户可以点击应用图标从个人模式转换到工作模式而无需延迟或重启。<ref name="IT">{{cite web|url=http://www.itwire.com/your-it-news/mobility/59182-samsung%E2%80%99s-knox%E2%84%A2-blackberry-off-balance|title=Samsung Knox™ BlackBerry off Balance|author=Ray Shaw|date=March 23, 2013|publisher=IT Wire|accessdate= 21 April 2013 }}</ref>制造商声称此功能将与安卓和[[谷歌|谷歌]]完全兼容，并提供工作和个人数据的完全隔离并「解决[[Android|Android]]中所有主要[[安全漏洞|安全漏洞]]」。<ref>{{cite web|url=http://money.cnn.com/2013/03/12/technology/security/samsung-knox/|title=Samsung targets BlackBerry with Knox|author=David Goldman|date=March 12, 2013|publisher=CNN Money}}</ref>

Knox服务是三星旗下的「三星企业服务」（SAFE）提供给[[智能手机|智能手机]]和[[平板電腦|平板電腦]]的功能。三星Knox的主要竞争者是一项分离个人和工作数据的[[BlackBerry_10|Blackberry Balance]]服务。三星Knox的名称源于{{tsl|en|United States Bullion Depository|美国金银存管|诺克斯堡}}（Fort Knox）。<ref name="UG">{{cite web|url=http://www.ubergizmo.com/2013/02/samsung-knox/|title=Samsung KNOX Provides Privacy To BYODUsers|author=Hubert Nguyen|date=February 25, 2013|publisher=UberGizmo|accessdate= 21 April 2013 }}</ref>

2014年10月，[[美国国家安全局|美国国家安全局]]批准[[三星Galaxy|三星Galaxy]]设备运行程序以快速部署商用技术。批准设备包括[[三星Galaxy_S4|Galaxy S4]], [[三星Galaxy_S5|Galaxy S5]]、[[三星Galaxy_S6|Galaxy S6]]、[[三星Galaxy_S7|Galaxy S7]]、[[三星Galaxy_Note_3|Galaxy Note 3]]和[[三星Galaxy_Note_10.1|Galaxy Note 10.1 2014]]。<ref name="NS">{{cite web|url=http://www.computerworld.com/article/2836380/nsa-approves-samsung-knox-devices-for-government-use.html|title=NSA approves Samsung Knox devices for government use|author=John Ribeiro|date=October 21, 2014|publisher=computerworld|accessdate=22 October 2014}}</ref>

2014年6月，5部三星设备被[[美国国防部|美国国防部]]{{tsl|en|Defense Information Systems Agency|美国国防信息系统局|国防信息系统局}}（测定商用技术用于国防）列入了敏感但未分类使用的批准产品名单。<ref name="DI">{{cite web|url=http://www.pcworld.com/article/2836612/samsung-knox-devices-approved-for-government-use-by-nsa.html|title=NSA approves Samsung Knox devices for government use|author=John Ribeiro|date=October 21, 2014|publisher=pcworld|accessdate=22 October 2014}}</ref>

2017年6月，三星终止了我的Knox服务并催促用户切换到替代产品——安全文件夹。<ref>{{cite web|url=http://www.androidauthority.com/samsung-discontinues-knox-switch-secure-folder-77714/|title=Samsung discontinues My Knox, urges users to switch to Secure Folder|date=June 2, 2017|publisher=Android Authority|accessdate=22 August 2017}}</ref>

=== 安全 ===

2014年10月，一位安全学者发现三星Knox以明文形式而非以[[盐_(密码学)|加盐]]和哈希过（使用{{tsl|en|PBKDF2|PBKDF2|PBKDF2}}更佳）再加以混淆的形式存储[[PIN碼|PIN码]]。<ref>{{cite web|url=http://threatpost.com/nsa-approved-samsung-knox-stores-pin-in-cleartext/109018|title=NSA-Approved Samsung Knox Stores PIN in Cleartext|date=October 24, 2014|publisher=threatpost|accessdate=22 August 2017}}</ref>

2016年5月，[[以色列|以色列]]学者烏里·卡诺诺夫（Uri Kanonov）和埃维森·沃（Avishai Wool）发现在特定版本中的Knox存在三个致命性的漏洞。<ref>{{cite web|url=http://www.techrepublic.com/article/samsung-knox-isnt-as-secure-as-you-think-it-is/|title=Samsung Knox isn't as secure as you think it is|date=May 31, 2016|publisher=TechRepublic|accessdate=22 August 2017}}</ref>

===e-fuse===

三星Knox设备使用[[EFUSE|e-fuse]]来辨别是否是通过「未受信任」（非三星）的启动路径启动。若设备使用非三星的引导程序、[[内核|内核]]、内核[[初始化|初始化]]脚本或数据，e-fuse将会被设置。[[Root_(Android)|Root]]设备并安装非三星的安卓发行版也将会设置e-fuse。当e-fuse设置时，设备不再能新建KNOX容器，亦或是访问先前存于已存在的KNOX容器中。<ref>{{cite web|url=https://www.samsungknox.com/en/blog/about-cf-auto-root|title=About CF-Auto-Root|author=Peng Ning|publisher=Samsung|date=2013-12-04|quote=The sole purpose of this fuse-burning action is to memorize that a kernel or critical initialization scripts or data that is not under Samsung's control has been put on the device. Once the e-fuse bit is burned, a Samsung KNOX-enabled device can no longer create a KNOX Container, or access the data previously stored in an existing KNOX Container.|deadurl=yes|archiveurl=https://web.archive.org/web/20151027024005/https://www.samsungknox.com/en/blog/about-cf-auto-root|archivedate=2015年10月27日|df=}}</ref>这些信息可能被三星用于拒绝这些被修改过设备的保修服务。<ref>{{cite web|url=https://plus.google.com/+Chainfire/posts/LCfF5A9fsTG|author=Chainfire|title=More on KNOX warranty void|date=2013-10-09|quote=Service center instructions are indeed that devices with this status tripped will not receive any warranty repairs. (Of course, the action they take may still depend on the service center). Their excuse is that the hardware is damaged by the owner.}}</ref>在美国境内无效化客户保修服务可能被[[馬格努森-莫斯質量保證法|馬格努森-莫斯質量保證法]]所禁止，尽管手机所出现的问题并不是由于[[Root_(Android)|root]]直接导致的。<ref>{{cite web|url=http://motherboard.vice.com/read/jailbreaking-iphone-rooting-android-does-not-void-warranty|title=Companies Can’t Legally Void the Warranty for Jailbreaking or Rooting Your Phone|quote=The Magnuson-Moss Warranty Act, passed by Congress in 1975, notes that “a warrantor cannot, as a matter of law, avoid liability under a written warranty where a defect is unrelated to the use by a consumer of ‘unauthorized’ articles or service.”|publisher={{tsl|en|Vice Media||Vice Media}}}}</ref>对于某些设备而言，使用刷新自制固件的方法来清除e-fuse是可能的。<ref>{{cite web|url=http://forum.xda-developers.com/showpost.php?p=52329946&postcount=76|title=A few things on knox|quote=This has been tested & working on Note 3 N900/Exynos on KitKat ND1 firmware which was on official status without root but Knox triggered, The file was flashed using Odin and after flashing I went into download mode and to my surprise Knox {{sic|hide=y|was| been|expected=had been}} reset from 0x1 to 0|publisher=[[XDA_Developers|XDA Developers]]}}</ref>

== 参考文献 ==
{{reflist|30em}}

== 外部链接 ==
*{{Official website|http://www.samsungknox.com/en}}
* [http://www.samsungknox.cn 中国官网]

{{Samsung Electronics}}

[[Category:行動軟體|Category:行動軟體]]
[[Category:三星軟體|Knox]]