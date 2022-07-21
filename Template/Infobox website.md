{{Infobox
| bodyclass  = vcard
| bodystyle = {{#if:{{{infoboxwidth|{{{width|}}}}}} |width:{{{infoboxwidth|{{{width}}}}}} }}
| child = {{lc:{{{embed|}}}}}
| decat = yes

| titleclass = fn org
| title      = {{if empty|{{{name|}}}|{{{company_name|}}}|{{{websitename|}}}|<includeonly>{{PAGENAMEBASE}}</includeonly>}}{{#if: {{both |{{{native_name|}}} | {{{native_name_lang|}}} }} | <br/>{{lang|{{{native_name_lang}}}|{{{native_name}}}}} }}

| image    = {{#invoke:InfoboxImage|InfoboxImage|image={{if empty|{{{company_logo|}}}|{{{logo|}}}|{{{websitelogo|}}}}}|size={{{logo_size|}}}|sizedefault=frameless|upright={{{image_upright|1}}}|alt={{{logo_alt|}}}}}
| caption1 = {{if empty|{{{logo_caption|}}}|{{{logocaption|}}}}}
| image2   = {{#if:{{{collapsible|}}}|{{hidden begin|title={{{collapsetext|截图}}}|titlestyle=background:{{{background|gainsboro}}};text-align:center|contentstyle=text-align:center}}}}
{{#invoke:InfoboxImage|InfoboxImage|image={{{screenshot|}}}|size={{{screenshot_size|}}}|sizedefault=300px|alt={{{screenshot_alt|}}}}}
| caption2 = {{{caption|}}}{{#if:{{{collapsible|}}}|{{hidden end}}}}

| labelstyle = white-space:nowrap;

| label1   = 公司类型
| class1   = category
| data1    = {{{company_type|}}}

| label2   = {{longitem|网站类型}}
| data2    = {{if empty|{{{website_type|}}}|{{{type|}}}}}

| label3   = 语言
| data3    = {{#if:{{{language_count|}}}
  |{{{language_count}}}种语言
  |{{{language|}}}
  }}{{{language_footnote|}}}
| data4    = {{#if:{{both| {{{language_count|}}} | {{{language|}}}}}
  |{{Begin hidden|titlestyle=background:transparent;|title=语言列表}}{{{language|}}}{{End hidden}}
  }}

| label5   = [[股票代號]]
| data5    = {{{traded_as|}}}

| label6   = 成立
| data6    = {{if empty|{{{founded|}}}|{{{foundation|}}}}}

| label7   = 結束
| data7    = {{{dissolved|}}}

| label8   = 前身
| data8    = {{{predecessor|}}}

| label9   = 後繼
| data9    = {{{successor|}}}

| label10  = 總部
| class10  = {{#if:{{{headquarters|}}}{{{location|}}}|label|adr}}
| data10   = {{comma separated entries
     | 1= {{if empty|{{{headquarters|}}}|{{{location|}}}}}
     | 2= {{#if:{{{location_city|}}}|<div style="display:inline;" class="locality">{{{location_city}}}</div>}}
     | 3= {{#if:{{{country|}}}{{{location_country|}}}|<div style="display:inline;" class="country-name">{{if empty|{{{country|}}}|{{{location_country}}}}}</div>}}
     }}

| label11  = 原产地
| data11   = {{{country_of_origin|}}}

| label12  = 營業據點數
| data12   = {{{locations|}}}

| label13  = 業務範圍
| data13   = {{{area_served|}}}

| label14  = 持有者
| data14   = {{if empty|{{{owners|}}}|{{{owner|}}}}}

| label15  = 创始人
| data15   = {{if empty|{{{author|}}}|{{{creator|}}}|{{{authors|}}}|{{{creators|}}}}}

| label16  = 创立者
| data16   = {{{founder|}}}

| label17  = 編輯
| data17   = {{if empty|{{{editors|}}}|{{{editor|}}}}}

| label18  = 首席
| data18   = {{{chairman|}}}

| label19  = [[董事長]]
| data19   = {{{chairperson|}}}

| label20  = [[总裁]]
| data20   = {{{president|}}}

| label21  = [[首席执行官]]
| data21   = {{{CEO|}}}

| label22  = [[执行董事|常務董事]]
| data22   = {{{MD|}}}

| label23  = [[总经理]]
| data23   = {{{GM|}}}

| label24  = 代表人物
| data24   = {{{key_people|}}}

| label25  = 产业
| class25  = category
| data25   = {{{industry|}}}

| label26  = [[产品]]
| data26   = {{{products|}}}

| label27  = [[服务]]
| data27   = {{{services|}}}

| label28  = [[营业额]]
| data28   = {{if empty|{{{revenue|}}}|{{{rev|}}}}}

| label29  = [[息稅前利潤|-{zh-hk:經營收入;zh-cn:息税前利润;zh-tw:稅前盈餘;}-]]
| data29   = {{{operating_income|}}}

| label30  = {{tsl|en|net income|淨收入|-{zh-hk:淨收入;zh-cn:净利润;zh-tw:稅後盈餘;}-}}
| data30   = {{{net_income|}}}

| label31  = [[資產|总资产]]
| data31   = {{{assets|}}}

| label32  = [[股东权益|总股本]]
| data32   = {{{equity|}}}

| label33  = 员工
| data33   = {{if empty|{{{employees|}}}|{{{num_employees|}}}}}

| label34  = [[控股公司|母公司]]
| data34   = {{{parent|}}}

| label35  = 部门
| data35   = {{{divisions|}}}

| label36  = 子公司
| data36   = {{if empty|{{{subsidiaries|}}}|{{{subsid|}}}}}

| label37  = 网址
| class37  = url
| data37   = {{#if:{{if empty|{{{website|}}}|{{{url|}}}|{{{homepage|}}}}}{{#ifeq:{{{qid|}}}|none|-}}
 | {{#ifeq:{{if empty|{{{website|}}}|{{{url|}}}|{{{homepage|}}}}} | hide | | {{if empty|{{{website|}}}|{{{url|}}}|{{{homepage|}}}}} }}
 | {{#if:{{wikidata|property|raw|{{{qid|}}}|P856}}
 | {{#invoke:WikidataIB |url2 |url={{Wdib|P856|rank=best|qid={{{qid|}}}|fwd=ALL|osd=no}}
 }}
 }}
 }}

| label38  = [[IPv6]]支持
| data38   = {{{ipv6|}}}

| label39  = [[网络广告|广告]]
| data39   = {{{advertising|}}}

| label40  = 商业性质
| data40   = {{{commercial|}}}

| label41  = 注册
| data41   = {{if empty|{{{registration|}}}|{{{reg|}}}}}

| label42  = 用户
| data42   = {{if empty|{{{users|}}}|{{{num_users|}}}}}

| label43  = 推出时间
| data43   = {{if empty|{{{launched|}}}|{{{launch_date|}}}|{{{date_of_launch|}}}}}

| label44  = 现状
| class44  = category
| data44   = {{{current_status|}}}

| label45  = [[系统平台]]
| data45   = {{{native_clients|}}}
<!-- Spelled differently; see [[MOS:ENGVAR]] -->
| label46  = {{#if:{{{content_license|}}}{{{license|}}}|{{longitem|內容許可}}}}
| data46   = {{if empty|{{{content_license|}}}|{{{license|}}}|{{{content_licence|}}}|{{{licence|}}}}}

| label47  = 編程語言
| data47   = {{{programming_language|}}}

| label48  = [[國際標準期刊號|ISSN]]
| data48   = {{ISSN link|1={{if empty|{{{issn|}}}|{{{ISSN|}}}}}|2={{if empty|{{{eissn|}}}|{{{eISSN|}}}}}}}

| label49  = [[OCLC]]号
| data49   = {{#if:{{{oclc|}}}|{{OCLC search link|{{{oclc}}} }} }}

| below    = {{{footnotes|}}}
}}{{#invoke:Check for unknown parameters|check|unknown=[[Category:{{main other|使用未知Infobox website参数的页面|使用未知Infobox website参数的非页面}}|_VALUE_{{PAGENAME}}]]|preview=页面使用了 [[Template:Infobox website]] 不存在的参数"_VALUE_"|ignoreblank=y| advertising | alexa | area_served | assets | author | authors | background | caption | CEO | chairman | chairperson | collapsetext | collapsible | commercial | company_logo | company_name | company_type | content_licence | content_license | country | country_of_origin | creator | creators | current_status | date_of_launch | dissolved | divisions | editor | editors | embed | employees | equity | footnotes | foundation | founded | founder | GM | headquarters | homepage | industry | infoboxwidth | international | intl | ipv6 | issn | ISSN | eissn | eISSN | key_people | language | language_count | language_footnote | launch_date | launched | licence | license | location | location_city | location_country | locations | logo | logo_alt | logo_caption | logo_size | logocaption | MD | name | native_name | native_name_lang | native_clients | net_income | num_employees | num_users | oclc | operating_income | owner | owners | parent | predecessor | president | products | programming_language | reg | registration | rev | revenue | screenshot | screenshot_alt | screenshot_size | services | subsid | subsidiaries | successor | traded_as | type | url | users | website | website_type | websitelogo | websitename |width
}}{{#invoke:check for clobbered parameters|check
| template = Infobox website
| cat = {{main other|Category:使用冗余Infobox website参数的页面}}
| name; company_name; websitename
| company_logo; logo; websitelogo
| logo_caption; logocaption
| website_type; type
| founded; foundation
| headquarters; location
| country; location_country
| owners; owner
| author; creator; authors; creators; founder
| editors; editor
| revenue; rev
| international; intl
| employees; num_employees
| subsidiaries; subsid
| url; website; homepage
| registration; reg
| users; num_users
| launched; launch_date; date_of_launch
| content_license; license; content_licence; licence
| issn; ISSN
| eissn; eISSN
| infoboxwidth; width
}}{{#if: {{{native_name|}}}{{{native_name_lang|}}}
   | {{#if: {{both |{{{native_name|}}} | {{{native_name_lang|}}} }}
      |
      |{{main other|[[Category:在网站信息框没有并用native_name和native_name_lang的页面]]}}
   }}
   | <!-- both native_name and native_name_lang are empty/omitted -->
}}<noinclude>
{{documentation}}
</noinclude>