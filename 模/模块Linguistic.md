-- some simple internationalization that can be called by other modules 

local p = {}
local f = require('Module:Fallback')
local i18n = mw.loadData('Module:I18n/linguistic')

local function getText(msg, lang)
	return f._langSwitch(i18n[msg], lang)
end

local vowels = 'aeiouyąăẵằẳặȃắâẫấầẩậãäǟāáàȁǎảẚåǻḁạǡæǣǽĕȇêễếềểệḙẽḛëēḕéḗèȅěẻẹęȩḝǝĭȋîĩḭïḯīíìȉǐỉịįıŏȏôỗốồổộõṏṍöōṑóṓòȍǒỏọǫǭơỡớờởợøǿŭȗûṷũṻṹṵüǖǘǜǚṳūúùȕǔủůụųưữứừửựŷỹÿȳýỳỷẙỵ'

local function wordor(lang) 
	return getText('or_conj', lang)
end

local function comma(lang)
	return getText("comma", lang)
end

function p.fullstop(lang)
	return getText("full_stop", lang)
end

function p.colon(lang)
	getText("colon", lang)
end

local function wordand(lang)
	return getText("and_conj", lang)
end

local function wordsep(lang) -- default separator between words
	return getText("word_separator", lang)
end	

local function isin(str, pattern)
	if str and pattern and mw.ustring.find(str, pattern, 1, true ) then
		return true
	end
end

local function langisin(str, lang)
	return isin(str, lang .. ' ') -- space is necessary to avoid false positives like zh in zh-hans
end

local function processgender(str)
	local t = {	
		f = 'feminine',
		fem = 'feminine',
		feminine = 'feminine',
		n = 'neutral',
		neutral = 'neutral',
		m = 'masculine',
		masc = 'masculine',
		masculine = 'masculine',
	}
	return t[str] or 'masculine'
end

local function processnumber(str)
	if (str == 'p') or (str == 'plural') then
		return 'plural'
	else 
		return 'singular'
	end
end

function p.vowelfirst (str)
	if str then return isin(vowels, str[1]) end
end

function p.inparentheses(str, lang)
	--todo: define language with exotic parentheses
	if str == '' then
		return str
	else 
		return ' (' .. str .. ')' 
		-- needs internationalization. 
		--Needs leading space in Enlgish because as some languages do not use it, it is part of the formatting
	end
end

function p.of(word, lang, raw, gender, number, determiner) -- rough translation of "of" in various languages
-- note that the cases when on "of" is employed varies a lot among languages, so it is more prudent to call this from lang specific function only
	if not raw then 
		raw = word
	end
	gender = processgender(gender)
	number = processnumber(number)
	-- raw is the string without the Wikiformatting so that it correctly analyses the string that is [[:fr:Italie|Italie]] -> 'italie'
	-- any way to automate this ?
	
	-- todo: ca to replace Template:Of/ca
	
	if lang == 'fr' then 
		if number == 'plural' then
			return 'des ' .. word
		elseif p.vowelfirst(raw) then
			return 'de l\'' .. word
		elseif gender == 'feminine' then
			return 'de la ' .. word
		elseif derterminer then
			return 'du ' .. word
		else
			return 'de ' .. word
		end
	end	

end

function p.noungroup(noun, adj, lang)
	if not noun or noun == '' then 
		return nil -- not '' so that it is not counted as a string by mw.listToText
	end
	if not adj or adj == ''
		then return noun
	end
	-- adjective before the noun
	if langisin('cs de de-at de-ch en en-ca en-gb pl sk zh zh-cn zh-hans zh-hant zh-my zh-sg zh-tw ', lang) then
		return adj .. wordsep(lang) .. noun
	-- adjective after the noun
	elseif langisin('fr fr-ca es it') then
		return noun .. wordsep(lang) .. adj
	else
		return noun ' (' .. adj .. ')'
	end
end

function p.conj(args, lang, conjtype)
	if (not args) then
		return nil
	end
	local newargs = {}
	for i, j in pairs(args) do
		if type(j) ~= 'nil' then
			table.insert(newargs, j)
		end
	end
	args = newargs
	if #args == 0 then
		return nil
	end
	if conjtype == 'comma' then
		return mw.text.listToText(args, comma(lang), comma(lang))
	elseif conjtype == 'or' then 
		return mw.text.listToText(args, comma(lang), wordor(lang)  .. wordsep(lang))
	elseif conjtype == 'explicit or' then -- adds "or" betwen all words when the context can be confusing
		return mw.text.listToText(args, wordor(lang) .. wordsep(lang), wordor(lang)  .. wordsep(lang))
	elseif conjtype then
		return mw.text.listToText(args, conjtype, conjtype)
	else 
		return mw.text.listToText(args, comma(lang), wordand(lang) .. wordsep(lang))
	end
end

return p