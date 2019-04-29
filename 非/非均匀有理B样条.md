{{noteTA|G1=IT}}
[[File:NURBstatic.png|right]]]]
'''NURBS'''是'''非均匀有理B样条曲线（Non-Uniform Rational B-Splines）'''的缩写，NURBS由Versprille在其博士学位论文中提出，1991年，国际标准化组织（ISO）颁布的工业产品数据交换标准STEP中，把NURBS作为定义工业产品几何形状的唯一数学方法。1992年，国际标准化组织又将NURBS纳入到规定独立于设备的交互图形编程接口的国际标准PHIGS（程序员层次交互图形系统）中，作为PHIGS Plus的扩充部分。Bezier、有理Bezier、均匀B样条和非均匀B样条都被统一到NURBS中。
'''非均匀有理样条'''（{{lang|en|Non uniform rational B-spline}}，NURBS），是在[[计算机图形学|计算机图形学]]中常用的数学模型，用于产生和表示曲线及曲面。它为处理解析函数和模型形状提供了极大的灵活性和精确性。NURBS通常在计算机辅助设计（CAD），制造 （CAM），及工程 （CAE） 中有广泛应用。是众多行业宽泛标准中的一部分，如IGES, STEP, ACIS和PHIGS。同时在很多不同的3D建模和动画软件中也能找到NURBS的工具集。
通过计算机程序，他们可以很有效率的被处理，还允许进行简单的人机交互。NURBS 曲面是映射到三维的空间中的曲面的两个参数的函数。由控制点确定曲面的形状。NURBS 曲面可以用紧凑的形式表示简单的几何形状。T-样条和细分曲面更适合于复杂的有机形状，因为和 NURBS 曲面相比，它们减少了控制点数目。
一般情况下，编辑 NURBS 曲线和曲面有高度直观性和可预测性。控制点要么和曲线或曲面直接相连，要么表现的如同他们通过一根橡皮筋而相连。根据用户界面的类型，可以通过元素的控制点实现编辑，最明显常见的例子是贝塞尔曲线。

== 历史 ==
在计算机处理之前，设计一般是通过在纸上的手绘完成，该过程需要借助许多绘画工具。例如直尺用于绘制直线，圆规用于绘制圆形，量角器用于绘制角度。但是许多不规则形状的曲线，例如船艏，是无法通过这些工具绘制的。虽然可以通过在手绘板上徒手完成，但由于尺寸原因这种手稿无法在实际生产中得到应用。
1946年，数学家开始研究样条形状，该形状通过分段的多项式公式推导出来，因为其和机械生产中的样条相类似，{{le|I. J. Schoenberg|Isaac Jacob Schoenberg}}将其命名为样条曲线或样条函数。<ref>{{cite journal
|first = I. J.
|last = Schoenberg
|title = Spline Functions and the Problem of Graduation
|journal = [[Proceedings_of_the_National_Academy_of_Sciences_of_the_United_States_of_America|Proceedings of the National Academy of Sciences of the United States of America]]
|publisher = [[National_Academy_of_Sciences|National Academy of Sciences]]
|date = August 19, 1964
|volume = 52
|issue = 4
|pages = 947–950
|url = http://www.pnas.org/cgi/reprint/52/4/947
|format = PDF
|accessdate = 2012-02-24
|doi=10.1073/pnas.52.4.947}}</ref>
NURBS的发展始于1950年代，它是由需要像在车体和船壳中使用的[[自由曲面|自由曲面]]的数学上的精确表示的工程师们所发现的，它可以在任何技术上需要的时候精确的复制出来。以前这类曲面的表示只存在于[[设计者|设计者]]创建的[[实体模型|实体模型]]。

该发展的先驱包括：[[皮埃尔·贝塞尔|皮埃尔·贝塞尔]]（Pierre Bézier）和[[Paul_de_Casteljau|Paul de Casteljau]]两个[[法国|法国]]人， 前者曾是[[雷诺|雷诺]]的工程师，后者在[[标致|标致]]工作。贝塞尔基本是和de Casteljau独立发展的，两人互相不知道对方的工作。但是因为贝塞尔发表了他的工作的结果，今天的一般的[[计算机图形学|计算机图形学]]用户认为[[样条|样条]] -- 通过在曲线上的控制点表示的那类 - 为[[贝塞尔样条|贝塞尔样条]]，而de Casteljau的名字仅作为他为计算参数化曲面所设计的算法而为人所知。在1960年代，人们认识到[[非均匀有理B样条|非均匀有理B样条]]是[[贝塞尔曲线|贝塞尔曲线]]的一个[[廣義化|推广]]，而贝赛尔曲线可以视为均匀有理B样条。

