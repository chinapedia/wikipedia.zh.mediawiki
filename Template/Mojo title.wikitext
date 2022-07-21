{{#if: {{{1|{{{id<includeonly>|</includeonly>}}}}}}
| [[Box Office Mojo]]上《[https://www.boxofficemojo.com/{{#if:{{#invoke:String|match|s={{{id|{{{1}}}}}}|pattern=^%d%d%d%d%d%d%d$|ignore_errors=true}} | title/tt{{{id|{{trim|{{{1}}}}}}}}/ | movies/?id={{{id|{{trim|{{{1}}}}}}}}.htm }} {{#if:{{{title|{{{2|}}}}}} | {{{title|{{{2}}}}}} | {{PAGENAMEBASE}} }}]》的資料{{en icon}}
| {{#if: {{#property:P1237}}
  | [[Box Office Mojo]]上《[https://www.boxofficemojo.com/movies/?id={{First word|{{#property:P1237}}|sep=,}}.htm {{#if:{{{2|{{{title<includeonly>|</includeonly>}}}}}} | {{{2|{{{title}}}}}} | {{PAGENAMEBASE}} }}]》的資料{{en icon}}{{EditAtWikidata|pid=P1237}} 
| {{#if:{{#property:P345}}
      | [[Box Office Mojo]]上《[https://www.boxofficemojo.com/title/{{First word|{{#property:P345}}|sep=,}}/ {{#if:{{{title|{{{2|}}}}}} | {{{title|{{{2}}}}}} | {{PAGENAMEBASE}} }}}}]》的资料{{en icon}}{{EditAtWikidata|pid=P345}}
  | <span class="error">&#123;&#123;[[Template:Mojo title|Mojo title]]&#125;&#125;模板缺少ID且不存在于维基数据。</span>
  }}
}}<noinclude>
{{Documentation}}
[[Category:电影外部链接模板|{{PAGENAME}}]]
</noinclude>