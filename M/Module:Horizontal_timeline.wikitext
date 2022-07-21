local horizontal_timeline = {};

local getArgs = require('Module:Arguments').getArgs
local builder = mw.html.create()

local function defaultInvokeFunc(funcName)
	return function (frame)
		args = getArgs(frame, {
                       trim = true,
                       removeBlanks = true,
                       parentFirst = true
                    })

        local from = getNotNilValue(tonumber(args['from']))
        local to =  getNotNilValue(tonumber(args['to']))

        if not from or not to or from == to then
            return ("<strong class='error'><code>from</code> and <code>to</code> cannot be <code>nil</code> or equal.</strong>")
        else
        	return horizontal_timeline[funcName](args)
        end
	end
end

horizontal_timeline.showTimeLine = defaultInvokeFunc('_showTimeLine')
function horizontal_timeline._showTimeLine(args)
    local wdth = getNotNilValue(args['width'], '100%' )
    local bordr = getNotNilValue(args['border'], '1px solid rgb(170, 170, 170)' )
    local bgCol = getNotNilValue(args['plot-color'], args['plot-colour'], 'transparent')
    local mrgn = getNotNilValue(args['margin'], '1em')

    local div_root = builder
        :tag('div')
        :cssText('float:left;border:'..bordr .. ';width:'..wdth)

    local cntnt = div_root
        :tag('div')
        :cssText('text-align:left; padding:1em; font-size:95%; margin:' ..mrgn.. '; background:'..bgCol)
           
    local rowNums = affixNums(args, 'row') -- Gets numbers for row1, row2, etc. with nil arguments removed.
    for _, num in ipairs(rowNums) do
        local rowType = args['row' .. num] -- Gets args.rowtype1, args.rowtype2, etc. with nil arguments removed.
        if rowType == 'scale' then
            cntnt:wikitext(horizontal_timeline.scaleRow(args))
        elseif rowType == 'note' then
            cntnt:wikitext(horizontal_timeline.noteRow(num, args))
        elseif rowType == 'timeline' then
            cntnt:wikitext(horizontal_timeline.timelineRow(num, args))
        else
            cntnt:wikitext(rowType)
        end
    end
    if args.caption then
        cntnt:tag('p')
            :cssText('clear:both; text-align:center')
            :wikitext(args.caption)
            :done()
    end
    return tostring(div_root) .. "<div style='clear:left;'></div>"
end

horizontal_timeline.showOneRow = defaultInvokeFunc('_showOneRow')
function horizontal_timeline._showOneRow(args)
    local rowNums = affixNums(args, 'row') -- Gets numbers for row1, row2, etc. with nil arguments removed.
    for _, num in ipairs(rowNums) do
        local rowType = args['row' .. num] -- Gets args.rowtype1, args.rowtype2, etc. with nil arguments removed.
        if rowType == 'scale' then
            return horizontal_timeline.scaleRow(args)
        elseif rowType == 'note' then
            return horizontal_timeline.noteRow(num, args)
        elseif rowType == 'timeline' then
            return horizontal_timeline.timelineRow(num, args)
        else
            return wikitext(rowType)
        end
    end
    return "?"
end

