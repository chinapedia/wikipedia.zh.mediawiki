-- 第一步：點擊頁面頂部「編輯」按鈕開始編輯本模組。
-- STEP 1: Click on the "edit" tab at the top of the page to edit this module.

-- 第二步：如果你想加上1之外的數目，請修改等號後的數字。
-- STEP 2: if you want to increment by a number other than 1, put that number below, after the equals sign. 
local increment = 1

-- 第三步：用你想增加數字的模板部分替換下方內容。
-- STEP 3: Replace the example template text with the template text that you wish to increment.
local templatetext = [==========[
|header3  = Section 1
|label5   = Label A
|data5    = Data A
|label7   = Label C
|data7    = Data C
|header10 = Section 2
|label12  = Label D
|data12   = Data D
]==========]

-- 第四步：保存本模組。
-- STEP 4: Save this module.

-- 第五步：你現在可以通過以下代碼輸出數字增加後的代碼：
--                {{subst:#invoke:IncrementParams|main}}
-- 又或者直接拷貝下方模組文檔中的修改後的代碼。
-- STEP 5: You can now output the incremented text with the following code:
--                {{subst:#invoke:IncrementParams|main}}
-- Or you can simply copy and paste the text from this module's documentation.

-- 第六步：檢查輸出內容！在某些情況下本模組可能會產生部分假陽性結果。
-- 比如它會將「[[Some_link|foo3=bar]]」修改為「[[Some_link|foo4=bar]]」。
-- 你可以通過模板編輯頁面中「顯示變更」按鈕檢查是否有假陽性結果存在。
-- STEP 6: Check the output! In rare cases this module might produce false positives.
-- For example, it will change the text "[[Some_link|foo3=bar]]" to "[[Some_link|foo4=bar]]".
-- You can use the "show changes" function in the edit window of the template you are editing
-- to find any false positives.

-- 第七步：當你完成後，撤回你於本模組的編輯，避免下一個使用本模組的人對使用方法感到混淆。
-- 謝謝使用本模組！
-- STEP 7: When you are finished, undo your changes to this page, so that the next person
-- won't be confused by seeing any non-default values. Thanks for using this module!

local p = {}
 
local function replace(prefix, num, suffix)
    return '|' .. prefix .. tostring(tonumber(num) + increment) .. suffix .. '='
end
 
function p.main(frame)
    -- Increment the template text.
    templatetext = mw.ustring.gsub(templatetext, '|(%s*%a?[%a_%-]-%s*)([1-9]%d*)(%s*[%a_%-]-%a?%s*)=', replace)
    -- Add pre tags and escape html etc. if the pre option is set.
    if frame and frame.args and frame.args.pre and frame.args.pre ~= '' then
        templatetext = mw.text.nowiki(templatetext)
        templatetext = '<pre style="white-space:-moz-pre-wrap; white-space:-pre-wrap; '
            .. 'white-space:-o-pre-wrap; white-space:pre-wrap; word-wrap:break-word;">' 
            .. templatetext .. '</pre>'
    end
    return templatetext
end
 
return p