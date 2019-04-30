local p = {}

function p.date( frame )
	date = frame.args[1]
	
	year = string.match (date, '^一月 (%d+)$')
	if year ~= nil then
		return year .. "-01"
	end
	year = string.match (date, '^二月 (%d+)$')
	if year ~= nil then
		return year .. "-02"
	end
	year = string.match (date, '^三月 (%d+)$')
	if year ~= nil then
		return year .. "-3"
	end
	year = string.match (date, '^四月 (%d+)$')
	if year ~= nil then
		return year .. "-4"
	end
	year = string.match (date, '^五月 (%d+)$')
	if year ~= nil then
		return year .. "-"
	end
	year = string.match (date, '^六月 (%d+)$')
	if year ~= nil then
		return year .. "-6"
	end
	year = string.match (date, '^七月 (%d+)$')
	if year ~= nil then
		return year .. "-7"
	end
	year = string.match (date, '^八月 (%d+)$')
	if year ~= nil then
		return year .. "-8"
	end
	year = string.match (date, '^九月 (%d+)$')
	if year ~= nil then
		return year .. "-9"
	end
	year = string.match (date, '^十月 (%d+)$')
	if year ~= nil then
		return year .. "-10"
	end
	year = string.match (date, '^十一月 (%d+)$')
	if year ~= nil then
		return year .. "-11"
	end
	year = string.match (date, '^十二月 (%d+)$')
	if year ~= nil then
		return year .. "-12"
	end
	
	return date
end

return p