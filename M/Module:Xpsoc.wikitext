-- This module implements {{xpsoc}}.

local mTemplateInvocation = require('Module:Template invocation')

local p = {}

function p._main(args, frame)
	frame = frame or mw.getCurrentFrame()

	-- Get the invocation arguments.
	local name = args[1]
	if not name then
		error('no template name passed to xpsoc', 2)
	end
	local invArgs = {}
	for k, v in pairs(args) do
		if k ~= 1 then
			if type(k) == 'number' then
				invArgs[k - 1] = v
			else
				local num = k:match('^n([1-9][0-9]*)$')
				if num then
					invArgs[args[k]] = args['v' .. num]
				end
			end
		end
	end

	local invocation = mTemplateInvocation.invocation(name, invArgs, 'nowiki')
	local gives = args.gives or mw.language.getContentLanguage():getArrow('forwards')
	local result = frame:preprocess(mTemplateInvocation.invocation(name, invArgs))
	
	return string.format('<code>%s</code> %s %s', invocation, gives, result)
end

function p.main(frame)
	return p._main(frame:getParent().args, frame)
end

return p