---
title: Tax Invoice Generator
tags : ["Composing"]
---

## Introduction
Tax Invoice Generator is one of the features of this software product. Using this feature we can display invoice generated for the panchayat in every financial year. Users will have access to Tax Invoice Generator if they have permission, Otherwise will not access.

## Business Assumptions
1. What type of users can access Tax Invoice Generator should be planned at design phase.

## Requirements
### Functional Requirements
1. Tax Invoice Generator feature is accessible at panchayat level only.
1. Properties and Tax Rates should be required to generate the Tax Invoice Generator.
1. Only one Tax Invoice Generator should be created for panchayat in one financial year.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access Invoice.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Tax Invoice Generate function is used to generate tax invoice for every financial year at panchayat.

### Design 
1. This feature shows all properties counts and Notification settings (SMS/Email/Whatsapp)
2. We can generate, view and export the Tax Invoice.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|
|HouseTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||
|HouseModuleTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||
|KolagaramTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||	
|TardeTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||	
|AdvertisementTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||
|VacantLandTax Rate|[gs0008-Administration]({{< ref "gs0008-Administration" >}})||	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_invoice_gen_generate|To generate the tax invoice|
|uc_invoice_gen_authorize|To authorize the tax invoice|
|uc_invoice_gen_list|To view all the invoice. This listing page should bind to a permission|
|uc_invoice_gen_view|To view the invoice. This view page should bind to a permission|
|uc_invoice_gen_search|To search the invoice. This search page should bind to a permission|
|uc_invoice_gen_export|To export the invoice rate in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Generate|Authorize|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|----|
|year|YES|NA|NA|@Column(name = "year", length = 16, nullable = false)|year bigint(20) NOT NULL|YES|NO|YES|YES|YES|YES||
|houseCount|YES|0|NA|@Column(name = "house_count", nullable = true)|house_count bigint(20) DEFAULT 0|YES|NO|YES|YES|NO|NO||
|kolagaramCount|NO|0|NA|@Column(name = "kolagaram_count", nullable = true)|kolagaram_count bigint(20) DEFAULT 0|YES|NO|YES|YES|NO|NO||
|auctionCount|NO|0|NA|@Column(name = "auction_count", nullable = true)|auction_count bigint(20) DEFAULT 0|YES|NO|YES|YES|NO|NO||
|advCount|NO|0|NA|@Column(name = "adv_count", nullable = true)|adv_count bigint(20) DEFAULT 0|YES|NO|YES|YES|NO|NO||
|tradeCount|NO|0|NA|@Column(name = "trade_count", nullable = true)|trade_count bigint(20) DEFAULT 0|YES|NO|YES|YES|NO|NO||
|vacantlandCount|NO|0|NA|@Column(name = "vacantland_count", nullable = true)|vacantland_count bigint(20) DEFAULT 0|YES|NO|YES|YES|NO|NO||
|houseAmount|NO|NA|NA|@Column(name = "house_amount", nullable = true)|house_amount float(16,2) DEFAULT NULL|NO|NO|YES|YES|NO|NO||
|kolagaramAmount|NO|NA|NA|@Column(name = "kolagaram_amount", nullable = true)|kolagaram_amount float(16,2) DEFAULT NULL|NO|NO|YES|YES|NO|NO||
|auctionAmount|NO|NA|NA|@Column(name = "auction_amount", nullable = true)|auction_amount float(16,2) DEFAULT NULL|NO|NO|YES|NO|NO|NO||
|advAmount|NO|NA|NA|@Column(name = "adv_amount", nullable = true)|adv_amount float(16,2) DEFAULT NULL|NO|NO|YES|YES|NO|NO||
|tradeAmount|NO|NA|NA|@Column(name = "trade_amount", nullable = true)|trade_amount float(16,2) DEFAULT NULL|NO|NO|YES|YES|NO|NO||
|vacantlandAmount|NO|NA|NA|@Column(name = "vacantland_amount", nullable = true)|vacantland_amount float(16,2) DEFAULT NULL|NO|NO|YES|YES|NO|NO||
|houseArrears|NO|NA|NA|@Column(name = "house_arrears", nullable = true)|house_arrears float(16,2) DEFAULT NULL|NO|NO|YES|NO|NO|NO||
|kolagaramArrears|NO|NA|NA|@Column(name = "kolagaram_arrears", nullable = true)|kolagaram_arrears float(16,2) DEFAULT NULL|NO|NO|YES|NO|NO|NO||
|auctionArrears|NO|NA|NA|@Column(name = "auction_arrears", nullable = true)|auction_arrears float(16,2) DEFAULT NULL|NO|NO|YES|YES|NO|NO||
|advArrears|NO|NA|NA|@Column(name = "adv_arrears", nullable = true)|adv_arrears float(16,2) DEFAULT NULL|NO|NO|YES|YES|NO|NO||
|tradeArrears|NO|NA|NA|@Column(name = "trade_arrears", nullable = true)|trade_arrears float(16,2) DEFAULT NULL|NO|NO|YES|YES|NO|NO||
|vacantlandArrears|NO|NA|NA|@Column(name = "vacantland_arrears", nullable = true)|vacantland_arrears float(16,2) DEFAULT NULL|NO|NO|YES|YES|NO|NO||
|houseTotalAmount|NO|NA|NA|@Column(name = "house_total_amount", nullable = true)|house_total_amount float(16,2) DEFAULT NULL|NO|YES|YES|YES|YES|NO||
|kolagaramTotalAmount|NO|NA|NA|@Column(name = "kolagaram_total_amount", nullable = true)|kolagaram_total_amount float(16,2) DEFAULT NULL|NO|YES|YES|YES|YES|NO||
|auctionTotalAmount|NO|NA|NA|@Column(name = "auction_total_amount", nullable = true)|auction_total_amount float(16,2) DEFAULT NULL|NO|YES|YES|YES|NO|NO||
|advTotalAmount|NO|NA|NA|@Column(name = "adv_total_amount", nullable = true)|adv_total_amount float(16,2) DEFAULT NULL|NO|YES|YES|YES|YES|NO||
|tradeTotalAmount|NO|NA|NA|@Column(name = "trade_total_amount", nullable = true)|trade_total_amount float(16,2) DEFAULT NULL|NO|YES|YES|YES|YES|NO||
|vacantlandTotalAmount|NO|NA|NA|@Column(name = "vacantland_total_amount", nullable = true)|vacantland_total_amount float(16,2) DEFAULT NULL|NO|YES|YES|YES|YES|NO||
|genStatus|YES|NA|NA|@Enumerated(EnumType.STRING)@Column(name = "generation_status", length = 16, nullable = false)|generation_status VARCHAR(16) NOT NULL|NO|NO|YES|YES|YES|NO||
|descr|YES|NA|NA|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) NOT NULL|YES|NO|YES|YES|NO|NO||
|loginPassword|YES|NA|NA|@Column(name = "login_password", length = 128, nullable = false)|login_password varchar(128) NOT NULL|YES|YES|YES|NO|NO|NO||
|notifySms|YES|NA|NA|@Column(name = "sms_notify", nullable = false)|sms_notify boolean DEFAULT false|YES|NO|YES|YES|NO|NO||
|notifyEmail|YES|NA|NA|@Column(name = "email_notify", nullable = false)|email_notify boolean DEFAULT false|YES|NO|YES|YES|NO|NO||
|notifyWhatsapp|YES|NA|NA|@Column(name = "whatsapp_notify", nullable = false)|whatsapp_notify boolean DEFAULT false|YES|NO|YES|YES|NO|NO||
|smsCode|NO|NA|NA|@Column(name = "sms_code", length = 6, nullable = true)|sms_code varchar(6) DEFAULT NULL|YES|NO|YES|YES|NO|NO||
|emailCode|NO|NA|NA|@Column(name = "email_code", length = 6, nullable = true)|email_code varchar(6) DEFAULT NULL|YES|NO|YES|YES|NO|NO||
|otpTime|NO|NA|NA|@DateTimeFormat(pattern = "dd-MM-yyyy")@Enumerated(EnumType.STRING)@Temporal(TemporalType.TIMESTAMP)@Column(name = "otp_time", nullable = true)|otp_time datetime DEFAULT NULL|NO|NO|YES|YES|NO|NO||
|retryCount|NO|NA|NA|@Column(name = "retry_count", length = 1, nullable = true)|retry_count bigint(20) DEFAULT 0|NO|NO|YES|YES|NO|NO||
|actionStatus|YES|NA|NA|@Column(name = "action_status", length = 16, nullable = false)|action_status varchar(16) NOT NULL|NO|NO|YES|YES|YES|NO||
|resendOTP|NO|NA|NA|@Transient|N/A|YES|NO|YES|NO|NO|NO||
|authLoginPassword|NO|NA|NA|@Column(name = "authorize_loginpassword", length = 128, nullable = true)|authorize_loginpassword varchar(128) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|authorizeStatus|NO|NA|NA|@Column(name = "authorize_status", length = 16, nullable = true)|authorize_status varchar(16) DEFAULT NULL|YES|NO|YES|YES|YES|NO||
|errormsg|NO|NA|NA|@Column(name = "error_msg", length = 256, nullable = true)|error_msg VARCHAR(256) default null|NO|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS
##### GenerationStatus

