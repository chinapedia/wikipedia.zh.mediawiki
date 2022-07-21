
{{dead end|time=2017-06-12T02:33:41+00:00}}

'''双重sinh-Gordon方程'''（Double sinh_Gordon equation）是一个[[非线性偏微分方程|非线性偏微分方程]]。<ref>Andrei D. Polyanin, Valentin F. Zaitsev,  HANDBOOK OF NONLINEAR PARTIAL DIFFERENTIAL EQUATIONS  SECOND EDITION  CRC Press, A  Chapman & Hall Book ISBN  9781420087239</ref>. <ref>Zeitschrift Für Naturforschung: A journal of physical sciences 2004  p933-937 </ref> <ref>A. M. WAZWAZ Exact solutions to the double sinh-gordon equation by the tanh method and a variable separated ODE method,Computers & Mathematics with Applications,Volume 50, Issues 10–12, November–December 2005, Pages 1685–1696</ref><ref>Issues in Logic, Operations, and Computational Mathematics and Geometry 2013  p484</ref><ref>Mathematical Reviews - Page 3708  2007</ref>.

<math>u_{xt}=asinh(u)+bsinh(2u)</math>

==行波解==
* <math> {v = _C5*JacobiCN(_C2+_C3*x-(a*_C5^2-2*b*_C5^2-2*b-a)*t/(_C3*(_C5^2-1)), \sqrt((-2*a*_C5^2+a*_C5^4+a+2*b-2*b*_C5^4)*(a*_C5^2-2*b*_C5^2-a))*_C5/(-2*a*_C5^2+a*_C5^4+a+2*b-2*b*_C5^4))}           </math>
* <math>{v = _C5*JacobiDN(_C2+_C3*x-_C5^2*(a*_C5^2-2*b*_C5^2-a)*t/(_C3*(-2*_C5^2+1+_C5^4)), \sqrt((-2*a*_C5^2+a*_C5^4+a+2*b-2*b*_C5^4)*(a*_C5^2-2*b*_C5^2-a))/((a*_C5^2-2*b*_C5^2-a)*_C5))}            </math>
* <math> {v = _C5*JacobiNC(_C2+_C3*x+(a*_C5^2-2*b*_C5^2-2*b-a)*t/(_C3*(_C5^2-1)), \sqrt(-(-2*a*_C5^2+a*_C5^4+a+2*b-2*b*_C5^4)*(a*_C5^2-2*b-a))/(-2*a*_C5^2+a*_C5^4+a+2*b-2*b*_C5^4))}           </math>
* <math> {v = _C5*JacobiND(_C2+_C3*x-(a*_C5^2-2*b-a)*t/(_C3*(-2*_C5^2+1+_C5^4)), \sqrt(-(-2*a*_C5^2+a*_C5^4+a+2*b-2*b*_C5^4)*(a*_C5^2-2*b-a))/(a*_C5^2-2*b-a))}           </math>
* <math>{v = \sqrt(a*(2*b+a))*csc(_C1+_C2*x-(2*b+a)*t/_C2)/a}            </math>
* <math>  {v = \sqrt(a*(2*b+a))*csc(_C2+_C3*x-(2*b+a)*t/_C3)/a}          </math>
* <math> {v = \sqrt(a*(2*b+a))*sec(_C1+_C2*x-(2*b+a)*t/_C2)/a}           </math>
* <math> {v = \sqrt(a*(2*b+a))*sech(_C1+_C2*x+(2*b+a)*t/_C2)/a}           </math>
* <math> {v = \sqrt(-a*(2*b+a))*csch(_C1+_C2*x+(2*b+a)*t/_C2)/a}           </math>
* <math> {v = \sqrt((a-2*b)*a)*cosh(_C2+_C3*x-(a-2*b)*t/_C3)/(a-2*b)}           </math>
* <math>  {v = \sqrt((a-2*b)*(2*b+a))*tanh(_C1+_C2*x+(1/8)*(a^2-4*b^2)*t/(_C2*b))/(a-2*b)}          </math>

其中
<math>v = tanh((1/2)*u)</math>

==特解==

*<math> u(x,t)= 2arctanh(1.5*JacobiCN(1.2+1.3*x+3.2307692307692307692*t, 1.0555973258234951998))    </math>
*<math>u(x,t)= 2arctanh(1.5*JacobiDN(1.2+1.3*x+3.6000000000000000000*t, .94733093343134184593))     </math>
*<math>u(x,t)=   2*arctanh(1.5*JacobiNC(-1.2-1.3*x+3.2307692307692307692*t, .33806170189140663100*I))   </math>
*<math>u(x,t)=2*arctanh(1.5*JacobiND(1.2+1.3*x+.36923076923076923077*t, 2.9580398915498080213*I))      </math>
*<math> u(x,t)=-2*arctanh(\sqrt(3)*csc(15.1-1.2*x+2.5000000000000000000*t))     </math>
*<math> u(x,t)=-2*arctanh(\sqrt(3)*csc(-1.2-1.3*x+2.3076923076923076923*t))     </math>
*<math> u(x,t)=2*arctanh(\sqrt(3)*sec(15.1-1.2*x+2.5000000000000000000*t))     </math>
*<math> u(x,t)= 2*arctanh(\sqrt(3)*sech(-15.1+1.2*x+2.5000000000000000000*t))     </math>
*<math>  u(x,t)= 2*arctanh(\sqrt(3)*sech(1.2+1.3*x+2.3076923076923076923*t))    </math>
*<math>  u(x,t)= 2*arctanh(\sqrt(-3)*csch(-15.1+1.2*x+2.5000000000000000000*t))    </math>
*<math>      </math>
*<math>      </math>
*<math>      </math>

==行波图==
{|
|[[File:DSHG_1.gif|File:DSHG 1.gif]]
|[[File:DSHG_2.gif|File:DSHG 2.gif]]
|}
{|
|[[File:DSHG_3.gif|File:DSHG 3.gif]]
|[[File:DSHG_4.gif|File:DSHG 4.gif]]
|}

{|
|[[File:DSHG_5.gif|File:DSHG 5.gif]]
|[[File:DSHG_6.gif|File:DSHG 6.gif]]
|}
{|
|[[File:DSHG_7.gif|File:DSHG 7.gif]]
|[[File:DSHG_8.gif|File:DSHG 8.gif]]
|}

==参考文献==
<references/>


[[Category:非线性偏微分方程|Category:非线性偏微分方程]]