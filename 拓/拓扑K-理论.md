{{Link style|time=2015-12-11T07:12:27+00:00}}
[[数学|数学]]中，'''拓扑 K-理论'''（{{lang|en|topological K-theory}}）是[[代数拓扑|代数拓扑]]的一个分支。它是研究一般[[拓扑空间|拓扑空间]]上[[向量丛|向量丛]]时发现的，所用的是由[[亚历山大·格罗滕迪克|亚历山大·格罗滕迪克]]引入的现在称为（一般）[[K-理论|K-理论]]的想法。早期拓扑 K-理论的工作归于[[迈克尔·阿蒂亚|迈克尔·阿蒂亚]]与[[弗里德里希·希策布鲁赫|弗里德里希·希策布鲁赫]]（[[:en:Friedrich_Hirzebruch|Friedrich Hirzebruch]]）。

== 定义 ==
拓扑 K-理论是[[紧空间|紧]][[豪斯多夫空间|豪斯多夫空间]][[范畴_(数学)|范畴]]的一种广义[[上同调理论|上同调理论]]，将一个空间上的[[向量丛|向量丛]]按[[稳定等价|稳定等价]]分类（向量丛称为稳定等价的当且仅当[[同构|同构]]的向量丛由向量丛与平凡向量丛的[[惠特尼和|惠特尼和]]生成<ref>http://mathworld.wolfram.com/StableEquivalence.html</ref>）。设 ''X'' 是一个紧豪斯多夫空间而 <math>k=\mathbb{R}</math> 或 <math>k=\mathbb{C}</math>。则 <math>K_{k}(X)</math> 是 ''X'' 上有限维 <math>k</math>-向量丛的[[同构类|同构类]]在运算
:<math>[E]\oplus [F] = [E\oplus F]</math>，对向量丛 ''E'' 与 ''F''，
下[[交换幺半群|交换幺半群]]的[[格罗滕迪克群|格罗滕迪克群]]。通常 <math>K_k(X)</math> 在复情形记作 <math>KO(X)</math>，复情形记作 <math>KU(X)</math>。

更确切地，'''稳定等价'''，''X'' 上丛 ''E'' 与 ''F'' 上的[[等价关系|等价关系]]，定义了  ''K''(''X'') 中同样的元素，出现于存在一个[[平凡丛|平凡丛]] ''G'' 使得
:<math>E\oplus G\cong F\oplus G.</math>

在[[向量丛的张量积|向量丛的张量积]]下 ''K''(''X'') 成为一个[[交换环|交换环]]。

[[向量丛的秩|向量丛的秩]]带入 ''K''-群中定义了同态

:<math>K(X)\to\check{H}^0(X,\mathbb{Z})</math>

这里 <math>\check{H}^0(X,\mathbb{Z})</math> 是[[切赫上同调|切赫上同调]]的 0-群，等于取值于 <math>\mathbb{Z}</math> 中的局部常值函数群。

如果 ''X'' 有一个[[带基点空间|特殊的基点]] x<sub>0</sub>，则约化 ''K''-群（与[[约化同调|约化同调]]比较）满足

:<math>K(X)\cong\tilde K(X)\oplus K(\{x_0\})</math>

定义为 <math>K(X)\to K(\{x_0\})</math>（这里 <math>\{x_0\}\to X</math> 是基点包含）的[[核_(范畴论)|核]]或 <math>K(\{x_0\})\to K(X)</math> 的[[余核|余核]]（这里 <math>X\to\{x_0\}</math> 是常映射）。

当 ''X'' 是[[连通空间|连通空间]]是，<math>\tilde K(X)\cong\operatorname{Ker}(K(X)\to\check{H}^0(X,\mathbb{Z})=\mathbb{Z})</math>。

函子 ''K'' 的定义扩张成[[紧空间|紧空间]]的[[范畴_(数学)|范畴]]偶（一个对象是一个偶 <math>(X,Y)</math>，<math>X</math> 紧而 <math>Y\subset X</math> 闭，<math>(X,Y)</math> 与 <math>(X',Y')</math> 间的[[态射|态射]]是一个连续映射 <math>f:X\to X'</math> 使得 <math>f(Y)\subset Y'</math>）。

:<math>K(X,Y):=\tilde{K}(X/Y)</math>

约化 ''K''-群有 <math>x_0=\{Y\}</math> 给出。

定义

:<math> K_{\mathbb{C}}^{n}(X,Y)=\tilde K_{\mathbb{C}}(S^{|n|}(X/Y)),</math> 

对 <math>n\in\mathbb{Z}</math> 给出了 ''K''-群序列，这里 ''S'' 表示[[约化纬垂|约化纬垂]]（[[:en:reduced_suspension|reduced suspension]]）。

== 性质 ==

* <math>K^n</math> 是一个[[反变函子|反变函子]]。
* <math>\tilde{K}</math> 的[[分类空间|分类空间]]是 <math>BO_k</math>（复情形为 ''BO''；复情形为 ''BU''），即 <math>K_k(X)\cong[X,BO_k]</math>。
* <math>K</math> 的[[分类空间|分类空间]]是 <math>\mathbb{Z}\times BO_k</math>（<math>\mathbb{Z}</math> 带着[[离散拓扑|离散拓扑]]），即 <math>K_k(X)\cong[X,\mathbb{Z}\times BO_k]</math>。
* 存在一个[[自然同态|自然]][[环同态|环同态]] <math>K^*(X)\to H^{2*}(X,\mathbb{Q})</math>，[[陈特征标|陈特征标]]（[[:en:Chern_character|Chern character]]），使得 <math>K^*(X)\otimes\mathbb{Q}\to H^{2*}(X,\mathbb{Q})</math> 是一个同构。
* 拓扑 K-理论可推广为 [[C*-代数|C*-代数]]上一个函子，参见[[算子K-理论|算子K-理论]]与 [[KK-理论|KK-理论]]。

== 博特周期性 ==

[[周期性|周期性]]现象冠以[[拉乌尔·博特|拉乌尔·博特]]之名（参见[[博特周期性定理|博特周期性定理]]），可作如下表述：
* <math>K(X\times S^2)=K(X)\otimes K(S^2),</math> and <math>K(S^2)=\mathbb Z[H]/(H-1)^2;</math> 这里 <math>H</math> 是 <math>S^2=\mathbb CP^1</math> 上的[[重言丛|重言丛]]类，即[[黎曼球面|黎曼球面]]作为[[复射影直线|复射影直线]]。
* <math>\tilde K^{n+2}(X)=\tilde K^n(X).</math>
* <math>\Omega^2\mathrm{BU}\simeq\mathrm{BU}\times\mathbf Z.</math>

在[[实K-理论|实K-理论]]中有类似的周期性，不过是模 8。

==参考文献==
<references/>
*M. Karoubi, [https://web.archive.org/web/20070913181033/http://www.institut.math.jussieu.fr/~karoubi/KBook.html K-theory, an introduction], 1978 - Berlin; New York: Springer-Verlag 
*M.F. Atiyah, D.W. Anderson ''K-Theory'' 1967 - New York, WA Benjamin

[[Category:代数拓扑|Category:代数拓扑]]
[[Category:K-理论|Category:K-理论]]