-- Module to implement use of a blacklist and whitelist for infobox fields
-- Can take a named parameter |qid which is the Wikidata ID for the article
-- if not supplied, it will use the Wikidata ID associated with the current page.
-- Fields in blacklist are never to be displayed, i.e. module must return nil in all circumstances
-- Fields in whitelist return local value if it exists or the Wikidata value otherwise
-- The name of the field that this function is called from is passed in named parameter |name
-- The name is compulsory when blacklist or whitelist is used,
-- so the module returns nil if it is not supplied.
-- blacklist is passed in named parameter |suppressfields (or |spf)
-- whitelist is passed in named parameter |fetchwikidata (or |fwd)

local p = {}

local cdate -- initialise as nil and only load _complex_date function if needed
-- [[Module:Complex_date|Module:Complex date]] is loaded lazily and has the following dependencies:
-- Module:I18n/complex date, Module:ISOdate, Module:DateI18n (alternative for Module:Date),
-- Module:Formatnum, Module:I18n/date, Module:Yesno, Module:Linguistic, Module:Calendar
-- The following, taken from https://www.mediawiki.org/wiki/Wikibase/DataModel#Dates_and_times,
-- is needed to use Module:Complex date which seemingly requires date precision as a string.
-- It would work better if only the authors of the mediawiki page could spell 'millennium'.
local dp = {
	[6] = "millennium",
	[7] = "century",
	[8] = "decade",
	[9] = "year",
	[10] = "month",
	[11] = "day",
}

local i18n =
{
	["errors"] =
	{
		["property-not-found"] = "未找到属性。",
		["No property supplied"] = "未找到Wikidata属性。",
		["entity-not-found"] = "未找到Wikidata实体。",
		 ["unknown-claim-type"] = "未知声称类型。",
		["unknown-entity-type"] = "未知实体类型。",
		["qualifier-not-found"] = "未找到修饰词。",
		["site-not-found"] = "未找到维基媒体项目。",
		["labels-not-found"] = "未找到Wikidata标签。",
		["descriptions-not-found"] = "未找到描述。",
		["aliases-not-found"] = "未找到別称",
		["unknown-datetime-format"] = "未知日期时间格式。",
		["local-article-not-found"] = "存在维基数据但中文维基尚无此条目",
		["dab-page"] = " (dab)",
	},
	["months"] =
	{
		"1月", "2月", "3月", "4月", "5月", "6月", "7月", "8月", "9月", "10月", "11月", "12月"
	},
	["century"] = "世纪",
	["BC"] = "公元前",
	["BCE"] = "公元前",
	["ordinal"] =
	{
		[1] = "",
		[2] = "",
		[3] = "",
		["default"] = ""
	},
	["filespace"] = "File",
	["Unknown"] = "Unknown",
	["NaN"] = "Not a number",
	-- set the following to the name of a tracking category,
	-- e.g. "[[Category:Articles_with_missing_Wikidata_information|Category:Articles with missing Wikidata information]]", or "" to disable:
	["missinginfocat"] = "[[Category:缺少維基數據信息的條目|Category:缺少維基數據信息的條目]]",
	["editonwikidata"] = "編輯維基數據",
	["latestdatequalifier"] = function (date) return "before " .. date end,
	-- some languages, e.g. Bosnian use a period as a suffix after each number in a date
	["datenumbersuffix"] = "",
	["list separator"] = ", ",
	["multipliers"] = {
		[0]  = "",
		[3]  = " thousand",
		[6]  = " million",
		[9]  = " billion",
		[12] = " trillion",
	}
}
-- This allows a internationisation module to override the above table
if 'en' ~= mw.getContentLanguage():getCode() then
	require("Module:i18n").loadI18n("Module:WikidataIB/i18n", i18n)
end

-- This piece of html implements a collapsible container. Check the classes exist on your wiki.
local collapsediv = '<div class="mw-collapsible mw-collapsed" style="width:100%; overflow:auto;" data-expandtext="{{int:show}}" data-collapsetext="{{int:hide}}">'

-- Some items should not be linked.
-- Each wiki can create a list of those in Module:WikidataIB/nolinks
-- It should return a table called itemsindex, containing true for each item not to be linked
local donotlink = {}
local nolinks_exists, nolinks = pcall(mw.loadData, "Module:WikidataIB/nolinks")
if nolinks_exists then
	donotlink = nolinks.itemsindex
end

-------------------------------------------------------------------------------
-- Private functions
-------------------------------------------------------------------------------
--
-------------------------------------------------------------------------------
-- makeOrdinal needs to be internationalised along with the above:
-- takes cardinal numer as a numeric and returns the ordinal as a string
-- we need three exceptions in English for 1st, 2nd, 3rd, 21st, .. 31st, etc.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local makeOrdinal = function(cardinal)
	local ordsuffix = i18n.ordinal.default
	if cardinal % 10 == 1 then
		ordsuffix = i18n.ordinal[1]
	elseif cardinal % 10 == 2 then
		ordsuffix = i18n.ordinal[2]
	elseif cardinal % 10 == 3 then
		ordsuffix = i18n.ordinal[3]
	end
	-- In English, 1, 21, 31, etc. use 'st', but 11, 111, etc. use 'th'
	-- similarly for 12 and 13, etc.
	if (cardinal % 100 == 11) or (cardinal % 100 == 12) or (cardinal % 100 == 13) then
		ordsuffix = i18n.ordinal.default
	end
	return tostring(cardinal) .. ordsuffix
end


-------------------------------------------------------------------------------
-- findLang takes a "langcode" parameter if supplied and valid
-- otherwise it tries to create it from the user's set language ({{int:lang}})
-- failing that it uses the wiki's content language.
-- It returns a language object
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local findLang = function(langcode)
	local langobj
	langcode = mw.text.trim(langcode or "")
	if mw.language.isKnownLanguageTag(langcode) then
		langobj = mw.language.new( langcode )
	else
		langcode = mw.getCurrentFrame():preprocess( '{{int:lang}}' )
		if mw.language.isKnownLanguageTag(langcode) then
			langobj = mw.language.new( langcode )
		else
			langobj = mw.language.getContentLanguage()
		end
	end
	return langobj
end


