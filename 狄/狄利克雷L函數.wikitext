在[[數學|數學]]中，'''狄利克雷L函數'''是[[狄利克雷級數|狄利克雷級數]]的特例，它是形如下式的複變數函數

:<math>L(s,\chi) = \sum_{n=1}^\infty \frac{\chi(n)}{n^s}.</math>

在此 <math>\chi</math> 是一個[[狄利克雷特徵|狄利克雷特徵]]，<math>s \in \mathbb{C}</math> 的實部大於一。此函數可[[解析延拓|解析延拓]]為整個複平面上的[[亞純函數|亞純函數]]。

[[約翰·彼得·狄利克雷|約翰·彼得·狄利克雷]]證明對所有 <math>\chi</math> 俱有 <math>L(1,\chi) \neq 0</math>，並藉此證明[[狄利克雷定理|狄利克雷定理]]。若 <math>\chi</math> 是主特徵，則 <math>L(s,\chi)</math> 在 <math>s=1</math> 有單[[極點|極點]]。

==零點==
* 若 <math>\chi</math> 是原特徵，<math>\chi(-1)=1</math>，則 <math>L(s,\chi)</math> 在 <math>\mathrm{Re}(s) < 0</math> 的零點是負偶數。
* 若 <math>\chi</math> 是原特徵，<math>\chi(-1)=-1</math>，則 <math>L(s,\chi)</math> 在 <math>\mathrm{Re}(s) < 0</math> 的零點是負奇數。

不論可能的[[西格爾零點|西格爾零點]]，狄利克雷L函數有與[[黎曼ζ函數|黎曼ζ函數]]相似的無零點區域，包括 <math>\{s:\mathrm{Re}(s) \geq 1\}</math>。一如黎曼ζ函數，狄利克雷L函數也有相應的[[廣義黎曼猜想|廣義黎曼猜想]]。

==函數方程==
假設 <math>\chi</math> 是模 <math>k</math> 的原特徵。定義
:<math>\Lambda(s,\chi) = \left(\frac{\pi}{k}\right)^{-(s+a)/2}
\Gamma\left(\frac{s+a}{2}\right) L(s,\chi),</math>
此處 <math>\Gamma</math> 表[[Γ函數|Γ函數]]，而符號 <math>a</math> 由下式給出
:<math>a=\begin{cases}0,& \quad\chi(-1)=1, \\ 1,&\quad\chi(-1)=-1,\end{cases}</math>

則有[[函數方程|函數方程]]
:<math>\Lambda(1-s,\overline{\chi})=\frac{i^ak^{1/2}}{\tau(\chi)}\Lambda(s,\chi).</math>
此處的 <math>\tau(\chi)</math> 表[[高斯和|高斯和]]
:<math>\sum_{n=1}^k\chi(n)\exp(2\pi in/k).</math>
我們亦有 <math>|\tau(\chi)| = k^{\frac{1}{2}}</math>。

== 文獻 ==
* {{cite book|author=H. Davenport
| title=Multiplicative Number Theory
|publisher=Springer
|year=2000
|id=ISBN 0-387-95097-4}}

[[Category:解析數論|Category:解析數論]]
[[Category:Ζ函數與L函數|Category:Ζ函數與L函數]]