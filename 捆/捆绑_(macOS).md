{{TA|G1=IT}}
[[NeXTSTEP|NeXTSTEP]]，[[Mac_OS_X|Mac OS X]]和[[GNUStep|GNUStep]]中，'''捆绑'''（Bundle）是一个目录（也可能是一个文件），它允许相关资源（例如[[可执行代码|可执行代码]]，[[本地化|本地化]]资源，[[图片|图片]]等）被组合在一起，在某些情况下可以当作一个单独文件看待。在[[Mac|Mac]]中，该特性在[[Mac_OS_9|Mac OS 9]]中引入，被称为“包”（package），它类似于[[RISC_OS|RISC OS]]和[[ROX_Desktop|ROX Desktop]]中[[应用程序目录|应用程序目录]]的特性，以及使用[[SpatialBundle|SpatialBundle]]技术的[[Ubuntu|Ubuntu]]和[[Debian|Debian]]等[[Linux发行版|Linux发行版]]。

[[应用程序|应用程序]]，[[应用程序框架|应用程序框架]]和[[插件|插件]]通常以捆绑的形式将其内部文件组织在一起，同时，文档也可以构成框架。在[[NeXT|NeXT]]的Foundation工具包和[[Cocoa|Cocoa]]的Foundation框架中，可以使用<tt>NSBundle</tt>类操作捆绑；在[[Core_Foundation|Core Foundation]]中，则使用<tt>CFBundle</tt>系列函数进行操作。

捆绑通常包含一个可执行代码文件和一些资源文件，例如[[Interface_Builder|NIB文件]]，图像，声音，[[本地化|本地化]]字符串，配置文件（通常是[[属性列表文件|属性列表文件]]）和其它媒体。在其它系统上，例如[[Microsoft_Windows|Microsoft Windows]]，这些资源通常在编译时就被直接包含在了可执行文件中。[[Mac_OS_X|Mac OS X]]从[[NeXTSTEP|NeXTSTEP]]中引入了捆绑的概念，用以代替早期[[Mac_OS|Mac OS]]中以[[资源分支|资源分支]]存储附加[[元数据|元数据]]的技术。多数类型的捆绑在使用时与普通文件类似，从而减少了其内部文件意外更改或丢失的风险。同时，捆绑的另一个意义在于可以使用文件夹简化组织资源的方式，避免使用资源分支导致的额外的复杂性。

捆绑的[[统一类型标识符|统一类型标识符]]是<tt>com.apple.bundle</tt>，而包的则是<tt>com.apple.package</tt>。

==Mac OS X中的应用程序捆绑==

应用程序捆绑通常为[[软件包|软件包]]，以单一文件的形式出现在用户面前。这个“文件”实际上是一个以<tt>.app</tt>为扩展名的文件夹。[[辅助点按|辅助点按]]这个包，然后选择“显示包内容”，即可以文件夹的形式打开该捆绑并查看、修改其内容。对于应用程序，捆绑中的唯一一个一级子目录通常是<tt>Contents</tt>。在<tt>Contents</tt>中，通常有另外一些目录，包括可执行文件目录（在Mac中为<tt>MacOS</tt>，GNUStep中则为应用程序的名字），资源目录（<tt>Resources</tt>）等。资源目录中通常包含了程序所需的本地化资源，包括字符串文件（<tt>.strings</tt>文件），[[Interface_Builder|nib文件]]等等。

其它常见的子目录包括<tt>Plugins</tt>，<tt>Frameworks</tt>和<tt>Shared Frameworks</tt>。<tt>Frameworks</tt>包括了该程序使用的框架，程序运行时会首先查找此处的框架而不是优先使用系统提供的，可以在一定程度上避免类似[[DLL地狱|DLL地狱]]的情况发生。<tt>Shared Frameworks</tt>目录包含了可以由本程序和其它程序使用的框架，同时，与<tt>Frameworks</tt>不同，只会在无法在系统中找到更新的版本时使用。<tt>Plugins</tt>目录则包含了程序使用的插件。

==Mac OS X中的框架捆绑==
Mac OS X中的框架也以捆绑的形式储存。框架中的[[动态库|动态库]]代码储存在与框架同名的文件中，放置于顶层目录中；顶层目录中也可能包含<tt>Headers</tt>，储存了该框架提供的[[头文件|头文件]]。

==Mac OS X中的可载入捆绑==
'''可载入捆绑'''即包含可以在运行时载入的代码的捆绑<ref>[http://developer.apple.com/documentation/Cocoa/Conceptual/LoadingCode/Concepts/AboutLoadableBundles.html Code Loading Programming Topics for Cocoa: About Loadable Bundles<!-- Bot generated title -->] {{webarchive|url=https://web.archive.org/web/20080905204925/http://developer.apple.com/documentation/Cocoa/Conceptual/LoadingCode/Concepts/AboutLoadableBundles.html |date=2008-09-05 }}</ref>，其扩展名通常为<tt>.bundle</tt>，常常被用作[[插件|插件]]。

==其它捆绑格式==
其它的一些捆绑包括包含图形的，以<tt>.rtfd</tt>为扩展名的[[RTF文件|RTF文件]]，[[Safari|Safari]]的下载未完成的文件等。[[GarageBand|GarageBand]]，[[Keynote|Keynote]]，[[Pages|Pages]]，[[Numbers|Numbers]]，[[iMovie|iMovie]]和[[Xcode|Xcode]]等程序的部分版本中，项目文件亦存储为捆绑。在[[iWork|iWork '09]]版中，其文件为一压缩的捆绑，可以将其解压后查看内部结构<ref>[http://www.macosxhints.com/article.php?story=20090225034801527 Open iWork' 09 flat files as folders]</ref>；另外，[[Microsoft_Office|Microsoft Office]] 2007引入的新文件格式也采用了类似的技术。

Apple's installer packages (<tt>.pkg</tt>) are bundles that contain <tt>[[pax_(program)|pax]]</tt> archives.  See [[Installer_(Mac_OS_X)|Installer (Mac OS X)]].
苹果安装器包（<tt>.pkg</tt>）是包含<tt>[[pax|pax]]</tt>归档文件的捆绑，参见[[Installer_(Mac_OS_X)|Installer (Mac OS X)]]。

Linux发行版[[Super_OS|Super OS]]使用[[RUNZ|RUNZ]]格式的捆绑。

==参考文献==
{{reflist}}

==参见==
* [[Application_Directory|Application Directory]] — [[RISC_OS|RISC OS]]中的应用程序捆绑
* [[klik|klik]] — 一个使用类似原理的Linux程序
* [[RUNZ|RUNZ]]
* [[SpatialBundle|SpatialBundle]] 采用“一个文件，一个程序”哲学的用于Linux的可移植程序

==外部链接==
* [http://developer.apple.com/mac/library/documentation/CoreFoundation/Conceptual/CFBundles/Introduction/Introduction.html Bundle Programming Guide] at Apple Developer Connection
* [http://www.gnustep.org/resources/documentation/Developer/Base/Reference/NSBundle.html NSBundle documentation] from the GNUstep project
* [http://www.sveinbjorn.org/platypus Platypus] — a tool to create application bundles around scripts
* [http://www.bgdna.com/ Tech News]{{dead link|date=2018年3月 |bot=InternetArchiveBot |fix-attempted=yes }} — new technology news information with reviews

[[Category:MacOS|Category:MacOS]]