最初NURBS仅用于汽车公司私有的[[计算机辅助设计|计算机辅助设计]]包。后来它们成为标准计算机图形包的一部分，包括[[OpenGL|OpenGL图形库]]。

NURBS曲线和曲面的实时、交互绘制最初由[[Silicon_Graphics|Silicon Graphics]]工作站于1989年提供。在1993年，CAS Berlin（一个和[[柏林工大|柏林工大]]合作的小创业公司）开发了第一个[[个人机|个人机]]上的交互式NURBS建模器，称为''[[NöRBS|NöRBS]]''。今天多数台式机上的专业计算机图形应用程序提供NURBS技术，一般通过集成一个从专用公司来的NURBS引擎。

== 使用 ==

NURBS对于[[计算机辅助设计|计算机辅助设计]]（CAD）、[[计算机辅助制造|制造]]（CAM）和[[计算机辅助工程|工程]]（CAE）是几乎无法回避的，并且是很多业界广泛采用的标准的一部分，例如[[IGES|IGES]]， [[STEP|STEP]]，和[[PHIGS|PHIGS]]。

但还是有很多它们在交互式建模中的优点和有用性的错误观念，主要是由于关于单一软件包及其用户界面的易用性而得出的猜测。
通常，据说编辑NURBS曲线和曲面是高度直观和可预测的。控制点总是直接连接到曲线或曲面上或象是通过一根橡皮筋连接。根据用户界面的类型，编辑可以通过它们各自的控制点实现，这对于[[贝塞尔曲线|贝塞尔曲线]]是最显然和最一般的，或者也可以通过高层的工具，例如样条建模或者层次结构的编辑。高层工具可以设计得很强大，并得益于NURBS创建和建立不同层次的连续性的能力：
c0连续性表示连通性，c1连续性可以视为没有尖角，而c2连续性通常称为几何连续性，视觉上也就是“光滑”的东西，用NURBS还可以达到更高阶的连续性，它们可以导致"亮度连续性"。这被新车模型的摄影师所倚重，他们热衷于展示霓虹灯在车身上的镜像。灯光可以展示出完美的光滑度，这在没有NURBS的情况下实际上是不可能。

== 定义 ==

NURBS是Non-Uniform Rational B-Splines的缩写，是非均匀有理B样条的意思。具体解释是：

Non-Uniform（非均匀性）：是指一个控制顶点的影响力的范围能够改变。当创建一个不规则曲面的时候这一点非常有用。同样，统一的曲线和曲面在透视投影下也不是无变化的，对于交互的3D建模来说这是一个严重的缺陷。

Rational（有理）：是指每个NURBS物体都可以用有理多项式形式表达式来定义。

B-Spline（B样条）：是指用路线来构建一条曲线，在一个或更多的点之间以内插值替换的。

简单地说，NURBS就是专门做曲面物体的一种造型方法。NURBS造型总是由曲线和曲面来定义的，所以要在NURBS表面里生成一条有棱角的边是很困难的。就是因为这一特点，我们可以用它做出各种复杂的曲面造型和表现特殊的效果，如人的皮肤，面貌或流线型的跑车等。

== 连续性 ==

考虑在建造中的曲面。例如马达游艇的船体，其表面通常由一些 NURBS 曲面构成。这些曲面能够被装配在一起使得它的边界线不可见，这是几何连续性的数学表达。通过研究NURBS的特性，能够得到一些高级的工具来创建一个不同层次的几何连续性条件：

位置连续性认为只要两条曲线或曲面的结束位置相吻合。曲线或曲面可能在某个角度上相吻合，形成一个尖利的拐角或边缘。

相切连续性要求曲线或曲面的结束矢量相平行或指向同样的方向，排除了锋利的边缘。因为焦点落在切线连续的边缘总是连续的，看起来很自然，这种程度的连续性通常被认为是充足的。

