-- This module implements the {{Track gauge}} template.
-- Data is in Module:Track gauge/data
local p = {}
local gaugeDataAll = nil
local dataPageName = 'Module:Track gauge/data' -- sandbox here
-----------------------------------------------------------------------------------
-- prepareArgs -- Normalise Arguments coming from an #invoke or from a module
-----------------------------------------------------------------------------------
local function prepareArgs(frame)
	local origArgs
	if frame == mw.getCurrentFrame() then
		origArgs = frame:getParent().args
		for k, v in pairs(frame.args) do
			origArgs = frame.args
			break
		end
	else
		origArgs = frame
	end
	local args = {}
	-- searchAlias is the cleaned value of args[1]. args[1] is kept as rawInput for error message
	local searchAlias = ''
	local rawDisp
	for k, v in pairs(origArgs) do
		if tonumber(k) == nil then -- Named argment
			if k == 'disp' then
				rawDisp = v -- Keep raw disp input to pass through plain (wiki)text
				args[k] = mw.ustring.lower(v)
			elseif k == 'first' then
				v = mw.ustring.lower(v)
				if v == 'met' or v == 'metric' then
					v = 'met'
				elseif v == 'imp' or v == 'imperial' then
					v = 'imp'
				else k = 'trashparam_first' end
				args[k] = v
			elseif k == 'nowrap' or k == 'wrap' then -- wrap=y deprecated; reading: nowrap=off
				v = mw.ustring.lower(v)
				if v == '' or v == 'off' or v == 'on' or v == 'all' then
				elseif v == 'inline' or (k == 'wrap' and v == 'y') then
					v = 'off'
				else v = '' end
				args['nowrap'] = v
			else
				args[k] = mw.ustring.lower(v)
			end
		else
			args[k] = v -- Keep rawInput in [1] for error message
			if k == 1 then
			-- Unnamed argument, the alias to be searched
			-- Cleanup
				searchAlias = p.normaliseAliasInput(v)
			end
		end
	end
	args['searchAlias'] = searchAlias
	if rawDisp then args['rawDisp'] = rawDisp end
	return args
end
-----------------------------------------------------------------------------------
-- normaliseAliasInput
-----------------------------------------------------------------------------------
function p.normaliseAliasInput(aliasIn)
	local a
	a = mw.ustring.lower(mw.ustring.gsub(aliasIn, '[%s%,]', ''))
	a = mw.ustring.gsub(a, ' ', '')
	a = mw.ustring.gsub(a, 'gauge$', '')
	a = mw.ustring.gsub(a, "'", "ft")
	a = mw.ustring.gsub(a, '"', 'in')
	a = mw.ustring.gsub(a, '⁄', '/')
	a = mw.ustring.gsub(a, '⁄', '/')
	return a	
end
-----------------------------------------------------------------------------------
-- debugReturnArgs -- Debug function.
-----------------------------------------------------------------------------------
function p.debugReturnArgs(frame)
	local args = prepareArgs(frame)
	local retArgs = {}
	for k, a in pairs(args) do
		table.insert(retArgs, k .. '=' .. a)
	end
	return 'Args: ' .. table.concat(retArgs, '; ')
end
-----------------------------------------------------------------------------------
-- getTrackGaugeEntry -- Find entry data for a single gauge (alias)
-----------------------------------------------------------------------------------
function p.getTrackGaugeEntry(searchAlias)
	gaugeDataAll = mw.loadData(dataPageName)
	if searchAlias == '' then
		return nil
	end
	local tgEntry = nil
	for i, tgEntry in ipairs(gaugeDataAll) do
		for j, alias in ipairs(tgEntry.aliases) do
			if alias == searchAlias then
				return tgEntry
			end
		end
	end
end
-----------------------------------------------------------------------------------
-- noWrap -- Add span tags to prevent a string from wrapping.
-----------------------------------------------------------------------------------
local function noWrap(s)
	return mw.ustring.format('<span class="nowrap">%s</span>', s)
end
-----------------------------------------------------------------------------------
-- frac -- A slimmed-down version of the {{frac}} template (a nowrap is to be added with the unit)
-----------------------------------------------------------------------------------
local function frac(whole, num, den)
	return mw.ustring.format(
		'<span class="frac">%s%s<sup>%s</sup>⁄<sub>%s</sub></span>',
		whole or '', whole and '<span class="visualhide"> </span>' or '',
		num, den)
