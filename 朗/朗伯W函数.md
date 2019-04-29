[[File:lambertw.png|thumb]]

'''朗伯W函数'''（{{lang-en|Lambert W function}}，又称为'''欧米加函数'''或'''乘积对数'''），是''f''(''w'') = ''we''<sup>''w''</sup>的[[反函数|反函数]]，其中''e''<sup>''w''</sup>是[[指数函数|指数函数]]，''w''是任意复数。对于任何复数''z''，都有：

:<math>z = W(z)e^{W(z)}.</math>

由于函数''f''不是[[单射|单射]]，因此函数''W''是[[多值函数|多值]]的（除了0以外）。如果我们把''x''限制为实数，并要求''w''是实数，那么函数仅对于''x'' ≥ −1/''e''有定义，在(−1/''e'', 0)内是多值的；如果加上''w'' ≥ −1的限制，则定义了一个单值函数''W''<sub>0</sub>(''x'')（见图）。我们有''W''<sub>0</sub>(0) = 0，''W''<sub>0</sub>(−1/''e'') = −1。而在<nowiki>[</nowiki>−1/''e'', 0)内的''w'' ≤ −1分支，则记为''W''<sub>−1</sub>(''x'')，从''W''<sub>−1</sub>(−1/''e'') = −1递减为''W''<sub>−1</sub>(0<sup>−</sup>) = −∞。

