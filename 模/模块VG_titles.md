require('Module:No globals')
local getArgs = require('Module:Arguments').getArgs
local yesno = require('Module:Yesno')

local p = {}

local function left(args, rowspan)

	local function article(args)
		
		return string.format('<div class="fn" style="margin-bottom: 4pt;">%s</div>', args.title or '<span class="error">未填写<code>title =</code>参数</span>')

	end
	
	local function release(args)
		local status, date
		
		if args.platform then
			return string.format('<div>%s － %s%s</div>',
				args.date or '<span class="error">未填写<code>date =</code>参数</span>',
				args.platform,
				args.refs or ''
			)
		end

		if yesno(args.series) then
			return (args.date or '') .. (args.refs or '')
		end

		if args.datetype then
			status, date = args.datetype, args.date
		elseif yesno(args.futuregame) then
			status, date = '预定发行日期', args.date
		elseif args.canceled then
			if args.date then
				status, date = '原定发行日期', args.date
			else
				status, date = '取消日期', args.canceled
			end
		else
			status = '首发日期'
			date = args.date or '<span class="error">未填写<code>date =</code>参数</span>'
		end
		
		return string.format('<div><b>%s</b>%s：<br />%s</div>', status, args.refs or '', date)
	end

	return string.format('\n| scope="row" style="%s" rowspan="%s" | %s',
		'vertical-align: middle; width: 24em; text-align: center; background-color:transparent;',
		rowspan,
		article(args) .. release(args)
	)
	
end

local function right1(args)
	local status
	
	if yesno(args.futuregame) then
		status = '预定平台与发行年份'
	elseif args.canceled then
		status = '原定平台与发行年份'
	else
		status = '各平台发行年份'
	end
	
	return '\n| td valign="top" | <b>' .. status .. '</b>：\n' ..args.release
end
	
local function right2(args)
	return '\n| valign="top" | <b>备注</b>：\n' .. (args.notes or '')
end

function p.item(frame)
	local args = getArgs(frame, {frameOnly = true})
	
	if args.release == nil then
		return left(args, '1') .. right2(args) .. '\n|-'
	end
	
	if args.notes == nil then
		return  left(args, '1') .. right1(args) ..'\n|-'
	end
	
	return left(args, '2') .. right1(args) .. '\n|-' .. right2(args) .. '\n|-'

end

return p