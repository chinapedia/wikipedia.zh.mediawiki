local p = {}

--引入的程式庫
local other_wiki_link_module = require('Module:Ilh')
local yesno = require('Module:Yesno')
local elements = require('Module:Element')
local element_data = require( 'Module:Element/data' )
local err_msg = require('Module:Error')

--靜態變數與函數
local static_funcs = { 
	default_link = "化學元素",
	default_symbol = "X",
	table_split = "\n|-",
	table_newline = "\n|",
	no_decay_data_row = "\n| colspan=\"3\" style=\"text-align:left;\" |",
	stable_data_row = "\n| colspan=\"4\" style=\"text-align:left;\" |",
	no_decay_data_row_with_energy = "\n| colspan=\"4\" style=\"text-align:left;\" |",
	stable_data_row_with_energy = "\n| colspan=\"5\" style=\"text-align:center;\" |",
	table_head = "{| class=\"wikitable\" cellpadding=0 style=\" text-align:center;width:100%; border-collapse:collapse; margin:0; padding:0;\"\n|-",
	table_head_isotope = "[[同位素|同位素]]",
	table_head_decay = "[[放射性#衰变|衰變]]",
	table_head_natural_abundance = "[[丰度|丰度]]",
	table_head_decay_halflife = "[[半衰期|半衰期]] <small><span style=\"font-weight:normal;\">(\'\'t\'\'<sub>1/2</sub>)</span></small>",
	table_head_decay_mode = "[[衰變方式|方式]]",
	table_head_decay_energy = "[[衰變能量|能量]]<small>（[[電子伏特|MeV]]）</small>",
	table_head_decay_product = "[[衰变产物|產物]]",
	table_head_elementbox_isotope_header = "\n! rowspan=2 |",
	table_head_isobox_isotope_header = "\n! |",
	table_head_isobox_isotope_outline_header = "\n! colspan=3 |",
	no_value = ' -'--
}
function static_funcs.Isotope_name(mass_data, symbol_data) return "<sup>" .. mass_data .. "</sup>" .. symbol_data end
function static_funcs.get_count(input_list) 
	count = 0 for __id, __value in pairs(input_list.list) do 
		if __value ~= nil then 
			if __value.mode ~= nil then
				if __value.decays ~= nil then
					count = count + __value.decays.count
				else
					count = count + 1
				end
			end
		end
	end 
	return count 
end
function static_funcs.observationally_stable(first_line) if first_line then return "[[觀測上穩定的同位素|觀測上穩定]]" else return "觀測上穩定" end end
function static_funcs.stable(first_line) if first_line then return "[[穩定同位素|穩定]]" else return "穩定" end end
function static_funcs.neutron(neutron_count) return "，帶" .. neutron_count .. "個[[中子|中子]]" end
function static_funcs.ref(ref_str) if ref_str then return ref_str else return '' end end
function static_funcs.default_decay_arg(flag) if flag then return "default" else return "__default__" end end
function static_funcs.rowspan(count, head) 
	if head then return "\n! rowspan=\"" .. count .. "\" style=\"text-align:right; vertical-align:middle;\" | " 
	else return "\n| rowspan=\"" .. count .. "\" style=\"text-align:right; vertical-align:middle;\" | " end
end
function static_funcs.decay_data_and_newline(mode, ref) 
	return "\n| |" .. (mode or ' ') .. (ref or ' ') .. "\n| style=\"text-align:right;\" | "
end
function static_funcs.check_natural_abundance(str)
	result = mw.ustring.find(str, "%%$", 1, false)
	if result == nil then result = 0 end 
	return result
end
function static_funcs.get_link(loc_link, tsl_link, tsl_lang, display_sym) 
	if loc_link == nil then link_str = display_sym else link_str = "[["_.._loc_link_.._"|" .. display_sym .."]]" end
	if tsl_link ~= nil and tsl_lang ~= nil and loc_link ~= nil then
		--construct ilh args
		link_str = other_wiki_link_module.main({
			['lang'] = tsl_lang, ['lang-code'] = tsl_lang, [1] = loc_link, [2] = tsl_link, ['d'] = display_sym
		})
	end
	return link_str