朗伯''W''函数不能用[[初等函数|初等函数]]来表示。它在[[组合数学|组合数学]]中有许多用途，例如[[树_(图论)|树]]的计算。它可以用来解许多含有指数的方程，也出现在某些[[微分方程|微分方程]]的解中，例如''y'''(''t'') = ''a'' ''y''(''t'' − 1)。
:[[File:Product_Log.jpg|thumb]]

== 微分和积分 ==
朗伯 <math>W\,</math>函数的积分形式为
:<math>W(x)=\frac{x}{\pi}\int_0^{\pi} \frac{\left(1-v\cot v\right)^2+v^2}{x+v\csc v \cdot e^{-v\cot v}} {\rm{d}}v,|\arg\left(x\right)|<\pi\,</math> 

:<math>W(x)=\int_{-\infty}^{-\frac{1}{e}}{-\frac{1}{\pi}}\Im \left[\frac{{\rm{d}}}{{\rm{d}}x}W(x)\right]\ln \left(1-\frac{z}{x}\right){\rm{d}}x\,</math>



若 <math>x\not\in\left[-\frac{1}{e},0\right],k\in{\mathbb{Z}}\,</math> ,若 <math>x\in\left(-\frac{1}{e},0\right),k=1,\pm2,\pm3,...\,</math>

:<math>W_k(x)=1+\left(\ln x-1+2k\pi {{\rm{i}}}\right)e^{\frac{{\rm{i}}}{2\pi}\int_0^{\infty}\ln \frac{t-\ln t+\ln x+(2k+1)\pi{\rm{i}}}{t-\ln t+\ln x+(2k-1)\pi{\rm{i}}}\cdot\frac{{\rm{d}}t}{t+1}}=1+\left(\ln x-1+2k\pi {{\rm{i}}}\right)e^{\frac{{\rm{i}}}{2\pi}\int_0^{\infty}\ln \frac{\left(t-\ln t+\ln x\right)^2+\left(4k^2-1\right)\pi^2+2\pi\left(t-\ln t+\ln x\right){\rm{i}}}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}\cdot\frac{{\rm{d}}t}{t+1}}\,</math>

把被积函数的实部和虚部分离出来：

:<math>W_k(x)=1+\left(\ln x-1+2k\pi {{\rm{i}}}\right)e^{\frac{{\rm{i}}}{2\pi}\int_0^\infty\left[\frac{1}{2}\ln\frac{\left(t-\ln t+\ln x\right)^2+\left(2k+1\right)^2\pi^2}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}+{\rm{i}}\arctan\frac{2\pi\left(t-\ln t+\ln x\right)}{\left(t-\ln t+\ln x\right)^2+\left(4k^2-1\right)\pi^2}\right]\cdot\frac{{\rm{d}}t}{t+1}}</math>

:<math>{}_{W_k(x)=1+\frac{\left(\ln x-1\right)\cos\frac{1}{4\pi}\int_0^{\infty}\ln\frac{\left(t-\ln t+\ln x\right)^2+\left(2k+1\right)^2\pi^2}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}\cdot\frac{{\rm{d}}t}{t+1}-2k\pi\sin\frac{1}{4\pi}\int_0^{\infty}\ln\frac{\left(t-\ln t+\ln x\right)^2+\left(2k+1\right)^2\pi^2}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}\cdot\frac{{\rm{d}}t}{t+1}+{\rm{i}}\left[\left(\ln x-1\right)\sin\frac{1}{4\pi}\int_0^{\infty}\ln\frac{\left(t-\ln t+\ln x\right)^2+\left(2k+1\right)^2\pi^2}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}\cdot\frac{{\rm{d}}t}{t+1}+2k\pi\cos\frac{1}{4\pi}\int_0^{\infty}\ln\frac{\left(t-\ln t+\ln x\right)^2+\left(2k+1\right)^2\pi^2}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}\cdot\frac{{\rm{d}}t}{t+1}\right]}{e^{\frac{1}{2\pi}\int_0^\infty\arctan\frac{2\pi\left(t-\ln t+\ln x\right)}{\left(t-\ln t+\ln x\right)^2+\left(4k^2-1\right)\pi^2}\cdot\frac{\rm{d}t}{t+1}}}}</math>


设 <math>W_k(x)=u+v{\rm{i}},x=t+s{\rm{i}}</math> ，则有 <math>\left(u+v{\rm{i}}\right)e^{u+v{\rm{i}}}=t+s{\rm{i}}</math> ，展开分离出实部和虚部，

<math>e^u\left(u\cos v-v\sin v\right)=t,e^u\left(u\sin v+v\cos v\right)=s</math>,当<math>s=0</math>时，易知 <math>u=-v\cot v</math>


:<math>{}_{W_k(x)=\frac{\left(1-\ln x\right)\sin\frac{1}{4\pi}\int_0^{\infty}\ln\frac{\left(t-\ln t+\ln x\right)^2+\left(2k+1\right)^2\pi^2}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}\cdot\frac{{\rm{d}}t}{t+1}-2k\pi\cos\frac{1}{4\pi}\int_0^{\infty}\ln\frac{\left(t-\ln t+\ln x\right)^2+\left(2k+1\right)^2\pi^2}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}\cdot\frac{{\rm{d}}t}{t+1}}{e^{\frac{1}{2\pi}\int_0^\infty\arctan\frac{2\pi\left(t-\ln t+\ln x\right)}{\left(t-\ln t+\ln x\right)^2+\left(4k^2-1\right)\pi^2}\cdot\frac{\rm{d}t}{t+1}}}\cot\frac{\left(\ln x-1\right)\sin\frac{1}{4\pi}\int_0^{\infty}\ln\frac{\left(t-\ln t+\ln x\right)^2+\left(2k+1\right)^2\pi^2}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}\cdot\frac{{\rm{d}}t}{t+1}+2k\pi\cos\frac{1}{4\pi}\int_0^{\infty}\ln\frac{\left(t-\ln t+\ln x\right)^2+\left(2k+1\right)^2\pi^2}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}\cdot\frac{{\rm{d}}t}{t+1}}{e^{\frac{1}{2\pi}\int_0^\infty\arctan\frac{2\pi\left(t-\ln t+\ln x\right)}{\left(t-\ln t+\ln x\right)^2+\left(4k^2-1\right)\pi^2}\cdot\frac{\rm{d}t}{t+1}}}
+\frac{\left(\ln x-1\right)\sin\frac{1}{4\pi}\int_0^{\infty}\ln\frac{\left(t-\ln t+\ln x\right)^2+\left(2k+1\right)^2\pi^2}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}\cdot\frac{{\rm{d}}t}{t+1}+2k\pi\cos\frac{1}{4\pi}\int_0^{\infty}\ln\frac{\left(t-\ln t+\ln x\right)^2+\left(2k+1\right)^2\pi^2}{\left(t-\ln t+\ln x\right)^2+\left(2k-1\right)^2\pi^2}\cdot\frac{{\rm{d}}t}{t+1}}{e^{\frac{1}{2\pi}\int_0^\infty\arctan\frac{2\pi\left(t-\ln t+\ln x\right)}{\left(t-\ln t+\ln x\right)^2+\left(4k^2-1\right)\pi^2}\cdot\frac{\rm{d}t}{t+1}}}{\rm{i}},}</math>

:<math>W_0(x)=1+\left(\ln x-1\right)e^{-\frac{1}{\pi}\int_0^\infty\arg\left(t-\ln t+\ln x+\pi{\rm{i}}\right)\cdot\frac{\rm{d}t}{t+1}},x>0</math>

若 <math>x>\frac{1}{e}</math> ，上式还可化为<math>W_0(x)=1+\left(\ln x-1\right)e^{-\frac{1}{\pi}\int_0^\infty\arctan\frac{\pi}{t-\ln t+\ln x}\cdot\frac{\rm{d}t}{t+1}}</math>

由[[隐函数|隐函数]]的求导法则，朗伯<math>W\,</math>函数满足以下的[[微分方程|微分方程]]：

:<math>z\left[1+W(z)\right]\frac{{\rm{d}}}{{\rm{d}}z}W(z)=W(z)</math>，<math>z\neq -\frac{1}{e}\,,</math>

因此：

:<math>\frac{{\rm{d}}}{{\rm{d}}z}W(z)=\frac{ W(z) }{z\left[1 + W(z)\right]}</math>，<math>z\neq -\frac{1}{e} \,.</math>

函数<math>W(x)\,</math>，以及许多含有<math>W(x)\,</math>的表达式，都可以用<math>w=W(x)\,</math>的[[换元积分法|变量代换]]来积分，也就是说<math>x=we^w\,</math> 

:<math>\int W(x) {\rm{d}}x = x \left[ W(x)+ \frac{1}{W (x) }-1 \right] + C</math>

:<math>\int_0^1 W(x) {\rm{d}}x = \Omega+\frac{1}{\Omega} -2\approx 0.330366</math>
其中<math>\Omega</math>為[[欧米加常数|欧米加常数]]。

== 性质 ==

<math>1\,</math>、<math>z^{z^{z^{z^{z^{.^{.^{.}}}}}}}=\lim_{n \to \infty}(z \upuparrows n) = - \frac{W(-\ln z)}{\ln z}</math>，

其中<math>\upuparrows</math>是[[高德納箭號表示法|高德納箭號表示法]]。

<math>2\,</math>、若<math>z>0 \,</math>，则<math>\ln W(z)=\ln z-W(z)\,</math>

== 泰勒级数 ==
<math>W_0 \,</math>在<math> x=0 \,</math>的泰勒级数如下：

:<math>
W_0 (x) = \sum_{n=1}^\infty \frac{(-n)^{n-1}}{n!}\ x^n = x - x^2 + \frac{3}{2}x^3 - \frac{8}{3}x^4 + \frac{125}{24}x^5 - \cdots
</math>

[[收敛半径|收敛半径]]为 <math> \frac{1}{e}\,</math> 。


== 加法定理 ==
:<math>W(x)+W(y)=W\left[\frac{xy}{W(x)}+\frac{xy}{W(y)}\right]\,</math>
:<math>x>0,y>0\,</math>

== 複數值 ==
實部
:<math> \Re\left[W(x+y{\rm{i}})\right]=\sum_{k=1}^{\infty}\frac{(-k)^{k-1}}{k!}\sqrt{(x^2+y^2)^k}\cos \left(k\arctan\frac{x}{y}\right)\,</math> , <math>x^2+y^2<\frac{1}{e^2}\,</math>
虛部
:<math> \Im\left[W(x+y{\rm{i}})\right]=\sum_{k=1}^{\infty}\frac{(-k)^{k-1}}{k!}\sqrt{(x^2+y^2)^k}\sin \left(k\arctan\frac{x}{y}\right)\,</math>, <math>x^2+y^2<\frac{1}{e^2}\,</math>
模長
:<math>|W(x+y{\rm{i}})|=W(\sqrt{x+y})\,</math>
模角
:<math>\arg\left[W(x+y{\rm{i}})\right]=\sum_{k=1}^{\infty}\frac{(-k)^{k-1}}{k!}\arctan\left[\cot(k\arctan\frac{x}{y})\right]\,</math>, <math>x^2+y^2<\frac{1}{e^2}\,</math>
共軛值
:<math> \overline{W(x+y{\rm{i}})}=\sum_{k=1}^{\infty}\frac{(-k)^{k-1}}{k!}\sqrt{(x^2+y^2)^k}\left[\cos \left(k\arctan\frac{x}{y}\right)-{\rm{i}}\sin \left(k\arctan\frac{x}{y}\right)\right]\,</math>, <math>x^2+y^2<\frac{1}{e^2}\,</math>

== 特殊值 ==

:<math>W\left(-\frac{\pi}{2}\right) = \frac{\pi}{2}i</math>

:<math>W\left(-\frac{\ln 2}{2}\right)= -\ln 2</math>

:<math>W\left(-{1\over e}\right) = -1</math>

:<math>W\left(1\right) = \Omega=\frac{1}{\int_{-\infty}^{\infty}\frac{{\rm{d}}x}{(e^x-x)^2+\pi^2}}-1\approx 0.56714329\dots \,</math>（[[欧米加常数|欧米加常数]]）

:<math>W(e) = 1\,</math>

:<math>W(e^{e+1}) = e\,</math>

:<math>W\left(\frac{1}{e^{1- \frac{1}{e}}}\right)= \frac{1}{e}</math>

:<math>W(-\frac{1}{e})=-1</math>

:<math>W({\pi}e^{\pi})=\pi</math>

:<math>W(k{\ln k})={\ln k}</math> <math>(k>0</math>

:<math>W({\rm{i}}\pi)=-{\rm{i}}\pi</math>

:<math>W(-{\rm{i}}\pi)={\rm{i}}\pi</math>

:<math>W({\rm{i}}\cos1-\sin1)={\rm{i}}</math>

:<math>W(-\frac{3}{2}{\pi})=-\frac{3}{2}{\pi}{\rm{i}}</math>

:<math>W(-\frac{\sqrt[7]{8}}{7}{\ln 2})=-\frac{32}{7}{\ln 2}</math>

:<math>W(-\frac{\sqrt{3}}{54}{\ln 3})=-\frac{9}{2}{\ln 3}</math>

:<math>W(-\frac{\ln 2}{4})=-4{\ln 2}</math>

:<math>W\left(-1\right)=\frac{e^{\frac{1}{2\pi}\int_0^\infty{1\over t+1}\arctan{2\pi\over t-\ln t}{\rm{d}}t}-\cos\left[\frac{1}{4\pi}\int_0^\infty{1\over t+1}\ln{\left(t-\ln t\right)^2\over 4\pi^2+\left(t-\ln t\right)^2}{\rm{d}}t\right]+\pi\sin\left[\frac{1}{4\pi}\int_0^\infty{1\over t+1}\ln{\left(t-\ln t\right)^2\over 4\pi^2+\left(t-\ln t\right)^2}{\rm{d}}t\right]-{\rm{i}}\left\{\pi\cos\left[\frac{1}{4\pi}\int_0^\infty{1\over t+1}\ln{\left(t-\ln t\right)^2\over 4\pi^2+\left(t-\ln t\right)^2}{\rm{d}}t\right]+\sin\left[\frac{1}{4\pi}\int_0^\infty{1\over t+1}\ln{\left(t-\ln t\right)^2\over 4\pi^2+\left(t-\ln t\right)^2}{\rm{d}}t\right]\right\}}{e^{\frac{1}{2\pi}\int_0^\infty{1\over t+1}\arctan{2\pi\over t-\ln t}{\rm{d}}t}}\approx -0.31813-1.33723{\rm{i}}</math>

:<math>W(-\frac{\ln k}{k})=-\ln k</math>

:<math>W\left[-\frac{\ln (x+1)}{x(x+1)^{\frac{1}{x}}}\right]=-\frac{x+1}{x}\ln (x+1)>,-1<x<0</math>

== 应用 ==
许多含有指数的方程都可以用<math>W\,</math>函数来解出。一般的方法是把未知数都移到方程的一侧，并设法化为<math>Y= Xe^X \,</math>的形式。

=== 例子 ===

;例子1

: <math>2^t  = 5 t\,</math>

: <math>\Rightarrow 1 = \frac{5 t}{2^t}\,</math>

: <math>\Rightarrow 1 = 5 t \, e^{-t \ln 2}\,</math>

: <math>\Rightarrow \frac{1}{5} = t \, e^{-t \ln 2}\,</math>

: <math>\Rightarrow -\frac{\ln 2}{5} = ( - \, t \, \ln 2 ) \, e^{-t \ln 2}\,</math>

: <math>\Rightarrow -t \ln 2 = W_k \left (-\frac{\ln 2}{5} \right )\,</math>

: <math>\Rightarrow t = -\frac{ W_k \left ( -\frac{\ln 2}{5} \right )}{\ln 2}\,</math>

更一般地，以下的方程

: <math> Q^{a x + b} = c x + d \,</math>
其中

: <math> Q > 0 \land Q \neq 1\land c \neq 0 </math>

两边同乘: <math> \frac{a}{c} </math>，

得到：<math> \frac{a}{c} Q^{ax+b} = ax + \frac{ad}{c}  \,</math>

同除以：<math> Q^{ax} \,</math>，

得到：<math> \frac{a}{c} Q^{b} = \left(ax + \frac{ad}{c} \right)Q^{-ax} \,</math>

同除：<math> Q^{\frac{ad}{c}} \,</math>， 

<math>\frac{a}{c} Q^{b-\frac{ad}{c}}= \left(ax + \frac{ad}{c}\right)Q^{-\left(ax+\frac{ad}{c}\right)}  \,</math>

可以用变量代换

令<math> t = a x + \frac{a d}{c} </math>

化为
 
: <math> t Q^{-t} = \frac{a}{c} Q^{b-\frac{a d}{c}} </math>

即：<math> t \left(e^{\ln Q}\right) ^{-t} = \frac{a}{c} Q^{b-\frac{a d}{c}} </math>

同乘：<math> {\ln Q} \,</math>

得出

:<math> t{\ln Q} \cdot e^{-t \ln Q}={\ln Q} \cdot \frac{a}{c} Q^{b-\frac{a d}{c}} </math>

故<math> t{\ln Q}=-W_k\left(-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}}\right) </math>

带入<math> t= a x + \frac{a d}{c} </math>

为

:<math> \left(ax+\frac{ad}{c}\right){\ln Q}=-W_k\left(-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}}\right) </math>

因此最终的解为

:<math> x = -\frac{W_k\left(-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}}\right)}{a\ln Q} - \frac{d}{c} </math>

若辅助方程：<math> xe^x=-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}} </math>中，

:<math>-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}} \in \left(-\infty ,-\frac{1}{e} \right) </math>,

辅助方程无实数解，原方程亦无实解；

若：<math>-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}} \in \left\{-\frac{1}{e}\right\} \cup\mathbf [0,+\infty ) </math>,

辅助方程有一实数解，原方程有一实解：

:<math> x = -\frac{W_k\left(-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}}\right)}{a\ln Q} - \frac{d}{c} </math>

若: <math>-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}} \in \left(-\frac{1}{e},0 \right) </math>,

辅助方程有二实解，设为<math>W\left(-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}}\right) </math>，

<math>{\rm{W}}_{-1}\left(-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}}\right) </math>，

为

<math> x_1=-\frac{W\left(-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}}\right)}{a\ln Q} - \frac{d}{c} </math>

<math> x_2=-\frac{{\rm{W}}_{-1}\left(-\frac{a\ln Q}{c}\,Q^{b-\frac{a d}{c}}\right)}{a\ln Q} - \frac{d}{c} </math>

;例子2

用类似的方法，可知以下方程的解

:<math>x^x={\mathrm{t}}\, ,</math>

为

:<math>x=\frac{\ln{\rm{t}}}{W(\ln {\rm{t}})}\, </math>

或

:<math>x=\exp\left(W_k\left[\ln({\rm{t}})\right]\right).</math>

;例子3

以下方程的解

:<math>x \log_b {x} = a \,</math>

具有形式

:<math>x = \frac{a {\ln b}}{W_k\left(a {\ln b}\right)}</math>


;例子4
:<math>x^a-b^x=0\,</math>
: <math> a > 0 \,</math> : <math> b > 0 \,</math> : <math> x > 0 \,</math>
取对数，
: <math> a \ln x=x \ln b \,</math>

: <math> \frac{\ln x}{x}=\frac{\ln b}{a}\,</math>

: <math>e^{\frac{\ln x}{x}}=e^{\frac{\ln b}{a}} \,</math>

: <math>x^{\frac{1}{x}}=b^{\frac{1}{a}}\,</math>

取倒数，
: <math> \left(\frac{1}{x} \right)^{\frac{1}{x}}=b^{-\frac{1}{a}}\,</math>

: <math> \frac{1}{x} =-\frac{\ln b}{aW\left(-\frac{1}{a} \ln b\right)}\,</math>

最终解为 : <math> x=-\frac{a}{\ln b}W_k\left(-\frac{\ln b}{a}\right)\,</math>

;例子5
:<math>(ax+b)^n=u^{cx+d} \,</math>
两边开<math>n \,</math>次方并除以<math>a \,</math>得

<math>x+\frac{b}{a}=\frac{u^{\frac{c}{n}x+\frac{d}{n}}}{a}\left(\cos\frac{2k\pi}{n}+{\rm{i}}\sin\frac{2k\pi}{n}\right)\,</math>

令<math>u=e^{\ln u}\,</math> ，

化为

<math>x+\frac{b}{a}=\frac{e^{\frac{c\ln u}{n}x+\frac{d\ln u}{n}}}{a}\left(\cos\frac{2k\pi}{n}+{\rm{i}}\sin\frac{2k\pi}{n}\right)\,</math>

两边同乘

<math>-\frac{c\ln u}{n}u^{-\frac{c}{n}x-\frac{cb}{na}}\,</math> ，

<math>\left(-\frac{c\ln u}{n}x-\frac{cb\ln u}{na}\right)e^{-\frac{c\ln u}{n}x-\frac{cb\ln u}{na}}=-\frac{c\ln u}{na}u^{\frac{d}{n}-\frac{cb}{na}}\left(\cos\frac{2k\pi}{n}+{\rm{i}}\sin\frac{2k\pi}{n}\right)\,</math>

最终得

<math>x_k=-\frac{n}{c\ln u}W_k\left[-\frac{c\ln u}{na}u^{\frac{d}{n}-\frac{cb}{na}}\left(\cos\frac{2k\pi}{n}+{\rm{i}}\sin\frac{2k\pi}{n}\right)\right]-\frac{b}{a}\,</math>

<math>k\in{\mathbb{Z}}\,</math>

==一般化==
標準的 Lambert W 函數可用來表示以下超越代數方程式的解：
:<math> e^{-c x} = a_o (x-r) ~~\quad\qquad\qquad\qquad\qquad(1)</math>
其中 ''a''<sub>0</sub>, ''c''   與 ''r''  為實常數。

其解為<math display="inline"> x = r +\tfrac{W\left(\frac{ce^{-c r}}{a_o}\right)}{c} </math>

Lambert W 函數之一般化<ref> T.C. Scott and R.B. Mann, ''General Relativity and Quantum Mechanics: Towards a Generalization of the Lambert W Function'', AAECC (Applicable Algebra in Engineering, Communication and Computing), vol. 17, no. 1, (April 2006), pp.41-47, [http://portal.acm.org/citation.cfm?id=1127202.1127208&coll=%20&dl=ACM]; Arxiv [http://arxiv.org/abs/math-ph/0607011] </ref><ref>T.C. Scott, G. Fee and J. Grotendorst, [http://www.sigsam.org/cca/issues/issue185.html "Asymptotic series of Generalized Lambert W Function"], SIGSAM, vol. 47, no. 3, (September 2013), pp. 75-83</ref><ref>T.C. Scott, G. Fee, J. Grotendorst and W.Z. Zhang, [http://www.sigsam.org/cca/issues/issue188.html "Numerics of the Generalized Lambert W Function"], SIGSAM, vol. 48, no. 2, (June 2014), pp. 42-56</ref> 包括: 
* 一項在低維空間內[[廣義相對論|廣義相對論]]與[[量子力學|量子力學]]的應用（[[量子引力|量子引力]]），實際上一種以前未知的 連結 於此二區域中，如 “Journal of Classical and Quantum Gravity”<ref>P.S. Farrugia, R.B. Mann, and T.C. Scott, ''N-body Gravity and the Schrödinger Equation'', Class. Quantum Grav. vol. 24, (2007), pp. 4647-4659, [http://www.iop.org/EJ/toc/0264-9381/24/18]; Arxiv  [http://arxiv.org/abs/gr-qc/0611144v2]</ref> 所示其 (1) 的右邊式現為二維多項式 x：

:<math> e^{-c x} = a_o (x-r_1 ) (x-r_2 ) ~~\qquad\qquad(2)</math> 

:其中 ''r''<sub>1</sub> 和 ''r''<sub>2</sub> 是不同實常數，為二維多項式的根。於此函數解有單一引數 ''x'' 但 ''r''<sub>i</sub>  和 ''a''<sub>o</sub> 為函數的參數。如此一來，此一般式類似於 “hypergeometric”（超几何分布）函數與 “Meijer G“，但屬於不同類函數。當 ''r''<sub>1</sub> = ''r''<sub>2</sub>，(2)的兩方可分解為 (1) 因此其解簡化為標準 W 函數。(2)式代表著 “dilaton”（[[軸子|軸子]]）場的方程，可據此推導線性，雙體重力問題 1+1 維（一空間維與一時間維）當兩不等（靜止）質量，以及，量子力學的特徵能[[Delta位勢阱|Delta位勢阱]]給不等電位於一維空間。

*量子力學的一特例特徵能的分析解三體問題，亦即（三維）[[氢分子离子|氢分子離子]]。<ref>T.C. Scott, M. Aubert-Frécon and J. Grotendorst, ''New Approach for the Electronic Energies of the Hydrogen Molecular Ion'',  Chem. Phys. vol. 324, (2006), pp. 323-338, [http://www.sciencedirect.com/science?_ob=ArticleURL&_udi=B6TFM-4HNYMS6-5&_user=10&_rdoc=1&_fmt=%20&_orig=search&_sort=d&view=c&_acct=C000050221&_version=1&_urlVersion=0&_userid=10&md5=9fd01e7be3137ccf30280c1281b62e14]; Arxiv [http://arxiv.org/abs/physics/0607081]</ref>於此 (1)（或 (2)）的右手邊現為無限級數多項式之比於 ''x''：

:<math> e^{-c x} = a_o \frac{\prod_{i=1}^{\infty} (x-r_i )}{ \prod_{i=1}^{\infty} (x-s_i)} \qquad \qquad\qquad(3)</math>             
: 其中 ''r''<sub>i</sub> 與 ''s''<sub>i</sub> 是相異實常數而 ''x'' 是特徵能和內核距離R之函數。式 (3) 與其特例表示於 (1) 和 (2) 是與一更大類型[[时滞微分方程|延遲微分方程]]。由于[[戈弗雷·哈罗德·哈代|哈代]]的“虚假导数”概念，多根的特殊情况得以解决<ref>Aude Maignan, T.C. Scott, "Fleshing out the Generalized Lambert W Function", SIGSAM, vol. 50, no. 2, (June 2016), pp. 45-60</ref>。

Lambert "W" 函數於基礎物理問題之應用並未完全即使標準情況如 (1) 最近在原子，分子，與光學物理領域可見。<ref>T.C. Scott, A. Lüchow, D. Bressanini and J.D. Morgan III, ''The Nodal Surfaces of Helium Atom Eigenfunctions'', Phys. Rev. A 75, (2007), p. 060101, [http://scitation.aip.org/getabs/servlet/GetabsServlet?prog=normal&id=PLRAAN000075000006060101000001&idtype=cvips&gifs=yes]</ref>

== 图象 ==
<gallery caption="朗伯W函数在复平面上的图像">
Image:LambertWRe.png| ''z'' = Re(W<sub>0</sub>(''x'' + ''i'' ''y''))
Image:LambertWIm.png| ''z'' = Im(W<sub>0</sub>(''x'' + ''i'' ''y''))
Image:LambertWAbs.png| ''z'' = |W<sub>0</sub>(''x'' + ''i'' ''y'')|
Image:LambertWAll.png
</gallery>

== 计算 ==

''W''函数可以用以下的[[递推关系|递推关系]]算出：

:<math>
w_{j+1}=w_j-\frac{w_j e^{w_j}-z}{e^{w_j}(w_j+1)-\frac{(w_j+2)(w_je^{w_j}-z)}
{2w_j+2}}
</math>

==参考来源==

<references/>

== 外部链接 ==

* [http://mathworld.wolfram.com/LambertW-Function.html MathWorld]

[[Category:特殊函数|L]]