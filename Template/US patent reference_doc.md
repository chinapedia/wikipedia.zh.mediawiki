<includeonly><!-- 在這裡加入模板的保護標識 --></includeonly><noinclude>{{template doc page viewed directly}}</noinclude>
<!-- 在本行下編輯模板說明 -->
这模板是用于在“参考文献”里加入一个美国注册专利的细节，如：发明家，标题和在美国专利局数据库的全文链接。

== 用法 ==
<pre style="width:250px">
{{US patent reference
 | number = 
 | y = 
 | m = 
 | d = 
 | inventor = 
 | title = 
}}</pre>
{| class=wikitable
!参数
!说明
|-
|number ||专利号码，省掉前头“US”字母，但如果前头是“D”需要打进去。
|-
|y ||注册年份，必须'''四位数'''。年份为阳历。例如：“1981”
|-
|m ||注册月份，必须'''两位数'''。例如：“02”
|-
|d ||注册日，必须'''两位数'''。例如：“01”
|-
|inventor||发明家名字，必须要填。可以加上维基链接。例如：“[[托马斯·爱迪生]]”
|-
|title ||专利的标题（根据资料库），必须要填。
|}

== 范例 ==
<pre>
{{US patent reference
 | number = 5285709
 | y = 1994
 | m = 02
 | d = 15
 | inventor = 约翰·D·格兰特
 | title = 微调弦乐器的机头，特别是吉他或类似的弦乐器
}}
</pre>

<blockquote>
{{US patent reference
 | number = 5285709
 | y = 1994
 | m = 02
 | d = 15
 | inventor = 约翰·D·格兰特
 | title = 微调弦乐器的机头，特别是吉他或类似的弦乐器
}}
</blockquote>

最好是能够在“参考文献”列入本模板后，给予较非正式的解释，方便读者了解这个专利。

== 參見 ==
请注意以下可能较适合的模板（如，文字内崁列入）
* {{tl|Citation/patent}}
* {{tl|Cite patent}}，用于创建 [http://ep.espacenet.com/ esp@cenet] 数据库里的美国或其它专利链接。
* {{tl|Citeref patent}}, for an inline citations to a patent bibliography
* {{tl|EPO Application}}, to include a link to the European Patent Application entry of a European patent application
* {{tl|EPO Register}}, to include a link to the European Patent Register entry of a European patent or patent application
* {{tl|Googpat}}, 
* {{tl|Patent}}, a generic template for general use referring to world's patent offices
* {{tl|Ref patent}}, similar to {{tl|US patent reference}}, but using espacenet with more details than {{tl|Cite patent}}
* {{tl|US patent}}，用于创建[[美国专利及商标局]]数据库里的美国注册专利链接。
* {{tl|US patent application}}，用于在“参考文献”里列入一个美国注册专利申请的细节。
* {{tl|US patent reference}}，用于在“参考文献”里列入一个美国注册专利的细节。
* {{tl|USPTO Application}}
* {{tl|USPTO Patent}}

<includeonly>
<!-- 本行下加入模板的分類 -->
[[Category:外部资源模板|{{PAGENAME}}]]

<!-- 本行下加入模板的跨語言鏈接 -->
[[en:Template:US patent reference]]
[[ja:Template:US patent reference]]
[[ms:Templat:Rujukan paten AS]]
</includeonly>