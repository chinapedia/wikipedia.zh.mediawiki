-- <nowiki>

-- {{PD-self}}
-- I, the copyright holder of this work, hereby release it into the public domain. This applies worldwide.
-- If this is not legally possible:
-- I grant any entity the right to use this work for any purpose, without any conditions, unless such conditions are required by law.
-- 2013 Hat600


-- 前期的历史见[[mw:Module:HardTimeline|mw:Module:HardTimeline]]
-- 简直就是丧心病狂！
-- 传说中为了解决easytimeline的各种奇葩问题而出现的装置
-- 硬生生的采用div/css编写
-- 基本输入：表格开始时间、结束时间、行数、行宽、行间距、CSS
-- 项目输入：项目开始时间、结束时间、所处行数、文字、颜色
-- todo: 使用HTMLBuilder重写、外框、行标记、时间标记

local p = {}
local lang = mw.language.new('zh')

function p.cvrtime( tstart, tend, itstart, itend )
    s1 = lang:formatDate( 'U', tstart )
    s2 = lang:formatDate( 'U', tend )
    s3 = lang:formatDate( 'U', itstart )
    s4 = lang:formatDate( 'U', itend )
    return (s4 - s3)/(s2 - s1)*100
end

function p.additem( tstart, tend, lineheight, whitespace, st, ed, line, tx, css )
    if ed == 'point' then
        lft = p.cvrtime( tstart, tend, tstart, st )
        top = line * (lineheight + whitespace)
        return '<div style="border-left: 1px solid ' .. css .. '; position: absolute; text-align: left; left: ' .. lft .. '%; top: ' .. top .. 'px; height: ' .. lineheight .. 'px; white-space:nowrap;">' .. tx .. '</div>'
    else
        wid = p.cvrtime( tstart, tend, st, ed )
        lft = p.cvrtime( tstart, tend, tstart, st )
        top = line * (lineheight + whitespace)
        return '<div style="background:' .. css .. '; position: absolute; text-align: center; left: ' .. lft .. '%; top: ' .. top .. 'px;  width: ' .. wid .. '%; height: ' .. lineheight .. 'px; white-space:nowrap;">' .. tx .. '</div>'
    end
end

function p.htl(frame)
    s = ''
    i = 1
    j = 6
    
    while i < 6 do
        if frame.args[i] == nil then
            return 0
        end
        i = i + 1
    end
    css = frame.args[6]
    whitespace = frame.args[5]
    lineheight = frame.args[4]
    lines = frame.args[3]
    tend = frame.args[2]
    tstart = frame.args[1]
    height = whitespace * 4 + lineheight * lines + whitespace * lines + 20
    s = s .. '<div style="position: relative; ' .. css .. '; height: ' .. height .. 'px; width: 80%; overflow: hidden;">'
    i = 6
    while 4 > 3 do
        while i < j + 5 do
            if frame.args[i] == nil then
                s = s .. '</div>'
                return s
            end
            i = i + 1
        end
        st = frame.args[j + 1]
        ed = frame.args[j + 2]
        line = frame.args[j + 3]
        tx = frame.args[j + 4]
        css = frame.args[j + 5]
        s = s .. p.additem ( tstart, tend, lineheight, whitespace, st, ed, line, tx, css )
        j = j + 5
        i = i + 1
    end
end

return p
-- </nowiki>