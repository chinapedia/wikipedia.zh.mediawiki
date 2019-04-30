return {
	secondaryModules = {
		[[Module:Syrian_Civil_War_detailed_map|Module:Syrian Civil War detailed map]],
		[[Module:Iraqi_insurgency_detailed_map|Module:Iraqi insurgency detailed map]]
	},
	marks = {
		-- The only marks that belong in this module are those on the Syrian-Iraqi border.
		-- All others belong in one of the above modules.
		{ lat = "36.277", long = "41.281", mark = "Mountain pass 12x12 e.svg", marksize = "20" },
		{ lat = "36.277", long = "41.281", mark = "Dot_yellow_ff4.svg", marksize = "6", label = "[[Umm_al_Jaris_border_crossing|Umm al Jaris border crossing]]", link = "Umm al Jaris border crossing", label_size = "0", position = "top" },
		{ lat = "36.061", long = "41.254", mark = "Mountain pass 12x12 sw.svg", marksize = "20" },
		{ lat = "36.061", long = "41.254", mark = "Map-ctl2-red+yellow.svg", marksize = "6", label = "[[Tal_Sufouq_border_crossing|Tal Sufouq border crossing]]", label_size = "0" },
		{ lat = "35.813", long = "41.367", mark = "Mountain pass 12x12 w.svg", marksize = "18" },
		{ lat = "35.813", long = "41.367", mark = "Location dot red.svg", marksize = "6", label = "[[Tawsin_border_crossing|Tawsin border crossing]]", link = "Tawsin border crossing", label_size = "0", position = "right" },
		{ lat = "35.118", long = "41.205", mark = "Mountain pass 12x12 w.svg", marksize = "18" },
		{ lat = "35.118", long = "41.205", mark = "Location dot black.svg", marksize = "6", label = "[[Tarifaoa_border_crossing|Tarifaoa border crossing]]", link = "Tawsin border crossing", label_size = "0", position = "right" },
		{ lat = "34.407", long = "40.980", mark = "Mountain pass 12x12 se.svg", marksize = "28" },
		{ lat = "34.407", long = "40.980", mark = "Location dot black.svg", marksize = "8", label = "[[Al-Qa'im_border_crossing|Abu Kamal–Al-Qa'im border crossing]]", link = "Al-Qa'im border crossing", label_size = "0", position = "top" },
		{ lat = "34.315", long = "40.631", mark = "Mountain pass 12x12 se.svg", marksize = "18" },
		{ lat = "34.315", long = "40.631", mark = "Location dot black.svg", marksize = "6", label = "[[Baktal_border_crossing|Baktal border crossing]]", link = "Baktal border crossing", label_size = "0", position = "bottom" },
		{ lat = "37.081", long = "42.372", mark = "Mountain pass 12x12 e.svg", marksize = "20" },
		{ lat = "37.081", long = "42.372", mark = "Dot_yellow_ff4.svg", marksize = "7", label = "[[Faysh_Khabur|Semalka border crossing]]", link = "Faysh Khabur", label_size = "75", position = "right" },
		{ lat = "36.807", long = "42.072", mark = "Mountain pass 12x12 se.svg", marksize = "20" },
		{ lat = "36.807", long = "42.072", mark = "Dot_yellow_ff4.svg", marksize = "8", label = "[[Rabia,_Iraq|Yarubiyah–Rabi'ah border crossing]]", link = "Rabia, Iraq", label_size = "0", position = "right" },
        },
	containerArgs = {
		'Syria-Iraq',
		AlternativeMap = 'Syria-Iraq location map1a.png',
		maplink = '',
		float = 'left',
		width = 4500,
		caption = [=['''Hold cursor over location to display name; click to go to location row in the "table of cities and towns" (if available).<br/>Control :  [[File:Location_dot_red.svg|11px]] Government ; [[File:Dot_green_0d0.svg|11px]] main rebels ; [[File:Dot_yellow_ff4.svg|11px]] [[Syrian_Democratic_Forces|Syrian Democratic Forces]] ; [[File:Map-dot-grey-68a.svg|11px]] [[Tahrir_al-Sham|Tahrir al-Sham]] (HTS) ; [[File:Location_dot_black.svg|11px]] [[Islamic_State_of_Iraq_and_the_Levant|Islamic State of Iraq and the Levant]] (ISIL) ; [[File:Location_dot_blue.svg|11px]] Local unaffiliated forces<br />
Rural presence :  [[File:3x3dot-red.svg|11px]]  [[File:3x3dot-lime.svg|11px]]  [[File:3x3dot-yellow.svg|11px]]  [[File:3x3dot-grey.svg|11px]]  [[File:3x3dot-black.svg|11px]]   [[File:4x4dot-red.svg|11px]]  [[File:4x4dot-lime.svg|11px]]  [[File:4x4dot-yellow.svg|11px]]  [[File:4x4dot-grey.svg|11px]]  [[File:4x4dot-black.svg|11px]]<br/>
Contested : [[File:80x80-red-lime-anim.gif|11px]] Gov't/main_rebels ; [[File:80x80-red-yellow-anim.gif|11px]] Gov't/SDF ; [[File:80x80-red-grey-anim.gif|11px]] Gov't/HTS ; [[File:80x80-red-black-anim.gif|11px]] Gov't/ISIL ; [[File:80x80-lime-yellow-anim.gif|11px]] main_rebels/SDF ; [[File:80x80-lime-grey-anim.gif|11px]] main_rebels/HTS ; [[File:80x80-lime-black-anim.gif|11px]] main_rebels/ISIL ; [[File:80x80-yellow-grey-anim.gif|11px]] SDF/HTS ; [[File:80x80-yellow-black-anim.gif|11px]] SDF/ISIL ; [[File:80x80-red-lime-yellow-anim.gif|11px]] 3-way ;<br />
Besieged_one_side : [[File:map-arcNN-red.svg|11px]] [[File:map-arcNN-lime.svg|11px]] [[File:map-arcNN-yellow.svg|11px]] [[File:map-arcNN-grey.svg|11px]] [[File:map-arcNN-black.svg|11px]]  
  [[File:map-arcNE-red.svg|11px]] [[File:map-arcNE-lime.svg|11px]] [[File:map-arcNE-yellow.svg|11px]] [[File:map-arcNE-grey.svg|11px]] [[File:map-arcNE-black.svg|11px]]
  [[File:map-arcEE-red.svg|11px]] [[File:map-arcEE-lime.svg|11px]] [[File:map-arcEE-yellow.svg|11px]] [[File:map-arcEE-grey.svg|11px]] [[File:map-arcEE-black.svg|11px]]
  [[File:map-arcSE-red.svg|11px]] [[File:map-arcSE-lime.svg|11px]] [[File:map-arcSE-yellow.svg|11px]] [[File:map-arcSE-grey.svg|11px]] [[File:map-arcSE-black.svg|11px]]
  [[File:map-arcSS-red.svg|11px]] [[File:map-arcSS-lime.svg|11px]] [[File:map-arcSS-yellow.svg|11px]] [[File:map-arcSS-grey.svg|11px]] [[File:map-arcSS-black.svg|11px]]
  [[File:map-arcSW-red.svg|11px]] [[File:map-arcSW-lime.svg|11px]] [[File:map-arcSW-yellow.svg|11px]] [[File:map-arcSW-grey.svg|11px]] [[File:map-arcSW-black.svg|11px]]
  [[File:map-arcWW-red.svg|11px]] [[File:map-arcWW-lime.svg|11px]] [[File:map-arcWW-yellow.svg|11px]] [[File:map-arcWW-grey.svg|11px]] [[File:map-arcWW-black.svg|11px]]
  [[File:map-arcNW-black.svg|11px]] [[File:map-arcNW-lime.svg|11px]] [[File:map-arcNW-yellow.svg|11px]] [[File:map-arcNW-grey.svg|11px]] [[File:map-arcNW-black.svg|11px]]<br />
Besieged : [[File:map-circle-red.svg|12px]] [[File:map-circle-lime.svg|12px]] [[File:map-circle-yellow.svg|12px]] [[File:map-circle-grey.svg|12px]] [[File:map-circle-black.svg|12px]]   
Military base : [[File:Abm-red-icon.png|13px]] [[File:Abm-lime-icon.png|13px]] [[File:Abm-yellow-icon.png|13px]] [[File:Abm-grey-icon.png|13px]] [[File:Abm-black-icon.png|13px]]   
Airport/Air base (plane) : [[File:Fighter-jet-red-icon.svg|13px]] [[File:Fighter-jet-lime-icon.svg|13px]] [[File:Fighter-jet-yellow-icon.svg|13px]] [[File:Fighter-jet-grey-icon.svg|13px]] [[File:Fighter-jet-black-icon.svg|13px]]   
Heliport/Helicopter base : [[File:Helicopter-red-icon.svg|13px]] [[File:Helicopter-lime-icon.svg|13px]] [[File:Helicopter-yellow-icon.svg|13px]] [[File:Helicopter-grey-icon.svg|13px]] [[File:Helicopter-black-icon.svg|13px]]<br/>
[[File:Anchor_pictogram.svg|12px]] Major port or naval base ; [[File:Mountain_pass_12x12_n.svg|20px]] Border Post ; [[File:Arch_dam_12x12_w.svg|16px]] Dam ; [[File:Gota07.svg|12px]] Oil/gas ; [[File:Icon_NuclearPowerPlant-black.svg|12px]] Industrial complex''' <br>'''2 nested circles: inner controls, outer sieges (or indicates strong enemy pressure) // 3 nested circles: mixed control with stable situation <br>Small icons within large circle: situation in individual neighbourhoods/districts''']=]
	}
}