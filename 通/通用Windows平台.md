{{noteTA
|G1=IT
|G2=Windows
|zh-cn:激活; zh-tw:啟用; zh-hk:啟用;
|zh-cn:任务栏; zh-tw:工具列; zh-hk:工作列;
|zh-cn:更新程序; zh-tw:更新檔;
|zh-cn:在线; zh-tw:線上;zh-hk:線上
|zh-cn:应用程序; zh-tw:應用程式;zh-hk:應用程式
|zh-cn:操作系统; zh-tw:作業系統;zh-hk:作業系統
|zh-cn:屏幕; zh-tw:螢幕;zh-hk:螢幕
|zh-cn:快捷方式; zh-tw:捷徑;zh-hk:捷徑
|zh-cn:后台; zh-tw:背景;zh-hk:後台
|zh-cn:通过; zh-tw:透過;zh-hk:透過
|zh-cn:禁用; zh-tw:停用;zh-hk:停用
}}
{{Infobox_Windows_component
| name                = Universal Windows Platform
| os                  = [[Microsoft_Windows|Microsoft Windows]]
| logo                =
| logo_size           =
| logo_caption        =
| screenshot          =
| screenshot_size     =
| caption             =
| other_names         = 
| type                = [[应用程序编程接口|应用程序编程接口]]
| service_name        =
| service_description =
| included_with       = [[Windows_10|Windows 10]]、[[Windows_10_Mobile|Windows 10 Mobile]]、[[Windows_Server_2016|Windows Server 2016]]
| also_available_for  =
| replaces            = [[Windows_Runtime|Windows Runtime]]
| replaced_by         =
| support_status      = 活跃
| related_components  = [[Windows_Store|Windows Store]]、[[Windows_API|Windows API]]
}}
'''通用Windows平台'''（'''Universal Windows Platform'''，简称'''UWP'''）是[[微软|微软公司]]建立并在[[Windows_10|Windows 10]]中首次引入的一个同性質應用程式架构平台。此软件平台的目的是帮助发展[[Metro-style_apps|Metro样式的應用程式]]，便于軟體可以在[[Windows_10|Windows 10]]和[[Windows_10行動版|Windows 10 Mobile]]上執行且无需重新編寫。它支援使用[[C++|C++]]、[[C♯|C#]]、[[Visual_Basic_.NET|VB.NET]]或[[XAML|XAML]]开发的[[Microsoft_Windows|Windows]]應用程式。API采用C++实现，并支持C++、VB.NET、C#和[[JavaScript|JavaScript]]。<ref name="MicrosoftWhatIs">{{Template:Cite web|url=https://msdn.microsoft.com/en-us/library/windows/apps/dn726767.aspx|title=What's a Universal Windows app?|accessdate=October 9, 2015|publisher=[[Microsoft|Microsoft]]|website=[[MSDN|MSDN]]}}</ref>UWP在[[Windows_Server_2012|Windows Server 2012]]和[[Windows_8|Windows 8]]中作为一个[[Windows_Runtime|Windows Runtime]]平台的扩展被首次引入，允许开发者创建可潜在运行在多种设备类型上的应用程序。<ref name="MicrosoftUWPIntro">{{Template:Cite web|url=https://msdn.microsoft.com/en-us/library/windows/apps/dn958439.aspx|title=Introduction to Universal Windows Platform (UWP) apps for designers|accessdate=October 9, 2015|publisher=[[Microsoft|Microsoft]]|website=[[MSDN|MSDN]]}}</ref>

== 兼容性 ==
UWP是Windows 10和Windows 10 Mobile的一部分。UWP應用程式不能在早期的[[微軟作業系統列表|Windows版本]]上執行。

应用程序能使用[[Microsoft_Visual_Studio|Visual Studio 2015]]进行此平台的原生开发。而面向[[Windows_8.1|Windows 8.1]]、[[Windows_Phone_8.1|Windows Phone 8.1]]及其两者（通用8.1）的旧版Metro應用程式需要一些修改才能迁移到UWP。<ref>{{Template:Cite web|url=https://msdn.microsoft.com/library/mt148501.aspx|title=Migrate apps to the Universal Windows Platform (UWP)|accessdate=31 July 2015|publisher=[[Microsoft|Microsoft]]|website=[[MSDN|MSDN]]}}</ref><ref>{{Template:Cite web|url=https://msdn.microsoft.com/en-us/library/windows/apps/xaml/mt238322.aspx|title=Move from Windows Runtime 8.x to UWP|accessdate=October 9, 2015|publisher=[[Microsoft|Microsoft]]|website=[[MSDN|Windows Developer Center]]}}</ref>

在[[Build_(开发者大会)|2015 Build]]期间，微软宣布了一个UWP“桥梁”集，允许[[Android|Android]]和[[iOS|iOS]]软件被移植到Windows 10 Mobile。<ref name="PCWorldWindowsBridge">{{Template:Cite web|url=http://www.pcworld.com/article/2960526/software-development/microsoft-releases-ios-to-windows-app-maker-windows-bridge-to-open-source.html|title=Microsoft releases iOS-to-Windows app maker Windows Bridge to open source|accessdate=October 9, 2015|date=August 6, 2015|last=Hachman|first=Mark|publisher=IDG|website=[[PC_World|PC World]]}}</ref> Windows Bridge for Android（代号“Astoria”）将允许使用Java或C++的Android應用程式被移植到Windows 10 Mobile和发布到[[Windows商店|Windows應用程式商店]]。Windows开发者平台的技术总监Kevin Gallo解释说，该层包含一些限制：Google Mobile服务和某些核心API将不可用，存在“深度集成到后台服务”的應用程式（如[[即时通信|通信]]软件）也不能在此环境下良好运行。<ref name="TechRadarLimits">{{Template:Cite web|url=http://www.techradar.com/us/news/software/applications/how-will-android-support-work-in-windows-10-mobile--1293295|title=How will Android support work in Windows 10 for Phones?|accessdate=October 9, 2015|date=May 11, 2015|last=Branscombe|first=Mary|website=[[TechRadar|TechRadar]]}}</ref><ref name="ArsTechnica">{{Template:Cite web|url=http://arstechnica.com/information-technology/2015/04/29/microsoft-brings-android-ios-apps-to-windows-10/|title=Microsoft brings Android, iOS apps to Windows 10|accessdate=October 9, 2015|date=April 29, 2015|last=Bright|first=Peter|website=[[Ars_Technica|Ars Technica]]}}</ref>Windows Bridge for iOS（代号“Islandwood”）是一个[[开源软件|开源中间件]]工具包，允许使用[[Objective-C|Objective-C]]开发的[[iOS|iOS]]软件使用[[Microsoft_Visual_Studio|Visual Studio 2015]]将[[Xcode|Xcode]]代码转换为Visual Studio项目以移植到Windows 10 Mobile。<ref name="PCWorldWindowsBridge">{{Template:Cite web|url=http://www.pcworld.com/article/2960526/software-development/microsoft-releases-ios-to-windows-app-maker-windows-bridge-to-open-source.html|title=Microsoft releases iOS-to-Windows app maker Windows Bridge to open source|accessdate=October 9, 2015|date=August 6, 2015|last=Hachman|first=Mark|publisher=IDG|website=[[PC_World|PC World]]}}</ref><ref name="AnandtechIslandwood">{{Template:Cite web|url=http://www.anandtech.com/show/9205/microsoft-demonstrates-android-and-ios-applications-running-on-windows-10|title=Microsoft Demonstrates Android and iOS Applications Running On Windows 10|accessdate=October 9, 2015|date=April 29, 2015|last=Chester|first=Brandon|publisher=Purch Inc.|website=[[Anandtech|Anandtech]]}}</ref><ref name="VentureBeatGuide">{{Template:Cite web|url=http://venturebeat.com/2015/05/01/everything-you-need-to-know-about-porting-android-and-ios-apps-to-windows-10/|title=Everything you need to know about porting Android and iOS apps to Windows 10|accessdate=October 9, 2015|date=May 1, 2015|last=Protalinski|first=Emil|website=[[VentureBeat|VentureBeat]]}}</ref>Windows Bridge for iOS的一个早期版本已使用[[MIT許可證|MIT许可证]]在2015年8月6日发布为一个开源软件，而Android版本仍在内部测试。<ref name="PCWorldWindowsBridge">{{Template:Cite web|url=http://www.pcworld.com/article/2960526/software-development/microsoft-releases-ios-to-windows-app-maker-windows-bridge-to-open-source.html|title=Microsoft releases iOS-to-Windows app maker Windows Bridge to open source|accessdate=October 9, 2015|date=August 6, 2015|last=Hachman|first=Mark|publisher=IDG|website=[[PC_World|PC World]]}}</ref>

2016年2月，微软宣布已经收购了位于旧金山的开发{{link-en|Xamarin|Xamarin}}软件的公司。<ref name="Xamarin">{{Template:Cite web|url=http://www.zdnet.com/article/microsoft-is-buying-mobile-tool-vendor-xamarin/|title=Microsoft is buying mobile tool vendor Xamarin|accessdate=February 26, 2016|date=February 24, 2016|last=Jo Foley|first=Mary|publisher=ZDNet}}</ref>此次收购后不久，微软宣布将放弃Android bridge项目，并计划支持在Windows 10上运行Android應用程式。他们的关注重点将主要集中在iOS bridge。<ref name="NoAndroid">{{Template:Cite web|url=http://www.zdnet.com/article/microsoft-our-android-windows-10-bridge-is-dead-but-ios-win32-ones-moving-ahead/|title=Microsoft: Our Android Windows 10 bridge is dead, but iOS, Win32 ones moving ahead|accessdate=February 26, 2016|date=February 25, 2016|last=Jo Foley|first=Mary|publisher=ZDNet}}</ref>

== 开发 ==
UWP是[[Windows_Runtime|Windows Runtime]]的一个扩展。采用UWP创建的“通用Windows应用程序”在其清单（manifest）构建中不再采用对特定操作系统的写法，相反，它们采用“通用Windows平台桥梁”针对一个或多个设备族群，例如[[个人电脑|个人电脑]]、[[智能手机|智能手机]]、[[平板電腦|平板电脑]]和[[Xbox_One|Xbox One]]。这些扩展允许应用程序自动利用当前运行设备中可用的功能。<ref name="VSMagBridges">{{Template:Cite web|url=https://visualstudiomagazine.com/articles/2015/05/01/inside-universal-windows-platform.aspx|title=Inside the Universal Windows Platform Bridges|accessdate=October 9, 2015|date=May 1, 2015|last=Domingo|first=Michael|publisher=Visual Studio Magazine}}</ref>通用應用程式即可以运行在智能手机上，也可以运行在平板电脑上，并为两者提供适当的体验。如果手机连接到一台桌面电脑或者一个合适的[[扩展坞|扩展坞]]，其上运行的通用應用程式还可能呈现为平板电脑上的体验。<ref>{{Template:Cite web|url=https://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn894631.aspx|title=Guide to Universal Windows Platform (UWP) apps|accessdate=October 9, 2015|publisher=[[Microsoft|Microsoft]]|website=[[MSDN|Windows Developers Center]]}}</ref>

== 反响 ==

=== 作为游戏平台 ===
UWP的游戏开发会受到技术限制，游戏可能无法做到桌面应用程序的所有功能，包括不兼容多显卡，无法禁用垂直同步，不能支持游戏模组，及不能使用游戏辅助软件如{{link-en|Fraps|Fraps}}、[[Steam|Steam]]游戏内界面和按键管理器等。<ref name="ars-novsync">{{Template:Cite web|url=http://arstechnica.co.uk/gaming/2016/02/microsoft-needs-to-stop-forcing-console-like-restrictions-on-windows-store-pc-games/|title=Microsoft needs to stop forcing console-like restrictions on Windows Store PC games|accessdate=30 March 2016|publisher=Conde Nast|website=Ars Technica}}</ref>[[Epic_Games|Epic Games]]创办人Tim Sweeney批评UWP是一个“[[封閉平臺|围墙花园]]”，默认情况下，UWP软件只能通过[[Windows商店|Windows應用程式商店]]安装，必须更改系统设置才能启用外部應用程式的安装（[[Android|Android]]系统有类似的设计）。此外，某些系统功能只能在UWP中调用，不能在基于[[Windows_API|Win32]]的软件中使用，这包括大多数PC电子游戏{{Dubious}}。Sweeny表示这些是“微软在以有史以来最激进的动作”，试图将PC转变为一个封闭平台，并且这些举动注定将使[[Steam|Steam]]等第三方商店处于劣势，微软在削减了用户自由安装全功能PC软件的自由，破坏开发者及发行商与其客户之间保持直接关系的权利。因此，Sweeney称[[最终用户|最终用户]]应该可以直接下载UWP软件并以桌面软件相同的方式安装它。<ref name="ars-epicceo">{{Template:Cite web|url=http://arstechnica.com/gaming/2016/03/tim-sweeney-to-microsoft-universal-windows-platform-can-should-must-and-will-die/|title=Epic CEO: “Universal Windows Platform can, should, must, and will die”|accessdate=30 March 2016|publisher=Conde Nast|website=Ars Technica}}</ref>

在Build 2016期间，微软Xbox部门负责人Phil Spencer宣布公司正在尝试解决一些问题，以改进UWP对PC游戏的能力。其指出微软正在“致力于达到或超过全屏游戏的性能预期，以及提供包括覆盖层、模组等附加功能的支持。”，同时也宣布提供禁用[[垂直同步|垂直同步]]的支持，以及{{tsl|en|AMD_FreeSync|AMD FreeSync}}和{{tsl|en|Nvidia_G-Sync|Nvidia G-Sync}}技术的支持，这将在[[Windows_10|Windows 10]]的未来更新中添加。<ref name="gamespot-spencerbuild16">{{Template:Cite web|url=http://www.gamespot.com/articles/xbox-boss-on-pc-gaming-weve-heard-the-feedback-lou/1100-6436148/|title=Xbox Boss on PC Gaming: "We've Heard the Feedback Loud and Clear"|accessdate=30 March 2016|website=GameSpot}}</ref>

== 参考资料 ==
{{Reflist|30em}}

== 外部链接 ==
* [https://msdn.microsoft.com/en-us/library/windows/apps/dn894631.aspx Guide to UWindows Runtimeniversal Windows Platform (UWP) apps]


{{Microsoft_Windows_components}}

[[Category:.NET|Category:.NET]]
[[Category:Microsoft_Windows|Category:Microsoft Windows]]
[[Category:操作系统技术|Category:操作系统技术]]