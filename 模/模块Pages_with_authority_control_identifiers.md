require('Module:No globals')

local p = {}
local ac_conf = require('Module:Authority control').conf
local currentTitle = mw.title.getCurrentTitle()
local title = currentTitle.text
local isCat = (currentTitle.namespace == 14)

local function whichTOC( frame )
	local pageCount = mw.site.stats.pagesInCategory(title, 'pages')
	if pageCount >= 5000 then
		return frame:expandTemplate{ title = 'Large category TOC' }
	elseif pageCount > 400 then
		return frame:expandTemplate{ title = 'Category TOC', args = { align = 'center' } }
	end
	return ''
end

--For use in [[Category:Pages_with_authority_control_information|Category:Pages with authority control information]],
--   i.e. on [[Category:Pages_with_VIAF_identifiers|Category:Pages with VIAF identifiers]]
local function pages( frame, id )
	for _, conf in pairs( ac_conf ) do
		if conf[1] == id or (conf[1] == 'MBA' and id == 'MusicBrainz') then
			local link = conf[2] --not used locally yet
			local txCatMore = frame:expandTemplate{ title = 'Cat more', args = {'Wikipedia:规范控制'} }
			local txWPCat = frame:expandTemplate{ title = 'Wikipedia category' }
			local outString = txCatMore..txWPCat..'\n'..
					'[[Category:包含规范控制信息的页面|'..id..']]'
			return outString
		end
	end
	return ''
end

--For use in [[Category:Miscellaneous_pages_with_authority_control_information|Category:Miscellaneous pages with authority control information]],
--   i.e. on [[Category:Miscellaneous_pages_with_VIAF_identifiers|Category:Miscellaneous pages with VIAF identifiers]]
local function misc( frame, id )
	for _, conf in pairs( ac_conf ) do
		if conf[1] == id or (conf[1] == 'MBA' and id == 'MusicBrainz') then
			local link = conf[2]
			local txCatExplain = frame:expandTemplate{ title = 'Category explanation', 
					args = { '含有{{[[Template:Authority_control|规范控制]]}}标识符'..link..'的页面。' } }
			local txCatMore = frame:expandTemplate{ title = 'Cat more', args = {'Wikipedia:规范控制'} }
			local txEmptyCat = frame:expandTemplate{ title = 'Possibly empty category' }
			local txWPCat = frame:expandTemplate{ title = 'Wikipedia category', args = { hidden = 'yes', tracking = 'yes' } }
			local txTOC = whichTOC( frame )
			local outString = txCatExplain..txCatMore..txEmptyCat..txWPCat..txTOC..'\n'..
					'本分类中的页面应该只能由[[Module:Authority_control|Module:Authority control]]添加。'..
					'[[Category:包含'..id..'标识符的页面|Category:包含'..id..'标识符的页面]]'..
					'[[Category:包含规范控制信息的其他页面|'..id..']]'
			return outString
		end
	end
	return ''
end

--For use in [[Category:User_pages_with_authority_control_information|Category:User pages with authority control information]],
--   i.e. on [[Category:User_pages_with_VIAF_identifiers|Category:User pages with VIAF identifiers]]
local function user( frame, id )
	for _, conf in pairs( ac_conf ) do
		if conf[1] == id or (conf[1] == 'MBA' and id == 'MusicBrainz') then
			local link = conf[2] --not used locally yet
			local txCatMore = frame:expandTemplate{ title = 'Cat more', args = {'Wikipedia:规范控制'} }
			local txEmptyCat = frame:expandTemplate{ title = 'Possibly empty category' }
			local txWPCat = frame:expandTemplate{ title = 'Wikipedia category', args = { hidden = 'yes', tracking = 'yes' } }
			local txTOC = whichTOC( frame )
			local outString = txCatMore..txEmptyCat..txWPCat..txTOC..'\n'..
					'本分类中的页面应该只能由[[Module:Authority_control|Module:Authority control]]添加。'..
					'[[Category:包含'..id..'标识符的页面|Category:包含'..id..'标识符的页面]]'..
					'[[Category:包含规范控制信息的用户页|'..id..']]'
			return outString
		end
	end
	return ''
