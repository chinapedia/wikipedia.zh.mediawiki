local p = {}

local diffString = '[[Special:Diff/%s|%s]]'

function p.row(frame)
    local status = frame.args.s
    local title = frame.args.t
    local short = p.shorttitle(title, 40)
    local size = frame.args.z
    local modified_by = frame.args.mr
    local modified_at = frame.args.md
    local old_id = frame.args.mi
    local special_user = frame.args.sr
    local special_time = frame.args.sd
    local special_id = tonumber(frame.args.si)
    local display_notes = tonumber(frame.args.n)
    local rowtemplate = "<tr style=\"background-color:%s\">%s</tr>"
    local colorthing =  p.color(status, false)
    local cols = {
    	string.format('<td>[[:%s|%s]]</td>', title, short),
    	string.format('<td data-sort-type="number" data-sort-value="%d">%.1f kB</td>', size, size / 1000)
    }
    
    local is_userspace = string.sub(frame.args.t, 1, 4) == "User"
    
    if is_userspace or display_notes then
    	cols[3] = string.format("<td>%s</td>", p.notes(frame))
    else
    	cols[3] = "<td></td>"
    end
    
    if special_id then
        cols[4] = p.printuser(special_user)
        cols[5] = string.format('<td data-sort-value="%s">%s</td>', special_id, string.format(diffString, special_id, special_time))
    else
        cols[4] = "<td>未知</td>"
        cols[5] = "<td>未知</td>"
    end
    
    cols[6] = p.printuser(modified_by)
    cols[7] = string.format('<td data-sort-value="%s">%s</td>', old_id, string.format(diffString, old_id, modified_at))
    return string.format(rowtemplate, colorthing, table.concat(cols))
end

function p.notes(frame)
    local result = ""
    local is_suspected_copyvio = tonumber(frame.args.nc)
    local is_unsourced = tonumber(frame.args.nu)
    local no_inline = tonumber(frame.args.ni)
    local is_short = tonumber(frame.args.ns)
    local is_resubmit = tonumber(frame.args.nr)
    local is_old = tonumber(frame.args.no)
    local is_rejected = tonumber(frame.args.nj)
    local submitter_is_blocked = tonumber(frame.args.nb)
    local is_userspace = string.sub(frame.args.t, 1, 4) == "User"
    
    if is_suspected_copyvio then result = result .. "<abbr title=\"提交的草稿可能侵犯版权\">疑似侵权</abbr>  " end
    if is_unsourced then result = result .. "<abbr title=\"提交的草稿完全没有任何参考文献\">无来源</abbr>  " end
    if no_inline then result = result .. "<abbr title=\"提交的草稿没有内文引用\">无脚注</abbr>  " end
    if is_short then result  = result .."<abbr title=\"提交的草稿不到一千字节\">短</abbr>  " end
    if is_resubmit then result  = result .. "<abbr title=\"提交的草稿在过去被拒绝过\">再次提交</abbr>  " end
    if is_old then result  = result .. "<abbr title=\"提交的草稿在过去四天没有编辑过\">内容陈旧</abbr>  " end
    if is_rejected then result  = result .. "<abbr title=\"提交的草稿被拒绝\">拒绝</abbr>  " end
    if submitter_is_blocked then result  = result .. "<abbr title=\"提交者已被封禁\">封禁</abbr>  " end
    if is_userspace then result  = result .. "<abbr title=\"提交的草稿位于用户或用户讨论空间\">位于用户空间</abbr>  " end
        
    return result
end

function p.color(status, dark)
    local result
    local dark_colors = {
        p = "#995",
        d = "#977",
        r = "#789",
        a = "#696"
    }
    local normal_colors = {
        p = "#eea",
        d = "#fcd",
        r = "#ade",
        a = "#afa"
    }
    if dark then
        return dark_colors[status] or "#777"
    else
        return normal_colors[status] or "#ddc"
    end
end

function p.printuser(user)
  return string.format("<td>[[User:%s|%s]] ([[User_talk:%s|t]])</td>", user, user, user)
end

function p.shorttitle(fulltitle, maxlength)
    --strip off namespace:basepage/ if it exists and anything is left
    --if not, strip off namespace
    --truncate to maxlength
    local startindex, size, namespace, basetitle, subtitle = mw.ustring.find(fulltitle, "([^:]*):([^\/]*)\/?(.*)")
    if subtitle == '' then subtitle = nil end
    local effective_title = subtitle or basetitle
    if effective_title == nil or effective_title == '' then effective_title = fulltitle end
    effective_title = string.gsub(effective_title, "^Submissions/", "")
    -- return mw.text.truncate( effective_title, maxlength ) (mw.text is not yet deployed!)
    if (mw.ustring.len(effective_title) > maxlength) then
        return mw.ustring.sub(effective_title, 1, maxlength - 3) .. "..."
    else
        return effective_title
    end
    
    
end

return p