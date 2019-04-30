[[File:Chebyshev_s_plane.svg|right]]在''s''平面下的極點和零點，後續要用離離散濾波器來近似]]

[[File:Chebyshev_mapped_z_plane.svg|right]]

'''匹配Z变换方法'''（matched Z-transform method）也稱為'''極點-零點映射'''（pole–zero mapping）<ref name=":3">{{cite book
 | title = Signals and Systems with MATLAB
 | author = Won Young Yang
 | publisher = Springer
 | year = 2009
 | isbn = 978-3-540-92953-6
 | page = 292
 | url = https://books.google.com/books?id=GnfpELDfzmEC&pg=PA292
 }}</ref><ref>
{{cite book
 | title = Space vehicle dynamics and control
 | author = Bong Wie
 | publisher = AIAA
 | year = 1998
 | isbn = 978-1-56347-261-9
 | page = 151
 | url = https://books.google.com/books?id=n97tEQvNyVgC&pg=PA151
 }}</ref>或'''極點－零點匹配法'''（pole–zero matching method）<ref name=":1">{{cite book
 | title = Design and analysis of control systems
 | author = Arthur G. O. Mutambara
 | publisher = CRC Press
 | year = 1999
 | isbn = 978-0-8493-1898-6
 | page = 652
 | url = https://books.google.com/books?id=VSlHxALK6OoC&pg=PA652
 }}</ref>，簡稱'''MPZ'''或'''MZT'''<ref name=":4">{{Cite journal|last=Al-Alaoui|first=M. A.|date=February 2007|title=Novel Approach to Analog-to-Digital Transforms|url=http://ieeexplore.ieee.org/document/4089107/|journal=IEEE Transactions on Circuits and Systems I: Regular Papers|volume=54|issue=2|pages=338–350|doi=10.1109/tcsi.2006.885982|issn=1549-8328}}</ref>，是將{{le|連續時間及離散時間|Discrete_time_and_continuous_time|連續時間}}濾波器轉換到離散時間濾波器（[[数字滤波器|数字滤波器]]）設計的技巧。

其作法是將所有的[[拉普拉斯变换|s平面]]設計時的極點和零點轉換到[[Z轉換|z平面]]的位置<math>z=e^{sT}</math>，其中取樣週期<math>T=1 / f_\mathrm{s}</math><ref>
{{cite book
 | title = Signal processing: principles and implementation
 | author = S. V. Narasimhan and S. Veena
 | publisher = Alpha Science Int'l Ltd.
 | year = 2005
 | isbn = 978-1-84265-199-5
 | page = 260
 | url = https://books.google.com/books?id=8UbV8vq8uV0C&pg=PA260
 }}</ref>。因此以下傳遞函數的類比濾波器：

:<math>H(s) = k_{\mathrm a} \frac{\prod_{i=1}^M (s-\xi_i) }{\prod_{i=1}^N (s-p_i) }</math>

會轉換為以下的數位傳遞函數

:<math> H(z) = k_{\mathrm d} \frac{ \prod_{i=1}^M (1 - e^{\xi_iT}z^{-1})}{ \prod_{i=1}^N (1 - e^{p_iT}z^{-1})} </math>

其增益<math>k_{\mathrm d}</math>需調整，使結果為其理想的增益，一般會和類比濾波器的直流增益匹配，透過[[终值定理|設定<math>s=0</math>及<math>z=1</math>]]，並且求解<math>k_{\mathrm d}</math>.<ref name=":1" /><ref name=":2">{{Cite book|url=https://www.worldcat.org/oclc/869825370|title=Feedback control of dynamic systems|last=Franklin|first=Gene F.|date=2015|publisher=Pearson|others=Powell, J. David, Emami-Naeini, Abbas|year=|isbn=0133496597|edition=Seventh|location=Boston|pages=607–611|oclc=869825370|quote=Because physical systems often have more poles than zeros, it is useful to arbitrarily add zeros at z = -1.}}</ref>。

因為此映射會將''s''平面的<math>j\omega</math>軸反覆的映射到''z''平面的單位圓上，若零點或是極點超過[[奈奎斯特頻率|奈奎斯特頻率]]，其映射後的位置會有混疊的情形<ref name=":0">{{Cite book|url=|title=Theory and application of digital signal processing|last=Rabiner|first=Lawrence R|last2=Gold|first2=Bernard|date=1975|publisher=Prentice-Hall|year=|isbn=0139141014|location=Englewood Cliffs, New Jersey|pages=224–226|language=en|quote=The expediency of artificially adding zeros at z = —1 to the digital system has been suggested ... but this ad hoc technique is at best only a stopgap measure. ... In general, use of impulse invariant or bilinear transformation is to be preferred over the matched z transformation.}}</ref>。

一般情形下，類比濾波器的極點會比零點多，在<math>s=\infty</math>處的零點可以移到奈奎斯特頻率，作法是放在<math>z=-1</math>的位置<!--dropping off like the BLT--><ref name=":3" /><ref name=":1" /><ref name=":2" /><ref name=":0" />。

此轉換方式可以保持[[有界輸入有界輸出穩定性|有界輸入有界輸出穩定性]]以及[[最小相位|最小相位]]，但不會保持時域或是頻域的響應，因此不常使用<ref>{{Cite book|url=https://books.google.com/books?id=VZ8uabI1pNMC&lpg=PA262&ots=gSD3om4Hy4&pg=PA262|title=Digital Filters and Signal Processing|last=Jackson|first=Leland B.|date=1996|publisher=Springer Science & Business Media|year=|isbn=9780792395591|location=|pages=262|language=en|quote=although perfectly usable filters can be designed in this way, no special time- or frequency-domain properties are preserved by this transformation, and it is not widely used.}}</ref><ref name=":0" />。較常使用的方式有[[雙線性轉換|雙線性轉換]]及[[冲激不变法|冲激不变法]]<ref name=":4" />。匹配Z变换方法的高頻響應誤差比雙線性轉換要小，因此比較容易透過加入額外的零點來修正其特性，此方式稱為MZTi（i表示改良版improved）<ref>{{Cite journal|last=Ojas|first=Chauhan|last2=David|first2=Gunness|date=2007-09-01|title=Optimizing the Magnitude Response of Matched Z-Transform Filters ("MZTi") for Loudspeaker Equalization|url=http://www.aes.org/e-lib/browse.cfm?elib=14198|journal=Audio Engineering Society|language=en|volume=|pages=|archive-url=http://www.khabdha.org/wp-content/uploads/2008/03/optimizing-the-magnitude-response-of-mzt-filters-mzti-2007.pdf|archive-date=2007|via=}}</ref>。

在數位控制中，匹配Z变换方法有一個特別的應用，就是{{link-en|艾克曼公式|Ackermann's formula}}，可以調整[[可控制性|可控制性]]系統的極點，一般會將不穩定（或接近不穩定）的極點調整到穩定的位置。

[[File:Chebyshev_responses.svg|thumb]]

==參考資料==
{{reflist}}
{{DSP}}
[[Category:控制理论|Category:控制理论]]
[[Category:数字信号处理|Category:数字信号处理]]
[[Category:滤波器理论|Category:滤波器理论]]