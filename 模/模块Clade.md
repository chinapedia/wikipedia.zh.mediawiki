--[[NOTE: this module contains functions for generating the table structure of the clade tree: 

The main function is called by the template using the {{invoke}} instruction; the three main functions are:
        p.main(frame) - opens and closes table, loops through the children of node, main is invoked once and controls the rest, calling ...
        p.addTaxon(childNumber, nodeLeaf) - the nuts and bolts; code dealing with each child node
        p.addLabel(childNumber) - adds the label text
        
        now used templatestyles
]]

local p = {}



--[[============================== main function  ===========================
-- main function, which will generate the table structure of the tree

Test version:
Usage: {{#invoke:Module:Sandbox/Jts1882/CladeN|main|style={{{STYLE|}}} }}
Template:CladeN

Release version:
Usage: {{#invoke:Clade|main|style={{{STYLE|}}} }}
Template:Clade
]]

function p.main(frame)

	local cladeString = ""	
	local maxChildren = 20 -- currently 17 in the clade/cladex templates
	local childNumber = 0
    lastNode = 0 -- make this global for now 
	local nodeCount = 0 -- total leafs plus new clade branches
	local leafCount = 0 -- just the terminal leaves
	local cladeCount = 0 -- new clade calls (each with a table)
	local childCount = 0 -- number of leaves in the clade (can use to set bottom of bracket in addTaxon()
	local totalCount = 0
	
    infoOutput = p.getCladeTreeInfo() -- get info about clade structure, e.g. lastNode (last |N= child number)

	local tableStyle = frame.args.style or ""
	--if tableStyle == '{{{style}}}' then tableStyle = "" end -- no longer needed as pipe added to template to suppress passing of {{{style}} when no value
	
	if tableStyle ~= "" then
		tableStyle = ' style="' .. tableStyle .. '"' -- include style= in string to suppress empty style elements
	end
    local reverseClade =frame.args.reverse or false
	local captionName =mw.getCurrentFrame():getParent().args['caption'] or ""
	local captionStyle = mw.getCurrentFrame():getParent().args['captionstyle'] or ""

    -- add an element to mimick nowiki WORKS BUT DISABLE FOR DEMO PURPOSES
    --cladeString = '<p class="mw-empty-elt"></p>\n'
    
	-- open table	
	-- (border-collapse causes problems (see talk) -- cladeString = cladeString .. '{| style="border-collapse:collapse;border-spacing:0;margin:0;' .. tableStyle .. '"'
    -- (before CSS styling) -- cladeString = cladeString .. '{| style="border-spacing:0;margin:0;' .. tableStyle .. '"'
    cladeString = cladeString .. '{|class="clade"' .. tableStyle

    -- add caption
	if captionName ~= "" then
		cladeString = cladeString .. '\n|+ style="' .. captionStyle .. '"|' .. captionName
	end
	
	-- global nodeParameters (unnumber, i.e. color, thickness, state) apply to whole node bracket, 
	--    but can be overrriden by branchParameters (numbered, e.g. color2, thickness2, state2)
	nodeColor = mw.getCurrentFrame():getParent().args['color'] or ""
	nodeThickness = tonumber(mw.getCurrentFrame():getParent().args['thickness']) or tonumber(mw.getCurrentFrame():getParent().args['粗']) or 1
	nodeState = mw.getCurrentFrame():getParent().args['state'] or "solid"
	
	local moreNeeded = true
	childNumber = 0
	--lastNode = 0

	--[[get child elements (add more rows for each child of node; each child is two rows)
	    the function addTaxon is called to add the rows for each child element;
	    each child add two rows: the first cell of each row contains the label or sublabel (below the line label), respectively;
	    the second cell spans both rows and contains the leaf name or a new clade structure
	    a third cell on the top row is sometimes added to contain a group  to the right
	]]
	
	-- main loop
	while 	childNumber < lastNode do -- use the last number determined in the preprocessing

		childNumber = childNumber + 1 -- so we start with 1
		local nodeLeaf = mw.getCurrentFrame():getParent().args[tostring(childNumber)] or ""  -- get data from |N=
		local nodeLabel = mw.getCurrentFrame():getParent().args['label'..tostring(childNumber)] or mw.getCurrentFrame():getParent().args['标'..tostring(childNumber)] or mw.getCurrentFrame():getParent().args['標'..tostring(childNumber)] or ""  -- get data from |labelN=
		
		
		local newickString = mw.getCurrentFrame():getParent().args['newick'..tostring(childNumber)] or ""  -- get data from |labelN=
		if newickString ~= "" then -- if using a newick string instead of a clade structure
			if nodeLabel == "" then -- use labelN by default, otherwise use root name from Newick string
				nodeLabel = p.getNewickOuterterm(newickString) -- need to use terminal part of newick string for label
			end
			cladeString = cladeString .. '\n' .. p.addTaxon(childNumber, p.newick(0, newickString), nodeLabel, lastNode)
			--lastNode=lastNode+1 -- there is a counting problem with the newickstring
		elseif nodeLeaf ~= "" then -- if the node contains a leaf name or clade structue
			if reverseClade then
				cladeString = cladeString .. '\n' .. p.addTaxonReverse(childNumber, nodeLeaf, nodeLabel, lastNode)
		    else
				cladeString = cladeString .. '\n' .. p.addTaxon(childNumber, nodeLeaf, nodeLabel, lastNode)
			end
		end
	end

	local footerText  = mw.getCurrentFrame():getParent().args['footer'] or ""
	local footerStyle = mw.getCurrentFrame():getParent().args['footerstyle'] or ""

	if footerText ~= "" then
	   cladeString = cladeString ..  '\n|-style="' .. footerStyle .. '"\n|colspan="2"|<p>' .. footerText .. '</p>||'
	end

	-- close table (wikitext to close table)
	cladeString = cladeString ..  '\n|}'
	
	return cladeString
	--return '<div style="width:auto;">\n' .. cladeString .. '</div>'
end

--[[ function to add child elements
     adds wikitext for two rows of the table for each child node, 
     	the first cell in each is used for the label and sublabel; the bottom border forms the horizonal branch of the bracket
     	the second cell is used for the leafname or a transcluded clade structure and spans both rows
     note that the first and last child nodes need to be handled differently from the middle elements
	     the middle elements (|2, |3 ...) use a left border to create the vertical line of the bracket
	     the first child element doesn't use a left border for the first cell in the top row (as it is above the bracket)
	     the last child doesn't use a left border for the first cell in the second row (as it is above the bracket)
	     a complication is that the number of the last child node is not known;
	     	as a result the cells will be added to the row on the next iteration or after the main loop finishes
]]
function p.addTaxon(childNumber, nodeLeaf, nodeLabel, lastNode)

	-- (1) get formating parameters for branch (default to global nodeParameters)
	--    - the branch parameters have a number, e.g. |colorN, |thicknessN, |stateN
	--    - the node parameters have no number, e.g. |color, |thickness, |state
	local branchThickness = tonumber(mw.getCurrentFrame():getParent().args['thickness'..tostring(childNumber)]) or tonumber(mw.getCurrentFrame():getParent().args['粗'..tostring(childNumber)]) or nodeThickness
	local branchColor = mw.getCurrentFrame():getParent().args['color'..tostring(childNumber)] or nodeColor
	local branchStyle = mw.getCurrentFrame():getParent().args['style'..tostring(childNumber)] or ""
	local branchState = mw.getCurrentFrame():getParent().args['state'..tostring(childNumber)] or nodeState -- "solid" 
	if branchState == 'double' then if branchThickness < 2 then branchThickness = 3 end end  -- need thick line for double

    -- the left border takes node parameters, the bottom border takes branch parameters
   local bottomBorder =  tostring(branchThickness) ..'px ' .. branchState  .. (branchColor~="" and ' ' .. branchColor or '')
   local leftBorder   =  tostring(nodeThickness)   ..'px ' .. nodeState  .. (nodeColor~="" and ' ' .. nodeColor or '')
	
	--[[ The default border styles should be put in the CSS
	     Then the inline styling would only be needed when thickness, color or state are changed
	     Hence: 
	         .clade-label {border-left:1px solid black;border-bottom:1px solid black;}
	         .clade-slabel {border-left:1px solid black;}
	         .clade-toplabel {border-bottom:1px solid black;}
	         .clade-bottomsublabel {nothing}
	     May be able to use td:first-child and td:last-child to handle top and bottom of bracket
	     This would remove a large amount of inline styling and greatly reduce the transclusion size
	     Need a flag to indicate when non-default styling is required
	--]]
	
	-- variables for right hand bar or bracket
	--local barColor  = "" 
	local barRight  = mw.getCurrentFrame():getParent().args['bar'..tostring(childNumber)] or "0"
	local barBottom = mw.getCurrentFrame():getParent().args['barend'..tostring(childNumber)] or "0"
	local barTop    = mw.getCurrentFrame():getParent().args['barbegin'..tostring(childNumber)] or "0"
	local barLabel  = mw.getCurrentFrame():getParent().args['barlabel'..tostring(childNumber)] or ""
	local groupLabel  = mw.getCurrentFrame():getParent().args['grouplabel'..tostring(childNumber)] or ""
	local groupLabelStyle  = mw.getCurrentFrame():getParent().args['labelstyle'..tostring(childNumber)] or ""

	--replace colours with format string; need right bar for all three options
	if barRight  ~= "0" then barRight  = "2px solid " .. barRight  end 
	if barTop    ~= "0" then barRight  = "2px solid " .. barTop    end
	if barBottom ~= "0" then barRight  = "2px solid " .. barBottom end 
	if barTop    ~= "0" then barTop    = "2px solid " .. barTop    end
	if barBottom ~= "0" then barBottom = "2px solid " .. barBottom end 
	
	-- now construct wikitext 
	local styleString = ''
	local cladeString = ''
   
    -- (1) wikitext for new row
    cladeString = cladeString .. '\n|-'

	-- (2) now add cell with label
	styleString = ''
	if childNumber == 1 then
		-- the width gives minimum spacing when all labels are empty (was 1.5em)
		--(before CSS styling) -- styleString = ' style="width:1em;border:0;padding:0 0.2em;border-bottom:' .. bottomBorder .. ';vertical-align:bottom;text-align:center;' .. branchStyle .. '"'
        styleString = 'style="border-bottom:' .. bottomBorder .. ';' .. branchStyle .. '"'
 	else -- for 2-17
    	--(before CSS styling) -- styleString = ' style="border:0;padding:0 0.2em;border-left:' .. leftBorder .. ';border-bottom:' .. bottomBorder .. ';vertical-align:bottom;text-align:center;' .. branchStyle .. '"'
    	styleString = 'style="border-left:' .. leftBorder .. ';border-bottom:' .. bottomBorder .. ';' .. branchStyle .. '"'
	end
    --  add wikitext for cell with label
    cladeString = cladeString .. '\n|class="clade-label" ' .. styleString  .. '|' .. p.addLabel(childNumber,nodeLabel) -- p.addLabel(nodeLabel)

	-- (3) add cell with leaf (which may be a table with transluded clade content)
    --cladeString = cladeString .. '|| rowspan=2 style="border: 0; padding: 0; border-right: ' .. barRight .. ';border-bottom: ' .. barBottom .. ';border-top: ' .. barTop .. ';' .. branchStyle .. ' " | '
	styleString = ''  
    if barRight  ~= "0"  then 
    	--(before CSS styling) -- styleString = 'style="border:0;padding:0;border-right:' .. barRight .. ';border-bottom:' .. barBottom .. ';border-top:' .. barTop .. ';' .. branchStyle .. '"'
    	styleString = ' style="border-right:' .. barRight .. ';border-bottom:' .. barBottom .. ';border-top:' .. barTop .. ';' .. branchStyle .. '"'
    else
    	--(before CSS styling) -- styleString = 'style="border:0;padding:0;' .. branchStyle .. '"'
    	if (branchStyle ~= '') then
    		styleString = ' style="' .. branchStyle .. '"'
        end
    end
    
    -- add wikitext for leaf cell (note: nodeLeaf needs to be on newline if new wikitable)
    cladeString = cladeString .. '\n|rowspan=2 class="clade-leaf"' .. styleString .. '|\n' .. nodeLeaf 
    --cladeString = cladeString .. '\n' .. nodeLeaf  -- needs to be on newline if new wikitable
    
    -- (4) stuff for right-hand brackets
	if barRight  ~= "0"  then 
    	cladeString = cladeString .. '  '            -- add spaces between leaf text and bar
		if barLabel ~= "" then 
			--cladeString = cladeString .. '<td style="border:0;padding:0;vertical-align:middle;">' .. barLabel ..'</td>' 
			cladeString = cladeString .. '\n| rowspan=2 class="clade-bar" |' .. barLabel 
		end
	end 
	-- note: it might be useful to add rowspan=2 to allow full range of positions
	if groupLabel ~= ""then 
		--cladeString = cladeString .. '<td style="'.. groupLabelStyle .. '">' .. groupLabel ..'</td>' 
		cladeString = cladeString .. '\n| rowspan=2 class="clade-bar" style="'.. groupLabelStyle .. '" |' .. groupLabel 
	end 	

	-- (5) add second row (only one cell needed for sublabel because of rowspan=2); 
    local branchStyleString = 'style="' .. branchStyle .. '"  ' 
    if branchStyle == '' then branchStyleString = ''  end -- avoid empty style elements
	cladeString = cladeString .. '\n|-' .. branchStyleString
	
   local subLabel = mw.getCurrentFrame():getParent().args['sublabel'..tostring(childNumber)] or ""  -- request in addLabel
	
	-- FOR TESTING: use subLabel for annotating the clade structues to use structure information (DEBUGGIING ONLY)
	--subLabel= '(N=' .. infoOutput .. ')'
	-- END TESTING
	
	-- (6) add cell containing sublabel
	if childNumber~=lastNode then -- if childNumber==lastNode we don't want left border, otherwise we do
		styleString = ' style="border-left:' .. leftBorder ..';"'
    else
	    --cladeString = cladeString ..  '\n' .. '| style="border: 0; padding: 0; vertical-align: top;" | <br/> '
	    --(before CSS styling) -- styleString = 'style="border:0;vertical-align:top;text-align:center;"'
		styleString = ''
    end 
    
    local sublabel = p.addLabel(childNumber,subLabel)
    local classString = '' -- class only needed if there is a label to display
    if sublabel ~= '<br/>' then classString = 'class="clade-slabel" ' end
    
    cladeString = cladeString .. '\n|' .. classString .. styleString .. '|' ..  sublabel
    
	return cladeString
end

---------------------------------------------------------------------------------------------
-- reverse version

function p.addTaxonReverse(childNumber, nodeLeaf, nodeLabel, lastNode)

	-- (1) get formating parameters for branch (default to global nodeParameters)
	--    - the branch parameters have a number, e.g. |colorN, |thicknessN, |stateN
	--    - the node parameters have no number, e.g. |color, |thickness, |state
	local branchThickness = tonumber(mw.getCurrentFrame():getParent().args['thickness'..tostring(childNumber)]) or tonumber(mw.getCurrentFrame():getParent().args['粗'..tostring(childNumber)]) or nodeThickness
	local branchColor = mw.getCurrentFrame():getParent().args['color'..tostring(childNumber)] or nodeColor
	local branchStyle = mw.getCurrentFrame():getParent().args['style'..tostring(childNumber)] or ""
	local branchState = mw.getCurrentFrame():getParent().args['state'..tostring(childNumber)] or nodeState -- "solid" 
	if branchState == 'double' then if branchThickness < 2 then branchThickness = 3 end end  -- need thick line for double

    -- the left border takes node parameters, the bottom border takes branch parameters
   local bottomBorder =  tostring(branchThickness) ..'px ' .. branchState  .. (branchColor~="" and ' ' .. branchColor or '')
   local leftBorder   =  tostring(nodeThickness)   ..'px ' .. nodeState  .. (nodeColor~="" and ' ' .. nodeColor or '')
	
	-- variables for right hand bar or bracket
	--local barColor  = "" 
	local barRight  = mw.getCurrentFrame():getParent().args['bar'..tostring(childNumber)] or "0"
	local barBottom = mw.getCurrentFrame():getParent().args['barend'..tostring(childNumber)] or "0"
	local barTop    = mw.getCurrentFrame():getParent().args['barbegin'..tostring(childNumber)] or "0"
	local barLabel  = mw.getCurrentFrame():getParent().args['barlabel'..tostring(childNumber)] or ""
	local groupLabel  = mw.getCurrentFrame():getParent().args['grouplabel'..tostring(childNumber)] or ""
	local groupLabelStyle  = mw.getCurrentFrame():getParent().args['labelstyle'..tostring(childNumber)] or ""

	--replace colours with format string; need right bar for all three options
	if barRight  ~= "0" then barRight  = "2px solid " .. barRight  end 
	if barTop    ~= "0" then barRight  = "2px solid " .. barTop    end
	if barBottom ~= "0" then barRight  = "2px solid " .. barBottom end 
	if barTop    ~= "0" then barTop    = "2px solid " .. barTop    end
	if barBottom ~= "0" then barBottom = "2px solid " .. barBottom end 
	
	-- now construct wikitext 
	local styleString = ''
	local cladeString = ''
   
    -- (1) wikitext for new row
    cladeString = cladeString .. '\n|-'

    -- (4) stuff for right-hand brackets (or left hand brackets in reverse version)

	-- note: it might be useful to add rowspan=2 to allow full range of positions
	if groupLabel ~= ""then 
		cladeString = cladeString .. '\n|rowspan=2 class="clade-bar" style="'.. groupLabelStyle .. '" |' .. groupLabel  
	end
    --[[ don't use bar label in the reverse version (probably best to get rid altogether)
	if barRight  ~= "0"  then 
    	cladeString = cladeString .. '  '            -- add spaces between leaf text and bar
		if barLabel ~= "" then 
			cladeString = cladeString .. '\n|rowspan=2 style="vertical-align:middle;" |' .. barLabel 
		end
	end 
    --]]


	-- (3) add cell with leaf (which may be a table with transluded clade content)
    --cladeString = cladeString .. '|| rowspan=2 style="border: 0; padding: 0; border-right: ' .. barRight .. ';border-bottom: ' .. barBottom .. ';border-top: ' .. barTop .. ';' .. branchStyle .. ' " | '
	styleString = ''  
    if barRight  ~= "0"  then 
    	--(before CSS styling) -- styleString = 'style="border:0;padding:0;border-right:' .. barRight .. ';border-bottom:' .. barBottom .. ';border-top:' .. barTop .. ';' .. branchStyle .. '"'
    	styleString = ' style="border-left:' .. barRight .. ';border-bottom:' .. barBottom .. ';border-top:' .. barTop .. ';' .. branchStyle .. '"'
    else
    	--(before CSS styling) -- styleString = 'style="border:0;padding:0;' .. branchStyle .. '"'
    	if (branchStyle ~= '') then
    		styleString = ' style="' .. branchStyle .. '"'
        end
    end
    
    -- add wikitext for leaf cell (note: nodeLeaf needs to be on newline if new wikitable)
    cladeString = cladeString .. '\n|rowspan=2 class="clade-leafR"' .. styleString .. '|\n' .. nodeLeaf 
    --cladeString = cladeString .. '\n' .. nodeLeaf  -- needs to be on newline if new wikitable

	-- (2) now add cell with label
	styleString = ''
	if childNumber == 1 then
		-- the width gives minimum spacing when all labels are empty (was 1.5em)
		--(before CSS styling) -- styleString = ' style="width:1em;border:0;padding:0 0.2em;border-bottom:' .. bottomBorder .. ';vertical-align:bottom;text-align:center;' .. branchStyle .. '"'
        styleString = 'style="border-bottom:' .. bottomBorder .. ';' .. branchStyle .. '"'
 	else -- for 2-17
    	--(before CSS styling) -- styleString = ' style="border:0;padding:0 0.2em;border-left:' .. leftBorder .. ';border-bottom:' .. bottomBorder .. ';vertical-align:bottom;text-align:center;' .. branchStyle .. '"'
    	styleString = 'style="border-right:' .. leftBorder .. ';border-bottom:' .. bottomBorder .. ';' .. branchStyle .. '"'
	end
    --  add wikitext for cell with label
    cladeString = cladeString .. '\n|class="clade-label" ' .. styleString  .. '|' .. p.addLabel(childNumber,nodeLabel) -- p.addLabel(nodeLabel)

    
 	

	-- (5) add second row (only one cell needed for sublabel because of rowspan=2) 
	
    local branchStyleString = 'style="' .. branchStyle .. '"  ' 
    if branchStyle == '' then branchStyleString = ''  end -- avoid empty style elements
	cladeString = cladeString .. '\n|-' .. branchStyleString
		
    local subLabel = mw.getCurrentFrame():getParent().args['sublabel'..tostring(childNumber)] or ""  -- request in addLabel
	
	-- FOR TESTING: use subLabel for annotating the clade structues to use structure information (DEBUGGIING ONLY)
	--subLabel= '(N=' .. infoOutput .. ')'
	-- END TESTING
	
	-- (6) add cell containing sublabel
	if childNumber~=lastNode then -- if childNumber==lastNode we don't want left border, otherwise we do
		styleString = ' style="border-right:' .. leftBorder ..';"'
    else
	    --cladeString = cladeString ..  '\n' .. '| style="border: 0; padding: 0; vertical-align: top;" | <br/> '
	    --(before CSS styling) -- styleString = 'style="border:0;vertical-align:top;text-align:center;"'
		styleString = ''
    end 
    
    local sublabel = p.addLabel(childNumber,subLabel)
    local classString = '' -- class only needed if there is a label to display
    if sublabel ~= '<br/>' then classString = 'class="clade-slabel" ' end
    
    cladeString = cladeString .. '\n|' .. classString .. styleString .. '|' ..  sublabel
    
	return cladeString
end


--[[ adds text for label or sublabel to a cell
]]
function p.addLabel(childNumber,nodeLabel)
	
	--local nodeLabel = mw.getCurrentFrame():getParent().args['label'..tostring(childNumber)] or ""

	--local firstChars = string.sub(nodeLabel, 1,2) -- get first two characters; will be {{ if no parameter (for Old method?)
	--if firstChars == "{{{" or nodeLabel == "" then
	if nodeLabel == "" then
		--return '<br/>' --' <br/>'  -- remove space to reduce post-expand include size (the width=1.5em handles spacing)
		--return '<br/>' -- must return something; this is critical for clade structure 
		return ' ' --      (thin nbsp)
	else
		-- spaces can cause  wrapping and can break tree structure, hence use span with nowrap class
		--return '<span class="nowrap">' .. nodeLabel .. '</span>'
		
		-- a better method for template expansion size is to replace spaces with nonbreaking spaces
		-- however, there is a problem if labels have a styling element (e.g. <span style= ..., <span title= ...)
		local stylingElementDetected = true
		if stylingElementDetected == true then 
			return '<span class="nowrap">' .. nodeLabel .. '</span>'
    	else	
    		local nowrapString = string.gsub(nodeLabel," ", " ") -- replace spaces with non-breaking space
			                       -- could replace hyphen with non-breaking hyphen (‑)
			return nowrapString
		end
	end
end



--[[=================== Newick string handling function =============================
]]
function p.getNewickOuterterm(newickString)
	return string.gsub(newickString, "%b()", "")   -- delete parenthetic term
end

function p.newick(count,newickString)
	
	local cladeString = ""
	count = count+1
	--start table
	--cladeString = cladeString .. '{| style="border-collapse:collapse;border-spacing:0;border:0;margin:0;'
	cladeString = cladeString .. '{| class="clade" '
	
	local j,k
	j,k = string.find(newickString, '%(.*%)')                 -- find location of outer parenthesised term
	local innerTerm = string.sub(newickString, j+1, k-1)      -- select content in parenthesis
	local outerTerm = string.gsub(newickString, "%b()", "")   -- delete parenthetic term
	if outerTerm == 'panthera' then outerTerm = "x" end     -- how is this set in local variable for inner nodes?
	
	outerTerm = tostring(count)
	
	-- need to remove commas in bracket terms before split, so temporarily replace commas between brackets
    local innerTerm2 =  string.gsub(innerTerm, "%b()",  function (n)
                                         	return string.gsub(n, ",%s*", "XXX")  -- also strip spaces after commas here
                                            end)
	--cladeString = cladeString .. '\n' .. p.addTaxon(1, innerTerm2, "")

    -- this needs a lastNode variable
	local s = strsplit(innerTerm2, ",")
	--oldLastNode=lastNode
	local lastNode=table.getn(s) -- number of child branches
	local i=1	
	while s[i] do	
		restoredString = string.gsub(s[i],"XXX", ",")   -- convert back to commas
		--restoredString = s[i]
		local outerTerm = string.gsub(restoredString, "%b()", "")
		if string.find(restoredString, '%(.*%)') then
			--cladeString = cladeString .. '\n' .. p.addTaxon(i, restoredString, "x")
			cladeString = cladeString .. '\n' .. p.addTaxon(i, p.newick(count,restoredString), outerTerm, lastNode)
			-- p.addTaxon(2, p.newick(count,newickString2), "root")
		else
			cladeString = cladeString .. '\n' .. p.addTaxon(i, restoredString, "", lastNode) --count)
		end
		i=i+1
	end
   -- lastNode=oldLastNode
    
	-- close table
	--cladeString = cladeString ..  '\n' .. '| style="border: 0; padding: 0; vertical-align: top;" | <br/> \n|}'
	cladeString = cladeString ..  '\n| <br/> \n|}'
	
	return cladeString
end
-- emulate a standard split string function
function strsplit(inputstr, sep) 
        if sep == nil then
                sep = "%s"
        end
        local t={} ; i=1
        for str in string.gmatch(inputstr, "([^"..sep.."]+)") do
                t[i] = str
                i = i + 1
        end
        return t
end


-- =================== experimental Newick to clade parser function =============================

--[[Function of convert Newick strings to clade format

Usage: {{#invoke:Module:Sandbox/Jts1882/CladeN|newickConverter|newickstring={{{NEWICK_STRING}}} }}
]]
function p.newickConverter(frame)
	
	local newickString = frame.args['newickstring']
	
	
	if newickString == '{{{newickstring}}}' then return newickString  end

	-- show the Newick string
	local cladeString = ''
	local levelNumber = 1           --  for depth of iteration
	local childNumber = 1           --  number of sister elements on node  (always one for root)
	
	--  converted the newick string to the clade structure
	cladeString = cladeString .. '{{clade'
	cladeString = cladeString .. p.newickParseLevel(newickString, levelNumber, childNumber) 
	cladeString = cladeString .. '\r}}'  

	local resultString = ''
    local option = mw.getCurrentFrame():getParent().args['option'] or ''
    if option == 'tree' then
	 	--show the transcluded clade diagram
		resultString =   cladeString    	
    else
    	-- show the Newick string
		resultString = '<pre>'..newickString..'</pre>'	
	    -- show the converted clade structure
	    resultString = resultString .. '<pre>'.. cladeString ..'</pre>'	
    end
    --resultString = frame:expandTemplate{ title = 'clade',  frame:preprocess(cladeString) }

    return resultString
end

--[[ Parse one level of Newick sting
     This function recieves a Newick string, which has two components
      1. the right hand term is a clade label: |labelN=labelname
      2. the left hand term in parenthesis has common delimited child nodes, each of which can be
           i.  a taxon name which just needs:  |N=leafname 
           ii. a Newick string which needs further processing through reiteration
]]
function p.newickParseLevel(newickString,levelNumber,childNumber)

    
	local cladeString = ""
	local indent = p.getIndent(levelNumber) 
	--levelNumber=levelNumber+1
	
	local j=0
	local k=0
	j,k = string.find(newickString, '%(.*%)')                 -- find location of outer parenthesised term
	local innerTerm = string.sub(newickString, j+1, k-1)      -- select content in parenthesis
	local outerTerm = string.gsub(newickString, "%b()", "")   -- delete parenthetic term

	cladeString = cladeString .. indent .. '|label'..childNumber..'='  .. outerTerm
	cladeString = cladeString .. indent .. '|' .. childNumber..'='  .. '{{clade'

	levelNumber=levelNumber+1
	indent = p.getIndent(levelNumber)
	
		-- protect commas in inner parentheses from split; temporarily replace commas between parentheses
	    local innerTerm2 =  string.gsub(innerTerm, "%b()",  function (n)
	                                         	return string.gsub(n, ",%s*", "XXX")  -- also strip spaces after commas here
	                                            end)
	
		local s = strsplit(innerTerm2, ",")
		local i=1	
		while s[i] do	
			restoredString = string.gsub(s[i],"XXX", ",")   -- convert back to commas
	
			local outerTerm = string.gsub(restoredString, "%b()", "")
			if string.find(restoredString, '%(.*%)') then
				--cladeString = cladeString .. indent .. '|y' .. i .. '=' .. p.newickParseLevel(restoredString,levelNumber+1,i) 
				cladeString = cladeString  .. p.newickParseLevel(restoredString,levelNumber,i) 
			else
				cladeString = cladeString .. indent .. '|' .. i .. '=' .. restoredString --.. '(level=' .. levelNumber .. ')'
			end
			i=i+1
		end
--    end -- end splitting of strings

	cladeString = cladeString .. indent .. '}}'  
    return cladeString
end

function p.getIndent(levelNumber)
	local indent = "\r"
	local extraIndent = mw.getCurrentFrame():getParent().args['indent'] or 0
	
	while tonumber(extraIndent) > 0 do
	    indent = indent .. " " -- an extra indent to make aligining compound trees easier
	    extraIndent = extraIndent - 1
	end
	
	while levelNumber > 1 do
		indent = indent .. "   "
		levelNumber = levelNumber-1
	end
	return indent
end

function p.newickstuff(newickString)

	
end

------------------------------------------------------------------------------------------


function p.test2(target)
	local target ="User:Jts1882/sandbox/templates/Template:Passeroidea"
	local result = mw.getCurrentFrame():expandTemplate{ title = target, args = {['style'] = '' } }
	return result
end
-------------------------------------------------------------------------------------------

function p.toggle(frame)
	
	if 1==2 then return 'some text' end
	
	--local toggleSymbol = 'toggle all'
	local toggleSymbol = mw.getCurrentFrame():getParent().args['button'] or ""

	local toggleString = '<div class="'
                
    local i=0
    while 	i < 20 do  -- limit on number of toggle elements controlled by the trigger button
    	i = i + 1 -- so we start with 1
		local target = mw.getCurrentFrame():getParent().args['id'..tostring(i)] 
	    
	    -- add classes for the three elements of each target: expand symbol, collapse symbol and contents
	    if target ~= nil then
            toggleString = toggleString .. ' mw-customtoggle-myClade' .. target 
                ..             ' mw-customtoggle-collapseSymbol' .. target 
                ..             ' mw-customtoggle-expandSymbol' .. target 
        end
    end
  
 
 toggleString = toggleString  ..  '">' .. toggleSymbol .. '</div>'

  return toggleString
end
-----------------------------------------------------------------------------------------------
function p.hidden(frame)
    
    local id = mw.getCurrentFrame():getParent().args['id'] or ""
    local mode = mw.getCurrentFrame():getParent().args['mode'] or "right"
    local expandSymbol = mw.getCurrentFrame():getParent().args['expand-symbol'] or "⊞"
    local collapseSymbol = mw.getCurrentFrame():getParent().args['collapse-symbol'] or "⊟"
    local initialState = mw.getCurrentFrame():getParent().args['expanded']
    
    -- default is content collapsed
    local contentState = " mw-collapsed" -- class to collapse content at start
    local collapseSymbolState = " mw-collapsed"
    local expandSymbolState = ""
    if initialState then
       contentState = ""
       collapseSymbolState =  ""
       expandSymbolState = " mw-collapsed" 
    end
    	
	
    -- collapsible element containing the expand sympol and/or text
    local expandSymbolString = '<td style="padding:0 0 0.25em 0;">' 
                .. '<div class="mw-collapsible' .. expandSymbolState .. '" id="mw-customcollapsible-expandSymbol' .. id .. '">'
                .. '<div class="mw-collapsible-content mw-customtoggle-expandSymbol' .. id .. '">'
                .. '<span class="mw-customtoggle-myClade' .. id 
                ..             ' mw-customtoggle-collapseSymbol' .. id 
                ..             ' mw-customtoggle-expandSymbol' .. id 
                ..    '" style="font-size:100%;">' .. expandSymbol .. '</span>'
                .. '</div></div></td>'
    
    -- collapsible element containing the clade content 
    local contentString = '<td style="padding:0;">'
                .. '<div class="mw-collapsible' .. contentState .. '" id="mw-customcollapsible-myClade' .. id .. '>'
                .. '<div class="mw-collapsible-content mw-customtoggle-NOT_ON_CONTENT" >' -- don't toggle on the content
                
                .. '\n' .. p.main(frame)  -- important to start wikitext tables on new line
                .. '</div></div></td>'
    
    -- collapsible element containing the collapse sympol and/or text
    local collapseSymbolString = '<td style="padding:0 0 0.4em 0;">'
                .. '<div class="mw-collapsible' .. collapseSymbolState .. '" id="mw-customcollapsible-collapseSymbol' .. id .. '">'
                .. '<div class="mw-collapsible-content mw-customtoggle-collapseSymbol' .. id .. '" >'
                .. '<span class="mw-customtoggle-expandSymbol' .. id 
                            .. ' mw-customtoggle-myClade' .. id 
                            .. ' mw-customtoggle-collapseSymbol' .. id 
                            .. ' " style="font-size:100%;" >' .. collapseSymbol .. '</span>'
                            .. '</div></div></td>'


	local tableStyle = frame.args.style or ""
	if tableStyle == '{{{style}}}' then tableStyle = "" end
 	local cladeString = '<table style="border-spacing:0;margin:0;'..tableStyle ..'"><tr>'
    cladeString = cladeString .. expandSymbolString 
    if mode == "left" then
    	cladeString = cladeString .. collapseSymbolString
    end
    cladeString = cladeString .. contentString 
    if mode == "right" then
    	cladeString = cladeString .. collapseSymbolString
    end
    -- Note: if we want collapse string left and right it needs an extra element with a different id
    cladeString = cladeString ..  '</tr></table>'


return cladeString
end
------------------------------------------------------------------------------------------

--[[function getCladeTreeInfo()
	    this preprocessing loop gets information about the whole structure (number of nodes, leaves etc)
		it makes a redundant calls to the templates through transclusion, but doen't affect the template depths; 
		it provides the global lastNode that is used to limit the main while loop
--]]
function p.getCladeTreeInfo()

    -- enable proprocessing loop
    local childNumber = 0
    local childCount =0
    local maxChildren =20
    
    --info veriables (these are global for now)
    nodeCount=0
    cladeCount=0
    leafCount=0
    
	while 	childNumber < maxChildren do -- preprocessing loop
		childNumber = childNumber + 1 -- so we start with 1
		local nodeLeaf,data = mw.getCurrentFrame():getParent().args[tostring(childNumber)] or ""  -- get data from |N=
        local newickString = mw.getCurrentFrame():getParent().args['newick'..tostring(childNumber)] or ""  -- get data from |labelN=
		if newickString ~= "" or nodeLeaf ~= "" then
		--if nodeLeaf ~= "" then 
			childCount = childCount + 1  -- this counts child elements in this clade
		    --[[]
		    for i in string.gmatch(nodeLeaf, "||rowspan") do -- count number of rows started (transclusion)
   				nodeCount = nodeCount + 1
     		end
		    for i in string.gmatch(nodeLeaf, '{|class="clade"') do -- count number of tables started (transclusion)
   				cladeCount = cladeCount + 1
     		end
     		]]
     		-- count occurences of clade structure tables and double span rows
            _, cladeCount = string.gsub(nodeLeaf, '{|class="clade"', "")
            _, nodeCount = string.gsub(nodeLeaf, "||rowspan", "")
            
			lastNode = childNumber -- this gets the last node with a valid entry, even when missing numbers
		end
	end
--]]	
    -- nodes can be either terminal leaves or a clade structure (table)
    nodeCount = nodeCount + childCount + 1-- number of double rows passed down by transduction plus current child elements (plus one for current clade)
	cladeCount = cladeCount + 1       -- number of clade structure tables passed down by transduction (plus one for current clade)
	leafCount = nodeCount-cladeCount   -- number of terminal leaves (equals height of cladogram)
	infoOutput = nodeCount -- global
	
	return cladeCount
	
end

--[[ code for placing TemplateStyles from the module
     source: Anomie (CC-0)  https://phabricator.wikimedia.org/T200442
]]

function p.templateStyle( frame, src )
   return frame:extensionTag( 'templatestyles', '', { src = src } );
end

function p.showClade(frame)
	--local code = frame.args.code or ""
    local code = frame:getParent().args['code2'] or ""
	
	--return  code 
	--return mw.text.unstrip(code)
	
	--local test = "<pre>Hello</pre>"
	--return string.sub(test,6,-7)
	
	local o1 =frame:getParent():getArgument('code2')
	return o1:expand()
	
	--return string.sub(code,2,-1)              -- strip marker  \127'"`UNIQ--tagname-8 hex digits-QINU`"'\127
	--return frame:preprocess(string.sub(code,3))
end
	
-- this must be at end

return p