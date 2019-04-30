--[=[

  已知以下幾種情況會導致錯誤，但是我們可以善意地認為沒有人會故意這樣做：

  1. 只有一個標題，後面沒有文字（或者是緊接著下一個標題）
  2. <nowiki>
     ...
     == aaa ==
     ...
     </nowiki>
  3. 放一個大小寫混用的HTML標籤  // Special:Redirect/revision/43073725 真的有人故意这么做
  4. 在標題中使用<ref>
  5. 標題沒有文字
  6. 标题中使用了[[User:Example|{{^}}]]这样的变态链接

  還有
  1. 没有人连续使用标题
  2. 大家都会空行
 
 當然Flow也不適用
]=]--

local z = {}
local HTMLTAGS = {'b', '[Bb][Ii][Gg]', 'blockquote', 'br', 'caption', 'center', 'code', 'del', 'div', 'em', 'font', 'i', 'kbd', 'mark', 'p', 'q', 'rp', 'rt', 'ruby', 's', 'small', 'span', 'strong', 'sub', 'sup', 'time', 'tt',
'B', 'BLOCKQUOTE', 'BR', 'CAPTION', 'CENTER', 'CODE', 'DEL', 'DIV', 'EM', 'FONT', 'I', 'KBD', 'MARK', 'P', 'Q', 'RP', 'RT', 'RUBY', 'S', 'SMALL', 'SPAN', 'STRONG', 'SUB', 'SUP', 'TIME', 'TT'
}

function getCandidates( frame )
    local page = mw.title.new( frame.args.title ):getContent() or ''
    local matches = {}
    local black = {}
    if frame.args.black then
        for b in mw.text.gsplit( frame.args.black, '|', true ) do
            black[b] = true
        end
    end
    for m in mw.ustring.gmatch( page, frame.args.pattern ) do
        if not black[m] then
            table.insert( matches, m )
        end
    end
    return matches
end

function z.count( frame )
    return #getCandidates( frame )
end

local function encodetitle( frame, text )
	-- 该函数将标题转化为锚点文字
	frame=frame or mw.getCurrentFrame()
    local r = text

    -- 提取<nowiki>和<pre>內容
    local nowikis = {}
    local extract = function (s)
        nowikis[#nowikis+1] = s
        return '__NOWIKI_UNIT_' .. #nowikis
    end
    r = string.gsub(r, '<[Nn][Oo][Ww][Ii][Kk][Ii]>(.-)</[Nn][Oo][Ww][Ii][Kk][Ii]>', extract)
    r = string.gsub(r, '<pre>(.-)</pre>', extract)

    -- 解析wikitext
    r = frame:preprocess(r)

    -- 粗體與斜體
    r = string.gsub(r, "'''''(.-)'''''", '%1')
    r = string.gsub(r, "'''(.-)'''", '%1')
    r = string.gsub(r, "''(.-)''", '%1')

    -- 去除圖片
    r = string.gsub(r, '%[%[[Ff]ile:(.-)%]%]', '')
    r = string.gsub(r, '%[%[[Ii]mage:(.-)%]%]', '')
    r = string.gsub(r, '%[%[文件:(.-)%]%]', '')
    r = string.gsub(r, '%[%[檔案:(.-)%]%]', '')

    -- 去除分类
    r = string.gsub(r, '%[%[[Cc]ategory:(.-)%]%]', '')
    r = string.gsub(r, '%[%[分类:(.-)%]%]', '')

    -- 去除ref和math等標籤
    r = mw.text.killMarkers(r)

    -- 展開連結
    r = string.gsub(r, '%[%[[^%|^%]]-%|(.-)%]%]', '%1')
    r = string.gsub(r, '%[%[:?(.-)%]%]', '%1')
    r = string.gsub(r, '%[[^%|^%]]-% (.-)%]', '%1')

    -- 去除HTML標籤
    for i, t in ipairs(HTMLTAGS) do
        r = string.gsub(r, '</?' .. t.. '.->', '')
    end

    -- 將pre與nowiki內容放回文字之中
    for i, t in ipairs(nowikis) do
        local u = mw.text.encode(t)
        r = string.gsub(r, '__NOWIKI_UNIT_' .. i, u)
    end

    -- 更換特殊字元
    r = mw.text.encode(r, '%[%]%|{}')

    return mw.text.trim(r)
end
function z.encodetitle(text) 
	return encodetitle(mw.getCurrentFrame(),text)
end --便于其他模块借用此函数
function z.list( frame )
    local list = getCandidates( frame )
    local linkprefix = mw.text.trim(frame.args.linkprefix)
    local anchorno = {}
    for i = 1, #list do
        if linkprefix then
            local title = encodetitle(frame, mw.text.trim(list[i]))

            -- 記錄標題文字，如果重複，那麼在後面附加「_2」、「_3」……
            anchorno[title] = (anchorno[title] or 0) + 1
            local postfix = (anchorno[title] > 1 and '_' .. anchorno[title]) or ''

            list[i] = '[[:'_.._linkprefix_.._string.gsub(title,_'&',_'&')_.._postfix_.._'|' .. title .. ']]'
        else
            list[i] = '[[:'_.._list[i]_.._'|:' .. list[i] .. ']]'
        end
    end
    if #list > 0 then
        return table.concat( list, '－' or frame.args.concat )
    else
        return '暂无'
    end
end

function z.listtalk( frame )
	-- 假设!
    frame.args.pattern = '\n==([^=][^\n]-)==\n'
    if frame.args[1] and not frame.args.title then
        frame.args.title = frame.args[1]
    end
    frame.args.linkprefix = mw.text.trim(frame.args.title or '') .. '#'
    return z.list(frame)
end

return z