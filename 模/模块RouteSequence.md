local p = {
    STATION_SEPARATOR = ' - ',
    DEFAULT_STATION_SUFFIX = '站',
    BLOCK_ALIGN_PATTERN = '##BLOCK_ALIGN##',
    BLOCK_START = ' < <div style="display:inline-block; text-align: ##BLOCK_ALIGN##; vertical-align:middle;">',
    BLOCK_START_PURE = '<div style="display:inline-block; text-align: ##BLOCK_ALIGN##; vertical-align:middle;">',
    BLOCK_LINE_SEPARATOR = '<br />',
    BLOCK_END = '</div> > ',
    BLOCK_END_PURE = '</div>'
}

p.sep_translate = {
    ['%%dash%%'] = '–',
    ['%%rarrow%%'] = '→',
    ['%%larrow%%'] = '←',
    ['%%darrow%%'] = '↔',
    ['%%ldarrow%%'] = '⇐',
    ['%%rdarrow%%'] = '⇒',
    ['%%ddarrow%%'] = '⇔'
}

p.station_suffix = p.DEFAULT_STATION_SUFFIX

function p.truncateEnds(s, l)
    if l == nil then l = 1 end
    return string.sub(s, l + 1, string.len(s) - l)
end

function p.appendStyle(s, a)
    s = mw.text.trim(s)
    if s == '' then
        return a
    elseif string.find(s, ';$') ~= nil then
        return s .. ' ' .. a
    else
        return s .. '; ' .. a
    end
end

function p.marshalStation(station_link, style, system_data, frame)
	local station_name
	
	function marshal(station_link, station_name, style)
	    if style == nil or mw.text.trim(style) == '' then
    	    return '[['_.._station_link_.._'|' .. station_name .. ']]'
    	else
        	return '[['_.._station_link_.._'|<span style="' .. style .. '">' .. station_name .. '</span>]]'
    	end
	end
	
	if system_data ~= nil and system_data.stationNames[station_link] ~= nil then
        local i, datum
        local repr = ''
        local station_parts
        local station_data = system_data.stationNames[station_link]
        
        if type(station_data) ~= 'table' then
            station_data = {station_data, }
        end
        for i, datum in ipairs(station_data) do
            if string.find(datum, '|', 1, true) == nil or string.find(datum, '[[', 1, true) ~= nil then
                repr = repr .. datum
            else
                station_parts = mw.text.split(datum, '|')
                station_link = station_parts[1]
                station_name = table.concat(station_parts, '|', 2)
                if frame ~= nil and string.find(station_name, '{', 1, true) ~= nil then
                    station_name = frame:preprocess(table.concat(station_parts, '|', 2))
                end
                repr = repr .. marshal(station_link, station_name, style)
            end
        end
        return repr
    else
        local link_name_split = mw.text.split(station_link, '!')
        if table.getn(link_name_split) == 1 then
            station_name, match = string.gsub(station_link, p.station_suffix .. ' +%(.+%)$', '')
            if match == 0 then
                station_name, match = string.gsub(station_link, p.station_suffix .. '$', '')
            end
            if match == 0 then
                station_name = station_link
                station_link = station_link .. p.station_suffix
            end
        else
            station_link = link_name_split[1]
            station_name = link_name_split[2]
        end
        return marshal(station_link, station_name, style)
    end
end

function p.parseLink(station_link, style, system_data, frame)
    local station_name, match
    local prefix, suffix = '', ''
    local link_name_split

    if string.find(station_link, "^%%.+%%$") ~= nil then
    	return p.renderPlain(p.truncateEnds(station_link), style, system_data, frame)
    end
    
    local has_decorator = true
    while has_decorator do
        local prefix_patterns = {
            ["^s.+s$"] = { prefix='<s>', suffix='</s>', len=1 },
            ["^'.+'$"] = { prefix="'", suffix="'", len=1 },
            ["^%(.+%)$"] = { prefix='(', suffix=')', len=1 },
            ["^（.+）$"] = { prefix='（', suffix='）', len=1 },
        }
        has_decorator = false
        if string.find(station_link, "^g.+g$") ~= nil then
            station_link = p.truncateEnds(station_link)
            style = p.appendStyle(style, 'color:gray')
            has_decorator = true
        end
        for patt, ps in pairs(prefix_patterns) do
            if string.find(station_link, patt) ~= nil then
                station_link = p.truncateEnds(station_link, ps.len)
                prefix = ps.prefix .. prefix
                suffix = suffix .. ps.suffix
                has_decorator = true
            end
        end
    end
	return prefix .. p.marshalStation(station_link, style, system_data, frame) .. suffix
end

