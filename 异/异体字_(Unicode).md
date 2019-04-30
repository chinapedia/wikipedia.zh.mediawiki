{{Double image aside|right|u66d9-k.svg|120|u66d9.svg|120|异体字选择器不开启的场合、有点的字体和没点的字体之间没有区别。VS(異体字选择器)17设置为没有点的字体、VS18设置为有点的字体。}}

'''[[异体字|异体字]]选择器'''<ref>
JIS X 0221:2007の規格票では「字形選択子」という訳語を当てているが、全く意味の異なる"Character shaping selectors"などにも全く同じ訳語を当てているので、混乱を避けるため本項では「異体字セレクタ」という訳語を用いる。
</ref>（{{lang-en|Variation Selector}}）是在[[Unicode|Unicode]]和[[ISO/IEC_10646|ISO/IEC 10646 (UCS)]]上，用来更详细地进行[[文字|文字]][[字体|字体]]之间的选择指定的一种程序。

== 描述 ==
[[Image:u845b-k.svg|thumb]]的葛}}]]
[[Image:u845b.svg|thumb]]的葛}}]]
[[Unicode|Unicode]]是一个字体间抽象的文字集合，它并没有描绘出每个字体的样式。因此同样意义的字符被赋予了相同的编码，因此在[[计算机字体|字形]]上作区分是有必要的<ref>{{cite web|url=http://www.unicode.org/reports/tr17/|title=Unicode Technical Report #17 - Character Encoding Model|date=2004-09-09|accessdate=2008-02-02}}</ref><ref>之所以不同的字有相同的编码，不如说是在最初定义字形的16位编码的字库不足，所以不足以将所有汉字的正确形态一一描述进去。</ref>。

需注意的是譬如[[拉丁字母|拉丁字母]]'a'是否有从顶部向右延伸的线，通常不属于不同间字体的差异，因为可以通过更改字体来修改。但举个例子，在[[中日韓統一表意文字|中日韓統一表意文字]]中，作为{{link-en|汉字统合|Han unification}}的字体以各国内标准的原因为理由，经常运用被认为是“另一个字”的字形，以其汉字的不同属于不同字体为由，经常发生字体重合（在最初的Unicode提案中就已经被关注了）。因此，根据情况，需要在{{link-en|纯文本|Plain text}}上保存不同字形的区别是有必要的。

* 在大部分的操作系统中，[[文件名|文件名]]是纯文本，不能区别在文本中不能区分的东西。
* [[输入法|输入法]]可以输入的字符串仅是通常的文本<ref>{{cite book|author=川俣晶|date=1998-10-30|title=Windows NT 日本語処理ガイドブック|publisher=Windows NT 漢字処理技術協議会|url=http://www.xkp.or.jp/xkp2.pdf|pages=p.5}}</ref>。因此[[字形|字形]]即使可以被选择，在要求与通常的文字进行不同的选择上，必须记住正确的组合，对于大部分的普通用户来说，不能用更多的时间来输入。例如[[Microsoft_Windows_Vista|Windows Vista]]开始可以区分{{JIS2004フォント|[[葛飾区|葛飾区]]}}以及{{JIS90フォント|[[葛城市|葛城市]]}}了<ref>{{cite web|url=http://download.microsoft.com/download/3/4/4/3448ddf3-ca22-45bd-9984-1237e8ed0019/Windows_Vista_application_compatibility_paper.doc|title=アプリケーション開発者向け Windows Vista 対応アプリケーションの互換性|pages=68|accessdate=2008-02-02}}{{Dead link|date=2018年9月 |bot=InternetArchiveBot |fix-attempted=yes }} [http://channel9.msdn.com/ShowPost.aspx?PostID=222960#222960 デモ映像]</ref>，如[[Image:u845b-k.svg|葛]]飾区和[[Image:u845b.svg|葛]]城市这种字体的区别，在编码上没有区别。<ref>{{cite web|url=http://www.ergo.co.jp/products/egb16/other.html#03|title=Mac専用日本語入力プログラム“egbridge Universal”|3=製品情報 </title>|accessdate=2008-02-15|archive-url=https://web.archive.org/web/20080919005857/http://www.ergo.co.jp/products/egb16/other.html#03|archive-date=2008-09-19|dead-url=yes}}</ref>。
* 用于发送[[电子邮件|电子邮件]]的[[简单邮件传输协议|SMTP]]等[[网络传输协议|网络传输协议]]是用纯文本发送的，因此不能区分一些相同编码字符的不同字形<ref>{{cite web|url=http://www.apple.com/jp/pro/design/typography/05/index6.html|title=アップル - Pro - 技術情報 - Mac OS Xと日本語タイポグラフィ 第5回：ヒラギノProの漢字を巡る座談会 - ページ6|accessdate=2008-02-15|archive-url=https://web.archive.org/web/20080221192733/http://www.apple.com/jp/pro/design/typography/05/index6.html|archive-date=2008-02-21|dead-url=yes}}</ref>。

异体字选择器是为了在unicode中解决上述问题而设计出的特殊的“字符”（有着相同[[码位|码位]]的异体字）。由异体字选择器决定在当前文本中所使用的文字，根据前后文判断并由异体字选择器选择不同的字形。<ref>{{cite web|url=http://www.w3.org/TR/2003/NOTE-unicode-xml-20030613/#Format|title=Format Characters Suitable for Use with Markup|date=2003-06-13|accessdate=2008-02-02}}</ref>。另外，异体字选择器具有更详细地指定附加的文字的字形的功能，但是并不显示异体选择器本身。

== 种类 ==
异体字选择器一般分两种，Standardized Variation Sequence（标准化的异体字选择器、简称 SVS<ref>一般にはSVSが略称として使われることがあるが、公式な略称ではない</ref>），以及Ideographic Variation Sequence（汉字异体字选择器、简称 '''IVS'''）。

SVS在非漢字及[[中日韓統一表意文字|中日韓統一表意文字]]中均有启用，这种字形选择定义为Unicode的标准化变体<ref>
{{Cite web | title=StandardizedVariants.txt | url=http://www.unicode.org/Public/UCD/latest/ucd/StandardizedVariants.txt | publisher=Unicode Consortium | date=2015-11-20 | accessdate=2017-06-01 }}
</ref>。向标准化变体里添加字体属于[[統一碼聯盟|統一碼聯盟]]的工作。

另一方面，IVS是汉字专用的，字形收集是由ideographic variation database（汉字异体字数据库，简称为ivd）定义的。要想在ivd中增加字形，也必须根据规定向統一碼聯盟申请。<ref name="tr37">
{{Cite web | title=Unicode® Technical Standard #37 UNICODE IDEOGRAPHIC VARIATION DATABASE | url=http://www.unicode.org/reports/tr37/| publisher=Unicode Consortium | date=| accessdate=2017-10-05 }}
</ref>。

直到2017年12月，由异体字选择器所使用的异体字如下所示。

'''Standardized Variants录入的字集和数量'''
* [[数学符号表|数学符号表]]：25个
* 缅甸的[[缅文|缅文]]：27个
* [[八思巴字母|八思巴字母]]：6个
* [[摩尼字母|摩尼字母]]：5个
* [[传统蒙古文|传统蒙古文]]：60个
* [[中日韓統一表意文字|中日韓統一表意文字]]：1,002通个
* [[颜文字|颜文字]]：702个（文本类型和图形文字的类型351个）<ref>{{Cite web| title=emoji-variation-sequences.txt| url=https://unicode.org/Public/emoji/6.0/emoji-variation-sequences.txt| publisher=Unicode Consortium| language=en| accessdate=2017-10-06}}{{Dead link|date=2018年9月 |bot=InternetArchiveBot |fix-attempted=yes }}</ref>

'''IVD（2017-12-12版）录入的字集和数量'''
* [[CID_(文字编码)|CID]]之adobe-japan1集：14,683个<ref>なおAdobe-Japan1-6の文字セットに含まれる漢字は14,664個である</ref>
* 通用电子信息交换环境整顿计划之Hanyo-Denshi集：13,045个
* 文字信息基础整备事业之Moji_Joho集：11,384个
* [[澳门|澳门特别行政区]]之MSARG集：21个
* [[韩国|韩国]]之KRName集：36个

但是hanyo-denshi与adobe-japan1有很多重复。<ref>
{{cite web|url=http://itpro.nikkeibp.co.jp/article/COLUMN/20110124/356398/|title=UnicodeのIVSがもたらすメリットとデメリット - 新常用漢字が引き起こす文字コード問題|author=安岡孝一|date=2011-01-24|accessdate=2011-02-01}}
</ref>

=== 字形规格 ===
* [[OpenType|OpenType]] 1.5版使用了“Unicode Variation Sequences”规格<ref>
{{cite web|url=http://www.microsoft.com/typography/otspec150/default.htm|title=Microsoft Typography - OpenType Specification|date=2008-01-29|accessdate=2008-03-10}}</ref>。
* [[Scalable_Vector_Graphics|SVG]]不仅局限于IVS，任意Unicode编码均可<ref>{{cite web|url=http://www.w3.org/TR/SVG/fonts.html#GlyphElement|title=Fonts – SVG 1.1 (Second Edition)|accessdate=2011-02-01}}</ref>。

=== 字体创建工具 ===
* [[FontForge|FontForge]] - 2007年10月2日之后<ref>{{cite web|url=http://fontforge.sourceforge.net/changelog.html|title=Change log for FontForge|date=2008-03-09|accessdate=2008-03-10}}</ref>。
* Adobe Font Development Kit for OpenType (AFDKO) 2.1版之后<ref name="IRGN1374">{{cite web|url=http://www.cse.cuhk.edu.hk/~irg/irg/irg29/IRGN1374_IUC.pdf|title=Ideographic Variation Sequences|pages=p.10|date=2007-10-17|accessdate=2008-03-10}}{{Dead link|date=2018年9月 |bot=InternetArchiveBot |fix-attempted=yes }}</ref>。
* TTX/FontTools - GlyphWiki来生成IVS对应字体。<ref>{{cite web|url=http://glyphwiki.org/wiki/GlyphWiki:%E3%83%95%E3%82%A9%E3%83%B3%E3%83%88%E7%94%9F%E6%88%90#i9|title=GlyphWiki:フォント生成|accessdate=2011-01-19}}</ref>。
* [[TTEdit|TTEdit]] - 对应生成IVS TrueType字体。

=== 库 ===
2007年10月[[FreeType|FreeType]]以后的开发板内置了[[應用程式介面|API]]工具<ref>{{cite web|url=http://lists.gnu.org/archive/html/freetype-devel/2007-10/threads.html#00016|title=freetype-devel (thread)|date=2007-10-31|accessdate=2008-03-10}}</ref>。

=== 软件 ===
* [[Windows_7|Windows 7]]在[[资源管理器|资源管理器]]的所显示文件名及[[记事本|记事本]]中可以生成异体字字形。但是需要字体支持<ref>{{cite web|url=http://biotronique.jp/techno/computing/unicode_variationselector_windows7|title=Biotronique - Computing - 実は異体字セレクタに対応済のWindows 7|date=2009-12-02|accessdate=2009-12-03}}</ref>
* [[Windows_8|Windows 8]]以后，采用IVS处理<ref>{{cite book|title=Unicode IVS/IVD入門 |author=田丸健三郎, 小林龍生 |isbn=978-4822294830 }}</ref>。
* [[Mac_OS_X_10.5|Mac OS X 10.5]]标准文本和绘制处理是由default ignorable所处理的<ref>{{cite web|url=http://unicode.org/faq/unsup_char.html|title=FAQ - Display of Unsupported Characters|accessdate=2011-01-19}}</ref>異体字セレクタを描画しないが、字形の切り替えはサポートしない。
* [[Mac_OS_X_10.6|Mac OS X 10.6]]开始自建标准文本的绘制处理可支持字形的转换<ref name="lunde2009">{{cite web|url=http://blogs.adobe.com/typblography/2009/08/ivs_ideographic.html|title=IVS (Ideographic Variation Sequence) support in OSes|author=Ken Lunde|accessdate=2011-02-01}}</ref>、Windows 7と同様標準フォントの[[ヒラギノ|ヒラギノ]]は異体字セレクタに未対応である。
* [[Mac_OS_X_Lion|Mac OS X Lion]]（10.7）则采用了adobe - japan1的IVS<ref>{{cite web |url=http://www.screen.co.jp/ga_product/sento/support/otf_ver_hiragino.html |title=ヒラギノとMac OS Xのバージョン相関表 |date=2014-07-08 |accessdate=2014-09-17 }}</ref>。
[[Image:uts37sample.png|thumb]]<!-- 曖昧さ回避不能 -->のお嬢様だ」「[[芦|芦]]」字之下的「戸」分别为[[新字体|新字体]]及[[旧字体|旧字体]]]]
* Alpha（文本编辑器） - 2008年2月在IVS-OTFT测试公开版中，通过将异体字选择器的信息转换为opentype功能标签的信息，对应于由不同体字选择器进行的格里夫的切换。<ref>{{cite web|url=http://alpha.sourceforge.jp/diary/|title=Alpha の бесполезный な日記|date=2008-03-04|accessdate=2008-03-10}}</ref>。
* [[gdi++|gdi++]]
* [[Emacs|Emacs 23]]<ref>{{cite web|url=http://kanji-database.sourceforge.net/emacs/index.html|title=Emacs 23 と Lookup|accessdate=2011-01-19}}</ref>
* [[EmEditor|EmEditor v11]]之后<ref>{{cite web|url=http://jp.emeditor.com/modules/feature1/|title=EmEditor Professional 11 の特長|accessdate=2011-09-24}}{{Dead link|date=2018年9月 |bot=InternetArchiveBot |fix-attempted=yes }}</ref>
* FooEditor （文本编辑器）<ref>{{cite web|url=http://fooeditor.sourceforge.jp/|accessdate=2013-10-13|title=Foo Editor}}</ref>
* [[gPad|gPad]]（文本编辑器）
* [[Mery|Mery]] （文本编辑器）
* [[oedit|oedit]] （文本编辑器）
* [[Adobe_Reader|Adobe Reader 9]]、[[Flash_Player|Flash Player 10]]、[[Adobe_InDesign|Adobe InDesign CS4]]之后的[[Adobe|Adobe]]软件<ref name="lunde2009"/>。
* Windows 7及之上的[[Opera|Opera]]（[[Presto|Presto]]）<ref>{{cite web|url=http://d.hatena.ne.jp/iwaman/20100827/p1|title=Windows7でIVSの表示テスト|accessdate=2011-01-19}}{{Dead link|date=2018年9月 |bot=InternetArchiveBot |fix-attempted=yes }}</ref>
* [[Mozilla_Firefox|Mozilla Firefox]]版本4之后<ref>{{cite web|url=https://bugzilla.mozilla.org/show_bug.cgi?id=552460|title=Bug 552460 - implement Ideographic Variation Sequences support|accessdate=2011-01-19}}</ref>。另外，在版本31以后，改由CJK来实现该功能<ref>{{cite web |url=https://bugzilla.mozilla.org/show_bug.cgi?id=989557 | title=Bug 989557 - Support fallback for CJK Compatibility Ideographs Standardized Variants | accessdate=2014-09-17 }}</ref>。
* [[WebKit|WebKit]]可以支持SVG字体，由SVG字体定义的IVS进行字形切换。这与Opera相同<ref>{{cite web|url=http://d.hatena.ne.jp/mandel59/20100131/1264941470|title=SVGフォントでIVSを表示するテスト|accessdate=2011-01-19}}</ref>。
* [[Microsoft_Office|Microsoft Office]] 2007 - 2010版本需要附加Unicode IVS Add-in for Microsoft Office插件<ref>{{cite web|url=http://ivsaddin.codeplex.com/|title=Unicode IVS Add-in for Microsoft Office|accessdate=2012-11-12}}</ref>，2010之后的默认自带。
* [[LibreOffice|LibreOffice]] 4.1之后/[[Apache_OpenOffice|Apache OpenOffice]] 4.0之后

== 参考资料 ==
{{reflist|2}}

== 延伸阅读 ==
* {{cite book|author=The Unicode Consortium|authorlink=ユニコードコンソーシアム|date=2006-11-03|title=The Unicode Standard, Version 5.0|publisher=Addison-Wesley Professional|id=ISBN 978-0321480910|url=http://www.unicode.org/versions/Unicode5.0.0/}}{{en icon}}
* {{cite book|author=ISO/IEC JTC 1|authorlink=ISO/IEC JTC 1|date=2003-12-15|title=ISO/IEC 10646:2003 Information technology -- Universal Multiple-Octet Coded Character Set (UCS)|url=http://std.dkuug.dk/jtc1/sc2/wg2/}}{{en icon}}
* {{cite book|author=ISO/IEC JTC 1|authorlink=ISO/IEC JTC 1|date=2005-11-18|title=ISO/IEC 10646:2003/Amd 1:2005 Glagolitic, Coptic, Georgian and other characters|url=http://std.dkuug.dk/jtc1/sc2/wg2/}}{{en icon}}
* {{cite book|author=ISO/IEC JTC 1|authorlink=ISO/IEC JTC 1|date=2006-07-04|title=ISO/IEC 10646:2003/Amd 2:2006 N'Ko, Phags-pa, Phoenician and other characters|url=http://std.dkuug.dk/jtc1/sc2/wg2/}}{{en icon}}
* {{cite book|author=日本規格協会|authorlink=日本規格協会|date=2007-12-20|title=JIS X 0221:2007 国際符号化文字集合 (UCS)|url=http://www.jisc.go.jp/app/JPS/JPSO0020.html|access-date=2018-08-21|archive-url=https://web.archive.org/web/20090524211408/http://www.jisc.go.jp/app/JPS/JPSO0020.html|archive-date=2009-05-24|dead-url=yes}} 上記3資料を併合して日本語訳したもの。

== 参见 ==
* [[字体|字体]]
* [[組合字符|組合字符]]
* [[控制字符|控制字符]]
* [[中日韓統一表意文字|中日韓統一表意文字]]
* [[中日韓相容表意文字|中日韓相容表意文字]]

== 外部链接 ==
* [http://www.unicode.org/Public/UNIDATA/StandardizedVariants.txt Standardized Variants - Unicode]{{en icon}} (已录入的SVS一覧) 
* [http://www.unicode.org/reports/tr37/ Unicode Technical Standard #37 - UNICODE IDEOGRAPHIC VARIATION DATABASE]{{en icon}} (IVD结构和注册程序) 
* [http://www.unicode.org/ivd/index.html Ideographic Variation Database - Unicode]{{en icon}} (关于IVD) 
* [http://www.unicode.org/ivd/data/2017-12-12/IVD_Sequences.txt  IVD Sequences - Unicode] (2017-12-12版) {{en icon}} (IVD登记的汉字的组合列表) 
* [https://747.github.io/vsselector/ 異体字选择器] - 搜索SVS・IVS所有可用的变体。

[[Category:Unicode|Category:Unicode]]