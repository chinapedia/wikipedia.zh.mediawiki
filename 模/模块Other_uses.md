local mHatnote = require('Module:Hatnote')
local mHatlist = require('Module:Hatnote list')
local mArguments --initialize lazily
local mTableTools --initialize lazily
local libraryUtil = require('libraryUtil')
local checkType = libraryUtil.checkType
local p = {}

-- Produces standard {{other uses}} implementation
function p.otheruses(frame)
	mArguments = require('Module:Arguments')
	mTableTools = require('Module:TableTools')
	local args = mTableTools.compressSparseArray(mArguments.getArgs(frame))
	local title = mw.title.getCurrentTitle().text
	return p._otheruses(args, {title=title})
end

-- Main generator
function p._otheruses(args, options)
	--Type-checks and defaults
	checkType('_otheruses', 1, args, 'table', true)
	args = args or {}
	checkType('_otheruses', 2, options, 'table')
	if not (options.defaultPage or options.title) then
		error('No default title data provided in "_otheruses" options table', 2)
	end
	local emptyArgs = true
	for k, v in pairs(args) do
		if type(k) == 'number' then emptyArgs = false break end
	end
	if emptyArgs then
		args = {
			options.defaultPage or
			mHatnote.disambiguate(options.title, options.disambiguator)
		}
	end
	--Generate and return hatnote
	local text = mHatlist.forSeeTableToString({{
		use = options.otherText and "關於與XXX名稱相近或相同的條目，詳見 " .. options.otherText or nil,
		pages = args
	}})
	return mHatnote._hatnote(text)
end

return p