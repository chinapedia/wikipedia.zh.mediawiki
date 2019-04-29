{{Refimprove|time=2017-09-30T07:21:39+00:00}}
{{Infobox Computer Hardware Cpu
| name = Pentium III
| image = Pentium 3 logo.jpg
| caption = Pentium III logo
| produced-start = 1999年
| produced-end = 2003年
| slowest = 450  | slow-unit = MHz
| fastest = 1.4  | fast-unit = GHz
| fsb-slowest = 100  | fsb-slow-unit = MHz
| fsb-fastest = 133  | fsb-fast-unit = MHz
| manuf1 = 英特爾
| core1 = Katmai
| core2 = Coppermine
| core3 = Coppermine-T
| core4 = Tualatin
| size-from = 0.25µm
| size-to = 0.13µm
| arch = x86 (686)
| microarch = [[Intel_P6|P6]]
| sock1 = Slot 1
| sock2 = Socket 370
}}

'''Pentium III'''是[[英特爾|英特爾]]的[[x86|x86]]（更準確地說是P6）架構之[[微處理器|微處理器]]，於1999年2月底推出。剛推出的版本與早期的[[Pentium_II|Pentium II]]非常相似，最值得注意的不同是[[SSE|SSE]]指令的擴充，以及在每個晶片製造的過程加入有爭議的序號進去。與Pentium II相同，也有低階的[[Celeron|Celeron]]版本和高階的[[Xeon|Xeon]]版本。Pentium III最後被[[Pentium_4|Pentium 4]]所取代，Pentium III的改進設計就是後來的[[Pentium_M|Pentium M]]。

== Pentium III核心 ==
{| class="wikitable" align="center"
!colspan="5"|Intel  Pentium III處理器家族
|-
!rowspan="2"|標準型標誌
!rowspan="2"|移動型標誌
!colspan="3"|[[桌上型電腦|桌上型電腦]]
|-
!代號
!核心
!推出日期
|- style="background:white"
|align="center"|[[File:Intel__Pentium_III_Processor_Logo.svg|90px]]
|align="center"|[[File:Intel__Pentium_III-M__Processor_Logo.svg|100px]]
|Katmai<br>Coppermine<br>Coppermine-T<br>Tualatin 
|（250 nm）<br>（180 nm）<br>（180 nm）<br>（130 nm）
|1999年5月<br>2000年3月<br>2000年8月<br>2001年4月
|-
!colspan="5"|<small>[[Intel_Pentium_III處理器列表|Intel Pentium III處理器列表]]</small>
|}
=== Katmai ===
原先的版本Katmai與Pentium II非常相似（均使用0.25µm製程），唯一的差別是加入SSE，以及改進第一級快取控制器（導致其比Pentium II擁有較好的效能）。首次推出的速度是450和500MHz。另外兩個版本是：550 MHz於1999年5月17日推出；600MHz於1999年8月2日推出。在1999年9月27日，[[Intel|Intel]]推出533B和600B的版本，分別是533/600MHz，但是使用的是133MHz前端匯流排，而先前的是使用100MHz。Katmai使用與[[Pentium_II|Pentium II]]相同的插座介面。

=== Coppermine ===
第二個版本Coppermine整合CPU內的低延遲性全速256[[KB|KB]]第二級快取，比Katmai有效能上的進步。在AMD Athlon處理器的競爭壓力下，Intel重作晶片內部的設計，最後修正了廣知的指令管線拖延問題。這個結果是使處理指令的效能增加了卓越的30%。

它使用0.18µm製程製造。Pentium III Coppermine執行速度為500、533、550、600、650、667、700和733MHz，於1999年10月25日推出。從1999年12月到2000年5月，英特爾共推出了速度為750、800、850、866、900、933、1000MHz (1GHz)的Pentium III。

