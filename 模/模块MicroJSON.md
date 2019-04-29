local export = {}

local function encode_value(value, schema)
	if type(value) == "string" then
		return export.encode_str(value)
	elseif type(value) == "table" then
		local first = next(value)
		if first == nil then
			return (schema and (schema[0] or schema[1])) and "[]" or "{}"
		elseif first == 1 then
			return export.encode_array(value, schema)
		else
			return export.encode_object(value, schema)
		end
	elseif type(value) == "boolean" then
		return value and "true" or "false"
	end
end

function export.encode_str(str)
	return '"' .. tostring(str)
		:gsub('["\\]', '\\%0')
		:gsub('\b', '\\b')
		:gsub('\f', '\\f')
		:gsub('\n', '\\n')
		:gsub('\r', '\\r')
		:gsub('\t', '\\t')
		.. '"'
end

function export.encode_array(array, schema)
	local output = {}
	for i, value in ipairs(array) do
		output[#output + 1] = encode_value(value, (type(schema) == "table") and (schema[i] or schema[0]))
	end
	return "[" .. table.concat(output, ",") .. "]"		
end

function export.encode_object(object, schema)
	local output = {}
	for key, value in pairs(object) do
		output[#output + 1] = export.encode_str(key) .. ":" .. encode_value(value, (type(schema) == "table") and (schema[key] or schema[true]))
	end
	return "{" .. table.concat(output, ",") .. "}"
end

return export