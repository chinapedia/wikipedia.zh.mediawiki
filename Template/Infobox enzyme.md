{| class="infobox" style="width: 22em; font-size: 88%; line-height: 1.5em; text-align: left"
! colspan=2 style="text-align: center; font-size: 125%" | {{{Name}}}
|-
{{#if: {{{image|}}}|
{{!}} colspan=2 style="text-align: center" {{!}} [[Image:{{PAGENAME:{{{image}}}}}{{!}}{{#if:{{{width|}}}|{{{width}}}|220}}px]]
{{!}}-
{{#if: {{{caption|}}}|
{{!}} colspan=2 style="text-align: center" {{!}} {{{caption}}}
{{!}}-
}}
}}
| colspan=2 cellpadding=0 | 
{| class="collapsible collapsed" style="text-align: left; border: none; width: 100%"
! colspan=2 style="text-align: center; background-color: #ddd" | 命名
|-
! style="background-color: #e7dcc3" | 系统命名
| style="background-color: #eee" | {{{Systematic_name|}}}
|-
! style="background-color: #e7dcc3" | 缩写
| style="background-color: #eee" | {{{Acronym|}}}
|-
{{#if: {{{Other_names|}}}|
! style="background-color: #e7dcc3" {{!}} 别名
{{!}} style="background-color: #eee" {{!}}  {{{Other_names|}}}
{{!}}-
}}
|}
|-
! colspan=2 style="text-align: center; background-color: #ddd" | 识别码
|-
! style="background-color: #e7dcc3" | [[EC編號]]
| style="background-color: #eee" | {{#if:{{{EC_number}}}|[http://www.chem.qmul.ac.uk/iubmb/enzyme/EC{{{IUBMB_EC_number}}}.html {{{EC_number}}}]|?}}
|-
{{#if: {{{CAS_number|}}}|
! style="background-color: #e7dcc3" {{!}} [[CAS号]]
{{!}} style="background-color: #eee" {{!}} {{#invoke:Chembox CASNo|main|hideNone=yes|value={{#invoke:參數|別名|CASNo|CAS號|CAS号|CASnumber|CAS_number|CAS number|CASNumber|CAS Number|name=CAS值|value=}}}} 
{{!}}-
}}
! colspan=2 style="text-align: center; background-color: #ddd" | 数据库
|-
{{#if: {{{EC_number|}}}|
! style="background-color: #e7dcc3" {{!}} [[IntEnz]]
{{!}} style="background-color: #eee" {{!}} [http://www.ebi.ac.uk/intenz/query?cmd=SearchEC&ec={{{EC_number}}} IntEnz浏览]
{{!}}-
}}
{{#if: {{{EC_number|}}}|
! style="background-color: #e7dcc3" {{!}} {{tsl|en|BRENDA|BRENDA}}
{{!}} style="background-color: #eee" {{!}} [http://www.brenda-enzymes.org/php/result_flat.php4?ecno={{{EC_number}}} BRENDA入口]
{{!}}-
}}
{{#if: {{{EC_number|}}}|
! style="background-color: #e7dcc3" {{!}} {{tsl|en|ExPASy|ExPASy}}
{{!}} style="background-color: #eee" {{!}} [http://www.expasy.org/enzyme/{{{EC_number}}}  NiceZyme浏览]
{{!}}-
}}
{{#if: {{{EC_number|}}}|
! style="background-color: #e7dcc3" {{!}} [[KEGG]]
{{!}} style="background-color: #eee" {{!}} [http://www.genome.ad.jp/dbget-bin/www_bget?enzyme+{{{EC_number}}}  KEGG入口]
{{!}}-
}}
{{#if: {{{EC_number|}}}|
! style="background-color: #e7dcc3" {{!}} {{tsl|en|MetaCyc|MetaCyc}}
{{!}} style="background-color: #eee" {{!}} [http://biocyc.org/META/substring-search?type=NIL&object={{{EC_number}}} 代谢路径]
{{!}}-
}}
{{#if: {{{EC_number|}}}|
! style="background-color: #e7dcc3" {{!}} {{tsl|en|PRIAM_enzyme-specific_profiles||PRIAM}}
{{!}} style="background-color: #eee" {{!}} [http://priam.prabi.fr/cgi-bin/PRIAM_profiles_CurrentRelease.pl?EC={{{EC_number}}} 概述]
{{!}}-
}}
{{#if: {{{EC_number|}}}|
! style="background-color: #e7dcc3" {{!}} [[蛋白質資料庫|PDB]]
{{!}} style="background-color: #eee" {{!}} <small>[https://www.rcsb.org/search?q=rcsb_polymer_entity.rcsb_ec_lineage.id:{{{EC_number}}} RCSB PDB] [https://pdbj.org/mine/sql?query=SELECT+DISTINCT+pdbid+FROM+entity+WHERE+entity.pdbx_ec%3D%27{{{EC_number}}}%27 PDBj] [http://www.ebi.ac.uk/pdbe-srv/PDBeXplore/enzyme/?ec={{{EC_number}}} PDBe] [http://www.ebi.ac.uk/thornton-srv/databases/cgi-bin/enzymes/GetPage.pl?ec_number={{{EC_number}}} PDBsum]</small>
{{!}}-
}}
{{#if: {{{GO_code|}}}|
! style="background-color: #e7dcc3" {{!}} [[基因本体]]
{{!}} style="background-color: #eee" {{!}} <small>[http://amigo.geneontology.org/cgi-bin/amigo/go.cgi?query=GO:{{{GO_code}}}&view=details AmiGO ] / [http://www.ebi.ac.uk/ego/DisplayGoTerm?id=GO:{{{GO_code}}}&format=normal EGO ]</small>
{{!}}-
}}
| colspan=2 cellpadding=0 | 
{| class="collapsible collapsed" style="text-align: left; border: none; width: 100%"
! colspan=2 style="text-align: center; background-color: #ddd" | 搜索
|-
{{#if: {{{EC_number|}}}|
! style="background-color: #e7dcc3" {{!}} [[公共医学中心数据库|PMC]]
{{!}} style="background-color: #eee" {{!}} [http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?db=pubmed&term={{{EC_number}}}%5BEC/RN%20Number%5D%20AND%20pubmed%20pmc%20local%5Bsb%5D 相关文献]
{{!}}-
}}
{{#if: {{{EC_number|}}}|
! style="background-color: #e7dcc3" {{!}} [[PubMed]]
{{!}} style="background-color: #eee" {{!}} [http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?db=pubmed&term={{{EC_number}}}%5BEC/RN%20Number%5D 相关文献] }}
|}
|}<noinclude>{{documentation}}<!-- please add category and language links to the /doc sub-page, not here --></noinclude>