function p.renderPlain(text, style, system_data, frame)
    local spos, epos, station_name = 1, 1, nil
    local out_text = ''
    local pos = 1
	while spos ~= nil do
		spos, epos, station_name = string.find(text, '%$([^%$]+)%$', pos)
		if spos ~= nil then
			out_text = out_text .. string.sub(text, pos, spos - 1) .. p.parseLink(station_name, style, system_data, frame)
			pos = epos + 1
		else
			out_text = out_text .. string.sub(text, pos, string.len(text))
		end
	end
	return out_text
end

function p.splitStationExpr(station)
    local new_split = {}
    local separators = {}
    local last_element, cur_element
    local cur_separator = ''
    local station_split = mw.text.split(station, '#')

    for i, spart in ipairs(station_split) do
        if i > 1 and (string.find(last_element, '&$') ~= nil  -- process html escapes, i.e., ` `
            or string.find(last_element, ': *$') ~= nil       -- process CSS color, i.e., `color: #cccccc`
            or string.find(last_element, '= *$') ~= nil       -- process old-fashioned property without quotes, i.e., `<font color=#cccccc>`
            or string.find(last_element, '= *\" *$') ~= nil   -- process old-fashioned property with quotes, i.e., `<font color="#cccccc">`
            ) then
            table.remove(new_split)
            table.remove(separators)
            cur_element = last_element .. '#' .. spart
        elseif i > 1 and spart == '' then
            table.remove(new_split)
            table.remove(separators)
            cur_separator = ' '
            cur_element = last_element
        else
            cur_element = spart
        end
        table.insert(new_split, cur_element)
        table.insert(separators, cur_separator)
        cur_separator = ''
        last_element = cur_element
    end
    return new_split, separators
end

function p.parseStation(station, style, system_data, frame)
    local station_str, station_link
    local station_prefix, station_suffix
    local station_split, station_seps = p.splitStationExpr(station, '#')
    
    if table.getn(station_split) == 1 then
        station_prefix = ''
        station_expr = mw.text.trim(station_split[1])
        station_suffix = ''
    elseif table.getn(station_split) == 2 then
        station_prefix = mw.text.trim(station_split[1]) .. station_seps[1]
        station_expr = mw.text.trim(station_split[2])
        station_suffix = ''
    elseif table.getn(station_split) == 3 then
        if mw.text.trim(station_split[1]) ~= '' then
            station_prefix = mw.text.trim(station_split[1]) .. station_seps[1]
        else
            station_prefix = ''
        end
        station_expr = mw.text.trim(station_split[2])
        station_suffix = station_seps[2] .. mw.text.trim(station_split[3])
    end
    if station_prefix ~= '' then
    	station_prefix = p.renderPlain(station_prefix, style, system_data, frame)
	end
    if station_suffix ~= '' then
    	station_suffix = p.renderPlain(station_suffix, style, system_data, frame)
	end
    station_link = p.parseLink(mw.text.trim(station_expr), style, system_data, frame)
    station_str = station_prefix .. station_link .. station_suffix
    if station_prefix ~= '' or station_suffix ~= '' then
        station_str = '<span class="nowrap">' .. station_str .. '</span>'
    end

    return station_str
end

