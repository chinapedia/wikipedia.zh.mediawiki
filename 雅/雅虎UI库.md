{{Infobox_Software
| name = Yahoo! UI Library（YUI）
| logo = [[File:Yuilib.jpg|File:Yuilib.jpg]]
| developer = [[Yahoo!|Yahoo!]]
| latest release version = 3.14.1
| latest release date = {{release date|2013|12|20}}
| genre = [[JavaScript函式庫|JavaScript函式庫]]
| programming language = [[JavaScript|JavaScript]]
| license = [[BSD許可證|BSD許可證]]
| website = [http://developer.yahoo.com/yui/ http://developer.yahoo.com/yui/]
}}
'''雅虎UI库'''（{{lang-en|Yahoo! UI Library}}，'''YUI'''）是一個開放原始碼的[[JavaScript|JavaScript]]函數庫，為了能建立一個高互動的網頁，它採用了[[AJAX|AJAX]]，[[DHTML|DHTML]]和[[文檔對象模型|DOM]]等程式碼技術<ref>{{cite web
 | url = http://www.eweek.com/article2/0,1759,1926831,00.asp
 | title = Yahoo, TIBCO, Oracle Join AJAX Craze
 | author = Darryl K. Taft  
 | publisher = [[eWeek|eWeek]]
 | date = 2006年2月14日
 | accessdate=2007-09-10
}}</ref>。它也包含了許多[[CSS|CSS]]資源。使用授權為[[BSD許可證|BSD許可證]]<ref name="developer_yahoo_yui">{{cite web
|url = http://developer.yahoo.com/yui/
|title= Yahoo! User Interface Library
|accessdate=2006-10-20}}
</ref>。
<br/>
於{{date|2014-08-29|iso}}，由於缺乏積極維護、過分龐大的library不合時代……等原因停止維護<ref>{{cite web
 | url = http://yahooeng.tumblr.com/post/96098168666/important-announcement-regarding-yui
 | title = Important Announcement Regarding YUI
 | author = jlecomte-yahoo
 | publisher =  
 | date = 2014-08-29
}}</ref>

== 功能 ==
YUI包含完整的說明文件。它包含了兩種元件：工具與控制項<ref name="developer_yahoo_yui"/>，和一些CSS資源。

=== 工具 ===
;動畫
:協助達成位置移動、大小改變、透明度和其他的網頁效果。

;瀏覽器歷史紀錄管理工具
:協助網頁程式使用瀏覽器之上一頁與書籤（我的最愛）工具。

;連線工具
:協助管理跨瀏覽器的[[XMLHttpRequest|XMLHttpRequest]]功能。他也整合了表單傳送、錯誤處理、[[callback_(computer_science)|callback]]和檔案上傳。

;資料源
:提供通用可配置介面給其他組件與種種資料，如從簡單的JavaScript陣列到線上伺服器，間透過XHR來互動。

;元素
:為DOM裡的HTMLElements提供包裝樣式，從而簡化一般工作如加入監聽者（listener）、對DOM操作、以及存取屬性。

;DOM
:為一般的[[DOM|DOM]]腳本作業提供幫助，它包括元素定位與CSS樣式管理。

;即拖即放
:為[[即拖即放|即拖即放]]的開發（建立與管理可在網頁上拖放的物件）提供幫助。

;事件
:提供開發者對瀏覽器[[事件驅動程式設計|事件]]，如滑鼠點擊與鍵盤按鍵，的簡易、安全之存取。它也提供自訂事件物件以應付用戶出版與訂閱自訂事件的需求。

=== 控制項 ===
;自動完成
:為用戶文字輸入的互動提供[[自動完成|自動完成]]功能（建議列表與隨打擊找的功能）。它支援廣泛的資料源格式。它也透過XMLHttpReqeust支援伺服器端資料源。

;按鈕
:讓用戶製作功能像傳統HTML表單按鈕般多樣、圖形化的按鈕。

;月曆
:圖形式、動態的控制，用於日期選擇。

;容器
:支援大量的DHTML視窗規範包括[[提示框|提示框]]（Tooltip）、面板、對話框、簡易對話框、模組與覆蓋層（Overlay）。

;資料表
:簡單且強大的應用程式介面用來顯示網頁上螢幕閱讀器可存取的表資料。值得關注的功能包括可排序的欄、分頁、捲軸、行選取、可放大縮小的欄、以及線上編輯。

;紀錄器
:提供一種快速簡單的方式來寫入[[日誌|日誌]]訊息到[[Mozilla_Firefox|Mozilla Firefox]]的Firebug擴充插件畫面終端、或者[[Safari|Safari]] JavaScript終端。

;表單
:提供簡易產生滑鼠移過彈出[[選單|選單]]的方式。

;滑塊：
:提供一般性滑塊組件讓用戶可在有限範圍內以單軸或者雙軸選擇值。

;分頁檢視
:提供以分頁方式來檢視內容。

;樹狀檢視
:產生目錄樹，其下節點可以縮放。

=== CSS資源 ===
* [https://web.archive.org/web/20070513072040/http://developer.yahoo.com/yui/grids/ CSS頁面網格]：七種基本線框外帶附加組件，支援超過1000種不同網頁佈局。
* [https://web.archive.org/web/20070513071702/http://developer.yahoo.com/yui/fonts/ 標準CSS字型集]：標準化跨瀏覽器字型家族與尺寸設定。
* [https://web.archive.org/web/20090703121002/http://developer.yahoo.com/yui/reset/ 標準CSS重設]：CSS宣告，用於移除頁邊空白並標準化跨瀏覽器對顯示一般元素的問題。

2007年8月，Yahoo放出YUI Compressor 1.0—一種JavaScript [[數據壓縮|壓縮器]]。<ref>{{cite web
 | url = http://www.ddj.com/web-development/201800137
 | title = YUI Compressor 1.0 Released
 | author = John Dorsey
 | publisher = [[Dr._Dobb's_Journal|Dr. Dobb's Journal]]
 | date = 2007年8月14日
 | accessdate=2007-09-10
}}</ref>

[https://web.archive.org/web/20080304222339/http://developer.yahoo.com/yui/theater/ YUI劇院（YUI Theater）]對全世界提供存取許多JavaScript與網頁開發知名的講師的技術會談。<ref>{{cite web
 | url = http://eclipse.sys-con.com/read/405912.htm
 | title = AJAX Lowers Yahoo! Page Views, Eric Miraglia Explains Why That's Good
 | publisher = Eclipse Developers Journal
 | date = 2007年9月7日
 | accessdate=2007-09-10
}}</ref>



== 參考資料 ==
{{reflist}}

== 外部連結 ==
* [http://developer.yahoo.com/yui/ 官方网站]{{en icon}}
* [http://www.yui-ext.com/ yui-ext - Jack Slocum's Yahoo! UI Extensions Library] {{en icon}}
* [http://yuiblog.com/ Yahoo! User Interface Blog] {{en icon}}
* [http://groups.yahoo.com/group/ydn-javascript ydn-javascript Yahoo! group] {{en icon}}
* [http://sourceforge.net/projects/yui SourceForge project page] {{en icon}}
* [https://web.archive.org/web/20080229011119/http://developer.yahoo.com/ypatterns/ Yahoo! Design Patterns Library] {{en icon}}

[[Category:雅虎|UI Library]]
[[Category:AJAX|Category:AJAX]]
[[Category:JavaScript函式庫|Category:JavaScript函式庫]]
[[Category:CSS框架|Category:CSS框架]]