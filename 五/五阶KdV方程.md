'''五阶KdV方程'''(Fifth order KdV equation)是一个非线性偏微分方程，简称[[fKdV方程|fKdV方程]]：<ref>Andrei D. Polyanin,Valentin F. Zaitsev, HANDBOOK OF NONLINEAR PARTIAL DIFFERENTIAL EQUATIONS, SECOND EDITION p1034 CRC PRESS</ref>
<math>u_{t}+\alpha*u^2*u_{x}+\beta*u_{x}*u_{xx}+\gamma*u*u_{xxx}+\delta*u_{xxxxx}=0</math>
==解析解==
:<math>u(x, t) = 6*_C3^2*(-(6*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma-\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))*\gamma^2/\alpha+(60*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma-\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))*\delta-72*\delta*\gamma^2+720*\delta^2*\alpha-120*\delta*\beta^2)*JacobiND(_C2+_C3*x-(6*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma-\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))*_C3^5*t/\alpha, \sqrt(2))^2/(\beta*(6*\beta^2-120*\delta*\alpha+12*\gamma^2+12*\beta*\gamma+6*\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))</math>
:<math>u(x, t) = 6*_C3^2*(-(6*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma-\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))*\gamma^2/\alpha+(60*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma-\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))*\delta-72*\delta*\gamma^2+720*\delta^2*\alpha-120*\delta*\beta^2)*JacobiNS(_C2+_C3*x-(6*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma-\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))*_C3^5*t/\alpha, I)^2/(\beta*(6*\beta^2-120*\delta*\alpha+12*\gamma^2+12*\beta*\gamma+6*\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))</math>
:<math>u(x, t) = -3*_C3^2*(-(3/2)*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma-\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2))*\gamma^2/\alpha+(15*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma-\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))*\delta-18*\delta*\gamma^2+180*\delta^2*\alpha-30*\delta*\beta^2)*JacobiCN(_C2+_C3*x-(3/2)*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma-\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2))*_C3^5*t/\alpha, (1/2)*\sqrt(2))^2/(\beta*((3/2)*\beta^2-30*\delta*\alpha+3*\gamma^2+3*\beta*\gamma+(3/2)*\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))</math>
:<math>u(x, t) = -6*_C3^2*(-(6*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma+\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))*\gamma^2/\alpha+(60*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma+\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))*\delta-72*\delta*\gamma^2+720*\delta^2*\alpha-120*\delta*\beta^2)*JacobiDN(_C2+_C3*x-(6*(-12*\delta*\alpha+\beta^2+2*\beta*\gamma+\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))*_C3^5*t/\alpha, \sqrt(2))^2/(\beta*(6*\beta^2-120*\delta*\alpha+12*\gamma^2+12*\beta*\gamma-6*\sqrt(-40*\delta*\alpha*\beta^2+\beta^4+4*\beta^3*\gamma+4*\beta^2*\gamma^2)))</math>
:<math>u(x, t) = _C5-(3*(-4*_C3^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\beta^2*_C5^2-8*_C3^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\gamma^2*_C5^2-(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\beta*_C5^3*\alpha-(3/2)*\gamma*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5^3*\alpha+(1/4)*\gamma*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5^3*\beta^2/\delta+(2/5)*\gamma^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5^3*\beta/\delta-\beta^2*_C5^4*\alpha+4800*_C3^6*\beta*\delta^2*_C5-160*_C3^4*\beta^2*_C5^2*\delta-800*\delta^2*\alpha*_C3^4*_C5^2+16*\gamma^2*_C5^3*\beta*_C3^2-320*\gamma^2*_C3^4*_C5^2*\delta+7200*\gamma*_C3^6*\delta^2*_C5+10*\gamma*\beta^2*_C5^3*_C3^2-3*\gamma*_C5^4*\beta*\alpha-48000*_C3^8*\delta^3+2*\beta^3*_C5^3*_C3^2+8*\gamma^3*_C5^3*_C3^2-2*\gamma^2*_C5^4*\alpha+10*_C5^4*\delta*\alpha^2+20*\gamma*_C5^3*\delta*\alpha*_C3^2-480*\gamma*_C3^4*_C5^2*\beta*\delta-12*\gamma*_C3^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5^2*\beta+40*_C3^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\delta*\alpha*_C5^2+120*_C3^4*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\delta*\gamma*_C5+120*_C3^4*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\delta*\beta*_C5-1200*_C3^6*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\delta^2+40*_C5^3*\delta*\alpha*\beta*_C3^2+(1/20)*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\beta^3*_C5^3/\delta+(1/5)*\gamma^3*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5^3/\delta))*JacobiSN(_C2+_C3*x+(1/25)*_C3*(3*_C3^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5*\beta*\gamma+45*_C3^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\delta*_C5*\alpha+(1/2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2)))*\alpha*_C5^2*\beta-150*_C3^4*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\delta*\beta-9*_C3^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\gamma^2*_C5-(9/4*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2)))*\gamma*\alpha*_C5^2+90*_C3^4*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\delta*\gamma+(1/20)*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5^2*\beta*\gamma^2/\delta-(1/20)*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5^2*\beta^2*\gamma/\delta+(3/10)*\gamma^3*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5^2/\delta+420*_C3^4*\delta*_C5*\beta*\gamma+3600*_C3^6*\delta^2*\gamma+300*_C3^4*\delta*_C5*\beta^2-6000*_C3^6*\delta^2*\beta+2*_C5^2*\beta*\gamma^2*_C3^2-2*_C5^2*\beta^2*\gamma*_C3^2+_C5^3*\beta*\gamma*\alpha-130*_C5^2*\delta*\alpha*\beta*_C3^2+15*_C5^3*\delta*\alpha^2+12*\gamma^3*_C5^2*_C3^2-3*\gamma^2*_C5^3*\alpha-360*_C3^4*\gamma^2*\delta*_C5)*t/(\delta*(-\alpha*_C5+2*\gamma*_C3^2+(1/20)*\gamma*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))/\delta)), (1/20)*\sqrt(10)*\sqrt((2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))/\delta)/_C3)^2/(60*_C3^4*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\delta*\beta-6*_C3^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\gamma^2*_C5+60*_C3^4*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\delta*\gamma-3*_C3^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5*\beta^2-(3/2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2)))*\gamma*\alpha*_C5^2-(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\alpha*_C5^2*\beta+(1/20)*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\beta^3*_C5^2/\delta-120*_C3^4*\delta*_C5*\beta^2+10*_C5^2*\beta^2*\gamma*_C3^2+16*_C5^2*\beta*\gamma^2*_C3^2-240*_C3^4*\gamma^2*\delta*_C5-3*_C5^3*\beta*\gamma*\alpha-\beta^2*_C5^3*\alpha+2400*_C3^6*\delta^2*\beta+2400*_C3^6*\delta^2*\gamma+10*_C5^3*\delta*\alpha^2+8*\gamma^3*_C5^2*_C3^2-2*\gamma^2*_C5^3*\alpha+2*\beta^3*_C5^2*_C3^2-360*_C3^4*\delta*_C5*\beta*\gamma+20*_C5^2*\delta*\alpha*\beta*_C3^2+(2/5)*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5^2*\beta*\gamma^2/\delta+(1/4)*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5^2*\beta^2*\gamma/\delta-9*_C3^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5*\beta*\gamma+30*_C3^2*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*\delta*_C5*\alpha+(1/5)*\gamma^3*(2*\gamma*_C5+_C5*\beta-40*\delta*_C3^2+\sqrt(4*\gamma^2*_C5^2+4*\gamma*_C5^2*\beta+_C5^2*\beta^2-40*\delta*\alpha*_C5^2))*_C5^2/\delta)</math>

:<math></math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>

==行波图==
{|
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_1.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_2.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_3.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_4.gif|thumb]]
|}
{|
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_5.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_6.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_7.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_8.gif|thumb]]
|}
{|
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_9.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_10.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_11.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_12.gif|thumb]]
|}
{|
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_14.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_13.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_15.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_16.gif|thumb]]
|}
{|
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_17.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_18.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_19.gif|thumb]]
|[[File:General_Fifth_order_KdV_equation_traveling_wave_plot_20.gif|thumb]]
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