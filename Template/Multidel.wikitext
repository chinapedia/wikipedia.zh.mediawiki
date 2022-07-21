{{tmbox
| small      = {{{small|}}}
| image      = [[Image:Clipboard.svg|35px|页面存废讨论]]
| smallimage = none
| text       = 此{{{type|頁}}}曾經多次評審其[[Wikipedia:删除守则|存廢]]。若要重新提案評議其存廢，請先參考以下紀錄：{{#ifeq:{{{collapse}}}|yes|
<table style="width:100%; background: transparent;" class="collapsible collapsed">
<tr><th>刪除討論：</th></tr>
<tr><td>
}}
{{{list|}}}{{#if:{{{oldlist|}}}|
<table cellspacing=0 cellpadding=0 class="collapsible collapsed" style="width:100%; background: transparent; padding:0; margin:0;">
<tr><th>更早的刪除討論：</th></tr>
<tr><td>
{{{oldlist}}}</td></tr></table>
}}{{#ifeq:{{{collapse}}}|yes|</td></tr></table>}}<!---- 
偷懶不用|list= 時可用
第一筆討論紀錄開始 
---->{{#if:{{{date1|}}}|
* {{#iferror: {{#expr: {{#time:Ymd|{{{date1|無}}}}} }} | {{{date1}}} | {{#time:Y年n月j日|{{{date1|}}} }} }}，{{#iferror: {{#expr: {{#time:Ymd|{{{date1|無}}}}} }}
|
 '''[[Wikipedia:删除投票和请求/{{{date1}}}#{{{page1|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
|
 {{#ifexpr:{{#time:Ymd|{{{date1|}}} }} < 20080812
  |'''[[Wikipedia:删除投票和请求/{{#time:Y年n月j日|{{{date1}}} }}#{{{page2|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
  |'''[[Wikipedia:{{#ifeq:{{NAMESPACE}}|{{ns:7}}|檔案|頁面}}存廢討論/記錄/{{#time:Y/m/d|{{{date1|}}} }}#{{{page1|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
 }}
}}為{{#switch:{{LC:{{{result1|}}}}}
|kept|k|保留='''保留'''
|nc|無共識|无共识='''無共識'''，本页面暫時'''保留'''
|m|moved|move|移動|移动='''移動'''到{{#if:{{{target1|}}}|[[{{{target1}}}]]|其他位置}}
|r|重定向='''重定向'''{{#if:{{{target1|}}}|至[[{{{target1}}}]]}}
|sk|快速保留|速留='''快速保留'''
|rep|重複提出，無效|重复提出，请求无效={{{Type|{{{type|請求}}}}}}重複提出，'''無效'''
|ir|無效|无效={{{Type|{{{type|請求}}}}}}'''無效'''
|rr='''請求理由已消失'''，页面'''保留'''
|merge|merged|併入|合併='''併入'''{{#if:{{{target1|}}}|[[{{{target1}}}]]|其他位置}}
|deleted|d|刪除='''刪除'''
|tk|暫時保留|暂时保留='''暫時保留'''
|#default={{{result1|'''保留'''}}}
}}。
}}<!---- 第二筆討論紀錄開始 ---->
{{#if:{{{date2|}}}|
* {{#iferror: {{#expr: {{#time:Ymd|{{{date2|無}}}}} }} | {{{date2}}} | {{#time:Y年n月j日|{{{date2|}}} }} }}，{{#iferror: {{#expr: {{#time:Ymd|{{{date2|無}}}}} }}
|
 '''[[Wikipedia:删除投票和请求/{{{date2}}}#{{{page2|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
|
 {{#ifexpr:{{#time:Ymd|{{{date2|}}} }} < 20080812
  |'''[[Wikipedia:删除投票和请求/{{#time:Y年n月j日|{{{date2}}} }}#{{{page2|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
  |'''[[Wikipedia:{{#ifeq:{{NAMESPACE}}|{{ns:7}}|檔案|頁面}}存廢討論/記錄/{{#time:Y/m/d|{{{date2|}}} }}#{{{page2|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
 }}
}}為{{#switch:{{LC:{{{result2|}}}}}
|kept|k|保留='''保留'''
|nc|無共識|无共识='''無共識'''，本页面暫時'''保留'''
|m|moved|move|移動|移动='''移動'''到{{#if:{{{target2|}}}|[[{{{target2}}}]]|其他位置}}
|r|重定向='''重定向'''{{#if:{{{target2|}}}|至[[{{{target2}}}]]}}
|sk|快速保留|速留='''快速保留'''
|ir|無效|无效={{{Type|{{{type|請求}}}}}}'''無效'''
|rr='''請求理由已消失'''，页面'''保留'''
|merge|merged|併入|合併='''併入'''{{#if:{{{target2|}}}|[[{{{target2}}}]]|其他位置}}
|deleted|d|刪除='''刪除'''
|tk|暫時保留|暂时保留='''暫時保留'''
|#default={{{result2|'''保留'''}}}
}}。
}}
<!---- 第三筆討論紀錄開始 ---->
{{#if:{{{date3|}}}|
* {{#iferror: {{#expr: {{#time:Ymd|{{{date3|無}}}}} }} | {{{date3}}} | {{#time:Y年n月j日|{{{date3|}}} }} }}，{{#iferror: {{#expr: {{#time:Ymd|{{{date3|無}}}}} }}
|
 '''[[Wikipedia:删除投票和请求/{{{date3}}}#{{{page3|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
|
 {{#ifexpr:{{#time:Ymd|{{{date3|}}} }} < 20080812
  |'''[[Wikipedia:删除投票和请求/{{#time:Y年n月j日|{{{date3}}} }}#{{{page3|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
  |'''[[Wikipedia:{{#ifeq:{{NAMESPACE}}|{{ns:7}}|檔案|頁面}}存廢討論/記錄/{{#time:Y/m/d|{{{date3|}}} }}#{{{page3|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
 }}
}}為{{#switch:{{LC:{{{result3|}}}}}
|kept|k|保留='''保留'''
|nc|無共識|无共识='''無共識'''，本页面暫時'''保留'''
|m|moved|move|移動|移动='''移動'''到{{#if:{{{target3|}}}|[[{{{target3}}}]]|其他位置}}
|r|重定向='''重定向'''{{#if:{{{target3|}}}|至[[{{{target3}}}]]}}
|sk|快速保留|速留='''快速保留'''
|ir|無效|无效={{{Type|{{{type|請求}}}}}}'''無效'''
|rr='''請求理由已消失'''，页面'''保留'''
|merge|merged|併入|合併='''併入'''{{#if:{{{target3|}}}|[[{{{target3}}}]]|其他位置}}
|deleted|d|刪除='''刪除'''
|tk|暫時保留|暂时保留='''暫時保留'''
|#default={{{result3|'''保留'''}}}
}}。
}}
<!---- 第四筆討論紀錄開始 ---->
{{#if:{{{date4|}}}|
* {{#iferror: {{#expr: {{#time:Ymd|{{{date4|無}}}}} }} | {{{date4}}} | {{#time:Y年n月j日|{{{date4|}}} }} }}，{{#iferror: {{#expr: {{#time:Ymd|{{{date4|無}}}}} }}
|
 '''[[Wikipedia:删除投票和请求/{{{date4}}}#{{{page4|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
|
 {{#ifexpr:{{#time:Ymd|{{{date4|}}} }} < 20080812
  |'''[[Wikipedia:删除投票和请求/{{#time:Y年n月j日|{{{date4}}} }}#{{{page4|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
  |'''[[Wikipedia:{{#ifeq:{{NAMESPACE}}|{{ns:7}}|檔案|頁面}}存廢討論/記錄/{{#time:Y/m/d|{{{date4|}}} }}#{{{page4|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
 }}
}}為{{#switch:{{LC:{{{result4|}}}}}
|kept|k|保留='''保留'''
|nc|無共識|无共识='''無共識'''，本页面暫時'''保留'''
|m|moved|move|移動|移动='''移動'''到{{#if:{{{target4|}}}|[[{{{target4}}}]]|其他位置}}
|r|重定向='''重定向'''{{#if:{{{target4|}}}|至[[{{{target4}}}]]}}
|sk|快速保留|速留='''快速保留'''
|ir|無效|无效={{{Type|{{{type|請求}}}}}}'''無效'''
|rr='''請求理由已消失'''，页面'''保留'''
|merge|merged|併入|合併='''併入'''{{#if:{{{target4|}}}|[[{{{target4}}}]]|其他位置}}
|deleted|d|刪除='''刪除'''
|tk|暫時保留|暂时保留='''暫時保留'''
|#default={{{result4|'''保留'''}}}
}}。
}}
<!---- 第五筆討論紀錄開始 ---->
{{#if:{{{date5|}}}|
* {{#iferror: {{#expr: {{#time:Ymd|{{{date5|無}}}}} }} | {{{date5}}} | {{#time:Y年n月j日|{{{date5|}}} }} }}，{{#iferror: {{#expr: {{#time:Ymd|{{{date5|無}}}}} }}
|
 '''[[Wikipedia:删除投票和请求/{{{date5}}}#{{{page5|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
|
 {{#ifexpr:{{#time:Ymd|{{{date5|}}} }} < 20080812
  |'''[[Wikipedia:删除投票和请求/{{#time:Y年n月j日|{{{date5}}} }}#{{{page5|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
  |'''[[Wikipedia:{{#ifeq:{{NAMESPACE}}|{{ns:7}}|檔案|頁面}}存廢討論/記錄/{{#time:Y/m/d|{{{date5|}}} }}#{{{page5|{{SUBJECTPAGENAME}}}}}|讨论结果]]'''
 }}
}}為{{#switch:{{LC:{{{result5|}}}}}
|kept|k|保留='''保留'''
|nc|無共識|无共识='''無共識'''，本页面暫時'''保留'''
|m|moved|move|移動|移动='''移動'''到{{#if:{{{target5|}}}|[[{{{target5}}}]]|其他位置}}
|r|重定向='''重定向'''{{#if:{{{target5|}}}|至[[{{{target5}}}]]}}
|sk|快速保留|速留='''快速保留'''
|ir|無效|无效={{{Type|{{{type|請求}}}}}}'''無效'''
|rr='''請求理由已消失'''，页面'''保留'''
|merge|merged|併入|合併='''併入'''{{#if:{{{target5|}}}|[[{{{target5}}}]]|其他位置}}
|deleted|d|刪除='''刪除'''
|tk|暫時保留|暂时保留='''暫時保留'''
|#default={{{result5|'''保留'''}}}
}}。
}}
}}<noinclude>{{documentation}}<!-- Add categories and interwikis to the /doc subpage, not here! -->