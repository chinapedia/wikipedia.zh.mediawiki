require('Module:No globals')

local p = {}

--[[==========================================================================|==========================================================================]]
--[[Category_functions|Category functions]]
--[[==========================================================================|==========================================================================]]

function p.getCatForId( id )
	local title = mw.title.getCurrentTitle()
	local namespace = title.namespace
	local catName = ''
	if namespace == 0 then
		catName = '包含' .. id .. '标识符的维基百科条目'
    elseif namespace == 2 and not title.isSubpage then
		catName = '包含' .. id .. '标识符的用户页'
    else
    	catName = '包含' .. id .. '标识符的其他页面'
	end
	return '[[Category:'_.._catName_.._'|Category:' .. catName .. ']]' .. p.redCatLink(catName)
end

function p.redCatLink( catName ) --catName == 'Blah', not 'Category:Blah', not '[[Category:Blah|Category:Blah]]'
	if catName and catName ~= '' and mw.title.new(catName, 14).exists == false then
		return '[[Category:规范控制分类为红链的页面|Category:规范控制分类为红链的页面]]'
	end
	return ''
end

--[[==========================================================================|==========================================================================]]
--[[Property_formatting_functions|Property formatting functions]]
--[[==========================================================================|==========================================================================]]

function p.iaafLink( id )
	--P1146's format regex: [1-9][0-9]* (e.g. 123)
	if not string.match( id, '^[1-9]%d*$' ) then
		return false
	end
	return '[https://www.iaaf.org/athletes/biographies/athcode=' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'IAAF' )
end

function p.viafLink( id )
	--P214's format regex: [1-9]\d(\d{0,7}|\d{17,20}) (e.g. 123456789, 1234567890123456789012)
	if not string.match( id, '^[1-9]%d%d?%d?%d?%d?%d?%d?%d?$' ) and
	   not string.match( id, '^[1-9]%d%d%d%d%d%d%d%d%d%d%d%d%d%d%d%d%d%d%d?%d?%d?$' ) then
		return false
	end
	return '[https://viaf.org/viaf/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'VIAF' )
end

function p.kulturnavLink( id )
	--P1248's format regex: [0-9a-f]{8}\-[0-9a-f]{4}\-[0-9a-f]{4}\-[0-9a-f]{4}\-[0-9a-f]{12} (e.g. 12345678-1234-1234-1234-1234567890AB)
	if not string.match( id, '^%x%x%x%x%x%x%x%x%-%x%x%x%x%-%x%x%x%x%-%x%x%x%x%-%x%x%x%x%x%x%x%x%x%x%x%x$' ) then
		return false
	end
	return '[http://kulturnav.org/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'KULTURNAV' )
end

function p.sikartLink( id )
	--P781's format regex: \d{7,9} (e.g. 123456789)
	if not string.match( id, '^%d%d%d%d%d%d%d%d?%d?$' ) then
		return false
	end
	return '[http://www.sikart.ch/KuenstlerInnen.aspx?id=' .. id .. '&lng=en ' .. id .. ']' .. p.getCatForId( 'SIKART' )
end

function p.tlsLink( id )
	local id2 = id:gsub(' +', '_')
	--P1362's format regex: \p{Lu}[\p{L}\d_',\.\-\(\)\*/–]{3,59} (e.g. Abcd)
	local class = "[%a%d_',%.%-%(%)%*/–]"
	local regex = "^%u" .. string.rep(class, 3) .. string.rep(class.."?", 56) .. "$"
	if not mw.ustring.match( id2, regex ) then
		return false
	end
	return '[http://tls.theaterwissenschaft.ch/wiki/' .. id2 .. ' ' .. id .. ']' .. p.getCatForId( 'TLS' )
end

function p.ciniiLink( id )
	--P271's format regex: DA\d{7}[\dX] (e.g. DA12345678)
	if not string.match( id, '^DA%d%d%d%d%d%d%d[%dX]$' ) then
		return false
	end
	return '[https://ci.nii.ac.jp/author/' .. id .. '?l=en ' .. id .. ']' .. p.getCatForId( 'CINII' )
end

function p.bneLink( id )
	--P950's format regex: (XX|FF|a)\d{4,7}|(bima|bimo|bica|bis[eo]|bivi|Mise|Mimo|Mima)\d{10} (e.g. XX1234567)
	if not string.match( id, '^[XF][XF]%d%d%d%d%d?%d?%d?$' ) and
	   not string.match( id, '^a%d%d%d%d%d?%d?%d?$' ) and
	   not string.match( id, '^bi[mcsv][aoei]%d%d%d%d%d%d%d%d%d%d$' ) and
	   not string.match( id, '^Mi[sm][eoa]%d%d%d%d%d%d%d%d%d%d$' ) then
		return false
	end
	return '[http://catalogo.bne.es/uhtbin/authoritybrowse.cgi?action=display&authority_id=' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'BNE' )
end

function p.uscongressLink( id )
	--P1157's format regex: [A-Z]00[01]\d{3} (e.g. A000123)
	if not string.match( id, '^[A-Z]00[01]%d%d%d$' ) then
		return false
	end
	return '[http://bioguide.congress.gov/scripts/biodisplay.pl?index=' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'USCongress' )
end

function p.naraLink( id )
	--P1225's format regex: ^([1-9]\d{0,7})$ (e.g. 12345678)
	if not string.match( id, '^[1-9]%d?%d?%d?%d?%d?%d?%d?$' ) then
		return false
	end
	return '[https://catalog.archives.gov/id/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'NARA' )
