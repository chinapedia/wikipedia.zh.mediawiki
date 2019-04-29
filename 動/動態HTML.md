{{Expand|time=2011-02-12}}
{{不是|动态网页}}
{{NoteTA|G1=IT}}
{{Template:HTML}}
'''動態HTML'''（'''Dynamic HTML'''，简称'''DHTML'''、'''DHML'''）指的是网页内容随着用户或计算机程序提供的参数而变化的HTML，通过结合[[HTML|HTML]]、用戶端脚本语言（Client Side Script，如[[JavaScript|JavaScript]]）、[[串接樣式表|串接樣式表]]（CSS）和[[文件物件模型|文件物件模型]]（DOM）来创建動態網頁內容。

== 应用 ==
动态HTML技术根据运行地点，分為客户端脚本（也称浏览器脚本）和服务器脚本。
# 客户端脚本<br />客户端脚本包括JavaScript技术。是指在某个页面中，通过鼠标点击或键盘操作，与网页产生交互动作；或者在特定时间激发某个事件。客户端脚本在用户的电脑系统里运行。常用于多媒体展示和远程脚本调用。
# 服务器脚本<br />服务器脚本包括ASP, ColdFusion, Perl, PHP, Ruby, WebDNA等技术，一般通过Common Gateway Interface (CGI)来产生动态页面。通过在HTML表单中填写数据，更改URL地址中的参数，更改浏览器的类型等，每次都可能产生不同的页面，称之为动态页面。

最常见的例子包括：
* 产生交互式表单
* 生成类似WebCT的e-learning交互式在线基础培训
* 创建基于浏览器的视频游戏

== 結構 ==
一個典型的使用 DHTML 如下:
<source lang="xml">
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
<html ns="http://www.w3.org/1999/xhtml">
  <head>
    <title>DHTML example</title>
    <script type="text/javascript"> 
      function init() {
      myObj = document.getElementById("navigation");
      // .... more code
      }
      window.onload=init;
    </script>
  </head>
  <body>
    <div id="navigation"></div>
    <pre>
      Often the code is stored in an external file; this is done by linking the file that contains the JavaScript. 
      This is helpful when several pages use the same script:
    </pre>
    <script type="text/javascript" src="myjavascript.js"></script>
  </body>
</html>
</source>

== 範例 ==
範例如下：<ref>[http://www.dynamicdrive.com/dynamicindex12/phong2.htm]</ref>
<!--
The following code illustrates an often-used function. An additional part of a web page will only be displayed if the user requests it. In [[e-learning|e-learning]], such a function might be used to display additional hints or an answer that the student initially should not see.-->
<source lang="xml">
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" 
      "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html ns="http://www.w3.org/1999/xhtml" xml:lang="en">
  <head>
    <title>Test</title>
    <style type="text/css">
      h2 {background-color: lightblue; width: 100%}
      a {font-size: larger; background-color: goldenrod} 
      a:hover {background-color: gold}
      #example1 {display: none; margin: 3%; padding: 4%; background-color: limegreen}
    </style>
    <script type="text/javascript">
      function changeDisplayState (id) {
        d=document.getElementById("showhide");
        e=document.getElementById(id);
        if (e.style.display == 'none' || e.style.display == "") {
          e.style.display = 'block';
          d.innerHTML = 'Hide example..............';
        } else {
          e.style.display = 'none';
          d.innerHTML = 'Show example';
        }
      }
    </script>
  </head>
  <body>
    <h2>How to use a DOM function</h2>
    <div><a id="showhide" href="javascript:changeDisplayState('example1')">Show example</a></div>
    <div id="example1">
      This is the example.
      (Additional information, which is only displayed on request)...
    </div>
    <div>The general text continues...</div>
  </body>
</html>
</source>

== 參考文獻 ==
{{Reflist}}

{{-}}
{{网页技术与标准}}
{{網頁設計}}

[[Category:HTML|Category:HTML]]