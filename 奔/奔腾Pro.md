{{Unreferenced|time=2016-12-04T18:14:04+00:00}}
{{noteTA
|G1=IT
}}
{{Infobox Computer Hardware Cpu
| name        = Pentium Pro
| image       = Ic-photo-intel-KB80521EX180-(pentium_pro).png
| caption     = Intel Pentium Pro微處理器
| produced-start =  1995年11月1日
| slowest     = 150  | slow-unit     = MHz
| fastest     = 200  | fast-unit     = MHz
| fsb-slowest = 60  | fsb-slow-unit = 
| fsb-fastest = 66  | fsb-fast-unit = 
| manuf1      = Intel
| arch        = x86
| size-from   = [[0.35微米製程|0.35µm]]
| size-to     = 0.50µm
| microarch   = [[Intel_P6|P6]]
| sock1       = Socket 8
}}

'''Pentium Pro'''為[[Intel|Intel]]的第一代[[Pentium|Pentium]]之后的下一代处理器，开创Intel的P6处理器架构。Pentium Pro的P6架构是Intel后期数款CPU架构的基础，一直沿用为[[Pentium_4|Pentium 4]]出现之前的所有Intel主流CPU的设计，后来的[[Intel_Core|Intel Core]]多核结构也是根据P6架构为单核原型的设计。Pentium Pro在1995年11月以[[Socket_8|Socket 8]]接口推出。

Pentium Pro以[[陶瓷|陶瓷]]或[[有機塑膠|有機塑膠]]封裝，其最大特色在於首先採用雙晶粒封裝與內建全速二級[[缓存|缓存]]，雙晶粒自然是指將運算核心與緩衝區兩顆[[晶片|晶片]]一同裝入CPU中，而片上（onchip）全速二級缓存則是因為这样做可以使得二级缓存可以与内核相同的频率运作，不必在像過去使用主機板上較慢速的L2記憶體。从而为“[[乱序执行|乱序执行]]”所导致的大量内存查找提供了捷径，直接提升了性能。此外，Pentium Pro还具备三个能够把x86指令转换成118位定长的[[RISC|RISC]]风格微操作的[[译码器|译码器]]（其中一个能把复杂x86指令转换成4个RISC风格微操作，另外两个解码器则是各可以把一条"简单"x86指令转换成一条RISC风格微操作，即所谓的“4+1+1”的3路解码格局）、实现了乱序执行等。

其二級緩存有256KB/512KB/1MB三款，其中1MB版本使用OLGA（有機塑膠封裝），但是肇因於[[0.35微米製程|0.35微米製程]]發熱功率甚大，故其時脈不曾高於233 MHz（正式版不超頻）。此外，由于指令队列的问题，Pentium Pro的16bit指令执行能力低于Pentium，造成Windows3.X和Windows9X与DOS系统下PentiumPro性能低下，被市场所诟病。

Pentium    PRO具有64條資料線，可一次傳輸64Bits的資料；两个8KB的L1 [[Cache|Cache]]。Pentium PRO有36條位址線，所以定址空間可以高達64GB。而且由於Pentium PRO的"非循序執行的超純量架構"，平均一個週期可執行三個指令，因此Pentium PRO的執行速度，可為Pentium的2倍。此外，為了匹配Pentium PRO的運算速度，Pentium PRO內建有256KB（最小）的L2 Cache，以避免使用到存取較慢的主記憶體而影響效率。另外Intel Pentium Pro也可以支援多處理器的架構。

因为Pentium Pro是一款全新设计的CPU，与Pentium CPU的架构完全不同。为了研发进度、可靠性、成本等综合考虑，所有各型号的Pentium Pro都没有包含[[MMX|MMX]]指令集。这影响了Pentium Pro在图形计算方面的性能。'''Pentium Pro'''的16位元计算性能有明显缺陷，16位元的软件在当时的Win9X操作系统上仍然有很多的应用。这也影响Pentium Pro的市场推广。随后的[[Pentium_II|Pentium II]]改进上述两个问题。

{{Intel_processors}}

[[Category:Intel_x86处理器|Category:Intel x86处理器]]