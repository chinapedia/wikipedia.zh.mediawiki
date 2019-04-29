'''耦合KdV方程组'''(Coupled KdV equation)是一个二元非线性偏微分方程组：<ref>李志斌编著 《非线性数学物理方程的行波解》 38页 科学出版社 2008</ref>

<math>u_{t}+6*\alpha*u*u_{x}-6*v*v_{x}+\alpha*u_{xxx}=0</math>

<math>v_{t}+3*\alpha*u*v_{x}+\alpha*v_{xxx}=0</math>

==解析解==
:<math>u(x, t) = (1/3)*(-_C3+\alpha*_C2^3)/(\alpha*_C2)-2*_C2^2*csc(_C1+_C2*x+_C3*t)^2, v(x, t) = -(1/3)*\sqrt(12*\alpha*_C2^4+6*_C2*_C3)*csc(_C1+_C2*x+_C3*t)</math>
:<math>u(x, t) = (1/3)*(-_C3+\alpha*_C2^3)/(\alpha*_C2)-2*_C2^2*sec(_C1+_C2*x+_C3*t)^2, v(x, t) = -(1/3)*\sqrt(12*\alpha*_C2^4+6*_C2*_C3)*sec(_C1+_C2*x+_C3*t)</math>
:<math>u(x, t) = (1/3)*(-_C3+2*\alpha*_C2^3)/(\alpha*_C2)-2*_C2^2*coth(_C1+_C2*x+_C3*t)^2, v(x, t) = -(1/3)*\sqrt(6*_C2*_C3+24*\alpha*_C2^4)*coth(_C1+_C2*x+_C3*t)</math>
:<math>u(x, t) = (1/3)*(-_C3+2*\alpha*_C2^3)/(alpha*_C2)-2*_C2^2*tanh(_C1+_C2*x+_C3*t)^2, v(x, t) = -(1/3)*\sqrt(6*_C2*_C3+24*alpha*_C2^4)*tanh(_C1+_C2*x+_C3*t)</math>
:<math>u(x, t) = -(1/3)*(_C3+\alpha*_C2^3)/(\alpha*_C2)-2*_C2^2*csch(_C1+_C2*x+_C3*t)^2, v(x, t) = -(1/3)*\sqrt(6*_C2*_C3-12*alpha*_C2^4)*csch(_C1+_C2*x+_C3*t)</math>
:<math>u(x, t) = -(1/3)*(_C3+8*\alpha*_C2^3)/(\alpha*_C2)-4*_C2^2*tan(_C1+_C2*x+_C3*t)^2, v(x, t) = -(1/6)*(_C3+8*\alpha*_C2^3)*\sqrt(2)/(_C2*\sqrt(\alpha))-2*\sqrt(2)*\sqrt(\alpha)*_C2^2*tan(_C1+_C2*x+_C3*t)^2</math>
:<math>u(x, t) = (1/3)*(-_C4+\alpha*_C3^3+\alpha*_C3^3*_C1^2)/(\alpha*_C3)-2*_C3^2*JacobiNS(_C2+_C3*x+_C4*t, _C1)^2, v(x, t) = -(1/3)*\sqrt(12*\alpha*_C3^4*_C1^2+12*\alpha*_C3^4+6*_C3*_C4)*JacobiNS(_C2+_C3*x+_C4*t, _C1)</math>
:<math>u(x, t) = (1/3)*(-_C4+\alpha*_C3^3+\alpha*_C3^3*_C1^2)/(\alpha*_C3)-2*_C3^2*_C1^2*JacobiSN(_C2+_C3*x+_C4*t, _C1)^2, v(x, t) = -(1/3)*\sqrt(12*\alpha*_C3^4*_C1^2+12*\alpha*_C3^4+6*_C3*_C4)*_C1*JacobiSN(_C2+_C3*x+_C4*t, _C1)</math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>

==行波图==
{|
|[[File:Coupled_KdV_equation_traveling_wave_plot_1.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_2.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_3.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_4.gif|thumb]]
|}
{|
|[[File:Coupled_KdV_equation_traveling_wave_plot_5.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_6.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_7.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_8.gif|thumb]]
|}
{|
|[[File:Coupled_KdV_equation_traveling_wave_plot_9.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_10.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_11.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_12.gif|thumb]]
|}
{|
|[[File:Coupled_KdV_equation_traveling_wave_plot_13.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_14.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_15.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_16.gif|thumb]]
|}
{|
|[[File:Coupled_KdV_equation_traveling_wave_plot_17.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_18.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_19.gif|thumb]]
|[[File:Coupled_KdV_equation_traveling_wave_plot_20.gif|thumb]]
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