{{#if: {{{1|{{{id<includeonly>|</includeonly>}}}}}}

| [[爛番茄]]上《[https://www.rottentomatoes.com/{{#ifeq:
  {{#invoke:String|find|source={{{1|{{{id}}}}}}|target=^m/|plain=false
  }}{{#invoke:String|find|source={{{1|{{{id}}}}}}|target=^tv/|plain=false
  }}{{#invoke:String|find|source={{{1|{{{id}}}}}}|target=^franchise/|plain=false
  }}{{#invoke:String|find|source={{{1|{{{id}}}}}}|target=^celebrity/|plain=false
  }}{{#invoke:String|find|source={{{1|{{{id}}}}}}|target=^critic/|plain=false
  }}|00000|m/}}{{Trim|{{{1|{{{id}}}}}}}} {{#ifeq:
  {{#invoke:String|find|source={{{1|{{{id}}}}}}|target=^celebrity/|plain=false
  }}{{#invoke:String|find|source={{{1|{{{id}}}}}}|target=^critic/|plain=false
  }}|00|}}{{#if: {{{2|{{{name|{{{title<includeonly>|</includeonly>}}}}}}}}}
  | {{{2|{{{name|{{{title}}}}}}}}}
  | {{PAGENAMEBASE}}
  }}{{#ifeq:
  {{#invoke:String|find|source={{{1|{{{id}}}}}}|target=^celebrity/|plain=false
  }}{{#invoke:String|find|source={{{1|{{{id}}}}}}|target=^critic/|plain=false
  }}|00|}}]》的資料{{en icon}}

| {{#if: {{#property:P1258}}

  | [[爛番茄]]上《[https://www.rottentomatoes.com/{{First word|1={{#property:P1258}}|sep=,}} {{#ifeq:
  {{#invoke:String|find|source={{#property:P1258}}|target=^celebrity/|plain=false
  }}{{#invoke:String|find|source={{#property:P1258}}|target=^critic/|plain=false
  }}|00|}}{{#if: {{{2|{{{name|{{{title|}}}}}}}}}
  | {{{2|{{{name|{{{title}}}}}}}}}
  | {{PAGENAMEBASE}}
  }}{{#ifeq:
  {{#invoke:String|find|source={{#property:P1258}}|target=^celebrity/|plain=false
  }}{{#invoke:String|find|source={{#property:P1258}}|target=^critic/|plain=false
  }}|00|}}]》的資料{{en icon}}{{EditAtWikidata|pid=P1258}}

  | <span class="error">&#123;&#123;[[Template:Rotten Tomatoes|Rotten Tomatoes]]&#125;&#125; template missing ID and not present in Wikidata.</span>{{Main other|[[Category:Rotten Tomatoes template missing ID and not in Wikidata]]}}

  }}

}}{{Main other|{{#if: {{{name|}}} | [[Category:Rotten Tomatoes template using name parameter]] }}}}<noinclude>{{Documentation}}
[[Category:电影外部链接模板|Rotten Tomatoes]]</noinclude>