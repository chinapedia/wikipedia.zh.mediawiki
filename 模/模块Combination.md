local p = {}

function p.getCombinationGenerator()
	CombinationGenerator = {
		list = {},
		nums = {},
		count = 0,
		number_count={},
		factors={},
		factor_index={}
	}
	function CombinationGenerator:init(prime_factors,fill_count)
		self.count=fill_count
		self.nums = {}
		for first,second in pairs(prime_factors) do
			if first ~= 'has_err' then 
				self.nums[#(self.nums) + 1] = first 
				self.number_count[first] = 0
				self.factors[first] = second
			end
		end
		table.sort(self.nums)
		for i = 1,#(self.nums) do
			self.factor_index[self.nums[i]]=i
		end
	end
	function CombinationGenerator:fill()
		if self.count <= 0 then return end
		local iterator = 1
		local now_number = self.nums[iterator]
		if #(self.list) > 0 then
			iterator = self.factor_index[self.list[#(self.list)]]
			now_number = self.nums[iterator]
		end
		while #(self.list) < self.count do
			--test a number 'now_number'
			if self.number_count[now_number] < self.factors[now_number] then
				--if number 'now_number' can be put
				self.list[#(self.list) + 1] = now_number
				self.number_count[now_number] = self.number_count[now_number] + 1
			else
				--if number 'now_number' can NOT be put
				if iterator + 1 > #(self.nums) then break end
				iterator = iterator + 1
				now_number = self.nums[iterator]
			end
		end
	end
	function CombinationGenerator:checkNumberCount()
		if self.count <= 0 then return end
		for i = 1,#(self.nums) do
			self.number_count[self.nums[i]] = 0
		end
		for i = 1,#(self.list) do
			self.number_count[self.list[i]] = self.number_count[self.list[i]] + 1
		end
	end
	function CombinationGenerator:set(input)
		local result = {}
		if xpcall(function()_=#input pairs(input) end,function(_)end) == true then
			for key,value in pairs(input) do
				if tostring(tonumber(tostring(key)) or 0) == tostring(key) then 
					result[key] = value
				end
			end
			self.list = result
		end
		self:checkNumberCount()
	end
	function CombinationGenerator:next()
		if #(self.list) > 0 then
			local iterator = self.factor_index[self.list[#(self.list)]]
			local now_number = self.nums[iterator]
			if iterator + 1 > #(self.nums) then return false end
			self.number_count[now_number] = self.number_count[now_number] - 1
			iterator = iterator + 1
			now_number = self.nums[iterator]
			self.number_count[now_number] = self.number_count[now_number] + 1
			self.list[#(self.list)] = now_number
			return true
		end
		return false
	end
	function CombinationGenerator:copyListTo(newlist)
		if xpcall(function()_=#newlist pairs(newlist) end,function(_)end) == true then
			for key,value in pairs(self.list) do
				if tostring(tonumber(tostring(key)) or 0) == tostring(key) then 
					newlist[key] = value
				end
			end
		end
	end
	function CombinationGenerator:findSubset(min_ele,max_ele)
		local outside_flag = true;
		local result = {}
		local end_val = tonumber(max_ele) or -1
		if (tonumber(min_ele) or -1) <= 0 then self.count = 0 else self.count = min_ele end
		if end_val >= 0 and self.count > end_val then return result end
		
		if #(self.nums) <= 0 then 
			if self.count <= 0 then result[#result + 1] = {} end
			return result 
		end
		
		self:set({nil})
		while outside_flag == true and (end_val < 0 or self.count <= end_val) do
			result, outside_flag = self:findCombination(nil, result, outside_flag)
			self.count = self.count + 1
		end
		return result
	end
	function CombinationGenerator:findCombination(item_count, input_array, outside_flag)
		local result = input_array or {}

		if item_count ~= nil then self.count = item_count end
		
		if #(self.nums) <= 0 then 
			if self.count <= 0 then result[#result + 1] = {} end
			return result 
		end
		
		if self.count <= 0 then
			self:set({nil})
			result[#result+1] = {}
			self:copyListTo(result[#result])
		else
			self:set({nil})
			self:fill()

			local middle_flag = true;
			while middle_flag == true do
				local inside_flag = true;
				while inside_flag == true do
					if (#(self.list) < self.count) then
						outside_flag = false
						break
					end
					result[#result+1] = {}

					self:copyListTo(result[#result])
					inside_flag = self:next()
				end

				local backtrack_flag = true;
				while backtrack_flag == true do

					local recursive_test = {value = tostring(table.concat(self.list,','))}
					local delete_num = self.list[#(self.list)]
					self.number_count[delete_num] = self.number_count[delete_num] - 1
					self.list[#(self.list)] = nil
					recursive_test.count = #(self.list)
					if #(self.list) <= 0 then break end
					middle_flag = self:next()

					self:fill()

					local in_check,_ = mw.ustring.sub( tostring(table.concat(self.list,',')), 1, #tostring(recursive_test.value))

					if ( 
						tostring(in_check) == recursive_test.value 
					) == true then
						while #(self.list) > recursive_test.count do
							self.list[#(self.list)] = nil
							self:checkNumberCount();
						end
					end

					backtrack_flag = (#(self.list) < self.count) or #(self.list) <= 0
				end
				if #(self.list) <= 0 then break end
			end
		end
		return result, outside_flag
	end
	return CombinationGenerator
end

function p.subset(inputstr)
	--#invoke 支援
		if not getArgs then getArgs = require('Module:Arguments').getArgs end
		args = getArgs(inputstr, {parentFirst=true})
		local t_vals = {}
		local t_args = {}
		for arg_name, arg_value in pairs( args ) do
			if tostring(mw.ustring.sub(arg_name,1,1)) == '\\' then
				if tostring(mw.ustring.sub(arg_name,2,2)) == '\\' then
					if (tonumber(arg_value)~=nil) then
						t_vals[tostring(mw.ustring.sub(arg_name,2))] = tonumber(arg_value)
					else
						t_args[tostring(mw.ustring.sub(arg_name,2))] = arg_value
					end
				else
					t_args[tostring(mw.ustring.sub(arg_name,2))] = arg_value
				end
			else
				if (tonumber(arg_value)~=nil) then
					t_vals[arg_name] = tonumber(arg_value)
				else
					t_args[arg_name] = arg_value
				end
			end
		end
		empty_set = "[[空集|空集合]]";
		format = "*{{{1}}}\n";
		for arg_name, arg_value in pairs( t_args ) do
			if arg_name == "format" then
				format = arg_value or "*{{{1}}}\n";
			elseif arg_name == "min" then
				min_val = tonumber(arg_value) or 0;
			elseif arg_name == "max" then
				max_val = tonumber(arg_value);
			elseif arg_name == "empty" or arg_name == "empty set" or arg_name == "empty_set" then
				empty_set = arg_value or "[[空集|空集合]]";
			elseif arg_name == "no_output" or arg_name == "no output" then
				no_output = arg_value;
			end
		end
		if not yesno then yesno = require('Module:Yesno') end
		no_output = yesno( no_output or 'no' )
		format = mw.ustring.gsub(format or "*{{{1}}}\n", "%{%{%{.-%}%}%}", "%%s" );
		it = mw.ustring.find(format, "%%s", 1)
		if(not no_output) then
			if it == nil then format = format .. "%s" end
		end
		format = mw.ustring.gsub(format, "\\n", "\n")
	local result = {}
	local gened=require('Module:Combination').getCombinationGenerator()

	gened:init(t_vals,0)
	local combination = gened:findSubset(min_val,max_val)

	body = ''
	for i, result_str in pairs( combination ) do
		if(not no_output) then
			if #result_str <= 0 then body = body .. mw.ustring.gsub(format, "%%s", empty_set) else
				 body = body .. mw.ustring.gsub(format, "%%s", table.concat(result_str,'')) 
			end
		else
			body = body .. format
		end
	end
	return body
end

return p