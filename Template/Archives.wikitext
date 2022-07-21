<table id="archivebox" role="presentation" class="{{talk other |tmbox tmbox-notice |ombox ombox-notice |demospace={{{demospace|}}}}} mbox-small {{#ifeq:{{{collapsed}}}|yes
 |collapsible collapsed
 |{{#ifeq:{{{collapsible}}}|yes
  |collapsible
 }}
}}" style="text-align: center; {{#if:{{{box-width|}}}|width:{{{box-width}}};}} {{{style|}}}">
<tr><th>{{#switch:{{{image|}}}
 |none        = <!-- no image -->
 |<!--blank-->= [[File:Replacement filing cabinet.svg|{{{image-size|40px}}}|alt=|link=]]<br>
 |#default    = {{#invoke:InfoboxImage|InfoboxImage
  |alt={{{alt|}}}
  |link={{{link|}}}
  |image={{{image|Replacement filing cabinet.svg}}}
  |size={{{image-size|}}}|sizedefault=40px
 }}<br>
}}{{#if:{{{index|}}}
 |[[{{#rel2abs: {{{index}}} }}|{{{title|存檔}}}]]
 |{{{title|存檔}}}
}}
</th></tr>
<tr><td style="text-align:left;">{{#if:{{{list|}}}
 |{{{list}}}
 |{{#switch:{{#switch:{{{auto|¬}}}
   |no       = no
   |long     = long
   |<!-- blank -->
   |¬        = {{#ifexist:{{#rel2abs:{{{archivelist|./archivelist}}}}}
    |{{#if:{{ {{#rel2abs:{{{archivelist|./archivelist}}}}} }}
     |index
     |long
    }}
    |long
   }}
   |yes
   |#default = list
  }}
  |no    = <!-- no output -->
  |long  = {{Archive list long|{{#if:{{{root|}}}|root}}={{{root}}} }}
  |index = {{ {{#rel2abs:{{#if:{{{archivelist|}}}|{{{archivelist}}}|./archivelist}} }} }}
  |list  = <div style="text-align:center;">{{Archive list|{{#if:{{{root|}}}|root}}={{{root}}} }}</div>
 }}
}}<!--Parameter content MUST be on newline in code or some wikimarkup will fail:-->
{{{1|}}}
</td></tr>{{#ifeq:{{{search|yes}}}|no|
 |<tr><td>{{#tag:inputbox|
bgcolor=transparent
type=fulltext
prefix={{#if:{{{prefix|}}}|{{{prefix}}}|{{#if:{{{root|}}}|{{{root}}}|{{FULLPAGENAME}}}}/}}
break={{#if:{{{search-break|}}}|{{{search-break}}}|no}}
width={{#if:{{{search-width|}}}|{{{search-width}}}|22}}
searchbuttonlabel={{#if:{{{search-button-label|}}}|{{{search-button-label}}}|-{zh-cn:搜索; zh-tw:搜尋;}-}}
}}
</td></tr>
}}{{#if:{{{bot|}}}{{{age|}}}{{{target|}}}
 |<tr><td>{{#if:{{{age|}}}
  |{{#if:{{{botnotesmall|}}}
   |<small>
  }}早於{{{age}}}{{{units|日}}}的討論{{#if:{{{minthreadszero|}}}|已|將會}}
  |本頁
 }}{{#if:{{{bot|}}}
  |由<span class="nowraplinks">[[User:{{{bot}}}|{{{bot}}}]]</span>
 }}存檔{{#if:{{{target|}}}
  |{{#ifexist:{{#rel2abs:{{{target}}}}}
   |至[[{{#rel2abs:{{{target}}}}}]]
  }}
 }}。</td></tr>
}}{{#ifeq:{{{auto}}}-{{{editbox|yes}}}|no-yes
 |<tr><td><small class="plainlinks">[{{fullurl:{{#rel2abs:{{{archivelist|./archivelist}}}}}|action=edit&preload=Template:Archives/Preload}} 編輯存檔框]</small></td></tr>
}}
</table><noinclude>{{Documentation}}</noinclude>