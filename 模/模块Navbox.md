--
-- This module will implement {{Navbox}}
--
 
local p = {}
 
local navbar = require('Module:Navbar')._navbar
local getArgs -- lazily initialized

local args
local tableRowAdded = false
local border
local listnums = {}

local function trim(s)
    return (mw.ustring.gsub(s, "^%s*(.-)%s*$", "%1"))
end

local function addNewline(s)
    if s:match('^[*:;#]') or s:match('^{|') then
        return '\n' .. s ..'\n'
    else
        return s
    end
end

local function addTableRow(tbl)
    -- If any other rows have already been added, then we add a 2px gutter row.
    if tableRowAdded then
        tbl
            :tag('tr')
                :css('height', '2px')
                :tag('td')
                	:attr('colspan', 3)
    end
    
    tableRowAdded = true
    
    return tbl:tag('tr')
end

local function renderNavBar(titleCell)
    -- Depending on the presence of the navbar and/or show/hide link, we may need to add a spacer div on the left
    -- or right to keep the title centered.
    local spacerSide = nil

    if args.navbar == 'off' then
        -- No navbar, and client wants no spacer, i.e. wants the title to be shifted to the left. If there's
        -- also no show/hide link, then we need a spacer on the right to achieve the left shift.
        if args.state == 'plain' then spacerSide = 'right' end
    elseif args.navbar == 'plain' or (not args.name and mw.getCurrentFrame():getParent():getTitle() == 'Template:Navbox' and (border == 'subgroup' or border == 'child' or border == 'none')) then
        -- No navbar. Need a spacer on the left to balance out the width of the show/hide link.
        if args.state ~= 'plain' then spacerSide = 'left' end
    else
        -- Will render navbar (or error message). If there's no show/hide link, need a spacer on the right
        -- to balance out the width of the navbar.
        if args.state == 'plain' then spacerSide = 'right' end

        titleCell:wikitext(navbar{ 
            args.name, 
            mini = 1, 
            fontstyle = (args.basestyle or '') .. ';' .. (args.titlestyle or '') ..  ';background:none transparent;border:none;'
        })
    end
    
    -- Render the spacer div.
    if spacerSide then
        titleCell
            :tag('span')
                :css('float', spacerSide)
                :css('width', '8em')
                :css('font-size', '80%')
                :css('margin-' .. (spacerSide == 'left' and 'right' or 'left'), '0.5em')
                :wikitext(' ')
    end
end

--
--   Title row
--
local function renderTitleRow(tbl)
    if not args.title then return end
 
    local titleRow = addTableRow(tbl)
     
    if args.titlegroup then
        titleRow
            :tag('th')
                :attr('scope', 'row')
                :addClass('navbox-group')
                :addClass(args.titlegroupclass)
                :cssText(args.basestyle)
                :cssText(args.groupstyle)
                :cssText(args.titlegroupstyle)
                :wikitext(args.titlegroup)
    end
    
    local titleCell = titleRow:tag('th'):attr('scope', 'col')
            
    if args.titlegroup then
        titleCell
            :css('border-left', '2px solid #fdfdfd')
            :css('width', '100%')
    end
    
    local titleColspan = 2
    if args.imageleft then titleColspan = titleColspan + 1 end
    if args.image then titleColspan = titleColspan + 1 end
    if args.titlegroup then titleColspan = titleColspan - 1 end
    
    titleCell
        :cssText(args.basestyle)
        :cssText(args.titlestyle)
        :addClass('navbox-title')
        :addClass(args.titleclass)
        :attr('colspan', titleColspan)
 
    renderNavBar(titleCell)

    titleCell
         :tag('div')
             :css('font-size', '110%')
             :wikitext(addNewline(args.title))
end

--
--   Above/Below rows
--

local function getAboveBelowColspan()
    local ret = 2
    if args.imageleft then ret = ret + 1 end
    if args.image then ret = ret + 1 end
    return ret
end

