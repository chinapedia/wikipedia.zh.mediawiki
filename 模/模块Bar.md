-- https://meta.wikimedia.org/wiki/Module:Bar
local p = {}
local inner = {}

--##########
--## Public functions
--##########
--- Render a bar chart.
-- @param frame The arguments passed to the script. See docs on renderFromLua.
function p.format( frame )
    -- extract args
    local width = frame.args['width']
    local barCSS = frame.args['barCSS']
    local zeroWidth = frame.args['zeroWidth']
    local total = frame.args['total']
    
    -- extract bar series from arguments like 'value,color,title'
    local series = {}
    for key, spec in ipairs(frame.args) do
        spec = mw.text.split(spec, ',')
        local data = {value = tonumber(spec[1] or 0), color = spec[2] or '#CCC', title = spec[3] or ''}
        if data['value'] > 0 then
            table.insert(series, data)
        end
    end
    
    return p.renderFromLua(series, total, width, barCSS, zeroWidth)
end

--- Render a bar chart from Lua.
-- @param series A table representing the bars to render, consisting of a sequence of tables like {value = 14, color = '#CCC', title = 'tooltip text'}.
-- @param total (optional) The total number of values represented by all bar series.
-- @param width (optional) The CSS width of the bar.
-- @param barCss (optional) Additional CSS to apply to the rendered bar table.
-- @param zeroWidth (optional) 
function p.renderFromLua(series, total, width, barCSS, zeroWidth)
    -- parse arguments
    width = width or '100%'
    total = tonumber(total or 0)
    zeroWidth = zeroWidth or '1px'
    
    -- calculate total
    local seriesTotal = 0
    for k,v in ipairs(series) do
       seriesTotal = seriesTotal + v['value']
    end
    if total < seriesTotal then
       total = seriesTotal
    end
    
    -- inject empty series for uncharted values
    if(seriesTotal < total) then
        table.insert(series, {value = total - seriesTotal, color = 'transparent', title = ''})
    end
    
    -- inject ratios
    for k,v in ipairs(series) do
       v['total'] = total
       v['ratio'] = inner.getRatio(v['value'], total)
       if v['ratio'] == 0 then
           v['width'] = zeroWidth
      end
    end
    
    -- render
    result = '<table style="width:' .. width .. ';' .. (barCSS or '') .. '" cellspacing="0"><tr>'
    for k, v in pairs(series) do
        result = result .. inner.renderSeries(v)
    end
    result = result .. '</tr></table>'
    return result
end

--##########
--## Private functions
--##########
--- Render an individual bar series.
-- @param series The bar series to render.
function inner.renderSeries(series)
    -- ignore empty series
    if not series.value or series.value == 0 then
        return ''
    end
    
    -- set width
    local width = series.width
    if not(width) then
        width = series.ratio .. '%'
    end
    
    -- format
    local result = mw.ustring.format('<td title="%s" style="width:%s; height:1em; padding:0; background:%s;" data-value="%s"></td>', series.title, width, series.color, series.value)
    return result
end

--- Get the percentage ratio of two numbers as a decimal value.
-- @param value The number of items in the subset.
-- @param total The total number of items in the set.
function inner.getRatio(value, total)
    if(total == 0) then
       error('the total for a series cannot be zero')
    end
    return math.floor(value / total * 10000) / 100
end

return p