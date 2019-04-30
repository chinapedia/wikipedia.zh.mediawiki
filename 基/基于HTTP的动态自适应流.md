{{NoteTA
|G1=IT
}}
{{校对翻译}}
'''基于HTTP的动态自适应流'''（{{lang-en|'''Dynamic Adaptive Streaming over HTTP'''}}，缩写'''DASH'''，也称'''MPEG-DASH'''）是一种[[自適性串流|自适应比特率串流]]技术，使高质量[[流媒体|流媒体]]可以通过传统的[[超文本传输协议|HTTP]]网络服务器以[[互联网|互联网]]传递。类似[[苹果公司|苹果公司]]的[[HTTP_Live_Streaming|HTTP Live Streaming]]（HLS）方案，MPEG-DASH会将内容分解成一系列小型的基于HTTP的文件片段，每个片段包含很短长度的可播放内容，而内容总长度可能长达数小时（例如电影或体育赛事直播）。内容将被制成多种比特率的备选片段，以提供多种比特率的版本供选用。当内容被MPEG-DASH客户端回放时，客户端将根据当前网络条件自动选择下载和播放哪一个备选方案。客户端将选择可及时下载的最高比特率片段进行播放，从而避免播放卡顿或重新缓冲事件。也因如此，MPEG-DASH客户端可以无缝适应不断变化的网络条件并提供高质量的播放体验，拥有更少的卡顿与重新缓冲发生率。

