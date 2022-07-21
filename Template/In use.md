{{mbox
| type  = notice
| image = [[File:Ambox clock.svg|50px]]
| text = '''本{{NS1}}{{#if:{{{m|}}}|{{{m}}}正在進行重大修改|正在進行重大修改}}，持續時間「{{{1|2小時}}}」，請不要在此期間進行編輯。'''<br><span style="font-size: smaller;">當重大編輯結束或暫時停止編輯時，請移除本模板。您可於{{Fullurl|1={{NAMESPACE}}:{{PAGENAME}}|2=action=history|3=編輯歷史}}中查看添加本模板的編者。<br>本模板是為了避免[[Help:編輯衝突|編輯衝突]]，請於本次重大編輯結束後'''立即移除本模板'''，讓其他編者能繼續編輯本{{NS1}}。<br>致其他編者：當本{{NS1}}'''最後編輯時間（{{TimeSinceLastEdit}}前，{{purge|-{zh-cn:刷新; zh-tw:重新整理}-}}）距今超逾「{{{1|2小時}}}」'''，請直接移除本模板即可。</span>
}}<includeonly>{{#ifeq:{{{nocat|}}}|true||{{{category|{{#switch:{{NAMESPACENUMBER}}|2|3=<!-- no category for user/talk pages-->|#default=[[Category:正在编辑的条目|{{CURRENTTIMESTAMP}}]]}}}}}}}{{#switch:{{NAMESPACENUMBER}}|2|3=|#default={{#ifexpr:{{#time:U}}-{{#time:U|{{REVISIONTIMESTAMP}}}}>7200|[[Category:被擱置的條目]]}}}}</includeonly><noinclude>
{{模板文件}}</noinclude>