{{<mermaid align="left">}}
classDiagram
    class GenerationStatus{
      NOT_STARTED
      IN_PROGRESS
      COMPLETED
    }
{{< /mermaid >}}

##### AuthorizeStatus

{{<mermaid align="left">}}
classDiagram
    class AuthorizeStatus{
      NOT_AUTHORIZED
      AUTHORIZED
    }
{{< /mermaid >}}

##### ActionStatus

{{<mermaid align="left">}}
classDiagram
    class ActionStatus{
      NOT_STARTED
      IN_PROGRESS
      COMPLETED
      IN_COMPLETED
    }
{{< /mermaid >}}


#### Feature Permission

|Permission code|Action|
|---------------|-------|
|INVOICE_GEN_GENERATE|Generate|
|INVOICE_GEN_AUTHORIZE|Authorize|
|INVOICE_GEN_REMOVE|Remove|
|INVOICE_VIEW|View|
|INVOICE_VIEW|Export|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_INVOICE_GEN_GENERATE|Only user having the user role with this permission should generate the tax invoice|
|AC_ROLE_INVOICE_GEN_AUTHORIZE|Only user having the user role with this permission should authorize the tax invoice|
|AC_ROLE_INVOICE_GEN_REMOVE|Only user having the user role with this permission should remove the tax invoice|
|AC_ROLE_INVOICE_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_INVOICE_VIEW|Only user having the user role with this permission should export the invoice in 2 formats Excel, PDF|

