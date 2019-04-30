require('Module:No globals')
local getArgs = require('Module:Arguments').getArgs

local p = {}

--[[--------------------------< I S _ S E T >------------------------------------------------------------------

Whether variable is set or not.  A variable is set when it is not nil and not empty.

]]

local function is_set( var )
	return not (var == nil or var == '');
end


--[[--------------------------< M A I N >----------------------------------------------------------------------

Template entry point.  This function takes up to two unnamed positional parameters:
	1 = coordinate string typically from a call to Wikidata like this: {{#property:P625|from=Q...}}
	2 = coordinate parameters; see Template:Coord
	
Also takes the named parameters |display=, |format=, |name=, |notes= which it passes on to {{coord}}

Reformats the Wikidata coordinate string into unnamed parameters for {{coord}}

{{#invoke:WikidataCoord|main|{{#property:P625|from={{{1}}}}}|{{{2}}}|display={{{display}}}|format={{{format}}}|name={{{name}}}|notes={{{notes}}}}}

]]

function p.main (frame)
	local args = getArgs(frame);
	local lat_long = {};														-- table of lat/long coords extracted from wikidata return 
	
	if not is_set (args[1]) then												-- in case wikidata returns nothing (happens when Q... is wrong)
		return '<span style="font-size:100%" class="error">{{WikidataCoord}} – missing coordinate data</span>';		-- error message and quit
	elseif mw.ustring.match (args[1], '%d+°%d+&#39;[%d%.]+"[NS],%s*%d+°%d+&#39;[%d%.]+"[EW]') then			-- if the returned data looks like 55°13&#39;12"N, 23°17&#39;17"E
		lat_long[1], lat_long[2], lat_long[3], lat_long[4], lat_long[5], lat_long[6], lat_long[7], lat_long[8] =	-- parse it into the table
			mw.ustring.match (args[1], '(%d+)°(%d+)&#39;([%d%.]+)"([NS]),%s*(%d+)°(%d+)&#39;([%d%.]+)"([EW])')
	elseif mw.ustring.match (args[1], '%d+°%d+&#39;[NS],%s*%d+°%d+&#39;[EW]') then									-- if the returned data looks like 54°24&#39;N, 25°25&#39;E
		lat_long[1], lat_long[2], lat_long[3], lat_long[4], lat_long[5], lat_long[6] =								-- parse it into the table
			mw.ustring.match (args[1], '(%d+)°(%d+)&#39;([NS]),%s*(%d+)°(%d+)&#39;([EW])')
	elseif mw.ustring.match (args[1], '%d+°%d+[′\'][%d%.]+[″\"][NS],?%s*%d+°%d+[′\'][%d%.]+[″\"][EW]') then			-- when args[1] is a dms string that uses quotes or primes
		lat_long[1], lat_long[2], lat_long[3], lat_long[4], lat_long[5], lat_long[6], lat_long[7], lat_long[8] =	-- parse it into the table
			mw.ustring.match (args[1], '(%d+)°(%d+)[′\']([%d%.]+)[″\"]([NS]),?%s*(%d+)°(%d+)[′\']([%d%.]+)[″\"]([EW])')
	elseif mw.ustring.match (args[1], '%d+°%d+[′\'][NS],?%s*%d+°%d+[′\'][EW]') then									-- when args[1] is a dms string that uses quotes or primes, bit shorter format
		lat_long[1], lat_long[2], lat_long[3], lat_long[4], lat_long[5], lat_long[6] =								-- parse it into the table
			mw.ustring.match (args[1], '(%d+)°(%d+)[′\']([NS]),?%s*(%d+)°(%d+)[′\']([EW])')
	elseif mw.ustring.match (args[1], '%d+%.?%d*°[NS],?%s*%d+%.?%d*°[EW]') then										-- when args[1] is a decimal degrees string
		lat_long[1], lat_long[2], lat_long[3], lat_long[4] =														-- parse it into the table
			mw.ustring.match (args[1], '(%d+%.?%d*)°([NS]),?%s*(%d+%.?%d*)°([EW])')
	else
		return '<span style="font-size:100%" class="error">{{WikidataCoord}} – malformed coordinate data</span>';	-- wikidata returned something else
	end

	if is_set (args[2]) then													-- coordinate parameters are in second unnammed positional parameter
		if is_set (lat_long[5]) then											-- set when args[1] format is dms
			lat_long[9]	= args[2];
		else
			lat_long[5]	= args[2];												-- this one when args[1] is decimal degrees format
		end
	end
	if is_set (args.display) then
		lat_long.display = args.display;
	end
	if is_set (args.format) then
		lat_long.format = args.format;
	end
	if is_set (args.name) then
		lat_long.name = args.name;
	end
	if is_set (args.notes) then
		lat_long.notes = args.notes;
	end


	return frame:expandTemplate{title = 'coord', args = lat_long}				-- invoke template {{coord}} with wikidata lat/long
end

return p;