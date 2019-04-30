local p = {
	gov = 'Location dot red.svg',
	opp = 'Dot green 0d0.svg',
	SDF = 'Dot yellow ff4.svg',
	JaN = 'Map-dot-grey-68a.svg',
	IS = 'Location dot black.svg',
	Trk = 'Location dot green.svg',
	lcl = 'Location dot blue.svg',
	spc = 'Location dot orange.svg',
	
	gov_oil = 'Gota01.svg',
	opp_oil = 'Gota02.svg',
	SDF_oil = 'Gota04.svg',
	JaN_oil = 'Gota08.svg',
	IS_oil = 'Gota07.svg',
	Trk_oil = 'GotaAH.svg',
	lcl_oil = 'Gota03.svg',
	
	truce_gov_opp = 'LACMTA Circle Purple Line.svg',
}

local sides = {
	'gov',
	'opp',
	'SDF',
	'JaN',
	'IS',
	'Trk',
	'lcl',
	'spc',
}

local colors = {
	gov = 'red',
	opp = 'lime',
	SDF = 'yellow',
	JaN = 'grey',
	IS = 'black',
	Trk = 'green',
	lcl = 'blue',
	spc = 'orange',
}

local directions = {
	N = 'NN',
	NE = 'NE',
	E = 'EE',
	SE = 'SE',
	S = 'SS',
	SW = 'SW',
	W = 'WW',
	NW = 'NW'
}

local symbols = {
	siege = 'Map-circle-%s.svg',
	hill = 'Map-peak-%s.svg',
	air = 'Fighter-jet-%s-icon.svg',
	heli = 'Helicopter-%s-icon.svg',
	naval = 'Anchor pictogram %s.svg',
	base = 'Abm-%s-icon.png',
	rural3 = '3x3dot-%s.svg',
	rural4 = '4x4dot-%s.svg',
	industry = 'Icon NuclearPowerPlant-%s.svg' --For Trk icons shared with opp icons (temp.)
}

for side,color in pairs(colors) do
	for k,v in pairs(directions) do
		p[string.format('%s_%s', side, k)] = string.format('Map-arc%s-%s.svg', v, color)
	end
	for k,v in pairs(symbols) do
		p[string.format('%s_%s', side, k)] = string.format(v, color)
	end
end

for i,sidei in ipairs(sides) do
	for j=(i+1),#sides do
		p[string.format('%s_%s', sidei, sides[j])] = string.format('80x80-%s-%s-anim.gif', colors[sidei], colors[sides[j]])
		p[string.format('stable_%s_%s', sidei, sides[j])] = string.format('Map-ctl2-%s+%s.svg', colors[sidei], colors[sides[j]])
		for k=(j+1),#sides do
			p[string.format('%s_%s_%s', sidei, sides[j], sides[k])] = string.format('80x80-%s-%s-%s-anim.gif', colors[sidei], colors[sides[j]], colors[sides[k]])
			p[string.format('stable_%s_%s_%s', sidei, sides[j], sides[k])] = string.format('Map-ctl3-%s+%s+%s.svg', colors[sidei], colors[sides[j]], colors[sides[k]])
		end
	end
end

for k in pairs(directions) do
	p[string.format('pass_%s', k)] = string.format('Mountain pass 12x12 %s.svg', k:lower())
	p[string.format('dam_%s', k)] = string.format('Arch dam 12x12 %s.svg', k:lower())
end

-- Overrides
p.SDF_base = 'Abm-yellow-icon-2.png'
p.IS_naval = 'Anchor pictogram.svg'
p.opp_industry = 'Icon NuclearPowerPlant-green.svg'
p.IS_lcl = '80x80-blue-black-anim.gif'
p.IS_Trk = '80x80-green-black-anim.gif'
p.opp_naval = 'Anchor pictogram green.svg'

return p