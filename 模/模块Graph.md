-- ATTENTION:  Please edit this code at https://de.wikipedia.org/wiki/Modul:Graph
--             This way all wiki languages can stay in sync. Thank you!
--
-- Version History (_PLEASE UPDATE when modifying anything_):
--   2018-10-13 Fix browser color-inversion issues via #54595d per [[mw:Template:Graph:PageViews|mw:Template:Graph:PageViews]]
--   2018-08-26 Use user-defined order for stacked charts
--   2018-02-11 Force usage of explicitely provided x minimum and/or maximum values, rotation of x labels
--   2017-08-09 Add showSymbols param to show symbols on line charts
--   2017-08-08 Added showSymbols param to show symbols on line charts
--   2016-05-16 Added encodeTitleForPath() to help all path-based APIs graphs like pageviews
--   2016-03-20 Allow omitted data for charts, labels for line charts with string (ordinal) scale at point location
--   2016-01-28 For maps, always use wikiraw:// protocol. https:// will be disabled soon.

local p = {}

local function numericArray(csv)
	if not csv then return end

	local list = mw.text.split(csv, "%s*,%s*")
	local result = {}
	local isInteger = true
	for i = 1, #list do
		if list[i] == "" then
			result[i] = nil
		else
			result[i] = tonumber(list[i])
			if not result[i] then return end
			if isInteger then
				local int, frac = math.modf(result[i])
				isInteger = frac == 0.0
			end
		end
	end
	return result, isInteger
end

local function stringArray(csv)
	if not csv then return end

	return mw.text.split(csv, "%s*,%s*")
end

local function isTable(t) return type(t) == "table" end

local function copy(x)
	if type(x) == "table" then
		local result = {}
		for key, value in pairs(x) do result[key] = copy(value) end
		return result
	else
		return x
	end
end

local function deserializeXData(serializedX, xType, xMin, xMax)
	local x

	if not xType or xType == "integer" or xType == "number" then
		local isInteger
		x, isInteger = numericArray(serializedX)
		if x then
			xMin = tonumber(xMin)
			xMax = tonumber(xMax)
			if not xType then
				if isInteger then xType = "integer" else xType = "number" end
			end
		else
			if xType then error("Numbers expected for parameter 'x'") end
		end
	end
	if not x then
		x = stringArray(serializedX)
		if not xType then xType = "string" end
	end

	return x, xType, xMin, xMax
end

local function deserializeYData(serializedYs, yType, yMin, yMax)
	local y = {}
	local areAllInteger = true

	for yNum, value in pairs(serializedYs) do
		local yValues
		if not yType or yType == "integer" or yType == "number" then
			local isInteger
			yValues, isInteger = numericArray(value)
			if yValues then
				areAllInteger = areAllInteger and isInteger
			else
				if yType then
					error("Numbers expected for parameter '" .. name .. "'")
				else
					return deserializeYData(serializedYs, "string", yMin, yMax)
				end
			end
		end
		if not yValues then yValues = stringArray(value) end

		y[yNum] = yValues
	end
	if not yType then
		if areAllInteger then yType = "integer" else yType = "number" end
	end
	if yType == "integer" or yType == "number" then
		yMin = tonumber(yMin)
		yMax = tonumber(yMax)
	end

	return y, yType, yMin, yMax
end

local function convertXYToManySeries(x, y, xType, yType, seriesTitles)
	local data =
	{
		name = "chart",
		format =
		{
			type = "json",
			parse = { x = xType, y = yType }
		},
		values = {}
	}
	for i = 1, #y do
		local yLen = table.maxn(y[i])
		for j = 1, #x do
			if j <= yLen and y[i][j] then table.insert(data.values, { series = seriesTitles[i], x = x[j], y = y[i][j] }) end
		end
	end
	return data
end

local function convertXYToSingleSeries(x, y, xType, yType, yNames)
	local data = { name = "chart", format = { type = "json", parse = { x = xType } }, values = {} }

	for j = 1, #y do data.format.parse[yNames[j]] = yType end

	for i = 1, #x do
		local item = { x = x[i] }
		for j = 1, #y do item[yNames[j]] = y[j][i] end

		table.insert(data.values, item)
	end
	return data
