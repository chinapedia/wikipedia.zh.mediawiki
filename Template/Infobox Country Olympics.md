{{infobox country at games
| NOC = {{{NOC|}}}
| games = {{{games|}}}奥林匹克运动会
| flagcaption = {{{flagcaption|auto}}}
| NOCname = {{{NOCname|{{Sport orgs alias|{{{NOC|}}}|fullName={{{games|}}}奥林匹克运动会}}}}}
| website = {{{website|{{Sport orgs alias|{{{NOC|}}}|fullName={{{games|}}}奥林匹克运动会|website=yes}}}}}
| oldcode = {{{oldcode|}}}
| location = {{{location|{{Infobox Country Olympics/Location and dates|type=location|games={{{games|}}}}}}}}
| date = {{{date|{{Infobox Country Olympics/Location and dates|type=date|games={{{games|}}}}}}}}
| competitors = {{{competitors|}}}
| competitors_men = {{{competitors_men|}}}
| competitors_women = {{{competitors_women|}}}
| sports = {{{sports|}}}
| events = {{{events|}}}
| officials = {{{officials|}}}
| flagbearer = {{{flagbearer|}}}
| rank = {{{rank|}}}
| gold = {{{gold|}}}
| silver = {{{silver|}}}
| bronze = {{{bronze|}}}
| app0_name = {{#invoke:String|replace|{{{games|}}}|^%d*年?[夏冬]季|ignore_errors=1|plain=0}}奥林匹克运动会
| altsummarypage = {{#if:{{{altsummarypage|}}}|{{{altsummarypage|}}}|{{#switch:{{{NOC|}}}|COK={{#ifeq:{{{games|}}}|1968年夏季|奥林匹克运动会刚果民主共和国代表团}}|MAL={{#ifeq:{{{games|}}}|1964年夏季|奥林匹克运动会马来西亚代表团|{{#ifeq:{{{games|}}}|1968年夏季|奥林匹克运动会马来西亚代表团}}}}|ROC={{#ifeq:{{{games|}}}|2020年夏季|奥林匹克运动会独立参赛者|{{#ifeq:{{{games|}}}|2022年冬季|奥林匹克运动会独立参赛者}}}}|#default=}}}}
| app1_name = 夏季{{#invoke:String|replace|{{{games|}}}|^%d*年?[夏冬]季|ignore_errors=1|plain=0}}奥林匹克运动会
<!--当输入COK+1968年夏季时国家/地区名称会返回刚果金沙萨，由于COK后来用于库克群岛，因此直接使用auto会误返回库克群岛的参赛记录，由于刚果（金）和库克群岛都没参加过冬奥，故冬季处暂时不处理-->
<!--当输入ROC+2020年夏季/2022年冬季时国家/地区名称会返回俄罗斯奥林匹克委员会，由于ROC以前用于中华民国，因此直接使用auto会误返回中华民国的参赛记录-->
| app1 = {{#if:{{{summerappearances|}}}|{{{summerappearances|}}}|{{#switch:{{{NOC|}}}|COK={{#ifeq:{{{games|}}}|1968年夏季|{{Team appearances list|team=COK_1968|competition=夏季奥林匹克运动会}}|auto}}|MAL={{#ifeq:{{{games|}}}|1964年夏季|{{Team appearances list|team=MAS|competition=夏季奥林匹克运动会}}|{{#ifeq:{{{games|}}}|1968年夏季|{{Team appearances list|team=MAS|competition=夏季奥林匹克运动会}}|auto}}}}|ROC={{#ifeq:{{{games|}}}|2020年夏季|{{Team appearances list|team=ROC_RUS|competition=夏季奥林匹克运动会}}|{{#ifeq:{{{games|}}}|2022年冬季|{{Team appearances list|team=ROC_RUS|competition=夏季奥林匹克运动会}}|auto}}}}|#default=auto}}}}
| app2_name = 冬季{{#invoke:String|replace|{{{games|}}}|^%d*年?[夏冬]季|ignore_errors=1|plain=0}}奥林匹克运动会
| app2 = {{#if:{{{winterappearances|}}}|{{{winterappearances|}}}|{{#switch:{{{NOC|}}}|MAL={{#ifeq:{{{games|}}}|1964年夏季|{{Team appearances list|team=MAS|competition=冬季奥林匹克运动会}}|{{#ifeq:{{{games|}}}|1968年夏季|{{Team appearances list|team=MAS|competition=冬季奥林匹克运动会}}|auto}}}}|ROC={{#ifeq:{{{games|}}}|2020年夏季|{{Team appearances list|team=ROC_RUS|competition=冬季奥林匹克运动会}}|{{#ifeq:{{{games|}}}|2022年冬季|{{Team appearances list|team=ROC_RUS|competition=冬季奥林匹克运动会}}|auto}}}}|#default=auto}}}}
| seealso = {{{seealso|{{Infobox Country Olympics/See also|{{#switch:{{{NOC|}}}|MAL={{#ifeq:{{{games|}}}|1964年夏季|MAS|{{#ifeq:{{{games|}}}|1968年夏季|MAS|MAL}}}}|ROC={{#ifeq:{{{games|}}}|2020年夏季|ROC_RUS|{{#ifeq:{{{games|}}}|2022年冬季|ROC_RUS|ROC}}}}|#default={{{NOC|}}}}}|{{#invoke:String|replace|{{{games}}}|^%d*年?[夏冬]季|ignore_errors=1|plain=0}}}}}}}
| previous = {{{previous|}}}
| next = {{{next|}}}
| cat = 1
}}<noinclude>
{{Documentation}}
</noinclude>