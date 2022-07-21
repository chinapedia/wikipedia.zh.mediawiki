{{
  #if: {{{Authorlink1|}}}
  |[[{{{Authorlink1}}} |{{{Surname1}}}{{
     #if: {{{Given1|}}}
     |, {{{Given1}}}
   }}]]
  |{{{Surname1}}}{{
     #if: {{{Given1|}}}
     |, {{{Given1}}}
   }}
}}{{
  #if: {{{Surname2|}}}
  |{{
     #if: {{{Surname3|}}}
     |<nowiki>; </nowiki>
     |&#32;&amp;&#32;
   }}{{
     #if: {{{Authorlink2|}}}
     |[[{{{Authorlink2}}} |{{{Given2|}}} {{{Surname2}}}]]
     |{{{Given2|}}} {{{Surname2}}}
   }}{{
     #if: {{{Surname3|}}}
     |&#32;&amp; {{
        #if: {{{Authorlink3|}}}
        |[[{{{Authorlink3}}} |{{{Given3|}}} {{{Surname3}}}]]
        |{{{Given3|}}} {{{Surname3}}}
      }}{{
        #if:{{{Surname4|}}}
        |&#32;et al.
      }}
   }}
}}<noinclude>

{{documentation}}
<!-- Categories go on the /doc subpage and interwikis go on Wikidata. -->
</noinclude>