end

local function getXScale(chartType, stacked, xMin, xMax, xType)
	if chartType == "pie" then return end

	local xscale =
	{
		name = "x",
		type = "linear",
		range = "width",
		zero = false, -- do not include zero value
		nice = true,  -- force round numbers for y scale
		domain = { data = "chart", field = "x" }
	}
	if xMin then xscale.domainMin = xMin end
	if xMax then xscale.domainMax = xMax end
	if xMin or xMax then
		xscale.clamp = true
		xscale.nice = false
	end
	if chartType == "rect" then
		xscale.type = "ordinal"
		if not stacked then xscale.padding = 0.2 end -- pad each bar group
	else
		if xType == "date" then xscale.type = "time"
		elseif xType == "string" then
			xscale.type = "ordinal"
			xscale.points = true
		end
	end

	return xscale
end

local function getYScale(chartType, stacked, yMin, yMax, yType)
	if chartType == "pie" then return end

	local yscale =
	{
		name = "y",
		type = "linear",
		range = "height",
		-- area charts have the lower boundary of their filling at y=0 (see marks.properties.enter.y2), therefore these need to start at zero
		zero = chartType ~= "line",
		nice = true
	}
	if yMin then yscale.domainMin = yMin end
	if yMax then yscale.domainMax = yMax end
	if yMin or yMax then yscale.clamp = true end
	if yType == "date" then yscale.type = "time"
	elseif yType == "string" then yscale.type = "ordinal" end
	if stacked then
		yscale.domain = { data = "stats", field = "sum_y" }
	else
		yscale.domain = { data = "chart", field = "y" }
	end

	return yscale
end

local function getColorScale(colors, chartType, xCount, yCount)
	if not colors then
		if (chartType == "pie" and xCount > 10) or yCount > 10 then colors = "category20" else colors = "category10" end
	end

	local colorScale =
	{
		name = "color",
		type = "ordinal",
		range = colors,
		domain = { data = "chart", field = "series" }
	}
	if chartType == "pie" then colorScale.domain.field = "x" end
	return colorScale
end

local function getAlphaColorScale(colors, y)
	local alphaScale
	-- if there is at least one color in the format "#aarrggbb", create a transparency (alpha) scale
	if isTable(colors) then
		local alphas = {}
		local hasAlpha = false
		for i = 1, #colors do
			local a, rgb = string.match(colors[i], "#(%x%x)(%x%x%x%x%x%x)")
			if a then
				hasAlpha = true
				alphas[i] = tostring(tonumber(a, 16) / 255.0)
				colors[i] = "#" .. rgb
			else
				alphas[i] = "1"
			end
		end
		for i = #colors + 1, #y do alphas[i] = "1" end
		if hasAlpha then alphaScale = { name = "transparency", type = "ordinal", range = alphas } end
	end
	return alphaScale
end

local function getValueScale(fieldName, min, max, type)
	local valueScale =
	{
		name = fieldName,
		type = type or "linear",
		domain = { data = "chart", field = fieldName },
		range = { min, max }
	}
	return valueScale
end

local function addInteractionToChartVisualisation(plotMarks, colorField, dataField)
	-- initial setup
	if not plotMarks.properties.enter then plotMarks.properties.enter = {} end
	plotMarks.properties.enter[colorField] = { scale = "color", field = dataField }

	-- action when cursor is over plot mark: highlight
	if not plotMarks.properties.hover then plotMarks.properties.hover = {} end
	plotMarks.properties.hover[colorField] = { value = "red" }

	-- action when cursor leaves plot mark: reset to initial setup
	if not plotMarks.properties.update then plotMarks.properties.update = {} end
	plotMarks.properties.update[colorField] = { scale = "color", field = dataField }
end

