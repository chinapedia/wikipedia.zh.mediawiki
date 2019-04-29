local z = {}
local sha1 = require( 'Module:Sha1' )

function z.hash( frame )
	local args = frame:getParent().args
	local hash_text = {}
	for k, v in ipairs( { 'article', 'question', 'image', 'type', 'author', 'nominator', 'timestamp' } ) do
		hash_text[k] = sha1.binary(args[v] or '')
	end
	return sha1.sha1( table.concat( hash_text ) )
end

function z.normalize( frame ) 
	local res = '{{ DYKEntry\n'
	local complaints = {''} -- 初始用一個空字串，到時候concat就自動加\n了（超懶的）
	local newargs = {}
	setmetatable(newargs, {
		["__index"] = function (t, key) 
			return (frame.args[key]):gsub( '\n', ' ' )
		end
	})
	
	-- 總有人（例如加入這段代碼的 Artoria2e5）不小心加 File:
	if type(frame.args['image']) == 'string' then
		-- strlen('File:') == 5
		local img = mw.text.trim(frame.args['image'])
		if img:sub(1, 5):lower() == 'file:' then
			newargs['image'] = img:sub(6)
		end
	end
	
	-- Normalize to lowercase, warn against Chinese
	-- (Being UTF-8-dumb here is good)
	if type(frame.args['type']) == 'string' then
		newargs['type'] = mw.text.trim(frame.args['type']):lower()
		local i, j = newargs['type']:find('[^\1-\127]+') -- No \0 for Lua
		if i ~= nil then
			table.insert(complaints, "** <font color=orange>'''警告'''：類名含有非ASCII字元，請使用英文類名</font>" ..
								     "(bytes " ..  tostring(i) .. " to " .. tostring(j) .. ")")
                end

		local i, j = newargs['type']:find('%s+')
		if i ~= nil then
			table.insert(complaints, "** <font color=orange>'''警告'''：類名含有空白字元，請保持簡略並避免過度細分</font>" ..
								     "(bytes " ..  tostring(i) .. " to " .. tostring(j) .. ")")
		end
	else
		table.insert(complaints, "** <font color=red>'''錯誤'''：未提供類名</font>")
	end
	
	for k, _ in pairs( frame.args ) do
		res = res .. ' | ' .. k .. ' = ' .. newargs[k] .. '\n'
	end
	return res .. '}}' .. (#complaints > 1 and table.concat(complaints, '\n') or '')
end

return z