-- vim: set noexpandtab ft=lua ts=4 sw=4:
require('Module:No globals')

local p = {}
local debug = false


------------------------------------------------------------------------------
-- module local variables and functions

local wiki =
{
	langcode = mw.language.getContentLanguage().code
}

-- internationalisation
local i18n =
{
	["errors"] =
	{
		["property-not-found"] = "Property not found.",
		["entity-not-found"] = "Wikidata entity not found.",
		["unknown-claim-type"] = "Unknown claim type.",
		["unknown-entity-type"] = "Unknown entity type.",
		["qualifier-not-found"] = "Qualifier not found.",
		["site-not-found"] = "Wikimedia project not found.",
		["unknown-datetime-format"] = "Unknown datetime format.",
		["local-article-not-found"] = "Article is not yet available in this wiki."
	},
	["datetime"] =
	{
		-- $1 is a placeholder for the actual number
		[0] = "$1 billion years",	-- precision: billion years
		[1] = "$100 million years",	-- precision: hundred million years
		[2] = "$10 million years",	-- precision: ten million years
		[3] = "$1 million years",	-- precision: million years
		[4] = "$100,000 years",		-- precision: hundred thousand years
		[5] = "$10,000 years",		-- precision: ten thousand years
		[6] = "$1 millennium",		-- precision: millennium
		[7] = "$1 century",			-- precision: century
		[8] = "$1s",				-- precision: decade
		-- the following use the format of #time parser function
		[9]  = "Y",					-- precision: year,
		[10] = "F Y",				-- precision: month
		[11] = "F j, Y",			-- precision: day
		[12] = "F j, Y ga",			-- precision: hour
		[13] = "F j, Y g:ia",		-- precision: minute
		[14] = "F j, Y g:i:sa",		-- precision: second
		["beforenow"] = "$1 BCE",	-- how to format negative numbers for precisions 0 to 5
		["afternow"] = "$1 CE",		-- how to format positive numbers for precisions 0 to 5
		["bc"] = '$1 "BCE"',		-- how print negative years
		["ad"] = "$1",				-- how print positive years
		-- the following are for function getDateValue() and getQualifierDateValue()
		["default-format"] = "dmy", -- default value of the #3 (getDateValue) or
									-- #4 (getQualifierDateValue) argument
		["default-addon"] = "BC",	-- default value of the #4 (getDateValue) or
									-- #5 (getQualifierDateValue) argument
		["prefix-addon"] = false,	-- set to true for languages put "BC" in front of the
									-- datetime string; or the addon will be suffixed
		["addon-sep"] = " ",		-- separator between datetime string and addon (or inverse)
		["format"] =				-- options of the 3rd argument
		{
			["mdy"] = "F j, Y",
			["my"] = "F Y",
			["y"] = "Y",
			["dmy"] = "j F Y",
			["ymd"] = "Y-m-d",
			["ym"] = "Y-m"
		}
	},
	["monolingualtext"] = '<span lang="%language">%text</span>',
	["warnDump"] = "[[Category:Called_function_'Dump'_from_module_Wikidata|Category:Called function 'Dump' from module Wikidata]]",
	["ordinal"] =
	{
		[1] = "st",
		[2] = "nd",
		[3] = "rd",
		["default"] = "th"
	}
}

-- Credit to http://stackoverflow.com/a/1283608/2644759
-- cc-by-sa 3.0
local function tableMerge(t1, t2)
	for k,v in pairs(t2) do
		if type(v) == "table" then
			if type(t1[k] or false) == "table" then
				tableMerge(t1[k] or {}, t2[k] or {})
			else
				t1[k] = v
			end
		else
			t1[k] = v
		end
	end
	return t1
end

local function loadI18n()
	local exist, res = pcall(require, "Module:Wikidata-i18n")
	if exist and next(res) ~= nil then
		tableMerge(i18n, res.i18n)
	end
end

loadI18n()

-- this function needs to be internationalised along with the above:
-- takes cardinal numer as a numeric and returns the ordinal as a string
-- we need three exceptions in English for 1st, 2nd, 3rd, 21st, .. 31st, etc.
local function makeOrdinal (cardinal)
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

local function printError(code)
	return '<span class="error">' .. (i18n.errors[code] or code) .. '</span>'
end

local function parseDateValue(timestamp, date_format, date_addon)
	local prefix_addon = i18n["datetime"]["prefix-addon"]
	local addon_sep = i18n["datetime"]["addon-sep"]
	local addon = ""

	-- check for negative date
	if string.sub(timestamp, 1, 1) == '-' then
		timestamp = '+' .. string.sub(timestamp, 2)
		addon = date_addon
	end
	local function d(f)
		local year_suffix
		local tstr = ""
		local lang_obj = mw.language.new(wiki.langcode)
		local f_parts = mw.text.split(f, 'Y', true)
		for idx, f_part in pairs(f_parts) do
			year_suffix = ''
			if string.match(f_part, "x[mijkot]$") then
				-- for non-Gregorian year
				f_part = f_part .. 'Y'
			elseif idx < #f_parts then
				-- supress leading zeros in year
				year_suffix = lang_obj:formatDate('Y', timestamp)
				year_suffix = string.gsub(year_suffix, '^0+', '', 1)
			end
			tstr = tstr .. lang_obj:formatDate(f_part, timestamp) .. year_suffix
		end
		if addon ~= "" and prefix_addon then
			return addon .. addon_sep .. tstr
		elseif addon ~= "" then
			return tstr .. addon_sep .. addon
		else
			return tstr
		end
	end
	local _date_format = i18n["datetime"]["format"][date_format]
	if _date_format ~= nil then
		return d(_date_format)
	else
		return printError("unknown-datetime-format")
	end
