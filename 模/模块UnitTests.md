-- [[en:Module:UnitTests|en:Module:UnitTests]]
-- UnitTester provides unit testing for other Lua scripts. For details see [[:en:Wikipedia:Lua#Unit_testing|:en:Wikipedia:Lua#Unit_testing]].
-- For user documentation see talk page.
local UnitTester = {}

local frame, tick, cross
local result_table_header = "{|class=\"wikitable\"\n! !! Text !! Expected !! Actual"
local result_table = ''
local num_failures = 0

function first_difference(s1, s2)
    if s1 == s2 then return '' end
    local max = math.min(#s1, #s2)
    for i = 1, max do
        if s1:sub(i,i) ~= s2:sub(i,i) then return i end
    end
    return max + 1
end

function UnitTester:preprocess_equals(text, expected, options)
    local actual = frame:preprocess(text)
    if actual == expected then
        result_table = result_table .. '| ' .. tick
    else
        result_table = result_table .. '| ' .. cross
        num_failures = num_failures + 1
    end
    local nowiki_open = (options and options.nowiki) and '<nowiki>' or ''
    local nowiki_close = (options and options.nowiki) and '</nowiki>' or ''
    local differs_at = self.differs_at and (' || ' .. first_difference(expected, actual)) or ''
    result_table = result_table .. ' || <nowiki>' .. text:gsub('%|', '|') .. '</nowiki> || ' .. nowiki_open .. expected .. nowiki_close .. ' || ' .. nowiki_open .. actual .. nowiki_close .. differs_at .. "\n|-\n"
end

function UnitTester:preprocess_equals_many(prefix, suffix, cases, options)
    for _, case in ipairs(cases) do
        self:preprocess_equals(prefix .. case[1] .. suffix, case[2], options)
    end
end

function UnitTester:preprocess_equals_preprocess(text1, text2, options)
    local actual = frame:preprocess(text1)
    local expected = frame:preprocess(text2)
    if actual == expected then
        result_table = result_table .. '| ' .. tick
    else
        result_table = result_table .. '| ' .. cross
        num_failures = num_failures + 1
    end
    local nowiki_open = (options and options.nowiki) and '<nowiki>' or ''
    local nowiki_close = (options and options.nowiki) and '</nowiki>' or ''
    local differs_at = self.differs_at and (' || ' .. first_difference(expected, actual)) or ''
    result_table = result_table .. ' || <nowiki>' .. text1:gsub('%|', '|') .. '</nowiki> || ' .. nowiki_open .. expected .. nowiki_close .. ' || ' .. nowiki_open .. actual .. nowiki_close .. differs_at .. "\n|-\n"
end

function UnitTester:preprocess_equals_preprocess_many(prefix1, suffix1, prefix2, suffix2, cases, options)
    for _, case in ipairs(cases) do
        self:preprocess_equals_preprocess(prefix1 .. case[1] .. suffix1, prefix2 .. (case[2] and case[2] or case[1]) .. suffix2, options)
    end
end

function UnitTester:equals(name, actual, expected, options)
    if actual == expected then
        result_table = result_table .. '| ' .. tick
    else
        result_table = result_table .. '| ' .. cross
        num_failures = num_failures + 1
    end
    local nowiki_open = (options and options.nowiki) and '<nowiki>' or ''
    local nowiki_close = (options and options.nowiki) and '</nowiki>' or ''
    local differs_at = self.differs_at and (' || ' .. first_difference(expected, actual)) or ''
    result_table = result_table .. ' || ' .. name .. ' || ' .. nowiki_open .. expected .. nowiki_close .. ' || ' .. nowiki_open .. actual .. nowiki_close .. differs_at .. "\n|-\n"
end

function UnitTester:run(frame_arg)
    frame = frame_arg
    self.frame = frame
    self.differs_at = frame.args['differs_at']
    tick = frame:preprocess('{{Tick}}')
    cross = frame:preprocess('{{Cross}}')

    local table_header = result_table_header
    if self.differs_at then
        table_header = table_header .. ' !! Differs at'
    end

    for key,value in pairs(self) do
        if key:find('^test') then
            result_table = result_table .. "'''" .. key .. "''':\n" .. table_header .. "\n|-\n"
            value(self)
            result_table = result_table .. "|}\n\n"
        end
    end

    return (num_failures == 0 and "<font color=\"#008000\">'''All tests passed.'''</font>" or "<font color=\"#800000\">'''" .. num_failures .. " tests failed.'''</font>") .. "\n\n" .. frame:preprocess(result_table)
end

function UnitTester:new()
    local o = {}
    setmetatable(o, self)
    self.__index = self
    return o
end

local p = UnitTester:new()
function p.run_tests(frame) return p:run(frame) end
return p