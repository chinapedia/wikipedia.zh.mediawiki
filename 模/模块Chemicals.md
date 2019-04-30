local p = {}
local origArgs
local error = require( 'Module:Error' )
local element = require( 'Module:Element' )
local strings = require( 'Module:String' )

function p.formula(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = pframe.args
	return p._formula(args)
end

function p.reaction(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = pframe.args
	return p._reaction(args)
end

function p.check_CAS(cas_no)
	arrs = strings.split(cas_no, '-', true, false)
	split_num = tonumber(table.getn(arrs))
	--avoid nil
	if (split_num and split_num  ~= '') then 
		if (split_num == 3) then 
			--cas no have 3 pattern
		else
			return 'false'
		end
	else
		--if nil
		return 'false'
	end
	cas_without_desh = arrs[1] .. arrs[2]
	
	check_length = {}    -- new array
    for seq_it=1, 3 do
      check_length[seq_it] = mw.ustring.len(arrs[seq_it])
    end
    
	if (check_length[1] < 2 or check_length[1] > 7) then return 'false' end
	if (check_length[2] ~= 2) then return 'false' end
	if (check_length[3] ~= 1) then return 'false' end
	
	cas_check = tonumber(arrs[3])
	if (cas_check and cas_check  ~= '') then 
	else
		return 'false'
	end
	cas_len = mw.ustring.len(cas_without_desh)
	cas_sum = 0
	for i = 1,cas_len do
		index = cas_len + 1 -i
		cas_symbol = tonumber(cas_without_desh:sub(index,index))
		if (cas_symbol and cas_symbol  ~= '') then 
			cas_sum = cas_sum + (cas_symbol*i)
		else
			return 'false'
		end
	end
	if ((cas_sum % 10) == cas_check) then 
		return 'true'
	else
		return 'false'
	end
	return 'false'
end

function p.check_CAS_test(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end	
	return p._check_CAS_test(args)
end

function p._check_CAS_test(args)
	-- For calling from #invoke.
	if (args[1] and args[1]  ~= '') then 
		casid = args[1]
	else
		casid = "000-00-0"
	end
	return p.check_CAS(casid)
end

function p._formula(args)
	local body = ''
	if (args['link'] and args['link']  ~= '') then link = args['link'] end
	last=''
	for v, x in ipairs(args) do 
		number=tonumber(x)
		lastn=tonumber(last)
		if(number)then
			if((not (lastn)) and last ~= '')then
				if(link and link ~= '')then 
					body = body .. element._element_symbol({last,x})
				else
					body = body .. element._elementlink({last,x})
				end
			else if(body == '' and last == '')then
				body = x .. body 
			else if (lastn)then
				if(number==1)then
					body = body .. '<sup>+</sup>'
				else if(number==-1)then
					body = body .. '<sup>-</sup>'
				else if(number>0)then
					body = body .. '<sup>'.. number ..'+</sup>'
				else if(number<0)then
					body = body .. '<sup>'.. -number ..'−</sup>'
				end end end end
			end end end
		else
			if ((not (lastn)) and last ~= '') then
				if(link and link ~= '')then 
					body = body .. element._element_symbol({last})
				else
					body = body .. element._elementlink({last})
				end
			end
		end
		last=x
	end
	lastn=tonumber(last)
	if ((not (lastn)) and last ~= '') then
		if(link and link ~= '')then 
			body = body .. element._element_symbol({last})
		else
			body = body .. element._elementlink({last})
		end
	end
	if(link and link ~= '')then
		if(link ~= '#')then
			body = '[['_.._link_.._'|' .. body ..']]'
		end
	end
	return body
end

function p._reaction(args)
	local body = ''
	last=''
	for v, x in ipairs(args) do 
		number=tonumber(x)
		lastn=tonumber(last)
		if(number)then
			if((not (lastn)) and last ~= '')then
				feq = ''
				if(number>1)then feq = feq .. number end
				if (last == '+') then
					body = body .. ' + ' .. feq
				elseif (last == 'eq' or last == '→') then
					body = body .. ' → ' .. feq
				elseif (last == '↑') then
					body = body .. '↑ ' .. feq
				elseif (last == '↓') then
					body = body .. '↓ ' .. feq
				elseif (last == 'eqm') then
					body = body .. ' [[File:Equilibrium.svg|15px]] ' .. feq
				else
					body = body .. element._elementlink({last,x})
				end
			else if(body == '' and last == '')then
				body = x .. body 
			else if (lastn)then
				if(number==1)then
					body = body .. '<sup>+</sup>'
				elseif(number==-1)then
					body = body .. '<sup>-</sup>'
				elseif(number>0)then
					body = body .. '<sup>'.. number ..'+</sup>'
				elseif(number<0)then
					body = body .. '<sup>'.. -number ..'−</sup>'
				end
			else
				body = last .. x .. body 
			end end end
		else
			if ((not (lastn)) and last ~= '') then
				if (last == '+') then
					body = body .. ' + '
				elseif (last == 'eq' or last == '→') then
					body = body .. ' → '
				elseif (last == '↑') then
					body = body .. '↑ '
				elseif (last == '↓') then
					body = body .. '↓ ' 
				elseif (last == 'eqm') then
					body = body .. ' [[File:Equilibrium.svg|15px]] '
				else
					body = body .. element._elementlink({last})
				end
			end
		end
		last=x
	end
	lastn=tonumber(last)
	if ((not (lastn)) and last ~= '') then
		if (last == '+') then
			body = body .. ' + '
		elseif (last == 'eq' or last == '→') then
			body = body .. ' → '
		elseif (last == '↑') then
				body = body .. '↑ '
		elseif (last == '↓') then
				body = body .. '↓ ' 
		elseif (last == 'eqm') then
			body = body .. ' [[File:Equilibrium.svg|15px]] '
		else
			body = body .. element._elementlink({last})
		end
	end
	return body
end

--本模塊的沙盒(測試)函數
function p.sandbox(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	local args = pframe.args
	return p._reaction(args)
end
function p._sandbox(args)
	return element_data[p.getListID(args[1])].name 
end
return p