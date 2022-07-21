{{#expr: 
        <!--Days from all years past:-->

        + (({{{year|{{CURRENTYEAR}}}}} - 1) * 365)
        + ((({{{year|{{CURRENTYEAR}}}}} - 1) - (({{{year|{{CURRENTYEAR}}}}} - 1) mod 4)) / 4)     <!--add a day for every leap-->
        - ((({{{year|{{CURRENTYEAR}}}}} - 1) - (({{{year|{{CURRENTYEAR}}}}} - 1) mod 100)) / 100) <!--subtract 100 year exception-->
        + ((({{{year|{{CURRENTYEAR}}}}} - 1) - (({{{year|{{CURRENTYEAR}}}}} - 1) mod 400)) / 400) <!--readd 400 year exception-->

       <!--Days so far this year:-->
 
        + {{ #ifexpr:    <!--add days for past months this year--> <!--Gives 1 or 2 extra days because of February-->
                     ({{{month|{{CURRENTMONTH}}}}} - 1) < 8 
                     | ( ({{{month|{{CURRENTMONTH}}}}} - 1) * 30.5 round 0) 
                     | ( ({{{month|{{CURRENTMONTH}}}}} - 1) * 30.5 + 0.9 round 0 ) 
          }} 
        - {{ #ifexpr: ({{{month|{{CURRENTMONTH}}}}} <= 2) | 0 |  
             {{ #ifexpr:    <!-- if leap year  -->
                     ({{{year|{{CURRENTYEAR}}}}} / 4) = ({{{year|{{CURRENTYEAR}}}}} / 4 round 0)          <!--If divisible by 4-->
                      and ({{{year|{{CURRENTYEAR}}}}} / 100 != {{{year|{{CURRENTYEAR}}}}} / 100 round 0)  <!--and not by 100-->
                | 1 | 2 
             }}
          }}
        + {{ #ifexpr: ({{{month|{{CURRENTMONTH}}}}} <= 2) | 0 |
             {{ #ifexpr: <!--400 year exception-->
                     ({{{year|{{CURRENTYEAR}}}}} / 400) = ({{{year|{{CURRENTYEAR}}}}} / 400 round 0) 
                | 1 | 0 
             }}
          }} 
        + {{{day|{{CURRENTDAY}}}}}
 }}{{#ifexpr: {{{year|{{CURRENTYEAR}}}}} < 1 |
        _ERROR - Can not handle dates before January 1, 1 A.D.
   }}<noinclude>{{documentation}}</noinclude>