1.13GHz的版本於2000年中期推出，但是在普遍的硬體評論網站證明他在編譯Linux時候不夠穩定，因而回收<ref>[http://www.people.com.cn/GB/channel5/28/20000829/207120.html 1.13GHz奔腾III芯片有问题 Intel开始回收]</ref>。這個問題是由於整合到內部的快取無法在1GHz以上的速度運作。英特爾花費至少6個月來解決這個問題，於2001年推出1.1和1.13GHz的版本。

=== Coppermine-T ===
FC-PGA2封裝的Coppermine CPU針腳與Tualatin相同，因此無法與FC-PGA主機板相容。

=== Tualatin ===
[[File:Pentium_III-S_Tualatin.JPG|thumb]]
第三個版本Tualatin只是實際上英特爾的0.13μm製程試驗。{{fact|有人猜測不管Tualatin是否曾經被製造出來，[[Pentium_4|Pentium 4]]已經在一個更加酣然的立足地位。|time=2008-03-19}}Tualatin運行得相當好，512KB L2快取的Tualatin性能在大多数软件中都可以超过主频高得多的Willamette核心奔腾4，最终Intel把512KB的Tualatin改为Pentium III-S，不对大众用户销售，以避免影响奔腾4的销售。Pentium III-S主要是給那些功率消耗有關的機器，也就是[[刀鋒伺服器|刀鋒伺服器]]。

Pentium III Tualatin是在2001年至2002年早期之間所推出，速度分別為1.0、1.13、1.2、1.26、1.33和1.4 GHz。Intel不想重蹈先前低價的Celeron能與更貴的Pentium II相抗衡的覆轍，因此Tualatin從來沒有更快於1.4 GHz，也就是[[Pentium_4|Pentium 4]]剛推出的時脈頻率，已经设计好的512KB二级缓存Tualatin也改为专供服务器领域使用的“Pentium III-S”。後來，[[Pentium_M|Pentium M]]證明了這個設計很好，可以在0.13 μm到達1.7GHz。

Tualatin核心是以[[俄勒岡|俄勒岡]]地區的[[Tualatin谷|Tualatin谷]]和[[Tualatin河|Tualatin河]]來命名。

== 核心規格 ==
=== Katmai（0.25µm） ===
* 第一級快取：16 + 16 KB（資料 +指令）
* 第二級快取：512 KB，位於CPU模組之外，僅有50%相對於CPU的速度
* [[MMX|MMX]]，[[Streaming_SIMD_Extensions|SSE]]
* [[Slot_1|Slot 1]] 
* [[前端匯流排|前端匯流排]]：100, 133 MHz
* 核心電壓：2.0V,（600 MHz: 2.05V）
* 首次推出：1999年5月17日
* 時脈頻率：450-600 MHz
** 100 MHz FSB: 450, 500, 550, 600 MHz
** 133 MHz FSB: 533, 600 MHz（B型號）

=== Coppermine（0.18µm） ===
* 第一級快取：16 + 16 KB（資料 +指令）
* 第二級快取：256 KB, fullspeed
* [[MMX|MMX]]，[[Streaming_SIMD_Extensions|SSE]]
* [[Slot_1|Slot 1]]，[[Socket_370|Socket 370]]（FC-PGA）
* [[前端匯流排|前端匯流排]]：100, 133 MHz
* 核心電壓：1.65, 1.70, 1.75V
* 首次推出：1999年10月25日
* 時脈頻率：550 - 1133 MHz
** 100 MHz FSB: 550, 600, 650, 700, 750, 800, 850, 900, 1000, 1100 MHz（E型號）
** 133 MHz FSB: 533, 600, 667, 733, 800, 866, 933, 1000, 1133 MHz（EB型號）

=== Coppermine-T（0.18µm） ===
* 第一級快取：16 + 16 KB（資料 +指令）
* 第二級快取：256 KB，全速
* [[MMX|MMX]]，[[SSE|SSE]]
* [[Socket_370|Socket 370]]（FC-PGA2）
* [[前端匯流排|前端匯流排]]：133 MHz
* 核心電壓：1.75V
* 首次推出：[[2001年6月|2001年6月]]
* 時脈頻率：866, 933, 1000, 1133 MHz

=== Tualatin（0.13µm） ===
* 第一級快取：16 + 16 KB（資料 +指令）
* 第二級快取：256或512KB，全速
* [[MMX|MMX]]，[[SSE|SSE]]
* [[Socket_370|Socket 370]]（FC-PGA2）
* [[前端匯流排|前端匯流排]]：133 MHz
* 核心電壓：1.45, 1.475, 1.5V
* 首次推出：2001
* 時脈頻率：1000 -1400 Mhz
**Pentium III（256 KB第二級快取）: 1000, 1133, 1200, 1333 MHz
**Pentium III-S（512 KB第二級快取）: 1133, 1266, 1400 Mhz

==参考资料==
{{reflist}}
{{Intel_processors}}

[[Category:Intel_x86处理器|Category:Intel x86处理器]]