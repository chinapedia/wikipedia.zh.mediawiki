-- This template is a copy of the ISXN validation code from [[Module:Citation/CS1|Module:Citation/CS1]]
-- which allows for validating ISBN, ISMN, and ISSN without invoking a citation template

local p = {}

--[[--------------------------< IS _ V A L I D _ I S X N >-----------------------------------------------------

ISBN-10 and ISSN validator code calculates checksum across all isbn/issn digits including the check digit. ISBN-13 is checked in check_isbn().
If the number is valid the result will be 0. Before calling this function, issbn/issn must be checked for length and stripped of dashes,
spaces and other non-isxn characters.

]]

local function is_valid_isxn (isxn_str, len)
	local temp = 0;
	isxn_str = { isxn_str:byte(1, len) };	-- make a table of byte values '0' → 0x30 .. '9'  → 0x39, 'X' → 0x58
	len = len+1;							-- adjust to be a loop counter
	for i, v in ipairs( isxn_str ) do		-- loop through all of the bytes and calculate the checksum
		if v == string.byte( "X" ) then		-- if checkdigit is X (compares the byte value of 'X' which is 0x58)
			temp = temp + 10*( len - i );	-- it represents 10 decimal
		else
			temp = temp + tonumber( string.char(v) )*(len-i);
		end
	end
	return temp % 11 == 0;					-- returns true if calculation result is zero
end


--[[--------------------------< IS _ V A L I D _ I S X N  _ 1 3 >----------------------------------------------

ISBN-13 and ISMN validator code calculates checksum across all 13 isbn/ismn digits including the check digit.
If the number is valid, the result will be 0. Before calling this function, isbn-13/ismn must be checked for length
and stripped of dashes, spaces and other non-isxn-13 characters.

]]

local function is_valid_isxn_13 (isxn_str)
	local temp=0;
	
	isxn_str = { isxn_str:byte(1, 13) };										-- make a table of byte values '0' → 0x30 .. '9'  → 0x39
	for i, v in ipairs( isxn_str ) do
		temp = temp + (3 - 2*(i % 2)) * tonumber( string.char(v) );				-- multiply odd index digits by 1, even index digits by 3 and sum; includes check digit
	end
	return temp % 10 == 0;														-- sum modulo 10 is zero when isbn-13/ismn is correct
end

--[[--------------------------< C H E C K _ I S B N >------------------------------------------------------------

Determines whether an ISBN string is valid

]]

local function check_isbn( isbn_str, error_string )
	if nil ~= isbn_str:match("[^%s-0-9X]") then -- fail if isbn_str contains anything but digits, hyphens, or the uppercase X
		return error_string;
	end
	isbn_str = isbn_str:gsub( "-", "" ):gsub( " ", "" );	-- remove hyphens and spaces
	local len = isbn_str:len();
 
	if len ~= 10 and len ~= 13 then
		return error_string;
	end

	if len == 10 then
		if isbn_str:match( "^%d*X?$" ) == nil then 
			return error_string; 
		end
		return is_valid_isxn(isbn_str, 10) and '' or error_string;
	else
		local temp = 0;
		if isbn_str:match( "^97[89]%d*$" ) == nil then -- isbn13 begins with 978 or 979; ismn begins with 979
			return error_string; 
		end
		return is_valid_isxn_13 (isbn_str) and '' or error_string;
	end
end

--[[--------------------------< C H E C K _ I S M N >------------------------------------------------------------

Determines whether an ISMN string is valid.  Similar to isbn-13, ismn is 13 digits begining 979-0-... and uses the
same check digit calculations.  See http://www.ismn-international.org/download/Web_ISMN_Users_Manual_2008-6.pdf
section 2, pages 9–12.

]]

local function check_ismn (id, error_string)
	local text;
	local valid_ismn = true;

	id=id:gsub( "[%s-–]", "" );													-- strip spaces, hyphens, and endashes from the ismn

	if 13 ~= id:len() or id:match( "^9790%d*$" ) == nil then					-- ismn must be 13 digits and begin 9790
		valid_ismn = false;
	else
		valid_ismn=is_valid_isxn_13 (id);										-- validate ismn
	end

	return valid_ismn and '' or error_string
end

--[[--------------------------< I S S N >----------------------------------------------------------------------

Validate and format an issn.  This code fixes the case where an editor has included an ISSN in the citation but has separated the two groups of four
digits with a space.  When that condition occurred, the resulting link looked like this:

	|issn=0819 4327 gives: [http://www.worldcat.org/issn/0819 4327 0819 4327]  -- can't have spaces in an external link
	
This code now prevents that by inserting a hyphen at the issn midpoint.  It also validates the issn for length and makes sure that the checkdigit agrees
with the calculated value.  Incorrect length (8 digits), characters other than 0-9 and X, or checkdigit / calculated value mismatch will all cause a check issn
error message.

]]

local function check_issn(id, error_string)
	local issn_copy = id;		-- save a copy of unadulterated issn; use this version for display if issn does not validate
	local text;
	local valid_issn = true;

	if not id:match ('^%d%d%d%d%-%d%d%d[%dX]$') then
		return error_string;
	end
	
	id=id:gsub( "[%s-–]", "" );									-- strip spaces, hyphens, and endashes from the issn

	if 8 ~= id:len() or nil == id:match( "^%d*X?$" ) then		-- validate the issn: 8 digits long, containing only 0-9 or X in the last position
		valid_issn=false;										-- wrong length or improper character
	else
		valid_issn=is_valid_isxn(id, 8);						-- validate issn
	end

	return valid_issn and '' or error_string
end


------------------------------< E N T R Y   P O I N T S >--------------------------------------------------====

function p.check_isbn(frame)
	return check_isbn(frame.args[1] or frame:getParent().args[1], frame.args['error'] or frame:getParent().args['error'] or 'error')
end

function p.check_ismn(frame)
	return check_ismn(frame.args[1] or frame:getParent().args[1], frame.args['error'] or frame:getParent().args['error'] or 'error')
end

function p.check_issn(frame)
	return check_issn(frame.args[1] or frame:getParent().args[1], frame.args['error'] or frame:getParent().args['error'] or 'error')
end

return p