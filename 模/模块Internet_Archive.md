--[[ 

For functions related to Internet Archive

Notes: 

1. Internet Archive runs Lucene search engine 

2. Program flowchart:

   Break name down into number of words
     Build a base URL based on number of words (1,2,3,4,5+), use of sopt=t switch, and availability of birth-death dates
       If any words contain extended-ascii characters
         append extra code for wildcards based on sopt=t or tx         
   return finished URL

3. Lucene has a number of known issues to be aware of

   A. Names with accented letters (é) - aka extended ascii - are problematic. There are records on IA in which the accent has been
      dropped thus é is e in the record. Thus a search strategy has to use wildcards in place of extended ascii characters. The "?"
      wildcard does not work correctly on Lucene and thus recommend "*". Wildcards severely slow down search times and after about 
      5 or 8 wildcards it may even time out. Thus, only use wildcards in a single expression within a search string. The 
      function p.ia_deaccent will return é = e, so it's possible to search on an "anglicized" version of the name as well using wildcards. 
   B. Extended ascii doesn't work correctly if 1. not surrounded in quotes and 2. search string contains numbers and/or wildcards
      somewhere in it and 3. multiple () statements. The extended ascii character becomes interpreted as ascii eg. é -> Ã© 
      Try for example : (Évariste Régis Huc) OR (Évariste Régis Huc 1813-1860) OR (É. R. Huc) OR (É. R. Huc 1813-1860) OR (Évariste R. Huc) OR (Évariste R. Huc 1813-1860) OR (Évariste Huc) OR (Évariste Huc 1813-1860)
   C. B can be nullified by enclosing the string in quotes, but this creates a literal string and many permutations must be searched
      on ("John Smith" OR "Smith, John" etc). For names longer than 2 words it could exceed URL limits. URLs are limited to about 2000
      characters to account for most browsers (IE is 2083). Thus, strategies used are a balance between possibilities 
      and URL length.

   Update: As of 4 Nov 2015 Internet Archive is running Elasticsearch. Some of the bugs noted above are fixed. 

]]

local p = {}

