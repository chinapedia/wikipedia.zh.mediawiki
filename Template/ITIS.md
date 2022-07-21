<includeonly>{{#ifeq: {{{ID|{{{id|}}}}}} |
| {{Citation error|使用{{tl|ITIS}}時必須提供<tt>id</tt>參數。|nocat={{{template doc demo|}}}}}
| {{#if: {{{taxon|{{{title|}}}}}}
  | {{cite web
    | url = https://www.itis.gov/servlet/SingleRpt/SingleRpt?search_topic=TSN&search_value={{{ID|{{{id|}}}}}}
    | title = {{{taxon|{{{title|}}}}}}
    | publisher = ''[[整合分類學資訊系統|ITIS]]''
    | access-date = {{#if: {{{accessdate|{{{access-date|}}}}}}
                   | {{{accessdate|{{{access-date|}}}}}}
                   | {{#if: {{{date|}}}|{{{date|}}},&nbsp;}}{{{year|}}}
                   }}
    | year = {{#if: {{{year|}}} | {{{year|}}} | }}
}}
  | [https://www.itis.gov/servlet/SingleRpt/SingleRpt?search_topic=TSN<!--
    -->&search_value={{{ID|{{{id|}}}}}} ITIS]
  }}
}}</includeonly><noinclude>
{{Documentation}}
</noinclude>