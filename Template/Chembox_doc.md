{{Documentation subpage}}
{{high-use|6101}}
化学信息框模板（Chembox）用于为[[化学物质]]相关条目提供一个直观的列出辨识和性质的表格，具体说明与讨论请阅读[[维基百科:化学信息框]]。这里仅列出与如何使用本模板的相关信息。

== 使用前的注意事项 ==
在开始应用化学信息框之前，有以下需要注意的事项：
# 化学信息框不是万能的。还有很多不同的信息框模板供你选择，例如，表述药物分子的条目或许用{{tl|Infobox_Drug}}更合适。
# 切勿展开本模板。不要用<nowiki>{{subst:}}</nowiki>展开本模板，这样会产生大量表格样式和逻辑判断代码，影响条目本身的编辑。右邊是用<nowiki>{{subst:Chembox}}</nowiki>的後果。
# 不需要删除空缺的参数。空参数不会在条目中显示，但是保留空缺参数可以方便其他编者补充数据。你可以删除不适用的小节，例如，很多化学物质不会爆炸，不需要爆炸性相关的小节。
# 不用追求大而全。过长的表格会失去其直观展示的目的，如果有很多数据需要展示，可以另外编辑条目附属的补充数据页（<nowiki>[[条目名/数据页]]</nowiki>），将一些数据转移到那里去，参见[[#数据页]]。

== 开始使用 ==
化学信息框采用模块化设计，主模块仅仅显示化学物质的名称和图片，其余信息以模块化的小节（Section）形式展现。当前可以加入的小节包括识别{{tl|Chembox Identifiers}}，性质{{tl|Chembox Properties}}，结构{{tl|Chembox Structure}}，热力学数据{{tl|Chembox Thermochemistry}}，药理学数据{{tl|Chembox Pharmacology}}，爆炸性{{tl|Chembox Explosive}}，危险性{{tl|Chembox Hazards}}，相关化学品{{tl|Chembox Related}}。这些小节模块可以根据不同化学物质的实际特点进行取舍。

=== 使用生成模板 ===
可以使用以下的可展开模板来生成化学信息框，用法为在条目开端加入<nowiki>{{subst:模板名}}</nowiki>，保存，然后再编辑即可填入参数对应数据。
* {{tl|Chembox subst small}}：简洁版，仅包含最常用属性，参数名为英文。用法为'''<nowiki>{{subst:Chembox subst small}}</nowiki>'''
** {{tl|Chembox subst hans}}：简洁版对应的参数名简体中文的版本。用法为'''<nowiki>{{subst:Chembox subst hans}}</nowiki>'''
**{{tl|Chembox subst hant}}：简洁版对应的参数名为繁体中文的版本。用法为'''<nowiki>{{subst:Chembox subst hant}}</nowiki>'''
* {{tl|Chembox subst medium}}：中型版，包含稍复杂的参数。用法为'''<nowiki>{{subst:Chembox subst small}}</nowiki>'''
* {{tl|Chembox subst large}}：复杂版，包含更多参数。用法为'''<nowiki>{{subst:Chembox subst large}}</nowiki>'''
* {{tl|Chembox subst full}}：完全版，包含全部可选参数，甚至包括互斥参数，使用时需要自行取舍。用法为'''<nowiki>{{subst:Chembox subst full}}</nowiki>'''

以上每个生成模板具体包含的参数与下一节的描述相对应，也可以在生成模板的文档中找到相应说明。

特殊版本的生成模板包括：
* {{tl|Chembox subst drug}}：带有多数药物识别参数和药理学小节的中型版。用法为'''<nowiki>{{subst:Chembox subst drug}}</nowiki>'''
* {{tl|Chembox subst explosive}}：带有爆炸性小节的中型版。用法为'''<nowiki>{{subst:Chembox subst explosive}}</nowiki>'''

=== 从这里复制 ===
您也可以直接从这里复制化学信息框，并粘贴到化学物质条目中，其效果与使用生成模板相同。

==== 简洁版 ====
复制粘贴以下内容到待编辑条目，相当于使用'''<nowiki>{{subst:Chembox subst small}}</nowiki>'''、'''<nowiki>{{subst:Chembox subst hans}}</nowiki>'''及'''<nowiki>{{subst:Chembox subst hant}}</nowiki>'''：
{|
|英文版
|简体中文版
|繁体中文版
|-
|
<pre>
{{Chembox
| Name = 
| NameEn = 
| ImageFile = 
|  ImageSize = 
|  ImageAlt = 
| IUPACName = 
| IUPACNameZh = 
| OtherNames = 
| Section1 = {{Chembox Identifiers
|   CASNo = 
|   CASNo_Ref = {{cascite}}
|   PubChem = 
|   SMILES =  }}
| Section2 = {{Chembox Properties
|   Formula = 
|   MolarMass = 
|   Appearance = 
|   Density = 
|   MeltingPt = 
|   BoilingPt = 
|   Solubility =  }}
| Section3 = {{Chembox Hazards
|   MainHazards = 
|   FlashPt = 
|   Autoignition =  }}
}}
</pre>
|
<pre>
{{Chembox
| 名称 = 
| 英文名 = 
| 图像文件 = 
|  图像大小 = 
|  图像替换 = 
| IUPAC英 = 
| IUPAC中 =
| 别名 = 
| Section1 = {{Chembox 识别
|   CAS号 = 
|   CASNo_Ref = {{cascite}}
|   PubChem = 
|   SMILES =  }}
| Section2 = {{Chembox 性质
|   化学式 = 
|   摩尔质量 = 
|   外观 = 
|   密度 = 
|   熔点 = 
|   沸点 = 
|   溶解度 =  }}
| Section3 = {{Chembox 危险性
|   主要危险 = 
|   闪点 = 
|   自燃点 =  }}
}}
</pre>
|
<pre>
{{Chembox
| 名稱 = 
| 英文名 = 
| 圖像檔案 = 
|  圖像大小 = 
|  圖像替換 = 
| IUPAC英 = 
| IUPAC中 =
| 別名 = 
| Section1 = {{Chembox 識別
|   CAS號 = 
|   CASNo_Ref = {{cascite}}
|   PubChem = 
|   SMILES =  }}
| Section2 = {{Chembox 性質
|   化學式 = 
|   摩爾質量 = 
|   外觀 = 
|   密度 = 
|   熔點 = 
|   沸點 = 
|   溶解度 =  }}
| Section3 = {{Chembox 危險性
|   主要危險 = 
|   閃點 = 
|   自燃點 =  }}
}}
</pre>
|}

