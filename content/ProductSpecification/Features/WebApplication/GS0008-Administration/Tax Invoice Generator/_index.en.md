---
title: Tax Invoice Generator
tags : ["Composing"]
---

## Introduction
Tax Invoice Generator is one of the features of this software product. Using this feature we can compute tax for different properties (House/Kolagaram/Advertisement/Trade/Vacantland) in every financial year. Users will have access to Tax Invoice Generator if they have permission, Otherwise will not access.

## Business Assumptions
What type of users can generate Tax Invoice should be planned at design phase.

## Requirements
### Functional Requirements
1. Users of all levels can view and export the Tax Invoice.  
2. We can generate and view Tax Invoice at panchayat level only.
3. Tax Invoice Generate feature is accessible at panchayat level only.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access Tax Invoice Generation.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Tax Invoice Generate function is used to generate tax invoice for every financial year at panchayat.

### Design 
1. This feature shows all properties counts and Notification settings (SMS/Email/Whatsapp)
2. We can generate, view and export the Tax Invoice.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|HouseTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||
|HouseModuleTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||
|KolagaramTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||	
|TardeTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||	
|AdvertisementTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||
|VacantLandTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||	
	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_tax_invoice_generate_list|To view all the invoice tax. This listing page should bind to a permission|
|uc_tax_invoice_generate|To generate the invoice tax. This generate page should bind to a permission|
|uc_tax_invoice_generate_view|To view the invoice tax. This view page should bind to a permission|
|uc_tax_invoice_generate_search|To search the invoice tax. This search page should bind to a permission|
|uc_tax_invoice_generate_export|To export the invoice tax rate in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|descr|YES|NA|a-zA-Z0-9/:#, _.-@,minlen=6,maxlen=128|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) NOT NULL|YES|NO|NO|NO|NO||
|loginPassword|YES|NA|At least 8 Characters, Alpha-numeric having at least one capital letter, digit and a special symbols(*!@#$%^&+=.)|@Column(name = "login_password", length = 128, nullable = false)|login_password varchar(128) NOT NULL|YES|NO|NO|NO|NO||
|notifySms|NO|False|Boolean|@Column(name = "sms_notify", nullable = false)|sms_notify boolean DEFAULT NULL|YES|NO|NO|NO|NO||
|notifyEmail|NO|False|Boolean|@Column(name = "email_notify", nullable = false)|email_notify boolean DEFAULT NULL|YES|NO|NO|NO|NO||
|notifyWhatsapp|NO|False|Boolean|@Column(name = "whatsapp_notify", nullable = false)|whatsapp_notify boolean DEFAULT NULL|YES|NO|NO|NO|NO||
|smsCode|YES|NA|0-9|@Column(name = "sms_code", length = 6, nullable = true)|sms_code  varchar(6)|YES|NO|NO|NO|NO||
|emailCode|YES|NA|0-9|@Column(name = "email_code", length = 6, nullable = true)|email_code  varchar(6)|YES|NO|NO|NO|NO||

#### ENUM CONSTANTS
No Enum Constants in vacant land tax rate.

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|TAX_INVOICE_GENERATE_VIEW|View|
|TAX_INVOICE_GENERATE_GENERATE|Generate|
|TAX_INVOICE_GENERATE_VIEW|Export|
|TAX_INVOICE_GENERATE_VIEW|List|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_TAX_INVOICE_GENERATE_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_TAX_INVOICE_GENERATE_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_TAX_INVOICE_GENERATE_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

## User Experience
1. Generate page based on the standard UX Listing Template
2. Listing page based on the standard UX Listing Template
3. View page based on the standard UX Listing Template
4. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    GenerateBtn[Generate]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="center">}}
graph TD 
	TaxInvoiceGenerateMenu((Tax Invoice Generate Menu))
	ListPage{Tax Invoice Generate List Page}
	GeneratePage((Generate Page))
	ViewPage((ViewPage))
	DownloadFile>Save File On Disk]
	ErrorPage((ErrorPage))
	Stop((Stop))
	Start((Start))
	Start-->TaxInvoiceGenerateMenu
	subgraph Menu
    TaxInvoiceGenerateMenu
	end
	subgraph List
	TaxInvoiceGenerateMenu-->ListPage
	ListPage--G-V-E-->ListPage
	end
	subgraph Error
	TaxInvoiceGenerateMenu-->ErrorPage
	ErrorPage-->Stop
	end
	subgraph Generate
    ListPage--G-->GeneratePage
    GeneratePage--SB-->ListPage
    GeneratePage--SB-->GeneratePage
    end
	subgraph View
	ListPage--V-->ViewPage
	ViewPage--B-->ListPage
	ViewPage--B-->ViewPage
	end
	subgraph Download
    ListPage--E-->DownloadFile
    end
    %%For success Representation
    linkStyle 1 stroke:green,stroke-width:2px;
    linkStyle 5 stroke:green,stroke-width:2px;
    linkStyle 6 stroke:green,stroke-width:2px;
    linkStyle 8 stroke:green,stroke-width:2px;
    linkStyle 9 stroke:green,stroke-width:2px;
    linkStyle 11 stroke:green,stroke-width:2px; 
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px; 
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;    
{{< /mermaid >}}


