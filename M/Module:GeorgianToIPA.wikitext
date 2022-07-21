local export = {}

local IPA_mapping = {
	["ა"] = "ɑ", ["ბ"] = "b", ["გ"] = "ɡ", ["დ"] = "d",
	["ე"] = "ɛ", ["ვ"] = "v", ["ზ"] = "z", ["თ"] = "tʰ",
	["ი"] = "ɪ", ["კ"] = "kʼ", ["ლ"] = "l", ["მ"] = "m",
	["ნ"] = "n", ["ო"] = "ɔ", ["პ"] = "pʼ", ["ჟ"] = "ʒ",
	["რ"] = "r", ["ს"] = "s", ["ტ"] = "tʼ", ["უ"] = "u",
	["ფ"] = "pʰ", ["ქ"] = "kʰ", ["ღ"] = "ʁ", ["ყ"] = "qʼ",
	["შ"] = "ʃ", ["ჩ"] = "tʃ", ["ც"] = "ts", ["ძ"] = "dz",
	["წ"] = "tsʼ", ["ჭ"] = "tʃʼ", ["ხ"] = "χ", ["ჯ"] = "dʒ",
	["ჰ"] = "h"
}

function export.convert(text)
	if type(text) == "table" then
		text = text.args[1]
	end
	return (mw.ustring.gsub(text, '.', IPA_mapping))
end

return export