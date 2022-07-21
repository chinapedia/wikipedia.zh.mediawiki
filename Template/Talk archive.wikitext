{{tmbox
| image = [[Image:{{{icon|Replacement filing cabinet.svg}}}|40x40px|alt=|link=]]
| text  = 本頁是以往討論的'''[[Wikipedia:如何將討論頁存檔|存檔]]'''。'''請勿編輯本頁'''。若您想發起新討論或重啟現有討論，請在{{#if: {{{1|}}} | [[{{{1}}}{{!}}當前討論頁]] | [[{{NAMESPACE}}:{{BASEPAGENAME}}{{!}}當前討論頁]] }}進行。<!-- Template:Talkarchive -->
}}

__NOEDITSECTION__ {{#if:{{{current|}}}|__NEWSECTIONLINK__|__NONEWSECTIONLINK__}}
<!--請注意：
分類按照名字空間進行，如果是主名字空間和Wikipedia名字空間，則按照不同條目（頁面）名稱進行。

經驗表明，Jimmy-bot 存檔機器人根據下述分類判斷一個頁面是否是存檔頁面。去掉分類會導致存檔頁面被誤認為是孤立頁面而被提交CSD。因此如果您打算改動分類，請知悉這個情報。
-->{{ #switch: {{NAMESPACE}}
| User talk = [[Category:用户对话页存档|{{BASEPAGENAME}}]]
| Template talk = [[Category:模板讨论页存档|{{BASEPAGENAME}}]]
| Category talk = [[Category:页面分类讨论页存档|{{BASEPAGENAME}}]]
| Wikipedia talk = [[Category:维基项目讨论页存档|{{BASEPAGENAME}}]]
| Talk = [[Category:条目讨论页存档|{{BASEPAGENAME}}]]
| Portal talk = [[Category:主题讨论页存档|{{BASEPAGENAME}}]]
| Image talk = [[Category:图像讨论页存档|{{BASEPAGENAME}}]]
| #default = [[Category:讨论页存档|{{BASEPAGENAME}}]]
}}<!--
分類功能語句完成
--><noinclude>
{{documentation}}
</noinclude>