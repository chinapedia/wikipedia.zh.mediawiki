{{Infobox Unicode block
|blockname  = Mongolian
|rangestart = 1800
|rangeend   = 18AF
|script1 = [[蒙古文|蒙古文]]（153个字符）
|script2 = 通用（3个字符）
|alphabets  = 蒙古文（[[胡都木蒙古文|胡都木]]、[[托忒蒙古文|托忒]]）<br />[[满文|满文]]<br />[[锡伯文|锡伯文]]
|3_0        = 155
|5_1        = 1
|note = <ref>{{cite web|url=http://www.unicode.org|title=Unicode character database|work=The Unicode Standard|accessdate=2018-01-30}}</ref><ref>{{cite web|url=http://www.unicode.org/versions/enumeratedversions.html|title=Enumerated Versions of The Unicode Standard|work=The Unicode Standard|accessdate=2018-01-30}}</ref>
}}
{{Contains Mongolian text}}
{{Contains Manchu text}}
{{Contains Xibe text}}
'''蒙古文Unicode区段'''是包含[[胡都木蒙古文|胡都木蒙古文]]{{NoteTag|Unicode标准中，将胡都木蒙古文称为“Mongolian”，将托忒蒙古文称为“Todo”。}}、[[托忒蒙古文|托忒蒙古文]]、[[满文|满文]]、[[锡伯文|锡伯文]]字符的[[Unicode区段|Unicode区段]]。<ref name="Standard">{{Cite web|url=http://www.unicode.org/versions/Unicode10.0.0/ch13.pdf#G27803|title=The Unicode® Standard Version 10.0 – Core Specification|publisher=The Unicode Consortium|accessdate=2018-01-30}}</ref>{{rp|528}}其书写方向为{{TextDir|tb-lr|full}}。在Unicode官方的字符表中该区段的字符被逆时针旋转90度显示<ref name="Standard"/>{{rp|529}}<ref name="U1800">{{Cite web|title=Mongolian code chart|url=http://www.unicode.org/charts/PDF/U1800.pdf|publisher=The Unicode Consortium|accessdate=2018-01-30}}</ref>。

胡都木蒙古文和满文{{NoteTag|满文中的阿礼嘎礼字母请参看[[满文#转写梵文藏文字母|满文#转写梵文藏文字母]]。}}使用的字符中包括一些用于翻译佛教经文的[[阿礼嘎礼字母|阿礼嘎礼字母]]。<ref name="Standard"/>{{rp|528}}

Unicode标准中为该区段的字符定义了数十个变体序列，用以在无法通过算法自动判断时指定具体应显示的{{le|变体形式 (Unicode)|Variant form (Unicode)|变体形式}}。<ref name="Variant">{{Cite web|url=http://www.unicode.org/Public/UNIDATA/StandardizedVariants.txt|title=Unicode Character Database: Standardized Variation Sequences|publisher=The Unicode Consortium|accessdate=2018-01-30}}</ref>

==区段内容==
本区段中发音不同但书写形状相同的字母被看作不同的字母，具有不同的码位。例如胡都木蒙古文字母O编码为U+1823，U编码为U+1824，但表现出的形状是一样的。<ref name="Standard"/>{{rp|530}}
{{Unicode chart Mongolian}}

== 变体形式 ==
本区段的同一个字符可能有多个变体，Unicode使用[[自由变体选择符|自由变体选择符]]（FVS，Free Variant Selector）来选择不同变体。FVS有3个，分别是FVS1（U+180B）、FVS2（U+180C）、FVS3（U+180D）。在特定字符的后面加上FVS能够改变字符的形态，这样的字符+FVS的组合称为标准变体（standardized variant）。<ref name="Standard"/>{{rp|532}}<ref name="Biligsaikhan">{{Cite journal|url=http://www.colips.org/journals/volume21/21.1.3-Biligsaikhan.pdf|title=A Study of Traditional Mongolian Script Encodings and Rendering: Use of Unicode in OpenType fonts|author1=Biligsaikhan Batjargal|author2=Garmaabazar Khaltarkhuu|author3=Fuminori Kimura|author4=Akira Maeda|journal=International Journal on Asian Language Processing|publisher=中文与东方语文信息处理学会|volume=21(1)|date=2011}}</ref>{{rp|33,34}}全部的标准变体见下表。<ref name="abkai">{{Cite web|title=满文转写|url=http://abkai.net/core/zh/manchu/manchu-transliteration/|archiveurl=https://web.archive.org/web/20170713233652/http://abkai.net/core/zh/manchu/manchu-transliteration/|archivedate=2017-07-13|publisher=太清网}}</ref>
{|
|-valign="top"
|
{| class="wikitable"
|+ 元音
! 字母 !! 变体 !! Unicode !! 独立形式 !! 字首形式 !! 字中形式 !! 字尾形式
|-
| rowspan="3" align="center" | '''A'''<br />a || rowspan="3" align="center" | '''基本''' || '''1820''' || {{MongolUnicode|valign=middle|ᠠ}} || {{MongolUnicode|valign=middle|ᠠ‍}} || {{MongolUnicode|valign=middle|‍ᠠ‍}} || {{MongolUnicode|valign=middle|‍ᠠ}} 
|-
| 1820 180B || {{MongolUnicode|valign=middle|ᠠ᠋}} || style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠠ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠠ᠋}} 
|-
| 1820 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠠ᠌‍}} || style="background: silver" | 
|-
| rowspan="6" align="center" | '''E'''<br />e || rowspan="2" align="center" | '''基本''' || '''1821''' || {{MongolUnicode|valign=middle|ᠡ}} || {{MongolUnicode|valign=middle|ᠡ‍}} || {{MongolUnicode|valign=middle|‍ᠡ‍}} || {{MongolUnicode|valign=middle|‍ᠡ}} 
|-
| 1821 180B || style="background: silver" | || {{MongolUnicode|valign=middle|ᠡ᠋‍}} || style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠡ᠋}} 
|-
| rowspan="2" align="center" | [[托忒蒙古文|托忒]] || 1844 || {{MongolUnicode|valign=middle|ᡄ}} || {{MongolUnicode|valign=middle|ᡄ‍}} || {{MongolUnicode|valign=middle|‍ᡄ‍}} || {{MongolUnicode|valign=middle|‍ᡄ}} 
|-
| 1844 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡄ᠋‍}} || style="background: silver" | 
|-
| rowspan="2" align="center" | [[锡伯文|锡伯文]] || 185D || {{MongolUnicode|valign=middle|ᡝ}} || {{MongolUnicode|valign=middle|ᡝ‍}} || {{MongolUnicode|valign=middle|‍ᡝ‍}} || {{MongolUnicode|valign=middle|‍ᡝ}} 
|-
| 185D 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡝ᠋‍}} || {{MongolUnicode|valign=middle|‍ᡝ᠋}} 
|-
| align="center" | '''EE'''<br />é || align="center" | '''基本''' || '''1827''' || {{MongolUnicode|valign=middle|ᠧ}} || {{MongolUnicode|valign=middle|ᠧ‍}} || {{MongolUnicode|valign=middle|‍ᠧ‍}} || {{MongolUnicode|valign=middle|‍ᠧ}} 
|-
| rowspan="11" align="center" | '''I'''<br />i || rowspan="2" align="center" | '''基本''' || '''1822''' || {{MongolUnicode|valign=middle|ᠢ}} || {{MongolUnicode|valign=middle|ᠢ‍}} || {{MongolUnicode|valign=middle|‍ᠢ‍}} || {{MongolUnicode|valign=middle|‍ᠢ}} 
|-
| 1822 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠢ᠋‍}} || style="background: silver" |
|-
| rowspan="2" align="center" | 托忒 || 1845 || {{MongolUnicode|valign=middle|ᡅ}} || {{MongolUnicode|valign=middle|ᡅ‍}} || {{MongolUnicode|valign=middle|‍ᡅ‍}} || {{MongolUnicode|valign=middle|‍ᡅ}} 
|-
| 1825 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡅ᠋‍}} || style="background: silver" |
|-
| rowspan="3" align="center" | 锡伯文 || 185E || {{MongolUnicode|valign=middle|ᡞ}} || {{MongolUnicode|valign=middle|ᡞ‍}} || {{MongolUnicode|valign=middle|‍ᡞ‍}} || {{MongolUnicode|valign=middle|‍ᡞ}} 
|-
| 185E 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡞ᠋‍}} || {{MongolUnicode|valign=middle|‍ᡞ᠋}} 
|-
| 185E 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡞ᠌‍}} || {{MongolUnicode|valign=middle|‍ᡞ᠌}} 
|-
| rowspan="4" align="center" | [[满文|满文]] || 1873 || {{MongolUnicode|valign=middle|ᡳ}} || {{MongolUnicode|valign=middle|ᡳ‍}} || {{MongolUnicode|valign=middle|‍ᡳ‍}} || {{MongolUnicode|valign=middle|‍ᡳ}} 
|-
| 1873 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡳ᠋‍}} || {{MongolUnicode|valign=middle|‍ᡳ᠋}} 
|-
| 1873 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡳ᠌‍}} || {{MongolUnicode|valign=middle|‍ᡳ᠌}} 
|-
| 1873 180D || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡳ᠍‍}} || style="background: silver" |
|-
| align="center" | '''IY''' || align="center" | 锡伯文 || 185F || {{MongolUnicode|valign=middle|ᡟ}} || {{MongolUnicode|valign=middle|ᡟ‍}} || {{MongolUnicode|valign=middle|‍ᡟ‍}} || {{MongolUnicode|valign=middle|‍ᡟ}} 
|-
| rowspan="4" align="center" | '''O'''<br />o || rowspan="2" align="center" | '''基本''' || '''1823''' || {{MongolUnicode|valign=middle|ᠣ}} || {{MongolUnicode|valign=middle|ᠣ‍}} || {{MongolUnicode|valign=middle|‍ᠣ‍}} || {{MongolUnicode|valign=middle|‍ᠣ}}
|-
| 1823 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠣ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠣ᠋}} 
|-
| rowspan="2" align="center" | 托忒 || 1846 || {{MongolUnicode|valign=middle|ᡆ}} || {{MongolUnicode|valign=middle|ᡆ‍}} || {{MongolUnicode|valign=middle|‍ᡆ‍}} || {{MongolUnicode|valign=middle|‍ᡆ}} 
|-
| 1846 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡆ᠋‍}} || style="background: silver" | 
|-
| rowspan="5" align="center" | '''OE'''<br />ö || rowspan="3" align="center" | '''基本''' || '''1825''' || {{MongolUnicode|valign=middle|ᠥ}} || {{MongolUnicode|valign=middle|ᠥ‍}} || {{MongolUnicode|valign=middle|‍ᠥ‍}} || {{MongolUnicode|valign=middle|‍ᠥ}}
|-
| 1825 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠥ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠥ᠋}} 
|-
| 1825 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠥ᠌‍}} || style="background: silver" | 
|-
| rowspan="2" align="center" | 托忒 || 1848 || {{MongolUnicode|valign=middle|ᡈ}} || {{MongolUnicode|valign=middle|ᡈ‍}} || {{MongolUnicode|valign=middle|‍ᡈ‍}} || {{MongolUnicode|valign=middle|‍ᡈ}} 
|-
| 1848 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡈ᠋‍}} || style="background: silver" | 
|-
| rowspan="6" align="center" | '''U'''<br />u || rowspan="2" align="center" | '''基本''' || '''1824''' || {{MongolUnicode|valign=middle|ᠤ}} || {{MongolUnicode|valign=middle|ᠤ‍}} || {{MongolUnicode|valign=middle|‍ᠤ‍}} || {{MongolUnicode|valign=middle|‍ᠤ}}
|-
| 1824 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠤ᠋‍}} || style="background: silver" | 
|-
| rowspan="3" align="center" | 托忒 || 1847 || {{MongolUnicode|valign=middle|ᡇ}} || {{MongolUnicode|valign=middle|ᡇ‍}} || {{MongolUnicode|valign=middle|‍ᡇ‍}} || {{MongolUnicode|valign=middle|‍ᡇ}} 
|-
| 1847 180B || {{MongolUnicode|valign=middle|ᡇ᠋}} || style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡇ᠋‍}} || {{MongolUnicode|valign=middle|‍ᡇ᠋}} 
|-
| 1847 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡇ᠌‍}} || style="background: silver" | 
|-
| align="center" | 锡伯文 || 1861 || {{MongolUnicode|valign=middle|ᡡ}} || {{MongolUnicode|valign=middle|ᡡ‍}} || {{MongolUnicode|valign=middle|‍ᡡ‍}} || {{MongolUnicode|valign=middle|‍ᡡ}} 
|-
| rowspan="7" align="center" | '''UE'''<br />ü || rowspan="3" align="center" | '''基本''' || '''1826''' || {{MongolUnicode|valign=middle|ᠦ}} || {{MongolUnicode|valign=middle|ᠦ‍}} || {{MongolUnicode|valign=middle|‍ᠦ‍}} || {{MongolUnicode|valign=middle|‍ᠦ}} 
|-
| 1826 180B || {{MongolUnicode|valign=middle|ᠦ᠋}} || style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠦ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠦ᠋}} 
|-
| 1826 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠦ᠌‍}} || style="background: silver" | 
|-
| rowspan="2" align="center" | 托忒 || 1849 || {{MongolUnicode|valign=middle|ᡉ}} || {{MongolUnicode|valign=middle|ᡉ‍}} || {{MongolUnicode|valign=middle|‍ᡉ‍}} || {{MongolUnicode|valign=middle|‍ᡉ}} 
|-
| 1849 180B || {{MongolUnicode|valign=middle|ᡉ᠋}} || style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡉ᠋‍}} || style="background: silver" | 
|-
| rowspan="2" align="center" | 锡伯文 || 1860 || {{MongolUnicode|valign=middle|ᡠ}} || {{MongolUnicode|valign=middle|ᡠ‍}} || {{MongolUnicode|valign=middle|‍ᡠ‍}} || {{MongolUnicode|valign=middle|‍ᡠ}} 
|-
| 1860 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡠ᠋‍}} || {{MongolUnicode|valign=middle|‍ᡠ᠋}} 
|-
|}
|
{| class="wikitable"
|+ 辅音
! 字母 !! 变体 !! Unicode !! 独立形式 !! 字首形式 !! 字中形式 !! 字尾形式
|-
| rowspan="3" align="center" | '''N'''<br />n || rowspan="3" align="center" | '''基本''' || '''1828''' || {{MongolUnicode|valign=middle|ᠨ}} || {{MongolUnicode|valign=middle|ᠨ‍}} || {{MongolUnicode|valign=middle|‍ᠨ‍}} || {{MongolUnicode|valign=middle|‍ᠨ}} 
|-
| 1828 180B || style="background: silver" | || {{MongolUnicode|valign=middle|ᠨ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠨ᠋‍}} || style="background: silver" | 
|-
| 1828 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠨ᠌‍}} || {{MongolUnicode|valign=middle|‍ᠨ᠌}} 
|-
| rowspan="3" align="center" | '''NG'''<br />ŋ || align="center" | '''基本''' || '''1829''' || {{MongolUnicode|valign=middle|ᠩ}} || {{MongolUnicode|valign=middle|ᠩ‍}} || {{MongolUnicode|valign=middle|‍ᠩ‍}} || {{MongolUnicode|valign=middle|‍ᠩ}} 
|-
| align="center" | 托忒 || 184A 180B || {{MongolUnicode|valign=middle|ᡊ}} || {{MongolUnicode|valign=middle|ᡊ‍}} || {{MongolUnicode|valign=middle|‍ᡊ‍}} || {{MongolUnicode|valign=middle|‍ᡊ}} 
|-
| align="center" | 锡伯文 || 1862 180B || {{MongolUnicode|valign=middle|ᡢ}} || {{MongolUnicode|valign=middle|ᡢ‍}} || {{MongolUnicode|valign=middle|‍ᡢ‍}} || {{MongolUnicode|valign=middle|‍ᡢ}} 
|-
| rowspan="3" align="center" | '''B'''<br />b || rowspan="2" align="center" | '''基本''' || '''182A''' || {{MongolUnicode|valign=middle|ᠪ}} || {{MongolUnicode|valign=middle|ᠪ‍}} || {{MongolUnicode|valign=middle|‍ᠪ‍}} || {{MongolUnicode|valign=middle|‍ᠪ}} 
|-
| 182A 180B || colspan="3" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠪ}} 
|-
| align="center" | 托忒 || 184B || {{MongolUnicode|valign=middle|ᡋ}} || {{MongolUnicode|valign=middle|ᡋ‍}} || {{MongolUnicode|valign=middle|‍ᡋ‍}} || {{MongolUnicode|valign=middle|‍ᡋ}} 
|-
| rowspan="3" align="center" | '''P'''<br />p || align="center" | '''基本''' || '''182B''' || {{MongolUnicode|valign=middle|ᠫ}} || {{MongolUnicode|valign=middle|ᠫ‍}} || {{MongolUnicode|valign=middle|‍ᠫ‍}} || {{MongolUnicode|valign=middle|‍ᠫ}} 
|-
| align="center" | 托忒 || 184C || {{MongolUnicode|valign=middle|ᡌ}} || {{MongolUnicode|valign=middle|ᡌ‍}} || {{MongolUnicode|valign=middle|‍ᡌ‍}} || {{MongolUnicode|valign=middle|‍ᡌ}} 
|-
| align="center" | 锡伯文 || 1866 || {{MongolUnicode|valign=middle|ᡦ}} || {{MongolUnicode|valign=middle|ᡦ‍}} || {{MongolUnicode|valign=middle|‍ᡦ‍}} || {{MongolUnicode|valign=middle|‍ᡦ}} 
|-
| rowspan="6" align="center" | '''Q'''<br />q/k || rowspan="4" align="center" | '''基本''' || '''182C''' || {{MongolUnicode|valign=middle|ᠬ}} || {{MongolUnicode|valign=middle|ᠬ‍}} || {{MongolUnicode|valign=middle|‍ᠬ‍}} || {{MongolUnicode|valign=middle|‍ᠬ}} 
|-
| 182C 180B || {{MongolUnicode|valign=middle|ᠬ᠋}} || {{MongolUnicode|valign=middle|ᠬ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠬ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠬ᠋}} 
|-
| 182C 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠬ᠌‍}} || style="background: silver" | 
|-
| 182C 180D || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠬ᠍‍}} || style="background: silver" | 
|-
| rowspan="2" align="center" | 托忒 || 184D || {{MongolUnicode|valign=middle|ᡍ}} || {{MongolUnicode|valign=middle|ᡍ‍}} || {{MongolUnicode|valign=middle|‍ᡍ‍}} || {{MongolUnicode|valign=middle|‍ᡍ}} 
|-
| 184D 180B || style="background: silver" | || {{MongolUnicode|valign=middle|ᡍ᠋‍}} || {{MongolUnicode|valign=middle|‍ᡍ᠋‍}} || style="background: silver" | 
|-
| rowspan="7" align="center" | '''G'''<br />ү/g || rowspan="4" align="center" | '''基本''' || '''182D''' || {{MongolUnicode|valign=middle|ᠭ}} || {{MongolUnicode|valign=middle|ᠭ‍}} || {{MongolUnicode|valign=middle|‍ᠭ‍}} || {{MongolUnicode|valign=middle|‍ᠭ}} 
|-
| 182D 180B || {{MongolUnicode|valign=middle|ᠭ᠋}} || {{MongolUnicode|valign=middle|ᠭ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠭ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠭ᠋}} 
|-
| 182D 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠭ᠌‍}} || {{MongolUnicode|valign=middle|‍ᠭ᠌}} 
|-
| 182D 180D || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠭ᠍‍}} || style="background: silver" | 
|-
| rowspan="2" align="center" | 托忒 || 184E || {{MongolUnicode|valign=middle|ᡎ}} || {{MongolUnicode|valign=middle|ᡎ‍}} || {{MongolUnicode|valign=middle|‍ᡎ‍}} || {{MongolUnicode|valign=middle|‍ᡎ}} 
|-
| 184E 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡎ᠋‍}} || style="background: silver" | 
|-
| align="center" | 锡伯文 || 1864 || {{MongolUnicode|valign=middle|ᡤ}} || {{MongolUnicode|valign=middle|ᡤ‍}} || {{MongolUnicode|valign=middle|‍ᡤ‍}} || {{MongolUnicode|valign=middle|‍ᡤ}} 
|-
| rowspan="2" align="center" | '''M'''<br />m || align="center" | '''基本''' || '''182E''' || {{MongolUnicode|valign=middle|ᠮ}} || {{MongolUnicode|valign=middle|ᠮ‍}} || {{MongolUnicode|valign=middle|‍ᠮ‍}} || {{MongolUnicode|valign=middle|‍ᠮ}} 
|-
| align="center" | 托忒 || 184F || {{MongolUnicode|valign=middle|ᡏ}} || {{MongolUnicode|valign=middle|ᡏ‍}} || {{MongolUnicode|valign=middle|‍ᡏ‍}} || {{MongolUnicode|valign=middle|‍ᡏ}} 
|-
| align="center" | '''L'''<br />l || align="center" | '''基本''' || '''182F''' || {{MongolUnicode|valign=middle|ᠯ}} || {{MongolUnicode|valign=middle|ᠯ‍}} || {{MongolUnicode|valign=middle|‍ᠯ‍}} || {{MongolUnicode|valign=middle|‍ᠯ}} 
|-
| rowspan="3" align="center" | '''S'''<br />s || rowspan="3" align="center" | '''基本''' || '''1830''' || {{MongolUnicode|valign=middle|ᠰ}} || {{MongolUnicode|valign=middle|ᠰ‍}} || {{MongolUnicode|valign=middle|‍ᠰ‍}} || {{MongolUnicode|valign=middle|‍ᠰ}} 
|-
| 1830 180B || colspan="3" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠰ᠋}} 
|-
| 1830 180C || colspan="3" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠰ᠌}} 
|-
| rowspan="2" align="center" | '''SH'''<br />š || align="center" | '''基本''' || '''1831''' || {{MongolUnicode|valign=middle|ᠱ}} || {{MongolUnicode|valign=middle|ᠱ‍}} || {{MongolUnicode|valign=middle|‍ᠱ‍}} || {{MongolUnicode|valign=middle|‍ᠱ}} 
|-
| align="center" | 锡伯文 || 1867 || {{MongolUnicode|valign=middle|ᡧ}} || {{MongolUnicode|valign=middle|ᡧ‍}} || {{MongolUnicode|valign=middle|‍ᡧ‍}} || {{MongolUnicode|valign=middle|‍ᡧ}} 
|-
| rowspan="6" align="center" | '''T'''<br />t || rowspan="2" align="center" | '''基本''' || '''1832''' || {{MongolUnicode|valign=middle|ᠲ}} || {{MongolUnicode|valign=middle|ᠲ‍}} || {{MongolUnicode|valign=middle|‍ᠲ‍}} || {{MongolUnicode|valign=middle|‍ᠲ}} 
|-
| 1832 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠲ᠋‍}} || style="background: silver" | 
|-
| align="center" | 托忒 || 1850 || {{MongolUnicode|valign=middle|ᡐ}} || {{MongolUnicode|valign=middle|ᡐ‍}} || {{MongolUnicode|valign=middle|‍ᡐ‍}} || {{MongolUnicode|valign=middle|‍ᡐ}} 
|-
| rowspan="3" align="center" | 锡伯文 || 1868 || {{MongolUnicode|valign=middle|ᡨ}} || {{MongolUnicode|valign=middle|ᡨ‍}} || {{MongolUnicode|valign=middle|‍ᡨ‍}} || {{MongolUnicode|valign=middle|‍ᡨ}} 
|-
| 1868 180B || style="background: silver" | || {{MongolUnicode|valign=middle|ᡨ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠲ᠋‍}} || style="background: silver" | 
|-
| 1832 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡨ᠌‍}} || style="background: silver" | 
|-
| rowspan="5" align="center" | '''D'''<br />d || rowspan="2" align="center" | '''基本''' || '''1833''' || {{MongolUnicode|valign=middle|ᠳ}} || {{MongolUnicode|valign=middle|ᠳ‍}} || {{MongolUnicode|valign=middle|‍ᠳ‍}} || {{MongolUnicode|valign=middle|‍ᠳ}} 
|-
| 1832 180B || style="background: silver" | || {{MongolUnicode|valign=middle|ᠳ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠳ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠳ᠋}} 
|-
| align="center" | 托忒 || 1851 || {{MongolUnicode|valign=middle|ᡑ}} || {{MongolUnicode|valign=middle|ᡑ‍}} || {{MongolUnicode|valign=middle|‍ᡑ‍}} || {{MongolUnicode|valign=middle|‍ᡑ}} 
|-
| rowspan="2" align="center" | 锡伯文 || 1869 || {{MongolUnicode|valign=middle|ᡩ}} || {{MongolUnicode|valign=middle|ᡩ‍}} || {{MongolUnicode|valign=middle|‍ᡩ‍}} || {{MongolUnicode|valign=middle|‍ᡩ}} 
|-
| 1869 180B || style="background: silver" | || {{MongolUnicode|valign=middle|ᡩ᠋‍}} || {{MongolUnicode|valign=middle|‍ᡩ᠋‍}} || style="background: silver" | 
|-
| rowspan="3" align="center" | '''CH'''<br />č || align="center" | '''基本''' || '''1834''' || {{MongolUnicode|valign=middle|ᠴ}} || {{MongolUnicode|valign=middle|ᠴ‍}} || {{MongolUnicode|valign=middle|‍ᠴ‍}} || {{MongolUnicode|valign=middle|‍ᠴ}} 
|-
| align="center" | 托忒 || 1852 || {{MongolUnicode|valign=middle|ᡒ}} || {{MongolUnicode|valign=middle|ᡒ‍}} || {{MongolUnicode|valign=middle|‍ᡒ‍}} || {{MongolUnicode|valign=middle|‍ᡒ}} 
|-
| align="center" | 锡伯文 || 1871 || {{MongolUnicode|valign=middle|ᡱ}} || {{MongolUnicode|valign=middle|ᡱ‍}} || {{MongolUnicode|valign=middle|‍ᡱ‍}} || {{MongolUnicode|valign=middle|‍ᡱ}} 
|-
| rowspan="4" align="center" | '''J'''<br />ǰ || rowspan="2" align="center" | '''基本''' || '''1835''' || {{MongolUnicode|valign=middle|ᠵ}} || {{MongolUnicode|valign=middle|ᠵ‍}} || {{MongolUnicode|valign=middle|‍ᠵ‍}} || {{MongolUnicode|valign=middle|‍ᠵ}} 
|-
| 1835 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠵ᠋‍}} || style="background: silver" | 
|-
| align="center" | 托忒 || 1853 || {{MongolUnicode|valign=middle|ᡓ}} || {{MongolUnicode|valign=middle|ᡓ‍}} || {{MongolUnicode|valign=middle|‍ᡓ‍}} || {{MongolUnicode|valign=middle|‍ᡓ}} 
|-
| align="center" | 锡伯文 || 186A || {{MongolUnicode|valign=middle|ᡪ}} || {{MongolUnicode|valign=middle|ᡪ‍}} || {{MongolUnicode|valign=middle|‍ᡪ‍}} || {{MongolUnicode|valign=middle|‍ᡪ}} 
|-
| rowspan="4" align="center" | '''Y'''<br />y || rowspan="3" align="center" | '''基本''' || '''1836''' || {{MongolUnicode|valign=middle|ᠶ}} || {{MongolUnicode|valign=middle|ᠶ‍}} || {{MongolUnicode|valign=middle|‍ᠶ‍}} || {{MongolUnicode|valign=middle|‍ᠶ}} 
|-
| 1836 180B || style="background: silver" | || {{MongolUnicode|valign=middle|ᠶ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠶ᠋‍}} || style="background: silver" | 
|-
| 1836 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠶ᠌‍}} || style="background: silver" | 
|-
| align="center" | 托忒 || 1855 || {{MongolUnicode|valign=middle|ᡕ}} || {{MongolUnicode|valign=middle|ᡕ‍}} || {{MongolUnicode|valign=middle|‍ᡕ‍}} || {{MongolUnicode|valign=middle|‍ᡕ}} 
|-
| rowspan="2" align="center" | '''R'''<br />r || align="center" | '''基本''' || '''1837''' || {{MongolUnicode|valign=middle|ᠷ}} || {{MongolUnicode|valign=middle|ᠷ‍}} || {{MongolUnicode|valign=middle|‍ᠷ‍}} || {{MongolUnicode|valign=middle|‍ᠷ}} 
|-
| align="center" | 满文 || 1875 || {{MongolUnicode|valign=middle|ᡵ}} || {{MongolUnicode|valign=middle|ᡵ‍}} || {{MongolUnicode|valign=middle|‍ᡵ‍}} || {{MongolUnicode|valign=middle|‍ᡵ}} 
|-
| align="center" | '''RA''' || align="center" | 锡伯文 || 1870 || {{MongolUnicode|valign=middle|ᡰ}} || {{MongolUnicode|valign=middle|ᡰ‍}} || {{MongolUnicode|valign=middle|‍ᡰ‍}} || {{MongolUnicode|valign=middle|‍ᡰ}} 
|-
| rowspan="3" align="center" | '''W'''<br />v || rowspan="2" align="center" | '''基本''' || '''1838''' || {{MongolUnicode|valign=middle|ᠸ}} || {{MongolUnicode|valign=middle|ᠸ‍}} || {{MongolUnicode|valign=middle|‍ᠸ‍}} || {{MongolUnicode|valign=middle|‍ᠸ}} 
|-
| 1838 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᠸ᠋‍}} || {{MongolUnicode|valign=middle|‍ᠸ᠋}} 
|-
| align="center" | 托忒 || 1856 || {{MongolUnicode|valign=middle|ᡖ}} || {{MongolUnicode|valign=middle|ᡖ‍}} || {{MongolUnicode|valign=middle|‍ᡖ‍}} || {{MongolUnicode|valign=middle|‍ᡖ}} 
|-
| rowspan="4" align="center" | '''F'''<br />f || align="center" | '''基本''' || '''1839''' || {{MongolUnicode|valign=middle|ᠹ}} || {{MongolUnicode|valign=middle|ᠹ‍}} || {{MongolUnicode|valign=middle|‍ᠹ‍}} || {{MongolUnicode|valign=middle|‍ᠹ}} 
|-
| align="center" | 锡伯文 || 186B || {{MongolUnicode|valign=middle|ᡫ}} || {{MongolUnicode|valign=middle|ᡫ‍}} || {{MongolUnicode|valign=middle|‍ᡫ‍}} || {{MongolUnicode|valign=middle|‍ᡫ}} 
|-
| rowspan="2" align="center" | 满文 || 1876 || {{MongolUnicode|valign=middle|ᡶ}} || {{MongolUnicode|valign=middle|ᡶ‍}} || {{MongolUnicode|valign=middle|‍ᡶ‍}} || {{MongolUnicode|valign=middle|‍ᡶ}} 
|-
| 1876 180B || style="background: silver" | || {{MongolUnicode|valign=middle|ᡶ᠋‍}} || {{MongolUnicode|valign=middle|‍ᡶ᠋‍}} || style="background: silver" | 
|-
| rowspan="8" align="center" | '''K''' || align="center" | '''基本''' || '''183A''' || {{MongolUnicode|valign=middle|ᠺ}} || {{MongolUnicode|valign=middle|ᠺ‍}} || {{MongolUnicode|valign=middle|‍ᠺ‍}} || {{MongolUnicode|valign=middle|‍ᠺ}} 
|-
| align="center" | 托忒 || 1857 || {{MongolUnicode|valign=middle|ᡗ}} || {{MongolUnicode|valign=middle|ᡗ‍}} || {{MongolUnicode|valign=middle|‍ᡗ‍}} || {{MongolUnicode|valign=middle|‍ᡗ}} 
|-
| rowspan="2" align="center" | 锡伯文 || 1863 || {{MongolUnicode|valign=middle|ᡣ}} || {{MongolUnicode|valign=middle|ᡣ‍}} || {{MongolUnicode|valign=middle|‍ᡣ‍}} || {{MongolUnicode|valign=middle|‍ᡣ}} 
|-
| 1863 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡣ᠋‍}} || style="background: silver" | 
|-
| rowspan="4" align="center" | 满文 || 1874 || {{MongolUnicode|valign=middle|ᡴ}} || {{MongolUnicode|valign=middle|ᡴ‍}} || {{MongolUnicode|valign=middle|‍ᡴ‍}} || {{MongolUnicode|valign=middle|‍ᡴ}} 
|-
| 1874 180B || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡴ᠋‍}} || {{MongolUnicode|valign=middle|‍ᡴ᠋}} 
|-
| 1874 180C || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡴ᠌‍}} || {{MongolUnicode|valign=middle|‍ᡴ᠌}} 
|-
| 1874 180D || colspan="2" style="background: silver" | || {{MongolUnicode|valign=middle|‍ᡴ᠍‍}} || style="background: silver" | 
|-
| align="center" | '''KH'''<br />k̄ || align="center" | '''基本''' || '''183B''' || {{MongolUnicode|valign=middle|ᠻ}} || {{MongolUnicode|valign=middle|ᠻ‍}} || {{MongolUnicode|valign=middle|‍ᠻ‍}} || {{MongolUnicode|valign=middle|‍ᠻ}} 
|-
| rowspan="2" align="center" | '''GA''' || align="center" | 托忒 || 1858 || {{MongolUnicode|valign=middle|ᡘ}} || {{MongolUnicode|valign=middle|ᡘ‍}} || {{MongolUnicode|valign=middle|‍ᡘ‍}} || {{MongolUnicode|valign=middle|‍ᡘ}} 
|-
| align="center" | 锡伯文 || 186C || {{MongolUnicode|valign=middle|ᡬ}} || {{MongolUnicode|valign=middle|ᡬ‍}} || {{MongolUnicode|valign=middle|‍ᡬ‍}} || {{MongolUnicode|valign=middle|‍ᡬ}} 
|-
| rowspan="3" align="center" | '''TS'''<br />c || align="center" | '''基本''' || '''183C''' || {{MongolUnicode|valign=middle|ᠼ}} || {{MongolUnicode|valign=middle|ᠼ‍}} || {{MongolUnicode|valign=middle|‍ᠼ‍}} || {{MongolUnicode|valign=middle|‍ᠼ}} 
|-
| align="center" | 托忒 || 1854 || {{MongolUnicode|valign=middle|ᡔ}} || {{MongolUnicode|valign=middle|ᡔ‍}} || {{MongolUnicode|valign=middle|‍ᡔ‍}} || {{MongolUnicode|valign=middle|‍ᡔ}} 
|-
| align="center" | 锡伯文 || 186E || {{MongolUnicode|valign=middle|ᡮ}} || {{MongolUnicode|valign=middle|ᡮ‍}} || {{MongolUnicode|valign=middle|‍ᡮ‍}} || {{MongolUnicode|valign=middle|‍ᡮ}} 
|-
| rowspan="3" align="center" | '''Z'''<br />z || align="center" | '''基本''' || '''183D''' || {{MongolUnicode|valign=middle|ᠽ}} || {{MongolUnicode|valign=middle|ᠽ‍}} || {{MongolUnicode|valign=middle|‍ᠽ‍}} || {{MongolUnicode|valign=middle|‍ᠽ}} 
|-
| rowspan="2" align="center" | 锡伯文 || 186F || {{MongolUnicode|valign=middle|ᡯ}} || {{MongolUnicode|valign=middle|ᡯ‍}} || {{MongolUnicode|valign=middle|‍ᡯ‍}} || {{MongolUnicode|valign=middle|‍ᡯ}} 
|-
| 186F 180B || style="background: silver" | || {{MongolUnicode|valign=middle|ᡯ᠋‍}} || {{MongolUnicode|valign=middle|‍ᡯ᠋‍}} || style="background: silver" | 
|-
| rowspan="3" align="center" | '''HA'''<br />h || align="center" | '''基本''' || '''183E''' || {{MongolUnicode|valign=middle|ᠾ}} || {{MongolUnicode|valign=middle|ᠾ‍}} || {{MongolUnicode|valign=middle|‍ᠾ‍}} || {{MongolUnicode|valign=middle|‍ᠾ}} 
|-
| align="center" | 托忒 || 1859 || {{MongolUnicode|valign=middle|ᡙ}} || {{MongolUnicode|valign=middle|ᡙ‍}} || {{MongolUnicode|valign=middle|‍ᡙ‍}} || {{MongolUnicode|valign=middle|‍ᡙ}} 
|-
| align="center" | 锡伯文 || 186D || {{MongolUnicode|valign=middle|ᡭ}} || {{MongolUnicode|valign=middle|ᡭ‍}} || {{MongolUnicode|valign=middle|‍ᡭ‍}} || {{MongolUnicode|valign=middle|‍ᡭ}} 
|-
| align="center" | '''ZR'''<br />ž/ř || align="center" | '''基本''' || '''183F''' || {{MongolUnicode|valign=middle|ᠿ}} || {{MongolUnicode|valign=middle|ᠿ‍}} || {{MongolUnicode|valign=middle|‍ᠿ‍}} || {{MongolUnicode|valign=middle|‍ᠿ}} 
|-
| rowspan="2" align="center" | '''ZH''' || align="center" | 锡伯文 || 1872 || {{MongolUnicode|valign=middle|ᡲ}} || {{MongolUnicode|valign=middle|ᡲ‍}} || {{MongolUnicode|valign=middle|‍ᡲ‍}} || {{MongolUnicode|valign=middle|‍ᡲ}} 
|-
| align="center" | 满文 || 1877 || {{MongolUnicode|valign=middle|ᡷ}} || {{MongolUnicode|valign=middle|ᡷ‍}} || {{MongolUnicode|valign=middle|‍ᡷ‍}} || {{MongolUnicode|valign=middle|‍ᡷ}} 
|-
| align="center" | '''LH'''<br />lh || align="center" | '''基本''' || '''1840''' || {{MongolUnicode|valign=middle|ᡀ}} || {{MongolUnicode|valign=middle|ᡀ‍}} || {{MongolUnicode|valign=middle|‍ᡀ‍}} || {{MongolUnicode|valign=middle|‍ᡀ}} 
|-
| align="center" | '''ZHI'''<br />zh || align="center" | '''基本''' || '''1841''' || {{MongolUnicode|valign=middle|ᡁ}} || {{MongolUnicode|valign=middle|ᡁ‍}} || {{MongolUnicode|valign=middle|‍ᡁ‍}} || {{MongolUnicode|valign=middle|‍ᡁ}} 
|-
| align="center" | '''CHI'''<br />ch || align="center" | '''基本''' || '''1842''' || {{MongolUnicode|valign=middle|ᡂ}} || {{MongolUnicode|valign=middle|ᡂ‍}} || {{MongolUnicode|valign=middle|‍ᡂ‍}} || {{MongolUnicode|valign=middle|‍ᡂ}} 
|-
| align="center" | '''JI''' || align="center" | 托忒 || 185A || {{MongolUnicode|valign=middle|ᡚ}} || {{MongolUnicode|valign=middle|ᡚ‍}} || {{MongolUnicode|valign=middle|‍ᡚ‍}} || {{MongolUnicode|valign=middle|‍ᡚ}} 
|-
| align="center" | '''NI''' || align="center" | 托忒 || 185B || {{MongolUnicode|valign=middle|ᡛ}} || {{MongolUnicode|valign=middle|ᡛ‍}} || {{MongolUnicode|valign=middle|‍ᡛ‍}} || {{MongolUnicode|valign=middle|‍ᡛ}} 
|-
| align="center" | '''DZ''' || align="center" | 托忒 || 185C || {{MongolUnicode|valign=middle|ᡜ}} || {{MongolUnicode|valign=middle|ᡜ‍}} || {{MongolUnicode|valign=middle|‍ᡜ‍}} || {{MongolUnicode|valign=middle|‍ᡜ}} 
|-
|}
|}

