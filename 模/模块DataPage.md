local p = {}
local yesno = require('Module:Yesno')

function p.getDisambiguationData(test_str)

	local start_iterator = 0
	while start_iterator >= 0 do
		start_pos = start_iterator
		start_iterator = mw.ustring.find( test_str, " (", start_iterator + 1, true )
		
		if start_iterator == nil then
        	start_iterator = -1
		end
		
	end
	
	local end_iterator = 0
	while end_iterator >= 0 do
		end_pos = end_iterator
		end_iterator = mw.ustring.find( test_str, ')', end_iterator + 1, true )
		if end_iterator == nil then
        	end_iterator = -1
		end
	end

	if (start_pos < 0) or (end_pos < 0) or (end_pos <= start_pos) then
		return {test_str , ''}
	end
	return {mw.ustring.sub(test_str, 1, start_pos - 1) , mw.ustring.sub(test_str, start_pos + 1, end_pos)}
end

function p.getWithoutDisambiguation(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	return p.getDisambiguationData(args)[1]
end

function p.getWithDisambiguation(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	return p.getDisambiguationData(args)[2]
end

function p.getDataPageNameByArg(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	
	isHans = "no"
	no_disambig = "no"
	
	if (args[1] and args[1]  ~= '') then 
		page_name = args[1]
	end
	
	if (args["isHans"] and args["isHans"]  ~= '') then 
		isHans = args["isHans"]
	end
	
	if (args["NoDisambig"] and args["NoDisambig"]  ~= '') then 
		no_disambig = args["NoDisambig"]
	end

	return p.getDataPageName(page_name, yesno(is_hans), yesno(no_disambig))
end

function p.getDataPageName(page_name, is_hans, no_disambig)

	datapage_str = "性質表"
	if is_hans then
		datapage_str = "性质表"
	end
	
	disambiguation_data = p.getDisambiguationData(page_name)
	if disambiguation_data[2] == '' then
		return disambiguation_data[1] .. datapage_str
	end
	
	if no_disambig then
		return disambiguation_data[1] .. datapage_str
	end
	
	return disambiguation_data[1] .. datapage_str .. ' ' .. disambiguation_data[2]
end

function p.testDataPageNameExist(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	
	if (args[1] and args[1]  ~= '') then 
		page_name = args[1]
	else
		return ''	
	end
	
	return p.getDataPageNameExist(page_name)
end

function p.getDataPageNameExist(page_name)
	disambiguation_data = p.getDisambiguationData(page_name)
	
	pagename = disambiguation_data[1]
	disambigname = disambiguation_data[2]
	--目前條目尚未移動，因此若要讓測試樣例看出效果，因此要包含舊的命名方式檢查
	name_array = { "性質表" .. ' ' .. disambiguation_data[2], "性质表" .. ' ' .. disambiguation_data[2],
		"性質表", "性质表",
		mw.ustring.sub(disambiguation_data[2], 2, -2) .. "性質表", mw.ustring.sub(disambiguation_data[2], 2, -2) .. "性质表",
		" (數據頁)", " (数据页)", "/數據頁", "/数据页"
	}
	
	for i = 1,10 do
		test_pagename = pagename .. name_array[i]
		test_page_entity = mw.title.new( test_pagename ); --mw.site.namespaces[0].displayName
		if test_page_entity and test_page_entity.exists then
			return test_pagename
		end
	end
	
	return ''
end

function p.getNameFromDataPage(datapagename)
    disambiguation_data = p.getDisambiguationData(datapagename)
    matter_name = disambiguation_data[1]
	startpos, endpos = mw.ustring.find( datapagename, "性[質质]表" )
	if startpos ~= nil then 
		matter_name = mw.ustring.gsub( disambiguation_data[1], "性[質质]表" , '')
		if disambiguation_data[2] ~= '' and disambiguation_data[2] ~= nil then
			matter_name = matter_name .. ' ' .. disambiguation_data[2]
		end
	    return matter_name
    end
    return ''
end

function p.get_name_from_datapage(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	if (args[1] and args[1]  ~= '') then 
		page_name = args[1]
	end
	return p.getNameFromDataPage(page_name)
end

return p