-- Note: Originally written on English Wikipedia as [[w:en:Module:Attached_KML|w:en:Module:Attached_KML]]
-- ##### Localisation (L10n) settings #####
local L10n = {}

-- Template parameter names
-- (replace values in quotes with local parameter names)
L10n.para = {
	display		= "display",
	from		= "from",
	header		= "header",
	title		= "title",
	wikidata	= "wikidata",
	demo		= "demo",
}

-- Other configuration settings
L10n.config = {
	inline_format	= "box",			-- controls the format used for inline display, can be set to "box" (default) or "line"
							   -- "box" example: https://en.wikipedia.org/wiki/Template:Attached_KML
							   -- "line" example: https://sv.wikipedia.org/wiki/Mall:KML
}

-- Other strings
L10n.str = {
	inline		= "inline",			-- used with display parameter: (|display=inline) or (|display=title) or (|display=inline,title) or (|display=title,inline)
	title		= "title",			-- (as above)
	dsep		= ",",				-- separator between inline and title (comma in the example above)
	kml_prefix	= "Template:Attached KML/",	-- local KML files are stored as subpages of this location
	default_title	= "路线图",			-- default title for links at top of page, when title parameter not used in transclusion
	default_header	= "",				-- default header for links in inline box, when header parameter not used in transclusion
	kml_file	= "KML文件",			-- text to display for link to raw KML file
	edit		= "编辑",			-- text to display for link to edit KML file
	help		= "帮助",			-- text to display for help page link
	help_location	= ":en:Help:Attached KML",		-- page to link to for help page link
	err_prepend	= "Attached KML",		-- text to prepend to the error messages, when shown at top of page (display=title)
	err		= {				-- error messages
		malformed_qid	= "錯誤：malformed  item id in <code><nowiki>|" .. L10n.para.wikidata .. "=</nowiki></code>",	-- item id doesn't match pattern (number with Q prefix)
		bad_qid		= "錯誤：item specified on Wikidata, or in <code><nowiki>|" .. L10n.para.wikidata .. "=</nowiki></code>, is not a KML file <small>(P31→Q26267864 not found)</small>",	-- item doesn't have a P31→Q26267864 statement
		no_item		= "錯誤：item specified in <code><nowiki>|" .. L10n.para.wikidata .. "=</nowiki></code> not found on Wikidata",	-- item not found on wikidata
		bad_from	= "錯誤：KML文件不存在，請檢查<code><nowiki>|" .. L10n.para.from .. "=</nowiki></code>",	-- KML specified by from parameter doesn't exist
		no_kml		= "錯誤：KML文件不存在",	-- no KML file found
	},
	cat		= {				-- tracking categories: full wikimarkup required, or set to the empty string ("") to not to track the condition
		wikidata_kml	= "[[Category:带有使用来自于Wikidata的KML的条目|Category:带有使用来自于Wikidata的KML的条目]]",	-- tracks mainspace articles using KML from Wikidata
		local_kml	= "[[Category:带有使用不来自于Wikidata的KML的条目|Category:带有使用不来自于Wikidata的KML的条目]]",	-- tracks mainspace articles not using KML from Wikidata
		error_mqid	= "[[Category:Attached_KML错误|M]]",			-- tracks malformed_qid error
		error_badqid	= "[[Category:Attached_KML错误|W]]",			-- tracks bad_qid error
		error_noitem	= "[[Category:Attached_KML错误|N]]",			-- tracks no_item error
		error_from	= "[[Category:Attached_KML错误|F]]",			-- tracks bad_from error
		error_nokml	= "[[Category:Attached_KML错误|K]]",			-- tracks no_kml error
	},
	line		= {				-- these strings are only needed if using 'inline_format = "line"' configuration
		start		= "",				-- wikitext to display at start of line, may include image markup, should start with a space
		separator	= "",				-- text to display between links to external mapping providers, should include spaces
		},
}

