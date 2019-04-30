local yesno = require('Module:Yesno')

local pageCutoffs = {
	-- minimum inactive cutoff, notarget cutoff, maximum inactive cutoff
	-- - minimum inactive cutoff and maximum inactive cutoff control
	--   the colours used to highlight an inactive member
	-- - notarget cutoff controls when a member is no longer sent a mass
	--   mailing
	['Wikipedia:WikiProject Maine/members'] = { '-10 years', '-10 years', '-10 years' },
	['Wikipedia:WikiProject Articles for creation/Participants/Message'] = { '-1 year', '-1 year', '-2 years' },
	['Wikipedia:WikiProject Baseball/Outreach/Newsletter/Subscriber list'] = { '-1 year', '-2 months', '-2 years' },
	['Template:Mailing list member/testcases'] = { '-1 year', '-18 months', '-2 years' }
}

local defaultCutoffs = { '-1 year', '-1 year', '-2 years' }

local p = {}

local function parenText(text, color, class)
	return string.format(
		' <span%s style="font-size:0.95em;font-weight:bold;color:%s">(%s)</span>',
		class and (' class="' .. class .. '"') or '',
		color,
		text
	)
end

function p.main(frame)
	local pargs = frame:getParent().args
	local lang = mw.getContentLanguage()
	local notarget = yesno(pargs.notarget)
	local page, retval
	if pargs.user then
		page = 'User talk:' .. pargs.user
		if yesno(pargs.blocked, true) then
			retval = frame:expandTemplate{title = 'Userblock', args = { pargs.user }} .. parenText('自' .. lang:formatDate('Y年Fj日', pargs.blocked)..'開始被封鎖', 'red', 'blocked-member')
			if notarget == nil then
				notarget = true
			end
		else
			retval = frame:expandTemplate{title = 'User', args = { pargs.user }}
		end
	elseif pargs.page then
		page = pargs.page
		retval = '[['_.._page_.._'|' .. page .. ']]'
	else
		return '<span class="error">未定義使用者名稱或頁面名稱。</span>'
	end
	if yesno(pargs.inactive, true) then
		local cutoffs = pageCutoffs[mw.title.getCurrentTitle().prefixedText] or defaultCutoffs
		local inactiveTS = tonumber(lang:formatDate('U', pargs.inactive))
		local minInactive = tonumber(lang:formatDate('U', cutoffs[1]))
		local notargetInactive = tonumber(lang:formatDate('U', cutoffs[2]))
		local maxInactive = tonumber(lang:formatDate('U', cutoffs[3]))
		if notarget == nil then
			notarget = inactiveTS < notargetInactive
		end
		local text, color = '開始不活躍時間:'
		if inactiveTS < maxInactive then
			color = 'red'
		elseif inactiveTS < minInactive then
			color = '#555'
		else
			color = '#080'
			text = '最後一次活動時間是在'
		end
		retval = retval .. parenText(string.format(
				'%s%s',
				text,
				lang:formatDate('Y年Fj日', pargs.inactive)
			), color, 'inactive-member')
	end
	if notarget then
		return retval .. parenText('未接收大量傳送的訊息。', '#555')
	end
	frame:callParserFunction('#target', page)
	return retval
end

return p