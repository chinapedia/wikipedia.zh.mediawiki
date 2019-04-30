require('Module:No globals')

local p = {}

local lang = 'zh-CN' -- local default language

--	Below these comments: Internationalization table
--	How to translate this module (for languages without variants):
--	• Characters inside single and double quotation marks are called strings.
--	  The strings in this i18n table are used as output.
--	• Strings within square brackets are keys.
--	• Strings are concatenated (joined) with two dots.
--	• Set the string after «local lang =» to your language's code.
--	  Change the first key after "i18n" (usually "en-GB") to the same thing.
--	• For each string which is not inside a function, translate it directly.
--	• Strings with keys named "format" are Lua regular expressions.
--	  «()» is a match; «.+» means all characters; «%s+» means all spaces.
--	• For each string which is concatenated to the variable «var»,
--	  translate the phrase assuming that «var» will be a noun.
--	• Remove any unnecessary translations.

local i18n = require("Module:Adjacent stations/i18n")
local function getData(system, verify)
	if verify then
		local title = mw.title.new('Module:Adjacent stations/' .. system -- .. '/sandbox'
			)
		if not (title and title.exists) then return nil end
	end
	return require('Module:Adjacent stations/' .. system -- .. '/sandbox'
		)
end

local function getLine(data, lineN)
	if lineN then
		if data['aliases'] then
			lineN = data['aliases'][mw.ustring.lower(lineN)] or lineN
		end
		local default = data['lines']['_default'] or {}
		local line = data['lines'][lineN] or {}
		for k, v in pairs(default) do
			if v then line[k] = line[k] or v end
		end
		line['title'] = line['title'] and mw.ustring.gsub(line['title'], '%%1', lineN)
		return line, lineN
	end
end

local function getColor(data, system, line, Type, frame)
	if system then
		if line then return frame:expandTemplate{ title = system .. ' color', args = {line, ['branch'] = Type} } end
		return frame:expandTemplate{ title = system .. ' color' }
	else
		line = (getLine(data, line))
		local default = data['lines']['_default']
		if line or default then
			default = default or {}
			if not line then line = mw.clone(default) end
			local color = line['color'] or line['background color'] or default['color'] or default['background color'] or data['system color']
			local Type_value = Type and line['types'] and (line['types'][Type] and line['types'][Type]['color'])
			if Type_value then color = Type_value end
			return color
		end
		return (default and (default['color'] or default['background color']) or data['system color'] or '')
	end
end

local lineN, typeN

local function getStation(station, _Format)
	if type(_Format) == 'table' then
		_Format = _Format[lineN] or _Format[1]
		if type(_Format) == 'table' then
			_Format = _Format[typeN] or _Format[1]
		end
	end
	if typeN then _Format = mw.ustring.gsub(_Format, '%%3', typeN) end
	if lineN then _Format = mw.ustring.gsub(_Format, '%%2', lineN) end
	return (mw.ustring.match(_Format, '%[%[.+%]%]')) and (mw.ustring.gsub(_Format, '%%1', station)) or table.concat({'[[',_mw.ustring.gsub(_Format,_'%%1',_station),_'|', station, ']]'})
end