--[[ 

For Template:Internet Archive author

]]
function p.author(frame)

  local pframe = frame:getParent()
  local args = pframe.args

  local tname = "Internet Archive author"                       -- name of calling template. Change if template rename.
  
  local name = nil                                              -- article name (default: current page name)
  dname = nil                                                   -- display name (default: current page name)
  local sname = nil                                             -- search name (default: current page name)
  local sopt = nil                                              -- search options (default: nil)
  byabout = "的作品或关于他的作品"
  tagline = "[[互联网档案馆|互联网档案馆]]中"
  urlhead = "//archive.org/search.php?query="
  mydate = ""                                                   -- birth-death date

  --- Determine name
  name = trimArg(args.name)                                     -- When using template outside main article space, the 'name' parameter is required (not optional)
  if not name then
    name = mw.title.getCurrentTitle().text
  end
  dname = mw.ustring.gsub(name,'%s+%([^%(]-%)$', '')            -- Remove the final disambig parentheses
  sname = dname
  if trimArg(args.sname) then                                       
    sname = trimArg(args.sname)
  end
  if trimArg(args.dname) then
    dname = trimArg(args.dname)
  end
 
  --- Determine search option
  sopt = trimArg(args.sopt)
  if sopt then
    sopt =  mw.ustring.lower(sopt)
    if sopt == "tight" then sopt = "t" end
    if sopt == "tightx" then sopt = "tx" end
    if sopt ~= "t" and sopt ~= "tx" then sopt = "unknown"  end
  end

  --- Determine tagline
  if trimArg(args.coda) then
    tagline = tagline .. " " .. trimArg(args.coda)
  end

  --- Custom search. Do early to avoid unnecessary processing. 
  if trimArg(args.search) then
    local search = p.ia_url_encode(trimArg(args.search))
    return tagline .. "[" .. urlhead .. search .. " " .. dname .. byabout .. "] "
  end

  -- Determine media string
  media = p.mediaTypes(args.media)
  if media == "" then
    mediaopen = "%28" -- added a default mediatype Dec 2015 see p.mediaTypes()
  else
    mediaopen = "%28"
  end

  -- Determine date of birth and death 
  local temp = mw.text.split(p.bdDate(args.birth, args.death, name), " ")
  local birth = temp[1]
  local death = temp[2]
  if birth == "Error" or death == "Error" then
    return "Error in [[:Template:"..tname.."|:Template:"..tname.."]]: [["_..name.._"|" ..name.. "]] doesn't exist."
  end

  --- Split sname into words and count words
  local N = mw.text.split(sname, " ")
  local l, count = mw.ustring.gsub(sname, "%S+", "")
  if count == 0 then
    return "Error in [[:Template:"..tname.."|:Template:"..tname.."]]: Zero-word name."
  end 

  --- Date string
  if birth ~= "none" and death ~= "none" then
    if p.ia_extendedascii(N[count]) == 1 then
      mydate = "%20OR%20%28%22"..birth.."-"..death.."%22%20AND%20%28%22"..p.urlX(N[count]).."%22%20OR%20"..p.urlX(p.ia_deaccent(N[count])).."%29%29"
    else
      mydate = "%20OR%20%28%22"..birth.."-"..death.."%22%20AND%20"..p.urlX(N[count]).."%29"
    end
  end
  

  --[[ 

      Format URL

  ]]

    if count == 1 then 

      myurl = p.oneWord(sname)

      if p.ia_extendedascii(sname) == 1 then

        if sopt == "tx" then
          return p.IArender("normal")
        end
 
        if sopt == "t" then
          local plainname = p.ia_deaccent(sname)       
          local A1 = "%20OR%20%22"..p.urlX(plainname)
          myurl = myurl .. A1 .. "%22"
          return p.IArender("normal")
        end

        if p.wildcrazycheck(N, count) == 1 then
          myurl = p.wildcrazyfix(N, count)
          return p.IArender("normal")
        end

        wild = "%20OR%20" .. p.ia_url_encode(p.ia_extendedascii2wildcard(sname))
        return p.IArender("wild")

      else 
        return p.IArender("normal")
      end
    end

    if count == 2 then
 
      myurl = p.twoWords(N, sopt)

      if p.ia_extendedascii(sname) == 1 then

        if sopt == "tx" then
          return p.IArender("normal")
        end

        if sopt == "t" then
          local plainname = p.ia_deaccent(sname)
          local PN = mw.text.split(plainname, " ") 
          -- Last, First
          local A1 = "%20OR%20%22"..p.urlX(PN[2]).."%2C%20"..p.urlX(PN[1])
          -- First Last
          local A2 = "%22%20OR%20%22"..p.urlX(PN[1]).."%20"..p.urlX(PN[2])
          myurl = myurl .. A1 .. A2 .. "%22"
          return p.IArender("normal")
        end

        if p.wildcrazycheck(N, count) == 1 then
          myurl = p.wildcrazyfix(N, count)
          return p.IArender("normal")
        end
 
        wild = "%20OR%20" .. p.ia_url_encode(p.ia_extendedascii2wildcard(sname)) 
        return p.IArender("wild")
        
      end

      return p.IArender("normal")

    end

    if count == 3 then

      myurl = p.threeWords(N, sopt)

      if p.ia_extendedascii(sname) == 1 then

        if sopt == "tx" then
          return p.IArender("normal")
        end

        if sopt == "t" then
          local plainname = p.ia_deaccent(sname)
          local PN = mw.text.split(plainname, " ") 
          local FIRST  = p.urlX(PN[1])
          local MIDDLE = p.urlX(PN[2])
          local LAST   = p.urlX(PN[3])
          local firstinitialp  = p.urlX( p.firstLetter(PN[1]) )
          local middleinitialp  = p.urlX( p.firstLetter(PN[2]) )
          -- First Middle Last
          local A1 = "%20OR%20%22"..FIRST.."%20"..MIDDLE.."%20"..LAST
          -- Last, First Middle
          local A2 = "%22%20OR%20%22"..LAST.."%2C%20"..FIRST.."%20"..MIDDLE
          -- Last, First M.
          local A3 = "%22%20OR%20%22"..LAST.."%2C%20"..FIRST.."%20"..middleinitialp.."%2E"
          -- Last, F. M.
          local A4 = "%22%20OR%20%22"..LAST.."%2C%20"..firstinitialp..".%20"..middleinitialp.."%2E"
          local ALL = A1 .. A2 .. A3 .. A4 .. "%22"
          myurl = myurl .. ALL
          return p.IArender("normal")
        end

        if p.wildcrazycheck(N, count) == 1 then
          myurl = p.wildcrazyfix(N, count)
          return p.IArender("normal")
        end

        wild = "%20OR%20" .. p.ia_url_encode(p.ia_extendedascii2wildcard(sname)) 
        return p.IArender("wild")

      end

      return p.IArender("normal")

    end

    if count == 4 then

      myurl = p.fourWords(N, sopt)
 
      if p.ia_extendedascii(sname) == 1 then

        if sopt == "tx" then
          return p.IArender("normal")
        end

        if sopt == "t" then
          local plainname = p.ia_deaccent(sname)
          local PN = mw.text.split(plainname, " ") 
          local FIRST  = p.urlX(PN[1])
          local SECOND = p.urlX(PN[2])
          local THIRD  = p.urlX(PN[3])
          local LAST   = p.urlX(PN[4])
          local firstinitialp  = p.urlX( p.firstLetter(PN[1]) )
          local secondinitialp  = p.urlX( p.firstLetter(PN[2]) )
          local thirdinitialp  = p.urlX( p.firstLetter(PN[3]) )
          -- Last, First Second Third
          local A1 = "%20OR%20%22"..LAST.."%2C%20"..FIRST.."%20"..SECOND.."%20"..THIRD
          -- First Second Third Last
          local A2 = "%22%20OR%20%22"..FIRST.."%20"..SECOND.."%20"..THIRD.."%20"..LAST
          -- Last, F. S. T.
          local A3 = "%22%20OR%20%22"..LAST.."%2C%20"..firstinitialp.."%2E%20"..secondinitialp.."%2E%20"..thirdinitialp.."%2E"
          local ALL = A1 .. A2 .. A3 .. "%22"
          myurl = myurl .. ALL 
          return p.IArender("normal")
        end 
       
        if p.wildcrazycheck(N, count) == 1 then
          myurl = p.wildcrazyfix(N, count)
          return p.IArender("normal")
        end

        wild = "%20OR%20" .. p.ia_url_encode(p.ia_extendedascii2wildcard(sname))
        return p.IArender("wild")     
      end

      return p.IArender("normal")

    end

    if count > 4 then

      myurl = "%28" .. p.ia_url_encode(sname) 

      if p.ia_extendedascii(sname) == 1 then
 
        if sopt == "tx" then
          return p.IArender("normal")
        end
 
        if sopt == "t" then
          local plainname = p.ia_deaccent(sname)       
          local A1 = "%29%20OR%20%28"..p.ia_url_encode(plainname)
          myurl = myurl .. A1 
          return p.IArender("normal")
        end
 
        if p.wildcrazycheck(N, count) == 1 then
          myurl = p.wildcrazyfix(N, count)
          return p.IArender("normal")
        end
 
        wild = "%29%20OR%20%28" .. p.ia_url_encode(p.ia_extendedascii2wildcard(sname))
        return p.IArender("wild")
 
      else 
        return p.IArender("normal")
      end

    end

  return "Unknown error (1). Please check documentation for [[Template:"..tname.."|Template:"..tname.."]]"

