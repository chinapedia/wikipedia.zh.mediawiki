local p = {}
local lang = mw.language.new('zh')

function tostringOrNil(value)
	if value ~= nil then
		value = tostring(value)
	end
	return value
end

function getCandidateList(pageName, currentTime)
	local page = mw.title.new(pageName)
	local candidates =
		mw.text.jsonDecode(page:getContent(), mw.text.JSON_TRY_FIXING)

	-- change mw timestamp to unix timestamp
	for _, item in pairs(candidates) do
		for i in pairs(item.displayTimeRanges) do
			item.displayTimeRanges[i][1] = tonumber(
				lang:formatDate('U', tostring(item.displayTimeRanges[i][1]))
			)
			-- use current time when the "end time" is null
			item.displayTimeRanges[i][2] = tonumber(
				lang:formatDate(
					'U', tostringOrNil(
						item.displayTimeRanges[i][2] or currentTime
					)
				)
			)
		end
	end
	return candidates
end

function pickCandidate(candidateList, currentTime, timeStart, timeInterval)
	local processedTime = timeStart
	local currentDisplayStart =
		math.floor(currentTime / timeInterval) * timeInterval
	local currentDisplayEnd = currentDisplayStart + timeInterval
	local maxCycles = 100
	mw.log("currentDisplayStart: ", currentDisplayStart)
	while maxCycles > 0 do
		local cycleItems = 0
		local nextStatusChanged = 0xffffffffffffffff
		for _, item in pairs(candidateList) do
			for _, range in pairs(item.displayTimeRanges) do
				local rangeStart =
					math.ceil(range[1] / timeInterval) * timeInterval
				local rangeEnd =
					math.ceil(range[2] / timeInterval) * timeInterval
				if rangeStart > processedTime then
					nextStatusChanged = math.min(nextStatusChanged, rangeStart)
				end
				if rangeEnd > processedTime then
					nextStatusChanged = math.min(nextStatusChanged, rangeEnd)
				end
				if processedTime < rangeStart or
					processedTime >= rangeEnd then
					-- continue
					-- mw.log(rangeStart)
					-- mw.log(rangeEnd)
					-- mw.log('---------')
				elseif processedTime >= currentDisplayStart and
					processedTime < currentDisplayEnd then
					return item.title
				else
					-- processedTime = processedTime + timeInterval
					cycleItems = cycleItems + 1
					break
				end
			end
			-- mw.log(processedTime)
		end
		mw.log("nextStatusChanged: ", nextStatusChanged)
		mw.log("CycleItems: ", cycleItems)
		mw.log("ProcessedTime (before): ", processedTime)
		if cycleItems > 0 then
			local times =
				math.ceil((nextStatusChanged - processedTime) / timeInterval)
			processedTime =
				processedTime + math.floor(times / cycleItems) *
				cycleItems * timeInterval;
			local remaining = times % cycleItems
			mw.log("remaining: ", remaining)

			-- process remaining items in the "partial" cycle
			if remaining > 0 then
				for _, item in pairs(candidateList) do
					-- mw.log(item.title)
					
					for _, range in pairs(item.displayTimeRanges) do
						-- mw.log(remaining, range[1], range[2])
						local rangeStart =
							math.ceil(range[1] / timeInterval) * timeInterval
						local rangeEnd =
							math.ceil(range[2] / timeInterval) * timeInterval
						if processedTime < rangeStart or
							processedTime > rangeEnd then
							-- continue
						--elseif remaining > 0 then
						--	remaining = remaining - 1
						--	break
						elseif processedTime >= currentDisplayStart and
							processedTime < currentDisplayEnd then
							return item.title
						else
							processedTime = processedTime + timeInterval
							break
						end
					end
				end
			end



		else
			processedTime = math.max(processedTime, nextStatusChanged)
		end
		mw.log("ProcessedTime: ", processedTime)
		maxCycles = maxCycles - 1
	end
	-- TODO: raise an error
	return 'EXCEED LIMITATION'
end

function p.getCandidate(frame)
	local args = frame.args
	local currentTime = tonumber(
		lang:formatDate('U', tostringOrNil(args.currentTime))
	)
	local candidateList = getCandidateList(
		args.candidateList,
		args.currentTime
	)
	local timeStart = tonumber(
		lang:formatDate(
			"U", tostringOrNil(args.timeStart) or '19700101000000'
		)
	)
	local timeInterval = tonumber(args.timeInterval) or 86400
	local title = args.titlePrefix or 'Wikipedia:特色条目/'
	title = title .. pickCandidate(
		candidateList, currentTime, timeStart, timeInterval)
	return title
end

function p.main(frame)
	return mw.getCurrentFrame():expandTemplate({
		title = p.getCandidate(frame)
	})
end

return p