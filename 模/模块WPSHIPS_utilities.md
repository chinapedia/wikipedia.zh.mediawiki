require('Module:No globals')

local wpsu={}


--[[-------------------------< S H I P  P R E F I X   L I S T >-----------------------------------------------

This is a list of currently supported ship prefixes.

To add to this list the form is:
	['prefix'] = true,
the trailing comma is important.

]]

local ship_prefix_list =
	{
	['ARA'] = true,																-- Armada de la República Argentina
	['ARC'] = true,																-- Armada Nacional de la República de Colombia
	['ARM'] = true,																-- Armada de la República Mexicana
	['ARV'] = true, 															-- Armada Republica de Venezuela
	['BAE'] = true,																-- Buque de la Armada de Ecuador
	['BAP'] = true,																-- Peruvian Navy Ship
	['BNS'] = true,																-- Bangladesh Navy Ship
	['BRP'] = true,																-- Barko ng Republika ng Pilipinas
	['CCGS'] = true,															-- Canadian Coast Guard Ship
	['CFAV'] = true,															-- Canadian Forces Auxiliary Vessel
	['CS'] = true,																-- Cable Ship
	['CSS'] = true,																-- Confederate States Ship
	['FGS'] = true,																-- Federal German Ship
	['GTS'] = true,																-- Gas Turbine Ship
	['HDMS'] = true,															-- His/Her Danish Majesty's Ship
	['HM'] = true,																-- His/Her Majesty's, then used with the type of ship in military use (UK)
	['HMAS'] = true,															-- Her/His Majesty's Australian Ship
	['HMBS'] = true,															-- Her/His Majesty's Britannic Ship (also: Bahamian, Bermudian, Burmese)
	['HMC'] = true,																-- Her/His Majesty's Cutter
	['HMCS'] = true,															-- Her/His Majesty's Canadian Ship (also Colonial)
	['HMHS'] = true,															-- His/Her Majesty's Hospital Ship
	['HMIS'] = true,															-- Her/His Majesty's Indian Ship (pre republic)
	['HMNZS'] = true,															-- Her/His Majesty's New Zealand Ship
	['HMPNGS'] = true,															-- His/Her Majesty's Papua New Guinea Ship
	['HMQS'] = true,															-- Her/His Majesty's Queensland Ship
	['HMRC'] = true,															-- His/Her Majesty's Revenue Cutter
	['HMS'] = true,																-- Her/His Majesty's Ship
	['HMSAS'] = true,															-- Her/His Majesty's South African Ship
	['HMT'] = true,																-- Her/His Majesty's Trawler
	['HMVS'] = true,															-- Her/His Majesty's Victorian Ship
	['HMY'] = true,																-- His/Her Majesty's Yacht
	['HNLMS'] = true,															-- His/Her Netherlands Majesty’s Ship
	['HNoMS'] = true,															-- His/Her Norwegian Majesty's Ship
	['HSwMS'] = true,															-- His/Her Swedish Majesty's Ship
	['HTMS'] = true,															-- His Thai Majesty's Ship
	['INS'] = true,																-- Indian Naval Ship, Israeli Naval Ship
	['JDS'] = true,																-- Japanese Defence Ship
	['JS'] = true,																-- Japanese Ship (post 2008)
	['KD'] = true,																-- Kapal Di-Raja — His Majesty's Ship (Malaysia)
	['KDM'] = true,																-- Kongelige Danske Marine
	['KRI'] = true,																-- Kapal Republik Indonesia
	['LÉ'] = true,																-- Long Éireannach – Irish ship
	['MF'] = true,																-- Motor Ferry
	['LKL'] = true,																-- Lietuvos Karinis Laivas – Lithuania
	['MS'] = true,																-- Motor Ship
	['MT'] = true,																-- Motor Tanker
	['MV'] = true,																-- Motor Vessel
	['NLV'] = true,																-- Northern Lighthouse Vessel
	['NMS'] = true,																-- Nava Majestăţii Sale (His/Her Majesty's Ship) - used before 1945 by the Royal Romanian Navy
	['NoCGV'] = true,															-- Norwegian Coast Guard Vessel
	['NOAAS'] = true,															-- National Oceanic and Atmospheric Administration Ship
	['NRP'] = true,																-- Navio da República Portuguesa
	['ORP'] = true,																-- Okręt Rzeczypospolitej Polskiej
	['PNS'] = true,																-- Pakistani Naval Ship
	['PS'] = true,																-- Paddle Steamer
	['RFA'] = true,																-- Royal Fleet Auxiliary
	['RMAS'] = true,															-- Royal Maritime Auxiliary Service
	['RMS'] = true,																-- Royal Mail Ship
	['RNLB'] = true,															-- Royal National Lifeboat
	['ROCS'] = true,															-- Republic of China Ship
	['ROKS'] = true,															-- Republic of Korea Ship
	['RPS'] = true,																-- Republic of the Philippines Ship
	['RRS'] = true,																-- Royal Research Ship
	['RSS'] = true,																-- Republic of Singapore Ship
	['RV'] = true,																-- Research Vessel
	['SAS'] = true,																-- South African Ship
	['SLNS'] = true,															-- Sri Lanka Naval Ship
	['SM'] = true,																-- Seiner Majestät Unterseeboot
	['SMS'] = true,																-- Seiner Majestät Schiff
	['SS'] = true,																-- Screw Steamer or Steamship
	['TCG'] = true,																-- Türkiye Cumhuriyeti Gemisi
	['TS'] = true,																-- Training ship
	['TV'] = true,																-- Training vessel
	['UAM'] = true,																-- Unidade Auxiliar da Marinha - Navy Auxiliary Unit (Portuguese Navy non-military ships)
	['USAFS'] = true,															-- United States Air Force ship
	['USAHS'] = true,															-- United States Army Hospital Ship
	['USAS'] = true,															-- United States Army Ship
	['USAT'] = true,															-- United States Army Transport
	['USAV'] = true,															-- United States Army Vessel
	['USC&GS'] = true,															-- United States Coast and Geodetic Survey
	['USC&GS'] = true,														-- United States Coast and Geodetic Survey (crude work-around)
	['USC&GS'] = true,														-- United States Coast and Geodetic Survey (crude work-around)
	['USC&GSS'] = true,															-- United States Coast and Geodetic Survey Ship
	['USC&GSS'] = true,														-- United States Coast and Geodetic Survey Ship (crude work-around)
	['USC&GSS'] = true,														-- United States Coast and Geodetic Survey Ship (crude work-around)
	['USCGC'] = true,															-- United States Coast Guard Cutter
	['USLHT'] = true,															-- United State Light House Tender
	['USNS'] = true,															-- United States Naval Ship
	['USRC'] = true,															-- United States Revenue Cutter
	['USS'] = true,																-- United States Ship
	}

--[[--------------------------< N A T I O N A L I T Y >--------------------------------------------------------

Article titles for ships in navies that do not use a standardized prefix follow the title format:
	<nationality> <ship type> <name> <(disambiguator)>

This is a list of nationalities. 

To add to this list the form is:
	['Nationality'] = true,
the trailing comma is important. Use the adjective form for nationality, always capitalize.  Please insert nationalities in alphabetical order.

]]

local nationality_list =
	{
	['Albanian'] = true,
	['American'] = true,
	['Australian'] = true,
	['Belgian'] = true,
	['Brazilian'] = true,
	['Bulgarian'] = true,
	['Chilean'] = true,	
	['Chinese'] = true,
	['Croatian'] = true,
	['Danish'] = true,
	['Dominican'] = true,
	['Dutch'] = true,
	['East Timorese'] = true,
	['Egyptian'] = true,
	['English'] = true,
	['Finnish'] = true,
	['French'] = true,
	['German'] = true,
	['Greek'] = true,
	['Grenadan'] = true,
	['Iranian'] = true,
	['Irish'] = true,
	['Italian'] = true,
	['Japanese'] = true,
	['Latvian'] = true,
	['Libyan'] = true,
	['Lithuanian'] = true,
	['Maltese'] = true,
	['Mexican'] = true,
	['Nigerian'] = true,
	['Ottoman'] = true,
	['Peruvian'] = true,
	['Portuguese'] = true,
	['Romanian'] = true,
	['Russian'] = true,
	['Scottish'] = true,
	['Slovenian'] = true,
	['Soviet'] = true,
	['Spanish'] = true,
	['Swedish'] = true,
	['Texan'] = true,
	['Ukrainian'] = true,
	['United States'] = true,
	['Vietnamese'] = true,
	['Yugoslav'] = true,
	}


--[[--------------------------< S H I P   T Y P E >------------------------------------------------------------

Article titles for ships in navies that do not use a standardized prefix follow the title format:
	<nationality> <ship type> <name> <(disambiguator)>

Article titles for ships may or may not be naval ships may follow the title format:
	<name> <(disambiguator)>
where <(disambiguator)> may be some form of ship type, hull designator or pennant number, or year.  This tool will
format ship names that contain a recognized ship type in <(disambiguator)>.

This list is used to <find ship> when the article title begins with a nationality.  This is important because the tool
needs to know where the <ship type> ends and <name> begins so that it can properly place the italic markup.  The search
will find an exact match (including case) for ship types that are 1 to 4 words long.

This list is also used to find ship type in <(disambiguator)>.  The search is whole word; use the simplest form.
For example, because 'icebreaker' is defined, that ship type is sufficient to cause the tool to properly format:
	Astrolabe (icebreaker)
	Krassin (1917 icebreaker)
	Taymyr (nuclear icebreaker)

Searches for ship type in <(disambiguator)> are whole word.  When looking for 'ship', the tool will find
	Auguste (ship)
	Queen of Nations (clipper ship)
but will not find:
	Sibir (steamship icebreaker) – the search for 'icebreaker' will

This is a list of ship types.  When adding new ship types, do not be too specific: 'aircraft carrier' but not 'light aircraft carrier'

To add to this list the form is:
	['ship type'] = true,
the trailing comma is important. At the time of this writing, a ship type may be one to four words, almost always lowercase.
Please insert ship types in alphabetical order.

]]

local ship_type_list =
	{
	['armoured cruiser'] = true,
	['aircraft carrier'] = true,
	['amphibious assault ship'] = true,
	['Army ship'] = true,														-- should be capitalized
	['auxiliary cruiser'] = true,
	['auxiliary raider'] = true,
	['auxiliary'] = true,
	['aviso'] = true,
	['barge'] = true,
	['barque'] = true,
	['barquentine'] = true,
	['battlecruiser'] = true,
	['battleship'] = true,
	['boat'] = true,
	['brig sloop'] = true,
	['brig-sloop'] = true,
	['brig'] = true,
	['brigantine'] = true,
	['carrack'] = true,
	['clipper'] = true,
	['coast defense ship'] = true,
	['coastal defence ship'] = true,
	['coastal defense ship'] = true,
	['communications ship'] = true,
	['corvette'] = true,
	['cruiser'] = true,
	['cutter'] = true,
	['deep submergence rescue vehicle'] = true,
	['destroyer leader'] = true,
	['destroyer'] = true,
	['dragger'] = true,
	['dredge'] = true,
	['East Indiaman'] = true,													-- should be capitalized
	['escort ship'] = true,
	['escort'] = true,
	['ferry'] = true,
	['ferryboat'] = true,
	['fireboat'] = true,
	['fleet oiler'] = true,
	['floating battery'] = true,
	['floating crane'] = true,
	['fluyt'] = true,
	['food supply ship'] = true,
	['freighter'] = true,
	['frigate'] = true,
	['galleon'] = true,
	['galley'] = true,
	['gunboat'] = true,
	['helicopter carrier'] = true,
	['hospital ship'] = true,
	['hovercraft'] = true,
	['hydrofoil'] = true,
	['icebreaker'] = true,
	['Indiaman'] = true,														-- should be capitalized
	['ironclad'] = true,
	['ketch'] = true,
	['landing ship medium'] = true,
	['lifeboat'] = true,
	['lightship'] = true,
	['log canoe'] = true,
	['lugger'] = true,
	['merchant cruiser'] = true,
	['minehunter'] = true,
	['minelayer'] = true,
	['minelaying cruiser'] = true,
	['minesweeper'] = true,
	['missile boat'] = true,
	['monitor'] = true,
	['munition ship'] = true,
	['naval ship'] = true,
	['night fighter direction vessel'] = true,
	['ocean liner'] = true,
	['oiler'] = true,
	['paddle steamer'] = true,
	['patrol boat'] = true,
	['patrol gunboat'] = true,
	['patrol vessel'] = true,
	['pinnace'] = true,
	['pollution control vessel'] = true,
	['privateer'] = true,
	['protected cruiser'] = true,
	['pusher'] = true,
	['rescue ship'] = true,
	['riverboat'] = true,
	['ROV'] = true,
	['sailboat'] = true,
	['schooner'] = true,
	['seaplane carrier'] = true,
	['seaplane tender'] = true,
	['ship of the line'] = true,
	['ship'] = true,
	['shipwreck'] = true,
	['shore establishment'] = true,												-- use stone frigate instead?
	['showboat'] = true,
	['sidewheeler'] = true,
	['skipjack'] = true,
	['sloop-of-war'] = true,
	['sloop'] = true,
	['smack'] = true,
	['snagboat'] = true,
	['speedboat'] = true,
	['steam frigate'] = true,
	['steam warship'] = true,
	['steamboat'] = true,
	['steamer'] = true,
	['steamship'] = true,
	['sternwheeler'] = true,
	['stores lighter'] = true,
	['submarine chaser'] = true,
	['submarine rescue vehicle'] = true,
	['submarine tender'] = true,
	['submarine'] = true,
	['submersible'] = true,
	['supertanker'] = true,
	['support ship'] = true,
	['survey ship'] = true,
	['tanker'] = true,
	['target ship'] = true,
	['tender'] = true,
	['torpedo boat'] = true,
	['torpedo gunboat'] = true,
	['towboat'] = true,
	['training cruiser'] = true,
	['training ship'] = true,
	['transport'] = true,
	['trawler'] = true,
	['trireme'] = true,
	['tug'] = true,
	['tugboat'] = true,
	['vessel'] = true,
	['warship'] = true,
	['weather ship'] = true,
	['whaler'] = true,
	['whaleship'] = true,
	['wherry'] = true,
	['yacht'] = true,
	['yawl'] = true,
	}


--[[--------------------------< I S _ S E T >------------------------------------------------------------------

Returns true if argument is set; false otherwise. Argument is 'set' when it exists (not nil) or when it is not an empty string.

]]
local function is_set( var )
	return not (var == nil or var == '');
end


--[[--------------------------< S I Z E O F _ S H I P _ T Y P E >----------------------------------------------

Returns the size in words of ship type.  Inputs are the fragment table, the number of elements in the fragment table,
and the number of words that make up nationality.

The number of fragments (words) in a ship name dictate the possible sizes of ship type.  If nationality takes one fragment,
and ship type takes four fragments, then the minimum number of fragments in a composite ship name is:
	5 = 1 (nationality) + 3 (ship type) + 1 (ship name) (same as 4 fragments (words) after nationality)

This function starts at the longest possible series of fragments that might be ship type.  This order is important becuase
some ship types might begin with similar fragments: 'ship' and 'ship of the line'.  Starting with the least possible
series of fragments (1) would find 'ship' and make 'of the line' part of the italicized name.

Returns 0 if there is no recognizable ship type.

]]

local function sizeof_ship_type (frag, frag_len, nat_len)
	local ship_type;
	
	if 5 <= (frag_len - nat_len) then											-- must have at least five fragments after nationality for four-word ship type
		ship_type = table.concat (frag, ' ', nat_len+1, nat_len+4);				-- four-word ship type
		if ship_type_list [ship_type] then
			return 4;
		end
	end
	if 4 <= (frag_len - nat_len) then											-- must have at least four fragments after nationality for three-word ship type
		ship_type = table.concat (frag, ' ', nat_len+1, nat_len+3);				-- three-word ship type
		if ship_type_list [ship_type] then
			return 3;
		end
	end
	if 3 <= (frag_len - nat_len) then											-- must have at least three fragments after nationality for two-word ship type
		ship_type = table.concat (frag, ' ', nat_len+1, nat_len+2);				-- two-word ship type
		if ship_type_list [ship_type] then
			return 2;
		end
	end	
	if 2 <= (frag_len - nat_len) then											-- must have at least two fragments after nationality for one-word ship type
		if ship_type_list [frag[nat_len+1]] then								-- one-word ship type
			return 1;
		end
	end
	return 0;																	-- no recognizable ship type
end

--[[--------------------------< S I Z E O F _ N A T I O N A L I T Y >------------------------------------------

This function the size (in words) of the nationality from the fragments table.  Nationality may be one or two
words that occupy the first one or two positions in the table.

Returns the number of words that identify the nationality:
	1 for French or German, etc.
	2 for United States;
	0 when table doesn't have a recognizable nationality

]]

local function sizeof_nationality (frag, frag_len)
	local nat = '';

	if not nationality_list [frag[1]] then										-- if not a one-word nationality
		if 2 <= frag_len - 2 then												-- must have at least two fragments after nationality for minimal ship type and name
			nat = table.concat (frag, ' ', 1, 2);
			if nationality_list [nat] then										-- is it a two-word nationality?
				return 2;														-- yes
			else
				return 0;														-- no
			end
		end
		return 0;																-- not one-word and not enough fragments for two-word
	end
	return 1;																	-- one-word nationality
end


--[[-------------------------< S H I P _ N A M E _ F O R M A T >-----------------------------------------------

This function applies correct styling to ship and ship-class names.  These names are, for example, ship-article titles
used by templates {{navsource}}, {{Infobox ship begin}}, where the article title is to be rendered with proper
styling.

This function requires one argument:
	|name= (required): a name is required; if missing or empty, this function returns an error message (may or may not be visible depending on where it is used)
		used in {{infobox ship begin}} to provide a value for {{DISPLAYTITLE:}} and to provide a value for |infobox caption=
			{{#invoke:WPSHIPS_utilities|ship_name_format|name={{PAGENAME}}}}
Optional arguments to support {{infobox ship begin}}:
	|dab=none – displays ship name without parenthetical disambiguator; use when |infobox caption=nodab
	|sclass=2 – for ship classes only; displays class name without italics (parameter name is loosely similar to {{slcass2}} which does the same thing); use when |infobox caption=class
	|adj=off – for ship classes only; displays class name as a noun (no hyphen, no ship type); use when |infobox caption=class

Arguments are passed in a table.

to call this function locally:
	do_ship_name_format ({['name=name'], ['dab']=dab, ['sclass']=sclass, ['adj']=adj, ['showerrs']=showerrs}) or
	args = {['name=name'], ['dab']=dab, ['sclass']=sclass, ['adj']=adj, ['showerrs']=showerrs};
	do_ship_name_format (args)

The function returns the formatted name or, if unable to format the name, the original name and an unformatted error message.

]]

local function do_ship_name_format (args)
	local name_sans_dab;														-- the ship or class name without a trailing parenthetical dab
	local dab;																	-- the dab stripped from the name
	local fragments = {};														-- a table of words that make up name_sans_dab
	local ship_type;															-- a word or phrase that describes a ship
	local type_len;																-- the number of words that describe a ship
	local nat_len;																-- the number of words used to specify a ship's nationality
	local name = '';															-- the reassembles and formatted ship name
	local error_msg = '';														-- a repository for error messages if any

--	args.name = mw.text.decode (args.name);										-- replace html entities in title with their characters; doesn't work for & and & in prefix
	args.name = args.name:gsub ("&#39;", "\'");									-- replace html appostrophe with the character
--	args.name = args.name:gsub ("&", "&");
--	args.name = args.name:gsub ("&", "&");
--	args.name = args.name:gsub ("&", "&");


	if args.name:match ('.+%-class%s+%a+') then									-- if a ship-class
		fragments = mw.text.split (args.name, '-class' );						-- split at -class
		if '2' == args.sclass then												-- for DISPLAYTITLE and infobox caption when class not named for a member of the class
			if 'off' == args.adj then
				return fragments[1] .. ' class';								-- for infobox caption do noun form <name> class (no hyphen, no ship type)
			end
			return args.name;													-- nothing to do so return original unformatted name
		end
		if 'off' == args.adj then
			return "''" .. fragments[1] .. "'' class";							-- for infobox caption do noun form <name> class (no hyphen, no ship type)
		end
		return "''" .. fragments[1] .. "''-class" .. fragments[2];				-- and return formatted adjectival name
	end
																				-- not a ship class so try to format a ship name
	name_sans_dab, dab = args.name:match('^(.+)%s+(%b())%s*$');					-- split name into name_sans_dab and dab
	if is_set (dab) then
		dab = ' ' .. dab;														-- insert a space for later reassembly
	else
		name_sans_dab = args.name;												-- because without a dab, the string.match returns nil
		dab = '';																-- empty string for concatenation
	end
	
	fragments = mw.text.split (name_sans_dab, '%s' );							-- split into a table of separate words

	nat_len = sizeof_nationality (fragments, #fragments);						-- get the number of words in the ship's nationality
	if 0 < nat_len then															-- if not zero we have a valid nationality
		type_len = sizeof_ship_type (fragments, #fragments, nat_len);			-- get the number of words in the ship type
		if 0 < type_len then													-- if not zero, ship type is valid; nationality and type not italics, the rest is name
			name = "''" .. table.concat (fragments, ' ', nat_len + type_len + 1) .. "''";	-- format name
			if 'none' == args.dab then											-- for |infobox caption=nodab
				return name;													-- return the formatted name without the nationality or ship type or dab
			end
			name = table.concat (fragments, ' ', 1, nat_len + type_len) .. " " .. name;	-- assemble everything but dab
		else
			error_msg = ' unrecognized ship type;';								-- valid nationality, invalid ship type
		end
	elseif ship_prefix_list[fragments[1]] then									-- if the first fragment is a ship prefix
		name = table.remove (fragments, 1);										-- fetch it from the table
		name = name .. " ''" .. table.concat (fragments, ' ') .. "''";			-- assemble formatted name
	else
		error_msg = ' no nationality or prefix;';								-- invalid nationality and first word in ship name not a valid prefix
	end

	if is_set (name) then														-- name will be set if we were able to format it
		if 'none' == args.dab then												-- for |infobox caption=nodab
			return name;														-- return the formatted name without the dab
		end
		return name .. dab;														-- return the formatted name with the dab
	end
	
	if is_set (dab) then
		if dab:match ('%(%u+[%- ]?%d+%)') or									-- one or more uppercase letters, optional space or hyphen, one or more digits
			dab:match ('%(%d+[%- ]?%u+%)') or									-- one or more digits, optional space or hyphen, one or more uppercase letters
			dab:match ('%(%u[%u%-]*%-%d+%)') or									-- one or more uppercase letters with hyphens, a hyphen, one or more digits (e.g., T-AO-157)
			dab:match ('%([12]%d%d%d%)') then									-- four digits representing year in the range 1000–2999
				name = "''" .. table.concat (fragments, ' ') .. "''";			-- format the name
				if 'none' == args.dab then										-- for |infobox caption=nodab
					return name;												-- return the formatted name without the dab
				end
			return name .. dab;													-- return the formatted name with the dab
		end
																				-- last chance, is there a ship type in the dab?
		for key, _ in pairs (ship_type_list) do									-- spin through the ship type list and see if there is a ship type (key) in the dab
	    	if dab:find ('%f[%a]' .. key .. '%f[^%a]') then						-- avoid matches that are not whole word
	    		name = "''" .. table.concat (fragments, ' ') .. "''";			-- format the name
				if 'none' == args.dab then										-- for |infobox caption=nodab
					return name;												-- return the formatted name without the dab
				end
				return name .. dab;												-- return the formatted name with the dab
	    	end
		end
		error_msg = error_msg .. ' no ship type in dab;';
		
		if 'none' == args.dab then												-- for |infobox caption=nodab
			return table.concat (fragments, ' '), error_msg;					-- return the unformatted name without the dab, and an error message
		end
	end

	return args.name, error_msg;												-- return original un-formatted name with unformatted error message if any
end


--[[-------------------------< S H I P _ N A M E _ F O R M A T >-----------------------------------------------

This function is the external interface to do_ship_name_format().

The function requires one parameter:
	|name= (required): a name is required; if missing or empty, this function returns an error message (may or may not be visible depending on where it is used)
		used in {{infobox ship begin}} to provide a value for {{DISPLAYTITLE:}} and to provide a value for |infobox caption=
			{{#invoke:WPSHIPS_utilities|ship_name_format|name={{PAGENAME}}}}
Optional parameters to support {{infobox ship begin}}:
	|dab=none – displays ship name without parenthetical disambiguator; use when |infobox caption=nodab
	|sclass=2 – for ship classes only; displays class name without italics (parameter name is loosely similar to {{slcass2}} which does the same thing); use when |infobox caption=class
	|adj=off – for ship classes only; displays class name as a noun (no hyphen, no ship type); use when |infobox caption=class
Other optional parameters:
	|showerrs=yes – marginally useful; can display error messages if the module invocation is not buried in a template
	
Values from the above parameters are placed in a table and that table passed as an argument in the call to do_ship_name_format().

do_ship_name_format() returns two strings: a name and an error message.  If do_ship_name_format() could format the name, it returns the formatted name and 
an empty string for the error message.  If it could not format the name, do_ship_name_format() returns the original name and an error message.

Formatting of the error message, in response to |showerrs=yes is the responsibility of the calling function.

]]

function wpsu.ship_name_format(frame)
	local name = '';															-- destination of the formatted ship name
	local error_msg = '';														-- destination of any error message

	if not is_set (frame.args.name) then										-- if a ship name not provided
		if 'yes' == frame.args.showerrs then									-- and we're supposed to show errors
			error_msg = '<span style="font-size:100%; font-weight:normal" class="error">Empty name</span>';	-- return an empty string error message if there is no name
		end
	else
		name, error_msg = do_ship_name_format (frame.args);						-- get formatted name and error message
		if is_set (error_msg) and 'yes' == frame.args.showerrs then				-- if appropriate, show error message
			error_msg = '<span style="font-size:100%; font-weight:normal" class="error">' .. error_msg .. '</span>';
		else
			error_msg = '';														-- for concatenation
		end
	end

	return name .. error_msg;													-- return name and error message
end


--[[--------------------------< H N S A >----------------------------------------------------------------------

Similar to {{navsource}}, this code supports {{hnsa}} by attempting to construct a link to a ship article at the
the Historic Nava Ships Association website.

The template has the form:
	{{hnsa|<page>|<name>}}
where:
	<page> is the name of the page at http://hnsa.org/hnsa-ships/<page>
	<name> (optional) is the name of the ship; if left blank, the template uses the current page title; if a ship name, it is formatted
from which this code produces:
	[http://hnsa.org/hnsa-ships/<page> <name>] at Historic Naval Ships Association

]]

function wpsu.hnsa (frame)
	local pframe = frame:getParent()											-- get arguments from calling template frame
	local ship_name = '';
	local error_msg = '';
	local article_title = mw.title.getCurrentTitle().text;						-- fetch the article title
	
	if not is_set (pframe.args[1]) then
		return '<span style="font-size:100%; font-weight:normal" class="error">missing hsna page</span>';
	end
	
	local fmt_params = {['name']='', ['showerrs']=nil};

	if is_set (pframe.args.showerrs) then										-- if showerrs set in template, override showerrs in #invoke:
		fmt_params.showerrs = pframe.args.showerrs;								-- template value
	else
		fmt_params.showerrs = frame.args.showerrs;								-- invoke value
	end

	if is_set (pframe.args[2]) then
		fmt_params.name = pframe.args[2];
	else
		fmt_params.name = article_title;										-- use article title
	end

	ship_name, error_msg = do_ship_name_format (fmt_params);
	
	if is_set (error_msg) and is_set (pframe.args[2]) then						-- if unable to format the name
		local escaped_name = pframe.args[2]:gsub("([%(%)%.%-])", "%%%1");		-- escape some of the Lua magic characters
		if pframe.args[2] == article_title or									-- is name same as article title?
			nil ~= article_title:find ('%f[%a]' .. escaped_name .. '%f[%s]') or	-- is name a word or words substring of article title?
			nil ~= article_title:find ('%f[%a]' .. escaped_name .. '$') then	-- is name a word or words substring that ends article title?
				ship_name = "''" .. pframe.args[2] .. "''";						-- non-standard 'name'; perhaps just the name without prefix and dab;
				error_msg = '';													-- unset because we think we have a name
		end
	end
	if is_set (error_msg) and 'yes' == fmt_params.showerrs then
		error_msg = '<span style="font-size:100%; font-weight:normal" class="error">' .. error_msg .. '</span>';
	else
		error_msg = '';															-- unset so it doesn't diplay
	end
	
	local output = {
		'[http://www.hnsa.org/hnsa-ships/',
		pframe.args[1],
		'/ ',
		ship_name,
		'] at Historic Naval Ships Association',
		error_msg,
		}

	return table.concat (output);
end


--[[--------------------------< N A V S O U R C E >------------------------------------------------------------

This version of the template {{navsource}} was added as a test vehicle for do_ship_name_format().

]]

function wpsu.navsource (frame)
	local pframe = frame:getParent()											-- get arguments from calling template frame
	local ship_name = '';
	local error_msg = '';
	local article_title = mw.title.getCurrentTitle().text;						-- fetch the article title
	
	if not is_set (pframe.args[1]) then
		return '<span style="font-size:100%; font-weight:normal" class="error">missing navsource URLcode</span>';
	end
	
	local fmt_params = {['name']='', ['showerrs']=nil};

	if is_set (pframe.args.showerrs) then										-- if showerrs set in template, override showerrs in #invoke:
		fmt_params.showerrs = pframe.args.showerrs;								-- template value
	else
		fmt_params.showerrs = frame.args.showerrs;								-- invoke value
	end

	if is_set (pframe.args[2]) then
		fmt_params.name = pframe.args[2];
	else
		fmt_params.name = article_title;										-- use article title
	end

	ship_name, error_msg = do_ship_name_format (fmt_params);
	
	if is_set (error_msg) and is_set (pframe.args[2]) then						-- if unable to format the name
		local escaped_name = pframe.args[2]:gsub("([%(%)%.%-])", "%%%1");		-- escape some of the Lua magic characters
		if pframe.args[2] == article_title or									-- is name same as article title?
			nil ~= article_title:find ('%f[%a]' .. escaped_name .. '%f[%s]') or	-- is name a word or words substring of article title?
			nil ~= article_title:find ('%f[%a]' .. escaped_name .. '$') then	-- is name a word or words substring that ends article title?
				ship_name = "''" .. pframe.args[2] .. "''";						-- non-standard 'name'; perhaps just the name without prefix and dab;
				error_msg = '';													-- unset because we think we have a name
		end
	end
	if is_set (error_msg) and 'yes' == fmt_params.showerrs then
		error_msg = '<span style="font-size:100%; font-weight:normal" class="error">' .. error_msg .. '</span>';
	else
		error_msg = '';															-- unset so it doesn't diplay
	end
	
	local output = {
		'[http://www.navsource.org/archives/',
		pframe.args[1],
		'.htm Photo gallery] of ',
		ship_name,
		' at NavSource Naval History',
		error_msg,
		}

	return table.concat (output);
end


--[[--------------------------< _ S H I P >--------------------------------------------------------------------

This is a possible replacement for the template {{ship}}.  It has better error detection and handling.

]]

local function _ship (prefix, name, dab, control, unlinked_prefix)
	local error_msg = '';
	
	if not is_set (control) then
		control = '';
	end
																				-- dispose of error conditions straight away
	if not is_set (name) then													-- this is the only required parameter
		error_msg = ' missing name';
	elseif not is_set (dab) and ('1' == control or '3' == control or '5' == control) then	-- dab required when control value set to expect it
		error_msg = ' missing disambiguator';
	elseif not is_set (prefix) and ('5' == control or '6' == control) then		-- prefix required when control value set to expect it
		error_msg = ' missing prefix';
	elseif '4' == control then													-- displaying only the prefix
		error_msg = 'invalid control parameter: ' .. control;
	elseif is_set (control) then
		if 1 > tonumber (control) or 6 < tonumber (control) then				-- control must be a number between 1 through 6
			error_msg = 'invalid control parameter: ' .. control;
		end
	elseif not is_set (prefix) and unlinked_prefix then							-- prefix required when |up=yes
		error_msg = ' missing prefix';
	end
	
	if is_set (error_msg) then
		return '<span style="font-size:100%" class="error">' .. error_msg .. '</span>';	-- return an error message; don't bother with making a link
	end
	
	local link_name;
	local link = '[[';
	if is_set (prefix) then
		link = link .. prefix .. ' ' .. name;									-- begin assembling the article name portion of the wikilink
	else
		link = link .. name;
	end

	if is_set (dab) then
		link = link .. ' (' .. dab .. ')';										-- wrap dab in parentheses
	end
	
	name = "''" .. name .. "''";												-- name is always italicized so do it now

	if '1' == control then
		link_name = dab;														-- special case when displaying only the dab, don't wrap in parentheses
	end
	
	if is_set (dab) then
		dab = ' (' .. dab .. ')';											-- for all other cases that display dab
	end
		
	if not is_set (control) then												-- when control not set: prefix, name, and dab
		if unlinked_prefix then													-- 'unlinked prefix'?
			link = prefix .. ' ' .. link;									-- yes, modify link so that prefix is not linked in final render
			link_name = name .. dab;
		elseif is_set (prefix) then
			link_name = prefix .. ' ' .. name .. dab;
		else
			link_name = name .. dab;
		end
	else																		-- when control is not 1 or none
		if '2' == control then													-- name only
			link_name = name;
		elseif '3' == control then												-- name and dab
			link_name = name .. dab;
		elseif '5' == control then												-- prefix and dab
			if unlinked_prefix then												-- 'unlinked prefix'?
				link = prefix .. ' ' .. link;								-- yes, modify link so that prefix is not linked in final render
				link_name = dab;
			else
				link_name = prefix .. dab;
			end
		elseif '6' == control then												-- prefix and name
			if unlinked_prefix then												-- 'unlinked prefix'?
				link = prefix .. ' ' .. link;								-- yes, modify link so that prefix is not linked in final render
				link_name = name;
			else
				link_name = prefix .. ' ' .. name;
			end
		end
	end

	return link .. '|' .. link_name .. ']]';
end

--[[--------------------------< W P S U . S H I P >------------------------------------------------------------

This is a possible replacement for the template {{ship}}.  It has better error detection and handling.

This function is the externally accessible entry point for template {{ship}}, {{HMS}}, {{USS}}, etc

]]

function wpsu.ship (frame)														-- this version not supported from the template yet
	local prefix = mw.text.trim (frame.args[1] or '');							-- fetch positional parameters into named variables for readability
	local name =  mw.text.trim (frame.args[2] or '');							-- stripped of leading and trailing whitespace 
	local dab =  mw.text.trim (frame.args[3] or '');							-- and and set to empty string (is that needed?)
	local control = frame.args[4];
	local unlinked_prefix = 'yes' == frame.args.up;
	
	return _ship (prefix, name, dab, control, unlinked_prefix);
end


--[[--------------------------< L I S T _ E R R O R >----------------------------------------------------------

Assembles an error message, the original parameter value and, if appropriate a category.  The error message precedes
the existing value of the parameter.  If the first non-whitespace character in the parameter is a '*', set prefix to
a '*' and sep to '\n'.  For line-break lists, set prefix to empty string and sep to '<br />'.

Category is appended to the end of the returned value only for pages in article space.

Inputs:
	prefix – a string of characters that precede the error message span; typically '' and '*'
	message – the error message to be displayed; goes inside the span
	sep – a string of characters that separates the span from the parameter value; typically '\n' and '<br />'
	param_val – the unmodified parameter value
	showerrs – a boolean, true to display the error message text

]]

local function list_error (prefix, message, sep, param_val, showerrs)
	local err_msg = '%s<span style="font-size:100%%" class="error">列表错误：%s（[[:Category:WPSHIPS:Infobox_list_errors|帮助]]）</span>%s%s%s';
	local category = '';

	if 0 == mw.title.getCurrentTitle().namespace then							-- only categorize pages in article space
		category = '[[Category:WPSHIPS:Infobox_list_errors|Category:WPSHIPS:Infobox list errors]]';
	end
	if true == showerrs then
		return string.format (err_msg, prefix, message, sep, param_val, category);			-- put it all together
	else
		return param_val .. category;
	end
end


--[[--------------------------< I N F O B O X _ L I S T S >----------------------------------------------------

Mediawiki:Common.css imposes limitations on plain, unbulleted lists.  The template {{plainlist}} does not render this correctly:
{{plainlist|
*Item 1
*Item 2
**Item 2a
***Item 2a1
**Item 2b
*Item 3}}
The above renders without proper indents for items marked ** and ***.

If the list is not wrapped in {{plainlist}} then the above list is rendered with bullets which is contrary to the Infobox ship usage guide.

This code translates a bulleted list into an html unordered list:

<ul style="list-style:none none; margin:0;"> 
 <li>Name 1</li>
 <li>Name 2</li>
 <ul style="list-style:none none">
  <li>Subname 2a</li>
  <ul style="list-style:none none">
   <li>Subname 2a1</li>
  </ul>
  <li>Subname 2b</li>
 </ul>
 <li>Name 3</li>
</ul>

There are rules:
	1. The parameter value must begin with a splat but may have leading and trailing whitespace.
	2. Each list item after the first must begin on a new line just as is required by normal bulleted lists.
	3. When adding a sublevel, the number of splats may increase by one and never more. This is illegal:
		*item
		***item
When any of these rules are violated, wpsu.unbulleted_list() returns the original text and adds the article
to Category:WPSHIPS:Infobox list errors.  Error messaging in this function is somewhat sketchy so they are
disabled.  After initial adoption, better error messaging could/should be implemented.

This function receives the content of one parameter:
	{{#invoke:WPSHIPS utilities|unbulleted_list|{{{param|}}}}}

]]

function wpsu.unbulleted_list (frame)
	local showerrs = true;														-- set to false to hide error messages
	local List_item_otag = '<li style="padding-left: .4em; text-indent: -.4em;">';	-- hanging indent markup; everything moves right with padding-left; first line moved left by neg indent
	
	if nil == frame.args[1]:match ('^%s*%*') then								-- parameter value must begin with a splat (ignoring leading white space)
		if frame.args[1]:match ('<[%s/]*[Bb][Rr][%s/]*>') then					-- if the parameter value has a list using variants of <br /> tag
			return list_error ('', '<br /> list', '<br />', frame.args[1], showerrs);		-- return an error message with maintenance category
		elseif frame.args[1]:match ('.+\n%*') then								-- if the parameter value has text followed by an unordered list
			return list_error ('', 'mixed text and list', '<br />', frame.args[1], showerrs);	-- return an error message with maintenance category
		end
		return frame.args[1];													-- return the parameter as is
	end
	
	local item_table = mw.text.split (mw.text.trim (frame.args[1]), '\n');		-- trim white space from end then make a table of bulleted items by splitting on newlines
	if 1 == #item_table then													-- if only one bulleted item, no need for a list
		return (item_table[1]:gsub ('^%*%s*', ''));								-- trim off the splat and any following white space and done
	end
	
	if item_table[1]:match ('^%*%*+') then										-- if first list item uses more than one splat, that's an error
		return list_error ('*', 'too many * at start of list', '\n', frame.args[1], showerrs);		-- return an error message with maintenance category
	end
	
	local html_table = {};														-- table to hold the html output
	local level = 1;															-- used to indicate when a new <ul> is required
	local splats = 0;															-- number of splats that start each item in the list
	local item = '';															-- the item text
	
	table.insert (html_table, '<ul style="list-style:none none; margin:0;">')	-- this for first <ul> tag; sets no bullets and no indent
	
	for _,v in ipairs (item_table) do
		splats, item = v:match ('(%*+)%s*(.*)');								-- split the item into splats and item text
		if nil == splats then													-- nil if there is an extra line between items
			return list_error ('*', 'list item missing markup', '\n', frame.args[1], showerrs);	-- return an error message with maintenance category
		elseif '' == item then
			return list_error ('*', 'empty list item', '\n', frame.args[1], showerrs);	-- return an error message with maintenance category
		elseif item:match ('^[;:]') then										-- if the list item is mixed unordered list / description list markup (*:)
			return list_error ('*', 'mixed list type', '\n', frame.args[1], showerrs);	-- return an error message with maintenance category
		end

		splats = splats:len();													-- change string of splats into a number indicating how many splats there are
		
		if splats == level then													-- if at the same level as previous item
			table.insert (html_table, List_item_otag .. item .. '</li>');
		elseif splats == level + 1 then											-- number of splats can only increase by one
			level = splats;														-- record the new level
			table.insert (html_table, '<ul style="list-style:none none">');		-- add a new sublist
			table.insert (html_table, List_item_otag .. item .. '</li>');		-- and the item
		elseif splats < level then												-- from three splats to one splat for example
			while splats < level do
				table.insert (html_table, '</ul>');								-- close each sub <ul> until level and splats match
				level = level - 1;
			end
			table.insert (html_table, List_item_otag .. item .. '</li>');		-- add the item
		else																	-- jumping more than one level up – one splat to three splats for example – is an error
			return list_error ('*', 'too many asterisks', '\n', frame.args[1], showerrs);	-- return an error message with maintenance category
		end
	end

	while 0 < level do
		table.insert (html_table, '</ul>');										-- close each <ul> until level counted down to zero
		level = level - 1;
	end

	return table.concat (html_table, '\n');										-- return the list as a string
end


--[=[-------------------------< I N F O B O X _ S H I P _ F L A G >--------------------------------------------

Output of {{shipboxflag|USA}}:
	[[File:Flag_of_the_United_States.svg|100x35px]]
	
Image syntax:
	[[File:Name|Type]]

This function standardizes the size of flag images in the infobox ship career header by simply overwriting the Size
parameter value in the Image wikilink with |100x28px.  This size leave a 1px gap between the top and bottom of the flag image and
the header edge.  A similar left-side gap of 2px is supplied by {{infobox ship career}}.

]=]

function wpsu.infobox_ship_flag (frame)
	if not is_set (frame.args[1]) then											-- if |Ship flag= not set
		return '';																-- return empty string
	end
	
	if frame.args[1]:match ('|[%s%dx]+px%s*') then								-- is there a size positional parameter?
		frame.args[1] = frame.args[1]:gsub('|[%s%dx]+px%s*', '%|100x28px');		-- overwrite it with |100x28px
	else
		return '<span style="font-size:100%" class="error">malformed flag image</span>'
	end
	return frame.args[1];														-- return the modified image
end
return wpsu;