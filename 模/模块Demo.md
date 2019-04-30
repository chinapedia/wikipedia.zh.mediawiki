local p = {}

--creates a frame object that cannot access any of the parent's args
--unless a table containing a list keys of not to inherit is provided
function disinherit(frame, onlyTheseKeys)
	local parent = frame:getParent() or frame
	local orphan = parent:newChild{}
	orphan.getParent = parent.getParent --returns nil
	orphan.args = {}
	if onlyTheseKeys then
		local family = {parent, frame}
		for f = 1, 2 do
			for k, v in pairs(family[f] and family[f].args or {}) do
				orphan.args[k] = orphan.args[k] or v
			end
		end
		parent.args = mw.clone(orphan.args)
		setmetatable(orphan.args, nil)
		for _, k in ipairs(onlyTheseKeys) do
			rawset(orphan.args, k, nil)
		end
	end
	return orphan, parent
end

function p.get(frame, arg, passArgs)
	local orphan, frame = disinherit(frame, passArgs and {arg or 1})
	local code, noWiki, preserve = frame.args[arg or 1] or ''
	if code:match'nowiki' then
		local placeholder, preserve = ('6'):char(), {}
		code = mw.text.unstripNoWiki(code)
		noWiki = code:gsub('%%', placeholder):gsub('<', '<'):gsub('>', '>')
		for k in noWiki:gmatch('&.-;') do
			if not preserve[k] then
				preserve[k] = true
				table.insert(preserve, (k:gsub('&', '&')))
				noWiki = noWiki:gsub('(&.-;)', '%%%s')
			end
		end
		noWiki = mw.text.nowiki(noWiki):format(unpack(preserve)):gsub(placeholder, '%%')
	end
	return {
		source = noWiki or code,
		output = orphan:preprocess(code):gsub(frame.args.demo_kill_categories and '%[%[Category.-%]%]' or '', ''),
		frame = frame
	}
end

function p.main(frame, demoTable)
	local show = demoTable or p.get(frame)
	local args = show.frame.args
	args.br = tonumber(args.br or 1) and ('<br>'):rep(args.br or 1) or args.br or ''
	if show[args.result_arg] then
		return show[args.result_arg]
	end
	return string.format('<pre%s>%s</pre>%s%s', args.style and string.format(" style='%s'", args.style) or '', show.source, args.br, show.output)
end

--passing of args into other module without preprocessing
function p.module(frame)
	local orphan, frame = disinherit(frame, {
		'demo_template',
		'demo_module',
		'demo_module_func',
		'demo_main',
		'demo_br',
		'demo_result_arg',
		'demo_kill_categories'
	})
	local template = frame.args.demo_template and 'Template:'..frame.args.demo_template
	local demoFunc = frame.args.demo_module_func or 'main\n'
	local demoModule = require('Module:' .. frame.args.demo_module)[demoFunc:match('^%s*(.-)%s*$')]
	frame.args.br, frame.args.result_arg = frame.args.demo_br, frame.args.demo_result_arg
	if demoModule then
		local named = {insert = function(self, ...) table.insert(self, ...) return self end}
		local source = {insert = named.insert, '{{', frame.args.demo_template or frame.args.demo_module, '\n'}
		if not template then
			source:insert(2, '#invoke:'):insert(4, '|'):insert(5, demoFunc)
		end
		local insertNamed = #source + 1
		for k, v in pairs(orphan.args) do
			local nan, insert = type(k) ~= 'number', {v}
			local target = nan and named or source
			target:insert'|'
			if nan then
				target:insert(k):insert'=':insert'\n'
				table.insert(insert, 1, #target)
			end
			target:insert(unpack(insert))
			local nowiki = v:match('nowiki')
			if nowiki or v:match('{{.-}}') then
				orphan.args[k] = frame:preprocess(nowiki and mw.text.unstripNoWiki(v) or v)
			end
		end
		source:insert'}}'
		table.insert(source, insertNamed, table.concat(named))
		return p.main(orphan, {
			source = mw.text.encode(table.concat(source), "<>'|=~"),
			output = tostring(demoModule(orphan)):gsub(frame.args.demo_kill_categories and '%[%[Category.-%]%]' or '', ''),
			frame = frame
		})
	else
		return "ERROR: Invalid module function: "..demoFunc
	end
end

return p