function p._main(_args) -- Arguments are processed here instead of the main function

	local yesno = require('Module:Yesno')
	local boolean = {
		['oneway-left'] = true,
		['oneway-right'] = true,
		['reverse'] = true,
		['reverse-left'] = true,
		['reverse-right'] = true
	}

	local args = {} -- Processed arguments
	local index = {} -- A list of addresses corresponding to number suffixes in the arguments

	for k, v in pairs(_args) do -- Maps each raw argument to processed arguments by string matching
		_args[k] = v:match('^%s*(.-)%s*$')
		if _args[k] and _args[k] ~= '' then
			local a = mw.ustring.match(k, '^(.*%D)%d+$') or k -- The parameter; address 1 can be omitted
			local b = tonumber(mw.ustring.match(k, '^.*%D(%d+)$')) or 1 -- The address for a given argument; address 1 can be omitted

			if boolean[a] then
				v = yesno(v)
			end

			if not args[b] then
				args[b] = {[a] = v}
				table.insert(index, b)
			elseif args[b][a] then
				return error(i18n[lang]['error_duplicate'](a .. b))
			else
				args[b][a] = v
			end
		end
	end
	table.sort(index)

	local function small(s, italic)
		return italic and '<div class="isA">' .. s .. '</div>'
			or '<div class="smA">' .. s .. '</div>'
	end

	local style = { -- Style for each cell type
		['header cell'] = 'class="hcA"|',
		['header midcell'] = 'colspan="3" class="hmA"|',
		['body cell'] = 'class="bcA"|',
		['body banner'] = 'class="bbA" style="background-color:#',
	}

	local Format
	local function subst(var1, var2)
		-- var1 is the terminus or table of termini; var2 is the key for the table of termini
		return type(var1) == 'string' and getStation(var1, (Format[var1] or Format[1]))
			or type(var1) == 'table' and #var1 > 0 and getStation(var1[var2], (Format[var1[var2]] or Format[1]))
			or ''
	end

	local function station(var)
		if Format then
			if type(var) == 'string' then
				return subst(var)
			elseif type(var) == 'table' and #var > 0 then
				local t = {subst(var, 1)}

				for i = 2, #var - 1 do
					t[i] = i18n[lang]['comma'](subst(var, i))
				end

				if #var > 1 then t[#var] = i18n[lang]['or'](subst(var, #var)) end
				if var['via'] then
					if i18n[lang]['via-first'] then
						table.insert(t, 1, i18n[lang]['via'](subst(var, 'via')))
					else
						table.insert(t, i18n[lang]['via'](subst(var, 'via')))
					end
				end

				return table.concat(t)
			else
				return ''
			end
		else
			return var or ''
		end
	end

	local function rgb(var)
		if var:len() == 3 then
			return {tonumber(var:sub(1, 1), 16) * 17, tonumber(var:sub(2, 2), 16) * 17, tonumber(var:sub(2, 2), 16) * 17}
		elseif var:len() == 6 then
			return {tonumber(var:sub(1, 2), 16), tonumber(var:sub(3, 4), 16), tonumber(var:sub(5, 6), 16)}
		end
		return {}
	end

	local data = {} -- A table of data modules for each address
	local wikitable = {'{| class="wikitable adjacent-stations"'}

	for i, v in ipairs(index) do
		-- If an address has a system argument, indexes the data module
		data[v] = args[v]['system'] and getData(args[v]['system'])
		-- If an address has no system, the row uses data from the previous address
			or data[index[i - 1]]
			or error(i18n[lang]['error_unknown'](args[v]['system']))

		local lang = data[v]['lang'] or lang

		if args[v]['system'] then -- Header row
			local stop_noun = data[v]['header stop noun'] or i18n[lang]['stop_noun']
			table.insert(wikitable, table.concat({'\n|-',
				'\n!', style['header cell'], i18n[lang]['preceding'](stop_noun),
				'\n!', style['header midcell'], (data[v]['system icon'] and data[v]['system icon'] .. ' ' or ''), (data[v]['system title'] or ('[['.._args[v]['system']_..'|'.. args[v]['system'] ..']]')),
				'\n!', style['header cell'], i18n[lang]['following'](stop_noun)
			}))
			table.insert(wikitable, '')
			table.insert(wikitable, '')
			table.insert(wikitable, '')
		end

		if args[v]['header'] then -- Subheader
			table.insert(wikitable, '\n|-\n!colspan="5" class="hmA"|'.. args[v]['header'])
			table.insert(wikitable, '')
			table.insert(wikitable, '')
			table.insert(wikitable, '')
		end

		if args[v]['line'] or args[v]['left'] or args[v]['right'] or args[v]['nonstop'] then
			if not args[v]['line'] and i > 1 and not args[v]['system'] then
				args[v]['line'] = args[index[i - 1]]['line']
			end

			lineN = args[v]['line'] or '_default'
			typeN = args[v]['type']
			if data[v]['aliases'] then
				lineN = data[v]['aliases'][mw.ustring.lower(lineN)] or lineN
				if typeN then typeN = data[v]['aliases'][mw.ustring.lower(typeN)] or typeN end
			end

			-- get the line table
			local line = data[v]['lines'] and (mw.clone(data[v]['lines'][lineN]) or error(i18n[lang]['error_unknown'](args[v]['line']))) or error(i18n[lang]['error_line'])
			local default = data[v]['lines']['_default'] or {}
			line['title'] = line['title'] or default['title']
			line['title'] = mw.ustring.gsub(line['title'], '%%1', lineN)

			-- cell across row for non-stop service
			if args[v]['nonstop'] then
				table.insert(wikitable,
					table.concat({'\n|-\n|colspan="5" ',
						style['body cell'],
						((args[v]['nonstop'] == 'former') and i18n[lang]['nonstop_past'] or i18n[lang]['nonstop_present'])(p._box({data = data[v], line = lineN, Type = typeN, inline = 'yes'}))
					})
				)
				table.insert(wikitable, '')
				table.insert(wikitable, '')
				table.insert(wikitable, '')
			else
				Format = data[v]['station format'] or i18n[lang]['error_format']

				local color, background_color
				local Type = line['types'] and line['types'][typeN] -- get the line type table

				if Type then
					if Type['color'] then
						-- line color is used as background if there is no background color in the line type table
						background_color = Type['background color'] or line['color']
						color = Type['color']
					elseif Type['background color'] then
						background_color = Type['background color']
						color = line['color'] or default['color'] or ''
					else
						background_color = line['background color']
						color = line['color'] or default['color'] or ''
					end
				else
					background_color = line['background color']
					color = line['color'] or default['color'] or ''
				end

				-- Alternate termini can be specified based on type
				local sideCell = {true, true}
				for i, b in ipairs({'left', 'right'}) do
					if not args[v][b] then -- If no station is given on one side, the station is assumed to be the terminus on that side
						local _through = args[v]['through-' .. b] or args[v]['through']
						local _through_data = getLine(data[v], _through)
						if _through_data then _through = _through_data['title'] or _through end
						sideCell[i] = _through and "''" .. i18n[lang]['through'](_through) .. "''"
							or "''" .. ((args[v]['reverse-' .. b]
							or args[v]['reverse']) and i18n[lang]['reverse']
							or i18n[lang]['terminus']) .. "''"
					else
						local terminusT
						local terminusN = Type and Type[b .. ' terminus'] or line[b .. ' terminus']

						-- If the terminus table has more than one numbered key or has the via key then the table shows only the default termini, since terminusN[2] cannot be used and terminusN[via] is reserved
						if type(terminusN) == 'string' or (type(terminusN) == 'table' and (terminusN[2] or terminusN['via'])) then
							if args[v]['to-' .. b] then
								terminusT = args[v]['to-' .. b]
								local _or = mw.ustring.match(terminusT, i18n[lang]['or-format'])
								if _or then
									terminusT = mw.ustring.gsub(terminusT, i18n[lang]['or-format'], '\127_OR_\127')
									terminusT = mw.ustring.gsub(terminusT, i18n[lang]['comma-format'], '\127_OR_\127')
								end
								local _via = (mw.ustring.match(terminusT, i18n[lang]['via-format']))
								if _via then
									terminusT = mw.ustring.gsub(terminusT, i18n[lang]['via-format'], '')
									terminusT = mw.text.split(terminusT, '\127_OR_\127')
									terminusT['via'] = _via
								elseif _or then
									terminusT = mw.text.split(terminusT, '\127_OR_\127')
								end
							else
								terminusT = terminusN
							end
						elseif type(terminusN) == 'table' then
							terminusT = terminusN[args[v]['to-' .. b]] or terminusN[args[v]['to']] or terminusN[1]
						end

						local mainText = args[v]['note-' .. b] and station(args[v][b]) .. small(args[v]['note-' .. b]) or station(args[v][b])

						local subText = (args[v]['oneway-' .. b] or line['oneway-' .. b]) and i18n[lang]['oneway']
							or args[v][b] == terminusT and i18n[lang]['terminus']
							or line['circular'] and terminusT
							or i18n[lang]['towards'](station(terminusT))
						subText = small(subText, true)

						sideCell[i] = mainText .. subText
					end
				end

				table.insert(wikitable, '\n|-')
				table.insert(wikitable, '\n|' .. style['body cell'] .. sideCell[1])
				table.insert(wikitable, table.concat({'\n|', style['body banner'], color, '"|',
					'\n|', (background_color and 'class="bcA" style="background-color:rgba(' .. table.concat(rgb(background_color), ',') .. ',.2)"|' or style['body cell']), line['title'],

					-- Type; table key 'types' in subpages (datatype table, with strings as keys). If table does not exist then the input is displayed as the text
					(typeN and '<div>' .. (Type and Type['title'] or typeN) .. '</div>' or ''),

					-- Note-mid; table key 'note-mid' in subpages. Overridden by user input
					((args[v]['note-mid'] and small(args[v]['note-mid'])) or (Type and Type['note-mid'] and small(Type['note-mid'])) or (line['note-mid'] and small(line['note-mid'])) or ''),

					-- Transfer; uses system's station link table
					(args[v]['transfer'] and small('于' .. station(args[v]['transfer']) .. '换乘', true) or ''),

					'\n|', style['body banner'], color, '"|'}))
				table.insert(wikitable, '\n|' .. style['body cell'] .. sideCell[2])
			end
		end

		if args[v]['note-row'] then -- Note
			table.insert(wikitable, '\n|-\n|colspan="5" ' .. style['body cell'] .. args[v]['note-row'])
			table.insert(wikitable, '')
			table.insert(wikitable, '')
			table.insert(wikitable, '')
		end
	end

	local function combine(t, n)
		if t[n + 4] ~= '' and t[n + 4] == t[n] then
			t[n + 4] = '' -- The cell in the next row is deleted
			local rowspan = 2
			while t[n + rowspan * 4] == t[n] do
				t[n + rowspan * 4] = ''
				rowspan = rowspan + 1
			end
			t[n] = mw.ustring.gsub(t[n], '\n|class="', '\n|rowspan="' .. rowspan .. '" class="')
		end
	end

	local M = #wikitable
	for i = 3, M, 4 do combine(wikitable, i) end
	for i = 4, M, 4 do combine(wikitable, i) end
	for i = 5, M, 4 do combine(wikitable, i) end

	table.insert(wikitable, '\n|}')

	return table.concat(wikitable)
