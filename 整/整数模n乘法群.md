{{Link style|time=2015-12-12T02:12:56+00:00}}
在[[同余|同余]]理论中，模 ''n'' 的[[互质|互质]][[同余类|同余类]]组成一个[[乘法|乘法]][[群|群]]，称为'''整数模 n 乘法群'''，也称为'''模 n 既约剩余类'''。在[[环_(代数)|环理论]]中，一个[[抽象代数|抽象代数]]的分支，也称这个群为整数模 n 的环的[[单位_(环论)|单位]]群（单位是指乘法可逆元）。

这个群是数论的基石，在[[密码学|密码学]]、[[整数分解|整数分解]]和[[素性测试|-{zh-hans: 素性测试; zh-hant: 質數測試}-]]均有运用。例如，关于这个群的阶（即群的“大小”），我们可以确定如果 ''n'' 是[[质数|质数]][[当且仅当|当且仅当]]阶数为 ''n''-1。

== 群公理 ==
容易验证模 ''n'' 互质同余类在乘法运算下满足[[阿贝尔群|阿贝尔群]]的公理。

:恒同: 1 是恒同；

:闭：如果 ''a'' 和 ''b'' 都与 ''n'' 互质，那么 ''ab'' 也是；

:逆：找 ''x'' 满足 ''ax'' ≡ 1 (mod ''n'') 等价于解 ''ax'' + ''ny'' = 1，可用[[欧几里得算法|欧几里得算法]]求出；

:结合性和交换性：由整数的相应事实以及模 ''n'' 运算是一个环[[同态|同态]]推出。

== 记法 ==
整数模 ''n'' 环记作 <math>\mathbb{Z}/n\mathbb{Z}</math> 或 <math>\mathbb{Z}/(n)</math>（即整数环模去[[理想_(环论)|理想]] ''n'''''Z''' = (''n'') ，由 ''n'' 的倍数组成）或 <math>\mathbb{Z}_n.</math> 因作者所喜，它的单位群可能记为 <math>(\mathbb{Z}/n\mathbb{Z})^*,</math> <math>(\mathbb{Z}/n\mathbb{Z})^\times,</math> <math>U(\mathbb{Z}/n\mathbb{Z}),</math> 或类似的记号，本文采用 <math>(\mathbb{Z}/n\mathbb{Z})^\times.</math>

== 结构 ==
=== 2 的幂次 ===
模 2 只有一个互质同余类 1，所以
<math>(\mathbb{Z}/2\mathbb{Z})^\times \cong \{1\}</math> 平凡。

模 4 有两个互质同余类，1 和 3，所以 <math>(\mathbb{Z}/4\mathbb{Z})^\times \cong C_2,</math> 两元循环群。

模 8 有四个互质同余类，1, 3, 5 和 7，每个平方都是 1，所以 <math>(\mathbb{Z}/8\mathbb{Z})^\times \cong  C_2 \times C_2,</math> [[Klein_四元群|Klein 四元群]]。

模 16 有八个互质同余类，1, 3, 5, 7, 9, 11, 13 和 15。<math>\{\pm 1, \pm 7\}\cong  C_2 \times C_2,</math> 为 2-扭子群（即每个元素的平方为 1），所以 <math>(\mathbb{Z}/16\mathbb{Z})^\times</math> 不是循环群。3的幂次：<math>\{1, 3, 9, 11\}</math> 是一个 4 阶子群，5 的幂次也是，<math>\{1, 5, 9, 13\}</math>。所以 <math>(\mathbb{Z}/16\mathbb{Z})^\times \cong C_2 \times C_4</math>。 

以上 8 和 16 的讨论对高阶幂次 2<sup>''k''</sup>, ''k'' > 2<ref>高斯, DA, arts. 90-91</ref> 也成立：
<math>\{\pm 1, 2^{ k-1} \pm 1\}\cong  C_2 \times C_2,</math> 是 2-扭子群（所以 <math>(\mathbb{Z}/2^k\mathbb{Z})^\times </math> 不是循环）而 3 的幂次是一个2<sup>''k''- 2</sup> 子群，所以 <math>(\mathbb{Z}/2^k\mathbb{Z})^\times  \cong C_2 \times C_{2^{k-2}}</math>。

