{{Template doc page viewed directly}}
{{Lua|Module:Tasks}}

本模板用于展示专题、主题的任务。

== 用法 ==

<pre>{{Tasks
<!-- 专题内协调 -->
| collaborate = 
| assess = 
<!-- 删除与合并 -->
| deletion = 
| notability = 
| merge = 
| split =
| move =
<!-- 清理 -->
| category =
| maintain =
| cleanup =
| wikify =
| orphans =
| disambiguation =
<!-- 内容 -->
| expand = 
| stubs =
| requests =
| copyedit =
| npov =
| update =
<!-- 来源 -->
| citations =
| unreferenced = 
| verify =
<!-- 其它请求 -->
| infobox = 
| photo =
| map = 
<!-- 评选 -->
| fac = 
| far =
| flc =
| gan =
| gar =
| dykc =
| pr =
}}</pre>

== 效果 ==
{{Tasks
|requests={{{requests}}} 
|assess={{{assess}}} 
|category={{{category}}} 
|citations={{{citations}}} 
|cleanup={{{cleanup}}} 
|collaborate={{{collaborate}}}
|copyedit={{{copyedit}}} 
|deletion={{{deletion}}}
|disambiguation={{{disambiguation}}} 
|expand={{{expand}}} 
|fac={{{fac}}} 
|far={{{far}}} 
|flc={{{flc}}}
|fsc={{{fsc}}}
|gan={{{gan}}} 
|gar={{{gar}}} 
|dykc={{{dykc}}}
|pr={{{pr}}}
|geocoord={{{geocoord}}} 
|infobox={{{infobox}}} 
|maintain={{{maintain}}} 
|map={{{map}}} 
|merge={{{merge}}} 
|notability={{{notability}}}
|npov={{{npov}}} 
|orphans={{{orphans}}} 
|photo={{{photo}}} 
|portal={{{portal}}}
|split={{{split}}} 
|stubs={{{stubs}}} 
|translate={{{translate}}}
|unreferenced={{{unreferenced}}}
|update={{{update}}} 
|verify={{{verify}}} 
|wikify={{{wikify}}} 
|other={{{other}}} 
|othertext={{{othertext}}}
}}
== 示例 ==

{| class="wikitable"
! 输入
! 效果
|-
| style="width: 50%" | <pre>{{Tasks 
| cleanup = {{Tasks/petscan|banner=WikiProject_Video_games|Game_guide|text=游戏攻略}}
| requests = [[Wikipedia:电子游戏专题/条目请求]]
| infobox = [[:Category:含有废弃电子游戏信息框参数的条目|废弃参数]]
}}</pre>
| {{Tasks 
| cleanup = {{Tasks/petscan|banner=WikiProject_Video_games|Game_guide|text=游戏攻略}}
| requests = [[Wikipedia:电子游戏专题/条目请求]]
| infobox = [[:Category:含有废弃电子游戏信息框参数的条目|废弃参数]]
}}
|}

== 参见 ==
*{{tl|Tasks/petscan}}，在没有相应维护分类时，通过外部工具petscan:列出维护页面列表。

<includeonly>
[[Category:維基百科維護模板|{{PAGENAME}}]]
</includeonly>