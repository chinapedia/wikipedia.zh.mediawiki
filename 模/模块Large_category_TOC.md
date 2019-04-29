local p = {}

local azupper = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
local azlower = 'abcdefghijklmnopqrstuvwxyz'
local aejot = 'aejot'

function p.scrollable(frame)
	return main('scrollable')
end

function p.collapsible(frame)
	return main('collapsible')
end

function p.aejot(frame)
	return main('aejot')
end

function main(toc_type)
	-- It should be much faster to only process these once, and just re use them as variables
	local pageurl = mw.title.getCurrentTitle():fullUrl()
	local toc = mw.message.new('Toc'):plain()
	
	-- Highest level div
	local toc_frame = mw.html.create('div')
				:addClass('plainlinks')
				:addClass('hlist')
				:addClass('toc')
				-- :attr('id','toc')
				:css('display','block !important')
				:css('background','WhiteSmoke')
				:css('clear','both')
				:css('width','98%')

	-- Contains "Content: Top 0-9 A - Z"
	local header = mw.html.create('div')
				:attr('id','toctitle')
				:attr('class','toctitle')
				:css('background','WhiteSmoke')
	
	-- Contains all the rest
	local body_wrapper
	local body = mw.html.create('div')
				:css('text-align', 'center')
	
	if toc_type == 'collapsible' then
		toc_frame:addClass('NavFrame')
		header:addClass('NavHead')
		body:addClass('NavContent')
			:css('background','white')
			:css('display','none')
	elseif toc_type == 'scrollable' then
		body:css('overflow-x','scroll')
			:css('overflow-y','hidden')
			:css('white-space','nowrap')
	end
	
	local header_content = '<strong>'..toc..':</strong>' ..
						' ['..pageurl..' Top]' ..
						' ['..pageurl..'?from=0 0–9]'
	
	for i=1,26 do
		local letter = string.sub(azupper,i,i)
		header_content = header_content..' ['..pageurl..'?from='..letter..' '..letter..']'
	end
	
	header:wikitext(header_content)
	
	local body_content
	
	if toc_type == 'collapsible' then
		body_content = '<b>#</b> '
		body_wrapper = mw.html.create('code')
				:css('background','White')
	else
		body_content = '['..pageurl..'?from=* <b>*</b>] <b>#</b> '
		body_wrapper = mw.html.create('span')
	end
	
	for i=0,9 do
		body_content = body_content..' ['..pageurl..'?from='..i..' '..i..']'
	end
	
	local function atoz(letter)
		local azlist
		local letterlist
		local maxind
		if toc_type == 'aejot' then
			letterlist = aejot
			maxind = 5
		else
			letterlist = azlower
			maxind = 26
		end
				
		if toc_type == 'aejot' or toc_type == 'scrollable' then
			azlist = ' • <b>'..letter..'</b> '
		else
			azlist = '<br /><b>'..letter..'</b> '
		end
			
		for i=1,maxind do
			local lowerletter = string.sub(letterlist,i,i)
			azlist = azlist..' ['..pageurl..'?from='..letter..lowerletter..' '..letter..lowerletter..'] '
		end
		return azlist
	end
	
	for i=1,26 do
		local letter = string.sub(azupper,i,i)
		body_content = body_content..atoz(letter)
	end
	
	body_wrapper:wikitext(body_content)
	body:node(body_wrapper)
	toc_frame:node(header)
	toc_frame:node(body)
	
	return '__NOTOC__\n'..tostring(toc_frame)
end

return p