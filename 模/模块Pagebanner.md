local p = {}
local defaultimage = {
    none = 'Pagebanner default.jpg',
    [""] = 'Pagebanner default.jpg',
    Europe = 'Pagebanner default.jpg',
    ["欧洲"] = 'Pagebanner default.jpg',
    ["歐洲"] = 'Pagebanner default.jpg',
    ["北美洲"] = 'Pagebanner default.jpg',
    ["North America"] = 'Pagebanner default.jpg',
    ["Pagebanner default.jpg"] = 'Pagebanner default.jpg',
    ["中东"] = 'Mena-asia_default_banner.jpg',
    ["中東"] = 'Mena-asia_default_banner.jpg',
    ["Middle East"] = 'Mena-asia_default_banner.jpg',
    ME = 'Mena-asia_default_banner.jpg',
    ["北非"] = 'Mena-asia_default_banner.jpg',
    ["North Africa"] = 'Mena-asia_default_banner.jpg',
    ["亚洲"] = 'Mena-asia_default_banner.jpg',
    ["亞洲"] = 'Mena-asia_default_banner.jpg',
    Asia = 'Mena-asia_default_banner.jpg',
    ["Mena-asia_default_banner.jpg"] = 'Mena-asia_default_banner.jpg',
    ["南美洲"] = 'S-amer africa default banner.jpg',
    ["South America"] = 'S-amer africa default banner.jpg',
    SA = 'S-amer africa default banner.jpg',
    ["非洲"] = 'S-amer africa default banner.jpg',
    Africa = 'S-amer africa default banner.jpg',
    ["S-amer africa default banner.jpg"] = 'S-amer africa default banner.jpg',
    ["加勒比"] = 'Caribbean default banner.jpg',
    Caribbean = 'Caribbean default banner.jpg',
    ["Caribbean default banner.jpg"] = 'Caribbean default banner.jpg',
    ["澳大利亚"] = 'Australia-oceania default banner.jpg',
    ["澳大利亞"] = 'Australia-oceania default banner.jpg',
    Australia = 'Australia-oceania default banner.jpg',
    ["大洋洲"] = 'Australia-oceania default banner.jpg',
    Oceania = 'Australia-oceania default banner.jpg',
    ["Australia-oceania default banner.jpg"] = 'Australia-oceania default banner.jpg',
    ["新西兰"] = 'NZ default banner.jpg',
    ["纽西兰"] = 'NZ default banner.jpg',
    ["新西蘭"] = 'NZ default banner.jpg',
    ["紐西蘭"] = 'NZ default banner.jpg',
    ["New Zealand"] = 'NZ default banner.jpg',
    NZ = 'NZ default banner.jpg',
    ["NZ default banner.jpg"] = 'NZ default banner.jpg',
    ["旅行话题"] = 'TT Banner.jpg',
    ["旅行話題"] = 'TT Banner.jpg',
    ["话题"] = 'TT Banner.jpg',
    ["話题"] = 'TT Banner.jpg',
    ["Travel topic"] = 'TT Banner.jpg',
    Topic = 'TT Banner.jpg',
    TT = 'TT Banner.jpg',
    ["TT Banner.jpg"] = 'TT Banner.jpg',
    ["飞行"] = 'Generic flying banner.jpg',
    ["飛行"] = 'Generic flying banner.jpg',
    Flying = 'Generic flying banner.jpg',
    ["Generic flying banner.jpg"] = 'Generic flying banner.jpg',
    ["潜水"] = 'Default Scuba diving banner.JPG',
    ["潛水"] = 'Default Scuba diving banner.JPG',
    ["Dive guide"] = 'Default Scuba diving banner.JPG',
    Dive = 'Default Scuba diving banner.JPG',
    Diving = 'Default Scuba diving banner.JPG',
    ["Default Scuba diving banner.JPG"] = 'Default Scuba diving banner.JPG',
    ["旅行路线"] = 'Itinerary banner.jpg',
    ["旅行路線"] = 'Itinerary banner.jpg',
    Itinerary = 'Itinerary banner.jpg',
    ["Itinerary banner.jpg"] = 'Itinerary banner.jpg',
    ["会话手册"] = 'Welcome banner.jpg',
    ["會話手冊"] = 'Welcome banner.jpg',
    Phrasebook = 'Welcome banner.jpg',
    ["Welcome banner.jpg"] = 'Welcome banner.jpg',
    ["奥运"] = 'Olympic flag Wikivoyage banner.jpg',
    ["奧運"] = 'Olympic flag Wikivoyage banner.jpg',
    Olympic = 'Olympic flag Wikivoyage banner.jpg',
    ["Olympic flag Wikivoyage banner.jpg"] = 'Olympic flag Wikivoyage banner.jpg',
    ["消歧义页"] = 'Disambiguation banner.png',
    ["消歧義頁"] = 'Disambiguation banner.png',
    Disambiguation = 'Disambiguation banner.png',
    ["Disambiguation banner.png"] = 'Disambiguation banner.png',
}