end

function p.botanistLink( id )
	--P428's format regex: ('t )?(d')?(de )?(la )?(van (der )?)?(Ma?c)?(De)?(Di)?\p{Lu}?C?['\p{Ll}]*([-'. ]*(van )?(y )?(d[ae][nr]?[- ])?(Ma?c)?[\p{Lu}bht]?C?['\p{Ll}]*)*\.? ?f?\.? (e.g. L.)
	--not easily/meaningfully implementable in Lua's regex since "(this)?" is not allowed...
	if not mw.ustring.match( id, "^[%u%l%d%. '-]+$" ) then --better than nothing
		return false
	end
	local id2 = id:gsub(' +', '%%20')
	return '[http://www.ipni.org/ipni/advAuthorSearch.do?find_abbreviation=' .. id2 .. ' ' .. id .. ']' .. p.getCatForId( 'Botanist' )
end

function p.mgpLink( id )
	--P549's format regex: \d{1,6} (e.g. 123456)
	if not string.match( id, '^%d%d?%d?%d?%d?%d?$' ) then
		return false
	end
	return '[http://www.genealogy.ams.org/id.php?id=' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'MGP' )
end

function p.rslLink( id )
	--P947's format regex: \d{1,9} (e.g. 123456789)
	if not string.match( id, '^%d%d?%d?%d?%d?%d?%d?%d?%d?$' ) then
		return false
	end
	return '[http://aleph.rsl.ru/F?func=find-b&find_code=SYS&adjacent=Y&local_base=RSL11&request=' .. id .. '&CON_LNG=ENG ' .. id .. ']' .. p.getCatForId( 'RSL' )
end

function p.leonoreLink( id )
	--P640's format regex: LH/\d{1,4}/\d{1,3}|19800035/\d{1,4}/\d{1,5}(Bis)?|C/0/\d{1,2} (e.g. LH/2064/18)
	if not id:match( '^LH/%d%d?%d?%d?/%d%d?%d?$' ) and             --IDs from       LH/1/1 to         LH/2794/54 (legionaries)
	   not id:match( '^19800035/%d%d?%d?%d?/%d%d?%d?%d?%d?$' ) and --IDs from 19800035/1/1 to 19800035/385/51670 (legionnaires who died 1954-1977 & some who died < 1954)
	   not id:match( '^C/0/%d%d?$' ) then                          --IDs from        C/0/1 to             C/0/84 (84 famous legionaries)
		return false
	end
	return '[http://www.culture.gouv.fr/public/mistral/leonore_fr?ACTION=CHERCHER&FIELD_1=COTE&VALUE_1=' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'Léonore' )
end

function p.sbnLink( id )
	--P396's format regex: IT\\ICCU\\(\d{10}|\D\D[\D\d]\D\\\d{6}) (e.g. IT\ICCU\CFIV\000163)
	if not string.match( id, '^IT\\ICCU\\%d%d%d%d%d%d%d%d%d%d$' ) and
	   not string.match( id, '^IT\\ICCU\\%u%u[%u%d]%u\\%d%d%d%d%d%d$' ) then --legacy: %u used here instead of %D (but the faulty ID cat is empty, out of ~12k uses)
		return false
	end
	return '[http://opac.sbn.it/opacsbn/opac/iccu/scheda_authority.jsp?bid=' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'SBN' )
end

function p.nkcLink( id )
	--P691's format regex: [a-z]{2,4}[0-9]{2,14} (e.g. abcd12345678901234)
	if not string.match( id, '^[a-z][a-z][a-z]?[a-z]?%d%d%d?%d?%d?%d?%d?%d?%d?%d?%d?%d?%d?%d?$' ) then
		return false
	end
	return '[https://aleph.nkp.cz/F/?func=find-c&local_base=aut&ccl_term=ica=' .. id .. '&CON_LNG=ENG ' .. id .. ']' .. p.getCatForId( 'NKC' )
end

function p.nclLink( id )
	--P1048's format regex: \d+ (e.g. 1081436)
	if not string.match( id, '^%d+$' ) then
		return false
	end
	return '[http://aleweb.ncl.edu.tw/F/?func=accref&acc_sequence=' .. id .. '&CON_LNG=ENG ' .. id .. ']' .. p.getCatForId( 'NCL' )
end

function p.dilaLink( id )
    return '[http://authority.ddbc.edu.tw/person/search.php?aid=' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'DDBC' )
end

function p.ndlLink( id )
	--P349's format regex: 0?\d{8} (e.g. 012345678)
	if not string.match( id, '^0?%d%d%d%d%d%d%d%d$' ) then
		return false
	end
	return '[https://id.ndl.go.jp/auth/ndlna/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'NDL' )
end

function p.sudocLink( id )
	--P269's format regex: (\d{8}[\dX]|) (e.g. 026927608)
	if not string.match( id, '^%d%d%d%d%d%d%d%d[%dxX]$' ) then --legacy: allow lowercase 'x'
		return false
	end
	return '[https://www.idref.fr/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'SUDOC' )
end

function p.hdsLink( id )
	--P902's format regex: 50\d{3}|[1-4]\d{4}|[1-9]\d{0,3}| (e.g. 50123)
	if not string.match( id, '^50%d%d%d$' ) and
	   not string.match( id, '^[1-4]%d%d%d%d$' ) and
	   not string.match( id, '^[1-9]%d?%d?%d?$' ) then
		return false
	end
	return '[http://www.hls-dhs-dss.ch/textes/f/F' .. id .. '.php ' .. id .. ']' .. p.getCatForId( 'HDS' )