end

-- Build final output and render
function p.IArender(type) 

   if type == "normal" then
     return tagline .. "[" .. urlhead .. mediaopen .. myurl .. "%29" .. mydate .. media .. " " .. dname .. byabout .. "] "
   end 

   if type == "wild" then
     return tagline .. "[" .. urlhead .. mediaopen .. myurl .. wild .. "%29" .. mydate .. media .. " " .. dname .. byabout .. "] "
   end

end

-- Lucene returns too many false positives if first or last character in a word is "*" wildcard ie. accented letter
--  Build special search in these cases. 
function p.wildcrazyfix(N, count)

  --- Split along "-" and use only first word ie. John-Taylor-Smith becomes John
  local NF = mw.text.split(N[1], "-")
  local NL = mw.text.split(N[count], "-")

  -- ..but use full name for 1-word names
  if count == 1 then
    NF[1] = N[1]
    NL[1] = N[1]
  end
  
  -- ((Fïrst OR First) AND (Lást OR Last))
  return "%28%28%22" .. NF[1] .. "%22%20OR%20" .. p.ia_deaccent(NF[1]) .. "%29%20AND%20%28%22" .. NL[1] .. "%22%20OR%20" .. p.ia_deaccent(NL[1]) .. "%29"

end

-- Return 1 if the first or last character in any word within name N is extended ascii
function p.wildcrazycheck(N, count)
  
  local i = 0
  
  while i < count do
    i = i + 1
    local firstl = N[i]:byte(1)
    local lastl  = N[i]:byte(N[i]:len())
    if (firstl < 32 or firstl > 126) then return 1 end
    if (lastl < 32 or lastl > 126) then return 1  end
  end

  return 0
end

function p.oneWord(sname)

      local nameurl = p.ia_url_encode(sname)
      local A1 = "%28subject%3A%22"..nameurl
      local A2 = "%22%20OR%20creator%3A%22"..nameurl
      local A3 = "%22%20OR%20description%3A%22"..nameurl
      local A4 = "%22%20OR%20title%3A%22"..nameurl
      return A1 .. A2 .. A3 .. A4 .. "%22"
end

