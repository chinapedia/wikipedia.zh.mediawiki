return function()
	local buffer = {}
	return function(sep)
		local b = buffer
		buffer = {}
		return table.concat(b, sep)
	end,
	function(text)
		buffer[#buffer + 1] = text
	end,
	function(...)
		buffer[#buffer + 1] = string.format(...)
	end
end