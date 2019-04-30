local getArgs = require('Module:Arguments').getArgs
local p = {} -- module's table

local am = {}  -- Elements with wiki links
am.H="[[氢|H]]";am.He="[[氦|He]]";
am.Li="[[锂|Li]]";am.Be="[[铍|Be]]";am.B="[[硼|B]]";am.C="[[碳|C]]";am.N="[[氮|N]]";am.O="[[氧|O]]";am.F="[[氟|F]]";am.Ne="[[氖|Ne]]";
am.Na="[[钠|Na]]";am.Mg="[[镁|Mg]]";am.Al="[[铝|Al]]";am.Si="[[硅|Si]]";am.P="[[磷|P]]";am.S="[[硫|S]]";am.Cl="[[氯|Cl]]";am.Ar="[[氩|Ar]]";
am.K="[[钾|K]]";am.Ca="[[钙|Ca]]";am.Sc="[[钪|Sc]]";am.Ti="[[钛|Ti]]";am.V="[[钒|V]]";am.Cr="[[铬|Cr]]";am.Mn="[[锰|Mn]]";am.Fe="[[铁|Fe]]";am.Co="[[钴|Co]]";am.Ni="[[镍|Ni]]";am.Cu="[[铜|Cu]]";am.Zn="[[锌|Zn]]";am.Ga="[[镓|Ga]]";am.Ge="[[锗|Ge]]";am.As="[[砷|As]]";am.Se="[[硒|Se]]";am.Br="[[溴|Br]]";am.Kr="[[氪|Kr]]";am.Rb="[[铷|Rb]]";
am.Sr="[[锶|Sr]]";am.Y="[[钇|Y]]";am.Zr="[[锆|Zr]]";am.Nb="[[铌|Nb]]";am.Mo="[[钼|Mo]]";am.Tc="[[锝|Tc]]";am.Ru="[[钌|Ru]]";am.Rh="[[铑|Rh]]";am.Pd="[[钯|Pd]]";am.Ag="[[銀|Ag]]";am.Cd="[[镉|Cd]]";am.In="[[铟|In]]";am.Sn="[[锡|Sn]]";am.Sb="[[锑|Sb]]";am.Te="[[碲|Te]]";am.I="[[碘|I]]";am.Xe="[[氙|Xe]]";
am.Cs="[[铯|Cs]]";am.Ba="[[钡|Ba]]";am.La="[[镧|La]]";am.Ce="[[铈|Ce]]";am.Pr="[[镨|Pr]]";am.Nd="[[钕|Nd]]";am.Pm="[[钷|Pm]]";am.Sm="[[钐|Sm]]";am.Eu="[[铕|Eu]]";am.Gd="[[钆|Gd]]";am.Tb="[[铽|Tb]]";am.Dy="[[镝|Dy]]";am.Ho="[[钬|Ho]]";am.Er="[[铒|Er]]";am.Tm="[[铥|Tm]]";am.Yb="[[镱|Yb]]";am.Lu="[[镥|Lu]]";am.Hf="[[铪|Hf]]";am.Ta="[[钽|Ta]]";am.W="[[钨|W]]";am.Re="[[铼|Re]]";am.Os="[[锇|Os]]";am.Ir="[[铱|Ir]]";am.Pt="[[铂|Pt]]";am.Au="[[金|Au]]";am.Hg="[[汞|Hg]]";am.Tl="[[铊|Tl]]";am.Pb="[[铅|Pb]]";am.Bi="[[铋|Bi]]";am.Po="[[钋|Po]]";am.At="[[砹|At]]";am.Rn="[[氡|Rn]]";
am.Fr="[[钫|Fr]]";am.Ra="[[镭|Ra]]";am.Ac="[[锕|Ac]]";am.Th="[[钍|Th]]";am.Pa="[[镤|Pa]]";am.U="[[鈾|U]]";am.Np="[[镎|Np]]";am.Pu="[[钚|Pu]]";am.Am="[[镅|Am]]";am.Cm="[[锔|Cm]]";am.Bk="[[锫|Bk]]";am.Cf="[[锎|Cf]]";am.Es="[[锿|Es]]";am.Fm="[[镄|Fm]]";am.Md="[[钔|Md]]";am.No="[[锘|No]]";am.Lr="[[鐒|Lr]]";am.Rf="[[鑪|Rf]]";am.Db="[[𨧀|Db]]";am.Sg="[[𨭎|Sg]]";am.Bh="[[𨨏|Bh]]";am.Hs="[[𨭆|Hs]]";am.Mt="[[䥑|Mt]]";am.Ds="[[鐽|Ds]]";am.Rg="[[錀|Rg]]";am.Cp="[[鎶|Cp]]";am.Nh="[[鉨|Nh]]";am.Fl="[[鈇|Fl]]";am.Mc="[[镆|Mc]]";am.Lv="[[鉝|Lv]]";am.Ts="[[鿬|Ts]]";am.Og="[[鿫|Og]]";

