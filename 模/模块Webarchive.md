--[[ ----------------------------------

     Lua module implementing the {{webarchive}} template. 

       A merger of the functionality of three templates: {{wayback}}, {{webcite}} and {{cite archives}}
   
  ]]

local p = {}

--[[--------------------------< inlineError >-----------------------

     Critical error. Render output completely in red. Add to tracking category.

 ]]

local function inlineError(arg, msg)

  track["Category:Webarchive模板错误"] = 1
  return '<span style="font-size:100%" class="error citation-comment">webarchive模板错误：检查<code style="color:inherit; border:inherit; padding:inherit;">|' .. arg .. '=</code>参数。' .. msg  .. '</span>'

end

--[[--------------------------< inlineRed >-----------------------

      Render a text fragment in red, such as a warning as part of the final output.
      Add tracking category.

 ]]

local function inlineRed(msg, trackmsg)

  if trackmsg == "warning" then
    track["Category:Webarchive模板警告"] = 1 
  elseif trackmsg == "error" then
    track["Category:Webarchive模板错误"] = 1 
  end

  return '<span style="font-size:100%" class="error citation-comment">' .. msg .. '</span>'

end

--[[--------------------------< trimArg >-----------------------

     trimArg returns nil if arg is "" while trimArg2 returns 'true' if arg is "" 
     trimArg2 is for args that might accept an empty value, as an on/off switch like nolink=

 ]]

local function trimArg(arg)
  if arg == "" or arg == nil then
    return nil
  else
    return mw.text.trim(arg)
  end
end
local function trimArg2(arg)
  if arg == nil then
    return nil
  else
    return mw.text.trim(arg)
  end
end

--[[--------------------------< base62 >-----------------------

     Convert base-62 to base-10
     Credit: https://de.wikipedia.org/wiki/Modul:Expr 

  ]]

local function base62( value )

    local r = 1

    if value:match( "^%w+$" ) then
        local n = #value
        local k = 1
        local c
        r = 0
        for i = n, 1, -1 do
            c = value:byte( i, i )
            if c >= 48  and  c <= 57 then
                c = c - 48
            elseif c >= 65  and  c <= 90 then
                c = c - 55
            elseif c >= 97  and  c <= 122 then
                c = c - 61
            else    -- How comes?
                r = 1
                break    -- for i
            end
            r = r + c * k
            k = k * 62
        end -- for i
    end
    return r
end 

--[[--------------------------< tableLength >-----------------------

      Given a 1-D table, return number of elements

  ]]

local function tableLength(T)
  local count = 0
  for _ in pairs(T) do count = count + 1 end
  return count
end


--[[--------------------------< dateFormat >-----------------------

     Given a date string, return its format: dmy, mdy, iso, ymd
       If unable to determine return nil

  ]]

local function dateFormat(date)

  local dt = {}
  dt.split = {}

  dt.split = mw.text.split(date, "-")
  if tableLength(dt.split) == 3 then
    if tonumber(dt.split[1]) > 1900 and tonumber(dt.split[1]) < 2200 and tonumber(dt.split[2]) and tonumber(dt.split[3]) then
      return "iso"
    else
      return nil
    end
  end  

  dt.split = mw.text.split(date, " ")
  if tableLength(dt.split) == 3 then
    if tonumber(dt.split[3]) then
      if tonumber(dt.split[3]) > 1900 and tonumber(dt.split[3]) < 2200 then
        if tonumber(dt.split[1]) then
          return "dmy"
        else
          return "mdy"
        end 
      else
        if tonumber(dt.split[1]) then
          if tonumber(dt.split[1]) > 1900 and tonumber(dt.split[1]) < 2200 then
            return "ymd"
          end
        end
      end
    end
  end
  return nil

end

--[[--------------------------< makeDate >-----------------------

     Given a zero-padded 4-digit year, 2-digit month and 2-digit day, return a full date in df format
     df = mdy, dmy, iso, ymd

 ]]

