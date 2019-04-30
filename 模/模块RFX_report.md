-- This module is a replacement for the RfX report bot.

local rfx = require( 'Module:Rfx' )
local colours = mw.loadData( 'Module:RFX report/colour' )

local p = {}

local function getRfxes()
    -- Get the title object for [[Wikipedia:Requests_for_adminship|Wikipedia:Requests for adminship]].
    local noError, rfa = pcall( mw.title.new, 'Wikipedia:申请成为管理人员/申请区' )
    if not noError or ( noError and not rfa ) then
        return nil
    end
    local rfaText = rfa:getContent()
    if not rfaText then
        return nil
    end
    
    -- Return a table with a list of pages transcluded from
    -- [[Wikipedia:Requests_for_adminship|Wikipedia:Requests for adminship]], minus the exceptions
    -- which are always transcluded there.
    local t = {}
    local exceptions = { 'header' }
    for rfxPage, rfxSubpage in mw.ustring.gmatch( rfaText, '{{[ _]*([wW]ikipedia:申[请請]成[为為][^/]-/([^{}]-))[ _]*}}' ) do
        local isException = false
        for _, v in ipairs( exceptions ) do
            if rfxSubpage == v then
                isException = true
                break
            end
        end
        if not isException then
            table.insert( t, rfxPage )
        end
    end
    return t
end