function p.twoWords(N, sopt)
      local FIRST  = p.urlX(N[1])
      local LAST   = p.urlX(N[2])
      local firstinitial  = p.urlX( p.firstLetter(N[1]) )

      -- Last, First
      local S1 = "%28subject%3A%22"..LAST.."%2C%20"..FIRST
      -- First Last
      local S2 = "%22%20OR%20subject%3A%22"..FIRST.."%20"..LAST
      local SALL = S1..S2
      -- Last, First
      local C1 = "%22%20OR%20creator%3A%22"..LAST.."%2C%20"..FIRST
      -- First Last
      local C2 = "%22%20OR%20creator%3A%22"..FIRST.."%20"..LAST
      local CALL = C1..C2
      -- First Last
      local T1 = "%22%20OR%20title%3A%22"..FIRST.."%20"..LAST
      local TALL = T1
      -- Last, First
      local D1 = "%22%20OR%20description%3A%22"..LAST.."%2C%20"..FIRST
      -- First Last
      local D2 = "%22%20OR%20description%3A%22"..FIRST.."%20"..LAST
      local DALL = D1..D2

      if sopt == "t" or sopt == "tx" then
        return SALL .. CALL .. TALL .. DALL .. "%22"
      else
        -- Last, F.
        local C3 = "%22%20OR%20creator%3A%22"..LAST.."%2C%20"..firstinitial.."%2E"
        local CALL = CALL..C3
        return SALL .. CALL .. TALL .. DALL .. "%22"
      end

end

function p.threeWords(N, sopt)
      -- CAUTION: The following is near the max 2000 character URL limit for most browsers when using long names 
      --          such as "René-Nicolas Dufriche Desgenettes". 

      local FIRST  = p.urlX(N[1])
      local MIDDLE = p.urlX(N[2])
      local LAST   = p.urlX(N[3])
      local firstinitial  = p.urlX( p.firstLetter(N[1]) )
      local middleinitial = p.urlX( p.firstLetter(N[2]) )

      -- Last, First Middle
      local S1 = "%28subject%3A%22"..LAST.."%2C%20"..FIRST.."%20"..MIDDLE
      -- Last, First M.
      local S2 = "%22%20OR%20subject%3A%22"..LAST.."%2C%20"..FIRST.."%20"..middleinitial.."%2E"
      -- Last, F. M.
      local S3 = "%22%20OR%20subject%3A%22"..LAST.."%2C%20"..firstinitial.."%2E%20"..middleinitial.."%2E"
      -- First Middle Last
      local S4 = "%22%20OR%20subject%3A%22"..FIRST.."%20"..MIDDLE.."%20"..LAST
      -- First M. Last
      local S5 = "%22%20OR%20subject%3A%22"..FIRST.."%20"..middleinitial.."%2E%20"..LAST
      -- F. M. Last
      local S6 = "%22%20OR%20subject%3A%22"..firstinitial.."%2E%20"..middleinitial.."%2E%20"..LAST
      local SALL = S1..S2..S3..S4..S5..S6
      -- First Middle Last
      local C1 = "%22%20OR%20creator%3A%22"..FIRST.."%20"..MIDDLE.."%20"..LAST
      -- First M. Last
      local C2 = "%22%20OR%20creator%3A%22"..FIRST.."%20"..middleinitial.."%2E%20"..LAST
      -- F. M. Last
      local C3 = "%22%20OR%20creator%3A%22"..firstinitial.."%2E%20"..middleinitial.."%2E%20"..LAST
      -- F. Middle Last
      local C4 = "%22%20OR%20creator%3A%22"..firstinitial.."%2E%20"..MIDDLE.."%20"..LAST
      -- Last, First Middle
      local C5 = "%22%20OR%20creator%3A%22"..LAST.."%2C%20"..FIRST.."%20"..MIDDLE
      -- Last, First M.
      local C6 = "%22%20OR%20creator%3A%22"..LAST.."%2C%20"..FIRST.."%20"..middleinitial.."%2E"
      -- Last, F. M.
      local C7 = "%22%20OR%20creator%3A%22"..LAST.."%2C%20"..firstinitial.."%2E%20"..middleinitial.."%2E"
      -- Last, F. M.
      local C8 = "%22%20OR%20creator%3A%22"..LAST.."%2C%20"..firstinitial.."%2E%20"..MIDDLE
      local CALL = C1..C2..C3..C4..C5..C6..C7..C8
      -- First Middle Last
      local T1 = "%22%20OR%20title%3A%22"..FIRST.."%20"..MIDDLE.."%20"..LAST
      -- First M. Last
      local T2 = "%22%20OR%20title%3A%22"..FIRST.."%20"..middleinitial.."%2E%20"..LAST
      -- F. M. Last
      local T3 = "%22%20OR%20title%3A%22"..firstinitial.."%2E%20"..middleinitial.."%2E%20"..LAST
      local TALL = T1..T2..T3
      -- First Middle Last
      local D1 = "%22%20OR%20description%3A%22"..FIRST.."%20"..MIDDLE.."%20"..LAST
      -- First M. Last
      local D2 = "%22%20OR%20description%3A%22"..FIRST.."%20"..middleinitial.."%2E%20"..LAST
      -- F. M. Last
      local D3 = "%22%20OR%20description%3A%22"..firstinitial.."%2E%20"..middleinitial.."%2E%20"..LAST
      -- Last, First Middle
      local D4 = "%22%20OR%20description%3A%22"..LAST.."%2C%20"..FIRST.."%20"..MIDDLE
      -- Last, First M.
      local D5 = "%22%20OR%20description%3A%22"..LAST.."%2C%20"..FIRST.."%20"..middleinitial.."%2E"
      local DALL = D1..D2..D3..D4..D5

      if sopt == "t" or sopt == "tx" then
        return SALL .. CALL .. TALL .. DALL .. "%22"
      else
        -- Last, First
        local S7 = "%22%20OR%20subject%3A%22"..LAST.."%2C%20"..FIRST
        -- First Last
        local S8 = "%22%20OR%20subject%3A%22"..FIRST.."%20"..LAST
        local SALL = SALL..S7..S8
        -- First Last
        local C9 = "%22%20OR%20creator%3A%22"..FIRST.."%20"..LAST
        -- Last, First
        local C10 = "%22%20OR%20creator%3A%22"..LAST.."%2C%20"..FIRST
        local CALL = CALL..C9..C10
        -- First Last
        local T4 = "%22%20OR%20title%3A%22"..FIRST.."%20"..LAST
        local TALL = TALL..T4
        -- First Last
        local D6 = "%22%20OR%20description%3A%22"..FIRST.."%20"..LAST
        -- Last, First
        local D7 = "%22%20OR%20description%3A%22"..LAST.."%2C%20"..FIRST
        local DALL = DALL..D6..D7

        return SALL .. CALL .. TALL .. DALL .. "%22"
      end
