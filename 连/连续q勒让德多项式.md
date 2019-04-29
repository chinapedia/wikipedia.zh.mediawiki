
'''连续勒让德多项式'''是一个以[[基本超几何函数|基本超几何函数]]定义的[[正交多项式|正交多项式]]<ref>Roelof Koekoek, Hypergeometric Orthogonal Polynomials and its q-Analogues, p475,Springer,2010</ref>


<math>P_n(x|q)=\;_{4}\phi_3\left(\begin{matrix} 
q^{-n} & q^{n+1} & q^{1/4}e^{i\theta}  & a^{1/4}e^{-i\theta} & \\ 
q & -q^{1/2} &-q  \end{matrix} 
; q,q \right)</math>
==极限关系==
令[[连续q勒让德多项式|连续q勒让德多项式]] q->1 得[[勒让德多项式|勒让德多项式]]

<math> \lim_{q \to 1}P_{n}(x|q)=P_{n}(x)</math>

;验证5阶连续q勒让德多项式→勒让德多项式
<math> \lim_{q \to 1}P_{5}(x|q)=P_{5}(x)</math>

由定义，
<math> P_{5}(x|q)=1+ \left( 1-{q}^{-5} \right)  \left( 1-{q}^{-4} \right)  \left( 1-{q}^
{-3} \right)  \left( 1-{q}^{6} \right)  \left( 1-{q}^{7} \right) 
 \left( 1-{q}^{8} \right)  \left( 1-\sqrt [4]{q} \left( x+i\sqrt {1-{x
}^{2}} \right)  \right)  \left( 1-{q}^{5/4} \left( x+i\sqrt {1-{x}^{2}
} \right)  \right)  \left( 1-{q}^{9/4} \left( x+i\sqrt {1-{x}^{2}}
 \right)  \right)  \left( 1-{\frac {\sqrt [4]{q}}{x+i\sqrt {1-{x}^{2}}
}} \right)  \left( 1-{\frac {{q}^{5/4}}{x+i\sqrt {1-{x}^{2}}}}
 \right)  \left( 1-{\frac {{q}^{9/4}}{x+i\sqrt {1-{x}^{2}}}} \right) {
q}^{3} \left( 1-q \right) ^{-2} \left( 1-{q}^{2} \right) ^{-2} \left( 
1-{q}^{3} \right) ^{-2} \left( 1+\sqrt {q} \right) ^{-1} \left( 1+{q}^
{3/2} \right) ^{-1} \left( 1+{q}^{5/2} \right) ^{-1} \left( 1+q
 \right) ^{-1} \left( 1+{q}^{2} \right) ^{-1} \left( 1+{q}^{3}
 \right) ^{-1}+ \left( 1-{q}^{-5} \right)  \left( 1-{q}^{-4} \right) 
 \left( 1-{q}^{-3} \right)  \left( 1-{q}^{-2} \right)  \left( 1-{q}^{6
} \right)  \left( 1-{q}^{7} \right)  \left( 1-{q}^{8} \right)  \left( 
1-{q}^{9} \right)  \left( 1-\sqrt [4]{q} \left( x+i\sqrt {1-{x}^{2}}
 \right)  \right)  \left( 1-{q}^{5/4} \left( x+i\sqrt {1-{x}^{2}}
 \right)  \right)  \left( 1-{q}^{9/4} \left( x+i\sqrt {1-{x}^{2}}
 \right)  \right)  \left( 1-{q}^{{\frac {13}{4}}} \left( x+i\sqrt {1-{
x}^{2}} \right)  \right)  \left( 1-{\frac {\sqrt [4]{q}}{x+i\sqrt {1-{
x}^{2}}}} \right)  \left( 1-{\frac {{q}^{5/4}}{x+i\sqrt {1-{x}^{2}}}}
 \right)  \left( 1-{\frac {{q}^{9/4}}{x+i\sqrt {1-{x}^{2}}}} \right) 
 \left( 1-{q}^{{\frac {13}{4}}} \left( x+i\sqrt {1-{x}^{2}} \right) ^{
-1} \right) {q}^{4} \left( 1-q \right) ^{-2} \left( 1-{q}^{2} \right) 
^{-2} \left( 1-{q}^{3} \right) ^{-2} \left( 1-{q}^{4} \right) ^{-2}
 \left( 1+\sqrt {q} \right) ^{-1} \left( 1+{q}^{3/2} \right) ^{-1}
 \left( 1+{q}^{5/2} \right) ^{-1} \left( 1+{q}^{7/2} \right) ^{-1}
 \left( 1+q \right) ^{-1} \left( 1+{q}^{2} \right) ^{-1} \left( 1+{q}^
{3} \right) ^{-1} \left( 1+{q}^{4} \right) ^{-1}+ \left( 1-{q}^{-5}
 \right)  \left( 1-{q}^{-4} \right)  \left( 1-{q}^{-3} \right) 
 \left( 1-{q}^{-2} \right)  \left( 1-{q}^{-1} \right)  \left( 1-{q}^{6
} \right)  \left( 1-{q}^{7} \right)  \left( 1-{q}^{8} \right)  \left( 
1-{q}^{9} \right)  \left( 1-{q}^{10} \right)  \left( 1-\sqrt [4]{q}
 \left( x+i\sqrt {1-{x}^{2}} \right)  \right)  \left( 1-{q}^{5/4}
 \left( x+i\sqrt {1-{x}^{2}} \right)  \right)  \left( 1-{q}^{9/4}
 \left( x+i\sqrt {1-{x}^{2}} \right)  \right)  \left( 1-{q}^{{\frac {
13}{4}}} \left( x+i\sqrt {1-{x}^{2}} \right)  \right)  \left( 1-{q}^{{
\frac {17}{4}}} \left( x+i\sqrt {1-{x}^{2}} \right)  \right)  \left( 1
-{\frac {\sqrt [4]{q}}{x+i\sqrt {1-{x}^{2}}}} \right)  \left( 1-{
\frac {{q}^{5/4}}{x+i\sqrt {1-{x}^{2}}}} \right)  \left( 1-{\frac {{q}
^{9/4}}{x+i\sqrt {1-{x}^{2}}}} \right)  \left( 1-{q}^{{\frac {13}{4}}}
 \left( x+i\sqrt {1-{x}^{2}} \right) ^{-1} \right)  \left( 1-{q}^{{
\frac {17}{4}}} \left( x+i\sqrt {1-{x}^{2}} \right) ^{-1} \right) {q}^
{5} \left( 1-q \right) ^{-2} \left( 1-{q}^{2} \right) ^{-2} \left( 1-{
q}^{3} \right) ^{-2} \left( 1-{q}^{4} \right) ^{-2} \left( 1-{q}^{5}
 \right) ^{-2} \left( 1+\sqrt {q} \right) ^{-1} \left( 1+{q}^{3/2}
 \right) ^{-1} \left( 1+{q}^{5/2} \right) ^{-1} \left( 1+{q}^{7/2}
 \right) ^{-1} \left( 1+{q}^{9/2} \right) ^{-1} \left( 1+q \right) ^{-
1} \left( 1+{q}^{2} \right) ^{-1} \left( 1+{q}^{3} \right) ^{-1}
 \left( 1+{q}^{4} \right) ^{-1} \left( 1+{q}^{5} \right) ^{-1}-{\frac 
{{q}^{5/4}}{ \left( 1-q \right) ^{2} \left( 1+\sqrt {q} \right) 
 \left( 1+q \right)  \left( x+i\sqrt {1-{x}^{2}} \right) }}-{\frac {{q
}^{5/4} \left( x+i\sqrt {1-{x}^{2}} \right) }{ \left( 1-q \right) ^{2}
 \left( 1+\sqrt {q} \right)  \left( 1+q \right) }}+{q}^{{\frac {29}{4}
}} \left( 1-q \right) ^{-2} \left( 1+\sqrt {q} \right) ^{-1} \left( 1+
q \right) ^{-1} \left( x+i\sqrt {1-{x}^{2}} \right) ^{-1}+{q}^{{\frac 
{29}{4}}} \left( x+i\sqrt {1-{x}^{2}} \right)  \left( 1-q \right) ^{-2
} \left( 1+\sqrt {q} \right) ^{-1} \left( 1+q \right) ^{-1}+{q}^{-{
\frac {15}{4}}} \left( 1-q \right) ^{-2} \left( 1+\sqrt {q} \right) ^{
-1} \left( 1+q \right) ^{-1} \left( x+i\sqrt {1-{x}^{2}} \right) ^{-1}
+ \left( x+i\sqrt {1-{x}^{2}} \right) {q}^{-{\frac {15}{4}}} \left( 1-
q \right) ^{-2} \left( 1+\sqrt {q} \right) ^{-1} \left( 1+q \right) ^{
-1}-{\frac {{q}^{9/4}}{ \left( 1-q \right) ^{2} \left( 1+\sqrt {q}
 \right)  \left( 1+q \right)  \left( x+i\sqrt {1-{x}^{2}} \right) }}-{
\frac {{q}^{9/4} \left( x+i\sqrt {1-{x}^{2}} \right) }{ \left( 1-q
 \right) ^{2} \left( 1+\sqrt {q} \right)  \left( 1+q \right) }}+
 \left( 1-{q}^{-5} \right)  \left( 1-{q}^{-4} \right)  \left( 1-{q}^{6
} \right)  \left( 1-{q}^{7} \right)  \left( 1-\sqrt [4]{q} \left( x+i
\sqrt {1-{x}^{2}} \right)  \right)  \left( 1-{q}^{5/4} \left( x+i
\sqrt {1-{x}^{2}} \right)  \right)  \left( 1-{\frac {\sqrt [4]{q}}{x+i
\sqrt {1-{x}^{2}}}} \right)  \left( 1-{\frac {{q}^{5/4}}{x+i\sqrt {1-{
x}^{2}}}} \right) {q}^{2} \left( 1-q \right) ^{-2} \left( 1-{q}^{2}
 \right) ^{-2} \left( 1+\sqrt {q} \right) ^{-1} \left( 1+{q}^{3/2}
 \right) ^{-1} \left( 1+q \right) ^{-1} \left( 1+{q}^{2} \right) ^{-1}
