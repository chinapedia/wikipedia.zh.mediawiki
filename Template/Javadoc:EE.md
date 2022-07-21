{{#if: {{{1|}}}
  |<code>[{{Javadoc:EE/Home URL}}/{{{1}}}/{{
    #if:{{{3|}}}
    |{{{2|package-summary}}}.html#{{{3}}}
    |{{{2|package-summary}}}.html
  }} {{
    #if:{{{name|}}}
    |{{{name}}}
    |{{
      #if:{{{package|}}}
      |{{{package}}}{{
        #if:{{{2|}}}
        |.
      }}
    }}{{
      #if:{{{2|}}}
      |{{{class|{{{2}}} }}}
    }}{{
      #if:{{{3|}}}
      |.{{{member|{{{3}}} }}}
    }}
  }}]</code>
  |[{{Javadoc:EE/Home URL}}/ Java EE 6 API Javadocs]
}}<noinclude>{{documentation}}</noinclude>