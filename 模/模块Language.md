require('Module:No globals')
local m_data = mw.loadData("Module:Language/data")

local p = {}

local sub = mw.ustring.sub
local gsub = mw.ustring.gsub
local find = mw.ustring.find
local match = mw.ustring.match
local lower = mw.ustring.lower
local upper = mw.ustring.upper

local function checkForString(variable)
	return variable ~= "" and variable ~= nil
end

local function makeLinkedName(languageCode)
	local data = m_data[languageCode]
	local article = data["article"]
	local name = data["Wikipedia_name"] or data["name"]
	return "[["_.._article_.._"|" .. name .. "]]: "
end

local function makeEntryName(word, languageCode)
	local data = m_data[languageCode]
	word = tostring(word)
	if word == nil then
		error("The function makeEntryName requires a string argument")
	elseif word == "" then
		return ""
	else
		-- Remove bold and italics, so that words that contain bolding or emphasis can be linked without piping.
		word = gsub(word, "\'\'\'", "")
		word = gsub(word, "\'\'", "")
		if data == nil then
			return word
		else
			local replacements = data and data["replacements"]
			if replacements == nil then
				return word
			else
				for regex, replacement in pairs(replacements) do
					word = gsub(word, regex, replacement)
				end
				return word
			end
		end
	end
end

local function getCodes(codes, text)
	local languageCode, scriptCode, invalidCode
	local errorText
	if codes == nil or codes == "" then
		errorText = 'no language or script code provided'
	elseif find(codes, "^%s*%a%a%a?%s*$") or find(codes, "^%s*%a%a%a?%-%a%a%a%a%s*$") then
		-- A three- or two-letter lowercase sequence at beginning of first parameter
		languageCode =
			find(codes, "^%s*%a%a%a?") and (
				match(codes, "^%s*(%l%l%l?)")
				or gsub(
					match(codes, "^%s*(%a%a%a?)"),
					"(%a%a%a?)",
					function(a)
						return lower(a)
					end,
					1
				)
			)
		-- One uppercase and three lowercase letters at the end of the first parameter
		scriptCode =
			find(codes, "%a%a%a%a%s*$") and (
				match(codes, "(%u%l%l%l)%s*$")
				or gsub(
					match(codes, "(%a%a%a%a)%s*$"),
					"(%a)(%a%a%a)",
					function(a, b)
						return upper(a) .. lower(b)
					end,
					1
				)
			)
	elseif find(codes, "^%s*%a%a%a%-%a%a%a$") then
		languageCode = match(codes, "^%s*%l%l%l%-%l%l%l$") and match (codes, "^%s*%l%l%l%-%l%l%l$") or gsub(match(codes, "^%s*%a%a%a%-%a%a%a$"), "(%a%a%a?)", function(a) return lower(a) end, 1)
	elseif find(codes, "^%s*%a%a%a?") then
		languageCode, invalidCode = match(codes, "^%s*(%a%a%a?)%-?(.*)")
		languageCode = lower(languageCode)
		errorText = '<code>'..invalidCode..'</code> is not a valid script code.'
	elseif find(codes, "%-?%a%a%a%a%s*$") then
		invalidCode, scriptCode = match(codes, "(.*)%-?(%a%a%a%a)%s*$")
		scriptCode = gsub(
			scriptCode,
			"(%a)(%a%a%a)",
			function(a, b)
				return upper(a) .. lower(b)
			end
		)
		errorText = '<code>'..invalidCode..'</code> is not a valid language code.'
	else
		errorText = '<code>'..codes..'</code> is not a valid language or script code.'
	end
	if not scriptCode then
		scriptCode = require("Module:Language/scripts").isLatn(text) and "Latn" or "unknown"
	end
	if errorText then
		errorText = ' <span style="font-size: smaller">[' .. errorText .. ']</span>'
	else
		errorText = ""
	end
	return languageCode, scriptCode, errorText
end

