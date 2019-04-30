-- Original module located at [[:en:Module:Wd|:en:Module:Wd]], [[:en:Module:Wd/i18n|:en:Module:Wd/i18n]] and [[:en:Module:Wd/aliasesP|:en:Module:Wd/aliasesP]].

local p = {}
local arg = ...
local i18n

function loadSubmodules(frame)
	local title
	
	if frame then
		-- current module invoked by page/template, get its title from frame
		title = frame:getTitle()
	else
		-- current module included by other module, get its title from ...
		title = arg
	end
	
	i18n = i18n or require(title .. "/i18n")
	p.aliasesP = p.aliasesP or mw.loadData(title .. "/aliasesP")
end

p.claimCommands = {
	property   = "property",
	properties = "properties",
	qualifier  = "qualifier",
	qualifiers = "qualifiers",
	reference  = "reference",
	references = "references"
}

p.generalCommands = {
	label      = "label",
	title      = "title",
	alias      = "alias",
	aliases    = "aliases",
	badge      = "badge",
	badges     = "badges"
}

p.flags = {
	linked        = "linked",
	short         = "short",
	raw           = "raw",
	multilanguage = "multilanguage",
	unit          = "unit",
	-------------
	preferred     = "preferred",
	normal        = "normal",
	deprecated    = "deprecated",
	best          = "best",
	future        = "future",
	current       = "current",
	former        = "former",
	edit          = "edit",
	editAtEnd     = "edit@end",
	mdy           = "mdy",
	single        = "single",
	sourced       = "sourced"
}

p.args = {
	eid = "eid"
}

local aliasesQ = {
	percentage              = "Q11229",
	prolepticJulianCalendar = "Q1985786",
	citeWeb                 = "Q5637226",
	citeQ                   = "Q22321052"
}

local parameters = {
	property  = "%p",
	qualifier = "%q",
	reference = "%r",
	alias     = "%a",
	badge     = "%b",
	separator = "%s",
	general   = "%x"
}

local formats = {
	property              = "%p[%s][%r]",
	qualifier             = "%q[%s][%r]",
	reference             = "%r",
	propertyWithQualifier = "%p[ <span style=\"font-size:85%\">(%q)</span>][%s][%r]",
	alias                 = "%a[%s]",
	badge                 = "%b[%s]"
}

local hookNames = {              -- {level_1, level_2}
	[parameters.property]         = {"getProperty"},
	[parameters.reference]        = {"getReferences", "getReference"},
	[parameters.qualifier]        = {"getAllQualifiers"},
	[parameters.qualifier.."\\d"] = {"getQualifiers", "getQualifier"},
	[parameters.alias]            = {"getAlias"},
	[parameters.badge]            = {"getBadge"}
}

-- default value objects, should NOT be mutated but instead copied
local defaultSeparators = {
	["sep"]      = {" "},
	["sep%s"]    = {","},
	["sep%q"]    = {"; "},
	["sep%q\\d"] = {", "},
	["sep%r"]    = nil,  -- none
	["punc"]     = nil   -- none
}

local rankTable = {
	["preferred"]  = 1,
	["normal"]     = 2,
	["deprecated"] = 3
}

local Config = {}
Config.__index = Config

-- allows for recursive calls
function Config.new()
	local cfg = {}
	setmetatable(cfg, Config)
	
	cfg.separators = {
		-- single value objects wrapped in arrays so that we can pass by reference
		["sep"]   = {copyTable(defaultSeparators["sep"])},
		["sep%s"] = {copyTable(defaultSeparators["sep%s"])},
		["sep%q"] = {copyTable(defaultSeparators["sep%q"])},
		["sep%r"] = {copyTable(defaultSeparators["sep%r"])},
		["punc"]  = {copyTable(defaultSeparators["punc"])}
	}
	
	cfg.entity = nil
	cfg.entityID = nil
	cfg.propertyID = nil
	cfg.propertyValue = nil
	cfg.qualifierIDs = {}
	cfg.qualifierIDsAndValues = {}
	
	cfg.bestRank = true
	cfg.ranks = {true, true, false}  -- preferred = true, normal = true, deprecated = false
	cfg.foundRank = #cfg.ranks
	cfg.flagBest = false
	cfg.flagRank = false
	
	cfg.periods = {true, true, true}  -- future = true, current = true, former = true
	cfg.flagPeriod = false
	
	cfg.mdyDate = false
	cfg.singleClaim = false
	cfg.sourcedOnly = false
	cfg.editable = false
	cfg.editAtEnd = false
	
	cfg.inSitelinks = false
	
	cfg.langCode = mw.language.getContentLanguage().code
	cfg.langName = mw.language.fetchLanguageName(cfg.langCode, cfg.langCode)
	cfg.langObj = mw.language.new(cfg.langCode)
	
	-- somewhat reliable way of determining global site ID in the absence of a library function, targeting the Wikipedia project (i.e. appending "wiki")
	cfg.siteID = (function() for i,v in pairs(mw.site.interwikiMap("local")) do if v.isCurrentWiki and i~="w" then return mw.ustring.gsub(i,"-","_").."wiki" end end end)()
	
	cfg.states = {}
	cfg.states.qualifiersCount = 0
	cfg.curState = nil
	
	cfg.prefetchedRefs = nil
	
	return cfg
end

local State = {}
State.__index = State

function State.new(cfg)
	local stt = {}
	setmetatable(stt, State)
	
	stt.conf = cfg
	
	stt.results = {}
	
	stt.parsedFormat = {}
	stt.separator = {}
	stt.movSeparator = {}
	stt.puncMark = {}
	
	stt.linked = false
	stt.rawValue = false
	stt.shortName = false
	stt.anyLanguage = false
	stt.unitOnly = false
	stt.singleValue = false
	
	return stt
end

function replaceAlias(id)
	if p.aliasesP[id] then
		id = p.aliasesP[id]
	end
	
	return id
end

function errorText(code, param)
	local text = i18n["errors"][code]
	if param then text = mw.ustring.gsub(text, "$1", param) end
	return text
end

function throwError(errorMessage, param)
	error(errorText(errorMessage, param))
end

function replaceDecimalMark(num)
	return mw.ustring.gsub(num, "[.]", i18n['numeric']['decimal-mark'], 1)
end

function padZeros(num, numDigits)
	local numZeros
	local negative = false
	
	if num < 0 then
		negative = true
		num = num * -1
	end
	
	num = tostring(num)
	numZeros = numDigits - num:len()
	
	for i = 1, numZeros do
		num = "0"..num
	end
	
	if negative then
		num = "-"..num
	end
	
	return num
end

function replaceSpecialChar(chr)
	if chr == '_' then
		-- replace underscores with spaces
		return ' '
	else
		return chr
	end
end

function replaceSpecialChars(str)
	local chr
	local esc = false
	local strOut = ""
	
	for i = 1, #str do
		chr = str:sub(i,i)
		
		if not esc then
			if chr == '\\' then
				esc = true
			else
				strOut = strOut .. replaceSpecialChar(chr)
			end
		else
			strOut = strOut .. chr
			esc = false
		end
	end
	
	return strOut
end

function buildWikilink(target, label)
	if not label or target == label then
		return "[["_.._target_.._"|" .. target .. "]]"
	else
		return "[["_.._target_.._"|" .. label .. "]]"
	end
end

-- used to make frame.args mutable, to replace #frame.args (which is always 0)
-- with the actual amount and to simply copy tables
function copyTable(tIn)
	if not tIn then
		return nil
	end
	
	local tOut = {}
	
	for i, v in pairs(tIn) do
		tOut[i] = v
	end
	
	return tOut
end

