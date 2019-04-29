-- 载入getArgs模块
local getArgs = require('Module:Arguments').getArgs

-- 导入数据
local d = mw.loadData('Module:SZM/data')
-- d.lineNames 线路名称解析列表
-- d.lineColors 线路色彩列表

-- 声明模块本体
local p = {}

-- {{深圳地铁}}模板原数据
p.displayLineNameFormat = {
    l = [=[[[深圳地铁%d号线|%d号线]]]=], --仅链接
    lc = [=[[[深圳地铁%d号线|<span style="color:#%s;">%d号线</span>]]]=], --带色彩链接
    tc = [=[<span style="color:#%s;">%d号线</span>]=], --带色彩文本
    c = [=[<span style="color:#%s;">■ </span>[[深圳地铁%d号线|%d号线]]]=], --带色块链接
    t = [=[%d号线]=], --纯文本
    i = [=[[[深圳地铁%d号线|<span title="可-{zh-hans:换乘; zh-hant:轉乘}-%d号线" style="color:#%s">■</span>]]]=], --换乘站
}

p.platformSignFormat = "[[File:SZM_Line%line_P%platform.svg|%size]]"

-- 错误信息
local errorlist = {
    unknowlinename = "未知线路名称\"%s\"",
    noargument = "\"%s\"无参数!",
    nocolor = "线路序号\"%d\"不存在色彩",
}

local function makeInvokeFunction(funcName)
    -- makes a function that can be returned from #invoke, using
    -- [[Module:Arguments|Module:Arguments]].
    return function (frame)
        local args = getArgs(frame, {parentOnly = true})
        return p[funcName](args)
    end
end

p.szmTemplate = makeInvokeFunction('_szmTemplate')
p.interchange = makeInvokeFunction('_interchange')
p.getcolor =  makeInvokeFunction('_getcolor')
p.parsing =  makeInvokeFunction('_parsing')
p.getPlatformSign =  makeInvokeFunction('_getPlatformSign')

-- 建立线路名称反查解析表
do
    p.revNamesTbl = {}
    for i, t in pairs(d.lineNames) do
        for _, k in pairs(t) do
            p.revNamesTbl[k] = i
        end
    end
end

-- 本地函数：解析线路名称，参数=线路名字，返回=线路编号
local function fromLineNameToLineNumber(lineName)
    if p.revNamesTbl[lineName] then
        return tonumber(p.revNamesTbl[lineName])
    else
        error(errorlist.unknowlinename:gsub("%%s", lineName or "NULL"))
        return
    end
end

-- 本地函数：解析线路色彩，参数=线路编号，返回=线路色彩RGB代码值
local function getLineColor(lineNumber)
    if d.lineColors[lineNumber] then
        return d.lineColors[lineNumber]
    else
        error(errorlist.nocolor:gsub("%%d", lineNumber or "NULL"))
        return
    end
end

-- 本地函数：获取站台图标，参数=线路编号，站台编号，图片大小（可选，默认20px）
local function getPlatformSign(line, platform, size)
    if not line or not platform then return end
    local img = p.platformSignFormat:gsub("%%line", line)
    img = img:gsub("%%platform", platform)
    img = img:gsub("%%size", size or "20px")
    return img
end

-- 替换原版{{深圳地铁}}模板函数，参数1=线路名称，参数2=控制符，返回=输出结果
function p._szmTemplate(args)
    local lineName = args[1]
    local control = args[2]
    local lineNumber = fromLineNameToLineNumber(lineName)
    local color = getLineColor(lineNumber)
    if not control then control = "l" end
    local result = p.displayLineNameFormat[control]:gsub("%%d", lineNumber):gsub("%%s", color)
    return result
end

-- 替换原版{{深圳地铁色彩}}模板函数，参数1=线路名称，参数2=控制输出'#'前缀，返回=色彩代码
function p._getcolor(args)
    local lineName = args[1]
    local noBash = args[2]
    local lineNumber = fromLineNameToLineNumber(lineName)
    if noBash and string.lower(noBash) == "no" then
        return getLineColor(lineNumber)
    else
        return mw.text.nowiki('#' .. getLineColor(lineNumber))
    end
end

-- 替换原版{{深圳地鐵名稱解析}}模板函数，参数1=线路名称，返回=线路数字
function p._parsing(args)
    local lineName = args[1]
    if not lineName then
        error(errorlist.noargument:gsub("%%s", mw.getCurrentFrame():getParent():getTitle() or ""))
        return
    end
    return fromLineNameToLineNumber(lineName)
end

-- 替换原版{{深圳地鐵路線換乘}}模板函数，参数1，参数2，参数3... =线路名称，返回=换乘1，换乘2，换乘3...且已经按顺序排序
function p._interchange(args)
    -- 第一个参数都无则返回错误
    if not args[1] then
        error(errorlist.noargument:gsub("%%s", mw.getCurrentFrame():getParent():getTitle() or ""))
        return
    end

    -- 把参数表里面的线路名字全部转为数字
    local lines = {}
    for i, line in ipairs(args) do
        if line and line ~= "" then
            local lineNumber = fromLineNameToLineNumber(line)
            if lineNumber then
                table.insert(lines, lineNumber)
            end
        end
    end

    -- 排序
    table.sort(lines)

    -- 输出结果
    local result = ""
    for i, lineNumber in ipairs(lines) do
        local color = getLineColor(lineNumber)
        local text = p.displayLineNameFormat.i:gsub("%%d", lineNumber):gsub("%%s", color)
        result = result .. text
    end
    return result
end

-- {{深圳地铁站台}}模板函数: line=线路数字, platform=站台编号, size=图片尺寸(留空默认20xp); 返回=站台图片
function p._getPlatformSign(args)
    return getPlatformSign(args.line, args.platform, args.size)
end

return p