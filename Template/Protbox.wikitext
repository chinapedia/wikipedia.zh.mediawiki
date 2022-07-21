{|border="0" bgcolor="#ffffff" cellpadding="2" cellspacing=0 align="right" width="305" style="border:2px solid #e7dcc3;margin-left:3px"
!bgcolor=#e7dcc3 colspan=2|{{{Name}}}
|-
{{#if: {{{Photo|}}} |
{{!}} align=center colspan=2 {{!}} [[File:{{{Photo}}}|300px]]<br>
{{{Caption}}} }}
|-valign=top
{{#if:{{{Symbol|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[国际人类基因组组织|代号]] {{!}}{{!}}  style="border-top:2px solid #e7dcc3;" width=220{{!}}[http://www.gene.ucl.ac.uk/nomenclature/data/get_data.php?hgnc_id=HGNC:{{{HGNCid}}} {{{Symbol}}}] {{{AltSymbols}}}}}
|-
{{#if:{{{Names|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}别名{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Names}}}}}
|-valign=top
{{#ifexpr:{{#expr:{{#if:{{{Chromosome|}}}|1|0}} or {{#if:{{{Gene|}}}|1|0}} or {{#if:{{{Gene_type|}}}|1|0}} }}|{{!}}bgcolor=#e7dcc3 colspan=2 align="center"{{!}}'''[[遺傳學|遺傳學資料]]'''}}
|-valign=top
{{#if:{{{Chromosome|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[基因座]] {{!}}{{!}} style="border-top:2px solid #e7dcc3; " width=220{{!}}[[{{{Chromosome}}}號染色體_(人類)|Chr. {{{Chromosome}}}]] ''[http://www.ncbi.nlm.nih.gov/Omim/getmap.cgi?chromosome={{{Chromosome}}}{{{Arm}}}{{{Band}}} {{{Arm}}}{{{Band}}}{{{LocusSupplementaryData}}}]''}}
|-valign=top
{{#if:{{{Gene|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} 基因編號 {{!}}{{!}}style="border-top:2px solid #e7dcc3" width=220{{!}} {{{Gene}}}}}
|-valign=top
{{#if:{{{Gene_type|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} 基因類型 {{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}} {{{Gene_type}}}}}
|-valign=top
{{#ifexpr:{{#expr:{{#if:{{{Protein_length|}}}|1|0}} or {{#if:{{{Molecular_weight|}}}|1|0}} or {{#if:{{{Structure|}}}|1|0}} or {{#if:{{{Type|}}}|1|0}} or {{#if:{{{Functions|}}}|1|0}} or {{#if:{{{Domains|}}}|1|0}} or {{#if:{{{Motifs|}}}|1|0}} or {{#if:{{{Alternative_products|}}}|1|0}}}}|{{!}}bgcolor=#e7dcc3 colspan=2 align="center"{{!}}'''蛋白质结构与功能'''}}
|-valign=top
{{#if:{{{Protein_length|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[蛋白質|蛋白質長度]] {{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}} {{{Protein_length}}} ([[氨基酸]])}}
|-valign=top
{{#if:{{{Molecular_weight|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[分子量]] {{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}} {{{Molecular_weight}}} (Da)}}
|-valign=top
{{#if:{{{Structure|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[蛋白质结构|结构]] {{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}} {{{Structure}}}}}
|-valign=top
{{#if:{{{Type|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[蛋白质]]类型{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}} {{{Type}}}}}
|-
{{#if:{{{Functions|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}功能{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}} {{{Functions}}}}}
|-
{{#if:{{{Domains|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[結構域]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}} {{{Domains}}}}}
|-
{{#if:{{{Motifs|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[结构花样|花样]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}} {{{Motifs}}}}}
|-
{{#if:{{{Alternative_products|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}替代產物{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}} {{{Alternative_products}}}}}
|-valign=top
{{#ifexpr:{{#expr:{{#if:{{{Taxa|}}}|1|0}} or {{#if:{{{Cells|}}}|1|0}} or {{#if:{{{Location|}}}|1|0}} or {{#if:{{{Mods|}}}|1|0}} or {{#if:{{{Biophysicochemical_properties|}}}|1|0}} or {{#if:{{{Pathways|}}}|1|0}} or {{#if:{{{Interactions|}}}|1|0}} }}|{{!}}bgcolor=#e7dcc3 colspan=2 align="center"{{!}}'''其他'''}}
|-
{{#if:{{{Taxa|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[分类单位|分类]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Taxa}}}}}
|-
{{#if:{{{Cells|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[List of distinct cell types in the adult human body|細胞類型]]:{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Cells}}}}}
|-
{{#if:{{{Location|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}亚细胞定位{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Location}}}}}
|-
{{#if:{{{Mods|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[共價鍵|共價]]修飾{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Mods}}}}}
|-
{{#if:{{{Pathways|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[信号转导|信号通路]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Pathways}}}}}
|-
{{#if:{{{Interactions|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[分子]]间相互作用{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Interactions}}}}}
|-valign=top
{{#if:{{{Biophysicochemical_properties|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}生物物理化学性质{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Biophysicochemical_properties}}}}}
|-valign=top
{{#ifexpr:{{#expr:{{#if:{{{Catalytic_activity|}}}|1|0}} or {{#if:{{{Cofactors|}}}|1|0}} or {{#if:{{{Km|}}}|1|0}}  or {{#if:{{{Vmax|}}}|1|0}} or {{#if:{{{Enzyme_regulation|}}}|1|0}} }}|{{!}}bgcolor=#e7dcc3 colspan=2 align="center"{{!}}'''Enzymatic Data'''}}
|-valign=top
{{#if:{{{Catalytic_activity|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[催化劑|催化活性]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Catalytic_activity}}}}}
|-
{{#if:{{{Cofactors|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[輔因子]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Cofactors}}}}}
|-
{{#if:{{{Enzyme_regulation|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[酶|酶調節]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Enzyme_regulation}}}}}
|-
{{#if:{{{Km|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[米氏方程|''K''<sub>M</sub>]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Km}}}}}
|-
{{#if:{{{Vmax|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[米氏方程|''V''<sub>Max</sub>]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Vmax}}}}}
|-valign=top
{{#ifexpr:{{#expr:{{#if:{{{Actions|}}}|1|0}} or {{#if:{{{Agonists|}}}|1|0}} or {{#if:{{{Antagonists|}}}|1|0}} }}|{{!}}bgcolor=#e7dcc3 colspan=2 align="center"{{!}}'''受体与配基数据'''}}
|-valign=top
{{#if:{{{Actions|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}作用{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Actions}}}}}
|-valign=top
{{#if:{{{Agonists|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[激动剂]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Agonists}}}}}
|-valign=top
{{#if:{{{Antagonists|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[受体拮抗剂|拮抗剂]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Antagonists}}}}}
|-valign=top
{{#ifexpr:{{#expr:{{#if:{{{Diseases|}}}|1|0}} or {{#if:{{{Pharmaceuticals|}}}|1|0}} or {{#if:{{{Biotechnology|}}}|1|0}} }}|{{!}}bgcolor=#e7dcc3 colspan=2 align="center"{{!}}'''医学与生物技术数据'''}}
|-valign=top
{{#if:{{{Diseases|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[疾病]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Diseases}}}}}
|-
{{#if:{{{Pharmaceuticals|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[药物]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Pharmaceuticals}}}}}
|-
{{#if:{{{Biotechnology|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}[[生物技術|生技應用]]{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Biotechnology}}}}}
|-valign=top
{{#ifexpr:{{#expr:{{#if:{{{EntrezGene|}}}|1|0}} or {{#if:{{{OMIM|}}}|1|0}} or {{#if:{{{RefSeq|}}}|1|0}} or {{#if:{{{UniProt|}}}|1|0}} or {{#if:{{{PDB|}}}|1|0}} or {{#if:{{{ECnumber|}}}|1|0}} or {{#if:{{{Codes|}}}|1|0}} or {{#if:{{{Accession_numbers|}}}|1|0}} }}|{{!}}bgcolor=#e7dcc3 colspan=2 align="center"{{!}}'''資料庫連結'''}}
|-valign=top
{{#if:{{{Accession_numbers|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} 检索号 {{!}}{{!}} style="border-top:1px solid #e7dcc3; " width=220{{!}}[http://www.ncbi.nlm.nih.gov/entrez/viewer.fcgi?val={{{Accession_numbers}}} {{{Accession_numbers}}}]}}
|-valign=top
{{#if:{{{ECnumber|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[EC編號]] {{!}}{{!}} style="border-top:1px solid #e7dcc3; " width=220{{!}}[http://www.expasy.org/enzyme/{{{ECnumber}}} {{{ECnumber}}}]}}
|-valign=top
{{#if:{{{EntrezGene|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[Entrez]] {{!}}{{!}} style="border-top:1px solid #e7dcc3; " width=220{{!}}[http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?db=gene&amp;cmd=retrieve&amp;dopt=default&amp;list_uids={{{EntrezGene}}}&rn=1 {{{EntrezGene}}}]}}
|-valign=top
{{#if:{{{OMIM|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[OMIM]] {{!}}{{!}} style="border-top:1px solid #e7dcc3; " width=220{{!}}[http://www.ncbi.nlm.nih.gov/entrez/dispomim.cgi?id={{{OMIM}}}&rn=1 {{{OMIM}}}]}}
|-valign=top
{{#if:{{{CASNo|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[CAS號]] {{!}}{{!}} style="border-top:1px solid #e7dcc3; " width=220{{!}}{{#invoke:Chembox CASNo|main|hideNone=yes}} }}
|-valign=top
{{#if:{{{PDB|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[蛋白质数据库|PDB]] {{!}}{{!}} style="border-top:1px solid #e7dcc3; " width=220{{!}}[http://www.pdb.org/pdb/cgi/explore.cgi?pdbId={{{PDB}}} {{{PDB}}}]}}
|-valign=top
{{#if:{{{RefSeq|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[美国国家生物技术信息中心|RefSeq]] {{!}}{{!}} style="border-top:1px solid #e7dcc3;" width=220{{!}}[http://genome.cse.ucsc.edu/cgi-bin/hgGene?org=Human&amp;hgg_gene={{{RefSeq}}}&rn=1 {{{RefSeq}}}]}}
|-valign=top
{{#if:{{{UniProt|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [[Swiss-Prot|UniProt]] {{!}}{{!}} style="border-top:1px solid #e7dcc3; " width=220{{!}}[http://www.expasy.org/uniprot/{{{UniProt}}} {{{UniProt}}}]}}
|-valign=top
{{#if:{{{Codes|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}} [http://www.gene.ucl.ac.uk/nomenclature/data/get_data.php?hgnc_id=HGNC:{{{HGNCid}}} 编号:] {{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}} {{{Codes}}}}}
|-valign=top
{{#ifexpr:{{#expr:{{#if:{{{Pages|}}}|1|0}} or {{#if:{{{Review|}}}|1|0}}}}|{{!}}bgcolor=#e7dcc3 colspan=2 align="center"{{!}}'''相關資訊'''}}
|-valign=top
{{#if:{{{Pages|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}相关文獻{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}}{{{Pages}}}}}
|-valign=top
{{#if:{{{Review|}}}|
{{!}} bgcolor=#e7dcc3 width=85{{!}}最近發表{{!}}{{!}}style="border-top:1px solid #e7dcc3" width=220{{!}} {{{Review}}}}}

|}<noinclude>

==关于这个模板==
这个模板提供有关蛋白质分子的信息。请参考[[:en:Wikipedia:WikiProject Molecular and Cellular Biology/protbox usage|protbox usage]]。这个模板的很多参数都是可以选择的，您可以不使用不需要的参数。 


{{esoteric}}
[[Category:化学信息框模板|{{PAGENAME}}]]

</noinclude>