local function makeDate(year, month, day, df)

  if not year or year == "" or not month or month == "" or not day or day == "" then
    return nil
  end

  local zmonth = month                                                      -- month with leading 0
  month = month:match("0*(%d+)")                                            -- month without leading 0
  if tonumber(month) < 1 or tonumber(month) > 12 then
    return year
  end
  local nmonth = os.date("%B", os.time{year=2000, month=month, day=1} )     -- month in name form       
  if not nmonth then
    return year
  end

  local zday = day
  day = zday:match("0*(%d+)")
  if tonumber(day) < 1 or tonumber(day) > 31 then
    if df == "mdy" or df == "dmy" then
      return nmonth .. " " .. year
    elseif df == "iso" then
      return year .. "-" .. zmonth 
    elseif df == "ymd" then
      return year .. " " .. nmonth
    else
      return nmonth .. " " .. year
    end
  end                                       

  if df == "mdy" then
    return nmonth .. " " .. day .. ", " .. year         -- September 1, 2016
  elseif df == "dmy" then
    return day .. " " .. nmonth .. " " .. year          -- 1 September 2016
  elseif df == "iso" then
    return year .. "-" .. zmonth .. "-" .. zday         -- 2016-09-01
  elseif df == "ymd" then
    return year .. " " .. nmonth .. " " .. cday          -- 2016 September 1
  else
    return nmonth .. " " .. day .. ", " .. year         -- September 1, 2016
  end

end


--[[--------------------------< decodeWebciteDate >-----------------------

      Given a URI-path to Webcite (eg. /67xHmVFWP) return the encoded date in df format

  ]]
local function decodeWebciteDate(path, df)

    local dt = {}
    dt.split = {}

    dt.split = mw.text.split(path, "/")

    -- valid URL formats that are not base62

    -- http://www.webcitation.org/query?id=1138911916587475
    -- http://www.webcitation.org/query?url=http..&date=2012-06-01+21:40:03
    -- http://www.webcitation.org/1138911916587475
    -- http://www.webcitation.org/cache/73e53dd1f16cf8c5da298418d2a6e452870cf50e
    -- http://www.webcitation.org/getfile.php?fileid=1c46e791d68e89e12d0c2532cc3cf629b8bc8c8e

    if mw.ustring.find( dt.split[2], "query", 1, plain) or 
       mw.ustring.find( dt.split[2], "cache", 1, plain) or
       mw.ustring.find( dt.split[2], "getfile", 1, plain) or
       tonumber(dt.split[2]) then
      return "query"
    end

    dt.full = os.date("%Y %m %d", string.sub(string.format("%d", base62(dt.split[2])),1,10) )
    dt.split = mw.text.split(dt.full, " ")
    dt.year = dt.split[1]
    dt.month = dt.split[2]
    dt.day = dt.split[3]

    if not tonumber(dt.year) or not tonumber(dt.month) or not tonumber(dt.day) then
      return inlineRed("[日期錯誤] (1)", "error")
    end

    if tonumber(dt.month) > 12 or tonumber(dt.day) > 31 or tonumber(dt.month) < 1 then
      return inlineRed("[日期錯誤] (2)", "error")
    end
    if tonumber(dt.year) > tonumber(os.date("%Y")) or tonumber(dt.year) < 1900 then
      return inlineRed("[日期錯誤] (3)", "error")
    end

    fulldate = makeDate(dt.year, dt.month, dt.day, df)
    if not fulldate then
      return inlineRed("[日期錯誤] (4)", "error")
    else
      return fulldate
    end

end

