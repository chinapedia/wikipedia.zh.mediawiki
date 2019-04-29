'''双重sine-Gordon方程'''是一个[[非线性|非线性]][[偏微分方程|偏微分方程]]，它在诸如[[铁磁性|铁磁]]物质研究、{{tsl|en|Charge density wave|带电密度波}}、[[液晶|液晶]]研究、[[氦|氦]]{{tsl|en|spin wave|自旋波}}、{{tsl|en|ultrashort pulse|超短光脉冲}}等[[工程物理|工程物理]]系领域有广泛的運用。双重sine-Gordon方程形式如下：<ref>Juntao Fu,Shikuo Liu and Shida Liu,Exact Jacobian Elliptic Function Solutions to the Double Sine-Gordon Equation,Z.Naturforsch. 60a,301-312   2005{{en}}</ref>

<math>u_{xt}=asin(u)+bsin(2u)</math>

==变换==

作变换

<math>u = 2*arctan(v)</math>

经简化后，上列方程化为

<math>2*v_{xt}+2*v_{xt}*v^2-4*v_{t}*v*v_{x} = 2*v*(a+a*v^2+2*b-2*b*v^2)</math>

==中间解==

此v方程有雅可比椭圆函数解：

<math>{v = _C5*JacobiCN(_C2+_C3*x-(a*_C5^2-2*b*_C5^2+a+2*b)*t/(_C3*(_C5^2+1)), \sqrt((a*_C5^4+2*a*_C5^2+a+2*b-2*b*_C5^4)*(a*_C5^2-2*b*_C5^2+a))*_C5/(a*_C5^4+2*a*_C5^2+a+2*b-2*b*_C5^4))}</math>

<math>{v = _C5*JacobiDN(_C2+_C3*x-_C5^2*(a*_C5^2-2*b*_C5^2+a)*t/(_C3*(_C5^4+2*_C5^2+1)),\sqrt((a*_C5^4+2*a*_C5^2+a+2*b-2*b*_C5^4)*(a*_C5^2-2*b*_C5^2+a))/((a*_C5^2-2*b*_C5^2+a)*_C5))}</math>

<math>{v = _C5*JacobiNC(_C2+_C3*x+(a*_C5^2-2*b*_C5^2+a+2*b)*t/(_C3*(_C5^2+1)), \sqrt((a*_C5^4+2*a*_C5^2+a+2*b-2*b*_C5^4)*(a*_C5^2+a+2*b))/(a*_C5^4+2*a*_C5^2+a+2*b-2*b*_C5^4))}</math>

<math>{v = _C5*JacobiND(_C2+_C3*x+(a*_C5^2+a+2*b)*t/(_C3*(_C5^4+2*_C5^2+1)), \sqrt((a*_C5^4+2*a*_C5^2+a+2*b-2*b*_C5^4)*(a*_C5^2+a+2*b))/(a*_C5^2+a+2*b))}</math>

<math>{v = _C5*JacobiNS(_C2+_C3*x+_C5^2*(a*_C5^2-2*b*_C5^2+a)*t/(_C3*(_C5^4+2*_C5^2+1)), \sqrt(-(a*_C5^2-2*b*_C5^2+a)*(a*_C5^2+a+2*b))/((a*_C5^2-2*b*_C5^2+a)*_C5))}</math>

…………………………

以及双曲函数解

<math>{v = \sqrt((a-2*b)*a)*sinh(_C1+_C2*x-(a-2*b)*t/_C2)/(a-2*b)}</math>

<math>{v = \sqrt(-(a-2*b)*a)*cosh(_C1+_C2*x-(a-2*b)*t/_C2)/(a-2*b)}</math>

<math>{v = \sqrt(-(a-2*b)*(a+2*b))*tanh(_C1+_C2*x+(1/8)*(a^2-4*b^2)*t/(_C2*b))/(a-2*b)}</math>

<math>{v = -\sqrt(a*(a+2*b))*csch(_C1+_C2*x+(a+2*b)*t/_C2)/a}</math>


………………

和三角函数解

<math> {v = \sqrt((a-2*b)*(a+2*b))*cot(_C1+_C2*x-(1/8)*(a^2-4*b^2)*t/(_C2*b))/(a-2*b)}    </math>

<math> {v = \sqrt((a-2*b)*(a+2*b))*tan(_C1+_C2*x-(1/8)*(a^2-4*b^2)*t/(_C2*b))/(a-2*b)}    </math>

<math> {v = \sqrt(-(a-2*b)*a)*cos(_C1+_C2*x+(a-2*b)*t/_C2)/(a-2*b)}    </math>

<math> {v = \sqrt(-(a-2*b)*a)*sin(_C1+_C2*x+(a-2*b)*t/_C2)/(a-2*b)}    </math>

……
==行波解==
作反变换

<math>u=tan(v/2)</math>即得原来sine-Gordon方程的行波解：


<math>\begin{align}
* 2 arctan(1.5 JacobiCN(-1.2 - 1.3 x + 0.17751479289940828402 t,   1.0741723110591493207 I))\\
*  2 arctan(1.5 JacobiDN(1.2 + 1.3 x + 0.20482476103777878925 t,    0.93094933625126274463 I))\\
*  2 arctan(1.5 JacobiNC(1.2 + 1.3 x + 0.17751479289940828402 t,    1.4675987714106856141))\\
  2 arctan(1.5 JacobiND(1.2 + 1.3 x + 0.38233955393718707328 t,    0.68138514386924689225))\\
* -2 arctan(1.5 JacobiNS(-1.2 - 1.3 x + 0.20482476103777878925 t,   1.3662601021279464511))\\
* -2 arctan(1.5 JacobiSN(-1.2 - 1.3 x + 0.38233955393718707328 t,   0.73192505471139988450))\\
*   -(2*I)*arctanh(sinh(-15.1+1.2*x+.83333333333333333333*t))\\
*2*arctan(sin(15.1-1.2*x+.83333333333333333333*t))\\
*2*arctan(sqrt(3)*coth(15.1-1.2*x+.31250000000000000000*t))\\

\end{align}</math>
==行波图==

{|
|[[File:DSG_1.gif|File:DSG 1.gif]]
|[[File:DSG_2.gif|File:DSG 2.gif]]
|}
{|
|[[File:DSG_3.gif|File:DSG 3.gif]]
|[[File:DSG_4.gif|File:DSG 4.gif]]
|}
{|
|[[File:DSG_5.gif|File:DSG 5.gif]]
|[[File:DSG_6.gif|File:DSG 6.gif]]
|}
{|
|[[File:DSG_7.gif|File:DSG 7.gif]]
|}

==参考文献==
<references/>

[[Category:非线性偏微分方程|Category:非线性偏微分方程]]