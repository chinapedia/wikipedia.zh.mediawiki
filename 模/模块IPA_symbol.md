local p, __output, args, data = {}, {}, {}, mw.loadData("Module:IPA symbol/data")
local id, output

__output.name = function() return data.correspondences[id]["name"] end
__output.wikipage = function() return data.correspondences[id]["wikipage"] end
__output.soundfile = function() return data.correspondences[id]["soundfile"] end
__output.type = function() return data.correspondences[id]["type"] end

local function html_error(message)
  if args[2] then
    return args[2]
  else
    return mw.ustring.format(
      '<strong class="error">错误使用{{[[Template:IPAsym|IPAsym]]}}：%s%s</strong>'
      ,message
      ,mw.title.getCurrentTitle().isContentPage and ("[[Category:需要注意的国际音标页面|" .. (args[1] or "") .. "]]") or ""
     )
  end
end

function p.main(frame)
  -- all input is trimmed; accepted parameters are:
  --   name              description
  --   ====              ===========
  --   (1)               the input
  --   (2)               overwrite the error message
  --   (3)               overwrite the output when input is empty
  --   output            the output, one of: input; name; wikipage; soundfile; type

  for k, v in pairs(frame:getParent().args) do
    args[k] = v and mw.text.trim(v)
  end
  args.output = args.output or 'wikipage'

  if not args[1] or args[1] == "" then return args[3] or "" end

  id = data.symbols[args[1]]
  if not id then return html_error('“' .. args[1] .. '”在列表中找不到') end

  return  __output[args.output] and __output[args.output]() or html_error("没有这样的输出选项")
end

return p