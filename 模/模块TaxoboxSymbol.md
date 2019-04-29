--[[
    This module define the data used by Module:Taxobox
--]]

local p = {}

--[[
    This table define the conservation system and its status and photo to be showed
    
    Note:
        If extinct is defined and is true, Module:Taxobox will try to print corresponding argument.
--]]
local conservationStatusTable = {
    ['iucn2.3'] = {
        ['introduction'] = '[[世界自然保护联盟濒危物种红色名录|IUCN 2.3]]',
        ['ex'] = {
            ['name'] = '[[絕滅|絕滅]]', ['category'] = '世界自然保护联盟濒危物种红色名录绝灭物种', ['extinct'] = true,
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_EX_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_EX_zh-hant.svg|frameless]]}-'
        },
        ['ew'] = {
            ['name'] = '[[野外绝灭|野外绝灭]]', ['category'] = '世界自然保护联盟濒危物种红色名录野外绝灭物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_EW_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_EW_zh-hant.svg|frameless]]}-'
        },
        ['cr'] = {
            ['name'] = '[[極危物種|極危]]', ['category'] = '世界自然保护联盟濒危物种红色名录野外极危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_CR_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_CR_zh-hant.svg|frameless]]}-'
        },
        ['en'] = {
            ['name'] = '[[瀕危物種|瀕危]]', ['category'] = '世界自然保护联盟濒危物种红色名录濒危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_EN_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_EN_zh-hant.svg|frameless]]}-'
        },
        ['vu'] = {
            ['name'] = '[[易危物種|易危]]', ['category'] = '世界自然保护联盟濒危物种红色名录濒危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_EN_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_EN_zh-hant.svg|frameless]]}-'
        },
        ['en'] = {
            ['name'] = '[[瀕危物種|瀕危]]', ['category'] = '世界自然保护联盟濒危物种红色名录濒危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_EN_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_EN_zh-hant.svg|frameless]]}-'
        },
        ['vu'] = {
            ['name'] = '[[易危物種|易危]]', ['category'] = '世界自然保护联盟濒危物种红色名录易危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_VU_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_VU_zh-hant.svg|frameless]]}-'
        },
        ['lr'] = {
            ['name'] = '[[低危|低危]]', ['category'] = '无效保护状况',
            ['photo'] = '[[File:Status_iucn2.3_blank.svg|File:Status iucn2.3 blank.svg]]'
        },
        ['lr/cd'] = {
            ['name'] = '[[保护依赖|保护依赖]]', ['category'] = '世界自然保护联盟濒危物种红色名录保护依赖物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_CD_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_CD_zh-hant.svg|frameless]]}-'
        },
        ['cd'] = {['alias'] = 'lr/cd'},
        ['lr/nt'] = {
            ['name'] = '[[近危|近危]]', ['category'] = '世界自然保护联盟濒危物种红色名录近危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_NT_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_NT_zh-hant.svg|frameless]]}-'
        },
        ['nt'] = {['alias'] = 'lr/nt'},
        ['lr/lc'] = {
            ['name'] = '[[无危|无危]]', ['category'] = '世界自然保护联盟濒危物种红色名录无危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_LC_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_LC_zh-hant.svg|frameless]]}-'
        },
        ['lc'] = {['alias'] = 'lr/lc'},
        ['dd'] = {
            ['name'] = '[[数据缺乏|数据缺乏]]', ['category'] = '世界自然保护联盟濒危物种红色名录数据缺乏物种',
            ['photo'] = '[[File:Status_none_DD.svg|File:Status none DD.svg]]'
        },
        ['ne'] = {['name'] = '未予评估'},
        ['nr'] = {['name'] = '未承认'},
        ['pe'] = {
            ['name'] = '[[極危|極危]]，可能絕滅', ['category'] = '世界自然保护联盟濒危物种红色名录野外极危物种',
            ['photo'] = '[[File:Status_none_PE.svg|frameless]]'
        },
        ['pew'] = {
            ['name'] = '[[極危|極危]]，可能野外絕滅', ['category'] = '世界自然保护联盟濒危物种红色名录野外极危物种',
            ['photo'] = '[[File:Status_none_PEW.svg|frameless]]'
        }
    },
    ['iucn'] = {
        ['introduction'] = '[[世界自然保护联盟濒危物种红色名录|IUCN 3.1]]',
        ['ex'] = {
            ['name'] = '[[绝灭|绝灭]]', ['category'] = '世界自然保护联盟濒危物种红色名录绝灭物种', ['extinct'] = true,
            ['photo'] = '-{zh-hans:[[File:Status_iucn3.1_EX_zh.svg|frameless]];zh-hant:[[File:Status_iucn3.1_EX_zh-hant.svg|frameless]]}-'
        },
        ['ew'] = {
            ['name'] = '[[野外绝灭|野外绝灭]]', ['category'] = '世界自然保护联盟濒危物种红色名录野外绝灭物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn3.1_EW_zh.svg|frameless]];zh-hant:[[File:Status_iucn3.1_EW_zh-hant.svg|frameless]]}-'
        },
        ['cr'] = {
            ['name'] = '[[極危物種|極危]]', ['category'] = '世界自然保护联盟濒危物种红色名录野外极危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn3.1_CR_zh.svg|frameless]];zh-hant:[[File:Status_iucn3.1_CR_zh-hant.svg|frameless]]}-'
        },
        ['en'] = {
            ['name'] = '[[瀕危物種|瀕危]]', ['category'] = '世界自然保护联盟濒危物种红色名录濒危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn3.1_EN_zh.svg|frameless]];zh-hant:[[File:Status_iucn3.1_EN_zh-hant.svg|frameless]]}-'
        },
        ['vu'] = {
            ['name'] = '[[易危物種|易危]]', ['category'] = '世界自然保护联盟濒危物种红色名录易危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn3.1_VU_zh.svg|frameless]];zh-hant:[[File:Status_iucn3.1_VU_zh-hant.svg|frameless]]}-'
        },
        ['nt'] = {
            ['name'] = '[[近危|近危]]', ['category'] = '世界自然保护联盟濒危物种红色名录近危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn3.1_NT_zh.svg|frameless]];zh-hant:[[File:Status_iucn3.1_NT_zh-hant.svg|frameless]]}-'
        },
        ['lc'] = {
            ['name'] = '[[无危|无危]]', ['category'] = '世界自然保护联盟濒危物种红色名录无危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn3.1_LC_zh.svg|frameless]];zh-hant:[[File:Status_iucn3.1_LC_zh-hant.svg|frameless]]}-'
        },
        ['dd'] = {
            ['name'] = '[[数据缺乏|数据缺乏]]', ['category'] = '世界自然保护联盟濒危物种红色名录数据缺乏物种',
            ['photo'] = '[[File:Status_none_DD.svg|File:Status none DD.svg]]'
        },
        ['ne'] = {['name'] = '未予评估'},
        ['nr'] = {['name'] = '未承认'},
        ['pe'] = {
            ['name'] = '[[極危|極危]]，可能絕滅', ['category'] = '世界自然保护联盟濒危物种红色名录野外极危物种',
            ['photo'] = '[[File:Status_none_PE.svg|frameless]]'
        },
        ['pew'] = {
            ['name'] = '[[極危|極危]]，可能野外絕滅', ['category'] = '世界自然保护联盟濒危物种红色名录野外极危物种',
            ['photo'] = '[[File:Status_none_PEW.svg|frameless]]'
        }
    },
    ['iucn3.1'] = {['alias'] = 'iucn'},
    ['epbc'] = {
        ['introduction'] = '[[环境保护和生物多样性保护法案野外绝灭生物群|EBPC]]',
        ['ex'] = {
            ['name'] = '[[绝灭|绝灭]]', ['category'] = '环境保护和生物多样性保护法案绝灭生物群', ['extinct'] = true,
            ['photo'] = '[[File:Status_EPBC_EX.svg|frameless]]',
            ['category'] = 'EPBC法案绝灭生物群'
        },
        ['ew'] = {
            ['name'] = '[[野外绝灭|野外绝灭]]', ['category'] = '环境保护和生物多样性保护法案野外绝灭生物群',
            ['photo'] = '[[File:Status_EPBC_EW.svg|frameless]]',
            ['category'] = 'EPBC法案野外绝灭生物群'
        },
        ['cr'] = {
            ['name'] = '[[極危物種|極危]]', ['category'] = '环境保护和生物多样性保护法案极危生物群',
            ['photo'] = '[[File:Status_EPBC_CR.svg|frameless]]',
            ['category'] = 'EPBC法案极危生物群'
        },
        ['en'] = {
            ['name'] = '[[瀕危物種|瀕危]]', ['category'] = '环境保护和生物多样性保护法案濒危生物群',
            ['photo'] = '[[File:Status_EPBC_EN.svg|frameless]]',
            ['category'] = 'EPBC法案濒危生物群'
        },
        ['vu'] = {
            ['name'] = '[[易危物種|易危]]', ['category'] = '环境保护和生物多样性保护法案易危生物群',
            ['photo'] = '[[File:Status_EPBC_VU.svg|frameless]]',
            ['category'] = 'EPBC法案易危生物群'
        },
        ['cd'] = {
            ['name'] = '[[保护依赖|保护依赖]]', ['category'] = '环境保护和生物多样性保护法案保护依赖生物群',
            ['photo'] = '[[File:Status_EPBC_CD.svg|frameless]]',
            ['category'] = 'EPBC法案保护依赖生物群'
        },
        ['dl'] = {['name'] = '除名', ['photo'] = '[[File:Status_EPBC_DL.svg|frameless]]'}
    },
    ['tnc'] = {
        ['introduction'] = '[[1999年環境保護與生物多樣性保護法案|EPBC法案]]',
        ['gx'] = {
            ['name'] = '推測[[绝灭|绝灭]]', ['category'] = '公益自然推测绝灭物种',
            ['photo'] = '[[File:Status_TNC_GX.svg|frameless]]'
        },
        ['gh'] = {
            ['name'] = '可能[[绝灭|绝灭]]', ['category'] = '公益自然可能绝灭物种',
            ['photo'] = '[[File:Status_TNC_GH.svg|frameless]]'
        },
        ['g1'] = {
            ['name'] = '严重濒绝', ['category'] = '公益自然严重濒绝物种',
            ['photo'] = '[[File:Status_TNC_G1.svg|frameless]]'
        },
        ['g2'] = {
            ['name'] = '濒绝', ['category'] = '公益自然濒绝物种',
            ['photo'] = '[[File:Status_TNC_G2.svg|frameless]]'
        },
        ['g3'] = {
            ['name'] = '易危', ['category'] = '公益自然易危物种',
            ['photo'] = '[[File:Status_TNC_G3.svg|frameless]]'
        },
        ['g4'] = {
            ['name'] = '可能安全', ['category'] = '公益自然可能安全物种',
            ['photo'] = '[[File:Status_TNC_G4.svg|frameless]]'
        },
        ['g5'] = {
            ['name'] = '安全', ['category'] = '公益自然安全物种',
            ['photo'] = '[[File:Status_TNC_G5.svg|frameless]]'
        },
        ['gu'] = {['name'] = '未分级', ['photo'] = '[[File:Status_TNC_blank.svg|frameless]]'},
        ['tx'] = {
            ['name'] = '推測[[绝灭|绝灭]]', ['category'] = '公益自然推测绝灭物种',
            ['photo'] = '[[File:Status_TNC_TX.svg|frameless]]'
        },
        ['th'] = {
            ['name'] = '可能[[绝灭|绝灭]]', ['category'] = '公益自然可能绝灭物种',
            ['photo'] = '[[File:Status_TNC_TH.svg|frameless]]'
        },
        ['t1'] = {
            ['name'] = '嚴重瀕絕', ['category'] = '公益自然严重濒绝物种',
            ['photo'] = '[[File:Status_TNC_T1.svg|frameless]]'
        },
        ['t2'] = {
            ['name'] = '瀕絕', ['category'] = '公益自然濒绝物种',
            ['photo'] = '[[File:Status_TNC_T2.svg|frameless]]'
        },
        ['t3'] = {
            ['name'] = '易危', ['category'] = '公益自然易危物种',
            ['photo'] = '[[File:Status_TNC_T3.svg|frameless]]'
        },
        ['t4'] = {
            ['name'] = '可能安全', ['category'] = '公益自然可能安全物种',
            ['photo'] = '[[File:Status_TNC_T4.svg|frameless]]'
        },
        ['t5'] = {
            ['name'] = '安全', ['category'] = '公益自然安全物种',
            ['photo'] = '[[File:Status_TNC_T5.svg|frameless]]'
        },
        ['tu'] = {['name'] = '未分級', ['photo'] = '[[File:Status_TNC_T_blank.svg|frameless]]'}
    },
    ['natureserve'] = {['alias'] = 'tnc'},
    ['esa'] = {
        ['introduction'] = '[[濒危物种法案|ESA]]',
        ['ex'] = {['name'] = '[[绝灭|绝灭]]', ['photo'] = '[[File:Status_ESA_EX_zh.svg|frameless]]'},
        ['le'] = {['name'] = '[[濒危物种|濒危]]', ['photo'] = '[[File:Status_ESA_LE_zh.svg|frameless]]'},
        ['e'] = {['alias'] = 'le'},
        ['lt'] = {['name'] = '[[受威胁物种|受威胁]]', ['photo'] = '[[File:Status_ESA_LT_zh.svg|frameless]]'},
        ['t'] = {['alias'] = 'lt'},
        ['dl'] = {['name'] = '除名', ['photo'] = '[[File:Status_ESA_DL_zh.svg|frameless]]'},
        ['delisted'] = {['alias'] = 'dl'}
    },
    ['cosewic'] = {
        ['introduction'] = '[[加拿大濒危野生动物现状调查委员会|COSEWIC]]',
        ['x'] = {['name'] = '[[绝灭|绝灭]]', ['photo'] = '[[File:Status_COSEWIC_X.svg|frameless]]', ['extinct'] = true},
        ['xt'] = {['name'] = '绝迹（加拿大）', ['photo'] = '[[File:Status_COSEWIC_XT.svg|frameless]]'},
        ['e'] = {['name'] = '[[濒危物种|濒危]]', ['photo'] = '[[File:Status_COSEWIC_E.svg|frameless]]'},
        ['t'] = {['name'] = '[[受威胁物种|受威胁]]', ['photo'] = '[[File:Status_COSEWIC_T.svg|frameless]]'},
        ['sc'] = {['name'] = '特别关注', ['photo'] = '[[File:Status_COSEWIC_SC.svg|frameless]]'},
        ['nar'] = {['name'] = '[[无危物种|无危]]', ['photo'] = '[[File:Status_COSEWIC_NAR.svg|frameless]]'}
    },
    ['decf'] = {
        ['introduction'] = '[[优先申报珍稀动植物名单|DEC]]',
        ['x'] = {['name'] = '珍稀申报 — 推测[[绝灭|绝灭]]', ['photo'] = '[[File:Status_DECF_X.svg|frameless]]', ['extinct'] = true},
        ['r'] = {['name'] = '珍稀申报', ['photo'] = '[[File:Status_DECF_R.svg|frameless]]'},
        ['p1'] = {['name'] = '第一优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P1.svg|frameless]]'},
        ['p2'] = {['name'] = '第二优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P2.svg|frameless]]'},
        ['p3'] = {['name'] = '第三优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P3.svg|frameless]]'},
        ['p4'] = {['name'] = '第四优先 — 珍稀类群', ['photo'] = '[[File:Status_DECF_P4.svg|frameless]]'},
        ['dl'] = {['name'] = '除名', ['photo'] = '[[File:Status_DECF_DL.svg|frameless]]'}
    },
    ['qldnca'] = {
        ['introduction'] = '[[1992年自然保护法案|NCA]]',
        ['ew'] = {['name'] = '[[野外绝灭|野外绝灭]]', ['photo'] = '[[File:Status_DECF_X.svg|frameless]]'},
        ['en'] = {['name'] = '珍稀申报', ['photo'] = '[[File:Status_DECF_R.svg|frameless]]'},
        ['vu'] = {['name'] = '第一优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P1.svg|frameless]]'},
        ['r'] = {['name'] = '第二优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P2.svg|frameless]]'},
        ['nt'] = {['name'] = '第三优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P3.svg|frameless]]'},
        ['lc'] = {['name'] = '第四优先 — 珍稀类群', ['photo'] = '[[File:Status_DECF_P4.svg|frameless]]'}
    },
    ['cites'] = {
        ['cites_a1'] = {['name'] = '珍稀申报 — 推测[[绝灭|绝灭]]', ['photo'] = '[[File:Status_DECF_X.svg|frameless]]'},
        ['cites_a2'] = {['name'] = '珍稀申报', ['photo'] = '[[File:Status_DECF_R.svg|frameless]]'},
        ['cites_a3'] = {['name'] = '第一优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P1.svg|frameless]]'}
    },
    ['nztcs'] = {
        ['ex'] = {['name'] = '珍稀申报 — 推测[[绝灭|绝灭]]', ['photo'] = '[[File:Status_DECF_X.svg|frameless]]'},
        ['nc'] = {['name'] = '珍稀申报', ['photo'] = '[[File:Status_DECF_R.svg|frameless]]'},
        ['ne'] = {['name'] = '第一优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P1.svg|frameless]]'},
        ['nv'] = {['name'] = '第二优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P2.svg|frameless]]'},
        ['sd'] = {['name'] = '第三优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P3.svg|frameless]]'},
        ['gd'] = {['name'] = '第四优先 — 珍稀类群', ['photo'] = '[[File:Status_DECF_P4.svg|frameless]]'},
        ['sp'] = {['name'] = '第三优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P3.svg|frameless]]'},
        ['rr'] = {['name'] = '第四优先 — 珍稀类群', ['photo'] = '[[File:Status_DECF_P4.svg|frameless]]'}
    },
    ['default'] = {
        ['introduction'] = '默认',
        ['ex'] = {['name'] = '绝灭'},
        ['ew'] = {
            ['name'] = '[[野外绝灭|野外绝灭]]', ['category'] = '世界自然保护联盟濒危物种红色名录野外绝灭物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_EW_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_EW_zh-hant.svg|frameless]]}-'
        },
        ['cr'] = {
            ['name'] = '[[極危物種|極危]]', ['category'] = '世界自然保护联盟濒危物种红色名录野外极危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_CR_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_CR_zh-hant.svg|frameless]]}-'
        },
        ['en'] = {
            ['name'] = '[[瀕危物種|瀕危]]', ['category'] = '世界自然保护联盟濒危物种红色名录濒危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_EN_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_EN_zh-hant.svg|frameless]]}-'
        },
        ['vu'] = {
            ['name'] = '[[易危物種|易危]]', ['category'] = '世界自然保护联盟濒危物种红色名录濒危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_EN_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_EN_zh-hant.svg|frameless]]}-'
        },
        ['nt'] = {
            ['name'] = '[[低危|低危]]', ['category'] = '无效保护状况',
            ['photo'] = '[[File:Status_iucn2.3_blank.svg|File:Status iucn2.3 blank.svg]]'
        },
        ['lc'] = {
            ['name'] = '[[保护依赖|保护依赖]]', ['category'] = '世界自然保护联盟濒危物种红色名录保护依赖物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_CD_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_CD_zh-hant.svg|frameless]]}-'
        },
        ['se'] = {
            ['name'] = '[[近危|近危]]', ['category'] = '世界自然保护联盟濒危物种红色名录近危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_NT_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_NT_zh-hant.svg|frameless]]}-'
        },
        ['secure'] = {['alias'] = 'se'},
        ['dd'] = {
            ['name'] = '[[无危|无危]]', ['category'] = '世界自然保护联盟濒危物种红色名录无危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_LC_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_LC_zh-hant.svg|frameless]]}-'
        },
        ['dom'] = {
            ['name'] = '[[无危|无危]]', ['category'] = '世界自然保护联盟濒危物种红色名录无危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_LC_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_LC_zh-hant.svg|frameless]]}-'
        },
        ['domesticated'] = {['alias'] = 'dom'},
        ['pe'] = {
            ['name'] = '[[无危|无危]]', ['category'] = '世界自然保护联盟濒危物种红色名录无危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_LC_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_LC_zh-hant.svg|frameless]]}-'
        },
        ['pew'] = {
            ['name'] = '[[无危|无危]]', ['category'] = '世界自然保护联盟濒危物种红色名录无危物种',
            ['photo'] = '-{zh-hans:[[File:Status_iucn2.3_LC_zh.svg|frameless]];zh-hant:[[File:Status_iucn2.3_LC_zh-hant.svg|frameless]]}-'
        },
        ['cites_a1'] = {['name'] = '珍稀申报 — 推测[[绝灭|绝灭]]', ['photo'] = '[[File:Status_DECF_X.svg|frameless]]'},
        ['cites_a2'] = {['name'] = '珍稀申报', ['photo'] = '[[File:Status_DECF_R.svg|frameless]]'},
        ['cites_a3'] = {['name'] = '第一优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P1.svg|frameless]]'},
        ['fossil'] = {['name'] = '第一优先 — 知之甚少的类群'},
        ['pre'] = {['name'] = '第一优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P1.svg|frameless]]'},
        ['text'] = {['name'] = '第一优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P1.svg|frameless]]'},
        ['lr/cd'] = {['name'] = '第一优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P1.svg|frameless]]'},
        ['lr/nt'] = {['name'] = '第一优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P1.svg|frameless]]'},
        ['lr/lc'] = {['name'] = '第一优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P1.svg|frameless]]'},
        ['gx'] = {['name'] = '第一优先 — 知之甚少的类群', ['photo'] = '[[File:Status_DECF_P1.svg|frameless]]'},
        ['gh'] = {
            ['name'] = '可能[[绝灭|绝灭]]', ['category'] = '公益自然可能绝灭物种',
            ['photo'] = '[[File:Status_TNC_GH.svg|frameless]]'
        },
        ['g1'] = {
            ['name'] = '严重濒绝', ['category'] = '公益自然严重濒绝物种',
            ['photo'] = '[[File:Status_TNC_G1.svg|frameless]]'
        },
        ['g2'] = {
            ['name'] = '濒绝', ['category'] = '公益自然濒绝物种',
            ['photo'] = '[[File:Status_TNC_G2.svg|frameless]]'
        },
        ['g3'] = {
            ['name'] = '易危', ['category'] = '公益自然易危物种',
            ['photo'] = '[[File:Status_TNC_G3.svg|frameless]]'
        },
        ['g4'] = {
            ['name'] = '可能安全', ['category'] = '公益自然可能安全物种',
            ['photo'] = '[[File:Status_TNC_G4.svg|frameless]]'
        },
        ['g5'] = {
            ['name'] = '安全', ['category'] = '公益自然安全物种',
            ['photo'] = '[[File:Status_TNC_G5.svg|frameless]]'
        },
        ['gu'] = {['name'] = '未分级', ['photo'] = '[[File:Status_TNC_blank.svg|frameless]]'},
        ['tx'] = {
            ['name'] = '推測[[绝灭|绝灭]]', ['category'] = '公益自然推测绝灭物种',
            ['photo'] = '[[File:Status_TNC_TX.svg|frameless]]'
        },
        ['th'] = {
            ['name'] = '可能[[绝灭|绝灭]]', ['category'] = '公益自然可能绝灭物种',
            ['photo'] = '[[File:Status_TNC_TH.svg|frameless]]'
        },
        ['t1'] = {
            ['name'] = '嚴重瀕絕', ['category'] = '公益自然严重濒绝物种',
            ['photo'] = '[[File:Status_TNC_T1.svg|frameless]]'
        },
        ['t2'] = {
            ['name'] = '瀕絕', ['category'] = '公益自然濒绝物种',
            ['photo'] = '[[File:Status_TNC_T2.svg|frameless]]'
        },
        ['t3'] = {
            ['name'] = '易危', ['category'] = '公益自然易危物种',
            ['photo'] = '[[File:Status_TNC_T3.svg|frameless]]'
        },
        ['t4'] = {
            ['name'] = '可能安全', ['category'] = '公益自然可能安全物种',
            ['photo'] = '[[File:Status_TNC_T4.svg|frameless]]'
        },
        ['t5'] = {
            ['name'] = '安全', ['category'] = '公益自然安全物种',
            ['photo'] = '[[File:Status_TNC_T5.svg|frameless]]'
        },
        ['tu'] = {['name'] = '未分級', ['photo'] = '[[File:Status_TNC_T_blank.svg|frameless]]'},
        ['invalid'] = {['name'] = '\'\'\'\'\'无效状况\'\'\'\'\'', ['category'] = '无效保护状况'}
    }
}

