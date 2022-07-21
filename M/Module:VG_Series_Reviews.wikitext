local getArgs = require('Module:Arguments').getArgs
local yesno = require('Module:Yesno')

local p = {}

local function switcher(args, col)
	if col == 'mc' then
		if yesno(args.mc) ~= false then
			return true
		end
	end
	
	if col == 'gr' then
		if yesno(args.gr) == true then
			return true
		end
	end
	
	if col == 'sales' then
		if yesno(args.sales) == true then
			return true
		end
	end
	
	if col == 'fam' then
		if yesno(args.fam) == true then
			return true
		end
	end

end
	
local function row(args, i)
	local ret = ""

	ret = ret .. "|-\n"
	ret = ret .. "! scope=\"row\" | " .. args["game" ..i] .. " \n"
	if switcher(args, 'sales') then
		ret = ret .. "| style=\"text-align: center;\" | " .. (args["sales" ..i] or '') .. " \n"
	end
	if switcher(args, 'fam') then
		ret = ret .. "| style=\"text-align: center;\" | " .. (args["fam" ..i] or '') .. " \n"
	end
	if switcher(args, 'gr') then
		ret = ret .. "| style=\"text-align: center;\" | " .. (args["gr" ..i] or '') .. " \n"
	end
	if switcher(args, 'mc') then
		ret = ret .. "| style=\"text-align: center;\" | " .. (args["mc" ..i] or '') .. " \n"
	end
	
	return ret
end

function p.main(frame)
	local args = getArgs(frame)
	return p._main(args)
end

function p._main(args)
	local ret = ""

	ret = ret .. "{| class=\"wikitable plainrowheaders\" style=\"font-size: 90%; float: right; clear: right; margin:0.5em 0 0.5em 1em;\"\n"
	
	ret = ret .."|+ style=\"font-size: 111.11%;\" | "
	if args.title then
		ret = ret .. args.title
	elseif switcher(args, 'sales') then
		if switcher(args, 'fam') then
			ret = ret .. "销量与得分"
		elseif switcher(args, 'gr') or switcher(args, 'mc') then
			ret = ret .. "销量与汇总得分"
		else
			ret = ret .. "销量"
		end
	elseif switcher(args, 'fam') then
		if switcher(args, 'gr') or switcher(args, 'mc') then
			ret = ret .. "日本与西方评论得分"
		else
			ret = ret .. "《Fami通》得分"
		end
	else
		ret = ret .. "汇总得分"
	end
	if args.updated then
		ret = ret .. "<br /><small>" .. args.updated .."更新</small>"
	end
	ret = ret .. " \n"
	
	ret = ret .. "! scope=\"col\" | 游戏 \n"
	if switcher(args, 'sales') then
		ret = ret .. "! scope=\"col\" | " .. (args.sales_title or "销量") .. " \n"
	end
	if switcher(args, 'fam') then
		ret = ret .. "! scope=\"col\" | " .. (args.fam_title or  "[[Fami通|Fami通]]") .. " \n"
	end
	if switcher(args, 'gr') then
		ret = ret .. "! scope=\"col\" | " .. (args.gr_title or  "[[GameRankings|GameRankings]]") .. " \n"
	end
	if switcher(args, 'mc') then
		ret = ret .. "! scope=\"col\" | " .. (args.mc_title or  "[[Metacritic|Metacritic]]") .. " \n"
	end
	
	for i = 1, 30 do
		if args["game" ..i] then
			ret = ret .. row(args, i)
		end
	end
	
	ret = ret .. "|}"
	
	return ret
end

return p