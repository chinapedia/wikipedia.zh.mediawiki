require('Module:No globals');


local p = {} 

local error_msg = '<span style=\"font-size:100%\" class=\"error\"><code style=\"color:inherit; border:inherit; padding:inherit;\">|_template=</code> missing or empty</span>';

-- data for various rankings held in module subpages, e.g. "Module:SportsRankings/data/FIFA World Rankings"
local data = {}      --[[ parameters containing data help in three tables
						data.source = {}     -- parameters for using in cite web (title, url, website)
						data.updated = {}    -- date of latest update (month, day, year)
						data.rankings = {}   -- the rankings list (country code, ranking, movement)
					    data.alias = {}      -- alias list (country code, country name [=key])
					    
					--]]

local  templateArgs = {} -- contains arguments from template involking module


local function getArgs(frame)
	local parents = mw.getCurrentFrame():getParent()
		
	for k,v in pairs(parents.args) do
		--check content
		if v and v ~= "" then
			templateArgs[k]=v --parents.args[k]
		end
	end
	for k,v in pairs(frame.args) do
		--check content
		if v and v ~= "" then
			templateArgs[k]=v --parents.args[k]
		end
	end
	-- allow empty caption to blank default
	if parents.args['caption'] then templateArgs['caption'] = parents.args['caption'] end
end

local function loadData(frame)
    
    local source = frame.args[1] -- source of rankings e.g. FIFA World Rankings
    data = require('Module:SportsRankings/data/'.. source);
    
end

local function getDate(option)
   
   local dateTable = data.updated         -- there must be date table (data.updated)
                                          -- TODO add a warning and/or category
   if option == "LAST" then 
   		local lastDateTable = data.previous 
   		if lastDateTable then             -- there might not be a previous data table (data.previous)
   			dateTable = lastDateTable
	   else 
	   		return "No previous date available (data.updated missing)"
       end
   end
   
   if templateArgs['mdy'] and templateArgs['mdy'] ~= "" then
   	   return dateTable['month'] .. " " .. dateTable['day'] .. ", " .. dateTable['year']
   else
   	   return dateTable['day'] .. " " .. dateTable['month'] .. " " .. dateTable['year']
   end
end

local function addCiteWeb(frame)  -- use cite web template
	
	return frame:expandTemplate{ title = 'cite web' , args = {
    		url = data.source['url'],            --"https://www.fifa.com/fifa-world-ranking/ranking-table/men/index.html", 
			title = data.source['title'],        -- "The FIFA/Coca-Cola World Ranking",
			website = data.source['website'],    --"FIFA",
			['date'] = getDate(),
			['access-date'] = getDate()
			}}
end
local function addReference(frame)
	
	local text = ""
	if data.source['text'] then text = data.source['text'] end
	
	return frame:expandTemplate{ title = 'refn' , args = {
		name=frame.args[1],                                 --ranking used, e.g. "FIFA World Rankings",
	    text .. addCiteWeb(frame)
	}}

end

--[[ the main function returning ranking for one country
      - takes three-letter country code or name of country as parameters
      - displays as rank | movement |date
]]
function p.main(frame)
	
    getArgs(frame) -- returns args table having checked for content
    loadData(frame)
    local outputString = ""
    local validCode = false
    local country = templateArgs[2] -- country name or county code passed as parameter
    local rank, move
    
    if string.len( country) ==  3 then -- if we have a three letter country code 
	    for _,u in pairs(data.alias) do  -- run through alias list { 3-letter code, country name }
	    	if u[1]==country then        -- if code = passed parameter
	       		country = u[2]           -- set country name as key for ranking table
	       		validCode = true
	       		break
	       	end
	    end    
	    -- if no match of code to country name, set category
	    if not validCode then
	    	outputString="[[Category:Pages_using_SportsRankings_with_unknown_parameters|Category:Pages using SportsRankings with unknown parameters]]" .. outputString
        end
    end
    for _,v in pairs(data.rankings) do
    	if v[1]==country then 
       		rank = v[2]    -- get rank
       		move = v[3]    -- get move from last ranking
       		break
       	end
    end
    if not rank then -- no ranking found (do we want a tracking for no rank found?)
    	rank = 'NR' 
	    --outputString="[[Category:Pages_using_SportsRankings_with_unknown_parameters|Category:Pages using SportsRankings with unknown parameters]]" .. outputString
        --outputString="[[Category:Pages_using_SportsRankings_with_no_ranking|Category:Pages using SportsRankings with no ranking]]" .. outputString
	end
	
	if rank ~= 'NR' then
		outputString = outputString .. ' ' .. rank .. ' '
		if move < 0 and math.abs( move ) == math.abs( rank ) then -- new teams in ranking: move = -ranking
			outputString = outputString .. frame:expandTemplate{ title = 'new entry' } 
	    elseif move == 0 then                                    -- if no change in ranking
	    	outputString = outputString .. frame:expandTemplate{ title = 'steady' } 
	    elseif move < 0 then                                 --  if ranking down
	    	outputString = outputString .. frame:expandTemplate{ title = 'decrease' } .. ' ' .. math.abs(move)
	    elseif move > 0 then                                 -- if ranking up
	    	outputString = outputString .. frame:expandTemplate{ title = 'increase' } .. ' ' .. move
	    end	
    else
    	outputString = outputString .. frame:expandTemplate{ title = 'Abbr', args = { "NR", "Not ranked"}  }
    	--	{{Abbr|NR|Not ranked}} 
	end
	outputString = outputString .. ' <small>(' .. getDate() .. ')</small>'
	outputString = outputString .. addReference(frame)
    
    return outputString
	
