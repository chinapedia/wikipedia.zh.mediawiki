-- module timing individual functions
-- @license (CC-BY-SA-3.0)
-- @copyright John Erling Blad <jeblad@gmail.com>

-- @var The table holding this modules exported members
local p = {
	['_count'] = 100,
	['_sets'] = 10,
}

-- access function for the number of items in each sets
-- @param number new count of items in each set
-- @return number of items in each set
function p.count( num )
	if num then
		assert(num>0, "Value of 'num' can\'t be zero")
		p._count = num
	end
	return p._count
end

-- access function for the number of sets
-- @param number new count of sets
-- @return number of sets
function p.sets( num )
	if num then
		assert(num>0, "Value of 'sets' can\'t be zero")
		p._sets = num
	end
	return p._sets
end

-- calculate the statistics for time series, and report mean and variance
-- for some background on this calculation, see [[w:en:average|w:en:average]] and [[w:en:Standard_deviation|w:en:Standard deviation]]
-- @param table timing is a sequence of time differences
-- @return table of mean and variance
function p.stats( timing )
	local minVal = timing[1]
	local maxVal = timing[1]
	local sqr,mean=0,0
	for i,v in ipairs(timing) do
		minVal = v < minVal and v or minVal
		maxVal = v > maxVal and v or maxVal
		mean = v + mean
		sqr = math.pow(v,2) + sqr
	end
	mean = mean / #timing
	local var = (sqr / #timing) - math.pow(mean,2)
	return { mean, var, minVal, maxVal }
end

-- runner that iterates a provided function while taking the time for each chunk of iterations
-- @param function func that is the kernel of the iterations
-- @return table of runtime for the given function
function p.runner(func, ...)
	-- measure the function
	local time = {}
	for i=1,p._sets do
		time[i] = os.clock()
		for j=1,p._count do
			func(...)
		end
		time[i] = os.clock() - time[i]
	end
	
	assert(#time>0, "No entries for time measurements")
	
	return time
end

-- combine the measurements into a new form
-- for some background on this calculation, see [[w:en:Sum_of_normally_distributed_random_variables|w:en:Sum of normally distributed random variables]]
-- @param table tick stats for the baseline
-- @param table tack stats for the observed function
-- @return table with the combined stats, shifted from variance to standard deviation
function p.combine(tick, tack)
	-- adjust the actual measurement for the baseline
	return { tack[1] - tick[1], math.pow(tack[2] + tick[2], 0.5), tick[3], tick[4] }
end

-- formatter for the result produced by the runner
-- @param table timing as a mean and a standard deviation
-- @return string describing the result
function p.report( timing )
	local messages = {}
	messages['call-result'] = 'Each call was running for about $1 seconds.\n'
	messages['mean-result'] = '\tMean runtime for each set was $1 seconds,\n\twith standard deviation of $2 seconds,\n\tminimum $3, maximum $4.\n'
	messages['overall-result'] = '\tTotal time spent was about $1 seconds.\n'
	messages['load-result'] = 'Relative load is estimated to $1.\n'
	
	local function g( key, ...)
		local msg = mw.message.new( 'timing-' .. key )
		if msg:isBlank() then
			msg = mw.message.newRawMessage( messages[key] )
		end
		return msg
	end
	
	local function f(formatstring, nums)
		local formatted = {}
		for _,v in ipairs(nums) do
			formatted[1+#formatted] = string.format( formatstring, v )
		end
		return formatted
	end
	
	local strings = {
		g('call-result'):numParams(unpack(f('%.1e', timing[1]))):plain(),
		g('mean-result'):numParams(unpack(f('%.1e', timing[2]))):plain(),
		g('overall-result'):numParams(unpack(f('%.1e', timing[3]))):plain(),
		g('load-result'):numParams(unpack(f('%.1f', timing[4]))):plain()
	}
	return table.concat(strings, '')
end

-- a dummy function that is used for a baseline measure
-- @return nil
function p.nop()
	return nil
end

-- metatable for the export
local mt = {
	-- call-form of the table, with arguments as if it were runner()
	-- @paramfunction func that is the kernel of the iterations
	-- @return string describing the result
	__call = function (self, func, ...)
		-- resolve to the same level
		local f1 = p.nop
		local f2 = func
		
		-- start the clock
		local tick = os.clock()
	
		local baseline = self.stats( self.runner(f1, ...) )
		local actual = self.stats( self.runner(f2, ...) )
		
		local combined = self.combine(baseline, actual)
		local tack = os.clock()
		return self.report({{ combined[1] / p._count }, combined, { tack - tick }, {actual[1]/baseline[1]}})
	end
}

-- install the metatable
setmetatable(p, mt)

-- done
return p