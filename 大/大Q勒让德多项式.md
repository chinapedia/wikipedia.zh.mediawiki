'''大q-勒让德多项式'''是一个以[[基本超几何函数|基本超几何函数]]定义的正交多项式<ref name=r>Roelof p443</ref>：
[[File:BIG_Q-LEGENDER_2D_PLOT.gif|thumb]]
:<math>\displaystyle   P_n(x;c;q)={}_3\phi_2(q^{-n},q^{n+1},x;q,cq;q,q) </math>

==正交性==
大q-勒让德多项式满足下列正交关系

<math>\int_{cq}^{q}P_m(x;c;q)P_n(x;c;q)d_{q}x=q(1-c)\frac{1-q}{1-q^{2n+1}}\frac{(c^{-1}q;q)_n}{(cq;q)_n}(-cq^2)^{n}q^{n \choose 2}\delta_{mn}</math>

==极限关系==
;大Q勒让德多项式→[[勒让德多项式|勒让德多项式]]

:<math>\displaystyle\lim_{q \to 1} P_n(x;0;q)=P_n(2x-1)</math>


令大q勒让德项式中的<math>c=0</math>,并且q→1 即得勒让德多项式

;验证

将c=0代人7阶(n=7)大q勒让德多项式得：

<math>qL=P_n(x;0;q)=1+{\frac {q}{ \left( 1-q \right) ^{2}}}-{\frac {qx}{ \left( 1-q
 \right) ^{2}}}-{\frac {{q}^{9}}{ \left( 1-q \right) ^{2}}}+{\frac {x{
q}^{9}}{ \left( 1-q \right) ^{2}}}-{\frac {1}{{q}^{6} \left( 1-q
 \right) ^{2}}}+{\frac {x}{{q}^{6} \left( 1-q \right) ^{2}}}+{\frac {{
q}^{2}}{ \left( 1-q \right) ^{2}}}-{\frac {x{q}^{2}}{ \left( 1-q
 \right) ^{2}}}+ \left( 1-{q}^{-7} \right)  \left( 1-{q}^{-6} \right) 
 \left( 1-{q}^{8} \right)  \left( 1-{q}^{9} \right)  \left( 1-x
 \right)  \left( 1-qx \right) {q}^{2} \left( 1-q \right) ^{-2} \left( 
1-{q}^{2} \right) ^{-2}+ \left( 1-{q}^{-7} \right)  \left( 1-{q}^{-6}
 \right)  \left( 1-{q}^{-5} \right)  \left( 1-{q}^{8} \right)  \left( 
1-{q}^{9} \right)  \left( 1-{q}^{10} \right)  \left( 1-x \right) 
 \left( 1-qx \right)  \left( 1-x{q}^{2} \right) {q}^{3} \left( 1-q
 \right) ^{-2} \left( 1-{q}^{2} \right) ^{-2} \left( 1-{q}^{3}
 \right) ^{-2}+ \left( 1-{q}^{-7} \right)  \left( 1-{q}^{-6} \right) 
 \left( 1-{q}^{-5} \right)  \left( 1-{q}^{-4} \right)  \left( 1-{q}^{8
} \right)  \left( 1-{q}^{9} \right)  \left( 1-{q}^{10} \right) 
 \left( 1-{q}^{11} \right)  \left( 1-x \right)  \left( 1-qx \right) 
 \left( 1-x{q}^{2} \right)  \left( 1-x{q}^{3} \right) {q}^{4} \left( 1
-q \right) ^{-2} \left( 1-{q}^{2} \right) ^{-2} \left( 1-{q}^{3}
 \right) ^{-2} \left( 1-{q}^{4} \right) ^{-2}+ \left( 1-{q}^{-7}
 \right)  \left( 1-{q}^{-6} \right)  \left( 1-{q}^{-5} \right) 
 \left( 1-{q}^{-4} \right)  \left( 1-{q}^{-3} \right)  \left( 1-{q}^{8
} \right)  \left( 1-{q}^{9} \right)  \left( 1-{q}^{10} \right) 
 \left( 1-{q}^{11} \right)  \left( 1-{q}^{12} \right)  \left( 1-x
 \right)  \left( 1-qx \right)  \left( 1-x{q}^{2} \right)  \left( 1-x{q
}^{3} \right)  \left( 1-x{q}^{4} \right) {q}^{5} \left( 1-q \right) ^{
-2} \left( 1-{q}^{2} \right) ^{-2} \left( 1-{q}^{3} \right) ^{-2}
 \left( 1-{q}^{4} \right) ^{-2} \left( 1-{q}^{5} \right) ^{-2}+
 \left( 1-{q}^{-7} \right)  \left( 1-{q}^{-6} \right)  \left( 1-{q}^{-
5} \right)  \left( 1-{q}^{-4} \right)  \left( 1-{q}^{-3} \right) 
 \left( 1-{q}^{-2} \right)  \left( 1-{q}^{8} \right)  \left( 1-{q}^{9}
 \right)  \left( 1-{q}^{10} \right)  \left( 1-{q}^{11} \right) 
 \left( 1-{q}^{12} \right)  \left( 1-{q}^{13} \right)  \left( 1-x
 \right)  \left( 1-qx \right)  \left( 1-x{q}^{2} \right)  \left( 1-x{q
}^{3} \right)  \left( 1-x{q}^{4} \right)  \left( 1-x{q}^{5} \right) {q
}^{6} \left( 1-q \right) ^{-2} \left( 1-{q}^{2} \right) ^{-2} \left( 1
-{q}^{3} \right) ^{-2} \left( 1-{q}^{4} \right) ^{-2} \left( 1-{q}^{5}
 \right) ^{-2} \left( 1-{q}^{6} \right) ^{-2}+ \left( 1-{q}^{-7}
 \right)  \left( 1-{q}^{-6} \right)  \left( 1-{q}^{-5} \right) 
 \left( 1-{q}^{-4} \right)  \left( 1-{q}^{-3} \right)  \left( 1-{q}^{-
2} \right)  \left( 1-{q}^{-1} \right)  \left( 1-{q}^{8} \right) 
 \left( 1-{q}^{9} \right)  \left( 1-{q}^{10} \right)  \left( 1-{q}^{11
} \right)  \left( 1-{q}^{12} \right)  \left( 1-{q}^{13} \right) 
 \left( 1-{q}^{14} \right)  \left( 1-x \right)  \left( 1-qx \right) 
 \left( 1-x{q}^{2} \right)  \left( 1-x{q}^{3} \right)  \left( 1-x{q}^{
4} \right)  \left( 1-x{q}^{5} \right)  \left( 1-x{q}^{6} \right) {q}^{
7} \left( 1-q \right) ^{-2} \left( 1-{q}^{2} \right) ^{-2} \left( 1-{q
}^{3} \right) ^{-2} \left( 1-{q}^{4} \right) ^{-2} \left( 1-{q}^{5}
 \right) ^{-2} \left( 1-{q}^{6} \right) ^{-2} \left( 1-{q}^{7}
 \right) ^{-2}</math>

