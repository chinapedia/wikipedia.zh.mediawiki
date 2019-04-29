''' 广义耦合KdV方程组'''(Generalized coupled KdV equations)是一个三元非线性偏微分方程组：<ref name=yan>阎振亚 第33 页</ref>

<math>  U_{t}-0.25*U_{xxx}-3*U*U_{x}-3*(W-V^2)_{x}=0,  </math>

<math>  V_{t}+0.5*V_{xxx}+3*U*V_{x}=0,  </math>

<math> W_{t}+0.5*W_{xxx}+3*U*W_{x}=0    </math>

==解析解==
:<math> u(x, t) = -.33333333333333333333*_C4/_C3+.50000000000000000000*_C3^2*JacobiCN(_C2+_C3*x+_C4*t, .70710678118654752440)^2</math> <math> v(x, t) = -5.000000000*10^9*_C8/\sqrt(-3.3333333333333333333*10^19*_C4*_C3)-1.0000000000000000000*10^(-10)*\sqrt(-3.3333333333333333333*10^19*_C4*_C3)*JacobiCN(_C2+_C3*x+_C4*t, .70710678118654752440),</math><math> w(x, t) = _C7+_C8*JacobiCN(_C2+_C3*x+_C4*t, .70710678118654752440)  </math>
:<math> u(x, t) = -.33333333333333333333*_C4/_C3+.50000000000000000000*_C3^2*JacobiCN(_C2+_C3*x+_C4*t, .70710678118654752440)^2, </math> <math> v(x, t) = 5.000000000*10^9*_C8/\sqrt(-3.3333333333333333333*10^19*_C4*_C3)+1.0000000000000000000*10^(-10)*\sqrt(-3.3333333333333333333*10^19*_C4*_C3)*JacobiCN(_C2+_C3*x+_C4*t, .70710678118654752440), </math> <math> w(x, t) = _C7+_C8*JacobiCN(_C2+_C3*x+_C4*t, .70710678118654752440)  </math>
:<math> u(x, t) = -.33333333333333333333*_C5/_C4-2.*_C4^2*WeierstrassP(_C3+_C4*x+_C5*t, 0., _C1), </math> <math> v(x, t) = -(.16666666666666666667*(4.*_C5*_C4+3.*_C7))/_C4^2-1.*_C4^2*WeierstrassP(_C3+_C4*x+_C5*t, 0., _C1),</math> <math>  w(x, t) = _C6+_C7*WeierstrassP(_C3+_C4*x+_C5*t, 0., _C1)  </math>
:<math> u(x, t) = -(.33333333333333333333*(_C3+_C2^3))/_C2-1.*_C2^2*tan(_C1+_C2*x+_C3*t)^2, </math> <math> v(x, t) = -5.000000000*10^9*_C5/\sqrt(-3.3333333333333333333*10^19*_C2^4+6.6666666666666666667*10^19*_C3*_C2)-1.0000000000000000000*10^(-10)*\sqrt(-3.3333333333333333333*10^19*_C2^4+6.6666666666666666667*10^19*_C3*_C2)*tan(_C1+_C2*x+_C3*t),</math> <math>  w(x, t) = _C4+_C5*tan(_C1+_C2*x+_C3*t)  </math>
:<math> u(x, t) = (.33333333333333333333*(-1.*_C3+_C2^3))/_C2-1.*_C2^2*coth(_C1+_C2*x+_C3*t)^2,</math> <math>  v(x, t) = 5.000000000*10^9*_C5/\sqrt(3.3333333333333333333*10^19*_C2^4+6.6666666666666666667*10^19*_C3*_C2)+1.0000000000000000000*10^(-10)*\sqrt(3.3333333333333333333*10^19*_C2^4+6.6666666666666666667*10^19*_C3*_C2)*coth(_C1+_C2*x+_C3*t), </math> <math> w(x, t) = _C4+_C5*coth(_C1+_C2*x+_C3*t)  </math>
:<math> u(x, t) = (.33333333333333333333*(-1.*_C3+_C2^3))/_C2-1.*_C2^2*tanh(_C1+_C2*x+_C3*t)^2,</math> <math>  v(x, t) = 5.000000000*10^9*_C5/\sqrt(3.3333333333333333333*10^19*_C2^4+6.6666666666666666667*10^19*_C3*_C2)+1.0000000000000000000*10^(-10)*\sqrt(3.3333333333333333333*10^19*_C2^4+6.6666666666666666667*10^19*_C3*_C2)*tanh(_C1+_C2*x+_C3*t),</math> <math>  w(x, t) = _C4+_C5*tanh(_C1+_C2*x+_C3*t)  </math>
:<math> u(x, t) = (.16666666666666666667*(-2.*_C4-2.*_C3^3+_C3^3*_C1^2))/_C3+_C3^2*JacobiDN(_C2+_C3*x+_C4*t, _C1)^2,</math> <math>  v(x, t) = 5.000000000*10^9*_C6/\sqrt(3.3333333333333333333*10^19*_C3^4-1.6666666666666666667*10^19*_C3^4*_C1^2-6.6666666666666666667*10^19*_C4*_C3)+1.0000000000000000000*10^(-10)*\sqrt(3.3333333333333333333*10^19*_C3^4-1.6666666666666666667*10^19*_C3^4*_C1^2-6.6666666666666666667*10^19*_C4*_C3)*JacobiDN(_C2+_C3*x+_C4*t, _C1),</math> <math>  w(x, t) = _C5+_C6*JacobiDN(_C2+_C3*x+_C4*t, _C1)  </math>
:<math>   </math>