end

--For use in [[Category:Wikipedia_articles_with_authority_control_information|Category:Wikipedia articles with authority control information]],
--   i.e. on [[Category:Wikipedia_articles_with_VIAF_identifiers|Category:Wikipedia articles with VIAF identifiers]]
local function wp( frame, id )
	for _, conf in pairs( ac_conf ) do
		if conf[1] == id or (conf[1] == 'MBA' and id == 'MusicBrainz') then
			local link = conf[2]
			local txCatExplain = frame:expandTemplate{ title = 'Category explanation', args = {'包含'..link..'标识符的条目。请不要添加[[Wikipedia:分类#子分类|子分类]]'} }
			local txCatMore = frame:expandTemplate{ title = 'Cat more', args = {'Wikipedia:规范控制'} }
			local txEmptyCat = frame:expandTemplate{ title = 'Possibly empty category' }
			local txWPCat = frame:expandTemplate{ title = 'Wikipedia category', args = { hidden = 'yes', tracking = 'yes' } }
			local txTOC = whichTOC( frame )
			local outString = txCatExplain..txCatMore..txEmptyCat..txWPCat..txTOC..'\n'..
					'本分类中的页面应该只能由[[Module:Authority_control|Module:Authority control]]添加。'..
					'[[Category:包含'..id..'标识符的页面|Category:包含'..id..'标识符的页面]]'..
					'[[Category:包含规范控制信息的维基百科条目|'..id..']]'
			return outString
		end
	end
	return ''
end

--For use in [[Category:Wikipedia_articles_with_faulty_authority_control_information|Category:Wikipedia articles with faulty authority control information]],
--   i.e. on [[Category:Wikipedia_articles_with_faulty_authority_control_identifiers_(VIAF)|Category:Wikipedia articles with faulty authority control identifiers (VIAF)]]
local function wpfaulty( frame, id )
	for _, conf in pairs( ac_conf ) do
		if conf[1] == id or (conf[1] == 'MBA' and id == 'MusicBrainz') then
			local link = conf[2] --not used locally yet
			local param = conf[3]
			local txCatMore = frame:expandTemplate{ title = 'Cat more', args = {'Wikipedia:Authority control', 'd:Property:P'..param} }
			local txEmptyCat = frame:expandTemplate{ title = 'Possibly empty category' }
			local txWPCat = frame:expandTemplate{ title = 'Wikipedia category', args = { hidden = 'yes', tracking = 'yes' } }
			local txDirtyCat = frame:expandTemplate{ title = 'Polluted category' }
			local txTOC = whichTOC( frame )
			local outString = txCatMore..txEmptyCat..txWPCat..txDirtyCat..txTOC..'\n'..
					'本分类中的页面应该只能由[[Module:Authority_control|Module:Authority control]]添加。'..
					'[[Category:包含'..id..'标识符的页面|Category:包含'..id..'标识符的页面]]'..
					'[[Category:包含错误规范控制信息的维基百科条目|Category:包含错误规范控制信息的维基百科条目]]'
			return outString
		end
	end
	return ''
end

--Main/external call
function p.autoDetect( frame )
	if isCat then
		local pagesID    = mw.ustring.match(title, '包含([%w%.%-]+)标识符的页面')
		local miscID     = mw.ustring.match(title, '包含([%w%.%-]+)标识符的其他页面')
		local userID     = mw.ustring.match(title, '包含([%w%.%-]+)标识符的用户页')
		local wpID       = mw.ustring.match(title, '包含([%w%.%-]+)标识符的维基百科条目')
		local wpfaultyID = mw.ustring.match(title, '包含错误规范控制信息的维基百科条目 %(([%w%.%-]+)%)')

		if     pagesID    then return pages( frame, pagesID )
		elseif miscID     then return misc( frame, miscID )
		elseif userID     then return user( frame, userID )
		elseif wpID       then return wp( frame, wpID )
		elseif wpfaultyID then return wpfaulty( frame, wpfaultyID )
		end
	end
	return ''
end

return p