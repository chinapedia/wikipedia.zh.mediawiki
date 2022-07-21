<noinclude>{{pp-protected|small=yes}}
<div class="messagebox standard-talk">使用方法請看[[Template:Infobox animanga]]。</div>
{{Infobox_animanga/Top}}
</noinclude>{{Infobox_animanga/Head|[[电视剧]]|{{{Title|{{{標題|{{{タイトル|}}}}}}}}}}}
{{Infobox_animanga/Image|{{{image|{{{圖像|{{{画像|}}}}}}}}}|size={{{尺寸|{{{サイズ|{{{size|}}}}}}}}}|title={{{說明|{{{説明|{{{caption|}}}}}}}}}}}
{{Infobox_animanga/Item|原作|{{{原作|}}}}}
{{Infobox_animanga/Item|導演|{{{導演|{{{監督|}}}}}}}}
{{Infobox_animanga/Item|製作|{{{製作|{{{制作|}}}}}}}}
{{Infobox_animanga/Item|腳本|{{{腳本|{{{脚本|}}}}}}}}
{{Infobox_animanga/Item|音樂|{{{音樂|{{{音楽|}}}}}}}}
{{Infobox_animanga/Item|代理發行|{{{代理發行|{{{代理发行|}}}}}}}}
{{Infobox_animanga/Collapsible|其他代理發行|{{{其他代理發行|{{{其他代理发行|}}}}}}}}
{{Infobox_animanga/Item|播放電視台|{{{播放電視台|{{{放送局|}}}}}}}}
{{Infobox_animanga/Item|播放時期|{{{播放開始|{{{放送開始|{{{播放开始}}}}}}}}}|display={{{播放開始|{{{放送開始|{{{播放开始}}}}}}}}}－{{#if:{{{播放結束|}}}{{{放送終了|}}}{{{播放结束|}}}|{{{播放結束|{{{放送終了|{{{播放结束|}}}}}}}}}|播放中}}}}
{{Infobox_animanga/Item|網路|{{{網路|{{{网络|{{{網絡|{{{network|}}}}}}}}}}}}}}
{{Infobox_animanga/Item|集數|{{{話數|{{{話数|}}}}}}}}
{{Infobox_animanga/Item|其他|{{{其他|{{{その他|}}}}}}}}
{{Infobox_animanga/Item|版权信息|{{{版權|{{{Copyright|{{{コピーライト|}}}}}}}}}|display=<strong>©</strong>{{{版權|{{{Copyright|{{{コピーライト}}}}}}}}}}}<noinclude>
{{Infobox_animanga/Bottom}}
{{High-use|100+|Template talk:Infobox_animanga}}
{{esoteric}}
<templatedata>
{
	"description": "ACG系列信息系列模板，电视剧模块",
	"params": {
		"image": {
			"label": "image",
			"type": "string",
			"description": "作品图片，Logo或海报，无需File:",
			"aliases": [
				"圖像",
				"画像"
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
		"代理發行": {
			"label": "代理發行",
			"type": "string",
			"description": "代理发行商",
			"aliases": [
				"代理发行"
			]
		},
		"原作": {
			"label": "原作",
			"type": "string",
			"description": "作品原作"
		},
		"導演": {
			"label": "導演",
			"type": "string",
			"required": true,
			"description": "作品导演",
			"aliases": [
				"監督"
			]
		},
		"制作": {
			"label": "制作",
			"type": "string",
			"required": true,
			"description": "製作單位（公司）",
			"aliases": [
				"製作"
			]
		},
		"腳本": {
			"label": "脚本",
			"type": "string",
			"required": true,
			"description": "腳本",
			"aliases": [
				"脚本"
			]
		},
		"音樂": {
			"label": "音楽",
			"type": "string",
			"description": "音樂",
			"aliases": [
				"音楽"
			]
		},
		"其他代理發行": {
			"label": "其他代理發行",
			"type": "string",
			"description": "他國代理發行商",
			"aliases": [
				"其他代理发行"
			]
		},
		"網絡": {
			"label": "網絡",
			"type": "string",
			"description": "網絡播放，包括有線電視，網絡直播等",
			"aliases": [
				"網路",
				"网络",
				"network"
			]
		},
		"話数": {
			"label": "話数",
			"type": "string",
			"required": false,
			"description": "播放话数",
			"aliases": [
				"話數"
			]
		},
		"播放開始": {
			"aliases": [
				"播放开始",
				"放送開始"
			],
			"label": "播放開始",
			"description": "播放开始日期",
			"type": "string",
			"required": true
		},
		"播放結束": {
			"aliases": [
				"播放结束",
				"放送終了"
			],
			"label": "播放結束",
			"description": "播放结束日期",
			"type": "string"
		},
		"其他": {
			"aliases": [
				"その他"
			],
			"label": "其他",
			"description": "其他说明项目",
			"type": "string"
		},
		"版权": {
			"aliases": [
				"コピーライト",
				"版權",
				"Copyright"
			],
			"label": "版权",
			"description": "版权信息",
			"type": "string"
		},
		"標題": {
			"aliases": [
				"タイトル",
				"Title"
			],
			"label": "標題",
			"description": "作品标题",
			"type": "string"
		},
		"播放電視台": {
			"aliases": [
				"放送局"
			],
			"label": "播放電視台",
			"description": "播放电视台",
			"type": "string",
			"required": true
		}
	},
	"paramOrder": [
		"標題",
		"image",
		"size",
		"caption",
		"原作",
		"導演",
		"制作",
		"腳本",
		"音樂",
		"代理發行",
		"其他代理發行",
		"播放電視台",
		"播放開始",
		"播放結束",
		"網絡",
		"話数",
		"其他",
		"版权"
	],
	"format": "block"
}
</templatedata>

[[Category:Infobox animanga|T]]
</noinclude>