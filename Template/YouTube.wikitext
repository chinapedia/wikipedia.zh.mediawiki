[https://www.youtube.com/{{#if:{{{user|{{{u|}}}}}}
 |user/{{trim|{{{user|{{{u|}}}}}}}} YouTube上的{{#if:{{{title|{{{1|}}}}}}|{{#switch:{{{title|{{{1|}}}}}}|=<span class="plainlinks">頻-{}-道</span>|#default=<span class="plainlinks">{{{title|{{{1}}}}}}</span>}}|{{PAGENAME}}}}頻-{}-道]
 |{{#if:{{{channel|{{{c|}}}}}}|channel/{{trim|{{{channel|{{{c|}}}}}}}} YouTube上的{{#if:{{{title|{{{1|}}}}}}|{{#switch:{{{title|{{{1|}}}}}}|=<span class="plainlinks">頻-{}-道</span>|#default=<span class="plainlinks">{{{title|{{{1}}}}}}</span>}}|{{PAGENAME}}}}頻-{}-道]
 |{{#if:{{{custom|{{{cc|}}}}}}|c/{{trim|{{{custom|{{{cc|}}}}}}}} YouTube上的{{#if:{{{title|{{{1|}}}}}}|{{#switch:{{{title|{{{1|}}}}}}|=<span class="plainlinks">頻-{}-道</span>|#default=<span class="plainlinks">{{{title|{{{1}}}}}}</span>}}|{{PAGENAME}}}}頻-{}-道]
 |{{#if:{{{playlist|{{{p|}}}}}}|playlist?list={{trim|{{{playlist|{{{p|}}}}}}}} YouTube上的{{#if:{{{title|{{{1|}}}}}}|{{#switch:{{{title|{{{1|}}}}}}|=<span class="plainlinks">播放列表</span>|#default=<span class="plainlinks">{{{title|{{{1}}}}}}</span>}}|{{PAGENAME}}}}播放列表]
 |{{#if:{{{show|}}}|show/{{trim|{{{show|}}}}} YouTube上的{{#if:{{{title|{{{1|}}}}}}|{{#switch:{{{title|{{{1|}}}}}}|=<span class="plainlinks">劇集</span>|#default=<span class="plainlinks">{{{title|{{{1}}}}}}</span>}}|《{{PAGENAME}}》}}劇集]
 |watch?v={{trim|{{{id|{{{1|}}}}}}}}&t={{#iferror:{{#expr:{{{h|0}}}}}|0|{{#expr:{{{h|0}}}}}}}h{{#iferror:{{#expr:{{{m|0}}}}}|0|{{#expr:{{{m|0}}}}}}}m{{#iferror:{{#expr:{{{s|0}}}}}|0|{{#expr:{{{s|0}}}}}}}s YouTube上的{{#switch:{{{title}}}|=-{zh-tw:影片; zh-cn:视频; zh-hk:影片}-|#default={{{title|{{#if:{{{2|}}}|{{#switch:{{{2}}}|=-{zh-tw:影片; zh-cn:视频; zh-hk:影片}-|#default={{{2}}}}}|-{zh-tw:影片; zh-cn:视频; zh-hk:影片}-}}}}}}}]{{#iferror:{{#expr:{{{h|0}}}*60*60+{{{m|0}}}*60+{{{s|0}}}}}|
  |{{#ifexpr: {{{h|0}}}*60*60+{{{m|0}}}*60+{{{s|0}}}>0 
   |，始於{{#ifexpr: ({{{h|0}}}*60*60+{{{m|0}}}*60+{{{s|0}}})/60/60>=1|{{floor|({{{h|0}}}*60*60+{{{m|0}}}*60+{{{s|0}}})/60/60}}小時}}{{#ifexpr: (({{{m|0}}}*60+{{{s|0}}})/60) mod 60 < 10 and ({{{h|0}}}*60*60+{{{m|0}}}*60+{{{s|0}}})/60/60>=1|0}}{{#expr:({{{m|0}}}*60+{{{s|0}}})/60 mod 60}}分{{#ifexpr:{{{s|0}}} mod 60<10|0}}{{#expr:{{{s|0}}} mod 60}}秒}}}}
 }}
 }}
 }}
 }}
}}{{#if:{{{language|}}}|{{#ifexist:Template:{{{language}}}|{{{{{language}}}}}|（{{{language}}}）}}}}<noinclude>
{{documentation}}
</noinclude>