## User Experience
1. Generate page based on the standard UX Listing Template
1. Authorize page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    GenerateBtn[Generate]---AuthorizeBtn[Authorize]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="center">}}
graph TD 
	InvoiceMenu((Tax Invoice Menu))
	ListPage{Tax Invoice List Page}
	ViewPage((ViewPage))
	GeneratePage((Generate Page))
	AuthorizePage((Authorize Page))
    RemovePage((Remove Page))
	DownloadFile>Save File On Disk]
	ErrorPage((ErrorPage))
	Stop((Stop))
	Start((Start))
	Start-->InvoiceMenu
	subgraph Menu
    InvoiceMenu
	end
	subgraph List
	InvoiceMenu-->ListPage
	ListPage--G-A-R-V-E-->ListPage
	end
	subgraph Error
	InvoiceMenu-->ErrorPage
	ErrorPage-->Stop
	end
	subgraph View
	ListPage--V-->ViewPage
	ViewPage--B-->ListPage
	ViewPage--B-->ViewPage
	end
	subgraph Download
    ListPage--E-->DownloadFile
    end
    subgraph Generate
	ListPage--G-->GeneratePage
	GeneratePage--SB-->ListPage
	GeneratePage--SB-->GeneratePage
	end
	subgraph Authorize
	ListPage--G-->AuthorizePage
	AuthorizePage--SB-->ListPage
	AuthorizePage--SB-->AuthorizePage
	end
	subgraph Remove
	ListPage--R-->RemovePage
	RemovePage--SB-->ListPage
	RemovePage--SB-->RemovePage
	end
    %%For success Representation
    linkStyle 1 stroke:green,stroke-width:2px;
    linkStyle 5 stroke:green,stroke-width:2px;
    linkStyle 6 stroke:green,stroke-width:2px;
    linkStyle 8 stroke:green,stroke-width:2px;
    linkStyle 9 stroke:green,stroke-width:2px;
    linkStyle 10 stroke:green,stroke-width:2px;
    linkStyle 12 stroke:green,stroke-width:2px;
    linkStyle 13 stroke:green,stroke-width:2px;
    linkStyle 15 stroke:green,stroke-width:2px;
    linkStyle 16 stroke:green,stroke-width:2px;
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px; 
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 11 stroke:red,stroke-width:2px;
    linkStyle 14 stroke:red,stroke-width:2px;
    linkStyle 17 stroke:red,stroke-width:2px;
{{< /mermaid >}}