--[[--------------------------< snapDateToString >-----------------------

Given a URI-path to Wayback (eg. /web/20160901010101/http://example.com )
  return the formatted date eg. "September 1, 2016" in df format 
  Handle non-digits in snapshot ID such as "re_" and "-" and "*"

 ]]

local function decodeWaybackDate(path, df)

    local snapdate, snapdatelong, currdate, fulldate

    local safe = path
    snapdate = string.gsub(safe, "^/w?e?b?/?", "")                      -- Remove leading "/web/" or "/"
    safe = snapdate
    local N = mw.text.split(safe, "/")
    snapdate = N[1]
    if snapdate == "*" then                                             -- eg. /web/*/http..
      return "index"
    end
    safe = snapdate
    snapdate = string.gsub(safe, "[a-z][a-z]_[0-9]?$", "")              -- Remove any trailing "re_" from date 
    safe = snapdate
    snapdate = string.gsub(safe, "[-]", "")                             -- Remove dashes from date eg. 2015-01-01 
    safe = snapdate
    snapdate = string.gsub(safe, "[*]$", "")                            -- Remove trailing "*" 

    if not tonumber(snapdate) then
      return inlineRed("[日期錯誤] (2)", "error")
    end
    local dlen = string.len(snapdate)
    if dlen < 4 then
      return inlineRed("[日期錯誤] (3)", "error")
    end
    if dlen < 14 then
      snapdatelong = snapdate .. string.rep("0", 14 - dlen)
    else
      snapdatelong = snapdate
    end
    local year = string.sub(snapdatelong, 1, 4)
    local month = string.sub(snapdatelong, 5, 6)
    local day = string.sub(snapdatelong, 7, 8)
    if not tonumber(year) or not tonumber(month) or not tonumber(day) then
      return inlineRed("[日期錯誤] (4)", "error")
    end
    if tonumber(month) > 12 or tonumber(day) > 31 or tonumber(month) < 1 then
      return inlineRed("[日期錯誤] (5)", "error")
    end
    currdate = os.date("%Y")
    if tonumber(year) > tonumber(currdate) or tonumber(year) < 1900 then
      return inlineRed("[日期錯誤] (6)", "error")
    end

    fulldate = makeDate(year, month, day, df)
    if not fulldate then
      return inlineRed("[日期錯誤] (7)", "error")
    else
      return fulldate
    end

end


--[[--------------------------< serviceName >-----------------------

     Given a domain extracted by mw.uri.new() (eg. web.archive.org) set tail string and service ID

  ]]

local function serviceName(frame, host, nolink)

  local tracking = "Category:Webarchive模板其他存档站点"

  local bracketopen = "[["
  local bracketclose = "]]"
  if nolink then
    bracketopen = ""
    bracketclose = ""
  end
  
  local service_names = {
  	['wayback'] = bracketopen .. "Wayback Machine|-{zh-cn:互联网档案馆; zh-tw:網際網路檔案館; zh-hk:互聯網檔案館;}-" .. bracketclose,
  	['webcite'] = bracketopen .. "WebCite" .. bracketclose,
  	['archiveis'] = bracketopen .. "Archive.is" .. bracketclose,
  	['archiveit'] = bracketopen .. "Archive-It" .. bracketclose,
  }
  
  ulx.url1.service = "other"
  ulx.url1.name = nil

  if mw.ustring.find( host, "archive.org", 1, plain ) then
    ulx.url1.service = "wayback"
  elseif mw.ustring.find( host, "webcitation.org", 1, plain ) then
    ulx.url1.service = "webcite"
  elseif mw.ustring.find( host, "archive.is", 1, plain ) then
    ulx.url1.service = "archiveis"
  elseif mw.ustring.find( host, "archive.fo", 1, plain ) then
    ulx.url1.service = "archiveis"
  elseif mw.ustring.find( host, "archive.today", 1, plain ) then
    ulx.url1.service = "archiveis"
  elseif mw.ustring.find( host, "archive.il", 1, plain ) then
    ulx.url1.service = "archiveis"
  elseif mw.ustring.find( host, "archive.ec", 1, plain ) then
    ulx.url1.service = "archiveis"
  elseif mw.ustring.find( host, "archive[-]it.org", 1, plain ) then
    ulx.url1.service = "archiveit"
  elseif mw.ustring.find( host, "arquivo.pt", 1, plain) then
    ulx.url1.name = "Portuguese Web Archive" 
  elseif mw.ustring.find( host, "loc.gov", 1, plain ) then
    ulx.url1.name = bracketopen .. "美國國會圖書館" .. bracketclose
  elseif mw.ustring.find( host, "webharvest.gov", 1, plain ) then
    ulx.url1.name = bracketopen .. "國家檔案和記錄管理局" .. bracketclose
  elseif mw.ustring.find( host, "bibalex.org", 1, plain ) then
    ulx.url1.name = "[[Bibliotheca_Alexandrina#Internet_Archive_partnership|Bibliotheca Alexandrina]]"
  elseif mw.ustring.find( host, "collectionscanada", 1, plain ) then
    ulx.url1.name = "Canadian Government Web Archive"
  elseif mw.ustring.find( host, "haw.nsk", 1, plain ) then
    ulx.url1.name = "Croatian Web Archive (HAW)"
  elseif mw.ustring.find( host, "veebiarhiiv.digar.ee", 1, plain ) then
    ulx.url1.name = "Estonian Web Archive"
  elseif mw.ustring.find( host, "vefsafn.is", 1, plain ) then
    ulx.url1.name = "[[National_and_University_Library_of_Iceland|National and University Library of Iceland]]"
  elseif mw.ustring.find( host, "proni.gov", 1, plain ) then
    ulx.url1.name = frame:expandTemplate{ title = "Link-en", args = {"北愛爾蘭公共記錄辦公室", "Public Record Office of Northern Ireland"} }
  elseif mw.ustring.find( host, "uni[-]lj.si", 1, plain ) then
    ulx.url1.name = "Slovenian Web Archive"
  elseif mw.ustring.find( host, "stanford.edu", 1, plain ) then
    ulx.url1.name = "[[Stanford_University_Libraries|Stanford Web Archive]]"
  elseif mw.ustring.find( host, "nationalarchives.gov.uk", 1, plain ) then
    ulx.url1.name = frame:expandTemplate{ title = "Link-en", args = {"英國政府網際網路檔案館", "UK Government Web Archive", "英國政府-{zh-cn:互联网; zh-tw:網際網路; zh-hk:互聯網;}-檔案館"} }
  elseif mw.ustring.find( host, "parliament.uk", 1, plain ) then
    ulx.url1.name = frame:expandTemplate{ title = "Link-en", args = {"英國議會網際網路檔案館", "UK Parliament's Web Archive", "英國議會-{zh-cn:互联网; zh-tw:網際網路; zh-hk:互聯網;}-檔案館"} }
  elseif mw.ustring.find( host, "webarchive.org.uk", 1, plain ) then
    ulx.url1.name = frame:expandTemplate{ title = "Link-en", args = {"英國網際網路檔案館", "UK Web Archive", "英國-{zh-cn:互联网; zh-tw:網際網路; zh-hk:互聯網;}-檔案館"} }
  elseif mw.ustring.find( host, "nlb.gov.sg", 1, plain ) then
    ulx.url1.name = "Web Archive Singapore" 
  elseif mw.ustring.find( host, "pandora.nla.gov.au", 1, plain ) then
    ulx.url1.name = frame:expandTemplate{ title = "Link-en", args = {"潘朵拉網際網路檔案館", "Pandora Archive", "潘朵拉-{zh-cn:互联网; zh-tw:網際網路; zh-hk:互聯網;}-檔案館"} }
  elseif mw.ustring.find( host, "perma.cc", 1, plain ) then
    ulx.url1.name = frame:expandTemplate{ title = "Link-en", args = {"Perma.cc"} }
  elseif mw.ustring.find( host, "perma[-]archives.cc", 1, plain ) then
    ulx.url1.name = frame:expandTemplate{ title = "Link-en", args = {"Perma.cc"} }
  elseif mw.ustring.find( host, "screenshots.com", 1, plain ) then
    ulx.url1.name = "Screenshots" 
  elseif mw.ustring.find( host, "wikiwix.com", 1, plain ) then
    ulx.url1.name = "Wikiwix" 
  elseif mw.ustring.find( host, "freezepage.com", 1, plain ) then
    ulx.url1.name = "Freezepage" 
  elseif mw.ustring.find( host, "webcache.googleusercontent.com", 1, plain ) then
    ulx.url1.name = "Google網頁-{zh-tw:快取;zh-cn:缓存}-" 
  else
  	ulx.url1.name = ulx.url1.host .. " " .. inlineRed("错误：存档服务未知")
    tracking = "Category:Webarchive模板未知存档站点"
  end

  if (ulx.url1.service ~= "other") and (ulx.url1.name == nil) then
  	tracking = 'Category:Webarchive模板' .. ulx.url1.service .. '链接'
  	ulx.url1.name = service_names[ulx.url1.service] or ulx.url1.service
  end

  track[tracking] = 1
end

--[[--------------------------< parseExtraArgs >-----------------------

     Parse numbered arguments starting at 2, such as url2..url10, date2..date10, title2..title10
       For example: {{webarchive |url=.. |url4=.. |url7=..}}
         Three url arguments not in numeric sequence (1..4..7). 
         Function only processes arguments numbered 2 or greater (in this case 4 and 7)
         It creates numeric sequenced table entries like:
           urlx.url2.url = <argument value for url4>
           urlx.url3.url = <argument value for url7>
       Returns the number of URL arguments found numbered 2 or greater (in this case returns "2")

 ]]

local function parseExtraArgs()

  local i, j, argurl, argurl2, argdate, argtitle

  j = 2
  for i = 2, maxurls do
    argurl = "url" .. i
    if trimArg(args[argurl]) then
      argurl2 = "url" .. j
      ulx[argurl2] = {}
      ulx[argurl2]["url"] = args[argurl]
      argdate = "date" .. j
      if trimArg(args[argdate]) then
        ulx[argurl2]["date"] = args[argdate]
      else
        ulx[argurl2]["date"] = inlineRed("[缺少日期]", "warning")
      end
      argtitle = "title" .. j
      if trimArg(args[argtitle]) then
        ulx[argurl2]["title"] = args[argtitle]
      else
        ulx[argurl2]["title"] = nil
      end
      j = j + 1
    end
  end

  if j == 2 then
    return 0
  else
    return j - 2
  end

end

--[[--------------------------< comma >-----------------------

     Given a date string, return "," if it's MDY 

  ]]

local function comma(date)
  local N = mw.text.split(date, " ")
  local O = mw.text.split(N[1], "-") -- for ISO
  if O[1] == "index" then return "" end
  if not tonumber(O[1]) then
    return "，"
  else
    return ""
  end
end

--[[--------------------------< createTracking >-----------------------

     Return data in track[] ie. tracking categories

  ]]

local function createTracking()

  local sand = ""
  if tableLength(track) > 0 then                        
    for key,_ in pairs(track) do
      sand = sand .. "[["_.._key_.._"|" .. key .. "]]"
    end
  end
  return sand

end

--[[--------------------------< createRendering >-----------------------

     Return a rendering of the data in ulx[][]

  ]]

local function createRendering()

    local sand, displayheader, displayfield

    local period1 = ""   -- For backwards compat with {{wayback}}
    local period2 = "."                                                            
  
    local indexstr = "存檔日期"
    if ulx.url1.date == "index" then	-- what is this?
      indexstr = "存檔"
    end  
                                                                                          -- For {{wayback}}, {{webcite}}

    if ulx.url1.format == "none" then                                                     
      if not ulx.url1.title and not ulx.url1.date then                                    -- No title. No date
        sand = ulx.url1.name .. "的[" .. ulx.url1.url .. " " ..  "存档]"
      elseif not ulx.url1.title and ulx.url1.date then                                    -- No title. Date.
        if ulx.url1.service == "wayback" then 
          period1 = "."
          period2 = "" 
        end
        sand = ulx.url1.name .. "的[" .. ulx.url1.url .. " " .. "存檔]，存档日期" .. ulx.url1.date .. comma(ulx.url1.date) .. period1
      elseif ulx.url1.title and not ulx.url1.date then                                    -- Title. No date.
        sand = "[" .. ulx.url1.url .. " " .. ulx.url1.title .. "]" .. "，存档于" .. ulx.url1.name
      elseif ulx.url1.title and ulx.url1.date then                                        -- Title. Date.
        sand = "[" .. ulx.url1.url .. " " .. ulx.url1.title .. "]" .. "，存档于" .. ulx.url1.name .. "（" .. indexstr .. " " .. ulx.url1.date .. "）"
      else
        return nil
      end
      if ulx.url1.extraurls > 0 then                                                      -- For multiple archive URLs
        local tot = ulx.url1.extraurls + 1
        sand = sand .. period2 .. " 其他存档："
        for i=2,tot do
          local indx = "url" .. i
          if ulx[indx]["title"] then 
            displayfield = "title"
          else
            displayfield = "date"
          end
          sand = sand .. "[" .. ulx[indx]["url"] .. " " .. ulx[indx][displayfield] .. "]"
          if i == tot then
            sand = sand .. "."
          else
            sand = sand .. ", "
          end
        end
      else
        return sand  
      end
      return sand
                                                                                          -- For {{cite archives}}

    else                                                                  
      if ulx.url1.format == "addlarchives" then                           -- Multiple archive services 
        displayheader = "其他存档："
      else                                                                -- Multiple pages from the same archive 
        displayheader = "於" .. ulx.url1.date .. "记录的其他存档："
      end
      local tot = 1 + ulx.url1.extraurls
      local sand = displayheader
      for i=1,tot do
        local indx = "url" .. i
        displayfield = ulx[indx]["title"]
        if ulx.url1.format == "addlarchives" then
          if not displayfield then 
            displayfield = ulx[indx]["date"]
          end
        else
          if not displayfield then 
            displayfield = "第" .. i .. "页"
          end
        end
        sand = sand .. "[" .. ulx[indx]["url"] .. " " .. displayfield .. "]"
        if i == tot then
          sand = sand .. "."
        else
          sand = sand .. "、"
        end
      end
      return sand
    end
end

function p.webarchive(frame)
  args = frame.args
  if (args[1]==nil) and (args["url"]==nil) then           -- if no argument provided than check parent template/module args
    args = frame:getParent().args 
  end
 
  local tname = "Webarchive"                              -- name of calling template. Change if template rename.
  ulx = {}                                                -- Associative array to hold template data 
  track = {}                                              -- Associative array to hold tracking categories
  maxurls = 10                                            -- Max number of URLs allowed. 
  local verifydates = "yes"                               -- See documentation. Set "no" to disable.

                                                          -- URL argument (first)

  local url1 = trimArg(args.url) or trimArg(args.url1)           
  if not url1 then
    return inlineError("url", "空。") .. createTracking()
  end
  if mw.ustring.find( url1, "https://web.http", 1, plain ) then    -- track bug 
    track["Category:Webarchive模板错误"] = 1 
    return inlineError("url", "https://web.http") .. createTracking()
  end 
  if url1 == "https://web.archive.org/http:/" then                 -- track bug
    track["Category:Webarchive模板错误"] = 1 
    return inlineError("url", "无效URL") .. createTracking()
  end

  ulx.url1 = {}
  ulx.url1.url = url1
  local uri1 = mw.uri.new(ulx.url1.url)
  ulx.url1.host = uri1.host
  ulx.url1.extraurls = parseExtraArgs()

                                                          -- Nolink argument 

  local nolink = trimArg2(args.nolink)

  serviceName(frame, uri1.host, nolink)

                                                          -- Date argument

  local date = trimArg(args.date) or trimArg(args.date1)
  if date == "*" and ulx.url1.service == "wayback" then
    date = "index"
  elseif date and ulx.url1.service == "wayback" and verifydates == "yes" then 
    local ldf = dateFormat(date)
    if ldf then
      local udate = decodeWaybackDate( uri1.path, ldf )
      if udate ~= date then
        date = udate .. inlineRed("<sup>[日期不符]</sup>", "warning")       
      end
    end
  elseif date and ulx.url1.service == "webcite" and verifydates == "yes" then 
    local ldf = dateFormat(date)
    if ldf then
      local udate = decodeWebciteDate( uri1.path, ldf )
      if udate == "query" then -- skip
      elseif udate ~= date then
        date = udate .. inlineRed("<sup>[日期不符]</sup>", "warning")      
      end
    end
  elseif not date and ulx.url1.service == "wayback" then
    date = decodeWaybackDate( uri1.path, "iso" )
    if not date then 
      date = inlineRed("[日期錯誤] (1)", "error") 
    end
  elseif not date and ulx.url1.service == "webcite" then
    date = decodeWebciteDate( uri1.path, "iso" )
    if date == "query" then
      date = inlineRed("[缺少日期]", "warning")
    elseif not date then 
      date = inlineRed("[日期錯誤] (1)", "error")
    end
  elseif not date then
    date = inlineRed("[缺少日期]", "warning")
  end
  ulx.url1.date = date

                                                          -- Format argument 

  local format = trimArg(args.format)
  if not format then
    format = "none"
  else
    if format == "addlpages" then
      if not ulx.url1.date then
        format = "none"
      end
    elseif format == "addlarchives" then
      format = "addlarchives"
    else
      format = "none"
    end
  end
  ulx.url1.format = format

                                                          -- Title argument 

  local title = trimArg(args.title) or trimArg(args.title1)
  ulx.url1.title = title
  

  local rend = createRendering()
  if not rend then
    rend = '<span style="font-size:100%" class="error citation-comment">Error in [[:Template:'_.._tname_.._'|:Template:' .. tname .. ']]: Unknown problem. Please report on template talk page.</span>'
    track["Category:Webarchive模板错误"] = 1 
  end

  return rend .. createTracking()

end

return p