*<math>qL2=\lim_{q \to 1}qL=-1+56\,x+3432\,{x}^{7}-12012\,{x}^{6}+16632\,{x}^{5}-11550\,{x}^{4}+
4200\,{x}^{3}-756\,{x}^{2}</math>

另7阶勒让德多项式：
*<math>P_7(2x-1)=-1+56\,x+3432\,{x}^{7}-12012\,{x}^{6}+16632\,{x}^{5}-11550\,{x}^{4}+
4200\,{x}^{3}-756\,{x}^{2}</math>

显然qL2=P_7(2x-1)   QED.

==图集==
下列复数域三阶大q勒让德多项式:<math>\displaystyle   P_n3(x+iy;-1.5;q) </math>的

一组三个虚数部、实数部与绝对值的复数三维动画图，以q为可变参数

一组三个虚数部、实数部与绝对值的复数密度动画图

{|
|[[File:BIG_Q-LEGENDER_ABS_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|[[File:BIG_Q-LEGENDER_IM_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|[[File:BIG_Q-LEGENDER_RE_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|}
{|
|[[File:BIG_Q-LEGENDER_ABS_DENSITY_MAPLE_PLOT.gif|thumb]]
|[[File:BIG_Q-LEGENDER_IM_DENSITY_MAPLE_PLOT.gif|thumb]]
|[[File:BIG_Q-LEGENDER_RE_DENSITY_MAPLE_PLOT.gif|thumb]]
|}

==参考文献==
*{{Citation | last1=Andrews | first1=George E. |authorlink1=George Andrews (mathematician)| last2=Askey | first2=Richard |authorlink2=Richard Askey | editor1-last=Brezinski | editor1-first=C. | editor2-last=Draux | editor2-first=A. | editor3-last=Magnus | editor3-first=Alphonse P. | editor4-last=Maroni | editor4-first=Pascal | editor5-last=Ronveaux | editor5-first=A. | title=Polynômes orthogonaux et applications.  Proceedings of the Laguerre symposium held at Bar-le-Duc, October 15–18, 1984.  | publisher=[[Springer-Verlag|Springer-Verlag]] | location=Berlin, New York | series=Lecture Notes in Math. | isbn=978-3-540-16059-5  | mr=838970 | year=1985 | volume=1171 | chapter=Classical orthogonal polynomials | doi=10.1007/BFb0076530 | pages=36–62}}
*{{Citation | last1=Gasper | first1=George | last2=Rahman | first2=Mizan | title=Basic hypergeometric series | publisher=[[Cambridge_University_Press|Cambridge University Press]] | edition=2nd | series=Encyclopedia of Mathematics and its Applications | isbn=978-0-521-83357-8 | doi=10.2277/0521833574 | mr=2128719 | year=2004 | volume=96}}
*{{Citation | last1=Koekoek | first1=Roelof | last2=Lesky | first2=Peter A. | last3=Swarttouw | first3=René F. | title=Hypergeometric orthogonal polynomials and their q-analogues | publisher=[[Springer-Verlag|Springer-Verlag]] | location=Berlin, New York | series=Springer Monographs in Mathematics | isbn=978-3-642-05013-8 | doi=10.1007/978-3-642-05014-5 | mr=2656096 | year=2010}}
*{{dlmf|id=18|title=|first=Tom H. |last=Koornwinder|first2=Roderick S. C.|last2= Wong|first3=Roelof |last3=Koekoek||first4=René F. |last4=Swarttouw}}
{{q超几何函数}}