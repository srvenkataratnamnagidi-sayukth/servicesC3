---
title: Advertisement Tax Rate
tags : ["Composing"]
---

## Introduction
Advertisement Tax Rate is one of the features of this software product. Advertisement tax rate is a tax rate defined for advertisement properties. It depends upon panchayat resolution. Advertisement tax rate may be different for advertisement properties based on advertisement asset and advertisement category. It may vary from one panchayat to other panchayat. Users will have access to advertisement tax rates if they have permission, Otherwise will not access.

## Business Assumptions
What type of users can create advertisement tax rate should be planned at design phase.

## Requirements
### Functional Requirements
1. Users of all levels can create, remove, view and export the advertisement tax rate.  
1. We can create and remove advertisement tax rate at panchayat level only.
1. Advertisement Tax Rate feature is accessible at panchayat level only.
1. Panchayat Resolution is required to create an advertisement tax rate.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access advertisement tax rates.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Advertisement tax rate feature contains information about different advertisement tax rates of panchayat.

### Design 
1. Each advertisement tax rate has Panchayat Resolution, Advertisement Category, Advertisement Asset, and Tax Value(RS).
1. Each advertisement tax rate in same panchayat has unique panchayat resolution or unique advertisement asset or unique advertisement category.
1. We can create, remove, view and export the advertisement tax rate.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_advertisement_tax_rate_list|To view all the advertisement tax rates. This listing page should bind to a permission|
|uc_advertisement_tax_rate_create|To create the advertisement tax rate. This create page should bind to a permission|
|uc_advertisement_tax_rate_remove|To remove the advertisement tax rate. This remove page should bind to a permission|
|uc_advertisement_tax_rate_view|To view the advertisement tax rate. This view page should bind to a permission|
|uc_advertisement_tax_rate_search|To search the advertisement tax rate. This search page should bind to a permission|
|uc_advertisement_tax_rate_export|To export the advertisement tax rate in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|panchayatResolution|YES|NA|Dropdown values|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "pr_id", nullable = false)|pr_id varchar(32) NOT NULL|YES|YES|YES|YES|NO||
|advCategory|YES|NA|Dropdown values|@Enumerated(EnumType.STRING) @Column(name = "adv_category", length = 16, nullable = false)|adv_category varchar(16) NOT NULL|YES|YES|YES|YES|YES||
|advAsset|YES|NA|Dropdown values|@Enumerated(EnumType.STRING) @Column(name = "adv_asset", length = 16, nullable = false)|adv_asset varchar(16) NOT NULL|YES|YES|YES|YES|YES||
|taxVal|YES|NA|0-9 and ., maxlen=8|@Column(name = "tax_val", nullable = false)|tax_val float(9,2) NOT NULL|YES|YES|YES|YES|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Advertisement Category

{{<mermaid align="left">}}
classDiagram
    class  AdvCatType{
      GROUND_BASED
	  MOVING
	  LIGHTING
	  NONE
    }
{{< /mermaid >}}

##### Advertisement Asset

{{<mermaid align="left">}}
classDiagram
    class AdvAssetType{
      PUBLIC
	  PRIVATE
	  NONE
    }
{{< /mermaid >}}


#### Feature Permission

|Permission code|Action|
|---------------|-------|
|ADVERTISEMENT_TAX_RATE_VIEW|View|
|ADVERTISEMENT_TAX_RATE_CREATE|Create|
|ADVERTISEMENT_TAX_RATE_REMOVE|Remove|
|ADVERTISEMENT_TAX_RATE_VIEW|Export|
|ADVERTISEMENT_TAX_RATE_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_adv_tax_rate__prid__pid__advcat__adv_asset (pr_id, org_panchayat_id, adv_category, adv_asset)|
|Foreign Key|fk__gs_adv_tax_rate__pr_id (pr_id) REFERENCES gs_pr (id)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_ADVERTISEMENT_TAX_RATE_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_ADVERTISEMENT_TAX_RATE_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_ADVERTISEMENT_TAX_RATE_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_ADVERTISEMENT_TAX_RATE_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

