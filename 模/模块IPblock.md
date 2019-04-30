-- Calculate the minimum-sized blocks of IP addresses that cover each
-- IPv4 or IPv6 address entered in the arguments.

local bit32 = require('bit32')

local Collection  -- a table to hold items
Collection = {
	add = function (self, item)
		if item ~= nil then
			self.n = self.n + 1
			self[self.n] = item
		end
	end,
	join = function (self, sep)
		return table.concat(self, sep)
	end,
	remove = function (self, pos)
		if self.n > 0 and (pos == nil or (0 < pos and pos <= self.n)) then
			self.n = self.n - 1
			return table.remove(self, pos)
		end
	end,
	sort = function (self, comp)
		table.sort(self, comp)
	end,
	new = function ()
		return setmetatable({n = 0}, Collection)
	end
}
Collection.__index = Collection

local function empty(text)
	-- Return true if text is nil or empty (assuming a string).
	return text == nil or text == ''
end

local timestamps = {}  -- cache
local function start_date(code, months)
	-- Return a timestamp string for a URL to list user contributions
	-- on and after the returned date.
	-- The code specifies the wanted format.
	-- For this module, only recent contributions are wanted, so the
	-- timestamp is today's date less the given number of months (1 to 12).
	local key = code .. months
	if not timestamps[key] then
		local date = os.date('!*t')  -- today's UTC date
		local y, m, d = date.year, date.month, date.day  -- full year, month (1-12), day (1-31)
		m = m - months
		if m <= 0 then
			m = m + 12
			y = y - 1
		end
		local limit = m == 2 and 28 or 30
		if d > limit then
			d = limit  -- good enough to ensure date is valid
		end
		timestamps['y-m-d' .. months] = string.format('%d-%02d-%02d', y, m, d)
		timestamps['ymdHMS' .. months] = string.format('%d%02d%02d000000', y, m, d)
	end
	return timestamps[key] or ''
end