--[[
    if the argName == className, just leave argName alone
--]]
local classificationTable = {
    {['argName'] = 'superdomain', ['entryName'] = '總域'},
    {['argName'] = 'domain', ['entryName'] = '域'},
    {['argName'] = 'superregnum', ['entryName'] = '總界'},
    {
        ['argName'] = 'regnum', ['entryName'] = '界',
        ['className'] = 'kingdom'
    },
    {['argName'] = 'subregnum', ['entryName'] = '亞界'},
    {['argName'] = 'superdivisio', ['entryName'] = '總門'},
    {['argName'] = 'superphylum', ['entryName'] = '超门'},
    {['argName'] = 'divisio', ['entryName'] = '門'},
    {['argName'] = 'phylum', ['entryName'] = '門'},
    {['argName'] = 'subdivisio', ['entryName'] = '亞門'},
    {['argName'] = 'subphylum', ['entryName'] = '亞門'},
    {['argName'] = 'infraphylum', ['entryName'] = '下門'},
    {['argName'] = 'microphylum', ['entryName'] = 'Microphylum'},
    {['argName'] = 'nanophylum', ['entryName'] = 'Nanophylum'},
    {['argName'] = 'superclassis', ['entryName'] = '總綱'},
    {['argName'] = 'classis', ['entryName'] = '綱'},
    {['argName'] = 'subclassis', ['entryName'] = '亞綱'},
    {['argName'] = 'infraclassis', ['entryName'] = '下綱'},
    {['argName'] = 'magnordo', ['entryName'] = 'Magnorder'},
    {['argName'] = 'superordo', ['entryName'] = '總目'},
    {['argName'] = 'ordo', ['entryName'] = '目'},
    {['argName'] = 'subordo', ['entryName'] = '亞目'},
    {['argName'] = 'infraordo', ['entryName'] = '下目'},
    {['argName'] = 'parvordo', ['entryName'] = '小目'},
    {['argName'] = 'zoodivisio', ['entryName'] = 'Division'},
    {['argName'] = 'zoosectio', ['entryName'] = '-{zh-hans:组;zh-hant:節}-'},
    {['argName'] = 'zoosubsectio', ['entryName'] = '亞-{zh-hans:组;zh-hant:節}-'},
    {['argName'] = 'superfamilia', ['entryName'] = '總科'},
    {['argName'] = 'familia', ['entryName'] = '科'},
    {['argName'] = 'subfamilia', ['entryName'] = '亞科'},
    {['argName'] = 'supertribus', ['entryName'] = '總族'},
    {['argName'] = 'tribus', ['entryName'] = '族'},
    {['argName'] = 'subtribus', ['entryName'] = '亞族'},
    {['argName'] = 'alliance', ['entryName'] = '群團'},
    {['argName'] = 'genus', ['entryName'] = '屬'},
    {['argName'] = 'subgenus', ['entryName'] = '亞屬'},
    {['argName'] = 'sectio', ['entryName'] = '-{zh-hans:组;zh-hant:節}-'},
    {['argName'] = 'subsectio', ['entryName'] = '-{zh-hans:亚组;zh-hant:亞節}-'},
    {['argName'] = 'series', ['entryName'] = '系'},
    {['argName'] = 'subseries', ['entryName'] = '亞系'},
    {['argName'] = 'species_group', ['entryName'] = '種組'},
    {['argName'] = 'species_subgroup', ['entryName'] = '種亞組'},
    {['argName'] = 'species_complex', ['entryName'] = '复合种'},
    {['argName'] = 'species', ['entryName'] = '種'},
    {['argName'] = 'subspecies', ['entryName'] = '亞種'},
    {['argName'] = 'variety', ['entryName'] = '變種'},
    {['argName'] = 'subvariety', ['entryName'] = '亞變種'},
    {['argName'] = 'forma', ['entryName'] = '變型'},
    {['argName'] = 'subforma', ['entryName'] = '亞變型'}
}

local typeSpeciesTable = {
    {['argPostfix'] = 'genus', ['entryText'] = '[[生物學模式|模式屬]]'},
    {['argPostfix'] = 'ichnogenus', ['entryText'] = '[[遗迹种|遗迹种]]'},
    {['argPostfix'] = 'oogenus', ['entryText'] = '[[蛋化石形态属|蛋化石形态属]]'},
    {['argPostfix'] = 'species', ['entryText'] = '[[生物學模式|模式種]]'},
    {['argPostfix'] = 'ichnospecies', ['entryText'] = '[[遗迹种|遗迹种]]'},
    {['argPostfix'] = 'oospecies', ['entryText'] = '[[蛋化石形态种|蛋化石形态种]]'},
    {['argPostfix'] = 'strain', ['entryText'] = '[[生物學模式|模式株]]'}
}

p.conservationStatusTable = conservationStatusTable
p.classificationTable = classificationTable
p.typeSpeciesTable = typeSpeciesTable

return p