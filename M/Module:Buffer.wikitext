--[[=============================
This Module was written by Alexander Zhikun He, also known as, User:Codehydro on the English Wikipedia

All methods were developed independently and any resemblance to other string buffer libraries would be coincidental.
Furthermore, many methods will not work when compiled by standard Lua libraries as they depend on behaviors unique to
the MediaMiki Scribunto mod, which, for example, has a getmetatable() method that always returns nil on non-tables.
https://www.mediawiki.org/wiki/Extension:Scribunto/Lua_reference_manual

Source code comments may be thin at some points because they are intended to be supplemented by the documentation page:
https://en.wikipedia.org/wiki/Module:Buffer/doc

Licensed under Creative Commons Attribution-ShareAlike 3.0 Unported License
https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License

https://en.wikipedia.org/wiki/Module:Buffer
https://en.wikipedia.org/wiki/User:Codehydro
=============================--]]
local function Valid(v)--type validation
	if v and v~=true then--reject nil/boolean; faster than 2 type() comparisons
		local str = tostring(v)--functions not filtered since unlikely passed by accident (Scribunto does not have userdata/thread types)
		if str~=v and str=='table' then return rawget(v, 1) and table.concat(v) end--tostring(string-type) returns same ref; same refs compare faster than type()
		if str~='' then return str end--numbers are coerced to string per table.concat op; appending in string form saves ops on repeat concat
	end
