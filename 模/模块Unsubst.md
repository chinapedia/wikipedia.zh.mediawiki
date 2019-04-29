local p = {}

local specialParams = {
	['$N'] = 'template name', -- Deprecated, but keeping until it is removed from transcluding templates
	['$B'] = 'template content',
}

p[''] = function ( frame )
	if not frame:getParent() then
		error( '{{#invoke:Unsubst|}} makes no sense without a parent frame' )
	end
	if not frame.args['$B'] then
		error( '{{#invoke:Unsubst|}} requires parameter $B (template content)' )
	end
	
	if mw.isSubsting() then
		---- substing
		-- Combine passed args with passed defaults
		local args = {}
		for k, v in pairs( frame.args ) do
			if not specialParams[k] then
				if v == '__DATE__' then
					v = mw.getContentLanguage():formatDate( 'Y年n月' )
				end
				args[k] = v
			end
		end
		for k, v in pairs( frame:getParent().args ) do
			args[k] = v
		end

		-- Build an equivalent template invocation
		-- First, find the title to use
		local titleobj = mw.title.new(frame:getParent():getTitle())
		local title
		if titleobj.namespace == 10 then -- NS_TEMPLATE
			title = titleobj.text
		elseif titleobj.namespace == 0 then -- NS_MAIN
			title = ':' .. titleobj.text
		else
			title = titleobj.prefixedText
		end

		-- Build the invocation body with numbered args first, then named
		local ret = '{{' .. title
		for k, v in ipairs( args ) do
			if string.find( v, '=', 1, true ) then
				-- likely something like 1=foo=bar, we need to do it as a named arg
				break
			end
			ret = ret .. '|' .. v
			args[k] = nil
		end
		for k, v in pairs( args ) do
			ret = ret .. '|' .. k .. '=' .. v
		end
		
		return ret .. '}}'
	else
		---- Not substing
		-- Just return the "body"
		return frame.args['$B'] .. (frame.args['$N'] and frame:getParent():getTitle() == mw.title.getCurrentTitle().prefixedText and '[[Category:使用$N的Module:Unsubst调用|Category:使用$N的Module:Unsubst调用]]' or '')
	end
end

return p