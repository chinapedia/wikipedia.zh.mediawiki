{{orphan|time=2018-09-14T00:19:41+00:00}}
{{noteTA
|G1=IT
}}
'''用户ID'''（{{lang-en|'''user identifier'''}}，一般缩写为'''User ID'''或'''UID'''），全称'''用户标识符'''，在[[类UNIX系统|类UNIX系统]]中是[[内核|内核]]用来辨识用户的一个无符号[[整型|整型]]数值，亦是[[UNIX|UNIX]][[文件系统|文件系统]]与[[进程|进程]]的必要组成部分之一。

== 数值范围 ==
在不同的系统中，UID的值的范围也有所不同，但一般来说UID都是由一个15位的整数表示，其范围在0～32767之内，且有如下限制：

* [[超级用户|超级用户]]的UID总为0；

* 按传统的做法，“{{Tsl|en|Nobody_(username)|Nobody (用户名)|nobody}}”（类UNIX系统的一种特殊账户）与超级用户相反，总占有数值最大的PID，即32767；相对应的，现今的系统为nobody分配的UID则在系统保留范围（1～100）或是65530-65535的范围内<ref name="db01">{{cite web | url=http://www.debianhelp.co.uk/usersid.htm | title=Usernames and User IDs in Debian Linux | author=DebianHelp.co.uk }}{{Dead link|date=2018年6月 |bot=InternetArchiveBot |fix-attempted=no }}</ref>。

* 数值于1～100内的UID约定预留给系统使用，有些手册则推荐在此基础上再预留101～499（如[[RHEL|RHEL]]<ref name="rh01">{{cite web | url=http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/4/html/Introduction_To_System_Administration/s1-acctsgrps-rhlspec.html | title=Red Hat Enterprise Linux-Specific Information | accessdate=2011-12-22 | author=Red Hat Documents}}</ref>）甚至是101～999（如[[Debian|Debian]]<ref name="db01" />）的UID以作备用；而相对应的，在Linux中用useradd命令创建第一个用户时,默认为之分配的UID则为1000。

除此之外,有些特殊的系统也支持16位的UID,因而UID的数目可以扩展到65536个；现代系统支持32位的UID，这也使UID数目进一步扩充到4,294,967,296个成为可能。

== 分类 ==

=== 有效用户ID ===
'''有效用户ID'''（''Effective UID''，即EUID）与'''有效用户组ID'''（''Effective Group ID''，即EGID）在创建与访问[[文件|文件]]的时候发挥作用；具体来说，创建文件时，系统内核将根据创建文件的进程的EUID与EGID设定文件的所有者/组属性，而在访问文件时，内核亦根据访问进程的EUID与EGID决定其能否访问文件。

=== 真实用户ID ===
'''真实用户ID'''（''Real UID'',即RUID）与'''真实用户组ID'''（''Real GID''，即RGID）用于辨识进程的真正所有者，且会影响到进程发送[[信号_(计算机科学)|信号]]的权限。没有超级用户权限的进程仅在其RUID与目标进程的RUID相匹配时才能向目标进程发送信号，例如在父子进程间，[[子进程|子进程]]从[[父进程|父进程]]处继承了认证信息，使得父子进程间可以互相发送信号。

=== 暂存用户ID ===
'''暂存用户ID'''（''Saved UID''，即'''SUID'''）于以提升权限运行的进程暂时需要做一些不需{{Tsl|en|Privilege (computing)|特权 (计算机科学)|特权}}的操作时使用，这种情况下进程会暂时将自己的有效用户ID从特权用户（常为[[超级用户|root]]）对应的UID变为某个非特权用户对应的UID，而后将原有的特权用户UID复制为SUID暂存；之后当进程完成不需特权的操作后，进程使用SUID的值重置EUID以重新获得特权。在这里需要说明的是，无特权进程的EUID值只能设为与RUID、SUID与EUID（也即不改变）之一相同的值。

=== 文件系统用户ID ===
'''文件系统用户ID'''（''File System UID''，即'''FSUID'''）在[[Linux|Linux]]中使用，且只用于对文件系统的[[文件系统权限|访问权限]]控制，在没有明确设定的情况下与EUID相同（若FSUID为root的UID，则SUID、RUID与EUID必至少有一亦为root的UID），且EUID改变也会影响到FSUID。设立FSUID是为了允许程序（如[[NFS|NFS]]服务器）在不需获取向给定UID账户发送信号的情况下以给定UID的权限来限定自己的文件系统权限。

== 杂项 ==
*UID的数值与用户账户的对应关系存放于[[Shadow_(文件系统)|/etc/passwd]]中<ref name="ut01">{{cite web | url=http://www.unixtutorial.org/2008/01/how-to-find-uid-in-unix/ | title=''How To Find Out User ID in Unix'' | author=UnixTutorial.org}}</ref>。用于存放密码的/etc/shadow以及[[NIS|网络信息服务]]也以UID的数值标识用户，但现在Linux系统下的shadow文件已经改用账户名来标识用户。

*在遵循POSIX的环境中，'''id'''这一命令可以给出当前用户的用户名、所属组及对应的UID、GID的值<ref name="ut01" />。

== 参考文献 ==
=== 引用 ===
{{Reflist|30em}}

=== 来源 ===
{{refbegin}}
* 《[[UNIX环境高级编程|UNIX环境高级编程]]》, 理查德·史蒂文斯 著
{{refend}}

== 外部链接 ==

== 参见 ==
* [[文件系统权限|文件系统权限]]

[[Category:计算机科学|Category:计算机科学]]
[[Category:操作系统|Category:操作系统]]