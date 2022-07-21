require('Module:No globals')

local p = {}
local data = require('Module:VG Reviews/data')
local yesno = require('Module:Yesno')
local vgwd = require('Module:Video game wikidata')
local getArgs

local function getActiveSystems(args)
	local activeSystems = {}
	for k,v in pairs(args) do
		if data.systems[k] and yesno(v) then
			table.insert(activeSystems, k)
		end
	end
	table.sort(activeSystems, function(a, b)
		return data.systems[a].sortkey < data.systems[b].sortkey
	end)
	return activeSystems
end

local function getArgKeyTables(args)
	local reviewers, aggregators, awards = {}, {}, {}
	for k in pairs(args) do
		if string.match(k, '^rev%d+$') then
			table.insert(reviewers, k)
		elseif string.match(k, '^agg%d+$') then
			table.insert(aggregators, k)
		elseif string.match(k, '^award%d+$') then
			table.insert(awards, k)
		end
	end
	local function comparator(a, b)
		return tonumber(a:match('%d+')) < tonumber(b:match('%d+'))
	end
	table.sort(reviewers, comparator)
	table.sort(aggregators, comparator)
	table.sort(awards, comparator)
	return reviewers, aggregators, awards
end

local function getProvidedReviewersAndAggregators(args, usePlatforms)
	local providedReviewers, providedAggregators = {}, {}
	if usePlatforms then
		local seen = {}
		for k in pairs(args) do
			local splitPos = string.find(k, '_')
			if splitPos then
				local halfarg = string.sub(k, 1, splitPos - 1)
				if not seen[halfarg] then
					seen[halfarg] = true
					if data.reviewers[halfarg] then
						table.insert(providedReviewers, halfarg)
					elseif data.aggregators[halfarg] then
						table.insert(providedAggregators, halfarg)
					end
				end
			end
		end
	else
		for k in pairs(args) do
			if not string.find(k, '_') then
				if data.reviewers[k] then
					table.insert(providedReviewers, k)
				elseif data.aggregators[k] then
					table.insert(providedAggregators, k)
				end
			end
		end
	end
	table.sort(providedReviewers, function(a, b)
		return data.reviewers[a].sortkey < data.reviewers[b].sortkey
	end)
	table.sort(providedAggregators, function(a, b)
		return data.aggregators[a].sortkey < data.aggregators[b].sortkey
	end)
	return providedReviewers, providedAggregators
end

local function renderTitleRow(tbl, title)
	local titleCell = tbl:tag('tr'):tag('th'):css('font-size', '120%')

	if title then
		titleCell
			:wikitext(title)
	else
		titleCell
			:addClass('Reception')
			:wikitext(data.i18n.reception)
	end
end

local function renderMainHeading(builder, colspan, headingText, borderTop)
	builder:tag('tr'):tag('th')
		:attr('colspan', colspan)
		:css('background', '#d1dbdf')
		:css('font-size', '120%')
		:css('border-top', borderTop)
		:wikitext(headingText)
end

