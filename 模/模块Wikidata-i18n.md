-- vim: set noexpandtab ft=lua ts=4 sw=4:
require('Module:No globals')

local r = {}

-- internationalisation
r.i18n = 
{
    ["errors"] =
    {
        ["property-not-found"] = "未找到属性。",
        ["entity-not-found"] = "未找到Wikidata实体。",
        ["unknown-claim-type"] = "未知声称类型。",
        ["unknown-entity-type"] = "未知实体类型。",
        ["qualifier-not-found"] = "未找到修饰词。",
        ["site-not-found"] = "未找到维基媒体项目。",
		["unknown-datetime-format"] = "未知日期时间格式。",
		["local-article-not-found"] = "此维基尚无此条目"
    },
    ["datetime"] =
	{
		-- $1 is a placeholder for the actual number
		[0] = "$10亿年",	-- precision: billion years
		[1] = "$1亿年",	-- precision: hundred million years
		[2] = "$1000万年",	-- precision: ten million years
		[3] = "$100万年",	-- precision: million years
		[4] = "$10万年",		-- precision: hundred thousand years
		[5] = "$1万年",		-- precision: ten thousand years
		[6] = "$1千年",	 	-- precision: millennium
		[7] = "$1世纪",			-- precision: century
		[8] = "$1年代",				-- precision: decade
		-- the following use the format of #time parser function
		[9]  = "Y年",					-- precision: year, 
		[10] = "Y年n月",				-- precision: month
		[11] = "Y年n月j日",			-- precision: day
		[12] = "Y年n月j日G时",			-- precision: hour
		[13] = "Y年n月j日G:i",		-- precision: minute
		[14] = "Y年n月j日G:i:s",		-- precision: second
		["beforenow"] = "公元前$1",	-- how to format negative numbers for precisions 0 to 5
		["afternow"] = "公元$1",		-- how to format positive numbers for precisions 0 to 5
		["bc"] = '公元前$1',		-- how print negative years
		["ad"] = "$1",				-- how print positive years
		-- the following are for function getDateValue() and getQualifierDateValue()
		["default-format"] = "ymd", -- default value of the #3 (getDateValue) or
								    -- #4 (getQualifierDateValue) argument
		["default-addon"] = "公元前",   -- default value of the #4 (getDateValue) or
									-- #5 (getQualifierDateValue) argument
		["prefix-addon"] = true,   -- set to true for languages put "BC" in front of the
									-- datetime string; or the addon will be suffixed
		["addon-sep"] = "",		-- separator between datetime string and addon (or inverse)
		["format"] =				-- options of the 3rd argument
		{
			["mdy"] = "Y年n月j日", -- this is actually ymd but not mdy, just for backward-compatible
			["my"] = "Y年n月",
			["y"] = "Y年",
			["dmy"] = "Y年n月j日",
			["ymd"] = "Y年n月j日",
			["ym"] = "Y年n月"
		}
	},
	["monolingualtext"] = '<span lang="%language">%text</span>',
	["warnDump"] = "[[Category:在Wikidata模块中使用了Dump函数|Category:在Wikidata模块中使用了Dump函数]]",
	["ordinal"] = 
	{
		[1] = "",
		[2] = "",
		[3] = "",
		["default"] = ""
	}
}

return r