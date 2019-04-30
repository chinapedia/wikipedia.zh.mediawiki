--[[ 
  __  __           _       _         ____                      _                 _       _       
 |  \/  | ___   __| |_   _| | ___ _ / ___|___  _ __ ___  _ __ | | _____  __   __| | __ _| |_ ___ 
 | |\/| |/ _ \ / _` | | | | |/ _ (_) |   / _ \| '_ ` _ \| '_ \| |/ _ \ \/ /  / _` |/ _` | __/ _ \
 | |  | | (_) | (_| | |_| | |  __/_| |__| (_) | | | | | | |_) | |  __/>  <  | (_| | (_| | ||  __/
 |_|  |_|\___/ \__,_|\__,_|_|\___(_)\____\___/|_| |_| |_| .__/|_|\___/_/\_\  \__,_|\__,_|\__\___|
                                                        |_|                                      
 
This module is intended for creation of complex date phrases in variety of languages.
 
Once deployed, please do not modify this code without applying the changes first at Module:Complex date/sandbox and testing 
at Module:Complex date/sandbox/testcases.
 
Authors and maintainers:
* User:Sn1per - first draft of the original version 
* User:Jarekt - corrections and expansion of the original version 
 
]]

-- List of external modules and functions
local p = {Error = nil}
local i18n       = require('Module:i18n/complex date')
local ISOdate    = require('Module:ISOdate')._ISOdate
local Calendar -- loaded lazily

-- ==================================================
-- === Internal functions ===========================
-- ==================================================

