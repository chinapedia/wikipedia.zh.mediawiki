{{noteTA
|G1=IT
|G2=地名
|1=zh-cn:面容ID; zh-hans:Face ID; zh-hant:Face ID;
|2=-zh-hans:面部; zh-hant:面部; zh-tw:臉部;
|3=-zh-hans:面容; zh-hant:臉部; zh-tw:臉部;
|T=zh-cn:面容ID; zh-hans:Face ID; zh-hant:Face ID;
|G1=IT}}


'''面容ID'''（{{lang-en|'''Face ID'''}}）是[[蘋果公司|蘋果公司]]设计和发布的一个{{le|臉部识别系统|Facial recognition system}}，在[[iPhone_X|iPhone X]]中首次出现。此功能于2017年9月12日首次公布<ref>{{Cite news|url=https://live.theverge.com/apple-live-blog-2017-iphone-8-event/|title=Apple iPhone 8 event live blog|accessdate=2017-09-12}}</ref><ref>{{Cite web|url=http://nymag.com/selectall/2017/09/replacing-touch-id-with-face-id-is-worse-than-you-think.html|title=Replacing Touch ID With Face ID Is a Worse Idea Than You Think|accessdate=13 September 2017|last=Feldman|first=Brian}}</ref>，旨在取代[[Touch_ID|Touch ID]]而非新增一种安全机制。它允许使用者解锁苹果裝置，在各个苹果-{zh-cn:数字;zh-tw:數位;}-媒体商店（[[iTunes|iTunes]]商店、[[App_Store_(iOS)|应用商店]]以及[[iBooks|iBooks]]商店）中购买，以及作为 [[Apple_Pay|Apple Pay]] 或應用程式内支付的[[身份验证|身份验证]]方式。

苹果公司称，非本人解锁手机的概率是百万分之一<ref>{{cite web|last1=Tepper|first1=Fitz|title=Face ID is replacing Touch ID on the new iPhone X|url=https://techcrunch.com/2017/09/12/face-id-is-replacing-touch-id-on-the-new-iphone-x/|website=TechCrunch|accessdate=13 September 2017|language=en}}</ref><ref>{{cite web|last1=Coldewey|first1=Devin|title=iPhone X basically has a Kinect on the front to enable FaceID|url=https://techcrunch.com/2017/09/12/iphone-x-basically-has-a-kinect-on-the-front-to-enable-faceid/|website=TechCrunch|accessdate=13 September 2017|language=en}}</ref>。苹果公司也表示，面容识别資訊本機存储于[[Apple_A11_Bionic|Apple A11 Bionic]]及次代芯片的安全区域，不会在[[雲端運算|云端]]存储。<!-- source = keynote -->

== 原理 ==
面容ID会先用泛光感应组件照亮用户的脸部获取2D红外照片，然后再用红外摄像头识别，接下来再用点阵投影器向物体的表面投出三万多个特定编码的红外点，再通过反射回到红外摄像头接收器，利用红外照片和反射回去的红外点间的偏移，就可以物体获得脸部表面的景深信息，从而构建一个3D精确模型，然后就会将红外图像和3D精准模型发送到处理器中，并转化成一道数学表达式，比对之前已注册的面部数据后，就会得出结论。
其中的“注视解锁”的功能是通过红外摄像头捕捉眼球的画面并识别瞳孔特征来实现的，技术提供方是：[[Sensomotoric_instruments|SensoMotoric Instruments]]、提供机构光技术的PrimeSense公司和提供面部捕捉技术的FaceShift公司。<ref>{{Cite news|url=http://www.cnetnews.com.cn/2017/0913/3098102.shtml|title=我们认真研究了FaceID的工作原理，用iPhoneX的可以安心睡觉了|accessdate=2018-08-05}}</ref>

== 特征 ==

=== 泛光照明器 ===
使用不可见的[[红外线|红外线]]光照帮助识别臉部，[[光线|光线]]昏暗下依然可用，能使红外摄像机判定眼睛是否直视螢幕，以确保只有使用者才可以解除锁定，并利用人工智能来学习记住长相的持续变化。

=== 点阵投影器 ===
将超3万个[[肉眼|肉眼]]不可见的定位点射到[[面部|面部]]，构建唯一的面容立体特征，此外发射器上每个光点的排列組合也是独一无二的。

=== 红外摄像机 ===
红外摄像机用于拍摄平面红外图像之外，同时读取立体[[点阵|点阵]]图形。把上面兩者做神经网路分析的資訊数据化后，数据将发送到A11 Bionic芯片中的安全区域来确认匹配性。

== 争论 ==
面容ID可能慢于[[Touch_ID|Touch ID]]<ref>{{Cite web|url=https://arstechnica.com/gadgets/2017/09/face-id-on-the-iphone-x-is-probably-going-to-suck/|title=I’m worried that FaceID is going to suck—and here’s why|accessdate=13 September 2017}}</ref>，存在种族偏见（更适合[[白人|白人]]與亞洲人，系統不利於辨識黑種人）<ref>{{Cite web|url=https://www.theverge.com/2017/9/12/16298156/apple-iphone-x-face-id-security-privacy-police-unlock|title=The five biggest questions about Apple’s new facial recognition system|accessdate=13 September 2017}}</ref>，以及容易被[[警方|警方]]破解<ref>{{Cite web|url=http://www.slate.com/blogs/future_tense/2017/09/12/the_iphone_x_s_face_id_is_a_major_privacy_concern.html|title=You'll Love Unlocking Your iPhone X With Your Face. So Will Police Trying to Access It.|accessdate=13 September 2017|date=12 September 2017|last=Glaser|first=April}}</ref>，或者有可能被[[雙胞胎|雙胞胎]]骗过<ref>{{Cite web|url=http://time.com/4938362/iphone-x-evil-twin-memes/|title=The Internet Had Jokes About Apple's New Face ID for iPhone|accessdate=13 September 2017|last=Lang|first=Cady}}</ref>。13歲以下的[[兒童|兒童]]出现錯誤匹配的機率不同，因为他們的獨特面部特徵可能尚未完全發育<ref>{{Cite news|url=https://9to5mac.com/2017/09/27/face-id-iphone-x-white-paper/|title=Apple explains how iPhone X facial recognition with Face ID works (and fails) in security paper|date=2017-09-27|work=9to5Mac|access-date=2017-10-02|language=en-US}}</ref>；苹果公司面向开发者的开发审核指南也要求，13岁以下用户使用面部ID功能时需同时提供额外的授权验证方式。11月14日，有人上載影片《10歲兒子的面容 解開母親的iPhone X》。雖然母親事前告訴兒子不要看，但兒子不理會她並成功解開了<ref>{{cite web |first=Dani |last=Deahl |title=This 10-year-old was able to unlock his mom’s iPhone using Face ID |url=https://www.theverge.com/2017/11/14/16650394/10-year-old-unlock-mom-iphone-face-id |website=[[The_Verge|The Verge]] |date=November 14, 2017 |accessdate=December 13, 2017}}</ref><ref>{{cite web|url=https://www.youtube.com/watch?v=dUMH6DVYskc|title=Ten-Year-Old's Face Unlocks Face ID on His Mom's iPhone X|first=|last=AtMaliks|date=2017-11-14|publisher=|via=YouTube}}</ref>，也因此部分臉部支付服務，若為兒童設計的程式的可能無法使用<ref>{{cite web|url=http://tc.people.com.cn/n1/2017/0918/c183008-29541133.html|title="熊孩子"不能直接用面容ID 苹果这招是?|website=人民网}}</ref>。[[越南|越南]]公司Bkav聲稱於11月9日成功以面具破解，面具的成本大約150美元<ref>{{cite web |title=Bkav’s new mask beats Face ID in "twin way": Severity level raised, do not use Face ID in business transactions |url=http://www.bkav.com/d/top-news/-/view_content/content/103968/face-id-beaten-by-mask-not-an-effective-security-measure |website=Bkav Corporation |accessdate=2019-04-11 |date=2017-11-27}}</ref>。被問到能否製造新面具，Bkav拒絕並解釋：測試影片的面具需要大約9小時製造<ref>{{cite web|url=https://www.bbc.com/news/av/technology-41992610/face-id-iphone-x-hack-demoed-live-with-mask-by-bkav|title=Face ID iPhone X 'hack' demoed live|website=BBC News}}</ref>。Bkav的出發點為{{link-en|概念驗證|Proof of Concept}}，他們並認為安全性仍然極高。

== 参见 ==
* [[Touch_ID|Touch ID]]
* {{le|结构光3D扫描器|Structured-light 3D scanner}}

== 参考资料 ==
{{Reflist|30em}}
==外部链接==
* [https://www.apple.com/iphone-x/#face-id 官方介绍]{{en}}
* [https://support.apple.com/zh-hk/HT208109 在 iPhone X 上使用 Face ID] {{zh}}
* [https://www.apple.com/cn/newsroom/2017/09/the-future-is-here-iphone-x/ 遇见未来：iPhone X]{{zh-cn}}

{{Apple}}

[[Category:認證方法|Category:認證方法]]
[[Category:IOS|Category:IOS]]