end

local getArgs = require('Module:Arguments').getArgs

local function makeInvokeFunction(funcName)
	-- makes a function that can be returned from #invoke, using
	-- [[Module:Arguments|Module:Arguments]]
	return function (frame)
		local args = getArgs(frame, {parentOnly = true})
		return p[funcName](args, frame)
	end
end

p.main = makeInvokeFunction('_main')

function p._color(args, frame)
	local data = args.data
	if args[1] or data then
		data = data or getData(args[1], true)
		if not data then return getColor(nil, args[1], args[2], args[3], frame) end
		return getColor(data, nil, args[2], args[3])
	end
end

p.color = makeInvokeFunction('_color')

function p._box(args, frame)
	local system = args[1] or args.system
	lineN = args[2] or args.line
	if not (system or lineN) then return '' end
	local line, Type, line_data
	local inline = args[3] or args.inline
	typeN = args.type
	local data = args.data
	if system or data then
		data = data or getData(system, true)
		local color
		if data then
			local default = data['lines']['_default'] or {}
			line, lineN = getLine(data, lineN)
			if typeN then
				typeN = data['aliases'] and data['aliases'][mw.ustring.lower(typeN)] or typeN
				Type = line['types'] and line['types'][typeN] and line['types'][typeN]['title'] or typeN
			end
			color = getColor(data, nil, lineN, typeN)
			if inline ~= 'box' then
				line_data = line or error(i18n[lang]['error_unknown'](lineN))
				line = line_data['title'] or default['title'] or error(i18n[lang]['error_missing']('title'))
				line = mw.ustring.gsub(line, '%%1', lineN)
			end
		else
			color = getColor(nil, system, lineN, typeN, frame)
			if inline ~= 'box' then
				line = frame:expandTemplate{ title = system .. ' lines', args = {lineN, ['branch'] = typeN} }
				if mw.text.trim(line) == '' then return error(i18n[lang]['error_unknown'](lineN)) end
			end
			Type = typeN
		end

		local result

		if Type and Type ~= '' and inline ~= 'box' then
			if line == '' then
				line = Type
			else
				result = ' – ' .. Type
			end
		end
		if args.note then result = (result or '') .. ' ' .. args.note end
		result = result or ''

		if not inline then -- [[Template:Legend|Template:Legend]]
			result = '<div class="legend" style="-webkit-column-break-inside:avoid;page-break-inside:avoid;break-inside:avoid-column"><span class="legend-color" style="display:inline-block;width:1.5em;height:1.5em;margin:1px 0;border:1px solid black;background-color:#' .. color .. '"> </span> ' .. line .. result .. '</div>'
		elseif inline == 'yes' then
			result = '<span style="background-color:#' .. color .. ';border:1px solid #000">    </span> ' .. line .. result
		elseif inline == 'box' then
			result = '<span style="background-color:#' .. color .. ';border:1px solid #000">    </span>' .. result
		elseif inline == 'link' then
			local link = args.link or mw.ustring.match(line, '%[%[([^%[:|%]]+)[|%]]')
			if link then
				result = '[['_.._link_.._'|<span style="background-color:#' .. color .. ';border:1px solid #000">    </span>]]' .. result
			else
				result = '<span style="background-color:#' .. color .. ';border:1px solid #000">    </span>' .. result
			end
		elseif inline == 'square' then
			result = '<span style="color:#' .. color .. ';line-height:initial">■</span> ' .. line .. result
		elseif inline == 'lsquare' then
			local link = args.link or mw.ustring.match(line, '%[%[([^%[:|%]]+)[|%]]')
			if link then
				result = '[['_.._link_.._'|<span style="color:#' .. color .. ';line-height:initial">■</span>]]'
			else
				result = '<span style="color:#' .. color .. ';line-height:initial">■</span>'
			end
		elseif inline == 'dot' then
			result = '<span style="color:#' .. color .. ';line-height:initial">●</span> ' .. line .. result
		elseif inline == 'ldot' then
			local link = args.link or mw.ustring.match(line, '%[%[([^%[:|%]]+)[|%]]')
			if link then
				result = '[['_.._link_.._'|<span style="color:#' .. color .. ';line-height:initial">●</span>]]'
			else
				result = '<span style="color:#' .. color .. ';line-height:initial">●</span>'
			end
		elseif inline == 'small' then
			result = '<span style="background-color:#' .. color .. '"> </span>' .. ' ' .. line .. result
		else
			local yesno = require("Module:Yesno")
			local link = args.link or mw.ustring.match(line, '%[%[([^%[:|%]]+)[|%]]')
			local border_color, text_color
			if line_data then
				if line_data['types'] and line_data['types'][typeN] then
					local Type_data = line_data['types'][typeN]
					border_color = Type_data['border color'] or line_data['border color'] or color
					text_color = Type_data['text color'] or line_data['text color']
					lineN = Type_data['short name'] or line_data['short name'] or lineN
				else
					border_color = line_data['border color'] or color
					text_color = line_data['text color']
					lineN = line_data['short name'] or lineN
				end
			else
				border_color = color
			end
			local greatercontrast = require('Module:Color contrast')._greatercontrast
			text_color = text_color and '#' .. text_color or greatercontrast{color}
			local bold = (yesno(args.bold) == false) or ';font-weight:bold'
			if inline == 'route' then -- [[Template:RouteBox|Template:RouteBox]]
				if link then
					result = '<span style="background-color:#' .. color .. ';border:.075em solid #' .. border_color .. ';padding:0 .3em">[['_.._link_.._'|<span style="color:' .. text_color .. bold .. ';font-size:inherit;white-space:nowrap">' .. lineN .. '</span>]]</span>'
				else
					result = '<span style="background-color:#' .. color .. ';border:.075em solid #' .. border_color .. ';padding:0 .3em;color:' .. text_color .. bold .. ';font-size:inherit;white-space:nowrap">' .. lineN .. '</span>'
				end
			elseif inline == 'croute' then -- [[Template:Bahnlinie|Template:Bahnlinie]]
				if link then
					result = '<span style="background-color:#' .. color .. ';border:.075em solid #' .. border_color .. ';border-radius:.5em;padding:0 .3em">[['_.._link_.._'|<span style="color:' .. text_color .. bold .. ';font-size:inherit;white-space:nowrap">' .. lineN .. '</span>]]</span>'
				else
					result = '<span style="background-color:#' .. color .. ';border:.075em solid #' .. border_color .. ';border-radius:.5em;padding:0 .3em;color:' .. text_color .. bold .. ';font-size:inherit;white-space:nowrap">' .. lineN .. '</span>'
				end
			elseif inline == 'xroute' then -- [[Template:Bahnlinie|Template:Bahnlinie]]
				if link then
					result = '<span style="border:.075em solid #' .. border_color .. ';border-radius:.5em;padding:0 .3em">[['_.._link_.._'|<span style="color:#' .. color .. bold .. ';font-size:inherit;white-space:nowrap">' .. lineN .. '</span>]]</span>'
				else
					result = '<span style="border:.075em solid #' .. border_color .. ';border-radius:.5em;padding:0 .3em;color:#' .. color .. bold .. ';font-size:inherit;white-space:nowrap">' .. lineN .. '</span>'
				end
			else -- [[Template:Legend|Template:Legend]] (fallback; duplication to simplify logic)
				result = '<div class="legend" style="-webkit-column-break-inside:avoid;page-break-inside:avoid;break-inside:avoid-column"><span class="legend-color" style="display:inline-block;width:1.5em;height:1.5em;margin:1px 0;border:1px solid black;background-color:#' .. color .. '"> </span> ' .. line .. result .. '</div>'
			end
		end

		result = mw.ustring.gsub(result, ':%s*#transparent', ':transparent')

		return result
	end
