-- This module counts table rows in wikitext.

local p = {}
local getArgs

function p.main(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	return p._main(getArgs(frame, {wrappers = 'Template:Table row counter'}))
end

function p._main(args)
	-- Get the title object.
	local titleObj
	do
		local success
		success, titleObj = pcall(mw.title.new, args.page)
		if not success or not titleObj then
			titleObj = mw.title.getCurrentTitle()
		end
	end

	-- Get the page content.
	local content = titleObj:getContent()
	if not content then
		return nil
	end

	-- Find the wikitables on that page.
	local wikitables = {}
	do
		local iWikitable = 0
		local s1 = content:match('^({|.-\n|})')
		if s1 then
			iWikitable = iWikitable + 1
			wikitables[iWikitable] = s1
		end
		for s in content:gmatch('\n({|.-\n|})') do
			iWikitable = iWikitable + 1
			wikitables[iWikitable] = s
		end
	end

	-- Find the wikitable to work on.
	local wikitable
	if args.id then
		for i, s in ipairs(wikitables) do
			if s:match('^{|[^\n]*id *= *" *(%w+) *"') == args.id then
				wikitable = s
				break
			end
		end
	else
		wikitable = wikitables[tonumber(args.tableno) or 1]
	end
	if not wikitable then
		return nil
	end

	-- Count the number of rows.
	local count
	do
		local temp
		temp, count = wikitable:gsub('\n|%-', '\n|-')
	end

	-- Count the number of empty last column
	local emptylastcolumn 
	do
		local temp
		temp, emptylastcolumn = wikitable:gsub('||%s*\n|%-', '||\n|-')
	end

	-- Control for missing row markers at the start.
	if not wikitable:find('^{|[^\n]*%s*\n|%-') then
		count = count + 1
	end

	-- Control for extra row markers at the end.
	if wikitable:find('\n|%-[^\n]-%s*\n|}$') then
		count = count - 1
	end

	-- Subtract the number of rows to ignore, and make sure the result isn't
	-- below zero.
	count = count - (tonumber(args.ignore) or 0)
	if args.ignoreempty then
		count = count - emptylastcolumn
	end
	if count < 0 then
		count = 0
	end
	return count
end

return p