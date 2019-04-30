{{noteTA
|G1=IT
|1=zh-tw:微軟行動;zh-hk:微軟流動;zh-cn:微软移动;
}}
{{Infobox OS
| name                   = 诺基亚X软件平台
| logo                   = [[File:NokiaXlogo.svg|240px]]
| screenshot             = 
| caption                =
| developer              = AOSP源代码：[[Google|Google]]<br>修改者：[[微软移动|微软移动]]（原[[诺基亚|诺基亚]]）
| family                 = [[Linux|Linux]]
| working state          = 停止开发
| source model           = 基于[[开源软件|开源]]Android的[[专有软件|专有软件]]以及所有具有专有组件的设备<ref name="philosophy">{{cite web |url=http://source.android.com/about/philosophy.html |title=Philosophy and Goals |work=Android Open Source Project |publisher=Google |accessdate=2012-04-21}}</ref>
| released               = 2014
| latest release version = 诺基亚X软件平台2.1
| latest release date    = 
| frequently updated     = 
| marketing target       = [[智能手机|智能手机]]
| programmed in          = [[C语言|C语言]], [[C++|C++]], {{nowrap|[[Java|Java]]<ref>{{cite web |title=Android Code Analysis|url=http://www.ohloh.net/p/android/analyses/latest |accessdate=6 June 2012}}</ref>}}
| language               = [[简体中文|简体中文]]、[[繁体中文|繁体中文]]、[[英文|英文]]、[[法文|法文]]、[[西班牙文|西班牙文]]、[[葡萄牙文|葡萄牙文]]等
| package manager        = [[APK|APK]]
| supported platforms    = 32位ARM
| kernel type            = Monolithic（修改的Linux内核）
| userland               = [[Bionic_(軟體)|Bionic libc]],<ref>[https://android.googlesource.com/platform/bionic/+/master/libc/ android/platform/bionic/]</ref> [[Korn_shell|mksh]] shell,<ref>[https://android.googlesource.com/platform/external/mksh/+/master android/platform/external/mksh/]</ref>本地核心实用程序（部分来自[[NetBSD|NetBSD]]）<ref>[https://android.googlesource.com/platform/system/core/+/master/toolbox/ android/platform/system/core/toolbox/]</ref>
| ui                     = 图形用户界面（多点触控）
| license                = 专有EULA，基于[[Apache_License|Apache License]] 2.0<br />在[[GNU|GNU]] [[GPL_v2|GPL v2]]下修改的[[Linux|Linux]]内核<ref name="Licenses">{{cite web|url=http://source.android.com/source/licenses.html|title=Licenses|work=Android Open Source Project.|publisher=Open Handset Alliance|accessdate=9 September 2012|date=|quote=''The preferred license for the Android Open Source Project is the Apache Software License, 2.0. ... Why Apache Software License? ... For userspace (that is, non-kernel) software, we do in fact prefer ASL2.0 (and similar licenses like BSD, MIT, etc.) over other licenses such as LGPL. Android is about freedom and choice. The purpose of Android is promote openness in the mobile world, but we don't believe it's possible to predict or dictate all the uses to which people will want to put our software. So, while we encourage everyone to make devices that are open and modifiable, we don't believe it is our place to force them to do so. Using LGPL libraries would often force them to do so.''}}</ref>
| website = {{URL|https://developer.nokia.com/nokia-x/platform-overview}}
}}

'''诺基亚X软件平台'''是一个基于[[Linux|Linux]]的[[移动操作系统|移动操作系统]]和[[系统平台|软件平台]]，最初由[[诺基亚|诺基亚]]开发，随后由[[微软移动|微软移动]]开发。 它于2014年2月24日推出，是[[Android|Android]]的一个[[复刻_(软件工程)|分支]]，并用于[[诺基亚X系列|诺基亚X系列]]的所有设备。

2014年7月17日，在收购诺基亚设备部门后，微软宣布将不再推出诺基亚X系列智能手机<ref>{{cite news|url=https://www.theverge.com/2014/7/17/5911909/microsoft-kills-off-its-nokia-android-phones |title=Microsoft kills off its Nokia Android phones |publisher=The Verge |date=2014-04-08}}</ref>，标志着诺基亚X软件平台发布几个月后就停止开发。 这些手机已经被微软移动旗下的低端[[Lumia|Lumia]]设备所取代。<ref>[http://www.microsoft.com/en-in/mobile/phone/lumia435-dual-sim/]</ref>

==概览==
诺基亚X软件平台基于Android开源项目（AOSP）<ref>[https://developer.nokia.com/nokia-x/platform-overview Nokia X Platform Overview | Nokia Developer] {{Wayback|url=https://developer.nokia.com/nokia-x/platform-overview |date=20140625225721 }}</ref>和[[Linux|Linux]]内核。<ref>{{cite news|url=http://www.zdnet.com/why-microsoft-may-keep-not-kill-nokias-new-android-phones-7000026690/ |title=Why Microsoft may keep, not kill, Nokia's new Android phones |first=Mary Jo |last=Foley |publisher=zdnet |date=2014-02-24 |accessdate=2014-03-05}}</ref> 诺基亚将Android应用与诺基亚体验（如[[Here地图|Here地图]]，诺基亚Xpress和MixRadio）以及微软服务（如Skype和Outlook）结合在一起。 诺基亚官方称该软件将带来“世界上最好的东西”。 它还包含Asha平台的功能，例如Fastlane通知中心。其用户界面与[[Windows_Phone|Windows Phone]]系统的类似。

该系统经常与[[亚马逊公司|亚马逊公司]]推出的[[Fire_OS|Fire OS]]进行对比，后者同样基于AOSP。

==应用程序==
[[Google|Google]]的应用程序被诺基亚和微软的同类应用程序取代。首次发布时[[Google_Play|Google Play]]并未预装，应用程序通过[[诺基亚商店|诺基亚商店]]提供。不过在2014年9月的2.1版本更新当中，用户可以通过第三方工具安装Google Play及其他各种Google服务，但如果用户尝试在诺基亚X系列设备上安装Google服务，则设备通常会“变砖”，并可能需要[[诺基亚软件恢复工具|诺基亚软件恢复工具]]来恢复数据。<ref name=NokiaPowerUserNokiaX2v2point1>{{cite news|last=Chowdhury|first=Kamal|title=Update: "Nokia X2 Tools" allows Nokia X2 to install Google Play Store & Google services.|url=http://www.nokiapoweruser.com/nokia-x2-tools-allows-nokiax2-to-install-google-play-store-google-services/|newspaper=Nokia PowerUser|date=15 August 2014}}</ref>

截至2014年2月，75%的Android应用程序与该平台兼容。

==开发者==
该平台可以使用一个SDK，其中包含一个基于Android模拟器的模拟器。 诺基亚不鼓励开发者使用Windows Phone设计模式，并鼓励在诺基亚X上使用Android设计指引。<ref>[http://developer.nokia.com/resources/library/nokia-x-ui/ux-checklist.html UX checklist - Nokia X Design Guidelines] {{Wayback|url=http://developer.nokia.com/resources/library/nokia-x-ui/ux-checklist.html |date=20140704225605 }}</ref>诺基亚开发者关系副总裁评论说，诺基亚影像SDK可能会从Windows Phone移植到该平台。<ref>http://www.theinquirer.net/inquirer/news/2331280/nokia-imaging-sdk-set-for-android-nokia-x-platform</ref>

==版本历史==
{| class="wikitable" style="float:center; text-align:center; margin-left:1em; margin-right:0"
|-
! 版本
! 发布时间
! 基于AOSP版本
! 注释
|-
| 1.0
| 2014-02-24
| API Level 16 (4.1.2 Jelly Bean)
| 
*初始版本
|-
| 1.1.1
| 2014-03-25
| API Level 16 (4.1.2 Jelly Bean)
| 
*改善性能
*可更改第三方应用磁贴的颜色<ref>[http://www.phonesreview.co.uk/2014/03/25/nokia-x-update-brings-improvements-already/]</ref>
|-
| 1.1.2.2
| 2014-05-10
| API Level 16 (4.1.2 Jelly Bean)
| 
*添加两个新应用：[[OneDrive|OneDrive]]和联系人转移
*各类性能修复<ref>[http://www.gsmarena.com/nokia_x_1122_software_update_now_rolling_out-news-8492.php]</ref>
|-
| 1.2.4.1/1.2.4.21
| 2014-07-28
| API Level 16 (4.1.2 Jelly Bean)
| 
*新的应用程序切换界面
*添加“通过短信拒接电话”的功能
*可在拨号盘内搜索联系人
*添加两个应用程序：[[Outlook.com|Outlook.com]]和[[Microsoft_OneNote|OneNote]]<ref>{{cite web|title=Announcement of software update v. 1.2.4.1/1.2.4.21|url=http://discussions.nokia.com/t5/Nokia-X/New-software-update-for-Nokia-X-Dual-SIM-RM-980-v-1-2-4-1-1-2-4/td-p/2850168|deadurl=yes|archiveurl=https://web.archive.org/web/20140803073858/http://discussions.nokia.com/t5/Nokia-X/New-software-update-for-Nokia-X-Dual-SIM-RM-980-v-1-2-4-1-1-2-4/td-p/2850168|archivedate=2014年8月3日|df=}}</ref>
|-
| 2.0
| 2014-06-24
| API Level 18 (4.3 Jelly Bean)
| 
*可添加第四列磁贴
*应用列表
*对磁贴大小调节及移动方面的改进
*新的相机用户界面
*新的虚拟键盘
*支持实体主页键
|-
| 2.1
| 2014-09-03
| API Level 18 (4.3 Jelly Bean)<!--Right for 2.1.0.12, assuming it means 2.1 not 2.0-->
| 
*智能拍摄模式
*动态壁纸和锁屏界面小部件
*Google服务
*本地日历支持
*电子邮件账号自动配置
*在邮件及短信应用中支持横屏模式
*其他小改进
|}

==参见==
* [[诺基亚Asha平台|诺基亚Asha平台]]
* [[诺基亚商店|诺基亚商店]]

==参考资料==
{{Reflist|30em}}
== 外部連結 ==
* {{en}}[https://www.nokia.com/en_int/phones 諾基亞全球]
* {{zh-cn}}[https://www.nokia.com/zh_int/phones 諾基亞中國大陸]
* {{zh-tw}}[https://www.nokia.com/zh_tw/phones 諾基亞台灣]
* {{zh-hk}}[https://www.nokia.com/zh_hk/phones 諾基亞香港]

{{Nokia}}
{{Mobile operating systems}}

[[Category:諾基亞|Category:諾基亞]]
[[Category:微軟移動|Category:微軟移動]]
[[Category:Linux|Category:Linux]]
[[Category:作業系統|Category:作業系統]]