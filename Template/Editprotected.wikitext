{{#ifeq:{{NAMESPACE}}
| {{TALKSPACE}}
| <!--
-->{{#switch:{{#if:{{{ok|{{{OK|}}}}}}|OK|{{#if:{{{no|{{{NO|}}}}}}|NO}}}}<!--
-->| OK = <span style="border: 1px solid #aaa; background: #f9fcf9; margin-right: .5em; padding: 6px;">[[File:Yes check.svg|20px|link=|alt=]] 请求已处理{{{sign|}}}</span><div style="clear:both;"></div><!--
-->| NO = <span style="border: 1px solid #aaa; background: #f9fcf9; margin-right: .5em; padding: 6px;">[[File:X mark.svg|20px|link=|alt=]] 请求已拒绝{{{sign|}}}</span><div style="clear:both;"></div><!--
-->| #default = <!--
---->{{#ifeq:{{{patch|0}}}{{{patch|1}}}{{{conflict|0}}}{{{conflict|1}}}|0101<!--
---->| {{Editprotected/new}}[[Category:維基百科編輯被保護頁面請求|{{If empty|{{SUBJECTSPACE}}|﹡}}]]<!--
---->| {{Editprotected/patch|patch={{{patch|}}}|conflict={{{conflict|}}}}}<!--
---->}}<!--
-->}}<includeonly><!--
-->{{#if:{{{ok|{{{OK|{{{no|{{{NO|}}}}}}}}}}}}<!--
-->| [[Category:已處理的維基百科編輯被保護頁面請求]]<!--
-->| <!--
---->{{#switch:{{#invoke:Effective protection level|edit|{{SUBJECTPAGENAME}}}}<!--
---->| autoconfirmed = [[Category:維基百科編輯半保護頁面請求|{{If empty|{{SUBJECTSPACE}}|﹡}}]]<!--
---->| extendedconfirmed = [[Category:維基百科編輯延伸確認保護頁面請求|{{If empty|{{SUBJECTSPACE}}|﹡}}]]<!--
---->| templateeditor = [[Category:維基百科編輯模板保護頁面請求|{{If empty|{{SUBJECTSPACE}}|﹡}}]]<!--
---->| * = [[Category:維基百科編輯無保護頁面請求|{{If empty|{{SUBJECTSPACE}}|﹡}}]]<!--
---->| #default = [[Category:維基百科編輯全保護頁面請求|{{If empty|{{SUBJECTSPACE}}|﹡}}]]<!--
---->}}<!--
-->}}</includeonly>
}}<noinclude>
{{Editprotected/new}}
{{Documentation}}</noinclude>