end

function p.lirLink( id )
	--P886's format regex: \d+ (e.g. 1)
	if not string.match( id, '^%d+$' ) then
		return false
	end
	return '[http://www.e-lir.ch/e-LIR___Lexicon.' .. id .. '.450.0.html ' .. id .. ']' .. p.getCatForId( 'LIR' )
end

function p.splitLccn( id )
	--P244's format regex: (n|nb|nr|no|ns|sh)([4-9][0-9]|00|20[0-1][0-9])[0-9]{6} (e.g. n78039510)
	if id:match( '^%l%l?%l?%d%d%d%d%d%d%d%d%d?%d?$' ) then
		id = id:gsub( '^(%l+)(%d+)(%d%d%d%d%d%d)$', '%1/%2/%3' )
	end
	if id:match( '^%l%l?%l?/%d%d%d?%d?/%d+$' ) then
		return mw.text.split( id, '/' )
	end
	return false
end

function p.append(str, c, length)
	while str:len() < length do
		str = c .. str
	end
	return str
end

function p.lccnLink( id )
	local parts = p.splitLccn( id ) --e.g. n78039510
	if not parts then
		return false
	end
	local lccnType = parts[1] ~= 'sh' and 'names' or 'subjects'
	id = parts[1] .. parts[2] .. p.append( parts[3], '0', 6 )
	return '[http://id.loc.gov/authorities/' .. lccnType .. '/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'LCCN' )
end

function p.mbaLink( id )
	--P434's format regex: [0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12} (e.g. 12345678-1234-1234-1234-1234567890AB)
	if not string.match( id, '^%x%x%x%x%x%x%x%x%-%x%x%x%x%-%x%x%x%x%-%x%x%x%x%-%x%x%x%x%x%x%x%x%x%x%x%x$' ) then
		return false
	end
	return '[https://musicbrainz.org/artist/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'MusicBrainz' )
end

--Returns the ISNI check digit isni must be a string where the 15 first elements are digits, e.g. 0000000066534145
function p.getIsniCheckDigit( isni )
	local total = 0
	for i = 1, 15 do
		local digit = isni:byte( i ) - 48 --Get integer value
		total = (total + digit) * 2
	end
	local remainder = total % 11
	local result = (12 - remainder) % 11
	if result == 10 then
		return "X"
	end
	return tostring( result )
end

--Validate ISNI (and ORCID) and retuns it as a 16 characters string or returns false if it's invalid
--See http://support.orcid.org/knowledgebase/articles/116780-structure-of-the-orcid-identifier
function p.validateIsni( id )
	--P213 (ISNI) format regex: [0-9]{4} [0-9]{4} [0-9]{4} [0-9]{3}[0-9X] (e.g. 0000-0000-6653-4145)
	--P496 (ORCID) format regex: 0000-000(1-[5-9]|2-[0-9]|3-[0-4])\d{3}-\d{3}[\dX] (e.g. 0000-0002-7398-5483)
	id = id:gsub( '[ %-]', '' ):upper()
	if not id:match( '^%d%d%d%d%d%d%d%d%d%d%d%d%d%d%d[%dX]$' ) then
		return false
	end
	if p.getIsniCheckDigit( id ) ~= string.char( id:byte( 16 ) ) then
		return false
	end
	return id
end

function p.isniLink( id )
	id = p.validateIsni( id ) --e.g. 0000-0000-6653-4145
	if not id then
		return false
	end
	return '[http://isni.org/isni/' .. id .. ' ' .. id:sub( 1, 4 ) .. ' ' .. id:sub( 5, 8 ) .. ' '  .. id:sub( 9, 12 ) .. ' '  .. id:sub( 13, 16 ) .. ']' .. p.getCatForId( 'ISNI' )
end

function p.orcidLink( id )
	id = p.validateIsni( id ) --e.g. 0000-0002-7398-5483
	if not id then
		return false
	end
	id = id:sub( 1, 4 ) .. '-' .. id:sub( 5, 8 ) .. '-'  .. id:sub( 9, 12 ) .. '-'  .. id:sub( 13, 16 )
	return '[https://orcid.org/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'ORCID' )
end

function p.gndLink( id )
	--P227's format regex: (1|1[01])\d{7}[0-9X]|[47]\d{6}-\d|[1-9]\d{0,7}-[0-9X]|3\d{7}[0-9X] (e.g. 4079154-3)
	if not string.match( id, '^1[01]?%d%d%d%d%d%d%d[0-9X]$' ) and
	   not string.match( id, '^[47]%d%d%d%d%d%d%-%d$' ) and
	   not string.match( id, '^[1-9]%d?%d?%d?%d?%d?%d?%d?%-[0-9X]$' ) and
	   not string.match( id, '^3%d%d%d%d%d%d%d[0-9X]$' ) then
		return false
	end
	return '[https://d-nb.info/gnd/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'GND' )
end

function p.selibrLink( id )
	--P906's format regex: [1-9]\d{4,5} (e.g. 123456)
	if not string.match( id, '^[1-9]%d%d%d%d%d?$' ) then
		return false
	end
	return '[https://libris.kb.se/auth/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'SELIBR' )
end

