{{NoteTA|G1=MediaWiki}}{{Documentation subpage}}
{{Intricate template}}
{{缺乏中文說明}}
{{High-use|2466}}
==概要==
{{Tl|Archives}}可以在討論頁添加子頁面的存檔連結，默認情況下如果子頁面名稱恰當，它會自動偵測存檔子頁面。
==參數及使用方法==
 <nowiki>{{Archives
| archivelist = <!-- 存檔頁面 -->
| auto        = <!-- short/long/no -->
| index       = <!-- /Archive index -->
| list        = 
| search      = <!-- yes/no -->
| root        =
| prefix      =
| collapsible = <!-- yes/no -->
| collapsed   = <!-- yes/no -->
| editbox     = <!-- yes/no -->
| box-width   =
| style       = 
| title       = 
| image       = 
| image-size  =
| alt         = 
| link        = 
| target      = 
| bot         = 
| age         = 
| units       = <!-- time units (defaults to days) -->
| 
}}</nowiki>
{{HideH|沒有翻譯的內容|
=== Archive list ===
; archivelist:指定子页的链接,例如“/ archivelist”,包含档案列表。
; auto= <short|long|no>: 指定的格式自动生成归档列表。如果未指定,默认是“长”;其他任何词(“不”除外)将导致“短”和“不”禁用自动侦测。
; index:链接指定的子页“档案”称号,如“/归档指数”,应该是所有归档的主题索引页的讨论。
[[用户:Legobot | Legobot]]可用于创建和维护一个索引。
; list: Inline list of archives. The ''list'' parameter overrides automatic archive detection of pages named "Archive 1", "Archive 2" and so on.
; (1st unnamed parameter): Can be used in addition to automatic archiving if additional pages with other names are available.

With no explicit parameters, the archive list presented in the box is determined automatically. If a subpage called "<code><nowiki>{{PAGENAME}}</nowiki>/archivelist</code>" exists, it will be used as the central content of the box. For an example, see <del>[[Talk:Evolution]]</del>, which [not currently] draws from [[Talk:Evolution/archivelist]]. The ''archivelist'' parameter changes the name of this subpage.

If no archive list subpage is detected, numbered archive subpages will be listed in long format. Such pages must be named as "/Archive #" because other naming styles will not be detected. The "<code>long</code>" auto format (the default) indicates "Archive 1", "Archive 2", and so on. The "<code>short</code>" auto format indicates only the archive number. See more examples below.

An additional list of archives can be passed in the first unnamed parameter, avoiding the need for a subpage.

Using "auto=no" will disable archive auto-detection. Manually specified archives will still be shown. [The archive box will also contain an "Edit" link, targeted at the archive list subpage, which can then be used to begin manually populating the list, if desired. This seems broken.]

==== Additional notes ====
The "<code>auto</code>" and "<code>archivelist</code>" parameters are not intended to be used together. (Doing so does not use the specified archive list page.)

The auto-generated archive list requires subpages to use the common naming convention. That is, "<nowiki>{{PAGENAME}}</nowiki>/Archive 1", "<nowiki>{{PAGENAME}}</nowiki>/Archive 2", and so on. The letter "A" must be capitalized, there must be a single space between the word "Archive" and the number, and there must be no leading zeros. If archive subpages do not conform to this convention, they can be [[Help:Moving a page|renamed]] to conform, or a manual list can be maintained.

Specifying "<code>auto</code>" with any right-hand-side value other than "<code>long</code>" or "<code>no</code>" results in the short-format list; the use of "<code>short</code>" as the value just makes things more obvious to others.

=== Icon image ===
; image : An alternate image to be used, defaults to "<code><nowiki>Replacement filing cabinet.svg</nowiki></code>". May also use '''image-size'''.
; alt : Alt text for the image, for visually impaired readers. See [[WP:ALT]]. This defaults to empty. If a nonempty value is specified for <code>link</code>, <code>alt</code> should be nonempty too, and should indicate what will happen if the user clicks on the image.
; link : Link for the image. This normally defaults to empty, which means no link. However, if <code>alt</code> is nonempty, it defaults to the image's file page.

The ''link'' and ''alt'' parameters only take effect if the image is changed from the default.

=== Search ===
; search: If ''yes'', adds a search box to the template. 
; root: Specify a different base than <code>{&#123;FULLPAGENAME}}/</code>.  Use '''prefix''' if the addition of a trailing slash is not desired.
;search-break: ''Default'':no
;search-width: ''Default'':22
;search-button-label: ''Default'': Search

=== Archival method ===
; target: The title of the page (just the name, no link syntax) that threads are currently being archived to, for manual archiving.
; bot : If specified, a note about automatic archiving will be shown.
; age : If specified, this will be displayed as the archiving delay.
; units : If specified, this will be displayed units for the archiving delay. The default is "days".

=== Other parameters ===
; collapsible : If ''yes'', makes the list [[Help:Collapsing|collapsible]].
; collapsed : If ''yes'', makes the list collapsed.
; style : An arbitrary string of CSS can be applied to the box (use with care). May also use '''box-width'''.
; title : An alternative title, defaults to "Archives". The title is automatically linked to the archive index page if one is specified, otherwise a wiki link may be specified here.
; editbox : If ''yes'' or omitted, includes a button to edit the archive box's sub-page /archivelist.
{{HideF}}
==範例==
===默認情況===
<syntaxhighlight lang=moin>{{Archives}}</syntaxhighlight>
{{Archives}}
{{Clear}}
===添加參數===
<syntaxhighlight lang=moin>{{Archives|auto=short|index=/Archive index}}</syntaxhighlight>
{{Archives|auto=short|index=/Archive index}}
{{Clear}}
==參見==
{{Warchivenav}}
<includeonly>{{Sandbox other||
[[Category:存檔模板]]
[[Category:討論頁模板]]
}}</includeonly>
<templatedata>
{
	"params": {
		"archivelist": {
			"label": "子頁面名稱",
			"description": "討論頁存檔的子頁面名稱",
			"example": "/存檔",
			"type": "content"
		}
	},
	"description": "提供討論頁存檔子頁面連結的模板",
	"format": "inline"
}
</templatedata>