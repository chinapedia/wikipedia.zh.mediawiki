require('Module:No globals')

local p = {}

local Sidebar = require('Module:Sidebar')
local Navbox = require('Module:Navbox')

function p.main(frame)
	local getArgs = require('Module:Arguments').getArgs
	local args = getArgs(frame)
	local footer = args['footer']
	local i, j, ni, k, v
	
	-- process the groups and lists
	local groups, lists, nums = {}, {}, {}
	for k,v in pairs(args) do
		if type(k) == 'string' and k:match('^list[0-9][0-9]*_[0-9][0-9]*$') then
			i = mw.ustring.gsub(k,'^list([0-9][0-9]*)_([0-9][0-9]*)$', '%1')
			j = mw.ustring.gsub(k,'^list([0-9][0-9]*)_([0-9][0-9]*)$', '%2')
			i = tonumber(i)
			j = tonumber(j)
			if lists[i] == nil then	
				lists[i] = {}
				if groups[i] == nil then
					table.insert(nums, i)
				end
			end
			lists[i][j] = v
		elseif type(k) == 'string' and k:match('^group[0-9][0-9]*$') then
			local i = mw.ustring.gsub(k,'^group([0-9][0-9]*)$', '%1')
			i = tonumber(i)
			if groups[i] == nil and lists[i] == nil then
				table.insert(nums, i)
			end
			groups[i] = v
		end
	end
	-- sort the group and list numbers
	table.sort(nums)
	
	-- table for args passed to sidebar or navbox
	local targs = {}
	for ni = 1, #nums do
		i = nums[ni]
		if footer then
			if lists[i] then
				if groups[i] then
					targs['group' .. i] = args['group' .. i]
				end
				targs['list' .. i] = ''
				for k,v in pairs(lists[i]) do
					targs['list' .. i] = targs['list' .. i] .. '* ' .. args['list' .. i .. '_' .. k] .. '\n'
				end
			else
				lists[i] = '\'\'\'' .. args['group' .. i] .. '\'\'\''
			end
		else
			if groups[i] then
				targs['heading' .. i] = args['group' .. i]
			end
			if lists[i] then
				local leven, lodd = '', ''
				for k,v in pairs(lists[i]) do
					if math.fmod(tonumber(k), 2) == 0 then
						leven = leven .. '* ' .. args['list' .. i .. '_' .. k] .. '\n'
					else
						lodd = lodd .. '* ' .. args['list' .. i .. '_' .. k] .. '\n'
					end
				end
				if leven ~= '' and lodd ~= '' then
					local cb = frame:expandTemplate{ title = 'col-begin' }
					local c2 = frame:expandTemplate{ title = 'col-2' }
					local ce = frame:expandTemplate{ title = 'col-end' }
					targs['content' .. i] = cb .. '\n' .. c2 .. '\n' .. lodd .. c2 .. '\n' .. leven .. ce
				else
					targs['content' .. i] = lodd .. leven
				end
			end
		end
	end
	
	targs['name'] = args['name'] or mw.title.getCurrentTitle().text
	targs['title'] = args['title'] or '{{{title}}}'
	if footer then
		targs['listclass'] = 'hlist'
		targs['state'] = args['state'] or 'autocollapse'
		return Navbox._navbox(targs)
	else
		targs['style'] = 'width: 30em; text-align: left;'
		targs['class'] = 'collapsible'
		targs['wraplinks'] = 'true'
		targs['titlestyle'] = 'font-size: 100%; background-color:lavender; text-align:center;'
		return Sidebar.sidebar(frame, targs)
	end
end

return p