{{#ifexist:{{{2}}}
|<!-- if parameter 2 exists -->{{#ifeq: {{{link|no}}}|yes|<!-- if use link -->[[{{Trim|{{{2}}}}}|<span title="{{Trim|{{{1}}}}}" class="rt-commentedText" style="display: inline-block; {{#ifeq:{{{dotted|yes}}}|no||border-bottom: 1px dotted; }}">{{Trim|{{{2}}}}}</span>]]|<!-- if no link --><span title="{{Trim|{{{1}}}}}" class="rt-commentedText" style="display: inline-block; {{#ifeq:{{{dotted|yes}}}|no||border-bottom: 1px dotted;}}">{{Trim|{{{2}}}}}</span>}}
|<!-- if parameter 2 does not exist --><span title="{{Trim|{{{1}}}}}" class="rt-commentedText" style="display: inline-block; {{#ifeq:{{{dotted|yes}}}|no||border-bottom: 1px dotted; }}">{{Trim|{{{2}}}}}</span>
}}<noinclude>
{{Documentation}}</noinclude>