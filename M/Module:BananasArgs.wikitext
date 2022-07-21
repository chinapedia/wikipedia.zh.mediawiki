--示例模組，更多資料參見http://www.mediawiki.org/wiki/Extension:Scribunto/Lua_reference_manual#Frame_object
-- Unit tests at Module:BananasArgs/testcases
 
local p = {}
 
-- No arguments, used like: {{#invoke:BananasArgs|hello_world}}
function p.hello_world()
	return "Hello, world!"
end
 
-- One argument, used like: {{#invoke:BananasArgs|hello|Fred}} 
function p.hello(frame)
	local name = frame.args[1] -- in this example, args[1] is the word Fred 
	return "Hello, " .. name .. "!" -- .. name .. replace by the word Fred
end
 
-- Two arguments, used like: {{#invoke:BananasArgs|add|5|3}}
function p.add(frame)
	local num1 = tonumber(frame.args[1])
	local num2 = tonumber(frame.args[2])
	return num1 + num2
end
 
-- Named arguments, used like: {{#invoke:BananasArgs|count_fruit|bananas=5|apples=3}}
function p.count_fruit(frame)
	local num_bananas = frame.args.bananas
	local num_apples = frame.args.apples
	return 'I have ' .. num_bananas .. ' bananas and ' .. num_apples .. ' apples'
end
 
-- Mixing regular args with named args and optional named args
-- Used like: {{#invoke:BananasArgs|has_fruit|Fred|bananas=5|cherries=7}}
function p.has_fruit(frame)
	local name = frame.args[1]
	local num_bananas = frame.args.bananas
	local num_apples = frame.args.apples
	local num_cherries = frame.args.cherries
 
	local result = name .. ' has:'
	if num_bananas then result = result .. ' ' .. num_bananas .. ' bananas' end
	if num_apples then result = result .. ' ' .. num_apples .. ' apples' end
	if num_cherries then result = result .. ' ' .. num_cherries .. ' cherries' end
	return result
end
 
-- Iterating over args, used like: {{#invoke:BananasArgs|custom_fruit|pineapples=10|kiwis=5}}
function p.custom_fruit(frame)
	local result = 'I have:'
	for name, value in pairs(frame.args) do
		result = result .. ' ' .. value .. ' ' .. name
	end
	return result
end
 
-- Iterating over args with separate mandatory args
-- Used like: {{#invoke:BananasArgs|custom_fruit_2|Fred|pineapples=10|kiwis=5}}
function p.custom_fruit_2(frame)
	local name = frame.args[1]
	local result = name .. ' has:'
	for name, value in pairs(frame.args) do
		if name ~= 1 then
			result = result .. ' ' .. value .. ' ' .. name
		end
	end
	return result
end
 
return p