-- This module returns the country name or the flag name for a country,
-- based on the three-letter IOC/CGA/FINA alias.

--[[
The following country code is used for multiple countries:
  ANG (workaround: added ANG_CGF)

The following names occur twice due to CGF/IOC/FINA differences
    Anguilla                         AIA, ANG_CGF
    Antigua and Barbuda              ANT, ATG
    Curaçao                          CUR, CUW
    Faroe Islands                    FAR, FRO
    French Polynesia                 PYF, TAH
    Hong Kong						 HKG, HKG_CGF (latter added to keep colonial flag)
    Iran                             IRI, IRN
    Ireland                          IRE, IRL - IRE is *only* for CGF apps
    Lebanon                          LBN, LIB
    Nicaragua                        NCA, NIC
    Refugee Olympic Team             ROA, ROT
    Romania                          ROM, ROU
    Saint Helena                     SHE, SHN
    Saint Vincent and the Grenadines SVG, VIN
    Sarawak                          SAR, SWK
    Singapore                        SGP, SIN
    South Africa                     RSA, SAF
    Tonga                            TGA, TON
    Trinidad and Tobago              TRI, TTO
    Turks and Caicos Islands         TCI, TKS
]]

local countries = {
	EXA = {                             -- example for testing
		name = "Example Country",
		{1951, "Flag1951.svg"},         -- year <= 1951
		{1995, "Flag1995.svg"},         -- 1951 < year <= 1995
		"Flag of test.svg",             -- otherwise
		["Paralympics"] = "Paralympics.svg",
		["Summer Olympics"] = {
			[1948] = "SO1948.svg",
			[1952] = "SO1952.svg",
			[1980] = "SO1980.svg",
		},
		["Winter Olympics"] = {
			[1956] = "WO1956.svg",
			[1964] = "WO1964.svg",
		},
	},
	ADN = {
		name = "亞丁",
		"Flag of the Colony of Aden.svg",
	},
	AFG = {
		name = "阿富汗",
		{1973, "Flag of Afghanistan (1931–1973).svg"},
		{1978, "Flag of Afghanistan (1974–1978).svg"},
		{1987, "Flag of Afghanistan (1980-1987).svg"},
		{1992, "Flag of Afghanistan (1987–1992).svg"},
		{1996, "Flag of Afghanistan (1992-1996; 2001).svg"},
		{2003, "Flag of Afghanistan (2002-2004).svg"},
		"Flag of Afghanistan.svg",
	},
	AHO = {
		name = "荷属安的列斯",
		{1982, "Flag of the Netherlands Antilles (1959-1986).svg"},
		{2010, "Flag of the Netherlands Antilles (1986-2010).svg"},
		"Flag of the Netherlands.svg",
		["Pan American Games"] = {
			[2011] = "Flag of PASO.svg",
		},
	},
	AIA = {
		name = "安圭拉",
		"Flag of Anguilla.svg",
	},
	ALB = {
		name = "阿尔巴尼亚",
		{1992, "Flag of Albania (1946-1992).svg"},
		"Flag of Albania.svg",
	},
	ALG = {
		name = "阿尔及利亚",
		"Flag of Algeria.svg",
	},
	AND = {
		name = "安道尔",
		"Flag of Andorra.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	ANG = {
		name = "安哥拉",
		"Flag of Angola.svg",
	},
	ANG_CGF = {
		name = "安圭拉",
		"Flag of Anguilla.svg",
	},
	ANT = {
		name = "安提瓜和巴布达",
		{1966, "Missing Blue Ensign.svg"},
		"Flag of Antigua and Barbuda.svg",
	},
	ANZ = {
		name = "澳大拉西亞",
		"Flag of Australasian team for Olympic games.svg",
	},
	AOI = {
		name = "獨立參賽者",
		"Olympic flag.svg",
	},
	ARG = {
		name = "阿根廷",
		"Flag of Argentina.svg",
	},
	ARM = {
		name = "亞美尼亞",
		"Flag of Armenia.svg",
	},
	ARU = {
		name = "阿魯巴",
		"Flag of Aruba.svg",
	},
	ASA = {
		name = "美屬薩摩亞",
		"Flag of American Samoa.svg",
	},
	ATG = {
		name = "安提瓜和巴布达",
		{1966, "Missing Blue Ensign.svg"},
		"Flag of Antigua and Barbuda.svg",
	},
	AUS = {
		name = "澳大利亚",
		{1900, "Flag of the United Kingdom.svg"},
		{1909, "Flag of Australia 1903-1909.svg"},
		"Flag of Australia.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	AUT = {
		name = "奥地利",
		{1912, "Flag of the Habsburg Monarchy.svg"},
		"Flag of Austria.svg",
	},
	AZE = {
		name = "阿塞拜疆",
		"Flag of Azerbaijan.svg",
	},
	BAH = {
		name = "巴哈马",
		{1923, "Flag of the Bahamas (1904-1923).svg"},
		{1953, "Flag of the Bahamas (1923-1953).svg"},
		{1964, "Flag of the Bahamas (1953-1964).svg"},
		{1972, "Bahamas Blue Ensign 1964.PNG"},
		"Flag of the Bahamas.svg",
	},
	BAN = {
		name = "孟加拉国",
		"Flag of Bangladesh.svg",
	},
	BAR = {
		name = "巴巴多斯",
		{1966, "Flag of Barbados (1870–1966).png"},
		"Flag of Barbados.svg",
	},
	BDI = {
		name = "蒲隆地",
		"Flag of Burundi.svg",
	},
	BEL = {
		name = "比利时",
		"Flag of Belgium (civil).svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	BEN = {
		name = "贝宁",
		{1990, "Flag of Benin (1975-1990).svg"},
		"Flag of Benin.svg",
	},
	BER = {
		name = "百慕大",
		{1999, "Flag of Bermuda 1910-1999.svg"},
		"Flag of Bermuda.svg",
	},
	BGU = {
		name = "British Guiana",
		{1906, "Flag of British Guiana (1875–1906).svg"},
		{1919, "Flag of British Guiana (1906-1919).svg"},
		{1955, "Flag of British Guiana (1919-1955).svg"},
		"Flag of British Guiana (1955-1966).svg",
	},
	BHU = {
		name = "不丹",
		"Flag of Bhutan.svg",
	},
	BIH = {
		name = "波斯尼亚和黑塞哥维那",
		{1998, "Flag of Bosnia and Herzegovina (1992-1998).svg"},
		"Flag of Bosnia and Herzegovina.svg",
	},
	BIR = {
		name = "缅甸",
		{1973, "Flag of Burma (1948-1974).svg"},
		{2010, "Flag of Myanmar (1974-2010).svg"},
		"Flag of Myanmar.svg",
	},
	BIZ = {
		name = "伯利兹",
		{1981, "Flag of British Honduras (1919-1981).svg"},
		"Flag of Belize.svg",
	},
	BLR = {
		name = "白俄罗斯",
		{2012, "Flag of Belarus (1995-2012).svg"},
		"Flag of Belarus.svg",
	},
	BNB = {
		name = "北婆羅洲",
		"Flag of North Borneo 1948-1963.png",
	},
	BOH = {
		name = "波希米亚",
		"Flag of Bohemia.svg",
		["Summer Olympics"] = {
			[1912] = "Bohemian Olympic Flag (1912).png",
		},
	},
	BOL = {
		name = "玻利維亞",
		"Flag of Bolivia.svg",
	},
	BOT = {
		name = "波札那",
		"Flag of Botswana.svg",
	},
	BRA = {
		name = "巴西",
		{1960, "Flag of Brazil (1889-1960).svg"},
		{1968, "Flag of Brazil (1960-1968).svg"},
		{1992, "Flag of Brazil (1968-1992).svg"},
		"Flag of Brazil.svg",
	},
	BRN = {
		name = "巴林",
		{2001, "Flag of Bahrain (1972-2002).svg"},
		"Flag of Bahrain.svg",
	},
	BRU = {
		name = "汶莱",
		"Flag of Brunei.svg",
	},
	BUL = {
		name = "保加利亚",
		{1948, "Flag of Bulgaria (1946-1948).svg"},
		{1967, "Flag of Bulgaria (1948-1967).svg"},
		{1971, "Flag of Bulgaria (1967-1971).svg"},
		{1990, "Flag of Bulgaria (1971-1990).svg"},
		"Flag of Bulgaria.svg",
	},
	BUR = {
		name = "布吉納法索",
		"Flag of Burkina Faso.svg",
	},
	BWI = {
		name = "British West Indies",
		"Flag of the West Indies Federation.svg",
	},
	CAF = {
		name = "中非共和國",
		"Flag of the Central African Republic.svg",
	},
	CAM = {
		name = "柬埔寨",
		{1970, "Flag of Cambodia.svg"},
		{1975, "Flag of the Khmer Republic.svg"},
		{1989, "Flag of the People's Republic of Kampuchea.svg"},
		{1991, "Flag of the State of Cambodia.svg"},
		{1993, "Flag of Cambodia under UNTAC.svg"},
		"Flag of Cambodia.svg",
	},
	CAN = {
		name = "加拿大",
		{1921, "Canadian Red Ensign 1868-1921.svg"},
		{1957, "Canadian Red Ensign 1921-1957.svg"},
		{1965, "Canadian Red Ensign (1957-1965).svg"},
		"Flag of Canada.svg",
		["Summer Olympics"] = {
			[1936] = "Canadian Red Ensign 1921-1957 (with disc).svg",
		},
	},
	CAY = {
		name = "開曼群島",
		{1999, "Flag of the Cayman Islands (pre-1999).svg"},
		"Flag of the Cayman Islands.svg",
	},
	CEY = {
		name = "斯里蘭卡",
		{1948, "British Ceylon flag.png"},
		{1951, "Flag of Ceylon (1948-1951).svg"},
		{1971, "Flag of Ceylon (1951-1972).svg"},
		"Flag of Sri Lanka.svg",
	},
	CGO = {
		name = "刚果",
		{1988, "Flag of the People's Republic of Congo.svg"},
		"Flag of the Republic of the Congo.svg",
	},
	CHA = {
		name = "乍得",
		"Flag of Chad.svg",
	},
	CHI = {
		name = "智利",
		"Flag of Chile.svg",
	},
	CHN = {
		name = "中国",
		"Flag of the People's Republic of China.svg",
	},
	CIV = {
		name = "科特迪瓦",
		"Flag of Côte d'Ivoire.svg",
	},
	CMR = {
		name = "喀麦隆",
		{1975, "Flag of Cameroon (1961-1975).svg"},
		"Flag of Cameroon.svg",
	},
	COD = {
		name = "刚果民主共和国",
		{1971, "Flag of Congo-Kinshasa (1966-1971).svg"},
		{1996, "Flag of Zaire.svg"},
		{2003, "Flag of the Democratic Republic of the Congo (1997-2003).svg"},
		{2006, "Flag of the Democratic Republic of the Congo (2003-2006).svg"},
		"Flag of the Democratic Republic of the Congo.svg",
	},
	COK = {
		name = "库克群岛",
		{1979, "Flag of the Cook Islands (1973-1979).svg"},
		"Flag of the Cook Islands.svg",
	},
	COL = {
		name = "哥伦比亚",
		"Flag of Colombia.svg",
	},
	COM = {
		name = "葛摩",
		{1996, "Flag of the Comoros (1992-1996).svg"},
		{2001, "Flag of the Comoros (1996-2001).svg"},
		"Flag of the Comoros.svg",
	},
	COR = {
		name = "南北韓聯隊",
		"Unification flag of Korea.svg",
		["Winter Olympics"] = {
			[2018] = "Unification flag of Korea (pre 2006).svg",
		},
	},
	CPV = {
		name = "佛得角",
		"Flag of Cape Verde.svg",
	},
	CRC = {
		name = "哥斯达黎加",
		"Flag of Costa Rica.svg",
	},
	CRO = {
		name = "克罗地亚",
		"Flag of Croatia.svg",
	},
	CUB = {
		name = "古巴",
		"Flag of Cuba.svg",
	},
	CUR = {
		name = "库拉索",
		"Flag of Curaçao.svg",
	},
	CUW = {
		name = "库拉索",
		"Flag of Curaçao.svg",
	},
	CYP = {
		name = "賽普勒斯",
		{2006, "Flag of Cyprus (1960-2006).svg"},
		"Flag of Cyprus.svg",
	},
	CZE = {
		name = "捷克",
		"Flag of the Czech Republic.svg",
	},
	DAH = {
		name = "Dahomey",
		"Flag of Benin.svg",
	},
	DEN = {
		name = "丹麦",
		"Flag of Denmark.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	DJI = {
		name = "吉布提",
		"Flag of Djibouti.svg",
	},
	DMA = {
		name = "多米尼克",
		{1965, "Flag of Dominica, 1955-1965.png"},
		{1978, "Flag of Dominica, 1965-1978.png"},
		{1981, "Flag of Dominica (1978-1981).svg"},
		{1988, "Flag of Dominica (1981-1988).svg"},
		{1990, "Flag of Dominica (1988-1990).svg"},
		"Flag of Dominica.svg",
	},
	DOM = {
		name = "多明尼加",
		"Flag of the Dominican Republic.svg",
	},
	ECU = {
		name = "厄瓜多尔",
		"Flag of Ecuador.svg",
	},
	EGY = {
		name = "埃及",
		{1914, "Flag of Egypt (1844-1867).svg"},
		{1922, "Flag of Egypt (1882-1922).svg"},
		{1952, "Flag of Egypt (1922–1958).svg"},
		{1958, "Flag of Egypt (1952-1958).svg"},
		{1971, "Flag of the United Arab Republic.svg"},
		{1984, "Flag of Egypt (1972-1984).svg"},
		"Flag of Egypt.svg",
	},
	ENG = {
		name = "英格兰",
		"Flag of England.svg",
	},
	ERI = {
		name = "厄立特里亚",
		"Flag of Eritrea.svg",
	},
	ESA = {
		name = "萨尔瓦多",
		"Flag of El Salvador.svg",
	},
	ESP = {
		name = "西班牙",
		{1931, "Flag of Spain (1785-1873 and 1875-1931).svg"},
		{1939, "Flag of Spain (1931 - 1939).svg"},
		{1977, "Flag of Spain (1945 - 1977).svg"},
		{1981, "Flag of Spain (1977 - 1981).svg"},
		"Flag of Spain.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	EST = {
		name = "爱沙尼亚",
		"Flag of Estonia.svg",
	},
	ETH = {
		name = "埃塞俄比亚",
		{1974, "Flag of Ethiopia (1897-1936; 1941-1974).svg"},
		{1975, "Flag of Ethiopia (1974-1975).svg"},
		{1987, "Flag of Ethiopia (1975–1987).svg"},
		{1991, "Flag of Ethiopia (1987–1991).svg"},
		{1996, "Flag of Ethiopia (1991-1996).svg"},
		"Flag of Ethiopia.svg",
	},
	EUA = {
		name = "德国联合",
		{1959, "Flag of Germany.svg"},
		"Flag of the German Olympic Team (1960-1968).svg",
	},
	EUN = {
		name = "独联体",
		"Olympic flag.svg",
		["Winter Paralympics"] = "Paralympics logo 1988-94.svg",
		["Paralympics"] = "Paralympics logo 1988-94.svg",
		["Summer Paralympics"] = "Paralympics logo 1988-94.svg",
	},
	FAI = {
		name = "福克兰群岛",
		{1999, "Flag of the Falkland Islands (1948-1999).svg"},
		"Flag of the Falkland Islands.svg",
	},
	FAR = {
		name = "法罗群岛",
		"Flag of the Faroe Islands.svg",
	},
	FIJ = {
		name = "斐濟",
		{1970, "Flag of Fiji 1924-1970.svg"},
		"Flag of Fiji.svg",
	},
	FIN = {
		name = "芬兰",
		{1912, "Flag of Russia.svg"},
		"Flag of Finland.svg",
	},
	FINA = {
		name = "FINA Independent Athletes",
		"Fédération International de Natation Amateur flag.gif"
	},
	FRA = {
		name = "法国",
		"Flag of France.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	FRG = {
		name = "西德",
		{1959, "Flag of Germany.svg"},
		{1968, "Flag of the German Olympic Team (1960-1968).svg"},
		"Flag of Germany.svg",
	},
	FRN = {
		name = "羅德西亞與尼亞薩蘭聯邦",
		"Flag of the Federation of Rhodesia and Nyasaland.svg",
	},
	FRO = {
		name = "法罗群岛",
		"Flag of the Faroe Islands.svg",
	},
	FSA = {
		name = "南阿拉伯聯邦",
		"Flag of the Federation of South Arabia.svg",
	},
	FSM = {
		name = "密克罗尼西亚群岛",
		"Flag of the Federated States of Micronesia.svg",
	},
	GAB = {
		name = "加蓬",
		"Flag of Gabon.svg",
	},
	GAM = {
		name = "冈比亚",
		"Flag of The Gambia.svg",
	},
	GBR = {
		name = "英国",
		"Flag of the United Kingdom.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	GBS = {
		name = "幾內亞比索",
		"Flag of Guinea-Bissau.svg",
	},
	GCO = {
		name = "黄金海岸",
		"Flag of the Gold Coast.svg",
	},
	GDR = {
		name = "東德",
		{1959, "Flag of East Germany.svg"},
		{1968, "Flag of the German Olympic Team (1960-1968).svg"},
		"Flag of East Germany.svg",
	},
	GEO = {
		name = "喬治亞",
		{2003, "Flag of Georgia (1990-2004).svg"},
		"Flag of Georgia.svg",
	},
	GEQ = {
		name = "赤道几内亚",
		"Flag of Equatorial Guinea.svg",
	},
	GER = {
		name = "德国",
		{1912, "Flag of the German Empire.svg"},
		{1932, "Flag of Germany (3-2 aspect ratio).svg"},
		{1945, "Flag of the German Reich (1935–1945).svg"},
		"Flag of Germany.svg",
	},
	GHA = {
		name = "加纳",
		{1960, "Flag of the Gold Coast.svg"},
		{1962, "Flag of the Union of African States (1961-1962).svg"},
		{1966, "Flag of Ghana (1964-1966).svg"},
		"Flag of Ghana.svg",
	},
	GIB = {
		name = "直布罗陀",
		{1981, "Government Ensign of Gibraltar 1939-1999.svg"},
		"Flag of Gibraltar.svg",
	},
	GRE = {
		name = "希腊",
		{1969, "Flag of Greece (1828-1978).svg"},
		{1975, "Flag of Greece (1970-1975).svg"},
		{1978, "Flag of Greece (1828-1978).svg"},
		"Flag of Greece.svg",
	},
	GRN = {
		name = "格林纳达",
		{1974, "Flag of Grenada 1967.svg"},
		"Flag of Grenada.svg",
	},
	GUA = {
		name = "危地马拉",
		"Flag of Guatemala.svg",
	},
	GUE = {
		name = "根西",
		{1985, "Flag of Guernsey (1936).svg"},
		"Flag of Guernsey.svg",
	},
	GUI = {
		name = "几内亚",
		"Flag of Guinea.svg",
	},
	GUM = {
		name = "關島",
		"Flag of Guam.svg",
	},
	GUY = {
		name = "圭亚那",
		{1906, "Flag of British Guiana (1875-1906).png"},
		{1919, "Flag of British Guiana (1906-1919).png"},
		{1955, "Flag of British Guiana (1919-1955).png"},
		{1966, "Flag of British Guiana (1955-1966).svg"},
		"Flag of Guyana.svg",
	},
	HAI = {
		name = "海地",
		{1963, "Flag of Haiti.svg"},
		{1986, "Flag of Haiti (1964-1986).svg"},
		"Flag of Haiti.svg",
	},
	HBR = {
		name = "英屬宏都拉斯",
		"Flag of British Honduras.svg",
	},
	HKG = {
		name = "香港",
		{1955, "Flag of Hong Kong 1876.svg"},
		{1959, "Flag of Hong Kong 1955.svg"},
                name = "中國香港",
		{1997, "Flag of Hong Kong (1959-1997).svg"},
		"Flag of Hong Kong.svg",
	},
	HON = {
		name = "洪都拉斯",
		"Flag of Honduras.svg",
	},
	HUN = {
		name = "匈牙利",
		{1918, "Flag of Hungary (1867-1918).svg"},
		{1946, "Flag of Hungary (1915-1918, 1919-1946; 3-2 aspect ratio).svg"},
		{1949, "Flag of Hungary (1946-1949, 1956-1957).svg"},
		{1955, "Flag of Hungary (1949-1956).svg"},
		{1957, "Flag of Hungary (1946-1949, 1956-1957).svg"},
		"Flag of Hungary.svg",
	},
	IFS = {
		name = "爱尔兰自由邦",
		"Flag of Ireland.svg",
	},
	INA = {
		name = "印度尼西亚",
		"Flag of Indonesia.svg",
	},
	IND = {
		name = "印度",
		{1946, "British Raj Red Ensign.svg"},
		{2012, "Flag of India.svg"},
		{2013, "Olympic flag.svg"},
		"Flag of India.svg",
	},
	IOA = {
		name = "獨立參賽者",
		"Olympic flag.svg",
	},
	IOC = {
		name = "科威特運動員",
		"Olympic flag.svg",
	},
	IOM = {
		name = "曼島",
		"Flag of the Isle of Man.svg",
	},
	IOP = {
		name = "獨立參賽者",
		"Olympic flag.svg",
	},
	['IOP, IOA, OAR'] = {
		name = "Independent Olympians",
		"Olympic flag.svg",
	},
	
	IPA = {
		name = "個人殘奧運動員",
		"Paralympic flag.svg",
	},
	IPP = {
		name = "獨立殘奧運動員",
		"Paralympics logo 1988-94.svg",
	},
	IRE = {
		name = "爱尔兰",
		"Green harp flag of Ireland.svg",
	},
	IRI = {
		name = "伊朗",
		{1932, "Early 20th Century Qajar Flag.svg"},
		{1964, "State Flag of Iran (1933-1964).svg"},
		{1980, "State Flag of Iran (1964-1980).svg"},
		"Flag of Iran.svg",
		["Summer Olympics"] = {
			[1964] = "State Flag of Iran (1964-1980).svg",
		},
	},
	IRL = {
		name = "爱尔兰",
		"Flag of Ireland.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	IRN = {
		name = "伊朗",
		{1932, "Early 20th Century Qajar Flag.svg"},
		{1964, "State Flag of Iran (1933-1964).svg"},
		{1980, "State Flag of Iran (1964-1980).svg"},
		"Flag of Iran.svg",
		["Summer Olympics"] = {
			[1964] = "State Flag of Iran (1964-1980).svg",
		},
	},
	IRQ = {
		name = "伊拉克",
		{1959, "Flag of Iraq (1921–1959).svg"},
		{1963, "Flag of Iraq (1959-1963).svg"},
		{1991, "Flag of Iraq (1963-1991); Flag of Syria (1963-1972).svg"},
		{2003, "Flag of Iraq (1991-2004).svg"},
		{2007, "Flag of Iraq (2004-2008).svg"},
		"Flag of Iraq.svg",
	},
	ISL = {
		name = "冰岛",
		{1915, "Flag of Denmark.svg"},
		{1944, "Light Blue Flag of Iceland.svg"},
		"Flag of Iceland.svg",
	},
	ISR = {
		name = "以色列",
		"Flag of Israel.svg",
	},
	ISV = {
		name = "维尔京群岛",
		"Flag of the United States Virgin Islands.svg",
	},
	ITA = {
		name = "意大利",
		{1946, "Flag of Italy (1861-1946).svg"},
		{2002, "Flag of Italy.svg"},
		{2006, "Flag of Italy (2003-2006).svg"},
		"Flag of Italy.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	IVB = {
		name = "英屬維爾京群島",
		"Flag of the British Virgin Islands.svg",
	},
	JAM = {
		name = "牙买加",
		{1957, "Flag of Jamaica (1906-1957).svg"},
		{1962, "Flag of Jamaica (1957-1962).svg"},
		"Flag of Jamaica.svg",
	},
	JER = {
		name = "澤西",
		{1980, "Flag of Jersey (pre 1981).svg"},
		"Flag of Jersey.svg",
	},
	JOR = {
		name = "约旦",
		"Flag of Jordan.svg",
	},
	JPN = {
		name = "日本",
		{1999, "Flag of Japan (1870-1999).svg"},
		"Flag of Japan.svg",
	},
	KAZ = {
		name = "哈萨克",
		"Flag of Kazakhstan.svg",
	},
	KEN = {
		name = "肯尼亚",
		{1963, "Flag of British East Africa.svg"},
		"Flag of Kenya.svg",
	},
	KGZ = {
		name = "吉尔吉斯",
		"Flag of Kyrgyzstan.svg",
	},
	KHM = {
		name = "高棉共和國",
		"Flag of the Khmer Republic.svg",
	},
	KIR = {
		name = "基里巴斯",
		"Flag of Kiribati.svg",
	},
	KOR = {
		name = "韩国",
		{1947, "Flag of South Korea (1945-1948).svg"},
		{1949, "Flag of South Korea (1948-1949).svg"},
		{1997, "Flag of South Korea (1984-1997).svg"},
		"Flag of South Korea.svg",
	},
	KOS = {
		name = "科索沃",
		"Flag of Kosovo.svg",
	},
	KSA = {
		name = "沙特阿拉伯",
		{1973, "Flag of Saudi Arabia (1938-1973).svg"},
		"Flag of Saudi Arabia.svg",
	},
	KUW = {
		name = "科威特",
		"Flag of Kuwait.svg",
	},
	LAO = {
		name = "老挝",
		{1975, "Flag of Laos (1952-1975).svg"},
		"Flag of Laos.svg",
	},
	LAT = {
		name = "拉脫維亞",
		"Flag of Latvia.svg",
	},
	LBA = {
		name = "利比亚",
		{1968, "Flag of Libya (1951).svg"},
		{1972, "Flag of Libya (1969–1972).svg"},
		{1977, "Flag of Libya (1972–1977).svg"},
		{2011, "Flag of Libya (1977-2011).svg"},
		"Flag of Libya.svg",
	},
	LBN = {
		name = "黎巴嫩",
		"Flag of Lebanon.svg",
	},
	LBR = {
		name = "利比里亚",
		"Flag of Liberia.svg",
	},
	LCA = {
		name = "圣卢西亚",
		{1967, "Flag of Saint Lucia (1939-1967).svg"},
		{1979, "Flag of Saint Lucia (1967-1979).svg"},
		{2002, "Flag of Saint Lucia (1979-2002).svg"},
		"Flag of Saint Lucia.svg",
	},
	LES = {
		name = "莱索托",
		{1987, "Flag of Lesotho (1966).svg"},
		{2006, "Flag of Lesotho (1987-2006).svg"},
		"Flag of Lesotho.svg",
	},
	LIB = {
		name = "黎巴嫩",
		"Flag of Lebanon.svg",
	},
	LIE = {
		name = "列支敦斯登",
		{1921, "Flag of Liechtenstein (1852-1921).svg"},
		{1937, "Flag of Liechtenstein (1921-1937).svg"},
		"Flag of Liechtenstein.svg",
	},
	LTU = {
		name = "立陶宛",
		{1940, "Flag of Lithuania (1918-1940).svg"},
		{2004, "Flag of Lithuania (1988-2004).svg"},
		"Flag of Lithuania.svg",
	},
	LUX = {
		name = "卢森堡",
		"Flag of Luxembourg.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	MAC = {
		name = "中國澳門",
		{1999, "Bandeira do Leal Senado.svg"},
		"Flag of Macau.svg",
	},
	MAD = {
		name = "马达加斯加",
		"Flag of Madagascar.svg",
	},
	MAL = {
		name = "馬來亞",
		"Flag of Malaya.svg",
	},
	MAR = {
		name = "摩洛哥",
		"Flag of Morocco.svg",
	},
	MAS = {
		name = "马来西亚",
		{1963, "Flag of Malaya.svg"},
		"Flag of Malaysia.svg",
	},
	MAW = {
		name = "马拉维",
		{2009, "Flag of Malawi.svg"},
		{2012, "Flag of Malawi (2010-2012).svg"},
		"Flag of Malawi.svg",
	},
	MDA = {
		name = "摩尔多瓦",
		"Flag of Moldova.svg",
	},
	MDV = {
		name = "马尔代夫",
		"Flag of Maldives.svg",
	},
	MEX = {
		name = "墨西哥",
		{1916, "Flag of Mexico (1893-1916).svg"},
		{1934, "Flag of the United Mexican States (1916-1934).svg"},
		{1968, "Flag of Mexico (1934-1968).svg"},
		"Flag of Mexico.svg",
	},
	MGL = {
		name = "蒙古",
		{1991, "Flag of the People's Republic of Mongolia (1940-1992).svg"},
		"Flag of Mongolia.svg",
		["Winter Olympics"] = {
			[1992] = "Flag of the People's Republic of Mongolia (1940-1992).svg",
		},
	},
	MHL = {
		name = "馬紹爾群島",
		"Flag of the Marshall Islands.svg",
	},
	MIX = {
		name = "混合國家",
		"Olympic flag.svg",
	},
	MKD = {
		name = "馬其頓",
		"Flag of Macedonia.svg",
	},
	MLI = {
		name = "马里",
		"Flag of Mali.svg",
	},
	MLT = {
		name = "马耳他",
		{1943, "Flag of Malta (1923-1943).svg"},
		{1964, "Flag of Malta (1943-1964).svg"},
		"Flag of Malta.svg",
	},
	MNE = {
		name = "蒙特內哥羅",
		"Flag of Montenegro.svg",
	},
	MNT = {
		name = "蒙塞拉特島",
		"Flag of Montserrat.svg",
	},
	MON = {
		name = "摩纳哥",
		"Flag of Monaco.svg",
	},
	MOZ = {
		name = "莫桑比克",
		{1983, "Flag of Mozambique (1975-1983).svg"},
		"Flag of Mozambique.svg",
	},
	MRI = {
		name = "毛里求斯",
		{1923, "Flag of Mauritius 1906.svg"},
		{1968, "Flag of Mauritius 1923.svg"},
		"Flag of Mauritius.svg",
	},
	MTN = {
		name = "毛里塔尼亚",
		"Flag of Mauritania.svg",
	},
	MYA = {
		name = "缅甸",
		{1973, "Flag of Burma (1948-1974).svg"},
		{2010, "Flag of Myanmar (1974-2010).svg"},
		"Flag of Myanmar.svg",
	},
	NAM = {
		name = "纳米比亚",
		"Flag of Namibia.svg",
	},
	NBO = {
		name = "北婆羅洲",
		"Flag of North Borneo 1948-1963.png",
	},
	NCA = {
		name = "尼加拉瓜",
		"Flag of Nicaragua.svg",
	},
	NCL = {
		name = "新喀里多尼亞",
		"Flag of New Caledonia.svg",
	},
	NED = {
		name = "荷兰",
		"Flag of the Netherlands.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	NEP = {
		name = "尼泊尔",
		"Flag of Nepal.svg",
	},
	NEW = {
		name = "紐芬蘭與拉布拉多省",
		"Newfoundland Red Ensign.png",
	},
	NFI = {
		name = "诺福克岛",
		"Flag of Norfolk Island.svg",
	},
	NGR = {
		name = "奈及利亞",
		{1960, "Flag of British Colonial Nigeria.svg"},
		"Flag of Nigeria.svg",
	},
	NIC = {
		name = "尼加拉瓜",
		"Flag of Nicaragua.svg",
	},
	NIG = {
		name = "尼日尔",
		"Flag of Niger.svg",
	},
	NIR = {
		name = "北爱尔兰",
		"Ulster banner.svg",
	},
	NIU = {
		name = "紐埃",
		"Flag of Niue.svg",
	},
	NMI = {
		name = "北马里亚纳群岛",
		"Flag of the Northern Mariana Islands.svg",
	},
	NOR = {
		name = "挪威",
		"Flag of Norway.svg",
	},
	NPA = {
		name = "中立殘奧運動員",
		"Paralympic flag.svg",
	},
	NRH = {
		name = "北羅德西亞",
		"Flag of Northern Rhodesia (1939-1953).svg",
	},
	NRU = {
		name = "諾魯",
		"Flag of Nauru.svg",
	},
	NZL = {
		name = "新西兰",
		"Flag of New Zealand.svg",
		["Summer Olympics"] = {
			[1980] = "Flag of New Zealand Olympic Committee (1979-1994).svg",
		},
	},
	OAR = {
		name = "俄罗斯奥林匹克运动员",
		"Olympic flag.svg",
        },
	OMA = {
		name = "阿曼",
		{1995, "Flag of Oman (1970-1995).svg"},
		"Flag of Oman.svg",
	},
	PAK = {
		name = "巴基斯坦",
		"Flag of Pakistan.svg",
	},
	PAN = {
		name = "巴拿马",
		"Flag of Panama.svg",
	},
	PAR = {
		name = "巴拉圭",
		{1954, "Flag of Paraguay (1842-1954).svg"},
		{1988, "Flag of Paraguay (1954-1988).svg"},
		{1990, "Flag of Paraguay (1988-1990).svg"},
		{2013, "Flag of Paraguay (1990-2013).svg"},
		"Flag of Paraguay.svg",
	},
	PER = {
		name = "秘鲁",
		{1950, "Flag of Peru (1825-1950).svg"},
		"Flag of Peru.svg",
	},
	PHI = {
		name = "菲律宾",
		{1936, "Flag of the Philippines (1919-1936).svg"},
		{1984, "Flag of the Philippines (navy blue).svg"},
		{1986, "Flag_of_the_Philippines_(light_blue).svg"},
		{1997, "Flag of the Philippines (navy blue).svg"},
		"Flag of the Philippines.svg",
		["Asian Games"] = {
			[1986] = "Flag of the Philippines (navy blue).svg",
		},
	},
	PLE = {
		name = "巴勒斯坦",
		"Flag of Palestine.svg",
	},
	PLW = {
		name = "帛琉",
		"Flag of Palau.svg",
	},
	PNG = {
		name = "巴布亚新几内亚",
		{1965, "Flag of the Territory of New Guinea.svg"},
		{1970, "Flag of Papua New Guinea 1965.svg"},
		"Flag of Papua New Guinea.svg",
	},
	POL = {
		name = "波兰",
		{1928, "Flag of Poland (1919-1928).svg"},
		{1980, "Flag of Poland (1928-1980).svg"},
		"Flag of Poland.svg",
	},
	POR = {
		name = "葡萄牙",
		"Flag of Portugal.svg",
		["Summer Olympics"] = {
			[1980] = "Flag of Portugal-1980-Olympics.svg",
		},
	},
	PRK = {
		name = "朝鮮",
		"Flag of North Korea.svg",
	},
	PUR = {
		name = "波多黎各",
		{1951, "Puerto Rico Azul Celeste.png"},
		{1995, "Flag of Puerto Rico (1952-1995).svg"},
		"Flag of Puerto Rico.svg",
		["Summer Olympics"] = {
			[1948] = "Puerto rico national sport flag.svg",
			[1952] = "Puerto rico national sport flag.svg",
			[1980] = "Olympic flag.svg",
		},
	},
	PYF = {
		name = "法屬玻里尼西亞",
		"Flag of French Polynesia.svg",
	},
	QAT = {
		name = "卡塔尔",
		"Flag of Qatar.svg",
	},
	RHO = {
		name = "羅德西亞",
		{1953, "Flag of Southern Rhodesia.svg"},
		{1963, "Flag of the Federation of Rhodesia and Nyasaland.svg"},
		{1968, "Flag of Rhodesia (1964).svg"},
		"Flag of Rhodesia.svg",
	},
	ROA = {
		name = "难民代表团",
		"Olympic flag.svg",
	},
	ROC = {
		name = "中華民國",
		{1928, "Flag of the Republic of China (1912-1928).svg"},
		"Flag of the Republic of China.svg",
	},
	ROM = {
		name = "羅馬尼亞",
		{1948, "Flag of Romania.svg"},
		{1952, "Flag of Romania (1948-1952).svg"},
		{1965, "Flag of Romania (1952-1965).svg"},
		{1989, "Flag of Romania (1965-1989).svg"},
		"Flag of Romania.svg",
	},
	ROT = {
		name = "难民代表团",
		"Olympic flag.svg",
	},
	ROU = {
		name = "羅馬尼亞",
		{1948, "Flag of Romania.svg"},
		{1952, "Flag of Romania (1948-1952).svg"},
		{1965, "Flag of Romania (1952-1965).svg"},
		{1989, "Flag of Romania (1965-1989).svg"},
		"Flag of Romania.svg",
	},
	RSA = {
		name = "南非",
		{1912, "Flag of the United Kingdom.svg"},
		{1928, "Red Ensign of South Africa (1912-1928).svg"},
		{1994, "Flag of South Africa (1928-1994).svg"},
		"Flag of South Africa.svg",
		["Winter Olympics"] = {
			[1994] = "South African Olympic Flag 1994.gif",
		},
		["Summer Olympics"] = {
			[1992] = "South African Olympic Flag.svg",
		},
	},
	RU1 = {
		name = "俄罗斯帝国",
		"Flag of Russia.svg",
	},
	RUS = {
		name = "俄罗斯",
		"Flag of Russia.svg",
	},
	RWA = {
		name = "卢旺达",
		{1961, "Flag of Rwanda (1959-1961).svg"},
		{2001, "Flag of Rwanda (1962-2001).svg"},
		"Flag of Rwanda.svg",
	},
	SAA = {
		name = "Saar",
		"Flag of Saar (1947–1956).svg",
	},
	SAF = {
		name = "南非",
		{1912, "Flag of the United Kingdom.svg"},
		{1928, "Red Ensign of South Africa (1912-1928).svg"},
		{1994, "Flag of South Africa (1928-1994).svg"},
		"Flag of South Africa.svg",
		["Winter Olympics"] = {
			[1994] = "South African Olympic Flag 1994.gif",
		},
		["Summer Olympics"] = {
			[1992] = "South African Olympic Flag.svg",
		},
	},
	SAM = {
		name = "萨摩亚",
		"Flag of Samoa.svg",
	},
	SAR = {
		name = "砂拉越",
		"Flag of the Crown Colony of Sarawak (1946).svg",
	},
	SCG = {
		name = "塞爾維亞與蒙特內哥羅",
		"Flag of Serbia and Montenegro.svg",
	},
	SCN = {
		name = "聖克里斯多福-尼維斯-安圭拉",
		"Flag of Saint Christopher-Nevis-Anguilla.svg",
	},
	SCO = {
		name = "蘇格蘭",
		"Flag of Scotland.svg",
	},
	SEN = {
		name = "塞内加尔",
		"Flag of Senegal.svg",
	},
	SEY = {
		name = "塞舌尔",
		{1996, "Flag of the Seychelles (1977-1996).svg"},
		"Flag of Seychelles.svg",
	},
	SGP = {
		name = "新加坡",
		{1959, "Flag of Singapore (1946-1959).svg"},
		"Flag of Singapore.svg",
	},
	SHE = {
		name = "圣赫勒拿",
		{1984, "Flag of Saint Helena (1874-1984).svg"},
		"Flag of Saint Helena.svg",
	},
	SHN = {
		name = "圣赫勒拿",
		{1984, "Flag of Saint Helena (1874-1984).svg"},
		"Flag of Saint Helena.svg",
	},
	SIN = {
		name = "新加坡",
		{1959, "Flag of Singapore (1946-1959).svg"},
		"Flag of Singapore.svg",
	},
	SKN = {
		name = "聖克里斯多福及尼維斯",
		{1983, "Flag of Saint Christopher-Nevis-Anguilla.svg"},
		"Flag of Saint Kitts and Nevis.svg",
	},
	SLE = {
		name = "塞拉利昂",
		{1961, "Flag of Sierra Leone 1916-1961.gif"},
		"Flag of Sierra Leone.svg",
	},
	SLO = {
		name = "斯洛文尼亚",
		"Flag of Slovenia.svg",
	},
	SMR = {
		name = "圣马力诺",
		{2010, "Flag of San Marino (before 2011).svg"},
		"Flag of San Marino.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	SOL = {
		name = "所罗门群岛",
		"Flag of the Solomon Islands.svg",
	},
	SOM = {
		name = "索马里",
		"Flag of Somalia.svg",
	},
	SRB = {
		name = "塞尔维亚",
		{1918, "State Flag of Serbia (1882-1918).svg"},
		{1944, "Flag of Serbia, 1941-1944.svg"},
		{1992, "Flag of SR Serbia.svg"},
		{2004, "Flag of Serbia (1992-2004).svg"},
		{2010, "Flag of Serbia (2004-2010).svg"},
		"Flag of Serbia.svg",
	},
	SRH = {
		name = "南羅德西亞",
		"Flag of Southern Rhodesia.svg",
	},
	SRI = {
		name = "斯里蘭卡",
		{1948, "British Ceylon flag.svg"},
		{1951, "Flag of Ceylon (1948-1951).svg"},
		{1971, "Flag of Ceylon (1951-1972).svg"},
		"Flag of Sri Lanka.svg",
	},
	SSD = {
		name = "南蘇丹",
		"Flag of South Sudan.svg",
	},
	STP = {
		name = "圣多美和普林西比",
		"Flag of Sao Tome and Principe.svg",
	},
	SUD = {
		name = "苏丹共和国",
		{1970, "Flag of Sudan (1956-1970).svg"},
		"Flag of Sudan.svg",
	},
	SUI = {
		name = "瑞士",
		"Flag of Switzerland.svg",
		["Summer Olympics"] = {
			[1980] = "Olympic flag.svg",
		},
	},
	SUR = {
		name = "蘇利南",
		{1975, "Flag of Dutch Guyana.svg"},
		"Flag of Suriname.svg",
	},
	SVG = {
		name = "圣文森特和格林纳丁斯",
		{1979, "Flag of Saint Vincent and the Grenadines (1907-1979).svg"},
		{1984, "Flag of Saint Vincent and the Grenadines (1979-1985).svg"},
		{1985, "Flag of Saint Vincent and the Grenadines (1985).svg"},
		"Flag of Saint Vincent and the Grenadines.svg",
	},
	SVK = {
		name = "斯洛伐克",
		"Flag of Slovakia.svg",
	},
	SWE = {
		name = "瑞典",
		{1905, "Swedish civil ensign (1844–1905).svg"},
		"Flag of Sweden.svg",
	},
	SWK = {
		name = "砂拉越",
		"Flag of the Crown Colony of Sarawak (1946).svg",
	},
	SWZ = {
		name = "斯威士兰",
		"Flag of Swaziland.svg",
	},
	SYR = {
		name = "叙利亚",
		{1958, "Flag of Syria (1932-1958; 1961-1963).svg"},
		{1961, "Flag of the United Arab Republic.svg"},
		{1963, "Flag of Syria (1932-1958; 1961-1963).svg"},
		{1972, "Flag of Iraq (1963-1991); Flag of Syria (1963-1972).svg"},
		{1980, "Flag of Syria (1972-1980).svg"},
		"Flag of Syria.svg",
	},
	TAG = {
		name = "坦噶尼喀",
		"Flag of Tanganyika.svg",
	},
	TAH = {
		name = "法屬玻里尼西亞",
		"Flag of French Polynesia.svg",
	},
	TAN = {
		name = "坦桑尼亚",
		{1964, "Flag of Tanganyika.svg"},
		"Flag of Tanzania.svg",
	},
	TCH = {
		name = "捷克斯洛伐克",
		"Flag of Czechoslovakia.svg",
	},
	TCI = {
		name = "特克斯和凯科斯群岛",
		"Flag of the Turks and Caicos Islands.svg",
	},
	TGA = {
		name = "東加",
		"Flag of Tonga.svg",
	},
	THA = {
		name = "泰国",
		"Flag of Thailand.svg",
	},
	TJK = {
		name = "塔吉克",
		"Flag of Tajikistan.svg",
	},
	TKL = {
		name = "托克劳",
		"Flag of Tokelau.svg",
	},
	TKM = {
		name = "土库曼",
		{1973, "Flag of Turkmen SSR (1956).svg"},
		{1991, "Flag of the Turkmen SSR.svg"},
		{1997, "Flag of Turkmenistan (1992-1997).svg"},
		{2001, "Flag of Turkmenistan (1997-2001).svg"},
		"Flag of Turkmenistan.svg",
	},
	TKS = {
		name = "特克斯和凯科斯群岛",
		"Flag of the Turks and Caicos Islands.svg",
	},
	TLS = {
		name = "东帝汶",
		"Flag of East Timor.svg",
	},
	TOG = {
		name = "多哥",
		"Flag of Togo.svg",
	},
	TON = {
		name = "東加",
		"Flag of Tonga.svg",
	},
	TPE = {
		name = "中华台北",
		{1979, "Flag of the Republic of China.svg"},
		"Flag of Chinese Taipei for Olympic games.svg",
		["奧林匹克運動會"] = "Flag of Chinese Taipei for Olympic games.svg",
		["夏季奧林匹克運動會"] = "Flag of Chinese Taipei for Olympic games.svg",
		["冬季奧林匹克運動會"] = "Flag of Chinese Taipei for Olympic games.svg",
		["亞洲帕拉運動會"] = "Chinese Taipei Paralympic Flag.svg",
		["夏季帕拉林匹克運動會"] = "Chinese Taipei Paralympic Flag.svg",
		["世界大學運動會"] = "Flag of Chinese Taipei for Universiade.svg",
		["夏季世界大學運動會"] = "Flag of Chinese Taipei for Universiade.svg",
		["冬季世界大學運動會"] = "Flag of Chinese Taipei for Universiade.svg",
                ["夏季殘奧會"] = "Chinese Taipei Paralympic Flag.svg",
                ["夏季傷殘奧林匹克運動會"] = "Chinese Taipei Paralympic Flag.svg",
                ["Olympics"] = "Flag of Chinese Taipei for Olympic games.svg",
		["Summer Olympics"] = "Flag of Chinese Taipei for Olympic games.svg",
		["Winter Olympics"] = "Flag of Chinese Taipei for Olympic games.svg",
		["Asian Para Games"] = "Chinese Taipei Paralympic Flag.svg",
		["Summer Paralympics"] = "Chinese Taipei Paralympic Flag.svg",
		["Universiade"] = "Flag of Chinese Taipei for Universiade.svg",
		["Summer Universiade"] = "Flag of Chinese Taipei for Universiade.svg",
		["Winter Universiade"] = "Flag of Chinese Taipei for Universiade.svg",

	},
	TRI = {
		name = "千里達及托巴哥",
		{1958, "Flag of Trinidad and Tobago 1889-1958.svg"},
		"Flag of Trinidad and Tobago.svg",
	},
	TTO = {
		name = "千里達及托巴哥",
		{1958, "Flag of Trinidad and Tobago 1889-1958.svg"},
		"Flag of Trinidad and Tobago.svg",
	},
	TUN = {
		name = "突尼西亞",
		{1999, "Pre-1999 Flag of Tunisia.svg"},
		"Flag of Tunisia.svg",
	},
	TUR = {
		name = "土耳其",
		{1936, "Flag of the Ottoman Empire.svg"},
		"Flag of Turkey.svg",
	},
	TUV = {
		name = "圖瓦盧",
		"Flag of Tuvalu.svg",
	},
	UAE = {
		name = "阿拉伯联合酋长国",
		"Flag of the United Arab Emirates.svg",
	},
	UAR = {
		name = "阿拉伯聯合共和國",
		"Flag of the United Arab Republic.svg",
	},
	UGA = {
		name = "乌干达",
		{1962, "Flag of the Uganda Protectorate.svg"},
		"Flag of Uganda.svg",
	},
	UKR = {
		name = "乌克兰",
		"Flag of Ukraine.svg",
	},
	URS = {
		name = "苏联",
		{1955, "Flag of the Soviet Union (1923-1955).svg"},
		{1980, "Flag of the Soviet Union (1955-1980).svg"},
		"Flag of the Soviet Union.svg",
	},
	URU = {
		name = "乌拉圭",
		"Flag of Uruguay.svg",
	},
	USA = {
		name = "美国",
		{1896, "US flag 44 stars.svg"},
		{1908, "US flag 45 stars.svg"},
		{1912, "US flag 46 stars.svg"},
		{1959, "US flag 48 stars.svg"},
		{1960, "US flag 49 stars.svg"},
		"Flag of the United States.svg",
	},
	UZB = {
		name = "乌兹别克",
		"Flag of Uzbekistan.svg",
	},
	VAN = {
		name = "瓦努阿图",
		"Flag of Vanuatu.svg",
	},
	VEN = {
		name = "委內瑞拉",
		{1930, "Flag of Venezuela (1905-1930).svg"},
		{1954, "Flag of Venezuela (1930-1954).svg"},
		{2006, "Flag of Venezuela (1954-2006).png"},
		"Flag of Venezuela.svg",
	},
	VIE = {
		name = "越南",
		{1975, "Flag of South Vietnam.svg"},
		"Flag of Vietnam.svg",
	},
	VIN = {
		name = "圣文森特和格林纳丁斯",
		{1979, "Flag of Saint Vincent and the Grenadines (1907-1979).svg"},
		{1984, "Flag of Saint Vincent and the Grenadines (1979-1985).svg"},
		{1985, "Flag of Saint Vincent and the Grenadines (1985).svg"},
		"Flag of Saint Vincent and the Grenadines.svg",
	},
	VNM = {
		name = "越南共和国",
		{1975, "Flag of South Vietnam.svg"},
		"Flag of Vietnam.svg",
	},
	VOL = {
		name = "Upper Volta",
		"Flag of Upper Volta.svg",
	},
	WAL = {
		name = "威爾士",
		{1952, "Flag of England.svg"},
		{1959, "Flag of Wales (1953-1959).svg"},
		"Flag of Wales 2.svg",
	},
	WLF = {
		name = "瓦利斯和富圖納",
		"Flag of Wallis and Futuna.svg",
	},
	WSM = {
		name = "萨摩亚",
		"Flag of Samoa.svg",
	},
	YAR = {
		name = "阿拉伯也门共和国",
		"Flag of North Yemen.svg",
	},
	YEM = {
		name = "也门",
		"Flag of Yemen.svg",
	},
	YMD = {
		name = "也门民主人民共和国",
		"Flag of South Yemen.svg",
	},
	YUG = {
		name = "南斯拉夫",
		{1941, "Flag of the Kingdom of Yugoslavia.svg"},
		{1946, "Flag of the Democratic Federal Yugoslavia.svg"},
		"Flag of SFR Yugoslavia.svg",
	},
	ZAI = {
		name = "薩伊",
		"Flag of Zaire.svg",
	},
	ZAM = {
		name = "赞比亚",
		{1953, "Flag of Northern Rhodesia (1939-1953).svg"},
		{1963, "Flag of the Federation of Rhodesia and Nyasaland.svg"},
		{1996, "Flag of Zambia (1964-1996).svg"},
		"Flag of Zambia.svg",
	},
	ZIM = {
		name = "辛巴威",
		{1953, "Flag of Southern Rhodesia.svg"},
		{1963, "Flag of the Federation of Rhodesia and Nyasaland.svg"},
		{1968, "Flag of Rhodesia (1964).svg"},
		{1978, "Flag of Rhodesia.svg"},
		{1979, "Flag of Zimbabwe Rhodesia.svg"},
		"Flag of Zimbabwe.svg",
	},
	ZZX = {
		name = "混合代表隊",
		"Olympic flag.svg",
	},
}

