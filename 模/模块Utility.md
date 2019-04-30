
local utils = {}

--[[

Number of elements in a dictionary

--]]

function utils.tablelength(T)
  local count = 0
  for _ in pairs(T) do count = count + 1 end
  return count
end


--[[

New table without first element

--]]

function utils.tail(list)
    return { select(2, unpack(list)) }
end


function utils.tableConcat(t1,t2)
    for i=1,#t2 do
        t1[#t1+1] = t2[i]
    end
    return t1
end


--[[

A class intended to serve as a set to quickly test whether an element belongs to a list or set

--]]

local Set = {} -- the table representing the class, which will double as the metatable for the instances
Set.__index = Set -- failed table lookups on the instances should fallback to the class table, to get methods

function Set:new(init, o)
    local obj = o or {} 
    setmetatable(obj, self)
    
    obj.value = init
    obj.prop_set = {}
    
    for _, val in pairs(init) do
    	obj.prop_set[val] = true
    end

    return obj
end

function Set:is_in(key)
    return self.prop_set[key] ~= nil
end

utils.Set = Set


-- table.filter({"a", "b", "c", "d"}, function(o, k, i) return o >= "c" end)  --> {"c","d"}
--
-- @FGRibreau - Francois-Guillaume Ribreau
-- @Redsmin - A full-feature client for Redis http://redsmin.com

-- https://gist.github.com/fnchooft/77779d80d6668e8eeb3043dad215575a

local function filter (t, filterIter)
  local out = {}

  for k, v in pairs(t) do
    if filterIter(v, k, t) then out[k] = v end
  end

  return out
end

utils.filter = filter 

--[[
	Functional programming, application of a function on each element of a table
	map(f,{a, b, c, ...}) = {f(a), f(b), f(c), ...} 
--]]



local function map(func, array)
  local new_array = {}
  for i,v in ipairs(array) do
    new_array[i] = func(v)
  end
  return new_array
end

utils.map = map

function utils.formatTableWithLastSep(vector, sep, lastsep)
	local descr = table.concat(vector, sep, 1, #vector-1)
	if #vector > 1 then
		descr = descr .. lastsep .. vector[#vector]
	else 
		descr = vector[1]
	end
	return descr
end

local function dump_to_console(val, indent)
	indent = indent or ""
	if type(val) == "table" then
		for a, b in pairs(val) do
			mw.log(indent .. a .. "=>")
			dump_to_console(b, indent .. "   ") 
		end
	else
		mw.log(indent .. tostring(val))
	end
end

utils.dump_to_console = dump_to_console
utils.dump = dump_to_console

-- some functions useful in lua


local function splitStr(val) -- Transforms Wikitext that uses comma delimination into strings 
	if type(val) == 'string' then
		val = mw.text.split(val, ",")
	end
	return val
end

utils.splitStr = splitStr

-- utility : stack manipulation functions
-- Console tests : 
-- plop = {} ; p.append(plop, "a") ; p.append(plop, "a") ; p.push(plop, "b")  ; p.append(plop, "c") ; p.push(plop, "a") ; mw.log(p. dump_to_console(plop)) ; p.shove_off(plop) ; p.pop(plop) ; mw.log(plop)

local function pop(list)
	local ind=1
	if list[0] then
		ind = 0
	end
	local elem = list[ind]
	table.remove(list, ind)
	return elem, list
end

utils.pop = pop

local function push(list, elem)
	if elem[0] then
		table.insert(list, 0, elem)
	else
		table.insert(list, 1, elem)
	end
end

utils.push = push


utils.append = function(list, elem)
	table.insert(list, #list+1, elem)
end

utils.shove_off = function(list, elem)
	table.remove(list, elem, #list+1)
end
utils.remove_last = utils.shove_off

return utils