|Symbol|Action|
|:-----|:-----|
|G|Generate|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|SB|Submit or Back|
|G-V-E|Generate or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Flowchart
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%
flowchart
    Start((start))
    End((end))
    Administration[Administration Menu]
    ListPage[Tax Invoice Listing Page]
    subgraph List Page
        DBCallLoadAllTaxInvoices[loadAllTaxInvoices From  DB]
        SetTaxInvoiceDatainListPage[Set Tax Invoice Data in List Page]
    end
    subgraph Generate Tax Invoice
        FormPage[Tax Invoice Form Page]
    end 
    subgraph Form Page
        FormPageInitialSetUp[Showing taxable properties count & Notification Settings]
        DataValidationCehck{Data Validation}
        OTPDetailsConfirmationPage[OTP Details Confirmation Page]
        ShowMessageDataValidation>Show Message: Please Enter Valid Data]
    end
    subgraph OTP Details Confirmation Page
        InputOTPData[Input SMS and EMail OTP]
        OTPDataValidationCehck{Data Validation}
        GenerateTaxInvoiceProcess[Generate TaxInvoice Process]
        ShowMessageDataValidation>Show Message: Please Enter Valid Data]
    end  
     subgraph Generate TaxInvoice Process
        AllTaxRatesCheck{TaxRates Check}
        PrepareTaxableInvoiceObject[ TaxInvoice Object Preparation]
        DBCallInsertTaxableInvoiceData[Insert TaxableInvoice Object in  DB]
    end       
    Start-->Administration
    Administration--Click Tax Invoice Generator-->ListPage
    %%List page
    ListPage-->DBCallLoadAllTaxInvoices
    DBCallLoadAllTaxInvoices-->SetTaxInvoiceDatainListPage
    %%Generate Tax Invoice
    ListPage--Generate-->FormPage
    FormPage-->FormPageInitialSetUp
    FormPageInitialSetUp--Input form Data-->DataValidationCehck
    DataValidationCehck--Valid-->OTPDetailsConfirmationPage
    DataValidationCehck--Not Valid-->ShowMessageDataValidation
    %% OTP Details Confirmation Page
    OTPDetailsConfirmationPage-->InputOTPData
    InputOTPData-->OTPDataValidationCehck
    OTPDataValidationCehck--Valid-->GenerateTaxInvoiceProcess
    OTPDataValidationCehck--Not Valid-->ShowMessageDataValidation
    %% Generate TaxInvoice Process
    GenerateTaxInvoiceProcess-->AllTaxRatesCheck
    AllTaxRatesCheck--Not Empty-->PrepareTaxableInvoiceObject
    AllTaxRatesCheck--Empty-->End
    PrepareTaxableInvoiceObject-->DBCallInsertTaxableInvoiceData
    DBCallInsertTaxableInvoiceData-->DBCallLoadAllTaxInvoices
{{< /mermaid >}}

