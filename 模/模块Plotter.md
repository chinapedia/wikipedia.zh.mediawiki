local p={}

function pick(a,n)
    return a[n+1]
end

function loadColorSet(page)
    if not(page) then page="" end
    if mw.ustring.sub(page,1,7) ~= "Module:" then page="Module:Plotter/DefaultColors" end
    local ct=mw.loadData(page)
    if not ct then ct=mw.loadData("Module:Plotter/DefaultColors") end
    local x=0
    local color={}
    local name={}
    repeat
        x=x+1
        local n=ct[x*2-1]
        local c=ct[x*2]
        if not (n and c) then break end
        table.insert(color,c)
        table.insert(name,n)
    until false
    return color, name
end
    
function piechartslice(color,percent,radius,link)
    radius=radius or 100
    local quadrant=math.floor(percent/25)
    local sin=math.floor(radius*math.sin(percent*math.pi/50))
    local cos=math.floor(radius*math.cos(percent*math.pi/50))
    local tan25=math.floor(-1*radius*math.cos(percent*math.pi/50)/math.sin(percent*math.pi/50))
    local output,lr,lrv,tv,bw1,bw2,bw3,bw4,bd,lrB,bw2B
    local a={} -- throwaway array to make value matrix more apparent
     -- quadrant 1 is upper left, quadrant 2 is lower left
    lr=pick({'left','right','right','left','left'},quadrant)
    lrv=pick({radius,radius,radius,radius,0},quadrant)
    tv=pick({radius-sin,0,radius,radius,0},quadrant)
     -- border width:bw1 (top) bw2 (right) bw3 (bottom) bw4 (left)
    bw1=pick({0,0,-1*sin,radius,0},quadrant)
    bw2=pick({0,tan25,-1*cos,0,2*radius},quadrant)
    bw3=pick({sin,radius,0,0,2*radius},quadrant)
    bw4=pick({cos,0,0,tan25,0},quadrant)
    bd=pick({'bottom-','right-','top-','left-',''},quadrant)
    lrB=pick({'n/a','right','left','left','n/a'},quadrant)
     -- right border for second div (the bottom border is radius and others are zero)
    bw2B=pick({'n/a',radius,2*radius,2*radius,'n/a'},quadrant)

    local output='<div class="transborder" style="position:absolute;width:'..radius..'px;line-height:0px;'..lr..':'..lrv..'px;top:'..tv..'px;border-width:'..bw1..'px '..bw2..'px '..bw3..'px '..bw4..'px;border-'..bd..'color:'..color..';"></div>'
    if quadrant==1 or quadrant==2 or quadrant==3 then
        output=output..'<div style="position:absolute;line-height:0px;border-style:solid;'..lrB..':0px;top:0px;border-width:0px '..bw2B..'px '..radius..'px 0px;border-color:'..color..';"></div>'
        if quadrant==3 then
            output=output.. '<div style="position:absolute;line-height:0px;border-style:solid;left:0px;top:0px;border-width:0px '..radius..'px '..2*radius..'px 0px;border-color:'..color..';"></div>'
        end
    end
    return output
end
    
