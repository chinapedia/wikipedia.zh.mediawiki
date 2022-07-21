-- Replacement for [[Template:Time_ago|Template:Time ago]]
local numberSpell = require('Module:NumberSpell')._main
local yesno = require('Module:Yesno')

local p = {}

-- Table to convert entered text values to numeric values.
timeText = {
	['seconds'] = 1,
	['minutes'] = 60,
	['hours'] = 3600,
	['days'] = 86400,
	['weeks'] = 604800,
	['months'] = 2678400,
	['years'] = 31557600
}

-- Table containing tables of possible units to use in output.
timeUnits = {
	[1] = { '秒', '秒', "秒", "秒" },
	[60] = { '分鐘', '分鐘', "分鐘", "分鐘" },
	[3600] = { '小時', '小時', "小時", "小時" },
	[86400] = { '天', '天', "天", "天" },
	[604800] = { '周', '周', "周", "周" },
	[2678400] = { '個月', '個月', "個月", "個月" },
	[31557600] = { '年', '年', "年", "年" }
}

function p._main( args )
	-- Initialize variables
	local lang = mw.language.getContentLanguage()
	local auto_magnitude_num
	local min_magnitude_num
	local result
	local result_unit
	local magnitude = args.magnitude
	local min_magnitude = args.min_magnitude
	local purge = args.purge
	local spell_out = args.spellout
	local spell_out_max = args.spelloutmax
	
	-- Add a purge link if something (usually "yes") is entered into the purge parameter
	if purge then
		purge = '​<span class="plainlinks">（[' .. mw.title.getCurrentTitle():fullUrl('action=purge') .. ' 更新]）</span>'
	else
		purge = ''
	end

	-- Check that the entered timestamp is valid. If it isn't, then give an error message.
	local noError, inputTime = pcall( lang.formatDate, lang, 'U', args[1], true )
	if not noError then
		return '<strong class="error">錯誤：第一個參數不能被解析為日期或時間。</strong>'
	end

	-- Store the difference between the current time and the inputted time, as well as its absolute value.
	local timeDiff = lang:formatDate( 'U', nil, true ) - inputTime
	local absTimeDiff = math.abs( timeDiff )

	if magnitude then
		auto_magnitude_num = 0
		min_magnitude_num = timeText[magnitude]
	else
		-- Calculate the appropriate unit of time if it was not specified as an argument.
		local autoMagnitudeData = {
			{ denom = 63115200, amn = 31557600 },
			{ denom = 5356800, amn = 2678400 },
			{ denom = 172800, amn = 86400 },
			{ denom = 7200, amn = 3600 },
			{ denom = 120, amn = 60 }
		}
		for i, t in ipairs( autoMagnitudeData ) do
			if absTimeDiff / t.denom >= 1 then
				auto_magnitude_num = t.amn
				break
			end
		end
		auto_magnitude_num = auto_magnitude_num or 1
		if min_magnitude then
			min_magnitude_num = timeText[min_magnitude]
		else
			min_magnitude_num = -1
		end
	end

	if not min_magnitude_num then
		-- Default to seconds if an invalid magnitude is entered.
		min_magnitude_num = 1
	end

	local magnitude_num = math.max( min_magnitude_num, auto_magnitude_num )
	local result_num = math.floor ( absTimeDiff / magnitude_num )

	local punctuation_key, suffix
	if timeDiff >= 0 then -- Past
		if result_num == 1 then
			punctuation_key = 1
		else
			punctuation_key = 2
		end
		if args.ago == '' then
			suffix = ''
		else
			suffix = '' .. (args.ago or '前')
		end
	else -- Future
		if args.ago == '' then
			suffix = ''
			if result_num == 1 then
				punctuation_key = 1
			else
				punctuation_key = 2
			end
		else
			suffix = '<!-- time-->'
			if result_num == 1 then
				punctuation_key = 3
			else
				punctuation_key = 4
			end
		end
	end
	result_unit = timeUnits[ magnitude_num ][ punctuation_key ]

	-- Convert numerals to words if appropriate.
	spell_out_max = tonumber( spell_out_max ) -- Would cause script errors if not a number.
	local result_num_text
	if ( spell_out == 'auto' and 1 <= result_num and result_num <= 9 and result_num <= ( spell_out_max or 9 ) )
		or ( yesno( spell_out ) and 1 <= result_num and result_num <= 100 and result_num <= ( spell_out_max or 100 ) )
	then
		result_num_text = numberSpell( result_num )
	else
		result_num_text = tostring( result_num )
	end

	result = result_num_text .. '' .. result_unit .. suffix -- Spaces for suffix have been added in earlier.
	return result .. purge
end

function p.main( frame )
	local args = require( 'Module:Arguments' ).getArgs( frame, {
		valueFunc = function( k, v )
			if v then
				v = v:match( '^%s*(.-)%s*$' ) -- Trim whitespace.
				if k == 'ago' or v ~= '' then
					return v
				end
			end
			return nil
		end,
		wrappers = 'Template:Time ago'
	})
	return p._main( args )
end

return p