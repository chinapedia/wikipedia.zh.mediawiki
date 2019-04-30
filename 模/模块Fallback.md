local p = {}

local langlist = require('Module:Fallbacklist')

function p.fblist(lang) -- list the full fallback chain from a language to en
	local fbtable = p.fallbackloop{ lang:lower() }
	table.insert(fbtable, 'default')
	table.insert(fbtable, 'en')
	return fbtable
end

function _inArray(x, t)
	for i, v in ipairs(t) do
		if v == x then return i end
	end
	return -1
end

function p.fallbackloop(fbtable)  --list of fallback languages in string format (more convenient than tables)
	local changes = false
	for i, j in ipairs(fbtable) do
		local seq = langlist[j]
		if seq then
			for k, l in ipairs(seq) do
				if _inArray(l, fbtable) == -1 then
					table.insert(fbtable, l)
					changes = true
				end
			end
		end
	end
	if changes then
		return p.fallbackloop(fbtable)
	end
	return fbtable
end

function p._langSwitch(args, lang) -- args: table of translations
	-- Return error if there is not default and no english version
	if not args.en and not args.default and args.nocat ~= '1' then
		return '<strong class="error">LangSwitch Error: no default</strong>[[Category:LangSwitch_template_without_default_version|Category:LangSwitch template without default version]]' 
	end
	-- get language (either stated one or user's default language)
	if not lang then
		return '<strong class="error">LangSwitch Error: no lang</strong>' -- must become proper error
	end
	-- get the list of accpetable language (lang + those in lang's fallback chain) and check their content
	local parselist = p.fblist(lang)
	for i, k in ipairs(parselist) do 
		if args[k] == '~' then return '' end
		if args[k] and args[k] ~= '' then return args[k] end
	end
end

function p.langSwitch(frame) -- version to be used from wikitext
	args = frame.args
	-- if no expected args provided than check parent template/module args
	if args.en==nil and args.default==nil and args.nocat==nil then
		args = mw.getCurrentFrame():getParent().args 
	end
	if args.lang and args.lang ~= '' then
		lang = args.lang
		args.lang = nil
	else -- get user's chosen language 
		lang = frame:preprocess( "{{int:lang}}" )
	end
	return p._langSwitch(args, lang)
end

function p.fallbackpage(base, lang, formatting)
	local languages = p.fblist(lang) 
	for i, lng in ipairs(languages) do
		if mw.title.new(base .. '/' .. lng).exists then
			if formatting == 'table' then
				return {base .. '/' .. lng, lng} -- returns name of the page + name of the language
			else
				return base .. '/' .. lng -- returns only the page
			end
		end
	end
end

function p.autotranslate(frame) -- logic for [[template:Autotranslate|template:Autotranslate]]
	local args = frame.args
	if not args.lang or args.lang == '' then
		args.lang = frame:preprocess( "{{int:lang}}" )           -- get user's chosen language 
	end
 
	-- find base page
	local base = args.base
	if not base or base == '' then
		return '<strong class="error">Base page not provided for autotranslate</strong>' 
	end
	if string.sub(base,2,9) ~= 'emplate:' then
		base = 'Template:' .. base   -- base provided without 'Template:' part 
	end
 
	-- find base template language subpage
	local page = p.fallbackpage(base, args.lang) -- 
	if (not page and base ~= args.base) then 
		-- try the original args.base string. This case is only needed if base is not in template namespace 
		page = p.fallbackpage(args.base, args.lang) 
	end
	if not page then
		return string.format('<strong class="error">no fallback page found for autotranslate (base=[[%s|%s]], lang=%s)</strong>', args.base, args.lang)
	end
 
        -- repack args in a standard table
	newargs = {}
	for field, value in pairs(args) do
		if field ~= 'base' then
			newargs[field] = value;
		end
	end
 
	-- Transclude {{page |....}} with template arguments the same as the ones passed to {{autotranslate}} template.
        return frame:expandTemplate{ title = page, args = newargs }
end

function p.translatelua(frame)
	local lang = frame.args.lang
	local page = require('Module:' .. mw.text.trim(frame.args[1])) -- page should only contain a simple of translations
	if not lang or mw.text.trim(lang) == '' then
		lang = frame:preprocess( "{{int:lang}}" )
	end
	if frame.args[2] then
		page = page[mw.text.trim(frame.args[2])]
	end
	return p._langSwitch(page, lang)
end

function p.runTests()
	local toFallbackTest = require('Module:Fallback/tests/fallbacks')
	local result = true

	mw.log('Testing fallback chains')
	for i, t in ipairs(toFallbackTest) do
		local fbtbl = table.concat(p.fblist(t.initial), ', ')
		local expected = table.concat(t.expected, ', ')
		local ret = (fbtbl == expected)
		mw.log(i, ret and 'passed' or 'FAILED', t.initial, (not ret) and ('FAILED\nis >>' .. fbtbl .. '<<\nbut should be >>' .. expected .. '<<\n') or '')
		result = result and ret
	end
	
	return result
end

function p.showTemplateArguments(frame)
-- list all input arguments of the template that calls "{{#invoke:Fallback|showTemplateArguments}}"
	local str = ''
	for name, value in pairs( mw.getCurrentFrame():getParent().args ) do
		if str=='' then
			str = string.format('%s=%s', name, value)          -- argument #1
		else
			str = string.format('%s, %s=%s', str, name, value) -- the rest
		end
	end
	return str
end

return p