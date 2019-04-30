return {

 -- crh (Crimean Tatar) cluster: crh-cyrl , crh-latn -> crh (Crimean Tatar)
 ['crh']        = {'crh-latn'},
 ['crh-cyrl']   = {'crh'}, 
 ['crh-latn']   = {'crh'},
 
 -- de (German) cluster:
 ['als']        = {'gsw', 'de'},    -- Alemannisch
 ['bar']        = {'de'},           -- Bavarian
 ['de-at']      = {'de'},           -- Austrian German
 ['de-ch']      = {'de'},           -- Swiss High German
 ['de-formal']  = {'de'},           -- German (formal address)
 ['dsb']        = {'de'},           -- Lower Sorbian
 ['frr']        = {'de'},           -- Northern Frisian
 ['hsb']        = {'de'},           -- Upper Sorbian
 ['ksh']        = {'de'},           -- Colognian
 ['lb']         = {'de'},           -- Luxembourgish
 ['nds']        = {'nds-nl', 'de'}, -- Low German
 ['nds-nl']     = {'nds', 'nl'},    -- Low Saxon (Netherlands)
 ['pdc']        = {'de'},           -- Deitsch
 ['pdt']        = {'nds', 'de'},    -- Plautdietsch
 ['pfl']        = {'de'},           -- Pälzisch
 ['sli']        = {'de'},           -- Lower Silesian
 ['stq']        = {'de'},           -- Seeltersk
 ['vmf']        = {'de'},           -- Upper Franconian
 
 -- es (Spanish) cluster
 ['an']         = {'es'},       -- Aragonese
 ['arn']        = {'es'},       -- Mapuche
 ['ay']         = {'es'},       -- Aymara
 ['cbk-zam']    = {'es'},       -- Chavacano de Zamboanga
 ['gn']         = {'es'},       -- Guarani
 ['lad']        = {'es'},       -- Ladino
 ['nah']        = {'es'},       -- Nahuatl
 ['qu']         = {'es'},       -- Quechua
 ['qug']        = {'qu', 'es'}, -- Runa shimi
 
 -- et (Estonian) cluster
 ['liv']         = {'et'},  -- Līvõ kēļ
 ['vep']         = {'et'},  -- Veps
 ['vro']         = {'et'},  -- Võro
 ['fio-vro']     = {'vro'}, -- Võro

 -- fa (Persian) cluster
 ['bcc']        = {'fa'},  -- Southern Balochi
 ['bqi']        = {'fa'},  -- Bakhtiari
 ['glk']        = {'fa'},  -- Gilaki
 ['mzn']        = {'fa'},  -- Mazandarani
 
 -- fi (Finnish) cluster:
 ['fit']        = {'fi'}, -- meänkieli
 ['vot']        = {'fi'}, -- Votic
 
 -- fr (French) cluster:
 ['bm']         = {'fr'}, -- Bambara
 ['br']         = {'fr'}, -- Breton
 ['co']         = {'fr'}, -- Corsican
 ['ff']         = {'fr'}, -- Fulah
 ['frc']        = {'fr'}, -- Cajun French
 ['frp']        = {'fr'}, -- Franco-Provençal
 ['ht']         = {'fr'}, -- Haitian
 ['ln']         = {'fr'}, -- Lingala
 ['mg']         = {'fr'}, -- Malagasy
 ['pcd']        = {'fr'}, -- Picard
 ['sg']         = {'fr'}, -- Sango
 ['ty']         = {'fr'}, -- Tahitian
 ['wa']         = {'fr'}, -- Walloon
 ['wo']         = {'fr'}, -- Wolof

 -- hi (Hindi) cluster
 ['anp']         = {'hi'}, -- Angika
 ['may']         = {'hi'}, -- Maithili
 ['sa']          = {'hi'}, -- Sanskrit

 -- hif (Fiji Hindi) cluster: hif-deva , hif-latn -> hif (Fiji Hindi)
 ['hif']        = {'hif-latn'},
 ['hif-deva']   = {'hif'}, 
 ['hif-latn']   = {'hif'}, 
 
 -- id (Indonesian) cluster
 ['min']        = {'id'},       -- Minangkabau
 ['ace']        = {'id'},       -- Achinese
 ['bug']        = {'id'},       -- Buginese
 ['bjn']        = {'id'},       -- Banjar
 ['jv']         = {'id'},       -- Javanese
 ['su']         = {'id'},       -- Sundanese
 ['map-bms']    = {'jv', 'id'}, -- Basa Banyumasan
 
 -- ike (Eastern Canadian Inuktitut) cluster: ike-cans , ike-latn -> ike (Eastern Canadian Inuktitut)
 ['ike-cans']   = {'ik'}, 
 ['ike-latn']   = {'ik'}, 
 
 -- it (Italian) cluster
 ['egl']        = {'it'}, -- Emiliàn
 ['eml']        = {'it'}, -- Emiliano-Romagnolo
 ['fur']        = {'it'}, -- Friulian
 ['lij']        = {'it'}, -- Ligure
 ['lmo']        = {'it'}, -- lumbaart
 ['nap']        = {'it'}, -- Neapolitan
 ['pms']        = {'it'}, -- Piedmontese
 ['rgn']        = {'it'}, -- Romagnol
 ['scn']        = {'it'}, -- Sicilian
 ['vec']        = {'it'}, -- vèneto
 
 -- kk (Kazakh) cluster:
 -- kk-arab , kk-cyrl , kk-latn , kk-cn , kk-kz , kk-tr -> kk (Kazakh)
 ['kk']         = {'kk-cyrl'},                  -- Kazakh
 ['kk-arab']    = {'kk-cyrl', 'kk'},            -- Kazakh (Arabic script)
 ['kk-cn']      = {'kk-arab', 'kk-cyrl', 'kk'}, -- Kazakh (China)
 ['kk-cyrl']    = {'kk'},                       -- Kazakh (Cyrillic script)
 ['kk-kz']      = {'kk', 'kk-cyrl'},            -- Kazakh (Kazakhstan)
 ['kk-latn']    = {'kk'},                       -- Kazakh (Latin script)
 ['kk-tr']      = {'kk-latn', 'kk'},            -- Kazakh (Turkey)
 ['kaa']        = {'kk-latn', 'kk-cyrl'},       -- Kara-Kalpak
 
 -- ku (Kurdish) cluster: ku-latn , ku-arab -> ku (Kurdish)
 ['ku']         = {'ku-latn'},
 ['ku-arab']    = {'ckb', 'ku'},  -- كوردي (عەرەبی)
 ['ku-latn']    = {'ku'},
 ['ckb']        = {'ku'},
 
 -- nl (Dutch) cluster
 ['af']         = {'nl'}, -- Afrikaans
 ['fy']         = {'nl'}, -- Western Frisian
 ['li']         = {'nl'}, -- Liechtenstein
 ['nl-informal']= {'nl'}, -- Nederlands (informeel)
 ['vls']        = {'nl'}, -- Vlaams
 ['zea']        = {'nl'}, -- Zeeuws
 
 --pl (Polish) cluster
 ['csb']        = {'pl'}, -- Kashubian
 ['szl']        = {'pl'}, -- Silesian
 
 -- pt (Portuguese) cluster
 ['gl']           = {'pt'},            -- Galician
 ['mwl']          = {'pt'},            -- Mirandese
 ['pt-br']        = {'pt'},            -- Brazilian Portuguese
 
 -- ro (Romanian) cluster
 ['mo']           = {'ro'},       -- Moldavian
 ['rmy']          = {'ro'},       -- Romani
 
 -- ru (Russian) cluster
 ['ab']           = {'ru'},            -- Abkhazian
 ['av']           = {'ru'},            -- Avaric
 ['ba']           = {'ru'},            -- Bashkir
 ['be-tarask']    = {'ru'},            -- Belorussian
 ['ce']           = {'ru'},            -- Chechen
 ['crh-cyrl']     = {'ru'},            -- Crimean Tatar (Cyrillic script)
 ['cv']           = {'ru'},            -- Chuvash
 ['inh']          = {'ru'},            -- Ingush
 ['koi']          = {'ru'},            -- Komi-Permyak
 ['krc']          = {'ru'},            -- Karachay-Balkar
 ['kv']           = {'ru'},            -- Komi
 ['lbe']          = {'ru'},            -- лакку
 ['lez']          = {'ru'},            -- Lezghian
 ['mhr']          = {'ru'},            -- Eastern Mari
 ['mrj']          = {'ru'},            -- Hill Mari
 ['myv']          = {'ru'},            -- Erzya
 ['os']           = {'ru'},            -- Ossetic
 ['rue']          = {'uk', 'ru'},      -- Rusyn
 ['sah']          = {'ru'},            -- Sakha
 ['tt']           = {'tt-cyrl', 'ru'}, -- Tatar
 ['tt-cyrl']      = {'ru'},            -- Tatar (Cyrillic script)
 ['udm']          = {'ru'},            -- Udmurt
 ['uk']           = {'ru'},            -- Ukrainian
 ['xal']          = {'ru'},            -- Kalmyk
 
 -- ruq (Megleno Romanian) cluster: ruq-cyrl , ruq-grek , ruq-latn -> ruq (Megleno Romanian)
 ['ruq']        = {'ruq-latn'},   -- Megleno-Romanian
 ['ruq-cyrl']   = {'ruq', 'mk'}, 
 ['ruq-grek']   = {'ruq'}, 
 ['rug-latn']   = {'ro', 'ruq'},  -- Megleno-Romanian (Latin script)
 
 -- sr (Serbian) cluster: sr-ec , sr-el -> sr (Serbian)
 ['sr']         = {'sr-ec'},
 ['sr-ec']      = {'sr'}, 
 ['sr-el']      = {'sr'}, 
  
 -- tg (Tajik) cluster: tg-cyrl , tg-latn -> tg (Tajik)
 ['tg']         = {'tg-cyrl'},
 ['tg-cyrl']    = {'tg'}, 
 ['tg-latn']    = {'tg'}, 
 
 -- tr (Turkish) cluster
 ['gag']        = {'tr'}, -- Gagauz
 ['kiu']        = {'tr'}, -- Kirmanjki
 ['lzz']        = {'tr'}, -- Lazuri
 
 -- tt (Tatar) cluster: tt-cyrl , tt-latn -> tt (Tatar)
 ['tt-cyrl']    = {'tt'}, 
 ['tt-latn']    = {'tt'}, 

 -- zh (Chinese) cluster
 ['gan']          = {'gan-hant', 'zh-hant'},  -- Gan 
 ['gan-hans']     = {'zh-hans'},              -- Simplified Gan script
 ['gan-hant']     = {'zh-hant'},              -- Traditional Gan script
 ['ii']           = {'zh-cn'},                -- Sichuan Yi
 ['wuu']          = {'zh-hans'},              -- Wu
 ['za']           = {'zh-hans'},              -- Zhuang
 ['zh-hans']      = {'zh-cn', 'zh'},          -- Simplified Chinese
 ['zh-hant']      = {'zh'},                   -- Traditional Chinese
 ['zh']           = {'zh-hans'},          
 ['zh-cn']        = {'zh-hans'},              -- Chinese (China)
 ['zh-hk']        = {'zh-hant'},              -- Chinese (Hong Kong)
 ['zh-mo']        = {'zh-hk', 'zh-hant'},     -- 中文（澳門）
 ['zh-my']        = {'zh-sg', 'zh-hans'},     -- 中文（马来西亚）‎
 ['zh-sg']        = {'zh-hans'},              -- Chinese (Singapore)
 ['zh-tw']        = {'zh-hant'},              -- Chinese (Taiwan)
 ['zh-classical'] = {'lzh'},                  -- Literary Chinese
 ['zh-min-nan']   = {'nan'},                  -- Chinese (Min Nan) -> Min Nan Chinese
 ['zh-yue']       = {'yue'},                  -- ? Cantonese -> Cantonese
 
 ------------------------
 --------- misc ---------
 ------------------------
 ['arz']        = {'ar'},            -- Egyptian Arabic -> Arabic
 ['azb']        = {'az'},            -- Southern Azerbaijani -> Azerbaijani 
 ['be-x-old']   = {'be-tarask'},     -- be-x-old -> be-tarask (wrong to correct Taraškievica form of Belarusian orthography)
 ['bh']         = {'bho'},           -- Bihari -> Bhojpuri
 ['bpy']        = {'bn'},            -- Bishnupria Manipuri -> Bengali
 
 -- da
 ['jut']        = {'da'},            -- Jutish -> Danish
 ['kl']         = {'da'},            -- Kalaallisut -> Danish
 
 ['en-gb']      = {'en'}, 
 ['yi']         = {'he'},            -- Yiddish -> Hebrew
 ['iu']         = {'ike-cans'},      -- Inuktitut -> Eastern Canadian (Aboriginal syllabics)
 ['xmf']        = {'ka'},            -- Mingrelian -> Georgian
 ['kbd']        = {'kbd-cyrl'},      -- Kabardian -> Адыгэбзэ
 ['tcy']        = {'kn'},            -- Tulu -> Kannada
 ['ko-kp']      = {'ko'},            -- 한국어 (조선) -> Korean
 ['ks']         = {'ks-arab'},       -- Kashmiri -> Kashmiri (Arabic script)
 
 -- lt
 ['bat-smg']    = {'sgs', 'lt'},     -- Samogitian -> Lithuanian
 ['sgs']    =     {'lt'},            -- Samogitian -> Lithuanian

 ['ltg']        = {'lv'},            -- Latvian -> Latgalian
 ['dtp']        = {'ms'},            -- Central Dusun -> Malay
 ['no']         = {'nb'},            -- Norwegian (bokmål) -> Norwegian Bokmål
 ['roa-rup']    = {'rup'},           -- ? Aromanian -> Aromanian
 ['aln']        = {'sq'},            -- Gheg Albanian -> Albanian
 ['ug']         = {'ug-arab'},       -- Uyghur -> Uyghur (Arabic script)
 ['khw']        = {'ur'},            -- Khowar -> Urdu
}