MPEG-DASH是首个基于HTTP的自适应比特率串流解决方案，它也是一项国际标准。<ref name="MPEGPressRelease">{{cite news|url=http://mpeg.chiariglione.org/meetings/geneva11-1/geneva_press.htm|title=MPEG ratifies its draft standard for DASH|date=2011-12-02|publisher=MPEG|accessdate=2012-08-26|deadurl=yes|archiveurl=https://web.archive.org/web/20120820233136/http://mpeg.chiariglione.org/meetings/geneva11-1/geneva_press.htm|archivedate=2012-08-20}}</ref>MPEG-DASH不应该与传输协议混淆——MPEG-DASH使用TCP传输协议。

MPEG-DASH使用现有的HTTP网络服务器基础设施。它允许如[[互联网电视|互联网电视]]、电视[[机顶盒|机顶盒]]、[[台式电脑|台式电脑]]、[[智能手机|智能手机]]、[[平板电脑|平板电脑]]等设备消费通过互联网传送的多媒体内容（如[[视频|视频]]、[[电视|电视]]、[[广播|广播]]等），并可应对变动的互联网接收条件。自适应流解决方案的标准化是为向市场提供信心，使该解决方案可以用于通用部署，抗衡类似但更专有的解决方案，如微软Smooth Streaming与Adobe的HDS。

不同于HLS、HDS和Smooth Streaming，DASH不关心[[编解码器|编解码器]]，因此它可以接受任何{{le|编码格式|Video coding format}}编码的内容，如[[高效率视频编码|H.265]]、[[H.264/MPEG-4_AVC|H.264]]、[[VP9|VP9]]等。<ref name="vs">{{cite web|url=https://bitmovin.com/mpeg-dash-vs-apple-hls-vs-microsoft-smooth-streaming-vs-adobe-hds/|title=MPEG-DASH vs. Apple HLS vs. Microsoft Smooth Streaming vs. Adobe HDS|accessdate=3 June 2016|date=2015-03-29}}</ref>

== 标准化 ==

MPEG-DASH技术在[[MPEG|MPEG]]之下开发。对DASH的工作始于2010年。2011年1月，它成为一项国际标准草案，并在2011年11月成为国际标准。<ref>[http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=57623 ISO/IEC DIS 23009-1.2 Dynamic adaptive streaming over HTTP (DASH)]</ref>MPEG-DASH标准已于2012年4月发布为[http://standards.iso.org/ittf/PubliclyAvailableStandards/c057623_ISO_IEC_23009-1_2012.zip ISO/IEC 23009-1:2012]。

DASH是一项与[[Adobe_Systems|Adobe Systems]] [[自適性串流|HTTP Dynamic Streaming]]、[[蘋果公司|蘋果公司]][[HTTP_Live_Streaming|HTTP Live Streaming]]（HLS）[[微软|微软]][[自適性串流|Smooth Streaming]]相关的技术。DASH基于[[3GPP|3GPP]]第9版中的Adaptive HTTP streaming（AHS）和{{tsl|en|Open IPTV Forum}} Release 2中的HTTP Adaptive Streaming（HAS）。<ref name="3GPP">ETSI 3GPP [http://www.3gpp.org/ftp/Specs/html-info/26247.htm 3GPP TS 26.247; Transparent end-to-end packet-switched streaming service (PSS); Progressive Download and Dynamic Adaptive Streaming over HTTP (3GP-DASH)]</ref><ref>[http://www.oipf.tv/live/oipf/release_2.html Open IPTV Forum Solution Specification Volume 2a – HTTP Adaptive Streaming V2.1] {{webarchive|url=https://web.archive.org/web/20111009063030/http://www.oipf.tv/live/oipf/release_2.html |date=2011-10-09 }}</ref>作为与MPEG协作的一部分，3GPP Release 10采用DASH（具有特定的编解码器和操作模式）用于无线网络。<ref name="3GPP" />

DASH行业论坛（{{tsl|en|DASH-IF}}）<ref name="dashif">[http://www.dash-if.org DASH Industry Forum]</ref>进一步促进和催化了MPEG-DASH的采用，并帮助将其从规范转变为实际业务。主要的流媒体和媒体公司，包括微软、Netflix、Google、爱立信、三星、Adobe等都在实际业务中尝试使用，并为不同使用环境创建了DASH使用指南。

MPEG-DASH也被集成在其他标准中，例如[[Hybrid_Broadcast_Broadband_TV|HbbTV]]中的MPEG-DASH支持（截至1.5版本）。<ref name="hbbtv">[http://www.hbbtv.org/pages/about_hbbtv/HbbTV-specification-1-5.pdf HbbTV Specification 1.5] {{webarchive|url=https://web.archive.org/web/20140703212343/http://www.hbbtv.org/pages/about_hbbtv/HbbTV-specification-1-5.pdf |date=2014-07-03 }}</ref>

== 概述 ==
DASH是一项[[自適性串流|自適性串流]]技术，其将[[多媒体|多媒体]]文件分割为一个或多个片段，并使用[[超文本传输协议|超文本传输协议]]传递给客户端。<ref>[http://mpeg.chiariglione.org/technologies/mpeg-b/mpb-dash/index.htm Overview of Dynamic Adaptive Streaming over HTTP (DASH)]</ref>
媒体演示描述（MPD）描述片段信息（计时、[[统一资源定位符|统一资源定位符]]，以及媒体特征，例如视频分辨率和[[比特率|比特率]]），并且可以根据使用环境以不同的方式组织，例如SegmentList, SegmentTemplate, SegmentBase和SegmentTimeline。<ref>[http://www.bitcodin.com/blog/2015/04/mpeg-dash/ MPEG-DASH Overview]</ref>
片段可以包含任何媒体数据，但是规范提供了与两种容器类型一起使用的特定指导和格式：{{tsl|en|ISO base media file format|ISO基础媒体文件格式}}（例如MP4文件格式）或[[MPEG2-TS|MPEG-2传输流]]。

DASH不关心音频/视频的[[编解码器|编解码器]]。多媒体文件通常有一种或多种表示（即不同分辨率或比特率版本），并可基于不同的[[计算机网络|网络]]条件、设备功能和用户偏好进行选择，达到[[自適性串流|自適性串流]]<ref>[http://www.mmsys.org/?q=node/43#mmt1 3GPP Dynamic Adaptive Streaming over HTTP – Standards and Design Principles] {{webarchive|url=https://web.archive.org/web/20160805222811/http://www.mmsys.org/?q=node%2F43 |date=2016-08-05 }} by T. Stockhammer</ref>和{{tsl|en|Fairness_measure#QoE_fairness||QoE (Quality of Experience) fairness}}。<ref>[https://scholar.google.com/citations?view_op=view_citation&citation_for_view=ZDbuOE4AAAAJ:hqOjcs7Dif8C Towards Network-wide QoE Fairness using OpenFlow-assisted Adaptive Video Streaming]</ref>DASH也与底层的应用层协议无关，因此可以配合任何协议中使用。例如，基于{{tsl|en|Content centric networking||CCN}}的DASH。<ref name="dashccn">[http://www-itec.uni-klu.ac.at/dash/?page_id=1097 Y. Liu, J. Geurts, J.-P. Point, S. Lederer, B. Rainer, C. Mueller, C. Timmerer and H. Hellwagner, "Dynamic Adaptive Streaming over CCN: A Caching and Overhead Analysis", In Proceedings of the IEEE International Conference on Communication (ICC) 2013 – Next-Generation Networking Symposium, Budapest, Hungary, June, 2013 ]</ref>

2015年7月27日，[[MPEG_LA|MPEG LA]]宣布呼吁与MPEG-DASH相关的专利，以便为该技术创建一个专利池。<ref>[http://www.mpegla.com/Lists/MPEG%20LA%20News%20List/Attachments/96/n-15-07-27.pdf MPEG LA Announces Call for Patents to Organize Joint License for MPEG-DASH] {{webarchive|url=https://web.archive.org/web/20150807012726/http://www.mpegla.com/Lists/MPEG%20LA%20News%20List/Attachments/96/n-15-07-27.pdf |date=2015-08-07 }}</ref>

== 实现 ==
通过ExoPlayer，MPEG-DASH在Android上可原生使用，如三星智能电视2012+、LG智能电视2012+、索尼电视2012+、飞利浦NetTV 4.1+、松下Viera 2013+和Chromecast。<ref name="device-compatibility">[http://www.bitcodin.com/blog/2015/03/mpeg-dash-device-compatibility Device Compatibility]</ref>YouTube以及Netflix已经支持MPEG-DASH，并且可使用多种MPEG-DASH播放器。<ref>[http://www.dash-player.com/blog/2015/02/the-status-of-mpeg-dash-today-and-why-youtube-and-netflix-use-it-in-html5/ The Status of MPEG-DASH today, and why Youtube & Netflix use it in HTML5]</ref>

虽然HTML5不直接支持MPEG-DASH，但是已有一些MPEG-DASH的JavaScript实现允许在网页浏览器中通过HTML5 [[Media_Source_Extensions|Media Source Extensions]]（MSE）使用MPEG-DASH。<ref name="mse">[https://dvcs.w3.org/hg/html-media/raw-file/tip/media-source/media-source.html HTML5 Media Source Extensions ]</ref>另有其他JavaScript实现，如bitdash播放器<ref>[http://www.dash-player.com/demo/drm-and-protection/ bitdash DRM Testarea] {{webarchive|url=https://web.archive.org/web/20150703200443/http://www.dash-player.com/demo/drm-and-protection/ |date=2015-07-03 }}</ref>支持使用HTML5[[加密媒体扩展|加密媒体扩展]]播放有[[数字版权管理|DRM]]的MPEG-DASH。<ref name="eme">[https://w3c.github.io/encrypted-media/ HTML5 Encrypted Media Extensions ]</ref>当WebGL结合使用，MPEG-DASH基于HTML5的自适应比特率流还可实现360°视频的实时和按需的高效流式传输。<ref name="360° Streaming in HTML5">[https://bitmovin.com/tutorials/vr-360-video-encoding-playout/ 360° Streaming in HTML5]</ref>

=== 客户端和程序库 ===

* Dash.js是Dash行业论坛官方参考和生产播放器。<ref>[https://github.com/Dash-Industry-Forum/dash.js A reference client implementation for the playback of MPEG DASH via Javascript and compliant browsers.]</ref>
* Shaka是出自Google的开源dash播放器。<ref>{{Cite news|url=http://news.softpedia.com/news/meet-shaka-player-google-s-html5-video-player-for-low-bandwidth-conditions-489937.shtml|title=Meet Shaka Player, Google's HTML5 Video Player for Low Bandwidth Conditions|last=Cimpanu|first=Catalin|date=2015-08-24|newspaper=Softpedia|accessdate=2016-08-13}}</ref>
* [[VLC多媒體播放器|VLC多媒體播放器]]3.0将为MP4/MPEG和实时流媒体发布一个新客户端插件。<ref name="itec-dash">[http://www-itec.uni-klu.ac.at/dash/ DASH at ITEC, VLC Plugin, DASHEncoder and Dataset] by C. Mueller, S. Lederer, C. Timmerer</ref><ref name="vlc-dash-paper">[http://www-itec.uni-klu.ac.at/bib/files/p723-muller.pdf C. Müller and C. Timmerer, "A VLC Media Player Plugin enabling Dynamic Adaptive Streaming over HTTP", In Proceedings of the ACM Multimedia 2011 , Scottsdale, Arizona, November 28, 2011.]</ref><ref>{{Cite web|url=http://git.videolan.org/?p=vlc.git;a=commitdiff;h=c13e7d4a399911f263876a0ec0611e1fb27e8b43|title=VLC 3.0 features}}</ref>
*跨平台FOSS多媒体框架[[GStreamer|GStreamer]]自从至少1.4版本以来支持MPEG-DASH和WebM DASH。<ref name="gstreamer">[https://coaxion.net/blog/2014/05/http-adaptive-streaming-with-gstreamer/ HTTP Adaptive streaming with GStreamer]</ref>
* 开源程序库libdash<ref name="libdash">[http://www.bitmovin.net/ libdash: Open-source DASH client library] by bitmovin Gmbh</ref>独立于平台，可在Android、iOS、Windows Phone等移动平台上运行。
* bitmovin为HTML5和Flash提供了bitdash MPEG-DASH播放器。<ref>[http://www.dash-player.com/feature-details/ bitdash MPEG-DASH Player Feature Details]</ref>
* [https://www.theoplayer.com/features/mpeg-dash THEOplayer]目前正在寻找伙伴来测试他们的MPEG-DASH视频播放器。<ref>{{Cite web|url=https://www.theoplayer.com|title=HLS HTML5 Video Player {{!}} THEOplayer|accessdate=2016-02-15|language=en-US}}</ref> 
* Viblast Player支持HTML5中的MPEG-DASH，并为iOS和Android提供SDK。<ref>https://www.theoplayer.com</ref>
* 巴黎电信学院中GPAC的OSMO4支持MPEG-DASH。<ref>[http://gpac.wp.mines-telecom.fr/player/ OSMO4 Player of GPAC]</ref>
* 克拉根福大学ITEC中的DASH-JS支持MPEG-DASH。<ref>[http://www-itec.uni-klu.ac.at/dash/?page_id=746 DASH-JS at ITEC of Klagenfurt University]</ref>
* Radiant Media Player支持HTML5中的MPEG-DASH（DASH264和WebM DASH）。<ref>[https://www.radiantmediaplayer.com/compatibility-table.html Radiant Media Player Compatibility Table]</ref>
* Videogular是AngularJS面向桌面和移动平台提供的一个视频应用框架，AngularJS为HTML5提供的视频播放器
* [https://github.com/google/ndash libndash]是一个开源（Apache许可证）的C++程序库，提供构建一个全功能MPEG-DASH媒体播放器所需的所有功能（不包括解码/渲染帧到显示器）。

=== 服务器 ===
请注意，除了Live Streaming外，DASH内容不需要服务器的特定支持。

* {{tsl|en|Brightcove}} {{tsl|en|Zencoder}}已支持MPEG-DASH transmuxing/transcoding。<ref>{{Cite web|url=https://app.zencoder.com/docs/guides/encoding-settings/dash|title=DASH Streaming and Playlists}}</ref>
* {{tsl|en|Elemental Technologies}}视频处理解决方案支持DASH。
* {{tsl|en|Helix Universal Server}}已支持各种模式下的DASH。
* nginx-rtmp-module支持生成MPEG-DASH实时流。<ref>[http://nginx-rtmp.blogspot.ru/2013/11/mpeg-dash-in-nginx-rtmp-module-108.html MPEG-DASH in nginx-rtmp-module 1.0.8]</ref>但在1.2.0版本以前，<ref>[http://nginx-rtmp.blogspot.ru/2017/07/mpeg-dash-improvements-in-nginx-rtmp.html MPEG-DASH improvements in nginx-rtmp-module 1.2.0]</ref>只能使用dash.js的修改版本<ref>[http://nginx-rtmp.blogspot.ru/2013/11/mpeg-dash-live-streaming-in-nginx-rtmp.html MPEG-DASH live streaming in nginx-rtmp-module]</ref>和bitdash播放。<ref name="bitdash">[http://www.dash-player.com bitdash MPEG-DASH player for HTML5 and Flash]</ref>
* nginx-ts-module支持实时MPEG-DASH<ref>[http://nginx-rtmp.blogspot.ru/2017/07/introducing-nginx-ts-module-for-hls-and.html Introducing nginx-ts-module for HLS and MPEG-DASH live streaming]</ref>
* {{tsl|en|Nimble Streamer}}有实时和点播MPEG-DASH的支持。对点播来说，它支持H.265和H.264编解码器<ref>[https://wmspanel.com/nimble/dash MPEG-DASH support in Nimble Streamer]</ref>
* {{tsl|en|Unified Streaming Platform|Unified Origin}}支持MPEG-DASH。<ref>[http://www.streamingmedia.com/PressRelease/Netview-and-Unified-Streaming-streaming-DASH_27097.aspx Netview and Unified Streaming streaming DASH]</ref><ref>[http://www.unified-streaming.com/products/factsheet/ USP Factsheet]</ref>
=== 服务 ===

* Amazon Web Services [https://aws.amazon.com/elastictranscoder/ Elastic Transcoder]已支持MPEG-DASH。<ref>{{Cite web|url=https://aws.amazon.com/about-aws/whats-new/2016/05/amazon-elastic-transcoder-now-supports-mpeg-dash/|title=Amazon Elastic Transcoder Now Supports MPEG-DASH|website=Amazon Web Services, Inc.|access-date=2016-06-03}}</ref>
* [[Level_3通信|Level 3通信]] CDN支持DASH。
* [[Akamai|Akamai]] [[內容傳遞網路|CDN]]支持DASH。<ref>[http://www.akamai.com/html/about/press/releases/2014/press-040814.html Akamai Announces Native MPEG-DASH and HDS Support for Live Video Workflows]</ref>
* {{tsl|en|Amazon CloudFront}} CDN支持DASH。
* [[Microsoft_Azure|Azure Media Services]]平台已支持MPEG-DASH。<ref>[http://msdn.microsoft.com/en-us/library/ie/dn551370(v=vs.85).aspx MPEG-DASH and streaming reference and resources]</ref>
* {{tsl|en|bitmovin}}提供的云转码服务bitcodin.com支持MPEG-DASH。<ref>[http://www.bitcodin.com/supported-formats/ bitcodin.com Supported Formats]</ref>
* {{tsl|en|Limelight Networks}} CDN支持DASH。
* {{tsl|en|Tata Communications}} CDN支持DASH。
* {{tsl|en|StreamRoot}}的混合CDN模型支持MPEG-DASH。
* ScaleEngine Video CDN支持DASH。

=== 内容生成器 ===
* ITEC的DASHEncoder。<ref name="dataset">[http://www-itec.uni-klu.ac.at/bib/files/p89-lederer.pdf S. Lederer, C. Mueller and C. Timmerer, "Dynamic Adaptive Streaming over HTTP Dataset", In Proceedings of the ACM Multimedia Systems Conference 2012, Chapel Hill, North Carolina, February 22-24, 2012.]</ref>
* MP4Box及其来自Telecom ParisTech的GPAC的多媒体框架<ref name="GPAC Telecom ParisTech">[http://gpac.wp.mines-telecom.fr/2011/02/02/mp4box-fragmentation-segmentation-splitting-and-interleaving/ GPAC Telecom ParisTech]</ref>
* 巴黎电讯的dashcast支持MPEG-DASH实时流<ref>[http://gpac.wp.mines-telecom.fr/dashcast/ dashcast of Telecom ParisTech]</ref>
* MediaGoom MPEG-DASH Packager<ref>{{cite web|url=http://mediagoom.com|title=MediaGoom. Essential Web Streaming.}}</ref>
* Bento4开源工具和SDK<ref>[https://www.bento4.com/developers/dash/ Bento4 MPEG DASH Documentation]</ref>

=== 其他 ===

* ITEC为MPEG-DASH媒体演示描述（MPD）文件提供验证服务
* Alpen-Adria克拉根福大学的信息技术研究所（ITEC）、巴黎电信学院GPAC小组和Digital TV Labs已提供多个DASH数据集。<ref name="MPEG DASH Dataset Overview">[http://www.dash-player.com/blog/2015/04/10-free-public-mpeg-dash-teststreams-and-datasets/ MPEG DASH Dataset Overview]</ref><ref name="distributeddataset">[http://www-itec.uni-klu.ac.at/dash/?page_id=958 S. Lederer, C. Mueller, C. Timmerer, C. Concolato, J. Le Feuvre and K. Fliegel, Distributed DASH Dataset, In Proceedings of the ACM Conference on Multimedia Systems (ACM MMSys) 2013, Oslo, Norway, 2013.]</ref><ref name="DASH Digital TV Labs">[http://digitaltv-labs.com/products/consumer_electronics/details/m-peg_dash MPEG DASH Test Suite]</ref>
* BBC有DASH测试流，包括基于HTTP/2的DASH。<ref>[http://www.bbc.co.uk/rd/blog/2013/09/mpeg-dash-test-streams MPEG DASH Test Streams]</ref>

== 参考资料 ==
{{Reflist|2}}

==外部链接==
* [http://standards.iso.org/ittf/PubliclyAvailableStandards/c065274_ISO_IEC_23009-1_2014.zip MPEG-DASH Standard]
* [http://lists.uni-klu.ac.at/mailman/listinfo/dash DASH subscription mailing list]
* [http://dash.itec.aau.at/ DASH research at Alpen-Adria Universität Klagenfurt]
* [https://web.archive.org/web/20130624105147/http://vicky.bitmovin.net/mailman/listinfo/libdash-dev Mailing list of the open-source DASH client library libdash]

[[Category:HTTP|Category:HTTP]]
[[Category:MPEG|Category:MPEG]]
[[Category:多媒体|Category:多媒体]]
[[Category:网络协议|Category:网络协议]]