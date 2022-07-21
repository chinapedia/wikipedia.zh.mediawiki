{{Infobox
| bodyclass   = vcard
| child       = {{{child}}}
| bodystyle   = width:{{#if:{{{tablewidth|}}}|{{px|{{{tablewidth}}}}}|275px}}; background:{{#if:{{{background|}}}|{{{background}}}|#FAFAFA}};
| abovestyle  = {{#if:{{{color|}}}|background-color: {{{color}}};|background-color: #FFD24A;}} {{#if:{{{fontcolor|}}}|color: {{{fontcolor}}} }}
| above       = {{#ifeq:{{{child|}}}|yes||{{#if:{{{Denomination|{{{面额|{{{面額|}}}}}}}}}|{{{Denomination|{{{面额|{{{面額}}}}}}}}}{{#if:{{{Country|{{{国家|{{{國家|}}}}}}}}}|（{{{Country|{{{国家|{{{國家}}}}}}}}}）}}|{{PAGENAME}}}} }}
| aboveclass  = navbox-title
| headerstyle = {{#if:{{{color|}}}|background-color: {{{color}}};|background-color: #FFE9A6;}} {{#if:{{{fontcolor|}}}|color:{{{fontcolor}}} }}
| labelstyle  = navbox-title

| image       = {{#ifeq:{{{child|}}}|yes||{{#if:{{{Image|{{{图案|{{{圖案|}}}}}}}}}|[[File:{{{Image|{{{图案|{{{圖案}}}}}}}}}|{{px|{{{Image Size|{{{Image size|150px}}}}}}|frameless}}|alt={{{alt|{{{imgalt|}}}}}}]]}}}}
| caption     = {{#if:{{{Image|{{{图案|{{{圖案|}}}}}}}}}|{{{Caption|{{{图说|{{{圖說|}}}}}}}}} }}

| label2     = {{nowrap|價值}}
|  data2     = {{{Value|{{{价值|{{{價值|}}}}}}}}} {{{Unit|{{{单位|{{{單位|}}}}}}}}}
| label3     = 直徑
|  data3     = {{#if:{{{Diameter_special|}}} | {{{Diameter_special}}} | {{#if:{{{Diameter|{{{直径|{{{直徑|}}}}}}}}}|{{convert|{{{Diameter|{{{直径|{{{直徑|}}}}}}}}}|mm|in}} }} }}
| label4     = 長度
|  data4     = {{#if:{{{Height|{{{长度|{{{長度|}}}}}}}}}|{{convert|{{{Height|{{{长度|{{{長度|}}}}}}}}}|mm|in}} }}
| label5     = 闊度
|  data5     = {{#if:{{{Width|{{{阔度|{{{闊度|}}}}}}}}}|{{convert|{{{Width|{{{阔度|{{{闊度|}}}}}}}}}|mm|in}} }}
| label6     = 厚度
|  data6     = {{#if:{{{Thickness|{{{厚度|}}}}}}|{{convert|{{{Thickness|{{{厚度|}}}}}}|mm|in}} }}
| label7     = 重量
|  data7     = {{#if:{{{Mass_special|}}}|{{{Mass_special}}}|{{#if:{{{Mass|{{{Weight|{{{重量|}}}}}}}}}|{{convert|{{{Mass|{{{Weight|{{{重量|}}}}}}}}}|g|ozt}} }} }}

| label8     = 邊緣
|  data8     = {{{Edge|{{{边缘|{{{邊緣|}}}}}}}}}
| label9     = 形狀
|  data9     = {{{Shape|{{{形状|{{{形狀|}}}}}}}}}
| label10    = {{nowrap|中心直徑}}
|  data10    = {{{Center Hole Diameter|{{{中心直径|{{{中心直徑|}}}}}}}}}
| label11    = {{nowrap|硬幣取向}}
|  data11    = {{{Orientation|{{{取向|}}}}}}
| label12    = 成分
|  data12    = {{{Composition|{{{Paper Type|{{{材料|{{{原材料|}}}}}}}}}}}}
| label16    = 含金量
|  data16    = {{#if:{{{Gold_troy_oz|}}}|{{{Gold_troy_oz}}}金衡盎司}}
| label17    = 含銀量
|  data17    = {{#if:{{{Silver_troy_oz|}}}|{{{Silver_troy_oz}}}金衡盎司}}

| label23    = {{nowrap|防偽特徵}}
|  data23    = {{{Security Features|{{{防伪特征|{{{防偽特徵|}}}}}}}}}
| label24    = {{#if:{{{Years of Minting|{{{铸造年份|{{{鑄造年份|{{{Diameter|{{{直径|{{{直徑|}}}}}}}}}}}}}}}}}}|鑄造年份|印製年份}}
|  data24    = {{{Years of Minting|{{{Years of Printing|{{{铸造年份|{{{鑄造年份|{{{年份|}}}}}}}}}}}}}}}
| label25    = {{Nowrap|鑄造標記}}
|  data25    = {{{Mint marks|{{{铸造标记|{{{鑄造標記|}}}}}}}}}
| label26    = {{nowrap|目錄編號}}
|  data26    = {{{Catalog Number|{{{编号|{{{編號|}}}}}}}}}

|header27    = {{#if:{{{Obverse|{{{正面|{{{Obverse1|{{{正面1|}}}}}}}}}}}}{{{Obverse Design|{{{正面图案|{{{正面圖案|{{{Obverse1 Design|{{{正面1图案|{{{正面1圖案|}}}}}}}}}}}}}}}}}}{{{Obverse Caption|{{{正面图说|{{{正面圖說|{{{Obverse1 Caption|{{{正面1图说|{{{正面1圖說|}}}}}}}}}}}}}}}}}} |正面}}
|  data28    = {{Infobox
  | child       = yes
  | image       = {{#if:{{{Image|{{{图案|{{{圖案|}}}}}}}}}||{{#if:{{{Obverse|{{{正面|{{{Obverse1|{{{正面1|}}}}}}}}}}}}|[[File:{{{Obverse|{{{正面|{{{Obverse1|{{{正面1}}}}}}}}}}}}|{{px|{{{obverse image size|{{{Obverse Image Size|{{{obverseimagesize|150px}}}}}}}}}}}|frameless]]}} }}
  | caption     = {{#if:{{{Image|{{{图案|{{{圖案|}}}}}}}}}||{{{Obverse Caption|{{{正面图说|{{{正面圖說|{{{Obverse1 Caption|{{{正面1图说|{{{正面1圖說|}}}}}}}}}}}}}}}}}} }}
  | label1      = 圖案
  |  data1      = {{{Obverse Design|{{{正面图案|{{{正面圖案|{{{Obverse1 Design|{{{正面1图案|{{{正面1圖案|}}}}}}}}}}}}}}}}}}
  | label2      = 設計師
  |  data2      = {{{Obverse Designer|{{{正面设计师|{{{正面設計師|{{{Obverse1 Designer|{{{正面1设计师|{{{正面1設計師|}}}}}}}}}}}}}}}}}}
  | label3      = {{nowrap|設計時間}}
  |  data3      = {{{Obverse Design Date|{{{正面日期|{{{Obverse1 Design Date|{{{正面1日期|{{{正面设计日期|}}}}}}}}}}}}}}}{{#if:{{{Obverse Discontinued|{{{Obverse1 Discontinued|}}}}}}| - {{{Obverse Discontinued|{{{Obverse1 Discontinued}}}}}}}}
  }}

|  data29    = {{Infobox
  | child       = yes
  | image       = {{#if:{{{Obverse2|{{{正面2|}}}}}}|[[File:{{{Obverse2|{{{正面2}}}}}}|{{px|{{{obverse2 image size|{{{Obverse2 Image Size|{{{obverse2imagesize|150px}}}}}}}}}}}|frameless]]}}
  | caption     = {{{Obverse2 Caption|{{{正面2图说|{{{正面2圖說|}}}}}}}}}
  | label1      = 圖案
  |  data1      = {{{Obverse2 Design|{{{正面2图案|{{{正面2圖案|}}}}}}}}}
  | label2      = 設計師
  |  data2      = {{{Obverse2 Designer|{{{正面2设计师|{{{正面2設計師|}}}}}}}}}
  | label3      = {{nowrap|設計時間}}
  |  data3      = {{{Obverse2 Design Date|{{{正面2日期|}}}}}}{{#if:{{{Obverse2 Discontinued|}}}| - {{{Obverse2 Discontinued}}}}}
  }}

|  data30    = {{Infobox
  | child       = yes
  | image       = {{#if:{{{Obverse3|{{{正面3|}}}}}}|[[File:{{{Obverse3|{{{正面3}}}}}}|{{px|{{{obverse3 image size|{{{Obverse3 Image Size|{{{obverse3imagesize|150px}}}}}}}}}}}|frameless]]}}
  | caption     = {{{Obverse3 Caption|{{{正面3图说|{{{正面3圖說|}}}}}}}}}
  | label1      = 圖案
  |  data1      = {{{Obverse3 Design|{{{正面3图案|{{{正面3圖案|}}}}}}}}}
  | label2      = 設計師
  |  data2      = {{{Obverse3 Designer|{{{正面3设计师|{{{正面3設計師|}}}}}}}}}
  | label3      = {{nowrap|設計時間}}
  |  data3      = {{{Obverse3 Design Date|{{{正面3日期|}}}}}}{{#if:{{{Obverse3 Discontinued|}}}| - {{{Obverse3 Discontinued}}}}}
  }}

|header41    = {{#if:{{{Reverse|{{{背面|{{{Reverse1|{{{背面1|}}}}}}}}}}}}{{{Reverse Design|{{{背面图案|{{{背面圖案|{{{Reverse1 Design|{{{背面1图案|{{{背面1圖案|}}}}}}}}}}}}}}}}}}{{{Reverse Caption|{{{背面图说|{{{背面圖說|}}}}}}}}} |背面}}
|  data42    = {{Infobox
  | child       = yes
  | image       = {{#if:{{{Image|{{{图案|{{{圖案|}}}}}}}}}||{{#if:{{{Reverse|{{{背面|{{{Reverse1|{{{背面1|}}}}}}}}}}}}|[[File:{{{Reverse|{{{背面|{{{Reverse1|{{{背面1}}}}}}}}}}}}|{{px|{{{reverse image size|{{{Reverse Image Size|{{{reverseimagesize|150px}}}}}}}}}}}|frameless]]}} }}
  | caption     = {{#if:{{{Image|{{{图案|{{{圖案|}}}}}}}}}||{{{Reverse Caption|{{{背面图说|{{{背面圖說|}}}}}}}}} }}
  | label1      = 圖案
  |  data1      = {{{Reverse Design|{{{背面图案|{{{背面圖案|{{{Reverse1 Design|{{{背面1图案|{{{背面1圖案|}}}}}}}}}}}}}}}}}}
  | label2      = 設計師
  |  data2      = {{{Reverse Designer|{{{背面设计师|{{{背面設計師|{{{Reverse1 Designer|{{{背面1设计师|{{{背面1設計師|}}}}}}}}}}}}}}}}}}
  | label3      = {{nowrap|設計時間}}
  |  data3      = {{{Reverse Design Date|{{{背面日期|{{{Reverse1 Design Date|{{{背面1日期|{{{背面设计日期|}}}}}}}}}}}}}}}{{#if:{{{Reverse Discontinued|{{{Reverse1 Discontinued|}}}}}}| - {{{Reverse Discontinued|{{{Reverse1 Discontinued}}}}}}}}
  }}

|  data43    = {{Infobox
  | child       = yes
  | image       = {{#if:{{{Reverse2|{{{背面2|}}}}}}|[[File:{{{Reverse2|{{{背面2}}}}}}|{{px|{{{reverse2 image size|{{{Reverse2 Image Size|{{{reverse2imagesize|150px}}}}}}}}}}}|frameless]]}}
  | caption     = {{{Reverse2 Caption|{{{背面2图说|{{{背面2圖說|}}}}}}}}}
  | label1      = 圖案
  |  data1      = {{{Reverse2 Design|{{{背面2图案|{{{背面2圖案|}}}}}}}}}
  | label2      = 設計師
  |  data2      = {{{Reverse2 Designer|{{{背面2设计师|{{{背面2設計師|}}}}}}}}}
  | label3      = {{nowrap|設計時間}}
  |  data3      = {{{Reverse2 Design Date|{{{背面2日期|}}}}}}{{#if:{{{Reverse2 Discontinued|}}}| - {{{Reverse2 Discontinued}}}}}
  }}

|  data44   = {{Infobox
  | child       = yes
  | image       = {{#if:{{{Reverse3|{{{背面3|}}}}}}|[[File:{{{Reverse3|{{{背面3}}}}}}|{{px|{{{reverse3 image size|{{{Reverse3 Image Size|{{{reverse3imagesize|150px}}}}}}}}}}}|frameless]]}}
  | caption     = {{{Reverse3 Caption|{{{背面3图说|{{{背面3圖說|}}}}}}}}}
  | label1      = 圖案
  |  data1      = {{{Reverse3 Design|{{{背面3图案|{{{背面3圖案|}}}}}}}}}
  | label2      = 設計師
  |  data2      = {{{Reverse3 Designer|{{{背面3设计师|{{{背面3設計師|}}}}}}}}}
  | label3      = {{nowrap|設計時間}}
  |  data3      = {{{Reverse3 Design Date|{{{背面3日期|}}}}}}{{#if:{{{Reverse3 Discontinued|}}}| - {{{Reverse3 Discontinued}}}}}
  }}

}}<noinclude>
<div style="float: left;">
{{documentation}}
</div>
</noinclude>