|Symbol|Action|
|:-----|:-----|
|G|Generate|
|A|Authorize|
|R|Remove|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|SB|Submit or Back|
|G-A-R-V-E|Generate or Authorize or Remove or View or Export|
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

### Sequence Diagram
1. Only a user with the ROLE_INVOICE_GEN_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant InvoiceGenListPage as Browser
    participant Net as Browser Net Tools
   	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet, GET /app/ctx/InvoiceGen/list ListPage
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: S:  GET /app/ctx/InvoiceGen/list ListPage
        cloud-->>-InvoiceGenListPage: RES:List Page
    end
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet, GET /app/InvoiceGen/generate/form GenerateFormPage
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: S : GET /app/InvoiceGen/generate/form GenerateFormPage
        cloud-->>-InvoiceGenListPage: RES: Generate Form Loaded
    end
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet: POST /app/InvoiceGen/generate Generate
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: S: POST /app/InvoiceGen/generate Generate
        cloud-->>-InvoiceGenListPage: RES: An Invoice Successfully Generated
    end
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet, GET /app/InvoiceGen/authorize/form AuthorizeFormPage
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: S : GET /app/InvoiceGen/authorize/form AuthorizeFormPage
        cloud-->>-InvoiceGenListPage: RES: Authorize Form Loaded
    end
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet: POST /app/InvoiceGen/authorize Authorize
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: S: POST /app/InvoiceGen/authorize Authorize
        cloud-->>-InvoiceGenListPage: RES: An Invoice Successfully Authorized
    end
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet: GET /app/InvoiceGen/remove/form RemoveFormPage
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: S : GET /app/InvoiceGen/remove/form RemoveFormPage
        cloud-->>-InvoiceGenListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet: POST /app/InvoiceGen/remove Remove
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: S : POST /app/InvoiceGen/remove Remove
        cloud-->>-InvoiceGenListPage: RES: An Invoice Successfully Removed
    end
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet: GET /app/InvoiceGen/view ViewPage
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: GET /app/InvoiceGen/view ViewPage
        cloud-->>-InvoiceGenListPage: RES: InvoiceGen View
    end
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet: GET /app/InvoiceGen/exportPdf ExportPdf
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: GET /app/InvoiceGen/exportPdf ExportPdf
        cloud-->>-InvoiceGenListPage: RES: InvoiceGen Pdf
    end
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet: GET /app/InvoiceGen/exportListPdf ExportListPdf
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: S : GET /app/InvoiceGen/exportListPdf ExportListPdf
        cloud-->>-InvoiceGenListPage: RES: InvoiceGen List Pdf
    end
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet: GET /app/InvoiceGen/exportXlx ExportXlx
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: GET /app/InvoiceGen/exportXlx ExportXlx
        cloud-->>-InvoiceGenListPage: RES: InvoiceGen Xlx
    end
    rect rgb(244,244,244)
        InvoiceGenListPage->>+Net: Check Internet: GET /app/InvoiceGen/exportListXlx ExportListXlx
        Net--x-InvoiceGenListPage: F : Connection Error
        InvoiceGenListPage->>+cloud: S : GET /app/InvoiceGen/exportListXlx ExportListXlx
        cloud-->>-InvoiceGenListPage: RES: InvoiceGen List Xlx
    end
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Generate |ut_p_g_GSTS_WEB_INVOICEGEN_206  ut_n_g_GSTS_WEB_INVOICEGEN_203 ut_n_g_GSTS_WEB_INVOICEGEN_204 |**Positive Test Cases:** Generating Tax Invoice with Authorised User **Negative Test Cases:** 1.Generating Tax Invoice with Invaid Inputs 2.Generating Tax Invoice without DB Connection 3.Generating Invoice with Invalid Password| **notifyEmail:**  1.Boolean **notifySms:** 1.Boolean  **notifyWhatsapp:** 1.Boolean **loginPassword:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=6 and length<=256 3.null **descr:** 1.valid characters[a-zA-Z0-9*!@#$%^&+=.] 2. length>=8 and length<=64 3.null|1|2|3|testAuthorisedUserGenerateInvoice, testAuthorisedUserGenerateInvoiceWithInvalidPassword, testAuthorisedUserGenerateInvoiceWithoutDBConnection|
|1.0| Generate Form|ut_p_g_GSTS_WEB_INVOICEGEN_200  ut_n_g_GSTS_WEB_INVOICEGEN_202 |**Positive Test Cases:** Open Tax Invoice Generate Form with Authorised User **Negative Test Cases:** 1.Generating Tax Invoice with Invaid Inputs 2.Generating Tax Invoice without DB Connection|N/A|1|1|2|testAuthorisedUserOpenInvoiceGenGenerateForm, testAuthorisedUserOpenInvoiceGenGenerateFormWithoutDBConnection|
|1.0| Authorize |ut_p_a_GSTS_WEB_INVOICEGEN_307  ut_n_a_GSTS_WEB_INVOICEGEN_300 ut_n_a_GSTS_WEB_INVOICEGEN_301 ut_n_a_GSTS_WEB_INVOICEGEN_302 ut_n_a_GSTS_WEB_INVOICEGEN_308 ut_n_a_GSTS_WEB_INVOICEGEN_309 |**Positive Test Cases:** Generating Tax Invoice with Authorised User **Negative Test Cases:** 1.Authorize Invoice with Invalid Password and Id 2.Authorize Invoice with Invalid Id 3.Authorize Invoice without DB Connection 4.Open InvoiceGen Authorize Form For Already Authorized Invoice| **loginPassword:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=6 and length<=256 3.null|1|5|6|testAuthorisedUserAuthorisedInvoice, testAuthorisedUserAuthorisedInvoiceWithInvalidPasswordAndId, testAuthorisedUserAuthorisedInvoiceWithInvalidId, testAuthorisedUserAuthorisedInvoiceWithoutDBConnection, testAuthorisedUserOpenInvoiceGenAuthorizeFormForAlreadyAuthorizedInvoice, testInvoiceGenAuthorizeNegativeTestCase|
|1.0| Authorize Form|ut_p_a_GSTS_WEB_INVOICEGEN_303  ut_n_a_GSTS_WEB_INVOICEGEN_304 ut_n_a_GSTS_WEB_INVOICEGEN_306 |**Positive Test Cases:** Open InvoiceGen Authorize Form with Authorised User **Negative Test Cases:** 1.Open InvoiceGen Authorize Form with Invalid Id 2.Open InvoiceGen Authorize Form without DB Connection|1.validId|1|3|4|testAuthorisedUserOpenInvoiceGenAuthorizeForm, testAuthorisedUserOpenInvoiceGenAuthorizeFormWithInvalidId, testAuthorisedUserOpenInvoiceGenAuthorizeFormWithoutDBConnection|
|1.0| List|ut_p_l_GSTS_WEB_INVOICEGEN_400  ut_n_l_GSTS_WEB_INVOICEGEN_402 |**Positive Test Cases:** Check the object list with Authorised User **Negative Test Cases:** Check the object list without DB Connection|N/A|1|1|2|testAuthorisedUserListInvoiceGen, testAuthorisedUserListInvoiceGenWithoutDBConnection|
|1.0| Search|ut_p_s_GSTS_WEB_INVOICEGEN_500  ut_n_s_GSTS_WEB_INVOICEGEN_502 ut_n_s_GSTS_WEB_INVOICEGEN_503 |**Positive Test Cases:** Search invoice gen with Authorised User **Negative Test Cases:** 1.Search invoice gen without DB Connection 2.Search Invoice gen with Invalid dates with Authorised User|N/A|1|2|3|testAuthorisedUserSearchInvoiceGen, testAuthorisedUserSearchInvoiceGenWithoutDBConnection, testAuthorisedUserSearchInvoiceGenNegativeCase| 
|1.0| View|ut_p_v_GSTS_WEB_INVOICEGEN_600  ut_n_v_GSTS_WEB_INVOICEGEN_601 ut_n_v_GSTS_WEB_INVOICEGEN_603 |**Positive Test Cases:** View Invoice Gen with valid Id **Negative Test Cases:** 1.View Invoice Gen with Invalid Id 2.View Invoice Gen without DB Connection|N/A|1|2|3|testAuthorisedUserViewInvoiceGen, testAuthorisedUserViewInvoiceGenWithInvalidId, testAuthorisedUserViewInvoiceGenWithoutDBConnection|
1.0| PDF |ut_p_ep_GSTS_WEB_INVOICEGEN_700 ut_n_ep_GSTS_WEB_INVOICEGEN_704 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|1|2|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_INVOICEGEN_701 ut_n_elp_GSTS_WEB_INVOICEGEN_705 ut_n_elp_GSTS_WEB_INVOICEGEN_712 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_INVOICEGEN_702 ut_n_ex_GSTS_WEB_INVOICEGEN_706 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|1|2|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_INVOICEGEN_703 ut_n_elx_GSTS_WEB_INVOICEGEN_707 ut_n_elx_GSTS_WEB_INVOICEGEN_713 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|
|1.0| Remove Form|ut_p_r_GSTS_WEB_INVOICEGEN_1000  ut_n_r_GSTS_WEB_INVOICEGEN_1001 ut_n_r_GSTS_WEB_INVOICEGEN_1003 |**Positive Test Cases:** Open InvoiceGen Remove Form with Valid Id **Negative Test Cases:** 1.Open InvoiceGen Remove Form with Invalid Id 2.Open InvoiceGen Remove Form without DB Connection|N/A|1|2|3|testAuthorisedUserOpenInvoiceGenRemoveFormWithValidId, testAuthorisedUserOpenInvoiceGenRemoveFormWithInvalidId, testAuthorisedUserOpenInvoiceGenRemoveFormWithoutDBConnection|
|1.0| Remove|ut_p_r_GSTS_WEB_INVOICEGEN_1009  ut_n_r_GSTS_WEB_INVOICEGEN_1004 ut_n_r_GSTS_WEB_INVOICEGEN_1005 ut_n_r_GSTS_WEB_INVOICEGEN_1006 ut_n_r_GSTS_WEB_INVOICEGEN_1007 |**Positive Test Cases:** Open InvoiceGen Remove Form with Valid Id **Negative Test Cases:** 1.Removing Invoice with Invalid Comment and Id 2.Removing Invoice with Invalid Id 3.Removing Invoice without DB Connection 4.Removing Invoice with Invalid Comment|N/A|1|4|5|testAuthorisedUserRemoveInvoice, testAuthorisedUserRemoveInvoiceWithInvalidCommentAndId, testAuthorisedUserRemoveInvoiceWithInvalidId, testAuthorisedUserRemoveInvoiceWithoutDBConnection, testAuthorisedUserRemoveInvoiceNegativeTestCase|

#### UnAuthorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Generate |ut_n_g_GSTS_WEB_INVOICEGEN_205 |UnAuthorised User does not have permission to generate| **notifyEmail:**  1.Boolean **notifySms:** 1.Boolean  **notifyWhatsapp:** 1.Boolean **descr:** 1.valid characters[a-zA-Z0-9*!@#$%^&+=.] 2. length>=8 and length<=64 3.null **loginPassword:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=6 and length<=256 3.null|0|1|1|testUnAuthorisedUserGenerateInvoice|
|1.0| Generate Form|ut_n_g_GSTS_WEB_INVOICEGEN_201 |UnAuthorised User does not have permission to Open Generate Form|N/A|0|1|1|testUnAuthorisedUserOpenInvoiceGenGenerateForm|
|1.0| Authorize Form|ut_n_g_GSTS_WEB_INVOICEGEN_305 |UnAuthorised User does not have permission to Open Authorize Form|N/A|0|1|1|testUnAuthorisedUserOpenInvoiceGenAuthorizeForm|
|1.0| Authorize |ut_n_a_GSTS_WEB_INVOICEGEN_310|UnAuthorize User does not have permission to authorize the invoice| **loginPassword:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=6 and length<=256 3.null|0|1|1|testUnAuthorisedUserAuthoriseInvoice|
|1.0| List| ut_n_l_GSTS_WEB_INVOICEGEN_401|Check the object list with UnAuthorised User|N/A|0|1|1|testUnAuthorisedUserListInvoiceGen|
|1.0| Search| ut_n_s_GSTS_WEB_INVOICEGEN_501|Search invoice gen with UnAuthorised User|N/A|0|1|1|testUnAuthorisedUserSearchInvoiceGen|
|1.0| View| ut_n_s_GSTS_WEB_INVOICEGEN_602|View invoice gen with UnAuthorised User|N/A|0|1|1|testUnAuthorisedUserViewInvoiceGen|
|1.0| PDF |ut_n_ep_GSTS_WEB_INVOICEGEN_708 |Export List Pdf with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_INVOICEGEN_709 |Export Pdf with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_INVOICEGEN_710 |Export XLX with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_INVOICEGEN_711 |Export List XLX with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportListXlx|
|1.0| Remove Form|ut_n_r_GSTS_WEB_INVOICEGEN_1002 |Open InvoiceGen Remove Form with UnAuthorised User|N/A|0|1|1| testUnAuthorisedUserOpenInvoiceGenRemoveFormWithValidId|
|1.0| Remove|ut_n_r_GSTS_WEB_INVOICEGEN_1008 |Removing Invoice with UnAuthorised User|N/A|0|1|1| testUnAuthorisedUserRemoveInvoice|


## Security compliance check
1. Only user having the permission **ROLE_INVOICE_GEN_GENERATE** should generate this functionality 
1. Only user having the permission **ROLE_INVOICE_GEN_AUTHORIZE** should authorize this functionality 
1. Only user having the permission **ROLE_INVOICE_GEN_VIEW** should view this functionality 
1. Only user having the permission **ROLE_INVOICE_GEN_REMOVE** should remove this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Invoice in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