-- Masks for external mapping providers, in the form:
--   externalLinkMasks[index-number] = { short = "short-label", long = "long-label", link = "url" }'
-- The short label is used for the title links; the long label is used for the inline links
-- Links in the output will be ordered by index-number
-- Instead of kml file's raw url or encoded raw url, use  __KML_URL__  or  __KML_URL_E__
local externalLinks = {}
--externalLinks[1] = { 
--	short = "Bing",
--	long  = "在Bing地图中显示",
--	link  = "http://www.bing.com/maps/?mapurl=__KML_URL__"
--}

-- #### End of L10n settings ####

-- Table of available wikis, in the order that they are to be searched for kml files
-- (once a kml file is found, further sites are not checked)
local sites = {}
sites[1]  = { mw.ustring.match( mw.site.server, "%w+" )  ..  mw.ustring.gsub( mw.ustring.lower(mw.site.siteName), "[mp]edia", ""),  mw.ustring.sub(mw.site.server, 3), "" } -- local wiki (listed first so local files can override files on other wikis)
sites[2]  = { "commonswiki", "commons.wikimedia.org", "c:" } -- Commons would be a logical central repository for KML files (but has no files as of August 2016)
sites[3]  = { "enwiki", "en.wikipedia.org", "w:en:" } -- largest source of KML files (as of August 2016)
sites[4]  = { "bnwiki", "bn.wikipedia.org", "w:bn:" } -- other sites with a KML template, listed in alphabetical order
sites[5]  = { "cswiki", "cs.wikipedia.org", "w:cs:" } 
sites[6]  = { "fawiki", "fa.wikipedia.org", "w:fa:" } 
sites[7]  = { "frwiki", "fr.wikipedia.org", "w:fr:" } 
sites[8]  = { "jawiki", "ja.wikipedia.org", "w:ja:" } 
sites[9]  = { "mlwiki", "ml.wikipedia.org", "w:ml:" } 
sites[10] = { "svwiki", "sv.wikipedia.org", "w:sv:" } 
sites[11] = { "zhwiki", "zh.wikipedia.org", "w:zh:" } 

--Parameter for cleaned-up parent.args (whitespace trimmed, blanks removed)
local Args = {}

local p = {}

