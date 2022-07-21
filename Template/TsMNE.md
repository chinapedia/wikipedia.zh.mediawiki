<includeonly>{{tsMultiple
| select={{{1}}}
| type={{{2}}}
| varselect={{{3}}}
| link=蒙特內哥羅
| cndefault=黑山
| hkdefault=黑山
| twdefault=蒙特內哥羅
| opt1=5
| cn1=黑山共和国
| hk1=黑山共和國
| tw1=蒙特內哥羅
| opt2=2
| cn2=黑山
| hk2=黑山
| tw2=蒙國
| opt3=1
| cn3=黑
| hk3=黑
| tw3=蒙
}}</includeonly><noinclude>此模板有三個參數供編者設置：

第一個參數：
*（不設），如<nowiki>{{tsMNE}}</nowiki>：大陸、港澳顯示'''{{tsMNE|||cn}}'''，臺灣顯示'''{{tsMNE|||tw}}'''。測試：{{tsMNE}}
* '''5'''，如<nowiki>{{tsMNE|5}}</nowiki>：大陸顯示'''{{tsMNE|5||cn}}'''，港澳顯示'''{{tsMNE|5||hk}}'''，臺灣顯示'''{{tsMNE|5||tw}}'''。測試：{{tsMNE|5}}
* '''2'''，如<nowiki>{{tsMNE|2}}</nowiki>：大陸、港澳顯示'''{{tsMNE|2||cn}}'''，臺灣顯示'''{{tsMNE|2||tw}}'''。測試：{{tsMNE|2}}
* '''1'''，如<nowiki>{{tsMNE|1}}</nowiki>：大陸、港澳顯示'''{{tsMNE|1||cn}}'''，臺灣顯示'''{{tsMNE|1||tw}}'''。測試：{{tsMNE|1}}

第二個參數：
*（不設）：無特殊功能
* '''T'''，如<nowiki>{{tsMNE||T}}</nowiki>：轉換文章標題。這時此模板所在的位置不再顯示任何文字
* '''A'''，如<nowiki>{{tsMNE||A}}</nowiki>：通篇轉換，設置之後，條目內其他出現同樣詞語的地方，都會自動轉成用戶需要的字體
* '''L'''，如<nowiki>{{tsMNE||L}}</nowiki>：增加連接。測試：{{tsMNE||L}}
* '''AL'''，如<nowiki>{{tsMNE||AL}}</nowiki>：以上 A 跟 L 的結合 

第三個參數：
*（不設）：按照用戶設置顯示字體
*  '''cn'''，如<nowiki>{{tsMNE|||cn}}</nowiki>：強制顯示大陸字體
*  '''hk'''，如<nowiki>{{tsMNE|||hk}}</nowiki>：強制顯示港澳字體
*  '''tw'''，如<nowiki>{{tsMNE|||tw}}</nowiki>：強制顯示臺灣字體

注意：
* 第三個參數假如有設置的話，第二個參數的A（通篇轉換）就會失效，第二個參數的AL就會失去A（通篇轉換）的功能，只剩下L（增加連接）。

[[Category:嵌入式繁簡轉換模板|M]]</noinclude>