=== 奇质数的幂 ===
对奇质数的幂 ''p''<sup>''k''</sup>，此群是循环群：<ref>高斯, DA, arts.52-56, 82-89</ref> <math>\;\;(\mathbb{Z}/p^k\mathbb{Z})^\times  \cong C_{p^{k-1}(p-1)} \cong C_{\varphi(p^k)}.</math>

===一般合数===
[[中国剩余定理|中国剩余定理]]<ref>Riesel 包含所有情形。 pp. 267-275</ref> 说明如果<math>\;\;n=p_1^{k_1}p_2^{k_2}p_3^{k_3}\dots, \;</math> 那么环 <math>\mathbb{Z}/n\mathbb{Z}</math> 每个质数幂因子相应的环的[[环的乘积|直积]]：

:<math>\mathbb{Z}/n\mathbb{Z}  \cong \mathbb{Z}/{p_1^{k_1}}\mathbb{Z}\; \times \;\mathbb{Z}/{p_2^{k_2}}\mathbb{Z} \;\times\; \mathbb{Z}/{p_3^{k_3}}\mathbb{Z}\dots\;\;</math> 

类似地，<math>(\mathbb{Z}/n\mathbb{Z})^\times</math> 的单位群是每个质数幂因子相应群的直积：

:<math>(\mathbb{Z}/n\mathbb{Z})^\times\cong (\mathbb{Z}/{p_1^{k_1}}\mathbb{Z})^\times \times (\mathbb{Z}/{p_2^{k_2}}\mathbb{Z})^\times  \times (\mathbb{Z}/{p_3^{k_3}}\mathbb{Z})^\times  \dots\;.</math>

== 阶数 ==
群的阶数由[[欧拉函数|欧拉函数]]给出：<math>| (\mathbb{Z}/n\mathbb{Z})^\times|=\varphi(n).</math> {{OEIS|id=A000010}}
这是直积中各循环阶数的乘积。

== 指数 ==
指数为[[卡邁克爾函數|卡邁克爾函數]]<math>\lambda(n)</math>，{{OEIS|id=A002322}}，即这些循环群的阶数的[[最小公倍数|最小公倍数]]。这意味着如果 ''a'' 和 ''n'' 互质，<math>a^{\lambda(n)} \equiv 1 \pmod n.</math>

== 生成元 ==
<math>(\mathbb{Z}/n\mathbb{Z})^\times</math> 是[[循环群|循环群]]当且仅当 <math>\varphi(n)=\lambda(n).</math> 这在 ''n'' 为奇质数的幂次、奇质数幂次 2 倍、2 和 4 成立，此时也称一个生成元为'''[[模n原根|模 n 的原根]]'''。

因为所有 <math>(\mathbb{Z}/n\mathbb{Z})^\times,</math> ''n'' = 1, 2, ..., 7 是循环群，上述结论的另一种说法是：如果 ''n'' < 8 那么 <math>\;(\mathbb{Z}/n\mathbb{Z})^\times</math> 有原根；如果 ''n'' ≥ 8，且不能被 4 或者两个不同的奇质数整除，<math>\;(\mathbb{Z}/n\mathbb{Z})^\times</math> 有原根。({{oeis|id=A033948}} = 1, 2, 3, 4, 5, 6, 7, 9, 10, 11, 13, 14, 17, 18, 19, 22, 23, 25, 26, 27, 29, 31, 34, 37, 38, 41, 43, 46, 47, 49, 50, ... )

一般情形每个直积因子循环有一个生成元。

== 列表 ==
这个表列出了较小 ''n'' <math>(\mathbb{Z}/n\mathbb{Z})^\times</math> 的结构和生成元。生成元不是惟一（mod ''n''）的，比如 (mod 16) 时 {–1, 3} 和{–1, 5} 都可以。生成元以和直积因子相同的顺序列出。

