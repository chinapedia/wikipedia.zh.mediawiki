local p = { }

local Navbox = require('Module:Navbox')
local Styles = require('Module:WPMILHIST Infobox style')

local function isblank(s)
	return (not s) or s == ''
end
local function isnotblank(s)
	return s and s ~= ''
end

function p.main(frame)
    local args = { }
    local pargs = frame:getParent().args
    local sargs = {}
    local tcats = ''

	-- process bodystyle and titlestyle
	if (pargs['style'] or '') == 'wide' then
		args['titlestyle'] = Styles['nav_box_wide_header']
		args['bodystyle'] = Styles['nav_box_wide']
	else
		args['titlestyle'] = Styles['nav_box_header']
		if (pargs['border'] or '') == 'child' or 
			(pargs['border'] or '') == 'subgroup' then
			args['bodystyle'] = Styles['nav_box_child']
			tcats = tcats .. '[[Category:使用军事导航subgroup而没有使用wide_style的的页面|Category:使用军事导航subgroup而没有使用wide style的的页面]]'
		else
			args['bodystyle'] = Styles['nav_box']
		end
	end
	sargs['titlestyle'] = 1
	sargs['bodystyle'] = 1

	-- process groupstyle, abovestyle, belowstyle
	args['groupstyle'] = Styles['nav_box_label'] .. (pargs['groupstyle'] or '')
	sargs['groupstyle'] = 1
	args['abovestyle'] = Styles['nav_box_label'] .. (pargs['abovestyle'] or '')
	sargs['abovestyle'] = 1
	args['belowstyle'] = Styles['nav_box_label'] .. (pargs['belowstyle'] or '')
	sargs['belowstyle'] = 1
	-- process oddstyle, evenstyle
	args['oddstyle'] = isnotblank(pargs['odd_color'])
		and ('background:' .. pargs['odd_color']) or nil
	sargs['oddstyle'] = 1
	args['evenstyle'] = isnotblank(pargs['even_color'])
		and ('background:' .. pargs['even_color']) or nil
	sargs['evenstyle'] = 1
	-- process name and rawname
	args['name'] = (isnotblank(pargs['name']) and pargs['name']) or pargs['rawname']
	if isblank(args['name']) then args['navbar'] = 'plain' end
	sargs['name'] = 1
	sargs['rawname'] = 1
	
    -- copy the remaining args
    for k, v in pairs(pargs) do
        if v and v ~= '' and sargs[k] == nil then
            args[k] = v
        end
    end
	-- add allow wrap
	if args['title'] and (pargs['style'] or '') ~= 'wide' then
		if not mw.ustring.match(args['title'], '<span class="wrap">') then
			-- probably a more efficient way to match 15 or more characters
			local m = '[^%[%]<>|][^%[%]<>|][^%[%]<>|][^%[%]<>|][^%[%]<>|]'
			m = m .. m .. m
			args['title'] = mw.ustring.gsub(args['title'], 
				'%[%[(' .. m .. '[^%[%]<>|]*)%]%]', 
				'[[%1|<span class="wrap">%1</span>]]')
			args['title'] = mw.ustring.gsub(args['title'], 
				'%[%[([^%[%]<>|]*)|(' .. m .. '[^%[%]<>|]*)%]%]', 
				'[[%1|<span class="wrap">%2</span>]]')
		end
	end
    return tcats .. Navbox._navbox(args)

end  

return p