end

-- This local function combines the year/month/day/BC/BCE handling of parseDateValue{}
-- with the millennium/century/decade handling of formatDate()
local function parseDateFull(timestamp, precision, date_format, date_addon)
	local prefix_addon = i18n["datetime"]["prefix-addon"]
	local addon_sep = i18n["datetime"]["addon-sep"]
	local addon = ""

	-- check for negative date
	if string.sub(timestamp, 1, 1) == '-' then
		timestamp = '+' .. string.sub(timestamp, 2)
		addon = date_addon
	end

	-- get the next four characters after the + (should be the year now in all cases)
	-- ok, so this is dirty, but let's get it working first
	local intyear = tonumber(string.sub(timestamp, 2, 5))
	if intyear == 0 and precision <= 9 then
		return ""
	end

	-- precision is 10000 years or more
	if precision <= 5 then
		local factor = 10 ^ ((5 - precision) + 4)
		local y2 = math.ceil(math.abs(intyear) / factor)
		local relative = mw.ustring.gsub(i18n.datetime[precision], "$1", tostring(y2))
		if addon ~= "" then
			-- negative date
			relative = mw.ustring.gsub(i18n.datetime.beforenow, "$1", relative)
		else
			relative = mw.ustring.gsub(i18n.datetime.afternow, "$1", relative)
		end
		return relative
	end

	-- precision is decades (8), centuries (7) and millennia (6)
	local era, card
	if precision == 6 then
		card = math.floor((intyear - 1) / 1000) + 1
		era = mw.ustring.gsub(i18n.datetime[6], "$1", makeOrdinal(card))
	end
	if precision == 7 then
		card = math.floor((intyear - 1) / 100) + 1
		era = mw.ustring.gsub(i18n.datetime[7], "$1", makeOrdinal(card))
	end
	if precision == 8 then
		era = mw.ustring.gsub(i18n.datetime[8], "$1", tostring(math.floor(math.abs(intyear) / 10) * 10))
	end
	if era then
		if addon ~= "" then
			era = mw.ustring.gsub(mw.ustring.gsub(i18n.datetime.bc, '"', ""), "$1", era)
		else
			era = mw.ustring.gsub(mw.ustring.gsub(i18n.datetime.ad, '"', ""), "$1", era)
		end
		return era
	end

	local _date_format = i18n["datetime"]["format"][date_format]
	if _date_format ~= nil then
		-- check for precision is year and override supplied date_format
		if precision == 9 then
			_date_format = i18n["datetime"][9]
		end
		local year_suffix
		local tstr = ""
		local lang_obj = mw.language.new(wiki.langcode)
		local f_parts = mw.text.split(_date_format, 'Y', true)
		for idx, f_part in pairs(f_parts) do
			year_suffix = ''
			if string.match(f_part, "x[mijkot]$") then
				-- for non-Gregorian year
				f_part = f_part .. 'Y'
			elseif idx < #f_parts then
				-- supress leading zeros in year
				year_suffix = lang_obj:formatDate('Y', timestamp)
				year_suffix = string.gsub(year_suffix, '^0+', '', 1)
			end
			tstr = tstr .. lang_obj:formatDate(f_part, timestamp) .. year_suffix
		end
		local fdate
		if addon ~= "" and prefix_addon then
			fdate = addon .. addon_sep .. tstr
		elseif addon ~= "" then
			fdate = tstr .. addon_sep .. addon
		else
			fdate = tstr
		end

		return fdate
	else
		return printError("unknown-datetime-format")
	end
end

-- the "qualifiers" and "snaks" field have a respective "qualifiers-order" and "snaks-order" field
-- use these as the second parameter and this function instead of the built-in "pairs" function
-- to iterate over all qualifiers and snaks in the intended order.
local function orderedpairs(array, order)
	if not order then return pairs(array) end

	-- return iterator function
	local i = 0
	return function()
		i = i + 1
		if order[i] then
			return order[i], array[order[i]]
		end
	end
end

