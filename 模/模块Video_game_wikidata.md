local Date = require('Module:Date')._Date
local yesno = require('Module:Yesno')

local p = {}

-- Local variables.
local reviewer = nil;
local df = "ymd";
local entity = nil;
local genRefs = true;
local showSystem = true;
local showUpdateLink = true;
local system = nil;
local systemId = nil;
local systemFormat = "colon";
local updateLinkStyle = nil;
local entities = {};

-- Translation table for converting numeric-IDs to shorthand aliases.
local systemAliases = {
	[10677] = 'PS1',
	[1323662] = 'PS1', -- Placeholder, this is actually the series but could be mistakenly used for PS1.
	[10680] = 'PS2',
	[10683] = 'PS3',
	[5014725] = 'PS4',
	[16338] = 'PC',
	[8079] = 'Wii',
	[56942] = 'WiiU',
	[132020] = 'XBOX',
	[48263] = 'X360',
	[13361286] = 'XONE',
	[203597] = '3DS',
	[188808] = 'PSV',
	[170323] = 'DS', -- Sometimes has been NDS
	[170325] = 'PSP',
	[48493] = 'IOS', -- iOS, iPhone, iPad
	[94] = 'AND', -- Android
	[186437] = 'GB',
	[188642] = 'GBA',
	[203992] = 'GBC',
	[184198] = 'DC',
	[200912] = 'SAT',
	[172742] = 'NES',
	[183259] = 'SNES',
	[184839] = 'N64',
	[182172] = 'GC', -- Sometimes has been NGC
}

-- Translation table for converting system aliases to QIDs
local systemIDs = {
	['PS1'] = 10677,
	['PS2'] = 10680,
	['PS3'] = 10683,
	['PS4'] = 5014725,
	['PC'] = 16338,
	['WII'] = 8079,
	['WIIU'] = 56942,
	['XBOX'] = 132020,
	['X360'] = 48263,
	['XONE'] = 13361286,
	['3DS'] = 203597,
	['PSV'] = 188808,
	['DS'] = 170323,
	['NDS'] = 170323,
	['PSP'] = 170325,
	['IOS'] = 48493,
	['AND'] = 94,
	['GB'] = 186437,
	['GBA'] = 188642,
	['GBC'] = 203992,
	['DC'] = 184198,
	['SAT'] = 200912,
	['NES'] = 172742,
	['SNES'] = 183259,
	['N64'] = 184839,
	['GC'] = 182172,
	['NGC'] = 182172,
}

-- List of accepted aggregator arguments and their related QID.
local aggregatorAliases = {
    [150248] = 'MC',
    [40160] = 'GR'
}   

-- List of accepted aggregator arguments and their related QID.
local aggregatorIDs = {
    ['MC'] = 150248,
    ['GR'] = 40160
}   

-- List of accepted reviewer arguments and their related QID.
local reviewerAliases = {
	[591573] = 'FAM',
	[207708] = 'IGN'
}   

-- List of accepted reviewer arguments and their related QID.
local reviewerIDs = {
	['FAM'] = 591573,
	['IGN'] = 207708
} 

local function sortByPlatform(a,b) 
	local platformA = nil;
	local platformB = nil;
	if(a['qualifiers']['P400'] ~= nil and b['qualifiers']['P400'][1] ~= nil) then
		platformA = p.getSystemAlias(a['qualifiers']['P400'][1]['datavalue']['value']['numeric-id']);
		if(platformA == nil) then
			platformA = mw.wikibase.label('Q'..a['qualifiers']['P400'][1]['datavalue']['value']['numeric-id']);
		end;
	end;
	if(b['qualifiers']['P400'] ~= nil and b['qualifiers']['P400'][1] ~= nil) then
		platformB = p.getSystemAlias(b['qualifiers']['P400'][1]['datavalue']['value']['numeric-id']);
		if(platformB == nil) then
			platformB = mw.wikibase.label('Q'..b['qualifiers']['P400'][1]['datavalue']['value']['numeric-id']);
		end;
	end;		
		
	return platformA < platformB
end;