function p.piechart(frame)
    local parent=frame.getParent(frame) or {}
    local color=loadColorSet(frame.args.colorset or parent.args.colorset) or {'red','green','blue','yellow','fuchsia','aqua','brown','orange','purple','sienna'}
    local value={}
    local label={}
    local link={}
    local slicecount=0
    local thumb,nowiki,radius
    if parent.args then
        thumb=parent.args.thumb
        nowik=parent.args.nowiki
        radius=parent.args.radius
    end
    thumb=frame.args.thumb or thumb
    nowiki=frame.args.nowiki or nowiki
    radius=frame.args.radius or radius or 100
    radius=tonumber(radius)
    if radius<1 then radius=100 end
    if not(thumb) then thumb="right" end
    if not(mw.ustring.match(thumb,"%S")) then thumb="right" end
    for i,j in pairs(parent.args or {}) do -- I should look up if there's a way to union parent.args AND frame.args
        local k=tonumber(mw.ustring.match(i,"color(%d*)"))
        if k then color[k]=j
        else k=tonumber(mw.ustring.match(i,"value(%d*)"))
            if k then
                value[k]=tonumber(j)
                if k>slicecount then slicecount=k end -- not using #value to avoid randomness if some values are left out
            else k=tonumber(mw.ustring.match(i,"label(%d*)"))
                if k then label[k]=j
                end
            end
        end
    end
     --- innermost absolute div around circle, then a second thumbcaption div around legend.  Note (/div)(div) at core between circle and legend.  The rest are accreted around this center.
    output='<div style="position:absolute;left:0;top:0">[[File:Circle_frame.svg|'..(radius*2)..'px]]<Module:Plotter internal imgmap insertion token></div> </div> <!-- Legend --> <div class="thumbcaption"> '
    for i,j in pairs(frame.args or {}) do -- supersede parent.args values
        local k=tonumber(mw.ustring.match(i,"color(%d*)"))
        if k then color[k]=j or ""
        else k=tonumber(mw.ustring.match(i,"value(%d*)"))
            if k then
                value[k]=tonumber(j)
                if k>slicecount then slicecount=k end -- not using #value to avoid randomness if some values are left out
            else k=tonumber(mw.ustring.match(i,"label(%d*)"))
                if k then label[k]=j or ""
                else k=tonumber(mw.ustring.match(i,"link(%d*)"))
                    if k then link[k]=j or ""
                    end
                end
            end
        end
    end
    local valuesum=0 -- sum of all slices
    local imgmap="" -- beginning of a polygon specification for <imagemap>
    for slice=1,slicecount do
        if value[slice] then
            if link[slice] then
                 -- center of the circle, NOTE coords are relative to 600 px image before scaling NOT the radius
                imgmap=imgmap.."poly 300 300" 
                for x=valuesum,valuesum+value[slice] do
                    local sin=math.floor(300*math.sin(x*math.pi/50))
                    local cos=math.floor(300*math.cos(x*math.pi/50))
                    imgmap=imgmap.." "..300+cos.." "..300-sin
                end
                imgmap=imgmap.." [["..link[slice].."|"..link[slice].."]]\n"
            end
            valuesum=valuesum+value[slice]
            output=piechartslice(color[slice],valuesum,radius)..output.."{{legend|"..(color[slice] or "").."|"..(label[slice] or "").." ("..valuesum.."%)}}"
        end
    end
     --- imagemap has its own absolute div to position with a separate transparent image
    imgmap='<div style="position:absolute;top:0px;left:0px;width:'..2*radius..'px;height:'..2*radius..'px;z-index:1000;">\n<imagemap>\nFile:transparent600.gif|'..2*radius..'px\n'..imgmap..'desc none\n</imagemap></div>'
    if #link==0 then imgmap="" end -- make sure imgmap is blank if no links
     --- outer thumb tleft/tright is float/clear left or right
     --- thumbinner encapsulates the graph
     --- third relative div container ends in the middle of ..output..
     --- next third div style "thumbcaption" begins in ..output..
     --- all three end at end
    output='<div class="thumb t'..thumb..'"><div class="thumbinner" style="width:'..2*radius..'px"> <!-- Graph --> <div style="background-color:white;margin:auto;position:relative;width:'..2*radius..'px;height:'..2*radius..'px;overflow:hidden;"> '..output..'{{legend|white|Other ('..tostring(math.floor((100-valuesum)*1000000)/1000000)..'%)}}</div></div></div>'
    output=mw.ustring.gsub(output,"<Module:Plotter internal imgmap insertion token>", imgmap)
    if nowiki then return frame.preprocess(frame,"<pre><nowiki>"..output.."</nowiki></pre>") else return frame.preprocess(frame,output) end
end
    