end
local noOp, MBpairs = function()end do local iMap, vMap, oMap, pIter, pOther, pFast, Next--Map
	local function init()--init = noOp after first run
		function Next(t) return next, t end--slightly faster to do this than to use select()
		function pIter(t, k) k = (iMap[t] or MBpairs(t, true) and iMap[t])[not k and 1 or vMap[t][k]] return k, t[k] end--don't use rawget; accepting unmapped tables does not measurably affect performance.
		function pOther(t, k) k = (oMap[t] or MBpairs(t, true) and oMap[t])[nil==k and 1 or vMap[t][k]] return k, t[k] end--comparison to nil because false is a valid key
		function pFast(t, k) k = not k and 1 or k < (vMap[t] or #t) and k + 1 or nil return k, t[k] end--mapless iterator; almost as fast as native ipairs; slight performance penalty when length not cached
							   --k and k < (vMap[t] or #t) and k + 1 or not k and 1 or nil return k, t[k] end--mapless iterator; almost as fast as native ipairs; slight performance penalty when length not cached
		local mk = {__mode = 'k'}--use mode 'k'; found that mode 'kv' sometimes garbage collects maps mid-loop (may not error because iterators auto re-map, but that's expensive)
		init, iMap, vMap, oMap = noOp, setmetatable({}, mk), setmetatable({}, mk), setmetatable({}, mk)--iMap is numeric keys, oMap is non-numeric keys, and vMap points to next key
	end
	function MBpairs(t, ...)--pairs always iterates in order
		local iter, ex = ...
		iter = iter==init()--nil
		if iter and not oMap[t] and ex==nil and rawget(t, 1)~=nil and next(t, #t)==nil then--while possible to miss keys, more thorough check would negate the benefit of pFast
			vMap[t] = #t return pFast, t, nil
		elseif ... or not vMap[t] or select('#', ...)~=1 then
			local ti, tn, to, n = {}, {}, {}, #t--reduces table lookups
			iMap[t], vMap[t], oMap[t] = ti, tn, to
			for k = 1, n do ti[k], tn[k] = k, k + 1 end--stage one avoids number type checking op in stage two for most numeric keys
			for k in (ex or Next)(t) do
				if not tn[k] then table.insert(tonumber(k)~=k and to or ti, k) end
			end
			if #ti~=n then
				table.sort(ti)
				for k = 1, #ti do tn[ti[k]] = k + 1 end--somewhat wasteful, but trying to avoid overwriting can be even more expensive
			end
			for k = 1, #to do tn[to[k]] = k + 1 end
		end
		return iter and pIter or oMap[t] and pOther or noOp, t--noOp for mapless
	end
end
local parent, rawkey, spec do--new scope for variables not reused outside (reduces number of var names that need to checked outside of scope)
	local mkv = {__mode='kv', __call=function(t,k,v)t[k]=v return k end}--shared meta for Buffer parent property, raw mode, and specialized functions
	parent, rawkey, spec = setmetatable({}, mkv), setmetatable({}, mkv), setmetatable({}, mkv)--shared meta less memory
end

local MB, MBi, MBmix, buffHTML, gfuncs, noCache, Element do--minimize number of locals per scope to reduce time spent sifting through irrelevant variable names
	local _stream do local stream--keep stream near top of scope
		local function init(f)--init = noOp after first run
			local function each(self, ...)
				for k = 1, select('#', ...) do
					k = Valid(select(k, ...))--slightly faster than table.insert(self, (Valid(select(k, ...))))
					if k then table.insert(self, k) end
				end
				return self
			end
			init, stream, _stream = noOp, {
				__call = function(t, v) v = v and Valid(v) return v and table.insert(t, v) or t end,--last_concat cleared before entering stream mode
				__index = function(t, i) return i=='each' and each or MB.__index(t, i) and setmetatable(t, MB)[i] end,--no table look up minimizes resources to retrieve the only stream function
				__tostring = function(t) return setmetatable(t, MB)() end
			} for k, v in next, MB do stream[k] = stream[k] or v end
			setmetatable(stream, getmetatable(MB))
		end
		function _stream(self, ...) self.last_concat = init() return setmetatable(self, stream):each(...) end
	end
	local function isMBfunc(Buffer, s, ...)--helper for :getParent()-like methods (including getBuffer which does not return a parent)
		return s and (select('#', ...)==0 and--eventually should figure out to make this work for :getHTML which is very similar
				(not rawkey[s] and tostring(s):match'^_.*' and MB.__index(Buffer, s) and MB.__index(Buffer, s)(Buffer) or MBmix(Buffer, s))--unprefixed function names append as a string
				or assert(MB.__index(Buffer, s), ('" %s " does not match any available Module:Buffer function'):format(s))(Buffer, ...)--getParent is a one-way trip so one-time assert not expensive
			) or Buffer
	end
	local function MBselect(n, ...)--helper for :_out and :_str
		local n, seps = n - 1, {select(2, ...)}
		if type(seps[n])=='table' then 
			if buffHTML and rawget(seps[n], buffHTML) then return ... end
			setmetatable(seps, {__index = setmetatable(seps[n], {__index = function(t) return rawget(t, 1) end})})[n] = nil
		end
		return ..., seps
	end
	local _inHTML do local lastBuffer, lastHTML
		local function init(...)--init replaced and new version called on return
			local create, mwFunc = mw.html.create do
				local mwHTMLmeta = getmetatable(create())
				buffHTML, mwFunc, _inHTML = setmetatable(mw.clone(mwHTMLmeta), getmetatable(MB)), mwHTMLmeta.__index--buffHTML declared near top of module; remove _inHTML from outer scope
				function init(nodes, ...)
					local name, args, tag = select(... and type(...)=='table' and 1 or 2, nil, ...)
					tag = create(Valid(name), args)
					if nodes then table.insert(nodes, tag.parent and tag or rawset(tag, 'parent', parent[nodes])) end
					if args then
						local a, b = args.selfClosing, args.parent
						args.selfClosing, args.parent = nil
						if next(args) then Element._add(parent(tag.nodes, tag), args) end
						args.selfClosing, args.parent = a, b--in case args is reused
					end
					return tag
				end
				for k, v in next, {[mw] = mwHTMLmeta,
					__call = function(h, v) return MBmix(spec[h.nodes] and h.nodes or spec(setmetatable(parent(h.nodes, h), MB), Element), v) end,
					__concat = false,--false means take from MB
					__eq = false
				} do buffHTML[k] = v or MB[k] end
			end
			local nonSelf, BHi = {tag=true,done=true,allDone=true}, buffHTML.__index do local g
				g = {__index = function(t, i)
					if gfuncs and gfuncs[i] then g.__index, gfuncs = gfuncs return g.__index[i] end
				end}
				setmetatable(nonSelf, g)
				setmetatable(BHi, g)
			end
			for k in next, nonSelf do--any HTML objects returned by these funcs will be granted Module:Buffer enhancements
				local func = mwFunc[k]
				BHi[k] = function(t, ...) local HTML = func(t, ...) return parent[HTML] and HTML or setmetatable(parent(HTML, t), buffHTML) end
			end
			do local function joinNode(HTML, sep)
					local nodes, join = HTML.nodes
					if noCache and rawkey[sep] or Valid(sep) then join, HTML.nodes = tostring(rawset(HTML, 'nodes', {MB.__call(nodes, sep)})), nodes end
					return join or tostring(HTML)
				end
				for k, v in next, {
					getParent = function(HTML, ...) lastHTML = HTML return MBi.getParent(HTML:allDone(), ...) end,--return to Buffer that created the HTML tree
					getBuffer = function(HTML, ...) lastHTML = HTML return isMBfunc(lastBuffer, ...) end,--return to last used
					killParent = function(HTML, ...) MBi.killParent(HTML:allDone(), ...) return HTML end,
					_out = function(HTML, ...)
						if ...==0 then MBi._out(HTML.nodes, ...) return HTML end
						lastHTML, HTML = HTML, HTML:allDone()
						local n, ops, seps = select('#', ...)
						if n > 1 then
							local ops, seps = MBselect(n, ...)
							return parent[HTML]:_in(joinNode(HTML, rawget(seps, 0))):_out(ops, rawset(seps, buffHTML, true))
						end
						return parent[HTML]:_(joinNode(HTML, ...))
					end,
					_str = function(HTML, ...)--does not set lastHTML
						if ...==0 then return joinNode(HTML, select(2, ...)) end--passing 0 strings without calling allDone()
						local HTML, n = HTML:allDone(), select('#', ...)
						if n > 1 then
							local ops, seps = MBselect(n, ...)
							return parent[HTML]:_in(joinNode(HTML, rawget(seps, 1))):_str(ops, rawset(seps, buffHTML, true))
						end
						return joinNode(HTML, ...)
					end,
					_parent = function(HTML, ...) table.insert(HTML.nodes, parent[HTML:allDone()]:_str(...)) return HTML end
				} do BHi[k] = v end
			end
			do local htmlArg, skip, outFuncs = {parent=true,selfClosing=true,tagName=true}, {}
				do local out local function func(nodes, ...) return out(parent[nodes], ...) end
					outFuncs = setmetatable({
						tag = function(nodes, ...) return parent(setmetatable(init(nodes, ...), buffHTML), parent[nodes]) end,
						done = function(b, ops)
							b = parent[b] 
							while b.parent and ops~=0 do b, ops = b.parent, ops and ops - 1 or 0 end
							return b
						end
					}, {__index = function(nodes, i)
						if rawget(BHi, i) then out = BHi[i] return func end--rawget to exclude globals
					end})
				end
				Element = {
					_add = function(nodes, t)
						for k, v in MBpairs(t), t, skip[t] do (v~=true and MBmix or noOp)(nodes, v) end
						local HTML = parent[nodes] for k, v in MBpairs(t, false) do
							if htmlArg[k] then HTML[k] = v
							elseif v and v~=true then
								if nonSelf[k] then
									if k=='tag' then
										if type(v)=='table' then
											skip[v], k = 1, rawset(create(Valid(v[1])), 'parent', HTML)
											Element._add(spec(parent(k.nodes, k, table.insert(nodes, k)), Element), v)
											if k.selfClosing then k.nodes = nil else spec[k.nodes], parent[k.nodes] = nil end--free memory/reduce clutter; parent ref will auto-unset when k.nodes is nil
											if not k.tagName then k.styles, k.attributes = nil end
										else table.insert(nodes, create(v)) end
									elseif mwFunc[k] then
										if k=='done' and tonumber(v)~=v and v[1] and tonumber(v[1])==v[1] then skip[v] = 1 end
										MBmix(outFuncs[k](nodes, skip[v] and v[1]).nodes, v)
									elseif v[1] or v[2] then
										k = MBi[k](nodes, unpack(v, 1, rawset(skip, v, k=='_B' and 1 or 2)[v]))
										Element._add(getmetatable(k) and rawget(k, 'nodes') or k, v)--if k is not a table, then v should not contain any extra keys or this may error.
									else MBi[k](nodes, v) end--k probably == '_G' or '_R'
								elseif mwFunc[k] then
									if type(v)~='table' or rawget(v, 'nodes') then mwFunc[k](HTML, v)
									else
										local css = k=='css'
										for x, y in MBpairs(v, true) do (y and y~=true and mwFunc[k] or noOp)(HTML, css and x:gsub('_', '-') or x, y) end--iterate non-numbers first
										for _, y in MBpairs(v, nil) do (y and y~=true and mwFunc[k] or noOp)(HTML, y) end--don't bother with gsub since text must be quoted anyhow
									end
								elseif rawget(Element, k) or rawget(MBi, k) then
									if tonumber(v)==v or v[1]==nil or getmetatable(v) then (Element[k] or MBi[k])(nodes, v)--v is probably string-able object, or a table to be handled by :_all
									else (Element[k] or MBi[k])(nodes, unpack(v, 1, table.maxn(v))) end--v is definately a table
								else mwFunc.css(HTML, k:gsub('_', '-', 1), tostring(v)) end--oddly enough, :_add clocked its fastest runtime after adding auto-gsub as a feature
								skip[v] = nil
							end
						end
						return nodes
					end
				}
				local tempMeta = {mode='v', copy={styles=true,attributes=true}}
				function tempMeta.__index(t, i) return tempMeta.copy[i] and rawset(t, i, MBi._cc(false, 0, t.orig[i]))[i] or t.orig[i] end
				rawkey[setmetatable(Element, {__index = outFuncs, __concat=function(Element, v) return setmetatable({nodes=spec({}, Element),orig=parent[v]}, tempMeta) end})] = math.huge
			end
			function MBi:getHTML(...)
				lastBuffer = self
				if ... then
					if select('#', ...)==1 then return not rawkey[s] and tostring(...):match'^_' and BHi[...] and BHi[...](lastHTML) or lastHTML(...)
					else return assert(BHi[...], ('" %s " does not match any mw.html or Buffer-mw.html function'):format(tostring(...)))(lastHTML, select(2, ...)) end
				end
				return lastHTML
			end
			function MBi:_html(...) return MBi._(self, lastHTML, select(spec[self]==Element and select('#', ...)==0 and 1 or 2, true, ...)) end
			return init(...)
		end
		function _inHTML(self, ...)
			local HTML = init(nil, ...)
			if HTML.selfClosing and spec[self]==Element then self.last_concat = table.insert(self, HTML) return self end
			lastBuffer, lastHTML = self, setmetatable(parent(HTML, self), buffHTML)--set after 'args' table processed by :_add
			return HTML
		end
	end
	local _var, unbuild do local prev, rebuild
		local function init(...)--init replaced before return
			local function pick(b, v) return b and table.insert(b, v) or v end
			local function c(a, num) return rawset(a.a or a, 0, a[0] and a[0] + a.c or num and a[1] or a[1]:byte())[0] end
			local same, build, alt = {__tostring = function(a, b) return a.a[0] and pick(b, a.a.string and string.char(a.a[0]) or a.a.table and a.a[1][a.a[0]] or a.a[0]) end}, {
				__index = {c = 1},
				__tostring = function(t) return t:_build() end,
				table = function(a, b) local i = next(a[1], a[0]) or a[0]==#a[1] and next(a[1]) return pick(b, rawset(a.a or a, 0, i)[1][i]) end,--change rate (a.c) ignored since users control the table's contents
				number = function(a, b) return pick(b, c(a, true)) end,
				string = function(a, b) return pick(b, string.char(c(a))) end
			}, {__index = function(a, i) return a.a[i] end, __tostring = function(a, b) return (rawget(a, 0) and a[0]==tostring(a[0]) and rawset(a, 0, a[0]:byte()) or a).a._build(a, b) end}
			local function shift(t, c)
				t[0] = t[0] and t[0] + c or t:_build() and t[0] - t.c + c
				if t.table then t[0] = (t[0] - 1) % #t[1] + 1 end
			end
			function rebuild(...)
				local v, c = ...
				if v or select('#', ...)==0 then
					if v and not c then return prev end
					local meta, c = select(v and 1 or 3, alt, c, same, 0)
					return setmetatable({a = prev, _build = meta.__tostring, c = c}, meta)
				elseif v==nil then--no-op
				elseif c then shift(prev, c)--v == false
				else prev:_build() end
			end
			init, noCache = function(v, c) prev = setmetatable({v, c = c, _build = build[type(v)] or v, [type(v)] = true, alt = {}}, build) return prev end, true
			return init(...)
		end
		function unbuild(sep)
			for k, v in MBpairs(sep, nil) do
				k = getmetatable(v) if k and (k==build or k==alt) then shift(v.a or v, -v.c) end
			end
		end
		function _var(self, ...)
			local obj if ... and ...~=true then obj = init(...)
			elseif prev then
				if ...~=false then obj = rebuild(...)
				else rebuild(...) end
			end
			return obj and MBi._(self, obj, nil, true) or self
		end
	end
	local lib; MBi = setmetatable({stream = _stream,
		_inHTML = _inHTML,
		_var = _var,
		_ = function(self, v, ...)
			local at, raw = select(select('#', ...)==1 and ...==true and 1 or 2, nil, ...)
			if raw then rawkey[self] = math.huge else v = Valid(v) end
			if v or raw then
				if at or rawkey[self] then raw = #self end--if length increases by more than one after table.insert, then set rawkey[self] = math.huge; rawkey[self] may be equal to a previous 'at'
				at, self.last_concat = at and (tonumber(at)~=at and raw + at or at)
				table.insert(self, select(at and 1 or 2, at, v))
				if at and at < 0 or raw and #self - raw > 1 then rawkey[self] = math.huge elseif at and #self==raw then rawkey[self] = rawkey[self] and math.max(rawkey[self], at) or at end
			end--above line looks bizarre because one table.insert op may make length jump from 0 to 8: local wtf={[2]=2,[4]=4,[8]=8}mw.log(#wtf,table.insert(wtf,1),#wtf)
			return self
		end,
		_nil = function(self, at, ...)
			if ...~=true and ...~=false then--faster than type(...) ~= 'boolean'
				if not at or at=='0' then
					self[#self] = ... if ... then rawkey[self] = math.huge end
				else
					local n, v = tonumber(at), ...
					if n~=at then 
						if n then n = #self + at
						elseif at~=true and select('#', ...)==0 then v, n = at, #self end
					end
					if n then 
						if v==nil and n > 0 then table.remove(self, n)
						else self[math.floor(n)], rawkey[self] = v, math.huge end--floor position for consistency with Table library
					end
				end
				self.last_concat = nil
			end
			return self
		end,
		_all = function(self, t, valKey)
			for k, v in MBpairs(t) do MBmix(self, v, valKey) end
			for k, v in valKey and MBpairs(t, false) or noOp, t do
				if tonumber(v) then MBi._(self, k, v)--self not always a buffer
				elseif rawget(MBi, k) and v and v~=true then
					if v[1]==nil or getmetatable(v) then MBi[k](self, v)
					else MBi[k](self, unpack(v, 1, table.maxn(v))) end
				end
			end
			return self
		end,
		_str = function(t, ...)
			local n = select('#', ...)
			if n > 1 then
				local k, ops, seps, r = 2, MBselect(n, ...)
				r = MB(t(seps[1]))
				while parent[t] and ops > 1 and r:_(parent[t](seps[k]), 1) do t, k, ops = parent[t], k + 1, ops - 1 end
				return table.concat(r, seps[k] or nil)
			end
			return MB.__call(t, ...)
		end,
		_in = function (self, ...) return parent(MB(...), self) end,
		_out = function(t, ...)
			if ...==0 then return parent(t, parent[t], MBi._cc(t, t, MB.__call(t, (select(2, ...))), getmetatable(t))) end--love how :_cc needed nothing new to implement this *self pat on back*
			local n = select('#', ...)
			if n > 1 then
				local k, ops, seps = 1, MBselect(n, ...)
				while parent[t] and ops > 0 do t, k, ops = parent[t]:_(t(seps[k])), k + 1, ops - 1 end
			elseif parent[t] then return parent[t]:_(t(...)) end
			return t
		end,
		_cc = function(self, clear, copy, meta)
			if clear then
				if rawequal(clear, copy) then return self, spec[MBi._cc] and setmetatable(spec[MBi._cc], MB)--rawequal to avoid re-string via __eq in case both are different Buffer objects
				elseif copy==true then copy = self end
				if clear~=0 then
					assert(type(clear)=='table', debug.traceback('Buffer:_cc can only "clear" tables. Did you forget to call with a colon?', 2))--errors can be hard to trace without this
					for k in self and next or noOp, clear do rawset(clear, k, nil) end
				else return MBi._cc(false, {unpack(copy)}, copy) end--copy length w/o empty strings; recursion to avoid self = false causing garbage collection (non-weak child may exist)
				if self==false or copy and type(copy)=='table' then--self==false means copy is a table (saves a type op for recursive calls)
					meta = meta or getmetatable(copy)
					if self and #copy > 1 then--preserves length with empty strings; developed from studying http://www.lua.org/source/5.1/ltable.c.html		
						local n, null, i, e = #copy, {}, math.ldexp(2, select(2, math.frexp(#copy)) - 2)
						e, spec[MBi._cc], parent[null] = i - 1, null, clear
						for k = 1, e do table.insert(clear, false) end
						while i<=n do table.insert(clear, i, '') i, null[i] = i + math.ldexp(2, select(2, math.frexp(n - i)) - 2), '' end
						for k = 1, e do rawset(clear, k, nil) end
					end
					for k, v in next, copy do rawset(clear, k, type(v)=='table' and MBi._cc(false, 0, v) or v) end
				elseif copy then rawset(clear, 1, (Valid(copy))) end
				rawkey[setmetatable(clear, meta)], parent[clear] = rawkey[copy], parent[copy]
			end
			return self and rawset(self, 'last_concat', nil) or clear
		end,
		_parent = function(self, ...) return parent[self] and MBi._(self, parent[self]:_str(...)) or self end,
		getParent = function(self, ...) return isMBfunc(parent[self] or parent[parent(self, setmetatable({}, MB))], ...) end,
		killParent = function(self, ...) return parent[self] and isMBfunc(parent[self], ...) and parent(self) or self end,
		_build = function(self, t) table.insert(t, self()) end,--for compatibility with mw.html:node()
		last_concat = false--prevent library check
	}, {__index = function(t, i)--import string, mw.text, and mw.ustring libraries on an as-needed basis
		local func = string[i] or mw.text[i] or mw.ustring[i] or type(i)=='string' and mw.ustring[i:match'^u(.+)'] if func then
			lib	= lib or function (s, f, ...)
				if parent[s] and next(s)==nil then return s:_((f(tostring(parent[Element and (spec[s]==Element and s:allDone() or spec[parent[s]]==Element and parent[s]) or s]), ...))) end
				return f(tostring(s), ...)--not using ternary/logical operators here to allow multiple return values
			end
			return rawset(t, i, i:match'^u?gsub' and function(self, p, r, ...)return lib(self, func, p, r or '', ...)end--Why are ugsub/gsub special? because empty strings are against my religion!
				or function(self, ...)return lib(self, func, ...)end)[i]
		end
	end})
end

function MBmix(t, v, ...) return v and ((type(v)~='table' or getmetatable(v)) and MBi._(t, v) or (select('#', ...)==0 and spec[t] and spec[t]._add or MBi._all)(t, v, ...)) or t end--:_all always passes two args

local _G, new_G = _G--localize _G for console testing (console _G ~= module _G)
return setmetatable({__index = function(t, i) return spec[t] and spec[t][i] or MBi[i] end,
	__call = function(t, ...)
		local rawsep, sep, i, j, raw = noCache and rawkey[...] and ..., ...
		if i or j or rawsep or Valid(sep) then
			raw, sep, i, j = rawkey[spec[t]] or rawkey[t], rawsep or Valid(sep), i and (i~=tonumber(i) and i + #t or i), j and (j~=tonumber(j) and j + #t or j)
			if rawsep or raw and (raw>=(j or #t) or i < 1) then
				raw, i, j = {}, i and math.floor(i), j and math.floor(j)--floor for consistency with table.concat(t, sep, i, j), which ignores decimals
				raw.lc, t.last_concat = t.last_concat--temporarily unset last_concat to prevent disqualification from mapless iteration
				for k, v in MBpairs(t) do
					if raw[1] or not i or k>=i then if j and k > j then break end
						if raw.s then raw.s = table.insert(raw, tostring(sep)) end--if sep contains v and v is a Buffer-variable, sep must be strung before v
						k = Valid(v) if k then
							raw.s = rawsep or sep and raw[1] and table.insert(raw, sep)
							table.insert(raw, k)
						end
					end
				end
				if rawsep and not raw.s then raw[#raw] = unbuild(sep) end--unbuild rawsep if final index in t was invalid
				t.last_concat = raw.lc return table.concat(raw)
			end
			return table.concat(t, sep, i and math.max(i, 1), j and math.min(j, #t))
		end
		return MB.__tostring(t)
	end,
	__tostring = function(t)
		if t.last_concat then return t.last_concat end
		local r = rawkey[spec[t]] or rawkey[t]
		r = table.concat(r and r>=#t and MBi._all({}, t) or t)
		return (noCache or rawset(t, 'last_concat', r)) and r
	end,
	__concat = function(a, b)
		if buffHTML then
			for k = 1, 2 do local v = select(k, a, b)--faster than for k, v in pairs{a, b} do
				if v and spec[v] and spec[v]==Element then
					if parent[v].selfClosing then
						if rawequal(a, b) then return (not noCache or parent[v].tagName) and v:_str(0):rep(2) or v:_str(0)..v:_str(0) end--rawequal avoids premature tostring of Buffer:_var objects;
						b, a = select(k, b, parent[v], a)
					else local temp = Element .. v --helper method; returns a mirror of parent[v]
						MBmix(MBmix(parent(temp.nodes, temp), a), k==1 and spec[b]==Element and parent[b] or b)
						return buffHTML.__tostring(setmetatable(temp, {__index=parent[v], __mode='v'}))--switch from tempMeta to avoid MBi._cc op of styles/attributes
					end
				end
			end
		end
		return table.concat(MBmix(MBmix({}, a), b))
	end,
	__pairs = MBpairs,
	__ipairs = MBpairs,
	__eq = function(a, b) return tostring(a)==tostring(b) end--avoid a==b in this module; use rawequal(a,b) when they may be different Buffers (premature tostring waste ops and is bad for Buffer:_var)
}, {__tostring = function()return''end,
	__call = function(self, ...) MB = MB or self
		if new_G then if ... and _G and ...==_G then new_G = ... end
		elseif ... and (...==_G or type(...)=='table' and (...)._G==...) then
			local Nil, mG = {}, (...):getmetatable() or (...):setmetatable{}:getmetatable()
			new_G, _G, gfuncs = ..., ..., {--gfuncs stored for Buffer:_inHTML; new_G is a is a Module:Buffer local declared just before the final return statement.
				_G = function(self, i, ...)
					local X, save = rawget(new_G, i), select('#', ...)==0 and self or ...
					if i and i~=true and not (X and save and rawequal(X, save)) and rawset(new_G, i, save) and (X~=nil or save==nil and new_G[i]~=nil) then--rawequal in case X is another buffer
						local mG = getmetatable(new_G) or {__call=mG.__call}
						if mG.__index then pcall(rawset, mG.__index, i, X)
						else mG.__index = setmetatable(new_G, mG) and {[i] = X} end
					end
					return self, ...--avoiding __eq with rawequal(self,save) is overkill since buffers can self-save without being passed as save
				end,
				_R = function(self, i, v, m)
					if i~='new_G' then if i and i~=true then rawset(new_G, i , v) end
					elseif not v or v==true or v._G~=_G then new_G = setmetatable(v~=true and v or {}, {__call = mG.__call, __index = v~=true and m~=true and (m or new_G) or nil})
					else new_G, (not m and (m~=nil or v==new_G) and Nil or getmetatable(v)).__index = v, m~=true and (m or new_G) or nil end--setting Nil.__index is noOp
					return self
				end,
				_2 = function(self, ...)
					if new_G[...]~=nil then return new_G[...] end--higher priority so Buffer:_G('new_G', ...) can prevent an overwrite
					if ...=='new_G' then return rawset((select('#', ...)~=1 and MBi._R(new_G, ...) or new_G), '_G', _G) end
					return select(select('#', ...)==1 and 1 or 2, self:_G(...))--return only one value; 'return select(2, self:_G(...)) or self' doesn't work for returning nil
				end,
				_B = function(self, v) return v or v==nil and Nil end
			} for k, v in next, gfuncs do MBi[k] = v end 
			setmetatable(Nil,{__concat=MB.__concat,__newindex=noOp,__call=noOp,__tostring=noOp,__metatable=MB,__index=setmetatable({_B=MBi._B,_=function()return Nil end,last_concat=''},
				{__index=function(t,i)return (MBi[i] or i and not tonumber(i)) and t._ or nil end})})
			function mG.__call(G, k, ...) return (k._G or G.type(k)=='table') and (G.select('#', ...)~=1 and G.rawset(k, ...) or G:rawset(..., k) and k) or G:rawset(k, (...)) and ... end
		end
		local new = setmetatable({}, self)
		if ... and (...)==new_G then return select(2, ...) and MBmix(new:_G((select(2, ...))), select(3, ...)) or new end
		return ... and MBi._(new, ...) or new
	end,
	__index = function(t, i)
		MB = MB or t return MBi[i] and function(...) return MBi[i](setmetatable({}, t), select(...==t and 2 or 1,...)) end
	end
})