曲率连续性 进一步要求结束向量具有相同的长度和长度变化率。亮点落在曲率连续的边缘不会显示任何的变化，使得两个曲面显示如同一个曲面。这可以直观地认识为非常"光滑"。这一级别的连续性在创建需要许多双立方曲面构成的模型中非常有用。

几何连续性条件主要是指形状的表面 ；因为 NURBS 曲面是函数，也有可能讨论其参数导数的曲面，这就是所谓的参数连续性。一定程度的参数连续性意味着在那种程度上的几何连续性。

第一和第二级的参数连续性是为位置和相切的连续性相同的实用目的设置。然而三级参数连续性不同于曲率连续性，其参数也是连续的。在实践中，如果使用均匀 B 样条三级参数连续性更容易实现。

n级连续性的定义要求某点邻域内的n阶导数在那点相等。注意曲线或曲面的偏导数是有方向和数值的矢量，这两者都应该彼此相等。高光和反射可以揭示完美的平滑，除了G²连续性的NURBS曲面没有其他方法可以在实际中做到。

连续性和度数是有关系的。一个度数为3的等式能产生C2连续性曲线。NURBS造型通常不需要这么高度数的曲线。
一条不同片断的NURBS曲线可以用不同级别的连续性。具体来说，在同样的位置或非常靠近的地方放置一些可控点，会降低连续性的级别。两个重叠的可控点会使曲率变尖锐。三个重叠的可控点会在曲线里建立一个有角度的尖角。附加一个或两个可控点会在曲线的附近联合它们的影响力。
从可控点中删除一个离开它们，就增加了曲线的连续性的级别。在3DMAX里，Fuse（熔化）可控点会在曲线里建立一个假象的曲率或尖角。如果要恢复原状，Unfuse（反熔化）那个点就可以了。

== 技術細節 ==
[[Image:Surface_modelling.svg|250px]]
一條NURBS曲線用一個帶比重控制點和曲線的次序以及一個''節點向量''的集合定義。<ref>{{cite book
 | title = Bio-Inspired Self-Organizing Robotic Systems
 | url = http://www.springer.com/engineering/computational+intelligence+and+complexity/book/978-3-642-20759-4
 | accessdate = 2014-01-06
 | page = 9
}}</ref>NURBS是[[B-樣條|B-樣條]]和[[貝塞尔曲線|貝塞尔曲線]]和曲面兩者的推廣，其主要差別在於控制點的比重，這使它們成為''有理的''（非有理B-樣條是有理B-樣條的特殊情形）。
NURBS曲線在一個參數方向上演變，通常內部用's'參數代表，而NURBS曲面在兩個參數方向上演變。
所以，通過計算NURBS曲線的s-參數，它可以在三維空間中表示，通過計算NURBS曲面的s和t它也可以在三維空間中表示。
推廣意味著：一條貝茲曲線總是一條NURBS曲線，就像狗總是動物。反過來則不總是成立，一條NURBS曲線可以是一條貝茲曲線，就像一個動物可以是一條狗。

NURBS有用的原因有很多條：他們
* 在[[仿射變換|仿射變換]]下不變也在[[圖形投影|投影變換]]下不變；<ref>
{{citation||last=Roger|first=David F.|title=An Introduction to NURBS with Historical Perspective| publisher=Morgan Kaufmann Publishers| year=2001}}，第7.1節。(Good elementary book for NURBS and related issues.)</ref>
* 提供了標準解析形體（例如[[圓錐曲面|圓錐曲面]]）和自由曲面兩者的共同數學形式；
* 提供了設計一大類形體的靈活性；
* 減少了存儲形體的記憶體消耗（和更簡單的方法相比）；
* 可以用[[數值上穩定|數值上穩定]]和精確的[[算法|算法]]較快的計算；
* 是非有理[[B-樣條|B-樣條]]和非有理和有理[[貝茲曲線|貝茲曲線]]和曲面的推廣。

===控制點===
[[Image:NURBS_3-D_surface.gif|250px]]
節點向量是一個參數值的序列，用於決定控制點在何處和如何影響NURBS曲線。<ref>{{cite book |last=Gershenfeld |first=Neil |authorlink=Neil Gershenfeld |year=1999 |page=141 |title=The Nature of Mathematical Modeling |publisher=[[Cambridge_University_Press|Cambridge University Press]] |isbn=0-521-57095-6}}</ref>節點的個數總是等於控制點的個數加上曲線的階數。節點必須只是用於內部計算，因而一般對於軟體的[[終端用戶|終端用戶]]來說是沒有幫助的、不可編輯、甚至不可以見的。

