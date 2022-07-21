'''连续q-哈恩多项式'''以[[基本超几何函数|基本超几何函数]]定义：<ref name=R>Roelof, p433</ref>
<math>p_n(x;a,b,c|q)=a^{-n}e^{-inu}(abe^{2iu},ac,ad;q)_n*_4\Phi_3(q^{-n},abcdq^{n-1},ae^{i{t+2u}},ae^{-it};abe^{2iu},ac,ad;q;q)</math>

并且

<math>x=cos(t+u)</math>

==极限关系==
[[连续q哈恩多项式|连续q哈恩多项式]]→[[Q梅西纳-帕拉泽克多项式|Q梅西纳-帕拉泽克多项式]]

<math>\frac{p_{n}(cos(\theta+\phi);a,0,0,a;q)}{(q;q)_{n}}=P_{n}(cos(\theta+\phi);a|q)</math>
;[[阿斯基-威尔逊多项式|阿斯基-威尔逊多项式]]→[[连续q哈恩多项式|连续q哈恩多项式]]
在阿斯基-威尔逊多项式中作代换<math>\theta  \to  \theta+\phi</math>,<math>a \to ae^{i\theta}</math>,<math>b \to be^{i\theta}</math>,<math>c \to ce^{-i\theta}</math>,<math>d \to de^{-i\theta}</math>即得连续q哈恩多项式：
<math>p_{n}(cos(\theta+\phi);ae^{i\theta},be^{i\theta},ce^{-i\theta},de^{-i\theta}|q)=p_{n}(cos(\theta+\phi),a,b,c,d;q)</math>
==图集==
{|
|[[File:CONTINUOUS_q_hahn_ABS_COMPLEX3D_Maple_PLOT.gif|thumb]]
|[[File:CONTINUOUS_q_hahn_IIM_COMPLEX3D_Maple_PLOT.gif|thumb]]
|[[File:CONTINUOUS_q_hahn_RE_COMPLEX3D_Maple_PLOT.gif|thumb]]
|}
{|
|[[File:CONTINUOUS_q_hahn_ABS_densitu_Maple_PLOT.gif|thumb]]
|[[File:CONTINUOUS_q_hahn_im_densitu_Maple_PLOT.gif|thumb]]
|[[File:CONTINUOUS_q_hahn_RE_densitu_Maple_PLOT.gif|thumb]]
|}


==参考文献==
*{{Citation | last1=Gasper | first1=George | last2=Rahman | first2=Mizan | title=Basic hypergeometric series | publisher=[[Cambridge_University_Press|Cambridge University Press]] | edition=2nd | series=Encyclopedia of Mathematics and its Applications | isbn=978-0-521-83357-8 | doi=10.2277/0521833574 | mr=2128719 | year=2004 | volume=96}}
*{{Citation | last1=Koekoek | first1=Roelof | last2=Lesky | first2=Peter A. | last3=Swarttouw | first3=René F. | title=Hypergeometric orthogonal polynomials and their q-analogues | publisher=[[Springer-Verlag|Springer-Verlag]] | location=Berlin, New York | series=Springer Monographs in Mathematics | isbn=978-3-642-05013-8 | doi=10.1007/978-3-642-05014-5 | mr=2656096 | year=2010}}
*{{dlmf|id=18|title=Chapter 18: Orthogonal Polynomials|first=Tom H. |last=Koornwinder|first2=Roderick S. C.|last2= Wong|first3=Roelof |last3=Koekoek||first4=René F. |last4=Swarttouw}}

[[Category:基本超幾何函數|Category:基本超幾何函數]]
[[Category:正交多项式|Category:正交多项式]]
{{q超几何函数}}