### Tax Invoice Prior Validation - Flowchart
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%
flowchart
    Start((start))
    End((end))
    subgraph PriorValidation for HousePropertyTax Computation
        getDistinctBlocksFromDB[Step1: Get distinct blocks from DataBase]
        DataValidationCheck{Is HouseTax Rate available for all distinct blocks?}
        getDistinctHouseCatTypeRoofTypeAndConstructionTypeFromDB[Step2: Get distinct pair of HouseCatType,RoofType and ConstructionType from DataBase]
        EndProcess>Show Message: Stop Tax Invoice Generation]
        HouseCatRoofTypeAndConstructionTypeDataValidationCheck{Is HouseModuleTax Rate available for all distinct pairs of HouseCat,RoofType and ConstructionType?}
        gotoKolagaramComputation[Go to PriorValidation of KolagaramTax Computation]
        EndProcess>Show Message: Stop Tax Invoice Generation]
    end
    subgraph PriorValidation for KolagaramTax Computation
        getDistinctKolagaramCatTypeFromDB[Step 1: Get distinct KolagaramCat types from DataBase]
        KolagaramDataValidationCheck{Is KolagaramTax Rate available for all distinct KolagaramCat types?}
        gotoAdevertisementComputation[Go to PriorValidation of AdvertisementTax Computation]
        EndProcess>Show Message: Stop Tax Invoice Generation]
    end  
    subgraph PriorValidation for AdvertisementTax Computation
        getDistinctAdvertisementCatTypeAndAssetTypeFromDB[Step 1: Get distinct pairs of AdvertisementCat and Asset types from DataBase]
        AdvertisementDataValidationCheck{Is AdvertisementTax Rate available for all distinct pairs of AdvertisementCat and Asset types?}
        gotoTradeComputation[Go to PriorValidation of TradeTax Computation]
        EndProcess>Show Message: Stop Tax Invoice Generation]
    end  
     subgraph PriorValidation for TradeTax Computation
        getDistinctTradeCatTypeFromDB[Step 1: Get distinct TradeCat types from DataBase]
        TradeDataValidationCheck{Is TradeTax Rate available for all distinct TradeCat types?}
        gotoVacantLandComputation[Go to PriorValidation of VacantLandTax Computation]
        EndProcess>Show Message: Stop Tax Invoice Generation]
    end  
    subgraph PriorValidation for VacantLandTax Computation
        VacantLandDataValidationCheck{Is VacantLandTax Rate available?}
        TaxComputationValidationCompleted[Prior Validations of Tax Computation Completed]
        EndProcess>Show Message: Stop Tax Invoice Generation]
    end  
    Start-->getDistinctBlocksFromDB
    %% PriorValidation for HousePropertyTax Computation
    getDistinctBlocksFromDB--Get data from houseProperty-->DataValidationCheck
    DataValidationCheck--Yes-->getDistinctHouseCatTypeRoofTypeAndConstructionTypeFromDB
    DataValidationCheck--No-->EndProcess
    getDistinctHouseCatTypeRoofTypeAndConstructionTypeFromDB--Get data from houseProperty&houseModule-->HouseCatRoofTypeAndConstructionTypeDataValidationCheck
    HouseCatRoofTypeAndConstructionTypeDataValidationCheck--Yes-->gotoKolagaramComputation
    HouseCatRoofTypeAndConstructionTypeDataValidationCheck--No-->EndProcess
    %% PriorValidation for KolagaramTax Computation
    gotoKolagaramComputation-->getDistinctKolagaramCatTypeFromDB
    getDistinctKolagaramCatTypeFromDB--Get data from KolagaramProperty-->KolagaramDataValidationCheck
    KolagaramDataValidationCheck--Yes-->gotoAdevertisementComputation
    KolagaramDataValidationCheck--No-->EndProcess
    %% PriorValidation for AdvertisementTax Computation
    gotoAdevertisementComputation-->getDistinctAdvertisementCatTypeAndAssetTypeFromDB
    getDistinctAdvertisementCatTypeAndAssetTypeFromDB--Get data from Advertisement-->AdvertisementDataValidationCheck
    AdvertisementDataValidationCheck--Yes-->gotoTradeComputation
    AdvertisementDataValidationCheck--No-->EndProcess
    %% PriorValidation for TradeTax Computation
    gotoTradeComputation-->getDistinctTradeCatTypeFromDB
    getDistinctTradeCatTypeFromDB--Get data from TradeProperty-->TradeDataValidationCheck
    TradeDataValidationCheck--Yes-->gotoVacantLandComputation
    TradeDataValidationCheck--No-->EndProcess
    %% PriorValidation for VacantLandTax Computation
    gotoVacantLandComputation-->VacantLandDataValidationCheck
    VacantLandDataValidationCheck--Yes-->TaxComputationValidationCompleted-->End
    VacantLandDataValidationCheck--No-->EndProcess
{{< /mermaid >}}

