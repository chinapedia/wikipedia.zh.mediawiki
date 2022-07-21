{{Date.day+n|{{#expr:
  ({{Date.OrdinalMinutesTZ|{{{1|0}}}|{{{2|{{CURRENTTIME}}}}}}} >= 1440 )
  - ( {{Date.OrdinalMinutesTZ|{{{1|0}}}|{{{2|{{CURRENTTIME}}}}}}}<0 ) 
}}}}{{UTCtime|{{{1|0}}}|{{{2|{{CURRENTTIME}}}}}}}<noinclude>{{Documentation}}</noinclude>