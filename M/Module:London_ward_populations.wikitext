-- This module implements [[Template:London_ward_populations|Template:London ward populations]].

local p = {}

function p._main(args, frame)
	if not args[1] then
		return nil
	elseif args[1] == 'year' then
		return 2011
	elseif args[1] == 'reference' then
		frame = frame or mw.getCurrentFrame()
		local cite = frame:expandTemplate{title = 'Cite web', args = {
			title      = '2011 Census Ward Population Estimates',
			url        = 'http://data.london.gov.uk/2011-census-ward-pop',
			publisher  = 'Greater London Authority',
			author     = 'Census Information Scheme',
			year       = 2012,
			accessdate = '30 January 2013'
		}}
		return frame:extensionTag{
			name = 'ref',
			args = {name = 'pop_ref_london'},
			content = cite,
		}
	elseif not args[2] then
		return nil
	else
		local data = mw.loadData('Module:London ward populations/data')
		local boroughData = data[args[1]]
		if boroughData then
			return boroughData[args[2]]
		else
			return nil
		end
	end
end

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {
		wrappers = 'Template:London ward populations'
	})
	return p._main(args, frame)
end

return p