local note_text = {
	range = '*Links for ranges show the contributions in the previous %s.',
	gadget = [=[
*<span id="need-gadget"></span>Contributions links for IPv6 ranges need the "<span style="color:green;">Allow /16, /24 and /27 – /32 CIDR ranges on Special:Contributions forms</span>" gadget enabled in [[Special:Preferences#mw-prefsection-gadgets|Special:Preferences]], and scripting enabled in the browser.]=],
}

local function make_note(strings, key)
	-- Record the fact that a particular note is needed, and return
	-- wikitext for a link to the note or '' if no link needed.
	if not strings.nonote then
		strings.notes = strings.notes or {}
		if not strings.notes[key] then
			if key == 'gadget' then
				strings.notes[key] = note_text[key]
			elseif key == 'range' then
				local when = 'month'
				if strings.months > 1 then
					when = strings.months .. ' months'
				end
				strings.notes[key] = string.format(note_text.range, when)
			else
				error('make_note: unexpected key')
			end
		end
		if key == 'gadget' then
			return ' [[#need-gadget|<sup>[note]</sup>]]'
		end
	end
	return ''
end

local function describe_total(total, isalloc)
	-- Return text describing given number of addresses or /64 allocations.
	if total <= 9999 then
		-- Can have fractions if total is the number of /64 allocations.
		if total < 9 then
			return (string.format('%.1f', total):gsub('%.0$', ''))
		end
		return string.format('%.0f', total)
	end
	if not isalloc then
		local alloc = 2^64
		if total >= alloc then
			return describe_total(total / alloc, true) .. ' /64'
		end
	end
	total = total/1024
	local suffix = 'K'
	if total >= 1024 then
		total = total/1024
		suffix = 'M'
		if total >= 1024 then
			total = total/1024
			suffix = 'G'
			if total > 64 then
				return '>64G'
			end
		end
	end
	return string.format('%.0f', total) .. suffix
end

local function describe_size(ipsize, size)
	-- Return text describing how many IPs are in a range with size = prefix length.
	local function numtext(n)
		if n <= 16 then
			return tostring(2^n)
		end
		if n <= 19 then
			return tostring(2^(n - 10)) .. 'K'
		end
		if n <= 29 then
			return tostring(2^(n - 20)) .. 'M'
		end
		if n <= 36 then
			return tostring(2^(n - 30)) .. 'G'
		end
		return '>64G'
	end
	local host = ipsize - size
	if host <= 32 then
		-- IPv4 or IPv6.
		return numtext(host)
	end
	-- Must be IPv6.
	if host <= 64 then
		local s = ({
			[64] = '1',  [63] = '50%', [62] = '25%', [61] = '12%',
			[60] = '6%', [59] = '3%',  [58] = '2%'
		})[host] or '<1%'
		return s .. ' /64'
	end
	-- IPv6 with size < 64.
	return numtext(host - 64) .. ' /64'
end

local function ipv6_string(ip)
	-- Return a string equivalent to the given IPv6 address.
	local z1, z2  -- indices of run of zeros to be displayed as "::"
	local zstart, zcount
	for i = 1, 9 do
		-- Find left-most occurrence of longest run of two or more zeros.
		if i < 9 and ip[i] == 0 then
			if zstart then
				zcount = zcount + 1
			else
				zstart = i
				zcount = 1
			end
		else
			if zcount and zcount > 1 then
				if not z1 or zcount > z2 - z1 + 1 then
					z1 = zstart
					z2 = zstart + zcount - 1
				end
			end
			zstart = nil
			zcount = nil
		end
	end
	local parts = Collection.new()
	for i = 1, 8 do
		if z1 and z1 <= i and i <= z2 then
			if i == z1 then
				if z1 == 1 or z2 == 8 then
					if z1 == 1 and z2 == 8 then
						return '::'
					end
					parts:add(':')
				else
					parts:add('')
				end
			end
		else
			parts:add(string.format('%x', ip[i]))
		end
	end
	return parts:join(':')
end

local function ip_string(ip)
	-- Return a string equivalent to given IP address (IPv4 or IPv6).
	if ip.n == 2 then
		-- IPv4.
		local parts = {}
		for i = 1, 2 do
			local w = ip[i]
			local q = i == 1 and 1 or 3
			parts[q] = math.floor(w / 256)
			parts[q+1] = w % 256
		end
		return table.concat(parts, '.')
	end
	return ipv6_string(ip)
end

-- Metatable for some operations on IP addresses.
local ipmt = {
	__eq = function (lhs, rhs)
		-- Return true if values in numbered tables match.
		if lhs.n == rhs.n then
			for i = 1, lhs.n do
				if lhs[i] ~= rhs[i] then
					return false
				end
			end
			return true
		end
		return false
	end,
	__lt = function (lhs, rhs)
		-- Return true if lhs < rhs; for sort.
		if lhs.n == rhs.n then
			for i = 1, lhs.n do
				if lhs[i] ~= rhs[i] then
					return lhs[i] < rhs[i]
				end
			end
			return false
		end
		return lhs.n < rhs.n  -- sort IPv4 before IPv6, although not needed
	end,
}

local function ipv4_address(ip_str)
	-- Return a collection of two 16-bit words (numbers) equivalent
	-- to the IPv4 address given as a quad-dotted string, or
	-- return nil if invalid.
	-- This representation is for compatibility with IPv6 addresses.
	local parts = Collection.new()
	local s = ip_str:match('^%s*(.-)%s*$') .. '.'
	for item in s:gmatch('(.-)%.') do
		parts:add(item)
	end
	if parts.n == 4 then
		for i, s in ipairs(parts) do
			if s:match('^%d+$') then
				local num = tonumber(s)
				if 0 <= num and num <= 255 then
					if num > 0 and s:match('^0') then
						-- A redundant leading zero is an error because it is for an IP in octal.
						return nil
					end
					parts[i] = num
				else
					return nil
				end
			else
				return nil
			end
		end
		local result = Collection.new()
		for i = 1, 3, 2 do
			result:add(parts[i] * 256 + parts[i+1])
		end
		return setmetatable(result, ipmt)
	end
	return nil
end

local function ipv6_address(ip_str)
	-- Return a collection of eight 16-bit words (numbers) equivalent
	-- to the IPv6 address given as a colon-delimited string, or
	-- return nil if invalid.
	local _, n = ip_str:gsub(':', ':')
	if n < 7 then
		ip_str, n = ip_str:gsub('::', string.rep(':', 9 - n))
	end
	local parts = Collection.new()
	for item in (ip_str .. ':'):gmatch('(.-):') do
		parts:add(item)
	end
	if parts.n == 8 then
		for i, s in ipairs(parts) do
			if s == '' then
				parts[i] = 0
			else
				local num = tonumber('0x' .. s)
				if num and 0 <= num and num <= 65535 then
					parts[i] = num
				else
					return nil
				end
			end
		end
		return setmetatable(parts, ipmt)
	end
	return nil
end

local function common_length(num1, num2, nr_bits)
	-- Return number of prefix bits that two integers have in common.
	-- Number of bits in each number is nr_bits = 16, 8, 4, 2 or 1.
	if nr_bits <= 1 then
		return num1 == num2 and 1 or 0
	end
	local half = nr_bits / 2
	local splitter = 2^half
	local upper1, lower1 = math.modf(num1 / splitter)
	local upper2, lower2 = math.modf(num2 / splitter)
	if upper1 == upper2 then
		lower1 = math.floor(lower1 * splitter + 0.5)
		lower2 = math.floor(lower2 * splitter + 0.5)
		return half + common_length(lower1, lower2, half)
	end
	return common_length(upper1, upper2, half)
end

local function common_prefix_length(ip1, ip2)
	-- Return number of prefix bits that two IPs have in common.
	-- Caller ensures that both IPs are IPv4 or both are IPv6.
	local size = 0
	for i = 1, ip1.n do
		local w1, w2 = ip1[i], ip2[i]
		if w1 == w2 then
			size = size + 16
		else
			return size + common_length(w1, w2, 16)
		end
	end
	return size
end

local function ip_prefix(ip, length)
	-- Return a copy of ip masked to contain only the prefix of given length.
	local result = { n = ip.n }
	for i = 1, ip.n do
		if length > 0 then
			if length >= 16 then
				result[i] = ip[i]
				length = length - 16
			else
				result[i] = bit32.band(ip[i], bit32.arshift(0xffff8000, length - 1))
				length = 0
			end
		else
			result[i] = 0
		end
	end
	return setmetatable(result, ipmt)
end

local function ip_incremented(ip)
	-- Return a new IP equal to ip + 1.
	-- Will wraparound (255.255.255.255 + 1 = 0.0.0.0)!
	local result = { n = ip.n }
	local carry = 1
	for i = ip.n, 1, -1 do
		local sum = ip[i] + carry
		if sum >= 0x10000 then
			carry = 1
			sum = sum - 0x10000
		else
			carry = 0
		end
		result[i] = sum
	end
	return setmetatable(result, ipmt)
end

local function is_next_ip(ip1, ip2)
	-- Return true if ip2 is the next IP after ip1 (ip2 == ip1 + 1).
	-- IPs are sorted and unique so ip1 < ip2 and can ignore wrapping to zero.
	-- This is lower overhead than making a new incremented IP then comparing.
	if ip1 and ip2 then
		local carry = 1
		for i = ip1.n, 1, -1 do
			local sum = ip1[i] + carry
			if sum >= 0x10000 then
				carry = 1
				sum = sum - 0x10000
			else
				carry = 0
			end
			if sum ~= ip2[i] then
				return false
			end
		end
		return true
	end
end

-- Each IP in a range except for the last IP has a 'common' field which is
-- a number specifying how many bits are common between the prefixes of this
-- IP and the next IP (0 if this IP starts with 0 and the next starts with 1).
-- Each non-empty range has exactly one "minimum common", that is, its value
-- of common is smaller than all others. That there is only one minimum common
-- follows from the fact that the IPs are unique and sorted.
local function make_range(iplist, ifirst, ilast)
	-- Return a table for the range of IPs from iplist[ifirst] to iplist[ilast] inclusive.
	local imin, vmin, done
	if ifirst < ilast then
		for i = ifirst, ilast - 1 do
			-- Find the (unique) minimum of common lengths.
			local common = iplist[i].common
			if vmin then
				if vmin > common then
					vmin = common
					imin = i
				end
			else
				vmin = common
				imin = i
			end
		end
	else
		vmin = iplist.ipsize
		imin = ifirst
		done = true
	end
	if vmin > iplist.allocation then
		-- For IPv6, the default allocation is /64 and there is no point having
		-- more precise ranges as they add unnecessary complexity.
		-- However, using results=all sets allocation = 128 so vmin is not changed.
		vmin = iplist.allocation
	end
	return {
		ifirst = ifirst,  -- index of first IP
		ilast = ilast,    -- index of last IP
		imin = imin,      -- index of IP with minimum common
		size = vmin,      -- number of common bits in prefix (the minimum)
		prefix = ip_prefix(iplist[imin], vmin),  -- IP table of the base IP
		done = done,      -- true if know that this range cannot be improved
	}
end

local function split_range(iplist, range, depth)
	-- Return a table of two or more ranges that more precisely target
	-- the IPs in range, or return nothing if unable to improve range.
	depth = depth and depth + 1 or 0
	if depth <= 20 and  -- 20 examines 1M contiguous addresses down to individual IPs
			not range.done and
			range.size < iplist.allocation and
			range.ifirst < range.ilast then
		local imin = range.imin
		assert(imin and range.ifirst <= imin and imin < range.ilast)
		local r1 = make_range(iplist, range.ifirst, range.imin)
		local r2 = make_range(iplist, range.imin + 1, range.ilast)
		local pointless = range.size + 1
		if r1.size > pointless or r2.size > pointless then
			return { r1, r2 }
		end
		local result = Collection.new()
		local function store_split(range)
			local split = split_range(iplist, range, depth)
			if split then
				for _, r in ipairs(split) do
					result:add(r)
				end
				return true
			else
				result:add(range)
			end
		end
		local improved1 = store_split(r1)
		local improved2 = store_split(r2)
		if improved1 or improved2 then
			return result
		end
	end
	range.done = true
end

local function better_summary(iplist, summary)
	-- Return a better summary that more precisely targets the specified IPs,
	-- or return nil if unable to improve the summary.
	local better = Collection.new()
	local improved
	for _, range in ipairs(summary) do
		local split = split_range(iplist, range)
		if split then
			improved = true
			for _, r in ipairs(split) do
				better:add(r)
			end
		else
			better:add(range)
		end
	end
	return improved and better
end

local function make_summaries(iplist)
	-- Return a collection where each item is a summary.
	-- A summary is a table of one or more ranges.
	-- A summary covers all the given IPs and probably more.
	-- A range is a table representing a CIDR block such as 1.2.248.0/21.
	-- The first summary found is a single range; each subsequent summary
	-- (if any) uses more ranges to better target the given IPs.
	-- The result omits any summary with a range size that is too small (too many IPs).
	local function good_size(summary)
		for _, range in ipairs(summary) do
			if range.size < iplist.minsize then
				return false
			end
		end
		return true
	end
	local summaries = Collection.new()
	if iplist.n > 0 then
		for i = 1, iplist.n - 1 do
			-- Set length of prefixes common between each pair of IPs.
			iplist[i].common = common_prefix_length(iplist[i], iplist[i+1])
		end
		local summary = { make_range(iplist, 1, iplist.n) }
		while summary and summaries.n < iplist.maxresults do
			if good_size(summary) then
				summaries:add(summary)
			end
			summary = better_summary(iplist, summary)
		end
	end
	return summaries
end

local function extract_ipv4(result, omitted, line)
	-- Extract any IPv4 addresses from given line or throw error.
	-- Accept CIDR /n to specify a range (only accept 16 to 32).
	-- Addresses must be delimited with whitespace to reduce false positives.
	local function store(hit)
		local n = 32
		local lhs, rhs = hit:match('^(.-)/(%d+)$')
		if lhs then
			hit = lhs
			n = tonumber(rhs)
			if not (n and 16 <= n and n <= 32) then
				error('CIDR /n only accepts n = 16 to 32, invalid: ' .. lhs .. '/' .. rhs, 0)
			end
		end
		local ip = ipv4_address(hit)
		if ip then
			if n == 32 then
				result:add(ip)
			else
				if ip ~= ip_prefix(ip, n) then
					error('Invalid base address (host bits should be zero): ' .. hit, 0)
				end
				for _ = 1, 2^(32 - n) do
					result:add(ip)
					ip = ip_incremented(ip)
				end
			end
		else
			omitted:add(hit)
		end
	end
	line = line:gsub(':', ' ')  -- so wikitext indents or other colons don't obscure an IVp4 address
	for hit in line:gmatch('%S+') do
		if hit:match('^%d+%.%d+[%.%d/]+$') then
			local _, n = hit:gsub('%.', '.')
			if n >= 3 then
				store(hit)
			end
		end
	end
end

local function extract_ipv6(result, omitted, line)
	-- Extract any IPv6 addresses from given line or throw error.
	-- Addresses must be delimited with whitespace to reduce false positives.
	-- Want to accept all valid IPv6 despite the fact that contributors will
	-- not have an address starting with ':'.
	-- Also want to be able to parse arbitrary wikitext which might use colons
	-- for indenting. To achieve that, if an address at the start of a line
	-- is valid, use it; otherwise strip any leading colons and try again.
	for pos, hit in line:gmatch('()(%S+)') do
		local ipstr, length = hit:match('^([:%x]+)(/?%d*)$')
		if ipstr then
			local _, n = ipstr:gsub(':', ':')
			if n >= 2 then
				local ip = ipv6_address(ipstr)
				if not ip and pos == 1 then
					ipstr, n = ipstr:gsub('^:+', '')
					if n > 0 then
						ip = ipv6_address(ipstr)
					end
				end
				if ip then
					if length and #length > 0 then
						error('CIDR /n not accepted for IPv6: ' .. hit, 0)
					end
					result:add(ip)
				else
					omitted:add(hit)
				end
			end
		end
	end
end

local function contribs(address, strings, ipbase, size)
	-- Return a URL or wikilink to list the contributions for an IP or IP range,
	-- or return an empty string if cannot do anything useful.
	-- The given address is a string of either a single IP or a CIDR range.
	-- If using old system:
	--   For IPv6 CIDR, return a Special:Contributions link using an asterisk
	--   wildcard which should work if the user has enabled the gadget
	--   "Allow /16, /24 and /27 – /32 CIDR ranges on Special:Contributions".
	local encoded, count = address:gsub('/', '%%2F')
	if strings.want_old and count > 0 then
		make_note(strings, 'range')
		if address:find(':', 1, true) then
			if ipbase and size then
				local digits = math.floor(size / 4)
				if digits < 3 then
					digits = 3
				end
				local wildcard = digits % 4 == 0 and ':*' or '*'
				local parts = {}
				for i = 1, 8 do
					local hex = string.format('%X', ipbase[i])  -- must be uppercase
					if digits >= 4 then
						parts[i] = hex
						digits = digits - 4
						if digits <= 0 then
							break
						end
					else
						local nz  -- number of leading zeros in this group of four digits
						if hex == '0' then
							nz = 4
						else
							nz = 4 - #hex
						end
						if digits <= nz then
							-- Cannot properly handle this case; have to omit group
							-- because "0" never occurs as the first digit.
							wildcard = ':*'
						else
							hex = string.rep('0', nz) .. hex  -- four digits
							parts[i] = hex:sub(1, digits)
						end
						break
					end
				end
				address = table.concat(parts, ':') .. wildcard
				local url = '[https://en.wikipedia.org/wiki/Special:Contributions/%s?ucstart=%s c]'
				-- %s = IPv6 prefix address in uppercase with '*' wildcard at end
				-- %s = Start date formatted 'yyyymmdd000000'
				return string.format(url, address, start_date('ymdHMS', strings.months)) .. make_note(strings, 'gadget')
			end
			return ''  -- no contributions link available
		end
		local url = '[https://tools.wmflabs.org/xtools/rangecontribs/?project=en.wikipedia.org&namespace=all&limit=50&text=%s&begin=%s c]'
		-- %s = IPv4 CIDR range with '/' changed to '%2F'
		-- %s = Start date formatted 'yyyy-mm-dd'
		return string.format(url, encoded, start_date('y-m-d', strings.months))
	end
	return '[[Special:Contributions/'_.._address_.._'|c]]'
end

-- Strings for results using plain text.
-- The pre tags used are html which do not provide "nowiki",
-- but that is not required by the text used.
local plaintext = {

header = [=[
<pre>
Total       Affected     Given        Range]=],

footer = '</pre>',

sumfirst = [=[
----------------------------------------------------------
%s%-12s %-12s %-11d %s%s]=],
-- %s = empty string (dummy for compatibility)
-- %s = total affected
-- %s = affected
-- %d = given (number of addresses given in input covered by this range)
-- %s = IP address range
-- %s = empty string

sumnext = [=[
             %-12s %-11d %s%s]=],
-- %s = affected
-- %d = given
-- %s = IP address range
-- %s = empty string

}

-- Strings for results using a table in wikitext.
local wikitable = {

header = [=[
{| class="wikitable"
! Total<br />affected !! Affected<br />addresses !! Given<br />addresses !! Range !! Contribs]=],

footer = '|}',

sumfirst = [=[
|- style="background: darkgray; height: 6px;"
|colspan="5" |
|- style="vertical-align: top;"
|rowspan="%s" |%s ||%s ||%d ||%s ||%s]=],
-- %s = string of number of ranges in summary (number of rows)
-- %s = total affected
-- %s = affected
-- %d = given
-- %s = IP address range
-- %s = contributions link

sumnext = [=[
|-
|%s ||%d ||%s ||%s]=],
-- %s = affected
-- %d = given
-- %s = IP address range
-- %s = contributions link

}

local function show_summary(lines, strings, iplist, summary)
	-- Show the summary by adding table wikitext or plain text to lines.
	local want_plain = iplist.want_plain
	local total = 0
	for _, range in ipairs(summary) do
		-- A number is a double which easily handles 2^128 = 3.4e38.
		total = total + 2^(iplist.ipsize - range.size)
	end
	for i, range in ipairs(summary) do
		local prefix = ip_string(range.prefix)
		local size = range.size
		local affected = describe_size(iplist.ipsize, size)
		local given = range.ilast - range.ifirst + 1
		local address
		local link = ''
		if size == iplist.ipsize then
			address = prefix
			if not want_plain then
				link = contribs(address, strings)
			end
		else
			address = prefix .. '/' .. size
			if not want_plain then
				link = contribs(address, strings, range.prefix, size)
			end
		end
		local s
		if i == 1 then
			s = string.format(strings.sumfirst,
					want_plain and '' or tostring(#summary),
					describe_total(total),
					affected, given, address, link)
		else
			s = string.format(strings.sumnext,
					affected, given, address, link)
		end
		-- Pre tags returned by a module are html tags, not like wikitext <pre>...</pre>.
		lines:add(want_plain and mw.text.nowiki(s) or s)
	end
end

local function process_ips(lines, iplist, omitted)
	-- Process a list of IP addresses, adding text of results to lines.
	-- The list should contain either all IPv4 addresses, or all IPv6 (not a mixture).
	local seq1, seq2, seqmany
	local function show_sequence()
		if seq1 and seq2 then
			local text = ip_string(seq1)
			if seqmany then
				seqmany = false
				text = text .. ' – ' .. ip_string(seq2)
			end
			seq1 = nil
			seq2 = nil
			local markup = text:sub(1, 1) == ':' and ':<nowiki/>' or ':'
			lines:add(markup .. text)
		end
	end
	local function show_ip(ip)
		-- Show IP or record it to be included in a "from to" sequence of IPs.
		if is_next_ip(seq2, ip) then
			seq2 = ip
			seqmany = true
		else
			show_sequence()
			seq1 = ip
			seq2 = ip
			seqmany = false
		end
	end
	if iplist.n < 1 then
		return
	end
	if lines.n > 0 then
		lines:add('')
	end
	if omitted.n > 0 then
		lines:add('Warning, omitted as invalid: ' .. omitted:join(' '))
		lines:add('')
	end
	local heading_line
	if not iplist.nolist then
		lines:add('')  -- this blank line is replaced with a heading
		heading_line = lines.n
	end
	local duplicates = Collection.new()
	local previous
	iplist:sort()
	-- Check for duplicates which can interfere with method to get ranges.
	for i, ip in ipairs(iplist) do
		if previous == ip then
			duplicates:add(i)  -- index to omit duplicate later
		elseif not iplist.nolist then
			show_ip(ip)
		end
		previous = ip
	end
	show_sequence()
	local duplicate_text = ''
	if duplicates.n > 0 then
		duplicate_text = ' (after omitting some duplicates)'
		for i = duplicates.n, 1, -1 do
			iplist:remove(duplicates[i])
		end
	end
	local heading_text = string.format('Sorted %d %s address%s',
		iplist.n,
		iplist.ipname,
		iplist.n == 1 and '' or 'es'
		)
	if heading_line then
		lines[heading_line] = heading_text .. duplicate_text .. ':'
	end
	local strings = iplist.want_plain and plaintext or wikitable
	strings.notes = nil  -- needed when module is kept loaded for multiple tests
	strings.want_old = iplist.want_old
	strings.nonote = iplist.nonote
	strings.months = iplist.months
	lines:add(strings.header)
	local upto = lines.n
	for _, summary in ipairs(make_summaries(iplist)) do
		show_summary(lines, strings, iplist, summary)
	end
	lines:add(strings.footer)
	if upto + 1 == lines.n then
		-- Show message in the very unlikely event that no results are found.
		lines:add('----')
		lines:add('No suitable ranges found; use <code>|results=all</code> to see all ranges.')
	end
	if strings.notes then
		lines:add('')
		lines:add("'''Notes'''")
		for _, key in ipairs({'range', 'gadget'}) do
			if strings.notes[key] then
				lines:add(strings.notes[key])
			end
		end
	end
end

local function make_options(args)
	-- Return table of options from validated args or throw error.
	local options = {}
	if not empty(args.comment) then
		options.comment = args.comment
	end
	-- Parameter 'months' is only used if 'old' is also used.
	local months = math.floor(tonumber(args.months) or tonumber(args.month) or 1)
	if months < 1 then
		months = 1
	elseif months > 12 then
		months = 12
	end
	options.months = months  -- silently ignore invalid input
	local allocation
	if not empty(args.allocation) then
		allocation = tonumber(args.allocation)
		if not (allocation and 48 <= allocation and allocation <= 128) then
			error('Invalid allocation "' .. args.allocation .. '" (should be 48 to 128; default is 64)', 0)
		end
	end
	local maxresults
	if not empty(args.results) then
		if args.results == 'all' then
			options.all = true
			allocation = allocation or 128
			maxresults = 1000
		else
			maxresults = tonumber(args.results)
			if not (maxresults and 1 <= maxresults and maxresults <= 100) then
				error('Invalid results "' .. args.results .. '" (should be 1 to 100)', 0)
			end
		end
	end
	options.allocation = allocation or 64
	options.maxresults = maxresults or 10
	local keywords = {
		-- Table of k, v strings.
		-- If an argument matches k, an option named v is set to true.
		ok = 'noannounce',
		old = 'want_old',
		nolist = 'nolist',
		nonote = 'nonote',
		text = 'text',
	}
	local want_old
	for i, arg in ipairs(args) do
		local flag = keywords[arg:match('^%s*(%w+)%s*$')]
		if flag then
			options[i] = 'skip'
			options[flag] = true
			if flag == 'want_old' then
				want_old = true
			end
		end
	end
	if not want_old then
		options.nonote = true
	end
	return options
end

local function _IPblock(args)
	-- Process given args; can be called from another module.
	-- Throw an error if need to report a problem.
	local options = make_options(args)
	local v4list, v4omitted = Collection.new(), Collection.new()
	local v6list, v6omitted = Collection.new(), Collection.new()
	v4list.ipsize = 32
	v4list.ipname = 'IPv4'
	v6list.ipsize = 128
	v6list.ipname = 'IPv6'
	v4list.allocation = 32
	v6list.allocation = options.allocation
	if options.all then
		v4list.minsize = 0
		v6list.minsize = 0
	else
		v4list.minsize = 16  -- cannot block more IPs than /16 for IPv4
		v6list.minsize = 19  -- or /19 for IPv6 ($wgBlockCIDRLimit)
	end
	for _, k in ipairs({'maxresults', 'months', 'want_old', 'nolist', 'nonote'}) do
		v4list[k] = options[k]
		v6list[k] = options[k]
	end
	if options.text then
		v4list.want_plain = true
		v6list.want_plain = true
	end
	for i, arg in ipairs(args) do
		if options[i] ~= 'skip' then
			for line in string.gmatch(arg .. '\n', '[\t ]*(.-)[\t\r ]*\n') do
				-- Skip line if is empty or a comment.
				if line ~= '' then
					local comment = options.comment
					if not (comment and line:sub(1, #comment) == comment) then
						-- Replace accepted delimiters with a space.
						line = line:gsub('[!"#&\'()+,%-;<=>?[%]_{|}]', ' ')
						extract_ipv4(v4list, v4omitted, line)
						extract_ipv6(v6list, v6omitted, line)
					end
				end
			end
		end
	end
	if v4list.n < 1 and v6list.n < 1 then
		error('No valid IPv4 or IPv6 address in arguments', 0)
	end
	local lines = Collection.new()
	if not options.noannounce then
		-- 1: Commented out April 2016 as expired.
		-- 1: lines:add("'''Please see [[Template_talk:Blockcalc#Version_February_2016|this announcement]].'''")
		-- 2: Commented out December 2017 as expired.
		-- 2: lines:add("'''By default, links now use [[Special:Contributions|Special:Contributions]] per [[Template_talk:IP_range_calculator#Version_November_2017|this announcement]].'''")
	end
	process_ips(lines, v4list, v4omitted)
	process_ips(lines, v6list, v6omitted)
	return lines:join('\n')
end

local function IPblock(frame)
	-- Return wikitext to display the smallest IPv4 or IPv6 CIDR range that
	-- covers each address given in the arguments, or return error text.
	-- Input can have any mixture of IPs; IPv4 and IPv6 are processed separately.
	local ok, msg = pcall(_IPblock, frame:getParent().args)
	if ok then
		return msg
	end
	return '<strong class="error">Error: ' .. msg .. '</strong>'
end

local function sha1(frame)
	-- Return SHA-1 hash of first parameter.
	-- This is for use at [[User:Johnuniq/Security|User:Johnuniq/Security]] to generate hash of a password.
	local text = (frame.args[1] or ''):match("^%s*(.-)%s*$")
	if text ~= '' then
		return 'SHA-1 hash after removing any leading or trailing whitespace is <code>' .. mw.hash.hashValue('sha1', text) .. '</code>'
	end
	return 'Usage: <code>{{#invoke:IPblock|sha1|text}}</code> to display the SHA-1 hash of <code>text</code>.'
end

return {
	IPblock = IPblock,
	_IPblock = _IPblock,
	sha1 = sha1,
}