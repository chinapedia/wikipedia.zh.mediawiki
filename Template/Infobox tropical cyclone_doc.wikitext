{{Documentation subpage}}
<!-- Place categories where indicated at the bottom of this page and interwikis at Wikidata (see [[Wikipedia:Wikidata]]) -->
{{intricate}}

==使用方法==

===普通用法===
<pre style="overflow:auto">{{Infobox hurricane
| name          = 
| basin         = <!-- Enter one: Atl, EPac, WPac, NIO, SWI, Aus, SPac (see [[Tropical cyclone basins]]) -->
| image         = <!-- filename only -->
| caption       = 
| formed        = <!-- {{start date|yyyy|mm|dd}} -->
| dissipated    = <!-- {{end date|yyyy|mm|dd}} -->
| extratropical = <!-- {{start date|yyyy|mm|dd}} -->
| remnant low   = <!-- {{start date|yyyy|mm|dd}} -->
| 1-min winds   = <!-- in knots, number only -->
| 3-min winds   = <!-- in knots, number only -->
| 10-min winds  = <!-- in knots, number only -->
| gusts         = <!-- in knots, number only -->
| pressure      = <!-- in mbar (hPa), number only -->
| fatalities    = 
| damages       = 
| affected      = 
| cycloneseason = 
}}</pre>

===活躍中的風暴===
<pre style="overflow:auto">{{Infobox hurricane
| name           = 
| basin          = <!-- Enter one: Atl, EPac, WPac, NIO, SWI, Aus, SPac (see [[Tropical cyclone basins]]) -->
| image          = <!-- filename only -->
| caption        = 
| formed         = <!-- {{start date|yyyy|mm|dd}} -->
| dissipated     = <!--leave blank until storm ends, then use {{end date|yyyy|mm|dd}} -->
| extratropical  = <!-- {{start date|yyyy|mm|dd}} -->
| remnant low    = <!-- {{start date|yyyy|mm|dd}} -->
| 1-min winds    = <!-- in knots (other units will display automatically) -->
| 3-min winds    = <!-- in knots (other units will display automatically) -->
| 10-min winds   = <!-- in knots (other units will display automatically) -->
| gusts          = <!-- in knots (other units will display automatically) -->
| pressure       = <!-- in mbar (hPa) (other units will display automatically) -->
| fatalities     = 
| damages        = <!-- Cost of damage in pure number form (in USD, unless currency specified) -->
| year           = <!-- year used for damages figure -->
| currency       = <!-- currency used for damages. Use the [[ISO 4217]] currency code (ex. USD, AUD, JPY) -->
| affected       = <!-- Areas affected -->
| cycloneseason  = <!-- link to season article (ex. [[2014 Pacific typhoon season]]) -->
<!-- Remove these after storm has ended -->
| track         = <!-- storm tracking image filename -->
| track_caption = <!-- Caption below tracking map. defaults to "Forecast map" -->
| time          = <!-- current time used for data (give both local and UTC) -->
| location      = <!-- {{Coord|LAT|LONG|type:event|display=inline}}  (set "display=inline,title" if used on a main article for the storm) -->
| movement      = <!-- direction and speed of movement -->
| mainarticle   = <!-- Page name of the main storm article (helpful when infobox used in season articles) -->
}}</pre>

===過去的風暴===
<pre style="overflow:auto">{{Infobox hurricane
| name          = 
| basin         = <!-- Enter one: Atl, EPac, WPac, NIO, SWI, Aus, SPac (see [[Tropical cyclone basins]]) -->
| type          = <!-- Manual entry of minor storm type (ex. Tropical depression, Tropical storm, Subtropical storm) -->
| category      = <!-- (use only if outside the above basins) manual entry of heading colors, see [[Template:Storm colour]] -->
| image         = 
| alt           = 
| caption       = 
| formed        = <!-- {{start date|yyyy|mm|dd}} -->
| dissipated    = <!--leave blank until storm ends, then use {{end date|yyyy|mm|dd}} -->
| extratropical = <!-- {{start date|yyyy|mm|dd}} -->
| remnant low   = <!-- {{start date|yyyy|mm|dd}} -->
| 1-min prefix  = 
| 1-min winds   = <!-- in knots (plain number only, other units will display automatically) -->
| 3-min prefix  = 
| 3-min winds   = <!-- in knots (plain number only, other units will display automatically) -->
| 10-min prefix = 
| 10-min winds  = <!-- in knots (plain number only, other units will display automatically) -->
| gustspre      = <!-- text to display before gusts, eg: <,≤,>,≥ -->
| gusts         = <!-- in knots (plain number only, other units will display automatically) -->
| pressurepre   = <!-- text to display before pressure, eg: <,≤,>,≥ -->
| pressure      = <!-- in mbar (hPa) -->
| pressurepost  = <!-- text to display below pressure, eg: "world record" -->
| fatalities    = 
| damagespre    = 
| damages       = <!-- Cost of damage in pure number form (in USD, unless currency specified) -->
| year          = <!-- year used for damages figure -->
| currency      = <!-- currency used for damages. Use the [[ISO 4217]] currency code (ex. USD, AUD, JPY) -->
| damagespost   = 
| affected      = <!-- Areas affected -->
| misc          = <!-- Additional relevant information not covered by other sections -->
| cycloneseason = <!-- link to season article (ex. [[2014 Pacific typhoon season]]) -->
| series        = 
| related       = 
| mainarticle   = <!-- Page name of the main storm article (helpful when infobox used in season articles) -->
}}</pre>

