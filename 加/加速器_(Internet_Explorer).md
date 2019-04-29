{{NoteTA
|G1=IT
}}
<div style="font-family:'microsoft yahei';">
{{Infobox file format
|name=加速器
|logo=
|screenshot=
|caption=在[[Windows_7|Windows 7]]中使用IE 9中加速器功能和[[Bing翻译|Bing翻译]]翻译选中句子
|owner=[[微软|微软]]
|latest_release_version = 0.8
|extended from=[[XML|XML]]
|free=yes
}}
</div>
'''加速器'''（{{lang|en|Accelerator}}）是由[[微软|微软]]于[[Internet_Explorer_8|Internet Explorer 8]]中引入的一种{{link-en|搜索选定内容|Selection-based search}}（{{lang|en|Selection-based search}}）的方式，它可使用户仅通过鼠标就能调用任意第三方页面的在线服务<ref>{{cite web | url = http://www.microsoft.com/windows/products/winfamily/ie/ie8/readiness/NewFeatures.htm | title = New and exciting features | accessdate = 2008-03-05 | publisher = [[微软|微软]]}}</ref>。当用户选中文本或其它对象时，加速器图标将会出现，之后用户就可为所选对象调用可用的加速器服务（例如使用选中文字写blog或者查看选中地理位置的地图）。[[微软|微软]]称，加速器使用户不必再在网页之间进行复制粘贴。<ref>{{cite web | url = http://blogs.zdnet.com/microsoft/?p=1241 | title = IE 8 to feature WebSlices, Activities | author = Mary Jo Foley | publisher = [[CNET|CNet]] Blogs | accessdate = 2007-03-05}}</ref>IE8指定了一种[[XML|XML]]编码方式，使[[网络应用|网络应用]]或[[网络服务|网络服务]]可以加速器的形式被调用，而服务将被如何调用及调用后展示什么类型的内容，则会由XML文件指定。<ref>{{cite web | url = http://www.microsoft.com/windows/products/winfamily/ie/ie8/readiness/DevelopersNew.htm | title = How do I make my site 'light up' with Internet Explorer 8? | publisher = [[微软|微软]] | accessdate = 2008-03-05}}</ref>已有人指出了加速器和曾在[[Internet_Explorer_6|IE6 Beta版]]中测试却因争议批评后而取消（虽然后来包括了在[[Microsoft_Office|Microsoft Office]]中）的[[智能标记|智能标记]]间的相似特性。<ref>{{cite web|url=http://www.winsupersite.com/reviews/ie8_beta1.asp |title=Internet Explorer 8 Beta 1 Review |author=Paul Thurrott |publisher=Windows IT Pro |accessdate=2008-03-12 |deadurl=yes |archiveurl=https://web.archive.org/web/20080314225106/http://www.winsupersite.com/reviews/ie8_beta1.asp |archivedate=2008-03-14 }}</ref>

== 历史 ==

微软在IE8 Beta1中以“{{lang|en|activities}}”为名引进加速器，后来其改名“{{lang|en|accelerators}}”。

==IE8==
加速器默认以加载项的类型被包括。

===示例加速器===
这是一个使用OpenService格式的地图加速器示例：

<source lang="xml">
<?xml version="1.0" encoding="UTF-8"?>
<openServiceDescription ns="http://www.microsoft.com/schemas/openservicedescription/1.0">
  <homepageUrl>http://www.example.com</homepageUrl>
  <display>
    <name>Map with Example.com</name>
    <icon>http://www.example.com/favicon.ico</icon>
  </display>
  <activity category="map">
    <activityAction context="selection">
      <preview action="http://www.example.com/geotager.html">
        <parameter name="b" value="{selection}"/>
        <parameter name="clean" value="true"/>
        <parameter name="w" value="320"/>
        <parameter name="h" value="240"/>
      </preview>
      <execute action="http://www.example.com/default.html">
        <parameter name="where1" value="{selection}" type="text"/>
      </execute>
    </activityAction>
  </activity>
</openServiceDescription>
</source>

==参见==
*[[智能标记|智能标记]]
*[[Ubiquity|Ubiquity]]

==参考资料==
{{reflist}}

==外部链接==
* [http://www.microsoft.com/windows/internet-explorer/videos.aspx?mname=accelerators Accelerators Video], [[微软|微软]]的 [[Internet_Explorer_8|Internet Explorer 8]]视频
* [https://web.archive.org/web/20100601091430/http://www.ieaddons.com/en/accelerators/ Add-ons Gallery: Accelerators], [[微软|微软]][[Internet_Explorer_8|Internet Explorer 8]]

===开发===
* [http://msdn.microsoft.com/en-us/library/cc289775(VS.85).aspx OpenService Accelerators Developer Guide]
* [http://www.microsoft.com/windows/internet-explorer/readiness/developers-new.aspx#accelerators Accelerators], Internet Explorer 8 Readiness Toolkit

===维基媒体基金会加速器===
* [https://web.archive.org/web/20110412190025/http://www.ieaddons.com/en/details/searchhelpers/Wikipedia_Visual_Search/ Wikipedia Visual Search], IE8 Addons Gallery
* [https://web.archive.org/web/20100113034640/http://ieaddons.com/en/details/dictionaries/Define_with_Wikipedia/ Define with Wikipedia], IE8 Addons Gallery
* [https://web.archive.org/web/20100113140752/http://ieaddons.com/en/details/dictionaries/Define_with_Wiktionary/ Define with Wiktionary], IE8 Addons Gallery
* [https://web.archive.org/web/20110106025104/http://www.ieaddons.com/en/details/photosvideos/Veoh_Video_Compass/ Veoh Video Compass], IE8 Addons Gallery <!-- This one does support Wikipedia search -->

{{microsoft}}
{{Internet Explorer}}
[[category:Internet_Explorer|category:Internet Explorer]]