local function getPieChartVisualisation(yCount, innerRadius, outerRadius, linewidth, radiusScale)
	local chartvis =
	{
		type = "arc",
		from = { data = "chart", transform = { { field = "y", type = "pie" } } },

		properties =
		{
			enter = {
				innerRadius = { value = innerRadius },
				outerRadius = { },
				startAngle = { field = "layout_start" },
				endAngle = { field = "layout_end" },
				stroke = { value = "white" },
				strokeWidth = { value = linewidth or 1 }
			}
		}
	}

	if radiusScale then
		chartvis.properties.enter.outerRadius.scale = radiusScale.name
		chartvis.properties.enter.outerRadius.field = radiusScale.domain.field
	else
		chartvis.properties.enter.outerRadius.value = outerRadius
	end

	addInteractionToChartVisualisation(chartvis, "fill", "x")

	return chartvis
end

local function getChartVisualisation(chartType, stacked, colorField, yCount, innerRadius, outerRadius, linewidth, alphaScale, radiusScale, interpolate)
	if chartType == "pie" then return getPieChartVisualisation(yCount, innerRadius, outerRadius, linewidth, radiusScale) end

	local chartvis =
	{
		type = chartType,
		properties =
		{
			-- chart creation event handler
			enter =
			{
				x = { scale = "x", field = "x" },
				y = { scale = "y", field = "y" }
			}
		}
	}
	addInteractionToChartVisualisation(chartvis, colorField, "series")
	if colorField == "stroke" then
		chartvis.properties.enter.strokeWidth = { value = linewidth or 2.5 }
	end

	if interpolate then chartvis.properties.enter.interpolate = { value = interpolate } end

	if alphaScale then chartvis.properties.update[colorField .. "Opacity"] = { scale = "transparency" } end
	-- for bars and area charts set the lower bound of their areas
	if chartType == "rect" or chartType == "area" then
		if stacked then
			-- for stacked charts this lower bound is the end of the last stacking element
			chartvis.properties.enter.y2 = { scale = "y", field = "layout_end" }
		else
			--[[
			for non-stacking charts the lower bound is y=0
			TODO: "yscale.zero" is currently set to "true" for this case, but "false" for all other cases.
			For the similar behavior "y2" should actually be set to where y axis crosses the x axis,
			if there are only positive or negative values in the data ]]
			chartvis.properties.enter.y2 = { scale = "y", value = 0 }
		end
	end
	-- for bar charts ...
	if chartType == "rect" then
		-- set 1 pixel width between the bars
		chartvis.properties.enter.width = { scale = "x", band = true, offset = -1 }
		-- for multiple series the bar marking needs to use the "inner" series scale, whereas the "outer" x scale is used by the grouping
		if not stacked and yCount > 1 then
			chartvis.properties.enter.x.scale = "series"
			chartvis.properties.enter.x.field = "series"
			chartvis.properties.enter.width.scale = "series"
		end
	end
	-- stacked charts have their own (stacked) y values
	if stacked then chartvis.properties.enter.y.field = "layout_start" end

	-- if there are multiple series group these together
	if yCount == 1 then
		chartvis.from = { data = "chart" }
	else
		-- if there are multiple series, connect colors to series
		chartvis.properties.update[colorField].field = "series"
		if alphaScale then chartvis.properties.update[colorField .. "Opacity"].field = "series" end
		-- apply a grouping (facetting) transformation
		chartvis =
		{
			type = "group",
			marks = { chartvis },
			from =
			{
				data = "chart",
				transform =
				{
					{
						type = "facet",
						groupby = { "series" }
					}
				}
			}
		}
		-- for stacked charts apply a stacking transformation
		if stacked then
			table.insert(chartvis.from.transform, 1, { type = "stack", groupby = { "x" }, sortby = { "-_id" }, field = "y" } )
		else
			-- for bar charts the series are side-by-side grouped by x
			if chartType == "rect" then
				-- for bar charts with multiple series: each serie is grouped by the x value, therefore the series need their own scale within each x group
				local groupScale =
				{
					name = "series",
					type = "ordinal",
					range = "width",
					domain = { field = "series" }
				}

				chartvis.from.transform[1].groupby = "x"
				chartvis.scales = { groupScale }
				chartvis.properties = { enter = { x = { field = "key", scale = "x" }, width = { scale = "x", band = true } } }
			end
		end
	end

	return chartvis
end