== Example ==
{{Infobox hurricane
| name          = Hurricane Hugo
| type          = hurricane
| basin         = Atl
| image         = Hurricane Hugo 15 September 1989 1105z.png
| caption       = Hurricane Hugo as a Category 3 hurricane
| formed        = {{start date|1989|09|10}}
| dissipated    = {{end date|1989|09|25}}
| extratropical = {{start date|1989|09|22}}
| 1-min winds   = 140
| pressure      = 918
| damages       = 10000
| year          = 1989
| fatalities    = 107 total <small>(estimated)</small>
| affected      = [[Lesser Antilles]], [[Puerto Rico]], [[Hispaniola]], [[Turks and Caicos Islands]]
| cycloneseason = [[1989 Atlantic hurricane season]]
}}
<pre style="overflow:auto">{{Infobox hurricane
| name          = Hurricane Hugo
| type          = hurricane
| basin         = Atl
| image         = Hurricane Hugo 15 September 1989 1105z.png
| caption       = Hurricane Hugo as a Category 3 hurricane
| formed        = {{start date|1989|09|10}}
| dissipated    = {{end date|1989|09|25}}
| extratropical = {{start date|1989|09|22}}
| 1-min winds   = 140
| pressure      = 918
| damages       = 10000
| year          = 1989
| fatalities    = 107 total <small>(estimated)</small>
| affected      = [[Lesser Antilles]], [[Puerto Rico]], [[Hispaniola]], [[Turks and Caicos Islands]]
| cycloneseason = [[1989 Atlantic hurricane season]]
}}</pre>

== Microformat ==
{{UF-hcal}}

