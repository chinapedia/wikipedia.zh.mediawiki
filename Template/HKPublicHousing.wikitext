<noinclude>{{Wraps infobox|Infobox building}}{{esoteric}}</noinclude>{{Infobox building
| building_name       = {{{title|{{{housename|{{PAGENAME}}}}}}}}
| image               = {{{photo|}}}
| image_size          = {{{photosize|}}}
| caption             = {{{phototitle|}}}
| client             = {{ #ifeq: {{{authority|HKHS}}} |HKHS| [[File:Hkhousingsociety-logo-2008.svg|25px]] [[香港房屋協會]] | 
{{#ifeq: {{{authority|}}} |香港平民屋宇有限公司| [[香港平民屋宇有限公司]] | [[File:Logo of Hong Kong Housing Authority.svg|25px]] [[香港房屋委員會]] }}}}
| building_type      = {{#if: {{{type|}}} |
    {{ #ifeq: {{{authority|}}} | HKHS |
      {{ #switch: {{{type}}}
        | 1 = 資助房屋：出租單位[[Category:香港房屋協會－租住屋邨]]
        | 2 = 郊區公共房屋[[Category:香港房屋協會－租住屋邨]]
        | 3 = 資助房屋：出租單位（包括郊區公共房屋）、住宅發售計劃[[Category:香港房屋協會－租住屋邨]][[Category:住宅發售計劃屋苑]]
        | 3A = 資助房屋：住宅發售計劃[[Category:住宅發售計劃屋苑]]
        | 4 = [[夾心階層住屋計劃]][[Category:香港夾屋屋苑]]
        | 5 = 資助出售房屋項目[[Category:資助出售房屋項目屋苑]]
        | #default = {{{type}}}
      }}
    |
      {{ #switch: {{{type}}}
        | 1 = 租住屋邨[[Category:香港房屋委員會－租住屋邨]]
        | 2 = [[租者置其屋計劃]][[Category:租者置其屋計劃屋邨]]
        | 3 = [[居者有其屋計劃]]
        | 4 = 私人機構參建居屋計劃[[Category:私人參建居屋]]
        | 5 = [[綠表置居計劃]]
        | #default = {{{type}}}
      }}
    }}
  | 不詳}}
| location_name       = 地区
| location_city       = {{#if:{{{disassembly|}}}|[[香港]]|{{#if:{{{district|}}}|{{HKG}}}}}}{{#if:{{{district|}}}|
     {{ #switch: {{{district}}}
        | 北區 = [[北區 (香港)|北區]]
        | 中西區 = [[中西區 (香港)|中西區]]
        | 南區 = [[南區 (香港)|南區]]
        | 東區 = [[東區 (香港)|東區]]
        | #default = [[{{{district}}}]]
     }}
|不詳}}
| address            = {{{address|}}}
| coordinates        = {{{coordinates|{{{coordinate|}}}}}}
| nrhp2             ={{#if:{{{year|}}}|</td></tr><tr><th scope="row">入-{伙}-年份</th><td>{{{year|}}}}}{{#if: {{{disassembly|}}}|</td></tr><tr><th scope="row">拆卸年份</th><td>{{{disassembly|}}}}}
| blocknumber       = {{{blocknumber|}}}
| flatnumber         = {{{rentalflats|}}}{{#if: {{{flatsize|}}}|</td></tr><tr><th scope="row">-{zh-cn:单套面积; zh-hk:單位面積;}-</th><td>{{{flatsize|}}} -{zh-cn:平方英尺; zh-hk:呎;}-（ft²）}}
| number_of_residents = {{{household|}}}{{#if:{{{auth|}}}|</td></tr><tr><th scope="row">認可人口</th><td>{{{auth|}}}}}
| website         = {{{website|}}}
}}<noinclude>
{{esoteric}}
{{template doc}}
<!-- Add cats and interwikis to the /doc subpage, not here! -->
</noinclude>