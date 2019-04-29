
'''大q-拉盖尔多项式'''是一个以[[基本超几何函数|基本超几何函数]]定义的[[正交多项式|正交多项式]]:

<math>P_n(x;a,b;q)=\frac{1}{(b^{-1}*q^{-n};q,n)}*_2\Phi_1(q^{-n},aqx^{-1};aq|q;\frac{x}{b})</math>

==极限关系==
;[[大q雅可比多项式|大q雅可比多项式]]→大q拉盖尔多项式
令大q雅可比多项式中的<math>b =0</math>,即得大q拉盖尔多项式

<math>P_{n}(x;a,0,c;q)=P_{n}(x;a,c;q)</math>

;大q拉盖尔多项式→[[小q拉盖尔多项式|小q拉盖尔多项式]]
在大q拉盖尔多项式中，令<math>x \to  bqx</math>,并令<math>b \to \infty</math>即得[[小q拉盖尔多项式|小q拉盖尔多项式]]
<math>\lim_{b \to \infty}P_{n}(bqx;a,b;q)=p_{n}(x;a|q)</math> 


;大→q拉盖尔多项式→[[阿尔-萨拉姆-卡里兹多项式_I|阿尔-萨拉姆-卡里兹多项式 I]]

==图集==
{|
|[[File:BIG_Q-LAGUERRE_POLYNOMIALS_ABS_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|[[File:BIG_Q-LAGUERRE_POLYNOMIALS_IM_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|[[File:BIG_Q-LAGUERRE_POLYNOMIALS_RE_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|}
{|
|[[File:BIG_Q-LAGUERRE_POLYNOMIALS_ABS_DENSITY_MAPLE_PLOT.gif|thumb]]
|[[File:BIG_Q-LAGUERRE_POLYNOMIALS_IM_DENSITY_MAPLE_PLOT.gif|thumb]]
|[[File:BIG_Q-LAGUERRE_POLYNOMIALS_RE_DENSITY_MAPLE_PLOT.gif|thumb]]
|}

==参考文献==
*{{Citation | last1=Gasper | first1=George | last2=Rahman | first2=Mizan | title=Basic hypergeometric series | publisher=[[Cambridge_University_Press|Cambridge University Press]] | edition=2nd | series=Encyclopedia of Mathematics and its Applications | isbn=978-0-521-83357-8 | doi=10.2277/0521833574 | mr=2128719 | year=2004 | volume=96}}
*{{Citation | last1=Koekoek | first1=Roelof | last2=Lesky | first2=Peter A. | last3=Swarttouw | first3=René F. | title=Hypergeometric orthogonal polynomials and their q-analogues | publisher=[[Springer-Verlag|Springer-Verlag]] | location=Berlin, New York | series=Springer Monographs in Mathematics | isbn=978-3-642-05013-8 | doi=10.1007/978-3-642-05014-5 | mr=2656096 | year=2010}}
*{{dlmf|id=18|title=|first=Tom H. |last=Koornwinder|first2=Roderick S. C.|last2= Wong|first3=Roelof |last3=Koekoek||first4=René F. |last4=Swarttouw}}

[[Category:正交多项式|Category:正交多项式]]
[[Category:基本超几何函数|Category:基本超几何函数]]
{{q超几何函数}}