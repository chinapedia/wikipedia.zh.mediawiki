{{no footnotes|time=2018-07-05T15:52:56+00:00}}
{{cleanup-jargon|time=2018-07-05T11:01:15+00:00}}
'''高級Z轉換'''（英語：Advanced z-transform，或 modified z-transform）是[[Z轉換|Z轉換]]的延伸，是[[數學|數學]]及[[信號處理|信號處理]]領域中的工具，它將不是[[取樣週期|取樣週期]]整數倍的延遲考慮進去。具有以下形式

:<math>F(z, m) = \sum_{k=0}^{\infty} f(k T + m)z^{-k}</math>

其中

* T為取樣週期

* m為延遲參數（delay parameter），<math>0 \leq m < T</math>

== 性質 ==
如果延遲參數m固定，則Z轉換具有的性質在高級Z轉換也都成立。

=== 線性 ===
:<math>\mathcal{Z} \left\{ \sum_{k=1}^{n} c_k f_k(t) \right\} = \sum_{k=1}^{n} c_k F_k(z, m)</math>

=== 時移 ===
:<math>\mathcal{Z} \left\{ u(t - n T)f(t - n T) \right\} = z^{-n} F(z, m)</math>

=== Z域的尺度性質 ===
:<math>\mathcal{Z} \left\{ f(t) e^{-a\, t} \right\} = e^{-a\, m} F(e^{a\, T} z, m)</math>

=== 微分 ===
:<math>\mathcal{Z} \left\{ t^y f(t) \right\} = \left(-T z \frac{d}{dz} + m \right)^y F(z, m)</math>

=== 終值定理 ===
:<math>\lim_{k \to \infty} f(k T + m) = \lim_{z \to 1} (1-z^{-1})F(z, m)</math>

== 範例 ==
以下計算 <math>f(t) = \cos(\omega t)</math>的高級Z轉換：

:<math>\begin{align}
F(z, m) & = \mathcal{Z} \left\{ \cos \left(\omega \left(k T + m \right) \right) \right\} \\
        & = \mathcal{Z} \left\{ \cos (\omega k T) \cos (\omega m) - \sin (\omega k T) \sin (\omega m) \right\} \\
        & = \cos(\omega m) \mathcal{Z} \left\{ \cos (\omega k T) \right\} - \sin (\omega m) \mathcal{Z} \left\{ \sin (\omega k T) \right\} \\
        & = \cos(\omega m) \frac{z \left(z - \cos (\omega T) \right)}{z^2 - 2z \cos(\omega T) + 1} - \sin(\omega m) \frac{z \sin(\omega T)}{z^2 - 2z \cos(\omega T) + 1} \\
        & = \frac{z^2 \cos(\omega m) - z \cos(\omega(T - m))}{z^2 - 2z \cos(\omega T) + 1}
\end{align}</math>

若 <math>m=0</math>，則<math>F(z, m)</math>簡化為

:<math>F(z, 0) = \frac{z^2 - z \cos(\omega T)}{z^2 - 2z \cos(\omega T) + 1}</math>

正是<math>f(t) = \cos(\omega t)</math>的Z轉換

== 參考文獻 ==

* Eliahu Ibrahim Jury, ''Theory and Application of the z-Transform Method'', Krieger Pub Co, 1973. {{ISBN|0-88275-122-0}}.
{{DSP}}
[[分類:變換|分類:變換]]