function p.main(frame)
	local parent = frame.getParent(frame)
	Args = setCleanArgs(parent.args)

	local qid = Args[L10n.para.wikidata] or nil

	-- get KML file url
	local wikiUrl, wikiTitle, wikiLink, trackingWikitext, kmlError
	if not (Args[L10n.para.from]) then
		if not qid then
			wikiUrl, wikiLink, siteindex, kmlError = getUrlFromWikidata()
		elseif  mw.ustring.find( qid, "^Q%d+" ) then
			wikiUrl, wikiLink, siteindex, kmlError = getUrlFromQid(qid)
		else
			kmlError = makeError(L10n.str.err.malformed_qid, L10n.str.cat.error_mqid)
		end
	end
	if not (wikiUrl) then
		wikiLink = Args[L10n.para.from] or mw.title.new(tostring(mw.title.getCurrentTitle())).text
		wikiLink = L10n.str.kml_prefix .. wikiLink
		wikiTitle = mw.title.new( wikiLink )
		if not (wikiTitle.exists) and not (kmlError) then
			if Args[L10n.para.from] then
				kmlError = makeError(L10n.str.err.bad_from, L10n.str.cat.error_from)
			else
				kmlError = makeError(L10n.str.err.no_kml, L10n.str.cat.error_nokml)
			end
		end
		wikiUrl = wikiTitle:fullUrl("action=raw","https")
		siteindex = 1
		trackingWikitext =  mw.ustring.format( "<div title=\"KML & Wikidata\" style=\"display:none;\">KML is not from Wikidata</div>{{#ifeq:{{NAMESPACE}}|{{ns:0}}|%s}}", L10n.str.cat.local_kml )
	else
		trackingWikitext =  mw.ustring.format( "<div title=\"KML & Wikidata\" style=\"display:none;\">KML is from Wikidata</div>{{#ifeq:{{NAMESPACE}}|{{ns:0}}|%s}}", L10n.str.cat.wikidata_kml )
	end

	-- replace __KML_URL__ or __KML_URL_E__ with actual values
	local encodedWikiUrl = mw.uri.encode(wikiUrl, "PATH")
	for i, v in ipairs( externalLinks ) do
		local el1 = safeReplace( v.link, "__KML_URL__", wikiUrl )
		local el2 = safeReplace( el1, "__KML_URL_E__", encodedWikiUrl )
		externalLinks[i]["link"] = el2
	end

	-- suppress errors and categories if demo parameter is set
	if Args[L10n.para.demo] then
		kmlError = nil
		trackingWikitext = ""
	end

	local wikitext = ""
	if Args[L10n.para.display] then
		local display = mw.text.split(Args[L10n.para.display], '%s*' .. L10n.str.dsep .. '%s*')
		if display[1] == L10n.str.title or display[2] == L10n.str.title then
			wikitext = makeTitleWikitext(Args[L10n.para.title] or L10n.str.default_title, kmlError)
		end
		if display[1] == L10n.str.inline or display[2] == L10n.str.inline or (display[1] ~= L10n.str.title and display[2] ~= L10n.str.title) then
			local inlineWikitext = makeInlineWikitext(Args[L10n.para.header] or L10n.str.default_header, wikiUrl, kmlError)
			wikitext = wikitext .. inlineWikitext
		end
	else
		wikitext = makeInlineWikitext(Args[L10n.para.header] or L10n.str.default_header, wikiUrl, kmlError)
	end
	wikitext = wikitext .. makeKmldataDiv(wikiLink, siteindex) .. trackingWikitext

	return frame:preprocess( wikitext )

end

function setCleanArgs(argsTable)
	local cleanArgs = {}
	for key, val in pairs(argsTable) do
		if type(val) == 'string' then
			val = val:match('^%s*(.-)%s*$')
			if val ~= '' then
				cleanArgs[key] = val
			end
		else
			cleanArgs[key] = val
		end
	end
	return cleanArgs
end

function safeReplace(string, pattern, replacement)
	-- avoids "Lua error: invalid capture index" that occurs with string.gsub when the replacement contains one or more literal % character
	local nonpattern_parts = mw.text.split( string, pattern )
	return table.concat(nonpattern_parts, replacement)
end


function makeTitleWikitext(titletext, err)
	if err and L10n.str.err_prepend then err =  mw.ustring.gsub( err, ">", ">" .. L10n.str.err_prepend .. " ", 1 ) end

	local titleLinks = {}
	for i, v in ipairs( externalLinks ) do
		titleLinks[i] =  mw.ustring.format( "[%s %s]", v.link , v.short)
	end
	return  mw.ustring.format( "<span style=\"font-size: small;\"><span id=\"coordinates\">\'\'\'%s\'\'\': %s</span></span>", titletext, err or table.concat(titleLinks, " / ") ) 
end


