--[=[

Lua support for the {{lang}}, {{lang-xx}}, and {{transl}} templates and replacement of various supporting templates. 

]=]

require('Module:No globals');
local p = {};

local initial_style_state;														-- set by lang_xx_inherit() and lang_xx_italic()

local getArgs = require ('Module:Arguments').getArgs;
local lang_name_table = mw.loadData ('Module:Language/name/data');

local synonym_table = mw.loadData ('Module:Lang/ISO 639 synonyms');				-- ISO 639-2/639-2T code translation to 639-1 code

local lang_data =  mw.loadData ('Module:Lang/data');							-- language name override and transliteration tool-tip tables

local namespace = mw.title.getCurrentTitle().namespace;							-- used for categorization

local maint_cats = {};															-- maintenance categories go here
local maint_msgs = {};															-- and their messages go here

local function page_exists (title)
    -- This function implements #ifexist
    local noError, titleObject = pcall (mw.title.new, title)
    if not noError then
        return false
    else
        if titleObject then
            return titleObject.exists
        else
            return false
        end
    end
end

--[[--------------------------< I S _ S E T >------------------------------------------------------------------

Returns true if argument is set; false otherwise. Argument is 'set' when it exists (not nil) or when it is not an empty string.

]]

local function is_set( var )
	return not (var == nil or var == '');
end


