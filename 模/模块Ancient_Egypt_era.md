-- This module implements {{Ancient Egypt era}}. It converts a year in the Gregorian
-- calendar to the equivalent year of the ancient Egyptian era organized by dynasties and kings.

local data = mw.loadData( 'Module:Ancient Egypt era/data' )
local lang = mw.language.getContentLanguage()

local p = {}

function p._main( inputYear )
	-- Convert the input to an integer if possible. Return "N/A" if the input could
	-- not be converted, or if the converted input is too big or too small.
	inputYear = tonumber( inputYear )
	if not inputYear or inputYear > tonumber( lang:formatDate( 'Y' ) ) then
		return "''N/A''"
	end

	-- Find the length of the data.
	-- We need the length of the data so that we can loop through it backwards.
	-- Normally we can get the length of tables with the # operator, but this
	-- doesn't work with mw.loadData, as mw.loadData uses a metatable, and the
	-- # operator doesn't work for tables that use metatables.
	local dataLength = 0
	for i, t in ipairs( data ) do
		dataLength = i
	end

	-- Find the year in the data page and display the output.
	for i = dataLength, 1, -1 do
		local t = data[i]
		if inputYear - 1 >= t.dynstart and inputYear - 1 <= t.dynend then
			-- year of the dynasty, test with = p._main( -495 )
			-- The input year in the calendar is one after the expected (-775 for the year 776 BC). This is why all values need to be corrected by 1. 
			return string.format(
				'[[%s|%s]] [[List_of_ancient_Egyptian_dynasties|dynasty]], %d',
				t.dynlink, t.dynasty, inputYear - t.dynstart
			)
		end
	end
end

function p.main( frame )
	-- If you only want to run this module from another Lua module, you can get
	-- rid of this function entirely. This function is only used if you want to
	-- run this individual module from a template.
	local args = require( 'Module:Arguments' ).getArgs( frame, {
		parentOnly = true
	} )
	return p._main( args[ 1 ] )
end

return p