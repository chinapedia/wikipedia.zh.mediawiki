{{infobox 
| child      = {{Yesno|{{{embed|no}}}}}
| labelstyle = white-space:nowrap

| abovestyle = background-color:{{{background|{{{Background|lightgrey}}}}}}
| above      = <includeonly>{{#if:{{{name|}}}{{{Name|}}}|{{{name|}}}{{{Name|}}}|{{PAGENAME}}}}</includeonly><noinclude>{{{name}}}或<nowiki>{{PAGENAME}}</nowiki></noinclude>

| label1 = [[同义词]]<!-- singular/plural -->
|  data1 = {{{Synonym|}}}{{{synonym|}}}{{{Synonyms|}}}{{{synonyms|}}}

<!-- image, caption -->
|  data5 = {{#invoke:InfoboxImageVariant|main
  | image = {{{image|{{{Image|}}}}}} | alt = {{{alt|{{{Alt|}}}}}}
  | image-hans = {{{image-hans|{{{Image-hans|}}}}}} | alt-hans = {{{alt-hans|{{{Alt-hans|}}}}}}
  | image-hant = {{{image-hant|{{{Image-hant|}}}}}} | alt-hant = {{{alt-hant|{{{Alt-hant|}}}}}}
  | image-cn = {{{image-cn|{{{Image-cn|}}}}}} | alt-cn = {{{alt-cn|{{{Alt-cn|}}}}}}
  | image-hk = {{{image-hk|{{{Image-hk|}}}}}} | alt-hk = {{{alt-hk|{{{Alt-hk|}}}}}}
  | image-mo = {{{image-mo|{{{Image-mo|}}}}}} | alt-mo = {{{alt-mo|{{{Alt-mo|}}}}}}
  | image-my = {{{image-my|{{{Image-my|}}}}}} | alt-my = {{{alt-my|{{{Alt-my|}}}}}}
  | image-sg = {{{image-sg|{{{Image-sg|}}}}}} | alt-sg = {{{alt-sg|{{{Alt-sg|}}}}}}
  | image-tw = {{{image-tw|{{{Image-tw|}}}}}} | alt-tw = {{{alt-tw|{{{Alt-tw|}}}}}}
  | size = {{{image_size|{{{Width|{{{width|}}}}}}}}}
  | sizedefault = frameless
  | upright = 1.36
  }}
|  data6 = {{#if:{{{image|}}}{{{Image|}}}|{{{caption|}}}{{{Caption|}}} }}

| label7 = 读音
|  data7 = {{#if:{{{pronounce|}}}{{{Pronounce|}}}{{{Pronunciation|}}}{{{pronunciation|}}}{{{pronounce comment|}}} |<!--
-->{{ubl|1={{{pronounce|}}}{{{Pronounce|}}}{{{Pronunciation|}}}{{{pronunciation|}}}{{{pronounce ref|}}}&#x20;{{{pronounce comment|}}}<!--
     -->|2={{{pronounce 2|}}} }}}}

| label11  = 症状
|  data11  = {{#invoke:Wikidata|getValue|P780|{{{Symptoms|{{{symptoms|FETCH_WIKIDATA}}}}}}}}

| label12  = [[併發症]]
|  data12  = {{{complications|{{{Complications|}}}}}}

| label13  = 常見始發於<!--{{incomprehensible|reason=原文是 usual onset}}-->
|  data13  = {{{Onset|{{{onset|}}}}}}

| label14  = [[病程]]
|  data14  = {{{Duration|{{{duration|}}}}}}

| label15  = 肇因
|  data15  = {{#invoke:Wikidata|getValue|P828|{{{causes|{{{Causes|{{{cause|{{{Cause|FETCH_WIKIDATA}}}}}}}}}}}}}}

| label16  = [[风险因子]]
|  data16  = {{#invoke:Wikidata|getValue|P5642|{{{risks|{{{Risks|{{{risk|{{{Risk|FETCH_WIKIDATA}}}}}}}}}}}}}}

| label17  = [[诊断|診斷方法]]
|  data17  = {{#invoke:Wikidata|getValue|P923|{{{Diagnosis|{{{diagnosis|FETCH_WIKIDATA}}}}}}}}

| label18  = [[鑑別診斷|相似疾病或共病]]<!--{{incomprehensible|reason=建議將表面的名字以"相似疾病"呈現。英文讀者直接從英文字面意思即可得知含意，然而中文讀這卻要進入條目看那一些文字才"可能"了解這個術語的意思}}--><!--英文版已改成similar conditions-->
|  data18  = {{{differential|{{{Differential|{{{Differential diagnosis|{{{differential diagnosis|{{{diff|{{{Diff|}}}}}}}}}}}}}}}}}}

| label19  = 預防
|  data19  = {{{Prevention|{{{prevention|}}}}}}

| label20  = {{#if:{{{management|}}}|管理|治療}}
|  data20  = {{#invoke:Wikidata|getValue|P924|{{{Management|{{{management|{{{Treatment|{{{treatment|FETCH_WIKIDATA}}}}}}}}}}}}}}

| label21  = 藥物
|  data21  = {{{Medication|{{{medication|}}}}}}

| label22  = [[预后]]
|  data22  = {{{Prognosis|{{{prognosis|}}}}}}

| label23  = [[患病率|盛行率]]
|  data23  = {{#if:{{{frequency|}}}|{{{frequency|{{#invoke:PrevalenceData|main}}}}}|{{#invoke:Wikidata|getValue|P1603|{{{frequency|FETCH_WIKIDATA}}}}}}}

| label24 = 死亡數
|  data24 = {{#invoke:Wikidata|getValue|P1120|{{{Deaths|{{{deaths|FETCH_WIKIDATA}}}}}}}}

| headerstyle = background:{{{Background|#eee;}}};
| header31 = 分类和外部资源

| label32 = [[醫學專科]]
|  data32 = {{#if:{{{field|}}}{{{Field|}}}{{{specialty|}}}{{{Specialty|}}}{{{Speciality|}}}{{{speciality|}}}
 |{{{field|}}}{{{Field|}}}{{{specialty|}}}{{{Specialty|}}}{{{Speciality|}}}{{{speciality|}}}
 |{{#statements:P1995}} }}

| label33 = [[國際疾病與相關健康問題統計分類|ICD]]-[[ICD-11|11]]
|  data33 = {{#invoke:Wikidata|getValue|P7329|{{{ICD11|FETCH_WIKIDATA}}}}}

| label34 = [[國際疾病與相關健康問題統計分類|ICD]]-[[ICD-10|10]]
|  data34 = {{#invoke:Wikidata|getValue|P494|{{{ICD10|FETCH_WIKIDATA}}}}}

| label35 = [[國際疾病與相關健康問題統計分類|ICD]]-[[ICD-9编码列表|9-CM]]
|  data35 = {{#invoke:Wikidata|getValue|P1692|{{{ICD9|FETCH_WIKIDATA}}}}}

| label36 = {{tsl|en|International Classification of Diseases for Oncology||ICD-O}}
|  data36 = {{{ICDO|}}}

| label41 = [[人類孟德爾遺傳學|OMIM]]
|  data41 = {{#if:{{{OMIM|}}}{{#statements:P492}}|[https://omim.org/entry/{{#invoke:Wikidata|getValue|P492|{{{OMIM|FETCH_WIKIDATA}}}}} {{#invoke:Wikidata|getValue|P492|{{{OMIM|FETCH_WIKIDATA}}}}}] {{{OMIM_mult|}}} }}

| label42 = [[疾病資料庫|DiseasesDB]]
|  data42 = {{#if:{{{DiseasesDB|}}}{{#statements:P557}}|[http://www.diseasesdatabase.com/ddb{{#invoke:Wikidata|getValue|P557|{{{DiseasesDB|FETCH_WIKIDATA}}}}}.htm {{#invoke:Wikidata|getValue|P557|{{{DiseasesDB|FETCH_WIKIDATA}}}}}] {{{DiseasesDB_mult|}}} }}

| label43 = [[MedlinePlus]]
|  data43 = {{#if:{{{MedlinePlus|}}}{{#statements:P604}}|[https://medlineplus.gov/ency/article/{{#invoke:Wikidata|getValue|P604|{{{MedlinePlus|FETCH_WIKIDATA}}}}}.htm {{#invoke:Wikidata|getValue|P604|{{{MedlinePlus|FETCH_WIKIDATA}}}}}]  {{{MedlinePlus_mult|}}} }}

| label44 = [[eMedicine]]
|  data44 = {{#if:{{{eMedicineSubj|}}}|{{#ifeq:{{{eMedicineSubj|}}}|search|[http://search.medscape.com/emedicine-search?queryText={{{eMedicineTopic}}} topic list]|{{#ifeq:{{{eMedicineSubj|}}}|article|[http://emedicine.medscape.com/article/{{{eMedicineTopic}}}-overview|[http://www.emedicine.com/{{{eMedicineSubj}}}/topic{{{eMedicineTopic}}}.htm}} {{{eMedicineSubj}}}/{{{eMedicineTopic}}}]}} |{{#statements:P673}}}} {{{eMedicine_mult|}}}

<!-- | label18 = [[美国国家癌症研究所|NCI]]
|  data18 = {{#if:{{#property:P1395}}|[http://www.cancer.gov{{#property:P1395}} {{{name|{{PAGENAME}}}}}] }} -->

| label45 = {{en-link|Patient UK}}
|  data45 = {{#if:{{#property:P1461}}|[http://patient.info/doctor/{{#property:P1461}} {{{name|{{PAGENAME}}}}}] }}

| label46 = [[医学主题词|MeSH]]
|  data46 = {{comma separated entries
  | 1 = {{#if:{{{MeshID|{{{MeSH|{{{MeSH1|}}}}}}}}} | {{mesh2|{{{MeshID|{{{MeSH|{{{MeSH1}}}}}}}}}|year= {{{MeshYear|{{{MeshYear1|}}}}}} }} }}
  | 2 = {{#if:{{{MeSH2|}}} | {{mesh2|{{{MeSH2|}}}|year={{{MeshYear2|}}}}} }}
  | 3 = {{#if:{{{MeSH3|}}} | {{mesh2|{{{MeSH3|}}}|year={{{MeshYear3|}}}}} }}
  | 4 = {{#if:{{{MeSH4|}}} | {{mesh2|{{{MeSH4|}}}|year={{{MeshYear4|}}}}} }}
  | 5 = {{#if:{{{MeSH5|}}} | {{mesh2|{{{MeSH5|}}}|year={{{MeshYear5|}}}}} }}
  | 6 = {{#if:{{{MeSH6|}}} | {{mesh2|{{{MeSH6|}}}|year={{{MeshYear6|}}}}} }}
  | 7 = {{#if:{{{MeSH7|}}} | {{mesh2|{{{MeSH7|}}}|year={{{MeshYear7|}}}}} }}
  | 8 = {{#if:{{{MeSH8|}}} | {{mesh2|{{{MeSH8|}}}|year={{{MeshYear8|}}}}} }}
  | 9 = {{#if:{{{MeSH9|}}} | {{mesh2|{{{MeSH9|}}}|year={{{MeshYear9|}}}}} }}
  |10 = {{#if: {{{MeshName|}}} | ''{{mesh2 | name = {{{MeshName}}} | number = {{{MeshNumber|}}} }}'' }}
  }}

| label47 = [[GeneReviews]]
| class47 = plainlist
|  data47 = {{#if: {{{GeneReviewsNBK|}}}{{{GeneReviewsNBK1|}}}| 
* {{NCBIBook2|{{{GeneReviewsNBK|{{{GeneReviewsNBK1}}}}}}|{{{GeneReviewsName|{{{GeneReviewsName1|}}}}}}}}|{{#if: {{{GeneReviewsID|}}}| 
* [https://www.ncbi.nlm.nih.gov/books/n/gene/{{{GeneReviewsID}}}/ {{#if: {{{GeneReviewsName|}}}|{{{GeneReviewsName}}}|{{{GeneReviewsID}}}}}]}}}}{{#if: {{{GeneReviewsNBK2|}}}| 
* {{NCBIBook2|{{{GeneReviewsNBK2}}}|{{{GeneReviewsName2|}}}}}}}{{#if: {{{GeneReviewsNBK3|}}}| 
* {{NCBIBook2|{{{GeneReviewsNBK3}}}|{{{GeneReviewsName3|}}}}}}}{{#if: {{{GeneReviewsNBK4|}}}| 
* {{NCBIBook2|{{{GeneReviewsNBK4}}}|{{{GeneReviewsName4|}}}}}}}{{#if: {{{GeneReviewsNBK5|}}}| 
* {{NCBIBook2|{{{GeneReviewsNBK5}}}|{{{GeneReviewsName5|}}}}}}}{{#if: {{{GeneReviewsNBK6|}}}| 
* {{NCBIBook2|{{{GeneReviewsNBK6}}}|{{{GeneReviewsName6|}}}}}}}{{#if: {{{GeneReviewsNBK7|}}}| 
* {{NCBIBook2|{{{GeneReviewsNBK7}}}|{{{GeneReviewsName7|}}}}}}}

| label48 = [[Orphanet]]
|  data48 = {{#if:{{{Orphanet|}}}{{#property:P1550}}|[http://www.orpha.net/consor/cgi-bin/OC_Exp.php?lng=en&Expert={{#invoke:Wikidata|getValue|P1550|{{{Orphanet|FETCH_WIKIDATA}}}}} {{#invoke:Wikidata|getValue|P1550|{{{Orphanet|FETCH_WIKIDATA}}}}}]  {{{Orphanet_mult|}}} }}

| label59 = 備註
|  data59 = {{{Notes|}}}

| header70      = {{{module|}}}

}}<!-- end of infobox

-->{{main other|1=<!--
-->{{#if:{{#ifeq:{{#invoke:Wikidata|pageId}}||DO_CAT}}{{#if:{{{QID|}}}|DO_CAT}}|[[Category:缺少维基数据的医学条目]]}}
}}<!--

-->{{#invoke:Check for unknown parameters|check|unknown={{main other|[[Category:使用醫學模板含有未知參數的頁面|_VALUE_{{PAGENAME}}]]}}|preview=页面使用的[[Template:Infobox medical condition]]含有未知参数 "_VALUE_" |ignoreblank= y
| Alt | alt | Alt-cn | alt-cn | Alt-hans | alt-hans | Alt-hant | alt-hant | Alt-hk | alt-hk | Alt-mo | alt-mo | Alt-my | alt-my | Alt-sg | alt-sg | Alt-tw | alt-tw | Caption | caption | cause | causes | complications | deaths | diagnosis | diff | differential | differential diagnosis | DiseasesDB | DiseasesDB_mult | duration | eMedicineSubj | eMedicineTopic | eMedicine_mult | Field | field | frequency | GeneReviewsID | GeneReviewsName | GeneReviewsName1 | GeneReviewsName2 | GeneReviewsName3 | GeneReviewsName4 | GeneReviewsName5 | GeneReviewsName6 | GeneReviewsName7 | GeneReviewsNBK | GeneReviewsNBK1 | GeneReviewsNBK2 | GeneReviewsNBK3 | GeneReviewsNBK4 | GeneReviewsNBK5 | GeneReviewsNBK6 | GeneReviewsNBK7 | ICD10 | ICD9 | ICDO | Image | image | Image-cn | image-cn | image-hans | Image-hans | Image-hant | image-hant | Image-hk | image-hk | Image-mo | image-mo | Image-my | image-my | Image-sg | image-sg | Image-tw | image-tw | image_size | Management | management | medication | MedlinePlus | MedlinePlus_mult | MeSH | MeSH1 | MeSH2 | MeSH3 | MeSH4 | MeSH5 | MeSH6 | MeSH7 | MeSH8 | MeSH9 | MeshID | MeshName | MeshNumber | MeshYear | MeshYear1 | MeshYear2 | MeshYear3 | MeshYear4 | MeshYear5 | MeshYear6 | MeshYear7 | MeshYear8 | MeshYear9 | module | Name | name | Notes | OMIM | OMIM_mult | onset | Orphanet | Orphanet_mult | prevention | prognosis | Pronounce | pronounce | pronounce 2 | pronounce comment | pronounce ref | Pronunciation | pronunciation | QID | risk | risks | Speciality | speciality | Specialty | specialty | symptoms | Synonym | synonym | Synonyms | synonyms | treatment | types | Width | width }}<!--

-->{{#ifexpr:({{#invoke:math|max|0
|{{#invoke:ParameterCount|main|pattern1=^[Nn]ame$|checkblanks=no}}
|{{#invoke:ParameterCount|main|pattern1=^[Cc]aption$|checkblanks=no}}
|{{#invoke:ParameterCount|main|pattern1=^[Ww]idth$|checkblanks=no}}
|{{#invoke:ParameterCount|main|pattern1=^[Aa]lt$|checkblanks=no}}
|{{#invoke:ParameterCount|main|pattern1=^[Ii]mage$|checkblanks=no}}
|{{#invoke:ParameterCount|main|pattern1=^[Pp]ronounce$|pattern2=^[Pp]ronunciation$|checkblanks=no}}
|{{#invoke:ParameterCount|main|pattern1=^[Ss]peciality$|pattern2=^[Ss]pecialty$|pattern3=[Ff]ield$|checkblanks=no}} }})>1|{{main other|1=[[Category:使用醫學模板含有多種參數的頁面]]|2=[[:使用醫學模板含有多種參數的頁面]]}}}}<!--

--><noinclude>{{documentation}}</noinclude>