### Tax Invoice Computation for HouseProperty - Flowchart
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%
flowchart
    Start((start))
    End((end))
    subgraph HousePropertyTax Computation
        getHousePropertyListFromDB[Get Active houseProperty List from DB]
        DataValidationCheck{Is houseProperty List Empty?}
        gotoKolagaramTaxComputation[Go to KolagaramTax Computation]
        iterateEachHouseProperty[Iterate each HouseProperty & Calculate Tax]
        getHouseTaxRateBasedOnBlock[Get houseTax Rate based on House property Block]
        HouseTaxRateDataValidationCheck{Is houseTax Rate Empty?}
        LandValueCalculation[Step1: Land Value Calculation = SiteArea From HouseProeprty * GovtLand Value from HouseTaxRate]
        EndProcess>Show Message: Stop Tax Invoice Generation]
        getHouseModuleListFromDB[Get Active houseModules List from DB]
        HouseModuleDataValidationCheck{Is houseModules List Empty?}
        iterateEachHouseModule[Iterate each HouseModule & Calculate Tax]
        getHouseModuleTaxRateBasedOnHouseCatRoofTypeAndConstructionType[Get houseModuleTax Rate based on combination of HouseCat,RoofType And ConstructionType]
        HouseModuleTaxRateDataValidationCheck{Is houseModuleTax Rate Empty?}
        HouseModuleConstValue[Step2: Construction Value = PlingthArea from HouseModule * Tax Value from HouseModuleTaxRate]
        CalculateDepreciationpercent[depreciationPrct Value = currentYear - taxStartYear - 10d]
        CalculateDepreciationpercentCheck{Is depreciationPrct > 30?}
        depreciationPrct[Step3: depreciationPrct = 30]
        depreciationPrctZero[Step3: depreciationPrct = BuildingAge in no.of Years - 10]
        CalculatedepreciationValue[Step4:depreciationVal = Step3 * Step2 / 100]
        ConstValueafterdepreciationValremove[Step5: ConstructionValue = Step2 - Step4]
        TotalConstValue[Step6: Total ConstVal = Sum of all HouseModules ConstructionValue]
        PropertyValueWithConstValue[Step7: PropertyValue = Step1 + Step6]
        HouseCatCheckForPropertyTaxVal{HouseCatCheck}
        PropertyTaxValForCommercialHouse[Step8:PropertyTaxVal = Step7 * Commercial Value from HouseTax Rate]
        PropertyTaxValForResidentialHouse[Step8:PropertyTaxVal = Step7 * Residential Value from HouseTax Rate]
        PropertyTaxValForExemptionalHouse[Step8:PropertyTaxVal = 0]
        CalculateLibrarayCess[Step9:LibraryTaxVal = Step7 * LibrarayCess Value from houseTax Rate/100]
        CalculatedrainageCess[Step10:DrainageTaxVal = Step7 * DrainageCess Value from houseTax Rate/100]
        CalculatewaterCess[Step11:WaterTaxVal = Step7 * WaterCess Value from houseTax Rate/100]
        CalculatelightServiceCess[Step12:LightServiceTaxVal = Step7 * LightService Value from houseTax Rate/100]
        CalculateHouseTaxValue[Step13: HouseTax Value = Step8+Step9+Step10+Step11+Step12]
        CalculateTotalHouseTaxValue[Step14: Sum of all HouseProperties HouseTax Value]
        PrepareHouseTaxInvoiceObject[Prepare House Tax Invoice Object and add to DBInsertion List]
    end
    Start-->getHousePropertyListFromDB
    %% PriorValidation for HousePropertyTax Computation
    getHousePropertyListFromDB-->DataValidationCheck
    DataValidationCheck--Yes-->gotoKolagaramTaxComputation
    DataValidationCheck--No-->iterateEachHouseProperty
    iterateEachHouseProperty-->getHouseTaxRateBasedOnBlock
    getHouseTaxRateBasedOnBlock-->HouseTaxRateDataValidationCheck
    HouseTaxRateDataValidationCheck--Yes-->EndProcess
    HouseTaxRateDataValidationCheck--No-->LandValueCalculation
    LandValueCalculation-->getHouseModuleListFromDB
    getHouseModuleListFromDB-->HouseModuleDataValidationCheck
    HouseModuleDataValidationCheck--Yes-->EndProcess
    HouseModuleDataValidationCheck--No-->iterateEachHouseModule
    iterateEachHouseModule-->getHouseModuleTaxRateBasedOnHouseCatRoofTypeAndConstructionType
    getHouseModuleTaxRateBasedOnHouseCatRoofTypeAndConstructionType-->HouseModuleTaxRateDataValidationCheck
    HouseModuleTaxRateDataValidationCheck--Yes-->EndProcess
    HouseModuleTaxRateDataValidationCheck--No-->HouseModuleConstValue
    HouseModuleConstValue-->CalculateDepreciationpercent
    CalculateDepreciationpercent-->CalculateDepreciationpercentCheck
    CalculateDepreciationpercentCheck--Yes-->depreciationPrct
    CalculateDepreciationpercentCheck--No-->depreciationPrctZero
    HouseModuleConstValue-->CalculatedepreciationValue
    CalculatedepreciationValue-->ConstValueafterdepreciationValremove
    ConstValueafterdepreciationValremove--Go to Next HouseModule-->getHouseModuleTaxRateBasedOnHouseCatRoofTypeAndConstructionType
    ConstValueafterdepreciationValremove-->TotalConstValue
    TotalConstValue-->PropertyValueWithConstValue
    PropertyValueWithConstValue-->HouseCatCheckForPropertyTaxVal
    HouseCatCheckForPropertyTaxVal--Commercial-->PropertyTaxValForCommercialHouse
    HouseCatCheckForPropertyTaxVal--Residential-->PropertyTaxValForResidentialHouse
    HouseCatCheckForPropertyTaxVal--Exemptional-->PropertyTaxValForExemptionalHouse
    PropertyTaxValForCommercialHouse-->CalculateLibrarayCess
    PropertyTaxValForResidentialHouse-->CalculateLibrarayCess
    CalculateLibrarayCess-->CalculatedrainageCess
    CalculatedrainageCess-->CalculatewaterCess
    CalculatewaterCess-->CalculatelightServiceCess
    CalculatelightServiceCess-->CalculateHouseTaxValue
    CalculateHouseTaxValue--Go to next houseProperty-->getHouseTaxRateBasedOnBlock
    CalculateHouseTaxValue-->CalculateTotalHouseTaxValue
    CalculateTotalHouseTaxValue-->PrepareHouseTaxInvoiceObject
    PrepareHouseTaxInvoiceObject-->gotoKolagaramTaxComputation
    gotoKolagaramTaxComputation-->End
{{< /mermaid >}}


## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|
|1.0| Generate |**Positive Test Case:** ut_p_g_GSTS_WEB_INVOICEGEN_1 **Negative Test Cases:** ut_n_g_GSTS_WEB_HOUSEPROPERTYINVOICE_2 ut_n_g_GSTS_WEB_KOLAGARAMPROPERTYINVOICE_2 ut_n_g_GSTS_WEB_ADVPROPERTYINVOICE_2 ut_n_g_GSTS_WEB_TRADEPROPERTYINVOICE_2 ut_n_g_GSTS_WEB_VACANTLANDPROPERTYINVOICE_2|**Positive Test Cases:** Generating Invoice with Authorised User **Negative Test Cases:** Generating Invoice with Authorised User|**loginPassword:**1.Valid Password 2.Invalid Password **Descr** **wizardStep** **year**|1|5|6|
|1.0| Authorize |**Positive Test Case:** ut_p_a_GSTS_WEB_INVOICEGEN_3 **Negative Test Cases:** ut_n_a_GSTS_WEB_INVOICEGEN_4 |**Positive Test Cases:** Authorize Invoice with Authorised User **Negative Test Cases:** Authorize Invoice with Authorised User|**loginPassword:**1.Valid Password 2.Invalid Password|1|1|2|
|1.0| Remove |ut_p_r_GSTS_WEB_INVOICEGEN_6  ut_n_r_GSTS_WEB_INVOICEGEN_8 |**Positive Test Cases:** Removing Invoice with Authorised User **Negative Test Cases:** Removing Invoice with Authorised User| **removeComment:** 1.valid characters 2.length>=6 and length<=256 3.null |1|1|2|

#### UnAuthorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|
|1.0| Generate |ut_p_g_GSTS_WEB_HOUSEPROPERTYINVOICE_2|UnAuthorised User does not have permission to Generate the invoice|**loginPassword:**1.Valid Password **Descr** **wizardStep** **year**|1|N/A|1|
|1.0| Authorize |ut_p_a_GSTS_WEB_INVOICEGEN_5 |UnAuthorised User does not have permission to Authorise the invoice|**loginPassword:**1.Valid Password 2.Invalid Password|1|N/A|1|
|1.0| Remove |ut_p_r_GSTS_WEB_INVOICEGEN_7 |UnAuthorised User does not have permission to remove the invoice| **removeComment:** 1.valid characters 2.length>=6 and length<=256 3.null |1|N/A|1|

## Security compliance check
1. Only user having the permission **ROLE_VACANT_LAND_TAX_RATE_VIEW** should view this functionality 
1. Only user having the permission **ROLE_VACANT_LAND_TAX_RATE_CREATE** should create this functionality 
1. Only user having the permission **ROLE_VACANT_LAND_TAX_RATE_REMOVE** should remove this functionality 
1. Only user having the permission **ROLE_VACANT_LAND_TAX_RATE_VIEW** should export this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Vacant Land Tax Rate in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0002|[GS-0002](https://shadkona.atlassian.net/browse/GS-0002)|Closed|


## References
1. [Spring Security](https://spring.io/projects/spring-security)
1. [Intro to Spring Security Expressions](https://www.baeldung.com/spring-security-expressions)
1. [Spring Security Role Based Access Authorization Example](https://www.journaldev.com/8748/spring-security-role-based-access-authorization-example)

## Development Estimations
|Release Tag|Feature/Defect ID|Scrum Deatils|Start date|End date|
|-----------|-----------------|-------------|----------|--------|
|2020OCT|GS-0002|Scrum 2020OCTs2|14 OCT 2020|28 OCT 2020|

## Feature Doneness Criteria
Check list for the Doneness criteria

|Metric|Unit Measure|Expected Result|Actual Result|Accepted?|Remarks|Approver|
|------|------------|---------------|-------------|---------|-------|----------|
|Acceptance Criteria Defined?|YES or NO|YES|YES|Accepted|All test cases passed|PM|
|Architecture Approved?|YES or NO|YES|YES|Accepted|Design is accepted|Architect|
|Coding Completed?|YES or NO|YES|YES|Completed|Completed|EM|
|Product Defects|Number|0|0|Accepted||EM|
|Unit Test Case Count?|Number|>5|8|Accepted|Tested|EM|
|Integration Test Cases Count|Number|>5|9|Accepted|Tested|EM|
|Sonar Vulnerabilities Count|Number|0|0|Accepted|validated|EM|
|Code Coverage|Number|>98%|99%|Accepted|Validated|EM|
|User Manual Verified?|YES or NO|YES|YES|Accepted|Validated|DocM|
|PenTest Defect Count?|Number|<2|0|Accepted|Validated|EM|
|PM Accepted?|YES or NO|YES|YES|Accepted|Good to go|PM|
|OM Accepted?|YES or NO|YES|YES|Accepted|Good to go|OM|
|Deployed to Staging?|YES or NO|YES|YES|Accepted|Good to go|EM|
|Deployed to Production?|YES or NO|YES|YES|Accepted|Good to go|OM|




 
