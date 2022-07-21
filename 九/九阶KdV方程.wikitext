'''九阶KdV方程'''(Ninth order KdV equation)是一个非线性偏微分方程：<ref>Andrei D. Polyanin,Valentin F. Zaitsev, HANDBOOK OF NONLINEAR PARTIAL DIFFERENTIAL EQUATIONS, SECOND EDITION p1041 CRC PRESS</ref>

<math>U[t]+6*U*U[x]+U[x,x,x]-U[x,x,x,x,x]+\alpha*U[x,x,x,x,x,x,x]+\beta*U[x,x,x,x,x,x,x,x,x]=0</math>

其中

U[t] 代表 <math>\frac{\partial  u(x,t)}{\partial t}</math>

U[x,x,x] 代表 <math>\frac{\partial^3  u(x,t)}{\partial x^3}</math>

余类推。

==解析解==
:<math>w[1] := (3816888075/22609585952)*sech(0.94052142507806327828e-5*sqrt(150156069)*(x-(11862900/3364741)*t))^8</math>
:<math>w[2] := (3816888075/22609585952)*csch(0.94052142507806327828e-5*sqrt(150156069)*(x-(11862900/3364741)*t))^8</math>
:<math>w[3] := 83040300/706549561+(3816888075/22609585952)*sech(0.94052142507806327828e-5*sqrt(150156069)*(x+(11862900/3364741)*t))^8</math>
:<math>w[4] := 83040300/706549561+(3816888075/22609585952)*csch(0.94052142507806327828e-5*sqrt(150156069)*(x+(11862900/3364741)*t))^8</math>
:<math>w[5] := (3816888075/22609585952)*sec(0.94052142507806327828e-5*sqrt(150156069)*(x-(11862900/3364741)*t))^8</math>
:<math>w[6] := (3816888075/22609585952)*csc(0.94052142507806327828e-5*sqrt(150156069)*(x-(11862900/3364741)*t))^8</math>
:<math>w[7] := 83040300/706549561+(3816888075/22609585952)*sec(0.94052142507806327828e-5*sqrt(150156069)*(x+(11862900/3364741)*t))^8</math>
:<math>w[8] := 83040300/706549561+(3816888075/22609585952)*csc(0.94052142507806327828e-5*sqrt(150156069)*(x+(11862900/3364741)*t))^8</math>
:<math>w[9] := (3816888075/22609585952)*sech(0.94052142507806327828e-5*sqrt(150156069)*(x-(11862900/3364741)*t))^8*(x-6*C1*t+C2)</math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>
:<math></math>

==行波图==
{|
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_1.gif|thumb]]
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_2.gif|thumb]]
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_3.gif|thumb]]
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_4.gif|thumb]]
|}

{|
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_5.gif|thumb]]
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_6.gif|thumb]]
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_7.gif|thumb]]
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_8.gif|thumb]]
|}
{|
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_9.gif|thumb]]
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_10.gif|thumb]]
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_11.gif|thumb]]
|[[File:Nineth_order_KdV_equation_traveling_wave_plot_12.gif|thumb]]
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