local function getTextMarks(chartvis, chartType, outerRadius, scales, radiusScale, yType, showValues)
	local properties
	if chartType == "rect" then
		properties =
		{
			x = { scale = chartvis.properties.enter.x.scale, field = chartvis.properties.enter.x.field },
			y = { scale = chartvis.properties.enter.y.scale, field = chartvis.properties.enter.y.field, offset = -(tonumber(showValues.offset) or -4) },
			--dx = { scale = chartvis.properties.enter.x.scale, band = true, mult = 0.5 }, -- for horizontal text
			dy = { scale = chartvis.properties.enter.x.scale, band = true, mult = 0.5 }, -- for vertical text
			align = { },
			baseline = { value = "middle" },
			fill = { },
			angle = { value = -90 },
			fontSize = { value = tonumber(showValues.fontsize) or 11 }
		}
		if properties.y.offset >= 0 then
			properties.align.value = "right"
			properties.fill.value = showValues.fontcolor or "white"
		else
			properties.align.value = "left"
			properties.fill.value = showValues.fontcolor or "black"
		end
	elseif chartType == "pie" then
		properties =
		{
			x = { group = "width", mult = 0.5 },
			y = { group = "height", mult = 0.5 },
			radius = { offset = tonumber(showValues.offset) or -4 },
			theta = { field = "layout_mid" },
			fill = { value = showValues.fontcolor or "black" },
			baseline = { },
			angle = { },
			fontSize = { value = tonumber(showValues.fontsize) or math.ceil(outerRadius / 10) }
		}
		if (showValues.angle or "midangle") == "midangle" then
			properties.align = { value = "center" }
			properties.angle = { field = "layout_mid", mult = 180.0 / math.pi }

			if properties.radius.offset >= 0 then
				properties.baseline.value = "bottom"
			else
				if not showValues.fontcolor then properties.fill.value = "white" end
				properties.baseline.value = "top"
			end
		elseif tonumber(showValues.angle) then
			-- qunatize scale for aligning text left on right half-circle and right on left half-circle
			local alignScale = { name = "align", type = "quantize", domainMin = 0.0, domainMax = math.pi * 2, range = { "left", "right" } }
			table.insert(scales, alignScale)

			properties.align = { scale = alignScale.name, field = "layout_mid" }
			properties.angle = { value = tonumber(showValues.angle) }
			properties.baseline.value = "middle"
			if not tonumber(showValues.offset) then properties.radius.offset = 4 end
		end

		if radiusScale then
			properties.radius.scale = radiusScale.name
			properties.radius.field = radiusScale.domain.field
		else
			properties.radius.value = outerRadius
		end
	end

	if properties then
		if showValues.format then
			local template = "datum.y"
			if yType == "integer" or yType == "number" then template = template .. "|number:'" .. showValues.format .. "'"
			elseif yType == "date" then template = template .. "|time:" .. showValues.format .. "'"
			end
			properties.text = { template = "{{" .. template .. "}}" }
		else
			properties.text = { field = "y" }
		end

		local textmarks =
		{
			type = "text",
			properties =
			{
				enter = properties
			}
		}
		if chartvis.from then textmarks.from = copy(chartvis.from) end

		return textmarks
	end
end

local function getSymbolMarks(chartvis)
	local symbolmarks =
	{
		type = "symbol",
		properties =
		{
			enter = 
			{
				x = { scale = "x", field = "x" },
				y = { scale = "y", field = "y" },
				fill = { scale = "color", field = "series" },
				shape = "circle",
				size = { value = 49 }
			}
		}
	}
	if chartvis.from then symbolmarks.from = copy(chartvis.from) end

	return symbolmarks
end