function p.bnfLink( id )
	--P268's format regex: \d{8}[0-9bcdfghjkmnpqrstvwxz] (e.g. 123456789)
	if not string.match( id, '^c?b?%d%d%d%d%d%d%d%d[0-9bcdfghjkmnpqrstvwxz]$' ) then
		return false
	end
	--Add cb prefix if it has been removed
	if not string.match( id, '^cb.+$' ) then
		id = 'cb' .. id
	end
	return '[http://catalogue.bnf.fr/ark:/12148/' .. id .. ' ' .. id .. '] [http://data.bnf.fr/ark:/12148/' .. id .. ' (data)]' .. p.getCatForId( 'BNF' )
end

function p.bpnLink( id )
	--P651's format regex: \d{8} (e.g. 12345678)
	if not string.match( id, '^%d%d%d%d%d%d%d%d$' ) then
		return false
	end
	return '[http://www.biografischportaal.nl/en/persoon/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'BPN' )
end

function p.ridLink( id )
	--P1053's format regex: [A-Z]-\d{4}-(19|20)\d\d (e.g. A-1234-1934)
	if not string.match( id, '^[A-Z]%-%d%d%d%d%-19%d%d$' ) and
	   not string.match( id, '^[A-Z]%-%d%d%d%d%-20%d%d$' ) then
		return false
	end
	return '[https://www.researcherid.com/rid/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'RID' )
end

function p.bibsysLink( id )
	--P1015's format regex: [1-9]\d* or [1-9](\d{0,8}|\d{12}) (e.g. 1234567890123)
	--TODO: follow up @ [[d:Property_talk:P1015#Discrepancy_between_the_2_regex_constraints|d:Property talk:P1015#Discrepancy between the 2 regex constraints]] or escalate/investigate
	if not string.match( id, '^[1-9]%d?%d?%d?%d?%d?%d?%d?%d?$' ) and
	   not string.match( id, '^[1-9]%d%d%d%d%d%d%d%d%d%d%d%d$' ) then
		return false
	end
	return '[https://authority.bibsys.no/authority/rest/authorities/html/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'BIBSYS' )
end

function p.ulanLink( id )
	--P245's format regex: 500\d{6} (e.g. 500123456)
	if not string.match( id, '^500%d%d%d%d%d%d$' ) then
		return false
	end
	return '[https://www.getty.edu/vow/ULANFullDisplay?find=%20&role=%20&nation=%20&subjectid=' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'ULAN' )
end

function p.nlaLink( id )
	--P409's format regex: [1-9][0-9]{0,11} (e.g. 123456789012)
	if not string.match( id, '^[1-9]%d?%d?%d?%d?%d?%d?%d?%d?%d?%d?%d?$' ) then
		return false
	end
	return '[https://nla.gov.au/anbd.aut-an' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'NLA' )
end

function p.rkdartistsLink( id )
	--P650's format regex: [1-9]\d{0,5} (e.g. 123456)
	if not string.match( id, '^[1-9]%d?%d?%d?%d?%d?$' ) then
		return false
	end
	return '[https://rkd.nl/en/explore/artists/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'RKDartists' )
end

function p.snacLink( id )
	--P3430's format regex: \d*[A-Za-z][0-9A-Za-z]* (e.g. A)
	if not string.match( id, '^%d*[A-Za-z][0-9A-Za-z]*$' ) then
		return false
	end
	return '[http://socialarchive.iath.virginia.edu/ark:/99166/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'SNAC-ID' )
end

function p.dblpLink( id )
	--P2456's format regex: \d{2,3} /\d+(-\d+)?|[a-z] /[a-zA-Z][0-9A-Za-z]*(-\d+)? (e.g. 123/123)
	if not string.match( id, '^%d%d%d?/%d+$' ) and
	   not string.match( id, '^%d%d%d?/%d+%-%d+$' ) and
	   not string.match( id, '^[a-z]/[a-zA-Z][0-9A-Za-z]*$' ) and
	   not string.match( id, '^[a-z]/[a-zA-Z][0-9A-Za-z]*%-%d+$' ) then
		return false
	end
	return '[https://dblp.org/pid/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'DBLP' )
end

function p.acmLink( id )
	--P864's format regex: \d{11} (e.g. 12345678901)
	if not string.match( id, '^%d%d%d%d%d%d%d%d%d%d%d$' ) then
		return false
	end
	return '[https://dl.acm.org/author_page.cfm?id=' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'ACM-DL' )
end

function p.autoresuyLink( id )
	--P2558's format regex: [1-9]\d{0,4} (e.g. 12345)
	if not string.match( id, '^[1-9]%d?%d?%d?%d?$' ) then
		return false
	end
	return '[http://autores.uy/autor/' .. id .. ' ' .. id .. ']' ..  p.getCatForId( 'autores.uy' )
end

function p.picLink( id )
	--P2750's format regex: [1-9]\d* (e.g. 1)
	if not string.match( id, '^[1-9]%d*$' ) then
		return false
	end
	return '[https://pic.nypl.org/constituents/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'PIC' )
end

function p.bildLink( id )
	--P2092's format regex: \d+ (e.g. 1)
	if not string.match( id, '^%d+$' ) then
		return false
	end
	return '[https://www.bildindex.de/document/obj' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'Bildindex' )
end

