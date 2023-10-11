---
title: House Module Tax Rate
tags : ["Composing"]
---

## Introduction
House Module Tax Rate is one of the features of this software product. House module tax rate is a tax rate defined for house modules. House module tax rate depends on panchayat resolution. House module tax rate may be different for house modules based on roof type and house category type and construction type. It may vary from one panchayat to other panchayat. Users will have access to house module tax rates if they have permission, Otherwise will not access.

## Business Assumptions
What type of users can create house module tax rate should be planned at design phase.

## Requirements
### Functional Requirements
1. Users of all levels can create, remove, view and export the house module tax rate.  
1. We can create and remove house module tax rate at panchayat level only.
1. House Module Tax Rate feature is accessible at panchayat level only.
1. Panchayat Resolution is required to create a house module tax rate.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access house module tax rates.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
House module tax rate feature contains information about different house module tax rates of panchayat.

### Design 
1. Each house module tax rate has Panchayat Resolution, Construction Value per SFT(RS), House Category Type, Roof Type, and Construction Type. 
1. Each house module tax rate in same panchayat has a unique panchayat resolution or unique roof type or unique construction type or unique house category.
1. We can create, remove, view and export the house module tax rate.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_house_module_tax_rate_list|To view all the house module tax rates. This listing page should bind to a permission|
|uc_house_module_tax_rate_create|To create the house module tax rate. This create page should bind to a permission|
|uc_house_module_tax_rate_remove|To remove the house module tax rate. This remove page should bind to a permission|
|uc_house_module_tax_rate_view|To view the house module tax rate. This view page should bind to a permission|
|uc_house_module_tax_rate_search|To search the house module tax rate. This search page should bind to a permission|
|uc_house_module_tax_rate_export|To export the house module tax rate in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|panchayatResolution|YES|NA|Dropdown values|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "pr_id", nullable = false)|pr_id varchar(32) NOT NULL|YES|YES|YES|YES|NO||
|taxVal|YES|NA|0-9 and ., maxlen=8|@Column(name = "tax_val", nullable = false)|tax_val float(9,2) NOT NULL|YES|YES|YES|YES|NO||
|houseCategoryType|YES|NA|Dropdown values|@Enumerated(EnumType.STRING) @Column(name = "house_category", length = 16, nullable = false)|house_category varchar(16) NOT NULL|YES|YES|YES|YES|YES||
|roofType|YES|NA|Dropdown values|@Enumerated(EnumType.STRING) @Column(name = "roof_type", length = 16, nullable = false)|roof_type varchar(32) NOT NULL|YES|YES|YES|YES|YES||
|constructionType|YES|NA|Dropdown values|@Enumerated(EnumType.STRING) @Column(name = "construction_type", length = 16, nullable = false)|construction_type varchar(32) NOT NULL|YES|YES|YES|YES|YES||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### House Category

{{<mermaid align="left">}}
classDiagram
    class HouseCatType{
      RESIDENTIAL
      COMMERCIAL
      EXEMPTION
      NONE
    }
{{< /mermaid >}}

##### Roof Type

{{<mermaid align="left">}}
classDiagram
    class RoofType{
      RCC
      AC_SHEETS_OR_ZINC_SHEETS
      COUNTRY_OR_MANGALORE_TILES
      SHABAD_STONES
      THATCHED_OR_MUD_ROOF
      NONE
    }
{{< /mermaid >}}

##### Construction Type

{{<mermaid align="left">}}
classDiagram
    class ConstructionType{
      COMPLETED
      NOT_COMPLETED
      NONE
    }
{{< /mermaid >}}


#### Feature Permission

