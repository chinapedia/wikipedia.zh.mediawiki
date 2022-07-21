--
-- This module implements {{Infobox3cols}}
-- Imported from enwiki and localizated by Dabao qian.
-- 同样比英文维基多解析了overimage, overcaption,
-- overimagerowclass以及header/labal/data*(a/b/c)style参数。
 
local p = {}

local navbar = require('Module:Navbar')._navbar

local args = {}
local origArgs
local root

local function union(t1, t2)
    -- Returns the union of the values of two tables, as a sequence.
    local vals = {}
    for k, v in pairs(t1) do
        vals[v] = true
    end
    for k, v in pairs(t2) do
        vals[v] = true
    end
    local ret = {}
    for k, v in pairs(vals) do
        table.insert(ret, k)
    end
    return ret
end

local function getArgNums(prefix,suffix)
    -- Returns a table containing the numbers of the arguments that exist
    -- for the specified prefix. For example, if the prefix was 'data', and
    -- 'data1', 'data2', and 'data5' exist, it would return {1, 2, 5}.
    local nums = {}
    for k, v in pairs(args) do
        local num = tostring(k):match('^' .. prefix .. '([0-9]%d*)' .. suffix .. '$')
        if num then table.insert(nums, tonumber(num)) end
    end
    table.sort(nums)
    return nums
end

local function addRow(rowArgs)
    -- Adds a row to the infobox, with either a header cell
    -- or a label/data cell combination.
    if rowArgs.header then
        root
            :tag('tr')
                :addClass(rowArgs.rowclass)
                :cssText(rowArgs.rowstyle)
                :attr('id', rowArgs.rowid)
                :tag('th')
                    :attr('colspan', 4)
                    :attr('id', rowArgs.headerid)
                    :addClass(rowArgs.class)
                    :addClass(args.headerclass)
                    :css('text-align', 'center')
                    :cssText(rowArgs.headerstyle)
                    :cssText(rowArgs.rowcellstyle)
                    :wikitext(rowArgs.header)
    elseif rowArgs.label then
        if rowArgs.data then
            local row = root:tag('tr')
            row:addClass(rowArgs.rowclass)
            row:cssText(rowArgs.rowstyle)
            row:attr('id', rowArgs.rowid)
            row
                :tag('th')
                    :attr('scope', 'row')
                    :attr('id', rowArgs.labelid)
                    :cssText(rowArgs.labelstyle)
                    :cssText(rowArgs.rowcellstyle)
                    :wikitext(rowArgs.label)
                    :done()
        
            local dataCell = row:tag('td')
            dataCell
                :attr('colspan', 3)
                :attr('id', rowArgs.dataid)
                :addClass(rowArgs.class)
                :cssText(rowArgs.datastyle)
                :cssText(rowArgs.rowcellstyle)
                :newline()
                :wikitext(rowArgs.data)
        elseif rowArgs.dataa or rowArgs.datab then
            local row = root:tag('tr')
            row:addClass(rowArgs.rowclass)
            row:cssText(rowArgs.rowstyle)
            row:attr('id', rowArgs.rowid)
            row
                :tag('th')
                    :attr('scope', 'row')
                    :attr('id', rowArgs.labelid)
                    :cssText(rowArgs.labelstyle)
                    :cssText(rowArgs.rowcellstyle)
                    :wikitext(rowArgs.label)
                    :done()

            local dataCella = row:tag('td')
            dataCella
                :attr('id', rowArgs.dataaid)
                :addClass(rowArgs.classa)
                :cssText(rowArgs.dataastyle)
                :cssText(rowArgs.rowcellstyle)
                :newline()
                :wikitext(rowArgs.dataa)
            if rowArgs.renderb then
                local dataCellb = row:tag('td')
                dataCellb
                    :attr('id', rowArgs.databid)
                    :addClass(rowArgs.classb)
                    :cssText(rowArgs.databstyle)
                    :cssText(rowArgs.rowcellstyle)
                    :newline()
                    :wikitext(rowArgs.datab)
            end
            if rowArgs.renderc then
                local dataCellc = row:tag('td')
                dataCellc
                    :attr('id', rowArgs.datacid)
                    :addClass(rowArgs.classc)
                    :cssText(rowArgs.datacstyle)
                    :cssText(rowArgs.rowcellstyle)
                    :newline()
                    :wikitext(rowArgs.datac)
            end
        end
    elseif rowArgs.data then
        local row = root:tag('tr')
        row:addClass(rowArgs.rowclass)
        row:cssText(rowArgs.rowstyle)
        row:attr('id', rowArgs.rowid)
                    
        local dataCell = row:tag('td')
        dataCell
            :attr('colspan', 4)
            :attr('id', rowArgs.dataid)
            :addClass(rowArgs.class)
            :css('text-align', 'center') 
            :cssText(rowArgs.datastyle)
            :cssText(rowArgs.rowcellstyle)
            :newline()
            :wikitext(rowArgs.data)
    end
