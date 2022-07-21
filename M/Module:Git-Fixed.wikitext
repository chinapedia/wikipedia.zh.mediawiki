local p = {}

local branches = {
	['1.24wmf1'] = os.time{year=2014, month=4, day=17},
	['1.24wmf17'] = os.time{year=2014, month=8, day=14},
	['1.25wmf1'] = os.time{year=2014, month=9, day=25},
	['1.25wmf13'] = os.time{year=2014, month=12, day=24},
}

local interval = 7 * 24 * 60 * 60

local delay = 7 * 24 * 60 * 60

local function parse(branch)
	major, minor, wmf = mw.ustring.match(branch, '(%d+)%.(%d+)wmf(%d+)')
	return tonumber(major), tonumber(minor), tonumber(wmf)
end

local function format(major, minor, wmf)
	return mw.ustring.format('%d.%dwmf%d', major, minor, wmf)
end

local function current()
	return parse(mw.ustring.match(mw.site.currentVersion, '(%S+)'))
end

local function compare(major1, minor1, wmf1, major2, minor2, wmf2)
	if major1 > major2 then
		return 1
	elseif major1 < major2 then
		return -1
	elseif minor1 > minor2 then
		return 1
	elseif minor1 < minor2 then
		return -1
	elseif wmf1 > wmf2 then
		return 1
	elseif wmf1 < wmf2 then
		return -1
	else
		return 0
	end
end

local function diffBranch(major1, minor1, wmf1, major2, minor2, wmf2)
	if major1 ~= major2 or minor1 ~= minor2 or wmf1 < wmf2 then
		error('Unknown branch ' .. format(major1, minor1, wmf1))
	end
	return wmf1 - wmf2
end

local function branchSchedule(major, minor, wmf)
	local latestMajor, latestMinor, latestWmf = 0, 0, 0
	local latestTime = 0
	for branch, branchTime in pairs(branches) do
		local branchMajor, branchMinor, branchWmf = parse(branch)
		if compare(branchMajor, branchMinor, branchWmf, latestMajor, latestMinor, latestWmf) > 0
			and compare(branchMajor, branchMinor, branchWmf, major, minor, wmf) <= 0
		then
				latestMajor, latestMinor, latestWmf = branchMajor, branchMinor, branchWmf
				latestTime = branchTime
		end
	end
	return latestTime + diffBranch(major, minor, wmf, latestMajor, latestMinor, latestWmf) * interval
end

local function fixed(frame)
	return frame:expandTemplate{ title = 'Template:Fixed' }
end

local function fixedLater(frame, timeDiff)
	local text
	if timeDiff < 12 * 60 * 60 then
		text = '将很快修复'
	else
		local friendlySeconds = math.modf((timeDiff + 12 * 60 * 60) / (24 * 60 * 60)) * (24 * 60 * 60)
		text = '将于' .. mw.getContentLanguage():formatDuration(friendlySeconds) .. '后修复'
	end
	return '[[File:Pictogram_voting_wait.svg|20px]] <b>' .. text .. '</b>'
end

function p.main(frame)
	local major, minor, wmf = parse(frame.args[1])
	local currentMajor, currentMinor, currentWmf = current()
	local text
	if compare(currentMajor, currentMinor, currentWmf, major, minor, wmf) >= 0 then
		text = fixed(frame)
	else
		text = fixedLater(frame, os.difftime(branchSchedule(major, minor, wmf) + delay, os.time()))
	end
	return text .. '<b>于[[mw:'_.._mw.ustring.format('MediaWiki_%d.%d/wmf%d',_major,_minor,_wmf)_.._'|MediaWiki ' .. format(major, minor, wmf) .. ']]</b>'
end

function p.next(frame)
	local major, minor, wmf = current()
	local branchTime = branchSchedule(major, minor, wmf)
	local currentTime = os.time()
	while true do
		local timeDiff = os.difftime(branchTime, currentTime)
		if math.abs(timeDiff) < 12 * 60 * 60 then
			error('You need to check whether branching took place or not manually today...')
		elseif timeDiff > 0 then
			return format(major, minor, wmf)
		else
			wmf = wmf + 1
			branchTime = branchTime + interval
		end
	end
end

return p