|Permission code|Action|
|---------------|-------|
|HOUSE_MODULE_TAX_RATE_VIEW|View|
|HOUSE_MODULE_TAX_RATE_CREATE|Create|
|HOUSE_MODULE_TAX_RATE_REMOVE|Remove|
|HOUSE_MODULE_TAX_RATE_VIEW|Export|
|HOUSE_MODULE_TAX_RATE_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_hmtr__prid__pid__rty__hcat__cty` (pr_id, org_panchayat_id, roof_type, house_category, construction_type)|
|Foreign Key|fk__gs_house_module_tax_rate__pr_id (pr_id) REFERENCES gs_pr (id)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_HOUSE_MODULE_TAX_RATE_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_HOUSE_MODULE_TAX_RATE_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_HOUSE_MODULE_TAX_RATE_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_HOUSE_MODULE_TAX_RATE_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

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
	HouseModuleTaxRateMenu((House Module TaxRate Menu))
	ListPage{House Module TaxRate List Page}
	CreatePage((Create Page))
	RemovePage((Remove Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->HouseModuleTaxRateMenu
    subgraph Menu
    HouseModuleTaxRateMenu
    end
    subgraph   
    HouseModuleTaxRateMenu-->ListPage
    ListPage--C-R-V-E-->ListPage
    end
    subgraph  
    HouseModuleTaxRateMenu--F-->ErrorPage
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
1. Only a user with the HOUSE_MODULE_TAX_RATE_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant HouseModuleTaxRateListpage as Browser
    participant Net as Browser Net Tools
    participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        HouseModuleTaxRateListpage->>+Net: Check Internet, GET /app/ctx/HouseModuleTaxRate/list ListPage
        Net--x-HouseModuleTaxRateListpage: F : Connection Error
        HouseModuleTaxRateListpage->>+cloud: S:  GET /app/ctx/HouseModuleTaxRate/list ListPage
        cloud-->>-HouseModuleTaxRateListpage: RES:List Page
    end
    rect rgb(244,244,244)
        HouseModuleTaxRateListpage->>+Net: Check Internet, GET /app/HouseModuleTaxRate/create/form CreateFormPage
        Net--x-HouseModuleTaxRateListpage: F : Connection Error
        HouseModuleTaxRateListpage->>+cloud: S : GET /app/HouseModuleTaxRate/create/form CreateFormPage
        cloud-->>-HouseModuleTaxRateListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        HouseModuleTaxRateListpage->>+Net: Check Internet: POST /app/HouseModuleTaxRate/create Create
        Net--x-HouseModuleTaxRateListpage: F : Connection Error
        HouseModuleTaxRateListpage->>+cloud: S : POST /app/HouseModuleTaxRate/create Create
        cloud-->>-HouseModuleTaxRateListpage: RES: An House Module TaxRate Successfully Created
    end
    rect rgb(244,244,244)
        HouseModuleTaxRateListpage->>+Net: Check Internet: GET /app/HouseModuleTaxRate/remove/form RemoveFormPage
        Net--x-HouseModuleTaxRateListpage: F : Connection Error
        HouseModuleTaxRateListpage->>+cloud: S : GET /app/HouseModuleTaxRate/remove/form RemoveFormPage
        cloud-->>-HouseModuleTaxRateListpage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        HouseModuleTaxRateListpage->>+Net: Check Internet: POST /app/HouseModuleTaxRate/remove Remove
        Net--x-HouseModuleTaxRateListpage: F : Connection Error
        HouseModuleTaxRateListpage->>+cloud: S : POST /app/HouseModuleTaxRate/remove Remove
        cloud-->>-HouseModuleTaxRateListpage: RES: An House Module TaxRate Successfully Removed
    end
    rect rgb(244,244,244)
        HouseModuleTaxRateListpage->>+Net: Check Internet: GET /app/HouseModuleTaxRate/view ViewPage
        Net--x-HouseModuleTaxRateListpage: F : Connection Error
        alt
		note right of Net:  House Module Tax Rate Cache Object Found
        HouseModuleTaxRateListpage->>+Cache: S : GET /app/HouseModuleTaxRate/view ViewPage
        Cache-->>-HouseModuleTaxRateListpage: RES: House Module TaxRate View
        else
		note right of Net:  House Module Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/HouseModuleTaxRate/view ViewPage
        cloud-->>-HouseModuleTaxRateListpage: RES: House Module TaxRate View
        end
    end
    rect rgb(244,244,244)
        HouseModuleTaxRateListpage->>+Net: Check Internet: GET /app/HouseModuleTaxRate/exportPdf ExportPdf
        Net--x-HouseModuleTaxRateListpage: F : Connection Error 
        alt
		note right of Net:  House Module Tax Rate Cache Object Found
        HouseModuleTaxRateListpage->>+Cache: S : GET /app/HouseModuleTaxRate/exportPdf ExportPdf
        Cache-->>-HouseModuleTaxRateListpage: RES: House Module TaxRate Pdf
        else
		note right of Net:  House Module Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/HouseModuleTaxRate/exportPdf ExportPdf
        cloud-->>-HouseModuleTaxRateListpage: RES: House Module TaxRate Pdf
        end
    end
    rect rgb(244,244,244)
        HouseModuleTaxRateListpage->>+Net: Check Internet: GET /app/HouseModuleTaxRate/exportListPdf ExportListPdf
        Net--x-HouseModuleTaxRateListpage: F : Connection Error
        HouseModuleTaxRateListpage->>+cloud: S : GET /app/HouseModuleTaxRate/exportListPdf ExportListPdf
        cloud-->>-HouseModuleTaxRateListpage: RES: House Module TaxRate List Pdf
    end
    rect rgb(244,244,244)
        HouseModuleTaxRateListpage->>+Net: Check Internet: GET /app/HouseModuleTaxRate/exportXlx ExportXlx
        Net--x-HouseModuleTaxRateListpage: F : Connection Error
        alt
		note right of Net:  House Module Tax Rate Cache Object Found
        HouseModuleTaxRateListpage->>+Cache: S : GET /app/HouseModuleTaxRate/exportXlx ExportXlx
        Cache-->>-HouseModuleTaxRateListpage: RES: House Module TaxRate Xlx
        else
		note right of Net:  House Module Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/HouseModuleTaxRate/exportXlx ExportXlx
        cloud-->>-HouseModuleTaxRateListpage: RES: House Module TaxRate Xlx
        end
    end
    rect rgb(244,244,244)
        HouseModuleTaxRateListpage->>+Net: Check Internet: GET /app/HouseModuleTaxRate/exportListXlx ExportListXlx
        Net--x-HouseModuleTaxRateListpage: F : Connection Error
        HouseModuleTaxRateListpage->>+cloud: S : GET /app/HouseModuleTaxRate/exportListXlx ExportListXlx
        cloud-->>-HouseModuleTaxRateListpage: RES: House Module TaxRate List Xlx
    end

          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|------|
|1.0| Create Form |ut_p_c_GSTS_WEB_HOUSEMODULETAXRATE_120 ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_115 ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_130 |**Positive Test Cases:** 1.Open HouseModule TaxRate Create Form At panchayat level  **Negative Test Cases:** 1. Open HouseModule TaxRate Create Form with no panchayat resolution exists 2. Open HouseModule TaxRate Create Form Without Db connection |-|1|2|3|testPosOpenHouseModuleTaxRateCreateFormWithAuthorisedUser,  testNegOpenHouseModuleTaxRateCreateFormWithNoPanchayatResolutionExists,  testPosOpenHouseModuleTaxRateCreateFormWithDBConnection|
|1.0| Create |ut_p_c_GSTS_WEB_HOUSEMODULETAXRATE_150  ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_160 ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_140 ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_270 ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_280 |**Positive Test Cases:** Create HouseModule TaxRate with valid inputs with Panchayat Level Authorised User **Negative Test Cases:** 1.Create HouseModule TaxRate with Invalid inputs 2.Create HouseModule TaxRate without db connection 3.Create HouseModule TaxRate with Removed Panchayat Resolution Id  4.Create HouseModule TaxRate with Invalid Panchayat Resolution Id|**panchayatResolutionId:** drop down list **houseCategoryType:** enums **roofType:** enums **constructionType:** enums **taxVal:** 1.null 2. >=1 and <=100000|72|73|145|testPosAuthorisedPanchayatLevelUserCreateHouseModuleTaxRateWithValidInputs,  testNegAuthorisedPanchayatLevelUserCreateHouseModuleTaxRateWithInValidInputs, testNegCreateHouseModuleTaxRateWithoutDBconnection,  testNegCreateHouseModuleTaxRateWithRemovedPanchayatResolutionId,  testNegCreateHouseModuleTaxRateWithInvalidPanchayatResolutionId|
|1.0| Remove Form |ut_p_r_GSTS_WEB_HOUSEMODULETAXRATE_330   ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_340   ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_350  ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_410|**Positive Test Cases:** Open HouseModule TaxRate remove form with valid Id with Authorised Panchayat level user    **Negative Test Cases:**  1.Open HouseModule TaxRate remove Form Without DB Connection 2. Open HouseModule TaxRate remove Form with Invalid id   3.Open HouseModule TaxRate remove form with Already removed HouseModule TaxRate Id with Authorised user|Id|1|3|4|testPosAuthorisedPanLevelUserOpenPanLevelHouseModuleTaxRateRemoveFormWithValidId,  testPosAuthorisedPanLevelUserOpenHouseModuleTaxRateRemoveFormWithoutDBConnection,  testNegAuthorisedPanLevelUserOpenHouseModuleTaxRateRemoveFormWithInValidId,  testNegAuthorisedPanUserOpenHouseModuleTaxRateRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_HOUSEMODULETAXRATE_360  ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_370 ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_390  ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_400  ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_420 |**Positive Test Cases:** Remove HouseModule TaxRate with Valid Remove Comment with Panchayat Level Authorised User **Negative Test Cases:** 1. Removing HouseModule TaxRate with invalid remove comment 2.Remove HouseModule TaxRate without db connection 3.Remove already removed HouseModule TaxRate  4. Remove HouseModule TaxRate with invalid Id| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|testPosPanLevelAuthorisedUserRemoveHouseModuleTaxRateWithValidRemoveCommentAndValidId,  testNegPanLevelAuthorisedUserRemoveHouseModuleTaxRateWithInValidRemoveCommentAndValidId,  testNegRemoveHouseModuleTaxRateWithoutDbConnection,  testNegAuthorisedUserRemoveAlreadyRemovedHouseModuleTaxRate,  testNegPanLevelAuthorisedUserRemoveHouseModuleTaxRateWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_HOUSEMODULETAXRATE_530  ut_n_v_GSTS_WEB_HOUSEMODULETAXRATE_540 ut_n_v_GSTS_WEB_HOUSEMODULETAXRATE_550 |**Positive Test Cases:** View HouseModule TaxRate with Valid Id  with Authorised User **Negative Test Cases:** 1.View HouseModule TaxRate without db connection 2.View HouseModule TaxRate with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewHouseModuleTaxRateWithValidId,  testPosAuthorisedUserViewHouseModuleTaxRateWithoutDbConnection,  testNegAuthorisedUserViewHouseModuleTaxRatewithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_HOUSEMODULETAXRATE_680 ut_n_s_GSTS_WEB_HOUSEMODULETAXRATE_690 ut_n_s_GSTS_WEB_HOUSEMODULETAXRATE_700|**Positive Test Cases:** Search HouseModule TaxRate with valid inputs **Negative Test Cases:** 1.Search HouseModule TaxRate without db connection 2.Search HouseModule TaxRate with invalid inputs|**1.houseCategoryType 2.roofType 3.constructionType**|1|2|3|testPosAuthorisedUserSearchHouseModuleTaxRateWithValidInputs, testNegAuthorisedUserSearchHouseModuleTaxRateWithoutDBconnection,  testNegAuthorisedUserSearchHouseModuleTaxRateWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_HOUSEMODULETAXRATE_610 ut_n_l_GSTS_WEB_HOUSEMODULETAXRATE_620|**Positive Test Cases:** Get HouseModule TaxRate List with Authorised User **Negative Test Cases:** |Validating with unique field|1|1|2|testPosAuthorisedUserHouseModuleTaxRateList, testNegAuthorisedUserHouseModuleTaxRateListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_HOUSEMODULETAXRATE_760   ut_n_ep_GSTS_WEB_HOUSEMODULETAXRATE_770   ut_n_ep_GSTS_WEB_HOUSEMODULETAXRATE_780 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportHouseModuleTaxRatePdfWithValidId,  testNegAuthorisedUserExportHouseModuleTaxRatePdfwithoutDbconnection,  testNegAuthorisedUserExportHouseModuleTaxRatePdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_HOUSEMODULETAXRATE_790   ut_n_elp_GSTS_WEB_HOUSEMODULETAXRATE_800   ut_n_elp_GSTS_WEB_HOUSEMODULETAXRATE_810 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportHouseModuleTaxRateListPdfWithValidId,  testNegAuthorisedUserExportHouseModuleTaxRateListPdfwithoutDbconnection,  testNegAuthorisedUserExportHouseModuleTaxRateListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_HOUSEMODULETAXRATE_820   ut_n_ex_GSTS_WEB_HOUSEMODULETAXRATE_830   ut_n_ex_GSTS_WEB_HOUSEMODULETAXRATE_840 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportHouseModuleTaxRateXlxWithValidId,  testNegAuthorisedUserExportHouseModuleTaxRateXlxwithoutDbconnection,  testNegAuthorisedUserExportHouseModuleTaxRateXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_HOUSEMODULETAXRATE_850   ut_n_elx_GSTS_WEB_HOUSEMODULETAXRATE_860   ut_n_elx_GSTS_WEB_HOUSEMODULETAXRATE_870 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportHouseModuleTaxRateListXlxWithValidId,  testNegAuthorisedUserExportHouseModuleTaxRateListXlxwithoutDbconnection,  testNegAuthorisedUserExportHouseModuleTaxRateListXlxInValidId|


#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------------|------|
|1.0| Create Form|ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_260|Unauthorised User opening HouseModule TaxRate create form||0|1|1|testNegUnAuthorisedUserOpenHouseModuleTaxRateCreateForm|
|1.0| Create |ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_250 |Unauthorised User does not have permission to create|**panchayatResolutionId:** drop down list **houseCategoryType:** enums **roofType:** enums **constructionType:** enums **taxVal:** 1.null 2. >=1 and <=100000|0|1|1|testNegUnAuthorisedUserCreateHouseModuleTaxRate|
|1.0| Remove Form|ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_510|Unauthorised User opening HouseModule TaxRate remove form||0|1|1|testNegUnAuthorisedPanLevelUserOpenHouseModuleTaxRateRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_520|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=256 3.null |0|1|1|testNegUnAuthorisedUserRemoveHouseModuleTaxRate|
|1.0| View |ut_n_v_GSTS_WEB_HOUSEMODULETAXRATE_600|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewHouseModuleTaxRate|
|1.0| Search |ut_n_s_GSTS_WEB_HOUSEMODULETAXRATE_750|Unauthorised User does not have permission to search|**1.houseCategoryType 2.roofType 3.constructionType**|0|1|1|testNegUnAuthorisedUserSearchHouseModuleTaxRate|
|1.0| List |ut_n_l_GSTS_WEB_HOUSEMODULETAXRATE_670|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserHouseModuleTaxRateList|
|1.0| PDF |ut_n_ep_GSTS_WEB_HOUSEMODULETAXRATE_920 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportHouseModuleTaxRatePdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_HOUSEMODULETAXRATE_930 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportHouseModuleTaxRateListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_HOUSEMODULETAXRATE_940 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportHouseModuleTaxRateXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_HOUSEMODULETAXRATE_950 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportHouseModuleTaxRateListXlxWithValidId|


#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|--------|
|1.0|Create|ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_170|Create HouseModule TaxRate at State Level| N/A |Will not be Created|1|testNegCreateHouseModuleTaxRateAtStateLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_180|Open HouseModule TaxRate Create Form at State Level| N/A |Will not be Opened|1|testNegOpenHouseModuleTaxRateCreateFormAtStateLevel|
|1.0|Create|ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_190|Create HouseModule TaxRate at District Level| N/A |Will not be Created|1|testNegCreateHouseModuleTaxRateAtDistLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_200|Open HouseModule TaxRate Create Form at District Level| N/A |Will not be Opened|1|testNegOpenHouseModuleTaxRateCreateFormAtDistLevel|
|1.0|Create|ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_210|Create HouseModule TaxRate at Division Level| N/A |Will not be Created|1|testNegCreateHouseModuleTaxRateAtDivLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_220|Open HouseModule TaxRate Create Form at Division Level| N/A |Will not be Opened|1|testNegOpenHouseModuleTaxRateCreateFormAtDivLevel|
|1.0|Create|ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_230|Create HouseModule TaxRate at Mandal Level| N/A |Will not be Created|1|testNegCreateHouseModuleTaxRateAtMandalLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_240|Open HouseModule TaxRate Create Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenHouseModuleTaxRateCreateFormAtMandalLevel|
1.0|Create|ut_n_c_GSTS_WEB_HOUSEMODULETAXRATE_290|Create HouseModule TaxRate in panchayat1112 with panchayat1111 Panchayat Resolution Id| N/A |Will not be Created|1|testNegCreateHouseModuleTaxRateInpanchayat1112WithPanchayat1111PanchayatResolutionId|
|1.0|Remove Form|ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_430|Open HouseModule TaxRate Remove Form at State Level| N/A |Will not be Opened|1|testNegOpenHouseModuleTaxRateRemoveFormAtStateLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_440|Remove HouseModule TaxRate at State Level| N/A |Will not be Removed|1|testNegRemoveHouseModuleTaxRateAtStateLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_450|Open HouseModule TaxRate Remove Form at District Level| N/A |Will not be Opened|1|testNegOpenHouseModuleTaxRateRemoveFormAtDistLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_460|Remove HouseModule TaxRate at District Level| N/A |Will not be Removed|1|testNegRemoveHouseModuleTaxRateAtDistLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_470|Open HouseModule TaxRate Remove Form at Division Level| N/A |Will not be Opened|1|testNegOpenHouseModuleTaxRateRemoveFormAtDivLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_480|Remove HouseModule TaxRate at Division Level| N/A |Will not be Removed|1|testNegRemoveHouseModuleTaxRateAtDivLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_490|Open HouseModule TaxRate Remove Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenHouseModuleTaxRateRemoveFormAtMandalLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_500|Remove HouseModule TaxRate at Mandal Level| N/A |Will not be Removed|1|testNegRemoveHouseModuleTaxRateAtMandalLevel|
|1.0|View|ut_n_v_GSTS_WEB_HOUSEMODULETAXRATE_560|View HouseModule TaxRate at State Level| N/A |Will not be Accessed|1|testNegViewHouseModuleTaxRateAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_HOUSEMODULETAXRATE_570|View HouseModule TaxRate at District Level| N/A |Will not be Accessed|1|testNegViewHouseModuleTaxRateAtDistLevel|
|1.0|View|ut_n_v_GSTS_WEB_HOUSEMODULETAXRATE_580|View HouseModule TaxRate at Division Level| N/A |Will not be Accessed|1|testNegViewHouseModuleTaxRateAtDivLevel|
|1.0|View|ut_n_v_GSTS_WEB_HOUSEMODULETAXRATE_590|View HouseModule TaxRate at Mandal Level| N/A |Will not be Accessed|1|testNegViewHouseModuleTaxRateAtMandalLevel|
|1.0|List|ut_n_l_GSTS_WEB_HOUSEMODULETAXRATE_630|Get HouseModule TaxRate List at State Level| N/A |Will not be Accessed|1|testNegHouseModuleTaxRateListAtStateLevel|
|1.0|List|ut_n_l_GSTS_WEB_HOUSEMODULETAXRATE_640|Get HouseModule TaxRate List at District Level| N/A |Will not be Accessed|1|testNegHouseModuleTaxRateListAtDistLevel|
|1.0|List|ut_n_l_GSTS_WEB_HOUSEMODULETAXRATE_650|Get HouseModule TaxRate List at Division Level| N/A |Will not be Accessed|1|testNegHouseModuleTaxRateListAtDivLevel|
|1.0|List|ut_n_l_GSTS_WEB_HOUSEMODULETAXRATE_660|Get HouseModule TaxRate List at Mandal Level| N/A |Will not be Accessed|1|testNegHouseModuleTaxRateListAtMandalLevel|
|1.0|Search|ut_n_s_GSTS_WEB_HOUSEMODULETAXRATE_710|Search HouseModule TaxRate  at State Level| N/A |Will not be Accessed|1|testNegSearchHouseModuleTaxRateAtStateLevel|
|1.0|Search|ut_n_s_GSTS_WEB_HOUSEMODULETAXRATE_720|Search HouseModule TaxRate  at District Level| N/A |Will not be Accessed|1|testNegSearchHouseModuleTaxRateAtDistLevel|
|1.0|Search|ut_n_s_GSTS_WEB_HOUSEMODULETAXRATE_730|Search HouseModule TaxRate  at Division Level| N/A |Will not be Accessed|1|testNegSearchHouseModuleTaxRateAtDivLevel|
|1.0|Search|ut_n_s_GSTS_WEB_HOUSEMODULETAXRATE_740|Search HouseModule TaxRate  at Mandal Level| N/A |Will not be Accessed|1|testNegSearchHouseModuleTaxRateAtMandalLevel|
|1.0|Pdf|ut_n_p_GSTS_WEB_HOUSEMODULETAXRATE_880|Export HouseModule TaxRate Pdf at State Level| N/A |Will not be exported|1|testNegExportHouseModuleTaxRatePdfAtStateLevel|
|1.0|List Pdf|ut_n_p_GSTS_WEB_HOUSEMODULETAXRATE_890|Export HouseModule TaxRate List Pdf at State Level| N/A |Will not be exported|1|testNegExportHouseModuleTaxRateListPdfAtStateLevel|
|1.0|Xlx|ut_n_p_GSTS_WEB_HOUSEMODULETAXRATE_900|Export HouseModule TaxRate Xlx at State Level| N/A |Will not be exported|1|testNegExportHouseModuleTaxRateXlxAtStateLevel|
|1.0|List Xlx|ut_n_p_GSTS_WEB_HOUSEMODULETAXRATE_910|Export HouseModule TaxRate List Xlx at State Level| N/A |Will not be exported|1|testNegExportHouseModuleTaxRateListXlxAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_HOUSEMODULETAXRATE_960|Panchayat1112 user trying to access Panchayat1111 HouseModule TaxRate which does not belongs to his context| N/A |Will not be accessed|1|testNegPanchayat1112UserAccessingPanchayat1111HouseModuleTaxRate|
|1.0|Remove|ut_n_r_GSTS_WEB_HOUSEMODULETAXRATE_965|Panchayat1112 user trying to remove Panchayat1111 HouseModule TaxRate which does not belongs to his context| N/A |Will not be removed|1|testNegPanchayat1112UserRemovingPanchayat1111HouseModuleTaxRate|



## Security compliance check
1. Only user having the permission **ROLE_HOUSE_MODULE_TAX_RATE_VIEW** should view this functionality 
1. Only user having the permission **ROLE_HOUSE_MODULE_TAX_RATE_CREATE** should create this functionality 
1. Only user having the permission **ROLE_HOUSE_MODULE_TAX_RATE_REMOVE** should remove this functionality 
1. Only user having the permission **ROLE_HOUSE_MODULE_TAX_RATE_VIEW** should export this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the House Module Tax Rate in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
