--
-- This module implements {{URL}}
--

local p = {}
 
local function safeUri(s)
    local success, uri = pcall(function()
        return mw.uri.new(s)
    end)
    if success then
        return uri
    end
end

function p._url(url, text)
    url = mw.text.trim(url or '')
    text = mw.text.trim(text or '')
    
    if url == '' then
        if text == '' then
            return mw.getCurrentFrame():expandTemplate{ title = 'tlx', args = { 'URL', "''example.com''", "''可选的显示文本''" } }
        else
            return text
        end
    end
    
    -- If the URL contains any unencoded spaces, encode them, because MediaWiki will otherwise interpret a space as the end of the URL.
    url = mw.ustring.gsub(url, '%s', function(s) return mw.uri.encode(s, 'PATH') end)
    
    -- If there is an empty query string or fragment id, remove it as it will cause mw.uri.new to throw an error
    url = mw.ustring.gsub(url, '#$', '')
    url = mw.ustring.gsub(url, '%?$', '')
    
    -- If it's an HTTP[S] URL without the double slash, fix it.
    url = mw.ustring.gsub(url, '^[Hh][Tt][Tt][Pp]([Ss]?):(/?)([^/])', 'http%1://%3')

    -- Handle URLs from Wikidata of the format http://
    url = mw.ustring.gsub(url, '^[Hh][Tt][Tt][Pp]([Ss]?)://', 'http%1://')
    
    local uri = safeUri(url)
    
    -- Handle URL's without a protocol and URL's that are protocol-relative, 
    -- e.g. www.example.com/foo or www.example.com:8080/foo, and //www.example.com/foo
    if uri and (not uri.protocol or (uri.protocol and not uri.host)) and url:sub(1, 2) ~= '//' then
        url = 'http://' .. url
        uri = safeUri(url)
    end
    
    if text == '' then
        if uri then
            if uri.path == '/' then uri.path = '' end
            
            local port = ''
            if uri.port then port = ':' .. uri.port end
            
            text = mw.ustring.lower(uri.host or '') .. port .. (uri.relativePath or '')

			-- Add <wbr> before _/.-# sequences
			text = mw.ustring.gsub(text,"(/+)","<wbr/>%1")      -- This entry MUST be the first. "<wbr/>" has a "/" in it, you know.
			text = mw.ustring.gsub(text,"(%.+)","<wbr/>%1")
			-- text = mw.ustring.gsub(text,"(%-+)","<wbr/>%1") 	-- DISABLED for now
			text = mw.ustring.gsub(text,"(%#+)","<wbr/>%1")
			text = mw.ustring.gsub(text,"(_+)","<wbr/>%1")
        else -- URL is badly-formed, so just display whatever was passed in
            text = url
        end
    end

    return mw.ustring.format('<span class="url">[%s %s]</span>', url, text)
end

function p.url(frame)
    local templateArgs = frame.args
	local parentArgs = frame:getParent().args;
    local url = templateArgs[1] or parentArgs[1] or ''
    local text = templateArgs[2] or parentArgs[2]
    if not text then
    	url = url or extractUrl(templateArgs) or extractUrl(parentArgs);
	end
	text = text or ''
    return p._url(url, text)
end
function extractUrl(args)
	for name, val in pairs(args) do
		local url = name .. "=" .. val;
		url = mw.ustring.gsub(url, '^[Hh][Tt][Tt][Pp]([Ss]?):(/?)([^/])', 'http%1://%3')
		local uri = safeUri(url);
		if uri and uri.host then
			return url
		end
	end
end
return p