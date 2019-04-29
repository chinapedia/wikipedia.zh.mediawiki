{{NoteTA
|G1=Electronics
}}
'''IP核'''，全称'''知识产权核'''（{{lang-en|'''intellectual property core'''}}），是在[[集成电路|集成电路]]的[[集成电路设计#可重用设计方法学|可重用设计方法学]]中，指某一方提供的、形式为逻辑单元、芯片设计的[[集成电路设计#可重用设计方法学|可重用]]模組。IP核通常已经通过了设计验证，设计人员以IP核为基础进行设计，可以缩短设计所需的周期。<ref>{{Cite book|author=虞希清|title=专用集成电路设计实用教程|publisher=浙江大学出版社|isbn=978-7-308-05113-2|page=3}}</ref>IP核可以通过协议由一方提供给另一方，或由一方独自占有。IP核的概念源于产品设计的[[专利|专利]]证书和源代码的[[版权|版权]]等。设计人员能够以IP核为基础进行[[特殊應用積體電路|特殊應用積體電路]]或[[现场可编程逻辑门阵列|现场可编程逻辑门阵列]]的逻辑设计，以减少设计周期。

IP核分为软核、硬核和固核。软核通常是与工艺无关、具有[[寄存器传输级|寄存器传输级]][[硬件描述语言|硬件描述语言]]描述的设计代码，可以进行后续设计；硬核是前者通过[[逻辑综合|逻辑综合]]、[[布局_(集成电路)|布局]]、[[布线_(集成电路)|布线]]之后的一系列表征文件，具有特定的工艺形式、物理实现方式；固核则通常介于上面两者之间，它已经通过[[功能验证|功能验证]]、[[静态时序分析|时序分析]]等过程，设计人员可以以[[逻辑门|逻辑门]]级[[网表|网表]]的形式获取。<ref>{{Cite book|author=杨宗凯，黄建，杜旭|title=数字专用集成电路的设计与验证|publisher=电子工业出版社|isbn=7-121-00378-3|page=37}}</ref>

== 相关条目 ==
* [[集成电路设计|集成电路设计]]
* [[系统芯片|系统芯片]]（SoC）
* [[电子设计自动化|电子设计自动化]]

== 参考文献 ==
{{Reflist}}
{{Refbegin}}
* {{cite book|author=徐志军等|title=EDA技术与PLD设计|publisher=人民邮电出版社|isbn=7-115-13796-X}}
{{Refend}}

== 外部链接 ==
* [http://www.opencores.org Open cores] "design and publish core" (under LGPL Licence)
* [https://web.archive.org/web/20120828201040/http://www.altera.com/products/ip/ref-index.jsp Altera cores] Free reference IP cores for FPGAs
* [http://jolt.law.harvard.edu/articles/pdf/v25/25HarvJLTech131.pdf Open Source Semiconductor Core Licensing, 25 Harvard Journal of Law & Technology 131 (2011)]  Article analyzing the law, technology and business of open source semiconductor cores

[[Category:电子设计自动化|I]]
[[Category:半导体IP核|Category:半导体IP核]]
[[Category:逻辑设计|Category:逻辑设计]]
[[Category:半导体元件制程|Category:半导体元件制程]]