{{Infobox
| bodyclass = vcard

| titleclass = fn org
| title = {{{组织名稱|{{{name|{{{organization_name|{{{Non-profit_name|<includeonly>{{PAGENAMEBASE}}</includeonly>}}}}}}}}}}}}

| subheader = {{#if:{{{native_name|{{{native name|}}}}}}|<span class="nickname" {{#if:{{{native_name_lang|}}}|lang="{{{native_name_lang}}}"}}>{{{native_name|{{{native name}}}}}}</span>}}

| image = {{#invoke:InfoboxImage|InfoboxImage |image={{{image|}}} |size={{{image_size|{{{imagesize|{{{size|}}}}}}}}} |sizedefault=frameless |alt={{{image_alt|{{{alt|}}}}}} }}
| caption = {{{caption|}}}

| image2 = {{#invoke:InfoboxImage|InfoboxImage |image={{{组织標誌|{{{logo|{{{organization_logo|{{{Non-profit_logo|}}}}}}}}}}}} |size={{{logo_size|}}} |sizedefault=250px |alt={{{logo_alt|}}} }}
| caption2 = {{{logo_caption|}}}

| image3 = {{#invoke:InfoboxImage|InfoboxImage |image={{{map|}}} |size={{{map_size|{{{msize|}}}}}} |sizedefault=250px |alt={{{map_alt|{{{malt|}}}}}} }}
| caption3 = {{{map_caption|{{{mcaption|}}}}}}

| image4 = {{#invoke:InfoboxImage|InfoboxImage |image={{{map2|}}} |size={{{map2_size|}}} |sizedefault=250px |alt={{{map2_alt|}}} }}
| caption4 = {{{map2_caption|}}}`

| labelstyle = padding-right:0.6em; width:75px;<!--(to ensure some gap between any (long/unwrapped) labels and subsequent data on same line)-->

| label2  = {{#if:{{{original_name|}}}|原名}}
|  data2  = {{#if:{{{original_name|}}}|<span style="font-weight:bold;">{{{original_name|}}}</span>}}

| label3  = 簡稱
| class3  = nickname
|  data3  = {{{abbreviation|}}}

| label4  = 紀念
|  data4  = {{{named_after|}}}

| label5  = 標語
| class5  = note
|  data5  = {{{motto|{{{organization_motto|{{{pledge|}}}}}}}}}

| label6  = 前身
|  data6  = {{{predecessor|}}}

| label7  = 併入
|  data7  = {{{merged|}}}

| label8  = 繼任
|  data8  = {{{successor|}}}

| label9  = {{#if:{{{成立年份|{{{formation|}}}}}} |{{nowrap|成立時間}}|{{#if:{{{founded_date|{{{founded|}}}}}}|{{nowrap|成立時間}}}} }}
| class9  = note
|  data9  = {{if empty |{{{成立年份|{{{formation|}}}}}} |{{{established|}}} |{{{founded_date|{{{founded|}}}}}} }}

| label10  = 創始人
|  data10  = {{#if:{{{founders|}}} |{{{founders}}} |{{{founder|}}} }}

| label11  = 創始地
|  data11  = {{{founding_location|}}}

| label12  = {{#if:{{{extinction|}}} |廢除 | 解散}}
|  data12  = {{#if:{{{extinction|}}} |{{{extinction}}} |{{{dissolved|}}} }}

| label13  = 合併自
|  data13  = {{{merger|}}}

| label14 = 類型
|  data14 = {{{组织性质|{{{type|{{{organization_type|{{{Non-profit_type|}}}}}}}}}}}}

| label15 = {{longitem |{{#if:{{{vat_id|}}} |[[VAT identification number|VAT ID no.]] |{{en-link|納稅人識別號碼|Taxpayer Identification Number|Tax ID no.}}}} }}
|  data15 = {{#if:{{{vat_id|}}} |{{{vat_id}}} |{{{tax_id|}}} }}

| label16 = 注冊號
|  data16 = {{{registration_id|}}}

| label17 = 法律地位
|  data17 = {{{status|}}}

| label18 = 目標
|  data18 = {{#if:{{{focus|}}} |{{{focus}}} |{{{purpose|}}} }}

| label19 = {{longitem|專業頭銜}}
|  data19 = {{{professional_title|}}}

| label20 = 總部
|  data20 = {{{总部地址|{{{headquarters|}}}}}}

| label21 = 地點
| class21 = label
|  data21 = {{Unbulleted list
             | 1 = {{comma separated entries
                    | 1 = {{#if:{{{location_city|}}}    |<span class="locality">{{{location_city}}}</span>}}
                    | 2 = {{#if:{{{location_country|}}} |<span class="country-name">{{{location_country}}}</span>}}
                   }}
             | 2 = {{{location|}}}
             | 3 = {{comma separated entries
                    | 1 = {{#if:{{{location_city2|}}}    |<span class="locality">{{{location_city2}}}</span>}}
                    | 2 = {{#if:{{{location_country2|}}} |<span class="country-name">{{{location_country2}}}</span>}}
                   }}
             | 4 = {{{location2|}}}
            }}

| label22 = 地點
| class22 = label
|  data22 = {{Unbulleted list
             | 1 = {{comma separated entries
                    | 1 = {{#if:{{{addnl_location_city|}}}    |<span class="locality">{{{addnl_location_city}}}</span>}}
                    | 2 = {{#if:{{{addnl_location_country|}}} |<span class="country-name">{{{addnl_location_country}}}</span>}}
                   }}
             | 2 = {{{addnl_location|{{{additional_location|}}}}}}
             | 3 = {{comma separated entries
                    | 1 = {{#if:{{{addnl_location_city2|}}}    |<span class="locality">{{{addnl_location_city2}}}</span>}}
                    | 2 = {{#if:{{{addnl_location_country2|}}} |<span class="country-name">{{{addnl_location_country2}}}</span>}}
                   }}
             | 4 = {{{addnl_location2|{{{additional_location2|}}}}}}
            }}

| label23 = 坐標
|  data23 = {{{coordinates|{{{coords|}}}}}}

| label24 = 起源
|  data24 = {{{origins|}}}

| label25 = {{longitem |{{#if:{{{area_served|}}} |服務地區 |{{#if:{{{region_served|}}}|服務地區}} }} }}
|  data25 = {{if empty |{{{area_served|}}} |{{{region_served|}}} |{{{region|}}} }}

| label26 = 產品{{#if:{{{products|}}}}}
|  data26 = {{#if:{{{products|}}} |{{{products}}} |{{{product|}}} }}

| label27 = 服務
| class27 = note
|  data27 = {{{services|}}}

| label28 = 方法{{#if:{{{methods|}}}}}
|  data28 = {{#if:{{{methods|}}} |{{{methods}}} |{{{method|}}} }}

| label29 = 領域{{#if:{{{fields|}}}}}
|  data29 = {{#if:{{{fields|}}} |{{{fields}}} |{{{field|}}} }}

| label30 = {{longitem |會員{{#if:{{{会员人数|{{{num_members|{{{members|}}}}}}}}}}} {{#if:{{{num_members_year|{{{membership_year|}}}}}} |{{nobold|（{{{num_members_year|{{{membership_year|}}}}}}）}} }} }}
|  data30 = {{#if:{{{会员人数|{{{num_members|{{{members|}}}}}}}}} |{{{会员人数|{{{num_members|{{{members}}}}}}}}} |{{{membership|}}} }}

| label31 = {{longitem |官方語言}}
|  data31 = {{#if:{{{languages|}}} |{{{languages}}} |{{{language|}}} }}

| label32 = 所有者{{#if:{{{owners|}}}}}
|  data32 = {{#if:{{{owners|}}} |{{{owners}}} |{{{owner|}}} }}

| label33 = {{longitem|秘書長}}
|  data33 = {{#if:{{{general|}}} |{{{general}}} |{{{sec_gen|}}} }}

| label34 = {{#if:{{{领导职务|{{{leader_title|}}}}}}|{{longitem|{{{领导职务|{{{leader_title}}}}}}}}|領導人}}
|  data34 = {{{现任领导|{{{leader_name|}}}}}}

| label35 = {{longitem|{{{leader_title2}}}}}
|  data35 = {{#if:{{{leader_title2|}}} |{{{leader_name2|}}} }}

| label36 = {{longitem|{{{leader_title3}}}}}
|  data36 = {{#if:{{{leader_title3|}}} |{{{leader_name3|}}} }}

| label37 = {{longitem|{{{leader_title4}}}}}
|  data37 = {{#if:{{{leader_title4|}}} |{{{leader_name4|}}} }}

| label38 = {{longitem|[[董事會]]}}
|  data38 = {{{board_of_directors|}}}

| label39 = {{longitem|重要人物}}
|  data39 = {{{key_people|}}}

| label40 = {{#if:{{{main_organ|}}} |{{longitem|机关刊物}} |出版物}}
|  data40 = {{#if:{{{main_organ|}}} |{{{main_organ}}} |{{{publication|}}} }}

| label41 = {{longitem|上級組織{{#if:{{{parent_organisation|}}}}}}}
|  data41 = {{#if:{{{parent_organisation|}}} |{{{parent_organisation}}} |{{{parent_organization|}}} }}

| label42 = 分支機構
|  data42 = {{#if:{{{subsidiaries|}}} |{{{subsidiaries}}} |{{{subsid|}}} }}

| label43 = 脫離
|  data43 = {{{secessions|}}}

| label44 = 隸屬
|  data44 = {{{affiliations|}}}

| label45 = {{longitem |預算{{#if:{{{budget_year|}}} |{{nobold|（{{{budget_year}}}）}} }} }}
|  data45 = {{{budget|}}}

| label46 = {{longitem |收入{{#if:{{{revenue_year|{{{income_year|}}}}}} |{{nobold|（{{{revenue_year|{{{income_year|}}}}}}）}} }} }}
|  data46 = {{{revenue|{{{income|}}}}}}

| label47 = 支出
|  data47 = {{{disbursed|{{{disbursements|{{{disbursement|}}}}}}}}}

| label48 = 支出{{#if:{{{expenses_year|}}} | {{nobold|（{{{expenses_year}}}）}} }}
|  data48 = {{{expenses|{{{spent|{{{expense|}}}}}}}}}

| label49 = 捐款
|  data49 = {{{endowment|}}}

| label50 = {{longitem |员工{{#if:{{{num_staff|}}}{{{staff|}}} }}<br> {{#if:{{{num_staff_year|{{{staff_year|{{{num_employees_year|{{{employees_year|}}}}}}}}}}}} |{{nobold|({{{num_staff_year|{{{staff_year|{{{num_employees_year|{{{employees_year|}}}}}}}}}}}})}} }} }}
|  data50 = {{if empty |{{{num_staff|}}} |{{{staff|}}} |{{{num_employees|}}} |{{{employees|}}} }}

| label51 = {{longitem |志願者{{#if:{{{num_volunteers_year|{{{volunteers_year|}}}}}} |{{nobold|（{{{num_volunteers_year|{{{volunteers_year|}}}}}}）}} }} }}
|  data51 = {{#if:{{{num_volunteers|}}} |{{{num_volunteers}}} |{{{volunteers|}}} }}

| label52 = 口號
|  data52 = {{{slogan|{{{Non-profit_slogan|{{{non-profit_slogan|}}}}}}}}}

| label53 = 使命聲明
|  data53 = {{{mission|}}}

| label54 = 獎項
|  data54 = {{{awards|}}}

| label55 = 網站
|  data55 = {{{组织网站|{{{website|{{{homepage|}}}}}}}}}

| label56 = 備註
|  data56 = {{{remarks|}}}

| label57 = {{longitem|原稱}}
| class57 = nickname
|  data57 = {{if empty |{{{former name|}}} |{{{former_name|}}} |{{{former|}}} |{{{formerly|}}} }}

| belowstyle = border-top:#aaa 1px solid;
| below = {{{footnotes|}}}

}}<noinclude>
{{Documentation}}
</noinclude>