local T_ELEM = 0         -- token types
local T_NUM = 1          -- number
local T_OPEN = 2         -- open '('
local T_CLOSE = 3        -- close ')'
local T_PM_CHARGE = 4    -- + or –
local T_WATER = 6        -- .xH2O x number
local T_CRYSTAL = 9      -- .x
local T_CHARGE = 8       -- charge (x+), (x-)
local T_SUF_CHARGE = 10  -- suffix and charge e.g. 2+ from H2+
local T_SUF_CHARGE2 = 12 -- suffix and (charge) e.g. 2(2+) from He2(2+)
local T_SPECIAL = 14     -- starting with \ e.g. \d for double bond (=)
local T_SPECIAL2 = 16    -- starting with \y{x} e.g. \i{12} for isotope with mass number 12
local T_ARROW_R = 17     -- match: ->
local T_ARROW_EQ = 18    -- match: <->
local T_UNDERSCORE = 19  -- _{ ... }
local T_CARET = 20       -- ^{ ... }
local T_NOCHANGE = 30        -- Anything else like ☃

function su(up, down) -- like template:su
  if (down == "") then 
    return "<span style=\"display:inline-block; margin-bottom:-0.3em; vertical-align:0.8em; line-height:1.2em; font-size:70%; text-align:left;\">" .. up .. "<br /></span>";
  else
    return "<span style=\"display:inline-block; margin-bottom:-0.3em; vertical-align:-0.4em; line-height:1.2em; font-size:70%; text-align:left;\">" .. up .. "<br />" .. down .. "</span>";
  end
end

function DotIt()
  return ' <span style="font-weight:bold;">·</span> '
end


function item(f) -- (iterator) returns one token (type, value) at a time from the formula 'f'
   local i = 1
   local first = "true";

   return function ()
	local t, x = nil, nil

        if (first == "true" and f:match('^[0-9]', i)) then 
                 x = f:match('^[%d.]+', i); t = T_NOCHANGE; i = i + x:len();   -- matching coefficient (need a space first)

        elseif i <= f:len() then
                              x = f:match('^%s+[%d.]+', i); t = T_NOCHANGE;  -- matching coefficient (need a space first)
		if not x then x = f:match('^%s[+]', i); t = T_NOCHANGE; end       -- matching + (H2O + H2O)
		if not x then x = f:match('^%&%#[%w%d]+%;', i); t = T_NOCHANGE; end       -- &#...;
		if not x then x = f:match('^%<%-%>', i); t = T_ARROW_EQ; end       -- matching <->
		if not x then x = f:match('^%-%>', i); t = T_ARROW_R; end       -- matching ->
		if not x then x = f:match('^%u%l*', i); t = T_ELEM; end        -- matching symbols like Aaaaa
		if not x then x = f:match('^%d+[+-]', i); t = T_SUF_CHARGE; end        -- matching x+, x-
		if not x then x = f:match('^%d+%(%d*[+-]%)', i); t = T_SUF_CHARGE2; end        -- matching x(y+/-), x(+/-)
		if not x then x = f:match('^%(%d*[+-]%)', i); t = T_CHARGE; end        -- matching (x+) (xx+), (x-) (xx-)
		if not x then x = f:match('^[%d.]+', i); t = T_NUM; end        -- matching number
		if not x then x = f:match('^[(|{|%[]', i); t = T_OPEN; end     -- matching ({[
		if not x then x = f:match('^[)|}|%]]', i); t = T_CLOSE; end           -- matching )}]
		if not x then x = f:match('^[+-]', i); t = T_PM_CHARGE; end        -- matching + or -
		if not x then x = f:match('^%*[%d.]*H2O', i); t = T_WATER; end -- Crystal water
		if not x then x = f:match('^%*[%d.]*', i); t = T_CRYSTAL; end -- Crystal
		if not x then x = f:match('^[\\].{%d+}', i); t = T_SPECIAL2; end -- \y{x}
		if not x then x = f:match('^[\\].', i); t = T_SPECIAL; end -- \x
		if not x then x = f:match('^_{[^}]*}', i); t = T_UNDERSCORE; end -- _{...}
		if not x then x = f:match('^\^{[^}]*}', i); t = T_CARET; end -- ^{...}
		if not x then x = f:match('^.', i); t = T_NOCHANGE; end  --the rest - one by one
		if x then i = i + x:len(); else i = i + 999; error("Invalid character in formula!!!!!!! : "..f) end
	end
        first = "false"
	return t, x
	end
   end

function p._chem(args)
   
