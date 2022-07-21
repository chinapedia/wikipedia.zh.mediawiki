<noinclude>
此模板移植自英文維基百科[http://en.wikipedia.org/wiki/Template:Maya_date]，利用了[[公曆|Gregorian serial date]]（暫譯為「公曆日」<!--在網路尚未找到其中文譯名-->）來產生瑪雅曆法的日期。這個模板會將今天的日期產生為瑪雅[[瑪雅曆#長紀曆|Long count]]（暫譯為「長計曆」）格式。使用'''<nowiki>{{Maya date|gsd= }}</nowiki>'''來得出所求的日期。如欲找出公曆日的日期，我們可以將模板[[:Template:Gregorian serial date]]插入本模板中。舉例來說，'''<nowiki>{{Maya date|gsd={{Gregorian serial date|month=12|day=21|year=2012}} }}</nowiki>'''可產生代表世界末日的{{Maya date|gsd={{Gregorian serial date|month=12|day=21|year=2012}} }}。

==今天的日期是==
</noinclude><!--Baktun:-->{{#expr: 
        (
        + ({{{gsd|{{Gregorian serial date}} }}} + 1137142) 
        - (({{{gsd|{{Gregorian serial date}} }}} + 1137142) mod 144000)
        ) 
        / 144000
}}.<!--Katun:-->{{#expr: 
        ((
        + ({{{gsd|{{Gregorian serial date}} }}} + 1137142) 
        - (({{{gsd|{{Gregorian serial date}} }}} + 1137142) mod 7200)
        ) 
        / 7200
        ) mod 20
}}.<!--Tun:-->{{#expr: 
        ((
        + ({{{gsd|{{Gregorian serial date}} }}} + 1137142) 
        - (({{{gsd|{{Gregorian serial date}} }}} + 1137142) mod 360)
        ) 
        / 360
        ) mod 20
}}.<!--Uinal:-->{{#expr: 
        ((
        + ({{{gsd|{{Gregorian serial date}} }}} + 1137142) 
        - (({{{gsd|{{Gregorian serial date}} }}} + 1137142) mod 20)
        ) 
        / 20
        ) mod 18
}}.<!--Kin:-->{{#expr: ({{{gsd|{{Gregorian serial date}} }}} + 1137142) mod 20}}
<noinclude>
[[Category:时间显示模板]]
</noinclude>