==历史==
以下文件记录了此区段的建立目的与各字符的定义过程。
{| class="wikitable"
|-
! [[Unicode#.E5.8E.86.E5.8F.B2|版本]] !! {{nobr|码位<ref group=lower-alpha name=final/>}} !! 码点数量 !! {{le|国际信息技术标准委员会|International Committee for Information Technology Standards|L2}} ID !! {{tsl|en|ISO/IEC JTC 1/SC 2|ISO/IEC JTC 1/SC 2|WG2}} ID !! 文件
|-
| rowspan="53" | 3.0 || rowspan="53" width="180" | U+1800..180E, 1810..1819, 1820..1877, 1880..18A9 || rowspan="53" | 155 || {{nobr|X3L2/93-066}} || N836 || {{Citation|title=Proposal for disposition of Chinese Comments on Mongolian characters in DIS 1.2|date=1992-06-27|first=Ken|last=Whistler}}
|-
| {{nobr|X3L2/94-086}} || N1011 || {{Citation|title=A proposal about installing Mongolian, Todo, Xibe (Manchu included) scripts into ISO/IEC 10646 BMP|date=1994-04-18}}
|-
| {{nobr|X3L2/95-133}} || || {{Citation|title=Correspondence from the National Body of Mongolia regarding Coded character set for the Mongolian Script|date=1995-10-23}}
|-
| {{nobr|X3L2/96-054}} || N1368 || {{Citation|title=Mongolian script proposal|date=1996-04-10}}
|-
| {{nobr|X3L2/96-055}} || N1383 || {{Citation|title=Ad hoc report on Mongolian script - Copenhagen meeting|date=1996-04-25}}
|-
| {{nobr|X3L2/96-102}} || N1437 || {{Citation|title=Report of 3rd international Mongolian encoding meeting|date=1996-08-06}}
|-
| {{nobr|X3L2/96-103}} || N1438 || {{Citation|title=Draft on encoding Mongolian character set|date=1996-08-08}}
|-
| {{nobr|X3L2/96-113}} || || {{Citation|title=About the function of identifiers of Mongolian Proposal|date=1996-11-10|first=Mao Yong|last=Gang}}
|-
| {{nobr|L2/97-028}} || N1497 || {{Citation|title=On the Use of Control Symbols in the Mongolian Script Encoding|date=1997-01-10|first1=Richard|last1=Moore|display-authors=etal}}
|-
| {{nobr|L2/97-035}} || N1515 || {{Citation|title=Report of the ad-hoc group on Mongolian encoding|date=1997-01-23|first1=Richard|last1=Moore|display-authors=etal}}
|-
| {{nobr|L2/97-152}} || N1607 || {{Citation|title=Mongolian proposal review|date=1997-06-20}}
|-
| {{nobr|L2/97-165}} || N1622 || {{Citation|title=Comments on Technical Issues of Mongolian in N 1515 and N1607|date=1997-07-03|first=Oliver|last=Corff}}
|-
| {{nobr|[http://www.unicode.org/L2/L1998/98088-n1711-scan.pdf L2/98-088]}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/N1711Scanned.pdf N1711] || {{Citation|title=The Working Meeting on Mongolian Encoding Attended by Representatives of China and Mongolia|date=1998-02-15}}
|-
| {{nobr|L2/98-104}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/n1734.pdf N1734] || {{Citation|title=Comments on the Mongolian Encoding Proposal, WG2 N1711|date=1998-03-20|first=Ken|last=Whistler}}
|-
| {{nobr|L2/98-252}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/n1833.doc N1833] || {{Citation|title=Feedback on Ken Whistler's Comments on Mongolian Encoding: N 1734|date=1998-05-04|first=Richard|last=Moore}}
|-
| {{nobr|L2/98-251}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/n1808.pdf N1808] || {{Citation|title=Reply to "Proposal WG2 N1734" Raised at the Seattle Meeting Regarding "Proposal WG 2 N1711"|date=1998-07-09}}
|-
| {{nobr|L2/98-272}} || || {{Citation|title=Mongolian: China's comments to Richard Moore's feedback in L2/98-252|date=1998-07-26|last=Choijingzhab}}
|-
| {{nobr|L2/98-268R}} || || {{Citation|title=Analysis and UTC Position Regarding Mongolian Encoding Issues|date=1998-07-30|first=Ken|last=Whistler}}
|-
| {{nobr|L2/98-369}} || N1878 || {{Citation|title=Report of the meetings of the ad-hoc group on Mongolian; London; 21/22 September, 1998|date=1998-09-23}}
|-
| {{nobr|[http://www.unicode.org/L2/L1998/02n3207.htm L2/98-326]}} || || {{Citation|title=Subdivision Proposal on JTC 1.02.18.01 for Amendment 29: Mongolian to ISO/IEC 10646-1|date=1998-10-28}}
|-
| {{nobr|[http://www.unicode.org/L2/L1998/02n3208.pdf L2/98-327]}} || || {{Citation|title=Combined PDAM registration and consideration ballot on WD for ISO/IEC 10646-1/Amd. 29, AMENDMENT 29: Mongolian|date=1998-10-28}}
|-
| {{nobr|[http://www.unicode.org/L2/L1998/98389.pdf L2/98-389R]}} || || {{Citation|title=Consent docket re WG2 Resolutions at its Meeting #35|first=Joan|last=Aliprand|section=RESOLUTION M35.11}}
|-
| {{nobr|[http://www.unicode.org/L2/L1999/02n32491.pdf L2/99-075.1]}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/n1973.pdf N1973] || {{Citation|title=Irish Comments on SC 2 N 3208|date=1999-01-19}}
|-
| {{nobr|[http://www.unicode.org/L2/L1999/02n3248.htm L2/99-074]}} || || {{Citation|title=Summary of Voting on SC 2 N 3207, Subdivision Proposal on JTC 1.02.18.01 for Amendment 29: Mongolian|date=1999-02-12}}
|-
| {{nobr|[http://www.unicode.org/L2/L1999/02n3249.htm L2/99-075]}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/n1972.htm N1972] || {{Citation|title=Summary of Voting on SC 2 N 3208, PDAM ballot on WD for ISO/IEC 10646-1/Amd. 29: Mongolian|date=1999-02-12}}
|-
| {{nobr|[http://www.unicode.org/L2/L1999/02n3308.pdf L2/99-113]}} || || {{Citation|title=Text for FPDAM ballot of ISO/IEC 10646, Amd. 29 - Mongolian|date=1999-04-06}}
|-
| {{nobr|[http://www.unicode.org/L2/L1999/02n3348.pdf L2/99-254]}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/n2068.pdf N2068] || {{Citation|title=Summary of Voting on SC 2 N 3308, ISO 10646-1/FPDAM 29 - Mongolian|date=1999-08-19}}
|-
| {{nobr|[http://www.unicode.org/L2/L1999/99303-02n3364.htm L2/99-303]}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/n2125.htm N2125] || {{Citation|title=Disposition of Comments Report on SC 2 N 3308, ISO/IEC 10646-1/FPDAM 29 AMD. 29: Mongolian|date=1999-09-20}}
|-
| {{nobr|[http://www.unicode.org/L2/L1999/99304-02n3365.pdf L2/99-304]}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/n2126.pdf N2126] || {{Citation|title=Revised Text for FDAM ballot of ISO/IEC 10646-1/FDAM 29, AMENDMENT 29: Mongolian|date=1999-10-01|first=Bruce|last=Paterson}}
|-
| {{nobr|[http://www.unicode.org/L2/L1999/99381-fdam29.pdf L2/99-381]}} || || {{Citation|title=Final text for ISO/IEC 10646-1, FDAM 29 -- Mongolian|date=1999-12-07}}
|-
| {{nobr|[http://www.unicode.org/L2/L2000/00046-02n3407.pdf L2/00-046]}} || || {{Citation|title=Summary of FDAM voting: ISO 10646 Amendment 29: Mongolian|date=2000-02-15}}
|-
| {{nobr|[http://www.unicode.org/L2/L2003/03065-mongolian.pdf L2/03-065]}} || || {{Citation|title=Use of ZWJ/ZWNJ with Mongolian Variant Selectors and Vowel Separator|date=2003-02-13|first1=Paul|last1=Nelson|first2=Asmus|last2=Freytag}}
|-
| {{nobr|[http://www.unicode.org/L2/L2003/03073-mongolian.txt L2/03-073]}} || || {{Citation|title=Error Report on Linebreaking of Mongolian Vowel Separator|date=2003-02-27|first=Tim|last=Partridge}}
|-
| {{nobr|[http://www.unicode.org/L2/L2003/03039.htm L2/03-039R]}} || || {{Citation|title=UTC #94 Minutes|date=2003-03-14|first=Lisa|last=Moore|section=Properties - Mongolian Vowel Separator}}
|-
| {{nobr|[http://www.unicode.org/L2/L2005/05378-mongolian-prop.txt L2/05-378]}} || || {{Citation|title=Proposal to change the script property for three Mongolian punctuation marks|date=2005-12-05|first=Eric|last=Muller}}
|-
| {{nobr|[http://www.unicode.org/L2/L2010/10279-mongolian-rendering.pdf L2/10-279]}} || || {{Citation|title=Mongolian Script Rendering Issues|date=2010-07-30|first1=Biligsaikhan|last1=Batjargal|display-authors=etal}}
|-
| {{nobr|[http://www.unicode.org/L2/L2011/11401-extender.pdf L2/11-401]}} || || {{Citation|title=Proposal to assign the Extender property to U+180A MONGOLIAN NIRUGU|date=2011-10-19|first=Laurențiu|last=Iancu}}
|-
| {{nobr|[http://www.unicode.org/L2/L2012/12202-shaping.txt L2/12-202]}} || || {{Citation|title=Proposal to Add Mongolian Letters to ArabicShaping.txt|date=2012-06-01|first=Behdad|last=Esfahbod|authorlink=葉密豪}}
|-
| {{nobr|[http://www.unicode.org/L2/L2012/12360-mong-shaping.txt L2/12-360]}} || || {{Citation|title=Mongolian and 'Phags-Pa Shaping|date=2012-11-05|first1=Behdad|last1=Esfahbod|first2=Roozbeh|last2=Pournader}}
|-
| {{nobr|[http://www.unicode.org/consortium/utc-minutes/UTC-133-2012011.html L2/12-343R2]}} || || {{Citation|title=UTC #133 Minutes|date=2012-12-04|first=Lisa|last=Moore|section=Properties — Mongolian Shaping}}
|-
| {{nobr|[http://www.unicode.org/L2/L2013/13004-vowel-sep-change.pdf L2/13-004]}} || || {{Citation|title=Proposal to change General Category of MONGOLIAN VOWEL SEPARATOR from Zs to Cf|date=2012-12-20|first=Behdad|last=Esfahbod}}
|-
| {{nobr|[http://www.unicode.org/consortium/utc-minutes/UTC-134-201301.html L2/13-011]}} || || {{Citation|title=UTC #134 Minutes|date=2013-02-04|first=Lisa|last=Moore|section=Properties — MONGOLIAN VOWEL SEPARATOR}}
|-
| {{nobr|[http://www.unicode.org/L2/L2013/13146-n4435.pdf L2/13-146]}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/n4435.pdf N4435] || {{Citation|title=Presentation of vertical scripts|date=2013-05-27|first=Michel|last=Suignard}}
|-
| {{nobr|[http://www.unicode.org/L2/L2014/14031-mong-chart-upd.pdf L2/14-031]}} || || {{Citation|title=Proposal to update the code charts for Mongolian|date=2014-01-20|first1=Aaron|last1=Bell|first2=Greg|last2=Eck|first3=Andrew|last3=Glass}}
|-
| {{nobr|[http://www.unicode.org/L2/L2015/15304-mongolian-chart.pdf L2/15-304]}} || || {{Citation|title=Draft Mongolian variation selectors|date=2015-08-27|first=Michel|last=Suignard}}
|-
| {{nobr|[http://www.unicode.org/L2/L2016/16041r-mongolian.pdf L2/16-041R]}} || || {{Citation|title=Mongolian discussion documents|date=2016-01-26|first=Greg|last=Eck}}
|-
| {{nobr|[http://www.unicode.org/L2/L2016/16004.htm L2/16-004]}} || || {{Citation|title=UTC #146 Minutes|date=2016-02-01|first=Lisa|last=Moore|section=C.13 Mongolian discussion documents}}
|-
| {{nobr|[http://www.unicode.org/L2/L2016/16258-mongolian-forms.pdf L2/16-258]}} || || {{Citation|title=Mongolian Base Forms, Positional Forms, & Variant Forms|date=2016-09-19|first=Greg|last=Eck}}
|-
| {{nobr|[http://www.unicode.org/L2/L2016/16259-wg2-65-discussion-points.pdf L2/16-259]}} || [http://www.unicode.org/wg2/docs/n4753r-WG2_N65_Discussion_Points.pdf N4753] || {{Citation|title=WG2 #65 Mongolian Discussion Points|date=2016-09-20|first1=Greg|last1=Eck|first2=Orlog Ou|last2=Rileke}}
|-
| {{nobr|[http://www.unicode.org/L2/L2016/16266-script-ad-hoc.pdf L2/16-266]}} || || {{Citation|title=Comments on Mongolian, Small Khitan, and other WG2 #65 documents|date=2016-09-26|first1=Deborah|last1=Anderson|first2=Ken|last2=Whistler|first3=Rick|last3=McGowan|first4=Roozbeh|last4=Pournader|first5=Andrew|last5=Glass|first6=Laurențiu|last6=Iancu|first7=Lisa|last7=Moore|section=1. Mongolian}}
|-
| {{nobr|[http://www.unicode.org/L2/L2016/16297-n4769-mongolian-ad-hoc.pdf L2/16-297]}} || [http://www.unicode.org/wg2/docs/n4769-MongolianAdHoc-4.pdf N4769] || {{Citation|title=Mongolian ad hoc report|date=2016-10-27|first=Deborah|last=Anderson}}
|-
| {{nobr|[http://www.unicode.org/L2/L2016/16342-script-ad-hoc.pdf L2/16-342]}} || || {{Citation|title=Recommendations to UTC #149 November 2016 on Script Proposals|date=2016-11-07|first1=Deborah|last1=Anderson|first2=Ken|last2=Whistler|first3=Roozbeh|last3=Pournader|first4=Andrew|last4=Glass|first5=Laurențiu|last5=Iancu|section=11. Mongolian}}
|-
| {{nobr|[http://www.unicode.org/L2/L2016/16325.htm L2/16-325]}} || || {{Citation|title=UTC #149 Minutes|date=2016-11-18|first=Lisa|last=Moore|section=C.5.4}}
|-
| rowspan="2" | 5.1 || rowspan="2" width="180" | U+18AA || rowspan="2" | 1 || {{nobr|[http://www.unicode.org/L2/L2006/06013-manchu-lha.pdf L2/06-013]}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/n3041.pdf N3041] || {{Citation|title=Proposal to encode one Manchu ali gali letter|date=2006-01-23|first=Andrew|last=West|authorlink=魏安}}
|-
| {{nobr|[http://www.unicode.org/L2/L2006/06285-n3092.pdf L2/06-285]}} || [http://std.dkuug.dk/jtc1/sc2/wg2/docs/n3092.pdf N3092] || {{Citation|title=Supporting references for WG2 N3041, Manchu Ali Gali|date=2006-03-27}}
|- class="sortbottom"
| colspan=6 | {{reflist|group=lower-alpha|refs=<ref name=final>提案中的字符码位与最终定稿的字符码位可能不同。</ref>}}
|}

== 参见 ==
*{{le|蒙古文补充 (Unicode区段)|Mongolian Supplement (Unicode block)}}
*[[中蒙联合转写|中蒙联合转写]]

== 注释 ==
{{ReflistH}}
{{NoteFoot}}
{{ReflistF}}

== 参考资料 ==
{{reflist}}

[[Category:Unicode區段|Category:Unicode區段]]
[[Category:满文|Category:满文]]
[[Category:蒙古文字|Category:蒙古文字]]