local function renderHeadingRowWithSystems(builder, mainHeading, activeSystems)
	renderMainHeading(builder, #activeSystems + 1, mainHeading)
	builder:tag('tr')
		:tag('th')
			:attr('rowspan', '2')
			:css('background', '#e8f4f8')
			:css('text-align', 'center')
			:css('vertical-align', 'middle')
			:wikitext(data.i18n.publication)
		:done()
		:tag('th')
			:attr('colspan', #activeSystems)
			:css('background', '#e8f4f8')
			:css('vertical-align', 'middle')
			:wikitext(data.i18n.score)
	builder = builder:tag('tr')
	for _,v in ipairs(activeSystems) do
		builder:tag('th'):wikitext(data.systems[v].name)
	end
end

local function renderHeadingRow(builder, mainHeading, nameHeading)
	renderMainHeading(builder, 2, mainHeading)
	builder
		:tag('tr')
			:tag('th')
				:css('background', '#e8f4f8')
				:css('text-align', 'center')
				:css('vertical-align', 'middle')
				:wikitext(nameHeading)
			:done()
			:tag('th')
				:css('background', '#e8f4f8')
				:css('vertical-align', 'middle')
				:wikitext(data.i18n.score)
end

local function renderRatingsBySystem(builder, code, name, activeSystems, args, na)
	builder = builder:tag('tr')
	builder:tag('td')
		:css('vertical-align','middle')
		:wikitext(name)

	for _,v in ipairs(activeSystems) do
		local combinedCode = code .. '_' .. v
		local cell = builder:tag('td')
		if args[combinedCode] then
			cell
				:css('vertical-align', 'middle')
				:css('font-size', '110%')
				:wikitext(args[combinedCode])
		elseif na then
			cell
				:css('color', 'lightgray')
				:css('vertical-align','middle')
				:css('text-align', 'center')
				:css('font-size', '110%')
				:addClass('table-na')
				:wikitext(data.i18n.na)
		end
	end
end

local function renderRating(builder, name, rating)
	builder:tag('tr')
		:tag('td')
			:css('text-align', 'center')
			:css('vertical-align', 'middle')
			:wikitext(name)
		:done()
		:tag('td')
			:css('text-align', 'center')
			:css('font-size', '110%')
			:wikitext(rating)
end

local function renderReviews(builder, providedReviewers, providedAggregators, activeSystems, customAggregatorKeys, customReviewerKeys, args)
	builder = builder:tag('table')
		:addClass('infobox wikitable')
		:attr('cellpadding', 0)
		:attr('cellspacing', 0)
		:css('width', '100%')
		:css('border-bottom', 'none')
		:css('margin', '0em')

	local reviewerCount = #providedReviewers + #customReviewerKeys
	local aggregatorCount = #providedAggregators + #customAggregatorKeys
	local reviewScore = data.i18n[reviewerCount == 1 and 'reviewScore' or 'reviewScores']
	local aggregateScore = data.i18n[aggregatorCount == 1 and 'aggregateScore' or 'aggregateScores']
	builder:css('font-size', '100%')
	if #activeSystems ~= 0 then
		builder:wikitext(data.i18n.multiplatformCategory)
		local na = yesno(args.na)
		local showplatforms = #activeSystems ~= 1 or yesno(args.showplatforms)
		if reviewerCount ~= 0 then
			if showplatforms then
				renderHeadingRowWithSystems(builder, reviewScore, activeSystems)
			else
				renderHeadingRow(builder, reviewScore, data.i18n.publication)
			end

			for _,v in ipairs(providedReviewers) do
				renderRatingsBySystem(builder, v, data.reviewers[v].name, activeSystems, args, na)
			end
			for _,v in ipairs(customReviewerKeys) do
				renderRatingsBySystem(builder, v, args[v], activeSystems, args, na)
			end
		end
		if aggregatorCount ~= 0 then
			if reviewerCount ~= 0 then
				renderMainHeading(builder, #activeSystems+1, aggregateScore)
			elseif showplatforms then
				renderHeadingRowWithSystems(builder, aggregateScore, activeSystems)
			else
				renderHeadingRow(builder, aggregateScore, data.i18n.aggregator)
			end

			for _,v in ipairs(providedAggregators) do
				renderRatingsBySystem(builder, v, data.aggregators[v].name, activeSystems, args, na)
			end
			for _,v in ipairs(customAggregatorKeys) do
				renderRatingsBySystem(builder, v, args[v], activeSystems, args, na)
			end
		end
	else
		builder:wikitext(data.i18n.singleplatformCategory)
		builder:css('font-size', '100%')
		if aggregatorCount ~= 0 then
			renderHeadingRow(builder, aggregateScore, data.i18n.aggregator)
			for _,v in ipairs(providedAggregators) do
				renderRating(builder, data.aggregators[v].name, args[v])
			end
			for _,v in ipairs(customAggregatorKeys) do
				renderRating(builder, args[v], args[v .. 'Score'])
			end
		end
		if reviewerCount ~= 0 then
			renderHeadingRow(builder, reviewScore, data.i18n.publication)
			for _,v in ipairs(providedReviewers) do
				renderRating(builder, data.reviewers[v].name, args[v])
			end
			for _,v in ipairs(customReviewerKeys) do
				renderRating(builder, args[v], args[v .. 'Score'])
			end
		end
	end
end

local function renderAwards(builder, args, awardKeys, borderTop)
	builder = builder:tag('table')
		:addClass('infobox wikitable')
		:css('width', '100%')
		:css('margin', '0em')
		:css('border-top', borderTop)
		:attr('cellpadding', 3)
		:attr('cellspacing', 0)
	
	renderMainHeading(builder, 2, data.i18n[#awardKeys == 1 and 'award' or 'awards'], borderTop)

	builder:tag('tr')
		:tag('th')
			:wikitext(data.i18n.publication)
		:done()
		:tag('th')
			:wikitext(data.i18n.award)

	for _,v in ipairs(awardKeys) do
		 builder:tag('tr')
			:tag('td')
			:css('font-weight','bold')
				:css('background-color','#f2f2f2')
				:wikitext(args[v .. 'Pub'])
			:done()
			:tag('td')
				:css('background-color','#f2f2f2')
				:wikitext(args[v])
	end
end

local function renderMainTable(providedReviewers, providedAggregators, awardKeys, activeSystems, customAggregatorKeys, customReviewerKeys, args, wikidata)
	local tbl = mw.html.create('table')
		:attr('cellpadding', 0)
		:attr('cellspacing', 0)
		:css('background', 'transparent')
		:css('padding', '0em')
		:css('margin', '0em 1em 1em 1em')
		:css('text-align', 'center')
		:css('font-size', '80%')
		:css('float', args.align or 'right')
		:css('clear', args.align or 'right')

	if #activeSystems == 0 then
		-- Width: 20% Seems better since it scales with the article size.
		tbl
			:css('width', args.width or '23em')
	end

	if args.title and args.state and (args.state == 'autocollapse'
			or args.state == 'collapsed' or args.state == 'expanded') then
		tbl
			:addClass('collapsible')
			:addClass(args.state)
	end
	renderTitleRow(tbl, args.title)

	if args.subtitle then
		tbl:tag('tr'):tag('th')
			:css('font-size', '120%')
			:wikitext(args.subtitle)
	end

	renderReviews(tbl:tag('tr'):tag('td'), providedReviewers, providedAggregators, activeSystems, customAggregatorKeys, customReviewerKeys, args)
	if #awardKeys ~= 0 then
		renderAwards(tbl:tag('tr'):tag('td'), args, awardKeys, (#customAggregatorKeys ~= 0 or #customReviewerKeys ~= 0 or #providedAggregators ~= 0 or #providedReviewers ~= 0) and 'none' or nil)
	end

	if wikidata == true then
		tbl:tag('tr'):tag('td')
			:tag('table')
			:addClass('infobox wikitable')
			:css('width', '100%')
			:css('margin', '0em')
			:css('border-top', 'none')
			:attr('cellpadding', 3)
			:attr('cellspacing', 0)
			:tag('tr'):tag('th')
			:css('background', '#d1dbdf')
			:css('font-size', '100%')
			:css('border-top', 'none')			
			:wikitext('在维基数据上编辑'.. vgwd.getUpdateLink('nosub'))
	end

	return tbl
end

local function checkForWikidata(frame, args, activeSystems, providedAggregators)
	local wikidata = false
	
	vgwd.setDateFormat(args["df"])
	vgwd.setGame(args["qid"])
	vgwd.setSystem(nil)
	vgwd.setGenerateReferences(true)
	vgwd.setShowUpdateLink(false)
	vgwd.setUpdateLinkStyle("pen")
	vgwd.setSystemFormat(args["systemFormat"])
	
	-- Loop through aggregators if we have any.
	if #providedAggregators ~= 0 then
		for _i,aggr in ipairs(providedAggregators) do
			-- Check if vgwd knows this aggregator.
			if vgwd.setReviewer(aggr) == nil then
				-- Loop through active systems
				if #activeSystems ~= 0 then
					for _j,sys in ipairs(activeSystems) do
						local combinedCode = aggr .. '_' .. sys
						if args[combinedCode] == 'wikidata' then
							vgwd.setSystem(sys)
							vgwd.setShowSystem(false)
							local vgwdScore = vgwd.printReviewScores(frame)
							if vgwdScore then
								args[combinedCode] = vgwdScore
							end
							wikidata = true							
						end
					end			
				else
					vgwd.setShowSystem(true)
		    		if args[aggr] == 'wikidata' then
						local vgwdScore = vgwd.printReviewScores(frame)
						if vgwdScore then
							args[aggr] = vgwdScore
						end
						wikidata = true
					end
				end	
			end
		end
	end

	return wikidata
end

function p._reviewbox(frame, args)
	local activeSystems = getActiveSystems(args)
	local customReviewerKeys, customAggregatorKeys, awardKeys = getArgKeyTables(args)
	local providedReviewers, providedAggregators = getProvidedReviewersAndAggregators(args, #activeSystems ~= 0)
	local wikidata = checkForWikidata(frame, args, activeSystems, providedAggregators)
	if #customAggregatorKeys ~= 0 or #customReviewerKeys ~= 0 or #providedAggregators ~= 0 or #providedReviewers ~= 0 or #awardKeys ~= 0 then
		return renderMainTable(providedReviewers, providedAggregators, awardKeys, activeSystems, customAggregatorKeys, customReviewerKeys, args, wikidata)
	elseif mw.title.getCurrentTitle().namespace == 0 then
		return data.i18n.emptyCategory
	end
end

function p.reviewbox(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	return p._reviewbox(frame, getArgs(frame, {wrappers = data.i18n.wrapper, trim = false, translate = data.argi18n}))
end

return p