<includeonly>{{Userbox-2
  |id1={{#switch: {{{1|1}}}
    | 1 | 2 | 3 | 4 | 5 = [[File:Original_Barnstar.png|40px|alt=星标]]
    | 6 | 7 | 8 | 9 | 10= [[File:Barnstar2.png|40px|alt=双星标]]
    | 11 | 12 | 13 | 14 | 15 = [[File:Barnstar3.png|40px|alt=三星标]]
    | #default = [[File:BarnstarGreen.png|38px|alt=绿星标]]
    }}
  |id1-c={{#switch: {{{1|1}}}
    | 5 = #cc9966
    | 10 = #6699cc
    | 15 = #cccc66
    | 20 = #339933
    | #default = #e1d3bd
    }}
  |id2=[[Wikipedia:维基创作奖|<span lang="en">{{{1|1}}}</span>]]
  |id2-c=#FFFFFF
  |info=<div class="center">這個用戶獲得了[[中文维基百科]]'''[[:Category:{{ #ifexpr:{{{1|1}}}<10|{{{1|1}}}|{{#expr:{{{1|1}}}-({{{1|1}}} mod 10)}}-{{#expr:{{{1|1}}}-({{{1|1}}} mod 10)+9}}}}级维基创作奖|{{{1|1}}}级维基创作奖]]。'''</div>
  |info-c={{#switch: {{{1|1}}}
    | 1 | 2 | 3 | 4 | 5 = #f0e9de
    | 6 | 7 | 8 | 9 | 10 = #99cccc
    | 11 | 12 | 13 | 14 | 15 = #cccc99
    | #default = #99cc99
    }}
  |info-s=9
  |border-c=brown
}}{{#switch:{{NAMESPACE}}|{{ns:2}}|{{ns:3}}=[[Category:{{ #ifexpr:{{{1|1}}}<10|{{{1|1}}}|{{#expr:{{{1|1}}}-({{{1|1}}} mod 10)}}-{{#expr:{{{1|1}}}-({{{1|1}}} mod 10)+9}}}}级维基创作奖|{{#ifexpr:{{#expr:{{{1|1}}}>10}}|{{#expr:{{{1|1}}} mod 10}}|{{PAGENAME}}}}]]|#default=}}</includeonly>