## User Experience
1. Create page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreateBtn[Create]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="left">}}
flowchart TD
	AdvertisementTaxRateMenu((Advertisement Tax Rate Menu))
	ListPage{Advertisement Tax Rate List Page}
	CreatePage((Create Page))
	RemovePage((Remove Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->AdvertisementTaxRateMenu
    subgraph Menu
    AdvertisementTaxRateMenu
    end
    subgraph   
    AdvertisementTaxRateMenu-->ListPage
    ListPage--C-R-V-E-->ListPage
    end
    subgraph  
    AdvertisementTaxRateMenu--F-->ErrorPage
    ErrorPage-->Stop   
    end
    subgraph Create
    ListPage--C-->CreatePage
    CreatePage--SB-->ListPage
    CreatePage--SB-->CreatePage
    end
    subgraph View
    ListPage--V-->ViewPage
    ViewPage--B-->ListPage
    ViewPage--B-->ViewPage
    end
    subgraph Remove
    ListPage--R-->RemovePage
    RemovePage--SB-->ListPage
    RemovePage--SB-->RemovePage
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
    linkStyle 12 stroke:green,stroke-width:2px;
    linkStyle 14 stroke:green,stroke-width:2px;
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;
    linkStyle 13 stroke:red,stroke-width:2px;

        
{{< /mermaid >}}


|Symbol|Action|
|:-----|:-----|
|C|Create|
|R|Remove|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|SB|Submit or Back|
|C-R-V-E|Create or Remove or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Sequence Diagram
1. Only a user with the ADVERTISEMENT_TAX_RATE_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant AdvertisementTaxRateListpage as Browser
    participant Net as Browser Net Tools
    participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        AdvertisementTaxRateListpage->>+Net: Check Internet, GET /app/ctx/AdvTaxRate/list ListPage
        Net--x-AdvertisementTaxRateListpage: F : Connection Error
        AdvertisementTaxRateListpage->>+cloud: S:  GET /app/ctx/AdvTaxRate/list ListPage
        cloud-->>-AdvertisementTaxRateListpage: RES:List Page
    end
    rect rgb(244,244,244)
        AdvertisementTaxRateListpage->>+Net: Check Internet, GET /app/AdvTaxRate/create/form CreateFormPage
        Net--x-AdvertisementTaxRateListpage: F : Connection Error
        AdvertisementTaxRateListpage->>+cloud: S : GET /app/AdvTaxRate/create/form CreateFormPage
        cloud-->>-AdvertisementTaxRateListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        AdvertisementTaxRateListpage->>+Net: Check Internet: POST /app/AdvTaxRate/create Create
        Net--x-AdvertisementTaxRateListpage: F : Connection Error
        AdvertisementTaxRateListpage->>+cloud: S : POST /app/AdvTaxRate/create Create
        cloud-->>-AdvertisementTaxRateListpage: RES: An Advertisement TaxRate Successfully Created
    end
    rect rgb(244,244,244)
        AdvertisementTaxRateListpage->>+Net: Check Internet: GET /app/AdvTaxRate/remove/form RemoveFormPage
        Net--x-AdvertisementTaxRateListpage: F : Connection Error
        AdvertisementTaxRateListpage->>+cloud: S : GET /app/AdvTaxRate/remove/form RemoveFormPage
        cloud-->>-AdvertisementTaxRateListpage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        AdvertisementTaxRateListpage->>+Net: Check Internet: POST /app/AdvTaxRate/remove Remove
        Net--x-AdvertisementTaxRateListpage: F : Connection Error
        AdvertisementTaxRateListpage->>+cloud: S : POST /app/AdvTaxRate/remove Remove
        cloud-->>-AdvertisementTaxRateListpage: RES: An Advertisement TaxRate Successfully Removed
    end
    rect rgb(244,244,244)
        AdvertisementTaxRateListpage->>+Net: Check Internet: GET /app/AdvTaxRate/view ViewPage
        Net--x-AdvertisementTaxRateListpage: F : Connection Error
        alt
		note right of Net:  Advertisement Tax Rate Cache Object Found
        AdvertisementTaxRateListpage->>+Cache: S : GET /app/AdvTaxRate/view ViewPage
        Cache-->>-AdvertisementTaxRateListpage: RES: Advertisement TaxRate View
        else
		note right of Net:  Advertisement Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/AdvTaxRate/view ViewPage
        cloud-->>-AdvertisementTaxRateListpage: RES: Advertisement TaxRate View
        end
    end
    rect rgb(244,244,244)
        AdvertisementTaxRateListpage->>+Net: Check Internet: GET /app/AdvTaxRate/exportPdf ExportPdf
        Net--x-AdvertisementTaxRateListpage: F : Connection Error 
        alt
		note right of Net:  Advertisement Tax Rate Cache Object Found
        AdvertisementTaxRateListpage->>+Cache: S : GET /app/AdvTaxRate/exportPdf ExportPdf
        Cache-->>-AdvertisementTaxRateListpage: RES: Advertisement TaxRate Pdf
        else
		note right of Net:  Advertisement Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/AdvTaxRate/exportPdf ExportPdf
        cloud-->>-AdvertisementTaxRateListpage: RES: Advertisement TaxRate Pdf
        end
    end
    rect rgb(244,244,244)
        AdvertisementTaxRateListpage->>+Net: Check Internet: GET /app/AdvTaxRate/exportListPdf ExportListPdf
        Net--x-AdvertisementTaxRateListpage: F : Connection Error
        AdvertisementTaxRateListpage->>+cloud: S : GET /app/AdvTaxRate/exportListPdf ExportListPdf
        cloud-->>-AdvertisementTaxRateListpage: RES: Advertisement TaxRate List Pdf
    end
    rect rgb(244,244,244)
        AdvertisementTaxRateListpage->>+Net: Check Internet: GET /app/AdvTaxRate/exportXlx ExportXlx
        Net--x-AdvertisementTaxRateListpage: F : Connection Error
        alt
		note right of Net:  Advertisement Tax Rate Cache Object Found
        AdvertisementTaxRateListpage->>+Cache: S : GET /app/AdvTaxRate/exportXlx ExportXlx
        Cache-->>-AdvertisementTaxRateListpage: RES: Advertisement TaxRate Xlx
        else
		note right of Net:  Advertisement Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/AdvTaxRate/exportXlx ExportXlx
        cloud-->>-AdvertisementTaxRateListpage: RES: Advertisement TaxRate Xlx
        end
    end
    rect rgb(244,244,244)
        AdvertisementTaxRateListpage->>+Net: Check Internet: GET /app/AdvTaxRate/exportListXlx ExportListXlx
        Net--x-AdvertisementTaxRateListpage: F : Connection Error
        AdvertisementTaxRateListpage->>+cloud: S : GET /app/AdvTaxRate/exportListXlx ExportListXlx
        cloud-->>-AdvertisementTaxRateListpage: RES: Advertisement TaxRate List Xlx
    end

          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------------|-----|
|1.0| Create Form |ut_p_c_GSTS_WEB_ADVTAXRATE_120 ut_n_c_GSTS_WEB_ADVTAXRATE_115 ut_n_c_GSTS_WEB_ADVTAXRATE_130 |**Positive Test Cases:** 1.Open Advertisement TaxRate Create Form At panchayat level  **Negative Test Cases:** 1. Open Advertisement TaxRate Create Form with no panchayat resolution exists 2. Open Advertisement TaxRate Create Form Without Db connection |-|1|2|3|testPosOpenAdvertisementTaxRateCreateFormWithAuthorisedUser,  testNegOpenAdvertisementTaxRateCreateFormWithNoPanchayatResolutionExists,  testPosOpenAdvertisementTaxRateCreateFormWithoutDBConnection|
|1.0| Create |ut_p_c_GSTS_WEB_ADVTAXRATE_150  ut_n_c_GSTS_WEB_ADVTAXRATE_160 ut_n_c_GSTS_WEB_ADVTAXRATE_140 ut_n_c_GSTS_WEB_ADVTAXRATE_270 ut_n_c_GSTS_WEB_ADVTAXRATE_280 |**Positive Test Cases:** Create Advertisement TaxRate with valid inputs with Panchayat Level Authorised User **Negative Test Cases:** 1.Create Advertisement TaxRate with Invalid inputs 2.Create Advertisement TaxRate without db connection 3.Create Advertisement TaxRate with Removed Panchayat Resolution Id  4.Create Advertisement TaxRate with Invalid Panchayat Resolution Id|**panchayatResolutionId:** drop down list **advCategory:** enums **advAsset:** enums  **taxVal:** 1.null 2. >=1 and <=100000|12|13|25|testPosAuthorisedPanchayatLevelUserCreateAdvertisementTaxRateWithValidInputs,  testNegAuthorisedPanchayatLevelUserCreateAdvertisementTaxRateWithInValidInputs,  testNegCreateAdvertisementTaxRateWithoutDBconnection,  testNegCreateAdvertisementTaxRateWithRemovedPanchayatResolutionId,  testNegCreateAdvertisementTaxRateWithInvalidPanchayatResolutionId|
|1.0| Remove Form |ut_p_r_GSTS_WEB_ADVTAXRATE_330   ut_n_r_GSTS_WEB_ADVTAXRATE_340   ut_n_r_GSTS_WEB_ADVTAXRATE_350  ut_n_r_GSTS_WEB_ADVTAXRATE_410|**Positive Test Cases:** Open Advertisement TaxRate remove form with valid Id with Authorised Panchayat level user    **Negative Test Cases:**  1.Open Advertisement TaxRate remove Form Without DB Connection 2. Open Advertisement TaxRate remove Form with Invalid id   3.Open Advertisement TaxRate remove form with Already removed Advertisement TaxRate Id with Authorised user|Id|1|3|4|testPosAuthorisedPanLevelUserOpenPanLevelAdvertisementTaxRateRemoveFormWithValidId,  testPosAuthorisedPanLevelUserOpenAdvertisementTaxRateRemoveFormWithoutDBConnection,  testNegAuthorisedPanLevelUserOpenAdvertisementTaxRateRemoveFormWithInValidId,  testNegAuthorisedPanUserOpenAdvertisementTaxRateRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_ADVTAXRATE_360  ut_n_r_GSTS_WEB_ADVTAXRATE_370 ut_n_r_GSTS_WEB_ADVTAXRATE_390  ut_n_r_GSTS_WEB_ADVTAXRATE_400  ut_n_r_GSTS_WEB_ADVTAXRATE_420 |**Positive Test Cases:** Remove Advertisement TaxRate with Valid Remove Comment with Panchayat Level Authorised User **Negative Test Cases:** 1. Removing Advertisement TaxRate with invalid remove comment 2.Remove Advertisement TaxRate without db connection 3.Remove already removed Advertisement TaxRate  4. Remove Advertisement TaxRate with invalid Id| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|testPosPanLevelAuthorisedUserRemoveAdvertisementTaxRateWithValidRemoveCommentAndValidId,  testNegPanLevelAuthorisedUserRemoveAdvertisementTaxRateWithInValidRemoveCommentAndValidId,  testNegRemoveAdvertisementTaxRateWithoutDbConnection,  testNegAuthorisedUserRemoveAlreadyRemovedAdvertisementTaxRate,  testNegPanLevelAuthorisedUserRemoveAdvertisementTaxRateWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_ADVTAXRATE_530  ut_n_v_GSTS_WEB_ADVTAXRATE_540 ut_n_v_GSTS_WEB_ADVTAXRATE_550 |**Positive Test Cases:** View Advertisement TaxRate with Valid Id  with Authorised User **Negative Test Cases:** 1.View Advertisement TaxRate without db connection 2.View Advertisement TaxRate with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewAdvertisementTaxRateWithValidId,  testPosAuthorisedUserViewAdvertisementTaxRateWithoutDbConnection,  testNegAuthorisedUserViewAdvertisementTaxRatewithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_ADVTAXRATE_680 ut_n_s_GSTS_WEB_ADVTAXRATE_690 ut_n_s_GSTS_WEB_ADVTAXRATE_700|**Positive Test Cases:** Search Advertisement TaxRate  with valid inputs **Negative Test Cases:** 1.Search Advertisement TaxRate without db connection 2.Search Advertisement TaxRate with invalid inputs|**1.advCategory 2.advAsset**|1|2|3|testPosAuthorisedUserSearchAdvertisementTaxRateWithValidInputs,  testNegAuthorisedUserSearchAdvertisementTaxRateWithoutDBconnection,  testNegAuthorisedUserSearchAdvertisementTaxRateWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_ADVTAXRATE_610 ut_n_l_GSTS_WEB_ADVTAXRATE_620|**Positive Test Cases:**  Get Advertisement TaxRate List with Authorised User **Negative Test Cases:** Get Advertisement TaxRate List without db connection|Validating with unique field|1|1|2|testPosAuthorisedUserGetAdvertisementTaxRateList,  testNegAuthorisedUserAdvertisementTaxRateListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_ADVTAXRATE_760   ut_n_ep_GSTS_WEB_ADVTAXRATE_770   ut_n_ep_GSTS_WEB_ADVTAXRATE_780 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportAdvertisementTaxRatePdfWithValidId,  testNegAuthorisedUserExportAdvertisementTaxRatePdfwithoutDbconnection,  testNegAuthorisedUserExportAdvertisementTaxRatePdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_ADVTAXRATE_790   ut_n_elp_GSTS_WEB_ADVTAXRATE_800   ut_n_elp_GSTS_WEB_ADVTAXRATE_810 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportAdvertisementTaxRateListPdfWithValidId,  testNegAuthorisedUserExportAdvertisementTaxRateListPdfwithoutDbconnection,  testNegAuthorisedUserExportAdvertisementTaxRateListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_ADVTAXRATE_820   ut_n_ex_GSTS_WEB_ADVTAXRATE_830   ut_n_ex_GSTS_WEB_ADVTAXRATE_840 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportAdvertisementTaxRateXlxWithValidId,  testNegAuthorisedUserExportAdvertisementTaxRateXlxwithoutDbconnection,  testNegAuthorisedUserExportAdvertisementTaxRateXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_ADVTAXRATE_850   ut_n_elx_GSTS_WEB_ADVTAXRATE_860   ut_n_elx_GSTS_WEB_ADVTAXRATE_870 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportAdvertisementTaxRateListXlxWithValidId,  testNegAuthorisedUserExportAdvertisementTaxRateListXlxwithoutDbconnection,  testNegAuthorisedUserExportAdvertisementTaxRateListXlxInValidId|


#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|------|
|1.0| Create Form|ut_n_c_GSTS_WEB_ADVTAXRATE_260|Unauthorised User opening Advertisement TaxRate create form||0|1|1|testNegUnAuthorisedUserOpenAdvertisementTaxRateCreateForm|
|1.0| Create |ut_n_c_GSTS_WEB_ADVTAXRATE_250|Unauthorised User does not have permission to create|**panchayatResolutionId:** drop down list **advCategory:** enums **advAsset:** enums  **taxVal:** 1.null 2. >=1 and <=100000|0|1|1|testNegUnAuthorisedUserCreateAdvertisementTaxRate|
|1.0| Remove Form|ut_n_r_GSTS_WEB_ADVTAXRATE_510|Unauthorised User opening Advertisement TaxRate remove form||0|1|1|testNegUnAuthorisedPanLevelUserOpenAdvertisementTaxRateRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_ADVTAXRATE_520|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserRemoveAdvertisementTaxRate|
|1.0| View |ut_n_v_GSTS_WEB_ADVTAXRATE_600|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewAdvertisementTaxRate|
|1.0| Search |ut_n_s_GSTS_WEB_ADVTAXRATE_750|Unauthorised User does not have permission to search|**1.advCategory 2.advAsset**|0|1|1|testNegUnAuthorisedUserSearchAdvertisementTaxRate|
|1.0| List |ut_n_l_GSTS_WEB_ADVTAXRATE_670|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserAdvertisementTaxRateList|
|1.0| PDF |ut_n_ep_GSTS_WEB_ADVTAXRATE_920 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportAdvertisementTaxRatePdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_ADVTAXRATE_930 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportAdvertisementTaxRateListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_ADVTAXRATE_940 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportAdvertisementTaxRateXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_ADVTAXRATE_950 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportAdvertisementTaxRateListXlxWithValidId|


#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|---------|
|1.0|Create|ut_n_c_GSTS_WEB_ADVTAXRATE_170|Create Advertisement TaxRate at State Level| N/A |Will not be Created|1|testNegCreateAdvertisementTaxRateAtStateLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_ADVTAXRATE_180|Open Advertisement TaxRate Create Form at State Level| N/A |Will not be Opened|1|testNegOpenAdvertisementTaxRateCreateFormAtStateLevel|
|1.0|Create|ut_n_c_GSTS_WEB_ADVTAXRATE_190|Create Advertisement TaxRate at District Level| N/A |Will not be Created|1|testNegCreateAdvertisementTaxRateAtDistLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_ADVTAXRATE_200|Open Advertisement TaxRate Create Form at District Level| N/A |Will not be Opened|1|testNegOpenAdvertisementTaxRateCreateFormAtDistLevel|
|1.0|Create|ut_n_c_GSTS_WEB_ADVTAXRATE_210|Create Advertisement TaxRate at Division Level| N/A |Will not be Created|1|testNegCreateAdvertisementTaxRateAtDivLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_ADVTAXRATE_220|Open Advertisement TaxRate Create Form at Division Level| N/A |Will not be Opened|1|testNegOpenAdvertisementTaxRateCreateFormAtDivLevel|
|1.0|Create|ut_n_c_GSTS_WEB_ADVTAXRATE_230|Create Advertisement TaxRate at Mandal Level| N/A |Will not be Created|1|testNegCreateAdvertisementTaxRateAtMandalLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_ADVTAXRATE_240|Open Advertisement TaxRate Create Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenAdvertisementTaxRateCreateFormAtMandalLevel|
1.0|Create|ut_n_c_GSTS_WEB_ADVTAXRATE_290|Create Advertisement TaxRate in panchayat1112 with panchayat1111 Panchayat Resolution Id| N/A |Will not be Created|1|testNegCreateAdvertisementTaxRateInpanchayat1112WithPanchayat1111PanchayatResolutionId|
|1.0|Remove Form|ut_n_r_GSTS_WEB_ADVTAXRATE_430|Open Advertisement TaxRate Remove Form at State Level| N/A |Will not be Opened|1|testNegOpenAdvertisementTaxRateRemoveFormAtStateLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_ADVTAXRATE_440|Remove Advertisement TaxRate at State Level| N/A |Will not be Removed|1|testNegRemoveAdvertisementTaxRateAtStateLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_ADVTAXRATE_450|Open Advertisement TaxRate Remove Form at District Level| N/A |Will not be Opened|1|testNegOpenAdvertisementTaxRateRemoveFormAtDistLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_ADVTAXRATE_460|Remove Advertisement TaxRate at District Level| N/A |Will not be Removed|1|testNegRemoveAdvertisementTaxRateAtDistLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_ADVTAXRATE_470|Open Advertisement TaxRate Remove Form at Division Level| N/A |Will not be Opened|1|testNegOpenAdvertisementTaxRateRemoveFormAtDivLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_ADVTAXRATE_480|Remove Advertisement TaxRate at Division Level| N/A |Will not be Removed|1|testNegRemoveAdvertisementTaxRateAtDivLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_ADVTAXRATE_490|Open Advertisement TaxRate Remove Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenAdvertisementTaxRateRemoveFormAtMandalLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_ADVTAXRATE_500|Remove Advertisement TaxRate at Mandal Level| N/A |Will not be Removed|1|testNegRemoveAdvertisementTaxRateAtMandalLevel|
|1.0|View|ut_n_v_GSTS_WEB_ADVTAXRATE_560|View Advertisement TaxRate at State Level| N/A |Will not be Accessed|1|testNegViewAdvertisementTaxRateAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_ADVTAXRATE_570|View Advertisement TaxRate at District Level| N/A |Will not be Accessed|1|testNegViewAdvertisementTaxRateAtDistLevel|
|1.0|View|ut_n_v_GSTS_WEB_ADVTAXRATE_580|View Advertisement TaxRate at Division Level| N/A |Will not be Accessed|1|testNegViewAdvertisementTaxRateAtDivLevel|
|1.0|View|ut_n_v_GSTS_WEB_ADVTAXRATE_590|View Advertisement TaxRate at Mandal Level| N/A |Will not be Accessed|1|testNegViewAdvertisementTaxRateAtMandalLevel|
|1.0|List|ut_n_l_GSTS_WEB_ADVTAXRATE_630|Get Advertisement TaxRate List at State Level| N/A |Will not be Accessed|1|testNegAdvertisementTaxRateListAtStateLevel|
|1.0|List|ut_n_l_GSTS_WEB_ADVTAXRATE_640|Get Advertisement TaxRate List at District Level| N/A |Will not be Accessed|1|testNegAdvertisementTaxRateListAtDistLevel|
|1.0|List|ut_n_l_GSTS_WEB_ADVTAXRATE_650|Get Advertisement TaxRate List at Division Level| N/A |Will not be Accessed|1|testNegAdvertisementTaxRateListAtDivLevel|
|1.0|List|ut_n_l_GSTS_WEB_ADVTAXRATE_660|Get Advertisement TaxRate List at Mandal Level| N/A |Will not be Accessed|1|testNegAdvertisementTaxRateListAtMandalLevel|
|1.0|Search|ut_n_s_GSTS_WEB_ADVTAXRATE_710|Search Advertisement TaxRate  at State Level| N/A |Will not be Accessed|1|testNegSearchAdvertisementTaxRateAtStateLevel|
|1.0|Search|ut_n_s_GSTS_WEB_ADVTAXRATE_720|Search Advertisement TaxRate  at District Level| N/A |Will not be Accessed|1|testNegSearchAdvertisementTaxRateAtDistLevel|
|1.0|Search|ut_n_s_GSTS_WEB_ADVTAXRATE_730|Search Advertisement TaxRate  at Division Level| N/A |Will not be Accessed|1|testNegSearchAdvertisementTaxRateAtDivLevel|
|1.0|Search|ut_n_s_GSTS_WEB_ADVTAXRATE_740|Search Advertisement TaxRate  at Mandal Level| N/A |Will not be Accessed|1|testNegSearchAdvertisementTaxRateAtMandalLevel|
|1.0|Pdf|ut_n_p_GSTS_WEB_ADVTAXRATE_880|Export Advertisement TaxRate Pdf at State Level| N/A |Will not be exported|1|testNegExportAdvertisementTaxRatePdfAtStateLevel|
|1.0|List Pdf|ut_n_p_GSTS_WEB_ADVTAXRATE_890|Export Advertisement TaxRate List Pdf at State Level| N/A |Will not be exported|1|testNegExportAdvertisementTaxRateListPdfAtStateLevel|
|1.0|Xlx|ut_n_p_GSTS_WEB_ADVTAXRATE_900|Export Advertisement TaxRate Xlx at State Level| N/A |Will not be exported|1|testNegExportAdvertisementTaxRateXlxAtStateLevel|
|1.0|List Xlx|ut_n_p_GSTS_WEB_ADVTAXRATE_910|Export Advertisement TaxRate List Xlx at State Level| N/A |Will not be exported|1|testNegExportAdvertisementTaxRateListXlxAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_ADVTAXRATE_960|Panchayat1112 user trying to access Panchayat1111 Advertisement TaxRate which does not belongs to his context| N/A |Will not be accessed|1|testNegPanchayat1112UserAccessingPanchayat1111AdvertisementTaxRate|
|1.0|Remove|ut_n_r_GSTS_WEB_ADVTAXRATE_965|Panchayat1112 user trying to remove Panchayat1111 Advertisement TaxRate which does not belongs to his context| N/A |Will not be removed|1|testNegPanchayat1112UserRemovingPanchayat1111AdvertisementTaxRate|


## Security compliance check
1. Only user having the permission **ROLE_ADVERTISEMENT_TAX_RATE_VIEW** should view this functionality 
1. Only user having the permission **ROLE_ADVERTISEMENT_TAX_RATE_CREATE** should create this functionality 
1. Only user having the permission **ROLE_ADVERTISEMENT_TAX_RATE_REMOVE** should remove this functionality 
1. Only user having the permission **ROLE_ADVERTISEMENT_TAX_RATE_VIEW** should export this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Advertisement Tax Rate in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
