{{expand|time=2014-05-24T16:54:25+00:00}}
{{Infobox software
| name               = 任务管理器
| logo               =
| type               = [[任务管理器|任务管理器]], [[系统监视器|系统监视器]] 和启动项管理器
| replaces           = [[系统监视器|系统监视器]]
| replaced_by        =
| operating system = [[Microsoft_Windows|Microsoft Windows]]
| developer        = [[微软|微软]]
}}
{{noteTA
|T=zh-hans:任务管理器 (Windows组件); zh-hant:工作管理員 (Windows元件);
|1=zh-hans:任务管理器; zh-hant:工作管理員;
|2=zh-hans:任务; zh-hant:工作;
|3=zh-hans:进程; zh-hant:處理程序;
|4=zh-hans:应用程序; zh-hant:應用程式;
|5=zh-hans:程序; zh-hant:程式;
|6=zh-hans:占用; zh-hant:佔用;
|7=zh-hans:应用历史记录;zh-hant:應用程式歷程記錄;
|G1=IT
}}
'''工作管理員'''（{{lang-en|'''Task Manager'''}}），是在[[微軟視窗|Windows]]系统中管理应用程式和處理程序的工具，通常由Windows自带，也有提供增强功能的第三方軟體。任务管理器可以让用户查看当前运行的處理程序。它提供有关电脑性能和运行软件的信息，包括运行进程的名称，CPU负载，内存使用，I/O情况，已登录的用户和 Windows 服务。任务管理器也可以用来设置进程优先级，处理器相关性，启动和停止服务，强制终止进程。此程序在最新的Windows上能通过按{{Key press|[[Windows_key|Win]]|R}}然后输入<code>taskmgr.exe</code>；按[[Control-Alt-Delete|{{Key press]]并选取“任务管理器”；按{{Key press|Ctrl|Shift|Esc}}；或右击[[任务栏#Microsoft_Windows|Windows任务栏]]并选取“任务管理器”。任务管理器在Windows NT 4.0以现在的形式被加入。以前的版本的 [[Windows_NT|Windows NT]] 和 [[Windows_3.x|Windows 3.x]] 则自带任务列表，它能够列出当前正在运行的进程，并终止它们，也可以创建一个新的进程。[[Windows_9x|Windows 9x]] 有一个被称为“ 关闭程序”的工具，该工具列出当前正在运行的程序，并提供关闭程序以及关闭电脑的选项。<ref name=9x>{{cite web
| url = http://nuance.custhelp.com/app/answers/detail/a_id/2048/~/how-to-end-task-on-the-items-that-are-running-in-the-background
| title = How to end task on the items that are running in the background
| date = June 22, 2002
| publisher = Nuance Communications
}}</ref>

== 功能 ==

=== 摘要视图 ===
在摘要模式下，任务管理器会显示当前正在运行的具有主窗口的程序列表。它有一个“详细信息”的按钮，按下就会激活完整的任务管理器。

右击列表中的任何应用程序都可以切换到该应用程序或结束应用程序的任务。按下结束任务会非强制地退出应用。

在Windows 10之前，在名为“应用程序”的选项卡中显示了摘要模式中显示的内容。

=== 进程和详细信息 ===
“进程”选项卡显示系统上所有正在运行的[[进程|进程]]的列表。此列表包含[[Windows_服务|Windows 服务]]和其他用户的进程。在Windows XP之前的版本会截断长度超过15个字符的进程名称。<ref>[http://yangcao88.spaces.live.com/blog/cns!45B36D487518CDF5!126.entry Magic 15 with GetProcessesByName on Windows 2000] {{dead link|date=June 2016|bot=medic}}{{cbignore|bot=medic}}</ref>从 Windows XP 开始，Delete键也可用于终止进程选项卡上的进程。默认情况下，“进程”选项卡会显示正在运行进程的用户帐户，CPU使用率以及进程正在使用的内存量。并且还有更多隐藏的列可以显示。从Windows 8开始，“进程”选项卡将进程分为三类：
* 应用：带有主窗口的程序
* Windows 进程：Windows 自身没有主窗口的组件，包括服务。
* 后台进程：不是Windows 自身的一部分，但又没有主窗口（包括服务）的程序。
此选项卡显示每个主窗口的名称以及与每个进程关联的服务。可以从此选项卡发送正常的退出命令和强制终止命令。

详细信息选项卡是进程选项卡的增强版，类似于 [[Windows_7|Windows 7]]及更早版本的进程选项卡。右击列表中的进程可以更改进程的优先级，设置处理器关联（设置进程可以使用的处理器），并且可以结束进程。选择结束任务会导致Windows 立即该终止进程。选择“结束进程树”会导致Windows 立即终止该进程的同时终止其直接或间接启动的所有进程。但是。如果需要结束与发出对TerminateProcess调用的进程在不同的安全上下文中运行的进程，则需要使用KILL命令行实用程序。<ref>{{cite web|url=http://support.microsoft.com/kb/155075 |title=Cannot End Service Processes with Task Manager |work=Support |publisher=[[Microsoft|Microsoft]] |date=2007-02-27 |accessdate=2012-12-06 |deadurl=no |archiveurl=https://web.archive.org/web/20070308102006/http://support.microsoft.com/kb/155075|archivedate=March 8, 2007}}</ref>

=== 性能 ===
“性能”选项卡显示有关系统性能的总体统计信息，例如总体CPU使用量和正在使用的内存量。显示了这两个值最近的图表。还显示了有关特定内存组合的详细信息。

有一个选项可以将CPU使用率图分成两个部分：内核模式时间和用户模式时间。许多设备驱动程序和操作系统的核心部分以内核模式运行，而用户应用程序以用户模式运行。从右击菜单中选择“ 显示内核时间”可以打开该选项。当此选项打开时，CPU使用率图将显示浅蓝和深蓝区域。深蓝区域是在内核模式下花费的时间量，浅蓝区域显示在用户模式下花费的时间量。

“性能”选项卡还显示与电脑中存在的每个网络适配器相关的统计信息，在Windows XP到Windows 7中，此信息位于单独的选项卡“ 网络”中。默认显示适配器名称，网络利用率的百分比，连接速度和网络适配器的状态，以及最近活动的图表。

=== 应用历史记录 ===
Windows 8中引入了“ 应用历史记录”选项卡，并显示了被称为“通用Windows平台”的应用程序的信息。Windows 会更紧密地控制这些应用程序的生命周期。此选项卡是Windows收集的关于它们的数据的查看处。

=== 启动 ===
“启动”选项卡也在Windows 8中被加入，并管理以Windows 外壳自启动的软件。（在以前需要使用[[MSConfig|MSConfig]]。）

=== 用户 ===
在Windows XP中被加入的“用户”选项卡显示了当前电脑上有会话的所有用户。例如服务器上使用远程桌面连接的多个用户。或是从Windows XP 开始并启用了快速用户切换的工作站上的多个用户。用户可以从此选项卡从此选项卡断开来连接或注销。

== 历史 ==

=== Windows 9x ===
在[[Windows_9x|Windows 9x]] 中，按下 [[Control-Alt-Delete|{{Key press]]时，会出现一个“关闭程序”对话框。<ref name="9x2" />另外， Windows 9x 中，Windows 目录中有一个名为“任务”（TASKMAN.EXE）的程序。TASKMAN.EXE是一个基本的程序并且功能很少。Windows 9x中的[[系统监视器|系统监视器]]实用程序包含类似于Windows任务管理器的进程和网络监视功能。（另外，如果Explorer进程关闭，则通过在桌面上双击来启动Tasks程序）。

=== Windows XP ===
在Windows XP 中，工作管理員提供了「关机」菜单，可以待机、休眠、关机、重新启动、注销、切换用户，但是如果不使用「歡迎畫面」，則工作管理員中不出現此功能表，且按下Ctrl+Alt+Delete後顯示的是「Windows 安全」對話方塊。

=== Windows Vista ===
在Windows Vista中，任务管理器加入了新功能，其中包括：

* “服务”选项卡可查看和修改当前运行的Windows服务，启动和停止任何服务以及启用/禁用进程的用户帐户控制（UAC）文件和注册表虚拟化。

* 在“进程”选项卡中加入了“映像路径名称”和“命令行”和“描述”列。它们显示在进程中运行的可执行文件的全名和路径，还可以显示的完整的命令行参数以及可执行文件的“描述”属性。

* 显示[[資料執行防止|資料執行防止]]状态和虚拟化状态的列。虚拟化状态是指UAC虚拟化，启用这个虚拟化会对某些系统位置的文件和注册表引用静默地重定向到用户特定的区域。

* 通过右键单击任何进程，可以直接打开进程[[執行檔|執行檔]]的属性或包含该进程的文件夹。

* 任务管理器也不太容易受到来自外部或病毒的攻击，因为它必须在管理员权限下运行才能执行某些任务，例如注销其他已登录的用户或发送消息。用户必须进入“进程”选项卡并单击“显示来自其他用户的进程”以验证管理员权限并解锁这些功能。除非UAC被禁用，否则显示来自所有用户的进程需要包括管理员在内的所有用户接受UAC提示。如果用户不是管理员，则当出现提示时，他们必须输入管理员帐户的密码，如果此时禁用了UAC，则无法进行操作。

* 通过右键单击任何正在运行的进程，可以创建内存转储。如果应用程序或进程没有响应，此功能可能会非常有用，因此可以在调试器中打开内存转储文件以获取更多信息。

* 包含待机、休眠、关机、重新启动、注销、切换用户的关机菜单已被移除。

* 性能选项卡显示系统正常运行时间。

=== Windows 8 ===
在Windows 8中，Windows 任务管理器已被彻底修改，并进行了以下更改：

* 默认使用摘要视图，该视图仅显示应用程序及其关联的进程。

* “进程”选项卡中的资源利用率显示为黄色阴影，较暗的颜色表示较高的使用率。

* “性能”选项卡分为CPU、内存、磁盘、以太网、无线网络（如果有的话）部分。选择其中一个选项来查看它的图表。

** CPU选项卡默认不再显示系统中每个逻辑处理器的单个图形。现在可以显示每个[[NUMA|NUMA]]节点的数据。

** “CPU”选项卡会在安装了64个到640个处理器上的电脑的图表中显示简单的百分率。<ref>{{cite web|url=http://blogs.msdn.com/b/b8/archive/2011/10/27/using-task-manager-with-64-logical-processors.aspx|title=Using Task Manager with 64+ logical processors|date=October 27, 2011|last=Sinofsky|first=Steven|work=Building Windows 8|publisher=[[Microsoft|Microsoft]]}}</ref>这些图表是蓝色的，而较暗的颜色表示较高的使用率。

** 现在将鼠标悬停在任何逻辑处理器的数据上会显示该处理器的[[非均匀访存模型|非均匀访存模型]]节点及其ID。

* 加入了一个新的启动选项卡，列出所有的自启动应用程序。<ref>{{cite web|url=http://www.itproportal.com/2011/10/24/how-get-most-out-new-windows-8-task-manager/|title=How to Get the Most out of New Windows 8 Task Manager?|date=October 24, 2011|last=Serban|first=Alex|work=ITProPortal|publisher=Future Publishing}}</ref>

* “进程”选项卡现在列出每个进程的名称、CPU、内存、硬盘、网络资源，应用的状态和总体使用情况的数据。

** 应用状态可以显示为暂停状态。

** 在以前版本的任务管理器中的“进程”选项卡更名为“详细信息”。

== 弱点 ==
任务管理器是[[计算机病毒|计算机病毒]]和其他形式的[[恶意软件|恶意软件]]的共同敌人; 通常恶意软件会在启动时立即关闭任务管理器，从而将自己隐藏起来。例如，[[狙击波蠕虫|狙击波蠕虫]]和[[Spybot|Spybot]]蠕虫的变种就使用了这种技术。<ref>{{cite web|url=http://windowsxp.mvps.org/ToolsQuit.htm|title=Task Manager, MSCONFIG, or REGEDIT disappears while opening|date=December 19, 2005|work=Ramesh's website}}</ref>使用组策略可以禁用任务管理器。许多类型的恶意软件也可以通过注册表来启用此策略。[[Rootkit|Rootkit]]可以在任务管理器中隐藏，从而防止它们被检测到并清除。

== 畫面说明 ==
[[File:Rwglq.png|thumb]]
通常，[[Windows_8|Windows 8]]、[[Windows_8.1|Windows 8.1]]、[[Windows_10|Windows 10]]用户可以在啟動工作管理員後看到如上圖的介面，按下“結束工作”可以进行結束該項工作，按下右鍵可以對單一應用程式進行切換應用程式和新工作等操作。

==参见==
* [[任务管理器|任务管理器]]

==注释==
<references />

{{Windows Components}}

[[Category:操作系统|Category:操作系统]]