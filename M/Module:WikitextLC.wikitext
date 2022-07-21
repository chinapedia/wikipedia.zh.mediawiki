local p = {}

--- Construct an inline conversion from a table input.
-- @param content table of the form
--        { ["zh-cn"]='foobar', ["zh-tw"]='firecat', ["zh-hk"]='' }
-- @returns string
--       "-{zh-cn:foobar;zh-tw:firecat;zh-hk:<span></span>}-"
--
-- @fixme allow for generating output without "-{" "}-", so that
--        it can be used with the last three wrappers.
function p.selective( content )
    local text = '-{'
    for variant, value in pairs( content ) do
        if value == '' then
            value = '<span></span>'
        end
        text = text .. variant .. ':' .. value .. ';'
    end
    text = text .. '}-'
    return text
end

--- Write some text with a limited set of variants to convert to
--
-- @param content text to be written
-- @param variant a variant (string), or a list of variants
--        (semicolon-deliminated string, or table of strings)
-- @param[opt] force convert even under "zh" (no conversion) locale
function p.converted( content, variant, force )
    if type( variant ) == 'table' then
        variant = table.concat( variant, ';' )
    end
    return '-{' .. ( force and '' or 'zh;' ) .. variant .. '|' .. content .. '}-'
end

--- Wraps some "raw text" to not convert.
--
-- @fixme Is the "R" flag some undocumented/undefined no-op magic?
--        Are we using it instead of the old '-{' .. content .. '}-'
--        to avoid confusion caused by a flag in the "content"?
function p.raw( content )
    return '-{R|' .. content .. '}-'
end

--- Wraps a title conversion rule.
function p.title( content )
    return '-{T|' .. content .. '}-'
end

--- Wraps a (hidden) conversion rule definition.
function p.hidden( content )
    return '-{H|' .. content .. '}-'
end

return p