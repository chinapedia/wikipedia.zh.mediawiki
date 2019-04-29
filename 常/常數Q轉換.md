'''常數Q轉換'''（{{lang|en|Constant Q transform}}）與[[短時距傅立葉轉換|短時距傅立葉轉換]]一樣為重要[[時頻分析|時頻分析]]工具，其中特別適用於音樂信號的分析，這個轉換產生的[[頻譜|頻譜]]最大的特色是在於頻率軸為對數標度（log scale）而不是線性標度（linear scale），且窗口長度（window length）會隨著頻率而改變。

== 基本概念 ==

[[十二平均律|十二平均律]]告訴我們，一個音會與其高[[八度|八度]]的的音頻率相差兩倍，我們以比率<math>2^{ \frac {1}{12} }</math>將一個八度平均分為十二等分（十二個半音），換句話說在一個八度中，十二個音的頻率會呈現等比數列，公比為<math>2^{ \frac {1}{12} }</math> (約為1.06)，如今各式各樣的音樂類型均符合十二平均律，所以常數Q轉換可說是十分適用於分析各種不同的音樂類型。

常數Q轉換是根據十二平均律，在頻率軸上每個八度均用12n格來表示，也就是說每個八度中十二個音均會被分到n格。另一方面來說，常數Q轉換其實就是一個1/(12n)th-oct 濾波器組（filter bank），第k個[[濾波器|濾波器]]的頻寬會是前一個濾波器的波長乘上一個倍數，也就是說

<math>\delta f_k = 2^{ \frac {1}{12n} } * \delta f_{k-1}</math>

換句話說，

<math>\delta f_k = (2^{ \frac {1}{12n} })^{k} * \delta f_{min}</math>

其中<math>f_{min}</math>為時頻圖上顯示的最小頻率。

== 計算方式 ==

常數Q轉換的計算方式大致與短時距傅立葉轉換相同，唯一的兩個差異是

1. 所使用的窗口（window）長度會隨著頻率而改變。

2. 頻率軸為對數標度(log scale)。

以下為短時距傅立葉轉換運算式，若要改成常數Q轉換只要將N與k作修正即可。

<math>X \left[ k \right] = \sum_{n=0}^{N-1} W[n] x[n] e^ { \frac{-j2 \pi kn}{N}} </math>

前面提過，這個轉換可視為濾波器組，其中第k個濾波器的頻寬為<math>\delta f_k</math>，

我們定義品質因子Q，<math> Q = \frac{f_k}{\delta f_k}</math>，

Q的值為常數，不會因為<math>f_k</math>而改變，順帶一提，此轉換的名稱便是從這裡來的。

<math>f_k</math>是第k個濾波器的中心頻率，也是時頻圖上第k格所代表的頻率
而窗口長度N表示如下

<math>N = N[k] = Q \frac {f_s}{f_k}</math>

其中<math>f_s</math>為取樣頻率，所以頻率越高，窗口長度越短。

除此之外，我們用<math> \frac {2 \pi Q}{N[k]} </math>來取代<math> \frac {2 \pi k}{N} </math>，目的是要讓頻率軸上每個八度均用12n格來表示。

所以常數Q轉換

<math>X \left[ k \right] = \frac {1}{N[k]} \sum_{n=0}^{N[k]-1} W[k,n] x[n] e^ { \frac{-j2 \pi Qn}{N[k]}} </math>

轉換結果除以N(窗口長度)的原因是要作一個歸一化(normalization)，這是由於不同頻率窗口長度不同的緣故。

== 特性 ==

常數Q轉換可說是為音樂訊號設計的，其中第一個原因是它讓窗口長度隨著頻率改變，進而提高低頻在頻域的解析度。

下表為C和C#在不同八度時的頻率： 
{| class="wikitable"
|-
| Midi number || C2 || C#2 || C5 || C#5
|-
| Frequency || 65.4 Hz || 69.2 Hz || 523.3 Hz || 554.4 Hz
|}
				
其中C2和C#2為低音，兩者間的頻率差不到4 Hz，然而C5和C#5為高三個八度的音，兩者間頻率差增加30 Hz 左右。
所以在線性標度的轉換下(比方說傅立葉轉換)，低音部分頻域的解析度會很差，這在判斷音高上造成極大的不便。

低頻部分窗口長度加長，這樣可以改善低頻頻域的解析度，避免音高的誤判，但改善解析度的唯一缺點是會犧牲低頻部分時域的解析度。

第二個原因是他在頻域軸上是對數標度，這會比線性標度更符合人耳聽覺系統，且產生出來的時頻圖較容易閱讀。

== 參考資料 ==

Judith C. Brown, [http://www.wellesley.edu/Physics/brown/pubs/cq1stPaper.pdf Calculation of a constant Q spectral transform], ''J. Acoust. Soc. Am.'', 89(1):425–434, 1991.


{{DEFAULTSORT:Constant Q Transform}}
[[Category:积分变换|Category:积分变换]]
[[Category:調和分析|Category:調和分析]]