function horizontal_timeline.timelineRow(num, args)
    local root = mw.html.create()
    
    local from = getNotNilValue(tonumber(args['from']))
    local to =  getNotNilValue(tonumber(args['to']))
    
    local style    = getNotNilValue(args['row' .. num .. '-style'], '')
    local hght     = getNotNilValue (args['row' .. num .. '-height'],
									 args[style .. '-height'],
									 '2.5em')
    local bordrTop = getNotNilValue (args['row' .. num .. '-bordertop'],
									 args[style .. '-bordertop'],
									 'none')
    local bordrBtm = getNotNilValue (args['row' .. num .. '-borderbottom'],
									 args[style .. '-borderbottom'],
									 'none')
    local txtTop   = getNotNilValue (args['row' .. num .. '-texttop'],
									 args[style .. '-texttop'],
									 '0em')
    local colr     = getNotNilValue (args['row' .. num .. '-colour'],
    	                             args['row' .. num .. '-color'],
    	                             args[style .. '-colour'],
    	                             args[style .. '-color'],
    	                             'transparent')
    	                             
    if bordrTop ~= 'none' then
    	bordrTop = 'border-top:' .. bordrTop .. ';'
    else
    	bordrTop = ''
	end
	
	if bordrBtm ~= 'none' then
    	bordrBtm = 'border-bottom:' .. bordrBtm .. ';'
    else
    	bordrBtm = ''
	end

    local p = root
         :tag('div')
            :cssText("clear:both;width:100%; padding:0px; height:".. hght)
            :cssText(bordrTop.. bordrBtm .. "background-color:"..colr)

    local rowDat = affixNums(args, 'row'..num..'%-', '%-[a-zA-Z]*')
    local lastTo = from
    local firstNode = true
    for _, vals in ipairs(rowDat) do

    	local styleL    = getNotNilValue(args['row' .. num .. '-'.. vals ..  '-style'], style)

        --These vars should be initialized every iteration. Do not move outside of loop
        local bar_to = tonumber(getNotNilValue(args['row' .. num .. '-'.. vals .. '-to'],
                                        args[styleL .. '-to'],
                                        args[style.. '-'.. vals .. '-to'], to  ) )
        local bar_fontsize =getNotNilValue(args['row' .. num .. '-'.. vals .. '-fontsize'],
        								args[styleL .. '-fontsize'],
                                        args[style..'-'.. vals .. '-fontsize'], '0.9em' )
        local bar_bordr= getNotNilValue(args['row' .. num .. '-'.. vals .. '-border'],
        								args[styleL .. '-border'],
                                        args[style..'-'.. vals .. '-border'],
                                        'none')
        local bar_txtTop= getNotNilValue(args['row' .. num .. '-'.. vals .. '-texttop'],
        								args[styleL .. '-texttop'],
                                        args[style..'-'.. vals .. '-texttop'], txtTop )
        local bar_text = getNotNilValue(args['row' .. num .. '-'.. vals .. '-text'],
        								args[styleL .. '-text'],
                                        args[style..'-'.. vals .. '-text'], '')
        local bar_colour = getNotNilValue(args['row' .. num .. '-'.. vals .. '-colour'],
                                        args['row' .. num .. '-'.. vals .. '-color'],
                                        args[styleL .. '-boxcolour'],
                                        args[styleL .. '-boxcolor'],
                                        args[style..'-'.. vals .. '-colour'],
                                        args[style..'-'.. vals .. '-color'],
                                        'transparent' )
                                        
        if from < to then
            if bar_to > to then bar_to = to end
            if lastTo < from then lastTo = from end
        else
            if bar_to < to then bar_to = to end
            if lastTo > from then lastTo = from end
    	end

        local width =( (bar_to-lastTo)*100 / (to-from) ) --math.abs

        if width > 0 and width <= 100 then
            if bar_bordr == 'none' then
                if firstNode then -- for first box both left and right border needed
                    bar_bordr = "1px solid #000; border-left:1px solid #000"
                    firstNode = false
                else
                    bar_bordr = "1px solid #000"
    	        end
		    end
            p:tag('div')
                :cssText("float:left; height:100%; text-align:center; overflow: hidden; background-color:"..bar_colour)
                :cssText("width:"..width .."%")
                    :tag('div')
                    :cssText("-moz-box-sizing: border-box; -webkit-box-sizing: border-box;box-sizing: border-box;")
                    :cssText("float:right; height:100%; width:100%; border-right:"..bar_bordr)
                        :tag('div')
                            :cssText('position: relative; top:'..bar_txtTop .. '; font-size:'.. bar_fontsize)
                            :wikitext(bar_text)
                        :done()
                    :done()
                :done()
        end

        lastTo = bar_to
    end
    return tostring(root)
end

