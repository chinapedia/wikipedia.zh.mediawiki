{| class="infobox" style="width: 22em; font-size: 88%; text-align: left; line-height: 1.5em;"
! colspan=2 style="text-align: center; font-size: 125%;" | {{{Name|{{PAGENAME}} }}}
|-
{{#if: {{{image|}}}|
{{!}} colspan=2 style="text-align: center" {{!}} [[File:{{{image}}}{{!}}{{#if: {{{width|}}}|{{{width}}}|220}}px]]
{{!}}-
|<includeonly>[[Category:需要图片的蛋白质页面]]</includeonly>
}}
{{#if: {{{caption|}}}|
{{!}} colspan=2 style="text-align: center;" {{!}} {{{caption}}}
{{!}}-
}}
! colspan=2 style="text-align: center; background-color: #ddd;" | 識別
|-
! style="background-color: #e7dcc3;" | 符號
| style="background-color: #eee" | {{#if:{{{Symbol|}}} | {{{Symbol}}} | ? }}
|-
{{#if: {{{AltSymbols|}}}|
! style="background-color: #e7dcc3" {{!}} 替換符號
{{!}} style="background-color: #eee" {{!}} {{{AltSymbols}}} }}
|-
{{#if: {{{IUPHAR_id|}}}|
! style="background-color: #e7dcc3" {{!}} [[国际基础药理学与临床药理学联合会|IUPHAR]]
{{!}} style="background-color: #eee" {{!}} {{IUPHAR|{{{Symbol}}}}} }}
|-
{{#if: {{{ATC_prefix|}}}|
! style="background-color: #e7dcc3" {{!}} [[解剖學治療學及化學分類系統|ATC編號]]
{{!}} style="background-color: #eee" {{!}} [[ATC_code_{{{ATC_prefix}}}|{{{ATC_prefix}}}]]{{#if:{{{ATC_suffix|}}} | <span class="reflink plainlinksneverexpand">[http://www.whocc.no/atcddd/indexdatabase/index.php?query={{{ATC_prefix}}}{{{ATC_suffix}}} {{{ATC_suffix}}}]</span>  {{{ATC_supplemental|}}} }} }}
|-
{{#if: {{{CAS_number|}}}|
! style="background-color: #e7dcc3" {{!}} [[CAS編號]]
{{!}} style="background-color: #eee" {{!}} {{#invoke:Chembox CASNo|main|hideNone=yes}} }}
|-
{{#if:{{{DrugBank|}}}|
! style="background-color: #e7dcc3" {{!}} [[DrugBank]]
{{!}} style="background-color: #eee" {{!}} <span class="reflink plainlinksneverexpand">[http://redpoll.pharmacy.ualberta.ca/drugbank/cgi-bin/getCard.cgi?CARD={{{DrugBank}}} {{{DrugBank}}}]</span>
}}
|-
{{#if: {{{EntrezGene|}}}|
! style="background-color: #e7dcc3" {{!}} [[Entrez]]
{{!}} style="background-color: #eee" {{!}} [http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?db=gene&amp;cmd=retrieve&amp;dopt=default&amp;list_uids={{{EntrezGene}}}&rn=1 {{{EntrezGene}}}] }}
|-
{{#if: {{{HGNCid|}}}|
! style="background-color: #e7dcc3" {{!}} [[国际人类基因组组织|HUGO]] 
{{!}} style="background-color: #eee" {{!}} [http://www.genenames.org/data/hgnc_data.php?hgnc_id={{{HGNCid}}} {{{HGNCid}}}] }}
|-
{{#if: {{{OMIM|}}}|
! style="background-color: #e7dcc3" {{!}} [[OMIM]]
{{!}} style="background-color: #eee" {{!}} [http://www.ncbi.nlm.nih.gov/omim/{{{OMIM}}} {{{OMIM}}}] }}
|-
{{#if: {{{PDB|}}}|
! style="background-color: #e7dcc3" {{!}} [[蛋白質資料庫|PDB]]
{{!}} style="background-color: #eee" {{!}} [http://www.pdb.org/pdb/cgi/explore.cgi?pdbId={{{PDB}}} {{{PDB}}}] }} {{#if:{{{PDB_supplemental|}}} | {{{PDB_supplemental|}}} }} 
|-
{{#if: {{{RefSeq|}}}|
! style="background-color: #e7dcc3" {{!}} [[NCBI|RefSeq]]
{{!}} style="background-color: #eee" {{!}} [http://genome.ucsc.edu/cgi-bin/hgTracks?Submit=Submit&position={{{RefSeq}}}&rn=1 {{{RefSeq}}}] }}
|-
{{#if: {{{UniProt|}}}|
! style="background-color: #e7dcc3" {{!}} [[UniProt]]
{{!}} style="background-color: #eee" {{!}} [http://www.uniprot.org/uniprot/{{{UniProt}}} {{{UniProt}}}] }}
|-
! colspan=2 style="text-align: center; background-color: #ddd" | 其他資料
|-
{{#if: {{{ECnumber|}}}|
! style="background-color: #e7dcc3" {{!}} [[EC編號]]
{{!}} style="background-color: #eee" {{!}} [http://www.genome.jp/dbget-bin/www_bget?enzyme+{{{ECnumber}}} {{{ECnumber}}}] }}
|- 
{{#if: {{{Chromosome|}}}|
! style="background-color: #e7dcc3" {{!}} [[基因座]] 
{{!}} style="background-color: #eee" {{!}} {{ #switch:{{{Chromosome|}}}
|X|x=[[X染色體|X]]
|Y|y=[[Y染色體|Y]]
|M|MT|Mt|mt=[[人類線粒體基因|M]]
|#default= [[{{{Chromosome}}}號染色體|{{{Chromosome}}}]]}} ''[http://www.ncbi.nlm.nih.gov/Omim/getmap.cgi?chromosome={{{Chromosome}}}{{{Arm}}}{{{Band}}} {{{Arm}}}{{{Band}}}{{{LocusSupplementaryData}}}]'' }}
|-
|}<includeonly>{{#switch:{{{Chromosome|}}}
|X|x=[[Category:位於人類X染色體的基因]]
|Y|y=[[Category:位於人類Y染色體的基因]]
|M|MT|Mt|mt=[[Category:人類線粒體基因]]
|#default = [[Category:位於{{{Chromosome}}}號人類染色體的基因]]}}</includeonly><noinclude>{{Documentation}}
</noinclude>