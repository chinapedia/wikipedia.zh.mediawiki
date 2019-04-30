-- This module implements {{Episode table}} and {{Episode table/part}}.

local HTMLcolor = mw.loadData( 'Module:Color contrast/colors' )

--------------------------------------------------------------------------------
-- EpisodeTable class
-- The main class.
--------------------------------------------------------------------------------

local contrast_ratio = require('Module:Color contrast')._ratio
local EpisodeTable = {}

function EpisodeTable.cell(background, width, text, reference)
	local cell = mw.html.create('th')
	
	-- Cell
	cell:attr('scope','col')
		:css('background',background or '#CCCCFF')
		:css('width',width ~= '' and width .. '%' or nil)
		:wikitext(text)
	
	-- Reference
	if reference then
		cell:wikitext(" " .. EpisodeTable.reference(reference, background))
	end
	
	return cell
end

function EpisodeTable.reference(reference, background)
	local link1_cr = contrast_ratio{'#0645AD', background or '#CCCCFF', ['error'] = 0}
	local link2_cr = contrast_ratio{'#0B0080', background or '#CCCCFF', ['error'] = 0}
	
	local refspan = mw.html.create('span')
		:wikitext(reference)
	
	if link1_cr < 7 or link2_cr < 7 then
		refspan
			:css('background-color','white')
			:css('padding','1px')
			:css('display','inline-block')
			:css('line-height','50%')
	end
	
	return tostring(refspan)
end

function EpisodeTable.abbr(text,title)
	local abbr = mw.html.create('abbr')
		:attr('title',title)
		:wikitext(text)
	return tostring(abbr)
end

function EpisodeTable.part(frame,args)
	local row = mw.html.create('tr')
	
	local black_cr = contrast_ratio{args.c, 'black', ['error'] = 0}
	local white_cr = contrast_ratio{'white', args.c, ['error'] = 0}
	
	local displaytext = (not args.nopart and 'Part ' or '') .. (args.p or '')
	
	row:tag('td')
		:attr('colspan',13)
		:css('text-align','center')
		:css('background-color', args.c)
		:css('color', black_cr > white_cr and 'black' or 'white')
		:wikitext("'''" .. frame:expandTemplate({title='Visible anchor',args={displaytext}}) .. "'''" .. (args.r and " " .. EpisodeTable.reference(args.r, args.c) or ''))
	
	return tostring(row)
end

function EpisodeTable.new(args)
	args = args or {}
	local categories = ''
	local background = (args.background and args.background ~= '' and args.background ~= '#') and args.background or nil
	
	-- Add # to background if necessary
	if background ~= nil and HTMLcolor[background] == nil then
		background = '#'..(mw.ustring.match(background, '^[%s#]*([a-fA-F0-9]*)[%s]*$') or '')
	end
	
	-- Create episode table
	local root = mw.html.create('table')
	
	root
		:addClass('wikitable')
		:addClass('plainrowheaders')
		:addClass('wikiepisodetable')
		:css('width', args.total_width and string.gsub(args.total_width,'%%','') .. '%' or '100%')
	
	-- Caption
	if args.caption then
		root:tag('caption'):wikitext(args.caption)
	end
	
	-- Colour contrast; add to category only if it's in the mainspace
	local title = mw.title.getCurrentTitle()
	local black_cr = contrast_ratio{background, 'black', ['error'] = 0}
	local white_cr = contrast_ratio{'white', background, ['error'] = 0}
	
	if title.namespace == 0 and (args.background and args.background ~= '' and args.background ~= '#') and black_cr < 7 and white_cr < 7 then
		categories = categories .. '[[Category:使用Template:Episode_table含有無效顏色組合的條目|Category:使用Template:Episode table含有無效顏色組合的條目]]' 
	end
	
	-- Main row
	local mainRow = root:tag('tr')
	mainRow
		:css('color', background and (black_cr > white_cr and 'black' or 'white') or 'black')
		:css('text-align', 'center')
	
	-- Cells
	do
		local used_season = false
		local country = args.country ~= '' and args.country ~= nil
		local viewers = (country and args.country or '') .. '收视人数' ..
			((not args.viewers_type or args.viewers_type ~= '') and '<br />（' .. (args.viewers_type or '百万') .. '）' or '')
		
		local cellNames = {
			{'overall','EpisodeNumber','总集数','全部集数'},
			{'season','EpisodeNumber2','集数','本系列集数'},
			{'series','EpisodeNumber2Series','续集数','续集数'},
			{'title','Title','标题'},
			{'aux1','Aux1',''},
			{'director','DirectedBy','导演'},
			{'writer','WrittenBy','编剧'},
			{'aux2','Aux2',''},
			{'aux3','Aux3',''},
			{'airdate','OriginalAirDate',(args.released and '上线' or '首播') .. '日期'},
			{'altdate','AltDate',''},
			{'prodcode','ProdCode','制作<br />代码'},
			{'aux5','Aux5',''},
			{'viewers','Viewers',viewers},
			{'aux4','Aux4',''}
		}
	
		for k,v in pairs(cellNames) do
			local thisCell = args[v[1]] or args[v[2]]
			if thisCell and (v[1] ~= 'series' or (v[1] == 'series' and used_season == false)) then
				if v[1] == 'season' then used_season = true end
				if (k <= 3 and thisCell == '') then thisCell = '5' end
				
				local thisCellT = args[v[1] .. 'T'] or args[v[2] .. 'T']
				local thisCellR = args[v[1] .. 'R'] or args[v[2] .. 'R']
				mainRow:node(EpisodeTable.cell(background, thisCell, thisCellT or v[3], thisCellR))
			end
		end
	
		-- Episodes
		root:node(args.episodes)
	end
	
	return (args.dontclose and mw.ustring.gsub(tostring(root), "</table>", "") or tostring(root)) .. categories
end

--------------------------------------------------------------------------------
-- Exports
--------------------------------------------------------------------------------

local p = {}

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {
		removeBlanks = false,
		wrappers = 'Template:Episode table'
	})
	return EpisodeTable.new(args)
end

function p.part(frame)
	local args = require('Module:Arguments').getArgs(frame, {
		removeBlanks = false,
		wrappers = 'Template:Episode table/part'
	})
	return EpisodeTable.part(frame,args)
end

function p.ref(frame)
	local args = require('Module:Arguments').getArgs(frame, {
		removeBlanks = false,
	})
	return EpisodeTable.reference(args.r,args.b)
end

return p