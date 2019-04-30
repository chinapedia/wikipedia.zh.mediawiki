local p = {}

local specialParams = {
	['$params'] = 'all parameters',
	['$extra'] = 'extra parameters',
	['$set1'] = 'parameter set 1',
	['$set2'] = 'parameter set 2',
	['$set3'] = 'parameter set 3',
	['$aliases'] = 'parameter aliases',
	['$indent'] = 'indent',
	['$flags'] = 'flags',
	['$B'] = 'template content'
}

p[''] = function ( frame )
	if not frame:getParent() then
		error( '{{#invoke:Unsubst-infobox|}} makes no sense without a parent frame' )
	end
	if not frame.args['$B'] then
		error( '{{#invoke:Unsubst-infobox|}} requires parameter $B (template content)' )
	end
	if not frame.args['$params'] then
		error( '{{#invoke:Unsubst-infobox|}} requires parameter $params (parameter list)' )
	end

	if mw.isSubsting() then
		---- substing
		-- Combine passed args with passed defaults
		local args = {}
		if string.find( ','..(frame.args['$flags'] or '')..',', ',%s*override%s*,' ) then
			for k, v in pairs( frame:getParent().args ) do
				args[k] = v
			end
			for k, v in pairs( frame.args ) do
				if not specialParams[k] then
					if v == '__DATE__' then
						v = mw.getContentLanguage():formatDate( 'Y年n月' )
					end
					args[k] = v
				end
			end
		else
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

		-- Remove empty fields
		for k, v in pairs( args ) do
			if v == '' then args[k] = nil end
		end

		-- Pull information from parameter aliases
		local aliases = {}
		if frame.args['$aliases'] then
			local list = mw.text.split( frame.args['$aliases'], '%s*,%s*' )
			for k, v in ipairs( list ) do
				local tmp = mw.text.split( v, '%s*>%s*' )
				aliases[(tonumber(mw.ustring.match(tmp[1], '^[1-9][0-9]*$'))) or tmp[1]] = ((tonumber(mw.ustring.match(tmp[2], '^[1-9][0-9]*$'))) or tmp[2])
			end
		end
		for k, v in pairs( aliases ) do
			if args[k] and not args[v] then args[v], args[k] = args[k], nil end
		end

		-- Build the invocation body with numbered args first, then named
		local ret = '{{' .. title
		for k, v in ipairs( args ) do
			if mw.ustring.find( v, '=', 1, true ) then
				-- likely something like 1=foo=bar, we need to do it as a named arg
				break
			end
			if not aliases[k] then
				ret = ret .. '|' .. v
				args[k] = nil
			end
		end

		-- Pull lists from special parameters
		local params = mw.text.split( frame.args['$params'], '%s*,%s*' )
		for k, v in ipairs( params ) do
			params[k] = (tonumber(mw.ustring.match(v, '^[1-9][0-9]*$'))) or v
		end
		local sets, setparams, extra = {{}, {}, {}}, {}, {}
		for k = 1, 3 do
			local v = frame.args['$set' .. k]
			if v then
				setparams[k] = mw.text.split( v, '%s*,%s*' )
				for x, y in ipairs( setparams[k] ) do
					setparams[k][x] = (tonumber(mw.ustring.match(y, '^[1-9][0-9]*$'))) or y
					sets[k][setparams[k][x]] = true
				end
			end
		end
		if frame.args['$extra'] then
			local tmp = mw.text.split( frame.args['$extra'], '%s*,%s*' )
			for k, v in ipairs( tmp ) do extra[(tonumber(mw.ustring.match(v, '^[1-9][0-9]*$'))) or v] = true end
		end

		-- Replace parameter list with short version if full version not necessary
		local tmp = {}
		for k, v in ipairs( sets ) do
			if next(v) then  -- if table v is not empty
				for _, x in ipairs( params ) do
					if args[x] and not v[x] then
						tmp[k] = true
						break
					end
				end
				if not tmp[k] then params = setparams[k] end
			end
		end

		-- Align parameters correctly and remove extra ones
		local maxlength = 0
		local discard = {}
		for k, v in ipairs( params ) do
			if (not extra[v]) or args[v] then
				local tmp = mw.ustring.len( tostring( v ) )
				if tmp > maxlength then maxlength = tmp end
			else
				table.insert( discard, 1, k )
			end
		end
		for k, v in ipairs( discard ) do table.remove( params, v ) end
		local indent = string.rep(' ', (tonumber(frame.args['$indent']) or 0))
		
		local space, newline = ' ', '\n'
		if not next(params) then space, newline = '', '' end

		for k, v in ipairs( params ) do
			local tmp = space
			if mw.ustring.match( mw.ustring.sub( ( args[v] or '' ) .. ' ', 1, 1 ), '[%*:;#]' ) then tmp = '\n' end
			ret = ret .. newline .. indent .. '|' .. space .. v .. string.rep(' ', (maxlength - mw.ustring.len( v ))) .. space .. '=' .. tmp .. (args[v] or '')
		end
		
		ret = ret .. newline .. '}}'

		ret = mw.ustring.gsub(ret, '%s+\n', '\n')

		return ret
	else
		-- Not substing
		-- Just return the "body"
		return frame.args['$B']
	end
end

return p