{{#switch:{{BASEPAGENAME}}
  |Template messages
  |Cleanup resources= 
  |{{#switch: {{NAMESPACE}}
     |{{ns:0}}
     <!-- |Wikipedia -->
     |File
     |Category
     |Mediawiki
     |Portal
     |Help = <div style="text-align: center;">{{error|'''[[Wikipedia:模板|模板]]擺放位置錯誤，請放在[[{{TALKPAGENAME}}|討論頁]]上。'''}}</div>
[[Category:未正確放置討論頁模板的頁面]]
}}}}{{#ifeq:{{NAMESPACE}}|Template|[[Category:檢查討論名字空間的模板|{{PAGENAME}}]]}}<noinclude>
{{Documentation}}</noinclude>