local function getAxes(xTitle, xAxisFormat, xAxisAngle, xType, yTitle, yAxisFormat, yType, chartType)
	local xAxis, yAxis
	if chartType ~= "pie" then
		if xType == "integer" and not xAxisFormat then xAxisFormat = "d" end
		xAxis =
		{
			type = "x",
			scale = "x",
			title = xTitle,
			format = xAxisFormat
		}
		if xAxisAngle then
			local xAxisAlign
			if xAxisAngle < 0 then xAxisAlign = "right" else xAxisAlign = "left" end
			xAxis.properties =
			{
				title =
				{
					fill = { value = "#54595d" }
				},
				labels =
				{
					angle = { value = xAxisAngle },
					align = { value = xAxisAlign },
					fill = { value = "#54595d" }
				},
				ticks =
				{
					stroke = { value = "#54595d" }
				},
				axis =
				{
					stroke = { value = "#54595d" },
					strokeWidth = { value = 2 }
				}
			}
		else
			xAxis.properties =
			{
				title =
				{
					fill = { value = "#54595d" }
				},
				labels =
				{
					fill = { value = "#54595d" }
				},
				ticks =
				{
					stroke = { value = "#54595d" }
				},
				axis =
				{
					stroke = { value = "#54595d" },
					strokeWidth = { value = 2 }
				}
			}
		end
		
		if yType == "integer" and not yAxisFormat then yAxisFormat = "d" end
		yAxis =
		{
			type = "y",
			scale = "y",
			title = yTitle,
			format = yAxisFormat
		}
		yAxis.properties =
		{
			title =
			{
				fill = { value = "#54595d" }
			},
			labels =
			{
				fill = { value = "#54595d" }
			},
			ticks =
			{
				stroke = { value = "#54595d" }
			},
			axis =
			{
				stroke = { value = "#54595d" },
				strokeWidth = { value = 2 }
			},
			grid =
			{
				stroke = { value = "#54595d" }
			}
		}
	end

	return xAxis, yAxis
end

local function getLegend(legendTitle, chartType, outerRadius)
	local legend =
	{
		fill = "color",
		stroke = "color",
		title = legendTitle,
	}
	if chartType == "pie" then
		-- move legend from center position to top
		legend.properties = { legend = { y = { value = -outerRadius } } }
	end
	return legend
end