local function langSwitch(list,lang)
	local langList = mw.language.getFallbacksFor(lang)
	table.insert(langList,1,lang)
	table.insert(langList,math.max(#langList,2),'default')
	for i,language in ipairs(langList) do
		if list[language] then
			return list[language]
		end
	end
end

local function formatnum1(numStr, lang)
-- mostly require('Module:Formatnum').formatNum function used to translate a number to use different numeral characters, 
-- except that it it does not call  that function unless the language is on the list "LList"
	local LList = {bn=1,bpy=1,kn=1,hi=1,mr=1,new=1,pa=1,gu=1,fa=1,glk=1,mzn=1,ur=1,ar=1,ckb=1,ks=1,lo=1,['or']=1,bo=1,['ml-old']=1,mn=1,te=1,th=1}
	if LList[lang] then -- call only when the language is on the list
		numStr = require('Module:Formatnum').formatNum(numStr, lang, 1)
	end
	return numStr
end

local function getISODate(datestr, datetype, lang, num, case)
-- translate dates in the format YYYY, YYYY-MM, and YYYY-MM-DD
	if  not case and i18n.Translations[datetype] then
		-- look up the grammatical case needed and call ISOdate module
		local rec = langSwitch(i18n.Translations[datetype], lang)
		if type(rec)=='table' then
			case = rec.case[num]
		end
	end
	return ISOdate(datestr, lang, case, '', 1)
end

local function translatePhrase(date1, date2, operation, lang, state)
-- use tables in Module:i18n/complex date to translate a phrase
	if not i18n.Translations[operation] then
		p.Error = string.format('<span style="background-color:red;">Error in [[Module:Complex_date|Module:Complex date]]: input parameter "%s" is not recognized.</span>', operation or 'nil')
		return ''
	end
	local dateStr = langSwitch(i18n.Translations[operation], lang)
	if type(dateStr)=='table' then
		dateStr = dateStr[1]
	end
	if type(dateStr)=='function' then
		local success
		local nDates = i18n.Translations[operation]['nDates']
		if nDates==2 then -- 2 date phrase
			success, dateStr = pcall(dateStr, date1, date2, state)
		else  -- 1 date phrase
			success, dateStr = pcall(dateStr, date1, state)
		end
	end
	
	if type(dateStr)=='string' then
		-- replace parts of the string '$date1' and '$date2' with date1 and date2 strings
		dateStr = mw.ustring.gsub(dateStr, '$date1', date1)
		dateStr = mw.ustring.gsub(dateStr, '$date2', date2)
	else
		-- Special case of more complex phrases that can be build out of simple phrases
		-- If complex case is not translated to "lang" than build it out of simpler ones
		local x = dateStr
		dateStr = p._complex_date(x.conj, x.adj1, date1, x.units1, x.era1, x.adj2, date2, x.units2, x.era2, lang, 2)
	end
	return dateStr
end

local function oneDatePhrase(dateStr, adj, era, units, lang, num, case, state)
-- translate a single date phrase
	if num==2 then
		state.adj, state.era, state.units, state.precision = state.adj2, state.era2, state.units2, state.precision2 
	end
	
	-- dateStr can have many forms: ISO date, year or a number for 
	-- decade, century or millennium
	if units == '' then -- unit is "year", "month", "day"
		dateStr = getISODate(dateStr, adj, lang, num, case)
	else -- units is "decade", "century", "millennium''
		dateStr = translatePhrase(dateStr, '', units, lang, state)
	end
	
	-- add adjective ("early", "mid", etc.) or preposition ("before", "after", 
	-- "circa", etc.) to the date
	if adj ~= '' then
		dateStr = translatePhrase(dateStr, '', adj, lang, state)
	else -- only era?
		dateStr = formatnum1(dateStr, lang)
	end
	
	-- add era
	if era ~= '' then
		dateStr = translatePhrase(dateStr, '', era, lang, state)
	end
	return dateStr
end

local function twoDatePhrase(date1, date2, state, lang)
-- translate a double date phrase
	local dateStr, case
	local era=''
	if state.era1 == state.era2 then
		-- if both eras are the same than add it only once
		era = state.era1
		state.era1 = ''
		state.era2 = ''
	end
	case = {nil, nil}
	if i18n.Translations[state.conj] then
		local rec = langSwitch(i18n.Translations[state.conj], lang)
		if type(rec)=='table' then
			case = rec.case
		end
	end
	date1   = oneDatePhrase(date1, state.adj1, state.era1, state.units1, lang, 1, case[1], state)
	date2   = oneDatePhrase(date2, state.adj2, state.era2, state.units2, lang, 2, case[2], state)
	dateStr = translatePhrase(date1, date2, state.conj, lang, state)
	if era ~= '' then
		dateStr = translatePhrase(dateStr, '', era, lang, state)
	end
	return dateStr
end

local function otherPhrases(date1, date2, operation, era, lang, state)
-- translate specialized phrases
	local dateStr = ''
		
	if operation == 'islamic' then
		if date2=='' then date2 = mw.getCurrentFrame():callParserFunction('#time', 'xmY', date1) end
		date1 = getISODate(date1, operation, lang, 1, nil)
		date2 = getISODate(date2, operation, lang, 2, nil)
		if era == '' then era = 'ad' end
		dateStr = translatePhrase(date1, '', era, lang, state) .. ' (' .. translatePhrase(date2, '', 'ah', lang, state) .. ')'
		era = ''
	elseif operation == 'julian' then
		if not date2 and date1 then -- Convert from Julian to Gregorian calendar date
			if Calendar == nil then
				Calendar = require("Module:Calendar")
			end
			local JDN = Calendar._date2jdn(date1, 0)
			if JDN then
				date2 = date1 -- first date is assumed to be Julian
				date1 = Calendar._jdn2date(JDN, 1)
			end
		end
		date1 = getISODate(date1, operation, lang, 1, nil)
		date2 = getISODate(date2, operation, lang, 2, nil)
		dateStr = translatePhrase(date1, date2, operation, lang, state)
		dateStr = mw.ustring.gsub(mw.ustring.gsub(dateStr, '%( ', '('), ' %)', ')') -- in case date2 is empty
	elseif operation == 'turn of the year' or operation == 'turn of the decade' or operation == 'turn of the century' then
		local dt = 1
		if operation == 'turn of the decade' then dt=10 end
		if not date2 or date2=='' then date2=tostring(tonumber(date1)-dt) end
		if era~='bp' and era~='bc' then date1, date2 = date2, date1 end
		if operation == 'turn of the year' then
			date1 = ISOdate(date1, lang, '', '', 1)
			date2 = ISOdate(date2, lang, '', '', 1)
		else
			date1 = formatnum1(date1, lang)
			date2 = formatnum1(date2, lang)
		end
		dateStr = translatePhrase(date1, date2, operation, lang, state)
	elseif operation == 'year unknown' then
		dateStr = translatePhrase('', '', operation, lang, state)
	elseif operation == 'unknown' then
		dateStr = tostring(mw.message.new( "exif-unknowndate" ):inLanguage( lang ))
	end
	
	-- add era
	if era ~= '' then
		dateStr = translatePhrase(dateStr, '', era, lang, state)
	end
	return dateStr
end

local function checkAliases(str1, str2, sType)
-- some inputs have many aliases - reconcile them and ensure string is playing a proper role	
local out = ''
if str1 and str1~='' then
	a = i18n.Synonyms[str1] -- look up synonyms of "str1"
	if a then
		out = a[1]
	else
		p.Error = string.format('<span style="background-color:red;">Error in [[Module:Complex_date|Module:Complex date]]: %s is not recognized.</span>', str1)
	end
elseif str2 and str2~='' then -- if "str1" of type "sType" is empty than maybe ...
	a = i18n.Synonyms[str2]   -- ..."str2" is of the same type and is not empty
	if a and a[2]==sType then
		out  = a[1]
		str2 = ''
	end
end
return out, str2
end

local function datePrecision(dateStr, units)	
-- "in this module "Units" is a string like millennium, century, or decade
--	"precision" is wikibase compatible date precision number: 6=millennium, 7=century, 8=decade, 9=year, 10=month, 11=day
-- based on string or numeric input calculate "Units" and "precision"
	local dateNum = tonumber(dateStr);
	if type(units)=='number' then
		precision = units
		if precision>11 then precision=11 end -- clip the range of precision values
		if     precision==6 then units='millennium' 		
		elseif precision==7 then units='century'
		elseif precision==8 then units='decade'
		else units = ''
		end
	elseif type(units)=='string' then
		units = string.lower(units);
		if     units=='millennium' then precision=6
		elseif units=='century'    then precision=7
		elseif units=='decade'     then precision=8
		else precision=9
		end
	end
	if units=='' or precision==9 then
		local sLen = mw.ustring.len(dateStr)
		if     sLen<= 4 then precision=9
		elseif sLen== 7 then precision=10
		elseif sLen>=10 then precision=11
		end
		units=''
	end
	if precision==6 and dateStr.match( dateStr, '%d000' )~=nil then 
		dateStr = tostring(math.floor(tonumber(dateStr)/1000) +1)
	elseif precision==7 and mw.ustring.match( dateStr, '%d%d00' )~=nil then
		dateStr = tostring(math.floor(tonumber(dateStr)/100) +1)
	end

	return dateStr, units, precision
end


local function isodate2timestamp(dateStr, precision, era)
-- convert date string to timestamps used by Quick Statements
	local tStamp = nil
	if era == 'ah' or precision<6 then
		return nil
	elseif era ~= '' then
		eraLUT = {ad='+', bc='-', bp='-' }
		era = eraLUT[era]
	else
		era='+'
	end

-- convert isodate to timestamp used by quick statements
	if precision>=9 then 
		if string.match(dateStr,"^%d%d%d%d$") then               -- if YYYY  format 
			tStamp = era .. dateStr .. '-00-00T00:00:00Z/9'
		elseif string.match(dateStr,"^%d%d%d%d%-%d%d$") then      -- if YYYY-MM format 
			tStamp = era .. dateStr .. '-00T00:00:00Z/10'
		elseif string.match(dateStr,"^%d%d%d%d%-%d%d%-%d%d$") then  -- if YYYY-MM-DD format 
			tStamp = era .. dateStr .. 'T00:00:00Z/11'
		end
	elseif precision==8 then -- decade
		tStamp = era .. dateStr .. '-00-00T00:00:00Z/8'
	elseif precision==7 then -- century
		local d = tostring(tonumber(dateStr)-1)
		tStamp = era .. d .. '50-00-00T00:00:00Z/7'
	elseif precision==6 then
		local d = tostring(tonumber(dateStr)-1)
		tStamp = era .. d .. '500-00-00T00:00:00Z/6'
	end
	
	return tStamp
end

local function oneDateQScode(dateStr, adj, era, precision)
-- create QuickStatements string for "one date" dates
	local outputStr = ''

	local d = isodate2timestamp(dateStr, precision, era)
	if not d then
		return ''
	end
	local rLUT = {            early='Q40719727'     , mid='Q40719748',      late='Q40719766',
		['1quarter']='Q40690303' , ['2quarter']='Q40719649'  , ['3quarter']='Q40719662', ['4quarter']='Q40719674',
		spring='Q40720559'   , summer='Q40720564'    , autumn='Q40720568'  , winter='Q40720553',
		firsthalf='Q40719687', secondhalf='Q40719707' }
	local qLUT = {['from']='P580', ['until']='P582', ['after']='P1319', ['before']='P1326'}

	local refine = rLUT[adj]
	local qualitier = qLUT[adj]

	if adj=='' then
		outputStr = d
	elseif adj=='circa' then
		outputStr = d..",P1480,Q5727902"
	elseif refine then
		outputStr = d..",P4241,"..refine
	elseif precision>7 and qualitier then
		local century = string.gsub(d, 'Z%/%d+', 'Z/7')
		outputStr = century ..",".. qualitier ..","..d
	end
	return outputStr 
end

local function twoDateQScode(date1, date2, state)
-- create QuickStatements string for "two date" dates
	if state.adj1~='' or state.adj2~='' or state.era1~=state.era2 then
		return ''
	end
	local outputStr = ''
	local d1 = isodate2timestamp(date1, state.precision1, state.era1)
	local d2 = isodate2timestamp(date2, state.precision2, state.era2)
	if (not d1) or (not d2) then
		return ''
	end	
	-- find date with lower precision in common to both dates
	local cd
	local year1 = string.sub(d1,2,5)
	local k = 0
	for i = 1,10,1 do 
		if string.sub(d1,1,i)==string.sub(d2,1,i) then 
			k = i -- find last matching letter
		end
	end
	if k>=9 then              -- same month, since "+YYYY-MM-" is in common
		cd = isodate2timestamp(string.sub(d1,2,8), 10, state.era1)
	elseif k>=6 and k<9 then  -- same year, since "+YYYY-" is in common
		cd = isodate2timestamp(year1, 9, state.era1)
	elseif k==4 then          -- same decade(k=4, precision=8),  since "+YYY" is in common
		cd = isodate2timestamp(year1, 8, state.era1)
	elseif k==3 then          -- same century(k=3, precision=7) since "+YY" is in common
	  local d = tostring(math.floor(tonumber(year1)/100) +1) -- convert 1999 -> 20
		cd = isodate2timestamp( d, 7, state.era1)
	elseif k==2 then          -- same millennium (k=2, precision=6),  since "+Y" is in common
		local d = tostring(math.floor(tonumber(year1)/1000) +1) -- convert 1999 -> 2
		cd = isodate2timestamp( d, 6, state.era1)
	else
		return ''
	end
	--if not cd then
	--	return ' <br/>error: ' .. d1.." / " .. d2.." / ".. (cd or '') .." / ".. string.sub(d1,2,5).." / " .. string.sub(d2,2,5).." / " .. tostring(k)
	--end

	--
	if state.conj=='from-until' then
		outputStr = cd ..",P580,".. d1 ..",P582,".. d2
	elseif state.conj=='between' then
		outputStr = cd ..",P1319,".. d1 ..",P1326,".. d2
	elseif state.conj=='circa2' then
		outputStr = cd ..",P1319,".. d1 ..",P1326,".. d2 ..",P1480,Q5727902"
	end

	return outputStr
end

-- ==================================================
-- === External functions ===========================
-- ==================================================

function p.Era(frame)
    -- process inputs
	local dateStr
	local args    = frame.args
	if not (args.lang and mw.language.isSupportedLanguage(args.lang)) then 
		args.lang = frame:callParserFunction( "int", "lang" ) -- get user's chosen language  
	end
	local lang    = args['lang']
	local dateStr = args['date'] or ''
	local eraType = string.lower(args['era']  or '')

	dateStr = ISOdate(dateStr, lang, '', '', 1)
	if eraType then 
		eraType = checkAliases(eraType ,'','e')
		dateStr = translatePhrase(dateStr, '', eraType, lang, {}) 
	end
	return dateStr
end
	
function p._complex_date(conj, adj1, date1, units1, era1, adj2, date2, units2, era2, lang, passNr)
	local Output=''

    -- process inputs and save date in state array
	local state  = {} 
	state.conj   = string.lower(conj   or '')
	state.adj1   = string.lower(adj1   or '')
	state.adj2   = string.lower(adj2   or '')
	state.era1   = string.lower(era1   or '')
	state.era2   = string.lower(era2   or '')
	state.units1 = string.lower(units1 or '')
	state.units2 = string.lower(units2 or '')
		  
	-- if date 1 is missing but date 2 is provided than swap them
	if date1 == '' and date2 ~= '' then
		date1 = date2
		date2 = ''
		state = {adj1 = state.adj2, era1 = state.era2, units1 = state.units2, 
		         adj2 = '',         era2 = '',         units2 = '',  conj=state.conj, num=1}
	end
	if     date2 ~= '' then state.nDates = 2 
	elseif date1 ~= '' then state.nDates = 1 
	else	                  state.nDates = 0
	end
	
	-- reconcile alternative names for text inputs
	local conj         = checkAliases(state.conj ,''  ,'j')
	state.adj1 ,conj   = checkAliases(state.adj1 ,conj,'a')
	state.units1,conj  = checkAliases(state.units1,conj,'p')
	state.era1 ,conj   = checkAliases(state.era1 ,conj,'e')
	state.special,conj = checkAliases('',conj,'c')
	state.adj2         = checkAliases(state.adj2 ,'','a')
	state.units2       = checkAliases(state.units2,'','p')
	state.era2         = checkAliases(state.era2 ,'','e')
	state.conj         = conj
	state.lang         = lang
	if p.Error~=nil then
		return nil
	end
	
	-- calculate date precision value
	date1, state.units1, state.precision1 = datePrecision(date1, state.units1)
	date2, state.units2, state.precision2 = datePrecision(date2, state.units2)

	-- Handle special cases 
	-- Some complex phrases can be created out of simpler ones. Therefore on pass # 1 we try to create 
	-- the phrase using complex phrase and if that is not found than on the second pass we try to build
	-- the phrase out of the simpler ones
	if passNr==1 then
		if state.adj1=='circa' and state.nDates == 2 then
			state.conj = 'circa2'
			state.adj1 = ''
			state.adj2 = ''
		end
		if state.nDates == 2 and state.adj1=='late' and state.adj2=='early' and state.conj=='and' 
		and state.units1==state.units2 and state.era1==state.era2 then
			if state.units1=='century' then
				state.conj='turn of the century'
			elseif state.units1=='decade' then
				state.conj='turn of the decade'
			elseif state.units1=='' then
				state.conj='turn of the year'
			end
			state.adj1 = ''
			state.adj2 = ''
			state.units1 = ''
			state.units2 = ''
		end
	end

	local errorStr = string.format(
	 '\n*conj=%s, adj1=%s, era1=%s, unit1=%s, prec1=%i, adj2=%s, era2=%s, unit2=%s, prec2=%i, special=%s', 
	  state.conj, state.adj1, state.era1, state.units1, state.precision1,
	  state.adj2, state.era2, state.units2, state.precision2, state.special)  
	state.adj, state.era, state.units, state.precision = state.adj1, state.era1, state.units1, state.precision1 

	-- call specialized functions
	local QScode = ''
	if state.special~='' then
		Output = otherPhrases(date1, date2, state.special, state.era1, lang, state)	
	elseif state.conj~='' then
		QScode = twoDateQScode(date1, date2, state)
		Output = twoDatePhrase(date1, date2, state, lang)
	elseif state.adj1~='' or state.era1~='' or state.units1~='' then
		Output = oneDatePhrase(date1, state.adj1, state.era1, state.units1, lang, 1, nil, state)
		QScode = oneDateQScode(date1, state.adj1, state.era1, state.precision1)
	elseif date1~='' then
		Output = ISOdate(date1, lang, '', 'dtstart', '100-999')
	end
	if p.Error~=nil then
		return errorStr
	end

	-- if there is any wikicode in the string than execute it
	if mw.ustring.find(Output, '{') then
		Output = mw.getCurrentFrame():preprocess(Output)
	end
	if QScode and #QScode>0 then
		QScode = ' <div style="display: none;">date QS:P,' .. QScode .. '</div>'
	end

	return Output .. QScode
end

function p.complex_date(frame)
    -- process inputs
	local dateStr, Error
	local args   = frame.args
	if not (args.lang and mw.language.isSupportedLanguage(args.lang)) then 
		args.lang = frame:callParserFunction( "int", "lang" ) -- get user's chosen language  
	end
	local date1  = args['date1'] or args['2'] or args['date'] or ''
	local date2  = args['date2'] or args['3'] or ''
	local conj   = args['conj']  or args['1'] or ''
	local adj1   = args['adj1']  or args['adj'] or ''
	local adj2   = args['adj2'] or ''
	local units1 = args['precision1'] or args['precision'] or ''
	local units2 = args['precision2'] or args['precision'] or ''
	local era1   = args['era1'] or args['era'] or ''
	local era2   = args['era2'] or args['era'] or ''
	local lang   = args['lang']

	dateStr = p._complex_date(conj, adj1, date1, units1, era1, adj2, date2, units2, era2, lang, 1)
	if p.Error~=nil then
		dateStr = p.Error .. '[[Category:Pages_using_Complex_date_template_with_incorrect_parameter|Category:Pages using Complex date template with incorrect parameter]]'
	end
	return dateStr
end

return p