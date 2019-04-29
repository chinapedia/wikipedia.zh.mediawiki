local i18n = {
	errors = {
		["parameter-missing"] = "参数缺失！",
		["collapsible-block-not-closed"] = "折叠单元未闭合！",
		["collapsible-block-not-open"] = "找不到折叠单元开始标记！",
		["collapsible-block-empty"] = "折叠单元不能为空！",
		["collapsible-block-no-first-row"] = "折叠单元没有第一行！",
		["collapsible-block-no-replacement"] = "折单元没有替代！",
		["colspan-less-rows-than-set"] = "行数少于列跨距！",
	},
	["error-categories"] = {
		default = '[[Category:有模块线路图错误的页面|Category:有模块线路图错误的页面]]',
		["text-images"] = '[[Category:使用带文字图片的线路图的页面|Category:使用带文字图片的线路图的页面]]',
		["separate-navbar"] = '[[Category:使用另有导航模板的线路图的页面|Category:使用另有导航模板的线路图的页面]]',
		["missing-text-values"] = '[[Category:使用BSto或BSsrws缺少文字值的页面|Category:使用BSto或BSsrws缺少文字值的页面]]',
		["br-tags"] = '[[Category:使用BSto、BSsplit、BSsrws或BScvt，有br标签的页面|Category:使用BSto、BSsplit、BSsrws或BScvt，有br标签的页面]]',
		["srws"] = '[[Category:使用BSsplit而不是BSsrws的页面|Category:使用BSsplit而不是BSsrws的页面]]',
		["rmr-error"] = '[[Category:有线路图模板错误值的页面|Category:有线路图模板错误值的页面]]'
	},
	text = {
		navbar_mini = true, -- for navbar pos 2 only
		navbar_text = '此线路图：', -- for navbar pos 2 only
		legend_text = '圖例',
		legend = {
			default = '[[Template:Railway line legend',
			track = '[[Template:Railway track legend',
			bus = '[[Template:Bus route legend',
			canal = '[[Template:Waterways legend',
			water = '[[Template:Waterways legend',
			waterway = '[[Template:Waterways legend',
			foot = '[[Template:Trails legend',
			footpath = '[[Template:Trails legend',
			walkway = '[[Template:Trails legend'
		}
	},
	html = {
		["cell-icon-fmt"] = '\
|style="padding:0%s"|[[File:BSicon_%s.svg|x20px]]%s',
		["cell-overlapicon-fmt"] = '<div style="position:absolute;left:0px;top:0px;padding:0%s">[[File:BSicon_%s.svg|x20px]]</div>',
		["cell-icon-fmt-with-overlap"] = '\
|style="padding:0%s"|<div style="position:relative">%s</div><div%s>[[File:BSicon_%s.svg|x20px]]%s</div>',
		["cell-text-fmt"] = '\
|style="padding:0;width:%s;min-width:%s;line-height:20px%s" title="%s"|<%s style="transform:scaleX(.9);line-height:.975;display:inline-block%s">%s%s%s%s</%s>',
		["cell-overlaptext-fmt"] = '<div style="position:absolute;width:%s;min-width:%s;line-height:20px%s" title="%s"><%s style="transform:scaleX(.9);line-height:.975;display:inline-block%s">%s%s%s</%s></div>',
		["cell-text-fmt-with-overlap"] = '\
|style="padding:0%s"|<div style="position:relative">%s</div><div style="width:%s;min-width:%s;line-height:20px%s" title="%s"><%s style="transform:scaleX(.9);line-height:.975;display:inline-block%s">%s%s%s%s</%s></div>',
		["cell-empty-fmt"] = '\n|style="padding:0;width:%s;min-width:%s;height:20px;min-height:20px%s"|%s',
		["cell-empty-fmt-with-overlap"] = '\n|style="padding:0%s"|<div style="position:relative">%s</div><div style="width:%s;min-width:%s;height:20px;min-height:20px%s">%s</div>',

		["cell-filler-fmt"] = '\n|style="padding:0; width:8px"| ||style="padding:0; width:4px; background-color:%s"| ||style="padding:0; width:8px"|',
		["cell-filler-empty-fmt"] = '\n|style="padding:0; width:20px"|',

		["row-linfo4-fmt"] = '\
|style="width:auto;vertical-align:middle;padding:0 3px 0 0;text-align:left;%s"|<div style="display:inline;font-size:90%%;">%s</div>',-- parameters:linfo4-width, linfo4
		["row-linfo3-fmt"] = '<div style="display:inline;font-size:90%%;">%s</div> ',
		["row-rinfo3-fmt"] = ' <div style="display:inline;font-size:90%%;">%s</div>',
		["row-rinfo4-fmt"] = '\
|style="width:auto;vertical-align:middle;padding:0 0 0 3px;text-align:right;%s"|<div style="display:inline;font-size:90%%;">%s</div>',-- parameters:rinfo4-width, rinfo4

		["row-general-fmt"] = '\
|- style="line-height:1" %s\
|colspan="%s" style="width:auto;vertical-align:middle;padding:0;text-align:right;%s"|%s\
|style="font-family:Liberation Mono,Courier New,Courier,Microsoft JhengHei,Microsoft YaHei,monospace;width:auto;vertical-align:middle;text-align:left;padding:0 %s;%s"|<div style="display:inline;font-size:90%%;">%s</div>\
|style="width:auto;padding:0%s"|\
{|cellspacing="0" cellpadding="0" style="display: table; width: unset; line-height: 0; padding:0 !important; margin: 0 auto !important"\
|- style="display:inline-table;%s"%s\
|}\
|style="font-family:Liberation Mono,Courier New,Courier,Microsoft JhengHei,Microsoft YaHei,monospace;width:auto;vertical-align:middle;text-align:right;padding:0 %s;%s"|<div style="display:inline;font-size:90%%;">%s</div>\
|colspan="%s" style="width:auto;vertical-align:middle;padding:0;text-align:left;%s"|%s%s',-- parameters: linfo4-fmt, colspan-left, linfo3+2-width, linfo3+2, linfo1-pad, linfo1-width, linfo1, bg, cells, rinfo1-pad, rinfo1-width, rinfo1, colspan-right, rinfo2+3-width, rinfo2+3, rinfo4-fmt

		["row-collapsible-begin-fmt"] = '\
|- style="line-height:1"\
|colspan="7" style="padding:0 !important;background-color:%s"|\
{|class="%s%s" cellpadding="0" cellspacing="0" style="%s padding:0 !important;vertical-align:middle;margin:0 !important;white-space:nowrap"',-- parameters: bg, "collapsible "/"mw-collapsible mw-", collapse-state, "float:right" / ""

		["row-collapsible-end-fmt"] = '\n|}',

		["row-collapsible-left-button-width"] = '45px',-- 50px is the minimal width for [показать] / [скрыть] button. Use 40px for [show] / [hide]
		["row-collapsible-left-button-fmt"] = '\n! style="padding-right:3px;min-width:%s;%s" |',--parameters: left-button-width, linfo4-width
		["row-collapsible-left-linfo4+3+2-fmt"] = '\
{|cellspacing="0" cellpadding="0" style="line-height:1;width:100%%;padding:0 !important;margin:0 !important"\
|style="width:auto;vertical-align:middle;padding:0 3px 0 1px;text-align:left"| <div style="display:inline;font-size:90%%;">%s</div>\
|style="width:auto;vertical-align:middle;text-align:right"| %s\
|}',-- parameters: linfo4, linfo3+2
		["row-collapsible-right-button-width"] = '45px',-- 72px is the minimal width for [развернуть] / [свернуть] button at 90%. Use 58px for [expand] / [collapse]
		["row-collapsible-right-rinfo2+3+4-fmt"] = '\
{|cellspacing="0" cellpadding="0" style="line-height:1;width:100%%;padding:0 !important;margin:0 !important"\
|style="width:auto;vertical-align:middle;text-align:left"| %s\
|style="width:auto;vertical-align:middle;padding:0 1px 0 3px;text-align:right"| <div style="display:inline;font-size:90%%;">%s</div>\
|}',-- parameters: rinfo2+3, linfo4
		["row-collapsible-right-button-fmt"] = '\n| style="width:auto;vertical-align:middle;padding-left:3px;font-size:90%%;min-width:%s;%s" |',--parameters: right-button-width, rinfo4-width

		["row-collapsible-replace-begin-fmt"] = '\
|- style="line-height:1"\
|colspan="7" style="padding:0 %s"|<div style="position:relative">\
{| cellspacing="0" cellpadding="0" style="position:absolute;margin:0;bottom:0px;%svertical-align:middle;white-space:nowrap;background-color:%s"',-- parameters: "right-button-width 0 0" / "0 0 left-button-width", "right:0px" / "", bg
		["row-collapsible-replace-end-fmt"] = '\n|}</div>',

		["colspan-fmt"] = '%s\n|-\n| colspan="7" style="background-color:%s;text-align:%s;%s"|\n%s',
		["empty-row-fmt"] = '\n|-\n| style="width:auto;padding:0 3px 0 0;%s" |\n| style="width:auto;padding: 0;%s" |\n| style="width:auto;padding:0 %s;%s" |\n| style="width:auto;padding:0" |\n| style="width:auto;padding:0 %s;%s" |\n| style="width:auto;padding:0;%s" |\n| style="width:auto;padding:0 0 0 3px;%s" |'
		}
}
local p,q={},{}

local getArgs = require('Module:Arguments').getArgs

local function makeInvokeFunction(funcName)
	-- makes a function that can be returned from #invoke, using
	-- [[Module:Arguments|Module:Arguments]].
	return function (frame)
		local args = getArgs(frame, {parentOnly = true})
		return p[funcName](args)
	end
end

local function formaterror(key,param)
	local result = string.format(i18n.html['colspan-fmt'], '', '', '', '', '<span class="error">' .. string.format(i18n.errors[key] or (tostring(key) .. ' %s'),
		tostring(param or '')) .. '</span>')
	if mw.site.namespaces[mw.title.getCurrentTitle().namespace].isContent then result = result .. (i18n['error-categories'][key] or i18n['error-categories'].default or '') end
	return result
end

