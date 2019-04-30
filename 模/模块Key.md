-- This module implements {{key press}}.

local kbdPrefix =
	'<kbd class=' ..
	'"keyboard-key nowrap" ' ..
	'style="border: 1px solid #aaa; ' ..
	-- The following is an expansion of {{border-radius|2px}}
	'-moz-border-radius: 2px; -webkit-border-radius: 2px; border-radius: 2px; ' ..
	-- The following is an expansion of {{box-shadow|1px|2px|2px|#ddd}}
	'-moz-box-shadow: 1px 2px 2px #ddd; -webkit-box-shadow: 1px 2px 2px #ddd; box-shadow: 1px 2px 2px #ddd; ' ..
	'background-color: #f9f9f9; ' ..
	-- The following is an expansion of {{linear-gradient|top|#eee, #f9f9f9, #eee}}
	'background-image: -moz-linear-gradient(top, #eee, #f9f9f9, #eee); background-image: -o-linear-gradient(top, #eee, #f9f9f9, #eee); background-image: -webkit-linear-gradient(top, #eee, #f9f9f9, #eee); background-image: linear-gradient(to bottom, #eee, #f9f9f9, #eee); ' ..
	'padding: 0.1em 0.3em; ' ..
	'font-family: inherit; ' ..
	'font-size: 0.85em;">'

local kbdSuffix = '</kbd>'

local keyText = {
	['caps lock'] = '⇪ Caps Lock',
	['[[caps_lock|caps lock]]'] = '⇪ [[大寫鎖定|Caps Lock]]',
	['shift'] = '⇧ Shift',
	['[[shift_key|shift]]'] = '⇧ [[换档键|Shift]]',
	['enter'] = '↵ Enter',
	['[[enter_key|enter]]'] = '↵ [[回車鍵|Enter]]',
	['cmd'] = '⌘ Cmd',
	['[[command_key|cmd]]'] = '⌘ [[Command键|Cmd]]',
	['command'] = '⌘ Command',
	['[[command_key|command]]'] = '⌘ [[Command键|Command]]',
	['opt'] = '⌥ Opt',
	['[[option_key|opt]]'] = '⌥ [[Option键|Opt]]',
	['option'] = '⌥ Option',
	['[[option_key|option]]'] = '⌥ [[Option键|Option]]',
	['tab'] = 'Tab ↹',
	['[[tab_key|tab]]'] = '[[製表鍵|Tab]] ↹',
	['backspace'] = '← Backspace',
	['[[backspace|backspace]]'] = '← [[后退键|ackspace]]',
	['win'] = '[[File:Windows_logo_-_2012_(black).svg|10px]] Win',
	['[[windows_key|win]]'] = '[[File:Windows_logo_-_2012_(black).svg|10px]] [[Windows键|Win]]',
	['menu'] = '≣ Menu',
	['[[menu_key|menu]]'] = '≣ [[菜单键|Menu]]',
	['up'] = '↑',
	['[[arrow_keys|up]]'] = '[[方向键|↑]]',
	['down'] = '↓',
	['[[arrow_keys|down]]'] = '[[方向键|↓]]',
	['left'] = '←',
	['[[arrow_keys|left]]'] = '[[方向键|←]]',
	['right'] = '→',
	['[[arrow_keys|right]]'] = '[[方向键|→]]',
	['asterisk'] = '*',
	['hash'] = '#',
	['[[#|#]]'] = '[[井号|#]]',
	['colon'] = ':',
	['[[:|:]]'] = '[[冒号|:]]',
	['pipe'] = '|',
	['[[|]]'] = '[[豎線|]]',
	['semicolon'] = ';',
	['[[;|;]]'] = '[[分号|;]]',
	['equals'] = '=',

	-- Left & right analog sticks.
	['l up'] = 'L↑',
	['l down'] = 'L↓',
	['l left'] = 'L←',
	['l right'] = 'L→',
	['l ne'] = 'L↗',
	['l se'] = 'L↘',
	['l nw'] = 'L↖',
	['l sw'] = 'L↙',

	['r up'] = 'R↑',
	['r down'] = 'R↓',
	['r left'] = 'R←',
	['r right'] = 'R→',
	['r ne'] = 'R↗',
	['r se'] = 'R↘',
	['r nw'] = 'R↖',
	['r sw'] = 'R↙',

	-- PlayStation.
	['ex'] = '×',
	['circle'] = '○',
	['square'] = '□',
	['triangle'] = '△',

	-- Nintendo 64 and GameCube.
	['c up'] = 'C↑',
	['c down'] = 'C↓',
	['c left'] = 'C←',
	['c right'] = 'C→',
	['c ne'] = 'C↗',
	['c se'] = 'C↘',
	['c nw'] = 'C↖',
	['c sw'] = 'C↙',
}

local keyAlias = {
	-- ['alternate name for key (alias)'] = 'name for key used in key table'
	['[[cmd_key|cmd]]'] = '[[command键|cmd]]',
	['[[cmd_key|command]]'] = '[[command键|command]]',
	['[[opt_key|opt]]'] = '[[option键|opt]]',
	['[[option_key|option key]]'] = '[[option键|option]]',
	['[[opt_key|option]]'] = '[[option键|option]]',
	['[[win_key|win]]'] = '[[windows键|win]]',
	['*'] = 'asterisk',
	['#'] = 'hash',
	[':'] = 'colon',
	[';'] = 'semicolon',
	['l-up'] = 'l up',
	['l-down'] = 'l down',
	['l-left'] = 'l left',
	['l-right'] = 'l right',
	['l-ne'] = 'l ne',
	['l-se'] = 'l se',
	['l-nw'] = 'l nw',
	['l-sw'] = 'l sw',
	['r-up'] = 'r up',
	['r-down'] = 'r down',
	['r-left'] = 'r left',
	['r-right'] = 'r right',
	['r-ne'] = 'r ne',
	['r-se'] = 'r se',
	['r-nw'] = 'r nw',
	['r-sw'] = 'r sw',
	['ps x'] = 'ex',
	['ps c'] = 'circle',
	['ps s'] = 'square',
	['ps t'] = 'triangle',
	['c-up'] = 'c up',
	['c-down'] = 'c down',
	['c-left'] = 'c left',
	['c-right'] = 'c right',
	['c-ne'] = 'c ne',
	['c-se'] = 'c se',
	['c-nw'] = 'c nw',
	['c-sw'] = 'c sw',
}

local Collection = {}
Collection.__index = Collection
do
	function Collection:add(item)
		if item ~= nil then
			self.n = self.n + 1
			self[self.n] = item
		end
	end
	function Collection:join(sep)
		return table.concat(self, sep)
	end
	function Collection:sort(comp)
		table.sort(self, comp)
	end
	function Collection.new()
		return setmetatable({n = 0}, Collection)
	end
end

local function keyPress(args)
	local chainNames = {
		'chain first',
		'chain second',
		'chain third',
		'chain fourth',
		'chain fifth',
		'chain sixth',
		'chain seventh',
		'chain eighth',
		'chain ninth',
	}
	local result = Collection.new()
	local chainDefault = args.chain or '+'
	for i, id in ipairs(args) do
		if i > 1 then
			result:add(args[chainNames[i - 1]] or chainDefault)
		end
		local lc = id:lower()
		local text = keyText[lc] or keyText[keyAlias[lc]] or id
		result:add(kbdPrefix .. text .. kbdSuffix)
	end
	return result:join()
end

local function keypress(frame)
	-- Called by "{{key press|...}}".
	-- Using the template doubles the post‐expand include size.
	return keyPress(frame:getParent().args)
end

local function press(frame)
	-- Called by "{{#invoke:key|press|...}}".
	return keyPress(frame.args)
end

return {
	keypress = keypress,
	press = press,
}