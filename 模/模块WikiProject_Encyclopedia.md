--
-- 模組功能：在 Template:WikiProject Encyclopedia 中，將「中國大百科全書/網路版/化學」分拆成「中國大百科全書」和「網路版/化學」兩部分。
--

local z = {}

local function split(str, part)
    if str then
        local position = string.find(str, "/")
        if position == nil then
            if part == 0 then
                return str
            else
                return ""
            end
        else
            if part == 0 then
                return string.sub(str, 1, position-1)
            elseif part == 1 then
                return string.sub(str, position+1, -1)
            else
                return ""
            end
        end
    else
        return ""
    end
end

-- 取得百科全書的書名
function z.get_book(frame)
    if frame.args[1] then
        return split(frame.args[1], 0)
    else
        return ""
    end
end

-- 取得百科全書的章節名
function z.get_chapter(frame)
    if frame.args[1] then
        return split(frame.args[1], 1)
    else
        return ""
    end
end

-- 根據百科全書連結和標題產生說明文字
function z.get_ref_desc(frame)
    local book_name = z.get_book(frame)
    local chapter_name = z.get_chapter(frame)
    local original_title = frame.args[2]
    local output = "本條目收錄於《[["_.._book_name_.._"|" .. book_name .. "]]》"

    if book_name == nil or book_name == "" then
        return ""
    end

    if chapter_name and chapter_name ~= "" then
        output = output .. "的「" .. chapter_name .. "」節"
    end

    if original_title and original_title ~= "" then
        output = output .. "，詞條名為" .. original_title
    end

    return output
end

-- 根據百科全書連結產生分類。
function z.get_ref_cat(frame)
    local book_name = z.get_book(frame)

    if book_name == nil or book_name == "" then
        return ""
    end

    local cat = {
        "收錄於《" .. book_name .. "》的條目",
        "收錄於" .. book_name .. "的條目",
        "收录于《" .. book_name .. "》的条目",
        "收录于" .. book_name .. "的条目"
    }
    local flag = nil
    for i=1, #cat do
        flag = cat[i]
        local title = mw.title.new( flag, "Category" )
        if title and title.exists then
            break
        end
    end

    return flag
end

return z