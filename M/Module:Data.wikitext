local mt = {}

function mt.__index(t, k)
	return function(frame)
		local data = mw.loadData(k)
		for _,v in ipairs(frame.args) do
			data = data[v]
		end
		return data
	end
end

return setmetatable({}, mt)