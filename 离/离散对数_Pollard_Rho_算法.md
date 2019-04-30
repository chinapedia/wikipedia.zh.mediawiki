{{roughtranslation|time=2018-04-17}}
'''离散对数 Pollard Rho 算法''' 是 [[John_Pollard_(mathematician)|John Pollard]] 在1978年发明的解决 [[离散对数|离散对数]] 问题的算法, 区别于解决 [[整数分解|整数分解]] 问题的同名算法。

算法的目标是求 <math>\gamma</math> 使得 <math>\alpha ^ \gamma = \beta</math>，其中 <math>\beta</math> 属于一个由 <math>\alpha</math> 生成的 [[循环群|循环群]] <math>G</math>。该算法寻找 <math>a</math>, <math>b</math>,  <math>A</math>, <math>B</math> 使得 <math>\alpha^a \beta^b = \alpha^A \beta^B</math>。若他们基于的群是一个 <math>n</math> 阶的循环群，则 <math>\gamma</math> 是方程 <math>(B-b)\gamma = (a-A) \pmod{n}</math> 的其中一个解。

为求得 <math>a</math>, <math>b</math>,  <math>A</math>, <math>B</math>， 该算法使用 [[Floyd判圈算法|Floyd判圈算法]] 在数列 <math>x_i = \alpha^{a_i} \beta^{b_i}</math> 中寻找一个环。 假设映射 <math>f: x_i \mapsto x_{i+1}</math> 是近似于随机的，则有可能在约 <math>\sqrt{\frac{\pi n}{2}}</math> 步后发现一个环。可使用一下规则来生成一个此类映射：将 <math>G</math> 分割为三个不相交的子集 <math>S_0</math>，<math>S_1</math>
，<math>S_2</math> ，且其所含元素数量大致相等，如果 <math>x_i \in S_0</math> 则将 <math>a</math> 和 <math>b</math> 加倍； 如果 <math>x_i \in S_1</math> 则将 <math>a</math> 自增； 如果 <math>x_i \in S_2</math> 则将 <math>b</math> 自增。

==算法==
使 {{mvar|G}} 是一个 {{mvar|p}} 阶的 [[循环群|循环群]], 且有 <math>\alpha, \beta\in G</math>, 以及一个分割 <math>G = S_0\cup S_1\cup S_2</math>, 定义映射 <math>f:G\to G</math> 

:<math>
f(x) = \begin{cases}
\beta x & x\in S_0\\
x^2 & x\in S_1\\
\alpha x & x\in S_2
\end{cases}
</math>

并据以下方式定义映射 <math>g:G\times\mathbb{Z}\to\mathbb{Z}</math> 和 <math>h:G\times\mathbb{Z}\to\mathbb{Z}</math> 

:<math>\begin{align}
g(x,n) &= \begin{cases}
n & x\in S_0\\
2n \pmod p & x\in S_1\\
n+1 \pmod p & x\in S_2
\end{cases}
\\
h(x,n) &= \begin{cases}
n+1 \pmod p & x\in S_0\\
2n \pmod p & x\in S_1\\
n & x\in S_2
\end{cases}
\end{align}</math>

  '''输入''' ''a'': a 是 ''G'' 的生成元, ''b'': ''G'' 的一个元素
  '''输出''' 整数 ''x'' 使得 ''a<sup>x</sup>'' = ''b'', 或者失败
 
  初始化 ''a''<sub>0</sub> ← 0, ''b''<sub>0</sub> ← 0, ''x''<sub>0</sub> ← 1 ∈ ''G'', 
 
  ''i'' ← 1
  '''loop'''
      ''x<sub>i</sub>'' ← ''f''(''x''<sub>''i''-1</sub>), 
      ''a<sub>i</sub>'' ← ''g''(''x''<sub>''i''-1</sub>, ''a''<sub>''i''-1</sub>), 
      ''b<sub>i</sub>'' ← ''h''(''x''<sub>''i''-1</sub>, ''b''<sub>''i''-1</sub>)
 
      ''x''<sub>2''i''</sub> ← ''f''(''f''(''x''<sub>2''i''-2</sub>)), 
      ''a''<sub>2''i''</sub> ← ''g''(''f''(''x''<sub>2''i''-2</sub>), ''g''(''x''<sub>2''i''-2</sub>, ''a''<sub>2''i''-2</sub>)), 
      ''b''<sub>2''i''</sub> ← ''h''(''f''(''x''<sub>2''i''-2</sub>), ''h''(''x''<sub>2''i''-2</sub>, ''b''<sub>2''i''-2</sub>))
 
      '''if''' ''x<sub>i</sub>'' = ''x''<sub>2''i''</sub> '''then'''
          ''r'' ← ''b<sub>i</sub>'' - ''b''<sub>2''i''</sub>
          '''if''' r = 0 '''return failure'''
          ''x'' ← ''r''<sup>−1</sup>(''a''<sub>2''i''</sub> - ''a<sub>i</sub>'') mod ''p''
          '''return''' ''x''
      '''else''' <u># ''x<sub>i</sub>'' ≠ ''x''<sub>2''i''</sub></u>
          ''i'' ← ''i''+1, 
          '''break loop'''
      '''end if'''
   '''end loop'''

