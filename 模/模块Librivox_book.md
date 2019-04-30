local p = {}

function p.book(frame)


  local pframe = frame:getParent()
  local args = pframe.args

  local tname = "Librivox book" -- name of calling template. Change if template rename.

  local title   = nil -- display and search title (default: article name w/out dab)
  local dtitle  = nil -- display title (default: title)
  local stitle  = nil -- search title (default: title)
  local lname   = nil -- last name
  local id      = nil -- unsupported argument
  local author  = nil -- author
  local tagline = "public domain audiobook at [[LibriVox|LibriVox]]"
  local urlhead = "https://librivox.org/search?"
  local italic   = "''"

  id = trimArg(args.id)
  if id then
    error("Error in Template:" .. tname .. " - id argument not supported - please see documentation at [[Template:Librivox_author|Template:Librivox author]]")
  end

  title = trimArg(args.title)
  if not title then
    title = mw.title.getCurrentTitle().text
  end
  dtitle = mw.ustring.gsub(title,'%s+%([^%(]-%)$', '')        -- Remove the final disambig paren
  stitle = dtitle

  if trimArg(args.stitle) then
    stitle = trimArg(args.stitle)
    if not trimArg(args.title) then                           -- For when used outside main article space
      dtitle = stitle
    end
  end
  if trimArg(args.dtitle) then
    dtitle = trimArg(args.dtitle)
    italic  = ""
  end

  local stitle = mw.ustring.gsub(stitle," ", "+")             -- replace "<space>" with "+"

  author = trimArg(args.author)
  if not author then
    lname = ""
  else
    --- Split name into words, count words, set name to last word
    local N = mw.text.split(author, " ")
    local l, count = mw.ustring.gsub(author, "%S+", "")
    lname = N[count]
  end

  local url = "[[File:Speaker_Icon.svg|15px]] " .. "[" .. urlhead .. "title=" .. stitle .. "&author=" .. lname .. "&reader=&keywords=&genre_id=0&status=all&project_type=either&recorded_language=&sort_order=catalog_date&search_page=1&search_form=advanced" .. " " .. italic .. dtitle .. italic .. "]" .. " " .. tagline

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