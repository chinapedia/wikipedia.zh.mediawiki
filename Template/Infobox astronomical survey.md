{{Infobox
|   title = {{{name|{{#if:{{#invoke:Wikidata|ViewSomething|labels|zh|value}}|{{#invoke:Wikidata|ViewSomething|labels|zh|value}}|{{PAGENAMEBASE}} }} }}}
|   image = {{#invoke:InfoboxImage|InfoboxImage|image={{#invoke:Wikidata|getValue|P18|{{{image|FETCH_WIKIDATA}}} }}|size={{{image_size|}}}|sizedefault=frameless|alt={{{alt|}}}}}
| caption = {{{caption|{{#invoke:Wikidata|getImageLegend|FETCH_WIKIDATA}}}}}
| labelsyle = white-space: nowrap;
|  label1 = 其他名称
|   data1 = {{{alt_names|{{#if:{{#invoke:Wikidata|ViewSomething|aliases|zh|1|value}}|{{#invoke:Wikidata|ViewSomething|aliases|zh|1|value}}|}}}}}
|  label2 = 类型
|   data2 = {{#invoke:WikidataIB|getValue|P31|name=type|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{type|}}} }}
|  label3 = 目标
|   data3 = {{#invoke:WikidataIB|getValue|P921|name=target|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{target|}}}}}
|  label4 = 组织
|   data4 = {{#invoke:WikidataIB|getValue|P137|name=organisation|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{organization|{{{organisation|}}}}}}}}
|  label5 = [[经纬度|-{zh-hans:坐标; zh-hant:座標;}-]]
|   data5 = {{#if:{{{coords|}}}{{{coordinates|}}} |  {{ifempty|{{{coordinates|}}}|{{{coords|}}}}} | {{#if:{{#Property:P625}} | {{If first display both|{{Coord|display=inline,title|format=dms}}|{{#ifeq:{{{refs|no}}}|yes|{{wikidata|references|normal+|P625}} }}{{EditAtWikidata|pid=P625}} }} }} }}
|  label6 = 得名
|   data6 = {{#invoke:WikidataIB|getValue|P138|name=namedafter|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{namedafter|}}} }}
|  label7 = [[天文台编号列表|天文台编号]]
|   data7 = {{{code|{{#if:{{#invoke:Wikidata|getValue|P717|FETCH_WIKIDATA}}|[[天文台编号列表#{{#invoke:Wikidata|getValue|P717|FETCH_WIKIDATA}}|{{#invoke:Wikidata|getValue|P717|FETCH_WIKIDATA}}]]}}}}}
|  label8 = 开始
|   data8 = {{#invoke:WikidataIB|getValue|P580|name=started|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{started|}}} }}
|  label9 = 结束
|   data9 = {{#invoke:WikidataIB|getValue|P582|name=ended|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{ended|}}} }}
| label10 = 发布
|  data10 = {{#invoke:WikidataIB|getValue|P577|name=published|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{published|}}} }}
| label11 = 观测
|  data11 = {{#invoke:WikidataIB|getValue|P121|name=observations|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{observations|}}}}}
| label12 = [[波长]]
|  data12 = {{#invoke:WikidataIB|getValue|P2808|name=wavelength|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{wavelength|}}}}}
| label13 = [[频率]]
|  data13 = {{#invoke:WikidataIB|getValue|P2144|name=frequency|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{frequency|}}}}}
| label14 = Band
|  data14 = {{#invoke:WikidataIB|getValue|P1227|name=band|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{band|}}}}}
| label15 = 数据产品
|  data15 = {{#invoke:WikidataIB|getValue|P1056|name=products|suppressfields={{{suppressfields|}}}|fetchwikidata={{{fetchwikidata|ALL}}}|onlysourced={{{onlysourced|no}}}|{{{products|}}}}}
| label16 = 网站
|  data16 = {{{website|{{#if:{{#property:P856}}|{{Url|1={{#invoke:Wikidata|getValue|P856|FETCH_WIKIDATA}} }} }} }}}
|  data20 = {{{embedded|}}}
|  data30 = {{#if:{{#invoke:Wikidata|getValue|P373|{{{commons|FETCH_WIKIDATA}}} }} | {{icon|Commons}} [[Commons:{{#if:{{{commons|}}} | {{{commons}}} | Category:{{#invoke:Wikidata|getValue|P373|FETCH_WIKIDATA}} }} |维基共享资源相关媒体]]}}
| below     = {{EditOnWikidata}}
}}<includeonly>{{main other|{{#if:{{safesubst:#invoke:Check for unknown parameters|check|unknown=1|preview=1}}|[[Category:Articles using Infobox astronomical survey using locally defined parameters]]|}}}}</includeonly><noinclude>
{{documentation}}
<!---Please add metadata to the /doc page, not here - thanks!--->
</noinclude>