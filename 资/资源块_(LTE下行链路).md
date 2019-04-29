'''资源块（LTE下行链路）'''是LTE下行链路分配给用户的最小单位。LTE下行链路能够分配给用户的资源包括频域资源、时域资源和空域资源，即既有频分复用，又有时分复用，还有空分复用。空域资源分配是通过[[MIMO|MIMO]]实现的。资源块（resource block）是包含了12个子载波（频域）并且持续一个时隙slot（时域）的一个资源组合。一个时隙长0.5毫秒。<ref>Stefania Sesia, Issam Toufik and Matthew Baker, ''LTE – The UMTS Long Term Evolution: From Theory to Practice'', (John Wiley & Sons, Ltd.), 2009, ISBN 978-0-470-69716-0.</ref>

在0.5毫秒（一个时隙）时间内，LTE下行链路能够生成7个OFDM符号，每个符号占据12个子载波。不过资源块中OFDM符号的持续时间不完全相等，第一个OFDM符号的时间稍长（通过延长OFDM符号的循环前缀CP来实现）。资源块由资源片（resource element）组成，资源片是1个子载波（频域）并且持续一个时隙slot（时域）的资源组合。

两个时隙组成一个1毫秒的子帧（subframe），10个子帧(subframe)组成一个10毫秒的帧(frame)。帧（frame）是时域资源的最大单位。

假设某个用户的信息只占用一个资源块，LTE下行链路先将用户信息数据包串并转换成12路子数据流；每个子数据流用一个子载波进行调制，一共是12个子载波；调制过程重复7次，即产生7个OFDM符号。持续的时间是0.5毫秒；最后12路子载波承载的信息通过并串转换，在空口发送出去。

==參見==
* [[Comparison_of_wireless_data_standards|无线数据标准的对比]]
* [[eMBMS|eMBMS]] – LTE增强型广播多播服务。
* [[E-UTRA|E-UTRA]] – LTE无线连接网络。
* [[Flat_IP|Flat IP]] – 移动网络扁平IP架构。
* [[長期演進技術|長期演進技術]]
* [[長期演進技術升級版|LTE Advanced]] – LTE的昇級版。
* [[系統架構演進|系統架構演進]] – 是3GPP對於LTE無線通信標準的核心網路架構的升級計劃。
* [[TD-LTE|TD-LTE]] (LTE TDD) – 由[[中国|中国]]所开发的一种可选的LTE标准。
* [[超行動寬頻|超行動寬頻]] – LTE曾经的竞争对手，从未进行过商业化。
* [[WiMAX|WiMAX]] – 同屬4G的規格。
* [[HSPA+|HSPA+]] - 3GPP[[HSPA|HSPA]]标准的增强版本。
* [[Zadoff–Chu_公式|Zadoff–Chu 公式]]
* [[下一代網路|下一代網路（NGN）]]

==註釋==
{{Reflist|colwidth=30em}}

