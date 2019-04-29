{{roughtranslation|time=2014-06-14T06:27:20+00:00}}
{{noteTA|G1=IT}}
{{Infobox recurring event
|name              = <!--Uses page name if omitted-->
|native_name       = 
|native_name_lang  = 
|logo              = File:IOCCC.png
|logo_alt          =
|logo_caption      = 
|logo_size         =
|image             = 
|image_size        =
|alt               =
|caption           = 
|status            = 活跃
|genre             = 程序设计赛事
|date              =
|begins            = {{start date|2017|12|29}}
|ends              = {{start date|2018|03|15}}
|frequency         = 每年
|venue         = 
|location          = 
|coordinates       = <!-- {{coord|LAT|LON|type:event|display=inline,title}} --> 
|country           = 
|years_active       = 1984–1996, 1998, 2000, 2001, 2004–2006, 2011-今
|first         = {{start date|1984}}
|founders       = [[Landon_Curt_Noll|Landon Curt Noll]], [[Larry_Bassel|Larry Bassel]]
|last              = <!-- Date of most recent event; if the event will not be held again, use {{End date|YYYY|MM|DD|df=y}} -->
|prev              = 
|next              = 
|participants      = 
|activity          = 
|leader_name       =
|patron            = 
|organised         = <!-- "organized=" also works -->
|filing            = 
|people            = 
|member            = 
|sponsor           = <!-- | or sponsors = -->
|website       = https://www.ioccc.org
|current           = 
|footnotes         = 
}}
'''国际C语言混乱代码大赛'''（IOCCC, The International Obfuscated C Code Contest）是一项国际[[程式設計|程式設計]]赛事。从1984年开始，本赛事每年举办一次（1997年、1999年、2002年、2003年和2006年例外）<ref>[http://www0.us.ioccc.org/years.html 国际C语言混乱代码大赛年度網頁]</ref>。本赛事的目的是写出最有创意和最让人难以理解的[[C语言|C语言]]代碼。

從線上提交开始，作品需要經過好幾回合的裁判審核。评判作品的标准基於濫用混亂代碼的程度（以及濫用程度的創造性）。通過最後一輪審核的作品會被歸成特別的一類以示嘉獎，例如「最濫用C[[预處理器|预處理器]]」或者「最古怪的行為」，並且發表在官方IOCCC網站。获胜作品将被公示于IOCCC网站，并以此作为奖赏。

==歷史==
IOCCC是由[[藍登·克特·諾爾|藍登·克特·諾爾]]（Landon Curt Noll）與[[拉里·貝索|拉里·貝索]]（Larry Bassel）在1984年受雇於[[國家半導體|國家半導體]]（National Semiconductor）的[[Genix|Genix]]程式移植事業群時開始的。比賽的點子是來自他們倆比較彼此有關於它們得修正的某些寫得很爛的程式碼筆記<ref>[http://www.ioccc.org/faq.html]</ref>。

==規則==
每年比賽開始前，IOCCC的比賽規則會張貼在其網站上。規則每年不同，並且會隨附上一組指導方針以試圖表達規則的精神。

這些規則通常是蓄意書寫成文，伴隨著精巧的漏洞讓參賽者有所鼓勵去發現並濫用。比賽結果就是「軟體開發過程的諷刺體」。作品佔某些規則裡頭的漏洞之便者（不管它是否通過最後一輪審核）會造成下年度比賽規則的調整（雖然常常其他微妙的漏洞又會被裁判故意放水）。

==被使用過的混亂規則==
出于該賽事的本質，作品通常运用奇怪或者不尋常的語法竅門，如利用C[[预處理器|预處理器]]去做不合设计本意的事、或者避免C程式語言正常使用的建構式，以用更曖昧難解的方式來達到同樣效果。舉例來說，下面是2004年得獎作品裡的引言：
* 為了讓事情簡單點，得避免经过C预處理器以及其他刁鑽的敘述如「if」、「for」、「do」、「while」、「switch」、以及「goto」<ref>[http://www.ioccc.org/2004/burley.hint IOCCC 2004 - Best Calculated Risk]</ref>。
* 人們還是不太確定這是否是个個有用的程式，不過這是IOCCC首見的核裂變反應<ref>[http://www.ioccc.org/2004/jdalbec.hint IOCCC 2004 - Best abuse of the Periodic table]</ref>。
* 為何不用程式來把另一段程式藏在程式中？這在當下看起來一定相當合理<ref>[http://www.ioccc.org/2004/sds.hint IOCCC 2004 - Best abuse of Indentation]</ref>。
* 該程式在C预處理器裡實現了11位元的[[算數邏輯單元|算數邏輯單元]]<ref name="cpp_abuse">[http://www.ioccc.org/2004/vik2.hint IOCCC 2004 - Best Abuse of CPP]</ref>。
* 人們找到自我递归超過650萬次的用来計算從1到1024間質數的程式<ref name="cpp_abuse" />。

許多卓著的貢獻包括：
* 將程式碼排成圖形或文字，如同[[ASCII藝術|ASCII藝術]]。
* 使用預處理器讓代碼難以閱讀。
* [[程序自修改|自我修改代碼]]。
* 最大限度濫用規則。許多年來，某些參賽作品如此公然謬用規則導致IOCCC需要於下年度重新定義某些規則。不容置疑的這是一種高度榮譽。一個範例是世界最短的[[自產生程式|自我繁殖程式]]。該作品是為零位元長度的程式，如果執行列印零位元到螢幕上（這需要某具有創造力的對[[Make|makefile]]應用才能讓它執行正確）<ref>{{cite web| url = http://www.ioccc.org/1994/smr.hint| title = smr.hint| accessdate = 2006-09-16| year = 1994| format = 純文字| publisher = IOCCC}}</ref>。

本競賽有著自然而然在C語言標準規範邊際遊走的編程本質，或者觸發極少用到的編譯器編譯後代碼路徑。這導致許多過去的作品可能無法直接通過當代編譯器，並且某些可能甚至造成該程式崩潰。

==範例==
在程式碼限定於區區幾千位元組條件下，參賽者得想盡辦法做複雜的事——例如某2004年大賽得獎者代碼實際上是個[[作業系統|作業系統]]<ref>{{cite web| url = http://www.ioccc.org/2004/gavin.hint| title = gavin.hint| accessdate = 2007-03-13| year = 2004| format = 純文字| publisher = IOCCC}}</ref>。

===計算圓周率===
下-{面}-是1988年參賽作品：透過自己佔的[[面積|面積]]來計算[[圓周率|圓周率]]<ref>[http://www0.us.ioccc.org/years.html#1988 5th International Obfuscated C Code Contest, 1988 - westley.c]</ref>，該作品是以[[K&R_C|K&R C]]寫成；代碼得做些小修改才能在[[ANSI_C|ANSI C]]下執行<ref>使用gcc情況下，以下面命令行進行編譯：gcc -traditional-cpp -o r r.c或者gcc -E r.c | sed 's/- -/--/g' > r2.c ; gcc -o r2 r2.c（原始碼檔案是r.c）</ref>。

 <source lang="c">
 #define _ -F<00||--F-OO--;
 int F=00,OO=00;main(){F_OO();printf("%1.3f\n",4.*-F/OO/OO);}F_OO()
 {
             _-_-_-_
        _-_-_-_-_-_-_-_-_
     _-_-_-_-_-_-_-_-_-_-_-_
   _-_-_-_-_-_-_-_-_-_-_-_-_-_
  _-_-_-_-_-_-_-_-_-_-_-_-_-_-_
  _-_-_-_-_-_-_-_-_-_-_-_-_-_-_
 _-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_
 _-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_
 _-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_
 _-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_
  _-_-_-_-_-_-_-_-_-_-_-_-_-_-_
  _-_-_-_-_-_-_-_-_-_-_-_-_-_-_
   _-_-_-_-_-_-_-_-_-_-_-_-_-_
     _-_-_-_-_-_-_-_-_-_-_-_
         _-_-_-_-_-_-_-_
             _-_-_-_
 }
 </source>

===飛行模擬器===
另一個範例是下-{面}-這個靈巧的飛行模擬器，為1998年IOCCC得獎作品<ref>[http://www.aerojockey.com/software/ioccc/index.html IOCCC Flight Simulator]</ref>：

<source lang="c">
 #include                                     <math.h>
 #include                                   <sys/time.h>
 #include                                   <X11/Xlib.h>
 #include                                  <X11/keysym.h>
                                           double L ,o ,P
                                          ,_=dt,T,Z,D=1,d,
                                          s[999],E,h= 8,I,
                                          J,K,w[999],M,m,O
                                         ,n[999],j=33e-3,i=
                                         1E3,r,t, u,v ,W,S=
                                         74.5,l=221,X=7.26,
                                         a,B,A=32.2,c, F,H;
                                         int N,q, C, y,p,U;
                                        Window z; char f[52]
                                     ; GC k; main(){ Display*e=
  XOpenDisplay( 0); z=RootWindow(e,0); for (XSetForeground(e,k=XCreateGC (e,z,0,0),BlackPixel(e,0))
 ; scanf("%lf%lf%lf",y +n,w+y, y+s)+1; y ++); XSelectInput(e,z= XCreateSimpleWindow(e,z,0,0,400,400,
 0,0,WhitePixel(e,0) ),KeyPressMask); for(XMapWindow(e,z); ; T=sin(O)){ struct timeval G={ 0,dt*1e6}
 ; K= cos(j); N=1e4; M+= H*_; Z=D*K; F+=_*P; r=E*K; W=cos( O); m=K*W; H=K*T; O+=D*_*F/ K+d/K*E*_; B=
 sin(j); a=B*T*D-E*W; XClearWindow(e,z); t=T*E+ D*B*W; j+=d*_*D-_*F*E; P=W*E*B-T*D; for (o+=(I=D*W+E
 *T*B,E*d/K *B+v+B/K*F*D)*_; p<y; ){ T=p[s]+i; E=c-p[w]; D=n[p]-L; K=D*m-B*T-H*E; if(p [n]+w[ p]+p[s
 ]== 0|K <fabs(W=T*r-I*E +D*P) |fabs(D=t *D+Z *T-a *E)> K)N=1e4; else{ q=W/K *4E2+2e2; C= 2E2+4e2/ K
  *D; N-1E4&& XDrawLine(e ,z,k,N ,U,q,C); N=q; U=C; } ++p; } L+=_* (X*t +P*M+m*l); T=X*X+ l*l+M *M;
   XDrawString(e,z,k ,20,380,f,17); D=v/l*15; i+=(B *l-M*r -X*Z)*_; for(; XPending(e); u *=CS!=N){
                                    XEvent z; XNextEvent(e ,&z);
                                        ++*((N=XLookupKeysym
                                          (&z.xkey,0))-IT?
                                          N-LT? UP-N?& E:&
                                          J:& u: &h); --*(
                                          DN -N? N-DT ?N==
                                          RT?&u: & W:&h:&J
                                           ); } m=15*F/l;
                                           c+=(I=M/ l,l*H
                                           +I*M+a*X)*_; H
                                           =A*r+v*X-F*l+(
                                           E=.1+X*4.9/l,t
                                           =T*m/32-I*T/24
                                            )/S; K=F*M+(
                                            h* 1e4/l-(T+
                                            E*5*T*E)/3e2
                                            )/S-X*d-B*A;
                                            a=2.63 /l*d;
                                            X+=( d*l-T/S
                                             *(.19*E +a
                                             *.64+J/1e3
                                             )-M* v +A*
                                             Z)*_; l +=
                                             K *_; W=d;
                                             sprintf(f,
                                             "%5d  %3d"
                                             "%7d",p =l
                                            /1.7,(C=9E3+
                               O*57.3)%0550,(int)i); d+=T*(.45-14/l*
                              X-a*130-J* .14)*_/125e2+F*_*v; P=(T*(47
                              *I-m* 52+E*94 *D-t*.38+u*.21*E) /1e2+W*
                              179*v)/2312; select(p=0,0,0,0,&G); v-=(
                               W*F-T*(.63*m-I*.086+m*E*19-D*25-.11*u
                                )/107e2)*_; D=cos(o); E=sin(o); } }
 </source>

==參見==

*[[混亂Perl代碼大賽|混亂Perl代碼大賽]]
*[[卑劣C代碼大賽|卑劣C代碼大賽]]

==參考資料==
<!-- See [[Wikipedia:Footnotes|Wikipedia:Footnotes]] for instructions. -->
<references />

==外部連結==

*[http://www.ioccc.org IOCCC網站]
<!-- Interwiki -->
[[Category:C语言|Category:C语言]]
[[Category:幽默與諷刺獎項|Category:幽默與諷刺獎項]]
[[Category:程序设计竞赛|Category:程序设计竞赛]]