+{\frac {q}{ \left( 1-q \right) ^{2} \left( 1+\sqrt {q} \right) 
 \left( 1+q \right) }}+{\frac {{q}^{3/2}}{ \left( 1-q \right) ^{2}
 \left( 1+\sqrt {q} \right)  \left( 1+q \right) }}-{\frac {{q}^{7}}{
 \left( 1-q \right) ^{2} \left( 1+\sqrt {q} \right)  \left( 1+q
 \right) }}-{\frac {{q}^{15/2}}{ \left( 1-q \right) ^{2} \left( 1+
\sqrt {q} \right)  \left( 1+q \right) }}-{\frac {1}{{q}^{4} \left( 1-q
 \right) ^{2} \left( 1+\sqrt {q} \right)  \left( 1+q \right) }}-{
\frac {1}{{q}^{7/2} \left( 1-q \right) ^{2} \left( 1+\sqrt {q}
 \right)  \left( 1+q \right) }}+{\frac {{q}^{2}}{ \left( 1-q \right) ^
{2} \left( 1+\sqrt {q} \right)  \left( 1+q \right) }}+{\frac {{q}^{5/2
}}{ \left( 1-q \right) ^{2} \left( 1+\sqrt {q} \right)  \left( 1+q
 \right) }}\cdots</math>

