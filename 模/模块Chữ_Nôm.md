---Lexicographic tools for Vietnamese demotic text.
local p = {}

p.han_fonts = {
	'Nom Na Tong',
	'HAN NOM A',
	'HAN NOM B',
	'Sun-ExtA',
	'Sun-ExtB',
	'Ming-Lt-HKSCS-UNI-H',
	'Ming-Lt-HKSCS-ExtB',
	'HanaMinA',
	'HanaMinB',
	'HanaMin',
	'MingLiU',
	'MingLiU-ExtB',
	'MingLiU_HKSCS',
	'MingLiU_HKSCS-ExtB',
	'SimSun',
	'SimSun-ExtB',
	'Arial Unicode MS',
	'Lucida Sans Unicode',
	'TITUS Cyberbit Basic',
	'Code2000',
}

p.han_cd_fonts = {
	'Sun-ExtB',
	'MingLiU_HKSCS-ExtB',
	'Ming-Lt-HKSCS-ExtB',
	'HanaMinB',
}

---[[Bản_mẫu:Vi-nom|Bản mẫu:Vi-nom]]
function p.applyHanFonts(text, size)
	if type(text) == "table" then
		text, size = text.args[1], text.args.size
	end
	
	local css = mw.ustring.format("font-family: '%s', sans-serif;",
		table.concat(p.han_cd_fonts, "', '"))
	
	-- U+2A700/U+2B734, U+2B740/U+2B81F
	text = mw.ustring.gsub(text, "([𪜀-𫜴𫝀-𫠟])",
		'<span class="cjkv-cd" style="' .. css .. '">%1</span>')
	
	css = mw.ustring.format("font-family: '%s', sans-serif;",
		table.concat(p.han_fonts, "', '"))
	if size then
		css = css .. " font-size: " .. size .. ";"
	end
	return mw.ustring.format('<span lang="vi-Hani" xml:lang="vi-Hani" class="han-nom" style="%s">%s</span>',
		css, text)
end

return p