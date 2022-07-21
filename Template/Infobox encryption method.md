{{ infobox
| title      = {{{name|<includeonly>{{PAGENAME}}</includeonly>}}}
| image     = {{#invoke:InfoboxImage|InfoboxImage|image={{{image|}}}|size={{{image size|{{{image_size|{{{imagesize|}}}}}}}}}|alt={{{alt|}}}}}
| caption    = {{{caption|}}}

| header1    = {{#if:{{{designers|}}}{{{publish date|}}}{{{series|}}}{{{derived from|}}}{{{derived to|}}}{{{related to|}}}{{{certification|}}}|概述}}
| label2     = {{nowrap|设计者}}
| data2      = {{{designers|}}}
| label3     = {{nowrap|首次发布}}
| data3      = {{{publish date|}}}
| label4     = 系列
| data4      = {{{series|}}}
| label5     = 衍生自
| data5      = {{{derived from|}}}
| label6     = 继承算法
| data6      = {{{derived to|}}}
| label7     = 相关算法
| data7      = {{{related to|}}}
| label8     = 认证
| data8      = {{{certification|}}}

| header9    = {{#if:{{{digest size|}}}{{{key size|}}}{{{security claim|}}}{{{block size|}}}{{{state size|}}}{{{structure|}}}{{{rounds|}}}|{{#if:{{{key size|}}}{{{block size|}}}|密码细节|细节}} }}
| label10    = [[密碼雜湊函數|摘要长度]]
| data10     = {{{digest size|}}}
| label11    = [[密钥]]长度
| data11     = {{{key size|}}}
| label12    = 安全声明
| data12     = {{{security claim|}}}
| label13    = [[块大小|分组长度]]
| data13     = {{{block size|}}}
| label14    = 状态长度
| data14     = {{{state size|}}}
| label15    = 结构
| data15     = {{{structure|}}}
| label16    = 重复回数
| data16     = {{{rounds|}}}
| label17    = 速度
| data17     = {{{speed|}}}

| header18   = {{#if:{{{cryptanalysis|}}}|最佳公开[[密码分析|破解]]}}
| below      = {{{cryptanalysis|}}}
| belowstyle = line-height: 1.25em; text-align: left
}}<includeonly>{{#ifeq:{{NAMESPACE}}|{{ns:0}}| {{#if:{{{digest size|}}}|[[Category:密码散列函数]]|{{#if:{{{block size|}}}|[[Category:分组密码]]|{{#if:{{{state size|}}}|[[Category:流密码]]}} }} }} }}</includeonly><noinclude>{{documentation}}<!-- Please add metadata to the <includeonly> section on the /doc subpage - thanks! -->
</noinclude>