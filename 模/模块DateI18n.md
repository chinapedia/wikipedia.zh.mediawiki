--[[  
 
This module is intended for processing of date strings.

Copied from https://commons.wikimedia.org/w/index.php?title=Module:Date&oldid=224728211
Used by Module:ISOdate, Module:Complex date, Module:WikidataIB

Authors and maintainers:
* User:Parent5446 - original version of the function mimicking template:ISOdate
* User:Jarekt - original version of the functions mimicking template:Date and template:ISOyear

]]


local p = {}

-- =======================================
-- === Dependencies ======================
-- =======================================
local i18n  = require('Module:I18n/date')		-- get localized translations of date formats
local yesno = require('Module:Yesno')

local function langSwitch(list,lang)
	local langList = mw.language.getFallbacksFor(lang)
	table.insert(langList,1,lang)
	for i,language in ipairs(langList) do
		if list[language] then
			return list[language]
		end
	end
end

--[[
Date
 
This function can be used to provide an ISOdate template. 
 
Usage:
{{#invoke:Date|Date|year=|month=|day=|hour=|minute=|second=|tzhour=|tzmin=|lang=en}}

Parameters:
  year,month,day,hour,minute,second: broken down date-time component strings
  tzhour, tzmin: timezone offset from UTC, hours and minutes
  lang: The language to display it in
  case: Language format (genitive, etc.) for some languages
 class: CSS class for the <time> node, use "" for no metadata at all

 Error Handling:

]]
function p.Date(frame)
	local args = frame.args
	if not (args.lang and mw.language.isSupportedLanguage(args.lang)) then 
		args.lang = frame:callParserFunction( "int", "lang" ) -- get user's chosen language 
	end
	return p._Date(	
		{ 
			args.year   or '', 
			args.month  or '',
			args.day    or '', 
			args.hour   or '', 
			args.minute or '', 
			args.second or '',
			args.tzhour or '',
			args.tzmin  or ''
		},
		args.lang,                  -- language
		args.case  or '',           -- allows to specify grammatical case for the month for languages that use them
		args.class or 'dtstart',    -- allows to set the html class of the time node where the date is included. This is useful for microformats.
		args.trim_year or '100-999' -- by default pad one and 2 digit years to be 4 digit long, while keeping 3 digit years as is
	)	
end


function p._Date(datevec, lang, case, class, trim_year)	
	-- make sure inputs are in the right format
	for i = #datevec + 1, 8 do
		datevec[i] = ''
	end
	if  not case  then case  = '' end
	if  not class then class = '' end
	if  not trim_year then trim_year = '100-999' end

	-- if language is not provided than look up users language
	-- WARNING: This step should be done by the template as it does not seem to work as well here (cache issues?)
	if not lang or not mw.language.isValidCode( lang ) then
		lang = 'en'
	end
	
	-- Just in case someone broke the internationalization code than fix the english defaults
	if i18n.DateLang['en'] == nil then
		i18n.DateLang['en'] = 'en-form'
	end	
	if i18n.DateFormat['en-form'] == nil then
		i18n.DateFormat['en-form'] = {YMDHMS='j F Y, H:i:s', YMDHM='j F Y, H:i', YMD='j F Y', YM='F Y', MD='j F', Y='Y'}
	end

	-- create datecode based on which variables are provided and check for out of bound values
	local maxval = {9999, 12, 31, 23, 59, 60, 23, 59} -- max values for year, month, ...
	local c = {'Y', 'M', 'D', 'H', 'M', 'S', '', ''}
	local datecode = '' -- a string signifying which combination of variables was provided
	local datenum = {}  -- date-time encoded as a vector = [year, month, ... , second]
	for i, v in ipairs( datevec ) do
		if v~=nil and v~='' then
			datecode = datecode .. c[i]
			datenum[i] = tonumber(v)
			if datenum[i]==nil and i==2 then
				-- month is not a number -> check if it is a month name in English
				v = mw.language.new('en'):formatDate( "n", v)
				datenum[i] = tonumber(v)
			end
			if datenum[i]==nil or datenum[i]>maxval[i] then
				-- Some numbers are out of range -> abort and return the empty string
				return ''
			end
		end
	end
	
	-- create time stamp string (for example 2000-02-20 02:20:20) based on which variables were provided
	local timeStamp
	if datecode == 'YMDHMS' then
		timeStamp = string.format('%04i-%02i-%02i %02i:%02i:%02i', datenum[1], datenum[2], datenum[3], datenum[4], datenum[5], datenum[6] )
	elseif datecode == 'YMDHM' then
		timeStamp = string.format('%04i-%02i-%02i %02i:%02i', datenum[1], datenum[2], datenum[3], datenum[4], datenum[5] )
	elseif datecode:sub(1,3)=='YMD' then
		timeStamp = string.format('%04i-%02i-%02i', datenum[1], datenum[2], datenum[3] )
		datecode = 'YMD' -- 'YMD', 'YMDHMS' and 'YMDHM' are the only supported format starting with 'YMD'. All others will be converted to 'YMD'
	elseif datecode == 'YM' then
		timeStamp = string.format('%04i-%02i', datenum[1], datenum[2] )
	elseif datecode:sub(1,1)=='Y' then
		timeStamp = string.format('%04i', datenum[1] )
		datecode = 'Y' 
	elseif datecode == 'M' then
		timeStamp = string.format('%04i-%02i-%02i', 2000, datenum[2], 1 )
		class = '' -- date not complete -> no html formating or micro-tagging of date string
	elseif datecode == 'MD' then
		timeStamp = string.format('%04i-%02i-%02i', 2000, datenum[2], datenum[3] )
		class = '' -- date not complete -> no html formating or micro-tagging of date string
	else
		return ''  -- format not supported
	end

	-- ==========================================================
	-- === Create Date String using in chosen language
	-- ==========================================================
	
	-- which form should the date take? 
	-- Use langSwitch to pick formating for each language
	local langDateForm = langSwitch(i18n.DateLang, lang)
	
	-- special case of French and Gallic dates, which require different date format for the 1st day of the month
	if datenum[3]==1 and (langDateForm=='fr-form' or langDateForm=='ga-form') then
		langDateForm = langDateForm .. '1' -- ordinal form for the first day of the month
	end
	-- special case of Basque dates, which require different date format for the 1st, 11th, 21st and 31st day of the month
	if langDateForm=='eu-form' then
		if (datenum[3]==1 or datenum[3]==21) then
			langDateForm = 'eu-form01'
		elseif (datenum[3]==11 or datenum[3]==31) then
			langDateForm = 'eu-form11'
		end
	end

	-- Look up country specific format input to {{#time}} function
	local dFormat = i18n.DateFormat[langDateForm][datecode]
	
	-- overwrite default grammatical case of the month (applies mostly to Slavic languages)
	if (case=='gen') then
		-- CAUTION: at the moment i18n.DateFormat uses "F" only as month name, but this might change and this operation does not check if 'F' is in "" brackets or not, so if some language starts using 'F'  in "" than this will not work for that language
		dFormat = dFormat:gsub("F", "xg"); 
	end
	if (case=='nom') then
		-- CAUTION: at the moment i18n.DateFormat uses "xg" only as month name, but this might change and this operation does not check if 'xg' is in "" brackets or not, so if some language starts using 'xg'  in "" than this will not work for that language
		dFormat = dFormat:gsub("xg", "F");
	end
	if ((lang=='ru' or lang=='pl' or lang=='cs' or lang=='sl' or lang=='sk') and (case=='loc' or case=='ins')) or
		(lang=='fi' and (case=='ptv' or case=='ine'or case=='ela'or case=='ill') ) then
		local monthEn =  mw.language.new('en'):formatDate( "F", timeStamp) -- month name in English
		-- month name using proper case and language. It relies on messages stored in MediaWiki namespace for some cases and languages
		-- That is why this IF statement uses "lang" not "langDateForm" variable to decide
		local monthMsg =  mw.message.new( string.format('%s-%s', monthEn, case ) ):inLanguage( lang )
		if not monthMsg:isDisabled() then -- make sure it exists
			local month=monthMsg:plain()
			dFormat = dFormat:gsub('F', '"'..month..'"'); -- replace default month with month name we already looked up
			dFormat = dFormat:gsub('xg', '"'..month..'"');
		end
	end
	-- Special case related to Quechua and Kichwa languages
	-- see https://commons.wikimedia.org/wiki/Template_talk:Date#Quechua from 2014
	if (lang=='qu' or lang=='qug') and case=='nom' then
		dFormat = dFormat:gsub('F"pi"', 'F');
	end	

	-- Lua only date formating using {{#time}} parser function (new)
		-- prefered call which gives "Lua error: too many language codes requested." on the [[Module_talk:Date/sandbox/testcases|Module talk:Date/sandbox/testcases]] page
		--local datestr = mw.language.new(lang):formatDate( dFormat, timeStamp) 
	local datestr = mw.getCurrentFrame():callParserFunction( "#time", { dFormat, timeStamp, lang } )
	
	-- Another special case related to Thai solar calendar
	if lang=='th' and datenum[1]~= nil and datenum[1]<=1940 then
		-- As of 2014 {{#time}} parser function did not resolve those cases properly
		-- See https://en.wikipedia.org/wiki/Thai_solar_calendar#New_year for reference
		-- Disable once https://bugzilla.wikimedia.org/show_bug.cgi?id=66648 is fixed
		if datecode=='Y' then -- date is ambiguous
			datestr = string.format('%04i หรือ %04i', datenum[1]+542, datenum[1]+543 ) 
		elseif datenum[2]<=3 then -- year is wrong (one too many)
			datestr = datestr:gsub( string.format('%04i', datenum[1]+543), string.format('%04i', datenum[1]+542 ) )
		end
	end
	
	-- If year<1000 than either keep it padded to the length of 4 digits or trim it
	-- decide if the year will stay padded with zeros (for years in 0-999 range)
	if datenum[1]~= nil and datenum[1]<1000 then
		local trim = yesno(trim_year,nil)
		if trim == nil then
			local YMin, YMax = trim_year:match( '(%d+)-(%d+)' )
			trim = (YMin~=nil and datenum[1]>=tonumber(YMin) and datenum[1]<=tonumber(YMax)) 
		end
	
		-- If the date form isn't the Thai solar calendar, don't zero pad years in the range of 100-999.  
		-- If at some point support for Islamic/Hebrew/Japanese years is added, they may need to be skipped as well. 
		if trim then
			--local yearStr1 = mw.language.new(lang):formatDate( 'Y', timeStamp)
			local yearStr1 = mw.getCurrentFrame():callParserFunction( "#time", { 'Y', timeStamp, lang } )
			--local yearStr1 = datestr:match( '%d%d%d%d' ) -- 4 digits in a row (in any language) - that must be a year
			local yearStr2 = yearStr1
			local zeroStr = mw.ustring.sub(yearStr1,1,1)
			for i=1,3 do -- trim leading zeros
				if mw.ustring.sub(yearStr2,1,1)==zeroStr then
					yearStr2 = mw.ustring.sub(yearStr2, 2, 5-i)
				else
					break
				end
			end
			datestr = datestr:gsub( yearStr1, yearStr2 )
			--datestr = string.format('%s (%s, %s)', datestr, yearStr1, yearStr2 )
		end
	end

	-- append timezone if present
	if datevec[7] ~= '' and (datecode == 'YMDHMS' or datecode == 'YMDHM') then
		local tzstr, tzhournum = '', tonumber(datevec[7])
		if tzhournum < 0 then tzstr = '−' else tzstr = '+' end
		tzstr = tzstr..string.format("%02d", math.abs(tzhournum))..':'
		if datevec[8] ~= '' then tzstr = tzstr..datevec[8] else tzstr = tzstr..'00' end
		datestr = datestr..' '..tzstr
	end

	-- html formating and tagging of date string
	if class ~= '' then
		local DateHtmlTags = '<span style="white-space:nowrap"><time class="%s" datetime="%s">%s</time></span>'
		datestr = DateHtmlTags:format(class, timeStamp, datestr)
	end
	return datestr
end

return p