function p.chart(frame)
	-- chart width and height
	local graphwidth = tonumber(frame.args.width) or 200
	local graphheight = tonumber(frame.args.height) or 200
	-- chart type
	local chartType = frame.args.type or "line"
	-- interpolation mode for line and area charts: linear, step-before, step-after, basis, basis-open, basis-closed (type=line only), bundle (type=line only), cardinal, cardinal-open, cardinal-closed (type=line only), monotone
	local interpolate = frame.args.interpolate
	-- mark colors (if no colors are given, the default 10 color palette is used)
	local colors = stringArray(frame.args.colors)
	-- for line charts, the thickness of the line; for pie charts the gap between each slice
	local linewidth = tonumber(frame.args.linewidth)
	-- x and y axis caption
	local xTitle = frame.args.xAxisTitle
	local yTitle = frame.args.yAxisTitle
	-- x and y value types
	local xType = frame.args.xType
	local yType = frame.args.yType
	-- override x and y axis minimum and maximum
	local xMin = frame.args.xAxisMin
	local xMax = frame.args.xAxisMax
	local yMin = frame.args.yAxisMin
	local yMax = frame.args.yAxisMax
	-- override x and y axis label formatting
	local xAxisFormat = frame.args.xAxisFormat
	local yAxisFormat = frame.args.yAxisFormat
	local xAxisAngle = tonumber(frame.args.xAxisAngle)
	-- for line chart, show a symbol at each data point
	local showSymbols = frame.args.showSymbols
	-- show legend with given title
	local legendTitle = frame.args.legend
	-- show values as text
	local showValues = frame.args.showValues
	-- pie chart radiuses
	local innerRadius = tonumber(frame.args.innerRadius) or 0
	local outerRadius = math.min(graphwidth, graphheight)
	-- format JSON output
	local formatJson = frame.args.formatjson

	-- get x values
	local x
	x, xType, xMin, xMax = deserializeXData(frame.args.x, xType, xMin, xMax)

	-- get y values (series)
	local yValues = {}
	local seriesTitles = {}
	for name, value in pairs(frame.args) do
		local yNum
		if name == "y" then yNum = 1 else yNum = tonumber(string.match(name, "^y(%d+)$")) end
		if yNum then
			yValues[yNum] = value
			-- name the series: default is "y<number>". Can be overwritten using the "y<number>Title" parameters.
			seriesTitles[yNum] = frame.args["y" .. yNum .. "Title"] or name
		end
	end
	local y
	y, yType, yMin, yMax = deserializeYData(yValues, yType, yMin, yMax)

	-- create data tuples, consisting of series index, x value, y value
	local data
	if chartType == "pie" then
		-- for pie charts the second second series is merged into the first series as radius values
		data = convertXYToSingleSeries(x, y, xType, yType, { "y", "r" })
	else
		data = convertXYToManySeries(x, y, xType, yType, seriesTitles)
	end

	-- configure stacked charts
	local stacked = false
	local stats
	if string.sub(chartType, 1, 7) == "stacked" then
		chartType = string.sub(chartType, 8)
		if #y > 1 then -- ignore stacked charts if there is only one series
		stacked = true
		-- aggregate data by cumulative y values
		stats =
		{
			name = "stats", source = "chart", transform =
		{
			{
				type = "aggregate",
				groupby = { "x" },
				summarize = { y = "sum" }
			}
		}
		}
		end
	end

	-- create scales
	local scales = {}

	local xscale = getXScale(chartType, stacked, xMin, xMax, xType)
	table.insert(scales, xscale)
	local yscale = getYScale(chartType, stacked, yMin, yMax, yType)
	table.insert(scales, yscale)

	local colorScale = getColorScale(colors, chartType, #x, #y)
	table.insert(scales, colorScale)

	local alphaScale = getAlphaColorScale(colors, y)
	table.insert(scales, alphaScale)

	local radiusScale
	if chartType == "pie" and #y > 1 then
		radiusScale = getValueScale("r", 0, outerRadius)
		table.insert(scales, radiusScale)
	end

	-- decide if lines (strokes) or areas (fills) should be drawn
	local colorField
	if chartType == "line" then colorField = "stroke" else colorField = "fill" end

	-- create chart markings
	local chartvis = getChartVisualisation(chartType, stacked, colorField, #y, innerRadius, outerRadius, linewidth, alphaScale, radiusScale, interpolate)
	local marks = { chartvis }
	
	-- text marks
	if showValues then
		if type(showValues) == "string" then -- deserialize as table
			local keyValues = mw.text.split(showValues, "%s*,%s*")
			showValues = {}
			for _, kv in ipairs(keyValues) do
				local key, value = mw.ustring.match(kv, "^%s*(.-)%s*:%s*(.-)%s*$")
				if key then showValues[key] = value end
			end
		end

		local chartmarks = chartvis
		if chartmarks.marks then chartmarks = chartmarks.marks[1] end
		local textmarks = getTextMarks(chartmarks, chartType, outerRadius, scales, radiusScale, yType, showValues)
		if chartmarks ~= chartvis then
			table.insert(chartvis.marks, textmarks)
		else
			table.insert(marks, textmarks)
		end
	end

	-- symbol marks
	if chartType == "line" and showSymbols then
		local chartmarks = chartvis
		if chartmarks.marks then chartmarks = chartmarks.marks[1] end
		local symbolmarks = getSymbolMarks(chartmarks)
		if chartmarks ~= chartvis then
			table.insert(chartvis.marks, symbolmarks)
		else
			table.insert(marks, symbolmarks)
		end
	end

	-- axes
	local xAxis, yAxis = getAxes(xTitle, xAxisFormat, xAxisAngle, xType, yTitle, yAxisFormat, yType, chartType)

	-- legend
	local legend
	if legendTitle then legend = getLegend(legendTitle, chartType, outerRadius) end

	-- construct final output object
	local output =
	{
		version = 2,
		width = graphwidth,
		height = graphheight,
		data = { data, stats },
		scales = scales,
		axes = { xAxis, yAxis },
		marks = marks,
		legends = { legend }
	}

	local flags
	if formatJson then flags = mw.text.JSON_PRETTY end
	return mw.text.jsonEncode(output, flags)
end

function p.chartWrapper(frame)
	return p.chart(frame:getParent())
end

-- Given an HTML-encoded title as first argument, e.g. one produced with {{ARTICLEPAGENAME}},
-- convert it into a properly URL path-encoded string
-- This function is critical for any graph that uses path-based APIs, e.g. PageViews graph
function p.encodeTitleForPath(frame)
	return mw.uri.encode(mw.text.decode(mw.text.trim(frame.args[1])	), 'PATH')
end

return p