以 ''n''=20 为例。<math>\varphi(20)=8</math> 意味着 <math>(\mathbb{Z}/20\mathbb{Z})^\times</math> 的阶数是 8（即有 8 个小于 20 的正整数与其互质）；<math>\lambda(20)=4</math> 说明任何和20互质的数的 4 次幂≡ 1(mod 20)；至于生成元，19 的指数为2，3 的指数为 4，而任何<math>(\mathbb{Z}/20\mathbb{Z})^\times</math> 中元素都是 19<sup>''a''</sup> × 3<sup>''b''</sup> 的形式，这里 ''a'' 为 0 或 1，''b'' 为 0, 1, 2, 或 3。

<blockquote>19 的幂是 {±1}，3 的幂为 {3, 9, 7, 1}。后者和他们的负数 (mod 20)，{17, 11, 13, 19} 是所有小于 20 且与其互质的数。19 的指数为 2 而 3 的指数为 4 意味着任何 <math>\mathbb{Z}_{20}^\times</math> 中数的 4 次幂 ≡ 1 (mod 20)。</blockquote>

{|  class="wikitable" style="text-align:center" cellpadding="2"

|+ '''(Z/''n''Z)<sup>×</sup>''' 的群结构

|-
! <math>n</math> || <math>(\mathbb{Z}/n\mathbb{Z})^\times</math> || <math>\varphi(n)</math> || <math>\lambda(n)</math> || 生成元
| width="25" rowspan="32" |  
! <math>n</math> || <math>(\mathbb{Z}/n\mathbb{Z})^\times</math> || <math>\varphi(n)</math> || <math>\lambda(n)</math> || 生成元
| width="25" rowspan="32" |  
! <math>n</math> || <math>(\mathbb{Z}/n\mathbb{Z})^\times</math> || <math>\varphi(n)</math> || <math>\lambda(n)</math> || 生成元
|-
! 1
| C<sub>1</sub> || 1 || 1 || 0
! 32 
| C<sub>2</sub>×C<sub>8</sub>  || 16 || 8 || 31, 3
! 63 
| C<sub>6</sub>×C<sub>6</sub> || 36 || 6 || 2, 5
|-
! 2 
| C<sub>1</sub> || 1 || 1 || 1
! 33 
| C<sub>2</sub>×C<sub>10</sub> || 20 || 10 || 10, 2
! 64
| C<sub>2</sub>×C<sub>16</sub> || 32 || 16 || 3, 63
|-
! 3 
| C<sub>2</sub> || 2 || 2 || 2
! 34 
| C<sub>16</sub> || 16 || 16 || 3
! 65
| C<sub>4</sub>×C<sub>12</sub> || 48 || 12 || 2, 12
|-
! 4 
| C<sub>2</sub> || 2 || 2 || 3
! 35 
| C<sub>2</sub>×C<sub>12</sub> || 24 || 12 || 6, 2
! 66
| C<sub>2</sub>×C<sub>10</sub> || 20 || 10 || 5, 7
|-
! 5
| C<sub>4</sub> || 4 || 4 || 2
! 36 
| C<sub>2</sub>×C<sub>6</sub> || 12 || 6 || 19, 5
! 67
| C<sub>66</sub> || 66 || 66 || 2
|-
! 6 
| C<sub>2</sub> || 2 || 2 || 5
! 37 
| C<sub>36</sub> || 36 || 36 || 2
! 68
| C<sub>2</sub>×C<sub>16</sub> || 32 || 16 || 3, 67
|-
! 7 
| C<sub>6</sub> || 6 || 6 || 3
! 38 
| C<sub>18</sub> || 18 || 18 || 3
! 69
| C<sub>2</sub>×C<sub>22</sub> || 44 || 22 || 2, 68
|-
! 8 
| C<sub>2</sub>×C<sub>2</sub> || 4 || 2 || 7, 3
! 39 
| C<sub>2</sub>×C<sub>12</sub> || 24 || 12 || 38, 2
! 70
| C<sub>2</sub>×C<sub>12</sub> || 24 || 12 || 3, 11
|-
! 9 
| C<sub>6</sub> || 6 || 6 || 2
! 40 
| C<sub>2</sub>×C<sub>2</sub>×C<sub>4</sub> || 16 || 4 || 39, 11, 3
! 71
| C<sub>70</sub> || 70 || 70 || 7
|-
! 10 
| C<sub>4</sub> || 4 || 4 || 3
! 41 
| C<sub>40</sub> || 40 || 40 || 6
! 72
| C<sub>2</sub>×C<sub>2</sub>×C<sub>6</sub> || 24 || 12 || 5, 7, 11
|-
! 11 
| C<sub>10</sub> || 10 || 10 || 2
! 42 
| C<sub>2</sub>×C<sub>6</sub> || 12 || 6 || 13, 5
! 73
| C<sub>72</sub> || 72 || 72 || 5
|-
! 12 
| C<sub>2</sub>×C<sub>2</sub> || 4 || 2 || 5, 7
! 43 
| C<sub>42</sub> || 42 || 42 || 3
! 74
| C<sub>36</sub> || 36 || 36 || 5
|-
! 13 
| C<sub>12</sub> || 12 || 12 || 2
! 44 
| C<sub>2</sub>×C<sub>10</sub> || 20 || 10 || 43, 3
! 75
| C<sub>2</sub>×C<sub>20</sub> || 40 || 20 || 2, 74
|-
! 14 
| C<sub>6</sub> || 6 || 6 || 3
! 45 
| C<sub>2</sub>×C<sub>12</sub> || 24 || 12 || 44, 2
! 76
| C<sub>2</sub>×C<sub>18</sub> || 36 || 18 || 3, 75
|-
! 15 
| C<sub>2</sub>×C<sub>4</sub> || 8 || 4 || 14, 2
! 46 
| C<sub>22</sub> || 22 || 22 || 5
! 77
| C<sub>2</sub>×C<sub>30</sub> || 60 || 30 || 2, 76
|-
! 16 
| C<sub>2</sub>×C<sub>4</sub> || 8 || 4 || 15, 3
! 47 
| C<sub>46</sub> || 46 || 46 || 5
! 78
| C<sub>2</sub>×C<sub>12</sub> || 24 || 12 || 5, 7
|-
! 17 
| C<sub>16</sub> || 16 || 16 || 3
! 48 
| C<sub>2</sub>×C<sub>2</sub>×C<sub>4</sub> || 16 || 4 || 47, 7, 5
! 79
| C<sub>78</sub> || 78 || 78 || 3
|-
! 18 
| C<sub>6</sub> || 6 || 6 || 5
! 49 
| C<sub>42</sub> || 42 || 42 || 3
! 80
| C<sub>2</sub>×C<sub>4</sub>×C<sub>4</sub> || 32 || 4 || 3, 7, 11
|-
! 19 
| C<sub>18</sub> || 18 || 18 || 2
! 50 
| C<sub>20</sub> || 20 || 20 || 3
! 81
| C<sub>54</sub> || 54 || 54 || 2
|-
! 20 
| C<sub>2</sub>×C<sub>4</sub> || 8 || 4 || 19, 3
! 51 
| C<sub>2</sub>×C<sub>16</sub> || 32 || 16 || 50, 5
! 82
| C<sub>40</sub> || 40 || 40 || 7
|-
! 21 
| C<sub>2</sub>×C<sub>6</sub> || 12 || 6 || 20, 2
! 52 
| C<sub>2</sub>×C<sub>12</sub> || 24 || 12 || 51, 7
! 83
| C<sub>82</sub> || 82 || 82 || 2
|-
! 22 
| C<sub>10</sub> || 10 || 10 || 7
! 53 
| C<sub>52</sub> || 52 || 52 || 2
! 84
| C<sub>2</sub>×C<sub>2</sub>×C<sub>6</sub> || 24 || 12 || 5, 11, 13
|-
! 23 
| C<sub>22</sub> || 22 || 22 || 5
! 54 
| C<sub>18</sub> || 18 || 18 || 5
! 85
| C<sub>4</sub>×C<sub>16</sub> || 64 || 16 || 2, 3
|-
! 24 
| C<sub>2</sub>×C<sub>2</sub>×C<sub>2</sub>  || 8 || 2 || 5, 7, 13
! 55 
| C<sub>2</sub>×C<sub>20</sub> || 40 || 20 || 21, 2
! 86
| C<sub>42</sub> || 42 || 42 || 3
|-
! 25 
| C<sub>20</sub> || 20 || 20 || 2
! 56 
| C<sub>2</sub>×C<sub>2</sub>×C<sub>6</sub> || 24 || 6 || 13, 29, 3
! 87
| C<sub>2</sub>×C<sub>28</sub> || 56 || 28 || 2, 86
|-
! 26 
| C<sub>12</sub> || 12 || 12 || 7
! 57 
| C<sub>2</sub>×C<sub>18</sub> || 36 || 18 || 20, 2
! 88
| C<sub>2</sub>×C<sub>2</sub>×C<sub>10</sub> || 40 || 10 || 3, 5, 7
|-
! 27 
| C<sub>18</sub> || 18 || 18 || 2
! 58 
| C<sub>28</sub> || 28 || 28 || 3
! 89
| C<sub>88</sub> || 88 || 88 || 3
|-
! 28 
| C<sub>2</sub>×C<sub>6</sub> || 12 || 6 || 13, 3
! 59 
| C<sub>58</sub> || 58 || 58 || 2
! 90
| C<sub>2</sub>×C<sub>12</sub> || 24 || 12 || 7, 11
|-
! 29 
| C<sub>28</sub> || 28 || 28 || 2
! 60 
| C<sub>2</sub>×C<sub>2</sub>×C<sub>4</sub> || 16 || 4 || 11, 19, 7
! 91
| C<sub>6</sub>×C<sub>12</sub> || 72 || 12 || 2, 3
|-
! 30 
| C<sub>2</sub>×C<sub>4</sub>  || 8 || 4 || 11, 7
! 61 
| C<sub>60</sub> || 60 || 60 || 2
! 92
| C<sub>2</sub>×C<sub>22</sub> || 44 || 22 || 3, 91
|-
! 31 
| C<sub>30</sub> || 30 || 30 || 3
! 62 
| C<sub>30</sub> || 30 || 30 || 3
! 93
| C<sub>2</sub>×C<sub>30</sub> || 60 || 30 || 5, 11
|}

