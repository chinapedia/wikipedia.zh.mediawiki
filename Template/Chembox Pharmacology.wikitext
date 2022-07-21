{{#if:{{{ATCCode|}}}{{{ATCCode_prefix|}}}{{{ATCCode_suffix|}}}{{{ATC_Supplemental|}}}{{{DrugBank|}}}{{{DrugBank1|}}}{{{DrugBank2|}}}{{{DrugBank3|}}}{{{DrugBank4|}}}{{{DrugBank5|}}}{{{DrugBankOther|}}}{{{AdminRoutes|}}}{{{Bioavail|}}}{{{ProteinBound|}}}{{{Metabolism|}}}{{{Metabolites|}}}{{{OnsetOfAction|}}}{{{HalfLife|}}}{{{DurationOfAction|}}}{{{Excretion|}}}{{{Licence_EU|}}}{{{Licence_US|}}}
{{{Legal_status|}}}{{{Legal_AU|}}}{{{Legal_CA|}}}{{{Legal_NZ|}}}{{{Legal_UK|}}}{{{Legal_US|}}}{{{Legal_UN|}}}{{{Legal_EU|}}}
{{{Legal_AU_comment|}}}{{{Legal_CA_comment|}}}{{{Legal_NZ_comment|}}}{{{Legal_UK_comment|}}}{{{Legal_US_comment|}}}{{{Legal_UN_comment|}}}{{{Legal_EU_comment|}}}
{{{Pregnancy_category|}}}{{{Pregnancy_AU|}}}{{{Pregnancy_US|}}}{{{Pregnancy_AU_comment|}}}{{{Pregnancy_US_comment|}}}{{{PLLR|}}}{{{Dependency_liability|}}}{{{Addiction_liability|}}}{{{PregCat|}}}{{{PregCat_AU|}}}{{{PregCat_US|}}}
|{{Chembox headerbar
|header=药理学
|addcats= }}
{{#if:{{{ATCCode|}}}{{{ATCCode_prefix|}}}{{{ATCCode_suffix|}}}{{{ATC_Supplemental|}}} |{{Chembox ATCCode |ATCCode={{{ATCCode|}}} |ATCCode_prefix={{{ATCCode_prefix|}}} |ATCCode_suffix={{{ATCCode_suffix|}}}|ATCCode_Supplemental={{{ATC_Supplemental|}}} |ATCCode_vet={{#switch:{{lc:{{{ATCvet|}}}}}|y|yes|true|1|q|vet=yes||#default=no}} }}}}<!--
 DrugBank Note: DrugBank is also a parameter for Chembox Identifiers -->
{{#if:{{{DrugBank|}}}{{{DrugBank1|}}}{{{DrugBank2|}}}{{{DrugBank3|}}}{{{DrugBank4|}}}{{{DrugBank5|}}}{{{DrugBanks|}}}{{{DrugBankOther|}}}
|{{Chembox DrugBank
|DrugBank={{#if:{{{DrugBank|}}}|{{Chembox DrugBank/format
|DrugBank={{{DrugBank|}}} |DrugBank_comment={{{DrugBank_Comment|}}} |DrugBank_Ref={{{DrugBank_Ref|}}} }}}}
|DrugBank1={{#if:{{{DrugBank1|}}}|{{Chembox DrugBank/format
|DrugBank={{{DrugBank1|}}} |DrugBank_comment={{{DrugBank1_Comment|}}} |DrugBank_Ref={{{DrugBank1_Ref|}}} }}}}
|DrugBank2={{#if:{{{DrugBank2|}}}|{{Chembox DrugBank/format
|DrugBank={{{DrugBank2|}}} |DrugBank_comment={{{DrugBank2_Comment|}}} |DrugBank_Ref={{{DrugBank2_Ref|}}} }}}}
|DrugBank3={{#if:{{{DrugBank3|}}}|{{Chembox DrugBank/format
|DrugBank={{{DrugBank3|}}} |DrugBank_comment={{{DrugBank3_Comment|}}} |DrugBank_Ref={{{DrugBank3_Ref|}}} }}}}
|DrugBank4={{#if:{{{DrugBank4|}}}|{{Chembox DrugBank/format
|DrugBank={{{DrugBank4|}}} |DrugBank_comment={{{DrugBank4_Comment|}}} |DrugBank_Ref={{{DrugBank4_Ref|}}} }}}}
|DrugBank5={{#if:{{{DrugBank5|}}}|{{Chembox DrugBank/format
|DrugBank={{{DrugBank5|}}} |DrugBank_comment={{{DrugBank5_Comment|}}} |DrugBank_Ref={{{DrugBank5_Ref|}}} }}}}
|DrugBankOther={{{DrugBankOther|}}} }}}}
{{#if:{{{legal_status|}}}{{{legal_AU|}}}{{{legal_CA|}}}{{{legal_NZ|}}}{{{legal_UK|}}}{{{legal_US|}}}{{{legal_EU|}}}{{{legal_UN|}}}{{{Legal_status|}}}{{{Legal_AU|}}}{{{Legal_CA|}}}{{{Legal_UK|}}}{{{Legal_US|}}}{{{Legal_EU|}}}{{{Legal_UN|}}}{{{legal_AU_comment|}}}{{{legal_CA_comment|}}}{{{legal_NZ_comment|}}}{{{legal_UK_comment|}}}{{{legal_US_comment|}}}{{{legal_EU_comment|}}}{{{legal_UN_comment|}}}{{{Legal_status|}}}{{{Legal_AU|}}}{{{Legal_CA|}}}{{{Legal_NZ|}}}{{{Legal_UK|}}}{{{Legal_US|}}}{{{Legal_UN|}}}{{{Legal_EU|}}}{{{Legal_AU_comment|}}}{{{Legal_CA_comment|}}}{{{Legal_NZ_comment|}}}{{{Legal_UK_comment|}}}{{{Legal_US_comment|}}}{{{Legal_UN_comment|}}}{{{Legal_EU_comment|}}}
|{{Chembox Legal_status
|legal_status={{{Legal_status|}}}
|legal_AU={{{Legal_AU|}}}
|legal_CA={{{Legal_CA|}}}
|legal_NZ={{{Legal_NZ|}}}
|legal_UK={{{Legal_UK|}}}
|legal_US={{{Legal_US|}}}
|legal_EU={{{Legal_EU|}}}
|legal_UN={{{Legal_UN|}}}
|legal_AU_comment={{{Legal_AU_comment|}}}
|legal_CA_comment={{{Legal_CA_comment|}}}
|legal_NZ_comment={{{Legal_NZ_comment|}}}
|legal_UK_comment={{{Legal_UK_comment|}}}
|legal_US_comment={{{Legal_US_comment|}}}
|legal_EU_comment={{{Legal_EU_comment|}}}
|legal_UN_comment={{{Legal_UN_comment|}}} }}}}
{{#if:{{{Pregnancy_category|}}}{{{Pregnancy_AU|}}}{{{Pregnancy_US|}}}{{{Pregnancy_AU_comment|}}}{{{Pregnancy_US_comment|}}}{{{PLLR|}}}{{{PregCat|}}}{{{PregCat_AU|}}}{{{PregCat_US|}}}
|{{Chembox PregCat
|pregnancy_category={{{PregCat|}}}{{{Pregnancy_category|}}}
|pregnancy_AU={{{PregCat_AU|}}}{{{Pregnancy_AU|}}}
|pregnancy_US={{{PregCat_US|}}}{{{Pregnancy_US|}}}
|pregnancy_AU_comment={{{Pregnancy_AU_comment|}}}
|pregnancy_US_comment={{{Pregnancy_US_comment|}}}
|PLLR={{{PLLR|}}} }}}}
{{#if:{{{Licence_EU|}}}{{{Licence_US|}}}
|{{Chembox Licence
|licenceEU={{{Licence_EU|}}}
|licenceUS={{{Licence_US|}}} }}}}
{{#if:{{{Dependence_liability|}}} |{{Chembox Dependence_liability |value={{{Dependence_liability|}}} }}}}
{{#if:{{{Addiction_liability|}}} |{{Chembox Addiction_liability |value={{{Addiction_liability|}}} }}}}
{{#if:{{{AdminRoutes|}}} |{{Chembox AdminRoutes |value={{{AdminRoutes|}}} }}}}
{{#if:{{{Bioavail|}}}{{{ProteinBound|}}}{{{Metabolism|}}}{{{Metabolites|}}}{{{OnsetOfAction|}}}{{{HalfLife|}}}{{{DurationOfAction|}}}{{{Excretion|}}} |{{Chembox Pharmacokinetics (set)
| bioavailability={{{Bioavail|}}}
| protein-binding = {{{ProteinBound|}}}
| metabolism ={{{Metabolism|}}}
| metabolites = {{{Metabolites|}}}
| onset-of-action={{{OnsetOfAction|}}}
| biochemical-half-life={{{HalfLife|}}}
| duration-of-action={{{DurationOfAction|}}}
| excretion={{{Excretion|}}} }}}}<!--
-->}}<!--

-->{{#invoke:TemplatePar
|check
|template=Template:Chembox Pharmacology
|all= |opt= Addiction_liability= ATCCode= ATCCode_prefix= ATCCode_suffix= ATC_Supplemental= ATCvet= AdminRoutes= Bioavail= ProteinBound= Metabolism= Metabolites= OnsetOfAction= HalfLife= DurationOfAction= Excretion= Licence_EU= Licence_US= 
Legal_status= Legal_AU= Legal_CA= Legal_NZ= Legal_UK= Legal_US= Legal_EU= Legal_UN= 
Legal_AU_comment= Legal_CA_comment= Legal_NZ_comment= Legal_UK_comment= Legal_US_comment= Legal_EU_comment= Legal_UN_comment= 
Pregnancy_category= Pregnancy_AU= Pregnancy_US= Pregnancy_AU_comment= Pregnancy_US_comment= 
PregCat= PregCat_AU= PregCat_US=
PLLR= Dependence_liability= DrugBank= DrugBank_Comment= DrugBank_Ref= DrugBank1= DrugBank1_Comment= DrugBank1_Ref= DrugBank2= DrugBank2_Comment= DrugBank2_Ref= DrugBank3= DrugBank3_Comment= DrugBank3_Ref= DrugBank4= DrugBank4_Comment= DrugBank4_Ref= DrugBank5= DrugBank5_Comment= DrugBank5_Ref= DrugBankOther
|cat=Chemical articles with unknown parameter in Chembox
|format=0|preview=1|errNS=0
}}<noinclude>{{documentation}}</noinclude>