==== 中型版 ====
复制粘贴以下内容到待编辑条目，相当于使用'''<nowiki>{{subst:Chembox subst medium}}</nowiki>'''：
{|
|-
| 
<pre>
{{Chembox
| Name = 
| NameEn = 
| ImageFile = 
|  ImageSize = 
|  ImageAlt = 
|  ImageName =
| ImageFileL1 =
|  ImageSizeL1 = 
|  ImageAltL1 = 
|  ImageNameL1 = 
| ImageFileR1 =
|  ImageSizeR1 = 
|  ImageAltR1 = 
|  ImageNameR1 = 
| IUPACName = 
| IUPACNameZh = 
| OtherNames = 
| Abbreviations = 
| Section1 = {{Chembox Identifiers
|  CASNo = 
|  EINECS = 
|  PubChem = 
|  SMILES = 
|  InChI = 
|  RTECS =
|  MeSHName =
|  ChEBI =
|  KEGG = 
|  ATCCode_prefix = 
|  ATCCode_suffix = 
|  ATC_Supplemental = }}
| Section2 = {{Chembox Properties
|  Formula = 
|  MolarMass =
|  Appearance =
|  Density = 
|  MeltingPt = 
|  Melting_notes =
|  BoilingPt = 
|  Boiling_notes = 
|  Solubility = 
|  SolubleOther = 
|  Solvent = 
|  pKa = 
|  pKb = }}
| Section3 = {{Chembox Hazards
|  EUClass = 
|  EUIndex = 
|  MainHazards = 
|  NFPA-H = 
|  NFPA-F = 
|  NFPA-R = 
|  NFPA-O =
|  RPhrases = 
|  SPhrases = 
|  RSPhrases =
|  FlashPt = 
|  Autoignition = 
|  ExploLimits = 
|  PEL = }}
| Section4 = {{Chembox Related
|  Function = 
|  OtherAnions = 
|  OtherCations = 
|  OtherCpds =
|  OtherFunctn =  }}
}}
</pre>
|}

==== 复杂版 ====
复制粘贴以下内容到待编辑条目，相当于使用'''<nowiki>{{subst:Chembox subst large}}</nowiki>'''：
{|
|-
| 
<pre>
{{Chembox
| Name = 
| NameEn = 
| ImageFile = 
|  ImageSize = 
|  ImageAlt = 
|  ImageName = 
| ImageFile1 =
|  ImageSize1 = 
|  ImageAlt1 = 
|  ImageName1 = 
| ImageFile2 =
|  ImageSize2 = 
|  ImageAlt2 = 
|  ImageName2 = 
| ImageFile3 =
|  ImageSize3 = 
|  ImageAlt3 = 
|  ImageName3 = 
| ImageFileL1 =
|  ImageSizeL1 = 
|  ImageAltL1 = 
|  ImageNameL1 = 
| ImageFileR1 =
|  ImageSizeR1 = 
|  ImageAltR1 = 
|  ImageNameR1 = 
| ImageFileL2 =
|  ImageSizeL2 = 
|  ImageAltL2 = 
|  ImageNameL2 = 
| ImageFileR2 =
|  ImageSizeR2 = 
|  ImageAltR2 = 
|  ImageNameR2 = 
| IUPACName = 
|  IUPACNameZh = 
|  SystematicName = 
|  OtherNames = 
| Abbreviations =
| Section1 = {{Chembox Identifiers
|  3DMet =
|  ATCvet = 
|  ATCCode_prefix = 
|  ATCCode_suffix = 
|  ATC_Supplemental =
|  Beilstein =
|  CASNo = 
|  CASNo_Ref =
|  CASNos =
|  CASOther =
|  ChEBI =
|  ChemSpiderID =
|  DrugBank =
|  EC-number =
|  EINECS = 
|  EINECSCASNO = 
|  Gmelin =
|  InChI = 
|  KEGG =
|  MeSHName =
|  PubChem = 
|  RTECS = 
|  SMILES = 
|  UNNumber =
}}
| Section2 = {{Chembox Properties
|  AtmosphericOHRateConstant = 
|  Appearance = 
|  BoilingPt = 
|  Boiling_notes = 
|  Density = 
|  Formula = 
|  HenryConstant = 
|  LogP = 
|  MolarMass = 
|  MeltingPt = 
|  Melting_notes = 
|  pKa = 
|  pKb =
|  Solubility = 
|  SolubleOther = 
|  Solvent = 
|  VaporPressure =}}
| Section3 = {{Chembox Structure 
|  Coordination =
|  CrystalStruct = 
|  MolShape = }}
| Section4 = {{Chembox Thermochemistry
|  DeltaHc =
|  DeltaHf =  
|  Entropy = 
|  HeatCapacity = }}
| Section5 = {{Chembox Pharmacology
|  AdminRoutes = 
|  Bioavail = 
|  Excretion = 
|  HalfLife = 
|  Metabolism = 
|  Legal_status = 
|  Legal_US = 
|  Legal_UK = 
|  Legal_AU = 
|  Legal_CA = 
|  PregCat = 
|  PregCat_AU = 
|  PregCat_US =
|  ProteinBound = }}
| Section6 = {{Chembox Explosive
|  ExplosiveV = 
|  FrictionSens = 
|  REFactor =
|  ShockSens = }}
| Section7 = {{Chembox Hazards
|  Autoignition = 
|  EUClass = 
|  EUIndex = 
|  ExploLimits = 
|  ExternalMSDS = 
|  FlashPt = 
|  LD50 =
|  MainHazards = 
|  NFPA-H = 
|  NFPA-F = 
|  NFPA-R = 
|  NFPA-O = 
|  PEL =
|  RPhrases = 
|  RSPhrases = 
|  SPhrases = }}
| Section8 = {{Chembox Related
|  Function = 
|  OtherAnions = 
|  OtherCations = 
|  OtherCpds =
|  OtherFunctn =  }}
}}
</pre>
|}

