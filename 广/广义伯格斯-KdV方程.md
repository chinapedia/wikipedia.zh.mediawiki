'''广义伯格斯-KdV方程 '''(Generalized Burgers-KdV equation)是一个非线性偏微分方程：<ref>Andrei D. Polyanin,Valentin F. Zaitsev, HANDBOOK OF NONLINEAR PARTIAL DIFFERENTIAL EQUATIONS,（《非线性偏微分方程手册》） SECOND EDITION p1045 CRC PRESS</ref>

<math>U[t]-\alpha*\frac{\partial^n u(x,t)}{\partial x^n}-\beta*u(x,t)*\frac{\partial u(x,t)}{\partial x}=0    </math>

==解析解==
当 n=7， 有下列特解：
:<math> u(x, t) = (71280*\alpha*_C4^7*_C1+_C5)/(\beta*_C4)-665280*\alpha*_C4^6*WeierstrassP(_C3+_C4*x+_C5*t, 0, _C1)^3/\beta  </math>
:<math> u(x, t) = (_C4-42240*\alpha*_C3^7+84480*\alpha*_C3^7*(-(1/2)*\sqrt(3)-1/2*I)^2)/(\beta*_C3)-665280*\alpha*_C3^6*(-1+(-(1/2)*\sqrt(3)-1/2*I)^2)*JacobiDN(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^2/\beta+665280*\alpha*_C3^6*((-(1/2)*\sqrt(3)-1/2*I)^2-2)*JacobiDN(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^4/\beta+665280*\alpha*_C3^6*JacobiDN(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^6/\beta  </math>
:<math> u(x, t) = (_C4-42240*\alpha*_C3^7+84480*\alpha*_C3^7*(-(1/2)*\sqrt(3)-1/2*I)^2)/(\beta*_C3)-665280*\alpha*_C3^6*(-1+(-(1/2)*\sqrt(3)-1/2*I)^2)*JacobiNC(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^2/\beta+665280*\alpha*_C3^6*((-(1/2)*\sqrt(3)-1/2*I)^2-2)*JacobiNC(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^4/\beta+665280*\alpha*_C3^6*JacobiNC(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^6/\beta  </math>
:<math>  u(x, t) = (_C4-42240*\alpha*_C3^7+84480*\alpha*_C3^7*(-(1/2)*\sqrt(3)-1/2*I)^2)/(\beta*_C3)-665280*_C3^6*\alpha*(-(1/2)*\sqrt(3)-1/2*I)^2*JacobiND(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^2/\beta+665280*\alpha*_C3^6*(1+(-(1/2)*\sqrt(3)-1/2*I)^2)*JacobiND(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^4/\beta-665280*\alpha*_C3^6*JacobiND(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^6/\beta </math>
:<math> u(x, t) = (_C4-42240*\alpha*_C3^7+84480*\alpha*_C3^7*(-(1/2)*\sqrt(3)+1/2*I)^2)/(\beta*_C3)-665280*_C3^6*\alpha*(-(1/2)*\sqrt(3)+1/2*I)^2*JacobiND(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)-1/2*I)^2/\beta+665280*\alpha*_C3^6*(1+(-(1/2)*\sqrt(3)+1/2*I)^2)*JacobiND(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)-1/2*I)^4/\beta-665280*\alpha*_C3^6*JacobiND(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)-1/2*I)^6/\beta  </math>
:<math> u(x, t) = (_C4-42240*\alpha*_C3^7+84480*\alpha*_C3^7*((1/2)*\sqrt(3)+1/2*I)^2)/(\beta*_C3)-665280*\alpha*_C3^6*(-1+((1/2)*\sqrt(3)+1/2*I)^2)*JacobiSN(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^2/\beta+665280*\alpha*_C3^6*(((1/2)*\sqrt(3)+1/2*I)^2-2)*JacobiSN(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^4/\beta+665280*\alpha*_C3^6*JacobiSN(_C2+_C3*x+_C4*t, (1/2)*\sqrt(3)+1/2*I)^6/\beta  </math>


广义伯格斯-KdV方程之部分通解为：

:<math> u(x, t) = C1^(n-1)*(x+C1)*(C1*x+b*C1*C2*t+C3)/(b*(C2+t))+C2  </math>
:<math> u(x, t) =  C1^(n-1)*(x+C1)*(C1*x+b*C1*C2*t+C3)/(b*(C2+t))+C2 </math>
:<math> u(x, t) = C1^(n-1)*((-1)^n*a*(2*n-1)!/(b*(n-1)!*(x+b*C1*t+C2)^(n-1))+C1)*(C1*x+b*C1*C2*t+C3)+C2 </math>
:<math> u(x, t) =C1^(n-1)*((-1)^n*a*(2*n-1)!/(b*(n-1)!*(x+b*C1*t+C2)^(n-1))+C1)*(C1*x+b*C1*C2*t+C3)+C2  </math>
:<math> u(x, t) =C1^(n-1)*(x+C1)*(C1^n*t+C4)/(b*(C2+t))+C2  </math>
:<math> u(x, t) =C1^(n-1)*(x+C1)*(C1^n*t+C4)/(b*(C2+t))+C2  </math>
:<math>   </math>
:<math>   </math>
:<math>   </math>
:<math>   </math>
:<math>   </math>
:<math>   </math>
:<math>   </math>

==行波图==
{|
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_1.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_2.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_3.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_4.gif|thumb]]
|}
{|
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_5.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_6.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_7.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_8.gif|thumb]]
|}
{|
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_9.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_10.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_11.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_12.gif|thumb]]
|}
{|
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_13.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_14.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_15.gif|thumb]]
|[[File:Generalized_7th_order_Burgers-KdV_equation_plot_16.gif|thumb]]
|}
{|
|[[File:Generalized_10th_order_Burgers-KdV_equation_plot_1.gif|thumb]]
|[[File:Generalized_10th_order_Burgers-KdV_equation_plot_2.gif|thumb]]
|[[File:Generalized_10th_order_Burgers-KdV_equation_plot_3.gif|thumb]]
|[[File:Generalized_10th_order_Burgers-KdV_equation_plot_4.gif|thumb]]
|}
{|
|[[File:Generalized_10th_order_Burgers-KdV_equation_plot_5.gif|thumb]]
|[[File:Generalized_10th_order_Burgers-KdV_equation_plot_6.gif|thumb]]
|[[File:Generalized_10th_order_Burgers-KdV_equation_plot_7.gif|thumb]]
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