function p.main(frame)
	args = frame:getParent().args
	entity = mw.wikibase.getEntityObject()
	text = '<div class="noprint"><div class="mf-pagebanner">'
	title = mw.title.getCurrentTitle()
	if title.namespace == 2 then
		text = text .. '<div width="100%" style="background: #0F4D92; color: white; font-size: 110%; padding-left: 10px; padding-top: 3px; padding-bottom: 3px">这是一个维基导游' .. "'''用户页'''。</div>"
	else
		if not (args.novariant or args["不转换"]) then
			text = text .. require("Module:NoteTA").main{ G1 = "地名", G2 = "地区用词" }
		end
	end
	text = text..'<div class="topbanner"><div class="name">'
	text = text..(args.pgname or args["页名"] or args["頁名"] or title.subpageText)
	text = text..'</div><div class="iconbox">'
	disambig = args.disambig or args["消歧义"] or args["消歧義"]
	size = args.size or 25
	if disambig then
		if disambig == 'yes' then
			disambig = title.text
		end
		text = text..'[[Image:Wait_Circle.svg|' .. size .. 'px]]"
	end
	if args.UNESCO or args.unesco or args["世界遗产"] or args["世界遺產"] then
		text = text..'[[Image:WorldHeritageBlanc.svg|' .. size .. 'px]][[Category:联合国教科文组织世界遗产|Category:联合国教科文组织世界遗产]]'
	end
	if args.star or args["明星"] then
		text = text..'[[Image:Cscr-featured.svg|' .. size .. 'px]]'
	end
	if args.otbp or args["曲径通幽"] or args["曲徑通幽"] then
		text = text..'[[Image:Question_Circle.svg|' .. size .. 'px]]'
	end
	if args.dotm or args["目的地"] then
		text = text..'[[Image:Yes_Check_Circle.svg|' .. size .. 'px]]'
	end
	if args.ftt or args["特色话题"] or args["特色話題"] then
		text = text..'[[Image:Writing_Circle.svg|' .. size .. 'px]]'
	end
	text = text..'</div><p>'
	image = args[1]
	if (not image) or defaultimage[image] then
		if entity and entity.claims and entity.claims["P948"] and entity.claims["P948"][1].mainsnak.datavalue.value then
			image = entity.claims["P948"][1].mainsnak.datavalue.value
		else
			image = defaultimage[image or "none"]
		end
	end
	if title.namespace == 0 then
		if image == "Disambiguation banner.png" then
			text = text..'[[Category:使用标准横幅条目|Category:使用标准横幅条目]]'
		elseif args.index then
		elseif entity and entity.claims and entity.claims["P948"] and entity.claims["P948"][1].mainsnak.datavalue.value then
			text = text..'[[Category:使用自定义横幅条目|Category:使用自定义横幅条目]]'
		elseif defaultimage[image] then
			text = text..'[[Category:使用默认横幅条目|Category:使用默认横幅条目]]'
		else
			text = text..'[[Category:使用自定义横幅条目|Category:使用自定义横幅条目]][[Category:维基数据缺少横幅|Category:维基数据缺少横幅]]'
		end
	end
	text = text..'[[File:'..image..'|frameless|1800px'
	if args.caption or args["说明"] or args["說明"] then
		text = text..'|'..(args.caption or args["说明"] or args["說明"])
	end
	text = text..']]<div class="topbanner-toc">'
	if not (args.notoc or args["无目录"] or args["無目錄"]) then
		text = text..'<div class="hlist tocbox-'
		box = args.box or args["目录"] or args["目錄"]
		if box == '白' then
			text = text..'w'
		elseif (box == '灰') or (box == 'gray') or (box == 'grey') then
			text = text..'s'
		else
			text = text..'b'
		end
		text = text..'">__TOC__</div>'
	end
    text = text..'</div></div></div></div>'
	if disambig then
		text = text..'\n:其他同名地点的条目，请见[['..disambig..'_(消歧义)|'..disambig..' (消歧义)]]。'
	end
	return text
end

return p