end

--[[  outputs a table of the rankings 
        called by list() or list2() 
        positional parameters - |ranking|first|last the ranking to use, fist and last in table
        other parameters: |style=               -- CSS styling
                          |headerN= footerN=    -- displays header and footer rows with additional information
                          |caption=             -- value of caption to display
                                                -- by default it generates a caption
                                                -- this can be suppressed with empty |caption=
]]
local function table(frame, ranking, first,last)

    local styleString = ""
    if templateArgs['style'] and templateArgs['style'] ~= "" then styleString = templateArgs['style'] end
    
    
    local sublist2 = { "ENG", "SCO", "WAL", "IRE", "NIR", "FRA", "England", "France", "Germany" }
    local sublist3 = { "AFG","AUS","BAN","BHR","BHU","BRU","CAM","CHN","GUM","HKG","IDN","IND","IRN","IRQ","JOR",
    	              "JPN","KGZ","KOR","KSA","KUW","LAO","LIB","MAC","MAS","MDV","MNG","MYA","NEP","OMA","PAK",
    	              "PHI","PLE","PRK","QAT","SIN","SRI","SYR","THA","TJK","TKM","TLS","TPE","UAE","UZB","VIE",
    	              "YEM" }
    local lastRank = 0
    local selectCount = 0
    local selectData = nil
    local selectList = nil
    if templateArgs['select'] then 
    	if data.confederation[templateArgs['select']] then
	    	selectList = templateArgs['select']
	    	selectData = data.confederation[selectList]
	    	selectCount = 1
    	end
    end
    
    -- column header customisation
    local rankHeader = templateArgs['rank_header'] or "Rank"
    local selectionHeader = templateArgs['selection_header'] or selectList or "Rank"
    local teamHeader = templateArgs['team_header'] or "Team"
    local pointsHeader = templateArgs['points_header'] or "Points"
    local changeHeader = templateArgs['change_header'] or "Change"
    
    --start table
    local outputString = '{| class="wikitable" style="text-align:center;' .. styleString .. '"'
    
    -- add default or custom caption
    local caption = ranking .. ' as of ' .. getDate() .. '.'
    if templateArgs['caption'] and templateArgs['caption']  ~= "" then 
    	caption = templateArgs['caption'] 
    	caption = p.replaceKeywords(caption)
    end
	outputString = outputString ..	'\n|+' .. caption .. addReference(frame)
    
    -- add header rows (logo, date of update etc)
    local count = 0
    local header = {}
    local tableWidth = 4
    if selectList then tableWidth = 5 end
    while count < 5 do
    	count = count + 1
	    if templateArgs['header'..count] then
	    	header[count] = templateArgs['header'..count] 
	    	header[count] = p.replaceKeywords( header[count])
	    	outputString = outputString ..	'\n|-\n| colspan="'.. tableWidth .. '" |' .. header[count]
	    end
    end
    
    -- add the add part of the table
    local optionalColumn = ""
    if selectList then
    	optionalColumn = '\n!' .. selectionHeader 
    end
   	outputString = outputString .. '\n|-' .. optionalColumn
    	                        .. '\n!' .. rankHeader .. '\n!' .. changeHeader 
    	                        .. '\n!' .. teamHeader .. '\n!' .. pointsHeader
   
    local change,code = '', ''
    --while i<last do 
    for k,v in pairs(data.rankings) do
	   --v[2] = tonumber(v[2])
	   if v[2] >= first and v[2] <= last then 

		   for _,u in pairs(data.alias) do  -- get country code from name
		    	if u[2]==v[1] then 
		       		code = u[1]    -- if alias (country code) then use country name as key
		       		break
		       	end
		    end   
	   	   
	   	    local continue = true
	   	    if selectList then                 -- select from list
	   	   	    continue = false 
	   			for _,u in pairs(selectData) do
	   				if u == v[1] or u == code then 
	   					continue = true 
	   					break
	   				end
	   			end
	   	    end
		
			if continue ==true  then 
	   	   
			   local rowString = '\n|-'
			   if selectList then 
			   	    local selectRank = selectCount
			   	    if v[2]==lastRank then selectRank = selectCount -1 end -- only handles two at same rank
					rowString = rowString ..  '\n|' .. selectRank 
					selectCount = selectCount + 1
			   end
			   rowString = rowString .. '\n|' .. v[2]  -- rank
			   lastRank = v[2]
			   
			   local move = v[3]
			   if move < 0 and math.abs( move ) == math.abs( v[2] ) then -- new teams in ranking: move = -ranking
					change = frame:expandTemplate{ title = 'new entry' } 
			   elseif move == 0 then                                    -- if no change in ranking
			    	change = frame:expandTemplate{ title = 'steady' } 
			    elseif move < 0 then                                 --  if ranking down
			    	change = frame:expandTemplate{ title = 'decrease' } .. ' ' .. math.abs(move)
			    elseif move > 0 then                                 -- if ranking up
			    	change = frame:expandTemplate{ title = 'increase' } .. ' ' .. move
			    end	
			   rowString = rowString .. '||' .. change
			   
	--[[		   for _,u in pairs(data.alias) do
			    	if u[2]==v[1] then 
			       		code = u[1]    -- if alias (country code) then use country name as key
			       		break
			       	end
			    end   
	]]		   
			   --TODO reorganise the following with better logic
			   --[[ template to display flag icon and team link (e.g. fb, fbw, bk, ih)
			       e.g.  "FIFA World Rankings" = 'fb', "FIFA Women's World Rankings" 'fbw',
			             "FIBA World Rankings" = 'bk', "IIHF World Ranking"  = 'ih'  
			       tries with country code, then if error, tried with country name]]
			   local countryTemplate = data.templates['flagged_team_link'] 
			   local countryIconString = frame:expandTemplate{ title = countryTemplate, args = {code} }    -- country
	 		   local _,test =  string.gsub( countryIconString, "Template:Country data", "") -- page does not exist
	 		   if test == 1 then -- if error try country name
	 		   	  countryIconString = frame:expandTemplate{ title = countryTemplate, args = {v[1]} }
	 		   	  --countryIconString = "testing"
	 		   else 
	 		   	 -- countryIconString = "exists"
	 		   end
	 		   	  
	 		   rowString = rowString .. '\n|style="text-align:left"|' .. countryIconString
			   
			   local points = ""
			   if v[4] then points = v[4] end
			   rowString = rowString ..  '||' .. points       -- country for now, later points
			   outputString = outputString .. rowString
			end
		end
	end
	
    -- add footer rows
    count = 0
    local footer = {}
    while count < 5 do
    	count = count + 1
	    if templateArgs['footer'..count] then
	    	footer[count] = templateArgs['footer'..count] 
	    	footer[count] = p.replaceKeywords(footer[count])
	    	outputString = outputString ..	'\n|-\n| colspan="'.. tableWidth .. '" |' .. footer[count]
	    end
    end


    outputString = outputString .. "\n|}"

    return outputString
	
