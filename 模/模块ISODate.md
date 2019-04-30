--[[  
 
This module is intended for processing of date strings.

Please do not modify this code without applying the changes first at Module:ISOdate/sandbox and testing 
at Module:ISOdate/sandbox/testcases and Module talk:ISOdate/sandbox/testcases.

Authors and maintainers:
* User:Parent5446 - original version of the function mimicking template:ISOdate
* User:Jarekt - original version of the functions mimicking template:Date and template:ISOyear

]]

 
local p = {}

-- =======================================
-- === Dependencies ======================
-- =======================================
local D = require('Module:DateI18n') -- the enwp version of c:Module:Date

--[[
ISOyear
 
This function returns year part of date string.
 
Usage:
{{#invoke:ISOdate|ISOyear|target_string}}
 
Parameters
    1: The date string 
 
Error Handling:
   If the string does not look like it contain the year than the function will not return anything.
   That is the preferred treatment for the template:Creator which is the main (only?) template calling it.
]]
function p.ISOyear( frame )
	 return p._ISOyear( frame.args[1] )
end

function p._ISOyear( input )
	if not input then
		return ''
	end
	input = mw.text.trim( input )
    
	-- if empty string then return it
	if input == "" then
		return input
	end
    
	-- if number then return it
	if tonumber( input ) then
		return mw.ustring.format( '%04i', input )
	end
    
	-- otherwise use regular expression match
	input = mw.ustring.match( input, '^+?(-?%d%d?%d?%d?)-' )
	if input and tonumber( input ) then
		return mw.ustring.format( '%04i', input )
	else
		return ''
	end
end

--[[
ISOdate
 
This function is the core part of the ISOdate template. 
 
Usage:
{{#invoke:ISOdate|ISOdate|target_string|lang=}}
 
Parameters:
     1: The date string 
  lang: The language to display it in
  form: Language format (genitive, etc.) for some languages
 class: CSS class for the <time> node

 Error Handling:
   If the string does not look like it contain the proper ISO date than the function will return the original string.
   
   That is the preferred treatment for the template:Information (and similar templates) which calling it.
]]
function p.ISOdate(frame)
	local datestr, succeded
	local args = frame.args
	if not (args.lang and mw.language.isSupportedLanguage(args.lang)) then 
		args.lang = frame:callParserFunction( "int", "lang" ) -- get user's chosen language 
	end
	datestr, succeded = p._ISOdate(
		mw.text.trim(args[1]),
		args.lang,                  -- language
		args.case  or '',           -- allows to specify grammatical case for the month for languages that use them
		args.class or 'dtstart',    -- allows to set the html class of the time node where the date is included. 
		args.trim_year or '100-999' -- by default pad one and 2 digit years to be 4 digit long, while keeping 3 digit years as is	
	)
	return datestr
end

function p._ISOdate(datestr, lang, case, class, trim_year)

	-- pattern: regexp - regular expresion to test; dlen - number of date elements; tail = which element is a "tail" if any
	-- regexp hints:
	--  1) Strings starting with "^" and ending with "$" indicate whole string match
	--  2) optional tail part copied as-is and following the main parsed part of the date have to be separated from the date by a whitespace, so "(\s.+)?"
	local patterns = {
		-- strings starting with YYYY-MM-DD HH:MM:SS. Year 4 digits (if we know seconds than it was within the last 100 years), the rest 1-2
		-- date and time can be separated by space or "T" and there could be a "Z" on the end indicating "Zulu" time zone
		{dlen=6, tail=7, regexp="^+?(%d%d%d%d)-(%d%d?)-(%d%d?)[ T](%d%d?):(%d%d?):(%d%d?)Z?(%s.*)"}, 
		{dlen=6, tail=0, regexp="^+?(%d%d%d%d)-(%d%d?)-(%d%d?)[ T](%d%d?):(%d%d?):(%d%d?)Z?$"}, 
		-- strings starting with YYYY-MM-DD HH:MM. Year 4 digits, the rest 1-2
		-- (if one knows hour and minute than it was probably after a year 1000)
		{dlen=5, tail=6, regexp="^+?(%d%d%d%d)-(%d%d?)-(%d%d?)[ T](%d%d?):(%d%d?)(%s.+)"},
		{dlen=5, tail=0, regexp="^+?(%d%d%d%d)-(%d%d?)-(%d%d?)[ T](%d%d?):(%d%d?)$"},
		-- strings starting with YYYY-MM-DD. Year 1-4 digits, the rest 1-2
		{dlen=3, tail=4, regexp="^+?(%d%d?%d?%d?)-(%d%d?)-(%d%d?)(%s.+)"},
		{dlen=3, tail=0, regexp="^+?(%d%d?%d?%d?)-(%d%d?)-(%d%d?)$"},
		-- strings starting with YYYY-MM. Year 3-4 digits, month 2 digits
		-- (want to avoit converting to dates strings like 10-5 = 5
		{dlen=2, tail=3, regexp="^+?(%d%d%d%d?)-(%d%d)(%s.+)"}, 
		-- if whole string is in YYYY-MM form: If Year 1-4 digits, month 1-2 digits
		{dlen=2, tail=0, regexp="^+?(%d%d?%d?%d?)-(%d%d?)$"}, 
		-- string starts with a number -> it has to be 3 or 4 digit long to be a year
		{dlen=1, tail=2, regexp="^+?(%d%d%d%d?)(%s.+)"},	
		 -- if whole string is a number (1-4 digit long) than it will be interpreted as a year
		{dlen=1, tail=0, regexp="^+?(%d%d?%d?%d?)$"},
	}
	
	-- create datevec based on which variables are provided
	local datevec, tail, formatNum
	datevec, tail, formatNum = p.test_date_formats(datestr or '', patterns)
	if datevec[1]=='' or datevec[1]==nil then
		-- quickly return if datestr does not look like date (it could be a template)
		return datestr, false
	end

	-- call p._Date function to format date string
	local succeded, datestr2
	succeded, datestr2 = pcall( D._Date, datevec, lang, case, class, trim_year)
	if succeded and datestr2~='' then
		return mw.text.trim( datestr2 .. tail), true
	else -- in case of errors return the original string
		return datestr, false
	end	
end

function p.ISOdate_extended(frame)
	-- pattern: regexp - regular expresion to test; dlen - number of date elements; tail = which element is a "tail" if any
	-- regexp hints:
	--  1) Strings starting with "^" and ending with "$" indicate whole string match
	--  2) optional tail part copied as-is and following the main parsed part of the date have to be separated from the date by a whitespace, so "(\s.+)?"

	local datestr, succeded
	local args = frame.args
	if not (args.lang and mw.language.isSupportedLanguage(args.lang)) then 
		args.lang = frame:callParserFunction( "int", "lang" ) -- get user's chosen language 
	end
	datestr, succeded = p._ISOdate(
		mw.text.trim(args[1]),
		args.lang,                  -- language
		args.case  or '',           -- allows to specify grammatical case for the month for languages that use them
		args.class or 'dtstart',    -- allows to set the html class of the time node where the date is included. 
		args.trim_year or '100-999' -- by default pad one and 2 digit years to be 4 digit long, while keeping 3 digit years as is	
	)
	if succeded then
		return datestr
	end

	local patterns = {
		-- Exended set of recognized formats: like MM/DD/YYYY
		{dlen=3, tail=4, regexp="^(%d%d?)[-./](%d%d?)[-./](%d%d%d%d)(%s.+)"},
		{dlen=3, tail=0, regexp="^(%d%d?)[-./](%d%d?)[-./](%d%d%d%d)$"},
		{dlen=3, tail=0, regexp="^(%d%d?)%s(%w+)%s(%d%d%d%d)$"},
		{dlen=3, tail=0, regexp="^(%w+)%s(%d%d?),%s(%d%d%d%d)$"},
	}
	
	local datevec, tail, formatNum, category = ''
	datevec, tail, formatNum = p.test_date_formats(frame.args[1], patterns)
	if formatNum==1 or formatNum==2 then
		vec = datevec;
		if tonumber(datevec[1])>12 then
			frame.args[1] = string.format('%04i-%02i-%02i', datevec[3], datevec[2], datevec[1] )
			category = '[[Category:Date_in_DD/MM/YYYY_format|Category:Date in DD/MM/YYYY format]]'
			return mw.text.trim( p.ISOdate(frame) .. tail);
		elseif tonumber(datevec[2])>12 then
			frame.args[1] = string.format('%04i-%02i-%02i', datevec[3], datevec[1], datevec[2] )
			category = '[[Category:Date_in_MM/DD/YYYY_format|Category:Date in MM/DD/YYYY format]]'
			return mw.text.trim( p.ISOdate(frame) .. tail);
		end
	elseif (formatNum==3 or formatNum==4) and (datevec[3]=='' or datevec[3]~=nil) then
		local str = mw.getCurrentFrame():callParserFunction( "#time", { 'Y-m-d', datestr} )
		local vec = {str:match( "^(%d%d?%d?%d?)-(%d%d?)-(%d%d?)$" )}
		if vec and vec[1]~=nil then
			frame.args[1] = string.format('%04i-%02i-%02i', vec[1], vec[2], vec[3] )
			category = '[[Category:Date_in_word_format|Category:Date in word format]]'
			return p.ISOdate(frame);
		end
	end	
	return datestr
end

function p.test_date_formats(datestr, patterns)
	-- pattern: regexp - regular expresion to test; dlen - number of date elements; tail = which element is a "tail" if any

	local datevec = {'','','','','',''}
	local tail = ''
	local vec, pat
	local formatNum = 0
	for i, pat in ipairs( patterns ) do
		vec = {datestr:match( pat.regexp )}
		if vec and vec[1]~=nil then
			for j=1,pat.dlen do
				datevec[j] = vec[j]
			end
			if pat.tail>0 and vec[pat.tail]~=nil then
				tail = mw.ustring.gsub(' ' .. vec[pat.tail], ' +', ' ')
			end
			formatNum = i
			break
		end
	end
	return datevec, tail, formatNum
end

return p