end

function p.fourWords(N, sopt)

      local FIRST  = p.urlX(N[1])
      local SECOND = p.urlX(N[2])
      local THIRD  = p.urlX(N[3])
      local LAST   = p.urlX(N[4])

      local firstinitial  = p.firstLetter(N[1])
      local secondinitial  = p.firstLetter(N[2])
      local thirdinitial = p.firstLetter(N[3])

      if sopt == "t" or sopt == "tx" then
        -- Last, First Second Third
        local S1 = "%28subject%3A%22"..LAST.."%2C%20"..FIRST.."%20"..SECOND.."%20"..THIRD
        -- First Second Third Last
        local S2 = "%22%20OR%20subject%3A%22"..FIRST.."%20"..SECOND.."%20"..THIRD.."%20"..LAST
        -- Last, First Second Third
        local C1 = "%22%20OR%20creator%3A%22"..LAST.."%2C%20"..FIRST.."%20"..SECOND.."%20"..THIRD
        -- First Second Third Last
        local C2 = "%22%20OR%20creator%3A%22"..FIRST.."%20"..SECOND.."%20"..THIRD.."%20"..LAST
        -- First Second Third Last
        local T1 = "%22%20OR%20title%3A%22"..FIRST.."%20"..SECOND.."%20"..THIRD.."%20"..LAST
        -- First Second Third Last
        local D1 = "%22%20OR%20description%3A%22"..FIRST.."%20"..SECOND.."%20"..THIRD.."%20"..LAST

        return S1..S2..C1..C2..T1..D1.."%22"
      end

      -- Last, First Second Third
      local S1 = "%28subject%3A%22"..LAST.."%2C%20"..FIRST.."%20"..SECOND.."%20"..THIRD
      -- First Second Third Last
      local S2 = "%22%20OR%20subject%3A%22"..FIRST.."%20"..SECOND.."%20"..THIRD.."%20"..LAST
      -- Last, First Second Third
      local C1 = "%22%20OR%20creator%3A%22"..LAST.."%2C%20"..FIRST.."%20"..SECOND.."%20"..THIRD
      -- First Second Third Last
      local C2 = "%22%20OR%20creator%3A%22"..FIRST.."%20"..SECOND.."%20"..THIRD.."%20"..LAST
      -- Last, F. S. T.
      local C3 = "%22%20OR%20creator%3A%22"..LAST.."%2C%20"..firstinitial.."%2E%20"..secondinitial.."%2E%20"..thirdinitial.."%2E"
      -- First Second Third Last
      local T1 = "%22%20OR%20title%3A%22"..FIRST.."%20"..SECOND.."%20"..THIRD.."%20"..LAST
      -- First Second Third Last
      local D1 = "%22%20OR%20description%3A%22"..FIRST.."%20"..SECOND.."%20"..THIRD.."%20"..LAST

      return S1..S2..C1..C2..C3..T1..D1.."%22"

end

function trimArg(arg)
  if arg == "" or arg == nil then
    return nil
  else
    return mw.text.trim(arg)
  end
end