--[[--------------------------< I S _ L A T N >----------------------------------------------------------------

Returns true if all of text argument is written using Latn script for letters, numbers and punctuationset; false else.

For the purposes of this function, Latn script is characters less control characters from these Unicode 10.0 Character Code Charts:
	[http://www.unicode.org/charts/PDF/U0000.pdf C0 Controls and Basic Latin] U+0020–U+007E (20 - 7E) + see note about <poem>...</poem> support
	[http://www.unicode.org/charts/PDF/U0080.pdf C1 Controls and Latin-1 Supplement] U+00A0-U+00AC, U+00C0–U+00FF (C2 A0 - C2 AC, C3 80 - C3 BF: \194\160-\194\172)
	[http://www.unicode.org/charts/PDF/U0100.pdf Latin Extended-A] U+0100–U+017F (C4 80 - C5 BF)
	[http://www.unicode.org/charts/PDF/U0180.pdf Latin Extended-B] U+0180–U+024F (C6 80 - C9 8F)
	[http://www.unicode.org/charts/PDF/U1E00.pdf Latin Extended Additional] U+1E00-U+1EFF (E1 B8 80 - E1 BB BF)
	[http://www.unicode.org/charts/PDF/U2C60.pdf Latin Extended-C] U+2C60–U+2C7F (E2 B1 A0 - E2 B1 BF)
	[http://www.unicode.org/charts/PDF/UA720.pdf Latin Extended-D] U+A720-U+A7FF (EA 9C A0 - EA 9F BF)
	[http://www.unicode.org/charts/PDF/UAB30.pdf Latin Extended-E] U+AB30-U+AB6F (EA AC B0 - EA AD AF)
	[http://www.unicode.org/charts/PDF/UFB00.pdf Alphabetic Presentaion Forms] U+FB00-U+FB06 (EF AC 80 - EF AC 86)
	[http://www.unicode.org/charts/PDF/UFF00.pdf Halfwidth and Fullwidth Forms] U+FF01-U+FF3C (EF BC 81 EF BC BC)

does not include:
	[http://www.unicode.org/charts/PDF/U1D00.pdf Phonetic Extensions] U+1D00-U+1D7F (E1 B4 80 - E1 B5 BF)
	[http://www.unicode.org/charts/PDF/U0250.pdf IPA Extensions] U+0250-U+02AF (C9 90 - CA AF)
	[http://www.unicode.org/charts/PDF/U1D80.pdf Phonetic Extensions Supplement] U+1D80-U+1DBF (E1 B6 80 - E1 B6 BF)

{{lang}} is used inside <poem>...</poem> tags for song lyrics, poetry, etc.  <poem>...</poem> replaces newlines with
poem stripmarkers.  These have the form:
	?'"`UNIQ--poem-67--QINU`"'?
where the '?' character is actually the delete character (U+007F, \127).  Including the '\n' (U+0010) and 'del' (U+007F)
characters in the latn character table allows {{lang}} to auto-italicize text within <poem>...</poem> tags.

]]

function p.is_latn (text)
	local latn = table.concat (
		{
		'[',																	-- this is a set so include opening bracket
		'\n\32-\127',															-- C0 Controls and Basic Latin			U+0020–U+007E (20 - 7E) + (U+0010 and U+007F <poem>...</poem> support)
		'\194\160-\194\172',													-- C1 Controls and Latin-1 Supplement	U+00A0-U+00AC (C2 A0 - C2 AC)
		'\195\128-\195\191',													-- (skip shy)							U+00C0–U+00FF (C3 80 - C3 BF)
		'\196\128-\197\191',													-- Latin Extended-A						U+0100–U+017F (C4 80 - C5 BF)
		'\198\128-\201\143',													-- Latin Extended-B						U+0180–U+024F (C6 80 - C9 8F)
		'\225\184\128-\225\187\191',											-- Latin Extended Additional			U+1E00-U+1EFF (E1 B8 80 - E1 BB BF)
		'\226\177\160-\226\177\191',											-- Latin Extended-C						U+2C60–U+2C7F (E2 B1 A0 - E2 B1 BF)
		'\234\156\160-\234\159\191',											-- Latin Extended-D						U+A720-U+A7FF (EA 9C A0 - EA 9F BF)
		'\234\172\176-\234\173\175',											-- Latin Extended-E						U+AB30-U+AB6F (EA AC B0 - EA AD AF)
		'\239\172\128-\239\172\134',											-- Alphabetic Presentaion Forms			U+FB00-U+FB06 (EF AC 80 - EF AC 86)
		'\239\188\129-\239\188\188',											-- Halfwidth and Fullwidth Forms		U+FF01-U+FF3C (EF BC 81 - EF BC BC)
		'–',																	-- ndash
		'—',																	-- mdash
		'«', '»',																-- guillemets commonly used in several 'Latn' languages
		']',																	-- close the set
		});

	text = mw.text.decode (text, true);											-- replace numeric and named html entities with their unicode characters
	text = mw.ustring.gsub (text, '%[%[[^|]+]]+)%]%]', '%1');				-- remove the link and markup from complex wikilink in case interwiki to non-Latn wikipedia
	return not is_set (mw.ustring.gsub (text, latn, ''));						-- replace all latn characters with empty space; if result is all empty space, text is latn
end


--[[--------------------------< I N V E R T  _ I T A L I C S >-------------------------------------------------

This function attempts to invert the italic markup a args.text by adding/removing leading/trailing italic markup
in args.text.  Like |italic=unset, |italic=invert disables automatic italic markup.  Individual leading/trailing
apostrophes are converted to their html numeric entity equivalent so that the new italic markup doesn't become
bold markup inadvertently.

Leading and trailing wiki markup is extracted from args.text into separate table elements.  Addition, removal,
replacement of wiki markup is handled by a string.gsub() replacement table operating only on these separate elements.
In the string.gsub() matching pattern, '.*' matches empty string as well as the three expected wiki markup patterns.

This function expects that markup in args.text is complete and correct; if it is not, oddness may result.

]]

local function invert_italics (source)
	local invert_pattern_table = {												-- leading/trailing markup add/remove/replace patterns
		[""]="\'\'",															-- empty string becomes italic markup
		["\'\'"]="",															-- italic markup becomes empty string
		["\'\'\'"]="\'\'\'\'\'",												-- bold becomes bold italic
		["\'\'\'\'\'"]="\'\'\'",												-- bold italic become bold
		};
	local seg = {};

	source = source:gsub ("%f[\']\'%f[^\']", '&');							-- protect single quote marks from being interpreted as bold markup

	seg[1] = source:match ('^(\'\'+%f[^\']).+') or '';							-- get leading markup, if any; ignore single quote
	seg[3] = source:match ('.+(%f[\']\'\'+)$') or '';							-- get trailing markup, if any; ignore single quote

	if '' ~= seg[1] and '' ~= seg[3] then										-- extract the 'text' 
		seg[2] = source:match ('^\'\'+%f[^\'](.+)%f[\']\'\'+$')					-- from between leading and trailing markup
	elseif '' ~= seg[1] then
		seg[2] = source:match ('^\'\'+%f[^\'](.+)')								-- following leading markup
	elseif '' ~= seg[3] then
		seg[2] = source:match ('(.+)%f[\']\'\'+$')								-- preceding trailing markup
	else
		seg[2] = source															-- when there is no markup
	end

	seg[1] = seg[1]:gsub (".*", invert_pattern_table, 1);						-- replace leading markup according to pattern table
	seg[3] = seg[3]:gsub (".*", invert_pattern_table, 1);						-- replace leading markup according to pattern table

	return table.concat (seg);													-- put it all back together and done
end


--[[--------------------------< V A L I D A T E _ I T A L I C >------------------------------------------------

validates |italic= or |italics= assigned values.

When |italic= is set and has an acceptible assigned value, return the matching css font-style property value or,
for the special case 'default', return nil.

When |italic= is not set, or has an unacceptible assigned value, return nil and a nil error message.

When both |italic= and |italics= are set, returns nil and a 'conflicting' error message.

The return value nil causes the calling lang, lang_xx, or transl function to set args.italic according to the template's
defined default ('inherit' for {{lang}}, 'inherit' or 'italic' for {{lang-xx}} depending on
the individual template's requirements, 'italic' for {{transl}}) or to the value appropriate to |script=, if set ({{lang}}
and {{lang-xx}} only).

Accepted values and the values that this function returns are are:
	nil		-	when |italic= absent or not set; returns nil
	default	-	for completeness, should rarely if ever be used; returns nil
	yes		-	force args.text to be rendered in italic font; returns 'italic'
	no		-	force args.text to be rendered in normal font; returns 'normal'
	unset	-	disables font control so that font-style applied to text is dictated by markup inside or outside the template; returns 'inherit'
	invert	-	disables font control so that font-style applied to text is dictated by markup outside or inverted inside the template; returns 'invert'

]]

local function validate_italic (italic, italics)
	local properties = {['yes'] = 'italic', ['no'] = 'normal', ['unset'] = 'inherit', ['invert'] = 'invert', ['default'] = nil};

	if italic and italics then													-- return nil and an error message if both are set 
		return nil, '冲突：|italic= 和 |italics=';
	end
	
	return properties[italic or italics], nil;									-- return an appropriate value and a nil error message
end


--[[--------------------------< I N _ A R R A Y >--------------------------------------------------------------

Whether needle is in haystack

]]

local function in_array( needle, haystack )
	if needle == nil then
		return false;
	end
	for n,v in ipairs( haystack ) do
		if v == needle then
			return n;
		end
	end
	return false;
end


--[[--------------------------< F O R M A T _ I E T F _ T A G >------------------------------------------------

prettify ietf tags to use recommended subtag formats:
	code: lower case
	script: sentence case
	region: upper case
	variant: lower case

]]

local function format_ietf_tag (code, script, region, variant)
	local out = {};

	table.insert (out, code:lower());
	if is_set (script) then
		script = script:lower():gsub ('^%a', string.upper);
		table.insert (out, script);
	end

	if is_set (region) then
		table.insert (out, region:upper());
	end
	
	if is_set (variant) then
		table.insert (out, variant:lower());
	end
	
	return table.concat (out, '-');
end


--[[--------------------------< G E T _ I E T F _ P A R T S >--------------------------------------------------

extracts and returns IETF language tag parts:
	primary language subtag (required) - 2 or 3 character IANA language code
	script subtag - four character IANA script code
	region subtag - two-letter or three digit IANA region code
	variant subtag - four digit or 5-8 alnum variant code
	private subtag - x- followed by 1-8 alnum private code; only supported with the primary language tag

in any one of these forms
	lang					lang-variant
	lang-script				lang-script-variant
	lang-region				lang-region-variant
	lang-script-region		lang-script-region-variant
	lang-x-private	
	
each of lang, script, region, variant, and private, when used, must be valid

Languages with both two- and three-character code synonyms are promoted to the two-character synonym because
the IANA registry file omits the synonymous three-character code; we cannot depend on browsers understanding
the synonymous three-character codes in the lang= attribute.

For {{lang-xx}} templates, the parameters |script=, |region=, and |variant= are supported (not supported in {{lang}}
because those parameters are superfluous to the IETF subtags in |code=)

returns six  values.  Valid parts are returned as themselves; omitted parts are returned as empty strings, invalid
parts are returned as nil; the sixth returned item is an error message (if an error detected) or nil.

see http://www.rfc-editor.org/rfc/bcp/bcp47.txt section 2.1

]]

local function get_ietf_parts (source, args_script, args_region, args_variant)
	local code;
	local script = '';
	local region = '';
	local variant = '';
	local private = '';

	if not is_set (source) then
		return nil, nil, nil, nil, nil, '缺少语言标签';
	end

	if source:match ('^%a%a%a?%-%a%a%a%a%-%a%a%-%d%d%d%d$') then												-- ll-Ssss-RR-variant (where variant is 4 digits)
		code, script, region, variant = source:match ('^(%a%a%a?)%-(%a%a%a%a)%-(%a%a)%-(%d%d%d%d)$');
	elseif source:match ('^%a%a%a?%-%a%a%a%a%-%d%d%d%-%d%d%d%d$') then											-- ll-Ssss-DDD-variant (where region is 3 digits; variant is 4 digits)
		code, script, region, variant = source:match ('^(%a%a%a?)%-(%a%a%a%a)%-(%d%d%d)%-(%d%d%d%d)$');
	elseif source:match ('^%a%a%a?%-%a%a%a%a%-%a%a%-[%a%d][%a%d][%a%d][%a%d][%a%d]+$') then						-- ll-Ssss-RR-variant (where variant is 5-8 alnum characters)
		code, script, region, variant = source:match ('^(%a%a%a?)%-(%a%a%a%a)%-(%a%a)%-([%a%d][%a%d][%a%d][%a%d][%a%d][%a%d]?[%a%d]?[%a%d]?)$');
	elseif source:match ('^%a%a%a?%-%a%a%a%a%-%d%d%d%-[%a%d][%a%d][%a%d][%a%d][%a%d]+$') then						-- ll-Ssss-DDD-variant (where region is 3 digits; variant is 5-8 alnum characters)
		code, script, region, variant = source:match ('^(%a%a%a?)%-(%a%a%a%a)%-(%d%d%d)%-([%a%d][%a%d][%a%d][%a%d][%a%d][%a%d]?[%a%d]?[%a%d]?)$');

	elseif source:match ('^%a%a%a?%-%a%a%a%a%-%d%d%d%d$') then													-- ll-Ssss-variant (where variant is 4 digits)
		code, script, variant = source:match ('^(%a%a%a?)%-(%a%a%a%a)%-(%d%d%d%d)$');
	elseif source:match ('^%a%a%a?%-%a%a%a%a%-[%a%d][%a%d][%a%d][%a%d][%a%d]+$') then							-- ll-Ssss-variant (where variant is 5-8 alnum characters)
		code, script, variant = source:match ('^(%a%a%a?)%-(%a%a%a%a)%-([%a%d][%a%d][%a%d][%a%d][%a%d][%a%d]?[%a%d]?[%a%d]?)$');

	elseif source:match ('^%a%a%a?%-%a%a%-%d%d%d%d$') then														-- ll-RR-variant (where variant is 4 digits)
		code, region, variant = source:match ('^(%a%a%a?)%-(%a%a)%-(%d%d%d%d)$');
	elseif source:match ('^%a%a%a?%-%d%d%d%-%d%d%d%d$') then													-- ll-DDD-variant (where region is 3 digits; variant is 4 digits)
		code, region, variant = source:match ('^(%a%a%a?)%-(%d%d%d)%-(%d%d%d%d)$');
	elseif source:match ('^%a%a%a?%-%a%a%-[%a%d][%a%d][%a%d][%a%d][%a%d]+$') then								-- ll-RR-variant (where variant is 5-8 alnum characters)
		code, region, variant = source:match ('^(%a%a%a?)%-(%a%a)%-([%a%d][%a%d][%a%d][%a%d][%a%d][%a%d]?[%a%d]?[%a%d]?)$');
	elseif source:match ('^%a%a%a?%-%d%d%d%-[%a%d][%a%d][%a%d][%a%d][%a%d]+$') then								-- ll-DDD-variant (where region is 3 digits; variant is 5-8 alnum characters)
		code, region, variant = source:match ('^(%a%a%a?)%-(%d%d%d)%-([%a%d][%a%d][%a%d][%a%d][%a%d][%a%d]?[%a%d]?[%a%d]?)$');

	elseif source:match ('^%a%a%a?%-%d%d%d%d$') then								-- ll-variant (where variant is 4 digits)
		code, variant = source:match ('^(%a%a%a?)%-(%d%d%d%d)$');
	elseif source:match ('^%a%a%a?%-[%a%d][%a%d][%a%d][%a%d][%a%d][%a%d]?[%a%d]?[%a%d]?$') then			-- ll-variant (where variant is 5-8 alnum characters)
		code, variant = source:match ('^(%a%a%a?)%-([%a%d][%a%d][%a%d][%a%d][%a%d][%a%d]?[%a%d]?[%a%d]?)$');

	elseif source:match ('^%a%a%a?%-%a%a%a%a%-%a%a$') then							-- ll-Ssss-RR
		code, script, region = source:match ('^(%a%a%a?)%-(%a%a%a%a)%-(%a%a)$');
	elseif source:match ('^%a%a%a?%-%a%a%a%a%-%d%d%d$') then						-- ll-Ssss-DDD (region is 3 digits)
		code, script, region = source:match ('^(%a%a%a?)%-(%a%a%a%a)%-(%d%d%d)$');

	elseif source:match ('^%a%a%a?%-%a%a%a%a$') then								-- ll-Ssss
		code, script = source:match ('^(%a%a%a?)%-(%a%a%a%a)$');

	elseif source:match ('^%a%a%a?%-%a%a$') then									-- ll-RR
		code, region = source:match ('^(%a%a%a?)%-(%a%a)$');
	elseif source:match ('^%a%a%a?%-%d%d%d$') then									-- ll-DDD (region is 3 digits)
		code, region = source:match ('^(%a%a%a?)%-(%d%d%d)$');

	elseif source:match ('^%a%a%a?$') then											-- ll
		code = source:match ('^(%a%a%a?)$');

	elseif source:match ('^%a%a%a?%-x%-[%a%d][%a%d]?[%a%d]?[%a%d]?[%a%d]?[%a%d]?[%a%d]?[%a%d]?$') then		-- ll-x-pppppppp)
		code, private = source:match ('^(%a%a%a?)%-x%-([%a%d]+)$');

	else
		return nil, nil, nil, nil, nil, table.concat ({'无法识别的语言标签：', source});		-- don't know what we got but it is malformed
	end

	code = code:lower();														-- ensure that we use and return lower case version of this
	
	if not (lang_data.override[code] or lang_name_table.lang[code]) then
		return nil, nil, nil, nil, nil, table.concat ({'无法识别的语言代码：', code});		-- invalid language code, don't know about the others (don't care?)
	end
	
	if synonym_table[code] then													-- if 639-2/639-2T code has a 639-1 synonym
		table.insert (maint_cats, table.concat ({'Lang和lang-xx代码升级为ISO 639-1|', code}));
		table.insert (maint_msgs, table.concat ({'代码：', code, '升级为代码：', synonym_table[code]}));
		code = synonym_table[code];												-- use the synonym
	end

	if is_set (script) then
		if is_set (args_script) then
			return code, nil, nil, nil, nil, '冗余文本标签';			-- both code with script and |script= not allowed
		end
	else
		script = args_script or '';												-- use args.script if provided
	end 

	if is_set (script) then
		script = script:lower();												-- ensure that we use and return lower case version of this
		if not lang_name_table.script[script] then
			return code, nil, nil, nil, nil, table.concat ({'无法识别的文本：', script, '用于代码：', code});	-- language code ok, invalid script, don't know about the others (don't care?)
		end
	end
	if lang_name_table.suppressed[script] then									-- ensure that code-script does not use a suppressed script
		if in_array (code, lang_name_table.suppressed[script]) then
			return code, nil, nil, nil, nil, table.concat ({'文本：', script, '不支持代码：', code});	-- language code ok, script is suppressed for this code
		end
	end

	if is_set (region) then
		if is_set (args_region) then
			return code, nil, nil, nil, nil, '冗余区域标签';			-- both code with region and |region= not allowed
		end
	else
		region = args_region or '';												-- use args.region if provided
	end 

	if is_set (region) then
		region = region:lower();												-- ensure that we use and return lower case version of this
		if not lang_name_table.region[region] then
			return code, script, nil, nil, nil, table.concat ({'无法识别的地区：', region, '用于代码：', code});
		end
	end
	
	if is_set (variant) then
		if is_set (args_variant) then
			return code, nil, nil, nil, nil, '冗余变体标签';			-- both code with variant and |variant= not allowed
		end
	else
		variant = args_variant or '';											-- use args.variant if provided
	end 

	if is_set (variant) then
		variant = variant:lower();												-- ensure that we use and return lower case version of this
		if not lang_name_table.variant[variant] then							-- make sure variant is valid
			return code, script, region, nil, nil, table.concat ({'未识别的变体：', variant});
		end																		-- does this duplicate/replace tests in lang() and lang_xx()?
		if is_set (script) then													-- if script set it must be part of the 'prefix'
			if not in_array (table.concat ({code, '-', script}), lang_name_table.variant[variant]['prefixes']) then
				return code, script, region, nil, nil, table.concat ({'未识别的变体：', variant, ' 用于代码-文本对', code, '-', script});
			end
		else
			if not in_array (code, lang_name_table.variant[variant]['prefixes']) then
				return code, script, region, nil, nil, table.concat ({'未识别的变体：', variant, '用于代码：', code});
			end				
		end
	end
	
	if is_set (private) then
		private = private:lower();												-- ensure that we use and return lower case version of this
		if not lang_data.override[table.concat ({code, '-x-', private})] then	-- make sure private tag is valid; note that index 
			return code, script, region, nil, nil, table.concat ({'无法识别的私有标签： ', private});
		end
	end
	return code, script, region, variant, private, nil;							-- return the good bits; make sure that msg is nil
end


--[[--------------------------< M A K E _ E R R O R _ M S G >--------------------------------------------------

assembles an error message from template name, message text, help link, and error category.

]]

local function make_error_msg (msg, args, template)
	local out = {};
	local category;
	
	if 'transl' == template then
		category = 'transl';
	else
		category = 'lang和lang-xx'
	end
	
	table.insert (out, table.concat ({'[', args.text or '未定义', '] '}));	-- for error messages output args.text if available
	table.insert (out, table.concat ({'<span style=\"font-size:100%; font-style:normal;\" class=\"error\">错误：{{', template, '}}：'}));
	table.insert (out, msg);
	table.insert (out, table.concat ({'（[[:Category:',_category,_'模板错误|帮助]]）'}));
	table.insert (out, '</span>');
	
	if (0 == namespace) and not is_set (args.nocat) then						-- only categorize in article space
		table.insert (out, table.concat ({'[[Category:',_category,_'模板错误|Category:', category, '模板错误]]'}));
	end

	return table.concat (out);
end
	

--[=[-------------------------< M A K E _ W I K I L I N K >----------------------------------------------------

Makes a wikilink; when both link and display text is provided, returns a wikilink in the form [[L|D]]; if only
link is provided, returns a wikilink in the form [[L|L]]; if neither are provided or link is omitted, returns an
empty string.

]=]

local function make_wikilink (link, display)
	if is_set (link) then
		if is_set (display) then
			return table.concat ({'[[',_link,_'|', display, ']]'});
		else
			return table.concat ({'[[',_link,_'|', link, ']]'});
		end
	else
		return '';
	end
end


--[[--------------------------< M A K E _ T E X T _ S P A N >--------------------------------------------------

TODO: add support for block: div tags instead of span tags; would need some sort of proper parameter to control the switch

For italic style, can't do ''{{lang|xx|text}}'' without using <span/> tags when text is italic because of -Latn, |italic=yes,
or auto-italics because the wrapping wikimarkup produces this:
	<i><i lang="xx">text</i></i>
which is later reduced to this:
	<i>text</i>
This reduction happens in some sort of cleanup process outside the scope of this template/module.

Until or unless this is fixed italic text must be:
	<i><span lang="xx">text</span></i>

]]

local function make_text_span (code, text, rtl, style, size, language)
	local span = {};
	local style_added = '';

	if text:match ('^%*') then
		table.insert (span, '*');											-- move proto language text prefix outside of italic markup if any; use numeric entity because plan splat confuses MediaWiki
		text = text:gsub ('^%*', '');											-- remove the splat from the text
	end

	if 'italic' == style then
		table.insert (span, '<i>');												-- open italic style tag
	end
		
	table.insert (span, table.concat ({'<span lang="'}));						-- open <span> tag
	table.insert (span, table.concat ({code, '\"'}));							-- add language attribute

	if rtl then
		table.insert (span, ' dir="rtl"');										-- add direction attribute for right to left languages
	end

	if 'normal' == style then													-- when |italic=no
		table.insert (span, ' style=\"font-style:normal;');						-- override external markup, if any
		style_added = '\"';														-- remember that style attribute added and is not yet closed
	end

	if is_set (size) then														-- when |size=<something>
		if is_set (style_added) then
			table.insert (span, table.concat ({' font-size:', size, ';'}));		-- add when style attribute already inserted
		else
			table.insert (span, table.concat ({' style=\"font-size:', size, ';'}));	-- create style attribute
			style_added = '\"';													-- remember that style attribute added and is not yet closed
		end
	end

	if is_set (language) then
		table.insert (span, table.concat ({style_added, ' title=\"', language}));	--start the title text
		if language:find ('languages') then
			table.insert (span, ' collective text\"');							-- for collective languages
		else
			table.insert (span, ' language text\"');							-- for individual languages
		end
		table.insert (span, '>');												-- close the opening span tag
	else
		table.insert (span, table.concat ({style_added, '>'}));					-- close the style attribute and close opening span tag
	end
	table.insert (span, text);													-- insert the text

	table.insert (span, '</span>');												-- close the <span> tag
	if 'italic' == style then
		table.insert (span, '</i>');											-- close italic style tag
	end
		
	if rtl then																	-- legacy; shouldn't be necessary because all of the rtl text is wrapped in <span dir="rtl">text</span>
		table.insert (span, '‎');											-- make sure the browser knows that we're at the end of the rtl
	end
	
	return table.concat (span);													-- put it all together and done
end


--[=[-------------------------< M A K E _ C A T E G O R Y >----------------------------------------------------

注意：此处有修改

对于中文，则返回以下分类：
	[[Category:含有明确引用中文的条目|Category:含有明确引用中文的条目]]

对于非中文内容：

	如果是常用语言，则直接返回以下分类：
		[[Category:含有<语言>的条目|Category:含有<语言>的条目]]（此处的<语言>为本模块内建）

	如果是非常用语言：

		如果存在对应语言的分类，则返回以下分类：
			[[Category:含有<语言>的条目|Category:含有<语言>的条目]]（此处的<语言>需读取数据库资料）

		反之，则返回以下分类：
			[[Category:含有非中文内容的条目|Category:含有非中文内容的条目]]

]=]

local function make_category (code, language_name, nocat)
	local cat = {};
	
	if (0 ~= namespace) or nocat then											-- only categorize in article space
		return '';																-- return empty string for concatenation
	end
		
	table.insert (cat, '[[Category:含有');
	
	if 'zh' == code then
		table.insert (cat, '明確引用中文');
	elseif 'ar' == code then
		table.insert (cat, '阿拉伯語')
	elseif 'en' == code then
		table.insert (cat, '英語')
	elseif 'es' == code then
		table.insert (cat, '西班牙語')
	elseif 'de' == code then
		table.insert (cat, '德語')
	elseif 'fr' == code then
		table.insert (cat, '法語')
	elseif 'ja' == code then
		table.insert (cat, '日語')
	elseif 'bg' == code then
		table.insert (cat, '保加利亞語')
	elseif 'cs' == code then
		table.insert (cat, '捷克語')
	elseif 'da' == code then
		table.insert (cat, '丹麥語')
	elseif 'nl' == code then
		table.insert (cat, '荷蘭語')
	elseif 'et' == code then
		table.insert (cat, '愛沙尼亞語')
	elseif 'fi' == code then
		table.insert (cat, '芬蘭語')
	elseif 'el' == code then
		table.insert (cat, '希臘語')
	elseif 'hu' == code then
		table.insert (cat, '匈牙利語')
	elseif 'ga' == code then
		table.insert (cat, '愛爾蘭語')
	elseif 'grc' == code then
		table.insert (cat, '古希臘語')
	elseif 'kr' == code then
		table.insert (cat, '卡努里語')
	elseif 'la' == code then
		table.insert (cat, '拉丁語')
	elseif 'cy' == code then
		table.insert (cat, '威爾斯語')
	elseif 'sl' == code then
		table.insert (cat, '斯洛維尼亞語')
	elseif 'yue' == code then
		table.insert (cat, '粵語')
	elseif (page_exists ('Category:含有' .. language_name .. '的條目') ) then
		table.insert (cat, language_name);
	else
		table.insert (cat, '非中文內容');
	end
	
	table.insert (cat, '的條目]]');

	return table.concat (cat);	
end


--[[--------------------------< M A K E _ T R A N S L I T >----------------------------------------------------

return translit <i lang=xx-Latn>...</i> where xx is the language code; else return empty string

The value |script= is not used in {{transl}} for this purpose; instead it uses |code.  Because language scripts
are listed in the {{transl}} switches they are included in the data tables.  The script parameter is introduced
at {{Language with name and transliteration}}.  If |script= is set, this function uses it in preference to code.

To avoid confusion, in this module and the templates that use it, the transliteration script parameter is renamed
to be |translit-script= (in this function, tscript)

This function is used by both lang_xx() and transl()
	lang_xx() always provides code, language_name, and translit; may provide tscript; never provides style
	transl() always provides language_name, translit, and one of code or tscript, never both; always provides style

For {{transl}}, style only applies when a language code is provided
]]

local function make_translit (code, language_name, translit, std, tscript, style)
	local title;
	local tout = {};
	local title_table = lang_data.translit_title_table;							-- table of transliteration standards and the language codes and scripts that apply to those standards
	
	if is_set (code) then														-- when a language code is provided (always with {{lang-xx}} templates, not always with {{transl}})
		if not style then														-- nil for is the default italic style
			table.insert (tout, "<span lang=\"");									-- so use <span> tag
		else
			table.insert (tout, table.concat ({'<span style=\"font-style:', style, '\" lang=\"'}));	-- non-standard style, construct a span tag for it
		end
		table.insert (tout, code);
		table.insert (tout, "-Latn\" title=\"");								-- transliterations are always Latin script
	else
		table.insert (tout, "<span title=\"");									-- when no language code: no lang= attribute, not italic ({{transl}} only)
	end
	
	std = std and std:lower();													-- lower case for table indexing
	
	if not is_set (std) and not is_set (tscript) then							-- when neither standard nor script specified
		table.insert (tout, language_name);										-- write a generic tool tip
		if not language_name:find ('languages') then							-- collective language names (plural 'languages' is part of the name)
			table.insert (tout, '-language')									-- skip this text (individual and macro languages only)
		end
		table.insert (tout, ' transliteration');								-- finish the tool tip
	elseif is_set (std) and is_set (tscript) then								-- when both are specified
		if title_table[std] then												-- and if standard is legitimate
			if title_table[std][tscript] then									-- and if script for that standard is legitimate
				table.insert (tout, table.concat ({title_table[std][tscript:lower()], ' (', lang_name_table.script[tscript][1], ' script) transliteration'}));	-- add the appropriate text to the tool tip
			else
				table.insert (tout, title_table[std]['default']);				-- use the default if script not in std table; TODO: maint cat? error message because script not found for this standard?
			end
		else
			return '';															-- invalid standard, setup for error message
		end

	elseif is_set (std) then													-- translit-script not set, use language code
		if not title_table[std] then return ''; end								-- invalid standard, setup for error message
		
		if title_table[std][code] then											-- if language code is in the table (transl may not provide a language code)
			table.insert (tout, table.concat ({title_table[std][code:lower()], ' (', lang_name_table.lang[code][1], ' language) transliteration'}));	-- add the appropriate text to the tool tip
		else																	-- code doesn't match
			table.insert (tout, title_table[std]['default']);					-- so use the standard's default
		end
	else																		-- here if translit-script set but translit-std not set
		if title_table['no_std'][tscript] then
			table.insert (tout, title_table['no_std'][tscript]);				-- use translit-script if set
		elseif title_table['no_std'][code] then
			table.insert (tout, title_table['no_std'][code]);					-- use language code
		else
			if is_set (tscript) then
				table.insert (tout, table.concat ({language_name, '-script transliteration'}));	-- write a script tool tip
			elseif is_set (code) then
				if not language_name:find ('languages') then					-- collective language names (plural 'languages' is part of the name)
					table.insert (tout, '-language')							-- skip this text (individual and macro languages only)
				end
				table.insert (tout, ' transliteration');						-- finish the tool tip
			else
				table.insert (tout, ' transliteration');						-- generic tool tip (can we ever get here?)
			end
		end
	end

	table.insert (tout, '">');
	table.insert (tout, translit);
	if is_set (code) and not style then														-- when a language code is provided (always with {{lang-xx}} templates, not always with {{transl}})
		table.insert (tout, "</span>");											-- close the span tag
	else
		table.insert (tout, "</span>");											-- no language code so close the span tag
	end
	return table.concat (tout);
end


--[=[-------------------------< V A L I D A T E _ T E X T >---------------------------------------------------

This function checks the content of args.text and returns empty string if nothing is amiss else it returns an
error message.  The tests are for empty or missing text and for improper or disallowed use of apostrophe markup.

Italic rendering is controlled by the |italic= template parameter so italic markup should never appear in args.text
either as ''itself''' or as '''''bold italic'''''.

]=]

local function validate_text (template, args)
	if not is_set (args.text) then
		return make_error_msg ('无文本', args, template);
	end

	if args.text:find ("%f[\']\'\'\'\'%f[^\']") or args.text:find ("\'\'\'\'\'[\']+") then	-- because we're looking, look for 4 appostrophes or 6+ appostrophes
		return make_error_msg ('文本有格式不正确的标记', args, template);
	end

	local style = args.italic or args.italics;

--	if ('unset' ~= args.italic) and ('unset' ~= args.italics) then				-- allow italic markup when |italic=unset or |italics=unset
	if ('unset' ~= style) and ('invert' ~=style) then
		if args.text:find ("%f[\']\'\'%f[^\']") or args.text:find ("%f[\']\'\'\'\'\'%f[^\']") then	-- italic but not bold, or bold italic
			return make_error_msg ('文本有斜体标记', args, template);
		end
	end
end


--[[--------------------------< R E N D E R _ M A I N T >------------------------------------------------------

render mainenance messages and categories

]]

local function render_maint(nocat)
	local maint = {};
	
	if 0 < #maint_msgs then														-- when there are maintenance messages
		table.insert (maint, table.concat ({'<span class="lang-comment" style="font-style:normal; display:none; color:#33aa33; margin-left:0.3em">'}));	-- opening <span> tag
		for _, msg in ipairs (maint_msgs) do
			table.insert (maint, table.concat ({msg, ' '}));					-- add message strings
		end
		table.insert (maint, '</span>');										-- close the span
	end
	
	if (0 < #maint_cats) and (0 == namespace) and not is_set (nocat) then		-- when there are mainenance categories; article namespace only
		for _, cat in ipairs (maint_cats) do
			table.insert (maint, table.concat ({'[[Category:',_cat,_'|Category:', cat, ']]'}));	-- format and add the categories
		end
	end
	
	return table.concat (maint);
end


--[[--------------------------< P R O T O _ P R E F I X >------------------------------------------------------

for proto languages, text is prefixed with a splat.  We do that here as a flag for make_text_span() so that a splat
will be rendered outside of italic markup (if used).  If the first character in text here is already a splat, we
do nothing

]]

local function proto_prefix (text, language_name)
	if language_name:find ('^Proto%-') and not text:find ('^*') then			-- language is a proto and text does not already have leading splat
		return table.concat ({'*', text});										-- prefix proto language text with a splat
	end
	
	return text;
end


--[[--------------------------< L A N G >----------------------------------------------------------------------

entry point for {{lang}}

there should be no reason to set parameters in the {{lang}} {{#invoke:}}
	<includeonly>{{#invoke:lang|lang}}</includeonly>

parameters are recieved from the template's frame (parent frame)

]]

function p.lang (frame)
	local args = getArgs(frame);
	local out = {};
	local language_name;														-- used to make category names
	local subtags = {};															-- IETF subtags script, region, variant, and private
	local code;																	-- the language code
	local msg;																	-- for error messages

	if args[1] and args.code then
		return make_error_msg ('冲突：{{{1}}} 和 |code=', args, 'lang');
	else
		args.code = args[1] or args.code;										-- prefer args.code
	end

	if args[2] and args.text then
		return make_error_msg ('冲突：{{{2}}} 和 |text=', args, 'lang');
	else
		args.text = args[2] or args.text;										-- prefer args.text
	end

	if nil == args.italic then													-- nil when |italic= absent or not set or |italic=default; args.italic controls
		args.italic = 'unset';
	end
	
	msg = validate_text ('lang', args);											-- ensure that |text= is set  (italic test disabled for the time being)
	if is_set (msg) then														-- msg is an already-formatted error message
		return msg;
	end

	args.rtl = args.rtl == 'yes';												-- convert to boolean: 'yes' -> true, other values -> false

	code, subtags.script, subtags.region, subtags.variant, subtags.private, msg = get_ietf_parts (args.code);	-- |script=, |region=, |variant= not supported because they should be part of args.code ({{{1}}} in {{lang}})

	if msg then
		return make_error_msg ( msg, args, 'lang');
	end

	args.italic, msg = validate_italic (args.italic, args.italics);
	if msg then
		return make_error_msg (msg, args, 'lang');
	end
	
	if is_set (subtags.script) then												-- if script set, override rtl setting
		if in_array (subtags.script, lang_data.rtl_scripts) then
			args.rtl = true;													-- script is an rtl script
		else
			args.rtl = false;													-- script is not an rtl script
		end
	end

	args.code = format_ietf_tag (code, subtags.script, subtags.region, subtags.variant);	-- format to recommended subtag styles; private omitted because private

	if is_set (subtags.private) and lang_data.override[table.concat ({code, '-x-', subtags.private})] then	-- look for private use tags; done this way because ...
		language_name = lang_data.override[table.concat ({code, '-x-', subtags.private})][1];				-- ... args.code does not get private subtag
	elseif lang_data.override[code] then										-- get the language name for categorization
		language_name = lang_data.override[code][1]								-- prefer language names taken from the override table
	elseif lang_name_table.lang[code] then
		language_name = lang_name_table.lang[code][1];							-- table entries sometimes have multiple names, always take the first one
	end

	if 'invert' == args.italic then
		args.text = invert_italics (args.text)
	end

	-- 中文版特化部分：为非中文文字禁用繁简转换，中文文字和其他以汉字作为书写系统的汉语方言文字启用繁简转换。
	if 'zh' == code then
		args.text = args.text
	elseif 'gan' == code then
		args.text = args.text
	elseif 'wuu' == code then
		args.text = args.text
	elseif 'yue' == code then
		args.text = args.text
	elseif 'lzh' == code then
		args.text = args.text
	elseif 'hsn' == code then
		args.text = args.text
	else
		args.text = '-{' .. args.text .. '}-'
	end
	
	args.text = proto_prefix (args.text, language_name);						-- prefix proto-language text with a splat

	table.insert (out, make_text_span (args.code, args.text, args.rtl, args.italic, args.size, language_name));
	table.insert (out, make_category (code, language_name, args.nocat));
	table.insert (out, render_maint(args.nocat));											-- maintenance messages and categories

	return table.concat (out);													-- put it all together and done
end


--[[--------------------------< L A N G _ X X >----------------------------------------------------------------

For the {{lang-xx}} templates, the only parameter required to be set in the template is the language code.  All
other parameters can, usually should, be written in the template call.  For {{lang-xx}} templates for languages
that can have multiple writing systems, it may be appropriate to set |script= as well.

For each {{lang-xx}} template choose the appropriate entry-point function so that this function know the default
styling that should be applied to text.

For normal, upright style:
	<includeonly>{{#invoke:lang|lang_xx_inherit|code=xx}}</includeonly>
For italic style:
	<includeonly>{{#invoke:lang|lang_xx_italic|code=xx}}</includeonly>

All other parameters should be received from the template's frame (parent frame)

Supported parameters are:
	|code = (required) the IANA language code
	|script = IANA script code; especially for use with languages that use multiple writing systems; yields to the script subtag in |code= if present [not yet implemented]
	|region = IANA region code
	|variant = IANA variant code
	|text = (required) the displayed text in language specified by code
	|link = boolean false ('no') unlinks language specified by code to associated language article
	|rtl = boolean true ('yes') identifies the language specified by code as a right-to-left language
	|nocat = boolean true ('yes') inhibits normal categorization; error categories are not affected
	|italic = boolean true ('yes') renders displayed text in italic font; boolean false ('no') renders displayed text in normal font; not set renders according to initial_style_state
	|lit = text that is a literal translation of text
	|label =	'none' to suppress all labeling (language name, 'translit.', 'lit.')
				any other text replaces language-name label - automatic wikilinking disabled
	
	for those {{lang-xx}} templates that support transliteration (those template where |text= is entirely latn script):
	|translit = text that is a transliteration of text
	|translit-std = the standard that applies to the transliteration
	|translit-script = ISO 15924 script name; falls back to code

For {{lang-xx}}, the positional parameters are:
	{{{1}}}	text
	{{{2}}}	transliterated text
	{{{3}}}	literal translation text
no other positional parameters are allowed

]]

local function _lang_xx (frame)
	local args = getArgs(frame, {parentFirst= true});							-- parameters in the template override parameters set in the {{#invoke:}}
	local out = {};
	local language_name;														-- used to make display text, article links
	local category_name;														-- same as language_name except that it retains any parenthetical disambiguators (if any) from the data set
	local subtags = {};															-- IETF subtags script, region, and variant
	local code;																	-- the language code

	local translit_script_name;													-- name associated with IANA (ISO 15924) script code
	local translit;
	local translit_title;
	local msg;																	-- for error messages

	if args[1] and args.text then
		return make_error_msg ('冲突：{{{1}}} 和 |text=', args, 'lang-xx');
	else
		args.text = args[1] or args.text;										-- prefer args.text
	end
	
	msg = validate_text ('lang-xx', args);										-- ensure that |text= is set, does not contain italic markup and is protected from improper bolding
	if is_set (msg) then
		return msg;
	end

	if args[2] and args.translit then
		return make_error_msg ('冲突：{{{2}}} 和 |translit=', args, 'lang-xx');
	else
		args.translit = args[2] or args.translit								-- prefer args.translit
	end
	
	if args[3] and (args.translation or args.lit) then
		return make_error_msg ('冲突：{{{3}}} 和 |lit= or |translation=', args, 'lang-xx');
	elseif args.translation and args.lit then
		return make_error_msg ('冲突：|lit= and |translation=', args, 'lang-xx');
	else
		args.translation = args[3] or args.translation or args.lit;				-- prefer args.translation
	end

	if args.links and args.link then
		return make_error_msg ('冲突：|links= and |link=', args, 'lang-xx');
	else
		args.link = args.link or args.links;									-- prefer args.link
	end

	args.rtl = args.rtl == 'yes';												-- convert to boolean: 'yes' -> true, other values -> false

	code, subtags.script, subtags.region, subtags.variant, subtags.private, msg = get_ietf_parts (args.code, args.script, args.region, args.variant);	-- private omitted because private

	if msg then																	-- if an error detected then there is an error message
		return make_error_msg (msg, args, 'lang-xx');
	end
	
	args.italic, msg = validate_italic (args.italic, args.italics);
	if msg then
		return make_error_msg (msg, args, 'lang-xx');
	end

	if nil == args.italic then													-- args.italic controls
		if is_set (subtags.script) then
			if 'latn' == subtags.script then
				args.italic = 'italic';											-- |script=Latn; set for font-style:italic
			else
				args.italic = initial_style_state;								-- italic not set; script is not latn; set for font-style:<initial_style_state>
			end
		else
			args.italic = initial_style_state;									-- here when |italic= and |script= not set; set for font-style:<initial_style_state>
		end
	end
	
	if is_set (subtags.script) then												-- if script set override rtl setting
		if in_array (subtags.script, lang_data.rtl_scripts) then
			args.rtl = true;													-- script is an rtl script
		else
			args.rtl = false;													-- script is not an rtl script
		end
	end

	args.code = format_ietf_tag (code, subtags.script, subtags.region, subtags.variant);	-- format to recommended subtag styles
	
	if is_set (subtags.private) and lang_data.override[table.concat ({code, '-x-', subtags.private})] then	-- look for private use tags; done this way because ...
		language_name = lang_data.override[table.concat ({code, '-x-', subtags.private})][1];				-- ... args.code does not get private subtag
	elseif lang_data.override[args.code:lower()] then							-- look for whole IETF tag in override table
		language_name = lang_data.override[args.code:lower()][1];				-- args.code:lower() because format_ietf_tag() returns mixed case
	elseif lang_data.override[code] then										-- not there so try basic language code
		language_name = lang_data.override[code][1];
	elseif not is_set (subtags.variant) then									
		if lang_name_table.lang[code] then
			language_name = lang_name_table.lang[code][1];						-- table entries sometimes have multiple names, always take the first one
		end
	else																		-- TODO: is this the right thing to do: take language display name from variants table?
		if lang_name_table.variant[subtags.variant] then						-- TODO: there is some discussion at Template talk:Lang about having a label parameter for use when variant name is not desired among other things
			language_name = lang_name_table.variant[subtags.variant]['descriptions'][1];	-- table entries sometimes have multiple names, always take the first one
		end
	end

	category_name = language_name;												-- category names retain IANA parenthetical diambiguators (if any)
	language_name = language_name:gsub ('%s+%b()', '');							-- remove IANA parenthetical disambiguators or qualifiers from names that have them

	if args.label then
		if 'none' ~= args.label then
			table.insert (out, table.concat ({args.label, '：'}));				-- custom label
		end
	else
		if 'no' == args.link then
			table.insert (out, language_name);									-- language name without wikilink
		else
		--	if language_name:find ('languages') then
			table.insert (out, make_wikilink (language_name));				-- collective language name uses simple wikilink
		--	else
		--		table.insert (out, make_wikilink (language_name .. ' language', language_name));	-- language name with wikilink
		--	end
		end
		table.insert (out, '：');												-- separator
	end

	if 'invert' == args.italic then
		args.text = invert_italics (args.text)
	end

	-- 中文版特化部分：为非中文文字禁用繁简转换，中文文字和其他以汉字作为书写系统的汉语方言文字启用繁简转换。
	if 'zh' == code then
		args.text = args.text
	elseif 'gan' == code then
		args.text = args.text
	elseif 'wuu' == code then
		args.text = args.text
	elseif 'yue' == code then
		args.text = args.text
	elseif 'lzh' == code then
		args.text = args.text
	elseif 'hsn' == code then
		args.text = args.text
	else
		args.text = '-{' .. args.text .. '}-'
	end
	
	args.text = proto_prefix (args.text, language_name);						-- prefix proto-language text with a splat

	table.insert (out, make_text_span (args.code, args.text, args.rtl, args.italic, args.size))

	if is_set (args.translit) and not p.is_latn (args.text) then					-- transliteration (not supported in {{lang}}); not supported when args.text is wholly latn text (this is an imperfect test)
		args.translit = '-{' .. args.translit .. '}-'
		table.insert (out, '，');												-- comma to separate text from translit
		if 'none' ~= args.label then
			table.insert (out, '<small>');
			if lang_name_table.script[args['translit-script']] then				-- when |translit-script= is set, try to use the script's name
				translit_script_name = lang_name_table.script[args['translit-script'][1]];
			else
				translit_script_name = language_name;							-- fall back on language name
			end
			translit_title = mw.title.makeTitle (0, table.concat ({translit_script_name, '羅馬化'}));		-- make a title object
			if translit_title.exists and ('no' ~= args.link) then
				table.insert (out, make_wikilink ((translit_script_name or language_name) .. '羅馬化', '转写'));	-- make a wikilink if there is an article to link to
			else
				table.insert (out, '转写');	-- else define the abbreviation
			end
			table.insert (out, '：</small>');								-- close the small tag
		end
		
		translit = make_translit (args.code, language_name, args.translit, args['translit-std'], args['translit-script'])
		if is_set (translit) then
			table.insert (out, translit);
		else
			return make_error_msg (table.concat ({'invalid translit-std: \'', args['translit-std'] or '[missing]'}), args, 'lang-xx');
		end
	end
	
	if is_set (args.translation) then											-- translation (not supported in {{lang}})
		table.insert (out, '，');
		if 'none' ~= args.label then
			table.insert (out, '<small>');
			if 'no' == args.link then
				table.insert (out, '直译');
			else
				table.insert (out, make_wikilink ('直译'));
			end
			table.insert (out, "：</small>");
		end
		table.insert (out, table.concat ({args.translation}));	-- use html entities to avoid wiki markup confusion
	end
	
	table.insert (out, make_category (code, category_name, args.nocat));
	table.insert (out, render_maint(args.nocat));								-- maintenance messages and categories

	return table.concat (out);													-- put it all together and done
end


--[[--------------------------< L A N G _ X X _ I T A L I C >--------------------------------------------------

Entry point for those {{lang-xx}} templates that call lang_xx_italic().  Sets the initial style state to italic.

]]

function p.lang_xx_italic (frame)
	initial_style_state = 'italic';
	return _lang_xx (frame);
end


--[[--------------------------< L A N G _ X X _ I N H E R I T >------------------------------------------------

Entry point for those {{lang-xx}} templates that call lang_xx_inherit().  Sets the initial style state to inherit.

]]

function p.lang_xx_inherit (frame)
	initial_style_state = 'inherit';
	return _lang_xx (frame);
end


--[[--------------------------< N A M E _ F R O M _ C O D E >--------------------------------------------------

Returns language name associated with IETF language tag if valid; empty string else.

All code combinations supported by {{lang}} and the {{lang-xx}} templates are supported by this function.

]]

function p.name_from_code (frame)
	local subtags = {};															-- IETF subtags script, region, variant, and private
	local raw_code = (frame.args and frame.args[1]) or frame;					-- save a copy of the input
	local code;																	-- the language code
	local msg;																	-- holds an error message (not used here) if IETF language tag is malformed or invalid
	local language_name = '';

	code, subtags.script, subtags.region, subtags.variant, subtags.private, msg = get_ietf_parts (raw_code);
	if msg then
		return '';
	end

	if lang_data.override[raw_code:lower()] then								-- look for whole IETF tag in override table (force lower case)
		language_name = lang_data.override[raw_code:lower()][1];
	elseif lang_data.override[code] then										-- not there so try basic language code in override table
		language_name = lang_data.override[code][1];
	elseif not is_set (subtags.variant) then									
		if lang_name_table.lang[code] then
			language_name = lang_name_table.lang[code][1];						-- table entries sometimes have multiple names, always take the first one
		end
	else																		-- TODO: is this the right thing to do: take language display name from variants table?
		if lang_name_table.variant[subtags.variant] then						-- TODO: there is some discussion at Template talk:Lang about having a label parameter for use when variant name is not desired among other things
			language_name = lang_name_table.variant[subtags.variant]['descriptions'][1];	-- table entries sometimes have multiple names, always take the first one
		end
	end

	language_name = language_name:gsub ('%s+%b()', '');							-- remove IANA parenthetical disambiguators or qualifiers from names that have them

	return language_name;

end


--[[--------------------------< T R A N S L >------------------------------------------------------------------

Prospective replacement for the template {{transl}}

]]

function p.transl (frame)
	local args = getArgs(frame);												-- no {{#invoke:}} parameters
	local title_table = lang_data.translit_title_table;							-- table of transliteration standards and the language codes and scripts that apply to those standards
	local language_name;														-- language name that matches language code; used for tool tip
	local translit;																-- translitterated text to display
	local script;																-- IANA script
	local msg;																	-- for when called functions return an error message

	if is_set (args[3]) then													-- [3] set when {{transl|code|standard|text}}
		args.text = args[3];													-- get the transliterated text
		args.translit_std = args[2] and args[2]:lower();						-- get the standard; lower case for table indexing

		if not title_table[args.translit_std] then
			return make_error_msg (table.concat ({'无法识别的转译标准：', args.translit_std}), args, 'transl');
		end
	else
		if is_set (args[2]) then												-- [2] set when {{transl|code|text}}
			args.text = args[2];												-- get the transliterated text
		else
			if args[1] and args[1]:match ('^%a%a%a?%a?$') then					-- args[2] missing; is args[1] a code or its it the transliterated text?
				return make_error_msg ('no text', args, 'transl');				-- args[1] is a code so we're missing text
			else
				args.text = args[1];											-- args[1] is not a code so we're missing that; assign args.text for error message
				return make_error_msg ('缺少语言/文字代码', args, 'transl');
			end
		end
	end

	if is_set (args[1]) then													-- IANA language code used for html lang= attribute; or ISO 15924 script code
		if args[1]:match ('^%a%a%a?%a?$') then									-- args[1] has correct form?
			args.code = args[1]:lower();										-- use the language/script code; only (2, 3, or 4 alpha characters); lower case because table indexes are lower case
		else
			return make_error_msg (table.concat ({'无法识别的语言/文字代码：', args[1]}), args, 'transl');	-- invalid language / script code
		end
	else
		return make_error_msg ('缺少语言/文字代码', args, 'transl');			-- missing language / script code so quit
	end

	args.italic, msg = validate_italic (args.italic, args.italics);
	if msg then
		return make_error_msg (msg, args, 'transl');
	end
	
	if 'italic' == args.italic then												-- 'italic' when |italic=yes; because that is same as absent or not set and |italic=default
		args.italic = nil;														-- set to nil; 
	end

	if lang_data.override[args.code] then										-- is code a language code defined in the override table?
		language_name = lang_data.override[args.code][1];
	elseif lang_name_table.lang[args.code] then									-- is code a language code defined in the standard language code tables?
		language_name = lang_name_table.lang[args.code][1];
	elseif lang_name_table.script[args.code] then								-- if here, code is not a language code; is it a script code?
		language_name = lang_name_table.script[args.code][1];
		script = args.code;														-- code was an ISO 15924 script so use that instead
		args.code = '';															-- unset because not a language code
	else
		return make_error_msg (table.concat ({'无法识别的语言/文字代码：', args.code}), args, 'transl');	-- invalid language / script code
	end
																				-- here only when all parameters passed to make_translit() are valid
	return make_translit (args.code, language_name, args.text, args.translit_std, script, args.italic);
end


return p;