end
function static_funcs.get_link_with_nuclear_isomer_link(loc_link, tsl_link, tsl_lang, 
		display_mass, display_nuclear_isomer, display_nuclear_isomer_link, display_symbol 
	) 
		if loc_link == nil then link_str = "<sup>" .. display_mass .. display_nuclear_isomer .."</sup>" .. display_symbol else 
			if display_nuclear_isomer_link ~= nil then
				link_str = "<sup>[["_.._loc_link_.._'|' .. display_mass .."]]" ..
					"[["_.._display_nuclear_isomer_link_.._'|' .. display_nuclear_isomer .. "]]</sup>" ..
					"[["_.._loc_link_.._'|' .. display_symbol .."]]"
			else
				link_str = "[["_.._loc_link_.._"|<sup>" .. display_mass .. display_nuclear_isomer .."</sup>" .. display_symbol .. "]]"
			end
		end
		if tsl_link ~= nil and tsl_lang ~= nil and loc_link ~= nil then
			if display_nuclear_isomer_link ~= nil then
				link_str = "<sup>" .. 
						other_wiki_link_module.main({
							['lang'] = tsl_lang, ['lang-code'] = tsl_lang, [1] = loc_link, [2] = tsl_link, ['d'] = display_mass
						}) ..
					"[["_.._display_nuclear_isomer_link_.._'|' .. display_nuclear_isomer .. "]]</sup>" ..
						other_wiki_link_module.main({
							['lang'] = tsl_lang, ['lang-code'] = tsl_lang, [1] = loc_link, [2] = tsl_link, ['d'] = display_symbol
						})
			else
				link_str = other_wiki_link_module.main({
					['lang'] = tsl_lang, ['lang-code'] = tsl_lang, [1] = loc_link, [2] = tsl_link, 
					['d'] = "<sup>" .. display_mass .. display_nuclear_isomer .."</sup>" .. display_symbol
				})
			end
		end
	return link_str
end
--------------------------------------
--debug
--------------------------------------