end

p.box = makeInvokeFunction('_box')

function p._icon(args, frame)
	local system = args[1] or args.system
	local line = args[2] or args.line
	local Type = args[3] or args.type
	local data = args.data
	if system or data then
		data = data or getData(system)

		local icon, Format

		line = (getLine(data, line))

		if line then
			if Type then
				Type = data['aliases'] and data['aliases'][mw.ustring.lower(Type)] or Type
				Type = line['types'] and line['types'][Type] -- If there's no type table or entry for this type, then it can't have its own icon
				Format = Type['icon format'] or data['type icon format']
				icon = Type['icon']
			end
			if not (Format or icon) then
				Format = line['icon format'] or data['line icon format']
				icon = line['icon']
			end
		end
		if not (Format or icon) then
			Format = data['system icon format']
			icon = data['system icon']
		end

		if Format then
			if Format ~= 'image' then return p._box({data = data, [2] = (args[2] or args.line), [3] = Format, type = (args[3] or args.type), bold = args.bold, link = args.link}, frame) end
		end

		local size = args.size
		if size then
			if mw.ustring.match(size, '%d$') then
				size = '|' .. size .. 'px'
			else
				size = '|' .. size
			end
			-- Upright values are to be disabled until there is use of upright scaling in subpages; doesn't seem to work anyway as of 2018-08-10
			local tmp = {
				'|%s*%d*x?%d+px%s*([%]|])', -- '|%s*upright=%d+%.?%d*%s*([%]|])', '|%s*upright%s*([%]|])'
			}
			if mw.ustring.match(icon, tmp[1]) then
				icon = mw.ustring.gsub(icon, tmp[1], size .. '%1')
		--	elseif mw.ustring.match(icon, tmp[2]) then
		--		icon = gsub(icon, tmp[2], size .. '%1')
		--	elseif mw.ustring.match(icon, tmp[3]) then
		--		icon = gsub(icon, tmp[3], size .. '%1')
			else
				icon = mw.ustring.gsub(icon, '(%[%[[^%]|]+)([%]|])', '%1' .. size .. '%2')
			end
		end

		local link = args.link
		if link then
			if mw.ustring.match(icon, '|%s*link=[^%]|]*[%]|]') then
				icon = mw.ustring.gsub(icon, '|%s*link=[^%]|]*([%]|])', '|link=' .. link .. '%1')
			else
				icon = mw.ustring.gsub(icon, '(%[%[[^%]|]+)([%]|])', '%1|link=' .. link .. '%2')
			end
		end

		local alt = args.alt or link
		if alt then
			if mw.ustring.match(icon, '|%s*alt=[^%]|]*[%]|]') then
				icon = mw.ustring.gsub(icon, '|%s*alt=[^%]|]*([%]|])', '|alt=' .. alt .. '%1')
			else
				icon = mw.ustring.gsub(icon, '(%[%[[^%]|]+)([%]|])', '%1|alt=' .. alt .. '%2')
			end
		end

		return icon
	end