local function buildCite(reference) 
	local referenceUrl = nil;
	local cite = nil;
	
	if(reference['snaks']['P854'] ~= nil and reference['snaks']['P854'][1] ~= nil) then
		referenceUrl = reference['snaks']['P854'][1]['datavalue']['value'];	
	end;

	if(referenceUrl ~= nil and referenceUrl ~= "") then
		cite = "{{cite web|url="..referenceUrl;
			
		local pubdate = nil;
		local accessdate = nil;
		local publisher = nil;
		local work = nil;
		local title = nil;
		local archiveUrl = nil;
		local archiveDate = nil;
		local authors = {};

		if(reference['snaks']['P577'] ~= nil and reference['snaks']['P577'][1] ~= nil) then
			pubdate = reference['snaks']['P577'][1]['datavalue']['value']['time'];
		end;
		if(reference['snaks']['P813'] ~= nil and reference['snaks']['P813'][1] ~= nil) then
			accessdate = reference['snaks']['P813'][1]['datavalue']['value']['time'];
		end;
		if(reference['snaks']['P123'] ~= nil and reference['snaks']['P123'][1] ~= nil) then
			publisher = mw.wikibase.label('Q'..reference['snaks']['P123'][1]['datavalue']['value']['numeric-id']);
		end;
		if(reference['snaks']['P1433'] ~= nil and reference['snaks']['P1433'][1] ~= nil) then
			work = mw.wikibase.label('Q'..reference['snaks']['P1433'][1]['datavalue']['value']['numeric-id']);
		end;			
		if(reference['snaks']['P1476'] ~= nil and reference['snaks']['P1476'][1] ~= nil) then
			title = reference['snaks']['P1476'][1]['datavalue']['value']['text'];
		end;
		if(reference['snaks']['P1065'] ~= nil and reference['snaks']['P1065'][1] ~= nil) then
			archiveUrl = reference['snaks']['P1065'][1]['datavalue']['value'];
		end;
		if(reference['snaks']['P2960'] ~= nil and reference['snaks']['P2960'][1] ~= nil) then
			archiveDate = reference['snaks']['P2960'][1]['datavalue']['value']['time'];
		end;	
		if(reference['snaks']['P50'] ~= nil and #reference['snaks']['P50'] > 0) then
			for i,authorDat in pairs(reference['snaks']['P50']) do
				local authorQid = 'Q'..authorDat['datavalue']['value']['numeric-id'];
				if(entities[authorQid] == nil) then
					entities[authorQid] = mw.wikibase.getEntity(authorQid);
				end;
				
				local author = {};
				author['fullname'] = mw.wikibase.label(authorQid); -- Default to label
				author['first'] = nil;
				author['last'] = nil;
				
				if(entities[authorQid]['claims']['P735'] ~= nil and entities[authorQid]['claims']['P735'][1] ~= nil) then
					author['first'] = mw.wikibase.label('Q'..entities[authorQid]['claims']['P735'][1]['mainsnak']['datavalue']['value']['numeric-id']);
				end;
				if(entities[authorQid]['claims']['P734'] ~= nil and entities[authorQid]['claims']['P734'][1] ~= nil) then
					author['last'] = mw.wikibase.label('Q'..entities[authorQid]['claims']['P734'][1]['mainsnak']['datavalue']['value']['numeric-id']);
				end;
				
				table.insert(authors, author);
			end;
		end;			
		
		if(title ~= nil and title ~= "") then
			cite = cite .. "|script-title=en:"..title;
		end;
		if(publisher ~= nil and publisher ~= "") then
			cite = cite .. "|publisher="..publisher;
		end;
		if(work ~= nil and work ~= "") then
			cite = cite .. "|work="..work;
		end;		
		if(pubdate ~= nil and pubdate ~= "") then
			local pubdateText = Date(pubdate):text(df);

			cite = cite .. "|date="..pubdateText;
		end;		
		if(accessdate ~= nil and accessdate ~= "") then
			local accessdateText = Date(accessdate):text(df);

			cite = cite .. "|accessdate="..accessdateText;
		end;
		if(archiveUrl ~= nil and archiveUrl ~= "" and archiveDate ~= nil and archiveDate ~= "") then
		    local archivedateText = Date(archiveDate):text(df);
			cite = cite .. "|archiveurl="..archiveUrl;
			cite = cite .. "|archivedate="..archivedateText;
		end;		
		if(#authors > 0) then
			for i,author in pairs(authors) do
				if(author['first'] ~= nil and author['last'] ~= nil and author['first'] ~= "" and author['last'] ~= "") then
					if(#authors == 1) then
						cite = cite .."|last="..author['last'].."|first="..author['first'];
					else
						cite = cite .."|last"..i.."="..author['last'].."|first"..i.."="..author['first'];
					end;
				else
					if(#authors == 1) then
						cite = cite .."|author="..author['fullname'];
					else
						cite = cite .."|author"..i.."="..author['fullname'];
					end;					
				end;
			end;			
		end;
		
		
		cite = cite..'}}';	
	end;
	
	return cite;
end;

local function printReviewRow(frame, reviewscore)
	local score = nil;

	if(reviewscore['mainsnak']['datavalue'] ~= nil and reviewscore['mainsnak']['datavalue']['value'] ~= nil) then
		score = reviewscore['mainsnak']['datavalue']['value'];
	else
		return "";
	end;
	
	local ret = ""
	local system = nil;
	local reference = nil;	

	if(reviewscore['qualifiers']['P400'] ~= nil and reviewscore['qualifiers']['P400'][1] ~= nil) then
		system = p.getSystemAlias(reviewscore['qualifiers']['P400'][1]['datavalue']['value']['numeric-id']);
	end	
	if(system ~= nil and system ~= "" and showSystem) then
		if(systemFormat == "para") then
			ret = ret.."("..system..") ";
		else
			ret = ret..system.."：";
		end;
	end;

	ret = ret..score;

	if(reviewscore['references'] ~= nil and reviewscore['references'][1] ~= nil and genRefs) then
		local cite = buildCite(reviewscore['references'][1], df);
		
		if(cite ~= nil) then
			local scoreBy = p.getAggregatorAlias(reviewscore['qualifiers']['P447'][1]['datavalue']['value']['numeric-id']);
			if(scoreBy == nil) then
				scoreBy = p.getReviewerAlias(reviewscore['qualifiers']['P447'][1]['datavalue']['value']['numeric-id']);
			end;

			local name = entity:getLabel()..'-'..scoreBy;
			if(system ~= nil and system ~= "") then
				name = name..system;
			end;

			cite = frame:extensionTag{ name = "ref", args = {name=name}, content=cite };
			ret = ret..cite;
		end;
	end;

	return ret.."<br />";
end

function p.getSystemAlias(numericId)
	return systemAliases[numericId];
end

function p.getSystemID(system)
	return systemIDs[system];
end

function p.getAggregatorAlias(numericId)
	return aggregatorAliases[numericId];
end

function p.getAggregatorID(system)
	return aggregatorIDs[system];
end

function p.getReviewerAlias(numericId)
	return reviewerAliases[numericId];
end

function p.getReviewerID(system)
	return reviewerIDs[system];
end

function p.setReviewer(iReviewer)
	-- No reviewer, stop. Must have reviewer at least.
	if(iReviewer == nil or iReviewer == "") then
		return "Missing reviewer";
	end;
	
	-- See if supplied reviewer is in the aggregator table.
	iReviewer = string.upper(iReviewer)
	reviewer = p.getAggregatorID(iReviewer);
	if(reviewer == nil or reviewer == "") then
		-- No? Maybe in the reviewer table.
		reviewer = p.getReviewerID(iReviewer);
		if(reviewer == nil or reviewer == "") then
			return "Invalid reviewer";
		end;
	end;	

	return nil;
end;

function p.setDateFormat(iDf)
	-- Check for a date format parameter. Default to mdy if missing.
	if(iDf ~= nil and iDf ~= "") then
		df = string.lower(iDf);
	end;
end;

function p.setSystemFormat(iSf)
	if(iSf ~= nil and iSf ~= "") then
		systemFormat = string.lower(iSf);
	end;
end;

function p.setUpdateLinkStyle(iStyle)
	if(iStyle ~= nil and iStyle ~= "") then
		updateLinkStyle = string.lower(iStyle);
	end;
end;

function p.setGame(iGame)
	-- Check for a game parameter. If missing, default to current article.
	if(iGame ~= nil and iGame ~= "") then
		if(entities[iGame] == nil) then
 			entities[iGame] = mw.wikibase.getEntity(iGame);
		end;
		
		entity = entities[iGame]
	else
		-- Need to research if we can determine the entity's ID before retrieving it.
		entity = mw.wikibase.getEntity();	
		if(entity ~= nil) then
			entities[entity['id']] = entity;
		end;
	end;
	
	if(entity == nil) then
		return "No matching wikidata entity found";
	end;
	
	return nil;
end;

function p.setSystem(iSystem)
	-- Check for system parameter, and resolve it's QID if possible.
	if(iSystem ~= nil and iSystem ~= "") then
		system = string.upper(iSystem);
		systemId = p.getSystemID(system);
	elseif(not showSystem) then
		-- If no system was specified, force showSystem on.
		showSystem = true;
	end;
end;

function p.setGenerateReferences(iGenRefs)
	-- Reference suppression.
	if(iGenRefs ~= nil and iGenRefs ~= "") then
		genRefs = yesno(iGenRefs, true);
	end;
end;

function p.setShowSystem(iShowSystem)
	-- Suppression of system aliases in front of score, i.e. (XBOX) xx/100.
	if(iShowSystem ~= nil and iShowSystem ~= "") then
		showSystem = yesno(iShowSystem, false);
	end;
	if(system == nil or system == '') then
		-- If no system was specified, force showSystem on.
		showSystem = true;
	end;
end;

function p.setShowUpdateLink(iShowUpdateLink)
	-- Suppression of update link to Wikidata at the end of the score, i.e. (XBOX) xx/100[+].
	if(iShowUpdateLink ~= nil and iShowUpdateLink ~= "") then
		showUpdateLink = yesno(iShowUpdateLink, false);
	end;
end;

function p.getUpdateLink()
	if(updateLinkStyle == "pen") then
		return "[[File:Blue_pencil.svg|frameless]]";
	elseif(updateLinkStyle == "noSub") then
		return '[[d:'..entity['id']..'#P444|[±]]]';
	end;
	
	return '<sub>[[d:'..entity['id']..'#P444|[±]]]</sub>';
end;

function p.getSitelink()
	return mw.wikibase.sitelink(entity['id']);
end;

function p.getLabel()
	return mw.wikibase.label(entity['id']);
end;

function p.getParts()
	local ret = {};	
	
	-- Loop all of "has Part" for this title
	local parts = entity['claims']['P527'];	
	if(parts) then
		for i,part in pairs(parts) do
			table.insert(ret,"Q"..part['mainsnak']['datavalue']['value']['numeric-id']);
		end;		
	end;

	return ret;	
end;

function p.getEarliestPublicationDate()
	local ret = {};
	
	local pubDates = entity['claims']['P577'];	
	if(pubDates) then
		for i,pubDate in pairs(pubDates) do
			local timestamp = pubDate['mainsnak']['datavalue']['value']['time'];
			local accessdate = Date(timestamp);	
			table.insert(ret,accessdate);
		end;		
	end;

	if(#ret < 1) then
		return nil;
	end;

	table.sort(ret);
	
	return ret[1];
end;

function p.printReviewScores(frame)
	local ret = "";	
	
	-- Loop all of "review scores" for this title
	local reviewscores = entity['claims']['P444'];	
	if(reviewscores) then
		-- Find reviews that qualify for printing and insert into array.
		local reviewsToPrint = {}
    	for i,review in pairs(reviewscores) do
			local scoreBy = nil 
			if(review['qualifiers']['P447'] ~= nil and review['qualifiers']['P447'][1] ~= nil) then
				scoreBy = review['qualifiers']['P447'][1]['datavalue']['value']['numeric-id'];
			end;
			if(scoreBy == reviewer) then
				-- If template specified a system, we need to check for the specific system and only output that one.
				if(system == nil or system == "") then
					-- No system specified, so output each one found.
					table.insert(reviewsToPrint,review);
				else
					-- Get platform if it exists.
					if(review['qualifiers']['P400'] ~= nil and review['qualifiers']['P400'][1] ~= nil) then
						-- Try to match based on QID.
						local reviewSysId = review['qualifiers']['P400'][1]['datavalue']['value']['numeric-id'];
						if(systemId == reviewSysId) then
							table.insert(reviewsToPrint,review);
						else 
							-- If that failed, try to match based on label.
							local systemName = mw.wikibase.label('Q'..reviewSysId);
							if(systemName ~= nil and string.upper(systemName) == system) then
								table.insert(reviewsToPrint,review);
							end;
						end;
					end;
				end;
			end;    		
		end;
	
		-- Sort the array by platform label.
    	table.sort(reviewsToPrint, sortByPlatform);
    	
    	-- If a system was not specified, showSystem has defaulted to true. If this title only has one platform and one review, we will turn it off.
    	-- Note: If the title has zero or more platforms defined, we leave showSystem on. We are unable to determine if this is a single-platform game.
    	--if((system == nil or system == "") and #reviewsToPrint == 1 and entity['claims']['P400'] ~= nil and #entity['claims']['P400'] == 1) then
    	-- Simplifying this based on discussion at [Template:Video game reviews]. If there's only one review, don't display system unless explicitly requested.
    	if((system == nil or system == "") and #reviewsToPrint == 1) then
    		showSystem = false;
    	end;

		-- Print the reviews
    	for i,review in ipairs(reviewsToPrint) do
    		ret = ret .. printReviewRow(frame, review);
		end;
	end;

	if(ret ~= "") then
		ret = string.sub(ret, 1, -7);
	elseif(not showUpdateLink) then
		ret = nil;
	end;
	
	-- Add edit link at end if showUpdateLink is on.
	if(showUpdateLink) then 
		ret = ret .. p.getUpdateLink();
	end;	

	return ret;
end;

return p