-- module to turn a parameter list into a list of [[Coxeter–Dynkin_diagram|Coxeter–Dynkin diagram]] images.
-- See the template documentation or any example for how it is used and works.
local p = {}
local origArgs

function p.CDD(frame)
	-- For calling from #invoke.
    if frame == mw.getCurrentFrame() then
        origArgs = frame:getParent().args
    else
        origArgs = frame
    end
	local pframe = frame:getParent()
	local args = pframe.args
	if (origArgs['FileType'] and origArgs['FileType']  ~= '') then
		filet=origArgs['FileType']
	else
		filet="png"
	end
	if (origArgs['CDDtype'] and origArgs['CDDtype'] ~= '') then
		cddt=origArgs['CDDtype'] .. "_"
	else
		cddt="CDel_"
	end
	if (origArgs['Size'] and origArgs['Size'] ~= '') then
		if (origArgs['Size'] ~= '') then
			cddSize=tonumber(origArgs['Size'])
		else
			cddSize=0
		end
	else
		cddSize=0
	end
	return p._CDD_(args,filet,cddt,cddSize)
end
	
function p._CDD(args)
	return p._CDD_(args,"png","CDel_",0)
end

function p._CDD_(args,ft,ct,dSize)
	-- For calling from other Lua modules.
	local body ='<span style="display:inline-block;">'         -- create and start the output string
	local filetype = ft
	local CDDtype = ct
	for v, x in ipairs(args) do                                -- process params, ignoring any names
		pgname="." .. filetype
		cpgname=CDDtype
        lasts = "|link=]]"
        if (dSize > 1) then
        	lasts = "|x" .. dSize .. "px|link=]]"
        end
		if (x ~= '') then					-- check for null/empty names
            d = tonumber(x)
            if (d ~= nil) then
                if (d > 20) then
                    for i = 1,string.len(x) do
                        tmpstr = string.sub(x,i,i)
                        if (tonumber(tmpstr) > 3) then
                            body = body .. "[[File:".. cpgname .. string.sub(x,i,i) .. pgname .. lasts
                        else
                            body = body .. "[[File:".. cpgname .. string.sub(x,i,i) .. "x" .. pgname .. lasts
                     	end
                 	end
             	else
                 	body = body .. "[[File:".. cpgname .. x  .. pgname .. lasts
                end
            else
             	body = body .. "[[File:".. cpgname .. x  .. pgname .. lasts
         	end
		end
	end
	body = body .. "</span>"                                   -- finish output string
	return body                                                -- return result
end

return p