function p.jocondeLink( id )
	--P347's format regex: [\-0-9A-Za-z]{11} (e.g. 12345678901)
	local regex = '^' .. string.rep('[%-0-9A-Za-z]', 11) .. '$'
	if not string.match( id, regex ) then
		return false
	end
	return '[http://www2.culture.gouv.fr/public/mistral/joconde_fr?ACTION=CHERCHER&FIELD_1=REF&VALUE_1=' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'Joconde' )
end

function p.rkdidLink( id )
	--P350's format regex: [1-9]\d{0,5} (e.g. 123456)
	if not string.match( id, '^[1-9]%d?%d?%d?%d?%d?$' ) then
		return false
	end
	return '[https://rkd.nl/nl/explore/images/' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'RKDID' )
end

function p.balatLink( id )
	--P3293's format regex: \d+ (e.g. 1)
	if not string.match( id, '^%d+$' ) then
		return false
	end
	return '[http://balat.kikirpa.be/object/104257' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'BALaT' )
end

function p.lnbLink( id )
	--P1368's format regex: \d{9} (e.g. 123456789)
	if not string.match( id, '^%d%d%d%d%d%d%d%d%d$' ) then
		return false
	end
	return '[https://kopkatalogs.lv/F?func=direct&local_base=lnc10&doc_number=' .. id .. '&P_CON_LNG=ENG ' .. id .. ']' .. p.getCatForId( 'LNB' )
end

function p.nskLink( id )
	--P1375's format regex: \d{9} (e.g. 123456789)
	if not string.match( id, '^%d%d%d%d%d%d%d%d%d$' ) then
		return false
	end
	return '[http://katalog.nsk.hr/F/?func=direct&doc_number=' .. id .. '&local_base=nsk10 ' .. id .. ']' .. p.getCatForId( 'NSK' )
end

function p.calisLink( id )
    return '[http://opac.calis.edu.cn/aopac/ajsp/detail.jsp?actionfrom=1&actl=CAL++' .. id .. ' ' .. id .. ']' .. p.getCatForId( 'CALIS' )
end

function p.hkcanLink( id )
	--P5909's format regex: [1-9][0-9]* (e.g. 123456789)
	if not string.match( id, '^[1-9][0-9]*$' ) then
		return false
	end
	return '[http://www.hkcan.net/hkcanopac/servlet/view/zh_TW?action=view&startPos=' .. id .. ' ' .. id .. ']' ..  p.getCatForId( 'HKCAN' )
end

function p.nlcLink( id )
    return '[http://opac.nlc.cn/F/?func=accref&acc_sequence=' .. id .. ' '..id..']' .. p.getCatForId( 'NLC' )
end

function p.aatLink( id )
    return '[http://vocab.getty.edu/page/aat/' .. id .. ' '..id..']' .. p.getCatForId( 'AAT' )
end

function p.fastLink( id )
    return '[//experimental.worldcat.org/fast/' .. id .. ' '..id..']' .. p.getCatForId( 'FAST' )
end

function p.nnlLink( id )
    return '[http://aleph.nli.org.il/F/?func=find-b&local_base=NNL10&find_code=SYS&con_lng=eng&request=' .. id .. ' '..id..']' .. p.getCatForId( 'NNL' )
end

function p.nlpLink( id )
    return '[http://mak.bn.org.pl/cgi-bin/KHW/makwww.exe?BM=01&IM=04&NU=01&WI=' .. id .. ' '..id..']' .. p.getCatForId( 'NLP' )
end

function p.lacLink( id )
    return '[https://www.collectionscanada.gc.ca/canadiana-authorities/index/view?index_name=cdnAutNbr&search_text=$1&page=1&cdnAutNbr=' .. id .. ' '..id..']' .. p.getCatForId( 'LAC' )
end

function p.ntaLink( id )
    return '[http://data.bibliotheken.nl/id/thes/p' .. id .. ' '..id..']' .. p.getCatForId( 'NTA' )
end

function p.bnaLink( id )
    return '[http://catalogo.bn.gov.ar/F/?func=direct&local_base=BNA10&doc_number=' .. id .. ' '..id..']' .. p.getCatForId( 'BNA' )
end

function p.cbdbLink( id )
    return '[https://cbdb.fas.harvard.edu/cbdbapi/person.php?id=' .. id .. ' '..id..']' .. p.getCatForId( 'CBDB' )
end

function p.conorLink( id )
    return '[http://www.cobiss.si/scripts/cobiss?command=DISPLAY&base=CONOR&rid=' .. id .. ' '..id..']' .. p.getCatForId( 'CONOR' )
end

function p.bncLink( id )
    return '[http://www.bncatalogo.cl/F?func=direct&local_base=red10&doc_number=' .. id .. ' '..id..']' .. p.getCatForId( 'BNC' )
end

function p.scopusLink( id )
    return '[https://www.scopus.com/authid/detail.uri?authorId=' .. id .. ' '..id..']' .. p.getCatForId( 'Scopus' )
end

function p.atclLink( id )
    return '[http://www.victorianresearch.org/atcl/show_author.php?aid=' .. id .. ' '..id..']' .. p.getCatForId( 'AtCL' )
end

--[[==========================================================================|==========================================================================]]
--[[Wikidata,_navigation_bar,_and_documentation_functions|Wikidata, navigation bar, and documentation functions]]
--[[==========================================================================|==========================================================================]]

function p.getIdsFromWikidata( itemId, property )
	local ids = {}
	local statements = mw.wikibase.getBestStatements( itemId, property )
	if statements then
		for _, statement in ipairs( statements ) do
			if statement.mainsnak.datavalue then
				table.insert( ids, statement.mainsnak.datavalue.value )
			end
		end
	end
	return ids
