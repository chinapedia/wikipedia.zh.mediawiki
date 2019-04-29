{{article issues
|expand=2011-08-02T08:06:11+00:00
|expert=2011-08-02T08:06:11+00:00
}}
{{NoteTA |G1 = IT}}

'''非侵入式JavaScript'''<ref>{{cite book |title=ASP.NET MVC 3高级编程 |publisher=清华大学出版社 |url = http://book.51cto.com/art/201207/345733.htm |date=2012-06 |ISBN=978-7-302-28675-2 }}</ref>是一種將[[Javascript|Javascript]]從[[HTML|HTML]]結構抽離的設計概念，避免在HTML標籤中夾雜一堆onchange、onclick等屬性去掛載Javascript事件，讓HTML與Javascript分離，依[[MVC|模型-视图-控制器]]的原則將功能權責清楚區分，使HTML也變得結構化容易閱讀。這個名称并不是正式定义，它的基本原则包括：
* 將网页的[[置标语言|行为层]]和[[样式表|表现层]][[关注点分离|分离]]开<ref>{{cite web
|last=Keith
|first=Jeremy
|title=Behavioral Separation
|date=2006-06-20
|url=http://www.alistapart.com/articles/behavioralseparation
}}</ref>；
* 是解决传统JavaScript编程问题（浏览器呈现不一致，缺乏扩展性）的最佳实践；
* 为可能不支持JavaScript高级特性的[[用户代理|用户代理]]（通常是浏览器）提供[[渐进增强|渐进增强]]的支持<ref>{{cite web
|last=Olsson
|first=Tommy
|title=Graceful Degradation & Progressive Enhancement
|date=2007-02-06
|url=http://accessites.org/site/2007/02/graceful-degradation-progressive-enhancement/
}}</ref>。

==新範式==
==行為與文件標籤的分離==
傳統上，JavaScript腳本通常與HTML文件的標籤放在一起。例如，以下是在HTML中註冊JavaScript事件處理程序的典型方法：
<source lang="xml">
<input type="text" name="date" onchange="validateDate()"/>
</source>

HTML標籤的目的通常是描述文件的排版結構，而不是網頁操作的程序行為。兩者的結合或許會對網站的可維護性產生負面影響，例如將[[呈现与内容分离|呈現和內容]]相結合。在HTML中建立和引用的JavaScript腳本行為，例如在單一元素上設置多個不同事件的處理程序，或在多個元素上設置相同的事件處理程序，或者在使用事件委派時，結果可能難以使用和維護。

非侵入式方案是以編程方式註冊需要的事件處理程序，而不是和網頁元素內嵌在一起。不同於前述那樣添加一個<code>onchange</code>屬性，相關的元素改用簡單的標識，例如以<code>class</code>，<code>id</code>屬性和它們值當成腳本參考的標識，或標記中一些其它的方式：
<source lang="xml"><input type="text" name="date" id="date" /></source>

當頁面首次加載到瀏覽器中時，執行的腳本可以尋找每個相關元素，並相對應地進行設置：
<source lang="xml">
    window.addEventListener("DOMContentLoaded"，function（event）{
         document.getElementById('date').addEventListener("change"，validateDate);
    });
</source>

==命名空間==
非侵入式JavaScript應儘量減少將物件添加到運行環境，或全局的[[命名空间|名前空間]]中。其它腳本有可能覆蓋掉全局名前空間中，所建立的任何變量或函數；而這將導致發生不預期的結果時，卻難以除錯的困擾。JavaScript並沒有內建明確的名前空間機制，但利用語言設計很容易可產生需求的效果。Flanagan建議以Java編程的開發風格，將開發人員自己的域名反轉，作為全球獨一的名前空間發佈。

<source lang="javascript">
var org;
if (!org) {
    org = {};
} else if (typeof org != 'object') {
    throw new Error("org already exists and is not an object.");
}
if (!org.example) {
    org.example = {};
} else if (typeof org.example != 'object') {
    throw new Error("org.example already exists and is not an object.");
}
</source>


雖然如上面的名前空間物件中，可定義各種變量，函數和物件，但是通常建議在名前空間內，使用[[闭包_(计算机科学)|閉包]]進一步隔離，作為私有的變量和函數來使用，以共用[[介面_(程式設計)|介面]]回傳每個函數作用的結果。上列代碼可依照以下內容，改寫為非侵入式：
<source lang="javascript">
org.example.Highlight = function() {
    // Define private data and functions
    var highlightId = 'x';
    function setHighlight(color) { 
        document.getElementById(highlightId).style.color = color;
    }
    
    // Return public pointers to functions or properties
    // that are to be public.
    return {
        goGreen: function() { setHighlight('green'); },
        goBlue:  function() { setHighlight('blue'); }
    }
}(); // End closure definition and invoke it.
</source>

從任何其它的模組，可以呼叫這些共用介面的方法，如下列：
<source lang="javascript">
org.example.Highlight.goBlue();

var h = org.example.Highlight;
h.goGreen();
</source>

以這種方式，每個模組－開發人員的代碼都包含在私有或唯一的名前空間中，並不會干擾或侵入任何其它代碼。

==正常退化==
== 最佳實務 ==
非侵入式Javascript的本質是增加了分離的行為層概念，而且這範式的提倡者認同一些相關的原則，如下列：
* [[動態HTML|DOM腳本]]，即遵循W3C DOM和事件模型，並避免使用某一瀏覽器特定的擴充功能。
* [[渐进增强|功能檢測]]，即在使用特定功能之前先檢查是否支援；對比相反於過去只檢測用戶端使用的瀏覽器(版本)。
* 更一般來說，JavaScript最佳實務通常與其它編程語言（例如[[封裝_(物件導向程式設計)|封裝]]和[[抽象層|抽象層]]，避免[[全局变量|全局变量]]，有意義的命名法約定，使用適當的[[设计模式|设计模式]]式和[[软件测试|系統測試]]）平行。這些原則對大規模軟體工程開發非常重要，但過去的JavaScript設計過程中並不受重視。這些原則的採行，使JavaScript被認為是從“玩具”的腳本語言，轉變為正規編程發展工具的重要組成。

== 参考文献 ==
{{Reflist}}

== 外部連結 ==
* [http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html Unobtrusive Client Validation in ASP.NET MVC 3]

== 参见 ==
{{Portal box|互联网|计算机程序设计}}
* [[渐进增强|渐进增强]]

{{-}}
{{JavaScript}}

[[Category:JavaScript|Category:JavaScript]]
[[Category:响应式网页设计|Category:响应式网页设计]]