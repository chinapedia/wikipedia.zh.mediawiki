-- Creates a slideshow gallery where the order is randomised. Intended for use on portal pages.
local p = {}
local excerptModule =  require('Module:Excerpt')
local randomModule = require('Module:Random')
local redirectModule = require('Module:Redirect')

function cleanupArgs(argsTable)
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

function normaliseCssMeasurement(input)
	local suffix = string.reverse(string.sub(string.reverse(input), 1, 2))
	if ( suffix == 'px' ) or ( suffix == 'em' ) or ( string.sub(suffix, 2, 2) == '%' ) then
		return input
	else
		return input .. 'px'
	end
end

function makeOutput(galleryLines, maxWidth, containerClassName)
	local randomiseArgs = {	['t'] = galleryLines }
	local randomisedLines = randomModule.main('array', randomiseArgs)
	local galleryContent = table.concat(randomisedLines, '\n')
	local output = '<div class="' .. containerClassName .. '" style="max-width:' .. normaliseCssMeasurement(maxWidth) .. '; margin:-4em auto;">{{#tag:gallery|' .. galleryContent  .. '|mode=slideshow}}</div>'
	return output
end

function makeGalleryLine(file, caption, credit)
	local title = mw.title.new(file, "File" )
	local creditLine = ( credit and '<p><span style="font-size:88%">' .. credit .. '</span></p>' or '' )
	return title.prefixedText .. '{{!}}' .. ( caption or '' ) .. creditLine
end

function makeGalleryLinesTable(args)
	local galleryLinesTable = {}
	local i = 1
	while args[i] do
		table.insert(galleryLinesTable, makeGalleryLine(args[i], args[i+1], args['credit' .. (i+1)/2]))
		i = i + 2
	end
	return galleryLinesTable 
end

function extractGalleryFiles(wikitext)
	local gallery = mw.ustring.match(wikitext, '<gallery.->%s*(.-)%s*</gallery>')
	if not gallery then
		return false
	end
	gallery = mw.ustring.gsub(gallery, '|', '{{!}}')
	return mw.text.split(gallery, '%c')
end

function extractRegularFiles(wikitext)
	local files = {}
	local frame = mw.getCurrentFrame()
	local expand = function(template)
		return frame:preprocess(template)
	end
	for file in mw.ustring.gmatch(wikitext, '%b[]' ) do
		-- remove keywords that don't work in galleries
		file = mw.ustring.gsub(file, '|%s*thumb%s*([|%]])', '%1')
		file = mw.ustring.gsub(file, '|%s*thumbnail%s*([|%]])', '%1')
		file = mw.ustring.gsub(file, '|%s*left%s*([|%]])', '%1')
		file = mw.ustring.gsub(file, '|%s*right%s*([|%]])', '%1')
		file = mw.ustring.gsub(file, '|%s*center%s*([|%]])', '%1')
		file = mw.ustring.gsub(file, '|%s*framed?%s*([|%]])', '%1')
		file = mw.ustring.gsub(file, '|%s*frameless%s*([|%]])', '%1')
		file = mw.ustring.gsub(file, '|%s*upright%s*([|%]])', '%1')
		file = mw.ustring.gsub(file, '|%s*upright%s*=.-([|%]])', '%1')
		-- remove spaces prior to captions (which cause pre-formatted text)
		file = mw.ustring.gsub(file, '|%s*', '|')
		-- expand templates
		file = mw.ustring.gsub(file, '{%b{}}', expand)
		-- remove loose closing braces which don't have matching opening braces
		file = mw.ustring.gsub(file, '}}', '')
		-- remove loose opening braces which don't have matching closing braces (and the subsequent content, which is probably just a template name)
		file = mw.ustring.gsub(file, '{{.-([|%]])', '$1')
		-- replace pipes and equals (which would otherwise break the {{#tag:}} syntax)
		file = mw.ustring.gsub(file, '|', '{{!}}')
		file = mw.ustring.gsub(file, '=', '{{=}}')
		-- remove linebreaks
		file = mw.ustring.gsub(file, '\n\n', '<br>')
		file = mw.ustring.gsub(file, '\n', '')
		-- remove surrounding square brackets
		file = mw.ustring.gsub(file, '^%[%[', '')
		file = mw.ustring.gsub(file, '%]%]$', '')
		table.insert(files, file)
	end
	return files
end

function makeTranscludedGalleryLinesTables(args)
	local namespaceNumber = function(pagetitle)
		local titleObject = mw.title.new(pagetitle)
		return titleObject and titleObject.namespace
	end
	local lines = {}
	local i = 1
	while args[i] do
		if namespaceNumber(args[i]) == 6 then -- file namespace
			-- args[i] is either just the filename, or uses syntax File:Name.jpg##Caption##Credit
			local parts = mw.text.split(args[i], '##%s*')
			local filename = parts[1]
			local caption = args['caption'..i] or parts[2] or false
			local credit = args['credit'..i] or parts[3] or false
			local line = makeGalleryLine(filename, caption, credit)
			table.insert(lines, line)
		else
			local content, pagename = excerptModule.getContent(args[i])
			if not pagename then
				return error('Cannot read a valid page for "' .. args[i] .. '"', 0)
			elseif not content then
				return error('No content found on page "' .. args[i] .. '"', 0)
			end
			if args['section'..i] then
				content = excerptModule.getsection(content, args['section'..i]) or ''
			end
			content = excerptModule.cleanupText(content)
	
			local galleryFiles = extractGalleryFiles(content)
			if galleryFiles then
				for _, f in pairs(galleryFiles) do
					local filename = string.gsub(f, '{{!}}.*', '')
					local isOkay = excerptModule.checkimage(filename)
					if isOkay then
						table.insert(lines, f)
					end
				end
			end
	
			local otherFiles = excerptModule.parse(content, {fileflags="1-100"}, true)
			if otherFiles then
				for _, f in pairs(extractRegularFiles(otherFiles)) do
					if f and f ~= '' and mw.ustring.sub(f, 1, 5) == 'File:' then
						table.insert(lines, f)
					end
				end
			end
		
		end
		i = i + 1
	end
	return ( #lines > 0 ) and lines or error('No images found')
end

p._main = function(args, transclude, containerClassName)
	if not args[1] then
		return error(linked and 'No page specified' or 'No page specified', 0)
	end
	local lines = transclude and makeTranscludedGalleryLinesTables(args) or makeGalleryLinesTable(args)
	return makeOutput(lines, args.width or '100%', containerClassName or 'randomSlideshow-container')
end

p.main = function(frame)
	local parent = frame.getParent(frame)
	local parentArgs = parent.args
	local args = cleanupArgs(parentArgs)
	local output = p._main(args, false)
	return frame:extensionTag{ name='templatestyles', args = { src='Random slideshow/styles.css'} } 
		.. frame:preprocess(output)
end

p.transclude = function(frame)
	local parent = frame.getParent(frame)
	local parentArgs = parent.args
	local args = cleanupArgs(parentArgs)
	local output = p._main(args, true)
	return frame:extensionTag{ name='templatestyles', args = { src='Random slideshow/styles.css'} } 
		.. frame:preprocess(output)
end

return p