local function makeRow( rfxObject )
    if not ( type( rfxObject ) == 'table' and rfxObject.getTitleObject and rfxObject.getSupportUsers ) then
        return nil
    end
    local style = ''
    local styleInline = ''
    local status = rfxObject:getStatus()
    if status == '已结束' then
        style = ' style="background: #f8cdc6;" |'
        styleInline = ' background: #f8cdc6;'
    end
    local page = rfxObject:getTitleObject().prefixedText
    local user = rfxObject.user or rfxObject:getTitleObject().subpageText
    local supports = rfxObject.supports
    local opposes = rfxObject.opposes
    local neutrals = rfxObject.neutrals
    local percent = rfxObject.percent
    local colour
    if percent then
        colour = colours[ percent ]
    end
    colour = colour or ''
    local votes
    if supports and opposes and neutrals and percent then
        votes = mw.ustring.format( [==[
        
| style="text-align: right;%s" | [[%s#支持|%d]]
| style="text-align: right;%s" | [[%s#反對|%d]]
| style="text-align: right;%s" | [[%s#中立|%d]]
| style="text-align: right; background: #%s;" | %d]==],
            styleInline, page, supports,
            styleInline, page, opposes,
            styleInline, page, neutrals,
            colour, percent
        )
    else
        votes = '\n| colspan="4" style="background: #f8cdc6;" | 投票-{zh-cn:解析;zh-tw:剖析}-失败'
    end
    if status then
        status = mw.ustring.format( '\n| %s %s', style, status )
    else
        status = '\n| style="background: #f8cdc6;" | 未能-{zh-cn:获取;zh-tw:取得}-狀態'
    end 
    local endTime = rfxObject.rawEndTime
    local secondsLeft = rfxObject:getSecondsLeft()
    local timeLeft = rfxObject:getTimeLeft()
    local time
    if endTime and timeLeft then
        time = mw.ustring.format( '\n| %s %s\n| %s %s', style, endTime, style, timeLeft )
    else
        time = '\n| colspan="2" style="background: #f8cdc6;" | 未讀出終止時間'
    end
    local dupes = rfxObject:dupesExist()
    if dupes then
    	if #dupes > 0 then
        	dupes = mw.ustring.format([==['''<abbr title="%s">有</abbr>''']==],
        		table.concat(dupes, '、'))
        else
        	dupes = '无'
        end
    else
        dupes = '--'
    end
    local report = rfxObject:getReport()
    if report then
        report = mw.ustring.format( '\n|%s [%s 验票]', style, tostring( report ) )
    else
        report = '\n| style="background: #f8cdc6;" | 找不到工具'
    end
    
    -- 第 x 次
    local attempt = rfxObject.attempt
    if attempt ~= '1' then
    	user = user .. '<sup>' .. attempt .. '</sup>'
	end
    
    return mw.ustring.format(
        '\n|-\n|%s [[%s|%s]]%s%s%s %s',
        style, page, user, votes, status, time, report
    )
end

local function makeHeading( rfxType )
    local rfxCaps
    if rfxType == 'rfa' then
        rfxCaps = '管理员'
    elseif rfxType == 'rfb' then
        rfxCaps = '行政员'
    elseif rfxType == 'rfcu' then
        rfxCaps = '用户查核员'
    elseif rfxType == 'rfo' then
        rfxCaps = '监督员'
    else
        return nil
    end
    local lang = mw.getContentLanguage()
    return mw.ustring.format(
        '\n|-\n! %s候選人 !! 支持 !! 反對 !! 中立 !! 支持率 (%%) !! 狀態 !! 完結時間 !! 剩餘時間 !! 驗票',
        rfxCaps
    )
end

local function makeReportRows()
    local rfxes = getRfxes()
    if not rfxes then
        return nil
    end
    -- Get RfX objects and separate RfAs, RfBs, RfCUs and RfOs.
    local rfas, rfbs, rfcus, rfos = {}, {}, {}, {}
    for i, rfxPage in ipairs( rfxes ) do
        local rfxObject = rfx.new( rfxPage )
        if rfxObject then
            if rfxObject.type == 'rfa' then
                table.insert( rfas, rfxObject )
            elseif rfxObject.type == 'rfb' then
                table.insert( rfbs, rfxObject )
            elseif rfxObject.type == 'rfcu' then
            	table.insert( rfcus, rfxObject )
            elseif rfxObject.type == 'rfo' then
            	table.insert( rfos, rfxObject )
            end
        end
    end
    local ret = {}
    if #rfas > 0 then
        table.insert( ret, makeHeading( 'rfa' ) )
        for i, rfaObject in ipairs( rfas ) do
            table.insert( ret, makeRow( rfaObject ) )
        end
    end
    if #rfbs > 0 then
        table.insert( ret, makeHeading( 'rfb' ) )
        for i, rfbObject in ipairs( rfbs ) do
            table.insert( ret, makeRow( rfbObject ) )
        end
    end
    if #rfcus > 0 then
        table.insert( ret, makeHeading( 'rfcu' ) )
        for i, rfcuObject in ipairs( rfcus ) do
            table.insert( ret, makeRow( rfcuObject ) )
        end
    end
    if #rfos > 0 then
        table.insert( ret, makeHeading( 'rfo' ) )
        for i, rfoObject in ipairs( rfos ) do
            table.insert( ret, makeRow( rfoObject ) )
        end
    end
    return table.concat( ret )
end

local function makeReport( args )
    local purgeLink = mw.title.getCurrentTitle():fullUrl( 'action=purge' )
    local header = mw.ustring.format(
        '\n|-\n! colspan="9" style="text-align: center;" | [[Wikipedia:申请成为管理人员|申请成为管理人员]]<span class="plainlinks" style="float: right;"><small>[%s 刷新]</small></span>',
        purgeLink
    )
    local rows = makeReportRows() or ''
    if rows == '' then
        rows = '\n|-\n| colspan="10" | 当前没有提名。请参阅[[Wikipedia:管理人員任免記錄|最近的管理人员任免记录]]。'
    end
    local style = args.style
    if not style then
        local float = args.float or args.align or 'right'
        local clear = args.clear or 'left'
        style = mw.ustring.format(
            'style="white-space:wrap; clear: %s; margin-top: 0em; margin-bottom: .5em; float: %s; padding: .5em 0em 0em 1.4em; background: #ffffff; border-collapse: collapse; border-spacing: 0;"',
            clear, float
        )
    end
    return mw.ustring.format( '\n{| class="wikitable" %s%s%s\n|-\n|}', style, header, rows )
end

local function countVotes( args )
	local title = args.title or mw.title.getCurrentTitle().prefixedText
	local split = args.split or '/'
	local rfxObject = rfx.new(title)
	if not rfxObject then
		return '<span class="error">投票-{zh-cn:解析;zh-tw:剖析}-失败[[Category:投票計算失效的頁面|Category:投票計算失效的頁面]]</span>'
	end
	local s, o, n = rfxObject.supports, rfxObject.opposes, rfxObject.neutrals
	if s and o and n then
		return string.format('[[%s#支持|%d]]%s[[%s#反對|%d]]%s[[%s#中立|%d]]',
			title, s, split, title, o, split, title, n)
	else
		return '<span class="error">投票-{zh-cn:解析;zh-tw:剖析}-失败[[Category:投票計算失效的頁面|Category:投票計算失效的頁面]]</span>'
	end
end

function p.count( frame )
    -- Process the arguments.
    local args
    if frame == mw.getCurrentFrame() then
        args = frame:getParent().args
        for k, v in pairs( frame.args ) do
            args = frame.args
            break
        end
    else
        args = frame
    end
    return countVotes( args )
end

function p.main( frame )
    -- Process the arguments.
    local args
    if frame == mw.getCurrentFrame() then
        args = frame:getParent().args
        for k, v in pairs( frame.args ) do
            args = frame.args
            break
        end
    else
        args = frame
    end
    return makeReport( args )
end

return p