-- precision: 0 - billion years, 1 - hundred million years, ..., 6 - millennia, 7 - century, 8 - decade, 9 - year, 10 - month, 11 - day, 12 - hour, 13 - minute, 14 - second
local function normalizeDate(date)
	date = mw.text.trim(date, "+")
	-- extract year
	local yearstr = mw.ustring.match(date, "^\-?%d+")
	local year = tonumber(yearstr)
	-- remove leading zeros of year
	return year .. mw.ustring.sub(date, #yearstr + 1), year
end

local function formatDate(date, precision, timezone)
	precision = precision or 11
	local date, year = normalizeDate(date)
	if year == 0 and precision <= 9 then return "" end

	-- precision is 10000 years or more
	if precision <= 5 then
		local factor = 10 ^ ((5 - precision) + 4)
		local y2 = math.ceil(math.abs(year) / factor)
		local relative = mw.ustring.gsub(i18n.datetime[precision], "$1", tostring(y2))
		if year < 0 then
			relative = mw.ustring.gsub(i18n.datetime.beforenow, "$1", relative)
		else
			relative = mw.ustring.gsub(i18n.datetime.afternow, "$1", relative)
		end
		return relative
	end

	-- precision is decades, centuries and millennia
	local era
	if precision == 6 then era = mw.ustring.gsub(i18n.datetime[6], "$1", tostring(math.floor((math.abs(year) - 1) / 1000) + 1)) end
	if precision == 7 then era = mw.ustring.gsub(i18n.datetime[7], "$1", tostring(math.floor((math.abs(year) - 1) / 100) + 1)) end
	if precision == 8 then era = mw.ustring.gsub(i18n.datetime[8], "$1", tostring(math.floor(math.abs(year) / 10) * 10)) end
	if era then
		if year < 0 then era = mw.ustring.gsub(mw.ustring.gsub(i18n.datetime.bc, '"', ""), "$1", era)
		elseif year > 0 then era = mw.ustring.gsub(mw.ustring.gsub(i18n.datetime.ad, '"', ""), "$1", era) end
		return era
	end

	-- precision is year
	if precision == 9 then
		return year
	end

	-- precision is less than years
	if precision > 9 then
		--[[ the following code replaces the UTC suffix with the given negated timezone to convert the global time to the given local time
		timezone = tonumber(timezone)
		if timezone and timezone ~= 0 then
			timezone = -timezone
			timezone = string.format("%.2d%.2d", timezone / 60, timezone % 60)
			if timezone[1] ~= '-' then timezone = "+" .. timezone end
			date = mw.text.trim(date, "Z") .. " " .. timezone
		end
		]]--

		local formatstr = i18n.datetime[precision]
		if year == 0 then formatstr = mw.ustring.gsub(formatstr, i18n.datetime[9], "")
		elseif year < 0 then
			-- Mediawiki formatDate doesn't support negative years
			date = mw.ustring.sub(date, 2)
			formatstr = mw.ustring.gsub(formatstr, i18n.datetime[9], mw.ustring.gsub(i18n.datetime.bc, "$1", i18n.datetime[9]))
		elseif year > 0 and i18n.datetime.ad ~= "$1" then
			formatstr = mw.ustring.gsub(formatstr, i18n.datetime[9], mw.ustring.gsub(i18n.datetime.ad, "$1", i18n.datetime[9]))
		end
		return mw.language.new(wiki.langcode):formatDate(formatstr, date)
	end
end

local function printDatavalueEntity(data, parameter)
	-- data fields: entity-type [string], numeric-id [int, Wikidata id]
	local id

	if data["entity-type"] == "item" then id = "Q" .. data["numeric-id"]
	elseif data["entity-type"] == "property" then id = "P" .. data["numeric-id"]
	else return printError("unknown-entity-type")
	end

	if parameter then
		if parameter == "link" then
			local linkTarget = mw.wikibase.sitelink(id)
			local linkName = mw.wikibase.label(id)
			if linkTarget then
				-- if there is a local Wikipedia article link to it using the label or the article title
				return "[["_.._linkTarget_.._"|" .. (linkName or linkTarget) .. "]]"
			else
				-- if there is no local Wikipedia article output the label or link to the Wikidata object to let the user input a proper label
				if linkName then return linkName else return "[[:d:"_.._id_.._"|" .. id .. "]]" end
			end
		else
			return data[parameter]
		end
	else
		return mw.wikibase.label(id) or id
	end
end

local function printDatavalueTime(data, parameter)
	-- data fields: time [ISO 8601 time], timezone [int in minutes], before [int], after [int], precision [int], calendarmodel [wikidata URI]
	--   precision: 0 - billion years, 1 - hundred million years, ..., 6 - millennia, 7 - century, 8 - decade, 9 - year, 10 - month, 11 - day, 12 - hour, 13 - minute, 14 - second
	--   calendarmodel: e.g. http://www.wikidata.org/entity/Q1985727 for the proleptic Gregorian calendar or http://www.wikidata.org/wiki/Q11184 for the Julian calendar]
	if parameter then
		if parameter == "calendarmodel" then data.calendarmodel = mw.ustring.match(data.calendarmodel, "Q%d+") -- extract entity id from the calendar model URI
		elseif parameter == "time" then data.time = normalizeDate(data.time) end
		return data[parameter]
	else
		return formatDate(data.time, data.precision, data.timezone)
	end
end

local function printDatavalueMonolingualText(data, parameter)
	-- data fields: language [string], text [string]
	if parameter then
		return data[parameter]
	else
		local result = mw.ustring.gsub(mw.ustring.gsub(i18n.monolingualtext, "%%language", data["language"]), "%%text", data["text"])
		return result
	end
end

local function findClaims(entity, property)
	if not property or not entity or not entity.claims then return end

	if mw.ustring.match(property, "^P%d+$") then
		-- if the property is given by an id (P..) access the claim list by this id
		return entity.claims[property]
	else
		-- otherwise, iterate over all properties, fetch their labels and compare this to the given property name
		for k, v in pairs(entity.claims) do
			if mw.wikibase.label(k) == property then return v end
		end
		return
	end
end

local function getSnakValue(snak, parameter)
	if snak.snaktype == "value" then
		-- call the respective snak parser
		if snak.datavalue.type == "string" then return snak.datavalue.value
		elseif snak.datavalue.type == "globecoordinate" then return printDatavalueCoordinate(snak.datavalue.value, parameter)
		elseif snak.datavalue.type == "quantity" then return printDatavalueQuantity(snak.datavalue.value, parameter)
		elseif snak.datavalue.type == "time" then return printDatavalueTime(snak.datavalue.value, parameter)
		elseif snak.datavalue.type == "wikibase-entityid" then return printDatavalueEntity(snak.datavalue.value, parameter)
		elseif snak.datavalue.type == "monolingualtext" then return printDatavalueMonolingualText(snak.datavalue.value, parameter)
		end
	end
	return mw.wikibase.renderSnak(snak)
end

local function getQualifierSnak(claim, qualifierId)
	-- a "snak" is Wikidata terminology for a typed key/value pair
	-- a claim consists of a main snak holding the main information of this claim,
	-- as well as a list of attribute snaks and a list of references snaks
	if qualifierId then
		-- search the attribute snak with the given qualifier as key
		if claim.qualifiers then
			local qualifier = claim.qualifiers[qualifierId]
			if qualifier then return qualifier[1] end
		end
		return nil, printError("qualifier-not-found")
	else
		-- otherwise return the main snak
		return claim.mainsnak
	end
end

local function getValueOfClaim(claim, qualifierId, parameter)
	local error
	local snak
	snak, error = getQualifierSnak(claim, qualifierId)
	if snak then
		return getSnakValue(snak, parameter)
	else
		return nil, error
	end
end

local function getReferences(frame, claim)
	local result = ""
	-- traverse through all references
	for ref in pairs(claim.references or {}) do
		local refparts
		-- traverse through all parts of the current reference
		for snakkey, snakval in orderedpairs(claim.references[ref].snaks or {}, claim.references[ref]["snaks-order"]) do
			if refparts then refparts = refparts .. ", " else refparts = "" end
			-- output the label of the property of the reference part, e.g. "imported from" for P143
			refparts = refparts .. tostring(mw.wikibase.label(snakkey)) .. ": "
			-- output all values of this reference part, e.g. "German Wikipedia" and "English Wikipedia" if the referenced claim was imported from both sites
			for snakidx = 1, #snakval do
				if snakidx > 1 then refparts = refparts .. ", " end
				refparts = refparts .. getSnakValue(snakval[snakidx])
			end
		end
		if refparts then result = result .. frame:extensionTag("ref", refparts) end
	end
	return result
end


------------------------------------------------------------------------------
-- module global functions

if debug then
	function p.inspectI18n(frame)
		local val = i18n
		for _, key in pairs(frame.args) do
			key = mw.text.trim(key)
			val = val[key]
		end
		return val
	end
end

function p.descriptionIn(frame)
	local langcode = frame.args[1]
	local id = frame.args[2]	-- "id" must be nil, as access to other Wikidata objects is disabled in Mediawiki configuration
	-- return description of a Wikidata entity in the given language or the default language of this Wikipedia site
	return mw.wikibase.getEntityObject(id).descriptions[langcode or wiki.langcode].value
end

function p.labelIn(frame)
	local langcode = frame.args[1]
	local id = frame.args[2]	-- "id" must be nil, as access to other Wikidata objects is disabled in Mediawiki configuration
	-- return label of a Wikidata entity in the given language or the default language of this Wikipedia site
	return mw.wikibase.getEntityObject(id).labels[langcode or wiki.langcode].value
end

-- This is used to get a value, or a comma separated list of them if multiple values exist
p.getValue = function(frame)
	local propertyID = mw.text.trim(frame.args[1] or "")
	local input_parm = mw.text.trim(frame.args[2] or "")
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntityObject()
		local claims
		if entity and entity.claims then
			claims = entity.claims[propertyID]
		end
		if claims then
			-- if wiki-linked value output as link if possible
			if (claims[1] and claims[1].mainsnak.snaktype == "value" and claims[1].mainsnak.datavalue.type == "wikibase-entityid") then
				local out = {}
				for k, v in pairs(claims) do
					local sitelink = mw.wikibase.sitelink("Q" .. v.mainsnak.datavalue.value["numeric-id"])
					local label = mw.wikibase.label("Q" .. v.mainsnak.datavalue.value["numeric-id"])
					if label == nil then label = "Q" .. v.mainsnak.datavalue.value["numeric-id"] end

					if sitelink then
						out[#out + 1] = "[["_.._sitelink_.._"|" .. label .. "]]"
					else
						out[#out + 1] = "[[:d:Q"_.._v.mainsnak.datavalue.value["numeric-id"]_.._"|" .. label .. "]]<abbr title='" .. i18n["errors"]["local-article-not-found"] .. "'>[*]</abbr>"
					end
				end
				return table.concat(out, "、")
			else
				-- just return best values
				return entity:formatPropertyValues(propertyID).value
			end
		else
			return ""
		end
	else
		return input_parm
	end
end

-- Same as above, but uses the short name property for label if available.
p.getValueShortName = function(frame)
	local propertyID = mw.text.trim(frame.args[1] or "")
	local input_parm = mw.text.trim(frame.args[2] or "")
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntityObject()
		local claims
		if entity and entity.claims then
			claims = entity.claims[propertyID]
		end
		if claims then
			-- if wiki-linked value output as link if possible
			if (claims[1] and claims[1].mainsnak.snaktype == "value" and claims[1].mainsnak.datavalue.type == "wikibase-entityid") then
				local out = {}
				for k, v in pairs(claims) do
					local sitelink = mw.wikibase.sitelink("Q" .. v.mainsnak.datavalue.value["numeric-id"])
					local label
					local claimEntity = mw.wikibase.getEntity("Q" .. v.mainsnak.datavalue.value["numeric-id"])
					if claimEntity ~= nil then
						if claimEntity.claims.P1813 then
							for k2, v2 in pairs(claimEntity.claims.P1813) do
								for _, variant in ipairs{"zh", "zh-hans", "zh-hant", "zh-cn", "zh-hk", "zh-mo", "zh-sg", "zh-tw"} do
									if v2.mainsnak.datavalue.value.language == variant then
										label = v2.mainsnak.datavalue.value.text
									end
								end
							end
						end
					end
					if label == nil or label == "" then label = mw.wikibase.label("Q" .. v.mainsnak.datavalue.value["numeric-id"]) end
					if label == nil then label = "Q" .. v.mainsnak.datavalue.value["numeric-id"] end

					if sitelink then
						out[#out + 1] = "[["_.._sitelink_.._"|" .. label .. "]]"
					else
						out[#out + 1] = "[[:d:Q"_.._v.mainsnak.datavalue.value["numeric-id"]_.._"|" .. label .. "]]<abbr title='" .. i18n["errors"]["local-article-not-found"] .. "'>[*]</abbr>"
					end
				end
				return table.concat(out, "、")
			else
				-- just return best vakues
				return entity:formatPropertyValues(propertyID).value
			end
		else
			return ""
		end
	else
		return input_parm
	end
end

-- This is used to get a value, or a comma separated list of them if multiple values exist
-- from an arbitrary entry by using its QID.
-- Use : {{#invoke:Wikidata|getValueFromID|<ID>|<Property>|FETCH_WIKIDATA}}
-- E.g.: {{#invoke:Wikidata|getValueFromID|Q151973|P26|FETCH_WIKIDATA}} - to fetch value of 'spouse' (P26) from 'Richard Burton' (Q151973)
-- Please use sparingly - this is an *expensive call*.
p.getValueFromID = function(frame)
	local itemID = mw.text.trim(frame.args[1] or "")
	local propertyID = mw.text.trim(frame.args[2] or "")
	local input_parm = mw.text.trim(frame.args[3] or "")
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntity(itemID)
		local claims
		if entity and entity.claims then
			claims = entity.claims[propertyID]
		end
		if claims then
			-- if wiki-linked value output as link if possible
			if (claims[1] and claims[1].mainsnak.snaktype == "value" and claims[1].mainsnak.datavalue.type == "wikibase-entityid") then
				local out = {}
				for k, v in pairs(claims) do
					local sitelink = mw.wikibase.sitelink("Q" .. v.mainsnak.datavalue.value["numeric-id"])
					local label = mw.wikibase.label("Q" .. v.mainsnak.datavalue.value["numeric-id"])
					if label == nil then label = "Q" .. v.mainsnak.datavalue.value["numeric-id"] end

					if sitelink then
						out[#out + 1] = "[["_.._sitelink_.._"|" .. label .. "]]"
					else
						out[#out + 1] = "[[:d:Q"_.._v.mainsnak.datavalue.value["numeric-id"]_.._"|" .. label .. "]]<abbr title='" .. i18n["errors"]["local-article-not-found"] .. "'>[*]</abbr>"
					end
				end
				return table.concat(out, "、")
			else
				return entity:formatPropertyValues(propertyID).value
			end
		else
			return ""
		end
	else
		return input_parm
	end
end

p.getQualifierValue = function(frame)
	local propertyID = mw.text.trim(frame.args[1] or "")
	local qualifierID = mw.text.trim(frame.args[2] or "")
	local input_parm = mw.text.trim(frame.args[3] or "")
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntityObject()
		if entity.claims[propertyID] ~= nil then
			local out = {}
			for k, v in pairs(entity.claims[propertyID]) do
				for k2, v2 in pairs(v.qualifiers[qualifierID]) do
					if v2.snaktype == 'value' then
						if (mw.wikibase.sitelink("Q" .. v2.datavalue.value["numeric-id"])) then
							out[#out + 1] = "[["_.._mw.wikibase.sitelink("Q"_.._v2.datavalue.value["numeric-id"])_.._"|" .. mw.wikibase.sitelink("Q" .. v2.datavalue.value["numeric-id"]) .. "]]"
						else
							out[#out + 1] = "[[:d:Q"_.._v2.datavalue.value["numeric-id"]_.._"|" .. mw.wikibase.label("Q" .. v2.datavalue.value["numeric-id"]) .. "]]<abbr title='" .. i18n["errors"]["local-article-not-found"] .. "'>[*]</abbr>"
						end
					end
				end
			end
			return table.concat(out, "、")
		else
			return ""
		end
	else
		return input_parm
	end
end

-- This is used to get a value like 'male' (for property p21) which won't be linked and numbers without the thousand separators
p.getRawValue = function(frame)
	local propertyID = mw.text.trim(frame.args[1] or "")
	local input_parm = mw.text.trim(frame.args[2] or "")
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntityObject()
		local claims
		if entity and entity.claims then claims = entity.claims[propertyID] end
		if claims then
			local result = entity:formatPropertyValues(propertyID, mw.wikibase.entity.claimRanks).value

			-- if number type: remove thousand separators, bounds and units
			if (claims[1] and claims[1].mainsnak.snaktype == "value" and claims[1].mainsnak.datavalue.type == "quantity") then
				result = mw.ustring.gsub(result, "(%d),(%d)", "%1%2")
				result = mw.ustring.gsub(result, "(%d)±.*", "%1")
			end
			return result
		else
			return ""
		end
	else
		return input_parm
	end
end

-- This is used to get the unit name for the numeric value returned by getRawValue
p.getUnits = function(frame)
	local propertyID = mw.text.trim(frame.args[1] or "")
	local input_parm = mw.text.trim(frame.args[2] or "")
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntityObject()
		local claims
		if entity and entity.claims then claims = entity.claims[propertyID] end
		if claims then
			local result = entity:formatPropertyValues(propertyID, mw.wikibase.entity.claimRanks).value
			if (claims[1] and claims[1].mainsnak.snaktype == "value" and claims[1].mainsnak.datavalue.type == "quantity") then
				result = mw.ustring.sub(result, mw.ustring.find(result, " ")+1, -1)
			end
			return result
		else
			return ""
		end
	else
		return input_parm
	end
end

-- This is used to get the unit's QID to use with the numeric value returned by getRawValue
p.getUnitID = function(frame)
	local propertyID = mw.text.trim(frame.args[1] or "")
	local input_parm = mw.text.trim(frame.args[2] or "")
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntityObject()
		local claims
		if entity and entity.claims then claims = entity.claims[propertyID] end
		if claims then
			local result
			if (claims[1] and claims[1].mainsnak.snaktype == "value" and claims[1].mainsnak.datavalue.type == "quantity") then
				-- get the url for the unit entry on Wikidata:
				result = claims[1].mainsnak.datavalue.value.unit
				-- and just reurn the last bit from "Q" to the end (which is the QID):
				result = mw.ustring.sub(result, mw.ustring.find(result, "Q"), -1)
			end
			return result
		else
			return ""
		end
	else
		return input_parm
	end
end

p.getRawQualifierValue = function(frame)
	local propertyID = mw.text.trim(frame.args[1] or "")
	local qualifierID = mw.text.trim(frame.args[2] or "")
	local input_parm = mw.text.trim(frame.args[3] or "")
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntityObject()
		if entity.claims[propertyID] ~= nil then
			local out = {}
			for k, v in pairs(entity.claims[propertyID]) do
				for k2, v2 in pairs(v.qualifiers[qualifierID]) do
					if v2.snaktype == 'value' then
						if v2.datavalue.value["numeric-id"] then
							out[#out + 1] = mw.wikibase.label("Q" .. v2.datavalue.value["numeric-id"])
						else
							out[#out + 1] = v2.datavalue.value
						end
					end
				end
			end
			local ret = table.concat(out, "、")
			return string.upper(string.sub(ret, 1, 1)) .. string.sub(ret, 2)
		else
			return ""
		end
	else
		return input_parm
	end
end

-- This is used to get a date value for date_of_birth (P569), etc. which won't be linked
-- Dates and times are stored in ISO 8601 format (sort of).
-- At present the local formatDate(date, precision, timezone) function doesn't handle timezone
-- So I'll just supply "Z" in the call to formatDate below:
p.getDateValue = function(frame)
	local propertyID = mw.text.trim(frame.args[1] or "")
	local input_parm = mw.text.trim(frame.args[2] or "")
	local date_format = mw.text.trim(frame.args[3] or i18n["datetime"]["default-format"])
	local date_addon = mw.text.trim(frame.args[4] or i18n["datetime"]["default-addon"])
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntityObject()
		if entity.claims[propertyID] ~= nil then
			local out = {}
			for k, v in pairs(entity.claims[propertyID]) do
				if v.mainsnak.datavalue.type == 'time' then
					local timestamp = v.mainsnak.datavalue.value.time
					local dateprecision = v.mainsnak.datavalue.value.precision
					-- A year can be stored like this: "+1872-00-00T00:00:00Z",
					-- which is processed here as if it were the day before "+1872-01-01T00:00:00Z",
					-- and that's the last day of 1871, so the year is wrong.
					-- So fix the month 0, day 0 timestamp to become 1 January instead:
					timestamp = timestamp:gsub("%-00%-00T", "-01-01T")
					out[#out + 1] = parseDateFull(timestamp, dateprecision, date_format, date_addon)
				end
			end
			return table.concat(out, "、")
		else
			return ""
		end
	else
		return input_parm
	end
end

p.getQualifierDateValue = function(frame)
	local propertyID = mw.text.trim(frame.args[1] or "")
	local qualifierID = mw.text.trim(frame.args[2] or "")
	local input_parm = mw.text.trim(frame.args[3] or "")
	local date_format = mw.text.trim(frame.args[4] or i18n["datetime"]["default-format"])
	local date_addon = mw.text.trim(frame.args[5] or i18n["datetime"]["default-addon"])
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntityObject()
		if entity.claims[propertyID] ~= nil then
			local out = {}
			for k, v in pairs(entity.claims[propertyID]) do
				for k2, v2 in pairs(v.qualifiers[qualifierID]) do
					if v2.snaktype == 'value' then
						local timestamp = v2.datavalue.value.time
						out[#out + 1] = parseDateValue(timestamp, date_format, date_addon)
					end
				end
			end
			return table.concat(out, "、")
		else
			return ""
		end
	else
		return input_parm
	end
end

-- This is used to fetch all of the images with a particular property, e.g. image (P18), Gene Atlas Image (P692), etc.
-- Parameters are | propertyID | value / FETCH_WIKIDATA / nil | separator (default=space) | size (default=frameless)
-- It will return a standard wiki-markup [[File:Filename|size]] for each image with a selectable size and separator (which may be html)
-- e.g. {{#invoke:Wikidata|getImages|P18|FETCH_WIKIDATA}}
-- e.g. {{#invoke:Wikidata|getImages|P18|FETCH_WIKIDATA|<br>|250px}}
-- If a property is chosen that is not of type "commonsMedia", it will return empty text.
p.getImages = function(frame)
	local propertyID = mw.text.trim(frame.args[1] or "")
	local input_parm = mw.text.trim(frame.args[2] or "")
	local sep = mw.text.trim(frame.args[3] or " ")
	local imgsize = mw.text.trim(frame.args[4] or "frameless")
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntityObject()
		local claims
		if entity and entity.claims then
			claims = entity.claims[propertyID]
		end
		if claims then
			if (claims[1] and claims[1].mainsnak.datatype == "commonsMedia") then
				local out = {}
				for k, v in pairs(claims) do
					local filename = v.mainsnak.datavalue.value
					out[#out + 1] = "[[File:"_.._filename_.._"|" .. imgsize .. "]]"
				end
				return table.concat(out, sep)
			else
				return ""
			end
		else
			return ""
		end
	else
		return input_parm
	end
end

-- This is used to get the TA98 (Terminologia Anatomica first edition 1998) values like 'A01.1.00.005' (property P1323)
-- which are then linked to http://www.unifr.ch/ifaa/Public/EntryPage/TA98%20Tree/Entity%20TA98%20EN/01.1.00.005%20Entity%20TA98%20EN.htm
-- uses the newer mw.wikibase calls instead of directly using the snaks
-- formatPropertyValues returns a table with the P1323 values concatenated with ", " so we have to split them out into a table in order to construct the return string
p.getTAValue = function(frame)
	local ent = mw.wikibase.getEntityObject()
	local props = ent:formatPropertyValues('P1323')
	local out = {}
	local t = {}
	for k, v in pairs(props) do
		if k == 'value' then
			t = mw.text.split( v, ", ")
			for k2, v2 in pairs(t) do
				out[#out + 1] = "[http://www.unifr.ch/ifaa/Public/EntryPage/TA98%20Tree/Entity%20TA98%20EN/" .. string.sub(v2, 2) .. "%20Entity%20TA98%20EN.htm " .. v2 .. "]"
			end
		end
	end
	local ret = table.concat(out, "<br> ")
	if #ret == 0 then
		ret = "Invalid TA"
	end
	return ret
end

--[[
This is used to return an image legend from Wikidata
image is property P18
image legend is property P2096

Call as {{#invoke:Wikidata |getImageLegend | <PARAMETER> | lang=<ISO-639code> |id=<QID>}}
Returns PARAMETER, unless it is equal to "FETCH_WIKIDATA", from Item QID (expensive call)
If QID is omitted or blank, the current article is used (not an expensive call)
If lang is omitted, it uses the local wiki language, otherwise it uses the provided ISO-639 language code
ISO-639: https://docs.oracle.com/cd/E13214_01/wli/docs92/xref/xqisocodes.html#wp1252447

Ranks are: 'preferred' > 'normal'
This returns the label from the first image with 'preferred' rank
Or the label from the first image with 'normal' rank if preferred returns nothing
Ranks: https://www.mediawiki.org/wiki/Extension:Wikibase_Client/Lua
]]

p.getImageLegend = function(frame)
	-- look for named parameter id; if it's blank make it nil
	local id = frame.args.id
	if id and (#id == 0) then
		id = nil
	end

	-- look for named parameter lang
	-- it should contain a two-character ISO-639 language code
	-- if it's blank fetch the language of the local wiki
	local lang = frame.args.lang
	if (not lang) or (#lang < 2) then
		lang = mw.language.getContentLanguage().code
	end

	-- first unnamed parameter is the local parameter, if supplied
	local input_parm = mw.text.trim(frame.args[1] or "")
	if input_parm == "FETCH_WIKIDATA" then
		local ent = mw.wikibase.getEntityObject(id)
		local imgs
		if ent and ent.claims then
			imgs = ent.claims.P18
		end
		local imglbl
		if imgs then
			-- look for an image with 'preferred' rank
			for k1, v1 in pairs(imgs) do
				if v1.rank == "preferred" and v1.qualifiers and v1.qualifiers.P2096 then
					local imglbls = v1.qualifiers.P2096
					for k2, v2 in pairs(imglbls) do
						if v2.datavalue.value.language == lang then
							imglbl = v2.datavalue.value.text
							break
						end
					end
				end
			end
			-- if we don't find one, look for an image with 'normal' rank
			if (not imglbl) then
				for k1, v1 in pairs(imgs) do
					if v1.rank == "normal" and v1.qualifiers and v1.qualifiers.P2096 then
						local imglbls = v1.qualifiers.P2096
						for k2, v2 in pairs(imglbls) do
							if v2.datavalue.value.language == lang then
								imglbl = v2.datavalue.value.text
								break
							end
						end
					end
				end
			end
		end
		return imglbl
	else
		return input_parm
	end
end

-- This is used to get the QIDs of all of the values of a property, as a comma separated list if multiple values exist
-- Usage: {{#invoke:Wikidata |getPropertyIDs |<PropertyID> |FETCH_WIKIDATA}}
-- Usage: {{#invoke:Wikidata |getPropertyIDs |<PropertyID> |<InputParameter> |qid=<QID>}}

p.getPropertyIDs = function(frame)
	local propertyID = mw.text.trim(frame.args[1] or "")
	local input_parm = mw.text.trim(frame.args[2] or "")
	-- can take a named parameter |qid which is the Wikidata ID for the article. This will not normally be used.
	local qid = frame.args.qid
	if qid and (#qid == 0) then qid = nil end
	if input_parm == "FETCH_WIKIDATA" then
		local entity = mw.wikibase.getEntityObject(qid)
		local propclaims
		if entity and entity.claims then
			propclaims = entity.claims[propertyID]
		end
		if propclaims then
			-- if wiki-linked value collect the QID in a table
			if (propclaims[1] and propclaims[1].mainsnak.snaktype == "value" and propclaims[1].mainsnak.datavalue.type == "wikibase-entityid") then
				local out = {}
				for k, v in pairs(propclaims) do
					out[#out + 1] = "Q" .. v.mainsnak.datavalue.value["numeric-id"]
				end
				return table.concat(out, "、")
			else
				-- not a wikibase-entityid, so return empty
				return ""
			end
		else
			-- no claim, so return empty
			return ""
		end
	else
		return input_parm
	end
end

-- returns the page id (Q...) of the current page or nothing of the page is not connected to Wikidata
function p.pageId(frame)
	local entity = mw.wikibase.getEntityObject()
	if not entity then return nil else return entity.id end
end

function p.claim(frame)
	local property = frame.args[1] or ""
	local id = frame.args["id"]	-- "id" must be nil, as access to other Wikidata objects is disabled in Mediawiki configuration
	local qualifierId = frame.args["qualifier"]
	local parameter = frame.args["parameter"]
	local list = frame.args["list"]
	local references = frame.args["references"]
	local showerrors = frame.args["showerrors"]
	local default = frame.args["default"]
	if default then showerrors = nil end

	-- get wikidata entity
	local entity = mw.wikibase.getEntityObject(id)
	if not entity then
		if showerrors then return printError("entity-not-found") else return default end
	end
	-- fetch the first claim of satisfying the given property
	local claims = findClaims(entity, property)
	if not claims or not claims[1] then
		if showerrors then return printError("property-not-found") else return default end
	end

	-- get initial sort indices
	local sortindices = {}
	for idx in pairs(claims) do
		sortindices[#sortindices + 1] = idx
	end
	-- sort by claim rank
	local comparator = function(a, b)
		local rankmap = { deprecated = 2, normal = 1, preferred = 0 }
		local ranka = rankmap[claims[a].rank or "normal"] .. string.format("%08d", a)
		local rankb = rankmap[claims[b].rank or "normal"] .. string.format("%08d", b)
		return ranka < rankb
	end
	table.sort(sortindices, comparator)

	local result
	local error
	if list then
		local value
		-- iterate over all elements and return their value (if existing)
		result = {}
		for idx in pairs(claims) do
			local claim = claims[sortindices[idx]]
			value, error = getValueOfClaim(claim, qualifierId, parameter)
			if not value and showerrors then value = error end
			if value and references then value = value .. getReferences(frame, claim) end
			result[#result + 1] = value
		end
		result = table.concat(result, list)
	else
		-- return first element
		local claim = claims[sortindices[1]]
		result, error = getValueOfClaim(claim, qualifierId, parameter)
		if result and references then result = result .. getReferences(frame, claim) end
	end

	if result then return result else
		if showerrors then return error else return default end
	end
end

-- look into entity object
function p.ViewSomething(frame)
	local f = (frame.args[1] or frame.args.id) and frame or frame:getParent()
	local id = f.args.id
	if id and (#id == 0) then
		id = nil
	end
	local data = mw.wikibase.getEntityObject(id)
	if not data then
		return nil
	end

	local i = 1
	while true do
		local index = f.args[i]
		if not index then
			if type(data) == "table" then
				return mw.text.jsonEncode(data, mw.text.JSON_PRESERVE_KEYS + mw.text.JSON_PRETTY)
			else
				return tostring(data)
			end
		end

		data = data[index] or data[tonumber(index)]
		if not data then
			return
		end

		i = i + 1
	end
end

-- getting sitelink of a given wiki
function p.getSiteLink(frame)
	local f = frame.args[1]
	local entity = mw.wikibase.getEntity()
	if not entity then
		return
	end
	local link = entity:getSitelink( f )
	if not link then
		return
	end
	return link
end

function p.Dump(frame)
	local f = (frame.args[1] or frame.args.id) and frame or frame:getParent()
	local data = mw.wikibase.getEntityObject(f.args.id)
	if not data then
		return i18n.warnDump
	end

	local i = 1
	while true do
		local index = f.args[i]
		if not index then
			return "<pre>"..mw.dumpObject(data).."</pre>".. i18n.warnDump
		end

		data = data[index] or data[tonumber(index)]
		if not data then
			return i18n.warnDump
		end

		i = i + 1
	end
end

return p