function p.mediaTypes(argsmedia)

  -- Added a default mediatype Dec 2015 due to too many false positives in the software mediatype, caused by birth-death dates catching numbers in source codes
  local media = "-mediatype:software"

  if argsmedia ~="" and argsmedia ~=nil then
    local medialist = mw.text.split(mw.text.trim(argsmedia), " ")
    local al, acount = mw.ustring.gsub(mw.text.trim(argsmedia), "%S+", "")
    local i = 0
    repeat -- the following could be condensed but repetitive for clarity 
      i = i + 1
      if(mw.ustring.lower(medialist[i]) == "text" or mw.ustring.lower(medialist[i]) == "texts") then
        media = media .. p.ia_url_encode(" OR mediatype:texts")         
      end
      if(mw.ustring.lower(medialist[i]) == "audio") then
        media = media .. p.ia_url_encode(" OR mediatype:audio")
      end
      if(mw.ustring.lower(medialist[i]) == "video") then
        media = media .. p.ia_url_encode(" OR mediatype:video")
      end
    until i == acount
  end

  media = "%29%20AND%20%28" .. media .. "%29"
  -- media = media .. "%29%20AND%20%28"

  return media

end

-- Alt way to get b/d dates via getContent()
function p.bdDateAlt(argsbirth, argsdeath, name)

    local pagetext = nil
    local birth = "none"
    local death = "none"

    -- Load the page
    local t = mw.title.new(name)
    if(t.exists) then
      pagetext = t:getContent()
    end
    if pagetext == nil then 
      return "Error"     
    end
 
    -- Remove false positives
    pagetext = mw.ustring.gsub( mw.ustring.gsub(pagetext, "<!--.--->", ""), "<nowiki>.-</nowiki>", "")
 
    -- "Category:1900 births" 
    if argsbirth == "" or argsbirth == nil then
      local birthcheck = mw.ustring.match(pagetext, "%[%[%s-[Cc]ategory:%s-%d+%.?%d*%s-births%s-%]%]" )
      if birthcheck ~= nil then
        birth = mw.ustring.match(birthcheck, "%d+%.?%d*")
      else
        birth = "none"
      end
    else
      birth = mw.text.trim(argsbirth)
    end

    -- "Category:2000 deaths" 
    if argsdeath == "" or argsdeath == nil then
      local deathcheck = mw.ustring.match(pagetext, "%[%[%s-[Cc]ategory:%s-%d+%.?%d*%s-deaths%s-%]%]" )
      if deathcheck ~= nil then
        death = mw.ustring.match(deathcheck, "%d+%.?%d*")
      else
        death = "none"
      end
    else
      death = mw.text.trim(argsdeath)
    end

    return birth .. " " .. death

end

-- Get b/d dates via Wikidata.
-- ‎ 
function p.bdDate(argsbirth, argsdeath, name)

  local pagetext = nil
  local birth = "none"
  local death = "none"

  
  entity = mw.wikibase.getEntityObject()
  if not entity or not entity.claims then 
    -- Alternative if template not on a page in mainspace. This is needed since Wikidata can only be retrieved
    -- for the article where the template is located.
    return p.bdDateAlt(argsbirth, argsdeath, name)
  end

  -- Note: The below uses formatPropertyValues() to get and format the date from Wikidata.
  --       For an alternative method, see sandbox revision dated 5:58 am, 15 October 2014
  if argsbirth == "" or argsbirth == nil then
    local birthtable = entity:formatPropertyValues( 'P569' )
    local birthsplit = mw.text.split(birthtable["value"], " ")
    local l, count = mw.ustring.gsub(birthtable["value"], "%S+", "")
    if count > 0 then
      if string.find(birthsplit[count], "^%d") then
        birth = birthsplit[count]
      elseif string.find(birthsplit[count], "BCE") then
        birth = birthsplit[count - 1]
      elseif string.find(birthsplit[count], "BC") then
        birth = birthsplit[count - 1]
      elseif string.find(birthsplit[count], "AD") then
        birth = birthsplit[count - 1]
      end
    end
  else
    birth = mw.text.trim(argsbirth)
  end

  if argsdeath == "" or argsdeath == nil then
    local deathtable = entity:formatPropertyValues( 'P570' )
    local deathsplit = mw.text.split(deathtable["value"], " ")
    local l, count = mw.ustring.gsub(deathtable["value"], "%S+", "")
    if count > 0 then
      if string.find(deathsplit[count], "^%d") then
        death = deathsplit[count]
      elseif string.find(deathsplit[count], "BCE") then
        death = deathsplit[count - 1]
      elseif string.find(deathsplit[count], "BC") then
        death = deathsplit[count - 1]
      elseif string.find(deathsplit[count], "AD") then
        death = deathsplit[count - 1]
      end
    end
  else
    death = mw.text.trim(argsdeath)
  end

  if birth == "none" and death == "none" then 
    -- Alternative if Wikidata is missing data
    -- return p.bdDateAlt(name)
    return birth .. " " .. death
  else
    return birth .. " " .. death
  end