== Parameters ==
{{TemplateData header}}
<templatedata>
{
	"description": "This infobox is for articles about specific [[tropical cyclone]] events (hurricanes, typhoons, tropical storms, tropical depressions)",
	"params": {
		"name": {
			"description": "The name of the storm as given by the RSMC, TCWC, or other meteorological organization with jurisdiction over the region where the storm was at peak intensity. (Capitalize every word.)",
			"type": "string",
			"required": true
		},
		"basin": {
			"description": "[Important!] Code for one of the [[tropical cyclone basins]] that the storm belongs. Enter one: Atl, EPac, WPac, NIO, SWI, Aus, SPac, or leave blank only if rare storm outside of main basins.",
			"type": "string"
		},
		"type": {
			"description": "Manual entry for type of storm if outside one of the basins (\"hurricane\", \"typhoon\" or \"cyclone\"). This parameter will accept everything, but ensure proper capitalization.",
			"type": "string"
		},
		"category": {
			"description": "Manual entry for type header, per [[Template:Storm colour]].",
			"type": "string"
		},
		"image": {
			"description": "[Important!] Location of picture to use",
			"type": "wiki-file-name",
			"aliases": [
				"Image location"
			]
		},
		"alt": {
			"description": "Alternate text for main image, use if file name is not descriptive.",
			"type": "string"
		},
		"caption": {
			"description": "Caption text for main image.",
			"type": "string"
		},
		"image_size": {
			"description": "Do not use this setting unless correcting a specific problem. Images will scale to user preferences.",
			"type": "string"
		},
		"track": {
			"description": "Used for active storms only. File name of storm map or forecast map.",
			"type": "wiki-file-name"
		},
		"track_alt": {
			"description": "Used for active storms only. Alternate text for tracking image, use if file name is not descriptive.",
			"type": "string"
		},
		"track_caption": {
			"description": "Used for active storms only. Caption text for tracking image.",
			"type": "string",
			"default": "Forecast map"
		},
		"formed": {
			"label": "Formed",
			"description": "Date of formation; use {{start date|yyyy|mm|dd}}.",
			"type": "date"
		},
		"dissipated": {
			"label": "Dissipated",
			"description": "Date of storm end; leave blank until storm ends, then add {{end date|yyyy|mm|dd}}.",
			"type": "string"
		},
		"extratropical": {
			"description": "Date storm went [[Extratropical cyclone|Extratropical]], use {{start date|yyyy|mm|dd}}.",
			"type": "date"
		},
		"remnant low": {
			"description": "Date storm degenerated into a [[Post-tropical cyclone|Remnant low]], use {{start date|yyyy|mm|dd}}.",
			"type": "date"
		},
		"10-min winds": {
			"label": "Highest winds",
			"description": "Sustained wind average over a period of 10 minutes (used by most weather agencies) as a pure number. The template will convert appropriately.",
			"type": "number"
		},
		"3-min winds": {
			"label": "Highest winds",
			"description": "Sustained wind average over a period of 3 minute (used by RSMC New Delhi) as a pure number. The template will convert appropriately.",
			"type": "number"
		},
		"1-min winds": {
			"label": "Highest winds",
			"description": "[Important!] Sustained wind average over a period of one minute (used for the Saffir–Simpson hurricane wind scale) as a pure number. The template will convert appropriately.",
			"type": "number"
		},
		"gusts": {
			"label": "Highest winds",
			"description": "[Important!] Gusts in [[Knot (unit)|knots]] as a pure number. The template will convert appropriately.",
			"type": "number"
		},
		"10-min prefix": {
			"label": "Highest winds",
			"description": "Optional text before \"10-min winds\"",
			"type": "string"
		},
		"3-min prefix": {
			"label": "Highest winds",
			"description": "Optional text before \"3-min winds\"",
			"type": "string"
		},
		"1-min prefix": {
			"label": "Highest winds",
			"description": "Optional text before \"1-min winds\"",
			"type": "string"
		},
		"gustspre": {
			"label": "Highest winds",
			"description": "Optional text before \"gusts\"",
			"type": "string"
		},
		"pressurepre": {
			"label": "Lowest pressure",
			"description": "Optional text before \"pressure\"",
			"type": "string"
		},
		"pressure": {
			"label": "Lowest pressure",
			"description": "[Important!] Pressure in mbar (hPa) as a pure number, will be displayed with labels and converted to inHg.",
			"type": "number"
		},
		"pressurepost": {
			"label": "Lowest pressure",
			"description": "Optional text after \"pressure\"",
			"type": "string"
		},
		"fatalities": {
			"label": "Fatalities",
			"description": "Number killed",
			"type": "string"
		},
		"damagespre": {
			"label": "Damages",
			"description": "Optional text before \"damages\"",
			"type": "string"
		},
		"damages": {
			"label": "Damages",
			"description": "Monetary cost of damage given as a pure number.",
			"type": "number"
		},
		"year": {
			"label": "Damages",
			"description": "Year used for damages amount",
			"type": "string"
		},
		"currency": {
			"label": "Damages",
			"description": "Alternative currency used for damage amount (default is USD)",
			"type": "string"
		},
		"damagespost": {
			"label": "Damages",
			"description": "Optional text after \"damages\"",
			"type": "string"
		},
		"affected": {
			"label": "Areas affected",
			"description": "Areas affected by the storm (wikilink to location articles)",
			"type": "wiki-page-name",
			"aliases": [
				"Areas"
			]
		},
		"time": {
			"description": "Used for active storms only. Time of report used for infobox data. Include both local time and UTC.",
			"type": "string"
		},
		"location": {
			"label": "Location",
			"description": "Used for active storms only. The current location of the storm, use {{Coord|LAT|LONG|type:event|display=inline}}  (set \"display=inline,title\" if used on a main article for the storm).",
			"type": "string"
		},
		"movement": {
			"label": "Movement",
			"description": "Speed and direction of storm",
			"type": "string"
		},
		"misc": {
			"aliases": [
				"module"
			],
			"description": "Use for relevant information not covered by other parameters (not typically used)."
		},
		"cycloneseason": {
			"description": "Page with list of other storms this year in the same basin.",
			"type": "wiki-page-name"
		},
		"series": {
			"description": "Other articles related to this storm (used only for major storms),",
			"type": "wiki-page-name"
		},
		"related": {
			"description": "Other related articles. (not typically used)",
			"type": "wiki-page-name"
		},
		"mainarticle": {
			"description": "If this infobox is used in a season article or in a section of some other page, provide a link to the main article for the storm.",
			"type": "wiki-page-name"
		}
	},
	"format": "block"
}
</templatedata>

==See also ==
* {{tl|Infobox earthquake}}
* {{tl|Infobox flood}}
* {{tl|Infobox storm}}
* {{tl|Infobox tornado}}
* [[:Category:需要關注的熱帶氣旋文章]] - used to track certain articles that experience errors using the infobox

<includeonly>{{#ifeq:{{SUBPAGENAME}}|sandbox | |
<!-- Categories below this line, please; interwikis at Wikidata -->
[[Category:氣象學信息框模板|Hurricane]]
[[Category:飓风模板|Hurricane]]
}}</includeonly>