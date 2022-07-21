[[File:Continuous_q_Laguerre_polynomials.gif|thumb]]
'''连续q拉盖尔多项式'''(Continuous q-Laguerre polynomials)是一个以[[基本超几何函数|基本超几何函数]]定义的[[正交多项式|正交多项式]]<ref>Roelof Koekoek, Peter Lesky, Rene Swarttouw,Hypergeometric Orthogonal Polynomials and Their q-Analogues, p514, Springer</ref>。

<math>P_{n}^{(\alpha)}(x|q)=\frac{(q^\alpha+1;q)_{n}}{(q;q)_{n}}</math><math>_{3}\Phi_{2}(q^{-n},q^{\alpha/2+1/4}e^{i\theta},q^{\alpha/2+1/4}*e^{-i\theta};q^{\alpha+1},0|q,q)</math>
==极限关系==
[[Q梅西纳-帕拉泽克多项式|Q梅西纳-帕拉泽克多项式]]→[[连续q拉盖尔多项式|连续q拉盖尔多项式]]

<math>P_{n}(cos(\theta+\phi);q^{\alpha/2+1/2}|q)=</math><math>q^{(-\alpha/2-1/4)*n}*P_{n}^(\alpha)(cos\theta|q)</math>

[[阿拉-萨拉姆-迟哈剌多项式|阿拉-萨拉姆-迟哈剌多项式]]→连续q拉盖尔多项式

令连续q拉盖尔多项式中<math>x=q^x</math>,q→1,即得[[拉盖尔多项式|拉盖尔多项式]]

;验证
3阶连续q拉盖尔多项式：
<math>\lim_{q  \to  1}P_{3}^(a)=1/6\,{a}^{3}-x{a}^{2}+{a}^{2}+{\frac {11}{6}}\,a+2\,a{x}^{2}-5\,ax+1-6
\,x-4/3\,{x}^{3}+6\,{x}^{2}</math>

3阶广义拉盖尔多项式：

<math>L_3^{a}(2x)=\frac{1}{6}(a+1)_{3}*_1F_1(-n,a+1;2x)</math>
<math>=1/6\,{a}^{3}-x{a}^{2}+{a}^{2}+{\frac {11}{6}}\,a+2\,a{x}^{2}-5\,ax+1-6
\,x-4/3\,{x}^{3}+6\,{x}^{2}
</math>

两者显然相等。

==图集==
{|
|[[File:CONTINUOUS_Q_LAGUERRE_ABS_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|[[File:CONTINUOUS_Q_LAGUERRE_IM_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|[[File:CONTINUOUS_Q_LAGUERRE_RE_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|}
{|
|[[File:CONTINUOUS_Q_LAGUERRE_ABS_DENSITY_MAPLE_PLOT.gif|thumb]]
|[[File:CONTINUOUS_Q_LAGUERRE_IM_DENSITY_MAPLE_PLOT.gif|thumb]]
|[[File:CONTINUOUS_Q_LAGUERRE_RE_DENSITY_MAPLE_PLOT.gif|thumb]]
|}
|
|}

==参考文献==

*{{Citation | last1=Gasper | first1=George | last2=Rahman | first2=Mizan | title=Basic hypergeometric series | publisher=[[Cambridge_University_Press|Cambridge University Press]] | edition=2nd | series=Encyclopedia of Mathematics and its Applications | isbn=978-0-521-83357-8 | doi=10.2277/0521833574 | mr=2128719 | year=2004 | volume=96}}
*{{Citation | last1=Koekoek | first1=Roelof | last2=Lesky | first2=Peter A. | last3=Swarttouw | first3=René F. | title=Hypergeometric orthogonal polynomials and their q-analogues | publisher=[[Springer-Verlag|Springer-Verlag]] | location=Berlin, New York | series=Springer Monographs in Mathematics | isbn=978-3-642-05013-8 | doi=10.1007/978-3-642-05014-5 | mr=2656096 | year=2010}}
*{{dlmf|id=18|title=|first=Tom H. |last=Koornwinder|first2=Roderick S. C.|last2= Wong|first3=Roelof |last3=Koekoek||first4=René F. |last4=Swarttouw}}

[[Category:正交多项式|Category:正交多项式]]

[[Category:特殊超几何函数|Category:特殊超几何函数]]
{{q超几何函数}}