local function RGBbyCode(code)-- RGB codes for BSicon sets at Commons:Category:Icons for railway descriptions/other colors
	local colors = {--       Any changes should be discussed at Commons:Talk:BSicon/Colors
		bahn     = 'BE2D2C', ex          = 'D77F7E',
		u        = '003399', uex         = '6281C0',
		f        = '008000', fex         = '64B164',
		g        = '2CA05A', gex         = '7EC49A',
		azure    = '3399FF', ex_azure    = '99CCFF',
		black    = '000000', ex_black    = '646464',
		blue     = '0078BE', ex_blue     = '64ACD6',
		brown    = '8D5B2D', ex_brown    = 'B89A7F',
		cerulean = '1A8BB9', ex_cerulean = '73B7D3',
		cyan     = '40E0D0', ex_cyan     = '8AEAE1',
		denim    = '00619F', ex_denim    = '649EC3',
		fuchsia  = 'B5198D', ex_fuchsia  = 'D173B8',
		golden   = 'D7C447', ex_golden   = 'E5DA8E',
		green    = '2DBE2C', ex_green    = '7FD67E',
		grey     = '999999', ex_grey     = 'C0C0C0',
		jade     = '53B147', ex_jade     = '95CE8E',
		lavender = '9999FF', ex_lavender = 'C0C0FF',
		lime     = '99CC00', ex_lime     = 'D1E681',
		maroon   = '800000', ex_maroon   = 'B16464',
		ochre    = 'CC6600', ex_ochre    = 'DEA164',
		olive    = '837902', ex_olive    = 'B2AC64',
		orange   = 'FF6600', ex_orange   = 'FF9955',
		pink     = 'F0668D', ex_pink     = 'F4A1B8',
		purple   = '8171AC', ex_purple   = 'B1A8CB',
		red      = 'EF161E', ex_red      = 'F37176',
		ruby     = 'CC0066', ex_ruby     = 'DE64A1',
		saffron  = 'FFAB2E', ex_saffron  = 'FFC969',
		sky      = '069DD3', ex_sky      = '67C2E3',
		steel    = 'A1B3D4', ex_steel    = 'C4CFE3',
		teal     = '339999', ex_teal     = '82C0C0',
		violet   = '800080', ex_violet   = 'B164B1',
		yellow   = 'FFD702', ex_yellow   = 'FFEB81',
	}
	return colors[code] or colors.bahn
end

p.RGBbyCode = makeInvokeFunction('_RGBbyCode')

function p._RGBbyCode(args)
	return RGBbyCode(args[1])
end

local function properties(str)
--str is a combination of properties with following syntax:
--property name=value,property name1=value1,property name2=value2 and so on
	local result = {}
	for i, v in ipairs(mw.text.split(str, ',')) do
		if v then
			local t = mw.text.split(v, '=')
			if string.find(v, '=') then
				t[1] = mw.text.trim(t[1]) --trim parameter names
				table.insert(result, t[1])
				result[t[1]] = t[2] or '' --fill table with pairs "property"="value"
			elseif result[result[i - 1]] then
				table.insert(result, result[i - 1])
				result[result[i]] = result[result[i]]..','..t[1] --if no equals sign then tack t[1] onto the previous result
			else
				table.insert(result, '~~')
			end
		else
			table.insert(result, '~~')
		end
	end
	return result
end

local function positive(x)
	if not x then return nil else x = string.lower(x) end
	if x == 'yes' or x == 'y' or x == '1' or x == 'true' then return 1 end
end

local function negative(x)
	if not x then return nil else x = string.lower(x) end
	if x == 'no' or x == 'n' or x == '0' or x == 'false' then return 0 end
end

local function alignment(x, y, z)
	if not x then return nil end
	local directions = {
		['inherit-left']    = {'l', 'left',},
		['inherit-right']   = {'r', 'right',},
		['top-inherit']     = {'a', 't', 'top',},
		['bottom-inherit']  = {'e', 'b', 'bottom',},
		['top-left']        = {'la', 'tl', 'c4', 'nw', 'top-left', 'topleft',},
		['top-right']       = {'ra', 'tr', 'c1', 'ne', 'top-right', 'topright',},
		['bottom-left']     = {'le', 'bl', 'c3', 'sw', 'bottom-left', 'bottomleft',},
		['bottom-right']    = {'re', 'br', 'c2', 'se', 'bottom-right', 'bottomright',},
		['inherit-center']  = {'c', 'center', 'centre',},
		['middle-inherit']  = {'m', 'middle',},
		['top-center']      = {'ma', 'tc', 'top-center', 'top-centre', 'topcenter', 'topcentre',},
		['bottom-center']   = {'me', 'bc', 'bottom-center', 'bottom-centre', 'bottomcenter', 'bottomcentre',},
		['middle-left']     = {'lm', 'ml', 'middle-left', 'middleleft',},
		['middle-right']    = {'rm', 'mr', 'middle-right', 'middleright',},
		['middle-center']   = {'cm', 'mc', 'middle-center', 'middle-centre', 'middlecenter', 'middlecentre',},
	}
	for k, v in pairs(directions) do
		for _, name in ipairs(v) do
			if x:lower() == name then
				local values = mw.text.split(k, '-')
				if values[1] == 'inherit' then values[1] = y end
				if values[2] == 'inherit' then values[2] = z end
				return values
			end
		end
	end
	return {y, z}
end

local function widths(p)
	local values = {
		['w'] = 160, ['+bs'] = 140, ['bs'] = 120, ['+s'] = 100,
		['s'] = 80, ['+db'] = 70, ['+b'] = 60, ['db'] = 50,
		['b'] = 40, ['+cd'] = 35, ['+d'] = 30, ['+c'] = 25,
		[''] = 20, ['ocd'] = 17.5, ['cd'] = 15, ['od'] = 12.5,
		['d'] = 10, ['oc'] = 7.5, ['c'] = 5, ['o'] = 2.5
	} -- in px
	return values[p]
end

