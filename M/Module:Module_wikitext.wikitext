local p = {}

p.text = ''

function p.main()
	return p.text
end

function p._addText(text, preprocessFrame)
	if preprocessFrame ~= false then
		text = (preprocessFrame or mw.getCurrentFrame()):preprocess(text)
	end
	p.text = p.text .. text
end

return p