求 q→1 的极限值：
<math> \lim_{q \to 1}P_{5}(x|q)={\frac {63}{8}}\,{x}^{5}-{\frac {35}{4}}\,{x}^{3}+{\frac {15}{8}}\,x</math>

而5阶勒让德多项式为：
<math>P_5(x)={\frac {63}{8}}\,{x}^{5}-{\frac {35}{4}}\,{x}^{3}+{\frac {15}{8}}\,x</math>

两者显然相等，所以
<math> \lim_{q \to 1}P_{5}(x|q)=P_{5}(x)</math>

验证毕

==图集==
{|
|[[File:CONTINUOUS_Q-LEGENDER_POLYNOMIALS_ABS_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|[[File:CONTINUOUS_Q-LEGENDER_POLYNOMIALS_IM_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|[[File:CONTINUOUS_Q-LEGENDER_POLYNOMIALS_RE_COMPLEX_3D_MAPLE_PLOT.gif|thumb]]
|}
{|
|[[File:CONTINUOUS_Q-LEGENDER_POLYNOMIALS_ABS_DENSITY_MAPLE_PLOT.gif|thumb]]
|[[File:CONTINUOUS_Q-LEGENDER_POLYNOMIALS_IM_DENSITY_MAPLE_PLOT.gif|thumb]]
|[[File:CONTINUOUS_Q-LEGENDER_POLYNOMIALS_RE_DENSITY_MAPLE_PLOT.gif|thumb]]
|}


==参考文献==
<references/>

[[Category:正交多项式|Category:正交多项式]]
[[Category:特殊函数|Category:特殊函数]]
[[Category:Q-模拟|Category:Q-模拟]]
{{q超几何函数}}