local function cell(icon,overlapIcons,rowProps)--[[

Icon handling. Each icon is defined as in the following example:
icon ID!~overlap icon ID!@image link target
Values for an icon ID containing "*" are treated as text, with the letter(s) before "*" as width prefix(es).
No limit on overlapping icons or text; just separate them by "!~".
Parameters can be added after every object, separated to the left by "!_". This, if there is a link, must be after the link.
Parameters for individual objects in an overlapping stack can also be added, separated to the left by "__".
Unless a link is provided, each cell will have mouseover text indicating its contents.

]]
	local tmp, tmp2, cellProps, iconProps, overlapProps, tmp_sep, link, tracking, icontext, iconpre, width = {}, {}, {}, {}, {}, '', '', ''
	if #overlapIcons > 0 then
		tmp = mw.text.split(overlapIcons[#overlapIcons], '!_')
		if #tmp > 1 then overlapIcons[#overlapIcons], cellProps = tmp[1], properties(tmp[2]) end
		tmp = mw.text.split(overlapIcons[#overlapIcons], '!@')
		overlapIcons[#overlapIcons] = tmp[1]
		if #tmp > 1 then link = tmp[2] end	
		tmp = mw.text.split(icon, '__')
		icon = tmp[1]
		if #tmp > 1 then iconProps = properties(tmp[2]) end
		for i, v in ipairs(overlapIcons) do
			tmp = mw.text.split(v, '__')
			overlapIcons[i] = mw.text.trim(tmp[1])
			if #tmp > 1 then overlapProps[i] = properties(tmp[2]) else overlapProps[i] = {} end
		end
	else
		tmp = mw.text.split(icon, '!_')
		if #tmp > 1 then icon, cellProps = tmp[1], properties(tmp[2]) end
		tmp = mw.text.split(icon, '!@')
		icon = mw.text.trim(tmp[1])
		if #tmp > 1 then link = tmp[2] end
	end
	if #overlapIcons > 0 and icon ~= '' then tmp_sep = '; ' end
	local icontip = mw.text.nowiki(mw.text.unstripNoWiki(icon..tmp_sep..table.concat(overlapIcons, '; ')))
	local textspl = string.find(icon, '%*')
	if textspl then
		icontext = mw.text.trim(mw.ustring.sub(icon, textspl + 1))
		if textspl ~= 1 then iconpre = mw.text.trim(mw.ustring.sub(icon, 1, textspl - 1)) end
	end
	if cellProps.style then cellProps.style = ';'..cellProps.style else cellProps.style = '' end
	cellProps.bg = cellProps.bg or cellProps.background or cellProps.bgcolor
	if cellProps.bg then cellProps.style = cellProps.style..';background:'..cellProps.bg end
	if #overlapIcons > 0 or icontext then
		cellProps._before, cellProps._after = rowProps._before or '', rowProps._after or ''
		cellProps.color = cellProps.color or cellProps.colour ; cellProps.bold = cellProps.bold or cellProps.b ; cellProps.italic = cellProps.italic or cellProps.i or cellProps.it
		if cellProps.color then cellProps.style = cellProps.style..';color:'..cellProps.color end
		if positive(cellProps.italic) then cellProps.style = cellProps.style..';font-style:italic' end
		if positive(cellProps.bold) then cellProps.style = cellProps.style..';font-weight:bold' end
		if not cellProps.fontsize or rowProps.fontsize or cellProps.fontsize == 'info' then
		elseif cellProps.fontsize == 'cmt' or cellProps.fontsize == 'comment' then
			cellProps._before, cellProps._after = '<div style="display:inline;font-size:90%;">', '</div>'
		else
			cellProps.style = cellProps.style..';font-size:'..cellProps.fontsize
		end
		if cellProps.align or rowProps.align then
			rowProps.align = rowProps.align or {'middle', 'center'}
			cellProps.align = alignment(cellProps.align, rowProps.align[1], rowProps.align[2]) or rowProps.align
			cellProps.style, cellProps.textfmt = cellProps.style..';vertical-align:'..cellProps.align[1]..';text-align:'..cellProps.align[2], ';vertical-align:'..cellProps.align[1]
		else
			cellProps.style, cellProps.textfmt = cellProps.style..';vertical-align:middle;text-align:center', ';vertical-align:middle;text-align:center'
		end
	end
	if #overlapIcons > 0 then
		tmp = {}
		for i, v in ipairs(overlapIcons) do
			if i ~= #overlapIcons then link = '' end
			if link and link ~= '' then icontip = link end
			if overlapProps[i].style then overlapProps.style = ';'..overlapProps[i].style else overlapProps.style = '' end
			overlapProps[i].bg = overlapProps[i].bg or overlapProps[i].background or overlapProps[i].bgcolor
			if overlapProps[i].bg then overlapProps.style = overlapProps.style..';background:'..overlapProps[i].bg end
			local tmp_textspl = string.find(v, '%*')
			if tmp_textspl then
				local tmp_icontext, tmp_iconpre = mw.text.trim(mw.ustring.sub(v, tmp_textspl + 1)), ''
				if tmp_textspl ~= 1 then tmp_iconpre = mw.text.trim(mw.ustring.sub(v, 1, tmp_textspl - 1)) end
				overlapProps._before, overlapProps._after = cellProps._before, cellProps._after
				overlapProps[i].color = overlapProps[i].color or overlapProps[i].colour ; overlapProps[i].bold = overlapProps[i].bold or overlapProps[i].b ; overlapProps[i].italic = overlapProps[i].italic or overlapProps[i].i or overlapProps[i].it
				if overlapProps[i].color then overlapProps.style = overlapProps.style..';color:'..overlapProps[i].color end
				if positive(overlapProps[i].italic) then overlapProps.style = overlapProps.style..';font-style:italic' end
				if positive(overlapProps[i].bold) then overlapProps.style = overlapProps.style..';font-weight:bold' end
				if rowProps.fontsize or cellProps.fontsize or overlapProps[i].fontsize == 'info' then
				elseif not overlapProps[i].fontsize then
					overlapProps.style = overlapProps.style..';font-size:10px'
				elseif overlapProps[i].fontsize == 'cmt' or overlapProps[i].fontsize == 'comment' then
					overlapProps._before, overlapProps._after = '<div style="display:inline;font-size:90%;">', '</div>'
				else
					overlapProps.style = overlapProps.style..';font-size:'..overlapProps[i].fontsize
				end
				if overlapProps[i].align or cellProps.align then
					cellProps.align = cellProps.align or {'middle', 'center'}
					overlapProps.align = alignment(overlapProps[i].align, cellProps.align[1], cellProps.align[2]) or cellProps.align
					overlapProps.style, overlapProps.textfmt = overlapProps.style..';vertical-align:'..overlapProps.align[1]..';text-align:'..overlapProps.align[2], ';vertical-align:'..overlapProps.align[1]
				else
					overlapProps.style, overlapProps.textfmt = overlapProps.style..';vertical-align:middle;text-align:center', ';vertical-align:middle;text-align:center'
				end
				if overlapProps[i].abbr then
					overlapProps.tag = {'abbr title="'..string.gsub(overlapProps[i].abbr, '"', '"')..'"', 'abbr'}
				else
					overlapProps.tag = {'div', 'div'}
				end
				width = (widths(tmp_iconpre) or 20)..'px'
				table.insert(tmp, string.format(i18n.html['cell-overlaptext-fmt'], width, width, overlapProps.style, icontip, overlapProps.tag[1], overlapProps.textfmt, overlapProps._before, tmp_icontext, overlapProps._after, overlapProps.tag[2]))
			else
				v = mw.text.trim(v)
				if string.find(v, 'num') then
					if not string.find(v, 'numN%d+') then tracking = tracking..(i18n['error-categories']['text-images'] or i18n['error-categories'].default) end
				end
				table.insert(tmp, string.format(i18n.html['cell-overlapicon-fmt'], overlapProps.style, v, link, icontip))
			end
		end
		if iconProps.style then tmp2[1] = true else iconProps.style = '' end
		iconProps.bg = iconProps.bg or iconProps.background or iconProps.bgcolor
		if iconProps.bg then iconProps.style = iconProps.style..';background:'..iconProps.bg end
		width = widths(icon)
		if width then
			if tmp2[1] then iconProps.style = ';'..iconProps.style end
			return string.format(i18n.html['cell-empty-fmt-with-overlap'], cellProps.style, mw.text.trim(table.concat(tmp)), width..'px', width..'px', iconProps.style, tracking)
		elseif icontext then
			iconProps._before, iconProps._after = cellProps._before, cellProps._after
			iconProps.color = iconProps.color or iconProps.colour ; iconProps.bold = iconProps.bold or iconProps.b ; iconProps.italic = iconProps.italic or iconProps.i or iconProps.it
			if iconProps.color then iconProps.style = iconProps.style..';color:'..iconProps.color end
			if positive(iconProps.italic) then iconProps.style = iconProps.style..';font-style:italic' end
			if positive(iconProps.bold) then iconProps.style = iconProps.style..';font-weight:bold' end
			if rowProps.fontsize or cellProps.fontsize or iconProps.fontsize == 'info' then
			elseif not iconProps.fontsize then
				iconProps.style = iconProps.style..';font-size:10px'
			elseif iconProps.fontsize == 'cmt' or iconProps.fontsize == 'comment' then
				iconProps._before, iconProps._after = '<div style="display:inline;font-size:90%;">', '</div>'
			else
				iconProps.style = iconProps.style..';font-size:'..iconProps.fontsize
			end
			if iconProps.align or cellProps.align then
				cellProps.align = cellProps.align or {'middle', 'center'}
				iconProps.align = alignment(iconProps.align, cellProps.align[1], cellProps.align[2]) or cellProps.align
				iconProps.style, iconProps.textfmt = iconProps.style..';vertical-align:'..iconProps.align[1]..';text-align:'..iconProps.align[2], ';vertical-align:'..iconProps.align[1]
			else
				iconProps.style, iconProps.textfmt = iconProps.style..';vertical-align:middle;text-align:center', ';vertical-align:middle;text-align:center'
			end
			if iconProps.abbr then
				iconProps.tag = {'abbr title="'..string.gsub(iconProps.abbr, '"', '"')..'"', 'abbr'}
			else
				iconProps.tag = {'div', 'div'}
			end
			if tmp2[1] then iconProps.style = ';'..iconProps.style end
			width = (widths(iconpre) or 20)..'px'
			return string.format(i18n.html['cell-text-fmt-with-overlap'], cellProps.style, mw.text.trim(table.concat(tmp)), width, width, iconProps.style, icontip, iconProps.tag[1], iconProps.textfmt, iconProps._before, icontext, iconProps._after, tracking, iconProps.tag[2])
		else
			if iconProps.style ~= '' then iconProps.style = string.gsub(' style="'..iconProps.style..'"', '";', '"', 1) end
			if string.find(icon, 'num') then
				if not string.find(icon, 'numN%d+') then tracking = tracking..(i18n['error-categories']['text-images'] or i18n['error-categories'].default) end
			end
			return string.format(i18n.html['cell-icon-fmt-with-overlap'], cellProps.style, mw.text.trim(table.concat(tmp)), iconProps.style, icon, icontip, tracking)
		end
	end
	width = widths(icon)
	if width then
		return string.format(i18n.html['cell-empty-fmt'], width..'px', width..'px', cellProps.style, tracking)
	else
		if link and link ~= '' then icontip = link end
		if icontext then
			if not cellProps.fontsize and not rowProps.fontsize then cellProps.style = cellProps.style..';font-size:10px' end
			if cellProps.abbr then
				cellProps.tag = {'abbr title="'..string.gsub(cellProps.abbr, '"', '"')..'"', 'abbr'}
			else
				cellProps.tag = {'div', 'div'}
			end
			width = (widths(iconpre) or 20)..'px'
			return string.format(i18n.html['cell-text-fmt'], width, width, cellProps.style, icontip, cellProps.tag[1], cellProps.textfmt, cellProps._before, icontext, cellProps._after, tracking, cellProps.tag[2])
		else
			if string.find(icon, 'num') then
				if not string.find(icon, 'numN%d+') then tracking = tracking..(i18n['error-categories']['text-images'] or i18n['error-categories'].default) end
			end
			return string.format(i18n.html['cell-icon-fmt'], cellProps.style, icon, link, icontip, tracking)
		end
	end
end

local function fillercell(code)
--Creates a 5px-high row.
--Values in icon pattern can only be [blank], d, [BSicon color] or #[hex triplet].
	if code == '' then
		return string.format(i18n.html['cell-filler-empty-fmt'], '20px', '20px')
	elseif code == 'd' then
		return string.format(i18n.html['cell-filler-empty-fmt'], '10px', '10px')
	elseif mw.ustring.sub(code,1,1) == '#' then
		return string.format(i18n.html['cell-filler-fmt'], code)
	else
		return string.format(i18n.html['cell-filler-fmt'], '#'..RGBbyCode(code))
	end
end

local function row(pattern,noformatting,filler)--[[

Row handling. Each row looks like the following:
row properties~~linfo4~~linfo3~~linfo2~~linfo1! !(icon pattern)~~rinfo1~~rinfo2~~rinfo3~~rinfo4~~row properties

]]
	local result = {['linfo4'] = '', ['linfo3+2'] = '', ['linfo1'] = '', rowstyle = '', ['cells'] = {}, ['rinfo1'] = '', ['rinfo2+3'] = '', ['rinfo4'] = '', ['rowProp'] = {}}
	local lcolspan, rcolspan, linfo4_fmt, rinfo4_fmt = '2', '2', '', ''
	local left, right, icons, overlapIcons, tmp = {}, {}, {}, {}, mw.text.split(pattern, '! !')
	if #tmp > 1 then--splitting the pattern by '! !'
		left = tmp[1] ; right = tmp[2]
	else
		left = '' ; right = tmp[1] or ''
	end

	tmp = mw.text.split(left, '~~')--analysing the left part
	if #tmp > 1 then--if there are several ~~
		result['linfo1'] = mw.getCurrentFrame():preprocess(mw.text.trim(tmp[#tmp]))
		result['linfo3+2'] = mw.text.trim(tmp[#tmp - 1])
		if #tmp > 2 then
			tmp[#tmp - 2] = mw.text.trim(tmp[#tmp - 2])
			if tmp[#tmp - 2] ~= '' then result['linfo3+2'] = string.format(i18n.html['row-linfo3-fmt'], tmp[#tmp - 2]) .. result['linfo3+2'] end
			if #tmp > 3 then
				tmp[#tmp - 3] = mw.text.trim(tmp[#tmp - 3])
				if tmp[#tmp - 3] ~= '' then
					result['linfo4'] = mw.getCurrentFrame():preprocess(tmp[#tmp - 3])
					lcolspan = '1'
					linfo4_fmt = string.format(i18n.html['row-linfo4-fmt'], '', result['linfo4'])
				end
				if #tmp > 4 then result.rowProp = properties(mw.text.trim(tmp[#tmp - 4])) end
			end
		end
	else--assume only linfo2 was provided.
		result['linfo3+2'] = mw.text.trim(tmp[1])
	end
	result['linfo3+2'] = mw.getCurrentFrame():preprocess(result['linfo3+2'])--expand possible templates in info.

	tmp = mw.text.split(right, '~~')--analysing the right part
	if #tmp > 2 then
		result['rinfo1'] = mw.getCurrentFrame():preprocess(mw.text.trim(tmp[2]))
		result['rinfo2+3'] = mw.text.trim(tmp[3])
		if #tmp > 3 then
			tmp[4] = mw.text.trim(tmp[4])
			if tmp[4] ~= '' then result['rinfo2+3'] = result['rinfo2+3'] .. string.format(i18n.html['row-rinfo3-fmt'], tmp[4]) end
			if #tmp > 4 then
				tmp[5] = mw.text.trim(tmp[5])
				if tmp[5] ~= '' then
					result['rinfo4'] = mw.getCurrentFrame():preprocess(tmp[5])
					rcolspan = '1'
					rinfo4_fmt = string.format(i18n.html['row-rinfo4-fmt'], '', result['rinfo4'])
				end
				if #tmp > 5 then result.rowProp = properties(mw.text.trim(tmp[6])) end
			end
		end
	else--assume only rinfo2 was provided.
		result['rinfo2+3'] = mw.text.trim(tmp[2] or '')
	end
	result['rinfo2+3'] = mw.getCurrentFrame():preprocess(result['rinfo2+3'])

-- The below parameter functions are passed through to the cells.
	if result.rowProp.fontsize == 'cmt' or result.rowProp.fontsize == 'comment' then
		result.rowProp._before, result.rowProp._after = '<span style="font-size:90%;">', '</span>'
	end
	if result.rowProp.align then
		result.rowProp.align = alignment(result.rowProp.align, 'middle', 'center') or {'middle', 'center'}
	end

	icons = mw.text.split(tmp[1], '\\')--splitting the string of icons first by "\"
	if type(filler) == 'string' then
		result.style = ';font-size:0px'
		result.rowstyle = 'height:' .. filler .. ';min-height:' .. filler --row parameter before any cells
		for i, v in ipairs(icons) do table.insert(result['cells'], fillercell(v)) end--no !@ or !~ for filler row
	else
		result.style = ''
		for i, v in ipairs(icons) do
			tmp = mw.text.split(v, '!~')
			icons[i] = tmp[1]
			table.remove(tmp, 1)
			table.insert(overlapIcons, tmp)
		end
		for i, v in ipairs(icons) do table.insert(result['cells'], cell(v, overlapIcons[i], result.rowProp)) end
	end
	result['cells'] = table.concat(result['cells'])
	if result.rowProp.style then result.style = result.style..';'..result.rowProp.style end
	result.rowProp.bg = result.rowProp.bg or result.rowProp.background or result.rowProp.bgcolor ; result.rowProp.color = result.rowProp.color or result.rowProp.colour ; result.rowProp.bold = result.rowProp.bold or result.rowProp.b ; result.rowProp.italic = result.rowProp.italic or result.rowProp.i or result.rowProp.it
	if result.rowProp.bg then result.style = result.style..';background:'..result.rowProp.bg end
	if result.rowProp.color then result.style = result.style..';color:'..result.rowProp.color end
	if positive(result.rowProp.italic) then result.style = result.style..';font-style:italic' end
	if positive(result.rowProp.bold) then result.style = result.style..';font-weight:bold' end
	if result.rowProp.align then
		result.style = result.style..';vertical-align:'..result.rowProp.align[1]..';text-align:'..result.rowProp.align[2]
	else
		result.style = result.style..';vertical-align:middle;text-align:center'
	end
	if result.rowProp.fontsize and result.rowProp._after == '' and result.rowProp.fontsize ~= 'info' then
		result.style = result.style..';font-size:'..result.rowProp.fontsize
	end
	if noformatting then
		return result
	else
		return string.format(i18n.html['row-general-fmt'], linfo4_fmt, lcolspan, '', result['linfo3+2'], q.linfo1_pad, '', result['linfo1'], result.style, result.rowstyle,
			result['cells'], q.rinfo1_pad, '', result['rinfo1'], rcolspan, '', result['rinfo2+3'], rinfo4_fmt)
	end
end

--↓ This table handles diagram rows beginning with a hyphen ("-").
q = {collapsibles = -1, text_width = {'', '', '', '', '', ''}, linfo1_pad = '3px', rinfo1_pad = '3px', bg = '#F9F9F9'}
q.isKeyword = function(pattern, i, rows, justTest)
	if mw.ustring.sub(pattern, 1, 1) ~= '-' then if justTest then return false else return nil end end--not a valid keyword
	local tmp = mw.text.split(string.sub(pattern, 2), '%-')
	if type(q[tmp[1]])=="function" and tmp[1] ~= 'isKeyword' then
		if justTest then return tmp[1] else return q[tmp[1]](tmp, i, rows) end--valid keyword
	else
		if justTest then return false else return nil end
	end
end
q['startCollapsible'] = function(params, i, rows)
	table.remove(rows, i)
	local tmp = q.isKeyword(rows[i], i, rows, true)
	if tmp then
		if tmp == 'endCollapsible' then return formaterror('collapsible-block-empty')
		else return formaterror('collapsible-block-no-first-row') ..  q.isKeyword(rows[i], i, rows) --no valid keywords that can follow "startCollapsible"
		end
	end
	if q.collapsibles == -1 then q.collapsibles = 1 else q.collapsibles = q.collapsibles + 1 end--q.collapsibles == -1 means there are no collapsibles at all; 0 - all closed; >0 - some not closed
	local collapsed, replace, props = params[2], params[3] or '', properties(table.concat(params, '-', 4))--params[1] is the keyword name so all indices are shifted by one.
	if collapsed == nil or collapsed == '' then collapsed = 'collapsed' end
	if props.bg == nil or props.bg == '' then props.bg = 'transparent' ; props['bg-replace'] = q.bg else props['bg-replace'] = props.bg end
	local mode, float, result
	if q.rinfo1_pad == '' then mode = 'collapsible ' ; float = 'float:right;'
	else mode = 'mw-collapsible mw-' ; float = ''
	end
	result = string.format(i18n.html["row-collapsible-begin-fmt"], props.bg, mode, collapsed, float)
	tmp = row(rows[i], true, nil)
	local linfo4_3_2_fmt, rinfo2_3_4_fmt = '', ''
	if q.rinfo1_pad == '' then
		if tmp['linfo4'] ~= '' or tmp['linfo3+2'] ~= '' then linfo4_3_2_fmt = string.format(i18n.html['row-collapsible-left-linfo4+3+2-fmt'], tmp['linfo4'], tmp['linfo3+2']) end
		result = result .. string.format(i18n.html['row-general-fmt'], string.format(i18n.html['row-collapsible-left-button-fmt'], i18n.html['row-collapsible-left-button-width'], q.text_width[1]),
			'1', q.text_width[2], linfo4_3_2_fmt, q.linfo1_pad, q.text_width[3], tmp['linfo1'], tmp.style, '', tmp['cells'], '', '', '', '1', '', '', string.format(i18n.html['row-rinfo4-fmt'], '', ''))
	else
		if tmp['rinfo4'] ~= '' or tmp['rinfo2+3'] ~= '' then rinfo2_3_4_fmt = string.format(i18n.html['row-collapsible-right-rinfo2+3+4-fmt'], tmp['rinfo2+3'], tmp['rinfo4']) end
		result = result .. string.format(i18n.html['row-general-fmt'], string.format(i18n.html['row-linfo4-fmt'], q.text_width[1], tmp['linfo4']),
			'1', q.text_width[2], tmp['linfo3+2'], q.linfo1_pad, q.text_width[3], tmp['linfo1'], tmp.style, '', tmp['cells'], q.rinfo1_pad, q.text_width[4], tmp['rinfo1'],
			'1', q.text_width[5], rinfo2_3_4_fmt, string.format(i18n.html['row-collapsible-right-button-fmt'], i18n.html['row-collapsible-right-button-width'], q.text_width[6]))
	end
	if replace ~= '' then
		if q.isKeyword(rows[i + 1], i, rows, true) then return result .. formaterror('collapsible-block-no-replacement') end--a plain row needed for replacement
		table.remove(rows, i)
		tmp = row(rows[i], true, nil)
		local padding, right = i18n.html['row-collapsible-right-button-width'] .. ' 0 0', ''
		if q.rinfo1_pad == '' then padding = '0 0 ' .. i18n.html['row-collapsible-left-button-width'] ; right = 'right:0px;' end
		result = result .. string.format(i18n.html['row-collapsible-replace-begin-fmt'], padding, right, props['bg-replace'])
		linfo4_3_2_fmt = '' ; rinfo2_3_4_fmt = ''
		if q.rinfo1_pad == '' then
			if tmp['linfo4'] ~= '' or tmp['linfo3+2'] ~= '' then linfo4_3_2_fmt = string.format(i18n.html['row-collapsible-left-linfo4+3+2-fmt'], tmp['linfo4'], tmp['linfo3+2']) end
			result = result .. string.format(i18n.html['row-general-fmt'], string.format(i18n.html['row-linfo4-fmt'], '', ''), '1', q.text_width[2], linfo4_3_2_fmt,
				q.linfo1_pad, q.text_width[3], tmp['linfo1'], tmp.style, '', tmp['cells'], '', '', '', '1', '', '', string.format(i18n.html['row-rinfo4-fmt'], '', ''))
		else
			if tmp['rinfo4'] ~= '' or tmp['rinfo2+3'] ~= '' then rinfo2_3_4_fmt = string.format(i18n.html['row-collapsible-right-rinfo2+3+4-fmt'], tmp['rinfo2+3'], tmp['rinfo4']) end
			result = result .. string.format(i18n.html['row-general-fmt'], string.format(i18n.html['row-linfo4-fmt'], q.text_width[1], tmp['linfo4']), '1', q.text_width[2],
				tmp['linfo3+2'], q.linfo1_pad, q.text_width[3], tmp['linfo1'], tmp.style, '', tmp['cells'], q.rinfo1_pad, q.text_width[4], tmp['rinfo1'], '1', q.text_width[5],
				rinfo2_3_4_fmt, string.format(i18n.html['row-rinfo4-fmt'], '', ''))
		end
		result = result .. i18n.html['row-collapsible-replace-end-fmt']
	end
	return result
end
q['endCollapsible'] = function(params, i, rows)
	if q.collapsibles > 0 then
		q.collapsibles = q.collapsibles - 1
		return i18n.html['row-collapsible-end-fmt']
	else
		return formaterror('collapsible-block-not-open')
	end
end
q['colspan'] = function(params, i, rows)
	if params[2] == 'end' then return '' end
	local tmp, j, nrows, props = {}, 0, tonumber(params[2]), properties(table.concat(params, '-', 3))
	if nrows ~= 0 then table.remove(rows, i) end
	if nrows == nil then nrows = #rows - i + 1 end
	while j < nrows and i <= #rows do
		j = j + 1
		if rows[i] == '-colspan-end'  then
			j = nrows
		else
			table.insert(tmp, rows[i])
		end
		if nrows ~= j or i == #rows then table.remove(rows, i) end
	end
	if j < nrows then j = formaterror('colspan-less-rows-than-set',j) else j = '' end
	return string.format(i18n.html['colspan-fmt'], j, props.bg or '', props.align or '', props['style'] or '', mw.getCurrentFrame():preprocess(table.concat(tmp, '\n')))
end
q['filler'] = function(params, i, rows)
	local tmp, height = table.concat(params, '-', 3), '5px'
	if #params < 3 or tmp == '' then return formaterror('parameter-missing') end--TODO: specify the name of the parameter
	if params[2] ~= '' then height = params[2] end
	return row(tmp, nil, height)
end

function p.RGBbyCode(frame)
	return RGBbyCode(mw.text.trim(frame.args[1] or ''))
end

local function localroute(pattern,ptw,pbg,process)
	local tmp = {}
	if mw.text.trim(pbg) ~= '' then q.bg = pbg end
	tmp = mw.text.split(mw.text.trim(ptw), '%s*,%s*')
	if #tmp == 6 then
		for i = 1, 6 do
			if tmp[i] ~= '' then
				if tonumber(string.sub(tmp[i],-1)) then
					q.text_width[i] = 'width:' .. tmp[i] .. 'px;min-width:' .. tmp[i] .. 'px;'
				else
					q.text_width[i] = 'width:' .. tmp[i] .. ';min-width:' .. tmp[i] .. ';'
				end
			end
		end
		if tmp[4] == '' and tmp[5] == '' and tmp[6] == '' then
			q.rinfo1_pad = ''--padding for rinfo1 column = 0, not 3px
		elseif tmp[1] == '' and tmp[2] == '' and tmp[3] == '' then
			q.linfo1_pad = ''
		end--padding for linfo1 column = 0, not 3px
	elseif #tmp == 3 then
		for i = 1, 3 do
			if tmp[i] ~= '' then
				if tonumber(string.sub(tmp[i],-1)) then
					q.text_width[i + 3] = 'width:' .. tmp[i] .. 'px;min-width:' .. tmp[i] .. 'px;'
				else
					q.text_width[i + 3] = 'width:' .. tmp[i] .. ';min-width:' .. tmp[i] .. ';'
				end
			end
		end
		q.linfo1_pad = ''
	elseif #tmp == 1 and tmp[1] ~= '' then
		if tonumber(string.sub(tmp[1],-1)) then
			q.text_width[5] = 'width:' .. tmp[1] .. 'px;min-width:' .. tmp[1] .. 'px;'
		else
			q.text_width[5] = 'width:' .. tmp[1] .. ';min-width:' .. tmp[1] .. ';'
		end
		q.linfo1_pad = ''
	end
	for i = 1, 6 do
		tmp = tonumber(mw.ustring.match(q.text_width[i], ':([0-9]+%.?[0-9]*)px;'))
		if tmp then
			tmp = tmp*3/40
			q.text_width[i] = 'width:' .. tmp .. 'em;min-width:' .. tmp .. 'em;'
		end
	end
	tmp = {}
	
	local index = 0
	local rows = {}
	if not process or process == '' or negative(process) then
		pattern = mw.ustring.gsub(pattern, '\n(#[0-9a-fA-F][0-9a-fA-F][0-9a-fA-F])', '%1')
	end
	for item in pattern:gmatch('([^\n]*)\n?') do
		item = mw.text.trim(item)
		if item ~= '' then
			index = index + 1
			rows[index] = item
		end
	end
	if index == 0 then return formaterror('parameter-missing') end
	for i, v in ipairs(rows) do
		local keyword = q.isKeyword(v, i, rows)
		if type(keyword) ~= "string" then
			table.insert(tmp, row(v, nil, nil))
		else
			table.insert(tmp, keyword)
		end
	end

	if q.collapsibles > 0 then table.insert(tmp, formaterror('collapsible-block-not-closed') .. q['endCollapsible']()) end
	if q.collapsibles ~= -1 then
		if q.rinfo1_pad == '' then
			q.text_width[1] = q.text_width[1] .. 'min-width:' .. i18n.html['row-collapsible-left-button-width'] .. ';'
		else
			q.text_width[6] = q.text_width[6] .. 'min-width:' .. i18n.html['row-collapsible-right-button-width'] .. ';' 
		end
	end
	-- ↓ empty row to set column widths; ↑ if q.collapsibles ≠ -1 and there are collapsible sections, leftmost or rightmost column should be wide enough to accomodate the button
	table.insert(tmp, string.format(i18n.html['empty-row-fmt'], q.text_width[1], q.text_width[2], q.linfo1_pad, q.text_width[3], q.rinfo1_pad, q.text_width[4], q.text_width[5], q.text_width[6]))
	return table.concat(tmp)
end

function p.route(frame)
	local rows = frame.args.pattern or ''
	local tw = frame.args['text-width'] or frame.args.tw or frame.args['text width'] or ''
	local bg = frame.args.bg or ''
	return localroute(rows,tw,bg)
end

local function getArgNums(prefix, args)
    -- Copied from Module:Infobox on enwiki.
    -- Returns a table containing the numbers of the arguments that exist
    -- for the specified prefix. For example, if the prefix were 'data', and
    -- 'data1', 'data2', and 'data5' existed, this would return {1, 2, 5}.
    local nums = {}
    for k, v in pairs(args) do
        local num = tostring(k):match('^' .. prefix .. '([1-9]%d*)$')
        if num then table.insert(nums, tonumber(num)) end
    end
    table.sort(nums)
    return nums
end

local greatercontrast = require('Module:Color contrast')._greatercontrast
local rgb_black = '#252525' -- class .mw-body in Mediawiki:Common.css

p.infobox = makeInvokeFunction('_infobox')

function p._infobox(args) -- Creates a pretty box.
	args.map1, args.tw, args['map1-title'], args['map1-collapsible'], args['map1-collapse'] = args.map1 or args.map, args.tw or args['text-width'] or args['text width'], args['map1-title'] or args['map-title'], args['map1-collapsible'] or args['map-collapsible'], args['map1-collapse'] or args['map1-collapsed'] or args['map-collapse'] or args['map-collapsed']
	local function map_prefix(x) return 'map'..x end
	local mapnums, prefix = {}
	if args[1] and args[1] ~= '' then
		prefix = tonumber
		for k, v in pairs(args) do
			if type(k) == 'number' then table.insert(mapnums, k) end
		end
	else
		prefix = map_prefix
		mapnums = getArgNums('map', args)
		table.sort(mapnums)
	end
	args['title bg color'] = args['title bg color'] or args['title-bg'] or '#27404E'
	args['title color'] = args['title color'] or args['title-color'] or greatercontrast{args['title bg color'], '#FFF', rgb_black}
	args.legend = args.legend or ''
	local navbar = require('Module:Navbar').navbar
	local navtable = {}
	args.navbar = args.navbar or args.tnavbar
	if args.navbar then
		navtable = {args.navbar, mini = i18n.text.navbar_mini, text = i18n.text.navbar_text}
		args.navbar = navbar(navtable)
	else
		args.navbar = ''
	end
	local result = ''
	if args.inline then result = result..' \n' end
	result = result..'{|'
	args.collapse = args.collapse or args.collapsed
	if args.inline or negative(args.collapsible) then
		args.collapsible = '0'
	else
		result = result .. 'class="collapsible '
		if args.collapse then result = result .. 'collapsed' end
		result = result .. '" '
	end
	args.float = args.float or 'right'
	if args.float == 'right' then
		args.margin = 'margin-left:1em;'
	elseif args.float == 'left' then
		args.margin = 'margin-right:1em;'
	else
		args.margin = ''
	end
	args.fontsize2 = 10000/88
	if args.inline then
		args.inline2 = 'float:none;width:100%;margin:0;border:none;'
		args.fontsize = 100
	else
		args.inline2 = 'box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 1px 5px 0 rgba(0, 0, 0, 0.12), 0 3px 1px -2px rgba(0, 0, 0, 0.2); -moz-box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 1px 5px 0 rgba(0, 0, 0, 0.12), 0 3px 1px -2px rgba(0, 0, 0, 0.2); -webkit-box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 1px 5px 0 rgba(0, 0, 0, 0.12), 0 3px 1px -2px rgba(0, 0, 0, 0.2);'
		args.fontsize = 88 -- as above: CSS rule for .infobox in %
	end
	args.bg = args.bg or '#F9F9F9'
	args.style = args.style or ''
	result = result .. 'cellspacing="0" cellpadding="0" style="float:' .. args.float .. ';clear:' .. args.float .. ';margin-top:0;margin-bottom:1em;' .. args.margin .. 'empty-cells:show;border-collapse:collapse;font-size:' .. args.fontsize .. '%;background:' .. args.bg .. ';' .. args.inline2 .. args.style .. '"'
	args.title = args.title or ''
	if args.inline or args.title == 'no' or args.title == '0' then
	else
		result = result .. '\n! style="color:' .. args['title color'] .. ';background:' .. args['title bg color'] .. ';text-align:center;padding:5px"|'
		if args['navbar pos'] then
			result = result .. '<div>'
		else
			if args.navbar ~= '' then
				navtable.mini = true
				navtable.brackets = true
				navtable.style = 'float:left;margin-right:5px;white-space:nowrap'
				navtable.fontstyle = 'font-size:'..args.fontsize2..'%;color:' .. args['title color']
				args.navbar = navbar(navtable) .. '<div style="margin-left:55px">'
			else
				args.navbar = '<div>'
			end
			result = result .. args.navbar
		end
		result = result .. '<div style="white-space:nowrap;'
		if args.collapsible == '0' and (args['navbar pos'] or args.navbar == '<div>') then
		else
			result = result .. 'margin-right:55px;'
			if args['navbar pos'] or args.navbar == '<div>' then
				result = result .. 'margin-left:55px;'
			end
		end
		result = result .. 'font-size:'..args.fontsize2..'%;">' .. args.title .. '</div></div>'
	end
	args.top = args.top or args['on top']
	if args.top then
		result = result .. '\n|-\n|style="padding:0px 5px;text-align:center;'..(args.topstyle or '')..'"|' .. args.top
	end
	result = result .. '\n|-\n|style="line-height:normal;padding:4px 5px"|'
	if args.navbar ~= '' and args['navbar pos'] == '1' then
		if not positive(args['navbar long']) and not negative(args['navbar mini']) then navtable.mini = true; args.navbar = navbar(navtable) end
		result = result .. '<div style="float:left;padding-right:5px">' .. args.navbar .. '</div>'
	end
	args.legend2 = mw.ustring.lower(args.legend)
	if args.legend2 ~= 'no' and args.legend2 ~= '0' then
		args.legend = i18n.text.legend[args.legend2] or ((args.legend2 ~= '') and ('[['..args.legend) or i18n.text.legend.default)
		args.legend = args.legend .. '|' .. (args['legend alt'] or i18n.text.legend_text) .. ']]'
		result = result .. '<div class="selfreference noprint" style="text-align:right;font-size:90%;">' .. args.legend .. '</div>'
	end
	if args.inline then args.padding2 = '0px' else args.padding2 = '0px 6px' end
	for k, v in ipairs(mapnums) do
		if not mapnums[k + 1] then
			if not args.inline then args.padding2 = '0px 6px 6px' end
		end
		args.ending = ''
		if args['map'..v..'-title'] then
			args.header_margin = '0'
			if k == 1 then args.border_header = 'border-bottom: 5px solid '..args.bg..';' else args.border_header = 'border-top: 5px solid '..args.bg..'; border-bottom: 5px solid '..args.bg..';' end
			if positive(args['map'..v..'-collapsible']) then
				args.header_margin = '0 55px'
				args.ending = '\n|}'
				if positive(args['map'..v..'-collapse']) or positive(args['map'..v..'-collapsed']) then args.map_collapsed = ' mw-collapsed autocollapse' else args.map_collapsed = '' end
				result = result..'\n|-\n|\n{|class="mw-collapsible'..args.map_collapsed..'" cellpadding="0" cellspacing="0" style="display: table; min-width:100%; margin:0 auto;"'
			end
			if args.inline then args.header_style2 = ' style="line-height:normal;"' else args.header_style2 = '' end
			result = result..'\n|-'..args.header_style2..'\n!style="'..args.border_header..'padding:3px 5px; text-align:center; vertical-align:middle; color:'..rgb_black..'; background-color: #EEEEEE" | <div style="margin:'..args.header_margin..';font-size:'..10000/args.fontsize..'%;">'..args['map'..v..'-title']..'</div>'
			args.border_top = ''
		else
			if k == 1 then args.border_top = '' else args.border_top = 'border-top: 5px solid '..args.bg..';' end
		end
		result = result .. '\n|-\n|style="'..args.border_top..'padding:' .. args.padding2 .. '"|\n{|cellpadding="0" cellspacing="0" class="nogrid" style="padding:0px;border:0px;background:transparent;white-space:nowrap;line-height:1.2;font-size:'..(args.fontsize2 * 0.95)..'%;margin:auto"\n'..localroute(args[prefix(v)], (args['tw'..v] or args['text-width'..v] or args['text width'..v] or args.tw or ''), args.bg, args.process)..'\n|}'..args.ending
	end
	args.bottom = args.bottom or args.footnote
	if args.bottom then
		if args.inline then args.padding2 = '6px' else args.padding2 = '0px' end
		result = result .. '\n|-\n|style="line-height:normal;text-align:right;padding:' .. args.padding2 .. ' 5px 5px;'..(args.bottomstyle or args.footnotestyle or '')..'"|' .. args.bottom
		if string.find(args.bottom, '&action=edit') then result = result .. (i18n['error-categories']['separate-navbar'] or i18n['error-categories'].default) end
	end
	if args.navbar ~= '' and args['navbar pos'] == '2' then
		if negative(args['navbar long']) or positive(args['navbar mini']) then navtable.mini = true; args.navbar = navbar(navtable) end
		if args.inline and not args.bottom then args.padding2 = '6px' else args.padding2 = '0px' end
		result = result .. '\n|-\n|style="line-height:normal;padding:' .. args.padding2 .. ' 5px 3px;text-align:center"|' .. args.navbar
	end
	return result .. '\n|}'
end

local function base(t1,t2,link,stn,italic,it,it2,bold,align,style,bg1,bg2,line,fs1,fs2,lh,v1,swap,inp,bs)
--Creates an inline table with two rows of text. Can be used in any Routemap text cell.
--Implemented in the BSsplit, BSto, BSsrws and BScvt templates.
	if not align then
		if bs == 'cvt' then
			align = 'right'
		else
			align = 'inherit'
		end
	end
	style = style or ''
	local result = ' <table cellspacing="0" cellpadding="0" style="font-size:80%; font-weight:inherit; color:inherit; background-color:transparent; margin-top:-2px; margin-bottom:-2px; display:inline-table; vertical-align:middle; text-align:'..align
	if italic or it == 'all' then result = result..';font-style:italic' end
	if bold then result = result..';font-weight:bold' end
	local rowstart = '<tr><td style="text-align:inherit;padding:0;line-height:'
	result = result..';'..style..'">'..rowstart..lh
	if line then result = result..';border-bottom:1px solid gray' end
	local bgpad = ';padding-left:0.5em;padding-right:0.5em'
	local function bgtext(v)
		return ';color:'..greatercontrast{v, '#FFF', rgb_black}
	end
	if bg1 then
		result = result..bgpad..bgtext(bg1)..';background-color:'..bg1
	elseif bg2 then
		result = result..bgpad
	end
	if fs1 then result = result..';font-size:'..fs1 end
	result = result..'">'
	if not t1 or string.find(t1, '^%s*$') then
		if not t2 then t2 = '' end
		if string.find(t2, '<br ?/?>') == nil then t1 = ' ' end
	end
	if not t2 or string.find(t2, '^%s*$') then
		if not t1 then t1 = '' end
		if string.find(t1, '<br ?/?>') == nil then t2 = ' ' end
	end
	if bs == 'srws' then
		if stn then
			link = t1..' '..t2..' '..stn
		else
			link = t1..' '..t2..' railway station'
		end
	elseif bs == 'cvt' then
		local split, floor, outp, v2, mult = mw.text.split, math.floor
		local function trim(x)
			return string.gsub(x, '%s', '')
		end
		local cvt = { -- conversion values
			['mi'] = 1.609344,
			['ch'] = 20.1168,
			['mi;ch'] = 80,
			['m'] = 1 / 0.9144,
			['yd'] = 0.9144,
			['ft'] = 0.3048,
		}
		local sf = { -- 10 ^ floor(log10(cvt[inp]) + 0.5); or 10 ^ floor(log10(cvt[inps[1]] * cvt[inp]) + 0.5) for dual-unit inputs. this corrects the accuracy of result so that it usually has same significant figures
			['mi'] = 1,
			['ch'] = 10,
			['mi;ch'] = 1/100,
			['m'] = 1,
			['yd'] = 1,
			['ft'] = 1/10,
		}
		if not inp then inp = 'mi' end
		inp = string.lower(trim(inp))
		if inp == 'ch' or inp == 'yd' or inp == 'ft' then -- output unit
			outp = 'm'
		elseif inp == 'm' then
			outp = 'yd'
		else
			if inp ~= 'mi;ch' then inp = 'mi' end
			outp = 'km'
		end
		local pos = string.find(v1, '%.')
		if not pos then
			mult = 1
		else
			mult = 10 ^ (string.len(v1) - pos)
		end
		local inps = string.find(inp, ';')
		if inps then
			inps = split(inp, ';')
			if swap then
				t1 = v1..' '..outp
				v1 = tonumber(v1)
				t2 = floor(v1 / cvt[inps[1]])..' '..inps[1]..' '..floor(v1 % cvt[inps[1]] / cvt[inps[1]] * cvt[inp] * mult * sf[inp] + 0.5) / mult / sf[inp]..' '..inps[2]
			else
				v1 = split(trim(v1), ';')
				t1 = v1[1]..' '..inps[1]..' '..v1[2]..' '..inps[2]
				t2 = floor((tonumber(v1[1]) * cvt[inps[1]] + tonumber(v1[2]) * cvt[inps[1]] / cvt[inp]) * mult / sf[inp] + 0.5) / mult * sf[inp]..' '..outp
			end
		else
			if swap then
				v2 = floor(tonumber(v1) / cvt[inp] * mult * sf[inp] + 0.5) / mult / sf[inp]
				inp, outp = outp, inp
			else
				v2 = floor(tonumber(v1) * cvt[inp] * mult / sf[inp] + 0.5) / mult * sf[inp]
			end
			t1 = v1..' '..inp
			t2 = v2..' '..outp
		end
	end
	if t1 then
		if link then
			result = result..'[['..link..'|'..t1..']]'
		else
			result = result..t1
		end
	end
	local rowend = '</td></tr>'
	result = result..rowend..rowstart..lh
	if bg2 then
		result = result..bgpad..bgtext(bg2)..';background-color:'..bg2
	elseif bg1 then
		result = result..bgpad
	end
	if fs2 then result = result..';font-size:'..fs2 end
	if (it ~= 'off' and bs == 'to') or it2 == 'italic' then
		result = result..';font-style:italic'
	elseif it == 'off' then
		result = result..';font-style:normal'
	end
	result = result..'">'
	if t2 then
		if link then
			result = result..'[['..link..'|'..t2..']]'
		else
			result = result..t2
		end
	end
	result = result..rowend..'</table> '
	if bs == 'to' or bs == 'srws' then
		if t1 == ' ' or t2 == ' ' then result = result..(i18n['error-categories']['missing-text-values'] or i18n['error-categories'].default) end
	end
	if string.find(t1, '<br ?/?>') ~= nil or string.find(t2, '<br ?/?>') ~= nil then result = result..(i18n['error-categories']['br-tags'] or i18n['error-categories'].default) end
	if bs == 'split' then
		if link and t1 and t2 then
			if string.find(link, '^'..t1..' '..t2..' ') then result = result..(i18n['error-categories']['srws'] or i18n['error-categories'].default) end
		end
	end
	return result
end

p.BSto = makeInvokeFunction('_BSto')

function p._BSto(args)
	args[3] = args[3] or args.L
	args[4] = args[4] or args.it or args.i
	args[5] = args[5] or args.b
	return base(args[1],args[2],args[3],nil,nil,args[4],nil,args[5],args.align,args.style,args.bg1,args.bg2,args.line,'105%','92%','0.9',nil,nil,nil,'to')
end

p.BSsplit = makeInvokeFunction('_BSsplit')

function p._BSsplit(args)
	args[3] = args[3] or args.L
	args[4] = args[4] or args.it or args.i
	args[5] = args[5] or args.b
	return base(args[1],args[2],args[3],nil,args[4],nil,nil,args[5],args.align,args.style,args.bg1,args.bg2,args.line,'inherit','inherit','0.9',nil,nil,nil,'split')
end

p.BSsrws = makeInvokeFunction('_BSsrws')

function p._BSsrws(args)
	args[3] = args[3] or args.S
	args[4] = args[4] or args.it or args.i
	args[5] = args[5] or args.b
	return base(args[1],args[2],nil,args[3],args[4],nil,nil,args[5],args.align,args.style,args.bg1,args.bg2,args.line,'inherit','inherit','0.9',nil,nil,nil,'srws')
end

p.BScvt = makeInvokeFunction('_BScvt')

function p._BScvt(args)
	return base(nil,nil,nil,nil,nil,nil,args.alt,nil,args.align,args.style,args.bg1,args.bg2,args.line,'inherit','inherit','0.9',args[1],args[2],args['in'],'cvt')
end

p.rmri = makeInvokeFunction('_rmri')

function p._rmri(args)--[[

Displays a blue arrow pointing in one of eight directions.
Implemented in the RoutemapRouteIcon template.

]]
	local directions, result = {
	['Up']         = {'u', 'up'},
	['Down']       = {'d', 'dn', 'down'},
	['Left']       = {'l', 'left'},
	['Right']      = {'r', 'right'},
	['UpperRight'] = {'ur', 'ne', 'c1', 'upperright'},
	['LowerRight'] = {'lr', 'se', 'c2', 'lowerright'},
	['LowerLeft']  = {'ll', 'sw', 'c3', 'lowerleft'},
	['UpperLeft']  = {'ul', 'nw', 'c4', 'upperleft'},
	}
	local d, link, size = args[1], args[2], args[3]
	if not d then
		if args[4] ~= ' ' then d, link, size = args[2], args[3], 's' end
	end
	for k, v in pairs(directions) do
		for _, name in ipairs(v) do
			if d:lower() == name then
				if size == 's' then
					size = '7'
				elseif not size then
					size = '10'
				end
				if not link then link = '' end
				result = '[[File:Arrow_Blue_'..k..'_001.svg|'..size..'px]]'
			end
		end
	end
	if not result then
		return '<span style="color:#f00">Invalid [[Template:RoutemapRoute|Template:RoutemapRoute]] arrow value "<span style="font-style:italic">'..d..'</span>".</span>'..(i18n['error-categories']['rmr-error'] or i18n['error-categories'].default)
	else
		return result
	end
end

p.rmr = makeInvokeFunction('_rmr')

function p._rmr(args)--[[

Displays text between two blue arrows (or to the left/right side of one).
Text can be split with an en dash if entered in both first and second numbered parameters.
Implemented in the RoutemapRoute template.

]]
	args.l = args.l or args.Licon or args.licon or args.L
	args.r = args.r or args.Ricon or args.ricon or args.R
	if args.l then args.l = p._rmri{args.l,args.llink,(args.lsize or args.size),' '}..' ' else args.l = '' end
	if args.r then args.r = ' '..p._rmri{args.r,args.rlink,(args.rsize or args.size),' '} else args.r = '' end
	if args[1] then
		if args[2] then args[1] = args[1]..' – '..args[2] end
	else
		args[1] = args[2] or ''
	end
	if positive(args.enclosed) then
		args.b1, args.b2 = '(', ')'
	else
		args.b1, args.b2 = '', ''
	end
	return args.b1..args.l..args[1]..args.r..args.b2
end

function p.BSrow(frame)
	local args = getArgs(frame, {
		parentOnly = true,
		removeBlanks = false,
	})
	return p._BSrow(args)
end

function p._BSrow(args)--[[

Creates Routemap syntax for a diagram row based on parameters.
Implemented in the RDTr template.

]]
	args.n = tonumber(args.n or '')
	if not args.n then
		local icontotal = getArgNums('', args)
		table.sort(icontotal)
		args.n = icontotal[#icontotal] or 1
	end
	local count, icons, overlaps, overlapCalc = tonumber(args['$count']) or 1, {}, {}, math.log10(args.n)
	local text = (args.text and '*') or ''
	if overlapCalc == math.floor(overlapCalc) then overlapCalc = 10^(overlapCalc) else overlapCalc = 10^(math.floor(overlapCalc) + 1) end
	while count <= args.n do
		local cellparams, overlapn = {}, (string.match(count/overlapCalc, '%.(0+)') or '')..count
		table.insert(icons, (text..(args[count] or '')))
		if args['O'..overlapn] then
			local iconparams, overlapparams, overlapt = {}, {}, {}
			for k, v in pairs({bg = (args['O'..overlapn..'0-bg'] or args['O'..overlapn..'0-background'] or args['O'..overlapn..'0-bgcolor']), color = (args['O'..overlapn..'0-color'] or args['O'..overlapn..'0-colour']), b = (args['O'..overlapn..'0-b'] or args['O'..overlapn..'0-bold']), i = (args['O'..overlapn..'0-i'] or args['O'..overlapn..'0-it'] or args['O'..overlapn..'0-italic']), align = args['O'..overlapn..'0-align'], fontsize = args['O'..overlapn..'0-fontsize'], abbr = args['O'..overlapn..'0-abbr'], style = args['O'..overlapn..'0-style']}) do
				if v then table.insert(iconparams, k..'='..v) end
			end
			if iconparams[1] then icons[count] = icons[count]..'__'..table.concat(iconparams, ',') end
			for k, v in pairs({bg = (args['O'..overlapn..'-bg'] or args['O'..overlapn..'-background'] or args['O'..overlapn..'-bgcolor']), color = (args['O'..overlapn..'-color'] or args['O'..overlapn..'-colour']), b = (args['O'..overlapn..'-b'] or args['O'..overlapn..'-bold']), i = (args['O'..overlapn..'-i'] or args['O'..overlapn..'-it'] or args['O'..overlapn..'-italic']), align = args['O'..overlapn..'-align'], fontsize = args['O'..overlapn..'-fontsize'], abbr = args['O'..overlapn..'-abbr'], style = args['O'..overlapn..'-style']}) do
				if v then table.insert(overlapparams, k..'='..v) end
			end
			if overlapparams[1] then args['O'..overlapn] = args['O'..overlapn]..'__'..table.concat(overlapparams, ',') end
			overlaps = getArgNums('O'..overlapn, args) or {}
			table.sort(overlaps)
			if overlaps[1] then
				for i, v in ipairs(overlaps) do
					overlapparams = {}
					for k, v2 in pairs({bg = (args['O'..overlapn..v..'-bg'] or args['O'..overlapn..v..'-background'] or args['O'..overlapn..v..'-bgcolor']), color = (args['O'..overlapn..v..'-color'] or args['O'..overlapn..v..'-colour']), b = (args['O'..overlapn..v..'-b'] or args['O'..overlapn..v..'-bold']), i = (args['O'..overlapn..v..'-i'] or args['O'..overlapn..v..'-it'] or args['O'..overlapn..v..'-italic']), align = args['O'..overlapn..v..'-align'], fontsize = args['O'..overlapn..v..'-fontsize'], abbr = args['O'..overlapn..v..'-abbr'], style = args['O'..overlapn..v..'-style']}) do
						if v2 then table.insert(overlapparams, k..'='..v2) end
					end
					if overlapparams[1] then args['O'..overlapn..v] = args['O'..overlapn..v]..'__'..table.concat(overlapparams, ',') end
					table.insert(overlapt, text..args['O'..overlapn..v])
				end
				overlaps = '!~'..text..args['O'..overlapn]..'!~'..table.concat(overlapt, '!~')
			else
				overlaps = '!~'..text..args['O'..overlapn]
			end
			icons[count] = icons[count]..overlaps
		else
			if args[count..'-abbr'] then table.insert(cellparams, 'abbr='..args[count..'-abbr']) end
		end
		if args[count..'-link'] then icons[count] = icons[count]..'!@'..args[count..'-link'] end
		for k, v in pairs({bg = (args[count..'-bg'] or args[count..'-background'] or args[count..'-bgcolor']), color = (args[count..'-color'] or args[count..'-colour']), b = (args[count..'-b'] or args[count..'-bold']), i = (args[count..'-i'] or args[count..'-it'] or args[count..'-italic']), align = args[count..'-align'], fontsize = args[count..'-fontsize'], style = args[count..'-style']}) do
			if v then table.insert(cellparams, k..'='..v) end
		end
		if cellparams[1] then icons[count] = icons[count]..'!_'..table.concat(cellparams, ',') end
		count = count + 1
	end
	local row, rowparams, left, right = table.concat(icons, '\\'), {}
	for k, v in pairs({bg = (args.bg or args.background or args.bgcolor), color = (args.color or args.colour), b = (args.b or args.bold), i = (args.i or args.it or args.italic), align = args.align, fontsize = args.fontsize, style = args.style}) do
		if v then table.insert(rowparams, k..'='..v) end
	end
	if rowparams[1] then args.R5 = table.concat(rowparams, ',') end
	for i, v in ipairs({'R1', 'R2', 'R3', 'R4', 'R5', 'L1', 'L2', 'L3', 'L4'}) do
		if not args[v] or string.find(args[v], '^%s*$') then args[v] = nil end
	end
	if args.R5 then
		right = {(args.R1 or ' '), (args.R2 or ' '), (args.R3 or ' '), (args.R4 or ' '), args.R5}
	elseif args.R4 then
		right = {(args.R1 or ' '), (args.R2 or ' '), (args.R3 or ' '), args.R4}
	elseif args.R3 then
		right = {(args.R1 or ' '), (args.R2 or ' '), args.R3}
	elseif args.R1 then
		right = {args.R1, (args.R2 or '')}
	elseif args.R2 then
		right = {args.R2}
	end
	if right then row = row..'~~'..table.concat(right, '~~') end
	if args.L4 then
		left = {args.L4, (args.L3 or ' '), (args.L2 or ' '), (args.L1 or '')}
	elseif args.L3 then
		left = {args.L3, (args.L2 or ' '), (args.L1 or '')}
	elseif args.L1 then
		left = {(args.L2 or ''), args.L1}
	elseif args.L2 then
		left = {args.L2}
	end
	if left then row = table.concat(left, '~~')..'! !'..row end
	return row
end

function p.BSrow_lite(frame)
	local args = getArgs(frame, {
		removeBlanks = false,
	})
	return p._BSrow_lite(args)
end

function p._BSrow_lite(args)--[[

Creates Routemap syntax for a diagram row based on parameters.
Simplified version; an in-app upgrade to the full version costs US$0.99.
Intended to be used to substitute legacy templates.
Note that for compatibility the link and sidebar parameter names are different.

]]
	args.n = tonumber(args.n or '')
	if not args.n then
		local icontotal = getArgNums('', args)
		table.sort(icontotal)
		args.n = icontotal[#icontotal] or 1
	end
	local count, icons, overlaps, overlapCalc = tonumber(args['$count']) or 1, {}, {}, math.log10(args.n)
	local text = (args.text and '*') or ''
	if overlapCalc == math.floor(overlapCalc) then overlapCalc = 10^(overlapCalc) else overlapCalc = 10^(math.floor(overlapCalc) + 1) end
	while count <= args.n do
		local cellparams, overlapn = {}, (string.match(count/overlapCalc, '%.(0+)') or '')..count
		table.insert(icons, (text..(args[count] or '')))
		if args['O'..overlapn] then
			local overlapt = {}
			overlaps = getArgNums('O'..overlapn, args) or {}
			table.sort(overlaps)
			if overlaps[1] then
				for i, v in ipairs(overlaps) do table.insert(overlapt, text..args['O'..overlapn..v]) end
				overlaps = '!~'..text..args['O'..overlapn]..'!~'..table.concat(overlapt, '!~')
			else
				overlaps = '!~'..text..args['O'..overlapn]
			end
			icons[count] = icons[count]..overlaps
		end
		if args['L'..count] then icons[count] = icons[count]..'!@'..args['L'..count] end
		count = count + 1
	end
	local row, rowparams, left, right = table.concat(icons, '\\'), {}
	for k, v in pairs({bg = (args.bg or args.background or args.bgcolor), style = args.style}) do
		if v then table.insert(rowparams, k..'='..v) end
	end
	if rowparams[1] then args.r5 = table.concat(rowparams, ',') end
	for i, v in ipairs({'r1', 'r2', 'r3', 'r4', 'r5', 'l1', 'l2', 'l3', 'l4'}) do
		if not args[v] or string.find(args[v], '^%s*$') then args[v] = nil end
	end
	if args.r5 then
		right = {(args.r1 or ' '), (args.r2 or ' '), (args.r3 or ' '), (args.r4 or ' '), args.r5}
	elseif args.r4 then
		right = {(args.r1 or ' '), (args.r2 or ' '), (args.r3 or ' '), args.r4}
	elseif args.r3 then
		right = {(args.r1 or ' '), (args.r2 or ' '), args.r3}
	elseif args.r1 then
		right = {args.r1, (args.r2 or '')}
	elseif args.r2 then
		right = {args.r2}
	end
	if right then row = row..'~~'..table.concat(right, '~~') end
	if args.l4 then
		left = {args.l4, (args.l3 or ' '), (args.l2 or ' '), (args.l1 or '')}
	elseif args.l3 then
		left = {args.l3, (args.l2 or ' '), (args.l1 or '')}
	elseif args.l1 then
		left = {(args.l2 or ''), args.l1}
	elseif args.l2 then
		left = {args.l2}
	end
	if left then row = table.concat(left, '~~')..'! !'..row end
	return row
end

local function pre_block(text)
	-- Pre tags returned by a module do not act like wikitext <pre>...</pre>.
	return '<pre>' ..
		mw.text.nowiki(text) ..
		(text:sub(-1) == '\n' and '' or '\n') ..
		'</pre>\n'
end

function p.convertbs(frame)--[[

Converts a legacy route diagram into Routemap format.
Code to be used is displayed in preview mode or after saving the page, above the original code.

{{#invoke:Routemap|convertbs|<nowiki>
(Original diagram)
</nowiki>}}

]]
	local org = mw.text.unstripNoWiki(frame.args[1]) or 'Paste legacy RDT markups between the nowiki tags'
	local res = org
	res = string.gsub(res, '{{[Bb][Ss]%-?map', '{{Routemap') -- "%-" is an escape for hyphen which is used as "between" in pattern.
	res = string.gsub(res, '{|%s?{{[Rr]ailway line header}}', '{{Routemap')
	res = string.gsub(res, '{{[Bb][Ss]%-header%d?|', '{{safesubst:BS-header/safesubst|') -- "%d?" means optional digit in case use of variant template like BS-header3.
	res = string.gsub(res, '{{[Bb][Ss]%-table%d?}}', '|map =')
	res = string.gsub(res, '{{[Bb][Ss](%d?)(%d?)|', '{{safesubst:BS%1%2/safesubst|')
	res = string.gsub(res, '{{[Bb][Ss](%d?)(%d?)%-replace|', '!replace{{safesubst:BS%1%2/safesubst|')
	res = string.gsub(res, '{{[Bb][Ss](%d?)(%d?)%-startCollapsible|', '-startCollapsible-collapsed\n{{safesubst:BS%1%2/safesubst|')
	res = string.gsub(res, '{{[Bb][Ss](%d?)(%d?)%-sc|', '-startCollapsible-collapsed\n{{safesubst:BS%1%2/safesubst|')
	res = string.gsub(res, '{{[Bb][Ss](%d?)(%d?)%text|', '{{safesubst:BS%1%2text/safesubst|')
	res = string.gsub(res, '{{[Bb][Ss](%d?)(%d?)%-2|', '{{safesubst:BS%1%2-2/safesubst|')
	res = string.gsub(res, '{{[Bb][Ss](%d?)(%d?)%-2replace|', '!replace{{safesubst:BS%1%2-2|')
	res = string.gsub(res, '{{[Bb][Ss](%d?)(%d?)%-2sc|', '-startCollapsible-collapsed\n{{safesubst:BS%1%2-2|')
	res = string.gsub(res, '{{!}}}', '-endCollapsible-')
	res = string.gsub(res, '{{[Ee]nd}}', '-endCollapsible-')
	res = string.gsub(res, '|}\n|}', '}}') -- Replace ending of Railway line header map setup.
	res = string.gsub(res, '{{[Bb][Ss]%-colspan}}\n{{safesubst', '{{safesubst') -- BS-colspan is unnecessary and would cause error in Routemap.
	res = string.gsub(res, '{{[Bb][Ss]%-colspan}}\n%-%-%-%-', '-colspan-2\n----')
	res = string.gsub(res, '<', '<')
	res = string.gsub(res, '>', '>')
	if string.find(res, '!replace') or string.find(res, '|%s*bg%s*=') then
		local restable = mw.text.split(res, '\n')
		for i, v in ipairs(restable) do
			if string.find(v, '!replace') then
				restable[i] = string.gsub(restable[i], '!replace', '')
				restable[i-2] = string.gsub(restable[i-2], 'collapsed', 'collapsed-replace')
			end
			if (string.find(v, '|%s*bg%s*=%s*#?[a-zA-Z0-9]+') or string.find(v, '|%s*bg%s*=%s*#?{{[^{}]+}}%s*|') or string.find(v, '|%s*bg%s*=%s*#?{{[^{}]+}}%s*}}')) and string.find(restable[i-1], '^-startCollapsible') then
				local bg = string.match(v, '|%s*bg%s*=%s*(#?[a-zA-Z0-9]+)') or string.find(v, '|%s*bg%s*=%s*(#?{{[^{}]+}})%s*|') or string.find(v, '|%s*bg%s*=%s*(#?{{[^{}]+}})%s*}}')
				restable[i] = string.gsub(restable[i], '|%s*bg%s*=%s*'..bg, '')
				restable[i-1] = string.gsub(restable[i-1], '%-?$', '--bg=')..bg
				if string.find(restable[i+1], '!replace') then
					restable[i+1] = string.gsub(restable[i+1], '!replace', '')
					restable[i-1] = string.gsub(restable[i-1], 'collapsed%-', 'collapsed-replace')
					if (string.find(restable[i+1], '|%s*bg%s*=%s*#?[a-zA-Z0-9]+') or string.find(restable[i+1], '|%s*bg%s*=%s*#?{{[^{}]+}}%s*|') or string.find(restable[i+1], '|%s*bg%s*=%s*#?{{[^{}]+}}%s*}}')) then
						local bg2 = string.match(restable[i+1], '|%s*bg%s*=%s*(#?[a-zA-Z0-9]+)') or string.find(restable[i+1], '|%s*bg%s*=%s*(#?{{[^{}]+}})%s*|') or string.find(restable[i+1], '|%s*bg%s*=%s*(#?{{[^{}]+}})%s*}}')
						if bg2 == bg then restable[i+1] = string.gsub(restable[i], '|%s*bg%s*=%s*'..bg2, '') end
					end
				end
			end
		end
		res = table.concat(restable, '\n')
	end
	return "\n'''Safe substitution''':\n" .. pre_block(res) .. "'''''Original''''':\n" .. pre_block(org)
end

return p