end

p.icon = makeInvokeFunction('_icon')

function p._line(args, frame)
	local system = args[1] or args.system
	local line = args[2] or args.line
	if not line then return '' end
	local Type = args[3] or args.type
	local data = args.data
	if system or data then
		data = data or getData(system, true)
		if data then
			line = (getLine(data, line)) or error(i18n[lang]['error_unknown'](line))
			if Type then
				Type = data['aliases'] and data['aliases'][mw.ustring.lower(Type)] or Type
				Type = line['types'] and line['types'][Type] and line['types'][Type]['title'] or Type
			end
			line = line['title'] or error(i18n[lang]['error_missing']('title'))
		else
			line = frame:expandTemplate{ title = system .. ' lines', args = {line, ['branch'] = Type} }
			if mw.text.trim(line) == '' then return error(i18n[lang]['error_unknown'](lineN)) end
		end

		if Type then
			if line == '' then
				line = Type
			else
				line = line .. ' – ' .. Type
			end
		end
		return line
	end
end

p.line = makeInvokeFunction('_line')

function p._station(args, frame)
	local system = args[1] or args.system
	local station = args[2] or args.station
	if not station then return '' end
	lineN = args[3] or args.line
	typeN = args[4] or args.type
	local data = args.data
	if system or data then
		data = data or getData(system, true)
		if data then
			local _Format = data['station format'][station] or data['station format'][1]
			if _Format then
				if data['aliases'] then
					if lineN then
						lineN = data['aliases'][mw.ustring.lower(lineN)] or lineN
					end
					if typeN then
						typeN = data['aliases'][mw.ustring.lower(typeN)] or typeN
					end
				end
				station = getStation(station, _Format)
			else
				station = station or ''
			end
		else
			station = frame:expandTemplate{ title = system .. ' stations', args = {['station'] = station, ['line'] = lineN, ['branch'] = typeN} }
		end

		return station
	end