-------------------------------------------------------------------------------
-- _getItemLangCode takes a qid parameter (using the current page's qid if blank)
-- If the item for that qid has property country (P17) it looks at the first preferred value
-- If the country has an official language (P37), it looks at the first preferred value
-- If that official language has a language code (P424), it returns the first preferred value
-- Otherwise it returns nothing.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local _getItemLangCode = function(qid)
	qid = mw.text.trim(qid or ""):upper()
	if qid == "" then qid = mw.wikibase.getEntityIdForCurrentPage() end
	if not qid then return end
	local prop17 = mw.wikibase.getBestStatements(qid, "P17")[1]
	if not prop17 or prop17.mainsnak.snaktype ~= "value" then return end
	local qid17 = prop17.mainsnak.datavalue.value.id
	local prop37 = mw.wikibase.getBestStatements(qid17, "P37")[1]
	if not prop37 or prop37.mainsnak.snaktype ~= "value" then return end
	local qid37 = prop37.mainsnak.datavalue.value.id
	local prop424 = mw.wikibase.getBestStatements(qid37, "P424")[1]
	if not prop424 or prop424.mainsnak.snaktype ~= "value" then return end
	return prop424.mainsnak.datavalue.value
end


-------------------------------------------------------------------------------
-- roundto takes a number (x)
-- and returns it rounded to (sf) significant figures
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local roundto = function(x, sf)
	if x == 0 then return 0 end
	local s = 1
	if x < 0 then
		x = -x
		s = -1
	end
	if sf < 1 then sf = 1 end
	local p = 10 ^ (math.floor(math.log10(x)) - sf + 1)
	x = math.floor(x / p + 0.5) * p * s
	-- if it's integral, cast to an integer:
	if x == math.floor(x) then x = math.floor(x) end
	return x
end


-------------------------------------------------------------------------------
-- decimalToDMS takes a decimal degrees (x) with precision (p)
-- and returns degrees/minutes/seconds according to the precision
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local decimalToDMS = function(x, p)
	-- if p is not supplied, use a precision around 0.1 seconds
	if not tonumber(p) then p = 1e-4 end
	local d = math.floor(x)
	local ms = (x - d) * 60
	if p > 0.5 then -- precision is > 1/2 a degree
		if ms > 30 then d = d + 1 end
		ms = 0
	end
	local m = math.floor(ms)
	local s = (ms - m) * 60
	if p > 0.008 then -- precision is > 1/2 a minute
		if s > 30 then m = m +1 end
		s = 0
	elseif p > 0.00014 then -- precision is > 1/2 a second
		s = math.floor(s + 0.5)
	elseif p > 0.000014 then -- precision is > 1/20 second
		s = math.floor(10 * s + 0.5) / 10
	elseif p > 0.0000014 then -- precision is > 1/200 second
		s = math.floor(100 * s + 0.5) / 100
	else -- cap it at 3 dec places for now
		s = math.floor(1000 * s + 0.5) / 1000
	end
	return d, m, s
end


-------------------------------------------------------------------------------
-- decimalPrecision takes a decimal (x) with precision (p)
-- and returns x rounded approximately to the given precision
-- precision should be between 1 and 1e-6, preferably a power of 10.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local decimalPrecision = function(x, p)
	local s = 1
	if x < 0 then
		x = -x
		s = -1
	end
	-- if p is not supplied, pick an arbitrary precision
	if not tonumber(p) then p = 1e-4
	elseif p > 1 then p = 1
	elseif p < 1e-6 then p = 1e-6
	else p = 10 ^ math.floor(math.log10(p))
	end
	x = math.floor(x / p + 0.5) * p * s
	-- if it's integral, cast to an integer:
	if  x == math.floor(x) then x = math.floor(x) end
	-- if it's less than 1e-4, it will be in exponent form, so return a string with 6dp
	-- 9e-5 becomes 0.000090
	if math.abs(x) < 1e-4 then x = string.format("%f", x) end
	return x
end


-------------------------------------------------------------------------------
-- formatDate takes a datetime of the usual format from mw.wikibase.entity:formatPropertyValues
-- like "1 August 30 BCE" as parameter 1
-- and formats it according to the df (date format) and bc parameters
-- df = ["dmy" / "mdy" / "y"] default will be "dmy"
-- bc = ["BC" / "BCE"] default will be "BCE"
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local format_Date = function(datetime, dateformat, bc)
	local datetime = datetime or "1 August 30 BCE" -- in case of nil value
	-- chop off multiple vales and/or any hours, mins, etc.
	-- keep anything before punctuation - we just want a single date:
	local dateval = string.match( datetime, "[%w ]+")

	local dateformat = string.lower(dateformat or "dmy") -- default to dmy

	local bc = string.upper(bc or "") -- can't use nil for bc
	-- we only want to accept two possibilities: BC or default to BCE
	if bc == "BC" then
		bc = " " .. i18n["BC"] -- prepend a non-breaking space.
	else
		bc = " " .. i18n["BCE"]
	end

	local postchrist = true -- start by assuming no BCE
	local dateparts = {}
	for word in string.gmatch(dateval, "%w+") do
		if word == "BCE" or word == "BC" then -- *** internationalise later ***
			postchrist = false
		else
			-- we'll keep the parts that are not 'BCE' in a table
			dateparts[#dateparts + 1] = word
		end
	end
	if postchrist then bc = "" end -- set AD dates to no suffix *** internationalise later ***

	local sep = " " -- separator is nbsp
	local fdate = table.concat(dateparts, sep) -- set formatted date to same order as input

	-- if we have day month year, check dateformat
	if #dateparts == 3 then
		if dateformat == "y" then
			fdate = dateparts[3]
		elseif dateformat == "mdy" then
			fdate = dateparts[2] .. sep .. dateparts[1] .. "," .. sep .. dateparts[3]
		end
	elseif #dateparts == 2 and dateformat == "y" then
		fdate = dateparts[2]
	end

	return fdate .. bc
end


-------------------------------------------------------------------------------
-- dateFormat is the handler for properties that are of type "time"
-- It takes timestamp, precision (6 to 11 per mediawiki), dateformat (y/dmy/mdy), BC format (BC/BCE),
-- a plaindate switch (yes/no/adj) to en/disable "sourcing cirumstances"/use adjectival form,
-- any qualifiers for the property, the language, and any adjective to use like 'before'.
-- It passes the date through the "complex date" function
-- and returns a string with the internatonalised date formatted according to preferences.
-------------------------------------------------------------------------------
-- Dependencies: findLang(); cdate(); dp[]
-------------------------------------------------------------------------------
local dateFormat = function(timestamp, dprec, df, bcf, pd, qualifiers, lang, adj, model)
	-- A year can be stored like this: "+1872-00-00T00:00:00Z",
	-- which is processed here as if it were the day before "+1872-01-01T00:00:00Z",
	-- and that's the last day of 1871, so the year is wrong.
	-- So fix the month 0, day 0 timestamp to become 1 January instead:
	timestamp = timestamp:gsub("%-00%-00T", "-01-01T")
	-- output formatting according to preferences (y/dmy/mdy)
	df = (df or ""):lower()
	-- just in case date precision is missing
	dprec = dprec or 11
	-- override more precise dates if required dateformat is year alone:
	if df == "y" and dprec > 9 then dprec = 9 end
	-- complex date only deals with precisions from 6 to 11, so clip range
	dprec = dprec>11 and 11 or dprec
	dprec = dprec<6 and 6 or dprec
	-- BC format is "BC" or "BCE"
	bcf = (bcf or ""):upper()
	-- plaindate only needs the first letter (y/n/a)
	pd = (pd or ""):sub(1,1):lower()
	if pd == "" or pd == "n" or pd == "f" or pd == "0" then pd = false end
	-- in case language isn't passed
	lang = lang or findLang().code
	-- set adj as empty if nil
	adj = adj or ""
	-- extract the day, month, year from the timestamp
	local bc = timestamp:sub(1, 1)=="-" and "BC" or ""
	local year, month, day = timestamp:match("[+-](%d*)-(%d*)-(%d*)T")
	local iso = tonumber(year) -- if year is missing, let it throw an error
	-- this will adjust the date format to be compatible with cdate
	-- possible formats are Y, YY, YYY0, YYYY, YYYY-MM, YYYY-MM-DD
	if dprec == 6 then iso = math.floor( (iso - 1) / 1000 ) + 1 end
	if dprec == 7 then iso = math.floor( (iso - 1) / 100 ) + 1 end
	if dprec == 8 then iso = math.floor( iso / 10 ) .. "0" end
	if dprec == 10 then iso = year .. "-" .. month end
	if dprec == 11 then iso = year .. "-" .. month .. "-" .. day end
	-- add "circa" (Q5727902) from "sourcing circumstances" (P1480)
	local sc = not pd and qualifiers and qualifiers.P1480
	if sc then
		for k1, v1 in pairs(sc) do
			if v1.datavalue and v1.datavalue.value.id == "Q5727902" then
				adj = "circa"
				break
			end
		end
	end
	-- deal with Julian dates:
	-- no point in saying that dates before 1582 are Julian - they are by default
	-- doesn't make sense for dates less precise than year
	-- we can supress it by setting |plaindate, e.g. for use in constructing categories.
	local calendarmodel = ""
	if tonumber(year) > 1582
		and dprec > 8
		and not pd
		and model == "http://www.wikidata.org/entity/Q1985786" then
		calendarmodel = "julian"
	end
	if not cdate then
		cdate = require("Module:Complex date")._complex_date
	end
	local fdate = cdate(calendarmodel, adj, tostring(iso), dp[dprec], bc, "", "", "", "", lang, 1)
	-- this may have QuickStatements info appended to it in a div, so remove that
	fdate = fdate:gsub(' <div style="display: none;">[^<]*</div>', '')
	-- it may also be returned wrapped in a microformat, so remove that
	fdate = fdate:gsub("<[^>]*>", "")
	-- if 'circa', use the abbreviated form *** internationalise later ***
	fdate = fdate:gsub('circa ', '<abbr title="circa">c.</abbr> ')
	-- deal with BC/BCE
	if bcf == "BCE" then
		fdate = fdate:gsub('BC', 'BCE')
	end
	-- deal with mdy format
	if df == "mdy" then
		fdate = fdate:gsub("(%d+) (%w+) (%d+)", "%2 %1, %3")
	end
	-- deal with adjectival form *** internationalise later ***
	if pd == "a" then
		fdate = fdate:gsub(' century', '-century')
	end
	return fdate
end


-------------------------------------------------------------------------------
-- parseParam takes a (string) parameter, e.g. from the list of frame arguments,
-- and makes "false", "no", and "0" into the (boolean) false
-- it makes the empty string and nil into the (boolean) value passed as default
-- allowing the parameter to be true or false by default.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local parseParam = function(param, default)
	if param and param ~= "" then
		param = param:lower()
		if (param == "false") or (param:sub(1,1) == "n") or (param == "0") then
			return false
		else
			return true
		end
	else
		return default
	end
end


-------------------------------------------------------------------------------
-- _getSitelink takes the qid of a Wikidata entity passed as |qid=
-- It takes an optional parameter |wiki= to determine which wiki is to be checked for a sitelink
-- If the parameter is blank, then it uses the local wiki.
-- If there is a sitelink to an article available, it returns the plain text link to the article
-- If there is no sitelink, it returns nil.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local _getSitelink = function(qid, wiki)
	qid = (qid or ""):upper()
	if qid == "" then qid = mw.wikibase.getEntityIdForCurrentPage() end
	if not qid then return nil end
	wiki = wiki or ""
	local sitelink
	if wiki == "" then
		sitelink = mw.wikibase.sitelink(qid)
	else
		sitelink = mw.wikibase.sitelink(qid, wiki)
	end
	return sitelink
end


-------------------------------------------------------------------------------
-- _getCommonslink takes an optional qid of a Wikidata entity passed as |qid=
-- It returns one of the following in order of preference:
-- 	the Commons sitelink of the Wikidata entity - but not if onlycat=true and it's not a category;
-- 	the Commons sitelink of the topic's main category of the Wikidata entity;
-- 	the Commons category of the Wikidata entity - unless fallback=false.
-------------------------------------------------------------------------------
-- Dependencies: _getSitelink(); parseParam()
-------------------------------------------------------------------------------
local _getCommonslink = function(qid, onlycat, fallback)
	qid = (qid or ""):upper()
	if qid == "" then qid = mw.wikibase.getEntityIdForCurrentPage() end
	if not qid then return nil end
	onlycat = parseParam(onlycat, false)
	if fallback == "" then fallback = nil end
	local sitelink = _getSitelink(qid, "commonswiki")
	if onlycat and sitelink and sitelink:sub(1,9) ~= "Category:" then sitelink = nil end
	if not sitelink then
		-- check for topic's main category
		local prop910 = mw.wikibase.getBestStatements(qid, "P910")[1]
		if prop910 then
			local tmcid = prop910.mainsnak.datavalue.value.id
			sitelink = _getSitelink(tmcid, "commonswiki")
		end
	end
	if not sitelink and fallback then
		-- check for Commons category (string value)
		local prop373 = mw.wikibase.getBestStatements(qid, "P373")[1]
		if prop373 then
			sitelink = prop373.mainsnak.datavalue.value
			if sitelink then sitelink = "Category:" .. sitelink end
		end
	end
	return sitelink
end


-------------------------------------------------------------------------------
-- The label in a Wikidata item is subject to vulnerabilities
-- that an attacker might try to exploit.
-- It needs to be 'sanitised' by removing any wikitext before use.
-- If it doesn't exist, return the id for the item
-- a second (boolean) value is also returned, value is true when the label exists
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local labelOrId = function(id)
	local label = mw.wikibase.label(id)
	if label then
		return mw.text.nowiki(label), true
	else
		return id, false
	end
end


-------------------------------------------------------------------------------
-- linkedItem takes an entity-id and returns a string, linked if possible.
-- This is the handler for "wikibase-item". Preferences:
-- 1. Display linked disambiguated sitelink if it exists
-- 2. Display linked label if it is a redirect
-- 3. TBA: Display an inter-language link for the label if it exists other than in default language
-- 4. Display unlinked label if it exists
-- 5. Display entity-id for now to indicate a label could be provided
-- dtxt is text to be used instead of label, or nil.
-- shortname is boolean switch to use P1813 (short name) instead of label if true.
-- lang is the current language code.
-------------------------------------------------------------------------------
-- Dependencies: labelOrId(); donotlink[]
-------------------------------------------------------------------------------
local linkedItem = function(id, lprefix, lpostfix, prefix, postfix, dtxt, shortname, lang)
	lprefix = lprefix or "" -- toughen against nil values passed
	lpostfix = lpostfix or ""
	prefix = prefix or ""
	postfix = postfix or ""
	lang = lang or "en" -- fallback to default if missing
	local disp
	local sitelink = mw.wikibase.sitelink(id)
	local label, islabel
	if dtxt then
		label, islabel = dtxt, true
	elseif shortname then
		-- see if there is a shortname in our language, and set label to it
		for k, v in ipairs( mw.wikibase.getBestStatements(id, "P1813") ) do
			if v.mainsnak.datavalue.value.language == lang then
				label, islabel = v.mainsnak.datavalue.value.text, true
				break
			end -- test for language match
		end -- loop through values of short name
		-- if we have no label set, then there was no shortname available
		if not islabel then
			label, islabel = labelOrId(id)
			shortname = false
		end
	else
		label, islabel = labelOrId(id)
	end
	if mw.site.siteName ~= "Wikimedia Commons" then
		if sitelink then
			if not (dtxt or shortname) then
				-- strip any namespace or dab from the sitelink and use that as label
				local pos = sitelink:find(":") or 0
				label = sitelink:sub(pos+1):gsub("%s%(.+%)$", ""):gsub(",.+$", "")
			end
			if donotlink[label] then
				disp = prefix .. label .. postfix
			else
				disp = "[["_.._lprefix_.._sitelink_.._lpostfix_.._"|" .. prefix .. label .. postfix .. "]]"
			end
		elseif islabel then
			-- no sitelink, label exists, so check if a redirect with that title exists
			local artitle = mw.title.new(label, 0)
			if artitle and artitle.redirectTarget and not donotlink[label] then
				-- there's a redirect with the same title as the label, so let's link to that
				disp = "[[".._lprefix_.._label_.._lpostfix_.._"|" .. prefix .. label .. postfix .. "]]"
			else
				-- no sitelink, label exists, not redirect (or donotlink) so output plain label
				disp = prefix .. label .. postfix
			end -- test if article title exists as redirect on current Wiki
		else
			-- no sitelink and no label, so return whatever was returned from labelOrId for now
			-- add tracking category [[Category:Articles_with_missing_Wikidata_information|Category:Articles with missing Wikidata information]]
			disp = prefix .. label .. postfix .. i18n.missinginfocat
		end
	else
		local ccat = mw.wikibase.getBestStatements(id, "P373")[1]
		if ccat and ccat.mainsnak.datavalue then
			ccat = ccat.mainsnak.datavalue.value
			disp = "[["_.._lprefix_.._"Category:"_.._ccat_.._lpostfix_.._"|" .. prefix .. label .. postfix .. "]]"
		elseif sitelink then
			-- this asumes that if a sitelink exists, then a label also exists
			disp = "[["_.._lprefix_.._sitelink_.._lpostfix_.._"|" .. prefix .. label .. postfix .. "]]"
		else
			-- no sitelink and no Commons cat, so return label from labelOrId for now
			disp = prefix .. label .. postfix
		end
	end
	return disp
end


-------------------------------------------------------------------------------
-- sourced takes a table representing a statement that may or may not have references
-- it counts how many references are sourced to something not containing the word "wikipedia"
-- it returns a boolean = true if there are any sourced references.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local sourced = function(claim)
	if claim.references then
		for kr, vr in pairs(claim.references) do
			local ref = mw.wikibase.renderSnaks(vr.snaks)
			if not ref:find("Wikipedia") then
				return true
			end
		end
	end
end


-------------------------------------------------------------------------------
-- setRanks takes a flag (parameter passed) that requests the values to return
-- "b[est]" returns preferred if available, otherwise normal
-- "p[referred]" returns preferred
-- "n[ormal]" returns normal
-- "d[eprecated]" returns deprecated
-- multiple values are allowed, e.g. "preferred normal" (which is the default)
-- "best" will override the other flags, and set p and n
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local setRanks = function(rank)
	rank = (rank or ""):lower()
	-- if nothing passed, return preferred and normal
	-- if rank == "" then rank = "p n" end
	local ranks = {}
	for w in string.gmatch(rank, "%a+") do
		w = w:sub(1,1)
		if w == "b" or w == "p" or w == "n" or w == "d" then
			ranks[w] = true
		end
	end
	-- check if "best" is requested or no ranks requested; and if so, set preferred and normal
	if ranks.b or not next(ranks) then
		ranks.p = true
		ranks.n = true
	end
	return ranks
end


-------------------------------------------------------------------------------
-- parseInput processes the Q-id , the blacklist and the whitelist
-- if an input parameter is supplied, it returns that and ends the call.
-- it returns (1) either the qid or nil indicating whether or not the call should continue
-- and (2) a table containing all of the statements for the propertyID and relevant Qid
-- if "best" ranks are requested, it returns those instead of all non-deprecated ranks
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
local parseInput = function(frame, input_parm, property_id)
	-- There may be a local parameter supplied, if it's blank, set it to nil
	input_parm = mw.text.trim(input_parm or "")
	if input_parm == "" then input_parm = nil end

	local args = frame.args

	-- can take a named parameter |qid which is the Wikidata ID for the article.
	-- if it's not supplied, use the id for the current page
	local qid = args.qid or ""
	if qid == "" then qid = mw.wikibase.getEntityIdForCurrentPage() end
	-- if there's no Wikidata item for the current page return nil
	if not qid then return false, input_parm end

	-- The blacklist is passed in named parameter |suppressfields
	local blacklist = args.suppressfields or args.spf

	-- The whitelist is passed in named parameter |fetchwikidata
	local whitelist = args.fetchwikidata or args.fwd
	if not whitelist or whitelist == "" then whitelist = "NONE" end

	-- The name of the field that this function is called from is passed in named parameter |name
	local fieldname = args.name or ""

	if blacklist then
		-- The name is compulsory when blacklist is used, so return nil if it is not supplied
		if not fieldname or fieldname == "" then return false, nil end
		-- If this field is on the blacklist, then return nil
		if blacklist:find(fieldname) then return false, nil end
	end

	-- If we got this far then we're not on the blacklist
	-- The blacklist overrides any locally supplied parameter as well
	-- If a non-blank input parameter was supplied return it
	if input_parm then return false, input_parm end

	-- We can filter out non-valid properties
	if property_id:sub(1,1):upper() ~="P" or property_id == "P0" then return false, nil end

	-- Otherwise see if this field is on the whitelist:
	-- needs a bit more logic because find will return its second value = 0 if fieldname is ""
	-- but nil if fieldname not found on whitelist
	local _, found = whitelist:find(fieldname)
	found = ((found or 0) > 0)
	if whitelist ~= 'ALL' and (whitelist:upper() == "NONE" or not found) then
		return false, nil
	end

	-- See what's on Wikidata (the call always returns a table, but it may be empty):
	local props = {}
	if args.reqranks.b then
		props = mw.wikibase.getBestStatements(qid, property_id)
	else
		props = mw.wikibase.getAllStatements(qid, property_id)
	end
	if props[1] then
		return qid, props
	end
	-- no property on Wikidata
	return false, nil
end


-------------------------------------------------------------------------------
-- createicon assembles the "Edit at Wikidata" pen icon.
-- It returns a wikitext string.
-------------------------------------------------------------------------------
-- Dependencies: i18n[];
-------------------------------------------------------------------------------
local createicon = function(langcode, entityID, propertyID)
	local icon = " [[" .. i18n["filespace"]
	icon = icon .. ":Blue pencil.svg |frameless |text-top |10px |alt="
	icon = icon .. i18n["editonwikidata"]
	icon = icon .. "|link=https://www.wikidata.org/wiki/" .. entityID
	icon = icon .. "?uselang=" .. langcode
	if propertyID then icon = icon .. "#" .. propertyID end
	icon = icon .. "|" .. i18n["editonwikidata"] .. "]]"
	return icon
end


-------------------------------------------------------------------------------
-- assembleoutput takes the sequence table containing the property values
-- and formats it according to switches given. It returns a string or nil.
-- It needs the entityID and propertyID to create a link in the pen icon.
-------------------------------------------------------------------------------
-- Dependencies: parseParam();
-------------------------------------------------------------------------------
local assembleoutput = function(out, args, entityID, propertyID)

	-- sorted is a boolean passed to enable sorting of the values returned
	-- if nothing or an empty string is passed set it false
	-- if "false" or "no" or "0" is passed set it false
	local sorted = parseParam(args.sorted, false)

	-- noicon is a boolean passed to suppress the trailing "edit at Wikidata" icon
	-- for use when the value is processed further by the infobox
	-- if nothing or an empty string is passed set it false
	-- if "false" or "no" or "0" is passed set it false
	local noic = parseParam(args.noicon, false)

	-- list is the name of a template that a list of multiple values is passed through
	-- examples include "hlist" and "ubl"
	-- setting it to "prose" produces something like "1, 2, 3, and 4"
	local list = args.list or ""

	-- sep is a string that is used to separate multiple returned values
	-- if nothing or an empty string is passed set it to the default
	-- any double-quotes " are stripped out, so that spaces may be passed
	-- e.g. |sep=" - "
	local sepdefault = i18n["list separator"]
	local separator = args.sep or ""
	separator = string.gsub(separator, '"', '')
	if separator == "" then
		separator = sepdefault
	end

	-- collapse is a number that determines the maximum number of returned values
	-- before the output is collapsed.
	-- Zero or not a number result in no collapsing (default becomes 0).
	local collapse = tonumber(args.collapse) or 0

	-- if there's anything to return, then return a list
	-- comma-separated by default, but may be specified by the sep parameter
	-- optionally specify a hlist or ubl or a prose list, etc.
	local strout
	if #out > 0 then
		if sorted then table.sort(out) end
		-- if a pen icon is wanted add it the end of the last value
		if not noic then
			out[#out] = out[#out] .. createicon(args.langobj.code, entityID, propertyID)
		end
		if list == "" then
			strout = table.concat(out, separator)
		elseif list:lower() == "prose" then
			strout = mw.text.listToText( out )
		else
			strout = mw.getCurrentFrame():expandTemplate{title = list, args = out}
		end
		if collapse >0 and #out > collapse then
			strout = collapsediv .. strout .. "</div>"
		end
	else
		strout = nil -- no items had valid reference
	end
	return strout
end


-------------------------------------------------------------------------------
-- rendersnak takes a table (propval) containing the information stored on one property value
-- and returns the value as a string and its language if monolingual text.
-- It handles data of type:
--		wikibase-item
--		time
--		string, url, commonsMedia, external-id
--		quantity
--		globe-coordinate
--		monolingualtext
-- It also requires linked, the link/pre/postfixes, uabbr, and the arguments passed from frame.
-- The optional filter parameter allows quantities to be be filtered by unit Qid.
-------------------------------------------------------------------------------
-- Dependencies: parseParam(); labelOrId(); i18n[]; dateFormat();
-- roundto(); decimalPrecision(); decimalToDMS(); linkedItem();
-------------------------------------------------------------------------------
local rendersnak = function(propval, args, linked, lpre, lpost, pre, post, uabbr, filter)
	lpre = lpre or ""
	lpost = lpost or ""
	pre = pre or ""
	post = post or ""
	args.lang = args.lang or findLang().code
	-- allow values to display a fixed text instead of label
	local dtxt = args.displaytext or args.dt
	if dtxt == "" then dtxt = nil end
	-- switch to use display of short name (P1813) instead of label
	local shortname = args.shortname or args.sn
	shortname = parseParam(shortname, false)
	local snak = propval.mainsnak or propval
	local dtype = snak.datatype
	local dv = snak.datavalue
	dv = dv and dv.value
	-- value and monolingual text language code returned
	local val, mlt
	if propval.rank and not args.reqranks[propval.rank:sub(1, 1)] then
		-- val is nil: value has a rank that isn't requested
		------------------------------------
	elseif snak.snaktype == "somevalue" then -- value is unknown
		val = i18n["Unknown"]
		------------------------------------
	elseif snak.snaktype == "novalue" then -- value is none
		-- val = "No value" -- don't return anything
		------------------------------------
	elseif dtype == "wikibase-item" then -- data type is a wikibase item:
		-- it's wiki-linked value, so output as link if enabled and possible
		local qnumber = dv.id
		if linked then
			val = linkedItem(qnumber, lpre, lpost, pre, post, dtxt, shortname, args.lang)
		else -- no link wanted so check for display-text, otherwise test for lang code
			local label, islabel
			if dtxt then
				label = dtxt
			else
				label, islabel = labelOrId(qnumber)
				local langlabel = mw.wikibase.getLabelByLang(qnumber, args.lang)
				if langlabel then
					label = mw.text.nowiki( langlabel )
				end
			end
			val = pre .. label .. post
		end -- test for link required
		------------------------------------
	elseif dtype == "time" then -- data type is time:
		-- time is in timestamp format
		-- date precision is integer per mediawiki
		-- output formatting according to preferences (y/dmy/mdy)
		-- BC format as BC or BCE
		-- plaindate is passed to disable looking for "sourcing cirumstances"
		-- or to set the adjectival form
		-- qualifiers (if any) is a nested table or nil
		-- lang is given, or user language, or site language
		val = dateFormat(dv.time, dv.precision, args.df, args.bc, args.pd, propval.qualifiers, args.lang, "", dv.calendarmodel)
		------------------------------------
	-- data types which are strings:
	elseif dtype == "commonsMedia" or dtype == "external-id" or dtype == "string" or dtype == "url" then
		-- commonsMedia or external-id or string or url
		-- all have mainsnak.datavalue.value as string
		if (lpre == "" or lpre == ":") and lpost == "" then
			-- don't link if no linkpre/postfix or linkprefix is just ":"
			val = pre .. dv .. post
		else
			val = "[["_.._lpre_.._dv_.._lpost_.._"|" .. pre .. dv .. post .. "]]"
		end -- check for link requested (i.e. either linkprefix or linkpostfix exists)
		------------------------------------
	-- data types which are quantities:
	elseif dtype == "quantity" then
		-- quantities have mainsnak.datavalue.value.amount and mainsnak.datavalue.value.unit
		-- the unit is of the form http://www.wikidata.org/entity/Q829073
		--
		-- implement a switch to turn on/off numerical formatting later
		local fnum = true
		--
		-- a switch to turn on/off conversions - only for en-wiki
		local conv = parseParam(args.conv or args.convert, false)
		-- if we have conversions, we won't have formatted numbers or scales
		if conv then
			fnum = false
			args.scale = "0"
		end
		--
		-- a switch to turn on/off showing units, default is true
		local showunits = parseParam(args.su or args.showunits, true)
		--
		-- convert amount to a number
		local amount = tonumber(dv.amount) or i18n["NaN"]
		--
		-- scale factor for millions, billions, etc.
		local sc = tostring(args.scale or ""):sub(1,1):lower()
		local scale
		if sc == "a" then
			-- automatic scaling
			if amount > 1e15 then
				scale = 12
			elseif amount > 1e12 then
				scale = 9
			elseif amount > 1e9 then
				scale = 6
			elseif amount > 1e6 then
				scale = 3
			else
				scale = 0
			end
		else
			scale = tonumber(args.scale) or 0
			if scale < 0 or scale > 12 then scale = 0 end
			scale = math.floor(scale/3) * 3
		end
		local factor = 10^scale
		amount = amount / factor
		-- ranges:
		local range = ""
		-- check if upper and/or lower bounds are given and significant
		local upb = tonumber(dv.upperBound)
		local lowb = tonumber(dv.lowerBound)
		if upb and lowb then
			-- differences rounded to 2 sig fig:
			local posdif = roundto(upb - amount, 2) / factor
			local negdif = roundto(amount - lowb, 2) / factor
			upb, lowb = amount + posdif, amount - negdif
			-- round scaled numbers to integers or 4 sig fig
			if (scale > 0 or sc == "a") then
				if amount < 1e4 then
					amount = roundto(amount, 4)
				else
					amount = math.floor(amount + 0.5)
				end
			end
			if fnum then amount = args.langobj:formatNum( amount ) end
			if posdif ~= negdif then
				-- non-symmetrical
				range = " +" .. posdif .. " -" .. negdif
			elseif posdif ~= 0 then
				-- symmetrical and non-zero
				range = " ±" .. posdif
			else
				-- otherwise range is zero, so leave it as ""
			end
		else
			-- round scaled numbers to integers or 4 sig fig
			if (scale > 0 or sc == "a") then
				if amount < 1e4 then
					amount = roundto(amount, 4)
				else
					amount = math.floor(amount + 0.5)
				end
			end
			if fnum then amount = args.langobj:formatNum( amount ) end
		end
		-- unit names and symbols:
		-- extract the qid in the form 'Qnnn' from the value.unit url
		-- and then fetch the label from that - or symbol if unitabbr is true
		local unit = ""
		local usep = ""
		local usym = ""
		local unitqid = string.match( dv.unit, "(Q%d+)" )
		if filter and unitqid ~= filter then return nil end
		if unitqid and showunits then
			local uname = mw.wikibase.getLabelByLang(unitqid, args.lang) or ""
			if uname ~= "" then usep, unit = " ", uname end
			if uabbr then
				-- see if there's a unit symbol (P5061)
				local unitsymbols = mw.wikibase.getAllStatements(unitqid, "P5061")
				-- construct fallback table
				local fbtbl = mw.language.getFallbacksFor( args.lang )
				table.insert( fbtbl, 1, args.lang )
				local found = false
				for idx1, us in ipairs(unitsymbols) do
					for idx2, fblang in ipairs(fbtbl) do
						if us.mainsnak.datavalue.value.language == fblang then
							usym = us.mainsnak.datavalue.value.text
							found = true
							break
						end
					if found then break end
					end -- loop through fallback table
				end -- loop through values of P5061
				if found then usep, unit = " ", usym end
			end
		end
		-- format display:
		if conv and usym ~= "" then
			if range == "" then
				val = mw.getCurrentFrame():expandTemplate{title = "cvt", args = {amount, usym}}
			else
				val = mw.getCurrentFrame():expandTemplate{title = "cvt", args = {lowb, "to", upb, usym}}
			end
		elseif unit == "$" or unit == "£" then
			val = unit .. amount .. range .. i18n.multipliers[scale]
		else
			val = amount .. range .. i18n.multipliers[scale] .. usep .. unit
		end
		------------------------------------
	-- datatypes which are global coordinates:
	elseif dtype == "globe-coordinate" then
		-- 'display' parameter defaults to "inline, title" *** unused for now ***
		-- local disp = args.display or ""
		-- if disp == "" then disp = "inline, title" end
		--
		-- format parameter switches from deg/min/sec to decimal degrees
		-- default is deg/min/sec -- decimal degrees needs |format = dec
		local form = (args.format or ""):lower():sub(1,3)
		if form ~= "dec" then form = "dms" end
		--
		-- show parameter allows just the latitude or longitude to be shown
		local show = (args.show or ""):lower()
		if show ~= "longlat" then show = show:sub(1,3) end
		--
		local lat, long, prec = dv.latitude, dv.longitude, dv.precision
		if show == "lat" then
			val = decimalPrecision(lat, prec)
		elseif show == "lon" then
			val = decimalPrecision(long, prec)
		elseif show == "longlat" then
			val = decimalPrecision(long, prec) .. ", " .. decimalPrecision(lat, prec)
		else
			local ns = "N"
			local ew = "E"
			if lat < 0 then
				ns = "S"
				lat = - lat
			end
			if long < 0 then
				ew = "W"
				long = - long
			end
			if form == "dec" then
				lat = decimalPrecision(lat, prec)
				long = decimalPrecision(long, prec)
				val = lat .. "°" .. ns .. " " .. long ..  "°" .. ew
			else
				local latdeg, latmin, latsec = decimalToDMS(lat, prec)
				local longdeg, longmin, longsec = decimalToDMS(long, prec)

				if latsec == 0 and longsec == 0 then
					if latmin == 0 and longmin == 0 then
						val = latdeg .. "°" .. ns .. " " .. longdeg ..  "°" .. ew
					else
						val = latdeg .. "°" .. latmin .. "′" .. ns .. " "
						val = val .. longdeg .. "°".. longmin .. "′" .. ew
					end
				else
					val = latdeg .. "°" .. latmin .. "′" .. latsec .. "″" .. ns .. " "
					val = val .. longdeg .. "°" .. longmin .. "′" .. longsec .. "″" .. ew
				end
			end
		end
		------------------------------------
	elseif dtype == "monolingualtext" then -- data type is Monolingual text:
		-- has mainsnak.datavalue.value as a table containing language/text pairs
		-- collect all the values in 'out' and languages in 'mlt' and process them later
		val = pre .. dv.text .. post
		mlt = dv.language
		------------------------------------
	else
		-- some other data type so write a specific handler
		val = "unknown data type: " .. dtype
	end -- of datatype/unknown value/sourced check
	return val, mlt
end


-------------------------------------------------------------------------------
-- propertyvalueandquals takes a property object, the arguments passed from frame,
-- and a qualifier propertyID.
-- It returns a sequence (table) of values representing the values of that property
-- and qualifiers that match the qualifierID if supplied.
-------------------------------------------------------------------------------
-- Dependencies: parseParam(); sourced(); labelOrId(); i18n.latestdatequalifier(); format_Date();
-- makeOrdinal(); roundto(); decimalPrecision(); decimalToDMS(); assembleoutput();
-------------------------------------------------------------------------------
local function propertyvalueandquals(objproperty, args, qualID)
	-- needs this style of declaration because it's re-entrant

	-- onlysourced is a boolean passed to return only values sourced to other than Wikipedia
	-- if nothing or an empty string is passed set it true
	local onlysrc = parseParam(args.onlysourced or args.osd, true)

	-- linked is a a boolean that enables the link to a local page via sitelink
	-- if nothing or an empty string is passed set it true
	local linked = parseParam(args.linked, true)

	-- prefix is a string that may be nil, empty (""), or a string of characters
	-- this is prefixed to each value
	-- useful when when multiple values are returned
	-- any double-quotes " are stripped out, so that spaces may be passed
	local prefix = (args.prefix or ""):gsub('"', '')

	-- postfix is a string that may be nil, empty (""), or a string of characters
	-- this is postfixed to each value
	-- useful when when multiple values are returned
	-- any double-quotes " are stripped out, so that spaces may be passed
	local postfix = (args.postfix or ""):gsub('"', '')

	-- linkprefix is a string that may be nil, empty (""), or a string of characters
	-- this creates a link and is then prefixed to each value
	-- useful when when multiple values are returned and indirect links are needed
	-- any double-quotes " are stripped out, so that spaces may be passed
	local lprefix = (args.linkprefix or args.lp or ""):gsub('"', '')

	-- linkpostfix is a string that may be nil, empty (""), or a string of characters
	-- this is postfixed to each value when linking is enabled with lprefix
	-- useful when when multiple values are returned
	-- any double-quotes " are stripped out, so that spaces may be passed
	local lpostfix = (args.linkpostfix or ""):gsub('"', '')

	-- wdlinks is a boolean passed to enable links to Wikidata when no article exists
	-- if nothing or an empty string is passed set it false
	local wdl = parseParam(args.wdlinks or args.wdl, false)

	-- unitabbr is a boolean passed to enable unit abbreviations for common units
	-- if nothing or an empty string is passed set it false
	local uabbr = parseParam(args.unitabbr or args.uabbr, false)

	-- qualsonly is a boolean passed to return just the qualifiers
	-- if nothing or an empty string is passed set it false
	local qualsonly = parseParam(args.qualsonly or args.qo, false)

	-- maxvals is a string that may be nil, empty (""), or a number
	-- this determines how many items may be returned when multiple values are available
	-- setting it = 1 is useful where the returned string is used within another call, e.g. image
	local maxvals = tonumber(args.maxvals) or 0

	-- pd (plain date) is a string: yes/true/1 | no/false/0 | adj
	-- to disable/enable "sourcing cirumstances" or use adjectival form for the plain date
	local pd = args.plaindate or args.pd or "no"
	args.pd = pd

	local lang = args.lang or findlang().code
	-- all proper values of a Wikidata property will be the same type as the first
	-- qualifiers don't have a mainsnak, properties do
	local datatype = objproperty[1].datatype or objproperty[1].mainsnak.datatype
	-- out[] holds the values for this property
	-- mlt[] holds the language code if the datatype is monolingual text
	local out = {}
	local mlt = {}
	for k, v in ipairs(objproperty) do
		local hasvalue = true
		if (onlysrc and not sourced(v)) then
			-- no value: it isn't sourced when onlysourced=true
			hasvalue = false
		else
			local val, lcode = rendersnak(v, args, linked, lprefix, lpostfix, prefix, postfix, uabbr)
			if not val then
				hasvalue = false -- rank doesn't match
			elseif qualsonly and qualID then
				-- suppress value returned: only qualifiers are requested
			else
				out[#out+1], mlt[#out+1] = val, lcode
			end
		end

		-- See if qualifiers are to be returned:
		local snak = v.mainsnak or v
		if hasvalue and v.qualifiers and qualID and snak.snaktype=="value" then
			local qsep = (args.qsep or ""):gsub('"', '')
			local qargs = {
				["osd"]         = "false",
				["linked"]      = tostring(linked),
				["prefix"]      = args.qprefix,
				["postfix"]     = args.qpostfix,
				["linkprefix"]  = args.qlinkprefix or args.qlp,
				["linkpostfix"] = args.qlinkpostfix,
				["wdl"]         = "false",
				["unitabbr"]    = tostring(uabbr),
				["maxvals"]     = 0,
				["sorted"]      = args.qsorted,
				["noicon"]      = "true",
				["list"]        = args.qlist,
				["sep"]         = qsep,
				["langobj"]     = args.langobj,
				["lang"]        = args.langobj.code,
			}
			local qlist = {}
			local t1, t2 = "", ""
			-- see if we want all qualifiers
			if qualID == "ALL" then
				if v["qualifiers-order"] then
					-- the values in the order table are the keys for the qualifiers table:
					for k1, v1 in ipairs(v["qualifiers-order"]) do
						if v1 == "P1326" then
							local ts = v.qualifiers[v1][1].datavalue.value.time
							local dp = v.qualifiers[v1][1].datavalue.value.precision
							qlist[#qlist + 1] = dateFormat(ts, dp, args.df, args.bc, pd, "", lang, "before")
						elseif v1 == "P1319" then
							local ts = v.qualifiers[v1][1].datavalue.value.time
							local dp = v.qualifiers[v1][1].datavalue.value.precision
							qlist[#qlist + 1] = dateFormat(ts, dp, args.df, args.bc, pd, "", lang, "after")
						else
							local q = assembleoutput(propertyvalueandquals(v.qualifiers[v1], qargs), qargs)
							-- we already deal with circa via 'sourcing circumstances'
							-- either linked or unlinked *** internationalise later ***
							if q ~= "circa" and not q:find("circa]]") then
								qlist[#qlist + 1] = q
							end
						end
					end
				else
					-- are there cases where qualifiers-order doesn't exist?
					local ql = propertyvalueandquals(v.qualifiers, qargs)
					for k1, v1 in ipairs(ql) do
						-- we already deal with circa via 'sourcing circumstances'
						-- either linked or unlinked *** internationalise later ***
						if v1 ~= "circa" and not v1:find("circa]]") then
							qlist[#qlist + 1] = v1
						end
					end
				end
			-- see if we want date/range
			elseif qualID == "DATES" then
				qargs.maxvals = 1
				for k1, v1 in pairs(v.qualifiers) do
					if k1 == "P580" then -- P580 is "start time"
						t1 = propertyvalueandquals(v1, qargs)[1] or ""
					elseif k1 == "P582" then -- P582 is "end time"
						t2 = propertyvalueandquals(v1, qargs)[1] or ""
					end
				end
			-- otherwise process qualID as a list of qualifiers
			else
				for q in mw.text.gsplit(qualID, "%p") do -- split at punctuation and iterate
					q = mw.text.trim(q):upper() -- remove whitespace and capitalise
					if q == "P1326" then
						-- latest date, so supply 'before' as well. Assume one date value.
						for k1, v1 in pairs(v.qualifiers) do
							if k1 == "P1326" then
								local ts = v1[1].datavalue.value.time
								local dp = v1[1].datavalue.value.precision
								qlist[#qlist + 1] = dateFormat(ts, dp, args.df, args.bc, pd, "", lang, "before")
							end
						end
					else
						for k1, v1 in pairs(v.qualifiers) do
							if k1 == q then
								local ql = propertyvalueandquals(v1, qargs)
								for k2, v2 in ipairs(ql) do
									qlist[#qlist + 1] = v2
								end
							end
						end
					end
				end -- of loop through list of qualifiers in qualID
			end -- of testing for what qualID is
			local t = t1 .. t2
			-- *** internationalise date separators later ***
			local dsep = "–"
			if t:find("%s") or t:find(" ") then dsep = " – " end
			if #qlist > 0 then
				local qstr = assembleoutput(qlist, qargs)
				if qualsonly then
					out[#out+1] = qstr
				else
					out[#out] = out[#out] .. " (" .. qstr .. ")"
				end
			elseif t > "" then
				if qualsonly then
					out[#out+1] = t1 .. dsep .. t2
				else
					out[#out] = out[#out] .. " (" .. t1 .. dsep .. t2 .. ")"
				end
			end
		end -- of test for qualifiers wanted

		if maxvals > 0 and #out >= maxvals then break end
	end -- of for each value loop

	-- we need to pick one value to return if the datatype was "monolingualtext"
	-- if there's only one value, use that
	-- otherwise look through the fallback languages for a match
	if datatype == "monolingualtext" and #out >1 then
		lang = mw.text.split( lang, '-', true )[1]
		local fbtbl = mw.language.getFallbacksFor( lang )
		table.insert( fbtbl, 1, lang )
		local bestval = ""
		local found = false
		for idx1, lang1 in ipairs(fbtbl) do
			for idx2, lang2 in ipairs(mlt) do
				if (lang1 == lang2) and not found then
					bestval = out[idx2]
					found = true
					break
				end
			end -- loop through values of property
		end -- loop through fallback languages
		if found then
			-- replace output table with a table containing the best value
			out = { bestval }
		else
			-- more than one value and none of them on the list of fallback languages
			-- sod it, just give them the first one
			out = { out[1] }
		end
	end
	return out
end


-------------------------------------------------------------------------------
-- Common code for p.getValueByQual and p.getValueByLang
-------------------------------------------------------------------------------
-- Dependencies: parseParam; setRanks; parseInput; sourced; assembleoutput;
-------------------------------------------------------------------------------
local _getvaluebyqual = function(frame, qualID, checkvalue)

	-- The property ID that will have a qualifier is the first unnamed parameter
	local propertyID = mw.text.trim(frame.args[1] or "")
	if propertyID == "" then return "no property supplied" end

	if qualID == "" then return "no qualifier supplied" end

	-- onlysourced is a boolean passed to return property values
	-- only when property values are sourced to something other than Wikipedia
	-- if nothing or an empty string is passed set it true
	-- if "false" or "no" or 0 is passed set it false
	local onlysrc = parseParam(frame.args.onlysourced or frame.args.osd, true)

	-- set the requested ranks flags
	frame.args.reqranks = setRanks(frame.args.rank)

	-- set a language object and code in the frame.args table
	frame.args.langobj = findLang(frame.args.lang)
	frame.args.lang = frame.args.langobj.code

	local args = frame.args

	-- check for locally supplied parameter in second unnamed parameter
	-- success means no local parameter and the property exists
	local qid, props = parseInput(frame, args[2], propertyID)

	local linked = parseParam(args.linked, true)
	local lpre = (args.linkprefix or args.lp or ""):gsub('"', '')
	local lpost = (args.linkpostfix or ""):gsub('"', '')
	local pre = (args.prefix or ""):gsub('"', '')
	local post = (args.postfix or ""):gsub('"', '')
	local uabbr = parseParam(args.unitabbr or args.uabbr, false)
	local filter = (args.unit or ""):upper()
	if filter == "" then filter = nil end

	if qid then
		local out = {}
		-- Scan through the values of the property
		-- we want something like property is "pronunciation audio (P443)" in propertyID
		-- with a qualifier like "language of work or name (P407)" in qualID
		-- whose value has the required ID, like "British English (Q7979)", in qval
		for k1, v1 in ipairs(props) do
			if v1.mainsnak.snaktype == "value" then
				-- check if it has the right qualifier
				local v1q = v1.qualifiers
				if v1q and v1q[qualID] then
					if onlysrc == false or sourced(v1) then
						-- if we've got this far, we have a (sourced) claim with qualifiers
						-- so see if matches the required value
						-- We'll only deal with wikibase-items for now
						if v1q[qualID][1].datatype == "wikibase-item" then
							if checkvalue(v1q[qualID][1].datavalue.value.id) then
								out[#out + 1] = rendersnak(v1, args, linked, lpre, lpost, pre, post, uabbr, filter)
							end
						end
					end -- of check for sourced
				end -- of check for matching required value and has qualifiers
			else
				return nil
			end -- of check for string
		end -- of loop through values of propertyID
		return assembleoutput(out, frame.args, qid, propertyID)
	else
		return props -- either local parameter or nothing
	end -- of test for success
	return nil
end


-------------------------------------------------------------------------------
-- _location takes Q-id and follows P276 (location)
-- or P131 (located in the administrative territorial entity) or P706 (located on terrain feature)
-- from the initial item to higher level territories/locations until it reaches the highest.
-- An optional boolean, 'first', determines whether the first item is returned (default: false).
-- An optional boolean 'skip' toggles the display to skip to the last item (default: false).
-- It returns a table containing the locations - linked where possible, except for the highest.
-------------------------------------------------------------------------------
-- Dependencies: findLang(); labelOrId(); linkedItem
-------------------------------------------------------------------------------
local _location = function(qid, first, skip)
	first = parseParam(first, false)
	skip = parseParam(skip, false)
	local locs = {"P276", "P131", "P706"}
	local out = {}
	local langcode = findLang():getCode()
	local finished = false
	local count = 0
	local prevqid = ""
	repeat
		local prop
		for i1, v1 in ipairs(locs) do
			local proptbl = mw.wikibase.getBestStatements(qid, v1)
			if #proptbl > 1 then
				-- there is more than one parent location
				for i2, v2 in ipairs(proptbl) do
					parttbl = v2.qualifiers and v2.qualifiers.P518
					if parttbl then
						-- this parent location has qualifier 'applies to part' (P518)
						for i3, v3 in ipairs(parttbl) do
							if v3.snaktype == "value" and v3.datavalue.value.id == prevqid then
								-- it has a value equal to the previous location
								prop = proptbl[i2]
								break
							end -- of test for matching last location
						end -- of loop through values of 'applies to part'
					end
				end -- of loop through parent locations
				-- fallback to second value if match not found
				prop = prop or proptbl[2]
			elseif #proptbl > 0 then
				prop = proptbl[1]
			end
			if prop then break end
		end

		-- check if it's an instance of (P31) a country (Q6256) and terminate the chain if it is
		local inst = mw.wikibase.getAllStatements(qid, "P31")
		if #inst > 0 then
			for k, v in ipairs(inst) do
				local instid = v.mainsnak.datavalue.value.id
				-- stop if it's a country (or a country within the United Kingdom if skip is true)
				if instid == "Q6256" or (skip and instid == "Q3336843") then
					prop = nil -- this will ensure this is treated as top-level location
					break
				end
			end
		end

		-- get the name of this location and update qid to point to the parent location
		if prop and prop.mainsnak.datavalue then
			if not skip or count == 0 then
				out[#out+1] = linkedItem(qid, ":", "", "", "") -- get a linked value if we can
			end
			qid, prevqid = prop.mainsnak.datavalue.value.id, qid
		else
			-- This is top-level location, so get short name except when this is the first item
			-- Use full label if there's no short name or this is the first item
			local prop1813 = mw.wikibase.getAllStatements(qid, "P1813")
			-- if there's a short name and this isn't the only item
			if prop1813[1] and (#out > 0)then
				local shortname
				-- short name is monolingual text, so look for match to the local language
				-- choose the shortest 'short name' in that language
				for k, v in pairs(prop1813) do
					if v.mainsnak.datavalue.value.language == langcode then
						local name = v.mainsnak.datavalue.value.text
						if (not shortname) or (#name < #shortname) then
							shortname = name
						end
					end
				end
				-- add the shortname if one is found, fallback to the label
				-- but skip it if it's "USA"
				if shortname ~= "USA" then
					out[#out+1] = shortname or labelOrId(qid)
				else
					if skip then out[#out+1] = "US" end
				end
			else
				-- no shortname, so just add the label
				local loc = labelOrId(qid)
				-- exceptions go here:
				if loc == "United States of America" then
					out[#out+1] = "United States"
				else
					out[#out+1] = loc
				end
			end
			finished = true
		end
		count = count + 1
	until finished or count >= 10 -- limit to 10 levels to avoid infinite loops

	-- remove the first location if not quired
	if not first then table.remove(out, 1) end

	-- we might have duplicate text for consecutive locations, so remove them
	if #out > 2 then
		local plain = {}
		for i, v in ipairs(out) do
			-- strip any links
			plain[i] = v:gsub("^%[%[[^|]*]]$", "")
		end
		local idx = 2
		repeat
			if plain[idx] == plain[idx-1] then
				-- duplicate found
				local removeidx = 0
				if (plain[idx] ~= out[idx]) and (plain[idx-1] == out[idx-1]) then
					-- only second one is linked, so drop the first
					removeidx = idx - 1
				elseif (plain[idx] == out[idx]) and (plain[idx-1] ~= out[idx-1]) then
					-- only first one is linked, so drop the second
					removeidx = idx
				else
					-- pick one
					removeidx = idx - (os.time()%2)
				end
				table.remove(out, removeidx)
				table.remove(plain, removeidx)
			else
				idx = idx +1
			end
		until idx >= #out
	end
	return out
end


-------------------------------------------------------------------------------
-- _getsumofparts scans the property 'has part' (P527) for values matching a list.
-- The list (args.vlist) consists of a string of Qids separated by spaces or any usual punctuation.
-- If the matched values have a qualifer 'quantity' (P1114), those quantites are summed.
-- The sum is returned as a number (i.e. 0 if none)
-- a table of arguments is supplied implementing the usual parameters.
-------------------------------------------------------------------------------
-- Dependencies: setRanks; parseParam; parseInput; sourced; assembleoutput;
-------------------------------------------------------------------------------
local _getsumofparts = function(args)
	local vallist = (args.vlist or ""):upper()
	if vallist == "" then return end
	args.reqranks = setRanks(args.rank)
	local f = {}
	f.args = args
	local qid, props = parseInput(f, "", "P527")
	if not qid then return 0 end
	local onlysrc = parseParam(args.onlysourced or args.osd, true)
	local sum = 0
	for k1, v1 in ipairs(props) do
		if (onlysrc == false or sourced(v1))
			and v1.mainsnak.snaktype == "value"
			and v1.mainsnak.datavalue.type == "wikibase-entityid"
			and vallist:match( v1.mainsnak.datavalue.value.id )
			and v1.qualifiers
			then
			local quals = v1.qualifiers["P1114"]
			if quals then
				for k2, v2 in ipairs(quals) do
					sum = sum + v2.datavalue.value.amount
				end
			end
		end
	end
	return sum
end


-------------------------------------------------------------------------------
-------------------------------------------------------------------------------
-- Public functions
-------------------------------------------------------------------------------
-------------------------------------------------------------------------------
-- getValue is used to get the value(s) of a property
-- The property ID is passed as the first unnamed parameter and is required.
-- A locally supplied parameter may optionaly be supplied as the second unnamed parameter.
-- The function will now also return qualifiers if parameter qual is supplied
-------------------------------------------------------------------------------
-- Dependencies: setRanks; parseInput; propertyvalueandquals; assembleoutput; parseParam; sourced;
-- labelOrId; i18n.latestdatequalifier; format_Date; makeOrdinal; roundto; decimalPrecision; decimalToDMS;
-------------------------------------------------------------------------------
p.getValue = function(frame)
	if not frame.args[1] then
		frame.args = frame:getParent().args
		if not frame.args[1] then return i18n.errors["No property supplied"] end
	end

	-- parameter sets for commonly used groups of parameters
	local paraset = tonumber(frame.args.ps or frame.args.parameterset or 0)
	if paraset == 1 then
		frame.args.rank = "best"
		frame.args.fetchwikidata = "ALL"
		frame.args.onlysourced = "no"
		frame.args.noicon = "true"
	elseif paraset == 2 then
		-- second set goes here
	end

	local propertyID = mw.text.trim(frame.args[1] or "")

	frame.args.reqranks = setRanks(frame.args.rank)

	local entityid, props = parseInput(frame, frame.args[2], propertyID)

	if not entityid then
		return props -- either the input parameter or nothing
	end
	-- qual is a string containing the property ID of the qualifier(s) to be returned
	-- if qual == "ALL" then all qualifiers returned
	-- if qual == "DATES" then qualifiers P580 (start time) and P582 (end time) returned
	-- if nothing or an empty string is passed set it nil -> no qualifiers returned
	local qualID = mw.text.trim(frame.args.qual or ""):upper()
	if qualID == "" then qualID = nil end

	-- set a language object and code in the frame.args table
	frame.args.langobj = findLang(frame.args.lang)
	frame.args.lang = frame.args.langobj.code

	-- table 'out' stores the return value(s):
	local out = propertyvalueandquals(props, frame.args, qualID)

	-- format the table of values and return it as a string:
	return assembleoutput(out, frame.args, entityid, propertyID)
end


-------------------------------------------------------------------------------
-- getPreferredValue is used to get a value,
-- (or a comma separated list of them if multiple values exist).
-- If preferred ranks are set, it will return those values, otherwise values with normal ranks
-- now redundant to getValue with |rank=best
-------------------------------------------------------------------------------
-- Dependencies: p.getValue; setRanks; parseInput; propertyvalueandquals; assembleoutput;
-- parseParam; sourced; labelOrId; i18n.latestdatequalifier; format_Date;
-- makeOrdinal; roundto; decimalPrecision; decimalToDMS;
-------------------------------------------------------------------------------
p.getPreferredValue = function(frame)
	frame.args.rank = "best"
	return p.getValue(frame)
end


-------------------------------------------------------------------------------
-- getCoords is used to get coordinates for display in an infobox
-- whitelist and blacklist are implemented
-- optional 'display' parameter is allowed, defaults to "inline, title"
-------------------------------------------------------------------------------
-- Dependencies: setRanks(); parseInput(); decimalPrecision();
-------------------------------------------------------------------------------
p.getCoords = function(frame)
	local propertyID = "P625"

	-- if there is a 'display' parameter supplied, use it
	-- otherwise default to "inline, title"
	local disp = frame.args.display or ""
	if disp == "" then
		disp = "inline, title"
	end

	-- there may be a format parameter to switch from deg/min/sec to decimal degrees
	-- default is deg/min/sec
	-- decimal degrees needs |format = dec
	local form = (frame.args.format or ""):lower():sub(1,3)
	if form ~= "dec" then
		form = "dms"
	end

	-- just deal with best values
	frame.args.reqranks = setRanks("best")

	local qid, props = parseInput(frame, frame.args[1], propertyID)
	if not qid then
		return props -- either local parameter or nothing
	else
		local dv = props[1].mainsnak.datavalue.value
		local lat, long, prec = dv.latitude, dv.longitude, dv.precision
		lat = decimalPrecision(lat, prec)
		long = decimalPrecision(long, prec)
		local lat_long = { lat, long }
		lat_long["display"] = disp
		lat_long["format"] = form
		-- invoke template Coord with the values stored in the table
		return frame:expandTemplate{title = 'coord', args = lat_long}
	end
end


-------------------------------------------------------------------------------
-- getQualifierValue is used to get a formatted value of a qualifier
--
-- The call needs:	a property (the unnamed parameter or 1=)
-- 					a target value for that property (pval=)
--					a qualifier for that target value (qual=)
-- The usual whitelisting and blacklisting of the property is implemented
-- The boolean onlysourced= parameter can be set to return nothing
-- when the property is unsourced (or only sourced to Wikipedia)
-------------------------------------------------------------------------------
-- Dependencies: parseParam(); setRanks(); parseInput(); sourced();
-- propertyvalueandquals(); assembleoutput();
-- labelOrId(); i18n.latestdatequalifier(); format_Date();
-- findLang(); makeOrdinal(); roundto(); decimalPrecision(); decimalToDMS();
-------------------------------------------------------------------------------
p.getQualifierValue = function(frame)

	-- The property ID that will have a qualifier is the first unnamed parameter
	local propertyID = mw.text.trim(frame.args[1] or "")

	-- The value of the property we want to match whose qualifier value is to be returned
	-- is passed in named parameter |pval=
	local propvalue = frame.args.pval

	-- The property ID of the qualifier
	-- whose value is to be returned is passed in named parameter |qual=
	local qualifierID = frame.args.qual

	-- onlysourced is a boolean passed to return qualifiers
	-- only when property values are sourced to something other than Wikipedia
	-- if nothing or an empty string is passed set it true
	-- if "false" or "no" or 0 is passed set it false
	local onlysrc = parseParam(frame.args.onlysourced or frame.args.osd, true)

	-- set a language object and language code in the frame.args table
	frame.args.langobj = findLang(frame.args.lang)
	frame.args.lang = frame.args.langobj.code

	-- set the requested ranks flags
	frame.args.reqranks = setRanks(frame.args.rank)

	-- check for locally supplied parameter in second unnamed parameter
	-- success means no local parameter and the property exists
	local qid, props = parseInput(frame, frame.args[2], propertyID)
	if qid then
		local out = {}
		-- Scan through the values of the property
		-- we want something like property is P793, significant event (in propertyID)
		-- whose value is something like Q385378, construction (in propvalue)
		-- then we can return the value(s) of a qualifier such as P580, start time (in qualifierID)
		for k1, v1 in pairs(props) do
			if v1.mainsnak.snaktype == "value" and v1.mainsnak.datavalue.type == "wikibase-entityid" then
				-- It's a wiki-linked value, so check if it's the target (in propvalue)
				-- and if it has qualifiers
				if v1.mainsnak.datavalue.value.id == propvalue and v1.qualifiers then
					if onlysrc == false or sourced(v1) then
						-- if we've got this far, we have a (sourced) claim with qualifiers
						-- which matches the target, so find the value(s) of the qualifier we want
						local quals = v1.qualifiers[qualifierID]
						if quals then
							-- can't reference qualifer, so set onlysourced = "no" (not boolean)
							local qargs = frame.args
							qargs.onlysourced = "no"
							local vals = propertyvalueandquals(quals, qargs, qid)
							for k, v in ipairs(vals) do
								out[#out + 1] = v
							end
						end
					end -- of check for sourced
				end -- of check for matching required value and has qualifiers
			end -- of check for wikibase entity
		end -- of loop through values of propertyID
		return assembleoutput(out, frame.args, qid, propertyID)
	else
		return props -- either local parameter or nothing
	end -- of test for success
	return nil
end


-------------------------------------------------------------------------------
-- getSumOfParts scans the property 'has part' (P527) for values matching a list.
-- The list is passed in parameter vlist.
-- It consists of a string of Qids separated by spaces or any usual punctuation.
-- If the matched values have a qualifier 'quantity' (P1114), those quantities are summed.
-- The sum is returned as a number or nothing if zero.
-------------------------------------------------------------------------------
-- Dependencies: _getsumofparts;
-------------------------------------------------------------------------------
p.getSumOfParts = function(frame)
	local sum = _getsumofparts(frame.args)
	if sum == 0 then return end
	return sum
end


-------------------------------------------------------------------------------
-- getValueByQual gets the value of a property which has a qualifier with a given entity value
-- The call needs:
--					a property ID (the unnamed parameter or 1=Pxxx)
--					the ID of a qualifier for that property (qualID=Pyyy)
--					the Wikibase-entity ID of a value for that qualifier (qvalue=Qzzz)
-- The usual whitelisting, blacklisting, onlysourced, etc. are implemented
-------------------------------------------------------------------------------
-- Dependencies: _getvaluebyqual; parseParam; setRanks; parseInput; sourced;
-- assembleoutput;
-------------------------------------------------------------------------------
p.getValueByQual = function(frame)
	local qualID = frame.args.qualID
	-- The Q-id of the value for the qualifier we want to match is in named parameter |qvalue=
	local qval = frame.args.qvalue or ""
	if qval == "" then return "no qualifier value supplied" end
	local function checkQID(id)
		return id == qval
	end
	return _getvaluebyqual(frame, qualID, checkQID)
end


-------------------------------------------------------------------------------
-- getValueByLang gets the value of a property which has a qualifier P407
-- ("language of work or name") whose value has the given language code
-- The call needs:
--					a property ID (the unnamed parameter or 1=Pxxx)
--					the MediaWiki language code to match the language (lang=xx[-yy])
--					(if no code is supplied, it uses the default language)
-- The usual whitelisting, blacklisting, onlysourced, etc. are implemented
-------------------------------------------------------------------------------
-- Dependencies: _getvaluebyqual; parseParam; setRanks; parseInput; sourced; assembleoutput;
-------------------------------------------------------------------------------
p.getValueByLang = function(frame)

	-- The language code for the qualifier we want to match is in named parameter |lang=
	local langcode = frame.args.lang or ""
	if langcode == "" then
		langcode = frame:callParserFunction{ name = "int", args = "lang" }
	end
	local function checkLanguage(id)
		-- id should represent a language like "British English (Q7979)"
		-- it should have string property "Wikimedia language code (P424)"
		-- qlcode will be a table:
		local qlcode = mw.wikibase.getBestStatements(id, "P424")
		if (#qlcode > 0) and (qlcode[1].mainsnak.datavalue.value == langcode) then
			return true
		end
	end
	return _getvaluebyqual(frame, "P407", checkLanguage)
end


-------------------------------------------------------------------------------
-- getValueByRefSource gets the value of a property which has a reference "stated in" (P248)
-- whose value has the given entity code.
-- The call needs:
--					a property ID (the unnamed parameter or 1=Pxxx)
--					the entity ID of a value to match where the reference is stated in (match=Qzzz)
-- The usual whitelisting, blacklisting, onlysourced, etc. are implemented
-------------------------------------------------------------------------------
-- Dependencies: parseParam; setRanks; parseInput; sourced; propertyvalueandquals assembleoutput;
-------------------------------------------------------------------------------
p.getValueByRefSource = function(frame)
	-- The property ID that we want to check is the first unnamed parameter
	local propertyID = mw.text.trim(frame.args[1] or ""):upper()
	if propertyID == "" then return "no property supplied" end

	-- The Q-id of the value we want to match is in named parameter |qvalue=
	local qval = (frame.args.match or ""):upper()
	if qval == "" then qval = "Q21540096" end

	local unit = (frame.args.unit or ""):upper()
	if unit == "" then unit = "Q4917" end

	local onlysrc = parseParam(frame.args.onlysourced or frame.args.osd, true)

	-- set the requested ranks flags
	frame.args.reqranks = setRanks(frame.args.rank)

	-- set a language object and code in the frame.args table
	frame.args.langobj = findLang(frame.args.lang)
	frame.args.lang = frame.args.langobj.code

	local linked = parseParam(frame.args.linked, true)

	local uabbr = parseParam(frame.args.uabbr or frame.args.unitabbr, false)

	-- qid not nil means no local parameter and the property exists
	local qid, props = parseInput(frame, frame.args[2], propertyID)

	if qid then
		local out = {}
		local mlt= {}
		for k1, v1 in ipairs(props) do
			if onlysrc == false or sourced(v1) then
				if v1.references then
					for k2, v2 in ipairs(v1.references) do
						if v2.snaks.P248 then
							for k3, v3 in ipairs(v2.snaks.P248) do
								if v3.datavalue.value.id == qval then
									out[#out+1], mlt[#out+1] = rendersnak(v1, frame.args, linked, "", "", "", "", uabbr, unit)
									if not mlt[#out] then
										-- we only need one match per property value
										-- unless datatype was monolingual text
										break
									end
								end -- of test for match
							end -- of loop through values "stated in"
						end -- of test that "stated in" exists
					end -- of loop through references
				end -- of test that references exist
			end -- of test for sourced
		end -- of loop through values of propertyID
		if #mlt > 0 then
			local langcode = frame.args.lang
			langcode = mw.text.split( langcode, '-', true )[1]
			local fbtbl = mw.language.getFallbacksFor( langcode )
			table.insert( fbtbl, 1, langcode )
			local bestval = ""
			local found = false
			for idx1, lang1 in ipairs(fbtbl) do
				for idx2, lang2 in ipairs(mlt) do
					if (lang1 == lang2) and not found then
						bestval = out[idx2]
						found = true
						break
					end
				end -- loop through values of property
			end -- loop through fallback languages
			if found then
				-- replace output table with a table containing the best value
				out = { bestval }
			else
				-- more than one value and none of them on the list of fallback languages
				-- sod it, just give them the first one
				out = { out[1] }
			end
		end
		return assembleoutput(out, frame.args, qid, propertyID)
	else
		return props -- no property or local parameter supplied
	end -- of test for success
end


-------------------------------------------------------------------------------
-- getPropOfProp takes two propertyIDs: prop1 and prop2 (as well as the usual parameters)
-- If the value(s) of prop1 are of type "wikibase-item" then it returns the value(s) of prop2
-- of each of those wikibase-items.
-- The usual whitelisting, blacklisting, onlysourced, etc. are implemented
-------------------------------------------------------------------------------
-- Dependencies: parseParam; setRanks; parseInput; sourced; propertyvalueandquals assembleoutput;
-------------------------------------------------------------------------------
p.getPropOfProp = function(frame)
	frame.args.reqranks = setRanks(frame.args.rank)
	frame.args.langobj = findLang(frame.args.lang)
	frame.args.lang = frame.args.langobj.code
	local args = frame.args
	local pid1 = args.prop1 or args.pid1 or ""
	local pid2 = args.prop2 or args.pid2 or ""
	local localval = mw.text.trim(args[1] or "")
	if pid1 == "" or pid2 == "" then return nil end
	local qid1, statements1 = parseInput(frame, localval, pid1)
	if not qid1 then return localval end
	local onlysrc = parseParam(args.onlysourced or args.osd, true)
	local maxvals = tonumber(args.maxvals) or 0
	local qualID = mw.text.trim(args.qual or ""):upper()
	if qualID == "" then qualID = nil end
	local out = {}
	for k, v in ipairs(statements1) do
		if not onlysrc or sourced(v) then
			local snak = v.mainsnak
			if snak.datatype == "wikibase-item" and snak.snaktype == "value" then
				local qid2 = snak.datavalue.value.id
				local statements2 = {}
				if args.reqranks.b then
					statements2 = mw.wikibase.getBestStatements(qid2, pid2)
				else
					statements2 = mw.wikibase.getAllStatements(qid2, pid2)
				end
				if statements2[1] then
					local out2 = propertyvalueandquals(statements2, args, qualID)
					out[#out+1] = assembleoutput(out2, args, qid2, pid2)
				end
			end -- of test for valid property1 value
		end -- of test for sourced
		if maxvals > 0 and #out >= maxvals then break end
	end -- of loop through values of property1
	return assembleoutput(out, args, qid1, pid1)
end


-------------------------------------------------------------------------------
-- getAwardCat takes most of the usual parameters. If the item has values of P166 (award received),
-- then it examines each of those awards for P2517 (category for recipients of this award).
-- If it exists, it returns the corresponding category,
-- with the item's P734 (family name) as sort key, or no sort key if there is no family name.
-- The sort key may be overridden by the parameter |sortkey (alias |sk).
-- The usual whitelisting, blacklisting, onlysourced, etc. are implemented
-------------------------------------------------------------------------------
-- Dependencies: parseParam; setRanks; parseInput; sourced; propertyvalueandquals assembleoutput;
-------------------------------------------------------------------------------
p.getAwardCat = function(frame)
	frame.args.reqranks = setRanks(frame.args.rank)
	frame.args.langobj = findLang(frame.args.lang)
	frame.args.lang = frame.args.langobj.code
	local args = frame.args
	args.sep = " "
	local pid1 = args.prop1 or "P166"
	local pid2 = args.prop2 or "P2517"
	if pid1 == "" or pid2 == "" then return nil end
	-- locally supplied value:
	local localval = mw.text.trim(args[1] or "")
	local qid1, statements1 = parseInput(frame, localval, pid1)
	if not qid1 then return localval end
	-- linkprefix (strip quotes)
	local lp = (args.linkprefix or args.lp or ""):gsub('"', '')
	-- sort key (strip quotes, hyphens and periods):
	local sk = (args.sortkey or args.sk or ""):gsub('["-.]', '')
	-- family name:
	local famname = ""
	if sk == "" then
		local p734 = mw.wikibase.getBestStatements(qid1, "P734")[1]
		local p734id = p734 and p734.mainsnak.snaktype == "value" and p734.mainsnak.datavalue.value.id or ""
		famname = mw.wikibase.sitelink(p734id) or ""
		-- strip namespace and disambigation
		local pos = famname:find(":") or 0
		famname = famname:sub(pos+1):gsub("%s%(.+%)$", "")
		if famname == "" then
			local lbl = mw.wikibase.label(p734id)
			famname = lbl and mw.text.nowiki(lbl) or ""
		end
	end
	local onlysrc = parseParam(args.onlysourced or args.osd, true)
	local maxvals = tonumber(args.maxvals) or 0
	local qualID = mw.text.trim(args.qual or ""):upper()
	if qualID == "" then qualID = nil end
	local out = {}
	for k, v in ipairs(statements1) do
		if not onlysrc or sourced(v) then
			local snak = v.mainsnak
			if snak.datatype == "wikibase-item" and snak.snaktype == "value" then
				local qid2 = snak.datavalue.value.id
				local statements2 = {}
				if args.reqranks.b then
					statements2 = mw.wikibase.getBestStatements(qid2, pid2)
				else
					statements2 = mw.wikibase.getAllStatements(qid2, pid2)
				end
				if statements2[1] and statements2[1].mainsnak.snaktype == "value" then
					local qid3 = statements2[1].mainsnak.datavalue.value.id
					local sitelink = mw.wikibase.sitelink(qid3)
					-- if there's no local sitelink, create the sitelink from English label
					if not sitelink then
						local lbl = mw.wikibase.getLabelByLang(qid3, "en")
						if lbl then
							if lbl:sub(1,9) == "Category:" then
								sitelink = mw.text.nowiki(lbl)
							else
								sitelink = "Category:" .. mw.text.nowiki(lbl)
							end
						end
					end
					if sitelink then
						if sk ~= "" then
							out[#out+1] = "[["_.._lp_.._sitelink_.._"|" .. sk .. "]]"
						elseif famname ~= "" then
							out[#out+1] = "[["_.._lp_.._sitelink_.._"|" .. famname .. "]]"
						else
							out[#out+1] = "[["_.._lp_.._sitelink_.._"|" .. lp .. sitelink .. "]]"
						end -- of check for sort keys
					end -- of test for sitelink
				end -- of test for category
			end -- of test for wikibase item has a value
		end -- of test for sourced
		if maxvals > 0 and #out >= maxvals then break end
	end -- of loop through values of property1
	return assembleoutput(out, args, qid1, pid1)
end


-------------------------------------------------------------------------------
-- getIntersectCat takes most of the usual parameters.
-- The usual whitelisting, blacklisting, onlysourced, etc. are implemented
-- It takes two properties, |prop1 and |prop2 (e.g. occupation and country of citizenship)
-- Each property's value is a wiki-base entity
-- For each value of the first parameter (ranks implemented) it fetches the value's main category
-- and then each value of the second parameter (possibly substituting a simpler description)
-- then it returns all of the categories representing the intersection of those properties,
-- (e.g. Category:Actors from Canada). A joining term may be supplied (e.g. |join=from).
-- The item's P734 (family name) is the sort key, or no sort key if there is no family name.
-- The sort key may be overridden by the parameter |sortkey (alias |sk).
-------------------------------------------------------------------------------
-- Dependencies: parseParam; setRanks; parseInput; sourced; propertyvalueandquals assembleoutput;
-------------------------------------------------------------------------------
p.getIntersectCat = function(frame)
	frame.args.reqranks = setRanks(frame.args.rank)
	frame.args.langobj = findLang(frame.args.lang)
	frame.args.lang = frame.args.langobj.code
	local args = frame.args
	args.sep = " "
	args.linked = "no"
	local pid1 = args.prop1 or "P106"
	local pid2 = args.prop2 or "P27"
	if pid1 == "" or pid2 == "" then return nil end
	local qid, statements1 = parseInput(frame, "", pid1)
	if not qid then return nil end
	local qid, statements2 = parseInput(frame, "", pid2)
	if not qid then return nil end
	-- topics like countries may have different names in categories from their label in Wikidata
	local subs_exists, subs = pcall(mw.loadData, "Module:WikidataIB/subs")
	local join = args.join or ""
	local onlysrc = parseParam(args.onlysourced or args.osd, true)
	local maxvals = tonumber(args.maxvals) or 0
	-- linkprefix (strip quotes)
	local lp = (args.linkprefix or args.lp or ""):gsub('"', '')
	-- sort key (strip quotes, hyphens and periods):
	local sk = (args.sortkey or args.sk or ""):gsub('["-.]', '')
	-- family name:
	local famname = ""
	if sk == "" then
		local p734 = mw.wikibase.getBestStatements(qid, "P734")[1]
		local p734id = p734 and p734.mainsnak.snaktype == "value" and p734.mainsnak.datavalue.value.id or ""
		famname = mw.wikibase.sitelink(p734id) or ""
		-- strip namespace and disambigation
		local pos = famname:find(":") or 0
		famname = famname:sub(pos+1):gsub("%s%(.+%)$", "")
		if famname == "" then
			local lbl = mw.wikibase.label(p734id)
			famname = lbl and mw.text.nowiki(lbl) or ""
		end
	end
	local cat1 = {}
	for k, v in ipairs(statements1) do
		if not onlysrc or sourced(v) then
			-- get the ID representing the value of the property
			local pvalID = (v.mainsnak.snaktype == "value") and v.mainsnak.datavalue.value.id
			if pvalID then
				-- get the topic's main category (P910) for that entity
				local p910 = mw.wikibase.getBestStatements(pvalID, "P910")[1]
				if p910 and p910.mainsnak.snaktype == "value" then
					local tmcID = p910.mainsnak.datavalue.value.id
					-- use sitelink or the English label for the cat
					local cat = mw.wikibase.sitelink(tmcID)
					if not cat then
						local lbl = mw.wikibase.getLabelByLang(tmcID, "en")
						if lbl then
							if lbl:sub(1,9) == "Category:" then
								cat = mw.text.nowiki(lbl)
							else
								cat = "Category:" .. mw.text.nowiki(lbl)
							end
						end
					end
					cat1[#cat1+1] = cat
				end -- of test for topic's main category exists
			end -- of test for property has vaild value
		end -- of test for sourced
		if maxvals > 0 and #cat1 >= maxvals then break end
	end
	local cat2 = {}
	for k, v in ipairs(statements2) do
		if not onlysrc or sourced(v) then
			local cat = rendersnak(v, args)
			if subs[cat] then cat = subs[cat] end
			cat2[#cat2+1] = cat
		end
		if maxvals > 0 and #cat2 >= maxvals then break end
	end
	out = {}
	for k1, v1 in ipairs(cat1) do
		for k2, v2 in ipairs(cat2) do
			if sk ~= "" then
				out[#out+1] = "[["_.._lp_.._v1_.._"_"_.._join_.._"_"_.._v2_.._"|" .. sk .. "]]"
			elseif famname ~= "" then
				out[#out+1] = "[["_.._lp_.._v1_.._"_"_.._join_.._"_"_.._v2_.._"|" .. famname .. "]]"
			else
				out[#out+1] = "[["_.._lp_.._v1_.._"_"_.._join_.._"_"_.._v2_.._"|" .. lp .. v1 .. " " .. join .. " " .. v2 .. "]]"
			end -- of check for sort keys
		end
	end
	args.noicon = "true"
	return assembleoutput(out, args, qid, pid1)
end


-------------------------------------------------------------------------------
-- getGlobe takes an optional qid of a Wikidata entity passed as |qid=
-- otherwise it uses the linked item for the current page.
-- If returns the Qid of the globe used in P625 (coordinate location),
-- or nil if there isn't one.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.getGlobe = function(frame)
	local qid = frame.args.qid or frame.args[1] or ""
	if qid == "" then qid = mw.wikibase.getEntityIdForCurrentPage() end
	local coords = mw.wikibase.getBestStatements(qid, "P625")[1]
	local globeid
	if coords and coords.mainsnak.snaktype == "value" then
		globeid = coords.mainsnak.datavalue.value.globe:match("(Q%d+)")
	end
	return globeid
end


-------------------------------------------------------------------------------
-- getCommonsLink takes an optional qid of a Wikidata entity passed as |qid=
-- It returns one of the following in order of preference:
-- the Commons sitelink of the linked Wikidata item;
-- the Commons sitelink of the topic's main category of the linked Wikidata item;
-------------------------------------------------------------------------------
-- Dependencies: _getCommonslink(); _getSitelink(); parseParam()
-------------------------------------------------------------------------------
p.getCommonsLink = function(frame)
	local oc = frame.args.onlycat or frame.args.onlycategories
	local fb = parseParam(frame.args.fallback or frame.args.fb, true)
	return _getCommonslink(frame.args.qid, oc, fb)
end


-------------------------------------------------------------------------------
-- getSitelink takes the qid of a Wikidata entity passed as |qid=
-- It takes an optional parameter |wiki= to determine which wiki is to be checked for a sitelink
-- If the parameter is blank, then it uses the local wiki.
-- If there is a sitelink to an article available, it returns the plain text link to the article
-- If there is no sitelink, it returns nil.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.getSiteLink = function(frame)
	return _getSitelink(frame.args.qid, frame.args.wiki or mw.text.trim(frame.args[1] or ""))
end


-------------------------------------------------------------------------------
-- getLink has the qid of a Wikidata entity passed as the first unnamed parameter or as |qid=
-- If there is a sitelink to an article on the local Wiki, it returns a link to the article
-- with the Wikidata label as the displayed text.
-- If there is no sitelink, it returns the label as plain text.
-- If there is no label in the local language, it displays the qid instead.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.getLink = function(frame)
	local itemID = mw.text.trim(frame.args[1] or frame.args.qid or "")
	if itemID == "" then return end
	local sitelink = mw.wikibase.sitelink(itemID)
	local label = labelOrId(itemID)
	if sitelink then
		return "[[:"_.._sitelink_.._"|" .. label .. "]]"
	else
		return label
	end
end


-------------------------------------------------------------------------------
-- getLabel has the qid of a Wikidata entity passed as the first unnamed parameter or as |qid=
-- It returns the Wikidata label for the local language as plain text.
-- If there is no label in the local language, it displays the qid instead.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.getLabel = function(frame)
	local itemID = mw.text.trim(frame.args[1] or frame.args.qid or "")
	if itemID == "" then return end
	local label = labelOrId(itemID)
	return label
end


-------------------------------------------------------------------------------
-- getAT (Article Title)
-- has the qid of a Wikidata entity passed as the first unnamed parameter or as |qid=
-- If there is a sitelink to an article on the local Wiki, it returns the sitelink as plain text.
-- If there is no sitelink, it returns nothing.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.getAT = function(frame)
	local itemID = mw.text.trim(frame.args[1] or frame.args.qid or "")
	if itemID == "" then return end
	return mw.wikibase.sitelink(itemID)
end


-------------------------------------------------------------------------------
-- getDescription has the qid of a Wikidata entity passed as |qid=
-- (it defaults to the associated qid of the current article if omitted)
-- and a local parameter passed as the first unnamed parameter.
-- Any local parameter passed (other than "Wikidata" or "none") becomes the return value.
-- It returns the article description for the Wikidata entity if the local parameter is "Wikidata".
-- Nothing is returned if the description doesn't exist or "none" is passed as the local parameter.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.getDescription = function(frame)
	local desc = mw.text.trim(frame.args[1] or "")
	local itemID = mw.text.trim(frame.args.qid or "")
	if itemID == "" then itemID = nil end
	if desc:lower() == 'wikidata' then
		return mw.wikibase.description(itemID)
	elseif desc:lower() == 'none' then
		return nil
	else
		return desc
	end
end


-------------------------------------------------------------------------------
-- getAliases has the qid of a Wikidata entity passed as |qid=
-- (it defaults to the associated qid of the current article if omitted)
-- and a local parameter passed as the first unnamed parameter.
-- It implements blacklisting and whitelisting with a field name of "alias" by default.
-- Any local parameter passed becomes the return value.
-- Otherwise it returns the aliases for the Wikidata entity with the usual list options.
-- Nothing is returned if the aliases do not exist.
-------------------------------------------------------------------------------
-- Dependencies: findLang(); assembleoutput()
-------------------------------------------------------------------------------
p.getAliases = function(frame)
	local args = frame.args

	local fieldname = args.name or ""
	if fieldname == "" then fieldname = "alias" end

	local blacklist = args.suppressfields or args.spf or ""
	if blacklist:find(fieldname) then return nil end

	local localval = mw.text.trim(args[1] or "")
	if localval ~= "" then return localval end

	local whitelist = args.fetchwikidata or args.fwd or ""
	if whitelist == "" then whitelist = "NONE" end
	if not (whitelist == 'ALL' or whitelist:find(fieldname)) then return nil end

	local qid = mw.text.trim(args.qid or "")
	if qid == "" then qid = nil end

	local entity = mw.wikibase.getEntity(qid)
	if not entity then return nil end
	local aliases = entity.aliases
	if not aliases then return nil end
	if not qid then qid= mw.wikibase.getEntityIdForCurrentPage() end

	args.langobj = findLang(args.lang)
	local langcode = args.langobj.code
	args.lang = langcode

	local out = {}
	for k1, v1 in pairs(aliases) do
		if v1[1].language == langcode then
			for k1, v2 in ipairs(v1) do
				out[#out+1] = v2.value
			end
			break
		end
	end

	return assembleoutput(out, args, qid)
end


-------------------------------------------------------------------------------
-- pageId returns the page id (entity ID, Qnnn) of the current page
-- returns nothing if the page is not connected to Wikidata
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.pageId = function(frame)
	return mw.wikibase.getEntityIdForCurrentPage()
end


-------------------------------------------------------------------------------
-- formatDate is a wrapper to export the private function format_Date
-------------------------------------------------------------------------------
-- Dependencies: format_Date();
-------------------------------------------------------------------------------
p.formatDate = function(frame)
	return format_Date(frame.args[1], frame.args.df, frame.args.bc)
end


-------------------------------------------------------------------------------
-- location is a wrapper to export the private function _location
-- it takes the entity-id as qid or the first unnamed parameter
-- optional boolean parameter first toggles the display of the first item
-- optional boolean parameter skip toggles the display to skip to the last item
-- parameter debug=<y/n> (default 'n') adds error msg if not a location
-------------------------------------------------------------------------------
-- Dependencies: _location();
-------------------------------------------------------------------------------
p.location = function(frame)
	local debug = (frame.args.debug or ""):sub(1, 1):lower()
	if debug == "" then debug = "n" end
	local qid = mw.text.trim(frame.args.qid or frame.args[1] or ""):upper()
	if qid == "" then qid=mw.wikibase.getEntityIdForCurrentPage() end
	if not qid then
		if debug ~= "n" then
			return i18n.errors["entity-not-found"]
		else
			return nil
		end
	end
	local first = mw.text.trim(frame.args.first or "")
	local skip = mw.text.trim(frame.args.skip or "")
	return table.concat( _location(qid, first, skip), ", " )
end


-------------------------------------------------------------------------------
-- checkBlacklist implements a test to check whether a named field is allowed
-- returns true if the field is not blacklisted (i.e. allowed)
-- returns false if the field is blacklisted (i.e. disallowed)
-- {{#if:{{#invoke:WikidataIB |checkBlacklist |name=Joe |suppressfields=Dave; Joe; Fred}} | not blacklisted | blacklisted}}
-- displays "blacklisted"
-- {{#if:{{#invoke:WikidataIB |checkBlacklist |name=Jim |suppressfields=Dave; Joe; Fred}} | not blacklisted | blacklisted}}
-- displays "not blacklisted"
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.checkBlacklist = function(frame)
	local blacklist = frame.args.suppressfields or frame.args.spf or ""
	local fieldname = frame.args.name or ""
	if blacklist ~= "" and fieldname ~= "" then
		if blacklist:find(fieldname) then
			return false
		else
			return true
		end
	else
		-- one of the fields is missing: let's call that "not on the list"
		return true
	end
end


-------------------------------------------------------------------------------
-- emptyor returns nil if its first unnamed argument is just punctuation, whitespace or html tags
-- otherwise it returns the argument unchanged (including leading/trailing space).
-- If the argument may contain "=", then it must be called explicitly:
-- |1=arg
-- (In that case, leading and trailing spaces are trimmed)
-- It finds use in infoboxes where it can replace tests like:
-- {{#if: {{#invoke:WikidatIB |getvalue |P99 |fwd=ALL}} | <span class="xxx">{{#invoke:WikidatIB |getvalue |P99 |fwd=ALL}}</span> | }}
-- with a form that uses just a single call to Wikidata:
-- {{#invoke |WikidataIB |emptyor |1= <span class="xxx">{{#invoke:WikidataIB |getvalue |P99 |fwd=ALL}}</span> }}
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.emptyor = function(frame)
	local s = frame.args[1] or ""
	if s == "" then return nil end
	local sx = s:gsub("%s", ""):gsub("<[^>]*>", ""):gsub("%p", "")
	if sx == "" then
		return nil
	else
		return s
	end
end


-------------------------------------------------------------------------------
-- labelorid is a public function to expose the output of labelOrId()
-- Pass the Q-number as |qid= or as an unnamed parameter.
-- It returns the Wikidata label for that entity or the qid if no label exists.
-------------------------------------------------------------------------------
-- Dependencies: labelOrId
-------------------------------------------------------------------------------
p.labelorid = function(frame)
	return labelOrId( frame.args.qid or frame.args[1] )
end


-------------------------------------------------------------------------------
-- getLang returns the MediaWiki language code of the current content.
-- If optional parameter |style=full, it returns the language name.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.getLang = function(frame)
	local style = (frame.args.style or ""):lower()
	local langcode = mw.language.getContentLanguage().code
	if style == "full" then
		return mw.language.fetchLanguageName( langcode )
	end
	return langcode
end


-------------------------------------------------------------------------------
-- getItemLangCode takes a qid parameter (using the current page's qid if blank)
-- If the item for that qid has property country (P17) it looks at the first preferred value
-- If the country has an official language (P37), it looks at the first preferred value
-- If that official language has a language code (P424), it returns the first preferred value
-- Otherwise it returns nothing.
-------------------------------------------------------------------------------
-- Dependencies: _getItemLangCode()
-------------------------------------------------------------------------------
p.getItemLangCode = function(frame)
	return _getItemLangCode(frame.args.qid or frame.args[1])
end


-------------------------------------------------------------------------------
-- findLanguage exports the local findLang() function
-- It takes an optional language code and returns, in order of preference:
-- the code if a known language;
-- the user's language, if set;
-- the server's content language.
-------------------------------------------------------------------------------
-- Dependencies: findLang
-------------------------------------------------------------------------------
p.findLanguage = function(frame)
	return findLang(frame.args.lang or frame.args[1]).code
end


-------------------------------------------------------------------------------
-- getQid returns the qid, if supplied
-- failing that, the Wikidata entity ID of the "category's main topic (P301)", if it exists
-- failing that, the Wikidata entity ID asociated with the curent page, if it exists
-- otherwise, nothing
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.getQid = function(frame)
	local qid = (frame.args.qid or ""):upper()
	-- check if a qid was passed; if so, return it:
	if qid ~= "" then return qid end
	-- check if there's a "category's main topic (P301)":
	qid = mw.wikibase.getEntityIdForCurrentPage()
	if qid then
		local prop301 = mw.wikibase.getBestStatements(qid, "P301")
		if prop301[1] then
			local mctid = prop301[1].mainsnak.datavalue.value.id
			if mctid then return mctid end
		end
	end
	-- otherwise return the page qid (if any)
	return qid
end


-------------------------------------------------------------------------------
-- followQid takes two optional parameters: qid and props
-- If qid is not given, it uses the qid for the connected page
-- or returns nil if there isn't one.
-- props is a list of properties, separated by punctuation.
-- If props is given, the Wikidata item for the qid is examined for each property in turn.
-- If that property contains a value that is another Wikibase-item, that item's qid is returned,
-- and the search terminates, unless |all=y when all of the qids are returned, sparated by spaces.
-- If props is not given, the qid is returned.
-------------------------------------------------------------------------------
-- Dependencies: parseParam()
-------------------------------------------------------------------------------
p.followQid = function(frame)
	local qid = (frame.args.qid or ""):upper()
	local all = parseParam(frame.args.all, false)
	if qid == "" then
		qid = mw.wikibase.getEntityIdForCurrentPage()
	end
	if not qid then return nil end
	local out = {}
	local props = (frame.args.props or ""):upper()
	if props ~= "" then
		for p in mw.text.gsplit(props, "%p") do -- split at punctuation and iterate
			p = mw.text.trim(p)
			for i, v in ipairs( mw.wikibase.getBestStatements(qid, p) ) do
				local linkedid = v.mainsnak.datavalue and v.mainsnak.datavalue.value.id
				if linkedid then
					if all then
						out[#out+1] = linkedid
					else
						return linkedid
					end -- test for all or just the first one found
				end -- test for value exists for that property
			end -- loop through values of property to follow
		end -- loop through list of properties to follow
	end
	if #out > 0 then
		return table.concat(out, " ")
	else
		return qid
	end
end


-------------------------------------------------------------------------------
-- siteID returns the root of the globalSiteID
-- e.g. "en" for "enwiki", "enwikisource", etc.
-- treats "en-gb" as "en", etc.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.siteID = function(frame)
	local txtlang = frame:preprocess( "{{int:lang}}" ) or ""
	-- This deals with specific exceptions: be-tarask -> be-x-old
	if txtlang == "be-tarask" then
		return "be_x_old"
	end
	local pos = txtlang:find("-")
	local ret = ""
	if pos then
		ret = txtlang:sub(1, pos-1)
	else
		ret = txtlang
	end
	return ret
end


-------------------------------------------------------------------------------
-- projID returns the code used to link to the reader's language's project
-- e.g "en" for [[:en:WikidataIB|:en:WikidataIB]]
-- treats "en-gb" as "en", etc.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.projID = function(frame)
	local txtlang = frame:preprocess( "{{int:lang}}" ) or ""
	-- This deals with specific exceptions: be-tarask -> be-x-old
	if txtlang == "be-tarask" then
		return "be-x-old"
	end
	local pos = txtlang:find("-")
	local ret = ""
	if pos then
		ret = txtlang:sub(1, pos-1)
	else
		ret = txtlang
	end
	return ret
end


-------------------------------------------------------------------------------
-- formatNumber formats a number according to the the supplied language code ("|lang=")
-- or the default language if not supplied.
-- The number is the first unnamed parameter or "|num="
-------------------------------------------------------------------------------
-- Dependencies: findLang()
-------------------------------------------------------------------------------
p.formatNumber = function(frame)
	local lang
	local num = tonumber(frame.args[1] or frame.args.num) or 0
	lang = findLang(frame.args.lang)
	return lang:formatNum( num )
end


-------------------------------------------------------------------------------
-- examine dumps the property (the unnamed parameter or pid)
-- from the item given by the parameter 'qid' (or the other unnamed parameter)
-- or from the item corresponding to the current page if qid is not supplied.
-- e.g. {{#invoke:WikidataIB |examine |pid=P26 |qid=Q42}}
-- or {{#invoke:WikidataIB |examine |P26 |Q42}} or any combination of these
-- or {{#invoke:WikidataIB |examine |P26}} for the current page.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.examine = function( frame )
	local args
	if frame.args[1] or frame.args.pid or frame.args.qid then
		args = frame.args
	else
		args = frame:getParent().args
	end
	local par = {}
	local pid = (args.pid or ""):upper()
	local qid = (args.qid or ""):upper()
	par[1] = mw.text.trim( args[1] or "" ):upper()
	par[2] = mw.text.trim( args[2] or "" ):upper()
	table.sort(par)
	if par[2]:sub(1,1) == "P" then par[1], par[2] = par[2], par[1] end
	if pid == "" then pid = par[1] end
	if qid == "" then qid = par[2] end
	if pid:sub(1,1) ~= "P" then return "No property supplied" end
	if qid:sub(1,1) ~= "Q" then qid = mw.wikibase.getEntityIdForCurrentPage() end
	if not qid then return "No item for this page" end
	return "<pre>" .. mw.dumpObject( mw.wikibase.getAllStatements( qid, pid ) ) .. "</pre>"
end


-------------------------------------------------------------------------------
-- checkvalue looks for 'val' as a wikibase-item value of a property (the unnamed parameter or pid)
-- from the item given by the parameter 'qid'
-- or from the Wikidata item associated with the current page if qid is not supplied.
-- If property is not supplied, then P31 (instance of) is assumed.
-- It returns val if found or nothing if not found.
-- e.g. {{#invoke:WikidataIB |checkvalue |val=Q5 |pid=P31 |qid=Q42}}
-- or {{#invoke:WikidataIB |checkvalue |val=Q5 |P31 |qid=Q42}}
-- or {{#invoke:WikidataIB |checkvalue |val=Q5 |qid=Q42}}
-- or {{#invoke:WikidataIB |checkvalue |val=Q5 |P31}} for the current page.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.checkvalue = function( frame )
	local args
	if frame.args.val then
		args = frame.args
	else
		args = frame:getParent().args
	end
	local val = args.val
	if not val then return nil end
	local pid = mw.text.trim(args.pid or args[1] or "P31"):upper()
	local qid = (args.qid or ""):upper()
	if pid:sub(1,1) ~= "P" then return nil end
	if qid:sub(1,1) ~= "Q" then qid = mw.wikibase.getEntityIdForCurrentPage() end
	if not qid then return nil end
	local stats = mw.wikibase.getAllStatements( qid, pid )
	if not stats[1] then return nil end
	if stats[1].mainsnak.datatype == "wikibase-item" then
		for k, v in pairs( stats ) do
			if v.mainsnak.snaktype == "value" and v.mainsnak.datavalue.value.id == val then
				return val
			end
		end
	end
	return nil
end


-------------------------------------------------------------------------------
-- url2 takes a parameter url= that is a proper url and formats it for use in an infobox.
-- If no parameter is supplied, it returns nothing.
-- This is the equivalent of Template:URL
-- but it keeps the "edit at Wikidata" pen icon out of the microformat.
-- Usually it will take its url parameter directly from a Wikidata call:
-- e.g. {{#invoke:WikidataIB |url2 |url={{wdib |P856 |qid=Q23317 |fwd=ALL |osd=no}}
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.url2 = function(frame)
	local txt = frame.args.url or ""
	if txt == "" then return nil end
	local url, icon = txt:match("(.+) (.+)")
	url = url or txt
	icon = icon or ""
	local prot, addr = url:match("(http[s]*://)(.+)")
	prot = prot or url
	addr = addr or ""
	local disp, n = addr:gsub("%.", "<wbr/>%.")
	return '<span class="url">[' .. prot .. addr .. " " .. disp .. "]</span> " .. icon
end


-------------------------------------------------------------------------------
-- getWebsite fetches the Official website (P856) and formats it for use in an infobox.
-- This is similar to Template:Official website but with a url displayed,
-- and it adds the "edit at Wikidata" pen icon beyond the microformat if enabled.
-- A local value will override the Wikidata value. "NONE" returns nothing.
-- e.g. {{#invoke:WikidataIB |getWebsite |qid= |noicon= |lang= |url= }}
-------------------------------------------------------------------------------
-- Dependencies: findLang(); parseParam();
-------------------------------------------------------------------------------
p.getWebsite = function(frame)
	local url = frame.args.url or ""
	if url:upper() == "NONE" then return nil end

	local qid = frame.args.qid or ""
	if qid == "" then qid = mw.wikibase.getEntityIdForCurrentPage() end
	if not qid then return nil end

	local urls = {}
	local quals = {}
	if url == "" then
		local prop856 = mw.wikibase.getBestStatements(qid, "P856")
		for k, v in pairs(prop856) do
			if v.mainsnak.snaktype == "value" then
				urls[#urls+1] = v.mainsnak.datavalue.value
				if v.qualifiers and v.qualifiers["P1065"] then
					 -- just take the first archive url (P1065)
					local au = v.qualifiers["P1065"][1]
					if au.snaktype == "value" then
						quals[#urls] = au.datavalue.value
					end -- test for archive url having a value
				end -- test for qualifers
			end -- test for website having a value
		end -- loop through website(s)
	else
		urls[1] = url
	end
	if #urls == 0 then return nil end

	local out = {}
	for i, u in ipairs(urls) do
		local link = quals[i] or u
		local prot, addr = u:match("(http[s]*://)(.+)")
		addr = addr or u
		local disp, n = addr:gsub("%.", "<wbr/>%.")
		out[#out+1] = '<span class="url">[' .. link .. " " .. disp .. "]</span>"
	end

	local langcode = findLang(frame.args.lang).code
	local noicon = parseParam(frame.args.noicon, false)
	if url == "" and not noicon then
		out[#out] = out[#out] .. createicon(langcode, qid, "P856")
	end

	local ret = ""
	if #out > 1 then
		ret = mw.getCurrentFrame():expandTemplate{title = "ubl", args = out}
	else
		ret = out[1]
	end

	return ret
end


-------------------------------------------------------------------------------
-- getAllLabels fetches the set of labels and formats it for display as wikitext.
-- It takes a parameter 'qid' for arbitrary access, otherwise it uses the current page.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.getAllLabels = function(frame)
	local args = frame.args or frame:getParent().args or {}

	local qid = args.qid
	if qid == "" then qid = nil end

	local entity = mw.wikibase.getEntity(qid)
	if not entity then return i18n["entity-not-found"] end

	local labels = entity.labels
	if not labels then return i18n["labels-not-found"] end

	local out = {}
	for k, v in pairs(labels) do
		out[#out+1] = v.value .. " (" .. v.language .. ")"
	end

	return table.concat(out, "; ")
end


-------------------------------------------------------------------------------
-- getAllDescriptions fetches the set of descriptions and formats it for display as wikitext.
-- It takes a parameter 'qid' for arbitrary access, otherwise it uses the current page.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.getAllDescriptions = function(frame)
	local args = frame.args or frame:getParent().args or {}

	local qid = args.qid
	if qid == "" then qid = nil end

	local entity = mw.wikibase.getEntity(qid)
	if not entity then return i18n["entity-not-found"] end

	local descriptions = entity.descriptions
	if not descriptions then return i18n["descriptions-not-found"] end

	local out = {}
	for k, v in pairs(descriptions) do
		out[#out+1] = v.value .. " (" .. v.language .. ")"
	end

	return table.concat(out, "; ")
end


-------------------------------------------------------------------------------
-- getAllAliases fetches the set of aliases and formats it for display as wikitext.
-- It takes a parameter 'qid' for arbitrary access, otherwise it uses the current page.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.getAllAliases = function(frame)
	local args = frame.args or frame:getParent().args or {}

	local qid = args.qid
	if qid == "" then qid = nil end

	local entity = mw.wikibase.getEntity(qid)
	if not entity then return i18n["entity-not-found"] end

	local aliases = entity.aliases
	if not aliases then return i18n["aliases-not-found"] end

	local out = {}
	for k1, v1 in pairs(aliases) do
		local lang = v1[1].language
		local val = {}
		for k1, v2 in ipairs(v1) do
			val[#val+1] = v2.value
		end
		out[#out+1] = table.concat(val, ", ") .. " (" .. lang .. ")"
	end

	return table.concat(out, "; ")
end


-------------------------------------------------------------------------------
-- showNoLinks displays the article titles that should not be linked.
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
p.showNoLinks = function(frame)
	local out = {}
	for k, v in pairs(donotlink) do
		out[#out+1] = k
	end
	table.sort( out )
	return table.concat(out, "; ")
end


-------------------------------------------------------------------------------
-- checkValidity checks whether the first unnamed parameter represents a valid entity-id,
-- that is, something like Q1235 or P123.
-- It returns the strings "true" or "false".
-- Change false to nil to return "true" or "" (easier to test with #if:).
-------------------------------------------------------------------------------
-- Dependencies: none
-------------------------------------------------------------------------------
function p.checkValidity(frame)
	local id = mw.text.trim(frame.args[1] or "")
	if mw.wikibase.isValidEntityId(id) then
		return true
	else
		return false
	end
end


return p


-------------------------------------------------------------------------------
-- List of exported functions
-------------------------------------------------------------------------------
-- getValue
-- getPreferredValue
-- getCoords
-- getQualifierValue
-- getSumOfParts
-- getValueByQual
-- getValueByLang
-- getValueByRefSource
-- getPropOfProp
-- getAwardCat
-- getIntersectCat
-- getGlobe
-- getCommonsLink
-- getSiteLink
-- getLink
-- getLabel
-- getAT
-- getDescription
-- getAliases
-- pageId
-- formatDate
-- location
-- checkBlacklist
-- emptyor
-- labelorid
-- getLang
-- findLanguage

-- getQID
-- followQid
-- siteID
-- projID
-- formatNumber
-- examine
-- checkvalue
-- url2
-- getWebsite
-- getAllLabels
-- getAllDescriptions
-- getAllAliases
-- showNoLinks
-- checkValidity
-------------------------------------------------------------------------------