function horizontal_timeline.noteRow(num, args)
    local root = mw.html.create()
    
    local from = getNotNilValue(tonumber(args['from']))
    local to =  getNotNilValue(tonumber(args['to']))
    
    local hght = getNotNilValue(args['row' .. num .. '-height'], '2.5em')

    local p = root
         :tag('div')
            :cssText("width:100%; position:relative; left:-0.2em; top:0.8em; clear:both; height:".. hght)

    local rowDat = affixNums(args, 'row'..num..'%-', '%-at')
    if not rowDat then
        return ("<strong class='error'>Please specify location for note at <code>"..'row' .. num .. '-'.. vals .. '-at'.."</code> parameter.</strong>")
    end
    for _, vals in ipairs(rowDat) do
        local note_at   =args['row' .. num .. '-'.. vals .. '-at'] --will never be nil as it is what is sued to recieve rowDat
        local note_text =getNotNilValue(args['row' .. num .. '-'.. vals .. '-text'], '' )
        local note_shift=getNotNilValue(args['row' .. num .. '-'.. vals .. '-shift'], '0em' )
        local note_lift =getNotNilValue(args['row' .. num .. '-'.. vals .. '-lift'], '0em' )
        local note_arrow=getNotNilValue(args['row' .. num .. '-'.. vals .. '-arrow'], '↓' )

		local note_sft = 100*(note_at - from) / (to-from)
        
        p:tag('div')
            :cssText("position:absolute; top:0px; width:100%")
                :tag('div')
                    :cssText("margin-left:".. note_sft .."%; margin-top:0; position:relative")
                    :tag('span')
                        :cssText("position:relative; top:0.25em; left:-1.5px")
                        :wikitext(note_arrow)
                        :done()
                    :tag('span')
                        :cssText("font-size:smaller; position:relative; line-height:3px; overflow:visible")
                        :cssText("left:"..note_shift.."; top:"..note_lift.."; z-index:".. (1000- tonumber(num)))
                        :wikitext(note_text)
                        :done()
                    :done()
                :done()
            :done()
    end
    return tostring(root)
end

function horizontal_timeline.scaleRow(args)
	local from = getNotNilValue(tonumber(args['from']))
    local to =  getNotNilValue(tonumber(args['to']))
    local inc = getNotNilValue( tonumber(args['inc']), (math.floor( (from - to) / 5 ) * -1) )
    local negativeFmt = getNotNilValue(args['axis-negativeFmt'], '−%s')
    local positiveFmt = getNotNilValue(args['axis-positiveFmt'], '%s')
    local zeroFmt     = getNotNilValue(args['axis-zeroFmt'], '%s')
    local nudge       = getNotNilValue(args['axis-nudge'], '-1.8em')

    local wdth = math.abs ( (100 * inc) / (from - to) )
    local root = mw.html.create()

    local p = root
        :wikitext("<div name='line' style='clear:both;width:100%;max-width:100%;border-top:0.1em solid black;height:1em;'></div>")
        :tag('div')
            :attr('id', 'Scale')
            :cssText('clear:both;position:relative;top:-1.4em;left:-0.2em;width:100%;padding:0;height:2.5em')
            
    for var=from, to, inc do
        if from < to then
            if var+inc > to then wdth = 0 end
        else
            if var+inc < to then wdth = 0 end
        end
        
        local lbl
        if var < 0 then
            lbl = string.format( negativeFmt, math.abs(var) )
        elseif var > 0 then
            lbl = string.format( positiveFmt, math.abs(var) )
        else
            lbl = string.format( zeroFmt, math.abs(var) )
        end

        local markr = getNotNilValue(args['axis-marker-'..lbl], '│') 
		lbl = getNotNilValue(args['axis-'..lbl], lbl)
		
        p:tag('div')
            :cssText('float:left;overflow:visible;width:'.. wdth .. '%')
            :wikitext(markr)
            :tag('div')
                :cssText('font-size:86%; position:relative; left:'..nudge..'; overflow:visible; white-space:nowrap')
                :wikitext(lbl)
                :done()
        :done()
    end
    p:done()
    return tostring(root)
end

--Returns the first non nil value from the list of parameters.
function getNotNilValue(...)
    for _,v in pairs(arg) do --Do not use ipairs. Will stop at first nil
        if v then return v end
    end
    return nil
end

function affixNums(t, prefix, suffix)
    prefix = prefix or ''
    suffix = suffix or ''
    
    local pattern = '^' .. prefix .. '([1-9]%d*)' .. suffix .. '$'
    local nums = {}
    for k, v in pairs(t) do
        if type(k) == 'string' then            
            local num = mw.ustring.match(k, pattern)
            if num then
                nums[#nums + 1] = tonumber(num)
            end
        end
    end
    table.sort(nums)
    return nums
end

return horizontal_timeline