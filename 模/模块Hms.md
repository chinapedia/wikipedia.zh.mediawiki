local p = {}

function p._error( error_str )
    return '[[Category:输入值出现错误的持续时间|Category:输入值出现错误的持续时间]]<strong class="error">错误：' .. error_str .. '</strong>'
end

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {wrappers = {'Template:Duration', 'Template:Duration/sandbox'}})
	local tmp = args.duration or args[1] or ''
	local duration = {}
	if tonumber(args[1]) or args[2] or args[3] then
		if args[4] then return p._error('不应指定参数4') end
		if not args[1] or args[1] == '' then
			duration = {args[2] or 0, args[3] or 0}
		else
			duration = {args[1], args[2] or 0, args[3] or 0}
		end
		tmp = nil
		for k, v in ipairs(duration) do
			duration[k] = tonumber(v)
			if not duration[k] then return p._error('无效的值') end
		end
	elseif args.h or args.m or args.s then
		if not args.h or args.h == '' then
			duration = {args.m or 0, args.s or 0}
		else
			duration = {args.h, args.m or 0, args.s or 0}
		end
		tmp = nil
		for k, v in ipairs(duration) do
			duration[k] = tonumber(v)
			if not duration[k] then return p._error('无效的值') end
		end
	else
		if mw.ustring.find(tmp, 'class="duration"', 1, yes) then return tmp end -- if there is already a microformat, don't do anything
		duration = mw.text.split(mw.ustring.match(tmp, '%d*:?%d+:%d+%.?%d*') or '', ':') -- split into table
		if duration[4] then return p._error('不能超过两个冒号') end
		for k, v in ipairs(duration) do duration[k] = tonumber(v) or 0 end -- convert values to numbers
	end
	if duration[3] then
		if (duration[1] + duration[2] + duration[3]) == 0 then return nil end
		if (duration[1] ~= math.ceil(duration[1])) or (duration[2] ~= math.ceil(duration[2])) then return p._error('小时数和分钟数必须是整数') end
		if duration[3] >= 60 then return p._error('秒数不能大于59') end
		if duration[2] >= 60 then return p._error('当小时数存在时，分钟数不能大于59') end
		if duration[2] < 10 then duration[2] = '0'..duration[2] end -- zero padding
		if duration[3] < 10 then duration[3] = '0'..duration[3] end
		duration = '<span class="duration"><span class="h">' .. duration[1] .. '</span>:<span class="min">' .. duration[2] .. '</span>:<span class="s">' .. duration[3] .. '</span></span>'
	elseif duration[2] then
		if (duration[1] + duration[2]) == 0 then return nil end
		if duration[1] ~= math.ceil(duration[1]) then return p._error('小时数和分钟数必须是整数') end
		if duration[2] >= 60 then return p._error('秒数不能大于59') end
		if duration[2] < 10 then duration[2] = '0'..duration[2] end -- zero padding
		duration = '<span class="duration"><span class="min">' .. duration[1] .. '</span>:<span class="s">' .. duration[2] .. '</span></span>'
	else
		duration = ''
	end
	
	if tmp and tmp ~= '' then
		if duration ~= '' then tmp = mw.ustring.gsub(tmp, '%d*:?%d+:%d+%.?%d*', duration, 1) else tmp = tmp .. ' [[Category:不含hAudio微格式的持续时间|Category:不含hAudio微格式的持续时间]]' end
	else
		if duration ~= '' then tmp = duration end
	end
	return tmp
end

return p