{{noteTA
|G1=IT
}}
{{selfref|關於維基姊妹計劃間的-{zh-tw:連結;zh-cn:链接;}-的使用，參見[[Wikipedia:维基项目间链接|Wikipedia:维基项目间链接]]}}
'''跨Wiki链接'''（'''{{lang|en|InterWiki links}}'''）是一种将[[万维网|万维网]]上的众多[[Wiki|Wiki]]网站链接到一起的方式。用户可以不用输入完整的[[统一资源定位符|URL]]（一般网页都需要）而使用相似的简写就能在同一Wiki网站内相互链接。

与互联网上的[[域名|域名]]不同，并不存在一个全球统一定义的跨Wiki前缀——并且Wiki用户必须准确定义他们所需的映射。用户通常得设立不同的帐户以便在各个Wiki部分中使用（除非他们想匿名编辑）。文本之间各式各样的格式和版面都会对于Wiki部分间的无缝链接产生阻碍。

为使某些特殊群体成员更简便地输入Wiki链接，以下一些特征有助于将不同的Wiki部分更紧密地联接。为了进一步实现这个目标，跨Wiki“巴士漫游”（类似于{{tsl|en|webring||webring}}）被用于解释和说明此目标并将不同的Wiki部分高亮显示。在[[中文维基百科|维基百科]]中的例子包括[[Wikipedia:观光巴士站|Wikipedia:观光巴士站]]以及{{tsl|en|Wikipedia:WikiNode|Wikipedia:WikiNode}}。

== 符号 ==
跨Wiki符号很大程度上因Wiki使用者的''链接模式''而不同。其中最重要的两种链接模式是[[駝峰式大小寫|駝峰式大小寫]]及自由链接（指被[[分隔符|分隔符]]分开的任意词语，比如<nowiki>{{tsl|en|</nowiki>double square brackets<nowiki>|</nowiki>双方括号<nowiki>}}</nowiki>).

相应地，基于駝峰式大小寫的跨Wiki链接常以这种形式出现：“信号:页面名称”，在这里''信号''是另一Wiki部分的跨映射前缀。因此，像这样一个链接:“Wikipedia:InterWiki”就能够做为[[HTML|HTML]]指向[[维基百科|Wikipedia]]中的某篇文章，比如[[Wikipedia:跨语言链接|Wikipedia:跨语言链接]]。以駝峰式大小寫Wiki方式链接到的页面标题中的空格应以下划线代替（比如WikiPedia:Main_Page）。

Wiki网站中的基于自由链接的跨Wiki链接，比如说维基百科，同样地遵守这样的原则，但是分隔符在这种情况下用于网站内部链接。这些链接如果用作内部链接将会被解析和转换为它们的本原，这使得输入变得容易，但是这可能会同其它一些特殊符号起冲突。比如在维基百科中，<code><nowiki>[[MeatBall:AssumeGoodFaith|MeatBall:AssumeGoodFaith]]</nowiki></code>会显示为{{tsl|en|Meatball:AssumeGoodFaith|}},<nowiki>{{tsl|de|InterWiki|}}</nowiki>（以前的语法为：<code><nowiki>[[DeWikipedia:InterWiki|DeWikipedia:InterWiki]]</nowiki></code>）将显示为{{tsl|de|InterWiki|}}.

[[MediaWiki|MediaWiki]]软件有一个附加属性，它使用类似的符号以创建自动的跨语言链接－比如说链接<nowiki>[[de:InterWiki|de:InterWiki]]</nowiki>（开头没有冒号）会自动创建一个标签“其它语言:{{tsl|de|InterWiki|Deutsch}}”于文章顶端和底端。不同种类的其它[[Wiki软件|Wiki软件]]也有一些用于这种“半内部”链接的特性，比如像对于[[名字空间|名字空间]]或者多种的子社区的支持。

== 实现 ==
就内部而言，使用跨Wiki链接的Wiki网站需要有一个“跨映射”来定义从Wiki代码到URLs的映射。比如，<code><nowiki>[[MeatBall:InterWiki|MeatBall:InterWiki]]</nowiki></code>将会显示为[[MeatBall:InterWiki|MeatBall:InterWiki]]，但却链接到''<nowiki>http://usemod.com/cgi-bin/mb.pl?InterWiki</nowiki>''。

因为大部分的Wiki系统在个人网页上使用URL，这些页面的标题将会以一个不变的地址出现于页面底部，因此定义这种映射的最简单办法就是将URL的不变部分以跨Wiki前缀来代替。所以在上述的例子中，<code>MeatBall</code>仅以''<nowiki>http://usemod.com/cgi-bin/mb.pl?</nowiki>''代替就可以创建一个[[HTML|HTML]]链接目标。

尽管如此，在使用特殊符号的时候还是要小心，这包含两个方面，一是作为本地链接模式规则的例外，一是作为目标系统中的必须被用来专门代表URL的符号。所以基于駝峰式大小寫的Wiki网站必须使用特殊规则来识别能作为跨Wiki链接一部分的非[[字母和数字|字母和数字]]符号，并且甚至连自由链接系统也可能因技术上的原因不允许某些符号如“+”包含在本地链接中。同样的，像“?”和“&”诸如此类的符号在URLs中是受到特别对待的，当用于Wiki中时需要转换成某些其它的不常用符号，在连接不同的网址时使用不同的[[符号编码|符号编码]]。

然而，与为每个Wiki部分创建新的列表以代替擦除的符号相比，从其它站点复制一份显得更为有用。像[[MeatballWiki|MeatballWiki]]和[[用户模式Wiki|用户模式Wiki]]等站点包含有一些用于此目的的全面的列表--前一种同其它Wiki网页一样被公开地编辑，后一种易于检查但是已有落伍之嫌了。

MeatBallWiki使用一种叫做[[文档替换|文档替换]]机制直接适用于公开编辑它自身的跨Wiki映射。映射的变化并不会立刻显现，但是跨映射的结构文档会在规定时间内没有被编辑的情况下重新提交。这种延迟意在确保所有的改变都得到显现但并无碍于公开编辑。

== 非Wiki网站的速记 ==
绝大部分跨映射实现仅仅是用完整URL的前缀来代替跨Wiki的前缀，如此多的非Wiki网站也同样可以使用这种系统。比如说在[[自由的在线计算机词典|自由的在线计算机词典]]上对某定义的参考资料能够以这样的形式出现：<code><nowiki>[[Foldoc:foo|Foldoc:foo]]</nowiki></code>，这会告诉系统将“foo”指向''<nowiki>http://www.foldoc.org/foldoc.cgi</nowiki>''，并将链接显示为[[Foldoc:foo|Foldoc:foo]]。这使得从Wiki网页内链接一般参考资源变得非常容易，这不需要对URL形式的有多少了解。

同样应注意的是跨Wiki概念能相应地应用于来自非Wiki网站的链接，比如{{tsl|en|Advogato|Advogato}}，它提供了一种基于MeatBall-derived跨映射的速记语法。

== 外部链接 ==
* [[meta:Interwiki_map|Wikipedia's InterWiki map]]
* [[MeatBall:InterMap|Discussion of the InterWiki concept]] at [[MeatballWiki|MeatballWiki]]
* [http://interwiki.wiki.taoriver.net/ The InterWiki Wiki]
* [[MeatBall:FileReplacement|Discussion of the FileReplacement concept]]

{{Wiki主题}}
[[Category:Wiki|*]]