end

p.station = makeInvokeFunction('_station')

function p._style(args, frame)
	local style = args[1] or args.style
	local system = args[2] or args.system
	local line = args[3] or args.line
	local station = args[4] or args.station
	local result = {}
	local data = args.data
	local default = 'background-color:#efefef' -- Default background color for {{Infobox station}}
	if system or data then
		data = data or getData(system, true)
	end
	if data then
		local function getValue(var)
			if type(var) == 'table' then
				var = var[line] or var[1]
				if type(var) == 'table' then
					var = var[station] or var[1]
				end
			end
			if var ~= '' then return var end
		end

		if style == 'header' then
			local tmp = data['name format'] and getValue(data['name format'])
			if tmp then table.insert(result, tmp) end
		elseif style == 'subheader' then
			local tmp = data['header background color'] and getValue(data['header background color'])
			if tmp then
				table.insert(result, 'background-color:#' .. tmp)
				local color = data['header text color'] and getValue(data['header text color'])
				if color then
					table.insert(result, 'color:#' .. color)
				else
					local greatercontrast = require('Module:Color contrast')._greatercontrast
					if greatercontrast{tmp} == '#FFFFFF' then table.insert(result, 'color:#FFFFFF') end
				end
			else
				table.insert(result, default)
				local color = data['header text color'] and getValue(data['header text color'])
				if color then table.insert(result, 'color:#' .. color) end
			end
		end
		result = table.concat(result, ';')
	elseif system then
		local title = 'Template:' .. system .. ' style'
		local titleObj = mw.title.new(title)
		if titleObj and titleObj.exists then
			local tmp
			if style == 'header' then
				tmp = frame:expandTemplate{ title = title, args = {'name_format', line, station} }
				if tmp ~= '' then table.insert(result, tmp) end
			elseif style == 'subheader' then
				tmp = frame:expandTemplate{ title = title, args = {'thbgcolor', line, station} }
				if tmp ~= '' then
					table.insert(result, 'background-color:#' .. tmp)
					local color = frame:expandTemplate{ title = title, args = {'thcolor', line, station} }
					if color ~= '' then
						table.insert(result, 'color:#' .. color)
					else
						local ratio = require('Module:Color contrast')._ratio
						if ratio{tmp, '222222'} < 4.5 then table.insert(result, 'color:#FFFFFF') end -- 222222 is the default text color in Vector
					end
				else
					table.insert(result, default)
					tmp = frame:expandTemplate{ title = title, args = {'thcolor', line, station} }
					if tmp ~= '' then
						table.insert(result, 'color:#' .. tmp)
					end
				end
			end
			result = table.concat(result, ';')
		else
			if style == 'subheader' then
				result = default
			else
				result = ''
			end
		end
	else
		if style == 'subheader' then
			result = default
		else
			result = ''
		end
	end

	return result
