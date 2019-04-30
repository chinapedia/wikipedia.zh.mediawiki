{{NoteTA|G1=IT|G2=Windows}}
'''微软POSIX子系统'''[[Windows_NT|Windows NT]]家族[[操作系统|操作系统]]的三个[[子系统|子系统]]之一（另两个是[[OS/2|OS/2]]和Windows子系统）。

[[Microsoft_Windows|微软Windows]]只实现了[[POSIX|POSIX]]标准的首个版本，即POSIX.1。POSIX.1的官方代码是ISO/IEC 9945-1:1990或[[电气电子工程师学会|IEEE]]标准1003.1-1990。引入此子系统是因为1980年代[[美國聯邦政府|美國聯邦政府]]在[[聯邦資料處理標準|聯邦資料處理標準]]（FIPS）151-2中列出的要求。<ref>{{Cite web|url=http://www.itl.nist.gov/fipspubs/fip151-2.htm|title=Federal Information Processing Standards Publication 151-2|deadurl=yes|archiveurl=https://web.archive.org/web/20080908065342/http://www.itl.nist.gov/fipspubs/fip151-2.htm|archivedate=2008年9月8日|df=}}</ref> [[Windows_NT_3.5|Windows NT 3.5]]、[[Windows_NT_3.51|Windows NT 3.51]]和[[Windows_NT_4|Windows NT 4]]被认定完全兼容FIPS 151-2。

此子系统是由两个文件提供的[[运行时系统|运行时环境]]：'''psxss.exe'''和'''psxdll.dll'''。POSIX应用程序使用'''psxdll.dll'''与此子系统通信，以及'''posix.exe'''在Windows桌面上提供显示功能。

此POSIX子系统在Windows XP和Windows Server 2003中已被移除。它被使用{{tsl|en|Interix}}子系统的“{{tsl|en|Windows Services for UNIX}}”取代<ref>{{Cite web|url=http://support.microsoft.com/kb/308259|title=POSIX and OS/2 are not supported in Windows XP or in Windows Server 2003}}</ref>。

== 参见 ==
* {{tsl|en|MKS Toolkit}}
* {{tsl|en|UWIN}}
* [[Cygwin|Cygwin]]
* {{tsl|en|UnxUtils}}

== 注释 ==
{{Reflist}}

== 参考资料 ==
{{refbegin}}
* {{cite book
|author = [[Mark_Russinovich|Russinovich, Mark]]
|author2=David Solomon |authorlink2=David A. Solomon
|date = December 8, 2004
|title = '''Microsoft Windows Internals'''
|edition = (Fourth Edition)
|publisher = Microsoft Press
|isbn = 0-7356-1917-4
}}
{{refend}}

{{Windows Components}}

[[Category:Windows组件|Category:Windows组件]]
[[Category:POSIX|Category:POSIX]]
[[Category:兼容层|Category:兼容层]]

{{Windows-stub}}