-- used to merge output arrays together;
-- note that it currently mutates the first input array
function mergeArrays(a1, a2)
	for i = 1, #a2 do
		a1[#a1 + 1] = a2[i]
	end
	
	return a1
end

function split(str, del)
	local out = {}
	local i, j = str:find(del)
	
	if i and j then
		out[1] = str:sub(1, i - 1)
		out[2] = str:sub(j + 1)
	else
		out[1] = str
	end
	
	return out
end

function parseWikidataURL(url)
	local id
	
	if url:match('^http[s]?://') then
		id = split(url, "Q")
		
		if id[2] then
			return "Q" .. id[2]
		end
	end
	
	return nil
end

function parseDate(dateStr, precision)
	precision = precision or "d"
	
	local i, j, index, ptr
	local parts = {nil, nil, nil}
	
	if dateStr == nil then
		return parts[1], parts[2], parts[3]  -- year, month, day
	end
	
	-- 'T' for snak values, '/' for outputs with '/Julian' attached
	i, j = dateStr:find("[T/]")
	
	if i then
		dateStr = dateStr:sub(1, i-1)
	end
	
	local from = 1
	
	if dateStr:sub(1,1) == "-" then
		-- this is a negative number, look further ahead
		from = 2
	end
	
	index = 1
	ptr = 1
	
	i, j = dateStr:find("-", from)
	
	if i then
		-- year
		parts[index] = tonumber(mw.ustring.gsub(dateStr:sub(ptr, i-1), "^\+(.+)$", "%1"), 10)  -- remove '+' sign (explicitly give base 10 to prevent error)
		
		if parts[index] == -0 then
			parts[index] = tonumber("0")  -- for some reason, 'parts[index] = 0' may actually store '-0', so parse from string instead
		end
		
		if precision == "y" then
			-- we're done
			return parts[1], parts[2], parts[3]  -- year, month, day
		end
		
		index = index + 1
		ptr = i + 1
		
		i, j = dateStr:find("-", ptr)
		
		if i then
			-- month
			parts[index] = tonumber(dateStr:sub(ptr, i-1), 10)
			
			if precision == "m" then
				-- we're done
				return parts[1], parts[2], parts[3]  -- year, month, day
			end
			
			index = index + 1
			ptr = i + 1
		end
	end
	
	if dateStr:sub(ptr) ~= "" then
		-- day if we have month, month if we have year, or year
		parts[index] = tonumber(dateStr:sub(ptr), 10)
	end
	
	return parts[1], parts[2], parts[3]  -- year, month, day
end

function datePrecedesDate(aY, aM, aD, bY, bM, bD)
	if aY == nil or bY == nil then
		return nil
	end
	aM = aM or 1
	aD = aD or 1
	bM = bM or 1
	bD = bD or 1
	
	if aY < bY then
		return true
	end
	
	if aY > bY then
		return false
	end
	
	if aM < bM then
		return true
	end
	
	if aM > bM then
		return false
	end
	
	if aD < bD then
		return true
	end
	
	return false
end

function getHookName(param, index)
	if hookNames[param] then
		return hookNames[param][index]
	elseif param:len() > 2 then
		return hookNames[param:sub(1, 2).."\\d"][index]
	else
		return nil
	end
end

function alwaysTrue()
	return true
end

-- The following function parses a format string.
--
-- The example below shows how a parsed string is structured in memory.
-- Variables other than 'str' and 'child' are left out for clarity's sake.
--
-- Example:
-- "A %p B [%s[%q1]] C [%r] D"
--
-- Structure:
-- [
--   {
--     str = "A "
--   },
--   {
--     str = "%p"
--   },
--   {
--     str = " B ",
--     child =
--     [
--       {
--         str = "%s",
--         child =
--         [
--           {
--             str = "%q1"
--           }
--         ]
--       }
--     ]
--   },
--   {
--     str = " C ",
--     child =
--     [
--       {
--         str = "%r"
--       }
--     ]
--   },
--   {
--     str = " D"
--   }
-- ]
--
function parseFormat(str)
	local chr, esc, param, root, cur, prev, new
	local params = {}
	
	local function newObject(array)
		local obj = {}  -- new object
		obj.str = ""
		
		array[#array + 1] = obj  -- array{object}
		obj.parent = array
		
		return obj
	end
	
	local function endParam()
		if param > 0 then
			if cur.str ~= "" then
				cur.str = "%"..cur.str
				cur.param = true
				params[cur.str] = true
				cur.parent.req[cur.str] = true
				prev = cur
				cur = newObject(cur.parent)
			end
			param = 0
		end
	end
	
	root = {}  -- array
	root.req = {}
	cur = newObject(root)
	prev = nil
	
	esc = false
	param = 0
	
	for i = 1, #str do
		chr = str:sub(i,i)
		
		if not esc then
			if chr == '\\' then
				endParam()
				esc = true
			elseif chr == '%' then
				endParam()
				if cur.str ~= "" then
					cur = newObject(cur.parent)
				end
				param = 2
			elseif chr == '[' then
				endParam()
				if prev and cur.str == "" then
					table.remove(cur.parent)
					cur = prev
				end
				cur.child = {}  -- new array
				cur.child.req = {}
				cur.child.parent = cur
				cur = newObject(cur.child)
			elseif chr == ']' then
				endParam()
				if cur.parent.parent then
					new = newObject(cur.parent.parent.parent)
					if cur.str == "" then
						table.remove(cur.parent)
					end
					cur = new
				end
			else
				if param > 1 then
					param = param - 1
				elseif param == 1 then
					if not chr:match('%d') then
						endParam()
					end
				end
				
				cur.str = cur.str .. replaceSpecialChar(chr)
			end
		else
			cur.str = cur.str .. chr
			esc = false
		end
		
		prev = nil
	end
	
	endParam()
	
	-- make sure that at least one required parameter has been defined
	if not next(root.req) then
		throwError("missing-required-parameter")
	end
	
	-- make sure that the separator parameter "%s" is not amongst the required parameters
	if root.req[parameters.separator] then
		throwError("extra-required-parameter", parameters.separator)
	end
	
	return root, params
end

function sortOnRank(claims)
	local rankPos
	local ranks = {{}, {}, {}, {}}  -- preferred, normal, deprecated, (default)
	local sorted = {}
	
	for i, v in ipairs(claims) do
		rankPos = rankTable[v.rank] or 4
		ranks[rankPos][#ranks[rankPos] + 1] = v
	end
	
	sorted = ranks[1]
	sorted = mergeArrays(sorted, ranks[2])
	sorted = mergeArrays(sorted, ranks[3])
	
	return sorted
end

-- if id == nil then item connected to current page is used
function Config:getLabel(id, raw, link, short)
	local label = nil
	local title = nil
	local prefix= ""
	local lang
	
	if not id then
		id = mw.wikibase.getEntityIdForCurrentPage()
		
		if not id then
			return ""
		end
	end
	
	id = id:upper()  -- just to be sure
	
	if raw then
		-- check if given id actually exists
		if mw.wikibase.getEntity(id) then
			label = id
			
			if id:sub(1,1) == "P" then
				prefix = "Property:"
			end
		end
		
		prefix = "d:" .. prefix
		
		title = label  -- may be nil
	else
		-- try short name first if requested
		if short then
			label = p._property({p.aliasesP.shortName, [p.args.eid] = id})  -- get short name
			
			if label == "" then
				label = nil
			end
		end
		
		-- get label
		if not label then
			label, lang = mw.wikibase.getLabelWithLang(id)
			
			-- don't allow language fallback
			if lang ~= self.langCode then
				label = nil
			end
		end
	end
	
	if not label then
		label = ""
	elseif link then
		-- build a link if requested
		if not title then
			if id:sub(1,1) == "Q" then
				title = mw.wikibase.sitelink(id)
			elseif id:sub(1,1) == "P" then
				-- properties have no sitelink, link to Wikidata instead
				title = id
				prefix = "d:Property:"
			end
		end
		
		if title then
			label = buildWikilink(prefix .. title, label)
		end
	end
	
	return label
end

function Config:getEditIcon()
	local value = ""
	local prefix = ""
	local front = " "
	local back = ""
	
	if self.entityID:sub(1,1) == "P" then
		prefix = "Property:"
	end
	
	if self.editAtEnd then
		front = '<span style="float:'
		
		if self.langObj:isRTL() then
			front = front .. 'left'
		else
			front = front .. 'right'
		end
		
		front = front .. '">'
		back = '</span>'
	end
	
	value = "[[File:Blue pencil.svg|frameless|text-top|10px|alt=" .. i18n['info']['edit-on-wikidata'] .. "|link=https://www.wikidata.org/wiki/" .. prefix .. self.entityID .. "?uselang=" .. self.langCode
	
	if self.propertyID then
		value = value .. "#" .. self.propertyID
	elseif self.inSitelinks then
		value = value .. "#sitelinks-wikipedia"
	end
	
	value = value .. "|" .. i18n['info']['edit-on-wikidata'] .. "]]"
	
	return front .. value .. back
end

-- used to create the final output string when it's all done, so that for references the
-- function extensionTag("ref", ...) is only called when they really ended up in the final output
function Config:concatValues(valuesArray)
	local outString = ""
	local j, skip
	
	for i = 1, #valuesArray do
		-- check if this is a reference
		if valuesArray[i].refHash then
			j = i - 1
			skip = false
			
			-- skip this reference if it is part of a continuous row of references that already contains the exact same reference
			while valuesArray[j] and valuesArray[j].refHash do
				if valuesArray[i].refHash == valuesArray[j].refHash then
					skip = true
					break
				end
				j = j - 1
			end
			
			if not skip then
				-- add <ref> tag with the reference's hash as its name (to deduplicate references)
				outString = outString .. mw.getCurrentFrame():extensionTag("ref", valuesArray[i][1], {name = "wikidata-" .. valuesArray[i].refHash .. "-v" .. i18n['cite']['version']})
			end
		else
			outString = outString .. valuesArray[i][1]
		end
	end
	
	return outString
end

function Config:convertUnit(unit, raw, link, short, unitOnly)
	local space = " "
	local label = ""
	
	if unit == "" or unit == "1" then
		return nil
	end
	
	if unitOnly then
		space = ""
	end
	
	itemID = parseWikidataURL(unit)
	
	if itemID then
		if itemID == aliasesQ.percentage then
			return "%"
		else
			label = self:getLabel(itemID, raw, link, short)
			
			if label ~= "" then
				return space .. label
			end
		end
	end
	
	return ""
end

function Config:getValue(snak, raw, link, short, anyLang, unitOnly, noSpecial)
	if snak.snaktype == 'value' then
		local datatype = snak.datavalue.type
		local subtype = snak.datatype
		local datavalue = snak.datavalue.value
		
		if datatype == 'string' then
			if subtype == 'url' and link then
				-- create link explicitly
				if raw then
					-- will render as a linked number like [1]
					return "[" .. datavalue .. "]"
				else
					return "[" .. datavalue .. " " .. datavalue .. "]"
				end
			elseif subtype == 'commonsMedia' then
				if link then
					return buildWikilink("c:File:" .. datavalue, datavalue)
				elseif not raw then
					return "[[File:"_.._datavalue_.._"|File:" .. datavalue .. "]]"
				else
					return datavalue
				end
			elseif subtype == 'geo-shape' and link then
				return buildWikilink("c:" .. datavalue, datavalue)
			elseif subtype == 'math' and not raw then
				return mw.getCurrentFrame():extensionTag("math", datavalue)
			elseif subtype == 'external-id' and link then
				local url = p._property({p.aliasesP.formatterURL, [p.args.eid] = snak.property})  -- get formatter URL
				
				if url ~= "" then
					url = mw.ustring.gsub(url, "$1", datavalue)
					return "[" .. url .. " " .. datavalue .. "]"
				else
					return datavalue
				end
			else
				return datavalue
			end
		elseif datatype == 'monolingualtext' then
			if anyLang then
				return datavalue['text'], datavalue['language']
			elseif datavalue['language'] == self.langCode then
				return datavalue['text']
			else
				return nil
			end
		elseif datatype == 'quantity' then
			local value = ""
			local unit
			
			if not unitOnly then
				-- get value and strip + signs from front
				value = mw.ustring.gsub(datavalue['amount'], "^\+(.+)$", "%1")
				
				if raw then
					return value
				end
				
				-- replace decimal mark based on locale
				value = replaceDecimalMark(value)
				
				-- add delimiters for readability
				value = i18n.addDelimiters(value)
			end
			
			unit = self:convertUnit(datavalue['unit'], raw, link, short, unitOnly)
			
			if unit then
				value = value .. unit
			end
			
			return value
		elseif datatype == 'time' then
			local y, m, d, p, yDiv, yRound, yFull, value, calendarID, dateStr
			local yFactor = 1
			local sign = 1
			local prefix = ""
			local suffix = ""
			local mayAddCalendar = false
			local calendar = ""
			local precision = datavalue['precision']
			
			if precision == 11 then
				p = "d"
			elseif precision == 10 then
				p = "m"
			else
				p = "y"
				yFactor = 10^(9-precision)
			end
			
			y, m, d = parseDate(datavalue['time'], p)
			
			if y < 0 then
				sign = -1
				y = y * sign
			end
			
			-- if precision is tens/hundreds/thousands/millions/billions of years
			if precision <= 8 then
				yDiv = y / yFactor
				
				-- if precision is tens/hundreds/thousands of years
				if precision >= 6 then
					mayAddCalendar = true
					
					if precision <= 7 then
						-- round centuries/millenniums up (e.g. 20th century or 3rd millennium)
						yRound = math.ceil(yDiv)
						
						if not raw then
							if precision == 6 then
								suffix = i18n['datetime']['suffixes']['millennium']
							else
								suffix = i18n['datetime']['suffixes']['century']
							end
							
							suffix = i18n.getOrdinalSuffix(yRound) .. suffix
						else
							-- if not verbose, take the first year of the century/millennium
							-- (e.g. 1901 for 20th century or 2001 for 3rd millennium)
							yRound = (yRound - 1) * yFactor + 1
						end
					else
						-- precision == 8
						-- round decades down (e.g. 2010s)
						yRound = math.floor(yDiv) * yFactor
						
						if not raw then
							prefix = i18n['datetime']['prefixes']['decade-period']
							suffix = i18n['datetime']['suffixes']['decade-period']
						end
					end
					
					if raw and sign < 0 then
						-- if BCE then compensate for "counting backwards"
						-- (e.g. -2019 for 2010s BCE, -2000 for 20th century BCE or -3000 for 3rd millennium BCE)
						yRound = yRound + yFactor - 1
					end
				else
					local yReFactor, yReDiv, yReRound
					
					-- round to nearest for tens of thousands of years or more
					yRound = math.floor(yDiv + 0.5)
					
					if yRound == 0 then
						if precision <= 2 and y ~= 0 then
							yReFactor = 1e6
							yReDiv = y / yReFactor
							yReRound = math.floor(yReDiv + 0.5)
							
							if yReDiv == yReRound then
								-- change precision to millions of years only if we have a whole number of them
								precision = 3
								yFactor = yReFactor
								yRound = yReRound
							end
						end
						
						if yRound == 0 then
							-- otherwise, take the unrounded (original) number of years
							precision = 5
							yFactor = 1
							yRound = y
							mayAddCalendar = true
						end
					end
					
					if precision >= 1 and y ~= 0 then
						yFull = yRound * yFactor
						
						yReFactor = 1e9
						yReDiv = yFull / yReFactor
						yReRound = math.floor(yReDiv + 0.5)
						
						if yReDiv == yReRound then
							-- change precision to billions of years if we're in that range
							precision = 0
							yFactor = yReFactor
							yRound = yReRound
						else
							yReFactor = 1e6
							yReDiv = yFull / yReFactor
							yReRound = math.floor(yReDiv + 0.5)
							
							if yReDiv == yReRound then
								-- change precision to millions of years if we're in that range
								precision = 3
								yFactor = yReFactor
								yRound = yReRound
							end
						end
					end
					
					if not raw then
						if precision == 3 then
							suffix = i18n['datetime']['suffixes']['million-years']
						elseif precision == 0 then
							suffix = i18n['datetime']['suffixes']['billion-years']
						else
							yRound = yRound * yFactor
							if yRound == 1 then
								suffix = i18n['datetime']['suffixes']['year']
							else
								suffix = i18n['datetime']['suffixes']['years']
							end
						end
					else
						yRound = yRound * yFactor
					end
				end
			else
				yRound = y
				mayAddCalendar = true
			end
			
			if mayAddCalendar then
				calendarID = parseWikidataURL(datavalue['calendarmodel'])
				
				if calendarID and calendarID == aliasesQ.prolepticJulianCalendar then
					if not raw then
						if link then
							calendar = " ("..buildWikilink(i18n['datetime']['julian-calendar'], i18n['datetime']['julian'])..")"
						else
							calendar = " ("..i18n['datetime']['julian']..")"
						end
					else
						calendar = "/"..i18n['datetime']['julian']
					end
				end
			end
			
			if not raw then
				local ce = nil
				
				if sign < 0 then
					ce = i18n['datetime']['BCE']
				elseif precision <= 5 then
					ce = i18n['datetime']['CE']
				end
				
				if ce then
					if link then
						ce = buildWikilink(i18n['datetime']['common-era'], ce)
					end
					suffix = suffix .. " " .. ce
				end
				
				value = tostring(yRound)
				
				if m then
					dateStr = self.langObj:formatDate("F", "1-"..m.."-1")
					
					if d then
						if self.mdyDate then
							dateStr = dateStr .. " " .. d .. ","
						else
							dateStr = d .. " " .. dateStr
						end
					end
					
					value = dateStr .. " " .. value
				end
				
				value = prefix .. value .. suffix .. calendar
			else
				value = padZeros(yRound * sign, 4)
				
				if m then
					value = value .. "-" .. padZeros(m, 2)
					
					if d then
						value = value .. "-" .. padZeros(d, 2)
					end
				end
				
				value = value .. calendar
			end
			
			return value
		elseif datatype == 'globecoordinate' then
			-- logic from https://github.com/DataValues/Geo
			
			local precision, numDigits, strFormat, value, globe
			local latValue, latitude, latDegrees, latMinutes, latSeconds
			local lonValue, longitude, lonDegrees, lonMinutes, lonSeconds
			local latDirection, latDirectionN, latDirectionS, latDirectionEN
			local lonDirection, lonDirectionE, lonDirectionW, lonDirectionEN
			
			local latDirectionEN_N = "N"
			local latDirectionEN_S = "S"
			local lonDirectionEN_E = "E"
			local lonDirectionEN_W = "W"
			
			if not raw then
				latDirectionN = i18n['coord']['latitude-north']
				latDirectionS = i18n['coord']['latitude-south']
				lonDirectionE = i18n['coord']['longitude-east']
				lonDirectionW = i18n['coord']['longitude-west']
				
				degSymbol = i18n['coord']['degrees']
				minSymbol = i18n['coord']['minutes']
				secSymbol = i18n['coord']['seconds']
				separator = i18n['coord']['separator']
			else
				latDirectionN = latDirectionEN_N
				latDirectionS = latDirectionEN_S
				lonDirectionE = lonDirectionEN_E
				lonDirectionW = lonDirectionEN_W
				
				degSymbol = "/"
				minSymbol = "/"
				secSymbol = "/"
				separator = "/"
			end
			
			latitude = datavalue['latitude']
			longitude = datavalue['longitude']
			
			if latitude < 0 then
				latDirection = latDirectionS
				latDirectionEN = latDirectionEN_S
				latitude = math.abs(latitude)
			else
				latDirection = latDirectionN
				latDirectionEN = latDirectionEN_N
			end
			
			if longitude < 0 then
				lonDirection = lonDirectionW
				lonDirectionEN = lonDirectionEN_W
				longitude = math.abs(longitude)
			else
				lonDirection = lonDirectionE
				lonDirectionEN = lonDirectionEN_E
			end
			
			precision = datavalue['precision']
			
			if not precision or precision == 0 then
				precision = 1 / 3600  -- precision unspecified, set to arcsecond
			end
			
			latitude = math.floor(latitude / precision + 0.5) * precision
			longitude = math.floor(longitude / precision + 0.5) * precision
			
			numDigits = math.ceil(-math.log10(3600 * precision))
			
			if numDigits < 0 or numDigits == -0 then
				numDigits = tonumber("0")  -- for some reason, 'numDigits = 0' may actually store '-0', so parse from string instead
			end
			
			strFormat = "%." .. numDigits .. "f"
			
			-- use string.format() to strip decimal point followed by a zero (.0) for whole numbers
			latSeconds = tonumber(strFormat:format(math.floor(latitude * 3600 * 10^numDigits + 0.5) / 10^numDigits))
			lonSeconds = tonumber(strFormat:format(math.floor(longitude * 3600 * 10^numDigits + 0.5) / 10^numDigits))
			
			latMinutes = math.floor(latSeconds / 60)
			lonMinutes = math.floor(lonSeconds / 60)
			
			latSeconds = latSeconds - (latMinutes * 60)
			lonSeconds = lonSeconds - (lonMinutes * 60)
			
			latDegrees = math.floor(latMinutes / 60)
			lonDegrees = math.floor(lonMinutes / 60)
			
			latMinutes = latMinutes - (latDegrees * 60)
			lonMinutes = lonMinutes - (lonDegrees * 60)
			
			latValue = latDegrees .. degSymbol
			lonValue = lonDegrees .. degSymbol
			
			if precision < 1 then
				latValue = latValue .. latMinutes .. minSymbol
				lonValue = lonValue .. lonMinutes .. minSymbol
			end
			
			if precision < (1 / 60) then
				latSeconds = strFormat:format(latSeconds)
				lonSeconds = strFormat:format(lonSeconds)
				
				if not raw then
					-- replace decimal marks based on locale
					latSeconds = replaceDecimalMark(latSeconds)
					lonSeconds = replaceDecimalMark(lonSeconds)
				end
				
				latValue = latValue .. latSeconds .. secSymbol
				lonValue = lonValue .. lonSeconds .. secSymbol
			end
			
			latValue = latValue .. latDirection
			lonValue = lonValue .. lonDirection
			
			value = latValue .. separator .. lonValue
			
			if link then
				globe = parseWikidataURL(datavalue['globe'])
				
				if globe then
					globe = mw.wikibase.getEntity(globe):getLabel("en"):lower()
				else
					globe = "earth"
				end
				
				value = "[https://tools.wmflabs.org/geohack/geohack.php?language="..self.langCode.."&params="..latitude.."_"..latDirectionEN.."_"..longitude.."_"..lonDirectionEN.."_globe:"..globe.." "..value.."]"
			end
			
			return value
		elseif datatype == 'wikibase-entityid' then
			local label
			local itemID = datavalue['numeric-id']
			
			if subtype == 'wikibase-item' then
				itemID = "Q" .. itemID
			elseif subtype == 'wikibase-property' then
				itemID = "P" .. itemID
			else
				return '<strong class="error">' .. errorText('unknown-data-type', subtype) .. '</strong>'
			end
			
			label = self:getLabel(itemID, raw, link, short)
			
			if label == "" then
				label = nil
			end
			
			return label
		else
			return '<strong class="error">' .. errorText('unknown-data-type', datatype) .. '</strong>'
		end
	elseif snak.snaktype == 'somevalue' and not noSpecial then
		if raw then
			return " "  -- single space represents 'somevalue'
		else
			return i18n['values']['unknown']
		end
	elseif snak.snaktype == 'novalue' and not noSpecial then
		if raw then
			return ""  -- empty string represents 'novalue'
		else
			return i18n['values']['none']
		end
	else
		return nil
	end
end

function Config:getSingleRawQualifier(claim, qualifierID)
	local qualifiers
	
	if claim.qualifiers then qualifiers = claim.qualifiers[qualifierID] end
	
	if qualifiers and qualifiers[1] then
		return self:getValue(qualifiers[1], true)  -- raw = true
	else
		return nil
	end
end

function Config:snakEqualsValue(snak, value)
	local snakValue = self:getValue(snak, true)  -- raw = true
	
	if snakValue and snak.snaktype == 'value' and snak.datavalue.type == 'wikibase-entityid' then value = value:upper() end
	
	return snakValue == value
end

function Config:setRank(rank)
	local rankPos
	
	if rank == p.flags.best then
		self.bestRank = true
		self.flagBest = true  -- mark that 'best' flag was given
		return
	end
	
	if rank:sub(1,9) == p.flags.preferred then
		rankPos = 1
	elseif rank:sub(1,6) == p.flags.normal then
		rankPos = 2
	elseif rank:sub(1,10) == p.flags.deprecated then
		rankPos = 3
	else
		return
	end
	
	-- one of the rank flags was given, check if another one was given before
	if not self.flagRank then
		self.ranks = {false, false, false}  -- no other rank flag given before, so unset ranks
		self.bestRank = self.flagBest       -- unsets bestRank only if 'best' flag was not given before
		self.flagRank = true                -- mark that a rank flag was given
	end
	
	if rank:sub(-1) == "+" then
		for i = rankPos, 1, -1 do
			self.ranks[i] = true
		end
	elseif rank:sub(-1) == "-" then
		for i = rankPos, #self.ranks do
			self.ranks[i] = true
		end
	else
		self.ranks[rankPos] = true
	end
end

function Config:setPeriod(period)
	local periodPos
	
	if period == p.flags.future then
		periodPos = 1
	elseif period == p.flags.current then
		periodPos = 2
	elseif period == p.flags.former then
		periodPos = 3
	else
		return
	end
	
	-- one of the period flags was given, check if another one was given before
	if not self.flagPeriod then
		self.periods = {false, false, false}  -- no other period flag given before, so unset periods
		self.flagPeriod = true                -- mark that a period flag was given
	end
	
	self.periods[periodPos] = true
end

function Config:qualifierMatches(claim, id, value)
	local qualifiers
	
	if claim.qualifiers then qualifiers = claim.qualifiers[id] end
	if qualifiers then
		for i, v in pairs(qualifiers) do
			if self:snakEqualsValue(v, value) then
				return true
			end
		end
	elseif value == "" then
		-- if the qualifier is not present then treat it the same as the special value 'novalue'
		return true
	end
	
	return false
end

function Config:rankMatches(rankPos)
	if self.bestRank then
		return (self.ranks[rankPos] and self.foundRank >= rankPos)
	else
		return self.ranks[rankPos]
	end
end

function Config:timeMatches(claim)
	local startTime = nil
	local startTimeY = nil
	local startTimeM = nil
	local startTimeD = nil
	local endTime = nil
	local endTimeY = nil
	local endTimeM = nil
	local endTimeD = nil
	
	if self.periods[1] and self.periods[2] and self.periods[3] then
		-- any time
		return true
	end
	
	local now = os.date('!*t')
	
	startTime = self:getSingleRawQualifier(claim, p.aliasesP.startTime)
	if startTime and startTime ~= "" and startTime ~= " " then
		startTimeY, startTimeM, startTimeD = parseDate(startTime)
	end
	
	endTime = self:getSingleRawQualifier(claim, p.aliasesP.endTime)
	if endTime and endTime ~= "" and endTime ~= " " then
		endTimeY, endTimeM, endTimeD = parseDate(endTime)
	elseif endTime == " " then
		-- end time is 'unknown', assume it is somewhere in the past;
		-- we can do this by taking the current date as a placeholder for the end time
		endTimeY = now['year']
		endTimeM = now['month']
		endTimeD = now['day']
	end
	
	if startTimeY ~= nil and endTimeY ~= nil and datePrecedesDate(endTimeY, endTimeM, endTimeD, startTimeY, startTimeM, startTimeD) then
		-- invalidate end time if it precedes start time
		endTimeY = nil
		endTimeM = nil
		endTimeD = nil
	end
	
	if self.periods[1] then
		-- future
		if startTimeY and datePrecedesDate(now['year'], now['month'], now['day'], startTimeY, startTimeM, startTimeD) then
			return true
		end
	end
	
	if self.periods[2] then
		-- current
		if (startTimeY == nil or not datePrecedesDate(now['year'], now['month'], now['day'], startTimeY, startTimeM, startTimeD)) and
		   (endTimeY == nil or datePrecedesDate(now['year'], now['month'], now['day'], endTimeY, endTimeM, endTimeD)) then
			return true
		end
	end
	
	if self.periods[3] then
		-- former
		if endTimeY and not datePrecedesDate(now['year'], now['month'], now['day'], endTimeY, endTimeM, endTimeD) then
			return true
		end
	end
	
	return false
end

function Config:processFlag(flag)
	if not flag then
		return false
	else
		flag = mw.text.trim(flag)
	end
	
	if flag == p.flags.linked then
		self.curState.linked = true
		return true
	elseif flag == p.flags.raw then
		self.curState.rawValue = true
		
		if self.curState == self.states[parameters.reference] then
			-- raw reference values end with periods and require a separator (other than none)
			self.separators["sep%r"][1] = {" "}
		end
		
		return true
	elseif flag == p.flags.short then
		self.curState.shortName = true
		return true
	elseif flag == p.flags.multilanguage then
		self.curState.anyLanguage = true
		return true
	elseif flag == p.flags.unit then
		self.curState.unitOnly = true
		return true
	elseif flag == p.flags.mdy then
		self.mdyDate = true
		return true
	elseif flag == p.flags.single then
		self.singleClaim = true
		return true
	elseif flag == p.flags.sourced then
		self.sourcedOnly = true
		return true
	elseif flag == p.flags.edit then
		self.editable = true
		return true
	elseif flag == p.flags.editAtEnd then
		self.editable = true
		self.editAtEnd = true
		return true
	elseif flag == p.flags.best or flag:match('^'..p.flags.preferred..'[+-]?$') or flag:match('^'..p.flags.normal..'[+-]?$') or flag:match('^'..p.flags.deprecated..'[+-]?$') then
		self:setRank(flag)
		return true
	elseif flag == p.flags.future or flag == p.flags.current or flag == p.flags.former then
		self:setPeriod(flag)
		return true
	elseif flag == "" then
		-- ignore empty flags and carry on
		return true
	else
		return false
	end
end

function Config:processFlagOrCommand(flag)
	local param = ""
	
	if not flag then
		return false
	else
		flag = mw.text.trim(flag)
	end
	
	if flag == p.claimCommands.property or flag == p.claimCommands.properties then
		param = parameters.property
	elseif flag == p.claimCommands.qualifier or flag == p.claimCommands.qualifiers then
		self.states.qualifiersCount = self.states.qualifiersCount + 1
		param = parameters.qualifier .. self.states.qualifiersCount
		self.separators["sep"..param] = {copyTable(defaultSeparators["sep%q\\d"])}
	elseif flag == p.claimCommands.reference or flag == p.claimCommands.references then
		param = parameters.reference
	else
		return self:processFlag(flag)
	end
	
	if self.states[param] then
		return false
	end
	
	-- create a new state for each command
	self.states[param] = State.new(self)
	
	-- use "%x" as the general parameter name
	self.states[param].parsedFormat = parseFormat(parameters.general)  -- will be overwritten for param=="%p"
	
	-- set the separator
	self.states[param].separator = self.separators["sep"..param]  -- will be nil for param=="%p", which will be set separately
	
	if flag:sub(-1) ~= 's' then
		self.states[param].singleValue = true
	end
	
	self.curState = self.states[param]
	
	return true
end

function Config:processSeparators(args)
	local sep
	
	for i, v in pairs(self.separators) do
		if args[i] then
			sep = replaceSpecialChars(args[i])
			
			if sep ~= "" then
				self.separators[i][1] = {sep}
			else
				self.separators[i][1] = nil
			end
		end
	end
end

function Config:setFormatAndSeparators(state, parsedFormat)
	state.parsedFormat = parsedFormat
	state.separator = self.separators["sep"]
	state.movSeparator = self.separators["sep"..parameters.separator]
	state.puncMark = self.separators["punc"]
end

-- determines if a claim has references by prefetching them from the claim using getReferences,
-- which applies some filtering that determines if a reference is actually returned,
-- and caches the references for later use
function State:isSourced(claim)
	self.conf.prefetchedRefs = self:getReferences(claim)
	return (#self.conf.prefetchedRefs > 0)
end

function State:resetCaches()
	-- any prefetched references of the previous claim must not be used
	self.conf.prefetchedRefs = nil
end

function State:claimMatches(claim)
	local matches, rankPos
	
	-- first of all, reset any cached values used for the previous claim
	self:resetCaches()
	
	-- if a property value was given, check if it matches the claim's property value
	if self.conf.propertyValue then
		matches = self.conf:snakEqualsValue(claim.mainsnak, self.conf.propertyValue)
	else
		matches = true
	end
	
	-- if any qualifier values were given, check if each matches one of the claim's qualifier values
	for i, v in pairs(self.conf.qualifierIDsAndValues) do
		matches = (matches and self.conf:qualifierMatches(claim, i, v))
	end
	
	-- check if the claim's rank and time period match
	rankPos = rankTable[claim.rank] or 4
	matches = (matches and self.conf:rankMatches(rankPos) and self.conf:timeMatches(claim))
	
	-- if only claims with references must be returned, check if this one has any
	if self.conf.sourcedOnly then
		matches = (matches and self:isSourced(claim))  -- prefetches and caches references
	end
	
	return matches, rankPos
end

function State:out()
	local result  -- collection of arrays with value objects
	local valuesArray  -- array with value objects
	local sep = nil  -- value object
	local out = {}  -- array with value objects
	
	local function walk(formatTable, result)
		local valuesArray = {}  -- array with value objects
		
		for i, v in pairs(formatTable.req) do
			if not result[i] or not result[i][1] then
				-- we've got no result for a parameter that is required on this level,
				-- so skip this level (and its children) by returning an empty result
				return {}
			end
		end
		
		for i, v in ipairs(formatTable) do
			if v.param then
				valuesArray = mergeArrays(valuesArray, result[v.str])
			elseif v.str ~= "" then
				valuesArray[#valuesArray + 1] = {v.str}
			end
			
			if v.child then
				valuesArray = mergeArrays(valuesArray, walk(v.child, result))
			end
		end
		
		return valuesArray
	end
	
	-- iterate through the results from back to front, so that we know when to add separators
	for i = #self.results, 1, -1 do
		result = self.results[i]
		
		-- if there is already some output, then add the separators
		if #out > 0 then
			sep = self.separator[1]  -- fixed separator
			result[parameters.separator] = {self.movSeparator[1]}  -- movable separator
		else
			sep = nil
			result[parameters.separator] = {self.puncMark[1]}  -- optional punctuation mark
		end
		
		valuesArray = walk(self.parsedFormat, result)
		
		if #valuesArray > 0 then
			if sep then
				valuesArray[#valuesArray + 1] = sep
			end
			
			out = mergeArrays(valuesArray, out)
		end
	end
	
	-- reset state before next iteration
	self.results = {}
	
	return out
end

-- level 1 hook
function State:getProperty(claim)
	local value = {self.conf:getValue(claim.mainsnak, self.rawValue, self.linked, self.shortName, self.anyLanguage, self.unitOnly)}  -- create one value object
	
	if #value > 0 then
		return {value}  -- wrap the value object in an array and return it
	else
		return {}  -- return empty array if there was no value
	end
end

-- level 1 hook
function State:getQualifiers(claim, param)
	local qualifiers
	
	if claim.qualifiers then qualifiers = claim.qualifiers[self.conf.qualifierIDs[param]] end
	if qualifiers then
		-- iterate through claim's qualifier statements to collect their values;
		-- return array with multiple value objects
		return self.conf.states[param]:iterate(qualifiers, {[parameters.general] = hookNames[parameters.qualifier.."\\d"][2], count = 1})  -- pass qualifier state with level 2 hook
	else
		return {}  -- return empty array
	end
end

-- level 2 hook
function State:getQualifier(snak)
	local value = {self.conf:getValue(snak, self.rawValue, self.linked, self.shortName, self.anyLanguage, self.unitOnly)}  -- create one value object
	
	if #value > 0 then
		return {value}  -- wrap the value object in an array and return it
	else
		return {}  -- return empty array if there was no value
	end
end

-- level 1 hook
function State:getAllQualifiers(claim, param, result, hooks)
	local out = {}  -- array with value objects
	local sep = self.conf.separators["sep"..parameters.qualifier][1]  -- value object
	
	-- iterate through the output of the separate "qualifier(s)" commands
	for i = 1, self.conf.states.qualifiersCount do
		
		-- if a hook has not been called yet, call it now
		if not result[parameters.qualifier..i] then
			self:callHook(parameters.qualifier..i, hooks, claim, result)
		end
		
		-- if there is output for this particular "qualifier(s)" command, then add it
		if result[parameters.qualifier..i] and result[parameters.qualifier..i][1] then
			
			-- if there is already some output, then add the separator
			if #out > 0 and sep then
				out[#out + 1] = sep
			end
			
			out = mergeArrays(out, result[parameters.qualifier..i])
		end
	end
	
	return out
end

-- level 1 hook
function State:getReferences(claim)
	if self.conf.prefetchedRefs then
		-- return references that have been prefetched by isSourced
		return self.conf.prefetchedRefs
	end
	
	if claim.references then
		-- iterate through claim's reference statements to collect their values;
		-- return array with multiple value objects
		return self.conf.states[parameters.reference]:iterate(claim.references, {[parameters.general] = hookNames[parameters.reference][2], count = 1})  -- pass reference state with level 2 hook
	else
		return {}  -- return empty array
	end
end

-- level 2 hook
function State:getReference(statement)
	local key, citeWeb, citeQ, label
	local params = {}
	local citeParams = {['web'] = {}, ['q'] = {}}
	local citeMismatch = {}
	local useCite = nil
	local useParams = nil
	local value = ""
	local ref = {}
	
	if statement.snaks then
		-- don't include "imported from", which is added by a bot
		if statement.snaks[p.aliasesP.importedFrom] then
			statement.snaks[p.aliasesP.importedFrom] = nil
		end
		
		-- don't include "language" if it is equal to the local one
		if self:getReferenceDetail(statement.snaks, p.aliasesP.language) == self.conf.langName then
			statement.snaks[p.aliasesP.language] = nil
		end
		
		-- retrieve all the parameters
		for i in pairs(statement.snaks) do
			label = ""
			
			-- multiple authors may be given
			if i == p.aliasesP.author then
				params[i] = self:getReferenceDetails(statement.snaks, i, false, self.linked, true)  -- link = true/false, anyLang = true
			else
				params[i] = {self:getReferenceDetail(statement.snaks, i, false, (self.linked or (i == p.aliasesP.statedIn)) and (statement.snaks[i][1].datatype ~= 'url'), true)}  -- link = true/false, anyLang = true
			end
			
			if #params[i] == 0 then
				params[i] = nil
			else
				if statement.snaks[i][1].datatype == 'external-id' then
					key = "external-id"
					label = self.conf:getLabel(i)
					
					if label ~= "" then
						label = label .. " "
					end
				else
					key = i
				end
				
				-- add the parameter to each matching type of citation
				for j in pairs(citeParams) do
					-- do so if there was no mismatch with a previous parameter
					if not citeMismatch[j] then
						-- check if this parameter is not mismatching itself
						if i18n['cite'][j][key] then
							-- continue if an option is available in the corresponding cite template
							if i18n['cite'][j][key] ~= "" then
								citeParams[j][i18n['cite'][j][key]] = label .. params[i][1]
								
								-- if there are multiple parameter values (authors), add those too
								for k=2, #params[i] do
									citeParams[j][i18n['cite'][j][key]..k] = label .. params[i][k]
								end
							end
						else
							citeMismatch[j] = true
						end
					end
				end
			end
		end
		
		-- get title of general template for citing web references
		citeWeb = split(mw.wikibase.sitelink(aliasesQ.citeWeb) or "", ":")[2]  -- split off namespace from front
		
		-- get title of template that expands stated-in references into citations
		citeQ = split(mw.wikibase.sitelink(aliasesQ.citeQ) or "", ":")[2]  -- split off namespace from front
		
		-- (1) use the general template for citing web references if there is a match and if at least both "reference URL" and "title" are present
		if citeWeb and not citeMismatch['web'] and citeParams['web'][i18n['cite']['web'][p.aliasesP.referenceURL]] and citeParams['web'][i18n['cite']['web'][p.aliasesP.title]] then
			useCite = citeWeb
			useParams = citeParams['web']
			
		-- (2) use the template that expands stated-in references into citations if there is a match and if at least "stated in" is present
		elseif citeQ and not citeMismatch['q'] and citeParams['q'][i18n['cite']['q'][p.aliasesP.statedIn]] then
			-- we need the raw "stated in" Q-identifier for the this template
			citeParams['q'][i18n['cite']['q'][p.aliasesP.statedIn]] = self:getReferenceDetail(statement.snaks, p.aliasesP.statedIn, true)  -- raw = true
			
			useCite = citeQ
			useParams = citeParams['q']
		end
		
		if useCite and useParams then
			-- if this module is being substituted then build a regular template call, otherwise expand the template
			if mw.isSubsting() then
				for i, v in pairs(useParams) do
					value = value .. "|" .. i .. "=" .. v
				end
				
				value = "{{" .. useCite .. value .. "}}"
			else
				value = mw.getCurrentFrame():expandTemplate{title=useCite, args=useParams}
			end
			
		-- (3) else, do some default rendering of name-value pairs, but only if at least "stated in", "reference URL" or "title" is present
		elseif params[p.aliasesP.statedIn] or params[p.aliasesP.referenceURL] or params[p.aliasesP.title] then
			citeParams['default'] = {}
			
			-- start by adding authors up front
			if params[p.aliasesP.author] and #params[p.aliasesP.author] > 0 then
				citeParams['default'][#citeParams['default'] + 1] = table.concat(params[p.aliasesP.author], " & ")
			end
			
			-- combine "reference URL" and "title" into one link if both are present
			if params[p.aliasesP.referenceURL] and params[p.aliasesP.title] then
				citeParams['default'][#citeParams['default'] + 1] = '[' .. params[p.aliasesP.referenceURL][1] .. ' "' .. params[p.aliasesP.title][1] .. '"]'
			elseif params[p.aliasesP.referenceURL] then
				citeParams['default'][#citeParams['default'] + 1] = params[p.aliasesP.referenceURL][1]
			elseif params[p.aliasesP.title] then
				citeParams['default'][#citeParams['default'] + 1] = '"' .. params[p.aliasesP.title][1] .. '"'
			end
			
			-- then add "stated in"
			if params[p.aliasesP.statedIn] then
				citeParams['default'][#citeParams['default'] + 1] = "''" .. params[p.aliasesP.statedIn][1] .. "''"
			end
			
			-- remove previously added parameters so that they won't be added a second time
			params[p.aliasesP.author] = nil
			params[p.aliasesP.referenceURL] = nil
			params[p.aliasesP.title] = nil
			params[p.aliasesP.statedIn] = nil
			
			-- add the rest of the parameters
			for i, v in pairs(params) do
				i = self.conf:getLabel(i)
				
				if i ~= "" then
					citeParams['default'][#citeParams['default'] + 1] = i .. ": " .. v[1]
				end
			end
			
			value = table.concat(citeParams['default'], "; ")
			
			if value ~= "" then
				value = value .. "."
			end
		end
		
		if value ~= "" then
			value = {value}  -- create one value object
			
			if not self.rawValue then
				-- this should become a <ref> tag, so safe the reference's hash for later
				value.refHash = statement.hash
			end
			
			ref = {value}  -- wrap the value object in an array
		end
	end
	
	return ref
end

-- gets a detail of one particular type for a reference
function State:getReferenceDetail(snaks, dType, raw, link, anyLang)
	local switchLang = anyLang
	local value = nil
	
	if not snaks[dType] then
		return nil
	end
	
	-- if anyLang, first try the local language and otherwise any language
	repeat
		for i, v in ipairs(snaks[dType]) do
			value = self.conf:getValue(v, raw, link, false, anyLang and not switchLang, false, true)  -- noSpecial = true
			
			if value then
				break
			end
		end
		
		if value or not anyLang then
			break
		end
		
		switchLang = not switchLang
	until anyLang and switchLang
	
	return value
end

-- gets the details of one particular type for a reference
function State:getReferenceDetails(snaks, dType, raw, link, anyLang)
	local values = {}
	
	if not snaks[dType] then
		return {}
	end
	
	for i, v in ipairs(snaks[dType]) do
		-- if nil is returned then it will not be added to the table
		values[#values + 1] = self.conf:getValue(v, raw, link, false, anyLang, false, true)  -- noSpecial = true
	end
	
	return values
end

-- level 1 hook
function State:getAlias(object)
	local value = object.value
	local title = nil
	
	if value and self.linked then
		if self.conf.entityID:sub(1,1) == "Q" then
			title = mw.wikibase.sitelink(self.conf.entityID)
		elseif self.conf.entityID:sub(1,1) == "P" then
			title = "d:Property:" .. self.conf.entityID
		end
		
		if title then
			value = buildWikilink(title, value)
		end
	end
	
	value = {value}  -- create one value object
	
	if #value > 0 then
		return {value}  -- wrap the value object in an array and return it
	else
		return {}  -- return empty array if there was no value
	end
end

-- level 1 hook
function State:getBadge(value)
	value = self.conf:getLabel(value, self.rawValue, self.linked, self.shortName)
	
	if value == "" then
		value = nil
	end
	
	value = {value}  -- create one value object
	
	if #value > 0 then
		return {value}  -- wrap the value object in an array and return it
	else
		return {}  -- return empty array if there was no value
	end
end

function State:callHook(param, hooks, statement, result)
	local valuesArray, refHash
	
	-- call a parameter's hook if it has been defined and if it has not been called before
	if not result[param] and hooks[param] then
		valuesArray = self[hooks[param]](self, statement, param, result, hooks)  -- array with value objects
		
		-- add to the result
		if #valuesArray > 0 then
			result[param] = valuesArray
			result.count = result.count + 1
		else
			result[param] = {}  -- an empty array to indicate that we've tried this hook already
			return true  -- miss == true
		end
	end
	
	return false
end

-- iterate through claims, claim's qualifiers or claim's references to collect values
function State:iterate(statements, hooks, matchHook)
	matchHook = matchHook or alwaysTrue
	
	local matches = false
	local rankPos = nil
	local result, gotRequired
	
	for i, v in ipairs(statements) do
		-- rankPos will be nil for non-claim statements (e.g. qualifiers, references, etc.)
		matches, rankPos = matchHook(self, v)
		
		if matches then
			result = {count = 0}  -- collection of arrays with value objects
			
			local function walk(formatTable)
				local miss
				
				for i2, v2 in pairs(formatTable.req) do
					-- call a hook, adding its return value to the result
					miss = self:callHook(i2, hooks, v, result)
					
					if miss then
						-- we miss a required value for this level, so return false
						return false
					end
					
					if result.count == hooks.count then
						-- we're done if all hooks have been called;
						-- returning at this point breaks the loop
						return true
					end
				end
				
				for i2, v2 in ipairs(formatTable) do
					if result.count == hooks.count then
						-- we're done if all hooks have been called;
						-- returning at this point prevents further childs from being processed
						return true
					end
					
					if v2.child then
						walk(v2.child)
					end
				end
				
				return true
			end
			gotRequired = walk(self.parsedFormat)
			
			-- only append the result if we got values for all required parameters on the root level
			if gotRequired then
				-- if we have a rankPos (only with matchHook() for complete claims), then update the foundRank
				if rankPos and self.conf.foundRank > rankPos then
					self.conf.foundRank = rankPos
				end
				
				-- append the result
				self.results[#self.results + 1] = result
				
				-- break if we only need a single value
				if self.singleValue then
					break
				end
			end
		end
	end
	
	return self:out()
end

function extractEntityFromInput(id, allowOmitPropPrefix)
	if id:sub(1,1):upper() == "Q" then
		return id:upper()  -- entity ID of an item was given
	elseif id:sub(1,9):lower() == "property:" then
		return replaceAlias(mw.text.trim(id:sub(10))):upper()  -- entity ID of a property was given
	elseif allowOmitPropPrefix and id ~= "" then
		return replaceAlias(id):upper()  -- could be an entity ID of a property without "Property:" prefix
	else
		return nil
	end
end

function extractEntityFromArgs(args, nextIndex, allowOmitPropPrefix)
	local id, eidArg
	
	if args[nextIndex] then
		args[nextIndex] = mw.text.trim(args[nextIndex])
	else
		args[nextIndex] = ""
	end
	
	id = extractEntityFromInput(args[nextIndex], allowOmitPropPrefix)
	eidArg = args[p.args.eid]
	
	if id then
		return id, nextIndex + 1
	elseif eidArg then
		return extractEntityFromInput(eidArg, true), nextIndex  -- if no positional id was found but eid was given, use eid without a default
	else
		return mw.wikibase.getEntityIdForCurrentPage(), nextIndex  -- by default, use item-entity connected to current page
	end
end

function claimCommand(args, funcName)
	local _ = Config.new()
	_:processFlagOrCommand(funcName)  -- process first command (== function name)
	
	local parsedFormat, formatParams, claims, value
	local hooks = {count = 0}
	
	local nextIndex = 1
	
	-- process flags and commands
	while _:processFlagOrCommand(args[nextIndex]) do
		nextIndex = nextIndex + 1
	end
	
	_.entityID, nextIndex = extractEntityFromArgs(args, nextIndex, false)
	
	-- if eid was explicitly set to empty, then this returns an empty string
	if _.entityID == nil then
		return ""
	end
	
	_.entity = mw.wikibase.getEntity(_.entityID)
	_.propertyID = replaceAlias(args[nextIndex]):upper()
	nextIndex = nextIndex + 1
	
	if _.states.qualifiersCount > 0 then
		-- do further processing if "qualifier(s)" command was given
		
		if #args - nextIndex + 1 > _.states.qualifiersCount then
			-- claim ID or literal value has been given
			
			_.propertyValue = mw.text.trim(args[nextIndex])
			nextIndex = nextIndex + 1
		end
		
		for i = 1, _.states.qualifiersCount do
			-- check if given qualifier ID is an alias and add it
			_.qualifierIDs[parameters.qualifier..i] = replaceAlias(mw.text.trim(args[nextIndex] or "")):upper()
			nextIndex = nextIndex + 1
		end
	elseif _.states[parameters.reference] then
		-- do further processing if "reference(s)" command was given
		
		if args[nextIndex] then
			_.propertyValue = mw.text.trim(args[nextIndex])
		end
		-- not incrementing nextIndex because it is never used after this
	end
	
	-- check for special property value 'somevalue' or 'novalue'
	if _.propertyValue then
		_.propertyValue = replaceSpecialChars(_.propertyValue)
		
		if _.propertyValue ~= "" and mw.text.trim(_.propertyValue) == "" then
			_.propertyValue = " "  -- single space represents 'somevalue', whereas empty string represents 'novalue'
		else
			_.propertyValue = mw.text.trim(_.propertyValue)
		end
	end
	
	-- parse the desired format, or choose an appropriate format
	if args["format"] then
		parsedFormat, formatParams = parseFormat(args["format"])
	elseif _.states.qualifiersCount > 0 then  -- "qualifier(s)" command given
		if _.states[parameters.property] then  -- "propert(y|ies)" command given
			parsedFormat, formatParams = parseFormat(formats.propertyWithQualifier)
		else
			parsedFormat, formatParams = parseFormat(formats.qualifier)
		end
	elseif _.states[parameters.property] then  -- "propert(y|ies)" command given
		parsedFormat, formatParams = parseFormat(formats.property)
	else  -- "reference(s)" command given
		parsedFormat, formatParams = parseFormat(formats.reference)
	end
	
	-- if a "qualifier(s)" command and no "propert(y|ies)" command has been given, make the movable separator a semicolon
	if _.states.qualifiersCount > 0 and not _.states[parameters.property] then
		_.separators["sep"..parameters.separator][1] = {";"}
	end
	
	-- if only "reference(s)" has been given, set the default separator to none (except when raw)
	if _.states[parameters.reference] and not _.states[parameters.property] and _.states.qualifiersCount == 0
	   and not _.states[parameters.reference].rawValue then
		_.separators["sep"][1] = nil
	end
	
	-- if exactly one "qualifier(s)" command has been given, make "sep%q" point to "sep%q1" to make them equivalent
	if _.states.qualifiersCount == 1 then
		_.separators["sep"..parameters.qualifier] = _.separators["sep"..parameters.qualifier.."1"]
	end
	
	-- process overridden separator values;
	-- must come AFTER tweaking the default separators
	_:processSeparators(args)
	
	-- define the hooks that should be called (getProperty, getQualifiers, getReferences);
	-- only define a hook if both its command ("propert(y|ies)", "reference(s)", "qualifier(s)") and its parameter ("%p", "%r", "%q1", "%q2", "%q3") have been given
	for i, v in pairs(_.states) do
		-- e.g. 'formatParams["%q1"] or formatParams["%q"]' to define hook even if "%q1" was not defined to be able to build a complete value for "%q"
		if formatParams[i] or formatParams[i:sub(1, 2)] then
			hooks[i] = getHookName(i, 1)
			hooks.count = hooks.count + 1
		end
	end
	
	-- the "%q" parameter is not attached to a state, but is a collection of the results of multiple states (attached to "%q1", "%q2", "%q3", ...);
	-- so if this parameter is given then this hook must be defined separately, but only if at least one "qualifier(s)" command has been given
	if formatParams[parameters.qualifier] and _.states.qualifiersCount > 0 then
		hooks[parameters.qualifier] = getHookName(parameters.qualifier, 1)
		hooks.count = hooks.count + 1
	end
	
	-- create a state for "properties" if it doesn't exist yet, which will be used as a base configuration for each claim iteration;
	-- must come AFTER defining the hooks
	if not _.states[parameters.property] then
		_.states[parameters.property] = State.new(_)
		
		-- if the "single" flag has been given then this state should be equivalent to "property" (singular)
		if _.singleClaim then
			_.states[parameters.property].singleValue = true
		end
	end
	
	-- if the "sourced" flag has been given then create a state for "reference" if it doesn't exist yet, using default values,
	-- which must exist in order to be able to determine if a claim has any references;
	-- must come AFTER defining the hooks
	if _.sourcedOnly and not _.states[parameters.reference] then
		_:processFlagOrCommand(p.claimCommands.reference)  -- use singular "reference" to minimize overhead
	end
	
	-- set the parsed format and the separators (and optional punctuation mark);
	-- must come AFTER creating the additonal states
	_:setFormatAndSeparators(_.states[parameters.property], parsedFormat)
	
	-- process qualifier matching values, analogous to _.propertyValue
	for i, v in pairs(args) do
		i = tostring(i)
		
		if i:match('^[Pp]%d+$') or p.aliasesP[i] then
			v = replaceSpecialChars(v)
			
			-- check for special qualifier value 'somevalue'
			if v ~= "" and mw.text.trim(v) == "" then
				v = " "  -- single space represents 'somevalue'
			end
			
			_.qualifierIDsAndValues[replaceAlias(i):upper()] = v
		end
	end
	
	if _.entity and _.entity.claims then claims = _.entity.claims[_.propertyID] end
	if claims then
		-- first sort the claims on rank to pre-define the order of output (preferred first, then normal, then deprecated)
		claims = sortOnRank(claims)
		
		-- then iterate through the claims to collect values
		value = _:concatValues(_.states[parameters.property]:iterate(claims, hooks, State.claimMatches))  -- pass property state with level 1 hooks and matchHook
		
		-- if desired, add a clickable icon that may be used to edit the returned values on Wikidata
		if _.editable and value ~= "" then
			value = value .. _:getEditIcon()
		end
		
		return value
	else
		return ""
	end
end

function generalCommand(args, funcName)
	local _ = Config.new()
	_.curState = State.new(_)
	
	local value = nil
	local nextIndex = 1
	
	while _:processFlag(args[nextIndex]) do
		nextIndex = nextIndex + 1
	end
	
	_.entityID, nextIndex = extractEntityFromArgs(args, nextIndex, true)
	
	-- if eid was explicitly set to empty, then this returns an empty string
	if _.entityID == nil then
		return ""
	end
	
	-- serve according to the given command
	if funcName == p.generalCommands.label then
		value = _:getLabel(_.entityID, _.curState.rawValue, _.curState.linked, _.curState.shortName)
	elseif funcName == p.generalCommands.title then
		_.inSitelinks = true
		
		if _.entityID:sub(1,1) == "Q" then
			value = mw.wikibase.sitelink(_.entityID)
		end
		
		if _.curState.linked and value then
			value = buildWikilink(value)
		end
	else
		local parsedFormat, formatParams
		local hooks = {count = 0}
		
		if funcName == p.generalCommands.alias or funcName == p.generalCommands.badge then
			_.curState.singleValue = true
		end
		
		_.entity = mw.wikibase.getEntity(_.entityID)
		
		if funcName == p.generalCommands.alias or funcName == p.generalCommands.aliases then
			local aliases
			
			-- parse the desired format, or parse the default aliases format
			if args["format"] then
				parsedFormat, formatParams = parseFormat(args["format"])
			else
				parsedFormat, formatParams = parseFormat(formats.alias)
			end
			
			-- process overridden separator values;
			-- must come AFTER tweaking the default separators
			_:processSeparators(args)
			
			-- define the hook that should be called (getAlias);
			-- only define the hook if the parameter ("%a") has been given
			if formatParams[parameters.alias] then
				hooks[parameters.alias] = getHookName(parameters.alias, 1)
				hooks.count = hooks.count + 1
			end
			
			-- set the parsed format and the separators (and optional punctuation mark)
			_:setFormatAndSeparators(_.curState, parsedFormat)
			
			if _.entity and _.entity.aliases then aliases = _.entity.aliases[_.langCode] end
			if aliases then
				value = _:concatValues(_.curState:iterate(aliases, hooks))
			end
		elseif funcName == p.generalCommands.badge or funcName == p.generalCommands.badges then
			_.inSitelinks = true
			
			local badges
			
			-- parse the desired format, or parse the default aliases format
			if args["format"] then
				parsedFormat, formatParams = parseFormat(args["format"])
			else
				parsedFormat, formatParams = parseFormat(formats.badge)
			end
			
			-- process overridden separator values;
			-- must come AFTER tweaking the default separators
			_:processSeparators(args)
			
			-- define the hook that should be called (getBadge);
			-- only define the hook if the parameter ("%b") has been given
			if formatParams[parameters.badge] then
				hooks[parameters.badge] = getHookName(parameters.badge, 1)
				hooks.count = hooks.count + 1
			end
			
			-- set the parsed format and the separators (and optional punctuation mark)
			_:setFormatAndSeparators(_.curState, parsedFormat)
			
			if _.entity and _.entity.sitelinks and _.entity.sitelinks[_.siteID] then badges = _.entity.sitelinks[_.siteID].badges end
			if badges then
				value = _:concatValues(_.curState:iterate(badges, hooks))
			end
		end
	end
	
	value = value or ""
	
	if _.editable and value ~= "" then
		-- if desired, add a clickable icon that may be used to edit the returned value on Wikidata
		value = value .. _:getEditIcon()
	end
	
	return value
end

-- modules that include this module should call the functions with an underscore prepended, e.g.: p._property(args)
function establishCommands(commandList, commandFunc)
	for commandIndex, commandName in pairs(commandList) do
		local function wikitextWrapper(frame)
			loadSubmodules(frame)
			return commandFunc(copyTable(frame.args), commandName)
		end
		p[commandName] = wikitextWrapper
		
		local function luaWrapper(args)
			loadSubmodules()
			return commandFunc(args, commandName)
		end
		p["_" .. commandName] = luaWrapper	
	end
end

establishCommands(p.claimCommands, claimCommand)
establishCommands(p.generalCommands, generalCommand)

-- main function that is supposed to be used by wrapper templates
function p.main(frame)
	local f, args, i, v
	
	loadSubmodules(frame)
	
	-- get the parent frame to take the arguments that were passed to the wrapper template
	frame = frame:getParent() or frame
	
	if not frame.args[1] then
		throwError("no-function-specified")
	end
	
	f = mw.text.trim(frame.args[1])
	
	if f == "main" then
		throwError("main-called-twice")
	end
	
	assert(p["_"..f], errorText('no-such-function', f))
	
	-- copy arguments from immutable to mutable table
	args = copyTable(frame.args)
	
	-- remove the function name from the list
	table.remove(args, 1)
	
	return p["_"..f](args)
end

return p