end
-----------------------------------------------------------------------------------
-- catMentions -- Wikicode for "article mentions gauge" categories
-----------------------------------------------------------------------------------
function p.catMentions(tgEntry, sortlabel, doReturn)
	local ns = 'Category:'
	local cat

	if tgEntry == nil then
		-- Parent, the container cat
		cat = 'Articles that mention a specific track gauge'
	else
		cat = 'Articles that mention track gauge ' .. tgEntry.id .. ' mm'
	end
	-- Argument 'label' can be used to add a catsort. Catsort is not used (as of 20 May 2014)
	if sortlabel ~= nil then
		sortlabel = '|' .. sortlabel
	else
		sortlabel = ''
	end
	if doReturn ~= nil then
		if doReturn == 'fullpagename' then
			return ns .. cat
		elseif doReturn == 'pagename' then -- plaintext, no namespace
			return cat
		elseif doReturn == 'show' then -- colontrick
			return '[[:'_.._ns_.._cat_.._sortlabel_.._'|:' .. ns .. cat .. sortlabel .. ']]'
		else -- unknown arg value
			return ns .. cat
		end
	else -- Returns straight categorisation (wikitext)
		return '[['_.._ns_.._cat_.._sortlabel_.._'|' .. ns .. cat .. sortlabel .. ']]'
	end
end
-----------------------------------------------------------------------------------
-- formatImp -- Formats imperial units size into a single text element
-----------------------------------------------------------------------------------
function p.formatImp(tgEntry, measurementToLink, setNowrap, addUnitlink)
	local ret = {}
	local ft = tgEntry.ft
	if ft then
		local ftlink = addUnitlink and measurementToLink ~= 'imp' and '[[Foot_(unit)|ft]]' or 'ft'
		table.insert(ret, mw.ustring.format('%s %s', ft, ftlink))
	end
	local inches = tgEntry['in']
	local num = tgEntry.num
	local den = tgEntry.den
	if inches and not num and not den then
		table.insert(ret, inches)
	elseif num and den then
		table.insert(ret, frac(inches, num, den))
	end
	if inches or num and den then
		local incheslink = addUnitlink and measurementToLink ~= 'imp' and '[[inch|in]]' or 'in'
		table.insert(ret, incheslink)
	end
	local gaugeSize
	if setNowrap then
		gaugeSize = noWrap(table.concat(ret, ' '))
	else
		gaugeSize = table.concat(ret, ' ')
	end
	if measurementToLink == 'imp' and tgEntry.pagename ~= nil then
		return mw.ustring.format('[[%s|%s]]', tgEntry.pagename, gaugeSize)
	else
		return gaugeSize
	end
end
-----------------------------------------------------------------------------------
-- formatMet -- Formats metric measurements into a single formatted text element. Public for autodocument
-----------------------------------------------------------------------------------
function p.formatMet(tgEntry, measurementToLink, setNowrap, addUnitlink)
	local m = tgEntry.m
	local gaugeSize
	if m then
		local mUnit = addUnitlink and measurementToLink ~= 'met' and '[[metre|m]]' or 'm'
		gaugeSize = mw.ustring.format('%s %s', m, mUnit)
	else
		local mm = tgEntry.mm
		mm = tonumber(mm)
		if mm then
			mm = mw.getContentLanguage():formatNum(mm)
		end
		local mmUnit = addUnitlink and measurementToLink ~= 'met' and '[[millimetre|mm]]' or 'mm'
		gaugeSize = mw.ustring.format('%s %s', mm, mmUnit)
	end
	if setNowrap then
		gaugeSize = noWrap(gaugeSize)
	end
	if measurementToLink == 'met' and tgEntry.pagename ~= nil then
		return mw.ustring.format('[[%s|%s]]', tgEntry.pagename, gaugeSize)
	else
		return gaugeSize
	end
end
-----------------------------------------------------------------------------------
-- formatAltName
-----------------------------------------------------------------------------------
function formatAltName(tgEntry, addGaugeName, addGaugeNameLink, disp, setNowrap, engvar)
	-- Assumed: at least one to add is true.
	if tgEntry.name == nil then
		-- Not checked: link does exist alone
		return ''
	end
	local retAlt = {}
	if disp == 'br' then
		table.insert(retAlt, '<br>')
	else
		table.insert(retAlt, ' ')
	end
	if setNowrap then
		table.insert(retAlt, '<span class="nowrap">')
	end
	if addGaugeNameLink then
		if engvar == 'en-us' then
			-- Current implementations (2016): metER for metRE (1000-met, 1009-met)
			table.insert(retAlt, tgEntry.en_US_link or tgEntry.link or tgEntry.name)
		else
			table.insert(retAlt, tgEntry.link or tgEntry.name)
		end
	else -- so must be unlinked .name to add
			if engvar == 'en-us' then
			-- Current implementations (2016): metER for metRE (1000-met, 1009-met)
			table.insert(retAlt, tgEntry.en_US_name or tgEntry.name)
		else
			table.insert(retAlt, tgEntry.name)
		end
	end
	if setNowrap then --close tag
		table.insert(retAlt, '</span>')
	end
	return table.concat(retAlt, '')
