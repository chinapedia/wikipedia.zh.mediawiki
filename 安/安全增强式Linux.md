{{noteTA
|G1=IT
}}
{{Infobox software
| name                   = SELinux
| title                  = 
| logo                   = SELinux logo.svg
| logo caption           = 
| logo_size              = 

| logo_alt               = 
| screenshot             = SELinux admin.png
| caption                = [[Fedora|Fedora 8]]中的SELinux管理界面
| screenshot_size        = 
| screenshot_alt         = 
| collapsible            = 
| author                 = [[NSA|NSA]]与[[Red_Hat|Red Hat]]
| developer              = [[Red_Hat|Red Hat]]
| released               = {{Start date and age|1998|01|01|}}
| discontinued           = 
| latest release version = 2.9
| latest release date    = {{Start date and age|2019|03|15|df=yes}}<ref>{{cite web |url=https://github.com/SELinuxProject/selinux/wiki/Releases |title=Release 2019-03-15 |first=Steve |last=Lawrence |work=selinux |publisher=SELinux Project |date=2019-03-15 |accessdate=2019-03-15}}</ref>
| latest preview version = 
| latest preview date    = <!-- {{Start date and age|YYYY|MM|DD|df=yes/no}} -->
| frequently updated     = <!-- DO NOT include this parameter unless you know what it does -->
| status                 = 
| programming language   = [[C_(编程语言)|C]]
| operating system       = [[Linux|Linux]]
| platform               = 
| size                   = 
| language               = 
| language count         = <!-- DO NOT include this parameter unless you know what it does -->
| language footnote      = 
| genre                  = 安全性、 [[Linux安全模块|Linux安全模块]] （LSM）
| license                = [[GNU_GPL|GNU GPL]]
| website                = {{URL|selinuxproject.org/page/Main_Page|SELinuxProject.org/page/Main Page}}
| standard               = 
| AsOf                   = 
}}

'''安全增強式Linux'''（SELinux，Security-Enhanced Linux）是一个[[Linux内核|Linux内核]]的[[Linux安全模组|安全模组]]，其提供了访问控制安全策略机制，包括了[[美国国防部|美国国防部]]风格的[[强制访问控制|强制访问控制]]（Mandatory Access Control，MAC）。

SELinux是一系列添加到多个[[Linux发行版|Linux发行版]]的内核修改与用户空间工具。其[[软件架构|软件架构]]力图从安全策略中分离出执行安全决策并优化涉及执行安全策略的软件。<ref>{{cite web|url=https://www.nsa.gov/what-we-do/research/selinux/faqs.shtml |title=SELinux Frequently Asked Questions (FAQ) - NSA/CSS |publisher=National Security Agency |date= |accessdate=2013-02-06}}</ref><ref>{{cite web |first=Peter |last=Loscocco |first2=Stephen |last2=Smalley |date=February 2001 |title=Integrating Flexible Support for Security Policies into the Linux Operating System |url=https://www.nsa.gov/resources/everyone/digital-media-center/publications/research-papers/assets/files/flexible-support-for-security-policies-into-linux-feb2001-report.pdf }}</ref>奠基SELinux的核心概念可以追溯回[[美国国家安全局|美国国家安全局]]（NSA）的一些早期项目。

== 概览 ==

美国国家安全局的安全增强式Linux团队称：<ref>{{cite web |url=https://www.nsa.gov/what-we-do/research/selinux/ |title=Security-Enhanced Linux - NSA/CSS |publisher=National Security Agency |date=2009-01-15 |accessdate=2013-02-06}}</ref>

<blockquote>安全增強式Linux是一組給Linux核心的[[修補程式|修補程式]]，並提供一些更強、更安全的強制存取控制架構來和核心的主要子系統共同運作。基於機密及完整性原則，它提供一個架構來強制資訊的分離，以對付入侵的威脅或任何企圖略過安全架構的應用程式。藉此限制惡意或設計不良的程式可能造成的破壞。它包含一組安全性原則組態設定檔的範本以符合一般的安全性目標</blockquote>

整合SELinux的Linux内核将执行限制用户程序和系统服务器访问文件与网络资源的强制访问控制策略。将权限限制到最小以减少或完全清除程序和[[守护进程|守护进程]]在失效或出错的情况（如[[缓存区溢出|缓存区溢出]]或错误配置）下对系统造成危害的可能性。此种限制机制独立与于传统的Linux[[自主访问控制|自主访问控制]]（Discretionary Access Control, DAC）进行。SELinux没有[[超级用户|“root”用户]]的概念，也没有传统Linux安全机制的缺点。（如依赖于[[setuid|setuid]]/{{tsl|en|setgid||setgid}}库）

“未修改过的”Linux系统安全性（即未整合SELinux的系统）依赖于内核、授权应用与其配置的正确性。三者中任意一个发生问题都将有可能导致整个系统被破解。相反，“修改过的”系统安全性（基于SELinux内核）主要基于其内核和配置的正确性。虽然当应用程序的正确性或配置出现问题可能会导致独立的用户程序和系统守护进程发生有限破解，但是它们并不会对其他用户程序和系统守护进程或整个系统的安全性造成威胁。

纯粹来看，SELinux提供了一个从强制访问控制、[[强制完整性控制|强制完整性控制]]、[[以角色為基礎的存取控制|以角色為基礎的存取控制]]和{{tsl|en|type enforcement architecture|类型强制架构|类型强制架构}}提取出的概念与功能的混合体。第三方工具可以使开发者构建多种安全策略。

== 历史 ==

早期工作主要指向在UNIX计算环境（准确而言是POSIX）下标准化强制和自主访问控制条款的方法。这归因于美国国家安全局受信UNIX（TRUSIX）工作组，他们在1987到1991年间接触并发布了一本{{tsl|en|Ranbow Series|彩虹系列|彩虹书}} （#020A），并制造了一个原初模型和最初未发布的关联评估证据原型（#020B）。

SELinux最初设计向Linux社区展示强制访问控制的价值和这些控制加入Linux的方法。起初，组成SELinux的补丁只能通过明确添加在Linux内核源码中来工作；在2.6系列的[[Linux内核|Linux内核]]中SELinux已被整合入。

作为最初SELinux的主要开发者，美国国家安全局于2000年12月22日基于[[GNU通用公共许可证|GNU通用公共许可证]]發行了第一版SELinux給了[[開放原始碼|開放原始碼]]開發社群。<ref>
比较
{{cite web
|url         = https://www.nsa.gov/news-features/press-room/press-releases/2001/se-linux.shtml
|title       = National Security Agency Shares Security Enhancements to Linux
|date        = 2001-01-02
|work        = NSA Press Release
|publisher   = National Security Agency Central Security Service
|location    = Fort George G. Meade, Maryland
|accessdate  = 2011-11-17
|quote       = The NSA is pleased to announce that it has developed, and is making available to the public, a prototype version of a security-enhanced Linux operating system.
}}
</ref>

SELinux随后被整合进了Linux内核2.6.0-test3版本的主分支，并在2003年8月8日发布。其他的显要贡献者有[[紅帽公司|紅帽公司]]、[[迈克菲|迈克菲]]、{{tsl|en|Secure Computing Corporation|安全计算公司|安全计算公司}}、特瑟思科技（Tresys Technology）和可信计算机解决方案（Trusted Computer Solutions）。{{tsl|en|FLASK||FLASK}}/TE实现通过[[FreeBSD|FreeBSD]]项目成功移植到了[[FreeBSD|FreeBSD]]和[[Darwin_(操作系统)|Darwin]]操作系统上。

SELinux实现了{{tsl|en|FLASK|FLASK|通量高级安全内核}}。这种内核包含了以{{tsl|en|Fluke operating system|锚爪操作系统|锚爪操作系统}}为原型的架构部件。这些提供给了强制执行多种强制访问控制策略许多通常支持，包括了基于{{tsl|en|type enforcement|类型强制|类型强制}}、[[以角色為基礎的存取控制|以角色為基礎的存取控制]]和{{tsl|en|multilevel security|多层安全|多层安全}}概念的策略。FLASK基于马赫衍生的（Mach-derived）{{tsl|en|Distributed Trusted Operating System|分布式受信操作系统|分布式受信操作系统}}（DTOS）和来自对DTOS的设计和实现有着影响的{{tsl|en|Trusted Information System|受信信息系统|受信信息系统}}的一个研究项目——受信马赫（Trusted Mach）。

== 用户、策略和安全上下文 ==

SELinux用户和角色不需要与实际系统用户与角色相关。对每个正在进行的用户或进程，SELinux分配一个三字符串上下文，包含了用户名、角色和域（或者类型）。此系统比通常所需要的系统更灵活：作为规定之一，大多数真实用户享有着相同的SELinux用户名，且所有的访问控制都经由第三个标签——域来进行。在一个进程被允许进入域的情况下必须在策略中配置。命令<code>runcon</code>允许启动进程进入一个显性定义上下文（用户、角色和域）环境中，但如果政策中未允许的话那么SELinux可能会拒绝此请求。

文件、网络端口和其他硬件均有可能含有SELinux上下文，有一个名字、角色（不常使用）和类型组成。文件系统在文件和安全上下文之间的映射被称为标记（Labeling）。标记在策略文件中被定义但也可以在不更改策略的情况下手动调整。硬件类型十分详细，比如<code>bin_t</code>（显示/bin下的所有文件）或<code>postgresql_port_t</code>（PostgreSQL端口5432）。远程文件系统的SELinux上下文可以在被挂载时显性定义。

SELinux给Shell命令<code>ls</code>、<code>ps</code>等中添加了<code>-Z</code>开关使得文件或进程的安全上下文可见。

典型的政策规则包含了显性权限；用户必须拥有哪些域才能用给定目标进行特定的行为（读、执行，网络端口中则是绑定或连接）等等。也可以进行更多复杂的映射，包括在角色级和安全级进行。

一个典型的策略包含了一个映射文件（标记）文件、一个规则文件和一个定义域过渡的界面文件。这三个文件必须被同时使用SELinux工具编译来生成单一的策略文件。生成的策略文件可以被载入到内核中并工作。载入和卸载策略并不需要重启。策略文件既有可能是手打也可能是用容易使用的SELinux管理工具生成。它们通常先在允许模式（Permissive Mode）下测试，在此模式下违反策略的行为都将被记录但被允许。<code>audit2allow</code>工具可以随后使用来生成扩展SELinux策略以允许受限应用的合法活动的附加规则。

== {{Anchor|AVC}}特性 ==
SELinux特性包含了：

* 在执行情况下将策略完全分离
* 定义充分的策略界面
* 支持问询策略并执行访问控制的应用程序（例如[[Cron|Cron]]在正确的上下文环境中运行工作）
* 独立于特定政策和策略语言
* 独立于特定安全标签格式与内容
* 对内核目标和服务的独立标记
* 支持策略更改
* 分离保护系统完整性（域名类）和数据保密（{{tsl|en|multilevel security|多层安全|多层安全}}）的措施
* 灵活的策略
* 控制进程初始化与继承和程序执行
* 控制文件系统、目录、文件和开放性[[文件描述符|文件描述符]]
* 控制套接字、信息和网络界面
* 控制使用“容量”（Capabilities）
* 在访问决定中通过''访问向量缓存''（Access Vector Cache, AVC）预缓存信息<ref>
{{cite book
| author     = Fedora Documentation Project
| title      = Fedora 13 Security-Enhanced Linux User Guide
| url        = https://books.google.com/books?id=feDeO4IglRkC
| accessdate = 2012-02-22
| year       = 2010
| publisher  = Fultus Corporation
| isbn       = 978-1-59682-215-3
| page       = 18
| quote      = SELinux decisions, such as allowing or disallowing access, are cached. This cache is known as the Access Vector Cache (AVC). Caching decisions decreases how often SELinux rules need to checked, which increases performance.
}}
</ref>

== 实现 ==

SELinux通过[[Red_Hat_Enterprise_Linux|Red Hat Enterprise Linux]]第四版及其所有未来的发行版中的商业支持得以可用。它的存在也在对应版本的[[CentOS|CentOS]]和[[Scientific_Linux|Scientific Linux]]中呈现。RHEL4中所支持的策略目标为最大化简易使用程度而并没有它能成为的那样有约束性。RHEL的未来版本准备将在目标策略中写入更多的目标，也就意味着有更多的限制策略。SELinux在[[Android|Android]]4.3版本中就已得以实现。<ref>{{cite web | title=Security-Enhanced Linux in Android | accessdate=2016-01-31 | publisher=Android Open Source Project | url=https://source.android.com/security/selinux/}}</ref>

在自由社区所支持的GNU/Linux发行版中，[[Fedora|Fedora]]是最早采用SELinux的，在Fedora Core 2中就已默认包含了对其的支持。其他发行版中，[[Debian|Debian]]在Etch发行版中包含了对它的支持<ref>{{cite web|url=https://wiki.debian.org/SELinux|title=SELinux|work=debian.org}}</ref>，[[Ubuntu|Ubuntu]]则在8.04版代号坚强的苍鹭（Hardy Heron）中加入。<ref>{{cite web|url=https://ubuntu-tutorials.com/2008/03/18/how-to-install-selinux-on-ubuntu-804-hardy-heron/|title=How To Install SELinux on Ubuntu 8.04 "Hardy Heron"|work=Ubuntu Tutorials}}</ref>截止[[SUSE|SUSE]]版本11.1中，它包含了SELinux的“基础实现”。<ref>{{cite web|url=https://news.opensuse.org/2008/08/20/opensuse-to-add-selinux-basic-enablement-in-111/ |title=openSUSE News|work=openSUSE News}}</ref> {{tsl|en|SUSE Linux Enterprise|SUSE Linux Enterprise|SUSE Linux Enterprise}} 11将SELinux作为“技术预览”。<ref>{{cite web|url=https://www.novell.com/linux/releasenotes/x86_64/SUSE-SLED/11/#02 |title=Release Notes for SUSE Linux Enterprise Desktop 11 |publisher=[[Novell|Novell]] |date= |accessdate=2013-02-06}}</ref>

SELinux在基于{{tsl|en|linux containers|Linux容器|Linux容器}}的系统中流向,比如[[CoreOS|CoreOS]]和rkt。<ref>{{cite web|url=https://coreos.com/os/docs/latest/selinux.html |title=SELinux on CoreOS|work=CoreOS Docs}}</ref>其作为额外的安全控制来帮助隔离容器和它们的主机十分有用。

== 使用情形 ==

SELinux可以潜在地通过详细的参数来控制允许系统每个用户的活动、进程以及守护进程。但是，它主要用于限制[[守护进程|守护进程]]比如被更显著定义数据访问和活动权限的数据库引擎或者网页服务器。这限制了被破解的限制守护进程的潜在危害。普通的用户进程通常运行于受限域中，不被SELinux所限制但被经典Linux访问权限所限制。

命令行工具包含：<ref>{{cite web|url=https://fedoraproject.org/wiki/SELinux/Commands |title=SELinux/Commands - FedoraProject |accessdate=2015-11-25}}</ref>
<code>chcon</code>,<ref>{{cite web |url=http://linuxcommand.org/man_pages/chcon1.html |title=chcon |publisher=Linuxcommand.org |date= |accessdate=2013-02-06 }}{{dead link|date=2018年5月 |bot=InternetArchiveBot |fix-attempted=yes }}</ref>
<code>restorecon</code>,<ref>{{cite web|url=http://linux.die.net/man/8/restorecon |title=restorecon(8) - Linux man page |publisher=Linux.die.net |date= |accessdate=2013-02-06}}</ref>
<code>restorecond</code>,<ref>{{cite web|url=http://linux.die.net/man/8/restorecond |title=restorecond(8) - Linux man page |publisher=Linux.die.net |date= |accessdate=2013-02-06}}</ref>
<code>runcon</code>,<ref>{{cite web|url=http://linux.die.net/man/1/runcon |title=runcon(1) - Linux man page |publisher=Linux.die.net |date= |accessdate=2013-02-06}}</ref>
<code>secon</code>,<ref>{{cite web|url=http://linux.die.net/man/1/secon |title=secon(1) - Linux man page |publisher=Linux.die.net |date= |accessdate=2013-02-06}}</ref>
<code>fixfiles</code>,<ref>{{cite web|url=http://linux.die.net/man/8/fixfiles |title=fixfiles(8): fix file SELinux security contexts - Linux man page |publisher=Linux.die.net |date= |accessdate=2013-02-06}}</ref>
<code>setfiles</code>,<ref name="auto">{{cite web|url=http://linux.die.net/man/8/setfiles |title=setfiles(8): set file SELinux security contexts - Linux man page |publisher=Linux.die.net |date= |accessdate=2013-02-06}}</ref>
<code>load_policy</code>,<ref>{{cite web|url=http://linux.die.net/man/8/load_policy |title=load_policy(8) - Linux man page |publisher=Linux.die.net |date= |accessdate=2013-02-06}}</ref>
<code>booleans</code>,<ref>{{cite web|url=http://linux.die.net/man/8/booleans |title=booleans(8) - Linux man page |publisher=Linux.die.net |date= |accessdate=2013-02-06}}</ref>
<code>getsebool</code>,<ref>{{cite web|url=http://linux.die.net/man/8/getsebool |title=getsebool(8): SELinux boolean value - Linux man page |publisher=Linux.die.net |date= |accessdate=2013-02-06}}</ref>
<code>setsebool</code>,<ref>{{cite web|url=http://linux.die.net/man/8/setsebool |title=setsebool(8): set SELinux boolean value - Linux man page |publisher=Linux.die.net |date= |accessdate=2013-02-06}}</ref>
<code>togglesebool</code><ref>{{cite web|url=http://linux.die.net/man/8/togglesebool |title=togglesebool(8) - Linux man page |publisher=Linux.die.net |date= |accessdate=2013-02-06}}</ref>
<code>setenforce</code>,
<code>semodule</code>,
<code>postfix-nochroot</code>,
<code>check-selinux-installation</code>,
<code>semodule_package</code>,
<code>checkmodule</code>,
<code>selinux-config-enforcing</code>,<ref>{{cite web |url=http://manpages.ubuntu.com/manpages/natty/man8/selinux-config-enforcing.8.html |title=Ubuntu Manpage: selinux-config-enforcing - change /etc/selinux/config to set enforcing |publisher=[[Canonical|Canonical]] |date= |accessdate=2013-02-06 |deadurl=yes |archiveurl=https://web.archive.org/web/20121220020432/http://manpages.ubuntu.com/manpages/natty/man8/selinux-config-enforcing.8.html |archivedate=2012-12-20 }}</ref>
<code>selinuxenabled</code>,<ref>{{cite web |url=http://manpages.ubuntu.com/manpages/natty/man1/selinuxenabled.1.html |title=Ubuntu Manpage: selinuxenabled - tool to be used within shell scripts to determine if |publisher=[[Canonical|Canonical]] |date= |accessdate=2013-02-06 |deadurl=yes |archiveurl=https://web.archive.org/web/20130209033811/http://manpages.ubuntu.com/manpages/natty/man1/selinuxenabled.1.html |archivedate=2013-02-09 }}</ref>
and <code>selinux-policy-upgrade</code><ref>{{cite web |url=http://manpages.ubuntu.com/manpages/natty/man8/selinux-policy-upgrade.8.html |title=Ubuntu Manpage: selinux-policy-upgrade - upgrade the modules in the SE Linux policy |publisher=[[Canonical|Canonical]] |date= |accessdate=2013-02-06 |deadurl=yes |archiveurl=https://web.archive.org/web/20120404160143/http://manpages.ubuntu.com/manpages/natty/man8/selinux-policy-upgrade.8.html |archivedate=2012-04-04 }}</ref>

== 示例 == 

将SELinux设置为强制模式（Enforcing Mode）：
:<code>$ sudo setenforce 1</code>
查询SELinux状态：
:<code>$ getenforce</code>

== 与AppArmor的对比 ==

SELinux代表了多个可能解决限制安装软件活动的方法之一。另外一个受欢迎的替代品被称为[[AppArmor|AppArmor]]，它在{{tsl|en|SUSE Linux Enterprise Server|SUSE Linux Enterprise Server|SUSE Linux Enterprise Server}}（SLES）、[[OpenSUSE|OpenSUSE]]和[[Linux发行版列表|其他Linux]]平台中可用。AppArmor原初是作为现不存在的{{tsl|en|Immunix|Immunix|Immunix Linux}}平台组件之一开发的。由于AppArmor和SELinux大相径庭，它们产生了两种完全不同的软件访问限制软件。虽然SELinux重新提出了特定的概念以提供更丰富的策略选择表达集，但AppArmor通过扩展用于自主访问控制级的特定相同[[自主访问控制|自主访问控制]]管理语言设计来简化其使用。

它们之间存在几个显著的不同：
* 一个重要的不同是AppArmor通过路径名而非通过索引节点来识别文件系统目标。打个比方，这意味着一个文件不可访问的文件可能在AppArmor创建硬链接的情况下得以访问，而SELinux则会通过新建立的硬链接来阻止访问。
** 结果，AppArmor可被称为不是一个[[类型强制|类型强制]]系统，因为文件并没有被分配类型；相反，它们仅仅在配置文件中被引用。
* SELinux和AppArmor在它们如何管理和整合系统的方面也存在着极大的不同。<ref>{{cite web | url= https://www.suse.com/documentation/sles11/book_security/data/sect1_chapter_book_security.html |publisher= SUSE |series= Security Guide |work= SELinux |title= SELinux backgrounds }}</ref>
* 由于其寻求使用强制访问控制级执行来重建传统的自主访问控制，AppArmor的一系列操作也认为比大多数SELinux实现要小得多。例如，AppArmor的一系列操作包含了：读、写、附加、执行、锁定和链接。<ref>{{cite web | url=http://manpages.ubuntu.com/manpages/hardy/man5/apparmor.d.5.html | title=apparmor.d - syntax of security profiles for AppArmor | deadurl=yes | archiveurl=https://web.archive.org/web/20131017094320/http://manpages.ubuntu.com/manpages/hardy/man5/apparmor.d.5.html | archivedate=2013-10-17 }}</ref>大多数的SELinux实现将支持一系列多于其的操作序列。比如，SELinux通常支持相同权限，但同时对于mknod包含了控制、绑定到网络包、隐性使用POSIX的能力、加载并卸载内核模块和多种访问共享内存的方法等。
* AppArmor没有能明确限制POSIX功能的控制项。由于当前功能实现的方法不包含操作主题的概念（只有执行者和操作本身），防止执行者外的强制控制领域（即[[沙箱|沙箱]]）授权文件操作通常由MAC层完成。AppArmor可以防止其策略被更改和文件系统被挂载/卸载，但不能防止用户踏出他们的控制域。
** 例如，人们通常认为桌面员工更改他们所不拥有的特定文件（例如：部门文件共享）的所有权或权限是有益的。你绝对不会想给用户机器的root权限，所以你会给他们<code>CAP_FOWNER</code>或<code>CAP_DAC_OVERRIDE</code>。在SELinux下（或你的平台制造商下），你可以配置SELinux来禁止所有其他未受限用户的能力，然后新建一个给员工的受限域以在登陆后进行过渡。这种情况可以给员工修改权限的能力，但仅限于合适类型的文件。 
* AppArmor没有多层安全的概念，因此也没有硬性的{{tsl|en|Bell–LaPadula model|贝尔-拉帕杜拉模型|贝尔-拉帕杜拉模型}}或{{tsl|en|Biba Model|比巴模型|比巴模型}}强制执行。
* AppArmor的配置通过唯一常规平面文件完成。SELinux（在大多数实现中为默认）则使用平面文件组合（在编译前由管理员和开发者编写人类可读的策略）和扩展属性完成。
* SELinux支持作为策略配置替代源的"远程策略服务器"概念（可在/etc/selinux/semanage.conf中配置）。AppArmor的中心化管理通常十分复杂，这是因为管理员必须决定策略部署工具以root权限运行（以允许策略更新）或在每台服务器上被手动配置。
* 
== 相似系统 ==
{{See also|Samsung Knox}}

孤立进程也可以通过类似[[作業系統層虛擬化|作業系統層虛擬化]]的机制实现；比如在[[OLPC|OLPC]]项目的首次实现中<ref>{{cite web|url=http://wiki.laptop.org/go/Rainbow|title=Rainbow|work=laptop.org}}</ref>它使用了[[沙盒_(電腦安全)|沙盒技术]]在轻量的{{tsl|en|Vserver|Vserver|Vserver}}环境中隔离独立的应用程序。同样[[美国国家安全局|美国国家安全局]]也在安全增强型[[Android|Android]]中采用了一些SELinux概念。<ref>{{cite web |title=
SELinux Related Work |work=NSA.gov |url=https://www.nsa.gov/what-we-do/research/selinux/related-work/ }}</ref>

== 参见 ==
{{Portal|Computer security|Linux}}
{{Columns-list|2|
* {{tsl|en|Grsecurity|Grsecurity|Grsecurity}}
* [[以規則集為基礎的存取控制|以規則集為基礎的存取控制]]
* {{tsl|en|Simplified Mandatory Access Control Kernel|简化强制访问控制内核|简化强制访问控制内核}}
* {{tsl|en|Solaris Trusted Extensions|Solaris受信扩展|Solaris受信扩展}}
* {{tsl|en|TOMOYO Linux|TOMOYO Linux|TOMOYO Linux}}
* [[FreeBSD|FreeBSD]]
* [[Qubes_OS|Qubes OS]]
}}

== 参考文献 ==
{{Reflist|30em}}

== 外部链接 ==
* {{Official website|https://selinuxproject.org/}}
* NSA:
** [https://www.nsa.gov/what-we-do/research/selinux/ Security-Enhanced Linux] at NSA
** [https://www.nsa.gov/what-we-do/research/selinux/mailing-list.shtml Mailing list]
** {{cite web |url= https://www.nsa.gov/news-features/press-room/press-releases/2001/se-linux.shtml  |work= Press release |title= NSA shares security enhancements to Linux |date= Jan 2, 2001 }}
* {{Github|SELinuxProject/selinux/wiki|SELinux}}
* {{cite web |url= https://opensource.com/business/13/11/selinux-policy-guide |title= Visual how-to guide for SELinux policy enforcement |date= 13 Nov 2013 |first= Daniel J |last= Walsh |publisher= Opensource.com }}

{{Linux内核}}
{{Linux}}

{{Authority control}}

[[Category:Linux内核功能|Category:Linux内核功能]]
[[Category:Linux安全软件|Category:Linux安全软件]]
[[Category:美国国家安全局|Category:美国国家安全局]]
[[Category:红帽软件|Category:红帽软件]]
[[Category:Unix文件系统技术|Category:Unix文件系统技术]]