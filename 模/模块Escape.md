local escape = {
	char = function(self, chr, args)
		args = args or {}
		local safe = args.safeChr or string.char(13)
		chr = tostring(chr or '\\')
		self[1] = ('%s0%%s%s'):format(
			('%x%s%s'):format(chr:byte(), safe, safe),
			('%s%x'):format(safe, chr:byte())
		)
		if not self[self[1]] then
			self[self[1]] = {
				char = chr,
				text = ('%s(.)'):format(chr),
				undo = self[1]:format'(%d+)'
			}
		end
		return args.text and self:text(args.text)
			or args.undo and self:undo(args.undo, chr)
			or args.kill and self:kill(args.kill)
			or self
	end,
	exec = function(self, text, mode, newEscape)
		local target = self[self[1] or self:char() and self[1]]
		for v in text:gfind(target[mode]) do
			text = text:gsub(
				mode == 'text' and
					('%s%s'):format(target.char, v:gsub('%W', '%%%1'))
					or self[1]:format(v),
				mode == 'text' and
					self[1]:format(v:byte())
					or (newEscape or '') .. v:char()
			)
		end
		return text
	end,
	text = function(self, text)
		return self:exec(type(text) == 'table' and text[1] or text, 'text')
	end,
	undo = function(self, text, newEscape)
		if type(text) == 'table' then
			text, newEscape = unpack(text)
		end
		return self:exec(text, 'undo', newEscape)
	end,
	kill = function(self, text, chars, newEscape)
		if type(text) == 'table' then
			text, chars, newEscape = unpack(text)
		end
		return self:undo(self:text(text):gsub(chars or '', ''), newEscape)
	end
}

function escape.main(frame)
	local args, family = {}, {frame:getParent(), frame}
	for f = 1, 2 do
		for k, v in pairs(family[f] and family[f].args or {}) do
			args[k] = args[k] or v:match('^%s*(.-)%s*$')
		end
	end
	if args.mode == 'char' then
		return escape:char(args.char or args[2], args)
	end
	return escape[args.mode](escape:char(args.char), args)
end

return escape