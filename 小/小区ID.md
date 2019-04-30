GSM '''小区ID'''（Cell ID，也称CID）是一个全局唯一的号码，用于区分各个[[基站子系统|基地收发机站]]（Base Transceiver Station，简称BTS）或者，如果不是在[[GSM|GSM]]网络内的话，则区分一个[[移动性管理#位置区|位置区码]]（Location Area Code，简称LAC）中的BTS的一个扇面（Sector）。

在某些情况下，CID的第一位或最后一位数字代表该小区的扇面（Sector）ID：

* 数值“0”表示全向天线，
* 数值“1”，“2”，“3”用于区分双扇面（bisector）或三扇面（trisector）天线的不同扇面。

在[[UMTS|UMTS]]中，小区ID（CID）和[[UTRAN|UTRAN]]小区ID（也被称为LCID）是有区别的。UTRAN小区ID（LCID）是把RNC-ID（一个12比特的数，[[无线网络控制器|无线网络控制器]]的ID）和小区ID（一个12比特数，小区的唯一标识）串联起来。 CID仍是原来的小区ID。二者串联后仍然是唯一的，但在一些小区ID数据库中可能会造成混淆，因为一些数据库存储CID，而另一些可能存储LCID。实际上有必要将二者分别单独存储，因为对于很多小区来说，RNC ID是相同的，CID才是唯一的。<ref>https://stackoverflow.com/questions/7240038/utran-cell-identity-returned-by-getcid</ref><ref>{{Cite web|title=3GPP TS|url=http://www.etsi.org/deliver/etsi_ts/125400_125499/125401/04.02.00_60/ts_125401v040200p.pdf#page=15|publisher=www.etsi.org|accessdate=2015年06月26日}}</ref>

在GSM和CDMA网络中，一个有效的CID范围是0～65535(2<sup>16</sup> −1)，而在UMTS和[[LTE|LTE]]网络中，有效范围则是0～268,435,455(2<sup>28</sup> −1)。<ref>{{Cite web|title=Cell Networks（蜂窝网络）|url=https://mozilla.github.io/ichnaea/internal_api/models/cell.html#cell-networks|accessdate=2015年09月21日|archive-url=https://web.archive.org/web/20160304211934/https://mozilla.github.io/ichnaea/internal_api/models/cell.html#cell-networks|archive-date=2016年3月4日|dead-url=yes}}</ref>

== 小区ID数据库和服务 ==
有许多可用的商业的和公共的小区ID数据库和服务：
{| class="wikitable sortable" border="1"
!名称
!小区个数
! align="right" |国家个数([[行動裝置國家代碼|MCC]])
!运营商个数([[行動裝置國家代碼|MNC]])
!Measurements
!免费数据库下载
!活跃项目
!数据许可证
! class="unsortable" |说明
|-
|Cellspotting.com
| align="right" |10万<ref>{{Cite web|url=http://cellspotting.com/thick/statistics.php|title=小区定点（CellSpotting）的统计数据|accessdate=2016年03月29日|format=|work=}}</ref>
| align="center" |
| align="center" |667
| align="right" |
| align="center" |
| align="center" |是
| {{Free|[[CC0|CC0]]}}
|
|-
|Combain移动 – [http://combain.com/ combain.com]
| align="right" |>1亿<ref>{{Cite web|url=http://www.combain.com/|title=康拜恩移动（Combain Mobile）|accessdate=2018年09月05日|format=|work=}}</ref>
| align="center" |>240
| align="center" |>1700
| align="right" |>660亿
| align="center" |否
| align="center" |是
|
|通过API支持 GSM、CDMA、UMTS、LTE 和 Wi-Fi (>1.6B Wi-Fis) 。<ref>{{Cite web|url=https://combain.com/coverage/|title=康拜恩移动（Combain Mobile）覆盖地图|accessdate=2018年02月20日|format=|work=}}</ref> <!-- 檔案不存在 [[File:Combain_CellID_Coverage.png|缩略图]] ，可從英文維基百科取得 -->
|-
|[https://www.locationapi.org/ LocationAPI.org]– 无线实验室（Unwired Labs）
| align="right" |1亿5789万<ref>{{Cite web|url=https://unwiredlabs.com/|title=无线实验室（Unwired Labs）的“位置应用程序接口”（LocationAPI）|accessdate=2016年03月29日|format=|work=}}</ref>
| align="center" |240
| align="center" |1712
| align="right" |250亿
| align="center" |否
| align="center" |是
|
|通过它提供的API支持WiFi、GSM、CDMA、UMTS以及LTE技术。[[File:Coverage_Map_-_Unwired_Labs_LocationAPI.png|缩略图]] <ref>{{Cite web|url=http://unwiredlabs.com/coverage|title=无线实验室（Unwired Labs）的覆盖地图|accessdate=2016年03月29日|format=|work=}}</ref>
|
|-
|[[谋智（Mozilla）位置服务|谋智（Mozilla）位置服务]]
| align="right" |2820万<ref name="mls-stats">{{Cite web|url=https://location.services.mozilla.com/stats|title=统计数据：谋智（Mozilla）位置服务|accessdate=2016年03月29日|format=|work=}}</ref>
| align="center" |240<ref>{{Cite web|url=https://location.services.mozilla.com/stats/regions|title=各国小区统计 - 谋智（Mozilla）位置服务|accessdate=2016年03月29日|format=|work=}}</ref>
| align="center" |
| align="right" |270亿<ref name="mls-stats" />
| align="center" |是<ref name="mls-downloads">{{Cite web|url=https://location.services.mozilla.com/downloads|title=小区下载 - 谋智（Mozilla）位置服务|accessdate=2015年01月30日|format=|work=}}</ref>
| align="center" |是<ref name="mls-stats" />
|
|基于众包数据。同时还有WiFi数据库。与OpenCelliD<ref name="mls-downloads" />和康拜恩（Combain）合作。<ref>{{Cite web|url=https://blog.mozilla.org/services/2015/03/06/combain-deal-helps-expand-mozilla-location-service/|title=康拜恩方案（Combain Deal）帮助扩展谋智（Mozilla）位置服务|accessdate=2015年04月09日|format=|work=}}</ref>
|-
|Mylnikov GEO<ref>{{Cite web|url=https://www.mylnikov.org/archives/1059|title=米尔尼科夫（Mylnikov）地理小区统计|accessdate=2016年03月29日|format=|work=}}</ref>
| align="right" |>3400万
| align="center" |505
| align="center" |3500
| align="right" |
| align="center" |是
| align="center" |是
|
|包含来自radiocells.org、OpenCellID以及MLS的数据。
|-
|Navizon<ref>{{Cite web|url=http://www.navizon.com/wifi-cell-tower-location-database|title=纳威森（Navizon）全球定位系统|accessdate=2016年03月29日|format=|work=}}</ref>
| align="right" |7100万
| align="center" |239
| align="center" |1712
| align="right" |220亿
| align="center" |否
| align="center" |是
|
|基于众包数据，也包括WiFi数据库。<ref>{{Cite web|url=http://www.navizon.com/navizon_coverage_cell.htm|title=纳威森（Navizon）蜂窝覆盖地图|accessdate=2016年03月29日|work=}}</ref>
|-
|NetMeterProject.com
| align="right" |20万
| align="center" |77
| align="center" |174
| align="right" |1000万
| align="center" |受限；仅供私有使用
| align="center" |no <ref>{{Cite web|url=http://board.netmeterproject.com/viewtopic.php?f=17&t=665|title=Board NetMeterProject|accessdate=2016年03月29日|format=|work=}}{{Dead link|date=August 2017|bot=InternetArchiveBot|fix-attempted=yes}}</ref>
|
|只有数据库中的一小部分数据可以被下载，并且仅供私有使用：那些众包用户接受“Creative Commons Namensnennung-Nicht-kommerziell-Weitergabe unter gleichen Bedingungen 3.0 Deutschland”协议的测量数据。
|-
|OpenCellID 由无线实验室（Unwired Labs）提供<ref>{{Cite web|url=http://opencellid.org/#action=statistics.cells&type=5&dateFrom=&dateTo=&mcc=&mnc=&sortBy=1|title=opencellid.org实时统计数据|accessdate=2015年08月30日|format=|work=}}</ref>
| align="right" |3890万
| align="center" |222
| align="center" |753
| align="right" |21亿
| align="center" |是
| align="center" |是
|{{Free|CC-BY-SA 3.0}}
|<!-- 檔案不存在 [[File:OpenCellID_database_growth.png|缩略图]] ，可從英文維基百科取得 -->基于众包数据；要下载数据库的话，需要免费API秘钥；该服务目前由无线实验室（Unwired Lab）维护。<ref>{{Cite web|url=http://wiki.opencellid.org/wiki/Main_Page|title=OpenCellID的百科网站主页|accessdate=2017年03月02日|format=|work=}}</ref><ref>{{Cite web|url=http://www.digitaljournal.com/pr/3421411|title=无线实验室（Unwired Labs）和ENAiKOON 发布关于对OpenCellID的维护工作的移交 - 媒体新闻稿 - 数字期刊（Digital Journal）|work=www.digitaljournal.com|accessdate=2017年08月03日}}</ref>
|-
|OpenSignal<ref>{{Cite web|url=http://opensignal.com/coverage-maps/|title=开放信号地图（OpenSignalMap）的统计数据|accessdate=2014年09月06日|format=|work=|archiveurl=https://archive.is/20150502112843/http://opensignal.com/coverage-maps/#|archivedate=2015-05-02}}</ref>
| align="right" |80万
| align="center" |
| align="center" |825
| align="right" |52亿
| align="center" |否
| align="center" |是
|
|-
|radiocells.org<ref>{{Cite web|url=http://www.radiocells.org/|title=radiocells.org|accessdate=2016年03月29日|format=|work=}}</ref>
| align="right" |70万
| align="center" |94
| align="center" |243
| align="right" |
| align="center" |是
| align="center" |是
|{{Free|[[CC-BY-SA_3.0|CC-BY-SA 3.0]]}}
|基于众包数据
|-
|WiGLE<ref>{{Cite web|url=https://wigle.net/stats|title=WiGLE的统计数据|accessdate=2016年03月29日|format=|work=}}</ref>
| align="right" |620万
| align="center" |
| align="center" |
| align="right" |
| align="center" |否
| align="center" |是
|
|-
|[http://cellmapper.net/ 小区映射器]
|
|
|
|
| align="center" |否
| align="center" |是
|
|-
|[http://openmobilenetwork.org/ 开放式移动网络]
|
|
|
|
|
|
|
|-
|[http://www.gyokovsolutions.com/G-NetWorld/G-NetWorld.php G-NetWold] 由 Gyokov解决方案提供
|
|
|
|
|
|
|
|-
|[http://www.skyhookwireless.com/ 天钩无线]
|
|
|
|
|
|
|
|-
|谷歌位置服务<ref>{{Cite web|url=https://www.google.com/privacy/lsf.html|title=在谋智（Mozilla）隐私策略中的谷歌位置服务|author=|first=|date=|work=|publisher=Google Inc.|accessdate=2016年09月30日}}</ref>
|
|
|
|
|
|
|
|-
|苹果位置服务<ref>{{Cite web|url=https://support.apple.com/en-ca/HT207056|title=关于位置服务和隐私|author=|first=|date=|work=|publisher=Apple Inc.|accessdate=2016年09月30日}}</ref>
|
|
|
|
|
|
|
|-
|微软位置服务<ref>{{Cite web|url=https://msdn.microsoft.com/library/windows/apps/br225603|title=Windows运行时应用程序接口（Runtime APIs） - Windows.Devices.Geolocation 名字空间|author=|first=|date=|work=|publisher=Microsoft Corp.|accessdate=2016-09-30}}</ref>
|
|
|
|
|
|
|
|}

== 参见 ==

* [[基地收发机站|基地收发机站]]
* 现场测试模式
* [[E-CellID|E-CellID]]

== 参考文献 ==
<references group="" responsive=""></references>

== 外部链接 ==

* [https://combain.com/ Combain定位服务]：以API方式提供的云服务，用于定位无线设备。基于小区ID和WiFi。
* [https://unwiredlabs.com/ 来自无线实验室（Unwired Lab）的LocationAPI]：位置即API服务，通过WiFi、蜂窝信号塔和IP地址来定位设备。
* [https://location.services.mozilla.com/ 谋智位置服务] ：一个开放式服务，它可以让设备通过网络基础设施（例如WiFi接入点和蜂窝信号塔）来确定它们的位置
* [https://www.cellmapper.net/map CellMapper]：蜂窝网络的覆盖范围和信号塔地图
* [https://opencellid.org OpenCellID]：一个开源项目，目的是创建一个全世界的小区ID以及它们所对应的位置的完整数据库。
* [https://cellidfinder.com/ cellidfinder]：找到任何已知的小区ID的坐标。
* [https://www.navizon.com/ Navizon]：以API方式提供的云服务，使用WiFi接入点和小区ID位置的一个全球性的数据库，来定位无线设备。
* [https://web.archive.org/web/20180601142241/http://www.openbmap.org/ openBmap]：一个免费和开放的无线通信设施（例如蜂窝天线、WiFi接入点等）。
* [http://minigps.net/map.html minigps]：中国境内的小区ID的一些信息
* [https://www.mylnikov.org/archives/1059 Mylnikov GEO]：一个开源API项目。 它让我们得到移动信号塔的坐标，没有任何限制，并且完全免费的。 ([[俄语|俄罗斯]])
* [http://people.csail.mit.edu/bkph/cellular_repeater_numerology.shtml 基站编号方案]：关于蜂窝中继器的编号的讨论
[[Category:GSM標準|Category:GSM標準]]
[[Category:有未审阅翻译的页面|Category:有未审阅翻译的页面]]