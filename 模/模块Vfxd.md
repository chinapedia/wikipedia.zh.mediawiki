local func = {}

local function rfind(s, pattern, init)
    local x, y
    local len = #s
    local i = init or len
    x, y = string.find(string.reverse(s), string.reverse(pattern), len-i+1, true)
    if x then
        return len-y+1, len-x+1
    end
end

function func.fakelink(frame)
    local text = frame.args[1] or ''
    text = (string.gsub(text, '%[%[([^\n]-)%]%]', function(x)
        if islinkeatable(x) then
            local target = string.gsub(x, '^(.-)%|.-$', '%1')
            local text = string.gsub(x, '^.-%|(.-)$', '%1')

            if string.find(target, ':') == 1 then
                if text == target then
                    text = string.sub(text, 2)
                end
                return '<span style="color:#36b;cursor:pointer;">' .. text .. '</span>'
            else
                if (not mw.title.new(target):getContent()) and (not frame.args['nored']) then
                    return '<span style="color:#ba0000;cursor:pointer;">' .. text .. '</span>'
                else
                    return '<span style="color:#0645ad;cursor:pointer;">' .. text .. '</span>'
                end
            end
        else
            return '[['_.._x_.._'|' .. x .. ']]'
        end
    end))

    text = (string.gsub(text, '%[https?://[^\n]- ([^\n]-)%]', function(x)
        return '<span style="color:#36b;cursor:pointer;">' .. x .. '</span>'
    end))

    return text
end

function func.fakelink2(frame)
    local text = frame.args[1] or ''
    local badtarget = frame.args['target'] or 'Special:Logout'
    text = (string.gsub(text, '%[%[([^\n]-)%]%]', function(x)
        if islinkeatable(x) then
            local target = string.gsub(x, '^(.-)%|.-$', '%1')
            local text = string.gsub(x, '^.-%|(.-)$', '%1')

            if string.find(target, ':') == 1 then
                if text == target then
                    text = string.sub(text, 2)
                end
                return '[['_.._badtarget_.._'|<span style="color:#36b;cursor:pointer;">' .. text .. '</span>]]'
            else
                if (not mw.title.new(target):getContent()) and (not frame.args['nored']) then
                    return '[['_.._badtarget_.._'|<span style="color:#ba0000;cursor:pointer;">' .. text .. '</span>]]'
                else
                    return '[['_.._badtarget_.._'|<span style="color:#0645ad;cursor:pointer;">' .. text .. '</span>]]'
                end
            end
        else
            return '[['_.._x_.._'|' .. x .. ']]'
        end
    end))

    text = (string.gsub(text, '%[https?://[^\n]- ([^\n]-)%]', function(x)
        return '[['_.._badtarget_.._'|<span style="color:#36b;cursor:pointer;">' .. x .. '</span>]]'
    end))

    return text
end

return func