'''巴尼斯G函数'''是[[階乘#超級階乘|超级阶乘]]函数在[[复数_(数学)|复数]]上的扩展。它与[[Γ函数|Γ函数]]、[[K函数|K函数]]以及[[格莱舍常数|格莱舍常数]]（Glaisher constant）有关。以[[数学家|数学家]][[欧尼斯特·巴尼斯|欧尼斯特·巴尼斯]]（Ernest William Barnes）的名字命名。<ref> E.W.Barnes, "The theory of the G-function", ''Quarterly Journ. Pure and Appl. Math.'' '''31''' (1900), 264-314.</ref>

巴尼斯G函数可以通用[[魏尔施特拉斯分解定理|魏尔施特拉斯分解定理]]的形式定义为：

:<math>G(z+1)=(2\pi)^{z/2} e^{-[z(z+1)+\gamma z^2]/2}\prod_{n=1}^\infty \left[\left(1+\frac{z}{n}\right)^ne^{-z+z^2/(2n)}\right].</math>
其中，γ表示欧拉-马歇罗尼常数。

==差分方程、函数方程与特殊值==

巴尼斯G函数满足[[差分方程|差分方程]]

:<math>G(z+1)=\Gamma(z)G(z).</math>

特殊地，G(1)=1. 从此方程可推出G取整数自变量时有：

:<math>G(n)=\begin{cases} 0&\mbox{if }n=0,-1,-2,\dots\\ \prod_{i=0}^{n-2} i!&\mbox{if }n=1,2,\dots\end{cases}.</math>

因此，

:<math>G(n)=\frac{(\Gamma(n))^{n-1}}{K(n)}.</math>
其中，<math>\Gamma(n)</math>表示[[Γ函数|Γ函数]]，<math>K(n)</math>表示[[K函数|K函数]]。

另外，在满足条件<math>\frac{d^3}{dx^3}G(x)\geq 0</math>时，差分方程唯一确定一个G函数。<ref>M. F. Vignéras, ''L'équation fonctionelle de la fonction zêta de Selberg du groupe mudulaire SL<math>(2,\mathbb{Z})</math>'', Astérisque '''61''', 235-249 (1979).</ref>.

由G函数的差分方程和Γ函数的函数方程可以得到（由Hermann Kinkelin提出）：

:<math> G(1-z) = G(1+z)\frac{ 1}{(2\pi)^z} \exp \int_0^z \pi x \cot \pi x \, dx.</math>

==乘法公式==

与Γ函数一样，G函数也有其乘法公式：<math>
G(nz)= K(n) n^{n^{2}z^{2}/2-nz} (2\pi)^{-\frac{n^2-n}{2}z}\prod_{i=0}^{n-1}\prod_{j=0}^{n-1}G\left(z+\frac{i+j}{n}\right).
</math>

:<math>
G(nz)= K(n) n^{n^{2}z^{2}/2-nz} (2\pi)^{-\frac{n^2-n}{2}z}\prod_{i=0}^{n-1}\prod_{j=0}^{n-1}G\left(z+\frac{i+j}{n}\right).
</math>

其中K是一个常数，定义为：

:<math> K(n)= e^{-(n^2-1)\zeta^\prime(-1)} \cdot
n^{\frac{5}{12}}\cdot(2\pi)^{(n-1)/2}\,=\,
(Ae^{-\frac{1}{12}})^{n^2-1}\cdot n^{\frac{5}{12}}\cdot (2\pi)^{(n-1)/2}.</math>

其中<math>\zeta^\prime</math>表示[[黎曼ζ函数|黎曼ζ函数]]的[[导函数|导函数]]，<math>A</math>则表示为格莱舍常数。

<math>\log \,G(z+1 )</math>可[[渐近展开|渐近展开]]为（由巴尼斯提出）：

:<math> \log G(z+1)=\frac{1}{12} - \log A + \frac{z}{2}\log 2\pi +\left(\frac{z^2}{2} -\frac{1}{12}\right)\log z -\frac{3z^2}{4}+
\sum_{k=1}^{N}\frac{B_{2k+2}}{4k\left(k+1\right)z^{2k}} + O\left(\frac{1}{z^{2N+2}}\right).</math>

其中<math>B_{k}</math>为伯努利数，<math>A</math>为格莱舍常数。（需要注意的是，在巴尼斯的时代，伯努利数<math>B_{2k}</math>习惯写成<math>(-1)^{k+1} B_k </math>。）

==相关条目==
* [[Γ函数|Γ函数]]
* [[K函数|K函数]]

==参考==
{{reflist}}

[[Category:数论|Category:数论]]
[[Category:伽玛及相关函数|Category:伽玛及相关函数]]