end
-----------------------------------------------------------------------------------
-- main -- The basic module
-----------------------------------------------------------------------------------
function p.main(frame)
	-- In general: tgEntry (from TG/data) is passed to the functions, arguments are processed here.
	local title = mw.title.getCurrentTitle()
	local args = prepareArgs(frame)
	local tgEntry = p.getTrackGaugeEntry(args.searchAlias)

	-- Categorise & preview warning when no track gauge definition was found.
	if tgEntry == nil then
		local input = args[1] or ''
		local errorTail = ''
		
		if frame:preprocess("{{REVISIONID}}") == "" then 
				errorTail = '<div class="hatnote" style="color:red"><strong>Warning:</strong> ' .. 'Track gauge ' .. (input .. ' ' or '') .. 'not in [[:Template:Track_gauge#List_of_defined_track_gauges|List of defined track gauges]] ([[Template_talk:Track_gauge|talk]]).' .. ' (This message is shown only in preview.)</div>'
		end

		if title:inNamespaces(0, 14) then -- mainspace and category space
			errorTail = errorTail .. "[[Category:Articles_using_template_'Track_gauge'_with_unrecognized_input|Category:Articles using template 'Track gauge' with unrecognized input]]"
		end
		return input .. errorTail
	end

	-- Check and set args & tgEntry props: disp, first, nowrap, first
	local disp = args.disp or ''
	local first = args.first or tgEntry.def1
	local unitlink = args.unitlink or ''
	local nowrap = args.nowrap or ''
	local setNowrapElement = (nowrap == '' or nowrap == 'off') -- To prevent nested nowrap tags
	local measurementToLink
	if args.lk == 'on' then
		if disp == '1' then
			measurementToLink = first -- Can make metric text links to the imp linked page
		else
			measurementToLink = tgEntry.def1 -- When first=swapped, this could link 2nd measure.
		end
	end
	-- String the text elements together (compose the return table)
	local ret = {}
	-- nowrap opening tag
	if nowrap == 'all' or nowrap == 'on' then
		table.insert(ret, '<span class="nowrap">')
	end
	-- First measure
	if first == 'met' then
		table.insert(ret,
			p.formatMet(tgEntry, measurementToLink, setNowrapElement, unitlink == 'on'))
	else
		table.insert(ret,
			p.formatImp(tgEntry, measurementToLink, setNowrapElement, unitlink == 'on'))
	end
	-- The joint and the second measure
	if disp == '1' then
	else
		local joinText = ''
		local closeDisp = ''
		if disp == 's' or disp == '/' then
			joinText = '/​'
		elseif disp == 'br' then
			joinText = '<br>('
			closeDisp = ')'
		elseif disp == '[' or disp == '[]' then
			joinText = ' ['
			closeDisp = ']'
		elseif disp ~= '' then -- Is anytext
			joinText = ' ' .. args['rawDisp'] .. ' '
		else
			joinText = ' ('
			closeDisp = ')'
		end
		table.insert(ret, joinText)
		if first ~= 'met' then
			table.insert(ret,
				p.formatMet(tgEntry, measurementToLink, setNowrapElement, unitlink == 'on'))
		else
			table.insert(ret,
				p.formatImp(tgEntry, measurementToLink, setNowrapElement, unitlink == 'on'))
		end
		table.insert(ret, closeDisp) -- Could be ''
	end
	if nowrap == 'on' then -- Closing tag
		table.insert(ret, '</span>')
	end
	-- Alternative name
	if args.al == 'on' or args.allk == 'on' then
		local setNowrapAltname = (nowrap == '' or nowrap == 'on') -- Logic applied to prevent nested nowrap tags
		table.insert(ret, formatAltName(tgEntry, args.al == 'on', args.allk == 'on', disp, setNowrapAltname, args.engvar))
	end
	-- Closing nowrap tag
	if nowrap == 'all' then
		table.insert(ret, '</span>')
	end
	
	-- Category mentionings (maintenance)
	if args.addcat or '' == 'no' then
		-- No categorization
	elseif title:inNamespaces(0) then
		-- switched off per [[Wikipedia:Categories_for_discussion/Log/2016_December_6#Category:Articles_that_mention_a_specific_track_gauge|Wikipedia:Categories_for_discussion/Log/2016_December_6#Category:Articles_that_mention_a_specific_track_gauge]]
		-- 2016-12-19
		-- table.insert(ret, p.catMentions(tgEntry))
	end

	-- Now sting the table together
	return table.concat(ret, '')
end

return p
--20161219: maintenance categorisation switched off per CfD
--20170602: fix bug, show name when al=on
--20180708: show preview warning when gauge is not in list.