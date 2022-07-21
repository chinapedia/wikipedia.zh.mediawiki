<noinclude>
<div class="messagebox standard-talk">使用方法請看[[Template:Infobox animanga]]。</div>
{{Infobox_animanga/Top}}
</noinclude>{{Infobox_animanga/Head|{{#if:{{{輕小說|}}}|[[輕小說]]|[[小说]]}}|{{{Title|{{{標題|{{{タイトル|{{{name|}}}}}}}}}}}}}}
{{Infobox_animanga/Image|{{{image|{{{圖像|{{{画像|}}}}}}}}}|size={{{尺寸|{{{サイズ|{{{size|}}}}}}}}}|title={{{說明|{{{説明|{{{caption|}}}}}}}}}|2=<br />{{{caption|{{{説明|{{{說明|}}}}}}}}}}}
{{Infobox_animanga/Item|原作|{{{原作|}}}}}
{{Infobox_animanga/Item|作者|{{{作者|{{{著者|{{{author|}}}}}}}}}}}
{{Infobox_animanga/Item|插圖|{{{插圖|{{{イラスト|{{{illustrator|}}}}}}}}}}}
{{Infobox_animanga/Item|出版社|{{{出版社|{{{publisher|}}}}}}}}
{{Infobox_animanga/Collapsible|其他出版社|{{{其他出版社|{{{publisher_other|}}}}}}}}
{{Infobox_animanga/Item|連載雜誌|{{{連載雜誌|{{{掲載誌|{{{magazine|}}}}}}}}}}}
{{Infobox_animanga/Item|[[文庫]]|{{{label|{{{標籤|{{{レーベル|}}}}}}}}}}}
{{Infobox_animanga/Item|發行日期|{{{發行日期|{{{発行日|}}}}}}}}
{{Infobox_animanga/Item|發售日|{{{發售日|{{{発売日|}}}}}}}}
{{Infobox_animanga/Item|登載號|{{{連載號|{{{掲載号|}}}}}}}}
{{Infobox_animanga/Item|連載期間|{{{連載開始|{{{開始号|}}}}}}|display={{{連載開始|{{{開始号}}}}}}－{{#if:{{{連載結束|}}}{{{終了号|}}}|{{{連載結束|{{{終了号}}}}}}|連載中}}}}
{{Infobox_animanga/Item|連載網站|{{{連載網站|{{{連載網絡|{{{连载网络|{{{網路|{{{網絡|}}}|{{{网络|}}}}}}}}}}}}}}}}}
{{Infobox_animanga/Item|出版期間|{{{出版開始|{{{開始|{{{開始日|}}}}}}}}}|display={{{出版開始|{{{開始|{{{開始日|}}}}}}}}}－{{#if: {{{出版結束|}}}{{{結束|}}}{{{終了|}}}{{{終了日|}}}|{{{出版結束|{{{結束|{{{終了|{{{終了日}}}}}}}}}}}}|出版中}}}}
{{Infobox_animanga/Item|冊數|{{{冊數|{{{巻数|{{{冊数|{{{volumes|}}}}}}}}}}}}}}
{{Infobox_animanga/Item|話數|{{{話數|{{{話数|}}}}}}}}
{{Infobox_animanga/Item|其他|{{{其他|{{{その他|}}}}}}}}
{{Infobox_animanga/Item|版权信息|{{{版權|{{{Copyright|{{{コピーライト|}}}}}}}}}|display=<strong>©</strong>{{{版權|{{{Copyright|{{{コピーライト}}}}}}}}}}}<noinclude>
{{Infobox_animanga/Bottom}}
{{High-use|300+|Template talk:Infobox_animanga}}
{{esoteric}}
<templatedata>
{
	"description": "ACG系列信息系列模板，（轻）小说模块",
	"params": {
		"image": {
			"label": "image",
			"type": "string",
			"description": "作品图片，Logo或海报，无需File:",
			"aliases": [
				"画像",
				"圖像"
			]
		},
		"size": {
			"label": "size",
			"type": "string",
			"description": "图片大小",
			"aliases": [
				"サイズ",
				"尺寸"
			]
		},
		"caption": {
			"label": "caption",
			"type": "string",
			"description": "图片说明",
			"aliases": [
				"說明",
				"説明"
			]
		},
		"著者": {
			"label": "著者",
			"type": "string",
			"required": true,
			"description": "作品作者",
			"aliases": [
				"作者",
				"author"
			]
		},
		"其他出版社": {
			"label": "其他出版社",
			"type": "string",
			"description": "连载作品其他出版社",
			"aliases": [
				"publisher_other"
			]
		},
		"出版社": {
			"label": "出版社",
			"type": "string",
			"required": true,
			"description": "连载作品出版社",
			"aliases": [
				"publisher"
			]
		},
		"label": {
			"label": "label",
			"type": "string",
			"description": "小说所属文库",
			"aliases": [
				"標籤",
				"レーベル"
			]
		},
		"話数": {
			"label": "話数",
			"type": "string",
			"description": "总连载话数",
			"aliases": [
				"話數",
				"话数"
			]
		},
		"輕小說": {
			"label": "輕小說",
			"type": "string",
			"description": "轻小说标记，只要填写任何值，标题则会变为轻小说"
		},
		"標題": {
			"aliases": [
				"タイトル",
				"Title",
				"name"
			],
			"label": "標題",
			"description": "作品标题",
			"type": "string"
		},
		"原作": {
			"label": "原作",
			"description": "作品原案作者"
		},
		"插圖": {
			"aliases": [
				"イラスト",
				"illustrator"
			],
			"label": "插圖",
			"description": "作品插图",
			"type": "string"
		},
		"連載雜誌": {
			"aliases": [
				"掲載誌",
				"magazine"
			],
			"label": "連載雜誌",
			"description": "出版连载杂志",
			"type": "string"
		},
		"連載號": {
			"aliases": [
				"掲載号"
			],
			"label": "連載號",
			"description": "发表杂志的连载号",
			"type": "string"
		},
		"連載開始": {
			"aliases": [
				"開始号"
			],
			"label": "連載開始",
			"description": "连载开始日期",
			"type": "string"
		},
		"連載結束": {
			"aliases": [
				"終了号"
			],
			"label": "連載結束",
			"description": "连载结束日期",
			"type": "string"
		},
		"連載網站": {
			"aliases": [
				"連載網絡",
				"连载网络"
			],
			"label": "連載網站",
			"description": "网络连载网站",
			"type": "string"
		},
		"發行日期": {
			"aliases": [
				"発行日"
			],
			"label": "發行日期",
			"description": "作品发行日期（宣布出版）",
			"type": "string"
		},
		"發售日": {
			"aliases": [
				"発売日"
			],
			"label": "發售日",
			"description": "发售日（开始公开发售）",
			"type": "string"
		},
		"冊數": {
			"aliases": [
				"巻数",
				"冊数",
				"volumes"
			],
			"label": "冊數",
			"description": "单行本或合集本数",
			"type": "string"
		},
		"其他": {
			"aliases": [
				"その他"
			],
			"label": "其他",
			"description": "其他补充信息",
			"type": "string"
		},
		"開始": {
			"label": "開始",
			"description": "单一卷-{}-发表开始日期",
			"type": "string"
		},
		"結束": {
			"aliases": [
				"終了"
			],
			"label": "結束",
			"description": "单一卷结束日期",
			"type": "string"
		},
		"版權": {
			"aliases": [
				"Copyright",
				"コピーライト"
			],
			"label": "版權",
			"description": "作品版权声明",
			"type": "string"
		}
	},
	"format": "block",
	"paramOrder": [
		"輕小說",
		"標題",
		"image",
		"size",
		"caption",
		"原作",
		"著者",
		"插圖",
		"出版社",
		"其他出版社",
		"連載雜誌",
		"label",
		"發行日期",
		"發售日",
		"連載號",
		"連載開始",
		"連載結束",
		"連載網站",
		"冊數",
		"開始",
		"結束",
		"話数",
		"其他",
		"版權"
	]
}
</templatedata>
[[Category:Infobox animanga|N]]
</noinclude>