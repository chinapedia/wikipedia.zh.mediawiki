local p = {}
local error = require( 'Module:Error' )

local function makeRandomComment()
	return '<!-- Module:ExpandTemplates # ' .. math.random() .. ' -->'
end

local function stripRandomComment( text )
	return mw.ustring.gsub( text, '<!%-%- Module:ExpandTemplates # [%d.]+ %-%->', '' )
end

local function doTitle( frame, title )
	if title == mw.title.getCurrentTitle() and not mw.isSubsting() then
		return error.error{ message = 'Module:ExpandTemplates on current title must be substed.' }
	end
	local text = title:getContent()
	if text == nil then
		return ''
	end
	-- frame:preprocess instead of expandTemplate so that <includeonly>s are not in transclusion mode
	-- and unfortunately it's impossible to specify a context title here...
	text = frame:preprocess( text )
	text = mw.text.unstrip( text )
	return stripRandomComment( text ) .. makeRandomComment()
end

function p.self( frame )
	return doTitle( frame, mw.title.getCurrentTitle() )
end

function p.page( frame )
	return doTitle( frame, mw.title.new( frame.args[1] ) )
end

return p