function p.sandbox_match_test(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	body = ''
	decay_list = p.get_decay_list(args)
	
	for decay_id, decay_value in pairs(decay_list.list) do
		body = body .. "\n:" .. "decay data " .. decay_value.id
		
		for decay_it, decay_data in pairs(decay_value) do
			if type(decay_data) ~= "table" then
				body = body .. "\n::" .. decay_it .. " = " .. decay_data
			end
		end
		
		body = body .. "\n::" .. "decay datas [" .. decay_value.decays.count .. "] :"
		for decay_it_entity, decay_entity in pairs(decay_value.decays.list) do
			body = body .. "\n:::" .. "decay data:"
			for decay_it1, decay_data1 in pairs(decay_entity) do
				body = body .. "\n::::" .. decay_it1 .. " = " .. decay_data1
			end
		end
		
	end
	
	return body
end

----------------------------------------------------------------------------
--本體
----------------------------------------------------------------------------

--主函數
function p.main(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	
	return p._gen_table(get_args)
end

--產生表格頭部
function p.create_table_head(frame)
	body  = ''
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	if get_args['element_box'] ~= nil then is_ele = yesno(get_args['element_box']) end
	if get_args['with_energy'] ~= nil then with_energy = yesno(get_args['with_energy']) end
	body = body .. static_funcs.table_head
	
	if is_ele then
		body = body .. static_funcs.table_head_elementbox_isotope_header .. static_funcs.table_head_isotope
		body = body .. static_funcs.table_head_elementbox_isotope_header .. static_funcs.table_head_natural_abundance
		body = body .. static_funcs.table_head_elementbox_isotope_header .. static_funcs.table_head_decay_halflife
		body = body .. static_funcs.table_head_isobox_isotope_outline_header .. static_funcs.table_head_decay
		body = body .. static_funcs.table_split
	else
		body = body .. static_funcs.table_head_isobox_isotope_outline_header .. static_funcs.table_head_isotope
		body = body .. static_funcs.table_head_isobox_isotope_outline_header .. static_funcs.table_head_decay
		body = body .. static_funcs.table_split .. static_funcs.table_head_isobox_isotope_header
		body = body .. static_funcs.table_head_isobox_isotope_header .. static_funcs.table_head_natural_abundance
		body = body .. static_funcs.table_head_isobox_isotope_header .. static_funcs.table_head_decay_halflife
	end
	body = body .. static_funcs.table_head_isobox_isotope_header .. static_funcs.table_head_decay_mode
	if with_energy then
		body = body .. static_funcs.table_head_isobox_isotope_header .. static_funcs.table_head_decay_energy
	end
	body = body .. static_funcs.table_head_isobox_isotope_header .. static_funcs.table_head_decay_product
	
	return body
end

function p.isotope_bottom_nav(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	body = "{| style=\"width:100%;\""
	sym = get_args['symbol']
	if sym == nil then return nil end
	
	eleid = elements.getListID(sym)
	ele1 = element_data[eleid]
	if ele1 ~= nil then if ele1.Z ~= nil then if ele1.Z == 0 then
		last_ele = { name="反氫" , page="反氫", Symbol="<font style=\"text-decoration: overline\">H</font>", Z=-1 }
	end end end
	last_ele = last_ele or elements.last_element(sym)
	next_ele = elements.next_element(sym)

	if last_ele == nil or next_ele == nil then return '' end
	body = body .. "\n| style=\"text-align:left; vertical-align:middle;\" |<small><span style=\"font-weight:normal;\">[[" ..
		last_ele.page .. "的同位素|←" ..  last_ele.Symbol .. "]]<sub>（[["_.._last_ele.page_.._'|' .. last_ele.Z .. "]]）</sub>"
	body = body .. "\n| style=\"text-align:right; vertical-align:middle;\" |<small><span style=\"font-weight:normal;\">[[" ..
		next_ele.page .. "的同位素|" ..  next_ele.Symbol .. "]]<sub>（[["_.._next_ele.page_.._'|' .. next_ele.Z .. "]]）</sub>[["_.._next_ele.page_.._"的同位素|→]]"
	body = body .. "\n|}"
	return body
end

--穩定同位素資料列
function p.stable_table(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	
	return p._gen_table(get_args, true)
end

--產生適合有有衰敗能量資訊表格的穩定同位素資料列
function p.stable_table_with_energy(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	
	return p._gen_table(get_args, true, true)
end

--產生有衰敗能量資訊的資料列
function p.table_with_energy(frame)
	if not getArgs then
		getArgs = require('Module:Arguments').getArgs
	end
	get_args = getArgs(frame, {parentFirst=true})
	
	return p._gen_table(get_args, false, true)
end

--不適合模板包含的呼叫方式
function p.gen_table(frame)
	-- For calling from #invoke.
	local pframe = frame:getParent()
	args = {}
	for k, v in pairs( frame.args ) do
		args[k] = v;	   
	end
	return p._gen_table(args)
end

--產生同位素資料列主函數
function p._gen_table(args, is_stable, with_energy)
	local body = ''
	iso_symbol = static_funcs.default_symbol
	iso_mass = ''
	iso_na = ''
	iso_halflife = static_funcs.no_value
	first_link = true
	check_flag = true

    --非穩定同位素，取得衰變方式個數
	if not is_stable then
		decay_list = p.get_decay_list(args)
		count = static_funcs.get_count(decay_list)
	end
	
	--檢查參數
	if args['mn'] ~= nil then iso_mass = args['mn'] end
	if args['mnm'] ~= nil then if mw.text.trim(args['mnm']) ~= '' then iso_nuclear_isomer = args['mnm'] end end
	if args['mnm_link'] ~= nil then if mw.text.trim(args['mnm_link']) ~= '' then iso_nuclear_isomer_link = args['mnm_link'] end end
	if args['link'] ~= nil then iso_link = args['link'] end
	if args['na'] ~= nil then iso_na = args['na'] end
	if args['halflife'] ~= nil then iso_halflife = args['halflife'] end
	if args['hl'] ~= nil then iso_halflife = args['hl'] end
	if args['firstlinks'] ~= nil then first_link = yesno(args['firstlinks']) end
	
	if args['sym'] ~= nil then 
		if args['sym'] == '' then check_flag = false else iso_symbol = args['sym']  end
	else check_flag = false end
	
	element_id = elements.getListID(iso_symbol)
	if element_id >= 0 then 
		iso_symbol = element_data[element_id].Symbol 
		element_id = element_data[element_id].Z
		if element_id == nil then element_id = -1 end
	end
	
	if args['info_row'] ~= nil then is_info_row = yesno(args['info_row']) else is_info_row = false end
	
	if is_info_row then 
		if args['info'] ~= nil then 
			if with_energy then
				return "\n|- \n| colspan = 6 | " .. args['info']
			else
				return "\n|- \n| colspan = 5 | " .. args['info']
			end
		end
	end
	
	--產生連結
	if iso_nuclear_isomer ~= nil then
		iso_link_data = static_funcs.get_link_with_nuclear_isomer_link(
			iso_link, args['tsl'], args['lang'], 
			iso_mass, iso_nuclear_isomer, iso_nuclear_isomer_link, iso_symbol 
		) 
	else
		iso_link_data = static_funcs.get_link(iso_link, args['tsl'], args['lang'], static_funcs.Isotope_name(iso_mass, iso_symbol))
	end
	
	check_flag = check_flag and element_id >= 0

	--確定rowspan
	if not is_stable then
		rowspan = 1 if count > 1 then rowspan = count end
	else
		rowspan = 1
	end
	--建立表格
	body = body .. static_funcs.table_split .. static_funcs.rowspan(rowspan, true and not with_energy) .. iso_link_data  .. static_funcs.ref(args['isotope_comment'])  .. static_funcs.ref(args['isotope_ref'])
	
	--豐度置中設定
	checkna = static_funcs.check_natural_abundance(iso_na)
	body = body .. "\n| rowspan=\"" .. rowspan .. "\" style=\""
	if checkna > 0 then 
		body = body .. "text-align:right"
	else
		body = body .. "text-align:center"
	end
	body = body .. "; vertical-align:middle;\" | " .. iso_na  .. static_funcs.ref(args['abundance_ref'])
	
	if not is_stable then
		--半衰期
		body = body
		--.. static_funcs.table_newline
		.. '\n' .. static_funcs.rowspan(rowspan) .. iso_halflife .. static_funcs.ref(args['halflife_ref'])
	
		--衰變資訊
		if count <= 0 then
			--無衰變資訊
			if with_energy then
				body = body .. static_funcs.no_decay_data_row_with_energy
			else
				body = body .. static_funcs.no_decay_data_row
			end
			
			if args['stable_data'] ~= nil then
				body = body .. args['stable_data'] .. static_funcs.ref(args['halflife_ref'])
			else
				body = body .. static_funcs.observationally_stable(first_link) .. static_funcs.ref(args['halflife_ref'])
			end

		else
			first_flag = true
			--列出所有衰變資訊
			for decay_i = 1,decay_list.max_number do
				decay_value = nil
				for decay_data_id, decay_data_value in pairs(decay_list.list) do if decay_data_value.number == decay_i then
					decay_value = decay_data_value
				end end
				if decay_value ~= nil then
				
					if first_flag==true then first_flag = false else body = body .. static_funcs.table_split end
					
					if decay_value.mode == nil then decay_value.mode = ' -' end
					decay_first_flag = true
					body = body .. static_funcs.rowspan(decay_value.decays.count) .. decay_value.mode .. static_funcs.ref(decay_value.mode_ref)
					
					first_decay_flag = true
					for i = 1,decay_value.decays.max_number do
						iterator = nil
						for decay_data_id, decay_data_value in pairs(decay_value.decays.list) do if decay_data_value.number == i then
							iterator = decay_data_value
						end end
						if iterator ~= nil then 
						if first_decay_flag==true then first_decay_flag = false else body = body .. static_funcs.table_split end
						
						if iterator.energy == nil then iterator.energy = '' end

						if with_energy then
							body = body .. static_funcs.decay_data_and_newline(iterator.energy, static_funcs.ref(iterator.energy_ref))
						else
							body = body .. static_funcs.table_newline
						end
						product_mass = ''
						if iterator.mass ~= nil then
							product_mass = iterator.mass
						end
						product_symbol = 'X'
						if iterator.symbol ~= nil then
							product_symbol = iterator.symbol
							eleid = elements.getListID(product_symbol)
							trim_str = mw.text.trim(iterator.symbol)
							if trim_str ~= '-' and trim_str ~= '—' and trim_str ~= '–' then check_flag = check_flag and eleid >= 0 end
							if eleid >= 0 then product_symbol = element_data[eleid].Symbol end
						end
						if iterator.nuclear_isomer ~= nil then
							body = body .. static_funcs.get_link_with_nuclear_isomer_link(
								iterator.link, iterator.otherwiki, iterator.lang_code, 
								product_mass, iterator.nuclear_isomer, iterator.nuclear_isomer_link, product_symbol 
							) 
						else
							body = body .. static_funcs.get_link(
								iterator.link, iterator.otherwiki, iterator.lang_code, 
								static_funcs.Isotope_name(product_mass, product_symbol)
							)
						end
						body = body .. static_funcs.ref(iterator.product_comment) .. static_funcs.ref(iterator.product_ref)
						end
					end
				
				end
			end

		end
	else
		--穩定同位素
		observationally_stable = "no"
		if args['observationally_stable'] ~= nil then
			observationally_stable = args['observationally_stable']
		end
		
		if with_energy then
			body = body .. static_funcs.stable_data_row_with_energy
		else
			body = body .. static_funcs.stable_data_row
		end

		if yesno(observationally_stable) then
			body = body .. static_funcs.observationally_stable(first_link) .. static_funcs.ref(args['halflife_ref'])
		else
			if args['stable_data'] ~= nil then
				body = body .. args['stable_data'] .. static_funcs.ref(args['halflife_ref'])
			else
				body = body .. static_funcs.stable(first_link) .. static_funcs.ref(args['halflife_ref'])
			end
			
			if with_energy then
				NandP = tonumber(iso_mass)
				print_N = false
				if NandP ~= nil then if NandP >= 0 and element_id >= 0 then
					body = body .. static_funcs.neutron(NandP - element_id)
					print_N = true
				end end
				if not print_N then
					if args['n'] ~= nil then
						body = body .. static_funcs.neutron(args['n'])
					end
				end
			end
		end
	end
    --檢查是否有錯誤的元素符號
	if (not check_flag) and mw.title.getCurrentTitle().namespace == 0 then body = body .. "[[Category:含有錯誤元素符號的條目|Category:含有錯誤元素符號的條目]]" end
	
	if decay_list ~= nil then for error_category_string, ___ in pairs(decay_list.error_category) do
		body = body .. "[[Category:"_.._error_category_string_.._"|Category:" .. error_category_string .. "]]"
	end body = body .. decay_list.err_msg end
	
	return body
end

--找出衰變資訊
function p.get_decay_list(args)
	--宣告空的衰變列表
	decay_list = { count = 0, list = {}, error_category = {}, max_number = 0, err_msg = '' }
	warning = {}
	unknow_arg = nil
	has_noid = false
	has_linkid = false
	if args['dm'] ~= nil or args['de'] ~= nil or args['halflife1'] ~= nil or args['hl1'] ~= nil or
		args['ps'] ~= nil or args['pn'] ~= nil or args['product_ref'] ~= nil or
		args['mode_ref'] ~= nil or args['halflife_ref1'] ~= nil or args['energy_ref'] ~= nil then
			has_noid = true
			decay_list.count = 1
			decay_list.max_number = 1
			decay_list.list[static_funcs.default_decay_arg()] = { iter = 1, id = '1', number = 1}
			if args['dm'] ~= nil or args['de'] ~= nil or args['pn'] ~= nil or args['ps'] ~= nil
				or args['product_ref'] ~= nil or args['energy_ref'] ~= nil
				or args['link1'] ~= nil or args['tsl1'] ~= nil or args['lang1'] ~= nil then
					decay_list.list[static_funcs.default_decay_arg()].decays = { count = 1, list = {}, max_number = 1 }
					decay_list.list[static_funcs.default_decay_arg()].decays.list[1] = {iter = 1, id = '1', number = 1}
			end
			if args['link1'] ~= nil or args['tsl1'] ~= nil or args['lang1'] ~= nil then has_linkid = true end
			decay_list.list[static_funcs.default_decay_arg()].mode = args['dm']
			if args['halflife1'] ~= nil then decay_list.list[static_funcs.default_decay_arg()].halflife = args['halflife1'] end
			if args['hl1'] ~= nil then decay_list.list[static_funcs.default_decay_arg()].halflife = args['hl1'] end
			if decay_list.list[static_funcs.default_decay_arg()].decays~= nil then
				decay_list.list[static_funcs.default_decay_arg()].decays.list[1].energy = args['de'] 
				decay_list.list[static_funcs.default_decay_arg()].decays.list[1].link = args['link1'] 
				decay_list.list[static_funcs.default_decay_arg()].decays.list[1].otherwiki = args['tsl1'] 
				decay_list.list[static_funcs.default_decay_arg()].decays.list[1].lang_code = args['lang1'] 
				decay_list.list[static_funcs.default_decay_arg()].decays.list[1].symbol = args['ps'] 
				decay_list.list[static_funcs.default_decay_arg()].decays.list[1].mass = args['pn'] 
				decay_list.list[static_funcs.default_decay_arg()].decays.list[1].nuclear_isomer = args['pnm'] 
				decay_list.list[static_funcs.default_decay_arg()].decays.list[1].nuclear_isomer_link = args['pnm_link'] 
				decay_list.list[static_funcs.default_decay_arg()].decays.list[1].product_comment = args['product_comment']
				decay_list.list[static_funcs.default_decay_arg()].decays.list[1].product_ref = args['product_ref'] 
				decay_list.list[static_funcs.default_decay_arg()].decays.list[1].energy_ref = args['energy_ref'] 
			elseif args['de'] == nil and args['link1'] == nil and args['tsl1'] == nil and  args['lang1'] == nil and 
					args['ps'] == nil and args['pn'] == nil and args['pnm'] == nil and  args['pnm_link'] == nil and 
					args['product_comment'] == nil and args['product_ref'] == nil and args['energy_ref'] == nil then
						decay_list.list[static_funcs.default_decay_arg()].decays = { count = 0, list = {}, max_number = 0 }
			end
			decay_list.list[static_funcs.default_decay_arg()].mode_ref = args['mode_ref'] 
			decay_list.list[static_funcs.default_decay_arg()].halflife_ref = args['halflife_ref1'] 
	end
    --搜尋所有參數
	for arg_name, arg_value in pairs(args) do
		if arg_value ~= '' then if mw.text.trim(arg_value) ~= nil then if mw.text.trim(arg_value) ~= '' then
			--{
			--mode, decays { energy, symbol, mass, link, tsl, lang }
			--}
			match_full_name = mw.ustring.match(arg_name, "[^0-9]+[0-9]+%a*")
			if match_full_name == nil then match_full_name = '' end
			match_full_data_name = mw.ustring.match(match_full_name, "[^0-9]+[0-9]+")
			if match_full_data_name == nil then match_full_data_name = '' end
			match_number = mw.ustring.match(arg_name, "[0-9]+")
			org_num_match = match_number
			match_number_id = mw.ustring.match(arg_name, "[0-9]+%a*")
			if match_number == nil then match_number = '0' decay_id = "default" else decay_id = match_number end
			if match_number_id == nil then match_number_id = '0' end
			decay_data_id = mw.ustring.match(match_number_id, "%a+")
			match_data_name = mw.ustring.match(match_full_data_name, "[^0-9]+")
			deacy_number = tonumber(match_number)
			
			if has_noid and has_linkid and match_number == '1' then
				if warning[deacy_number] == nil then 
					if arg_name ~= 'link1' and arg_name ~= 'tsl1' and arg_name ~= 'lang1' and arg_name ~= 'halflife1' and arg_name ~= 'hl1' and arg_name ~= 'halflife_ref1' then
						warning[deacy_number] = true
						decay_list.err_msg = decay_list.err_msg .. err_msg.error{ "參數編號“" .. deacy_number .. '”重複使用。' } .. " <br/> "
					end
				end
				decay_list.error_category['模板參數錯誤的頁面'] = true
			elseif deacy_number == nil then
				--if unknow_arg == nil then unknow_arg =  "“" .. arg_name .. "”" 
				--else unknow_arg = unknow_arg .. "、“" .. arg_name .. "”" end
				--decay_list.error_category['模板參數未知的頁面'] = true
			elseif (deacy_number == 0 or deacy_number > 16384) and org_num_match ~= nil then
				if unknow_arg == nil then unknow_arg =  "“" .. arg_name .. "”" 
				else unknow_arg = unknow_arg .. "、“" .. arg_name .. "”" end
				decay_list.error_category['模板參數未知的頁面'] = true
			else
				if match_full_name ~= nil and match_data_name ~= nil then
					if deacy_number > decay_list.max_number then decay_list.max_number = deacy_number end
					match_data_name = mw.text.trim(match_data_name)
					if decay_list.list[decay_id] == nil then 
						decay_list.count = decay_list.count + 1
						decay_list.list[decay_id] = 
						{ 
							iter = decay_list.count, 
							number = deacy_number, 
							id = decay_id, 
							decays = { count = 0, max_number = 0, list = {} }
						} 
					end
					if decay_data_id ~= nil then 
						if mw.ustring.len(decay_data_id or 'error') == 1 then
							decay_data_id_num = mw.ustring.byte(decay_data_id, 1, 1) - mw.ustring.byte('a') + 1
							if decay_list.list[decay_id].decays.max_number < decay_data_id_num then decay_list.list[decay_id].decays.max_number = decay_data_id_num end
							if decay_list.list[decay_id].decays.list[decay_data_id] == nil then 
								decay_list.list[decay_id].decays.count = decay_list.list[decay_id].decays.count + 1
								decay_list.list[decay_id].decays.list[decay_data_id] = {iter = decay_list.list[decay_id].decays.count, id = decay_data_id, number = decay_data_id_num }
							end
							if match_data_name == "de" then decay_list.list[decay_id].decays.list[decay_data_id].energy = arg_value
							elseif match_data_name == "pn" then decay_list.list[decay_id].decays.list[decay_data_id].mass = arg_value
							elseif match_data_name == "pnm" then decay_list.list[decay_id].decays.list[decay_data_id].nuclear_isomer = arg_value
							elseif match_data_name == "pnm_link" then decay_list.list[decay_id].decays.list[decay_data_id].nuclear_isomer_link = arg_value
							elseif match_data_name == "ps" then decay_list.list[decay_id].decays.list[decay_data_id].symbol = arg_value
							elseif match_data_name == "lang" then decay_list.list[decay_id].decays.list[decay_data_id].lang_code = arg_value
							elseif match_data_name == "tsl" then decay_list.list[decay_id].decays.list[decay_data_id].otherwiki = arg_value
							elseif match_data_name == "link" then decay_list.list[decay_id].decays.list[decay_data_id].link = arg_value
							elseif match_data_name == "product_ref" then decay_list.list[decay_id].decays.list[decay_data_id].product_ref = arg_value
							elseif match_data_name == "product_comment" then decay_list.list[decay_id].decays.list[decay_data_id].product_comment = arg_value
							elseif match_data_name == "energy_ref" then decay_list.list[decay_id].decays.list[decay_data_id].energy_ref = arg_value end
						else
							if unknow_arg == nil then unknow_arg =  "“" .. arg_name .. "”" 
							else unknow_arg = unknow_arg .. "、“" .. arg_name .. "”" end
							decay_list.error_category['模板參數未知的頁面'] = true
						end
					else
						if (match_data_name == "de" or match_data_name == "pn" or match_data_name == "ps" or 
							match_data_name == "pnm" or match_data_name == "pnm_link" or 
							match_data_name == "lang" or match_data_name == "tsl" or match_data_name == "link" or 
							match_data_name == "product_comment" or match_data_name == "product_ref" or match_data_name == "energy_ref") and decay_list.list[decay_id].decays.list[1] == nil then
								decay_list.list[decay_id].decays.list[1] = {iter = 1, id = '1', number = 1}
								decay_list.list[decay_id].decays.max_number = 1
								decay_list.list[decay_id].decays.count = decay_list.list[decay_id].decays.count + 1
						end
						if match_data_name == "de" then decay_list.list[decay_id].decays.list[1].energy = arg_value
						elseif match_data_name == "pn" then decay_list.list[decay_id].decays.list[1].mass = arg_value
						elseif match_data_name == "pnm" then decay_list.list[decay_id].decays.list[1].nuclear_isomer = arg_value
						elseif match_data_name == "pnm_link" then decay_list.list[decay_id].decays.list[1].nuclear_isomer_link = arg_value
						elseif match_data_name == "ps" then decay_list.list[decay_id].decays.list[1].symbol = arg_value
						elseif match_data_name == "lang" then decay_list.list[decay_id].decays.list[1].lang_code = arg_value
						elseif match_data_name == "tsl" then decay_list.list[decay_id].decays.list[1].otherwiki = arg_value
						elseif match_data_name == "link" then decay_list.list[decay_id].decays.list[1].link = arg_value
						elseif match_data_name == "product_ref" then decay_list.list[decay_id].decays.list[1].product_ref = arg_value
						elseif match_data_name == "product_comment" then decay_list.list[decay_id].decays.list[1].product_comment = arg_value
						elseif match_data_name == "energy_ref" then decay_list.list[decay_id].decays.list[1].energy_ref = arg_value 
						elseif match_data_name == "dm" then decay_list.list[decay_id].mode = arg_value 
						elseif match_data_name == "halflife" or match_data_name == "hl" then decay_list.list[decay_id].halflife = arg_value
						elseif match_data_name == "mode_ref" then decay_list.list[decay_id].mode_ref = arg_value 
						elseif match_data_name == "halflife_ref" then decay_list.list[decay_id].halflife_ref = arg_value end
					end
					--
				end
				--
			end
		end end end
	end
	if unknow_arg ~= nil then decay_list.err_msg = decay_list.err_msg .. err_msg.error{ "未知的參數" .. unknow_arg .. '。' } end
	return decay_list
end

return p