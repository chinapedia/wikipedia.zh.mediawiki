<noinclude>
{{Template doc page viewed directly}}
</noinclude>
{{更新|time=2013-12-14T04:01:41+00:00}}
''这是一个2007年7月7日增加的新模板，目前看来在{{tl|User RA}}和{{tl|User Mabinogi}}中工作良好。如果这个模板成为公认的好用的模板，请删掉这行文字。''

{{Userboxtop
|toptext=''目前试用了这个模板的用户框''
|extra-css=font-size:9pt
}}
{{User RA}}
{{User Mabinogi}}
{{Userboxbottom}}

*用法：
:在创建或修改用户框时，使用这个模板替代<nowiki>[[Category:目标分类]]</nowiki>：
:<nowiki>{{UserboxCat|目标分类}}</nowiki>


这个模板解决了两个问题：
*避免了在分类中使用用户框样例将会导致分类中出现递归显示
:*例：
:#若[[:Category:目标分类]]中使用了用户框{{tl|User Foo}}作为诠释，
:#并且{{tl|User Foo}}中设置[['''Category:目标分类''']]，
::则[[:Category:目标分类]]的子分类中可能出现[[:Category:目标分类]]自身，并且会产生递归显示：
::[-] [[:Category:目标分类]]
:::[-] [[:Category:目标分类]]
::::[-] [[:Category:目标分类]]
:::::[-] [[:Category:目标分类]]
:::::: ...


:若{{tl|User Foo}}中使用了本模板，则不会产生这种情况。


*避免了将放置用户框的用户页子页加入相应分类
:*例：
:#若用户框{{tl|User Foo}}中设置了[['''Category:目标分类''']]，
:#并且在用户页子页User:Bar/ubx中使用{{tl|User Foo}}，
::则[[:Category:目标分类]]中将会出现User:Bar/ubx。


::若用户页User:Bar/ubx中使用了{{[[User:Bar/ubx|/ubx]]}}，
::则[[:Category:目标分类]]中将会同时存在User:Bar和User:Bar/ubx。


:如果在用户框中使用了本模板，将不会出现用户页和用户页子页同时存在于同一个分类中的情况。
:*例：
:#若用户框{{tl|User Foo}}使用了{{tl|UserboxCat|目标分类}}，
:#并且用户页子页User:Bar/ubx中使用了用户框{{tl|User Foo}}，
::用户页子页User:Bar/ubx将会出现在[[:Category:目标分类/]]中，而不是[[:Category:目标分类]]。


::若用户页User:Bar中使用了{{[[User:Bar/ubx|/ubx]]}}，
::用户页User:Bar则会出现在[[:Category:目标分类]]中。