end

function p.matchesWikidataRequirements( itemId, reqs )
	for _, group in ipairs( reqs ) do
		local property = 'P' .. group[1]
		local qid = group[2]
		local statements = mw.wikibase.getBestStatements( itemId, property )
		if statements then
			for _, statement in ipairs( statements ) do
				if statement.mainsnak.datavalue then
					if statement.mainsnak.datavalue.value['numeric-id'] == qid then
						return true
					end
				end
			end
		end
	end
	return false
end

function p.createRow( id, label, rawValue, link, withUid )
	if link then
		if withUid then
			return '*<span class="nowrap">' .. label .. ' <span class="uid">' .. link .. '</span></span>\n'
		end
		return '*<span class="nowrap">' .. label .. ' ' .. link .. '</span>\n'
	end

	local catName = '包含错误规范控制信息的维基百科条目 (' .. id .. ')'
	return '* <span class="error">' .. id .. '编号' .. rawValue .. '不正确。</span>[[Category:'_.._catName_.._'|Category:' .. catName .. ']]' .. p.redCatLink(catName) .. '\n'
end

-- Creates a human-readable standalone wikitable version of p.conf, and tracking categories with page counts, for use in the documentation
function p.docConfTable( frame )
	local wikiTable = '{| class="wikitable sortable"\n' ..
					  '! rowspan=2 | 参数\n' ..
					  '! rowspan=2 | 名称\n' ..
					  '! rowspan=2; data-sort-type=number | 维基数据属性值\n' ..
					  '! colspan=4 | 跟踪分类与页面计数\n' ..
					  '|-\n' ..
					  '! 条目\n' ..
					  '! 用户页\n' ..
					  '! 其他页面\n' ..
					  '! 错误ID\n' ..
					  '|-\n'
					  
	local lang = mw.getContentLanguage()
	for _, conf in pairs( p.conf ) do
		local param, link, pid = conf[1], conf[2], conf[3]
		if param == 'MBA' then param = 'MusicBrainz' end --it's weird; 'MusicBrainz' for cats only
		local args = { id = 'f', pid }
		local wpl = frame:expandTemplate{ title = 'Wikidata property link', args = args }
		local articleCat = '包含'..param..'标识符的维基百科条目'
		local userCat =    '包含'..param..'标识符的用户页'
		local miscCat =    '包含'..param..'标识符的其他页面'
		local faultyCat =  '包含错误规范控制信息的维基百科条目 ('..param..')'
		local articleCount = lang:formatNum( mw.site.stats.pagesInCategory(articleCat, 'pages') )
		local userCount =    lang:formatNum( mw.site.stats.pagesInCategory(userCat, 'pages') )
		local miscCount =    lang:formatNum( mw.site.stats.pagesInCategory(miscCat, 'pages') )
		local faultyCount =  lang:formatNum( mw.site.stats.pagesInCategory(faultyCat, 'pages') )
		if param == 'MusicBrainz' then param = 'MBA' end --it's weird; 'MBA' for param name only
		wikiTable = wikiTable..'\n'..
					'|-\n'..
					'||'..param..
					'||'..link..
					'||data-sort-value='..pid..'|'..wpl..
					'||style="text-align: right;"|[[:Category:'..articleCat..'|'..articleCount..']]'..
					'||style="text-align: right;"|[[:Category:'..___userCat..'|'..   userCount..']]'..
					'||style="text-align: right;"|[[:Category:'..___miscCat..'|'..   miscCount..']]'..
					'||style="text-align: right;"|[[:Category:'.._faultyCat..'|'.. faultyCount..']]'
	end
	return wikiTable .. '\n|}'
end

--[[==========================================================================|==========================================================================]]
--[[Main|Main]]
--[[==========================================================================|==========================================================================]]

-- Check that the Wikidata item has this property-->value before adding it
local reqs = {}

