local p = { PrimeTable = {} }
local numlib = require("Module:Number")
local numdata = require("Module:Number/data")
local calclib = require("Module:Complex Number/Calculate")

--debug
--local cmath,tonum=p.cmath.init(),p.cmath.init().toComplexNumber; mw.logObject(cmath.abs(cmath.nonRealPart(tonum("2+3i"))))

p.cmath = {
	abs=function(z)
		local real, imag = z.real or tonumber(z) , z.imag or (tonumber(z) and 0) 
		if math.abs(imag) < 1e-12 then return math.abs(real) end
		return math.sqrt(real * real + imag * imag)
	end,
	floor=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		return p.cmath.getComplexNumber(math.floor(real), math.floor(imag)) 
	end,
	ceil=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		return p.cmath.getComplexNumber(math.ceil(real), math.ceil(imag)) 
	end,
	round=function(op1,op2,op3)
		local number = p.cmath.getComplexNumber(tonumber(op1) or op1.real or 0, (tonumber(op1) and 0) or op1.imag or 0) 
		local digs = p.cmath.getComplexNumber(tonumber(op2) or (op2 or {}).real or 0, (tonumber(op2) and 0) or (op2 or {}).imag or 0) 
		local base = p.cmath.getComplexNumber(tonumber(op3) or (op3 or {}).real or 10, (tonumber(op3) and 0) or (op3 or {}).imag or 0) 
		local round_rad = p.cmath.pow(base,digs)
		local check_number = number * round_rad
		check_number.real = check_number.real + 0.5; check_number.imag = check_number.imag + 0.5; 
		return p.cmath.floor( check_number ) / round_rad
	end,
	div=function(op1,op2)
		local a, c = tonumber(op1) or op1.real, tonumber(op2) or op2.real
		local b, d = (tonumber(op1) and 0) or op1.imag, (tonumber(op2) and 0) or op2.imag
		local op1_d, op2_d = a*a + b*b, c*c + d*d
		if op2_d <= 0 then return op1_d / op2_d end
		return p.cmath.getComplexNumber((a * c + b * d) / op2_d, (b * c - a * d) / op2_d) 
	end,
	re=function(z)return tonumber(z) or z.real end,
	im=function(z) return (tonumber(z) and 0) or z.imag end,
	nonRealPart=function(z) return p.cmath.getComplexNumber(0, (tonumber(z) and 0) or z.imag) end,
	conjugate=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		return p.cmath.getComplexNumber(real, -imag)
	end,
	inverse=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		return p.cmath.getComplexNumber(real, -imag) / ( real*real + imag*imag )
	end,
	tovector=function(z)
		return {tonumber(z) or z.real, (tonumber(z) and 0) or z.imag}
	end,
	--判斷是否為第一象限高斯質數
	is_prime_quadrant1=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		if imag == 0 and real == 0 then return false end
		if not numdata._is_integer(imag) or not numdata._is_integer(real) then return false end
		if imag == 0 then 
			if real <= 1 then return false end
			if numdata._is_integer((real - 3.0) / 4.0) then
				if p.PrimeTable.table_max == nil then p.PrimeTable = require('Module:Factorization') end
				p.PrimeTable.primeIndexOf({(real or 0)+2})
				return p.PrimeTable.lists[real] ~= nil
			end
		end
		--非第一象限高斯質數
		if imag < 0 or real < 0 then return false end
		if imag ~= 0 and real == 0 then return false end
		local value = imag*imag + real*real
		if p.PrimeTable.table_max == nil then p.PrimeTable = require('Module:Factorization') end
		p.PrimeTable.primeIndexOf({value+2})
		return p.PrimeTable.lists[value] ~= nil
	end,
	sqrt=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local argument = 0
		local length = math.sqrt( real * real + imag * imag )
		if imag ~= 0 then
			argument = 2.0 * math.atan(imag / (length + real))
		else
			if real > 0 then argument = 0.0 
			else argument = math.pi end
		end
		local sq_len = math.sqrt(length)
		return p.cmath.getComplexNumber(sq_len * math.cos(argument/2.0), sq_len * math.sin(argument/2.0)):clean()
	end,
	
	sin=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		return p.cmath.getComplexNumber(math.sin(real) * math.cosh(imag), math.cos(real) * math.sinh(imag)) 
	end,
	cos=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		return p.cmath.getComplexNumber(math.cos(real) * math.cosh(imag), -math.sin(real) * math.sinh(imag)) 
	end,
	tan=function(z)
		local theta = p.cmath.getComplexNumber(tonumber(z) or z.real, (tonumber(z) and 0) or z.imag) 
		return p.cmath.sin(theta) / p.cmath.cos(theta)
	end,
	cot=function(z)
		local theta = p.cmath.getComplexNumber(tonumber(z) or z.real, (tonumber(z) and 0) or z.imag) 
		return p.cmath.cos(theta) / p.cmath.sin(theta)
	end,

	asin=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local u, v = p.cmath.getComplexNumber(0, imag), p.cmath.getComplexNumber(real, imag)
		local sgnimag = p.cmath.sgn(u); if math.abs(sgnimag.imag) < 1e-12 then sgnimag.imag = 1 end
		return -sgnimag * p.cmath.asinh( v * sgnimag )
	end,
	acos=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local u, v = p.cmath.getComplexNumber(0, imag), p.cmath.getComplexNumber(real, imag)
		local sgnimag = p.cmath.sgn(u); if math.abs(sgnimag.imag) < 1e-12 then sgnimag.imag = 1 end
		return -sgnimag * p.cmath.acosh( v )
	end,
	atan=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local u, v = p.cmath.getComplexNumber(0, imag), p.cmath.getComplexNumber(real, imag)
		local sgnimag = p.cmath.sgn(u); if math.abs(sgnimag.imag) < 1e-12 then sgnimag.imag = 1 end
		return -sgnimag * p.cmath.atanh( v * sgnimag )
	end,
	acot=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local u, v = p.cmath.getComplexNumber(0, imag), p.cmath.getComplexNumber(real, imag)
		local sgnimag = p.cmath.sgn(u); if math.abs(sgnimag.imag) < 1e-12 then sgnimag.imag = 1 end
		return sgnimag * p.cmath.acoth( v * sgnimag )
	end,
	
	sinh=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local im_sgn if imag > 0 then im_sgn = 1 elseif imag < 0 then im_sgn = -1 else im_sgn = 0 end
		return p.cmath.getComplexNumber( math.cos(math.abs(imag)) * math.sinh(real) , im_sgn * math.sin(math.abs(imag)) * math.cosh(real) )
	end,
	cosh=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local im_sgn if imag > 0 then im_sgn = 1 elseif imag < 0 then im_sgn = -1 else im_sgn = 0 end
		return p.cmath.getComplexNumber( math.cos(math.abs(imag)) * math.cosh(real) , im_sgn * math.sin(math.abs(imag)) * math.sinh(real) )
	end,
	tanh=function(z)
		local theta = p.cmath.getComplexNumber(tonumber(z) or z.real, (tonumber(z) and 0) or z.imag) 
		return p.cmath.sinh(theta) / p.cmath.cosh(theta)
	end,
	coth=function(z)
		local theta = p.cmath.getComplexNumber(tonumber(z) or z.real, (tonumber(z) and 0) or z.imag) 
		return p.cmath.cosh(theta) / p.cmath.sinh(theta)
	end,

	asinh=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local u = p.cmath.getComplexNumber(real, imag)
		return p.cmath.log( u + p.cmath.sqrt( u * u + p.cmath.getComplexNumber(1,0) ) )
	end,
	acosh=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local u = p.cmath.getComplexNumber(real, imag)
		return p.cmath.log( u + p.cmath.sqrt( u * u + p.cmath.getComplexNumber(-1,0) ) )
	end,
	atanh=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local u = p.cmath.getComplexNumber(real, imag)
		return ( p.cmath.log( 1 + u ) - p.cmath.log( 1 - u ) ) / 2
	end,
	acoth=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local u = p.cmath.getComplexNumber(real, imag)
		return ( p.cmath.log( u + 1 ) - p.cmath.log( u - 1 ) ) / 2
	end,

	dot=function (op1, op2) 
		local real1, real2 = tonumber(op1) or op1.real, tonumber(op2) or op2.real
		local imag1, imag2 = (tonumber(op1) and 0) or op1.imag, (tonumber(op2) and 0) or op2.imag
		return p.cmath.getComplexNumber(real1 * real2, imag1 * imag2) 
	end,
	sgn=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		if real == 0 and imag == 0 then return p.cmath.getComplexNumber(0, 0) end
		local length = math.sqrt( real * real + imag * imag )
		return p.cmath.getComplexNumber(real/length, imag/length)
	end,
	arg=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		if imag ~= 0 then
			local length = math.sqrt( real * real + imag * imag )
			return 2.0 * math.atan(imag / (length + real))
		else
			if real >= 0 then return 0.0 
			else return math.pi end
		end
		return tonumber("nan")
	end,
	cis=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local hyp = 1
		if imag ~= 0 then hyp = math.cosh(imag) - math.sinh(imag) end
		return p.cmath.getComplexNumber(math.cos(real) * hyp, math.sin(real) * hyp)
	end,
	exp=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local cis_r, cis_i, exp_r = 1, 0, math.exp(real)
		if imag ~= 0 then cis_r, cis_i = math.cos(imag), math.sin(imag) end
		return p.cmath.getComplexNumber(exp_r * cis_r, exp_r * cis_i)
	end,
	log=function(z)
		local real, imag = tonumber(z) or z.real, (tonumber(z) and 0) or z.imag
		local argument = 0
		local length = math.sqrt( real * real + imag * imag )
		if imag ~= 0 then
			argument = 2.0 * math.atan(imag / (length + real))
		else
			if real > 0 then argument = 0.0 
			else argument = math.pi end
		end
		return p.cmath.getComplexNumber(math.log(length), argument)
	end,
	pow=function(op1,op2)
		--a ^ z
		local a = p.cmath.getComplexNumber( tonumber(op1) or op1.real, (tonumber(op1) and 0) or op1.imag )
		local z = p.cmath.getComplexNumber( tonumber(op2) or op2.real, (tonumber(op2) and 0) or op2.imag )
		return p.cmath.exp(z * p.cmath.log(a)):clean()
	end,
	ComplexNumberMeta = {
		__add = function (op1, op2) 
			local real1, real2 = tonumber(op1) or op1.real, tonumber(op2) or op2.real
			local imag1, imag2 = (tonumber(op1) and 0) or op1.imag, (tonumber(op2) and 0) or op2.imag
			return p.cmath.getComplexNumber(real1 + real2, imag1 + imag2) 
		end,
		__sub = function (op1, op2) 
			local real1, real2 = tonumber(op1) or op1.real, tonumber(op2) or op2.real
			local imag1, imag2 = (tonumber(op1) and 0) or op1.imag, (tonumber(op2) and 0) or op2.imag
			return p.cmath.getComplexNumber(real1 - real2, imag1 - imag2) 
		end,
		__mul = function (op1, op2) 
			local a, c = tonumber(op1) or op1.real, tonumber(op2) or op2.real
			local b, d = (tonumber(op1) and 0) or op1.imag, (tonumber(op2) and 0) or op2.imag
			return p.cmath.getComplexNumber(a * c - b * d, b * c + a * d) 
		end,
		__div = function (op1, op2) 
			local a, c = tonumber(op1) or op1.real, tonumber(op2) or op2.real
			local b, d = (tonumber(op1) and 0) or op1.imag, (tonumber(op2) and 0) or op2.imag
			local op1_d, op2_d = a*a + b*b, c*c + d*d
			if op2_d <= 0 then return op1_d / op2_d end
			return p.cmath.getComplexNumber((a * c + b * d) / op2_d, (b * c - a * d) / op2_d) 
		end,
		__mod = function (op1, op2) 
			local x = p.cmath.getComplexNumber(tonumber(op1) or op1.real, (tonumber(op1) and 0) or op1.imag)
			local y = p.cmath.getComplexNumber(tonumber(op2) or op2.real, (tonumber(op2) and 0) or op2.imag) 
			return x - y * p.cmath.floor(x / y) 
		end,
		__tostring = function (this) 
			local body = ''
			if this.real ~= 0 then body = tostring(this.real) end
			if this.imag ~= 0 then 
				if body ~= '' and this.imag > 0 then body = body .. '+' end
				if this.imag == -1 then  body = body .. '-' end
				if math.abs(this.imag) ~= 1 then body = body .. tostring(this.imag) end
				body = body .. 'i'
			end
			if body == '' then body = '0' end
			return body
		end,
		__unm = function (this)
			return p.cmath.getComplexNumber(-this.real, -this.imag) 
		end,
		__eq = function (op1, op2)
			local diff_real = math.abs( (tonumber(op1) or op1.real) - (tonumber(op2) or op2.real) )
			local diff_imag1 = math.abs( ( (tonumber(op1) and 0) or op1.imag) - ( (tonumber(op2) and 0) or op2.imag) )
			return diff_real < 1e-12 and diff_imag1 < 1e-12
		end,
	},
	getComplexNumber = function(real,imag)
		ComplexNumber = {}
		setmetatable(ComplexNumber,p.cmath.ComplexNumberMeta) 
		function ComplexNumber:update()
			self.argument = 0
			self.length = math.sqrt( self.real * self.real + self.imag * self.imag )
			if self.imag ~= 0 then
				self.argument = 2.0 * math.atan(self.imag / (self.length + self.real))
			else
				if self.real > 0 then self.argument = 0.0 
				else self.argument = math.pi end
			end
		end
		function ComplexNumber:clean()
			if math.abs(self.real) <= 1e-12 then self.real = 0 end
			if math.abs(self.imag) <= 1e-12 then self.imag = 0 end
			if math.abs(self.real - math.floor(self.real)) <= 1e-12 then self.real = math.floor(self.real) end
			if math.abs(self.imag - math.floor(self.imag)) <= 1e-12 then self.imag = math.floor(self.imag) end
			return self
		end
		ComplexNumber.real, ComplexNumber.imag = real, imag
		return ComplexNumber
	end,
	toComplexNumber = function(num_str)
		local real, imag
		if num_str == nil then return nil end
		if ( type(num_str)==type(0) or ( num_str and type(num_str.real)==type(0) ) ) then
			real, imag = tonumber(num_str) or num_str.real, (tonumber(num_str) and 0) or num_str.imag
		else
			real, imag = p.cmath.toComplexNumberPart(num_str)
		end
		if real == nil or imag == nil then return nil end
		return p.cmath.getComplexNumber(real, imag)
	end,
	toComplexNumberPart = function(num_str)
		local body = ''
		local real, imag = 0, 0
		local split_str = mw.text.split(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(
				num_str or '',
			'%s+',''),'%++([%d%.])',',+%1'),'%++([ij])',',+1%1'),'%-+([%d%.])',',-%1'),'%-+([ij])',',-1%1'),'%*+([%d%.])',',*%1'),'%*+([ij])',',*1%1'),'%/+([%d%.])',',/%1'),'%/+([ij])',',/1%1'),',')
		local first = true
		local continue = false
		
		for k,v in pairs(split_str) do
			continue = false
			local val = mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.text.trim(v),'[ij]+','i'),'^(%.)','0%1'),'^([%d%.])','+%1'),'([%+%-])([%d%.])','%1\48%2'),'^([ij])','+1%1')
			if mw.ustring.find(val,"%/") or mw.ustring.find(val,"%*") then return end
			if val == nil or val == '' then if first == true then first = false continue = true else return end end
			if not continue then
				local num_text = mw.ustring.match(val,"[%+%-][%d%.]+i?")
				if num_text ~= val then return end
				local num_part = tonumber(mw.ustring.match(num_text,"[%+%-][%d%.]+"))
				if num_part == nil then return end
				if mw.ustring.find(num_text,"i") then
					imag = imag + num_part
				else
					real = real + num_part
				end
			end
		end
		return real, imag
	end,
	init = function()
		p.cmath.e = p.cmath.getComplexNumber(math.exp(1), 0) 
		p.cmath.pi = p.cmath.getComplexNumber(math.pi, 0) 
		p.cmath.nan = p.cmath.getComplexNumber(tonumber("nan"), tonumber("nan")) 
		p.cmath.zero = p.cmath.getComplexNumber(0, 0) 
		p.cmath.one = p.cmath.getComplexNumber(1, 0) 
		p.cmath[-1] = p.cmath.getComplexNumber(-1, 0) 
		p.cmath.i = p.cmath.getComplexNumber(0, 1) 
		p.cmath[0],p.cmath[1] = p.cmath.zero,p.cmath.one
		return p.cmath
	end
}
p.math={
	init = function()
		local my_math = math my_math.e = math.exp(1) my_math.nan = tonumber("nan")
		my_math.inverse = function(x)return 1.0/(tonumber(x)or 1.0)end
		my_math.sgn=function(x)if x==0 then return 0 elseif x<0 then return -1 elseif x>0 then return 1 else return tonumber("nan")end end
		my_math.arg=function(x)if x >= 0 then return 0.0 else return math.pi end end
		my_math.re=function(z) return tonumber(z) or z.real or 0 end
		my_math.im=function(z) return (tonumber(z) and 0) or z.imag or 0 end
		my_math.nonRealPart=function(z) return (tonumber(z) and 0) or z.imag or 0 end
		my_math.tovector=function(z) return {tonumber(z) or z.real or 0} end

		my_math.div=function(op1,op2) return tonumber(op1) / tonumber(op2) end
		my_math.dot=function(x,y)return x*y end
		
		--sin, cos, tan are already support
		my_math.cot=function(z)local theta = tonumber(z)return math.cos(theta) / math.sin(theta)end
		
		--asin, acos, atan are already support
		my_math.acot=function(x)return p.cmath.acot(x).real end
		
		--sinh, cosh, tanh are already support
		my_math.coth=function(x)return math.cosh(x) / math.sinh(x) end
		
		my_math.asinh=function(x)return math.log( x + math.sqrt( x * x + 1 ) )end
		my_math.acosh=function(x)return math.log( x + math.sqrt( x * x - 1 ) )end
		my_math.atanh=function(x) local result = p.cmath.atanh(x):clean() if math.abs(result.imag) > 1e-12 then return tonumber('nan') else return result.real end end
		my_math.acoth=function(x) local result = p.cmath.acoth(x):clean() if math.abs(result.imag) > 1e-12 then return tonumber('nan') else return result.real end end
		
		return my_math
	end
}
p.bmath={
	nonRealPart=function(bv) return p.bmath.toBoolean(0) end,
	BooleanNumberMeta = {
		__add = function (op1, op2) 
			local a, b = p.bmath.toBoolean(op1) or p.bmath.toBoolean(false), p.bmath.toBoolean(op2) or p.bmath.toBoolean(false)
			b.value = a.value or b.value
			return b 
		end,
		__sub = function (op1, op2) 
			local a, b = p.bmath.toBoolean(op1) or p.bmath.toBoolean(false), p.bmath.toBoolean(op2) or p.bmath.toBoolean(false)
			b.value = a.value and (not b.value)
			return b 
		end,
		__mul = function (op1, op2) 
			local a, b = p.bmath.toBoolean(op1) or p.bmath.toBoolean(false), p.bmath.toBoolean(op2) or p.bmath.toBoolean(false)
			b.value = a.value and b.value
			return b 
		end,
		__tostring = function (this) return this.value_table[this.value] end,
		__unm = function (this)local that = p.bmath.toBoolean(this)that.value = not that.value return that end,
		__eq = function (op1, op2)return p.bmath.toBoolean(op1).value == p.bmath.toBoolean(op2).value end,
	},
	value_table={
		[1]={[true]=1,[false]=0},[0]={[true]=1,[false]=0},
		['1']={[true]=1,[false]=0},['0']={[true]=1,[false]=0},
		['yes']={[true]='yes',[false]='no'},['no']={[true]='yes',[false]='no'},
		['y']={[true]='Y',[false]='N'},['n']={[true]='Y',[false]='N'},
		[true]={[true]=true,[false]=false},[false]={[true]=true,[false]=false},
		['true']={['true']=true,['false']=false},['false']={['true']=true,['false']=false},
		['t']={[true]='T',[false]='F'},['f']={[true]='T',[false]='F'},
		['on']={[true]='on',[false]='off'},['off']={[true]='on',[false]='off'},
		['是']={[true]='是',[false]='否'},['否']={[true]='是',[false]='否'},
		['开']={[true]='开',[false]='关'},['关']={[true]='开',[false]='关'},
		['開']={[true]='開',[false]='關'},['關']={[true]='開',[false]='關'},},
	toBoolean = function(num_str)
		if (type(num_str) == type({})) and num_str.value_table ~= nil and num_str.value ~= nil then 
			BooleanNumber = {value_table=num_str.value_table,value=num_str.value}
		else
			if yesno == nil then yesno = require('Module:Yesno') end
			local input_str = mw.ustring.gsub(mw.text.trim(num_str),"%s",'')
			local data = yesno(num_str) or yesno(input_str)
			if data == nil then return nil end
			BooleanNumber = {}
			BooleanNumber.value_table=p.bmath.value_table[num_str] or p.bmath.value_table[input_str] or {[true]='T',[false]='F'}
			BooleanNumber.value=data
		end
		setmetatable(BooleanNumber,p.bmath.BooleanNumberMeta) 
		return BooleanNumber
	end,
	init = function()
		p.bmath.zero = p.bmath.toBoolean(0) 
		p.bmath.one = p.bmath.toBoolean(1) 
		p.bmath[0],p.bmath[1] = p.bmath.zero,p.bmath.one
		p.bmath.is_bool_lib = true
		return p.bmath
	end
}
p.qmath = {
	abs=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		if imag == 0 and jpart == 0 and kpart == 0 then return math.abs(real) end
		return math.sqrt( real * real + imag * imag + jpart * jpart + kpart * kpart )
	end,
	floor=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		return p.qmath.getQuaternionNumber(math.floor(real), math.floor(imag), math.floor(jpart), math.floor(kpart))
	end,
	ceil=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		return p.qmath.getQuaternionNumber(math.ceil(real), math.ceil(imag), math.ceil(jpart), math.ceil(kpart))
	end,
	div=function(left,z)
		local lreal, limag, ljpart, lkpart = tonumber(left) or left.real, (tonumber(left) and 0) or (left.imag or 0), (tonumber(left) and 0) or (left.jpart or 0), (tonumber(left) and 0) or (left.kpart or 0)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		return p.qmath.getQuaternionNumber(lreal, limag, ljpart, lkpart) * (p.qmath.getQuaternionNumber( real, -imag, -jpart, -kpart ) / ( real*real + imag*imag + jpart*jpart + kpart*kpart ))
	end,
	round=function(op1,op2,op3)
		local number = p.qmath.getQuaternionNumber(tonumber(op1) or op1.real or 0, (tonumber(op1) and 0) or (op1.imag or 0) or 0, (tonumber(op1) and 0) or (op1.jpart or 0) or 0, (tonumber(op1) and 0) or (op1.kpart or 0) or 0) 
		local digs = p.qmath.getQuaternionNumber(tonumber(op2) or (op2 or {}).real or 0, (tonumber(op2) and 0) or ((op2 or {}).imag or 0) or 0, (tonumber(op2) and 0) or ((op2 or {}).jpart or 0) or 0, (tonumber(op2) and 0) or ((op2 or {}).kpart or 0) or 0 ) 
		local base = p.qmath.getQuaternionNumber(tonumber(op3) or (op3 or {}).real or 10, (tonumber(op3) and 0) or ((op3 or {}).imag or 0) or 0, (tonumber(op3) and 0) or ((op3 or {}).jpart or 0) or 0, (tonumber(op3) and 0) or ((op3 or {}).kpart or 0) or 0 ) 
		local round_rad = p.qmath.pow(base,digs)
		local check_number = number * round_rad
		check_number.real = check_number.real + 0.5; check_number.imag = check_number.imag + 0.5; 
		check_number.jpart = check_number.jpart + 0.5; check_number.kpart = check_number.kpart + 0.5; 
		return p.qmath.floor( check_number ) * p.qmath.inverse(round_rad)
	end,
	re=function(z)return tonumber(z) or z.real end,
	im=function(z) return (tonumber(z) and 0) or z.imag end,
	conjugate=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		return p.qmath.getQuaternionNumber( real, -imag, -jpart, -kpart )
	end,
	inverse=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		return p.qmath.getQuaternionNumber( real, -imag, -jpart, -kpart ) / ( real*real + imag*imag + jpart*jpart + kpart*kpart )
	end,
	tovector=function(z)
		return {tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)}
	end,
	sqrt=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		if jpart == 0 and kpart == 0 then 
			local complex = p.cmath.sqrt(p.cmath.getComplexNumber(real, imag))
			return p.qmath.getQuaternionNumber(complex.real, complex.imag, 0, 0)
		end
		return p.qmath.pow(z, 0.5)
	end,
	
	sin=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u = p.qmath.getQuaternionNumber(0, imag, jpart, kpart)
		return ( math.cosh(p.qmath.abs(u)) * math.sin(real) ) + ( p.qmath.sgn(u) * math.sinh(p.qmath.abs(u)) * math.cos(real) )
	end,
	cos=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u = p.qmath.getQuaternionNumber(0, imag, jpart, kpart)
		return ( math.cosh(p.qmath.abs(u)) * math.cos(real) ) - ( p.qmath.sgn(u) * math.sinh(p.qmath.abs(u)) * math.sin(real) )
	end,
	tan=function(z)
		local theta = p.qmath.getQuaternionNumber(tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)) 
		return p.qmath.sin(theta) * p.qmath.inverse( p.qmath.cos(theta) )
	end,
	cot=function(z)
		local theta = p.qmath.getQuaternionNumber(tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)) 
		return p.qmath.cos(theta) * p.qmath.inverse( p.qmath.sin(theta) )
	end,

	asin=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u, v = p.qmath.getQuaternionNumber(0, imag, jpart, kpart), p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
		local sgnu = p.qmath.sgn(u); 
		if math.abs(sgnu.imag) < 1e-12 and math.abs(sgnu.jpart) < 1e-12 and math.abs(sgnu.kpart) < 1e-12 then sgnu.imag = 1 end
		return -sgnu * p.qmath.asinh( v * sgnu )
	end,
	acos=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u, v = p.qmath.getQuaternionNumber(0, imag, jpart, kpart), p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
		local sgnu = p.qmath.sgn(u); 
		if math.abs(sgnu.imag) < 1e-12 and math.abs(sgnu.jpart) < 1e-12 and math.abs(sgnu.kpart) < 1e-12 then sgnu.imag = 1 end
		return -sgnu * p.qmath.acosh( v )
	end,
	atan=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u, v = p.qmath.getQuaternionNumber(0, imag, jpart, kpart), p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
		local sgnu = p.qmath.sgn(u); 
		if math.abs(sgnu.imag) < 1e-12 and math.abs(sgnu.jpart) < 1e-12 and math.abs(sgnu.kpart) < 1e-12 then sgnu.imag = 1 end
		return -sgnu * p.qmath.atanh( v * sgnu )
	end,
	acot=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u, v = p.qmath.getQuaternionNumber(0, imag, jpart, kpart), p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
		local sgnu = p.qmath.sgn(u); 
		if math.abs(sgnu.imag) < 1e-12 and math.abs(sgnu.jpart) < 1e-12 and math.abs(sgnu.kpart) < 1e-12 then sgnu.imag = 1 end
		return sgnu * p.qmath.acoth( v * sgnu )
	end,

	sinh=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u = p.qmath.getQuaternionNumber(0, imag, jpart, kpart)
		return ( math.cos(p.qmath.abs(u)) * math.sinh(real) ) + ( p.qmath.sgn(u) * math.sin(p.qmath.abs(u)) * math.cosh(real) )
	end,
	cosh=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u, v = p.qmath.getQuaternionNumber(0, imag, jpart, kpart), p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
		return ( math.cos(p.qmath.abs(u)) * math.cosh(real) ) + ( p.qmath.sgn(u) * math.sin(p.qmath.abs(u)) * math.sinh(real) )
	end,
	tanh=function(z)
		local theta = p.qmath.getQuaternionNumber(tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)) 
		return p.qmath.sinh(theta) * p.qmath.inverse( p.qmath.cosh(theta) )
	end,
	coth=function(z)
		local theta = p.qmath.getQuaternionNumber(tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)) 
		return p.qmath.cosh(theta) * p.qmath.inverse( p.qmath.sinh(theta) )
	end,

	asinh=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u = p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
		return p.qmath.log( u + p.qmath.sqrt( u * u + p.qmath.getQuaternionNumber(1,0,0,0) ) )
	end,
	acosh=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u = p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
		return p.qmath.log( u + p.qmath.sqrt( u * u + p.qmath.getQuaternionNumber(-1,0,0,0) ) )
	end,
	atanh=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u = p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
		return ( p.qmath.log( 1 + u ) - p.qmath.log( 1 - u ) ) / 2
	end,
	acoth=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u = p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
		return ( p.qmath.log( u + 1 ) - p.qmath.log( u - 1 ) ) / 2
	end,

	dot = function (op1, op2) 
		local a, t = tonumber(op1) or op1.real, tonumber(op2) or op2.real
		local b, x = (tonumber(op1) and 0) or op1.imag, (tonumber(op2) and 0) or op2.imag
		local c, y = (tonumber(op1) and 0) or (op1.jpart or 0), (tonumber(op2) and 0) or (op2.jpart or 0)
		local d, z = (tonumber(op1) and 0) or (op1.kpart or 0), (tonumber(op2) and 0) or (op2.kpart or 0)
		return a * t + b * x + c * y + d * z
	end,
	scalarPartQuaternion=function(z)
		return p.qmath.getQuaternionNumber(tonumber(z) or z.real, 0, 0, 0)
	end,
	nonRealPart=function(z) return p.qmath.getQuaternionNumber(0, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)) end,
	vectorPartQuaternion=function(z)
		return p.qmath.getQuaternionNumber(0, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0))
	end,
	sgn=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local length = math.sqrt( real * real + imag * imag + jpart * jpart + kpart * kpart )
		if length <= 0 then return p.qmath.getQuaternionNumber(0,0,0,0) end
		return z / length
	end,
	arg=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local length = math.sqrt( real * real + imag * imag + jpart * jpart + kpart * kpart )
		return math.acos( real / length )
	end,
	cis=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u = p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
		return p.qmath.cos(u) + p.qmath.getQuaternionNumber(0,1,0,0) * p.qmath.sin(u)
	end,
	exp=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u = p.qmath.getQuaternionNumber(0, imag, jpart, kpart)
		return ( (p.qmath.sgn(u) * math.sin(p.qmath.abs(u))) + math.cos(p.qmath.abs(u))) * math.exp(real)
	end,
	log=function(z)
		local real, imag, jpart, kpart = tonumber(z) or z.real, (tonumber(z) and 0) or (z.imag or 0), (tonumber(z) and 0) or (z.jpart or 0), (tonumber(z) and 0) or (z.kpart or 0)
		local u, v = p.qmath.getQuaternionNumber(0, imag, jpart, kpart), p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
		return (p.qmath.sgn(u) * p.qmath.arg(v)) + math.log(p.qmath.abs(v))
	end,
	pow=function(op1,op2)
		--a ^ z
		local a = p.qmath.getQuaternionNumber( tonumber(op1) or op1.real, (tonumber(op1) and 0) or (op1.imag or 0), (tonumber(op1) and 0) or (op1.jpart or 0), (tonumber(op1) and 0) or (op1.kpart or 0) )
		local z = p.qmath.getQuaternionNumber( tonumber(op2) or op2.real, (tonumber(op2) and 0) or (op2.imag or 0), (tonumber(op2) and 0) or (op2.jpart or 0), (tonumber(op2) and 0) or (op2.kpart or 0) )
		a:clean();z:clean();
		if a.jpart == 0 and z.jpart == 0 and a.kpart == 0 and z.kpart == 0 then 
			local complex = p.cmath.pow(p.cmath.getComplexNumber(a.real, a.imag), p.cmath.getComplexNumber(z.real, z.imag))
			return p.qmath.getQuaternionNumber(complex.real, complex.imag, 0, 0)
		end
		return p.qmath.exp(z * p.qmath.log(a)):clean()
	end,
	QuaternionNumberMeta = {
		__add = function (op1, op2) 
			local a, t = tonumber(op1) or op1.real, tonumber(op2) or op2.real
			local b, x = (tonumber(op1) and 0) or op1.imag, (tonumber(op2) and 0) or op2.imag
			local c, y = (tonumber(op1) and 0) or (op1.jpart or 0), (tonumber(op2) and 0) or (op2.jpart or 0)
			local d, z = (tonumber(op1) and 0) or (op1.kpart or 0), (tonumber(op2) and 0) or (op2.kpart or 0)
			return p.qmath.getQuaternionNumber(a + t, b + x, c + y, d + z) 
		end,
		__sub = function (op1, op2) 
			local a, t = tonumber(op1) or op1.real, tonumber(op2) or op2.real
			local b, x = (tonumber(op1) and 0) or op1.imag, (tonumber(op2) and 0) or op2.imag
			local c, y = (tonumber(op1) and 0) or (op1.jpart or 0), (tonumber(op2) and 0) or (op2.jpart or 0)
			local d, z = (tonumber(op1) and 0) or (op1.kpart or 0), (tonumber(op2) and 0) or (op2.kpart or 0)
			return p.qmath.getQuaternionNumber(a - t, b - x, c - y, d - z) 
		end,
		__mul = function (op1, op2) 
			local a1, a2 = tonumber(op1) or op1.real, tonumber(op2) or op2.real
			local b1, b2 = (tonumber(op1) and 0) or op1.imag, (tonumber(op2) and 0) or op2.imag
			local c1, c2 = (tonumber(op1) and 0) or (op1.jpart or 0), (tonumber(op2) and 0) or (op2.jpart or 0)
			local d1, d2 = (tonumber(op1) and 0) or (op1.kpart or 0), (tonumber(op2) and 0) or (op2.kpart or 0)
			return p.qmath.getQuaternionNumber(
				a1 * a2 - b1 * b2 - c1 * c2 - d1 * d2, 
				a1 * b2 + b1 * a2 + c1 * d2 - d1 * c2,
				a1 * c2 - b1 * d2 + c1 * a2 + d1 * b2, 
				a1 * d2 + b1 * c2 - c1 * b2 + d1 * a2
			) 
		end,
		__div = function (op1, op2) 
			local r1, r2 = tonumber(op1) or op1.real, tonumber(op2) or op2.real
			local i1, i2 = (tonumber(op1) and 0) or op1.imag, (tonumber(op2) and 0) or op2.imag
			local j1, j2 = (tonumber(op1) and 0) or (op1.jpart or 0), (tonumber(op2) and 0) or (op2.jpart or 0)
			local k1, k2 = (tonumber(op1) and 0) or (op1.kpart or 0), (tonumber(op2) and 0) or (op2.kpart or 0)
			if i2 ~= 0 or j2 ~= 0 or k2 ~= 0 then error( "Quaternion can not divide by non scalar value" ) end
			local op1_d, op2_d = r1*r1 + i1*i1 + j1*j1 + k1*k1, r2*r2 + i2*i2 + j2*j2 + k2*k2
			if op2_d <= 0 then return op1_d / op2_d end
			return p.qmath.getQuaternionNumber(r1/r2, i1/r2, j1/r2, k1/r2) 
		end,
		__mod = function (op1, op2) 
			local x = p.qmath.getQuaternionNumber(tonumber(op1) or op1.real, (tonumber(op1) and 0) or op1.imag, (tonumber(op1) and 0) or (op1.jpart or 0), (tonumber(op1) and 0) or (op1.kpart or 0) )
			local y = p.qmath.getQuaternionNumber(tonumber(op2) or op2.real, (tonumber(op2) and 0) or op2.imag, (tonumber(op2) and 0) or (op2.jpart or 0), (tonumber(op2) and 0) or (op2.kpart or 0) ) 
			return x - y * p.qmath.floor(x / y) 
		end,
		__tostring = function (this) 
			local body = ''
			if this.real ~= 0 then body = tostring(this.real) end
			if this.imag ~= 0 then 
				if body ~= '' and this.imag > 0 then body = body .. '+' end
				if this.imag == -1 then  body = body .. '-' end
				if math.abs(this.imag) ~= 1 then body = body .. tostring(this.imag) end
				body = body .. 'i'
			end
			if this.jpart ~= 0 then 
				if body ~= '' and this.jpart > 0 then body = body .. '+' end
				if this.jpart == -1 then  body = body .. '-' end
				if math.abs(this.jpart) ~= 1 then body = body .. tostring(this.jpart) end
				body = body .. 'j'
			end
			if this.kpart ~= 0 then 
				if body ~= '' and this.kpart > 0 then body = body .. '+' end
				if this.kpart == -1 then  body = body .. '-' end
				if math.abs(this.kpart) ~= 1 then body = body .. tostring(this.kpart) end
				body = body .. 'k'
			end
			if body == '' then body = '0' end
			return body
		end,
		__unm = function (this)
			return p.qmath.getQuaternionNumber(-this.real, -this.imag, -this.jpart, -this.kpart) 
		end,
		__eq = function (op1, op2)
			local diff_real = math.abs( (tonumber(op1) or op1.real) - (tonumber(op2) or op2.real) )
			local diff_imag1 = math.abs( ( (tonumber(op1) and 0) or op1.imag) - ( (tonumber(op2) and 0) or op2.imag) )
			local diff_jpart = math.abs( ( (tonumber(op1) and 0) or (op1.jpart or 0)) - ( (tonumber(op2) and 0) or (op2.jpart or 0)) )
			local diff_kpart = math.abs( ( (tonumber(op1) and 0) or (op1.kpart or 0)) - ( (tonumber(op2) and 0) or (op2.kpart or 0)) )
			return diff_real < 1e-12 and diff_imag1 < 1e-12 and diff_jpart < 1e-12 and diff_kpart < 1e-12
		end,
	},
	getQuaternionNumber = function(real, imag, jpart, kpart)
		QuaternionNumber = {}
		setmetatable(QuaternionNumber,p.qmath.QuaternionNumberMeta) 
		function QuaternionNumber:update()
			self.argument = 0
			self.length = math.sqrt( self.real * self.real + self.imag * self.imag
				+ self.jpart * self.jpart + self.kpart * self.kpart )
		end
		function QuaternionNumber:clean()
			if math.abs(self.real) <= 1e-12 then self.real = 0 end
			if math.abs(self.imag) <= 1e-12 then self.imag = 0 end
			if math.abs(self.jpart) <= 1e-12 then self.jpart = 0 end
			if math.abs(self.kpart) <= 1e-12 then self.kpart = 0 end
			if math.abs(self.real - math.floor(self.real)) <= 1e-12 then self.real = math.floor(self.real) end
			if math.abs(self.imag - math.floor(self.imag)) <= 1e-12 then self.imag = math.floor(self.imag) end
			if math.abs(self.jpart - math.floor(self.jpart)) <= 1e-12 then self.jpart = math.floor(self.jpart) end
			if math.abs(self.kpart - math.floor(self.kpart)) <= 1e-12 then self.kpart = math.floor(self.kpart) end
			return self
		end
		QuaternionNumber.real, QuaternionNumber.imag, QuaternionNumber.jpart, QuaternionNumber.kpart = real, imag, jpart, kpart
		return QuaternionNumber
	end,
	toQuaternionNumber = function(num_str)
		local real, imag, jpart, kpart
		if num_str == nil then return nil end
		if ( type(num_str)==type(0) or ( num_str and type(num_str.real)==type(0) ) ) then
			real, imag, jpart, kpart = tonumber(num_str) or num_str.real, (tonumber(num_str) and 0) or (num_str.imag or 0), (tonumber(num_str) and 0) or (num_str.jpart or 0), (tonumber(num_str) and 0) or (num_str.kpart or 0)
		else
			real, imag, jpart, kpart = p.qmath.toQuaternionNumberPart(tostring(num_str))
		end
		if real == nil or imag == nil or jpart == nil or kpart == nil then return nil end
		return p.qmath.getQuaternionNumber(real, imag, jpart, kpart)
	end,
	toQuaternionNumberPart = function(num_str)
		local body = ''
		local real, imag, jpart, kpart = 0, 0, 0, 0
		local split_str = mw.text.split(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(
				num_str or '',
			'%s+',''),'%++([%d%.])',',+%1'),'%++([ijk])',',+1%1'),'%-+([%d%.])',',-%1'),'%-+([ijk])',',-1%1'),'%*+([%d%.])',',*%1'),'%*+([ijk])',',*1%1'),'%/+([%d%.])',',/%1'),'%/+([ijk])',',/1%1'),',')
		local first = true
		local continue = false
		
		for k,v in pairs(split_str) do
			continue = false
			local val = mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.ustring.gsub(mw.text.trim(v),'^(%.)','0%1'),'^([%d%.])','+%1'),'([%+%-])([%d%.])','%1\48%2'),'^([ijk])','+1%1')
			if mw.ustring.find(val,"%/") or mw.ustring.find(val,"%*") then return end

			if val == nil or val == '' then if first == true then first = false continue = true else return end end
			if not continue then
				local num_text = mw.ustring.match(val,"[%+%-][%d%.]+[ijk]?")
				if num_text ~= val then return end
				local num_part = tonumber(mw.ustring.match(num_text,"[%+%-][%d%.]+"))
				if num_part == nil then return end
				if mw.ustring.find(num_text,"i") then
					imag = imag + num_part
				elseif mw.ustring.find(num_text,"j") then
					jpart = jpart + num_part
				elseif mw.ustring.find(num_text,"k") then
					kpart = kpart + num_part
				else
					real = real + num_part
				end
			end
		end
		return real, imag, jpart, kpart
	end,
	init = function()
		p.qmath.pi = p.qmath.getQuaternionNumber(math.pi, 0, 0, 0) 
		p.qmath.e = p.qmath.getQuaternionNumber(math.exp(1), 0, 0, 0)
		p.qmath.nan = p.qmath.getQuaternionNumber(tonumber("nan"), tonumber("nan"), tonumber("nan"), tonumber("nan")) 
		p.qmath.zero = p.qmath.getQuaternionNumber(0, 0, 0, 0) 
		p.qmath.one = p.qmath.getQuaternionNumber(1, 0, 0, 0) 
		p.qmath[-1] = p.qmath.getQuaternionNumber(-1, 0, 0, 0) 
		p.qmath.i = p.qmath.getQuaternionNumber(0, 1, 0, 0) 
		p.qmath.j = p.qmath.getQuaternionNumber(0, 0, 1, 0)
		p.qmath.k = p.qmath.getQuaternionNumber(0, 0, 0, 1) 
		p.qmath[0],p.qmath[1] = p.qmath.zero,p.qmath.one
		return p.qmath
	end
}

return p