local f = args[1] or ''

   f = string.gsub(f, "–", "-")  -- replace – with -
   f = string.gsub(f, "−", "-")  -- replace – with -

   local sumO = 0
   local formula = ''
   local t, x

   local link = args['link'] or ""
   local auto = args['auto'] or ""

   if not (link == '') then formula = formula .. "[[" .. link .. "|"; end   -- wikilink start [[link|
 
   for t, x in item(f) do 
      if     t == T_ELEM then if (auto == '') then formula = formula .. x elseif am[x] then formula = formula .. am[x]; am[x] = x else formula = formula .. x end 
      elseif t == T_COEFFICIENT then formula = formula .. x
      elseif t == T_NUM   then formula = formula .. su("", x);
      elseif t == T_OPEN  then formula = formula .. x; sumO = sumO + 1;        -- ( {
      elseif t == T_CLOSE then formula = formula .. x; sumO = sumO -1;         -- ) }
      elseif t == T_PM_CHARGE    then formula = formula .. su(string.gsub(x, "-", "−"), "");
      elseif t == T_SUF_CHARGE then 
           formula = formula .. su(string.gsub(string.match(x, "[+-]"), "-", "−"), string.match(x, "%d+"), "");
      elseif t == T_SUF_CHARGE2 then 
          formula = formula .. su(string.sub(string.gsub(string.match(x, "%(%d*[+-]"), "-", "−"), 2, -1), string.match(x, "%d+"))

      elseif t == T_CHARGE then formula = formula .. "<sup>"; if string.match(x, "%d+") then formula = formula .. string.match(x, "%d+"); end formula = formula .. string.gsub(string.match(x, "[%+-]"), "-", "−") .. "</sup>";  -- can not concatenat a nil value from string.match(x, "%d+");

      elseif t == T_CRYSTAL then formula = formula .. DotIt() .. string.gsub( x, "*", ' ', 1 );

      elseif t == T_SPECIAL then
          parameter = string.sub(x, 2, 2) -- x fra \x  
          if       parameter == "s" then formula = formula .. "–"   -- single bond
            elseif parameter == "d" then formula = formula .. "="   -- double bond
            elseif parameter == "t" then formula = formula .. "≡"   -- tripple bond
            elseif parameter == "q" then formula = formula .. "≣"   -- Quadruple bond
            elseif parameter == "h" then formula = formula .. "η"   -- η, hapticity
            elseif parameter == "-" then formula = formula .. "-"   -- -
            elseif parameter == "\\" then formula = formula .. "\\"   -- \
            elseif parameter == "\'" then formula = formula .. "&#39;"   -- html-code for '
          end
      elseif t == T_SPECIAL2 then  -- \y{x}
         parameter = string.sub(x, 2, 2) -- y fra \y{x} 
          if parameter  == "h" then --[[哈普托數|Hapticity]]
             if (auto == '') then formula = formula .. "η<sup>" .. string.match(x, '%d+') .. "</sup>−" 
               else
             formula = formula .. "[[哈普托數|η<sup>" .. string.match(x, '%d+') .. "</sup>]]−" 
             end
--          elseif parameter == "i" then formula = formula .. su(string.match(x, '%d+'), "") -- [[同位素|isotope]]
          elseif parameter == "m" then formula = formula .. "μ<sup>" .. string.match(x, '%d+') .. "</sup>−"   -- mu ([[橋接配體|bridging ligand]])
          end
      elseif t == T_WATER then 
        if string.match(x, "^%*[%d.]") then 
            formula = formula .. DotIt() .. string.match(x, "%f[%.%d]%d*%.?%d*%f[^%.%d%]]") .. "H<sub>2</sub>O";
        else
          formula = formula .. DotIt() .. "H<sub>2</sub>O";
        end  
 
-- not (auto == nil or auto == '') then formula = formula .. DotIt .. 
-- "[[结晶水|H<sub>2</sub>O]]";
--            else
--              formula = formula .. 
-- DotIt .. "H<sub>2</sub>O";
---- xxx brug af sub til tal
--            end

      elseif t == T_UNDERSCORE  then formula = formula .. su("", string.sub(x,3,-2)) -- x contains _{string}
      elseif t == T_CARET then formula = formula .. su(string.sub(x,3,-2), "") -- x contains ^{string}

      elseif t == T_ARROW_R then formula = formula .. " → "
      elseif t == T_ARROW_EQ then formula = formula .. " ⇌ "

      elseif t == T_NOCHANGE  then formula = formula .. x;  -- The rest - everything which isn't captured by the regular expresions. E.g. wikilinks and pipes
     
      else error('unreachable - ???') end -- in fact, unreachable

end

-- Removed: Gives false positive for wikilinks, like {{chem2|[[氮|N]]}}.
--   if      sumO > 0 then formula = formula .. "<span style=\"display:none;font-size:100%\" class=\"error citation-comment\">   Too many (</span>;"
--    elseif sumO < 0 then formula = formula .. "'<span style=\"display:none;font-size:100%\" class=\"error citation-comment\">   Too many )</span>;"
--   end

   if not (link == nil or link == '') then formula = formula .. "]]"; end   -- wikilink closing ]]

   return formula
end

function p.chem(frame)
	local args = getArgs(frame)
	return p._chem(args)
end

return p