local function renderAboveRow(tbl)
    if not args.above then return end

    addTableRow(tbl)
        :tag('td')
            :addClass('navbox-abovebelow')
            :addClass(args.aboveclass)
            :cssText(args.basestyle)
            :cssText(args.abovestyle)
            :attr('colspan', getAboveBelowColspan())
            :tag('div')
                :wikitext(addNewline(args.above))
end

local function renderBelowRow(tbl)
    if not args.below then return end

    addTableRow(tbl)
        :tag('td')
            :addClass('navbox-abovebelow')
            :addClass(args.belowclass)
            :cssText(args.basestyle)
            :cssText(args.belowstyle)
            :attr('colspan', getAboveBelowColspan())
            :tag('div')
                :wikitext(addNewline(args.below))
end
 
--
--   List rows
--
local function renderListRow(tbl, listnum)
    local row = addTableRow(tbl)
    
    if listnum == 1 and args.imageleft then
        row
            :tag('td')
                :addClass('navbox-image')
                :addClass(args.imageclass)
                :css('width', '0%')
                :css('padding', '0px 2px 0px 0px')
                :cssText(args.imageleftstyle)
                :attr('rowspan', 2 * #listnums - 1)
                :tag('div')
                    :wikitext(addNewline(args.imageleft))
    end
 
    if args['group' .. listnum] then
        local groupCell = row:tag('th')
        
        groupCell
               :attr('scope', 'row')
               :addClass('navbox-group')
               :addClass(args.groupclass)
               :cssText(args.basestyle)
               
        if args.groupwidth then
            groupCell:css('width', args.groupwidth)
        end
           
        groupCell
            :cssText(args.groupstyle)
            :cssText(args['group' .. listnum .. 'style'])
            :wikitext(args['group' .. listnum])
    end
    
    local listCell = row:tag('td')

    if args['group' .. listnum] then
        listCell
            :css('text-align', 'left')
            :css('border-left-width', '2px')
            :css('border-left-style', 'solid')
    else
        listCell:attr('colspan', 2)
    end
    
    if not args.groupwidth then 
        listCell:css('width', '100%')
    end
    
    local isOdd = (listnum % 2) == 1
    local rowstyle = args.evenstyle
    if isOdd then rowstyle = args.oddstyle end
 
    local evenOdd
    if args.evenodd == 'swap' then
        if isOdd then evenOdd = 'even' else evenOdd = 'odd' end
    else
        if isOdd then evenOdd = args.evenodd or 'odd' else evenOdd = args.evenodd or 'even' end
    end

    listCell
        :css('padding', '0px')
        :cssText(args.liststyle)
        :cssText(rowstyle)
        :cssText(args['list' .. listnum .. 'style'])
        :addClass('navbox-list')
        :addClass('navbox-' .. evenOdd)
        :addClass(args.listclass)
        :tag('div')
            :css('padding', (listnum == 1 and args.list1padding) or args.listpadding or '0em 0.25em')
            :wikitext(addNewline(args['list' .. listnum]))

    if listnum == 1 and args.image then
        row
            :tag('td')
                :addClass('navbox-image')
                :addClass(args.imageclass)
                :css('width', '0%')
                :css('padding', '0px 0px 0px 2px')
                :cssText(args.imagestyle)
                :attr('rowspan', 2 * #listnums - 1)
                :tag('div')
                    :wikitext(addNewline(args.image))
    end
end


--
--   Tracking categories
--

local function needsHorizontalLists()
    if border == 'child' or border == 'subgroup'  or args.tracking == 'no' then return false end
    
    local listClasses = {'plainlist', 'hlist', 'hlist hnum', 'hlist hwrap', 'hlist vcard', 'vcard hlist', 'hlist vevent'}
    for i, cls in ipairs(listClasses) do
        if args.listclass == cls or args.bodyclass == cls then
            return false
        end
    end

    return true
end

local function hasBackgroundColors()
    return mw.ustring.match(args.titlestyle or '','background') or mw.ustring.match(args.groupstyle or '','background') or mw.ustring.match(args.basestyle or '','background')
end

local function argNameAndRealTitleAreDifferent()
	if border == 'child' or border == 'subgroup'  or args.tracking == 'no' then return false end

	if args.name ~= mw.title.getCurrentTitle().text then
		return true
	end
	return false
end

local function getTrackingCategories()
    local cats = {}
    if needsHorizontalLists() then table.insert(cats, '没有使用水平列表的导航框') end
    if hasBackgroundColors() then table.insert(cats, '使用背景颜色的导航框') end
    if argNameAndRealTitleAreDifferent() then table.insert(cats, 'name參數和實際不同的導航框') end
    return cats
end

local function renderTrackingCategories(builder)
    local title = mw.title.getCurrentTitle()
    if title.namespace ~= 10 then return end -- not in template space
    local subpage = title.subpageText
    if subpage == 'doc' or subpage == 'sandbox' or subpage == 'testcases' then return end
    
    for i, cat in ipairs(getTrackingCategories()) do
        builder:wikitext('[[Category:'_.._cat_.._'|Category:' .. cat .. ']]') 
    end
end

--
--   Main navbox tables
--
local function renderMainTable()
    local tbl = mw.html.create('table')
        :attr('cellspacing', 0)
        :addClass('nowraplinks')
        :addClass(args.bodyclass)
             
    if args.title and (args.state ~= 'plain' and args.state ~= 'off') then
        tbl
            :addClass('collapsible')
            :addClass(args.state or 'autocollapse')
    end
 
    tbl:css('border-spacing', 0)
    if border == 'subgroup' or border == 'child' or border == 'none' then
        tbl
            :addClass('navbox-subgroup')
            :cssText(args.bodystyle)
            :cssText(args.style)
    else -- regular navobx - bodystyle and style will be applied to the wrapper table
        tbl
            :addClass('navbox-inner')
            :css('background', 'transparent')
            :css('color', 'inherit')
    end
    tbl:cssText(args.innerstyle)
 
    renderTitleRow(tbl)
    renderAboveRow(tbl)
    for i, listnum in ipairs(listnums) do
        renderListRow(tbl, listnum) 
    end
    renderBelowRow(tbl)
    
    return tbl
end

function p._navbox(navboxArgs)
    args = navboxArgs
    
    for k, v in pairs(args) do
        local listnum = ('' .. k):match('^list(%d+)$')
        if listnum then table.insert(listnums, tonumber(listnum)) end
    end
    table.sort(listnums)
 
    border = trim(args.border or args[1] or '')

    -- render the main body of the navbox
    local tbl = renderMainTable()

    -- render the appropriate wrapper around the navbox, depending on the border param
    local res = mw.html.create()
    if border == 'none' then
        res:node(tbl)
    elseif border == 'subgroup' or border == 'child' then
        -- We assume that this navbox is being rendered in a list cell of a parent navbox, and is
        -- therefore inside a div with padding:0em 0.25em. We start with a </div> to avoid the
        -- padding being applied, and at the end add a <div> to balance out the parent's </div>
        res
            :wikitext('</div>') -- mw.html 未支持 unclosed
            :node(tbl)
            :wikitext('<div>') -- mw.html 未支持 unclosed
    else
        res
            :tag('table')
                :attr('cellspacing', 0)
                :addClass('navbox')
                :css('border-spacing', 0)
                :cssText(args.bodystyle)
                :cssText(args.style)
                :tag('tr')
                    :tag('td')
                        :css('padding', '2px')
                        :node(tbl)
    end
 
    renderTrackingCategories(res)
 
    return tostring(res)
end
 
function p.navbox(frame)
    if not getArgs then
    	getArgs = require('Module:Arguments').getArgs
    end
    args = getArgs(frame, {wrappers = 'Template:Navbox'})

    -- Read the arguments in the order they'll be output in, to make references number in the right order.
    local _
    _ = args.title
    _ = args.above
    for i = 1, 35 do
        _ = args["group" .. tostring(i)]
        _ = args["list" .. tostring(i)]
    end    
    _ = args.below

    return p._navbox(args)
end
 
return p