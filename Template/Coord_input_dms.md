<includeonly>{{Coord/link|dms-lat={{{1}}}°{{#if:{{{2}}}|{{{2}}}′}}{{#if:{{{3}}}|{{{3}}}″}}{{{4}}}|dms-long={{{5}}}°{{#if:{{{6}}}|{{{6}}}′}}{{#if:{{{7}}}|{{{7}}}″}}{{{8}}}|dec-lat={{coord/dms2dec|{{{4}}}|{{{1}}}|0{{{2}}}|0{{{3}}}}}|dec-long={{coord/dms2dec|{{{8}}}|{{{5}}}|0{{{6}}}|0{{{7}}}}}|param={{{1}}}_{{{2}}}_{{{3}}}_{{{4}}}_{{{5}}}_{{{6}}}_{{{7}}}_{{{8}}}_{{{9}}}|default={{#if:{{{format|}}}|{{{format}}}|dms}}|name={{{name|}}}}}<!-- 
 -->{{#if:{{{10}}}|{{Coord/input/error2|msg=extra parameters|sort_ch=#}}}}<!-- 
 -->{{#ifexpr:0{{{1}}}>90|{{Coord/input/error2|msg=latd>90|sort_ch=>}}}}<!-- 
 -->{{#ifexpr:0{{{1}}}<-90|{{Coord/input/error2|msg=latd<-90|sort_ch=<}}}}<!-- 
 -->{{#ifexpr:0{{{2}}}<60||{{Coord/input/error2|msg=latm>=60|sort_ch='}}}}<!-- 
 -->{{#ifexpr:0{{{2}}}<0|{{Coord/input/error2|msg=latm<0|sort_ch='}}}}<!-- 
 -->{{#ifexpr:0{{{3}}}<60||{{Coord/input/error2|msg=lats>=60|sort_ch="}}}}<!-- 
 -->{{#ifexpr:0{{{3}}}<0|{{Coord/input/error2|msg=lats<0|sort_ch="}}}}<!-- 
 -->{{#ifexpr:0{{{5}}}<360||{{Coord/input/error2|msg=longd>=360|sort_ch=>}}}}<!-- 
 -->{{#ifexpr:0{{{5}}}>-360||{{Coord/input/error2|msg=longd<=-360|sort_ch=<}}}}<!-- 
 -->{{#ifexpr:0{{{6}}}<60||{{Coord/input/error2|msg=longm>=60|sort_ch='}}}}<!-- 
 -->{{#ifexpr:0{{{6}}}<0|{{Coord/input/error2|msg=longm<0|sort_ch='}}}}<!-- 
 -->{{#ifexpr:0{{{7}}}<60||{{Coord/input/error2|msg=longs>=60|sort_ch="}}}}<!-- 
 -->{{#ifexpr:0{{{7}}}<0|{{Coord/input/error2|msg=longs<0|sort_ch="}}}}<!-- 
 --></includeonly><noinclude>
{{template doc|Coord/sub doc}}
</noinclude>