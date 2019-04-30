<!--{{expert needed|1=Engineering|date=June 2018}}-->
[[File:Nyquist_grid.svg|thumb]]
'''等M圓'''及'''等N圓'''（M-circles and N-circles）英文也稱為是Hall circles，是[[控制理论|控制理论]]中利用開迴路傳遞函數的[[奈奎斯特圖|奈奎斯特圖]]（或[[尼柯尔斯图|尼柯尔斯图]]）來求得其[[閉迴路傳遞函數|閉迴路傳遞函數]]數值的繪圖工具。此作法最早是由Albert C. Hall在其控制理論的論文中提出<ref>{{Cite book|url=https://www.worldcat.org/oclc/857968901|title=The analysis and synthesis of linear servomechanisms|last=C.|first=Hall, Albert|date=1943|publisher=Technology Press, Massachusetts Institute of Technology|isbn=9780262080736|location=Cambridge|oclc=857968901}}</ref>。

== 建構方式 ==
考慮閉迴路線性控制系統，其開迴路[[傳遞函數|傳遞函數]]為<math>G(s)</math>，反饋路徑的增益為1。其閉迴路傳遞函數為<math display="inline"> T(s) = \frac{G(s)}{1+G(s)} </math>。 

若要確認''T''(''s'')的穩定性，可以用開迴路傳遞函數''G''(''s'')的[[奈奎斯特圖|奈奎斯特圖]]配合[[奈奎斯特稳定判据|奈奎斯特稳定判据]]來確認。不過若只靠奈奎斯特圖，無法知道''T''(''s'')的數值。為了要在G(s)平面上得到這些資訊，Hall在G(s)平面加上了使''T''(''s'')有固定大小以及有固定相位的二組曲線。

假設一正值''M''表示固定的大小，令G(s)為''z''，滿足<math display="block"> M = |T(s)| = \frac{|G(s)|}{|1+G(s)|} = \frac{|z|}{|1+z|} </math>的點是那些在''G''(''s'')平面上和0的距離以及和-1的距離比例為''M''倍的點。這些符合條件的點''z''的軌跡為{{link-en|阿波羅尼斯圓|circles of Apollonius}}，在控制系統中稱為等M圖。

若假設一正值''N''表示相位角，滿足<math display="block"> N = \arg \left[\frac{G(s)}{1+G(s)}\right] = \arg[G(s)] - \arg[1+G(s)] = \arg[z] - \arg[1+z] </math>的點<!--的是點are given by the points z in the ''G''(''s'')-plane such that the angle between -1 and z and the angle between 0 and z is constant. In other words, the angle opposed to the line segment between -1 and 0 must be constant. -->。滿足此條件的點z的軌跡為圓弧<ref>{{Cite web|url=https://www.cut-the-knot.org/pythagoras/Munching/inscribed.shtml|title=Munching on Inscribed Angles|last=|first=|date=|website=cut-the-knot|archive-url=|archive-date=|dead-url=|access-date=2018-05-25}}</ref>，在控制系統中稱為等N圖。
== 用法 ==
[[File:Nichols_chart.svg|thumb]]
若要使用此方法，會在開迴路傳遞函數的奈奎斯特圖上重疊不同數值的等M圓及等N圓，根據傳遞函數和等M圓及等N圓的交點即知道閉迴路傳遞函數的大小及相位。

等M圓及等N圓也可以和[[尼柯尔斯图|尼柯尔斯图]]一起使用，不過等M圓及等N圓會進行坐標轉換，其縱軸會是<math> 20 \log_{10}(|G(s)|) </math>，橫軸是<math> \arg(G(s))</math>。尼柯尔斯图的好處是調整開迴路傳遞函數時，只要將曲線往上移即可。

== 相關條目 ==
* [[奈奎斯特圖|奈奎斯特圖]]
* [[尼柯尔斯图|尼柯尔斯图]]

== 參考資料 ==
{{Reflist}}
* {{Cite book|url=https://www.worldcat.org/oclc/46619221|title=Modern control engineering|last=Katsuhiko|first=Ogata|date=2002|publisher=Prentice Hall|isbn=0130609072|edition=4th|location=Upper Saddle River, NJ|oclc=46619221}}
* {{Cite book|url=https://www.worldcat.org/oclc/154798791|title=Control systems engineering|last=S.|first=Nise, Norman|date=2008|publisher=Wiley|year=|isbn=9780471794752|edition=5th|location=Hoboken, NJ|pages=|oclc=154798791}}

[[Category:控制理论|Category:控制理论]]
[[Category:算法|Category:算法]]
[[Category:控制工程|Category:控制工程]]