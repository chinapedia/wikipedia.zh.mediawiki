local p = {}
 
function p.author(frame)
  
  local pframe = frame:getParent()
  local args = pframe.args
 
  local tname = "Gutenberg author"                                 -- name of calling template. Change if template is renamed.
 
  local id       = nil                                             -- author name, or number. Name goes to search page, number goes direct to author page 
  local name     = nil                                             -- display name on Wikipedia (default: article title)
  local url      = nil
  local tagline  = "at [[Project_Gutenberg|Project Gutenberg]]"
  local urlheadname  = "https://www.gutenberg.org/author/"          
  local urlheadnumb  = "https://www.gutenberg.org/ebooks/author/" 
  local urlhead  = nil

  -- Argument |id=
  id = trimArg(args[1]) or trimArg(args.id)
  if not id then
    error("Parameter id is missing. See [[Template:"_.._tname_.._"|Template:" .. tname .. "]] documentation")
  else
    if tonumber(id) then -- it's a number
      urlhead = urlheadnumb
    else
      urlhead = urlheadname
      id = mw.ustring.gsub(id," ", "+")
    end
  end 

  -- Argument |name=
  name = trimArg(args[2]) or trimArg(args.name)
  if not name then
    name = mw.title.getCurrentTitle().text:gsub('%s+%([^%(]-%)$', '') -- Current page name without the final parentheses
  end

  -- Argument |coda=
  if trimArg(args.coda) then
    tagline = tagline .. " " .. trimArg(args.coda)
  end

  url = "[" .. urlhead .. id .. " Works by " .. name .. "] " .. tagline

  return url

end

function p.Australia(frame)
  
  local pframe = frame:getParent()
  local args = pframe.args

  local tname = "Gutenberg Australia"                              -- name of calling template. Change if template is renamed.
 
  local id       = nil                                             -- ID. eg. http://gutenberg.net.au/plusfifty-n-z.html#shanks .. the ID = plusfifty-n-z.html#shanks
                                                                   -- ID is the same for linking an individual book title, or all books by the author.
  local name     = nil                                             -- display name on Wikipedia (default: article title)
  local author   = nil                                             -- flag if an author (default: no)
  local url      = nil
  local urlhead  = "http://gutenberg.net.au/"
  local prefix   = ""
  local tagline  = "at [[Project_Gutenberg_Australia|Project Gutenberg Australia]]"
  local italic   = "''"

  -- Argument |id=
  id = trimArg(args[1]) or trimArg(args.id)
  if not id then
    error("Parameter id is missing. See [[Template:"_.._tname_.._"|Template:" .. tname .. "]] documentation")
  end 

  -- Argument |name=
  name = trimArg(args[2]) or trimArg(args.name)
  if not name then
    name = mw.title.getCurrentTitle().text:gsub('%s+%([^%(]-%)$', '') -- Current page name without the final parentheses
  end

  -- Argument |author=
  author = trimArg(args.author)
  if author then
    if mw.ustring.lower(author) == "yes" then
      prefix = "Works by "
      italic = ""
    end
  end

  -- Argument |coda=
  if trimArg(args.coda) then
    tagline = tagline .. " " .. trimArg(args.coda)
  end

  url = "[" .. urlhead .. id .. " " .. prefix .. italic .. name .. italic .. "] " .. tagline

  return url

end

function p.Canada(frame)
  
  local pframe = frame:getParent()
  local args = pframe.args

  local tname = "FadedPage"                                        -- name of calling template. Change if template is renamed.
 
  local id       = nil                                             -- ID for author, eg. http://fadedpage.com/csearch.php?author=Shortt%2C%20Adam .. the id = Shortt, Adam
                                                                   -- ID for book titles, eg. http://fadedpage.com/showbook.php?pid=20160704 .. the id = 20160704
  local name     = nil                                             -- display name on Wikipedia (default: article title)
  local author   = nil                                             -- flag if an author (default: no)
  local url      = nil
  local urlhead  = "https://fadedpage.com/"
  local urlbook  = "showbook.php?pid="
  local urlauth  = "csearch.php?author="
  local prefix   = ""
  local tagline  = "at [[Distributed_Proofreaders_Canada|Faded Page]] (Canada)"
  local italic   = "''"

  -- Argument |id=
  id = trimArg(args[1]) or trimArg(args.id)
  if not id then
    error("Parameter id is missing. See [[Template:"_.._tname_.._"|Template:" .. tname .. "]] documentation")
  end 

  -- Argument |name=
  name = trimArg(args[2]) or trimArg(args.name)
  if not name then
    name = mw.title.getCurrentTitle().text:gsub('%s+%([^%(]-%)$', '') -- Current page name without the final parentheses
  end

  -- Argument |author=
  author = trimArg(args.author)
  if author then
    if mw.ustring.lower(author) == "yes" then
      id = mw.uri.encode( id, "PATH" )                                -- handle spaces within id argument string
      prefix = "Works by "
      italic = ""
      url = "[" .. urlhead .. urlauth .. id .. " " .. prefix .. italic .. name .. italic .. "] " .. tagline
      return url
    end
  end

  url = "[" .. urlhead .. urlbook .. id .. " " .. prefix .. italic .. name .. italic .. "] " .. tagline

  return url

end

function trimArg(arg)

  if arg == "" or arg == nil then
    return nil
  else
    return mw.text.trim(arg)
  end

end

return p