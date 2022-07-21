-- Convert standard numbers to greek numerals, and vice versa
-- Gts-tg@el wiki, Aug. 2017

local p = {}

local greek_numerals = {
	["α"]  = 1,    -- ἄλφα / alpha
	["β"]  = 2,    -- βῆτα / beta 
	["γ"]  = 3,    -- γάμμα / gamma
	["δ"]  = 4,    -- δέλτα / delta
	["ε"]  = 5,    -- ἔψιλον / epsilon
	["Ϛ"]  = 6,    -- δίγαμμα / digamma
	["ζ"]  = 7,    -- ζῆτα / zeta
	["η"]  = 8,    -- ῆτα / heta
	["θ"]  = 9,    -- θῆτα / theta
	["ι"]  = 10,   -- ιῶτα / iota
	["κ"]  = 20,   -- κάππα / kappa
	["λ"]  = 30,   -- λάμδα / lamda
	["μ"]  = 40,   -- μῦ / mu
	["ν"]  = 50,   -- νῦ / nu
	["ξ"]  = 60,   -- ξί / xi
	["ο"]  = 70,   -- ὄμικρον / omikron
	["π"]  = 80,   -- πί / pi
	["ϟ"]  = 90,   -- κόππα / koppa
	["ρ"]  = 100,  -- ρό / rho
	["σ"]  = 200,  -- σίγμα / sigma
	["ς"]  = 200,  -- σίγμα / sigma	(final variation)
	["τ"]  = 300,  -- ταῦ / ταυ
	["υ"]  = 400,  -- ύψιλον / ypsilon
	["φ"]  = 500,  -- φί / phi
	["χ"]  = 600,  -- χί / chi
	["ψ"]  = 700,  -- ψί / psi
	["ω"]  = 800,  -- ὠμέγα / omega
	["ϡ"]  = 900,  -- σαμπί / sampi
}

-- used for math graph template
local numeral_latin_transliteration = {
	["α"]  = 'alpha',
	["β"]  = 'beta',
	["γ"]  = 'gamma',
	["δ"]  = 'delta',
	["ε"]  = 'epsilon',
	["Ϛ"]  = 'digamma',
	["ζ"]  = 'zeta',
	["η"]  = 'eta',
	["θ"]  = 'theta',
	["ι"]  = 'iota',
	["κ"]  = 'kappa',
	["λ"]  = 'lambda',
	["μ"]  = 'mu',
	["ν"]  = 'nu',
	["ξ"]  = 'xi',
	["ο"]  = 'omicron',
	["π"]  = 'pi',
	["ϟ"]  = 'koppa',
	["ρ"]  = 'rho',
	["σ"]  = 'sigma',
	["ς"]  = 'sigma', --(final variation)
	["τ"]  = 'tau',
	["υ"]  = 'upsilon',
	["φ"]  = 'phi',
	["χ"]  = 'chi',
	["ψ"]  = 'psi',
	["ω"]  = 'omega',
	["ϡ"]  = 'sampi',
}

-- return number corresponding to letter
-- params: letter (string)
-- return: number
local function value(letter)
	if letter ~= 'Ϛ' and letter ~= 'ϟ' and letter ~= 'ϡ' then
		letter = mw.ustring.lower(letter) 
    end
	
    return greek_numerals[letter]
end

-- letter value * 1000
-- params: letter (string), total (number)
-- return: number
local function thousandth(letter, total)
	
	if letter ~= false then
		total = total - value(letter) -- remove previous addition as simple number
    	total = total + ( value(letter) * 1000 )
    end
    
    return total
end

-- reverse table (index to values, values to index)
-- params: tbl (table)
-- return: table
local function reverse_table(tbl)
   
	local reversedTable = {}

	for letter, value in pairs(tbl) do
        reversedTable[value] = letter
    end
    
	return reversedTable
	    
end

-- special notation for numbers > 9999
local function mu_notation(greek_number, digits)
  local result  = ''
  local postfix = ''
  
  -- digits greater than 9999
  for index, digit in pairs(digits) do
  	-- mw.log(digit)
     result = result .. '\\' .. numeral_latin_transliteration[digit]
     
     greek_number = greek_number:gsub(digit, "", 1)
  end
  
  if greek_number ~= '' then -- if not all digits are multiples of myriad
     postfix = 	"͵" .. greek_number .. "´"
  end
  
  result = '<math>\\stackrel{' .. result .. '}{\\Mu}</math>' .. postfix
  
  return result	
end

-- convert standard number to greek
-- params: frame (obj)
-- return: string
function p.to_greek(frame)
	local number = frame.args[1]
	local tbl = null
	local result = ''
	local big_values = {}
	local m_notation = false
	
	if tonumber(number) > 9999  then 
 	   m_notation = true
    end
	
	tbl = reverse_table(greek_numerals) -- reverse to [<number>] = '<letter>'
	
 	if tbl[number] ~= null then 
 		result = tbl[number] -- direct hit 
 	else
 		local str_number = tostring(number)
 		local highest_numeric_position = #str_number
 		local i = 0
 		local index = ''
 		
 		for digit in str_number:gmatch"." do -- break up number digits
 			highest_numeric_position = highest_numeric_position - 1
 			
 			if tonumber(digit) > 0 then
 			    index = tonumber(digit .. mw.ustring.rep('0', highest_numeric_position))
 			    
	 			if highest_numeric_position >= 3 then
	 			   
	 			   match = false
	 			   while match == false do
	 			   
	 			      if index < 1 then index = index * 10 end
	 			      	
	 			      if tbl[index] == nil then
	 			      	 index = index / 10000
	 			      else
	 			      	result = result .. tostring(tbl[tonumber(index)])
	 			      	match = true
	 			      end
	 			   end
	 			   
	 		 	   if highest_numeric_position > 3 then table.insert(big_values, tbl[tonumber(index)]) end
	 		 	   
	 		 	else
	 		 	   result = result .. tostring(tbl[tonumber(index)])
	 		 	end
	 		end
 		end
 		--local d = require "Module:Debugging"
 		--mw.log(result)
 		--mw.log(d.dump(big_values))
 	end
	
 	if m_notation == true then --special notation
 		
 		result = mu_notation(result, big_values)
 		local frame = mw.getCurrentFrame()
 		result = frame:preprocess(result)
 	else
 		if tonumber(number) >= 1000 then result = ',' .. result end
 		result = mw.ustring.upper(result) .. "´"
 	end
 	
 	return result
	
end

-- convert greek number to standard
-- greek number sample for testing: αωκα´ = 1821
-- params: frame (obj)
-- return: number
function p.to_standard(frame)
	local greek_number = frame.args[1]
	local total = 0
	local thousand_flag = false
	local prev_letter = false
	
	greek_number = greek_number:gsub("´", "")
	
	if type(greek_number) ~= 'string' then 
		return 'Error: value ' .. greek_number .. ' is ' .. type(greek_number) .. ' instead of expected string'  
	end
	
	-- iterate through letters
	for letter in mw.ustring.gmatch(greek_number, ".") do
	  
		    -- check if thousand marker exists
		    if letter == "," then 
		    	thousand_flag = true
            else
        	    if thousand_flag == true then
                    total = thousandth(letter, total)   	
        	    	thousand_flag = false
        	    end 
        	    
        	    total = total + value(letter)
        	    prev_letter = letter
        	end
    end
    
    if thousand_flag == true then
       total = thousandth(prev_letter, total)	
    end
	
	return total
end	

return p