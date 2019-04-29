{{noteTA
|G1 =IT
}}
[[File:SASHardDriveComparsion.jpg|thumb]]Kiss[[薄荷糖|薄荷糖]]的大小比較。]] 
'''序列式SCSI'''（SAS：Serial Attached SCSI）是一種[[I/O总线|電腦集線]]的技術，其功能主要是作為週邊零件的數據傳輸，例如：[[硬碟|硬碟]]、[[CD-ROM|CD-ROM]]等設備而設計的界面。序列式SCSI 由[[並列SCSI|並列SCSI]]物理存儲介面演化而來，是由ANSI INCITS [[T10技術委員會|T10技術委員會]]（[http://www.t10.org T10 committee]）開發及維護的新的存儲介面標準。與並列方式相比，序列方式能提供更快速的通信傳輸速度以及更簡易的配置。此外SAS並支援與序列式ATA（[[SATA|SATA]]）設備相容，且兩者可以使用相類似的電纜。

SAS是點對點（point-to-point）連接，並允許多個端口集中於單個控制器上，其可以內建於主機板（mother board）當中；也可另外添加。該技術建立在強大的並列SCSI通信技術基礎上。SAS是採用SATA相容的電纜線採取點對點連接方式，從而在計算機系統中不需要建立雛菊鏈結（daisy-chaining）方式便可簡單地實現線纜安裝。

* 第一代SAS為陣列中的每個驅動器提供 3.0 Gbps（3000 Mbps）的傳輸速率。
* 第二代SAS為陣列中的每個驅動器提供 6.0 Gbps（6000 Mbps）的傳輸速率。
* 第三代SAS為陣列中的每個驅動器提供 12.0 Gbps（12000 Mbps）的傳輸速率。
* 第四代SAS為陣列中的每個驅動器提供 24.0 Gbps（24000 Mbps）的傳輸速率（開發中，預計2017年推出）。

== 介面 ==
SAS介面比普通SCSI介面小很多，並支援2.5英寸的硬碟。 SAS採取直接的點對點序列式傳輸方式，傳輸速率最高可達12Gbps，目前計劃於2017年左右達到24Gbps。

SAS的介面接頭有很多形式：

{| class="wikitable"
! 圖片
! 代號
! 別名
! 內接/外接
! 針腳數量
! 儲存設備數量
! 備註
|-
| [[File:SAS-drive-connector.jpg|200px]]
| SFF 8482
|
| 內接
| 
| 1
| 与SATA兼容的标准接口
|-
| [[File:SFF_8484_angled.jpg|200px]]
| SFF 8484
|
| 內接
|
| 4
| 高密度內接連接器
|-
|
| SSF 8485
|
|
|
|
| Routes data plus "sideband-signals" (Like LEDS) through serial link
|-
| [[File:SFF_8470.jpg|200px]]
| SFF 8470
| [[InfiniBand|InfiniBand]] connector
| 外接
| 32
| 4
| 高密度外接連接器（亦可內接使用）
|-
|[[File:SFF_8087.jpg|200px]]
| SFF 8087
| Internal Mini-SAS
| 內接
|
| 4
| [[Molex|Molex]] iPASS reduced width internal 4x connector with future 10 Gbit/s support
|-
| [[File:SFF_8088.jpg|200px]]
| SFF 8088
| External Mini-SAS
| 外接
| 32
| 4
| [[Molex|Molex]] iPASS reduced width external 4x connector with future 10 Gbit/s support
|}

SFF8482連接器可讓SATA的裝置（如SATA硬碟、光碟機）連接至SAS控制器，但SAS裝置並不能接到SATA控制器。為了防止誤接，SAS裝置的連接器有[[防呆|防呆]]設計。

== 技术细节 ==
SAS由3种类型协议组成，根据连接的不同设备使用相应的协议进行数据传输。
* 序列SCSI协议 (SSP) — 用于和SCSI設備溝通。
* 序列ATA通道协议 (STP) — 用于和SATA設備溝通。
* SCSI管理协议 (SMP) — 用于对SAS设备的维护和管理。

== 拓樸 ==

== 參看 ==
* [[List_of_device_bandwidths|List of device bandwidths]]

== 外部連結 ==
* [http://www.t10.org T10 committee]
* {{PDFlink|[http://www.t10.org/ftp/t10/drafts/sas2/sas2r10.pdf Download SAS 2 draft revision from T10]|6.47 [[Mebibyte|MiB]]<!-- application/pdf, 6787720 bytes -->}}
* [http://searchstorage.techtarget.com/tip/0,289483,sid5_gci1175003,00.html Implementing SAS storage]

{{Computer-bus}}

[[Category:SCSI|Category:SCSI]]
[[Category:Serial_ATA|Category:Serial ATA]]
[[Category:Serial_buses|Category:Serial buses]]