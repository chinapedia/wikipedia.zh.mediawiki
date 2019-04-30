local p = {}

function p.indent(frame)
    -- Trim whitespace from the arguments and remove blank values.
    local args = {}
    if type(frame.args) == 'table' then
        for k, v in pairs( frame.args ) do
            v = mw.text.trim(v)
            if v ~= '' then
                args[k] = v
            end
        end
    end
    
    -- Set variables.
    local indent = tonumber( args[1] )
    local br = args[2]
    local ret = ''
    
    -- Insert line breaks to match the functionality of the original template.
    -- If "br" is set, we need two line breaks; if not, we just need one.
    if br then
        ret = ret .. '<br />' 
    end
    ret = ret .. '<br />'
    
    -- Control for bad or zero input. If found, output the line breaks only, 
    -- as this was the previous behaviour of the template.
    if not indent or indent <= 0 or math.floor(indent) ~= indent then
        return ret
    end
    
    -- Generate the indents. The first four cases are special.
    if indent == 1 then
        return ret .. ' '
    elseif indent == 2 then
        return ret .. '  '
    elseif indent == 3 then
        return ret .. '   '
    elseif indent == 4 then
        return ret .. '     '
    end
    
    -- Set variables for generating the output after indent == 5.
    local r = {}
    r.base = ' ' -- Common text to all output.
    r.rep = '    ' -- The text to repeat.
    r.mod1 = ' ' -- To return on modulo 1.
    r.mod2 = '  ' -- To return on modulo 2.
    r.mod3 = '   ' -- To return on modulo 3.
    
    -- New iteratorText values needed at 5, 9, 13, 17, etc., so repeat the
    -- text (indent - 1)/4 times and find the remainder.
    local reps = math.floor( (indent - 1) / 4 )
    local remainder = math.fmod( indent - 1, 4 )
    
    -- Generate the indent text.
    ret = ret .. r.base .. mw.ustring.rep( r.rep, reps )
    if remainder >= 1 and remainder <= 3 then
        ret = ret .. r[ 'mod' .. remainder ]
    end
    
    return ret
end

return p