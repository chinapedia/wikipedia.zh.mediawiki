-- This module implements {{Ancient Olympiads}}. It converts a year in the Julian
-- calendar to the equivalent year of the ancient Greek era organized by Olympiads.

local data = mw.loadData( 'Module:Ancient Olympiads/data' )
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
		if inputYear - 1 == t.year then
			-- year of the Olympiad, test with = p._main( -495 )
			-- The input year in the calendar is one after the expected (-775 for the year 776 BC). This is why all values need to be corrected by 1. 
			-- Year of Olympiad creates autolink to same page, therefore eliminated here
			return string.format(
				'%s [[Olympiad|Olympiad]] ([[%s|victor]][[Winner_of_the_Stadion_race|)¹]]',
				t.numberOl, t.winner
			)
		end
        if inputYear > t.year then
			-- Years 2-4 of the Olympiad, test with = p._main( -494 )  etc.
			-- It would be nice, if the string could be as follows:
			-- '[[%s|%s]] [[Olympiad|Olympiad]], [[%d_BC|year %d]]',
			-- t.numberOl, inputYear * - 1 + 1, inputYear - t.year
			-- but unfortunately it links to the very same page and won't be displayed as a link but in bold.
			return string.format(
				'[[%s|%s]] [[Olympiad|Olympiad]], year %d',
				t.yearBC, t.numberOl, inputYear - t.year 
			)
		end
	end

	-- If input year is before 776 BC (-775), the year of the first Olympiad.
	return string.format(
		'%d before [[776_BC|1st]] [[Olympiad|Olympiad]]',
		inputYear * -1 - 775
	)
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