require('Module:No globals')

local p = {}
local lang = mw.language.getContentLanguage();									-- language object for this wiki
local presentation ={};															-- table of tables that contain currency presentation data
local properties;


--[[--------------------------< I S _ S E T >------------------------------------------------------------------

Whether variable is set or not.  A variable is set when it is not nil and not empty.

]]

local function is_set( var )
	return not (var == nil or var == '');
end


--[[--------------------------< M A K E _ S H O R T _ F O R M  _ N A M E >-------------------------------------

Assembles value and symbol according to the order specified in the properties table for this currency code

]]

local function make_short_form_name (amount, code, linked)
	local symbol;
	local position = properties[code].position;

	if linked then
		symbol = string.format ('[[%s|%s]]', properties[code].page, properties[code].symbol);	-- make wikilink of page and symbol
	else
		symbol = properties[code].symbol;
	end

	amount = lang:formatNum (tonumber(amount));									-- add appropriate comma separators
	amount = amount:gsub ('^%-', '−');											-- replace the hyphen with unicode minus

	if 'b' == position then														-- choose appropriate format: unspaced before the amount
		return string.format ('%s%s', symbol, amount);
	elseif 'bs' == position then												-- spaced before the amount
		return string.format ('%s %s', symbol, amount);
	elseif 'a' == position then													-- unspaced after the amount
		return string.format ('%s%s', amount, symbol);
	elseif 'as' == position then												-- spaced after the amount
		return string.format ('%s %s', amount, symbol);
	elseif 'd' == position then													-- special case that replaces the decimal separator with symbol (Cifrão for CVE is the only extant case)
		local digits, decimals;													-- this code may not work for other currencies or on other language wikis
		if amount:match ('[%d,]+%.%d+') then									-- with decimal separator and decimals
			digits, decimals = amount:match ('([%d,]+)%.(%d+)')
			amount = string.format ('%s%s%s', digits, symbol, decimals);		-- insert symbol
		elseif amount:match ('[%d,]+%.?$') then									-- with or without decimal separator
			digits = amount:match ('([%d,]+)%.?$')
			amount = string.format ('%s%s00', digits, symbol);					-- add symbol and 00 ($00)
		end
		amount = amount:gsub (',', '%.');										-- replace grouping character with period
		return amount;
	end
	return amount .. ' <span style="font-size:inherit" class="error">{{CurrencyConvert}} – definition missing position ([[Template:CurrencyConvert/doc#Error_messages|help]])</span>';	-- position not defined
end


--[[--------------------------< M A K E _ N A M E >----------------------------------------------------------

Make a wikilink from the currency's article title and its plural (if provided).  If linked is false, returns only
the article title (unlinked)

]]

local function make_name (linked, page, plural)
	if not linked then
		if not is_set (plural) then
			return page;														-- just the page
		elseif 's' == plural then												-- if the simple plural form
			return string.format ('%ss', page);									-- append an 's'
		else
			return plural;														-- must be the complex plural form (pounds sterling v. dollars)
		end
	else
		if not is_set (plural) then
			return string.format ('[[%s|%s]]', page);
		elseif 's' == plural then												-- if the simple plural form
			return string.format ('[[%s|%s]]s', page);
		else
			return string.format ('[[%s|%s]]', page, plural);					-- must be the complex plural form (pounds sterling v. dollars)
		end
	end
end


--[[--------------------------< M A K E _ L O N G _ F O R M  _ N A M E >---------------------------------------

assembles a long-form currency name from amount and name from the properties tables; plural for all values not equal to 1

]]

local function make_long_form_name (amount, code, linked)
	local name;
	
	if not is_set (properties[code].page) then
		return '<span style="font-size:inherit" class="error">{{CurrencyConvert}} – definition missing page ([[Template:CurrencyConvert/doc#Error_messages|help]])</span>';
	end

	amount = tonumber (amount);													-- make sure it's a number
	
	if 1 == amount then
		name = make_name (linked, properties[code].page);						-- the singular form
	elseif is_set (properties[code].plural) then								-- plural and there is a plural form
		name = make_name (linked, properties[code].page, properties[code].plural);
	else
		name = make_name (linked, properties[code].page);						-- plural but no separate plural form so use the singular form
	end

	return string.format ('%s %s', lang:formatNum (amount), name);				-- put it all together
end


--[[--------------------------< R E N D E R _ C U R R E N C Y >------------------------------------------------

Renders currency amount with symbol or long-form name.

Also, entry point for other modules.  Assumes that parameters have been vetted; amount is a number, code is upper
case string, long_form is boolean; all are required.

]]

local function render_currency (amount, code, long_form, linked)
	local name;

	presentation = mw.loadData ('Module:CurrencyConvert/Presentation');				-- get presentation data

	if presentation.currency_properties[code] then								-- if code is an iso 4217 code
		properties = presentation.currency_properties;
	elseif presentation.code_translation[code] then								-- not iso 4217 but can be translated
		code = presentation.code_translation[code];								-- then translate
		properties = presentation.currency_properties;
	elseif presentation.non_standard_properties[code] then						-- last chance, is it a non-standard code?
		properties = presentation.non_standard_properties;
	else
		return '<span style="font-size:inherit" class="error">{{CurrencyConvert}} – invalid code ([[Template:CurrencyConvert/doc#Error_messages|help]])</span>';
	end

	if long_form then
		return make_long_form_name (amount, code, linked);								-- 
	else
		return make_short_form_name (amount, code, linked);
	end
