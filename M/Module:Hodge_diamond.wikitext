-- This module implements {{hodge diagram}}

local p = {}

function p.diagram(frame)
	local args = (frame.args[3] ~= nil) and frame.args or frame:getParent().args
	local style = args['style'] or ''
	local width = args['width'] or '2.5em'
	local cstyle = args['cstyle'] or ''
	local caption = args['caption']
	local note = args['note']
	local entries = {}
	
	local argcount = 0
	for k, v in pairs( args ) do
        if type( k ) == 'number' then
           entries[ k ] = v
           argcount = argcount + 1
        end
    end
    local side = math.floor(math.sqrt(argcount))
    local rows = 2*side - 1
    
    local root = mw.html.create('table')
   	root
   		:css('text-align', 'center')
   		:cssText(style)
    
    if caption then  
    	root:tag('caption'):wikitext(caption)
    end

    local c = 1    
    for i = 1,side do
    	row = root:tag('tr')

    	for j = 1,(side-i) do
    		row:tag('td')
		end
		for k = 1,i do
			local cell = row:tag('td')
			cell
				:css('width', width)
				:cssText(cstyle)
				:wikitext(entries[c])
			if k < i then
				row:tag('td')
			else
				if i == side and note then
					row:tag('td'):wikitext(note)
				end
			end
			
			c = c + 1
		end
		for j = 1,(side-i) do
			row:tag('td')
		end
	end
	for i = 1,(side-1) do
		row = root:tag('tr')
    	for j = 1,i do
    		row:tag('td')
		end
		for k = 1,(side-i) do
			cell = row:tag('td')
			cell
				:css('width', width)
				:cssText(cstyle)
				:wikitext(entries[c])
			if k < (side-i) then row:tag('td') end
			c = c + 1
		end
		for j = 1,i do
    		row:tag('td')
		end
	end

	return tostring(root)
end
 
return p