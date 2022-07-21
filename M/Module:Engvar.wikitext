-- This module implements Template:Engvar.
-- Template:Engvar is to be build into the template (like an infobox), with default & variant spellings defined.
-- That template should also allow parameter '|engvar=' for the editor (article page).
-- The module/template Engvar then returns the spelling variant as is set in that article (for example '|engvar=en-GB').
-- The defaultWord is returned, unless the engvar input hits on a defined (en-XX) variant word.
local p = {}
local getArgs = require('Module:Arguments').getArgs
local gsub = string.gsub
local lower = string.lower
local upper = string.upper

function p.variants(frame)
local args = getArgs(frame)
	return p._variants(args)
end

function p._variants(args)
local returnWord = nil

	local defaultWord = args.defaultWord or ''
	if args.engvar == nil then
		-- Nothing to look for; use defaultWord right away
		returnWord = defaultWord
	elseif args.defaultLang == gsub(lower(args.engvar), '^en%-(%w%w)$', formatISO) then
		-- By the defaultLang, the defaultWord is asked
		returnWord = defaultWord
	else
		returnWord = args[gsub(lower(args.engvar), '^en%-(%w%w)$', formatISO)]
	end

	if returnWord == nil then
		-- No hit so far. Search by words in the engvar entered, checking the list
		local useLang = engvarLang(args.engvar)
		if useLang == nil then
			returnWord = defaultWord .. addMaintCat(args)
		else
			returnWord = args[useLang] or defaultWord
		end
	end

	return returnWord
end

-- Returns arguments and intermediate result. Plus the template result, in front.
function p.explain(frame)
local args = getArgs(frame)
local ret = {}
	table.insert(ret, '\n\n: Settings:')
	table.insert(ret, 'defaultWord=' .. (args.defaultWord or '') .. '; ')
	table.insert(ret, 'defaultLang=' .. (args.defaultLang or '') .. '; ')
	table.insert(ret, 'engvarCat=' .. (args.engvarCat or '[default:yes]') .. '; ')
	table.insert(ret, 'engvarCatSort=' .. (args.engvarCatSort or ''))
	table.insert(ret, '\n\n: engvar=' .. (args.engvar or '') .. ' [input] ')
	local useLang = engvarLang(args.engvar or '')
	table.insert(ret, ' => Engvar code [used]: >' .. (useLang or '') .. '<.')
	
	for k, v in pairs(args) do
		if k == 'en-UK' then
			table.insert(ret, k .. ' ? better: use "en-GB"; ')
		elseif k == 'en-SA' then
			table.insert(ret, k .. ' ? misleading; use "en-ZA"; ')
		end
		
		if k == 'defaultWord' then
		elseif k == 'defaultLang' then
		elseif k == 'engvar' then
		elseif k == 'engvarcat' then
		elseif k == gsub(lower(k), '^en%-(%w%w)$', formatISO) then
			table.insert(ret, k .. '=' .. v .. '; ')
		else
			table.insert(ret, k .. ' [not standard:]=' .. v .. '; ')
		end

	end
	return (args.engvar or '') .. ' => ' .. p._variants(args) .. table.concat(ret, ' ')
end

-- Turn a match into pattern 'en-XX'
function formatISO(country)
	return ('en-' .. upper(country) or '')
end

function engvarLang(searchEngvar)
-- Search verbose language identifiers to ISO-format 'en-XX'
-- Assumed: not a blank string '' to seacrch
local match = string.match

	searchEngvar = gsub(searchEngvar, '^%s*en%-(.*)', '%1') -- rm any opening 'en-'.
	searchEngvar = gsub(lower(searchEngvar), '[%s%(%)%-]', '') -- To lc, remove all: (, ) , ws, hyphen.
	local useLang
	--Special codes
	if match(searchEngvar, 'oxford')
		or searchEngvar == oed then
			useLang = 'en-OED' -- 'oxford' to catch before anyting 'british'
	elseif match(searchEngvar, 'iupac') then
			useLang = 'en-IUPAC' -- chemistry
	-- Very often used
	elseif match(searchEngvar, 'british')
		or searchEngvar == 'uk'
		or searchEngvar == 'gbr' then
			useLang = 'en-GB'
	elseif searchEngvar == 'us'
		or match(searchEngvar, 'unitedstates')
		or searchEngvar == 'american'
		or searchEngvar == 'usa' then
			useLang = 'en-US'
	elseif match(searchEngvar, 'australia')
		or searchEngvar == 'aus' then
			useLang = 'en-AU'
	-- Often used
	elseif match(searchEngvar, 'india')
		or searchEngvar == 'ind' then
			useLang = 'en-IN'
	elseif searchEngvar == 'newzealand'
		or searchEngvar == 'nzl' then
			useLang = 'en-NZ'
	elseif match(searchEngvar, 'southafrica') -- not: en-SA
		or searchEngvar == 'zaf' then
			useLang = 'en-ZA'
	elseif searchEngvar == 'canada'
		or searchEngvar == 'can' then
			useLang = 'en-CA'
	elseif match(searchEngvar, 'hiberno')
		or match(searchEngvar, 'ireland')
		or match(searchEngvar, 'irish')
		or searchEngvar == 'irl' then
			useLang = 'en-EI'
	elseif match(searchEngvar, 'hongkong')
		or searchEngvar == 'hkg' then
			useLang = 'en-HK'
	-- Less often used
	elseif match(searchEngvar, 'jamaica')
		or searchEngvar == 'jam' then
			useLang = 'en-JM'
	elseif match(searchEngvar, 'malawi')
		or searchEngvar == 'mwi' then
			useLang = 'en-MW'
	elseif match(searchEngvar, 'nigeria')
		or searchEngvar == 'nga' then
			useLang = 'en-NG'
	elseif match(searchEngvar, 'pakistan')
		or searchEngvar == 'pak' then
			useLang = 'en-PK'
	elseif match(searchEngvar, 'philippine')
		or searchEngvar == 'phl' then
			useLang = 'en-PH'
	elseif match(searchEngvar, 'scotland')
		or match(searchEngvar, 'scottish')
		or searchEngvar == 'sco' then
			useLang = 'en-SCO' -- Has no alpha-2 code; not 'scotch'
	elseif match(searchEngvar, 'singapore')
		or searchEngvar == 'sgp' then
			useLang = 'en-SG'
	elseif match(searchEngvar, 'trinidad')
		or match(searchEngvar, 'tobago')
		or searchEngvar == 'tto' then
			useLang = 'en-TT'
	else
		useLang = nil
	end
	
	return useLang
end

function addMaintCat(args)
local catMaintenance
	if args.engvarCat == 'no' then
	else
		local title = mw.title.getCurrentTitle()
		if title:inNamespaces(0) then  -- 0=main, 10=templ, 828=module
			if args.engvarCatSort then
				catMaintenance = '|' .. args.engvarCatSort .. ', ' .. title.text
			end
			catMaintenance = '[[Category:Articles_using_an_unknown_Template:Engvar_option'_.._(catMaintenance_or_'')_.._'|Category:Articles using an unknown Template:Engvar option' .. (catMaintenance or '') .. ']]'
		end
	end
	return catMaintenance or ''
end

return p