function makeInlineWikitext(headertext, url, err)
	local inlineLinks = {}
	for i, v in ipairs( externalLinks ) do
		inlineLinks[i] =  mw.ustring.format( "[%s %s]", v.link , v.long)
	end
	local editUrl =  mw.ustring.gsub( url, "action=raw", "action=edit" )
	local wiki_link_class
	if  mw.ustring.find( editUrl, mw.site.server, 1, true ) then
		wiki_link_class = "plainlinks"
	else
		wiki_link_class = ""
	end

	if L10n.config.inline_format == "line" then
		return  mw.ustring.format( "<li>%s%s%s (<span class=\"%s\">[%s %s] <span style=\"font-size:85%%;\">([%s %s] • [[%s|%s]])</span></span>)</li>", headertext, L10n.str.line.start, err or table.concat(inlineLinks, L10n.str.line.separator), wiki_link_class, url, L10n.str.kml_file, editUrl, L10n.str.edit, L10n.str.help_location, L10n.str.help)
	else
		return  mw.ustring.format( "<table class=\"metadata mbox-small\" style=\"border:1px solid #aaa;background-color:#f9f9f9;font-size: 88%%; line-height: 1.5em\"><tr><td style=\"width:1px\"></td><td class=\"mbox-text plainlist\">%s<span class=\"%s\">\'\'\'[%s %s]\'\'\' ([%s %s] • [[%s|%s]])</span>\n<ul><li>%s</li></ul></td></tr></table>", headertext, wiki_link_class, url, L10n.str.kml_file, editUrl, L10n.str.edit, L10n.str.help_location, L10n.str.help, err or table.concat(inlineLinks, "</li><li>") )
	end
end

function makeKmldataDiv(link, s_index)
	return  mw.ustring.format( "<div class=\"kmldata\" data-server=\"%s\" title=\"%s\" style=\"display:none;\">[[%s%s|%s%s]]</div>", sites[s_index][2], link, sites[s_index][3], link )

end

function makeError(msg, cat)
	return  mw.ustring.format( "%s%s%s%s%s%s", "<strong class=\"error\" style=\"font-size:100%\">",  mw.ustring.gsub( msg, "<code>", "<code class=\"error\" style=\"font-size:inherit;font-weight:normal;border:0\">" ), "</strong>", "{{#switch:{{NAMESPACE}}|{{ns:0}}|{{ns:118}}=", cat, "}}")
end


function getUrlFromWikidata()					-- Attempts to get url from linked wikidata items, will return nil if it can't
	local entity = mw.wikibase.getEntityObject()
	if not entity then return nil end			

	local kml_claim = entity:getBestStatements("P3096")	-- P3096 is property "KML file"
	
	if kml_claim then
		-- get the QID of the first value of the property
		if (kml_claim[1] and kml_claim[1].mainsnak.snaktype == "value" and kml_claim[1].mainsnak.datavalue.type == "wikibase-entityid") then
			local kml_qid = "Q" .. kml_claim[1].mainsnak.datavalue.value["numeric-id"]
			return getUrlFromQid( kml_qid )
		else
			return nil	-- TODO: error message
		end
	else
		return nil	-- TODO: error message
	end
end

function getUrlFromQid( kml_qid )
	local pcall_result, kml_entity = pcall(mw.wikibase.getEntity, kml_qid)
	if not pcall_result then return nil, nil, nil, makeError(L10n.str.err.no_item, L10n.str.cat.error_noitem) end -- Error if entity doesn't exist

	local p31_claim = kml_entity:getBestStatements("P31")		-- P31 is property "instance of"
	local has_good_p31
	for k, v in pairs( p31_claim ) do
		if (p31_claim[k] and p31_claim[k].mainsnak.snaktype == "value" and p31_claim[k].mainsnak.datavalue.type == "wikibase-entityid" and p31_claim[k].mainsnak.datavalue.value["numeric-id"] == 26267864) then
			has_good_p31 = true
		end
	end
	if not (has_good_p31) then return nil, nil, nil, makeError(L10n.str.err.bad_qid, L10n.str.cat.error_badqid) end -- Error if item isn't a kml file

	local kml_sitelink
	local kml_siteindex
	local kml_url
	for i, v in ipairs( sites ) do
		kml_sitelink = kml_entity:getSitelink( v[1] )
		if kml_sitelink then
			kml_url = "https://" .. v[2] .. "/w/index.php?title=" .. mw.uri.encode( kml_sitelink, "WIKI" ) .. "&action=raw"
			kml_siteindex = i
		end
		if kml_url then break end
	end
	return kml_url or nil, kml_sitelink or nil, kml_siteindex or nil, nil
end

return p