end

local function renderOverImage()
    if not args.overimage then return end

    local row = root:tag('tr')
	row:addClass(args.overimagerowclass)
	local topImage = row:tag('td')
	topImage:attr('colspan', 4)
	topImage:addClass(args.class)
	topImage:cssText(args.datastyle)
	topImage:css('text-align', 'center')
	if args.overcaption then
		topImage:wikitext(args.overimage .. '<br><span style=\"' .. args.captionstyle .. '\">' .. args.overcaption .. '</span>')
	else
		topImage:wikitext(args.overimage)
	end
end

local function renderTitle()
    if not args.title then return end

    root
        :tag('caption')
            :addClass(args.titleclass)
            :cssText(args.titlestyle)
            :wikitext('\'\'\'' .. args.title .. '\'\'\'')
end

local function renderAboveRow()
    if not args.above then return end
    
    root
        :tag('tr')
            :tag('th')
                :attr('colspan', 4)
                :addClass(args.aboveclass)
                :css('text-align', 'center')
                :css('font-size', '125%')
                :css('font-weight', 'bold')
                :cssText(args.abovestyle)
                :wikitext(args.above)
end

local function renderBelowRow()
    if not args.below then return end
    
    root
        :tag('tr')
            :tag('td')
                :attr('colspan', 4)
                :addClass(args.belowclass)
                :css('text-align', 'center')
                :cssText(args.belowstyle)
                :newline()
                :wikitext(args.below)
end

local function renderSubheaders()
    if args.subheader then
        args.subheader1 = args.subheader
    end
    if args.subheaderrowclass then
        args.subheaderrowclass1 = args.subheaderrowclass
    end
    local subheadernums = getArgNums('subheader','')
    for k, num in ipairs(subheadernums) do
        addRow({
            data = args['subheader' .. tostring(num)],
            datastyle = args.subheaderstyle or args['subheaderstyle' .. tostring(num)],
            class = args.subheaderclass,
            rowclass = args['subheaderrowclass' .. tostring(num)]
        })
    end
end

local function renderImages()
    if args.image then
        args.image1 = args.image
    end
    if args.caption then
        args.caption1 = args.caption
    end
    local imagenums = getArgNums('image','')
    for k, num in ipairs(imagenums) do
        local caption = args['caption' .. tostring(num)]
        local data = mw.html.create():wikitext(args['image' .. tostring(num)])
        if caption then
            data
                :tag('div')
                    :cssText(args.captionstyle)
                    :wikitext(caption)
        end
        addRow({
            data = tostring(data),
            datastyle = args.imagestyle,
            class = args.imageclass,
            rowclass = args['imagerowclass' .. tostring(num)]
        })
    end
end

local function renderRows()
    -- Gets the union of the header and data argument numbers,
    -- and renders them all in order using addRow.
    local rownums = union(getArgNums('header',''), getArgNums('data','[ab]?'))
    local datab_count = #(getArgNums('data','b'))
    local datac_count = #(getArgNums('data','c'))

    table.sort(rownums)
    for k, num in ipairs(rownums) do
        addRow({
            renderb = datab_count > 0,
            renderc = datac_count > 0,
            header = args['header' .. tostring(num)],
            headerstyle = (args.headerstyle or '') .. ';' .. (args['header' .. tostring(num) .. 'style'] or ''),
            label = args['label' .. tostring(num)],
            labelstyle = (args.labelstyle or '') .. ';' .. (args['label' .. tostring(num) .. 'style'] or ''),
            data = args['data' .. tostring(num)],
            datastyle = (args.datastyle or '') .. ';' .. (args['data' .. tostring(num) .. 'style'] or ''),
            class = args['class' .. tostring(num)],
            dataa = args['data' .. tostring(num) .. 'a'],
            dataastyle = (args.datastylea or '') .. ';' .. (args['data' .. tostring(num) .. 'astyle'] or ''),
            classa = args['class' .. tostring(num) .. 'a'],
            datab = args['data' .. tostring(num) .. 'b'],
            databstyle = (args.datastyleb or '') .. ';' .. (args['data' .. tostring(num) .. 'bstyle'] or ''),
            classb = args['class' .. tostring(num) .. 'b'],
            datac = args['data' .. tostring(num) .. 'c'],
            datacstyle = (args.datastylec or '') .. ';' .. (args['data' .. tostring(num) .. 'cstyle'] or ''),
            classc = args['class' .. tostring(num) .. 'c'],
            rowclass = args['rowclass' .. tostring(num)],
            rowstyle = args['rowstyle' .. tostring(num)],
            rowcellstyle = args['rowcellstyle' .. tostring(num)],
            dataid = args['dataid' .. tostring(num)],
            dataaid = args['dataid' .. tostring(num) .. 'a'],
            dataaib = args['dataid' .. tostring(num) .. 'b'],
            dataaic = args['dataid' .. tostring(num) .. 'c'],
            labelid = args['labelid' .. tostring(num)],
            headerid = args['headerid' .. tostring(num)],
            rowid = args['rowid' .. tostring(num)]
        })
    end