==举例==
考虑，举例来说，一个由 2 模 <math>N=1019</math> 生成的群(群的阶是<math>n=1018</math>，2是生成元，生成群的元素模1019同余)。这个算法可由以下 [[C++|C++]] 程序实现。

<source lang="cpp">
 #include <stdio.h>
 
 const int n = 1018, N = n + 1;  /* N = 1019 -- 素数       */
 const int alpha = 2;            /* 生成元                 */
 const int beta = 5;             /* 2^{10} = 1024 = 5 (N) */
 
 void new_xab( int& x, int& a, int& b ) {
   switch( x%3 ) {
   case 0: x = x*x     % N;  a =  a*2  % n;  b =  b*2  % n;  break;
   case 1: x = x*alpha % N;  a = (a+1) % n;                  break;
   case 2: x = x*beta  % N;                  b = (b+1) % n;  break;
   }
 }
 
 int main(void) {
   int x=1, a=0, b=0;
   int X=x, A=a, B=b;
   for(int i = 1; i < n; ++i ) {
     new_xab( x, a, b );
     new_xab( X, A, B );
     new_xab( X, A, B );
     printf( "%3d  %4d %3d %3d  %4d %3d %3d\n", i, x, a, b, X, A, B );
     if( x == X ) break;
   }
   return 0;
 }
</source>

结果如下 (已截断):

  i     x   a   b     X   A   B
 ------------------------------
  1     2   1   0    10   1   1
  2    10   1   1   100   2   2
  3    20   2   1  1000   3   3
  4   100   2   2   425   8   6
  5   200   3   2   436  16  14
  6  1000   3   3   284  17  15
  7   981   4   3   986  17  17
  8   425   8   6   194  17  19
 ..............................
 48   224 680 376    86 299 412
 49   101 680 377   860 300 413
 50   505 680 378   101 300 415
 51  1010 681 378  1010 301 416

可见 <math>2^{681} 5^{378} = 1010 = 2^{301} 5^{416} \pmod{1019}</math> 以及 <math>(416-378)\gamma = 681-301 \pmod{1018}</math>。
正如预期，其中 <math>\gamma_1=10</math> 是一个解。由于 <math>n=1018</math> 不是素数，因此存在另一个解 <math>\gamma_2=519</math>，使得 <math>2^{519} = 1014 = -5\pmod{1019}</math> 成立。

==复杂度==
时间复杂度近似于 <math>\mathcal{O}(\sqrt{n})</math>。如果配合使用算法 [[Pohlig–Hellman_algorithm|Pohlig-Hellman algorithm]]，则整体时间复杂度近似于 <math>\mathcal{O}(\sqrt{p})</math>， 其中 <math>p</math> 是 <math>n</math> 的最大质因数。

==参考文献==
*{{cite journal |first=J. M. |last=Pollard |title=Monte Carlo methods for index computation (mod ''p'') |journal=[[Mathematics_of_Computation|Mathematics of Computation]] |volume=32 |year=1978 |issue=143 |pages=918–924 |doi= 10.2307/2006496 }}
*{{cite book |first=Alfred J. |last=Menezes |first2=Paul C. |last2=van Oorschot |first3=Scott A. |last3=Vanstone |chapterurl=http://www.cacr.math.uwaterloo.ca/hac/about/chap3.pdf |title=Handbook of Applied Cryptography |chapter=Chapter 3 |year=2001 |location= |publisher= |isbn= }}

{{Number-theoretic algorithms}}

[[Category:Logarithms|Category:Logarithms]]
[[Category:Number_theoretic_algorithms|Category:Number theoretic algorithms]]