===節點向量===
節點向量的值必須升序：下面的[[向量|向量]]是正確的：[0 0 1 2 3]，而接下來這個不是：[0 0 2 1 3]。也要注意唯一重要的因素是值之間的比例：節點向量[0 0 1 2 3]，[0 0 2 4 6]和[1 1 2 3 4]產生相同的曲線。不可以有比曲線的度數更多的重合值：節點的重複度≤度數。
對於一階NURBS，每個節點和一個控制點結對。

曲線的序大於或等於2，對應與一條線性曲線（序=2，表示一條直線），一條二次曲線（序=3)以及一條三次曲線（序=4）。數學上曲線用同階的多項式表示，一條三次曲線用3階多項式表示，其序為4。另外，控制點的個數必須等於或大於曲線的序。實踐上，3階的三次類型是表示曲線和曲面時最常用的。而4次或5次的有時候有用，特別是用於導數，更高階實際上從來不用因為他們經常導致內部數值問題並趨向於消耗更多的不必要的計算。

非有理曲線有時不夠用，例如用於表示圓。
這是表示一個XY平面上的均勻的圓的控制點，第四個參數是比重：
    cp_circle[0] = Controlpoint( 1、 0、0、     1);
    cp_circle[1] = Controlpoint( 1、 1、0、sqrt(2) / 2.0);
    cp_circle[2] = Controlpoint( 0、 1、0、     1);
    cp_circle[3] = Controlpoint(-1、 1、0、sqrt(2) / 2.0);
    cp_circle[4] = Controlpoint(-1、 0、0、     1);
    cp_circle[5] = Controlpoint(-1、-1、0、sqrt(2) / 2.0);
    cp_circle[6] = Controlpoint( 0、-1、0、     1);
    cp_circle[7] = Controlpoint( 1、-1、0、sqrt(2) / 2.0);
    cp_circle[8] = Controlpoint( 1、 0、0、     1);

== 产生方法 ==

AutoCAD用 SPLINE 命令创建样条曲线即 NURBS 曲线。还提供用 PEDIT 命令，平滑多段线（POLYLINE）拟合生成近似样条曲线，以下称为“样条拟合多段线”。这种曲线不是真正意义上的样条曲线，而是由若干直线（曲线）段构成的多段线，逼近于样条曲线。但使用 SPLINE 命令可把这种二维和三维样条拟合多段线转换为样条曲线。
用SPLINE命令创建的样条曲线和编辑平滑多段线生成的样条拟合多段线相比，有以下不同：
样条曲线显然要比样条拟合多段线精确的多。在工程应用中，样条拟合多段线不能作为数学分析的基础，不能在曲线上，生成切线、法线或提取曲线上的点位数据。

== 參見 ==
*[[B樣條|B樣條]]

==参考資料==
{{Reflist}}

*{{cite book |last1=Piegl|first1=Les|last2=Tiller|first2=Wayne|title=The NURBS Book|publisher=Springer-Verlag|year=1995–1997|edition=2nd ed}} The main reference for Bézier, B-Spline and NURBS; chapters on mathematical representation and construction of curves and surfaces, interpolation, shape modification, programming concepts.
*Dr. Thomas Sederberg, BYU ''NURBS'', http://cagd.cs.byu.edu/~557/text/ch5.pdf
*Dr. Lyle Ramshaw. ''Blossoming: A connect-the-dots approach to splines'', Research Report 19, Compaq Systems Research Center, Palo Alto, CA, June 1987.

== 外部链接 ==
*[http://www.cs.wpi.edu/~matt/courses/cs563/talks/nurbs.html About Nonuniform Rational B-Splines - NURBS]
*[http://www.tsplines.com TSplines is a Superset of NURBS]
*[http://freeitsolutions.com/3ds/?search=nurb NURBS with 3ds max tutorials] (en)
*[http://ibiblio.org/e-notes/Splines/Intro.htm An Interactive Introduction to Splines]

[[Category:样条|Category:样条]]