==== 完全版 ====
参见下文的[[#全部参数]]。

=== 直接套用 ===
化学信息框的参数名和小节名兼容英文维基百科的[[:en:Template:Chembox]]和衍生自[[:en:Template:Chembox]]的其他语言化学信息框。英文条目的化学信息框仅需做极少修改就可以直接套用，除了必要的翻译数据（如外观等）外，还需注意：
* 中文化学信息框属性（Properties）一节中的摩尔质量（MolarMass）自带单位，可以把英文条目中的g/mol去掉。
* 日文化学信息框危险性（Hazards）一节中的危险和安全警示词（SPhrases/RPhrases）需要将形如<nowiki>{{R-phrases|10|11|12}}</nowiki>拆为<nowiki>{{R10}}，{{R11}}，{{R12}}</nowiki>。
* 英文版的OtherCompounds参数在这里并不适用，需要改成OtherCpds。

=== 自行取舍 ===
如果你经常需要创建同一类的化学物质条目，可以自行取舍模块和参数，将需要的部分从[[#完全版]]中复制到自己的用户页或用户页子页面备用。

=== [[ChemSpider]] ===
ChemSpider.com提供了自动生成化学信息框的功能，在用户界面选择wikibox即可弹出相应的chembox供复制。

== 全部参数 ==
这里列出本模板所有的参数，复制下面的代码相当于使用'''<nowiki>{{subst:Chembox subst full}}</nowiki>'''：

{|
|- valign=top
| 
<pre>
{{Chembox
| Reference = 
| Name = 
| NameEn = 
| ImageFile = 
|  ImageSize = 
|  ImageAlt = 
|  ImageName = 
| ImageFile1 =
|  ImageSize1 = 
|  ImageAlt1 = 
|  ImageName1 = 
| ImageFileL1 =
|  ImageSizeL1 = 
|  ImageAltL1 = 
|  ImageNameL1 = 
| ImageFileR1 =
|  ImageSizeR1 = 
|  ImageAltR1 = 
|  ImageNameR1 = 
| ImageFile2 =
|  ImageSize2 = 
|  ImageAlt2 = 
|  ImageName2 = 
| ImageFileL2 =
|  ImageSizeL2 = 
|  ImageAltL2 = 
|  ImageNameL2 = 
| ImageFileR2 =
|  ImageSizeR2 = 
|  ImageAltR2 = 
|  ImageNameR2 = 
| ImageFile3 =
|  ImageSize3 = 
|  ImageAlt3 = 
|  ImageName3 = 
| CustomizedImage = 
| IUPACName = 
|  IUPACNameZh = 
|  SystematicName = 
|  SystematicNameZh = 
|  OtherNames = 
|  Abbreviations = 
|  INN = 
|   rINN = 
|   pINN = 
|  CADN = 
|  USAN = 
|  BAN =  
| Section1 = {{Chembox Identifiers
|  CASNo = 
|   CASNo_url = 
|   CASNo_Comment = 
|   CASNo1 = 
|    CASNo1_url = 
|    CASNo1_Comment = 
|   CASNo2 = 
|    CASNo2_url = 
|    CASNo2_Comment = 
|   CASNo3 = 
|    CASNo3_url = 
|    CASNo3_Comment = 
|   CASNo4 = 
|    CASNo4_url = 
|    CASNo4_Comment = 
|   CASNo5 = 
|    CASNo5_url = 
|    CASNo5_Comment = 
|  CASNos =
|  CASOther =
|  PubChem = 
|   PubChem_Comment = 
|   PubChem1 = 
|    PubChem1_Comment =
|   PubChem2 = 
|    PubChem2_Comment =
|   PubChem3 = 
|    PubChem3_Comment =
|   PubChem4 = 
|    PubChem4_Comment =
|   PubChem5 = 
|    PubChem5_Comment =
|  PubChems =
|  PubChemOther =
|  ChemSpiderID = 
|   ChemSpiderID_Comment = 
|   ChemSpiderID1 = 
|    ChemSpiderID1_Comment = 
|   ChemSpiderID2 = 
|    ChemSpiderID2_Comment = 
|   ChemSpiderID3 = 
|    ChemSpiderID3_Comment = 
|   ChemSpiderID4 = 
|    ChemSpiderID4_Comment = 
|   ChemSpiderID5 = 
|    ChemSpiderID5_Comment = 
|  ChemSpiderIDs =  
|  ChemSpiderIDOther =  
|  SMILES = 
|  InChI = 
|  InChIKey = 
|  Beilstein =
|  Gmelin =
|  3DMet =
|  UNNumber =
|  EC-number =
|   EINECS = 
|   ELINCS = 
|   NLP = 
|  ChEBI =
|  RTECS = 
|  E_number = 
|  FEMA = 
|  DrugBank = 
|  KEGG = 
|  MeSHName = 
|  IUPHAR_ligand = 
|  ATCCode = 
|   ATCvet = 
|   ATCCode_prefix = 
|   ATCCode_suffix = 
|    ATC_Supplemental =  }}
| Section2 = {{Chembox Properties
|  Reference = 
|  C = | H = | O = 
|  Formula = 
|  MolarMass = 
|   MolarMass_notes = 
|  ExactMass = 
|  MolarMassOther = 
|  Appearance = 
|  Odor = 
|  Density = 
|   DensitySolid = 
|   DensityLiquid = 
|   DensityGas = 
|  MeltingPt = 
|   MeltingPtC = 
|    MeltingPtCL =
|    MeltingPtCH =
|   MeltingPtK = 
|    MeltingPtKL =
|    MeltingPtKH =
|   Melting_notes = 
|  BoilingPt = 
|   BoilingPtC = 
|    BoilingPtCL =
|    BoilingPtCH =
|   BoilingPtK = 
|    BoilingPtKL =
|    BoilingPtKH =
|   BoilingPt_notes = 
|  SublimationConditions = 
|  CriticalPt = 
|   CriticalPt_notes = 
|  Solubility = 
|  SolubilityProduct = 
|   SolubilityProductAs = 
|  SolubleOther = 
|   Solvent = 
|  Solubility1 = 
|   Solvent1 = 
|  Solubility2 = 
|   Solvent2 = 
|  Solubility3 = 
|   Solvent3 = 
|  Solubility4 = 
|   Solvent4 = 
|  Solubility5 = 
|   Solvent5 = 
|  SolOther = 
|  LogP = 
|  VaporPressure = 
|  HenryConstant = 
|  AtmosphericOHRateConstant = 
|  pKa = 
|   pKa1 = 
|   pKa2 = 
|   pKa3 = 
|   pKa4 = 
|   pKa5 = 
|   pKa6 = 
|  pKb =
|   pKb1 = 
|   pKb2 = 
|   pKb3 = 
|   pKb4 = 
|   pKb5 = 
|   pKb6 = 
|  IsoelectricPt = 
|  LambdaMax = 
|  Absorbance = 
|  BandGap = 
|   BandGap_notes = 
|  ElectronMobility = 
|  SpecRotation = 
|   SpecRotation_t = 
|   SpecRotation_l = 
|  MagSus = 
|  ThermalConductivity = 
|  RefractIndex = 
|   RefractIndex_t = 
|   RefractIndex_l = 
|  Viscosity = 
|  CriticalRelativeHumidity = 
|  SpecificSurfaceArea = 
|  PoreVolume = 
|  AveragePoreSize =  }}
| Section3 = {{Chembox Structure
|  Reference = 
|  CrystalStruct = 
|  SpaceGroup = 
|  Coordination = 
|  LattConst_a = 
|   LattConst_b = 
|   LattConst_c = 
|  LattConst_alpha = 
|   LattConst_beta = 
|   LattConst_gamma = 
|  MolShape = 
|  OrbitalHybridisation = 
|  Dipole =  }}
| Section4 = {{Chembox Thermochemistry
|  Reference = 
|  DeltaHf = 
|  DeltaHc = 
|  Entropy = 
|  HeatCapacity =
|   Cp = 
|   Cv =  }}
| Section5 = {{Chembox Pharmacology
|  Reference = 
|  Bioavail = 
|  AdminRoutes = 
|  Metabolism = 
|  Metabolites = 
|  HalfLife = 
|  ProteinBound =
|  Excretion = 
|  Licence_EU = 
|  Licence_US = 
|  Legal_status = 
|   Legal_AU = 
|   Legal_CA = 
|   Legal_UK = 
|   Legal_US = 
|  PregCat = 
|   PregCat_AU = 
|   PregCat_CA =
|   PregCat_DE = 
|   PregCat_UK =
|   PregCat_US =  }}
| Section6 = {{Chembox Explosive
|  Reference = 
|  ShockSens = 
|  FrictionSens = 
|  ExplosiveV = 
|  REFactor = }}
| Section7 = {{Chembox Hazards
|  Reference = 
|  ExternalMSDS = 
|  EUIndex = 
|  EUHazardSymbol = 
|  EUHSref =
|  EUClass = 
|  RPhrases = 
|  SPhrases = 
|  RSPhrases = 
|  GHSPictograms = 
|  GHSSignalWord = 
|  HPhrases = 
|  PPhrases = 
|  MainHazards = 
|  IngestionHazard = 
|  InhalationHazard = 
|  EyeHazard = 
|  SkinHazard = 
|  NFPA-H = 
|  NFPA-F = 
|  NFPA-R = 
|  NFPA-O = 
|  FlashPt = 
|  Autoignition = 
|  ExploLimits = 
|  PEL = 
|  TLV = 
|   MAK = 
|   MELS = 
|  LD50 = 
|   LC50 = 
|   LCt50 =  }}
| Section8 = {{Chembox Related
|  OtherAnions = 
|  OtherCations = 
|  OtherFunctn = 
|  Function = 
|  OtherCpds = }}
}}
</pre>
|
<pre>
Chembox 参数说明
* Reference/-{參考}-/-{参考}-：参考资料，标注在化学物质名称的右方。
* Name/-{名稱}-/-{名称}-：化学物质名（如空缺，默认值为条目名称）。
* NameEn/英文名：化学物质的英文名。
* ImageFile/-{圖像檔案}-/-{图像文件}-：图像文件名，如：filename.svg（仅文件名，无需[[File:]]格式）。
* ImageSize/-{圖像大小}-/-{图像大小}-：图像宽度大小，如：ImageSize = 100px（默认值为200px）。
* ImageAlt/-{圖像替換}-/-{图像替换}-：图像的替代文字，如：ImageAlt = 白色粉末。
* ImageName/-{圖像名稱}-/-{图像名称}-：图像的标题名称，如：ImageName = 乙醇的球棍模型。
* 同上，另一组图像参数。参数也可用中文，形如：ImageFile1/-{圖像檔案1}-/-{图像文件1}-。



* 另一组图像参数，此图片将和ImageFileR1并排展示。参数可用中文，形如：ImageNameL1/-{圖像名稱左1}-/-{图像名称左1}-。



* 与ImageFileL1并排的图片。参数可用中文，形如：ImageNameR1/-{圖像名稱右1}-/-{图像名称右1}-。



* 另一组图像参数，仅有英文参数。



* 另一组左右并排展示图片，仅有英文参数。







* 另一组图像参数，仅有英文参数。



* CustomizedImage/-{定制圖像}-/-{定制图像}-：自定义图像，只要符合维基语法，可任意发挥。
* IUPACName/IUPAC英：IUPAC英文命名。
* IUPACNameZh/IUPAC中：IUPAC中文命名。
* SystematicName/-{系統名}-/-{系统名}-：IUPAC系统名。
* SystematicNameZh/-{中文系統名}-/-{中文系统名}-：中文系统命名法命名，若IUPAC中文系统名夾帶繁簡轉換用的括號時請加入<nowiki><nowiki></nowiki></nowiki>。
* OtherNames/-{別名}-/-{别名}-：其他名称。
* Abbreviations/-{縮寫}-/-{缩写}-：缩写，如氨基酸缩写，配体缩写。
* INN：国际非专利药品名称。
* rINN：推荐国际非专利药品名称。
* pINN：提议国际非专利药品名称。以上三参数选一。
* CADN：中国药物通用名。
* USAN：美国药物通用名。
* BAN：英国药物通用名。
Identifiers/-{識別}-/-{识别}-：识别小节，主要是各种编码和检索方式。
* CASNo/-{CAS號}-/-{CAS号}-：美国化学会化学文摘CAS索引号。
* CASNo_url：CAS查询网址，默认值为CAS官方的www.commonchemistry.org
* CASNo_Comment：注释，可选参数。如：一水合物，左旋。
* 另一组CAS索引号。


* 另一组CAS索引号。


* 另一组CAS索引号。


* 另一组CAS索引号。


* 另一组CAS索引号。

  ^-上述可带有自定义url，注释和参考资料的CASNo共6组-^
* CASNos：没有详细参数的CAS号，用户可以自定义表现形式。
* CASOther：另一个可以自定义的CAS号。
* PubChem：PubChem索引号，带有pubchem.ncbi.nlm.nih.gov的查询链接。 
* PubChem_Comment：注释，可选参数。如：一水合物。
* 另一组PubChem。

* 另一组PubChem

* 另一组PubChem

* 另一组PubChem

* 另一组PubChem
  ^-上述PubChem属性共6组-^
* PubChems：不自动带查询链接的PubChem号，用户可以自定义表现形式。
* PubChemOther：另一个可自定义的PubChem。
* ChemSpiderID: ChemSpider网络数据库索引号，带有www.chemspider.com查询链接。
* ChemSpiderID_Comment：注释，可选参数。如：一水合物。
* 另一组ChemSpiderID

* 另一组ChemSpiderID

* 另一组ChemSpiderID

* 另一组ChemSpiderID

* 另一组ChemSpiderID

* ChemSpiderIDs：不自动带查询链接的ChemSpiderID，用户可以自定义表现形式。
* ChemSpiderIDOther：另一个可自定义的ChemSpiderID。
* SMILES：简化分子线性输入规范。
* InChI：国际化合物标识。
* InChIKey：InChI散列值。
* Beilstein：伯恩斯坦有机物数据库登记号。
* Gmelin：盖墨林无机物数据库索引号。
* 3DMet：3DMet数据库收录号。
* UNNumber/-{UN編號}-/-{UN编号}-：联合国危险货物编号。
* EC-number/-{EC編號}-/-{EC编号}-：欧盟编号，带有查询链接。
* EINECS：欧洲现有商业化学品目录，已并入EC-number。
* ELINCS：欧洲申报化学物质名录，已并入EC-number。
* NLP：更新非聚合物名录，已并入EC-number。以上四个参数仅可使用一个。
* ChEBI：ChEBI数据库索引，带有查询链接。
* RTECS：化学物质毒性数据库索引。
* E_number/-{E編號}-/-{E编码}-：欧盟食品添加剂编码。
* FEMA：美国食品添加剂公认安全名单，带有联合国粮农组织查询链接。
* DrugBank：DrugBank数据库索引，带有查询链接。
* KEGG：京都遺伝子ゲノム百科事典数据库索引，带有查询链接。
* MeSHName/-{醫學主題詞}-/-{医学主题词}-：医学主题词关键字，带有查询链接。
* IUPHAR_ligand/-{IUPHAR配體}-/-{IUPHAR配体}-：IUPHAR配体索引，以及其在www.iuphar-db.org的记录链接。
* ATCCode/-{ATC碼}-/-{ATC码}-：药物分子的解剖学治疗学及化学分类系统(ATC)代码。
* ATCvet：若为兽医用药请填入“yes”，默认或不设置为否。
* ATCCode_prefix/-{ATC碼前綴}-/-{ATC码前缀}-：ATC码前缀，与后缀结合使用
* ATCCode_suffix/-{ATC碼後綴}-/-{ATC码后缀}-：若已设定ATCCode参数，ATCCode_prefix和ATCCode_surffix会列于其之后。
* ATC_Supplemental/-{ATC補充}-/-{ATC补充}-：如有更多ATCCode，可用{{ATCCode}}模板加入在此处，如：ATC_supplemental ={{ATC|M02|AA15}}，{{ATC|S01|BC03}}。
Properties/-{性質}-/-{性质}-：性质小节，主要是化学物质的物理性质和少量化学性质。
* Reference/-{參考}-/-{参考}-：参考资料，标注在小节标题右上角。
* 元素符号参数，可以用所有已知化学元素做为参数名。例如：| C = 5 | H = 12 | O = 1，会自动生成下面的化学式和摩尔质量。
* Formula/-{化學式}-/-{化学式}-：化学物物质的化学式。
* MolarMass/-{摩爾質量}-/-{摩尔质量}-：化学物质的摩尔质量，仅需数字，会自动添加g/mol单位。
* MolarMass_notes：注释，会置于g/mol单位之后。
* ExactMass：精确质量。指定同位素的化学物质的计算分子量（无量纲）。
* MolarMassOther：化学物质的摩尔质量，不带单位，可以自定义格式。
* Appearance/-{外觀}-/-{外观}-：外观性状。
* Odor/Odour/-{氣味}-/-{气味}-：气味，可以合并写入外观里。
* Density/密度：密度，需自行添加单位。
* DensitySolid：固体密度，会自动加入单位g·cm^-3。
* DensityLiquid：液体密度，会自动加入单位g·ml^-1。
* DensityGas：气体密度，会自动加入单位kg·m^-3。
* MeltingPt/-{熔點}-/-{熔点}-：熔点，需自行添加单位。
* MeltingPtC：摄氏温标熔点，会自动添加单位，并计算华氏和绝对温标数值。
* MeltingPtCL：摄氏温标熔点范围低端，若无MetlingPtCH则与MeltingPtC等价，会自动添加单位，并计算华氏和绝对温标数值。
* MeltingPtCH：：摄氏温标熔点范围高端，与MeltingPtCL配对，会自动添加单位，并计算华氏和绝对温标数值
* MeltingPtK：绝对温标熔点，会自动添加单位，并计算摄氏和华氏温标数值。
* MeltingPtKL：绝对温标熔点范围低端，若无MetlingPtKH则与MeltingPtK等价，会自动添加单位，并计算摄氏和华氏温标数值。
* MeltingPtKH：绝对温标熔点范围高端，与MeltingPtKL配对，会自动添加单位，并计算摄氏和华氏温标数值。
* Melting_notes：熔点注释，会置于温度单位之后。以上熔点数据互斥，请自行选择合适的一个使用。
* BoilingPt/-{沸點}-/-{沸点}-：参数设置与沸点相同。







* SublimationConditions/-{升華條件}-/-{升华条件}-：升华条件。
* CriticalPt/-{臨界點}-/-{临界点}-：临界点条件（温度及压力）。
* CriticalPt_notes：临界点注释。
* Solubility：在水中的溶解性或溶解度。
* SolubilityProduct/Ksp：溶度积。
* SolubilityProductAs：溶度积实际表示物质，与上一参数配合使用，可选参数。
* SolubleOther/溶解度：溶解度。
* Solvent/-{溶劑}-/-{溶剂}-：溶剂，与上一参数配合使用，可选参数。
* Solubility1：在Solvent1中的溶解度，与Solvent1参数配合使用。
* Solvent1：溶剂，与Solubility1配合使用
* 另一组溶解度和溶剂

* 另一组溶解度和溶剂

* 另一组溶解度和溶剂

* 另一组溶解度和溶剂

* SolOther/溶解度其他：在其他溶剂中的溶解度。
* LogP：化学物质在正辛醇-水体系中的分配系数。
* VaporPressure/-{蒸氣壓}-/-{蒸气压}-：蒸气压。
* HenryConstant/-{亨利常數}-/-{亨利常数}-：亨利常数。
* AtmosphericOHRateConstant：大气中与·OH自由基反应速率。
* pKa：酸离解常数。可用逗号分隔多元酸的pKa1/pKa2等，也可用下面的系列参数。
* pKa1：一级离解常数。与pKa互斥。
* 多元酸的多级离解常数，直到pKa6




* pKb：碱离解常数，与pKa使用方法相同。






* IsoelectricPt/pI/-{等電點}-/-{等电点}-：等电点。
* LambdaMax/-{最大吸收波長}-/-{最大吸收波长}-：UV-Vis吸收光谱最大吸收波长。
* Absorbance/吸光度：吸光度，应指明波长，默认为最大吸收波长处吸光度。
* BandGap/能隙/带隙：能隙，自带单位电子伏eV。
* BandGap_notes：能隙注释，会置于电子伏单位后。
* ElectronMobility/-{電子遷移率}-/-{电子迁移率}-：电子迁移率。
* SpecRotation：比旋光度。
* SpecRotation_t：比旋光度数据的温度条件，默认值20摄氏度。
* SpecRotation_l：比旋光度数据的谱线条件，默认值为钠灯D线。
* MagSus：磁化率。
* ThermalConductivity：热导率。
* RefractIndex：折射率/折光度。
* RefractIndex_t：折射率数据的温度条件。
* RefractIndex_l：折射率数据的谱线条件，默认值为钠灯D线。
* Viscosity/-{黏度}-/-{粘度}-：粘度。
* CriticalRelativeHumidity： 临界相对湿度。
* SpecificSurfaceArea：比表面积。
* PoreVolume：孔隙体积。
* AveragePoreSize：平均孔径。
Structure/-{結構}-/-{结构}-：分子构型和晶体结构信息。
* Reference/-{參考}-/-{参考}-：参考资料，标注在小节标题右上角
* CrystalStruct：晶体结构。
* SpaceGroup：空间群。
* Coordination：配位几何。
* LattConst_a：晶格参数 a。
* LattConst_b：晶格参数 b。
* LattConst_c：晶格参数 c。
* LattConst_alpha：晶格参数 α，默认值90°。
* LattConst_beta：晶格参数 β，默认值90°。
* LattConst_gamma：晶格参数 γ，默认值90°。
* MolShape：分子构型。
* OrbitalHybridisation：杂化轨道。
* Dipole：偶极矩。
Thermochemistry/-{熱力學}-/-{热力学}-：热力学相关属性
* Reference/-{參考}-/-{参考}-：参考资料，标注在小节标题右上角。
* DeltaHf：标准摩尔生成焓。
* DeltaHc：标准摩尔燃烧焓。
* Entropy：标准摩尔熵。
* HeatCapacity：热容。
* Cp：定压热容。
* Cv：定容热容。
Pharmacology/-{藥理}-/-{药理}-：药理学和药品相关数据
* Reference/-{參考}-/-{参考}-：参考资料，标注在小节标题右上角。
* Bioavail：生物利用度。
* AdminRoutes：给药途径
* Metabolism：代谢。
* Metabolites：代谢产物。
* HalfLife：消除半衰期。
* ProteinBound：蛋白结合率。
* Excretion：排泄。
* Licence_EU：欧盟（EMEA）药品许可证。
* Licence_US：美国（FDA）药品许可证。
* Legal_status：法律规定的药品分类分级。
* Legal_AU：澳大利亚药品分级。
* Legal_CA：加拿大药品分级。
* Legal_UK：英国药品分级。
* Legal_US：美国药品分级。
* PregCat：妊娠期药物分类。
* PregCat_AU：澳大利亚妊娠期药物分类。
* PregCat_CA：加拿大妊娠期药物分类。
* PregCat_DE：德国妊娠期药物分类。
* PregCat_UK：英国妊娠期药物分类。
* PregCat_US：美国妊娠期药物分类。 }}
Explosive/爆炸性：爆炸性相关数据
* Reference/-{參考}-/-{参考}-：参考资料，标注在小节标题右上角。
* ShockSens：撞击感度。
* FrictionSens：摩擦感度。
* ExplosiveV：爆速。
* REFactor：相对TNT当量系数。
Hazards/-{危險性}-/-{危险性}-
* Reference/-{參考}-/-{参考}-：参考资料，标注在小节标题右上角。
* ExternalMSDS：外部MSDS链接。
* EUIndex：欧盟危险品索引。
* EUHazardSymbol：欧盟危险品符号，例：EUHazardSymbol = {{Chembox EUHazardSymbol|Xn|T}}
* EUHSref：欧盟危险品符号的参考资料
* EUClass：欧盟化学物质分类。
* RPhrases：欧盟化学品风险术语，例：RPhrases = {{R21}}，{{R35}}
* SPhrases：欧盟化学品安全术语。
* RSPhrases：欧盟化学品风险及安全术语。
* GHSPictograms：GHS危险品标识。
* GHSSignalWord：GHS警示词。
* HPhrases：GHS危险术语。
* PPhrases：GHS防范术语。
* MainHazards：主要危害。
* IngestionHazard：摄入危害。
* InhalationHazard：吸入危害。
* EyeHazard：眼部危害。
* SkinHazard：皮肤危害。
* NFPA-H：NFPA704健康危害等级。
* NFPA-F：NFPA704可燃性等级。
* NFPA-R：NFPA704反应活性等级。
* NFPA-O：NFPA704其他标注。
* FlashPt：闪点。
* Autoignition：自燃温度。
* ExploLimits：爆炸极限。
* PEL：OSHA最大允许暴露浓度。
* TLV：美国工作场合化学品最高接触浓度。
* MAK：德国工作场合化学品最高接触浓度。
* MELS：英国工作场合化学品最高接触浓度。
* LD50：半数致死量。
* LC50：半数致死浓度。
* LCt50：半数致死浓度及时间。
Related/-{相關}-/-{相关}-：相关化学物质列表
* OtherAnions：同阳离子不同阴离子物质。
* OtherCations：同阴离子不同阳离子物质。
* OtherFunctn：相似物质（例如具有相同官能团，或同为氧化物，等等）。
* Function：与上一参数结合使用。如：Function = 醇，或 Function = 氯化物。
* OtherCpds：其他相关化学物质，参见某某化学物质。
- 星号(*)后为参数名，等效参数用“/”分隔。冒号后为解释。
</pre>
|}

== 参数说明 ==
此处列出化学信息框主模块参数具体说明，模块小节内参数请参阅相应模块文档，见[[#模块化小节的编排]]。
{| style="border-collapse:collapse; width:100%; border-style:solid; border-width:1px; empty-cells:show;" border="1"
|- style="background-color:#b3b7ff;"
! 参数（等效参数用“/”分隔） || 说明 || 实例
|-
| Reference / -{參考}- / -{参考}- || 相关参考资料 || <nowiki>Reference = <ref name="ref1">某注释</ref></nowiki>
|- style="background-color:#f8eaba;"
| Name / -{名稱}- / -{名称}- || 化学物质名称，必要参数，如没有设定，将会自动使用条目名作为化合物名称 || Name = 氯化钠
|-
| NameEn / 英文名 || 化学物质英文名称|| NameEn = Sodium chloride
|-
| ImageFile / -{圖像檔案}- / -{图像文件}- || 化学物质结构式或相关图像，仅文件名，不需方括号 || ImageFile = Halite(Salt)USGOV.jpg
|-
| ImageSize / -{圖像大小}- / -{图像大小}- || 上述图像文件的宽度，单位为px，默认值200px || ImageSize = 150px
|-
| ImageAlt / -{圖像替換}- / -{图像替换}- || 上述图像文件的替换说明文字，当图片无法显示时的文字信息 || ImageAlt = 无色透明立方晶体
|-
| ImageName / -{圖像名稱}- / -{图像名称}- || 上述图像文件的标题，会以提示文字的形式出现在光标旁 || ImageName = 氯化钠晶体
|- style="background-color:#dafada;"
| colspan="3" align="center" style="border-color:#999;" | ImageFile1参数使用与ImageFile相同，图像会列于ImageFile下方。
|-
| ImageFileL1 / -{圖像檔案左1}- / -{图像文件左1}- || 并列展示的两图像中左侧的图像，会被列于ImageFile/ImageFile1之下空间的左侧 || ImageFile = Ozone-3D-vdW.png
|-
| ImageSizeL1 / -{圖像大小左1}- / -{图像大小左1}- || 上述图像文件的宽度，单位为px，默认值100px || ImageSize = 125px
|-
| ImageAltL1 / -{圖像替換左1}- / -{图像替换左1}- || 上述图像文件的替换说明文字，当图片无法显示时的文字信息 || ImageAlt = 角形相连的三个球体
|-
| ImageNameL1 / -{圖像名稱左1}- / -{图像名称左1}- || 上述图像文件的标题，会以提示文字的形式出现在光标旁 || ImageName = 臭氧的三维模型
|- style="background-color:#dafada;"
| colspan="3" align="center" style="border-color:#999;" | ImageFileR1参数使用与ImageFileL1相同，图像会列于ImageFileL1右方。
|- style="background-color:#dafada;"
| colspan="3" align="center" style="border-color:#999;" | ImageFile2参数使用与ImageFile/ImageFile1相同，图像会列于ImageFile/ImageFile1/ImageFileL1及ImageFileR1的下方。
|- style="background-color:#dafada;"
| colspan="3" align="center" style="border-color:#999;" | ImageFileL2和ImageFileR2参数使用与ImageFileL1和ImageFileR1相同，图像会列于ImageFile/ImageFile1/ImageFileL1/ImageFileR1/ImageFile2的下方。
|- style="background-color:#dafada;"
| colspan="3" align="center" style="border-color:#999;" | ImageFile3参数使用与ImageFile/ImageFile1/ImageFile2相同，图像会列于ImageFile/ImageFile1/ImageFileL1/ImageFileR1/ImageFile2/ImageFileL2/ImageFileR2的下方。
|-
| CustomizedImage / -{定制圖像}- / -{定制图像}- || 可自由组合或定义的化学物质结构式或相关图像，图片需要使用&#91;&#91;File:ImageFileName&#93;&#93;的格式 || <nowiki>CustomizedImage = [[File:Co2+.svg|钴离子]][[File:Sulfat-Ion2.svg|硫酸根离子]]</nowiki>
|- style="background-color:#dafada;"
| colspan="3" align="center" style="border-color:#999;" | 以上图像参数的具体效果参见[[#图像应用]]
|- style="background-color:#f8eaba;"
| IUPACName / IUPAC英 || 化学物质的[[IUPAC命名法]]命名 || IUPACName = Sodium chloride
|-
| IUPACNameZh / IUPAC中 || 化学物质的[[IUPAC命名法]]命名|| IUPACNameZh = 氯化钠
|-
| SystematicName / -{系統名}- / -{系统名}-|| 化学物质的[[IUPAC命名法]]系统命名，不完全等价于IUPAC名，因为IUPAC名包含很多常用名，若是該[[IUPAC命名法]]系统命名包含[[Help:高级字词转换语法#界定符號|<nowiki>-{}-</nowiki>]]時請在該對括號的兩側加入<nowiki><nowiki></nowiki></nowiki> || SystematicName = Sodium chloride
|-
| SystematicNameZh / -{中文系統名}- / -{中文系统名}- || 化学物质的[[IUPAC命名法]]中文系统命名，若是該[[IUPAC命名法]]中文系统命名包含[[Help:高级字词转换语法#界定符號|<nowiki>-{}-</nowiki>]]時請在該對括號的兩側加入<nowiki><nowiki></nowiki></nowiki> || SystematicNameZh = 氯化钠
|-
| OtherNames / -{別名}- / -{别名}- || 化学物质的其他名称，多个名称之间依长短可用逗号或&lt;br /&gt;分隔 || OtherNames = 食盐、石盐、盐、食用盐
|-
| Abbreviations / -{縮寫}- / -{缩写}- || 化学物质的缩写，多个之间依长短可用逗号或&lt;br /&gt;分隔 || Abbreviations = Glu，E
|-
| INN || 药物的[[国际非专利药品名称]] || INN = paracetamol
|- style="background-color:#dafada;"
| colspan="3" align="center" style="border-color:#999;" | rINN和pINN参数使用与INN相同，分别表示推荐名和建议名，INN / rINN / pINN 三者只能选一
|-
| CADN || 药物的[[中国药品通用名称]] || CADN = 对乙酰氨基酚
|-
| USAN || 药物的美国药品通用名称 || USAN = acetaminophen
|-
| BAN || 药物的英国药品通用名称 || BAN = Paracetamol
|-
| Section1 || 小节模块 || Section1 = &#123;&#123;Chembox Identifiers &#124;此处省略小节内参数&#125;&#125;
|- style="background-color:#dafada;"
| colspan="3" align="center" style="border-color:#999;" | Section2参数使用与Section1相同，小节会列于Section1下方。
|- style="background-color:#dafada;"
| colspan="3" align="center" style="border-color:#999;" | Section3参数使用与Section1/Section2相同，小节会列于Section1/Section2下方。
|- style="background-color:#dafada;"
| colspan="3" align="center" style="border-color:#999;" | 以上小节参数共15个，具体设置参见[[#模块化小节的编排]]
|-
| DataSheetEn || 可选参数，英文数据页名称，用于补充中文数据页暂时欠缺的数据，参见[[#数据页]] || DataSheetEn = Pyridine (data page)
|}

模块化小节内参数说明请继续阅读{{tl|Chembox Identifiers}}、{{tl|Chembox Properties}}、{{tl|Chembox Structure}}、{{tl|Chembox Thermochemistry}}、{{tl|Chembox Pharmacology}}、{{tl|Chembox Explosive}}、{{tl|Chembox Hazards}}、{{tl|Chembox Related}}的说明文档。

== 高级应用 ==
=== 模块化小节的编排 ===
化学信息框最多可以有15个小节，当前有8个模块可供选择显示，即：
* 识别{{tl|Chembox Identifiers}}，也可用{{tl|Chembox 識別}}或{{tl|Chembox 识别}}：记录各种识别和索引，如[[CAS号]]。
* 性质{{tl|Chembox Properties}}，也可用{{tl|Chembox 性質}}或{{tl|Chembox 性质}}：记录[[化学式]]、[[摩尔质量]]、以及各种常用物理性质和化学性质数据。
* 结构{{tl|Chembox Structure}}，也可用{{tl|Chembox 結構}}或{{tl|Chembox 结构}}：记录[[分子构型]]和[[晶体结构]]数据。
* 热力学数据{{tl|Chembox Thermochemistry}}，也可用{{tl|Chembox 熱力學}}或{{tl|Chembox 热力学}}：记录热力学数据，焓和熵。
* 药理学数据{{tl|Chembox Pharmacology}}，也可用{{tl|Chembox 藥理}}或{{tl|Chembox 药理}}：记录[[药理学]]、[[药剂学]]相关数据以及药物的法律分类和地位。
* 爆炸性{{tl|Chembox Explosive}}，也可用{{tl|Chembox 爆炸性}}：记录[[炸藥]]的爆炸相关属性。
* 危险性{{tl|Chembox Hazards}}，也可用{{tl|Chembox 危險性}}或{{tl|Chembox 危险性}}：记录化学物质的危险性相关说明、分类、标签。
* 相关化学品{{tl|Chembox Related}}，也可用{{tl|Chembox 相關}}或{{tl|Chembox 相关}}：记录相关化学物质、衍生物、同系物等，如具有同样阳离子的[[氯化钠|NaCl]]和[[溴化钠|NaBr]]。
每个小节的具体参数设置请阅读各个模板的说明文档。

化学信息框中对模块化小节的引用通过以下形式调用：
<pre>
{{Chembox
|
...省略参数
| Section1 = {{Chembox Identifiers
               |
               ...省略参数
             }}
| Section2 = {{Chembox Properties
               |
               ...省略参数
             }}
| Section3 = ...
}}
</pre>
在这里，小节号不可以重复，否则拥有重复的小节号的模块将不会显示。如果想将某模块提前，可以给该小节赋予比较小的Section号码。

=== 图像应用 ===
化学物质的结构式、分子模型、晶体结构以及外观性状图像有助于给读者该化学物质的直观认识，未设定图像的包含化学信息框模板的条目将会被归于维护用分类[[:Category:缺少結構式的化學品條目]]。

化学信息框中一共可以插入8个普通图像：它们分别是ImageFile、ImageFile1、ImageFileL1、ImageFileR1、ImageFile2、ImageFileL2、ImageFileR2、ImageFile3，其中ImageFile、ImageFile1、ImageFile2、ImageFile3默认宽度为200px，两组并排排列的图像的默认宽度为100px。在下面的范例中，这8个图像分别用1-8来标识：
{|
|<pre>
|{{Chembox
| Name = 图像使用演示
| ImageFile = Circle_sign_1.svg
| ImageSize = 100px
| ImageName = Circle_1
| ImageAlt = 1 in a circle
| ImageFile1 = Circle_sign_2.svg
| ImageSize1 = 100px
| ImageName1 = Circle_2
| ImageAlt1 = 2 in a circle
| ImageFileL1 = Circle_sign_3.svg
| ImageSizeL1 = 100px
| ImageNameL1 = Circle_3
| ImageAltL1 = 3 in a circle
| ImageFileR1 = Circle_sign_4.svg
| ImageSizeR1 = 100px
| ImageNameR1 = Circle_4
| ImageAltR1 = 4 in a circle
| ImageFile2 = Circle_sign_5.svg
| ImageSize2 = 100px
| ImageName2 = Circle_5
| ImageAlt2 = 5 in a circle
| ImageFileL2 = Circle_sign_6.svg
| ImageSizeL2 = 100px
| ImageNameL2 = Circle_6
| ImageAltL2 = 6 in a circle
| ImageFileR2 = Circle_sign_7.svg
| ImageSizeR2 = 100px
| ImageNameR2 = Circle_7
| ImageAltR2 = 7 in a circle
| ImageFile3 = Circle_sign_8.svg
| ImageSize3 = 100px
| ImageName3 = Circle_8 }}
| ImageAlt3 = 8 in a circle
...
</pre>
|{{Chembox
| Name = 图像使用演示
| ImageFile = Circle_sign_1.svg
| ImageSize = 100px
| ImageName = Circle_1
| ImageAlt = 1 in a circle
| ImageFile1 = Circle_sign_2.svg
| ImageSize1 = 100px
| ImageName1 = Circle_2
| ImageAlt1 = 2 in a circle
| ImageFileL1 = Circle_sign_3.svg
| ImageSizeL1 = 100px
| ImageNameL1 = Circle_3
| ImageAltL1 = 3 in a circle
| ImageFileR1 = Circle_sign_4.svg
| ImageSizeR1 = 100px
| ImageNameR1 = Circle_4
| ImageAltR1 = 4 in a circle
| ImageFile2 = Circle_sign_5.svg
| ImageSize2 = 100px
| ImageName2 = Circle_5
| ImageAlt2 = 5 in a circle
| ImageFileL2 = Circle_sign_6.svg
| ImageSizeL2 = 100px
| ImageNameL2 = Circle_6
| ImageAltL2 = 6 in a circle
| ImageFileR2 = Circle_sign_7.svg
| ImageSizeR2 = 100px
| ImageNameR2 = Circle_7
| ImageAltR2 = 7 in a circle
| ImageFile3 = Circle_sign_8.svg
| ImageSize3 = 100px
| ImageName3 = Circle_8
| ImageAlt3 = 8 in a circle }}
|}
您可以选用其中的几个组合需要的展示形式。除此之外，CustomizedImage参数提供一个空白容器，可供填入任意内容，如若干图像的组合甚至是数学公式。例如：
<pre>
{{Chembox
| Name = 自定义图像演示
| CustomizedImage = [[File:2.svg|x35px|2 ·]] [[File:K+.svg|x35px|钾离子]] [[File:Ferrate ion.svg|130px|高铁酸根离子]]
<br /><math>\sum_{n=0}^\infty \frac{x^n}{n!}</math>
...
</pre>
{{Chembox
| Name = 自定义图像演示
| CustomizedImage = [[File:2.svg|x35px|2 ·]] [[File:K+.svg|x35px|钾离子]] [[File:Ferrate ion.svg|130px|高铁酸根离子]]<br /><math>\sum_{n=0}^\infty \frac{x^n}{n!}</math>
}}{{-}}<br>

=== 数据页 ===
如果化学信息框表格中的数据过多，可以考虑建立化学物质主条目的附属数据页。形如'''[-{}-[化学物质主条目/数据页]]'''。在新建的空白数据页里，可以应用数据页生成模板{{tl|Chembox subst datasheet}}，使用方法是在编辑窗口加入'''<nowiki>{{subst:Chembox subst datasheet}}</nowiki>'''，保存，即可再次编辑，填充数据。

化学信息框模板检测是否存在'''[-{}-[化学物质主条目/数据页]]'''，如数据页存在，将在化学信息框模板末端添加连往数据页的链接。若设置了DataSheetEn参数，在没有中文数据页的情况下，会添加连往英文维基百科相应数据页的链接。
{|
|
<pre>
{{Chembox
| Name = 英文附加数据页演示
| DataSheetEn = Ethanol (data page)
}}
</pre>
| 
{{Chembox | Name = 英文附加数据页演示 | DataSheetEn = Ethanol (data page)}}
|}

== 故障排除 ==
如果化学信息框显示不正确，请先检查使用的格式：
* 模板参数区分大小写，请确认参数的大小写是否正确。
* 仅常用参数提供中文形式，请参照[[#参数详解]]。
* 参数是否在对应的小节中，不在对应小节中的参数不会被显示出来。
* 小节序号是否有重复，序号重复的整个小节都不会显示。
* 模块小节应在SectionN = <nowiki>{{模块名}}</nowiki>中，请检查是否花括号不匹配。

如果仍然显示错误，请查看其他使用化学信息框模板的条目，如果出现混乱，请到[[维基百科:化学信息框]]讨论。

== 其他信息 ==
如有对参数设置或模块设置方面的建议和意见，请到[[维基百科:化学信息框]]讨论，与维基百科其他用户包括化学兴趣小组成员共同改进本模板。

<includeonly>
<!-- 分类与跨语言链接 Categories and interwikis -->

[[Category:化学信息框模板|*]]
[[Category:使用了分析程序的模板|{{PAGENAME}}]]

[[af:Sjabloon:Chemiekas nuut]]
[[ar:قالب:Chembox]]
[[az:Şablon:Maddə]]
[[bn:টেমপ্লেট:Chembox]]
[[ca:Plantilla:Chembox]]
[[da:Skabelon:Kemiboks ny]]
[[de:Vorlage:Infobox Chemikalie]]
[[el:Πρότυπο:Πληροφορίες χημικής ένωσης]]
[[en:Template:Chembox]]
[[eo:Ŝablono:Informkesto kemia substanco]]
[[es:Plantilla:Ficha de compuesto químico]]
[[fa:الگو:Chembox]]
[[fr:Modèle:Infobox Chimie]]
[[he:תבנית:תרכובת]]
[[hsb:Předłoha:Infokašćik chemikalije]]
[[id:Templat:Chembox]]
[[it:Template:Composto chimico]]
[[ja:Template:Chembox]]
[[ka:თარგი:ინფოდაფა ნივთიერება]]
[[ko:틀:화합물 정보]]
[[krc:Шаблон:Химия вещество]]
[[nds:Vörlaag:Infobox cheemsch Stoff]]
[[nl:Sjabloon:Infobox chemische stof]]
[[pl:Szablon:Związek chemiczny infobox]]
[[pt:Predefinição:Info/Química]]
[[qu:Plantilla:T'inkisqa]]
[[fi:Malline:Yhdiste]]
[[ro:Format:InfoBoxChimie]]
[[ru:Шаблон:Вещество]]
[[simple:Template:Chembox new]]
[[sk:Šablóna:Infobox Chemická zlúčenina]]
[[sv:Mall:Kemibox]]
[[th:แม่แบบ:กล่องข้อมูล สารเคมี]]
[[tr:Şablon:Kimya bilgi kutusu]]
[[ur:سانچہ:معلومات کیمیاء]]
[[vi:Bản mẫu:Chembox new]]
[[zh-yue:Template:Chembox]]
</includeonly>