local p = {}
--p.Weighted_page_size 修改自module:Template:Weighted_page_size
function p.Weighted_page_size( titleText )
    if not titleText then
        return 0
    end
    local title = mw.title.new( titleText )
    if not title then
        return 0
    end
    local content = title:getContent()
    if not content then
        return 0
    end
    local chars = mw.ustring.len( content )
    return math.floor( chars * 3.7 + 0.5 )
end

function p.main( frame )
    local titleText = frame.args[1]
    local size
    local icontext
    size = p.Weighted_page_size(titleText)

    if size<3000 then
        icontext='[[File:Qsicon_Ueberarbeiten.svg|16px]]'
    elseif size<10000 then   
        icontext='[[File:Qsicon_inArbeit.svg|16px]]'
    elseif size<30000 then  
        icontext='[[File:YesCheck_BlueLinear.svg|16px]]'
    else    
        icontext='[[File:YesCheck_GreenLinear.svg|16px]]'
    end
    return icontext
end
--產生優良條目, 特色條目的圖示
function p.FA_GA_icon(frame)
	local return_string = ""
    if not frame then
        return_string = ""
    else
        local titletext = frame.args[1]
        -- Weighted_page_size() > 0, 表示條目存在
        if p.Weighted_page_size(titletext) > 0 then
            local text = mw.ustring.lower(mw.title.new(titletext):getContent())
	        if text == '' or text == nil then
	        else	
                local GotFA = string.find(text, "{{featured article}}", 1, true)
                local GotGA = string.find(text, "{{good article}}", 1, true)
                if GotGA then
                    return_string = '[[File:Symbol_support_vote.svg|16px]] '
                else
                    if GotFA then
    	                return_string = '[[File:Cscr-featured.png|16px]] '
                    end              
                end    
            end    
        end    
    end   
    return return_string
end


return p