==行波图==
{|
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_1.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_2.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_3.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_4.gif|thumb]]
|}
{|
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_5.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_6.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_7.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_8.gif|thumb]]
|}
{|
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_9.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_10.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_11.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_12.gif|thumb]]
|}
{|
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_13.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_14.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_15.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_16.gif|thumb]]
|}
{|
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_17.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_18.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_19.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_20.gif|thumb]]
|}
{|
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_21.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_22.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_23.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_24.gif|thumb]]
|}
{|
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_25.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_26.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_27.gif|thumb]]
|[[File:Generalized_coupled_KdV_equation_traveling_wave_plot_28.gif|thumb]]
|}

==参考文献==
<references/>
# *谷超豪 《[[孤立子|孤立子]]理论中的[[达布变换|达布变换]]及其几何应用》 上海科学技术出版社
# *阎振亚著 《复杂非线性波的构造性理论及其应用》 科学出版社 2007年
# 李志斌编著 《非线性数学物理方程的行波解》 科学出版社
#王东明著 《消去法及其应用》 科学出版社 2002
# *何青 王丽芬编著 《[[Maple|Maple]] 教程》 科学出版社 2010 ISBN 9787030177445
#Graham W. Griffiths William E.Shiesser Traveling Wave Analysis of Partial Differential p135 Equations Academy Press
# Richard H. Enns George C. McCGuire, Nonlinear Physics Birkhauser,1997
#Inna Shingareva, Carlos Lizárraga-Celaya,Solving Nonlinear Partial Differential Equations with Maple Springer.
#Eryk Infeld and George Rowlands,Nonlinear Waves,Solitons and Chaos,Cambridge 2000
#Saber Elaydi,An Introduction to Difference Equationns, Springer 2000
#Dongming Wang, Elimination Practice,Imperial College Press 2004
# David Betounes, Partial Differential Equations for Computational Science: With Maple and Vector Analysis Springer, 1998 ISBN 9780387983004
# George Articolo Partial Differential Equations & Boundary Value Problems with Maple V Academic Press 1998 ISBN 9780120644759

{{非线性偏微分方程}}
[[category:非线性偏微分方程|category:非线性偏微分方程]]