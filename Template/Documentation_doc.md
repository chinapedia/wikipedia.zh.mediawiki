{{NoteTA|G1=MediaWiki|G2=IT}}{{Documentation subpage}}{{High-use|1=20550}}{{Uses Lua|Module:Documentation}}
==概要==
{{See also|Wikipedia:模板文件頁模式}}
这个模板自动显示“模板文档”框，就像你现在看到的这样，文档框中的内容由其它页面生成。
==參數及使用方法==
# 在主模板中增加<code>&lt;noinclude&gt;&#123;{Documentation}&#125;&lt;/noinclude&gt;</code>。
# 点击“编辑”链接，它将打开<tt>/doc</tt>子页面，并在那里填写文档。
# 將分類增加在<tt>/doc</tt>子頁面的<code>&lt;includeonly&gt;&lt;/includeonly&gt;</code>中。
===正常的/doc子页面===
 &lt;noinclude&gt;&#123;&#123;{{{template-name|Documentation}}}&#125;&#125;&lt;/noinclude&gt;
===任意/doc子页面===
 &lt;noinclude&gt;&#123;&#123;{{{template-name|Documentation}}}|Template:any page/doc&#125;&#125;&lt;/noinclude&gt;
===内联内容===
 &lt;noinclude&gt;&#123;&#123;{{{template-name|Documentation}}}|content=这是一个文档。&#125;&#125;&lt;/noinclude&gt;
===有[查看][编辑]链接的内联内容===
 &lt;noinclude&gt;&#123;&#123;{{{template-name|Documentation}}}
 |1 = Template:模板名/doc
 |content =&#123;&#123;Template:模板名/doc|参数}}
 }}&lt;/noinclude>
===最佳用法===
此代码应该放置在模板代码的底部“<code>&lt;noinclude></code>”之前且不加多余的空格（否则会导致使用该模板的页面上出现多余空格）。参数可以像上面这样来使用以包含任意文档页。
用于模板本身的分类链接应该用 <code>&lt;includeonly> &lt;/includeonly></code> 标签来添加到文档页面。
更复杂的案例请参见 [[Wikipedia:模板文件頁模式#分类链接]]。
如果文档页包含 <code>includeonly</code> 或 <code>noinclude</code> 标签并作为文档的一部分，请用“<code>&amp;lt;</code>”替代“<code><</code>”。

請勿在/doc子頁面裡再掛上{{tlx|Documentation}}，以避免出錯
==重定向==
*{{Tl|Doc}}
*{{Tl|Documentation, template}}
*{{Tl|Documentations}}
*{{Tl|Template doc}}
*{{Tl|Template doc page}}
*{{Tl|Template doc page transcluded}}
*&#123;&#123;[[Template:模板文件|-{模板文件}-]]&#125;&#125;
*&#123;&#123;[[Template:模板文档|-{模板文档}-]]&#125;&#125;
*{{Tl|帮助文档}}
<includeonly>{{Sandbox other||
[[Category:模板說明文件|D]]
[[Category:模板頁的模板|D]]
[[Category:Lua模板|D]]
}}</includeonly>
<templatedata>
{
	"params": {},
	"description": "顯示模板文件框",
	"format": "inline"
}
</templatedata>