function p.processRoute(route_str, gstyle, condition, system, frame)
    if gstyle == nil then
        gstyle = ''
    end
    if condition == nil then
        condition = ''
    end
    
    local style = gstyle
    local out_style = gstyle
    
    local stations = mw.text.split(route_str, '~')
    local output_str = ''

    local condition = mw.text.trim(condition)
    local cond_expr, conds, cond, raw_cond
    local cond_met = true
    
    local gray_state, italic_state = false, false
    
    local block_level = 0
    local block_align
    local station_index = 0

    local separator
    local next_separator = p.STATION_SEPARATOR
    local user_separator = p.STATION_SEPARATOR
    
    local system_data = nil
    if system ~= nil and mw.text.trim(system) ~= '' then
        system_data = mw.loadData("Module:RailSystems/" .. system)
    end

    for i, station in ipairs(stations) do
        station = mw.text.trim(station)
        if string.find(station, '^style *=') ~= nil then
            style = mw.text.trim(mw.text.split(station, '=')[2])
            if style == '' then
                style = gstyle
            end
        elseif string.find(station, '^con *=') ~= nil then
            cond_expr = mw.text.trim(mw.text.split(station, '=')[2])
            if cond_expr == '' then
                cond_met = true
            else
                conds = mw.text.split(cond_expr, '#')
                cond_met = false
                for i, cond in ipairs(conds) do
                    raw_cond = mw.text.trim(cond)
                    if string.find(raw_cond, '^- *') ~= nil then
                        raw_cond = string.gsub(raw_cond, '^- *', '')
                        if mw.text.trim(raw_cond) ~= condition then
                            cond_met = true
                            break
                        end
                    else
                        if mw.text.trim(raw_cond) == condition then
                            cond_met = true
                            break
                        end
                    end
                end
            end
        elseif string.find(station, '^sep *=') ~= nil then
            separator = mw.text.trim(mw.text.split(station, '=')[2])
            if separator == '' then
                separator = p.STATION_SEPARATOR
            else
                separator = ' ' .. separator .. ' '
                for spatt, sep in pairs(p.sep_translate) do
                    separator = string.gsub(separator, spatt, sep)
                end
            end
            next_separator = separator
            user_separator = separator
        elseif station == 'blstart' then
            block_level = block_level + 1
            if station_index > 0 then
                next_separator = string.gsub(p.BLOCK_START, p.BLOCK_ALIGN_PATTERN, 'left')
            else
                next_separator = string.gsub(p.BLOCK_START_PURE, p.BLOCK_ALIGN_PATTERN, 'right')
            end
        elseif string.find(station, '^blstart *=') ~= nil then
            block_level = block_level + 1
            block_align = mw.text.trim(mw.text.split(station, '=')[2])
            if station_index > 0 then
                next_separator = string.gsub(p.BLOCK_START, p.BLOCK_ALIGN_PATTERN, block_align)
            else
                next_separator = string.gsub(p.BLOCK_START_PURE, p.BLOCK_ALIGN_PATTERN, block_align)
            end
        elseif station == 'blline' then
            next_separator = p.BLOCK_LINE_SEPARATOR
        elseif station == 'blend' then
            block_level = block_level - 1
            next_separator = p.BLOCK_END
        elseif station == 'gstart' then
            gray_state = true
        elseif station == 'gend' then
            gray_state = false
        elseif station == 'istart' then
            italic_state = true
        elseif station == 'iend' then
            italic_state = false
        elseif station == 'line' then
            while block_level > 0 do
                block_level = block_level - 1
                output_str = output_str .. p.BLOCK_END_PURE
            end
            next_separator = '<br />'
        elseif cond_met then
            station_index = station_index + 1
            if station_index > 1 or block_level > 0 then
                output_str = output_str .. next_separator
            end
            out_style = style
            if gray_state then
                out_style = p.appendStyle(style, 'color:gray')
            end
            if italic_state then
                out_style = p.appendStyle(style, 'font-style:italic')
            end
            output_str = output_str .. p.parseStation(station, out_style, system_data, frame)
            next_separator = user_separator
        end
    end
    while block_level > 0 do
        block_level = block_level - 1
        output_str = output_str .. p.BLOCK_END_PURE
    end
    return output_str
end

function p.route(frame)
    local gstyle = frame.args['style']
    local route_str = frame.args['stations']
    local condition = frame.args['condition']
    local system = frame.args['system']

    p.station_suffix = mw.text.trim(frame.args['station_suffix'] or p.DEFAULT_STATION_SUFFIX)

    return p.processRoute(string.gsub(route_str, '\n', ''), gstyle, condition, system, frame)
end

function p.testCase(frame)
    local result
    cases = {
        {
            {stations='东环南路 ~ style=color:gray ~ 邱隘东站 ~ 宝幢站 (地铁) ~ style= ~ 邬隘站 (地铁)'},
            '[[东环南路站|东环南路]] - [[邱隘东站|<span style="color:gray">邱隘东</span>]] - [[宝幢站_(地铁)|<span style="color:gray">宝幢</span>]] - [[邬隘站_(地铁)|邬隘]]'
        },
        {
            {stations='东环南路 ~ gstart ~ 邱隘东站 ~ 宝幢站 (地铁) ~ gend ~ 邬隘站 (地铁)'},
            '[[东环南路站|东环南路]] - [[邱隘东站|<span style="color:gray">邱隘东</span>]] - [[宝幢站_(地铁)|<span style="color:gray">宝幢</span>]] - [[邬隘站_(地铁)|邬隘]]'
        },
        {
            {stations='（$高桥西$方向）#东环南路 ~ 霞浦 ~ 左边站!右边 ~ %原来的东西%', system='UseCase'},
            '<span class="nowrap">（[[高桥西站_(宁波)|高桥西]]方向）[[东环南路站|东环南路]]</span> - [[霞浦站_(宁波)|霞浦]] - [[左边站|右边]] - 原来的东西'
        },
    }
    for _idx, case in ipairs(cases) do
        result = p.route{args=case[1]}
        if result ~= case[2] then
            error('Test ' .. tostring(_idx) .. ' failed.\nExpect: ' .. case[2] .. '\nActual: ' .. result)
        end
    end
end
 
return p