local function tag(text, languageCode, script, italics)
	local data = m_data[languageCode]
	
	local italicize = script == "Latn" and italics
	
	if not text then text = "[text?]" end
	
	local textDirectionMarkers = { "", "", "" }
	if data and data["direction"] == "rtl" then
		textDirectionMarkers = { ' dir="rtl"', '‏', '‎' }
	end
	
	local out = { textDirectionMarkers[2] }
	if italicize then
		table.insert(out, "<i lang=\"" .. languageCode .. "\" xml:lang=\"" .. languageCode  .. "\"" .. textDirectionMarkers[1] .. ">" .. text .. "</i>")
	else
		table.insert(out, "<span lang=\"" .. languageCode .. "\" xml:lang=\"" .. languageCode .. "\"" .. textDirectionMarkers[1] .. ">" .. text .. "</span>")
	end
	table.insert(out, textDirectionMarkers[3])
	
	return table.concat(out)
end

function p.lang(frame)
	local parent = frame:getParent()
	local args = parent.args[1] and parent.args or frame.args
	
	local codes = args[1]
	local text = args[2] or error("Provide text in the second parameter")
	
	local languageCode, scriptCode, errorText = getCodes(codes, text)
	
	local italics = args.italics or args.i
	italics = not (italics == "n" or italics == "-")
	
	return tag(text, languageCode, scriptCode, italics) .. errorText
end

local function linkToWiktionary(entry, linkText, languageCode)
	local data = m_data[languageCode]
	local name
	if languageCode then
		if data and data.name then
			name = data.name
		elseif mw.language.fetchLanguageName(languageCode, 'en') ~= "" then
			-- On other languages' wikis, use mw.getContentLanguage():getCode(), or replace with that wiki's language code.
			name = mw.language.fetchLanguageName(languageCode, 'en')
		else
			error("No name for the language " .. (languageCode or "nil") .. " could be found")
		end
		if sub(entry, 1, 1) == "*"  then
			if name ~= "" then
				entry = "Reconstruction:" .. name .. "/" .. sub(entry, 2)
			else
				error("Language name is empty")
			end
		end
		if entry and linkText then
			return "[[wikt:"_.._entry_.._"#"_.._name_.._"|" .. linkText .. "]]"
		else
			error("linkToWiktionary needs a Wiktionary entry or link text, or both")
		end
	else
		return "[[wikt:"_.._entry_.._"|" .. linkText .. "]]"
	end
end

function p.wiktlang(frame)
	local parent = frame:getParent()
	local args = parent.args[1] and parent.args or frame.args
	
	local codes = args[1] or nil
	local word1 = args[2] or nil
	local word2 = args[3] or nil
	
	local languageCode, scriptCode, errorText = getCodes(codes, word1)
	
	local italics = args.italics or args.i
	italics = not (italics == "n" or italics == "-")
	
	local entry, linkText
	if checkForString(word2) and checkForString(word1) then
		entry = makeEntryName(word1, languageCode)
		linkText = word2
	elseif checkForString(word1) then
		entry = makeEntryName(word1, languageCode)
		linkText = word1
	end
	
	local out
	if languageCode and entry and linkText then
		out = tag(linkToWiktionary(entry, linkText, languageCode), languageCode, scriptCode, italics)
	elseif entry and linkText then
		out = linkToWiktionary(entry, linkText)
	else
		out = '<span style="font-size: smaller;">[text?]</span>'
	end
	
	if out and errorText then
		return out .. errorText
	else
		return errorText or error("The function wiktlang generated nothing")
	end
end

function p.wikt(frame)
	local parent = frame:getParent()
	local args = parent.args[1] and parent.args or frame.args
	
	local codes = args[1] or nil
	local word1 = args[2] or nil
	local word2 = args[3] or nil
	
	if not word1 then
		error("Provide a word in parameter 2.")
	end
	
	local languageCode, scriptCode, errorText = getCodes(codes, word1)
	
	local entry, linkText
	if checkForString(word2) and checkForString(word1) then
		entry = makeEntryName(word1, languageCode)
		linkText = word2
	elseif checkForString(word1) then
		entry = makeEntryName(word1, languageCode)
		linkText = word1
	end
	
	local out
	if languageCode and entry and linkText then
		out = linkToWiktionary(entry, linkText, languageCode) 
	elseif entry and linkText then
		out = linkToWiktionary(entry, linkText)
	else
		out = '<span style="font-size: smaller;">[text?]</span>'
	end
	
	if out and errorText then
		return out and out .. errorText
	else
		return errorText or error("The function wikt generated nothing")
	end
end

return p