end

function p.style(frame)
	local args = getArgs(frame, {frameOnly = true})
	return p._style(args, frame)
end

function p.convert(frame)
	local args = frame.args
	local code = mw.text.split(mw.ustring.gsub(args[1], '^%s*{{(.*)}}%s*$', '%1'), '%s*}}%s*{{%s*')
	local system
	local group = 0
	local delete = {
		['s-rail'] = true,
		['s-rail-next'] = true,
		['s-rail-national'] = true,
		['s-start'] = true,
		['s-rail-start'] = true,
		['start'] = true,
		['s-end'] = true,
		['end'] = true
	}
	local order = {
		'line', 'left', 'right', 'to-left', 'to-right',
		'oneway-left', 'oneway-right', 'through-left', 'through-right',
		'reverse', 'reverse-left', 'reverse-right',
		'note-left', 'note-mid', 'note-right', 'transfer'
		-- circular: use module subpage
		-- state: not implemented
	}
	local replace = {
		['previous'] = 'left',
		['next'] = 'right',
		['type'] = 'to-left',
		['type2'] = 'to-right',
		['branch'] = 'type',
		['note'] = 'note-left',
		['notemid'] = 'note-mid',
		['note2'] = 'note-right',
		['oneway1'] = 'oneway-left',
		['oneway2'] = 'oneway-right',
		['through1'] = 'through-left',
		['through2'] = 'through-right'
	}
	local remove_rows = {}
	local data = {}
	for i, v in ipairs(code) do
		code[i] = mw.ustring.gsub(code[i], '\n', ' ')
		local template = mw.ustring.lower(mw.text.trim(mw.ustring.match(code[i], '^[^|]+')))
		code[i] = mw.ustring.match(code[i], '(|.+)$')
		if template == 's-line' then
			data[i] = {}
			local this_system = mw.text.trim(mw.ustring.match(code[i], '|%s*system%s*=([^|]+)'))
			code[i] = mw.text.split(code[i], '%s*|%s*')
			for m, n in ipairs(code[i]) do
				local tmp = mw.text.split(n, '%s*=%s*')
				if tmp[3] then
					tmp[2] = mw.ustring.gsub(n, '^.-%s*=', '')
				end
				tmp[1] = replace[tmp[1]] or tmp[1]
				if tmp[2] then
					-- checks for matching brackets
					local curly = select(2, mw.ustring.gsub(tmp[2], "{", ""))-select(2, mw.ustring.gsub(tmp[2], "}", ""))
					local square = select(2, mw.ustring.gsub(tmp[2], "%[", ""))-select(2, mw.ustring.gsub(tmp[2], "%]", ""))
					if not (curly+square==0) then
						local count = mw.clone(m)+1
						while not (curly+square==0) do
							tmp[2] = tmp[2]..'|'..code[i][count]
							curly = curly+select(2, mw.ustring.gsub(code[i][count], "{", ""))-select(2, mw.ustring.gsub(code[i][count], "}", ""))
							square = square+select(2, mw.ustring.gsub(code[i][count], "%[", ""))-select(2, mw.ustring.gsub(code[i][count], "%]", ""))
							code[i][count] = ''
							count = count+1
						end
					end
					data[i][tmp[1]] = tmp[2]
				end
			end
			if (this_system ~= system) or (not system) then
				system = this_system
				data[i]['system'] = system
			else
				data[i]['system'] = nil
			end
			local last = data[i-1] or data[i-2] or data[i-3]
			if last then
				for r, s in pairs({
					['hide1'] = {'left', 'to-left', 'note-left', 'oneway-left'},
					['hide2'] = {'right', 'to-right', 'note-right', 'oneway-right'},
					['hidemid'] = {'type', 'note-mid'}
					}) do
					if data[i][r] then
						for m, n in ipairs(s) do
							if not data[i][n] then
								data[i][n] = last[n]
							end
						end
					end
				end
			end
			code[i] = {}
			local X = '|'
			local Y = (i+group)..'='
			if data[i]['system'] then
				table.insert(code[i], '|system')
				table.insert(code[i], Y)
				table.insert(code[i], data[i]['system'])
				table.insert(code[i], '\n')
			end
			for m, n in ipairs(order) do
				if data[i][n] then
					table.insert(code[i], X)
					table.insert(code[i], n)
					table.insert(code[i], Y)
					table.insert(code[i], data[i][n])
				end
			end
			code[i] = table.concat(code[i])
		elseif template == 's-note' then
			code[i] = mw.ustring.gsub(code[i], '|%s*text%s*=', '|header'..i+group..'=')
			code[i] = mw.ustring.gsub(code[i], '|%s*wide%s*=[^|]*', '')
		elseif template == 's-text' then
			code[i] = mw.ustring.gsub(code[i], '|%s*text%s*=', '|note-row'..i+group..'=')
		elseif delete[template] then
			code[i] = ''
			table.insert(remove_rows, 1, i) -- at the start, so that the rows are deleted in reverse order
			group = group-1
		end
	end
	for i, v in ipairs(remove_rows) do
		table.remove(code, v)
	end
	code = table.concat(code, '\n')
	local t = {'{{Adjacent stations', '\n}}'}
	system = mw.ustring.match(code, '|system(%d*)=')
	code = mw.ustring.gsub(code, '\n\n+', '\n')
	if tonumber(system) > 1 then
		-- If s-line isn't the first template then the system will have to be moved to the top
		system = mw.ustring.match(code, '|system%d*=([^|]*[^|\n])')
		code = mw.ustring.gsub(code, '|system%d*=[^|]*', '')
		code = '\n|system1='..system..code
	elseif not mw.ustring.match(code, '^[^{%[]*|[^=|]+2=') then
		-- If there's only one parameter group then there's no need to have line breaks
		code = mw.ustring.gsub(code, '\n', '')
		code = mw.ustring.gsub(code, '(|[^=|]+)1=', '%1=')
		t[2] = '}}'
		if not mw.ustring.match(code, '[%[{]') then
			code = mw.ustring.gsub(code, '|[^=|]*=$', '')
			code = mw.ustring.gsub(code, '|[^=|]*$', '')
		end
	end
	if not mw.ustring.match(code, '[%[{]') then
		code = mw.ustring.gsub(code, '|[^=|]*=|', '|')
		code = mw.ustring.gsub(code, '|[^=|]*|', '|')
		code = mw.ustring.gsub(code, '|[^=|]*=\n', '\n')
		code = mw.ustring.gsub(code, '|[^=|]*\n', '\n')
	end
	return t[1]..code..t[2]
end

return p