end

local function renderNavBar()
    if not args.name then return end
    
    root
        :tag('tr')
            :tag('td')
                :attr('colspan', '4')
                :css('text-align', 'right')
                :wikitext(navbar{
                    args.name,
                    mini = 1,
                })
end

local function renderItalicTitle()
    local italicTitle = args['italic title'] and mw.ustring.lower(args['italic title'])
    if italicTitle == '' or italicTitle == 'force' or italicTitle == 'yes' then
        root:wikitext(mw.getCurrentFrame():expandTemplate({title = 'italic title'}))
    end
end

local function renderTrackingCategories()
    if args.decat ~= 'yes' then
        if #(getArgNums('data','[abc]?')) == 0 and mw.title.getCurrentTitle().namespace == 0 then
            root:wikitext('[[Category:使用无数据行信息框模板的条目|Category:使用无数据行信息框模板的条目]]')
        end
        if args.child == 'yes' and args.title then
            root:wikitext('[[Category:使用带有标题参数的嵌入式信息框模板的条目|Category:使用带有标题参数的嵌入式信息框模板的条目]]')
        end
    end
end

local function _infobox()
    -- Specify the overall layout of the infobox, with special settings
    -- if the infobox is used as a 'child' inside another infobox.

    root = mw.html.create('table')
        
    root
        :addClass('infobox')
        :addClass(args.bodyclass)
        :attr('cellspacing', 3)
        :css('border-spacing', '3px')
    if args.child == 'yes' or args.subbox == 'yes' then
        root
            :css('padding', '0')
            :css('border', 'none')
            :css('margin', (args.subbox == 'yes') and '-3px' or 'auto')
            :css('width', 'auto')
            :css('min-width', '100%')
            :css('font-size', 'small')
            :css('clear', 'none')
            :css('float', 'none')
            :css('background-color', 'transparent')
            :cssText(args.bodystyle)
            :wikitext(args.title)
    else
        root
            :css('width', '22em')
            :css('text-align', 'left')
            :css('font-size', 'small')
            :css('line-height', '1.5em')
            :cssText(args.bodystyle)
    renderTitle()
    renderAboveRow()
    end

    renderOverImage()
    renderSubheaders()
    renderImages() 
    renderRows() 
    renderBelowRow()  
    renderNavBar()
    renderItalicTitle()
    renderTrackingCategories()
    
    return tostring(root)
end

local function preprocessSingleArg(argName)
    -- If the argument exists and isn't blank, add it to the argument table.
    -- Blank arguments are treated as nil to match the behaviour of ParserFunctions.
    if origArgs[argName] and origArgs[argName] ~= '' then
        args[argName] = origArgs[argName]
    end
end

local function preprocessArgs(prefixTable, step)
    -- Assign the parameters with the given prefixes to the args table, in order, in batches
    -- of the step size specified. This is to prevent references etc. from appearing in the
    -- wrong order. The prefixTable should be an array containing tables, each of which has
    -- two possible fields, a "prefix" string and a "depend" table. The function always parses
    -- parameters containing the "prefix" string, but only parses parameters in the "depend"
    -- table if the prefix parameter is present and non-blank.
    if type(prefixTable) ~= 'table' then
        error("Non-table value detected for the prefix table", 2)
    end
    if type(step) ~= 'number' then
        error("Invalid step value detected", 2)
    end
    
    -- Get arguments without a number suffix, and check for bad input.
    for i,v in ipairs(prefixTable) do
        if type(v) ~= 'table' or type(v.prefix) ~= "string" or (v.depend and type(v.depend) ~= 'table') then
            error('Invalid input detected to preprocessArgs prefix table', 2)
        end
        preprocessSingleArg(v.prefix)
        -- Only parse the depend parameter if the prefix parameter is present and not blank.
        if args[v.prefix] and v.depend then
            for j, dependValue in ipairs(v.depend) do
                if type(dependValue) ~= 'string' then
                    error('Invalid "depend" parameter value detected in preprocessArgs')
                end
                preprocessSingleArg(dependValue)
            end
        end
    end

    -- Get arguments with number suffixes.
    local a = 0 -- Counter variable.
    local moreArgumentsExist = true
    while moreArgumentsExist == true do
        moreArgumentsExist = false
        for i = a, a + step - 1 do
            for j,v in ipairs(prefixTable) do
                local prefixArgName = v.prefix .. tostring(i) .. (v.suffix or '')
                if origArgs[prefixArgName] then
                    moreArgumentsExist = true -- Do another loop if any arguments are found, even blank ones.
                    preprocessSingleArg(prefixArgName)
                end
                -- Process the depend table if the prefix argument is present and not blank, or
                -- we are processing "prefix1" and "prefix" is present and not blank, and
                -- if the depend table is present.
                if v.depend and (args[prefixArgName] or (i == 1 and args[v.prefix])) then
                    for j,dependValue in ipairs(v.depend) do
                        local dependArgName = dependValue .. tostring(i) .. (v.dependsuffix or '')
                        preprocessSingleArg(dependArgName)
                    end
                end
            end
        end
        a = a + step
    end