-- Parameter format: { name of the parameter, label, propertyId in Wikidata, formatting function }
p.conf = {
	{ 'AAT', '[[藝術與建築索引典|AAT]]', 1014, p.aatLink },	
	{ 'ACM-DL', '[[计算机协会数字图书馆|ACM DL]]', 864, p.acmLink },
	{ 'AtCL', '[[d:Q18228305|AtCL]]', 1564, p.atclLink },	
	{ 'autores.uy', '[[autores.uy|autores.uy]]', 2558, p.autoresuyLink },
	{ 'BALaT', '[[BALaT|BALaT]]', 3293, p.balatLink },
	{ 'BIBSYS', '[[BIBSYS|BIBSYS]]', 1015, p.bibsysLink },
	{ 'Bildindex', '[[Marburg_Picture_Index|Bildindex]]', 2092, p.bildLink },
    { 'BNA', '[[阿根廷国家图书馆|BNA]]', 3788, p.bnaLink },	
    { 'BNC', '[[d:Q19896851|BNC]]', 1890, p.bncLink },	    
    { 'BNE', '[[西班牙国家图书馆|BNE]]', 950, p.bneLink },
	{ 'BNF', '[[法国国家图书馆|BNF]]', 268, p.bnfLink },
    { 'Botanist', '[[植物学作者引证|Botanist]]', 428, p.botanistLink },
    { 'BPN', '[[Biografisch_Portaal|BPN]]', 651, p.bpnLink },
    { 'CALIS', '[[中国高等教育文献保障系统|CALIS]]', 270, p.calisLink },
    { 'CBDB', '[[中国历代人物传记资料库|CBDB]]', 497, p.cbdbLink },    
    { 'CINII', '[[CiNii|CiNii]]', 271, p.ciniiLink },
     { 'CONOR', '[[CONOR|CONOR]]', 1280, p.conorLink },   
	{ 'DBLP', '[[DBLP|DBLP]]', 2456, p.dblpLink },
    { 'DDBC', '[[法鼓文理學院|DILA]]', 1187, p.dilaLink }, --仅人物码，地方码为 1188
    { 'FAST', '[[d:Property:P2163|FAST]]', 2163, p.fastLink },    
    { 'GND', '[[整合规范文档|GND]]', 227, p.gndLink },
    { 'HDS', '[[瑞士歷史辭典|HDS]]', 902, p.hdsLink }, 
    { 'HKCAN', '[[香港中文名稱規範數據庫|HKCAN]]', 5909, p.hkcanLink },
    { 'ISNI', '[[國際標準名稱識別碼|ISNI]]', 213, p.isniLink },	
	{ 'Joconde', '[[Joconde|Joconde]]' , 347, p.jocondeLink },
    { 'KULTURNAV', '[[KulturNav|KulturNav]]', 1248, p.kulturnavLink },
    { 'LAC', '[[加拿大国家图书馆暨档案馆|LAC]]', 1670, p.lacLink },   
	{ 'LCCN', '[[美国国会图书馆控制号|LCCN]]', 244, p.lccnLink },
	{ 'LIR', '[[Lexicon_Istoric_Retic|LIR]]', 886, p.lirLink },
	{ 'LNB', '[[拉托维亚国家图书馆|LNB]]', 1368, p.lnbLink },
	{ 'Léonore', '[[Base_Léonore|Base Léonore]]', 640, p.leonoreLink }, 
	{ 'MBA', '[[MusicBrainz|MusicBrainz]]', 434, p.mbaLink }, 
	{ 'MGP', '[[數學譜系計畫|MGP]]', 549, p.mgpLink },
	{ 'NARA', '[[国家档案和记录管理局|NARA]]', 1225, p.naraLink },
	{ 'NCL', '[[中華民國國家圖書館|NCL]]', 1048, p.nclLink }, 
	{ 'NDL', '[[國立國會圖書館|NDL]]', 349, p.ndlLink },
	{ 'NKC', '[[捷克国家图书馆|NKC]]', 691, p.nkcLink },
	{ 'NLA', '[[澳洲國家圖書館|NLA]]', 409, p.nlaLink },
	{ 'NLC', '[[中国国家图书馆|NLC]]', 1213,  p.nlcLink },
	{ 'NLP', '[[波蘭國家圖書館|NLP]]', 1695,  p.nlpLink },	
	{ 'NNL', '[[以色列国家图书馆|NNL]]', 949,  p.nnlLink },	
	{ 'NSK', '[[萨格勒布国家和大学图书馆|NSK]]', 1375, p.nskLink },
	{ 'NTA', '[[荷蘭皇家圖書館|NTA]]', 1375, p.ntaLink },	
	{ 'ORCID', '[[ORCID|ORCID]]', 496, p.orcidLink },
	{ 'PIC', '[[:d:Q23892012|PIC]]', 2750, p.picLink },
	{ 'RID', '[[ResearcherID|ResearcherID]]', 1053, p.ridLink },
	{ 'RKDartists', '[[荷兰艺术历史学院|RKD]]', 650, p.rkdartistsLink },
	{ 'RKDID', '[[:d:Q17299580|RKDimages ID]]', 350, p.rkdidLink },
	{ 'RSL', '[[俄罗斯国立图书馆|RSL]]', 947, p.rslLink },
	{ 'SBN', '[[意大利图书馆联合目录中央研究所|ICCU]]', 396, p.sbnLink },     
	{ 'Scopus', '[[Scopus|Scopus]]', 1153, p.scopusLink },     	
	{ 'SELIBR', '[[LIBRIS|SELIBR]]', 906, p.selibrLink },
	{ 'SIKART', '[[SIKART|SIKART]]', 781, p.sikartLink },
	{ 'SNAC-ID', '[[SNAC|SNAC]]', 3430, p.snacLink },
    { 'SUDOC', '[[大學文檔系統|SUDOC]]', 269, p.sudocLink },  	
    { 'TLS', '[[瑞士剧场词典|TLS]]', 1362, p.tlsLink },	
    { 'ULAN', '[[艺术家联合名录|ULAN]]', 245, p.ulanLink },
    { 'USCongress', '[[美國國會國家人物傳記大辭典|美國國會國家人物傳記大辭典]]', 1157, p.uscongressLink },	
    { 'VIAF', '[[虚拟国际规范文档|VIAF]]', 214, p.viafLink },
}

-- Legitimate aliases to p.conf, for convenience
-- Format: { alias, parameter name in p.conf }
p.aliases = {
	{ 'RLS', 'RSL' },
	{ 'MusicBrainz', 'MBA' },
	{ 'Leonore', 'Léonore' },
}

-- Deprecated aliases to p.conf, which also get assigned to a tracking cat
-- Format: { deprecated parameter name, replacement parameter name in p.conf }
p.deprecated = {
	{ 'GKD', 'GND' },
	{ 'PND', 'GND' },
	{ 'SWD', 'GND' },
	{ 'NARA-organization', 'NARA' },
	{ 'NARA-person', 'NARA' },
}

