<noinclude><div class="messagebox standard-talk">使用方法請看[[Template:Infobox animanga]]。</div>
{{lua|Module:Check for unknown parameters}}
{{Infobox_animanga/Top}}
</noinclude>{{Infobox_animanga/Head|[[电影]]|{{{title|{{{標題|{{{タイトル|}}}}}}}}} }}
{{Infobox_animanga/Image|{{{image|{{{圖像|{{{画像|}}}}}}}}}|size={{{尺寸|{{{サイズ|{{{size|}}}}}}}}}|title={{{說明|{{{説明|{{{caption|}}}}}}}}} }}
{{Infobox_animanga/Item|日文名稱|{{{日文名稱|}}}|display=-{<span lang="ja">{{{日文名稱|}}}</span>}-}}
{{Infobox_animanga/Item|英文名稱|{{{英文名稱|}}} }}
{{Infobox_animanga/Item|原案|{{{原案|}}} }}
{{Infobox_animanga/Item|原作|{{{原作|}}} }}
{{Infobox_animanga/Item|總導演|{{{總導演|{{{総監督|}}}}}} }}
{{Infobox_animanga/Item|導演|{{{director|{{{監督|{{{導演|}}}}}}}}} }}
{{Infobox_animanga/Item|編劇|{{{腳本|{{{脚本|{{{劇本|{{{編劇|}}}}}}}}}}}} }}
{{Infobox_animanga/Item|人物原案|{{{人物原案|{{{キャラクター原案|}}}}}} }}
{{Infobox_animanga/Item|人物設定|{{{人物設定|{{{キャラクターデザイン|}}}}}} }}
{{Infobox_animanga/Item|機械設定|{{{機械設定|{{{メカニックデザイン|}}}}}} }}
{{Infobox_animanga/Item|音樂|{{{音樂|{{{音楽|}}}}}} }}
{{Infobox_animanga/Item|音樂製作|{{{studio|{{{音樂製作|{{{音楽制作|}}}}}}}}} }}
{{Infobox_animanga/Item|動畫製作|{{{studio|{{{動畫製作|{{{アニメーション制作|}}}}}}}}} }}
{{Infobox_animanga/Item|製作|{{{studio|{{{制作|{{{製作|}}}}}}}}} }}
{{Infobox_animanga/Item|影片發行|{{{studio|{{{影片發行|}}}}}} }}
{{Infobox_animanga/Collapsible|其他影片發行|{{{其他影片發行|}}} }}
{{Infobox_animanga/Item|代理發行|{{{代理發行|}}} }}
{{Infobox_animanga/Collapsible|其他代理發行|{{{其他代理發行|}}} }}
{{Infobox_animanga/Item|上映日期|{{{release_date|{{{封切日|{{{上映日|}}}}}}}}} }}
{{Infobox_animanga/Item|影片長度|{{{runtime|{{{上映時間|{{{片長|}}}}}}}}} }}
{{Infobox_animanga/Item|預算|{{{預算|{{{budget|}}}}}} }}
{{Infobox_animanga/Item|票房|{{{票房|{{{gross|{{{sales|}}}}}}}}} }}
{{Infobox_animanga/Item|[[電影公映許可證|公映許可]]|{{{公映許可|}}}}}
{{Infobox_animanga/Item|网-{zh-cn:络;zh-hk:絡;zh-tw:路;}-播放|{{{網路|{{{网络|{{{網絡|{{{network|}}}}}}}}}}}}}}
{{Infobox_animanga/Item|其他|{{{其他|{{{その他|}}}}}} }}
{{Infobox_animanga/Item|[[電影分級制度|分级]]|{{{分级|{{{分級|}}}}}} }}
{{Infobox_animanga/Item|版权信息|{{{版權|{{{Copyright|{{{コピーライト|}}}}}}}}}|display=<strong>©</strong>{{{版權|{{{Copyright|{{{コピーライト}}}}}}}}}}}<noinclude>
{{Infobox_animanga/Bottom}}
{{High-use|200+|Template talk:Infobox_animanga}}
{{esoteric}}
<templatedata>
{
	"description": "ACG系列信息系列模板，电影模块",
	"params": {
		"image": {
			"label": "image",
			"type": "string",
			"description": "作品图片，如Logo，海报，不用File:",
			"aliases": [
				"圖像",
				"画像"
			]
		},
		"size": {
			"label": "size",
			"type": "string",
			"description": "图片尺寸",
			"aliases": [
				"尺寸",
				"サイズ"
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
		"日文名稱": {
			"label": "日文名稱",
			"type": "string",
			"description": "作品日文名称"
		},
		"英文名稱": {
			"label": "英文名稱",
			"type": "string",
			"description": "作品英文名称"
		},
		"原案": {
			"label": "原案",
			"type": "string",
			"description": "作品原案"
		},
		"原作": {
			"label": "原作",
			"type": "string",
			"description": "作品原作"
		},
		"人物原案": {
			"label": "人物原案",
			"type": "string",
			"description": "提供人物設定雛形",
			"aliases": [
				"キャラクター原案"
			]
		},
		"人物設定": {
			"label": "人物設定",
			"type": "string",
			"description": "作品人物设定",
			"aliases": [
				"キャラクターデザイン"
			]
		},
		"影片發行": {
			"label": "影片發行",
			"type": "string",
			"description": "作品原地发行"
		},
		"其他影片發行": {
			"label": "其他影片發行",
			"type": "string",
			"description": "作品非原地发行"
		},
		"代理發行": {
			"label": "代理發行",
			"type": "string",
			"description": "作品原地代理发行"
		},
		"其他代理發行": {
			"label": "其他代理發行",
			"type": "string",
			"description": "作品非原地代理发行"
		},
		"票房": {
			"label": "票房",
			"type": "string",
			"description": "票房",
			"aliases": [
				"sales",
				"gross"
			]
		},
		"標題": {
			"aliases": [
				"タイトル",
				"title"
			],
			"label": "標題",
			"description": "作品标题",
			"type": "string"
		},
		"總導演": {
			"aliases": [
				"総監督"
			],
			"label": "總導演",
			"description": "作品总导演",
			"type": "string"
		},
		"導演": {
			"aliases": [
				"監督",
				"director"
			],
			"label": "導演",
			"description": "作品导演",
			"type": "string",
			"required": true
		},
		"脚本": {
			"aliases": [
				"腳本",
				"編劇",
				"劇本"
			],
			"label": "脚本",
			"description": "作品编剧",
			"type": "string"
		},
		"機械設定": {
			"aliases": [
				"メカニックデザイン"
			],
			"label": "機械設定",
			"description": "作品机械设定",
			"type": "string"
		},
		"音樂": {
			"aliases": [
				"音楽"
			],
			"label": "音樂",
			"description": "作品音乐编作",
			"type": "string"
		},
		"音樂製作": {
			"aliases": [
				"音楽制作"
			],
			"label": "音樂製作",
			"description": "作品音乐制作",
			"type": "string"
		},
		"動畫製作": {
			"aliases": [
				"アニメーション制作"
			],
			"label": "動畫製作",
			"description": "动画制作",
			"type": "string"
		},
		"製作": {
			"aliases": [
				"制作"
			],
			"label": "製作",
			"description": "作品制作",
			"type": "string",
			"required": true
		},
		"studio": {
			"label": "studio",
			"description": "非日语或汉语语境下的制作，包括音乐制作、动画制作和发行。",
			"type": "string"
		},
		"上映日": {
			"aliases": [
				"封切日",
				"release_date"
			],
			"label": "上映日",
			"description": "上映日期",
			"type": "string",
			"required": true
		},
		"片長": {
			"aliases": [
				"上映時間",
				"runtime"
			],
			"label": "片長",
			"description": "影片长度",
			"type": "string",
			"required": true
		},
		"分级": {
			"aliases": [
				"分級"
			],
			"label": "分级",
			"description": "在各国的评级",
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
		"网络": {
			"label": "网络",
			"type": "string",
			"description": "网络播放，包括有线电视，网络直播等",
			"aliases": [
				"網路",
				"網絡",
				"network"
			]
		},
		"版權": {
			"aliases": [
				"コピーライト",
				"Copyright"
			],
			"label": "版權",
			"description": "版权说明",
			"type": "string"
		},
		"預算": {
			"aliases": [
				"budget"
			],
			"label": "預算",
			"description": "預算",
			"type": "string"
		},
		"公映許可": {
			"label": "公映許可",
			"type": "string",
			"description": "影片的電影公映許可證，僅用於引進了中國大陸的影片。"
		}
	},
	"paramOrder": [
		"標題",
		"image",
		"size",
		"caption",
		"日文名稱",
		"英文名稱",
		"原案",
		"原作",
		"總導演",
		"導演",
		"脚本",
		"人物原案",
		"人物設定",
		"機械設定",
		"音樂",
		"音樂製作",
		"動畫製作",
		"製作",
		"影片發行",
		"studio",
		"其他影片發行",
		"代理發行",
		"其他代理發行",
		"上映日",
        "公映許可",
		"片長",
		"票房",
		"网络",
		"其他",
		"分级",
		"版權",
		"預算"
	],
	"format": "block"
}
</templatedata>
[[Category:Infobox animanga|M]]
</noinclude>