end

--- URL-encode special characters
--- Note: this function was added later to deal with "&" characters instead of using p.ia_url_encode since 
---       that may break existing instances of the template.
function p.urlX(str)
  if (str) then
    str = mw.ustring.gsub (str, "&", "%%26")
  end
  return str
end

--- URL-encode a string
--- http://lua-users.org/wiki/StringRecipes
---
function p.ia_url_encode(str)
  if (str) then
    str = mw.ustring.gsub (str, "\n", "\r\n")
    str = mw.ustring.gsub (str, "([^%w %-%_%.%~])",
        function (c) return mw.ustring.format ("%%%02X", string.byte(c)) end)
    str = mw.ustring.gsub (str, " ", "+")
  end
  return str	
end

-- Does str contain extended ascii? 1 = yes
function p.ia_extendedascii(str)
    for i = 1, str:len() do
      if (str:byte(i) >= 32 and str:byte(i) <= 126) and str:byte(i) ~= 39 then -- 39 = '
        --do nothing
      else
        return 1
      end
    end
    return 0
end

-- UTF-8 aware replacement for string.sub() which doesn't support UTF-8.
-- Note: Using instead of mw.ustring.sub() which I suspect(?) might be cause of intermittent error, and faster here for first-letter job.
-- Source: prapin @ Stack Overflow http://stackoverflow.com/questions/13235091/extract-the-first-letter-of-a-utf-8-string-with-lua
function p.firstLetter(str)
  return str:match("[%z\1-\127\194-\244][\128-\191]*")
end


-- Replace all extended ascii characters with wildcard '*'
function p.ia_extendedascii2wildcard(str)
    local s = ""
    local j = 0
    local k = 0    
    for i = 1, str:len() do
      k = str:byte(i)
      if k >= 32 and k <= 126 then
-- For list of Lucene special characters needing to be escaped: 
-- http://lucene.apache.org/core/4_10_0/queryparser/org/apache/lucene/queryparser/classic/package-summary.html#Escaping_Special_Characters
-- We only worry about - (45) and " (34) since the others are unlikely to appear in a proper name.
-- Also ' (39) since it is sometimes the extended character ’
        if k == 45 or k == 34 or k == 39 then 
          s = s .. "*" 
        else
          s = s .. str:sub(i,i)
        end
      else
        if j == 1 then
          s = s .. "*"
          j = 2
        end
        if j == 0 then j = 1 end
        if j == 2 then j = 0 end
      end
    end
    return s
end