function p.main(frame)
    local args=frame.args
    local parent=frame.getParent(frame)
    local pargs=parent.args or {}
    local icon=args.icon or pargs.icon
    local iconradius=args.iconradius or pargs.iconradius or 10
    local lineicon=args.lineicon or pargs.lineicon or "•"
    local lineiconradius=args.lineiconradius or pargs.lineiconradius or 5
    local linefix=iconradius-lineiconradius
    local plotsizex = args.plotsizex or pargs.plotsizex or 100
    local plotsizey = args.plotsizey or pargs.plotsizey or 100
    local plotstep = args.plotstep or pargs.plotstep or 10
    local output = [[<div_style="position:relative;border-style:solid;border-color:_#0077ff;width:|<div style="position:relative;border-style:solid;border-color: #0077ff;width:]] .. plotsizex+(2*iconradius) .. [[px;height:|px;height:]] .. plotsizey+(2*iconradius) .. [[px;">|px;">]]
    if (args[2] or pargs[2]) ~= nil then
        local x=(args[1] or pargs[1])+0
        local y=(args[2] or pargs[2])+0
        local xmin = x
        local xmax = x
        local ymin = y
        local ymax = y
        local index = 3
        while (args[index+1] or pargs[index+1]) ~= nil do
           local x=(args[index]+0 or pargs[index]+0)
           local y=(args[index+1]+0 or pargs[index+1]+0)
           if (x < xmin) then xmin = x end
           if (x > xmax) then xmax = x end
           if (y < ymin) then ymin = y end
           if (y > ymax) then ymax = y end
           index = index + 2
        end
        local lastx=0
        local lasty=0
        if args[2] ~= nil then
            local x=(args[1] or pargs[1])+0
            local y=(args[2] or pargs[2])+0
            local plotx=math.floor(plotsizex*(x-xmin)/(xmax-xmin))
            local ploty=math.floor((plotsizey-plotsizey*(y-ymin)/(ymax-ymin)))
            output = output .. [[<span_style="position:absolute;left:|<span style="position:absolute;left:]] .. plotx .. [[px;_top:|px; top:]] .. ploty .. [[px;">|px;">]] .. icon .. "</span>"
            lastx = plotx
            lasty = ploty
        end
        index = 3
        while (args[index+1] or pargs[index+1]) ~= nil do
            local x=(args[index] or pargs[index])+0
            local y=(args[index+1] or pargs[index+1])+0
            local plotx=math.floor(plotsizex*(x-xmin)/(xmax-xmin))
            local ploty=math.floor((plotsizey-plotsizey*(y-ymin)/(ymax-ymin)))
            if plotstep+0 ~= 0 then
               local delx=plotx-lastx
               local dely=ploty-lasty
               plotdist=math.sqrt(delx*delx+dely*dely)
               plotparm=plotdist-iconradius-plotstep/2
               while plotparm>iconradius+lineiconradius+plotstep/2 do
                  output = output .. [[<span_style="position:absolute;left:|<span style="position:absolute;left:]] .. lastx+linefix+math.floor(delx*(plotparm/plotdist)) .. [[px;_top:|px; top:]] .. lasty+linefix+math.floor(dely*(plotparm/plotdist)) .. [[px;">|px;">]] .. lineicon .. "</span>"
                  plotparm = plotparm - plotstep
               end
               lastx = plotx
               lasty = ploty
            end
            output = output .. [[<span_style="position:absolute;left:|<span style="position:absolute;left:]] .. plotx .. [[px;_top:|px; top:]] .. ploty .. [[px;">|px;">]] .. icon .. "</span>"
            index = index + 2
        end
    else output = "error"
    end
    output = output .. "</div>"
    return output
end

-- data structure is
-- data[y][x].value
-- maxyval[y]
-- data[y].color
-- data[y].legend
-- data.legend[x]

function p.bar(frame)
    local debuglog=""
    local args=frame.args
    local parent=frame.getParent(frame)
    local pargs=parent.args or {}
    local delimiter = args.delimiter or pargs.delimiter or ","
    local width = args.width or pargs.width or 200
    local height = args.height or pargs.height or 200
    
     ---- Set up the table of "norms".  Series 1 to N normalize to (%d+)
    local normalize = args.normalize or pargs.normalize or ""
    local prowl=mw.ustring.gmatch(normalize,"(%d+)")
    norm={}
    local ngroup={} -- ngroup[yseries] identifies an index for ymax
    local nngroup=0 -- the current maximum ngroup assigned
    repeat
       local t=prowl()
       if not(t) then break end
       t=tonumber(t)
       table.insert(norm,t)
    until false
    
     --- import the actual data in group1 .. groupN
    local yseries=0;local x=0
    local data={} -- main data storage array
    local maxy=0;local maxx=0; local maxyval={}; local minyval={} -- keeping these out of the data array after being driven half mad giving them cutesy names in the array!
    repeat
       yseries=yseries+1
       data[yseries]={}
        --- pull in the "groupN" data (delimited) --> text
       local text=args["group"..yseries] -- each _group_ is a group of x-values in a y-series
       if not (text) then maxy=yseries-1 break end
               ---- pull in the originN=some number
       data[yseries].origin=args["origin"..yseries] or 0
       data[yseries].origin=tonumber(data[yseries].origin)
       data[yseries].max=data[yseries].origin;data[yseries].min=data[yseries].origin
       debuglog=debuglog.."I"..yseries..tostring(norm[yseries])
        --- set ngroup[yseries] to whatever its norm points at, or new
       if norm[yseries]
       then if ngroup[norm[yseries]]
           then ngroup[yseries]=ngroup[norm[yseries]]
           else nngroup=nngroup+1
               ngroup[yseries]=nngroup
           end
       else ngroup[yseries]=1 -- if no norm specified, just dump to the first series group
       end
        ---- pull in the actual values
       prowl=mw.ustring.gmatch(text,"([^" .. delimiter .. "]+)")
       x=0
       repeat
          x=x+1
          data[yseries][x]={}
          data[yseries][x].value=prowl()
          debuglog=debuglog.."V"..x..yseries..tostring(data[yseries][x].value)
          if not(data[yseries][x].value) then if x>maxx then maxx = x-1 end; break end
          data[yseries][x].value=tonumber(data[yseries][x].value)
          if data[yseries].max then if data[yseries][x].value>data[yseries].max then data[yseries].max=data[yseries][x].value end else data[yseries].max=data[yseries][x].value end
          if data[yseries].min then if data[yseries][x].value<data[yseries].min then data[yseries].min=data[yseries][x].value end else data[yseries].min=data[yseries][x].value end
       until false
        ---- pull in the colorN="whatever"
       data[yseries].color=args["color"..yseries] or "" -- one color for yseries group; can be nil
       if data[yseries].color=="" then data[yseries].color="black" end
    until false
    
     --- import the xlegends for each group
    prowl=mw.ustring.gmatch(args.xlegend,"[^" .. delimiter .. "]+")
    x=0
    data.legend={} -- for x legends, y="legend"
    repeat
       x=x+1
       data.legend[x]=prowl()
       if not (data.legend[x]) then break end
       data.legend[x]=data.legend[x]
    until false
    
     --- import the ylegends for each group
    prowl=mw.ustring.gmatch(args.ylegend,"[^" .. delimiter .. "]+")
    yseries=0
    repeat
       yseries=yseries+1
       data[yseries].legend=prowl()
    until not (data[yseries].legend)
    
     -- set the maxval[ngroup[(each series)]] = data[(any series in ngroup).max
    yseries=0
    repeat
       yseries=yseries+1
       if not(data[yseries].max) then break end
       debuglog=debuglog..tostring(yseries)..":"..tostring(ngroup[yseries]) .. ">"..tostring(data[yseries].max)
       if maxyval[ngroup[yseries]]
       then if data[yseries].max>maxyval[ngroup[yseries]]
           then maxyval[ngroup[yseries]]=data[yseries].max
           end
       else maxyval[ngroup[yseries]]=data[yseries].max;debuglog=debuglog.."A"..tostring(data[yseries].max)..tostring(data[yseries].min)
       end
       if minyval[ngroup[yseries]]
       then if data[yseries].min<minyval[ngroup[yseries]]
           then minyval[ngroup[yseries]]=data[yseries].min
           end
       else minyval[ngroup[yseries]]=data[yseries].min;debuglog=debuglog.."A"..tostring(data[yseries].min)
       end


    until false

     --- Draw the output
    local output = [[<div_style="position:relative;border-style:solid;border-color:_#0077ff;width:|<div style="position:relative;border-style:solid;border-color: #0077ff;width:]] .. width .. [[px;height:|px;height:]] .. height .. [[px;">|px;">]]
    local output='<div style="position:relative;overflow:visible;border-style:solid;border-color: #0077ff;width:' .. width .. 'px;height:' .. height .. 'px;">'
    local topreserve=20*(maxy)
    local bottomreserve=20
    local leftreserve=20
    local rightreserve=20
    local reducedheight=height-topreserve-bottomreserve
    local reducedwidth=width-leftreserve-rightreserve
    local ew=math.floor(reducedwidth/((maxx)*(maxy+1)))
    for y = 1,maxy do
        for x = 1, maxx do
            debuglog=debuglog..y..x..tostring(ngroup[y])..tostring(data[y][x]) .. tostring(maxyval[ngroup[y]])..tostring(minyval[ngroup[y]])
            if data[y][x] and maxyval[ngroup[y]]
            then local pw=(data[y][x].value-data[y].origin)/(maxyval[ngroup[y]]-minyval[ngroup[y]]) -- proportion of value to the max value for that y-series
               local po=(data[y].origin-minyval[ngroup[y]])/(maxyval[ngroup[y]]-minyval[ngroup[y]])
               local eh=math.floor(pw*reducedheight)
               local et=topreserve+math.floor(reducedheight - eh - po*reducedheight)
               if eh<0 then eh=-1*eh;et=et-eh end -- pw can be negative; plot "backwards" looks the same
               local el=leftreserve+math.floor(((x-1)*(maxy+1) + (y-1) + 0.5)*ew)
               output=output..'<div style="position:absolute;background-color:' .. data[y].color .. ';width:' .. ew .. 'px;height:' .. eh .. 'px;top:' .. et .. 'px;left:' .. el .. 'px;"></div>'
            end -- if data[y][x] and maxval[ngroup[y]]
        end -- for x = 1, maxx
    end -- for y=1,maxy
     ---- draw the ylegends
    for x = 1,maxx do
        output=output .. '<span style="position:absolute;top:'.. reducedheight+topreserve .. 'px;left:'..leftreserve+math.floor(( (x-1)*(maxy+1)+(maxx/2) )*ew)..'px;">'..data.legend[x]..'</span>'
    end
    for y = 1,maxy do
        output=output .. '<span style="position:absolute;color:'.. data[y].color .. ';top:' .. (y-1)*20 .. 'px;left:'.. (leftreserve+10) ..'px;">'.. (data[y].legend or "") ..'</span>'
        local point={minyval[ngroup[y]],data[y].origin,maxyval[ngroup[y]]}
        for i,j in ipairs(point) do
           local po=(j-minyval[ngroup[y]])/(maxyval[ngroup[y]]-minyval[ngroup[y]])
           local et=topreserve+math.floor((1-po)*reducedheight)
           debuglog=debuglog.."pass" .. y .. ngroup[y]
           if tonumber(ngroup[y])==1
           then debuglog=debuglog.."left";output=output .. '<span style="position:absolute;color:'.. data[y].color .. ';'..data[y].color .. ';text-align:right;top:' .. et-10 .. 'px;width:'..leftreserve..'px;left:0px;">'.. j .. '</span>'
           else debuglog=debuglog.."right";output=output .. '<span style="position:absolute;color:'.. data[y].color .. ';'..data[y].color .. ';text-align:left;top:' .. et-10 .. 'px;width:'..rightreserve..'px;left:'..leftreserve+reducedwidth..'px;">'.. j .. '</span>'
           end
       end
    end
    debuglog=debuglog..tostring(maxyval[1])..tostring(maxyval[2])..tostring(maxyval[3])..tostring(data[1].max)..tostring(data[2].max)..tostring(data[3].max)..tostring(minyval[1])..tostring(minyval[2])..tostring(minyval[3])..tostring(data[1].min)..tostring(data[2].min)..tostring(data[3].min)..data.legend[1]..data.legend[2]..data.legend[3]
    output = output .. "</div>\n"
    if (args.debug or pargs.debug) then output=output..debuglog end
    return output
end

return p