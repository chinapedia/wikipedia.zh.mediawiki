-- This module implements {{error}}.

local p = {}

local function _error(args)
    local message = args.message or args[1] or error('没有指定的-{zh-cn:信息; zh-tw:資訊}-', 2)
    message = tostring(message)
    local tag = mw.ustring.lower(tostring(args.tag))

    -- Work out what html tag we should use.
    if not (tag == 'p' or tag == 'span' or tag == 'div') then
        tag = 'strong'
    end

    -- Generate the html.
    local root = mw.html.create(tag)
    root
        :addClass('error')
        :wikitext(message)

    return tostring(root)
end

function p.error(frame)
    local args
    if frame == mw.getCurrentFrame() then
        -- We're being called via #invoke. The args are passed through to the module
        -- from the template page, so use the args that were passed into the template.
        args = frame.args
    else
        -- We're being called from another module or from the debug console, so assume
        -- the args are passed in directly.
        args = frame
    end
    -- if the message parameter is present but blank, change it to nil so that Lua will
    -- consider it false.
    if args.message == "" then
        args.message = nil
    end
    return _error(args)
end

return p