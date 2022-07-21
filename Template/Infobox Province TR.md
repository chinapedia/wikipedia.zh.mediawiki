{{Infobox settlement
<!-- See Template:Infobox settlement for additional fields and descriptions -->
| name = {{PAGENAME}}
| native_name                    = {{#if: {{{name|}}} | {{{name}}} | {{PAGENAMEBASE}} }} ili
| native_name_lang        = tr<!-- ISO 639-2 code e.g. "tr" for Turkish. If more than one, use {{lang}} instead -->
| settlement_type         = [[土耳其行政区划|省份]]
| image_skyline           = {{{image|}}}
| image_caption           = {{{caption|}}}
<!-- maps and coordinates ------>
| image_map               = <includeonly>File:{{{name|}}} in Turkey.svg</includeonly>
| mapsize                 = 300px
| map_caption             = {{PAGENAME}}在[[土耳其]]的位置
<!-- location ------------------>
| subdivision_type        = 國家
| subdivision_name        = {{TUR}}
| subdivision_type1       = [[土耳其地域統計單位命名法|地區]]
| subdivision_name1       = {{#if:{{{region|}}}|[[{{{region}}}地區 (統計)|{{{region}}}]]}}
| subdivision_type2       = [[土耳其地域統計單位命名法|次分區]]
| subdivision_name2       = {{#if:{{{subregion|}}}|[[{{{subregion}}}次分區|{{{subregion}}}]]}}
| seat_type               = 首府{{#ifeq:{{{seat|}}}|{{{largest_city|}}}|及最大城市}}
| seat                    = {{{seat|}}}
| seat1_type              = 最大城市
| seat1                   = {{#ifeq:{{{seat|}}}|{{{largest_city|}}}| | {{{largest_city|}}} }}
<!-- coordinates -->
| coordinates = {{#if:{{{coordinates|}}}|{{#invoke:Coordinates|coordinsert|{{{coordinates}}}|type:adm1st_region:{{#if:{{{licence|}}}|TR-{{{licence|}}}|TR}}}}}}
<!-- government type, leaders -->
| leader_title            = {{#if:{{{name|}}} | {{link-en|土耳其選區|Electoral districts of Turkey|選區}} }}
| leader_name             = {{#ifexist: {{{name}}} (選區)| [[{{{name}}} (選區)|{{{name}}}]] | {{if empty|{{{electdistrict|}}}|{{{name|}}}}} }}
| leader_title1           = {{#if: {{{governor|}}} | 省長 }}
| leader_name1            = {{{governor|}}}
| total_type              = 總計
| area_total_km2          = {{{area|}}}
| population_footnotes    = 
| population_total        = {{#iferror:{{#expr:{{Metadata Population Turkish province|{{{turkname|}}} }}+1}} | {{#iferror:{{#expr:{{Metadata Population Turkish province|{{{name|}}} }}+1}} | {{{total population|}}} | {{Metadata Population Turkish province|{{{name|}}} }} }} | {{Metadata Population Turkish province|{{{turkname|}}} }} }}
| population_as_of        =  {{#if:{{#iferror:{{#expr:{{Metadata Population Turkish province|{{{turkname|}}} }}+1}} | {{#iferror:{{#expr:{{Metadata Population Turkish province|{{{name|}}} }}+1}} |  1 }} }} | {{{tpop_as_of|}}} | {{Metadata Population Turkish province|TIMESTAMP}} }}
| population_density_km2  = auto
| population_urban        = {{{urban population|}}}
| population_urban_footnotes     = {{{upop_ref|}}} {{#if:{{{upop_as_of|}}} | ({{{upop_as_of}}}) }}
| population_rural        = {{{rural population|}}}
| population_rural_footnotes     = {{{rpop_ref|}}} {{#if:{{{rpop_as_of|}}} | ({{{rpop_as_of}}}) }}
| area_code_type          = <!-- defaults to: Area code(s) -->
| area_code               = {{#if:{{{area_code|}}}|+90 {{{area_code|}}}}}
| registration_plate      = {{{licence|}}}
| website                 = {{{website|}}}
| footnotes               = 
}}<noinclude>
{{Documentation}}
</noinclude>