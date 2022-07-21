<includeonly>{{Coord/link|dms-lat={{coord/dec2dms|{{{1}}}|{{{2}}}|{{#ifeq:{{{2}}}|N|S|N}}|{{coord/prec dec|{{{1}}}|{{{3}}}}}}}|dms-long={{coord/dec2dms|{{{3}}}|{{{4}}}|{{#ifeq:{{{4}}}|E|W|E}}|{{coord/prec dec|{{{1}}}|{{{3}}}}}}}|dec-lat={{#ifeq:{{{2}}}|S|-}}{{{1}}}|dec-long={{#ifeq:{{{4}}}|W|-}}{{{3}}}|dec-lat-display={{{1}}}°{{{2}}}|dec-long-display={{{3}}}°{{{4}}}|param={{{1}}}_{{{2}}}_{{{3}}}_{{{4}}}_{{{5}}}|default={{#if:{{{format|}}}|{{{format}}}|{{#ifeq:{{coord/prec dec|{{{1}}}|{{{3}}}}}|d|dms|dec}}}}|name={{{name|}}}}}<!-- 
 -->{{#if:{{{6}}}|{{Coord/input/error2|msg=extra parameters|sort_ch=#}}}}<!-- 
 -->{{#ifexpr:0{{{1}}}>90|{{Coord/input/error2|msg=latd>90|sort_ch=>}}}}<!-- 
 -->{{#ifexpr:0{{{1}}}<-90|{{Coord/input/error2|msg=latd<-90|sort_ch=<}}}}<!-- 
 -->{{#ifexpr:0{{{3}}}<360||{{Coord/input/error2|msg=longd>=360|sort_ch=>}}}}<!-- 
 -->{{#ifexpr:0{{{3}}}>-360||{{Coord/input/error2|msg=longd<=-360|sort_ch=<}}}}<!-- 
 --></includeonly><noinclude>{{template doc|Template:Coord/sub doc}}</noinclude>