local function strip_to_nil(text)
	-- If text is a string, return its trimmed content, or nil if empty.
	-- Otherwise return text (which may, for example, be nil).
	if type(text) == 'string' then
		text = text:match('(%S.-)%s*$')
	end
	return text
end

local function yes(parameter)
	-- Return true if parameter should be interpreted as "yes".
	return ({ y = true, yes = true, on = true })[parameter]
end

local function getFlag(args, country)
	-- Return name of flag selected from country data (nil if none defined).
	local year = tonumber(args.year)
	local games = strip_to_nil(args.games)
	if games then
		local gdata = country[games]
		if gdata then
			if type(gdata) == 'string' then
				return gdata
			end
			if gdata[year] then
				return gdata[year]
			end
		end
	end
	for _, item in ipairs(country) do
		if type(item) == 'string' then
			return item
		end
		if year and year <= item[1] then
			return item[2]
		end
	end
end

local function main(frame)
	local args = frame.args
	local alias = args.alias
	local country = countries[alias]
	local function quit(message)
		if args.error then
			return args.error
		end
		error(message)
	end
	if not country then
		return quit('Invalid country alias: ' .. tostring(alias))
	end
	if yes(args.flag) then
		return getFlag(args, country) or quit('No flag defined for ' .. alias)
	else
		return country.name or quit('No name defined for ' .. alias)
	end
end

return { main = main }