function p.authorityControl( frame )
	local resolve = require( "Module:ResolveEntityId" )
	local title = mw.title.getCurrentTitle()
	local namespace = title.namespace
	local talkspace = (mw.site.talkNamespaces[namespace] ~= nil)
	local testcases = (string.sub(title.subpageText,1,9) == 'testcases')
	local parentArgs = frame:getParent().args
	local elements = {} --create/insert rows later
	local suppressedIdCat = ''
	local deprecatedIdCat = ''

	--Redirect aliases to proper parameter names
	for _, a in pairs( p.aliases ) do
		local alias, param = a[1], a[2]
		if (parentArgs[param] == nil or parentArgs[param] == '') and parentArgs[alias] then
			parentArgs[param] = parentArgs[alias]
		end
	end

	--Redirect deprecated parameters to proper parameter names, and assign tracking cat
	for _, d in pairs( p.deprecated ) do
		local dep, param = d[1], d[2]
		if (parentArgs[param] == nil or parentArgs[param] == '') and parentArgs[dep] then
			parentArgs[param] = parentArgs[dep]
			if namespace == 0 then
				deprecatedIdCat = '[[Category:包含已弃用规范控制信息的维基百科条目|'..dep..']]'
			end
		end
	end

	--Use QID= parameter for testing/example purposes only
	local itemId = nil
	if testcases or talkspace then
		if parentArgs['QID'] then
			itemId = 'Q' .. mw.ustring.gsub(parentArgs['QID'], '^[Qq]', '')
			itemId = resolve._entityid(frame, itemId) --nil if unresolvable
		end
	else
		itemId = mw.wikibase.getEntityIdForCurrentPage()
	end

	--Wikidata fallback if requested
	if itemId then
		for _, params in ipairs( p.conf ) do
			if params[3] > 0 then
				local val = parentArgs[params[1]]
				if val == nil or val == '' then
					local canUseWikidata = nil
					if reqs[params[1]] then
						canUseWikidata = p.matchesWikidataRequirements( itemId, reqs[params[1]] )
					else
						canUseWikidata = true
					end
					if canUseWikidata then
						local wikidataIds = p.getIdsFromWikidata( itemId, 'P' .. params[3] )
						if wikidataIds[1] then
							if val == '' and (namespace == 0 or testcases) then
								suppressedIdCat = '[[Category:包含已废止规范控制信息的维基百科条目|' .. params[1] .. ']]'
							else
								parentArgs[params[1]] = wikidataIds[1]
	end	end	end	end	end	end	end

	--Worldcat
	if parentArgs['WORLDCATID'] and parentArgs['WORLDCATID'] ~= '' then
		table.insert( elements, p.createRow( 'WORLDCATID', '', parentArgs['WORLDCATID'], '[https://www.worldcat.org/identities/' .. parentArgs['WORLDCATID'] .. ' WorldCat Identities]', false ) ) --Validation?
	elseif parentArgs['VIAF'] and string.match( parentArgs['VIAF'], '^%d+$' ) then -- Hackishly copy the validation code; this should go away when we move to using P1793 and P1630
		table.insert( elements, p.createRow( 'VIAF', '', parentArgs['VIAF'], '[https://www.worldcat.org/identities/containsVIAFID/' .. parentArgs['VIAF'] .. ' WorldCat Identities]', false ) )
	elseif parentArgs['LCCN'] and parentArgs['LCCN'] ~= '' then
		local lccnParts = p.splitLccn( parentArgs['LCCN'] )
		if lccnParts and lccnParts[1] ~= 'sh' then
			table.insert( elements, p.createRow( 'LCCN', '', parentArgs['LCCN'], '[https://www.worldcat.org/identities/lccn-' .. lccnParts[1] .. lccnParts[2] .. '-' .. lccnParts[3] .. ' WorldCat Identities]', false ) )
		end
	end

--Configured rows
	local rct = 0
	for _, params in ipairs( p.conf ) do
		local val = parentArgs[params[1]]
		if val and val ~= '' then
			table.insert( elements, p.createRow( params[1], params[2] .. ':', val, params[4](val), true ) ) 
			rct = rct + 1
		end
	end
	local Navbox = require('Module:Navbox')
	local elementsCat = ''
	if rct > 13 then
    	local catName = '包含' .. rct .. '元素的规范控制'
    	elementsCat  = '[[Category:'_.._catName_.._'|Category:' .. catName .. ']]' .. p.redCatLink(catName)
	end

	local outString = ''
	if #elements > 0 then
		local args = {}
		if testcases and itemId then args = { qid = itemId } end --expensive
		-- local pencil = frame:expandTemplate{ title = 'EditAtWikidata', args = args} 需要解决换行问题
		outString = Navbox._navbox( {
			name  = '规范控制',
			bodyclass = 'hlist',
			group1 = '[[Help:规范控制|规范控制]]',-- .. pencil,
			list1 = table.concat( elements )
			} )
		local auxCats = elementsCat .. suppressedIdCat .. deprecatedIdCat
		if testcases then
			auxCats = mw.ustring.gsub(auxCats, '(%[%[)(Category)', '%1:%2') --for easier checking
		end
		outString = outString .. auxCats
		if namespace ~= 0 then
			outString = mw.ustring.gsub(outString, '(%[%[)(Category:Wikipedia articles)', '%1:%2') --by definition
		end
	end

	return outString
end

return p