==参见==
[[Lenstra_椭圆曲线分解|Lenstra 椭圆曲线分解]]（[[:en:Lenstra_elliptic_curve_factorization|:en:Lenstra elliptic curve factorization]]，[[:en:Arjen_Lenstra|Lenstra]] 给出的基于椭圆曲线的整数因子分解算法）

== 注释 ==
{{reflist}}

== 参考文献 ==
<small>[[高斯|高斯]]的[[算术研究|算术研究]]（Disquisitiones Arithemeticae）由[[西塞罗|西塞罗]][[拉丁语|拉丁语]]翻译成英语和德语。德语版包含他所有数论的论文：所有关于二次互反律的证明，高斯和符号的确定，双二次互反律的研究以及未发表的笔记。</small>
* {{citation
  | last1 = Gauss  | first1 = Carl Friedrich
  | last2 = Clarke | first2 = Arthur A. (translator into English)  
  | title = Disquisitiones Arithemeticae (Second, corrected edition)
  | publisher = [[Springer|Springer]]
  | location = New York
  | date = 1986
  | isbn = 0387962549}}

* {{citation
  | last1 = Gauss  | first1 = Carl Friedrich
  | last2 = Maser | first2 = H. (translator into German)  
  | title = Untersuchungen uber hohere Arithmetik (Disquisitiones Arithemeticae & other papers on number theory) (Second edition)
  | publisher = Chelsea
  | location = New York
  | date = 1965
  | isbn = 0-8284-0191-8}}

* {{citation
  | last1 = Riesel  | first1 = Hans
  | title = Prime Numbers and Computer Methods for Factorization (second edition)
  | publisher = Birkhäuser
  | location = Boston
  | date = 1994
  | isbn = 0-8176-3743-5}}

== 外部链接 ==
* {{MathWorld|title=Modulo Multiplication Group|urlname=ModuloMultiplicationGroup}}

[[Category:同余|Category:同余]]
[[Category:群论|Category:群论]]
[[Category:有限群|Category:有限群]]