==延伸阅读==
* Erik Dahlman, Stefan Parkvall, Johan Sköld "4G – LTE/LTE-Advanced for Mobile Broadband", Academic Press, 2011, ISBN 978-0-12-385489-6
* Stefania Sesia, Issam Toufik, and Matthew Baker, "LTE – The UMTS Long Term Evolution – From Theory to Practice", Second Edition including Release 10 for LTE-Advanced, John Wiley & Sons, 2011, ISBN 978-0-470-66025-6
* Chris Johnson, "[http://www.lte-bullets.com LTE in BULLETS]", CreateSpace, 2010, ISBN 978-1-4528-3464-1
* Erik Dahlman, Stefan Parkvall, Johan Sköld, Per Beming, "3G Evolution – HSPA and LTE for Mobile Broadband", 2nd edition, Academic Press, 2008,ISBN 978-0-12-374538-5
* Borko Furht, Syed A. Ahson, "Long Term Evolution: 3GPP LTE Radio And Cellular Technology", Crc Press, 2009, ISBN 978-1-4200-7210-5
* F. Khan, "LTE for 4G Mobile Broadband – Air Interface Technologies and Performance", Cambridge University Press, 2009
* Mustafa Ergen, "Mobile Broadband – Including WiMAX and LTE", Springer, NY, 2009
* H. Ekström, A. Furuskär, J. Karlsson, M. Meyer, S. Parkvall, J. Torsner, and M. Wahlqvist, "Technical Solutions for the 3G Long-Term Evolution," ''IEEE Commun. Mag.'', vol. 44, no. 3, March 2006, pp. 38–45
* E. Dahlman, H. Ekström, A. Furuskär, Y. Jading, J. Karlsson, M. Lundevall, and S. Parkvall, "The 3G Long-Term Evolution – Radio Interface Concepts and Performance Evaluation," ''IEEE Vehicular Technology Conference (VTC) 2006 Spring'', Melbourne, Australia, May 2006
* K. Fazel and S. Kaiser, ''Multi-Carrier and Spread Spectrum Systems: From OFDM and MC-CDMA to LTE and WiMAX'', 2nd Edition, John Wiley & Sons, 2008, ISBN 978-0-470-99821-2
* Agilent Technologies, "[http://www.agilent.com/find/ltebook LTE and the Evolution to 4G Wireless: Design and Measurement Challenges]", John Wiley & Sons, 2009 ISBN 978-0-470-68261-6
* Sajal Kumar Das, John Wiley & Sons (April 2010): "Mobile Handset Design", ISBN 978-0-470-82467-2 .
* Beaver, Paul, "[http://www.eetimes.com/design/microwave-rf-design/4228238/What-is-TD-LTE-?Ecosystem=microwave-rf-design What is TD-LTE?]", RF&Microwave Designline, September 2011.
* Samuel C. Yang, "OFDMA System Analysis and Design", Artech House, 2010, ISBN 978-1-60807-076-3

==外部連結==
{{Sister project links|commons=Category:LTE|n=no|q=no|wikt=no|v=no|b=no|s=no}}
* [http://www.3gpp.org/article/lte LTE homepage] from the 3GPP website
* [http://sites.google.com/site/lteencyclopedia/home LTE A-Z Description] 3GPP LTE Encyclopedia

===白皮书及其他技术信息===
{{div col}}
* [https://web.archive.org/web/20120611084858/http://testrf.com/tag/lte-tutorial/ LTE Technology Overview and Tutorial Series including Webinars and Video presentations]
* [http://www.ericsson.com/ericsson/corpinfo/publications/review/2005_02/07.shtml "The Long Term Evolution of 3G" on Ericsson Review, no. 2, 2005]
* [http://www.rohde-schwarz.com/appnote/1MA111.pdf LTE technology introduction]{{dead link|date=十月 2017 |bot=InternetArchiveBot }}
* [http://www.signal.uu.se/Research/PCCWIP/Tunisia/WIP05_EAB.pdf "3G Long-Term Evolution" by Dr. Erik Dahlman at Ericsson Research]
* [http://www.calit2.net/events/pdfs/S3G_Stefan_Parkvall.pdf "Long-Term 3G Evolution – Radio Access" by Dr. Stefan Parkvall at Ericsson Research]
* [https://web.archive.org/web/20070927195715/http://www.ikr.uni-stuttgart.de/Content/itg/fg524/Meetings/2006-09-29-Ulm/01-3GPP_LTE-SAE_Overview_Sep06.pdf "3GPP Long-Term Evolution / System Architecture Evolution: Overview" by Ulrich Barth at Alcatel]
* [http://www.ericsson.com/res/thecompany/docs/journal_conference_papers/atsp/the_3g_long-term_evolution_radi_interface.pdf The 3G Long-Term Evolution – Radio Interface Concepts and Performance Evaluation]
* [http://www.3g4g.co.uk/Lte/LTE_Security_WP_0907_Agilent.pdf LTE and the Evolution to 4G Wireless Design and Measurement Challenges – "LTE Security"]
* [https://www.cosic.esat.kuleuven.be/ecrypt/courses/end/slides-28/9-niemi.pdf Role of Crypto in Mobile Communications "LTE Security"]
{{div col end}}
* [http://asp.eurasipjournals.com/content/pdf/1687-6180-2011-61.pdf LTE Uplink Interference Modeling]
{{Mobile telecommunications standards}}
{{DEFAULTSORT:3gpp Long Term Evolution}}
[[Category:協作項目|Category:協作項目]]