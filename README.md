# Contributions-of-modifiable-risk-factors-to-increased-dementia-risk-in-depression

Code by Anouk Geraets, Kay Deckers and Sebastian Köhler for doi: https://doi.org/10.1017/S0033291722003968 

Please cite this paper when using the code: Geraets AFJ, Leist AK, Deckers K, Verhey FRJ, Schram MT, Köhler S (2023). Contributions of modifiable risk factors to increased dementia risk in depression. Psychological Medicine 1–9. https://doi.org/10.1017/S0033291722003968 

## Data availability

Data are from the English Longitudinal Study of Ageing (ELSA) and are available from the UK Data Service for researchers who meet the criteria for access to confidential data, under conditions of the End User License http://ukdataservice.ac.uk/media/455131/cd137-enduserlicence.pdf. The data can be accessed from: http://discover.ukdataservice.ac.uk/series/?sn=200011.  Contact with the UK data service regarding access to the English Longitudinal Study of Ageing can be made through the website http://ukdataservice.ac.uk/help/get-in-touch.aspx , by phone +44 (0)1206 872143 or by email at ku.ca.ecivresatadku@pleh. 

## Funding

The English Longitudinal Study of Ageing is administered by a team of researchers based at the University College London, NatCen Social Research, the Institute for Fiscal Studies and the University of Manchester. Funding is provided by National Institute on Aging (R01AG017644; principal investigator: Dr Steptoe) and by a consortium of UK government departments coordinated by the National Institute for Health Research. 

This work has received funding from the European Research Council (ERC) under the European Union’s Horizon 2020 research and innovation programme (grant agreement No. 803239 to AKL), the Cardiovascular Research Institute Maastricht (CARIM; HS-BAFTA ‘Talented Ph.D. candidates’ to AFJG) and Alzheimer Nederland (to AFJG).

## Main Code Details

We used data from Wave 1 (2002/2003) till Wave 9 (2018/2019). Since Wave 4 (2008/2009; n=9,886) includes a large number of modifiable risk factors for dementia, it was considered the baseline for this study. In case of missing information on depression, modifiable risk factors for dementia or potential confounders, non-missing data from adjacent waves (in most cases Wave 3 (2006/2007) or Wave 5 (2010/2011) was used. The most recent data files available on August 25th, 2021, were downloaded that day. Information about the operationalization of the variables can be find in the Supplemental Material: https://doi.org/10.1017/S0033291722003968 

## Main analyses

keep if `finstat4` =="C1CM" | `finstat4` =="C3CM" | `finstat` =="C4CM" 

replace `w4xwgt` = 0.00000001 if `w4xwgt`==0

stset `end_dem_int` [pweight = `w4xwgt`] if `LIBRA_amount`==11 & !missing(`SEB_dem_prev_w9`) , id(`idauniq`) failure(`SEB_dem_prev_w9`==1) enter(`time date_ii4`) origin(`time birthdate`) scale(365.25)

keep if `survivaltime`>.14 & !missing(`survivaltime`) & `indager`<70

stcox i.`depression` i.`indsex` i.`education_a` i.`education_0` i.`wealth_wave4_tertiles` `LIBRA_nodepr`, vce(cluster `idahhw4`)

## Mediation by LIBRA

Variable:

Names are

`idauniq` `idahhw4` `indsex` `indager` `w4xwgt` `diabetes` `heartdisease` `physactivity` `smoking` `hypertension` `cholesterol` `alcohol` `cognactivity` `obesity` `diet` `LIBRA_nodepr` `depression` `SEB_dem_prev_w9` `wealth_2` `wealth_3` `education_0` `education_a` `t` `survivaltime`;

Missing are all (-9999) ;

Survival = `survivaltime` (ALL) ;

Timecensored = `SEB_dem_prev_w9` (1=”NOT” 0=”RIGHT”) ;

Usevariables are `survivaltime` `SEB_dem_prev_w9` `depression` `LIBRA_nodepr` `indsex` `indager` `education_0` `education_a` `wealth_2` `wealth_3`;

Idvariable is `idauniq` ;

Useobservations are  `indager` < 70 ;

Weight is `w4xwgt` ;

Cluster is `idahhw4` ;

Analysis:

Basehazard=OFF ;

Type=complex ;

Model:

`survivaltime`  ON `depression` `LIBRA_nodepr` `indsex` `education_0` `education_a` `wealth_2` `wealth_3` `indager` ;

`LIBRA_nodepr` ON `depression` `indsex` `education_0` `education_a` `wealth_2` `wealth_3` `indager` ;

Model indirect:
     
`survivaltime`  IND `depression` ;

## Mediation by cognitive and social activity

Variable:

Names are
 
`idauniq` `idahhw4` `indsex` `indager` `w4xwgt` `diabetes` `heartdisease` `physactivity` `smoking` `hypertension` `cholesterol` `alcohol` `cognactivity` `obesity` `diet` `LIBRA_nodepr` `depression` `SEB_dem_prev_w9` `wealth_2` `wealth_3` `education_0` `education_a` `t` `survivaltime`;
 
 Missing are all (-9999) ;
 
 Survival = survivaltime (ALL) ;
 
 Timecensored = `SEB_dem_prev_w9` (1=”NOT” 0=”RIGHT”) ;
 
 Usevariables are `survivaltime` `SEB_dem_prev_w9` `depression` ` cognactivity` `indsex` `indager` `education_0` `education_a` `wealth_2` `wealth_3`;
 
 Categorical are `cognactivity`;
 
 Idvariable is `idauniq` ;
 
 Useobservations are  `indager` < 70 ;
 
 Weight is `w4xwgt` ;
 
 Cluster is `idahhw4` ;
 
 Analysis:
 
 Basehazard=OFF ;
 
 Type=complex ;
 
 Model:
 
 `survivaltime`  ON `depression` ` cognactivity` `indsex` `education_0` `education_a` `wealth_2` `wealth_3` `indager` ;
 
 `cognactivity` ON `depression` `indsex` `education_0` `education_a` `wealth_2` `wealth_3` `indager` ;
 
 Model indirect:
 
 `survivaltime`  IND `depression` ;
