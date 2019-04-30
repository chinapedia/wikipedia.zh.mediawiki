local p = {}

local separators = {
	dot = true,
	pipe = true,
	comma = true,
	['tpt-languages'] = true
}

local function getSeparator(sep)
	if type(sep) ~= 'string' then
		return nil
	end
	if separators[sep] then
		return mw.message.new(sep .. '-separator'):plain()
	else
		return sep
	end
end

local function generateLink(page, nspace, delim, endDelim)
	if not page then
		return nil
	end
	local pagename = mw.title.new(page)
	if not pagename then
		-- Default to the args we were passed if our page
		-- object was nil.
		pagename = page
	else
		pagename = pagename.text
	end
	delim = delim or ''
	endDelim = endDelim or delim
	nspace = nspace or ''
	if nspace == 'all' then
		nspace = ''
		pagename = page
	end
	local outStr = mw.ustring.gsub( 
		string.format( 
			'%s[[:%s:%s|%s]]%s',
			delim, nspace, pagename, page, endDelim
		),
		 ':+',
		 ':' 
	)
	return outStr
end

function p._main(args)
	local t = {}
	local separator = getSeparator(args.separator)
	local conjunction = getSeparator(args.conjunction)
	for i, v in ipairs(args) do
		table.insert(t, generateLink(
			v, args.nspace, args.delim, args.edelim
		))
	end
	return mw.text.listToText(t, separator, conjunction)
end

function p.main(frame)
	local origArgs = require('Module:Arguments').getArgs(frame, {
		trim = false,
		removeBlanks = false,
		wrappers = 'Template:Pagelist'
	})

	-- Process integer args. Allow for explicit positional arguments that are
	-- specified out of order, e.g. {{br separated entries|3=entry3}}.
	-- After processing, the args can be accessed accurately from ipairs.
	local args = {}
	for k, v in pairs(origArgs) do
		if type(k) == 'number' and 
			k >= 1 and
			math.floor(k) == k and
			string.match(v, '%S') then -- Remove blank or whitespace values.
			table.insert(args, k)
		end
	end
	table.sort(args)
	for i, v in ipairs(args) do
		args[i] = origArgs[v]
		-- Trim whitespace.
		if type(args[i]) == 'string' then
			args[i] = mw.text.trim(args[i])
		end
	end

	-- Get old named args. We don't need to remove blank values
	-- as for the nspace and edelim parameters the behaviour is different
	-- depending on whether the parameters are blank or absent, and for
	-- the delim parameter the default should be the blank string anyway.
	args.delim = origArgs.delim
	args.edelim = origArgs.edelim
	args.nspace = origArgs.nspace

	-- Get new named args, "separator" and "conjunction", and strip blank values.
	if origArgs.separator and origArgs.separator ~= '' then
		args.separator = origArgs.separator
	end
	if origArgs.conjunction and origArgs.conjunction ~= '' then
		args.conjunction = origArgs.conjunction
	end

	return p._main(args)
end

return p