-- Replace accented letters with non-accented equivalent letters
-- Note: this is not a complete list of all possible accented letters. Rather it is 
--       all of the accented letters found in the first 10,000 names which are using 
--       the Internet Archive author template.
function p.ia_deaccent(str)
    local s = str

    s = mw.ustring.gsub(s, "á", "a")
    s = mw.ustring.gsub(s, "a︡", "a")
    s = mw.ustring.gsub(s, "Á", "A")
    s = mw.ustring.gsub(s, "ă", "a")
    s = mw.ustring.gsub(s, "â", "a")
    s = mw.ustring.gsub(s, "æ", "ae")
    s = mw.ustring.gsub(s, "Æ", "AE")
    s = mw.ustring.gsub(s, "à", "a")
    s = mw.ustring.gsub(s, "ā", "a")
    s = mw.ustring.gsub(s, "Ā", "A")
    s = mw.ustring.gsub(s, "ą", "a")
    s = mw.ustring.gsub(s, "å", "a")
    s = mw.ustring.gsub(s, "Å", "A")
    s = mw.ustring.gsub(s, "ã", "a")
    s = mw.ustring.gsub(s, "ä", "a")
    s = mw.ustring.gsub(s, "Ä", "A")
    s = mw.ustring.gsub(s, "β", "B")
    s = mw.ustring.gsub(s, "ć", "c")
    s = mw.ustring.gsub(s, "č", "c")
    s = mw.ustring.gsub(s, "Č", "C")
    s = mw.ustring.gsub(s, "ç", "c")
    s = mw.ustring.gsub(s, "Ç", "C")
    s = mw.ustring.gsub(s, "ĉ", "c")
    s = mw.ustring.gsub(s, "ď", "d")
    s = mw.ustring.gsub(s, "đ", "d")
    s = mw.ustring.gsub(s, "é", "e")
    s = mw.ustring.gsub(s, "É", "E")
    s = mw.ustring.gsub(s, "ě", "e")
    s = mw.ustring.gsub(s, "ê", "e")
    s = mw.ustring.gsub(s, "è", "e")
    s = mw.ustring.gsub(s, "È", "E")
    s = mw.ustring.gsub(s, "ε", "e")
    s = mw.ustring.gsub(s, "ē", "e")
    s = mw.ustring.gsub(s, "Ē", "E")
    s = mw.ustring.gsub(s, "ę", "e")
    s = mw.ustring.gsub(s, "ð", "e")
    s = mw.ustring.gsub(s, "ë", "e")
    s = mw.ustring.gsub(s, "Ë", "E")
    s = mw.ustring.gsub(s, "γ", "Y")
    s = mw.ustring.gsub(s, "ħ", "h")
    s = mw.ustring.gsub(s, "i︠a︡", "ia")
    s = mw.ustring.gsub(s, "í", "i")
    s = mw.ustring.gsub(s, "i︠", "i")
    s = mw.ustring.gsub(s, "ĭ", "i")
    s = mw.ustring.gsub(s, "Í", "I")
    s = mw.ustring.gsub(s, "î", "i")
    s = mw.ustring.gsub(s, "Î", "I")
    s = mw.ustring.gsub(s, "ì", "i")
    s = mw.ustring.gsub(s, "ī", "i")
    s = mw.ustring.gsub(s, "ł", "i")
    s = mw.ustring.gsub(s, "ï", "i")
    s = mw.ustring.gsub(s, "Ï", "I")
    s = mw.ustring.gsub(s, "ĺ", "I")
    s = mw.ustring.gsub(s, "Ĺ", "L")
    s = mw.ustring.gsub(s, "μ", "u")
    s = mw.ustring.gsub(s, "µ", "u")
    s = mw.ustring.gsub(s, "ń", "n")
    s = mw.ustring.gsub(s, "ň", "n")
    s = mw.ustring.gsub(s, "ņ", "n")
    s = mw.ustring.gsub(s, "ñ", "n")
    s = mw.ustring.gsub(s, "Ñ", "N")
    s = mw.ustring.gsub(s, "ó", "o")
    s = mw.ustring.gsub(s, "Ó", "O")
    s = mw.ustring.gsub(s, "ô", "o")
    s = mw.ustring.gsub(s, "œ", "oe")
    s = mw.ustring.gsub(s, "ò", "o")
    s = mw.ustring.gsub(s, "ō", "o")
    s = mw.ustring.gsub(s, "ø", "o")
    s = mw.ustring.gsub(s, "Ø", "o")
    s = mw.ustring.gsub(s, "õ", "o")
    s = mw.ustring.gsub(s, "ö", "o")
    s = mw.ustring.gsub(s, "ő", "o")
    s = mw.ustring.gsub(s, "Ö", "O")
    s = mw.ustring.gsub(s, "φ", "o")
    s = mw.ustring.gsub(s, "ŕ", "r")
    s = mw.ustring.gsub(s, "ř", "r")
    s = mw.ustring.gsub(s, "Ř", "R")
    s = mw.ustring.gsub(s, "ś", "s")
    s = mw.ustring.gsub(s, "Ś", "S")
    s = mw.ustring.gsub(s, "š", "s")
    s = mw.ustring.gsub(s, "ṣ", "s")
    s = mw.ustring.gsub(s, "Š", "S")
    s = mw.ustring.gsub(s, "ş", "s")
    s = mw.ustring.gsub(s, "Ş", "S")
    s = mw.ustring.gsub(s, "ŝ", "s")
    s = mw.ustring.gsub(s, "σ", "s")
    s = mw.ustring.gsub(s, "ť", "t")
    s = mw.ustring.gsub(s, "ţ", "t")
    s = mw.ustring.gsub(s, "τ", "t")
    s = mw.ustring.gsub(s, "þ", "p")
    s = mw.ustring.gsub(s, "Þ", "p")
    s = mw.ustring.gsub(s, "ú", "u")
    s = mw.ustring.gsub(s, "Ú", "U")
    s = mw.ustring.gsub(s, "û", "u")
    s = mw.ustring.gsub(s, "ù", "u")
    s = mw.ustring.gsub(s, "ū", "u")
    s = mw.ustring.gsub(s, "ů", "u")
    s = mw.ustring.gsub(s, "ü", "u")
    s = mw.ustring.gsub(s, "Ü", "U")
    s = mw.ustring.gsub(s, "ŵ", "w")
    s = mw.ustring.gsub(s, "ý", "y")
    s = mw.ustring.gsub(s, "ŷ", "y")
    s = mw.ustring.gsub(s, "¥", "y")
    s = mw.ustring.gsub(s, "ÿ", "y")
    s = mw.ustring.gsub(s, "Ÿ", "Y")
    s = mw.ustring.gsub(s, "ź", "z")
    s = mw.ustring.gsub(s, "Ž", "Z")
    s = mw.ustring.gsub(s, "ž", "z")
    s = mw.ustring.gsub(s, "ż", "z")
    s = mw.ustring.gsub(s, "Ż", "Z")

    return s

end

return p