end

--[[--------------------------< P A R S E _ F O R M A T T E D _ N U M B E R >----------------------------------

replacement for lang:parseFormattedNumber() which doesn't work; all it does is strip commas.

This function returns a string where all comma separators have been removed from the source string.  If the source
is malformed: has characters other than digits, commas, and decimal points; has too many decimal points; has commas
in in appropriate locations; then the function returns nil.

]]

local function parse_formatted_number (amount)
	local count;
	local parts = {};
	local digits = {};
	local decimals;
	local sign = '';
	local _;
	
	if amount:find ('[^%-−%d%.,]')	then										-- anything but sign, digits, decimal points, or commas
		return nil;
	end
	
	amount = amount:gsub ('−', '-');											-- replace unicode minus with hyphen
	
	_, count = amount:gsub('%.', '')											-- count the number of decimal point characters 
	if 1 < count then
		return nil;																-- too many dots
	end

	_, count = amount:gsub(',', '')												-- count the number of grouping characters 
	if 0 == count then
		return amount;															-- no comma separators so we're done
	end;
	
	if amount:match ('[%-][%d%.,]+') then										-- if the amount is negative
		sign, amount = amount:match ('([%-])([%d%.,]+)');						-- strip off and save the sign
	end

	parts = mw.text.split (amount, '.', true);									-- split amount into digits and decimals
	decimals = table.remove (parts, 2) or '';									-- if there was a decimal portion, remove from the table and save it

	digits = mw.text.split (parts[1], ',')										-- split amount into groups 
	for i, v in ipairs (digits) do												-- loop through the groups
		if 1 == i then															-- left-most digit group
			if (3 < v:len() or not is_set (v)) then								-- first digit group: 1, 2, 3 digits; can't be empty string (first char was a comma)
				return nil;
			end
		else
			if v and 3 ~= v:len() then											-- all other groups must be three digits long
				return nil;	
			end
		end
	end

	return sign .. table.concat (digits) .. '.' .. decimals;					-- reassemble without commas and return
end


--[[--------------------------< C O N V E R T _ S T R I N G _ T O _  N U M E R I C >------------------------------------------------

Converts quantified number/string combinations to a number e.g. 1 thousand to 1000.

]]

local function convert_string_to_numeric (amount)
	local quantifiers = {['thousand'] = 1000, ['million'] = 1000000, ['m'] = 1000000, ['billion'] = 1000000000, ['b'] = 1000000000, ['trillion'] = 1000000000000};

	
	local n, q = amount:match ('([%-−]?[%d%.,]+)%s*(%a+)$');						-- see if there is a quantifier following a number; zero or more space characters
	if nil == n then
		n, q = amount:match ('([%-−]?[%d%.,]+) (%a+)$')							-- see if there is a quantifier following a number; nbsp html entity ({{format price}} output
	end
	if nil == n then return amount end;											-- if not <number><space><quantifier> return amount unmolested
	
	n = n:gsub (',', '');														-- strip comma separators if present
	q = q:lower();																-- set the quantifier to lower case

	if nil == quantifiers[q] then return amount end;							-- if not a recognized quantifier
	
	return tostring (n * quantifiers[q]);										-- return a string, not a number
end


--[[--------------------------< C U R R E N C Y >--------------------------------------------------------------

Template:CurrencyConvert 入口点，含有三个函数：
	positional (1st), |amount=, |Amount=	: digits and decimal points only
	positional (2nd), |type=, |Type=		: code that identifies the currency
	|first=									: uses currency name instead of symbol

]]

local function CurrencyConvert (frame)
	local args = require('Module:Arguments').getArgs (frame);

	local amount, code;
	local long_form = false;
	local linked = true;

	if not is_set (args[1]) then
		return '<span style="font-size:inherit" class="error">{{CurrencyConvert}} – invalid amount ([[Template:CurrencyConvert/doc#Error_messages|help]])</span>';
	end
	
--	amount = lang:parseFormattedNumber(args[1]);								-- if args[1] can't be converted to a number then error (this just strips grouping characters)
--	if args[1]:find ('[^%d%.]') or not amount then								-- non-digit characters or more than one decimal point (because lag:parse... is broken)
--		return '<span style="font-size:inherit" class="error">{{CurrencyConvert}} – invalid amount ([[Template:CurrencyConvert/doc#Error_messages|help]])</span>';
--	end
	amount = convert_string_to_numeric (args[1]);
	amount = parse_formatted_number(amount);									-- if args[1] can't be converted to a number then error
	if not amount then
		return '<span style="font-size:inherit" class="error">{{CurrencyConvert}} – invalid amount ([[Template:CurrencyConvert/doc#Error_messages|help]])</span>';
	end
	
	if not is_set(args[2]) then													-- if not provided
		code = 'USD';															-- default to USD
	else
		code = args[2]:upper();													-- always upper case; used as index into data tables which all use upper case
	end
	
	if args[3] then																-- this is the |first= parameter  TODO: make this value meaningful? y, yes, true?
		long_form = true;
	end
	
	if 'no' == args[4] then														-- this is the |linked= parameter; defaults to 'yes'; any value but 'no' means yes
		linked = false;
	end

	return render_currency (amount, code, long_form, linked)
end

return {
	CurrencyConvert = CurrencyConvert,														-- template entry point
	_render_currency = render_currency,											-- other modules entry point
	}