end

function preprocessSpecificStyle(styleTable, step)
	-- Assign the parameters *style to the args table
    local a = 0 -- Counter variable.
    local moreArgumentsExist = true
    while moreArgumentsExist == true do
        moreArgumentsExist = false
        for i = a,a + step - 1 do
            for j,v in ipairs(styleTable) do
                local styleArgName = v.arg .. tostring(i) .. (v.suf or '') .. 'style'
                if origArgs[styleArgName] then
                    moreArgumentsExist = true -- Do another loop if any arguments are found, even blank ones.
                    preprocessSingleArg(styleArgName)
                end
            end
        end
        a = a + step
    end
end
 
function p.infobox(frame)
    -- If called via #invoke, use the args passed into the invoking template.
    -- Otherwise, for testing purposes, assume args are being passed directly in.
    if frame == mw.getCurrentFrame() then
        origArgs = frame:getParent().args
    else
        origArgs = frame
    end
    
    -- Parse the data parameters in the same order that the old {{infobox}} did, so that
    -- references etc. will display in the expected places. Parameters that depend on
    -- another parameter are only processed if that parameter is present, to avoid
    -- phantom references appearing in article reference lists.
    preprocessSingleArg('child')
    preprocessSingleArg('bodyclass')
    preprocessSingleArg('subbox')
    preprocessSingleArg('bodystyle')
    preprocessSingleArg('overimage')
    preprocessSingleArg('overcaption')
    preprocessSingleArg('overimagerowclass')
    preprocessSingleArg('title')
    preprocessSingleArg('titleclass')
    preprocessSingleArg('titlestyle')
    preprocessSingleArg('above')
    preprocessSingleArg('aboveclass')
    preprocessSingleArg('abovestyle')
    preprocessArgs({
        {prefix = 'subheader', depend = {'subheaderstyle', 'subheaderrowclass'}}
    }, 10)
    preprocessSingleArg('subheaderstyle')
    preprocessSingleArg('subheaderclass')
    preprocessSingleArg('image')
    preprocessSingleArg('caption')
    preprocessArgs({
        {prefix = 'image', depend = {'caption', 'imagerowclass'}}
    }, 10)
    preprocessSingleArg('captionstyle')
    preprocessSingleArg('imagestyle')
    preprocessSingleArg('imageclass')
    preprocessArgs({
        {prefix = 'header'},
        {prefix = 'data', depend = {'label'}},
        {prefix = 'data', suffix = 'a', depend = {'label'}},
        {prefix = 'data', suffix = 'a', depend = {'data'}, dependsuffix='c'},
        {prefix = 'data', suffix = 'b', depend = {'label'}},
        {prefix = 'data', suffix = 'b', depend = {'data'}, dependsuffix='c'},
        {prefix = 'rowclass'},
        {prefix = 'rowstyle'},
        {prefix = 'rowcellstyle'},
        {prefix = 'class'},
        {prefix = 'dataid'},
        {prefix = 'labelid'},
        {prefix = 'headerid'},
        {prefix = 'rowid'}
    }, 80)
    preprocessSpecificStyle({
        {arg = 'header'},
        {arg = 'label'},
        {arg = 'data'},
        {arg = 'data', suf = 'a'},
        {arg = 'data', suf = 'b'},
        {arg = 'data', suf = 'c'}
    }, 80)
    preprocessSingleArg('headerclass')
    preprocessSingleArg('headerstyle')
    preprocessSingleArg('labelstyle')
    preprocessSingleArg('datastyle')
    preprocessSingleArg('datastylea')
    preprocessSingleArg('datastyleb')
    preprocessSingleArg('datastylec')
    preprocessSingleArg('below')
    preprocessSingleArg('belowclass')
    preprocessSingleArg('belowstyle')
    preprocessSingleArg('name')
    args['italic title'] = origArgs['italic title'] -- different behaviour if blank or absent
    preprocessSingleArg('decat')
 
    return _infobox()
end
 
return p