-- This module may be used to compare the arguments passed to the parent
-- with a list of arguments, returning a specified result if an argument is
-- not on the list
local p = {}

local function trim(s)
	return s:match('^%s*(.-)%s*$')
end

local function isnotempty(s)
	return s and trim(s) ~= ''
end

function p.check (frame)
	local args = frame.args
	local pargs = frame:getParent().args
	local ignoreblank = isnotempty(frame.args['ignoreblank'])
	local showblankpos = isnotempty(frame.args['showblankpositional'])
	local knownargs = {}
	local unknown = frame.args['unknown'] or 'Found _VALUE_, '
	local preview = frame.args['preview']

	local values = {}
	local res = {}
	local regexps = {}

	-- create the list of known args, regular expressions, and the return string
	for k, v in pairs(args) do
		if type(k) == 'number' then
			v = trim(v)
			knownargs[v] = 1
		elseif k:find('^regexp[1-9][0-9]*$') then
			table.insert(regexps, '^' .. v .. '$')
		end
	end
	if isnotempty(preview) then 
		preview = '<div class="hatnote" style="color:red"><strong>警告：</strong>' .. preview .. '（此信息仅在预览中显示）。</div>'
	elseif preview == nil then
		preview = unknown
	end

	-- loop over the parent args, and make sure they are on the list
	for k, v in pairs(pargs) do
		if type(k) == 'string' and knownargs[k] == nil then
			local knownflag = false
			for i, regexp in ipairs(regexps) do
				if mw.ustring.match(k, regexp) then
					knownflag = true
					break
				end
			end
			if not knownflag and ( not ignoreblank or isnotempty(v) )  then
				k = mw.ustring.gsub(k, '[^%w\-_ ]', '?')
				table.insert(values, k)
			end
		elseif type(k) == 'number' and 
			knownargs[tostring(k)] == nil and
			( showblankpos or isnotempty(v) )
		then
			local vlen = mw.ustring.len(v)
			v = mw.ustring.sub(v, 1, (vlen < 25) and vlen or 25) 
			v = mw.ustring.gsub(v, '[^%w\-_ ]', '?')
			table.insert(values, k .. ' = ' .. v .. ((vlen >= 25) and ' ...' or ''))
		end
	end

	-- add resuls to the output tables
	if #values > 0 then
		if frame:preprocess( "{{REVISIONID}}" ) == "" then
			unknown = preview
		end
		for k, v in pairs(values) do
			if v == '' then
			-- Fix odd bug for | = which gets stripped to the empty string and
			-- breaks category links
			v = ' '
			end
			local r =  unknown:gsub('_VALUE_', v)
			table.insert(res, r)
		end
	end

	return table.concat(res)
end

return p