end
function p.replaceKeywords(keyword)
      keyword =  string.gsub( keyword, "INSERT_UPDATE_DATE", getDate())
      keyword =  string.gsub( keyword, "INSERT_LAST_DATE", getDate("LAST"))
      keyword =  string.gsub( keyword, "INSERT_REFERENCE", addReference(mw.getCurrentFrame()))
      return keyword
end

--[[ create a table of rankings
       parameters:  |ranking=        -- ranking to display (e.g. FIFA World Rankings)
                    |first= |last=   -- first and last ranking to display (defaults 1-10)
]]
function p.list(frame)

    getArgs(frame) -- returns args table having checked for content
    loadData(frame)	
    local ranking = frame.args[1]
    local first, last = 1,10
    first = tonumber(frame.args['2'])
    last = tonumber(frame.args['3'])
    
    return table(frame, ranking, first, last)
end

--[[ create a particla table of rankings above and below a country 
       parameters:  |ranking |country |span     
                                              -- ranking - the ranking to display (e.g. FIFA World Rankings)
                                              -- country - country table is centred around
                                              -- span=   - rows to display above and below country
]]
function p.list2(frame)

    getArgs(frame) -- returns args table having checked for content
    loadData(frame)	
    local ranking = frame.args[1]
    local first, last = 1,10
    local country = frame.args[2]           -- name or code of country to center table around
    local span = frame.args[3] or 2         -- number of rows to display above and below country (default:2)
    
    if string.len(country) == 3 then        -- if three letter country code
    		for _,u in pairs(data.alias) do
		    	if u[1]==country then 
		       		country = u[2]          -- if country code then use country name 
		       		break
		       	end
		    end   
    end
    for k,v in pairs(data.rankings) do      -- find position of country in rankings
       if v[1] == country then
       	  first = v[2]-span
       	  last = v[2]+span
       end
    end
    
    return table(frame, ranking, first, last)
end

return p