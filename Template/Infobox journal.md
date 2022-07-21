<!-- 以下模板及相关分类来自英文维基百科，用于检查期刊条目是否存在各类缩写重定向，若缺少某个缩写重定向，则通过隐藏式分类页面提醒编者进行创建。本地出于简洁性考虑，暂不引入此套机制，若日后确有需要，可依照英维创建这些模板及分类页面：

{{#if:{{{bypass-rcheck|}}}|[[Category:绕过重定向检查的期刊信息框]]|{{Namespace detect
 |main={{Infobox journal/Bluebook check|1={{{bluebook|}}}}}{{Infobox journal/ISO 4 check|1={{{abbreviation|}}}}}{{Infobox journal/MathSciNet check|1={{{mathscinet|}}}|2={{{ISSN|{{{ISSN1|}}}}}}}}{{Infobox journal/NLM check|1={{{nlm|}}}|2={{{eISSN|{{{ISSN|{{{ISSN1|}}}}}}}}}}}{{Infobox journal/Former check|1={{{formername|{{{former_name|{{{formernames|{{{former_names|}}}}}}}}}}}}|2={{{eISSN|{{{ISSN|{{{ISSN1|}}}}}}}}}}}}}}}{{#ifeq:{{{abbreviation|}}}|no|[[Category:绕过 ISO 4 缩写的期刊信息框]]}}

-->{{Infobox
| bodyclass    = hproduct 
| bodystyle    = {{#if:{{{boxwidth|}}} |width:{{{boxwidth}}};}}

| title        = <includeonly><span class="fn">{{{title|{{PAGENAMEBASE}}}}}</span><!--
 --><span class="Z3988" title="ctx_ver=Z39.88-2004&rft_val_fmt={{urlencode:info:ofi/fmt:kev:mtx:journal}}<!--
     -->{{#if:{{{title|}}} |&rft.jtitle={{urlencode:{{{title}}}}}}}<!--
     -->{{#if:{{{abbreviation|}}} |&rft.stitle={{urlencode:{{{abbreviation}}}}}}}<!--
     -->{{#if:{{{CODEN|{{{CODEN1|}}}}}} |&rft.coden={{urlencode:{{{CODEN|{{{CODEN1}}}}}}}}}}<!--
     -->{{#if:{{{ISSN|{{{ISSN1|}}}}}} |&rft.issn={{urlencode:{{{ISSN|{{{ISSN1}}}}}}}}}}<!--
     -->{{#if:{{{eISSN|{{{eISSN1|}}}}}} |&rft.eissn={{urlencode:{{{eISSN|{{{eISSN1}}}}}}}}}}<!--
     -->{{#if:{{{LCCN|{{{LCCN1|}}}}}} |&rft_id=info:lccn/{{urlencode:{{{LCCN|{{{LCCN1}}}}}}}}}}<!--
     -->{{#if:{{{OCLC|{{{OCLC1|}}}}}} |&rft_id=info:oclcnum/{{urlencode:{{{OCLC|{{{OCLC1}}}}}}}}}}<!--
     -->{{#if:{{{JSTOR|{{{JSTOR1|}}}}}} |&rft_id=//www.jstor.org/journals/{{urlencode:{{{JSTOR|{{{JSTOR1}}}}}}}}#id-name=JSTOR}}<!--
     -->{{#if: {{{website|{{{url|}}}}}} |&rft_id={{urlencode:{{{website|{{{url}}}}}}}}}}"></span></includeonly>
| subheader  = {{#if:{{{native_title|}}} |<div class="nickname" {{#if:{{{native_title_lang|}}}|lang="{{{native_title_lang}}}"}}>''{{{native_title}}}''</div>}}
| image        = {{#invoke:InfoboxImage|InfoboxImage|image={{{cover|{{{image|}}}}}}|size={{#if:{{{image_size|}}}|{{{image_size}}}|200px}}|sizedefault=frameless|alt={{{alt|}}}|suppressplaceholder=yes}} 
| caption      = {{{caption|}}}

| headerstyle  = background:#dfc;
|  datastyle   = text-align:left;

<!---------------------------------（基本信息）---------------------------------->
|  label1      = [[学术领域大纲|{{#if:{{{subject|}}} |科目 |学科}}]]
|  class1      = category
|   data1      = {{#if:{{{subject|}}} |{{{subject}}} |{{{discipline|}}} }}

|  label2      = [[同行評審]]
|   data2      = {{#ifeq:{{lc:{{{peer-reviewed|}}}}}|yes||{{{peer-reviewed|}}}}}{{#if:{{{peer-reviewed|}}}|[[Category:含有 peer-reviewed 参数的期刊信息框]]}}

|  label3      = 语言
|   data3      = {{#if:{{{language|}}}|{{{language|}}}|<includeonly>中文</includeonly>}}

|  label4      = [[主编]]
|   data4      = {{#if:{{{editors|}}} |{{{editors}}} |{{{editor|}}} }}

<!--------------------------- 出版信息 ----------------------------->
| header5      = {{#if:{{{publisher|}}}{{{history|}}}{{{frequency|}}}{{{openaccess|}}}{{{license|}}}{{{impact|}}}|出版-{zh-hans:信息; zh-hant:資訊;}-}}

|  label6      = 曾用名
|   data6      = {{#if:{{{formername|{{{former_name|{{{formernames|{{{former_names|}}}}}}}}}}}}|{{{formername|{{{former_name|{{{formernames|{{{former_names|}}}}}}}}}}}}}}

|  label7      = 出版历史
|   data7      = {{{history|}}}

|  label8      = 出版者
|   data8      = {{#if:{{{publisher|}}} |{{longitem|{{{publisher}}}{{#if:{{{country|}}}|（{{{country}}}）}}}} }} 

|  label9      = [[期刊#發行週期|發行週期]]
|   data9      = {{{frequency|}}}

|  label10     = [[开放获取]]
|   data10     = {{{openaccess|}}}

|  label11     = [[授權 (法律)|许可]]
|   data11     = {{{license|}}}

|  label12     = -{zh-hans:[[影响因子]]; zh-hk:[[影響因子]]; zh-tw:[[影響指數]];}-
|   data12     = {{{impact|}}}{{#if:{{{impact-year|}}}|<span style="font-weight:normal">（{{ifnumber|{{{impact-year|}}}|{{{impact-year}}}年|{{{impact-year}}}}}）</span>}}

<!--------------------------- 缩写 ------------------------------>
| header13     = {{#ifeq:{{{abbreviation|}}}|no||{{#if:{{{abbreviation|}}}{{{bluebook|}}}{{{mathscinet|}}}{{{nlm|}}}|标准缩写<br>{{Infobox journal/Abbreviation search|1={{#if:{{{ISSN|{{{ISSN1|}}}}}}|{{{ISSN|{{{ISSN1|}}}}}}|{{{eISSN|}}}}}|2={{{title|{{PAGENAME}}}}}}}}}}}

|  label14     = {{nowrap|[[蓝皮书|蓝皮书缩写]]}}
|  class14     = identifier
|   data14     = {{#ifeq:{{{bluebook}}}|no||{{#if:{{{bluebook|}}}|''{{smallcaps|{{{bluebook}}}}}''}}}}


|  label15     = {{nowrap|[[ISO 4|ISO 4 缩写]]}}
|  class15     = identifier
|   data15     = {{#ifeq:{{{abbreviation}}}|no||{{#if:{{{abbreviation|}}}|''{{{abbreviation}}}''|{{namespace detect|main=请[https://marcinwrochna.github.io/abbrevIso/?search={{#if:{{{title|}}}|{{urlencode:{{{title|}}}|WIKI}}|{{urlencode:{{PAGENAME}}|WIKI}}}} 在此]搜索 [[Category:缺少 ISO 4 缩写的期刊信息框]]||draft=请[https://marcinwrochna.github.io/abbrevIso/?search={{#if:{{{title|}}}|{{urlencode:{{{title|}}}|WIKI}}|{{urlencode:{{PAGENAME}}|WIKI}}}} 在此搜索]}}}}}}

|  label16     = {{nowrap|[[MathSciNet|MathSciNet 缩写]]}}
|  class16     = identifier
|   data16     = {{#ifeq:{{{mathscinet}}}|no||{{#if:{{{mathscinet|}}}|''{{{mathscinet}}}''}}}}

|  label17     = {{nowrap|[[美国国家医学图书馆|NLM 缩写]]}}
|  class17     = identifier
|   data17     = {{#ifeq:{{{nlm}}}|no||{{#if:{{{nlm|}}}|''{{{nlm}}}''}}}}

<!-------------------------------- 索引 ----------------------------------->
| header18     = {{#if:{{{ISSN|{{{ISSN1|}}}}}}{{{eISSN|{{{eISSN1|}}}}}}{{{LCCN|}}}{{{OCLC|}}}{{{CODEN|}}}{{{JSTOR|}}}|索引{{Infobox journal/Indexing search|1={{#if:{{{ISSN|{{{ISSN1|}}}}}}|{{{ISSN|{{{ISSN1|}}}}}}|{{{eISSN|}}}}}|2={{{title|{{PAGENAME}}}}}}}}}

<!-------------------------------- 期刊1 ---------------------------------->
|   data19     = {{#if:{{{ISSNlabel|{{{ISSNlabel1|{{{ISSN1label|}}}}}}}}}|<div style="text-align: center">''{{longitem|{{{ISSNlabel|{{{ISSNlabel1|{{{ISSN1label|}}}}}}}}}}}''</div>}}

|  label20     = <span class="type">[[CODEN]]</span>
|   data20     = {{#if:{{{CODEN|{{{CODEN1|}}}}}}|{{#ifeq:{{{coden-link1}}}|no|{{{CODEN|{{{CODEN1|}}}}}}|[//cassi.cas.org/searching.jsp?searchIn=codens&exactMatch=y&c=WIy460-R_DY&searchFor={{{CODEN|{{{CODEN1|}}}}}} {{{CODEN|{{{CODEN1|}}}}}}]}}}}

|  label21     = <span class="type">[[國際標準期刊號|ISSN]]</span>
|   data21     = {{#if:{{{ISSN|{{{ISSN1|}}}}}}{{{eISSN|{{{eISSN1|}}}}}}|{{Infobox journal/ISSN-eISSN|{{{ISSN|{{{ISSN1|}}}}}}|{{{eISSN|{{{eISSN1|}}}}}}}}}}

|  label22     = <span class="type">[[国内统一连续出版物号|CN]]</span>
|   data22     = {{{CN|{{{CN1|}}}}}}

|  label23     = <span class="type">[[LCCN]]</span>
|   data23     = {{#if:{{{LCCN|{{{LCCN1|}}}}}}|[//lccn.loc.gov/{{{LCCN|{{{LCCN1|}}}}}} {{{LCCN|{{{LCCN1|}}}}}}]}}

|  label24     = <span class="type">[[JSTOR]]</span>
|   data24     = {{#if:{{{JSTOR|{{{JSTOR1|}}}}}}|[//www.jstor.org/journals/{{{JSTOR|{{{JSTOR1|}}}}}} {{{JSTOR|{{{JSTOR1|}}}}}}]}}

|  label25     = <span class="type">{{nowrap|[[OCLC]] 編號}}</span>
|   data25     = {{#if:{{{OCLC|{{{OCLC1|}}}}}}|[//www.worldcat.org/oclc/{{{OCLC|{{{OCLC1|}}}}}} {{{OCLC|{{{OCLC1|}}}}}}]}}

<!-------------------------------- 期刊2 ---------------------------------->
|   data26     = {{#if:{{{ISSNlabel2|{{{ISSN2label|}}}}}}|<div style="text-align: center">''{{longitem|{{{ISSNlabel2|{{{ISSN2label|}}}}}}}}''</div>}}

|  label27     = <span class="type">[[CODEN]]</span>
|   data27     = {{#if:{{{CODEN2|}}}|{{#ifeq:{{{coden-link2}}}|no|{{{CODEN2|}}}|[//cassi.cas.org/searching.jsp?searchIn=codens&exactMatch=y&c=WIy460-R_DY&searchFor={{{CODEN2|}}} {{{CODEN2|}}}]}}}}

|  label28     = <span class="type">[[國際標準期刊號|ISSN]]</span>
|   data28     = {{#if:{{{ISSN2|}}}{{{eISSN2|}}}|{{Infobox journal/ISSN-eISSN|{{{ISSN2|}}}|{{{eISSN2|}}}}}}}

|  label29     = <span class="type">[[国内统一连续出版物号|CN]]</span>
|   data29     = {{{CN2|}}}

|  label30     = <span class="type">[[LCCN]]</span>
|   data30     = {{#if:{{{LCCN2|}}}|[//lccn.loc.gov/{{{LCCN2}}} {{{LCCN2}}}]}}

|  label31     = <span class="type">[[JSTOR]]</span>
|   data31     = {{#if:{{{JSTOR2|}}}|[//www.jstor.org/journals/{{{JSTOR2}}} {{{JSTOR2}}}]}}

|  label32     = <span class="type">{{nowrap|[[OCLC]] 編號}}&nbsp;no.</span>
|   data32     = {{#if:{{{OCLC2|}}}|[//www.worldcat.org/oclc/{{{OCLC2}}} {{{OCLC2}}}]}}

<!-------------------------------- 期刊3 ---------------------------------->
|   data33     = {{#if:{{{ISSNlabel3|{{{ISSN3label|}}}}}}|<div style="text-align: center">''{{longitem|{{{ISSNlabel3|{{{ISSN3label|}}}}}}}}''</div>}}

|  label34     = <span class="type">[[CODEN]]</span>
|   data34     = {{#if:{{{CODEN3|}}}|{{#ifeq:{{{coden-link3}}}|no|{{{CODEN3|}}}|[//cassi.cas.org/searching.jsp?searchIn=codens&exactMatch=y&c=WIy460-R_DY&searchFor={{{CODEN3|}}} {{{CODEN3|}}}]}}}}

|  label35     = <span class="type">[[國際標準期刊號|ISSN]]</span>
|   data35     = {{#if:{{{ISSN3|}}}{{{eISSN3|}}}|{{Infobox journal/ISSN-eISSN|{{{ISSN3|}}}|{{{eISSN3|}}}}}}}

|  label36     = <span class="type">[[国内统一连续出版物号|CN]]</span>
|   data36     = {{{CN3|}}}

|  label37     = <span class="type">[[LCCN]]</span>
|   data37     = {{#if:{{{LCCN3|}}}|[//lccn.loc.gov/{{{LCCN3}}} {{{LCCN3}}}]}}

|  label38     = <span class="type">[[JSTOR]]</span>
|   data38     = {{#if:{{{JSTOR3|}}}|[//www.jstor.org/journals/{{{JSTOR3}}} {{{JSTOR3}}}]}}

|  label39     = <span class="type">{{nowrap|[[OCLC]] 編號}}&nbsp;no.</span>
|   data39     = {{#if:{{{OCLC3|}}}|[//www.worldcat.org/oclc/{{{OCLC3}}} {{{OCLC3}}}]}}

<!-------------------------------- 期刊4 ---------------------------------->
|   data40     = {{#if:{{{ISSNlabel4|{{{ISSN4label|}}}}}}|<div style="text-align: center">''{{longitem|{{{ISSNlabel4|{{{ISSN4label|}}}}}}}}''</div>}}

|  label41     = <span class="type">[[CODEN]]</span>
|   data41     = {{#if:{{{CODEN4|}}}|{{#ifeq:{{{coden-link4}}}|no|{{{CODEN4|}}}|[//cassi.cas.org/searching.jsp?searchIn=codens&exactMatch=y&c=WIy460-R_DY&searchFor={{{CODEN4|}}} {{{CODEN4|}}}]}}}}

|  label42     = <span class="type">[[國際標準期刊號|ISSN]]</span>
|   data42     = {{#if:{{{ISSN4|}}}{{{eISSN4|}}}|{{Infobox journal/ISSN-eISSN|{{{ISSN4|}}}|{{{eISSN4|}}}}}}}

|  label43     = <span class="type">[[国内统一连续出版物号|CN]]</span>
|   data43     = {{{CN4|}}}

|  label44     = <span class="type">[[LCCN]]</span>
|   data44     = {{#if:{{{LCCN4|}}}|[//lccn.loc.gov/{{{LCCN4}}} {{{LCCN4}}}]}}

|  label45     = <span class="type">[[JSTOR]]</span>
|   data45     = {{#if:{{{JSTOR4|}}}|[//www.jstor.org/journals/{{{JSTOR4}}} {{{JSTOR4}}}]}}

|  label46     = <span class="type">{{nowrap|[[OCLC]] 編號}}&nbsp;no.</span>
|   data46     = {{#if:{{{OCLC4|}}}|[//www.worldcat.org/oclc/{{{OCLC4}}} {{{OCLC4}}}]}}


<!-------------------------------- 期刊5 ---------------------------------->
|   data47     = {{#if:{{{ISSNlabel5|{{{ISSN5label|}}}}}}|<div style="text-align: center">''{{longitem|{{{ISSNlabel5|{{{ISSN5label|}}}}}}}}''</div>}}

|  label48     = <span class="type">[[CODEN]]</span>
|   data48     = {{#if:{{{CODEN5|}}}|{{#ifeq:{{{coden-link5}}}|no|{{{CODEN5|}}}|[//cassi.cas.org/searching.jsp?searchIn=codens&exactMatch=y&c=WIy460-R_DY&searchFor={{{CODEN5|}}} {{{CODEN5|}}}]}}}}

|  label49     = <span class="type">[[國際標準期刊號|ISSN]]</span>
|   data49     = {{#if:{{{ISSN5|}}}{{{eISSN5|}}}|{{Infobox journal/ISSN-eISSN|{{{ISSN5|}}}|{{{eISSN5|}}}}}}}

|  label50     = <span class="type">[[国内统一连续出版物号|CN]]</span>
|   data50     = {{{CN5|}}}

|  label51     = <span class="type">[[LCCN]]</span>
|   data51     = {{#if:{{{LCCN5|}}}|[//lccn.loc.gov/{{{LCCN5}}} {{{LCCN5}}}]}}

|  label52     = <span class="type">[[JSTOR]]</span>
|   data52     = {{#if:{{{JSTOR5|}}}|[//www.jstor.org/journals/{{{JSTOR5}}} {{{JSTOR5}}}]}}

|  label53     = <span class="type">{{nowrap|[[OCLC]] 編號}}&nbsp;no.</span>
|   data53     = {{#if:{{{OCLC5|}}}|[//www.worldcat.org/oclc/{{{OCLC5}}} {{{OCLC5}}}]}}

<!-------------------------------- 期刊6 ---------------------------------->
|   data54     = {{#if:{{{ISSNlabel6|{{{ISSN6label|}}}}}}|<div style="text-align: center">''{{longitem|{{{ISSNlabel6|{{{ISSN6label|}}}}}}}}''</div>}}

|  label55     = <span class="type">[[CODEN]]</span>
|   data55     = {{#if:{{{CODEN6|}}}|{{#ifeq:{{{coden-link6}}}|no|{{{CODEN6|}}}|[//cassi.cas.org/searching.jsp?searchIn=codens&exactMatch=y&c=WIy460-R_DY&searchFor={{{CODEN6|}}} {{{CODEN6|}}}]}}}}

|  label56     = <span class="type">[[國際標準期刊號|ISSN]]</span>
|   data56     = {{#if:{{{ISSN6|}}}{{{eISSN6|}}}|{{Infobox journal/ISSN-eISSN|{{{ISSN6|}}}|{{{eISSN6|}}}}}}}

|  label57     = <span class="type">[[国内统一连续出版物号|CN]]</span>
|   data57     = {{{CN6|}}}

|  label58     = <span class="type">[[LCCN]]</span>
|   data58     = {{#if:{{{LCCN6|}}}|[//lccn.loc.gov/{{{LCCN6}}} {{{LCCN6}}}]}}

|  label59     = <span class="type">[[JSTOR]]</span>
|   data59     = {{#if:{{{JSTOR6|}}}|[//www.jstor.org/journals/{{{JSTOR6}}} {{{JSTOR6}}}]}}

|  label60     = <span class="type">{{nowrap|[[OCLC]] 編號}}&nbsp;no.</span>
|   data60     = {{#if:{{{OCLC6|}}}|[//www.worldcat.org/oclc/{{{OCLC6}}} {{{OCLC6}}}]}}

<!-------------------------------- 期刊7 ---------------------------------->
|   data61     = {{#if:{{{ISSNlabel7|{{{ISSN7label|}}}}}}|<div style="text-align: center">''{{longitem|{{{ISSNlabel7|{{{ISSN7label|}}}}}}}}''</div>}}

|  label62     = <span class="type">[[CODEN]]</span>
|   data62     = {{#if:{{{CODEN7|}}}|{{#ifeq:{{{coden-link7}}}|no|{{{CODEN7|}}}|[//cassi.cas.org/searching.jsp?searchIn=codens&exactMatch=y&c=WIy460-R_DY&searchFor={{{CODEN7|}}} {{{CODEN7|}}}]}}}}

|  label63     = <span class="type">[[國際標準期刊號|ISSN]]</span>
|   data63     = {{#if:{{{ISSN7|}}}{{{eISSN7|}}}|{{Infobox journal/ISSN-eISSN|{{{ISSN7|}}}|{{{eISSN7|}}}}}}}

|  label64     = <span class="type">[[国内统一连续出版物号|CN]]</span>
|   data64     = {{{CN7|}}}

|  label65     = <span class="type">[[LCCN]]</span>
|   data65     = {{#if:{{{LCCN7|}}}|[//lccn.loc.gov/{{{LCCN7}}} {{{LCCN7}}}]}}

|  label66     = <span class="type">[[JSTOR]]</span>
|   data66     = {{#if:{{{JSTOR7|}}}|[//www.jstor.org/journals/{{{JSTOR7}}} {{{JSTOR7}}}]}}

|  label67     = <span class="type">{{nowrap|[[OCLC]] 編號}}&nbsp;no.</span>
|   data67     = {{#if:{{{OCLC7|}}}|[//www.worldcat.org/oclc/{{{OCLC7}}} {{{OCLC7}}}]}}

<!-------------------------------- 期刊8 ---------------------------------->
|   data68     = {{#if:{{{ISSNlabel8|{{{ISSN8label|}}}}}}|<div style="text-align: center">''{{longitem|{{{ISSNlabel8|{{{ISSN8label|}}}}}}}}''</div>}}

|  label69     = <span class="type">[[CODEN]]</span>
|   data69     = {{#if:{{{CODEN8|}}}|{{#ifeq:{{{coden-link8}}}|no|{{{CODEN8|}}}|[//cassi.cas.org/searching.jsp?searchIn=codens&exactMatch=y&c=WIy460-R_DY&searchFor={{{CODEN8|}}} {{{CODEN8|}}}]}}}}

|  label70     = <span class="type">[[國際標準期刊號|ISSN]]</span>
|   data70     = {{#if:{{{ISSN8|}}}{{{eISSN8|}}}|{{Infobox journal/ISSN-eISSN|{{{ISSN8|}}}|{{{eISSN8|}}}}}}}

|  label71     = <span class="type">[[国内统一连续出版物号|CN]]</span>
|   data71     = {{{CN8|}}}

|  label72     = <span class="type">[[LCCN]]</span>
|   data72     = {{#if:{{{LCCN8|}}}|[//lccn.loc.gov/{{{LCCN8}}} {{{LCCN8}}}]}}

|  label73     = <span class="type">[[JSTOR]]</span>
|   data73     = {{#if:{{{JSTOR8|}}}|[//www.jstor.org/journals/{{{JSTOR8}}} {{{JSTOR8}}}]}}

|  label74     = <span class="type">{{nowrap|[[OCLC]] 編號}}&nbsp;no.</span>
|   data74     = {{#if:{{{OCLC8|}}}|[//www.worldcat.org/oclc/{{{OCLC8}}} {{{OCLC8}}}]}}

<!-------------------------------- 期刊9 ---------------------------------->
|   data75     = {{#if:{{{ISSNlabel9|{{{ISSN9label|}}}}}}|<div style="text-align: center">''{{longitem|{{{ISSNlabel9|{{{ISSN9label|}}}}}}}}''</div>}}

|  label76     = <span class="type">[[CODEN]]</span>
|   data76     = {{#if:{{{CODEN9|}}}|{{#ifeq:{{{coden-link9}}}|no|{{{CODEN9|}}}|[//cassi.cas.org/searching.jsp?searchIn=codens&exactMatch=y&c=WIy460-R_DY&searchFor={{{CODEN9|}}} {{{CODEN9|}}}]}}}}

|  label77     = <span class="type">[[國際標準期刊號|ISSN]]</span>
|   data77     = {{#if:{{{ISSN9|}}}{{{eISSN9|}}}|{{Infobox journal/ISSN-eISSN|{{{ISSN9|}}}|{{{eISSN9|}}}}}}}

|  label78     = <span class="type">[[国内统一连续出版物号|CN]]</span>
|   data78     = {{{CN9|}}}

|  label79     = <span class="type">[[LCCN]]</span>
|   data79     = {{#if:{{{LCCN9|}}}|[//lccn.loc.gov/{{{LCCN9}}} {{{LCCN9}}}]}}

|  label80     = <span class="type">[[JSTOR]]</span>
|   data80     = {{#if:{{{JSTOR9|}}}|[//www.jstor.org/journals/{{{JSTOR9}}} {{{JSTOR9}}}]}}

|  label81     = <span class="type">{{nowrap|[[OCLC]] 編號}}&nbsp;no.</span>
|   data81     = {{#if:{{{OCLC9|}}}|[//www.worldcat.org/oclc/{{{OCLC9}}} {{{OCLC9}}}]}}

<!-------------------------------- 期刊10 ---------------------------------->
|   data82     = {{#if:{{{ISSNlabel10|{{{ISSN10label|}}}}}}|<div style="text-align: center">''{{longitem|{{{ISSNlabel10|{{{ISSN10label|}}}}}}}}''</div>}}

|  label83     = <span class="type">[[CODEN]]</span>
|   data83     = {{#if:{{{CODEN10|}}}|{{#ifeq:{{{coden-link10}}}|no|{{{CODEN10|}}}|[//cassi.cas.org/searching.jsp?searchIn=codens&exactMatch=y&c=WIy460-R_DY&searchFor={{{CODEN10|}}} {{{CODEN10|}}}]}}}}

|  label84     = <span class="type">[[國際標準期刊號|ISSN]]</span>
|   data84     = {{#if:{{{ISSN10|}}}{{{eISSN10|}}}|{{Infobox journal/ISSN-eISSN|{{{ISSN10|}}}|{{{eISSN10|}}}}}}}

|  label85     = <span class="type">[[国内统一连续出版物号|CN]]</span>
|   data85     = {{{CN10|}}}

|  label86     = <span class="type">[[LCCN]]</span>
|   data86     = {{#if:{{{LCCN10|}}}|[//lccn.loc.gov/{{{LCCN10}}} {{{LCCN10}}}]}}

|  label87     = <span class="type">[[JSTOR]]</span>
|   data87     = {{#if:{{{JSTOR10|}}}|[//www.jstor.org/journals/{{{JSTOR10}}} {{{JSTOR10}}}]}}

|  label88     = <span class="type">{{nowrap|[[OCLC]] 編號}}&nbsp;no.</span>
|   data88     = {{#if:{{{OCLC10|}}}|[//www.worldcat.org/oclc/{{{OCLC10}}} {{{OCLC10}}}]}}

<!---------------------------------- 链接 ------------------------------------>
| header89     = {{#if:{{{website|{{{url|}}}}}}{{{link1|}}}|-{zh-hans:链接; zh-hant:連結;}-}}

|   data90     = {{#if:{{{website|{{{url|}}}}}} |
* [{{{website|{{{url}}}}}} {{#if:{{{type|}}}|{{ucfirst:{{{type|}}}}}|期刊}}首页]}}{{#if:{{{link1|}}} |
* [{{{link1}}} {{{link1-name}}}]}}{{#if:{{{link1-at|}}}|&#32;at {{{link1-at}}}}}{{#if:{{{link2|}}} |
* [{{{link2}}} {{{link2-name}}}]}}{{#if:{{{link2-at|}}}|&#32;at {{{link2-at}}}}}{{#if:{{{link3|}}} |
* [{{{link3}}} {{{link3-name}}}]}}{{#if:{{{link3-at|}}}|&#32;at {{{link3-at}}}}}{{#if:{{{link4|}}} |
* [{{{link4}}} {{{link4-name}}}]}}{{#if:{{{link4-at|}}}|&#32;at {{{link4-at}}}}}{{#if:{{{link5|}}} |
* [{{{link5}}} {{{link5-name}}}]}}{{#if:{{{link5-at|}}}|&#32;at {{{link5-at}}}}}{{#if:{{{link6|}}} |
* [{{{link6}}} {{{link6-name}}}]}}{{#if:{{{link6-at|}}}|&#32;at {{{link6-at}}}}}{{#if:{{{link7|}}} |
* [{{{link7}}} {{{link7-name}}}]}}{{#if:{{{link7-at|}}}|&#32;at {{{link7-at}}}}}{{#if:{{{link8|}}} |
* [{{{link8}}} {{{link8-name}}}]}}{{#if:{{{link8-at|}}}|&#32;at {{{link8-at}}}}}{{#if:{{{link9|}}} |
* [{{{link9}}} {{{link9-name}}}]}}{{#if:{{{link9-at|}}}|&#32;at {{{link9-at}}}}}{{#if:{{{link10|}}} |
* [{{{link10}}} {{{link10-name}}}]}}{{#if:{{{link10-at|}}}|&#32;at {{{link10-at}}}}}
}}<includeonly><!-- 

   ------- 自动分类 --------
-->{{ns0|{{#if:{{{ISSN|{{{ISSN1}}}}}}{{{eISSN}}}{{{LCCN}}}{{{OCLC}}}{{{CODEN}}} | |[[Category:需要 ISSN 的页面]]}}}}<!--
-->{{ns0|{{#if:{{{impact-year|}}}|{{#ifeq:{{{impact-year|}}}|2020||[[Category:含有{{{impact-year}}}年的过时影响因子的条目]]}}}}}}<!--

   ------- 参数查验 -------
-->{{#ifeq:{{{licence|xz}}}|xz | |<br/>Infobox journal: invalid "licence" - try "licen'''s'''e=copyright"}}<!--
-->{{#ifeq:{{{URL|xz}}}    |xz | |<br/>Infobox journal: invalid "URL" - try lowercase "url=" or "website=".}}<!--
-->{{#ifeq:{{{jstor|xz}}}  |xz | |<br/>Infobox journal: invalid "jstor" - try uppercase "JSTOR=".}}<!--
-->{{#ifeq:{{{issn|xz}}}   |xz | |<br/>Infobox journal: invalid "issn" - try uppercase "ISSN=".}}<!--
-->{{#ifeq:{{{eissn|xz}}}  |xz | |<br/>Infobox journal: invalid "eissn" - try uppercase "eISSN=".}}<!--
-->{{#ifeq:{{{lccn|xz}}}   |xz | |<br/>Infobox journal: invalid "lccn" - try uppercase "LCCN=".}}<!--
-->{{#ifeq:{{{oclc|xz}}}   |xz | |<br/>Infobox journal: invalid "oclc" - try uppercase "OCLC=".}}<!--
-->{{#ifeq:{{{coden|xz}}}  |xz | |<br/>Infobox journal: invalid "coden" - try uppercase "CODEN=".}}<!--
-->{{#ifeq:{{{Coden|xz}}}  |xz | |<br/>Infobox journal: invalid "Coden" - try uppercase "CODEN=".}}<!--
--></includeonly>{{#invoke:Check for unknown parameters|check|unknown={{main other|[[Category:含有未知参数的期刊信息框|_VALUE_{{PAGENAME}}]]}}|preview=[[Template:Infobox journal]] 含有未知参数“_VALUE_”|ignoreblank=y| abbreviation | alt | boxwidth | caption | CN | CN1 | CN2 | CN3 | CN4 | CN5 | CN6 | CN7 | CN8 | CN9 | CN10 | CODEN | CODEN1 | CODEN2 | CODEN3 | CODEN4 | CODEN5 | CODEN6 | CODEN7 | CODEN8 | CODEN9 | CODEN10 | coden-link1 | coden-link2 | coden-link3 | coden-link4 | coden-link5 | coden-link6 | coden-link7 | coden-link8 | coden-link9 | coden-link10 | country | cover | discipline | editor | editors | eISSN | eISSN1 | eISSN2 | eISSN3 | eISSN4 | eISSN5 | eISSN6 | eISSN7 | eISSN8 | eISSN9 | eISSN10 | former_name | former_names | formername | formernames | frequency | history | image | image_size | impact | impact-year | ISSN | ISSN1 | ISSN1label | ISSN2 | ISSN2label | ISSN3 | ISSN3label | ISSN4 | ISSN4label | ISSN5 | ISSN5label | ISSN6 | ISSN6label | ISSN7 | ISSN7label | ISSN8 | ISSN8label | ISSN9 | ISSN9label | ISSN10 | ISSN10label | ISSNlabel | ISSNlabel1 | ISSNlabel2 | ISSNlabel3 | ISSNlabel4 | ISSNlabel5 | ISSNlabel6 | ISSNlabel7 | ISSNlabel8 | ISSNlabel9 | ISSNlabel10 | native_title | native_title_lang | JSTOR | JSTOR1 | JSTOR2 | JSTOR3 | JSTOR4 | JSTOR5 | JSTOR6 | JSTOR7 | JSTOR8 | JSTOR9 | JSTOR10 | language | LCCN | LCCN1 | LCCN2 | LCCN3 | LCCN4 | LCCN5 | LCCN6 | LCCN7 | LCCN8 | LCCN9 | LCCN10 | license | link1 | link1-name | link1-at | link2 | link2-name | link2-at | link3 | link3-name | link3-at | link4 | link4-name | link4-at | link5 | link5-name | link5-at | link6 | link6-name | link6-at | link7 | link7-name | link7-at | link8 | link8-name | link9-at | link9 | link9-name | link9-at | link10 | link10-name | link10-at | OCLC | OCLC1 | OCLC2 | OCLC3 | OCLC4 | OCLC5 | OCLC6 | OCLC7 | OCLC8 | OCLC9 | OCLC10 | openaccess | peer-reviewed | publisher | subject | title | url | website | bluebook | bypass-rcheck | nlm | mathscinet | type}}<noinclude>{{Documentation}}</noinclude>