-- To be used in template {{template|Athex}} for mapping web addresses

local data = {
	AEGN = 1183,
	AIOLC = 69,
	ALPHA = 43,
	ANEK = 660,
	BELA = 456,
	BOC = 877,
	CENTR = 938,
	EEE = 1297,
	ELKA = 205,
	ELLAKTOR = 179,
	ELPE = 624,
	ETE = 52,
	EUPIC = 429,
	EUROB = 61,
	EXAE = 859,
	EYDAP = 794,
	FFGRP = 611,
	FRIGO = 768,
	GEKTERNA = 287,
	GRIV = 1003,
	HOL = 898,
	HTO = 105,
	INLOT = 761,
	INTRK = 399,
	KARE = 256,
	METKK = 217,
	MIG = 325,
	MINOA = 618,
	MLS = 901,
	MOH = 904,
	MYTIL = 336,
	OPAP = 896,
	PLAIS = 666,
        PPA = 963,
	PPC = 916,
	PROF = 971,
	PSYST = 824,
	TATT = 44,
	TELL = 47,
	TENERGY = 1194,
	TITK = 158,
	TITP = 159,
	TPEIR = 60,
	VIO = 1311,
	XALY = 229,
}

local p = {}

function p.main(frame)
	local args = require('Module:Arguments').getArgs(frame, {wrappers = 'Template:Athens Exchange'})
	if not args[1] then
		error('A stock symbol must be provided')
	elseif not data[args[1]] then
		error(string.format(
			'No entry for stock symbol %s is present in [[Module:Athens_Exchange|Module:Athens Exchange]]',
			args[1]
		))
	else
		return string.format(
			'[[Athens_Stock_Exchange|Athex]]: [http://www.helex.gr/web/guest/stock-snapshot/-/select-stock/%s %s]',
			data[args[1]],
			args[1]
		)
	end
end

return p