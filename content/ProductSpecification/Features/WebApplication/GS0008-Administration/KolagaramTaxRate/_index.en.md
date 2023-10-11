---
title: Kolagaram Tax Rate
tags : ["Composing"]
---

## Introduction
Kolagaram Tax Rate is one of the features of this software product. Kolagaram tax rate is a tax rate defined for kolagaram properties. Kolagaram tax rate depends upon panchayat resolution. Kolagaram tax rate may be differnt for kolagaram properties based on kolagaram cateogry. It may vary from one panchayat to other panchayat. Users will have access to kolagaram tax rates if they have permission, Otherwise will not access.

## Business Assumptions
What type of users can create kolagaram tax rate should be planned at design phase.

## Requirements
### Functional Requirements
1. Users of all levels can create, remove, view and export the kolagaram tax rate.  
1. We can create and remove kolagaram tax rate at panchayat level only.
1. Kolagaram Tax Rate feature is accessible at panchayat level only.
1. Panchayat Resolution is required to create a kolagaram tax rate.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access kolagaram tax rates.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Kolagaram tax rate feature contains information about different kolagaram tax rates of panchayat.

### Design 
1. Each kolagaram tax rate has Panchayat Resolution, Tax Value (%), and  Kolagaram Category.
1. Each kolagaram tax rate in same panchayat has unique panchayat resolution or unique kolagaram category.
1. We can create, remove, view and export the kolagaram tax rate.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_kolagaram_tax_rate_list|To view all the kolagaram tax rates. This listing page should bind to a permission|
|uc_kolagaram_tax_rate_create|To create the kolagaram tax rate. This create page should bind to a permission|
|uc_kolagaram_tax_rate_remove|To remove the kolagaram tax rate. This remove page should bind to a permission|
|uc_kolagaram_tax_rate_view|To view the kolagaram tax rate. This view page should bind to a permission|
|uc_kolagaram_tax_rate_search|To search the kolagaram tax rate. This search page should bind to a permission|
|uc_kolagaram_tax_rate_export|To export the kolagaram tax rate in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|panchayatResolution|YES|NA|Dropdown values|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "pr_id", nullable = false)|pr_id varchar(32) NOT NULL|YES|YES|YES|YES|NO||
|taxVal|YES|NA|0-9 and ., maxlen=6|@Column(name = "tax_val", nullable = false)|tax_val float(9,2) NOT NULL|YES|YES|YES|YES|NO||
|kolgCatType|YES|NA|Dropdown values|@Enumerated(EnumType.STRING) @Column(name = "kolg_asset", length = 16, nullable = false)|kolg_asset varchar(16) NOT NULL|YES|YES|YES|YES|YES||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Kolagaram Category

{{<mermaid align="left">}}
classDiagram
    class KolagaramCatType{
      BRICKS
      CEMENT_BRICKS
      EGGS
      COMMERCIAL_CROPS
      GLASS_BEADS
      OTHER
      NONE
    }
{{< /mermaid >}}


#### Feature Permission

|Permission code|Action|
|---------------|-------|
|KOLAGARAM_TAX_RATE_VIEW|View|
|KOLAGARAM_TAX_RATE_CREATE|Create|
|KOLAGARAM_TAX_RATE_REMOVE|Remove|
|KOLAGARAM_TAX_RATE_VIEW|Export|
|KOLAGARAM_TAX_RATE_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_kolg_tax_rate__prid__org_panchayat_id__kolg_asset (pr_id, org_panchayat_id, kolg_asset)|
|Foreign Key|fk__gs_kolg_tax_rate__pr_id (pr_id) REFERENCES gs_pr (id)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_KOLAGARAM_TAX_RATE_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_KOLAGARAM_TAX_RATE_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_KOLAGARAM_TAX_RATE_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_KOLAGARAM_TAX_RATE_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

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
	KolagaramTaxRateMenu((Kolagaram Tax Rate Menu))
	ListPage{Kolagaram Tax Rate List Page}
	CreatePage((Create Page))
	RemovePage((Remove Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->KolagaramTaxRateMenu
    subgraph Menu
    KolagaramTaxRateMenu
    end
    subgraph   
    KolagaramTaxRateMenu-->ListPage
    ListPage--C-R-V-E-->ListPage
    end
    subgraph  
    KolagaramTaxRateMenu--F-->ErrorPage
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
1. Only a user with the KOLAGARAM_TAX_RATE_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant KolagaramTaxRateListpage as Browser
    participant Net as Browser Net Tools
    participant Cache as GS-Cloud-Cache    
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        KolagaramTaxRateListpage->>+Net: Check Internet, GET /app/ctx/KolagaramTaxRate/list ListPage
        Net--x-KolagaramTaxRateListpage: F : Connection Error
        KolagaramTaxRateListpage->>+cloud: S:  GET /app/ctx/KolagaramTaxRate/list ListPage
        cloud-->>-KolagaramTaxRateListpage: RES:List Page
    end
    rect rgb(244,244,244)
        KolagaramTaxRateListpage->>+Net: Check Internet, GET /app/KolagaramTaxRate/create/form CreateFormPage
        Net--x-KolagaramTaxRateListpage: F : Connection Error
        KolagaramTaxRateListpage->>+cloud: S : GET /app/KolagaramTaxRate/create/form CreateFormPage
        cloud-->>-KolagaramTaxRateListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        KolagaramTaxRateListpage->>+Net: Check Internet: POST /app/KolagaramTaxRate/create Create
        Net--x-KolagaramTaxRateListpage: F : Connection Error
        KolagaramTaxRateListpage->>+cloud: S : POST /app/KolagaramTaxRate/create Create
        cloud-->>-KolagaramTaxRateListpage: RES: An Kolagaram TaxRate Successfully Created
    end
    rect rgb(244,244,244)
        KolagaramTaxRateListpage->>+Net: Check Internet: GET /app/KolagaramTaxRate/remove/form RemoveFormPage
        Net--x-KolagaramTaxRateListpage: F : Connection Error
        KolagaramTaxRateListpage->>+cloud: S : GET /app/KolagaramTaxRate/remove/form RemoveFormPage
        cloud-->>-KolagaramTaxRateListpage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        KolagaramTaxRateListpage->>+Net: Check Internet: POST /app/KolagaramTaxRate/remove Remove
        Net--x-KolagaramTaxRateListpage: F : Connection Error
        KolagaramTaxRateListpage->>+cloud: S : POST /app/KolagaramTaxRate/remove Remove
        cloud-->>-KolagaramTaxRateListpage: RES: An Kolagaram TaxRate Successfully Removed
    end
    rect rgb(244,244,244)
        KolagaramTaxRateListpage->>+Net: Check Internet: GET /app/KolagaramTaxRate/view ViewPage
        Net--x-KolagaramTaxRateListpage: F : Connection Error
        alt
		note right of Net:  Kolagaram Tax Rate Cache Object Found
        KolagaramTaxRateListpage->>+Cache: S : GET /app/KolagaramTaxRate/view ViewPage
        Cache-->>-KolagaramTaxRateListpage: RES: Kolagaram TaxRate View
        else
		note right of Net:  Kolagaram Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/KolagaramTaxRate/view ViewPage
        cloud-->>-KolagaramTaxRateListpage: RES: Kolagaram TaxRate View
        end
    end
    rect rgb(244,244,244)
        KolagaramTaxRateListpage->>+Net: Check Internet: GET /app/KolagaramTaxRate/exportPdf ExportPdf
        Net--x-KolagaramTaxRateListpage: F : Connection Error 
        alt
		note right of Net:  Kolagaram Tax Rate Cache Object Found
        KolagaramTaxRateListpage->>+Cache: S : GET /app/KolagaramTaxRate/exportPdf ExportPdf
        Cache-->>-KolagaramTaxRateListpage: RES: Kolagaram TaxRate Pdf
        else
		note right of Net:  Kolagaram Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/KolagaramTaxRate/exportPdf ExportPdf
        cloud-->>-KolagaramTaxRateListpage: RES: Kolagaram TaxRate Pdf
        end
    end
    rect rgb(244,244,244)
        KolagaramTaxRateListpage->>+Net: Check Internet: GET /app/KolagaramTaxRate/exportListPdf ExportListPdf
        Net--x-KolagaramTaxRateListpage: F : Connection Error
        KolagaramTaxRateListpage->>+cloud: S : GET /app/KolagaramTaxRate/exportListPdf ExportListPdf
        cloud-->>-KolagaramTaxRateListpage: RES: Kolagaram TaxRate List Pdf
    end
    rect rgb(244,244,244)
        KolagaramTaxRateListpage->>+Net: Check Internet: GET /app/KolagaramTaxRate/exportXlx ExportXlx
        Net--x-KolagaramTaxRateListpage: F : Connection Error
        alt
		note right of Net:  Kolagaram Tax Rate Cache Object Found
        KolagaramTaxRateListpage->>+Cache: S : GET /app/KolagaramTaxRate/exportXlx ExportXlx
        Cache-->>-KolagaramTaxRateListpage: RES: House TaxRate Xlx
        else
		note right of Net:  Kolagaram Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/KolagaramTaxRate/exportXlx ExportXlx
        cloud-->>-KolagaramTaxRateListpage: RES: Kolagaram TaxRate Xlx
        end        
    end
    rect rgb(244,244,244)
        KolagaramTaxRateListpage->>+Net: Check Internet: GET /app/KolagaramTaxRate/exportListXlx ExportListXlx
        Net--x-KolagaramTaxRateListpage: F : Connection Error
        KolagaramTaxRateListpage->>+cloud: S : GET /app/KolagaramTaxRate/exportListXlx ExportListXlx
        cloud-->>-KolagaramTaxRateListpage: RES: Kolagaram TaxRate List Xlx
    end

          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------------|----|
|1.0| Create Form |ut_p_c_GSTS_WEB_KOLAGARAMTAXRATE_120 ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_115 ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_130 |**Positive Test Cases:** 1.Open Kolagaram TaxRate Create Form At panchayat level  **Negative Test Cases:** 1. Open Kolagaram TaxRate Create Form with no panchayat resolution exists 2. Open Kolagaram TaxRate Create Form Without Db connection |-|1|2|3|testPosOpenKolagaramTaxRateCreateFormWithAuthorisedUser,  testNegOpenKolagaramTaxRateCreateFormWithNoPanchayatResolutionExists,  testPosOpenKolagaramTaxRateCreateFormWithoutDBConnection|
|1.0| Create |ut_p_c_GSTS_WEB_KOLAGARAMTAXRATE_150   ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_160 ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_140 ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_270  ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_280 |**Positive Test Cases:** Create Kolagaram TaxRate with valid inputs with Panchayat Level Authorised User **Negative Test Cases:** 1.Create Kolagaram TaxRate with Invalid inputs 2.Create Kolagaram TaxRate without db connection 3.Create Kolagaram TaxRate with Removed Panchayat Resolution Id  4.Create Kolagaram TaxRate with Invalid Panchayat Resolution Id|**panchayatResolutionId:** drop down list **kolgCatType:** enums **taxVal:** 1.null 2. >=1 and <=100|7|8|15|testPosAuthorisedPanchayatLevelUserCreateKolagaramTaxRateWithValidInputs,  testNegAuthorisedPanchayatLevelUserCreateKolagaramTaxRateWithInValidInputs,  testNegCreateKolagaramTaxRateWithoutDBconnection,  testNegCreateKolagaramTaxRateWithRemovedPanchayatResolutionId,  testNegCreateKolagaramTaxRateWithInvalidPanchayatResolutionId|
|1.0| Remove Form |ut_p_r_GSTS_WEB_KOLAGARAMTAXRATE_330   ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_340   ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_350  ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_410|**Positive Test Cases:** Open Kolagaram TaxRate remove form with valid Id with Authorised Panchayat level user    **Negative Test Cases:**  1.Open Kolagaram TaxRate remove Form Without DB Connection 2. Open Kolagaram TaxRate remove Form with Invalid id   3.Open Kolagaram TaxRate remove form with Already removed Kolagaram TaxRate Id with Authorised user|Id|1|3|4|testPosAuthorisedPanLevelUserOpenPanLevelKolagaramTaxRateRemoveFormWithValidId,  testPosAuthorisedPanLevelUserOpenKolagaramTaxRateRemoveFormWithoutDBConnection,  testNegAuthorisedPanLevelUserOpenKolagaramTaxRateRemoveFormWithInValidId,  testNegAuthorisedPanUserOpenKolagaramTaxRateRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_KOLAGARAMTAXRATE_360  ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_370 ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_390  ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_400  ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_420 |**Positive Test Cases:** Remove Kolagaram TaxRate with Valid Remove Comment with Panchayat Level Authorised User **Negative Test Cases:** 1. Removing Kolagaram TaxRate with invalid remove comment 2.Remove Kolagaram TaxRate without db connection 3.Remove already removed Kolagaram TaxRate  4. Remove Kolagaram TaxRate with invalid Id| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|testPosPanLevelAuthorisedUserRemoveKolagaramTaxRateWithValidRemoveCommentAndValidId,  testNegPanLevelAuthorisedUserRemoveKolagaramTaxRateWithInValidRemoveCommentAndValidId,  testNegRemoveKolagaramTaxRateWithoutDbConnection,  testNegAuthorisedUserRemoveAlreadyRemovedKolagaramTaxRate,  testNegPanLevelAuthorisedUserRemoveKolagaramTaxRateWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_KOLAGARAMTAXRATE_530  ut_n_v_GSTS_WEB_KOLAGARAMTAXRATE_540 ut_n_v_GSTS_WEB_KOLAGARAMTAXRATE_550 |**Positive Test Cases:** View Kolagaram TaxRate with Valid Id  with Authorised User **Negative Test Cases:** 1. View Kolagaram TaxRate without db connection  2.View Kolagaram TaxRate with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewKolagaramTaxRateWithValidId,  testPosAuthorisedUserViewKolagaramTaxRateWithoutDbConnection,  testNegAuthorisedUserViewKolagaramTaxRatewithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_KOLAGARAMTAXRATE_680 ut_n_s_GSTS_WEB_KOLAGARAMTAXRATE_690 ut_n_s_GSTS_WEB_KOLAGARAMTAXRATE_700|**Positive Test Cases:** Search Kolagaram TaxRate with valid inputs **Negative Test Cases:** 1.Search Kolagaram TaxRate without db connection 2.Search Kolagaram TaxRate with invalid Inputs|**1.kolgCatType**|1|2|3|testPosAuthorisedUserSearchKolagaramTaxRateWithValidInputs, testNegAuthorisedUserSearchKolagaramTaxRateWithoutDBconnection|
|1.0| List |ut_p_l_GSTS_WEB_KOLAGARAMTAXRATE_610 ut_n_l_GSTS_WEB_KOLAGARAMTAXRATE_620|**Positive Test Cases:** Get Kolagaram TaxRate List with Authorised User **Negative Test Cases:** Get Kolagaram TaxRate List without db connection|Validating with unique field|1|1|2|testPosAuthorisedUserKolagaramTaxRateList,  testNegAuthorisedUserKolagaramTaxRateListWithoutDBconnection,  testNegAuthorisedUserSearchKolagaramTaxRateWithInvalidInputs|
|1.0| PDF |ut_p_ep_GSTS_WEB_KOLAGARAMTAXRATE_760   ut_n_ep_GSTS_WEB_KOLAGARAMTAXRATE_770   ut_n_ep_GSTS_WEB_KOLAGARAMTAXRATE_780 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportKolagaramTaxRatePdfWithValidId,  testNegAuthorisedUserExportKolagaramTaxRatePdfwithoutDbconnection,  testNegAuthorisedUserExportKolagaramTaxRatePdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_KOLAGARAMTAXRATE_790   ut_n_elp_GSTS_WEB_KOLAGARAMTAXRATE_800   ut_n_elp_GSTS_WEB_KOLAGARAMTAXRATE_810 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportKolagaramTaxRateListPdfWithValidId,  testNegAuthorisedUserExportKolagaramTaxRateListPdfwithoutDbconnection,  testNegAuthorisedUserExportKolagaramTaxRateListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_KOLAGARAMTAXRATE_820   ut_n_ex_GSTS_WEB_KOLAGARAMTAXRATE_830   ut_n_ex_GSTS_WEB_KOLAGARAMTAXRATE_840 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportKolagaramTaxRateXlxWithValidId,  testNegAuthorisedUserExportKolagaramTaxRateXlxwithoutDbconnection,  testNegAuthorisedUserExportKolagaramTaxRateXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_KOLAGARAMTAXRATE_850   ut_n_elx_GSTS_WEB_KOLAGARAMTAXRATE_860   ut_n_elx_GSTS_WEB_KOLAGARAMTAXRATE_870 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportKolagaramTaxRateListXlxWithValidId,  testNegAuthorisedUserExportKolagaramTaxRateListXlxwithoutDbconnection,  testNegAuthorisedUserExportKolagaramTaxRateListXlxInValidId|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------------|-----|
|1.0| Create Form|ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_260|Unauthorised User opening Kolagaram TaxRate create form||0|1|1|testNegUnAuthorisedUserOpenKolagaramTaxRateCreateForm|
|1.0| Create |ut_N_c_GSTS_WEB_KOLAGARAMTAXRATE_250 |Unauthorised User does not have permission to create|**panchayatResolutionId:** drop down list **kolgCatType:** enums **taxVal:** 1.null 2. >=1 and <=100|0|1|1|testNegUnAuthorisedUserCreateKolagaramTaxRate|
|1.0| Remove Form|ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_510|Unauthorised User opening Kolagaram TaxRate remove form||0|1|1|testNegUnAuthorisedPanLevelUserOpenKolagaramTaxRateRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_520|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserRemoveKolagaramTaxRate|
|1.0| View |ut_n_v_GSTS_WEB_KOLAGARAMTAXRATE_600|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewKolagaramTaxRate|
|1.0| Search |ut_n_s_GSTS_WEB_KOLAGARAMTAXRATE_750|Unauthorised User does not have permission to search|**1.kolgCatType**|0|1|1|testNegUnAuthorisedUserSearchKolagaramTaxRate|
|1.0| List |ut_n_l_GSTS_WEB_KOLAGARAMTAXRATE_670|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserKolagaramTaxRateList|
|1.0| PDF |ut_n_ep_GSTS_WEB_KOLAGARAMTAXRATE_920 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportKolagaramTaxRatePdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_KOLAGARAMTAXRATE_930 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportKolagaramTaxRateListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_KOLAGARAMTAXRATE_940 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportKolagaramTaxRateXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_KOLAGARAMTAXRATE_950 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportKolagaramTaxRateListXlxWithValidId|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|------------|
|1.0|Create|ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_170|Create Kolagaram TaxRate at State Level| N/A |Will not be Created|1|testNegCreateKolagaramTaxRateAtStateLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_180|Open Kolagaram TaxRate Create Form at State Level| N/A |Will not be Opened|1|testNegOpenKolagaramTaxRateCreateFormAtStateLevel|
|1.0|Create|ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_190|Create Kolagaram TaxRate at District Level| N/A |Will not be Created|1|testNegCreateKolagaramTaxRateAtDistLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_200|Open Kolagaram TaxRate Create Form at District Level| N/A |Will not be Opened|1|testNegOpenKolagaramTaxRateCreateFormAtDistLevel|
|1.0|Create|ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_210|Create Kolagaram TaxRate at Division Level| N/A |Will not be Created|1|testNegCreateKolagaramTaxRateAtDivLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_220|Open Kolagaram TaxRate Create Form at Division Level| N/A |Will not be Opened|1|testNegOpenKolagaramTaxRateCreateFormAtDivLevel|
|1.0|Create|ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_230|Create Kolagaram TaxRate at Mandal Level| N/A |Will not be Created|1|testNegCreateKolagaramTaxRateAtMandalLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_240|Open Kolagaram TaxRate Create Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenKolagaramTaxRateCreateFormAtMandalLevel|
1.0|Create|ut_n_c_GSTS_WEB_KOLAGARAMTAXRATE_290|Create Kolagaram TaxRate in panchayat1112 with panchayat1111 Panchayat Resolution Id| N/A |Will not be Created|1|testNegCreateKolagaramTaxRateInpanchayat1112WithPanchayat1111PanchayatResolutionId|
|1.0|Remove Form|ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_430|Open Kolagaram TaxRate Remove Form at State Level| N/A |Will not be Opened|1|testNegOpenKolagaramTaxRateRemoveFormAtStateLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_440|Remove Kolagaram TaxRate at State Level| N/A |Will not be Removed|1|testNegRemoveKolagaramTaxRateAtStateLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_450|Open Kolagaram TaxRate Remove Form at District Level| N/A |Will not be Opened|1|testNegOpenKolagaramTaxRateRemoveFormAtDistLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_460|Remove Kolagaram TaxRate at District Level| N/A |Will not be Removed|1|testNegRemoveKolagaramTaxRateAtDistLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_470|Open Kolagaram TaxRate Remove Form at Division Level| N/A |Will not be Opened|1|testNegOpenKolagaramTaxRateRemoveFormAtDivLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_480|Remove Kolagaram TaxRate at Division Level| N/A |Will not be Removed|1|testNegRemoveKolagaramTaxRateAtDivLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_490|Open Kolagaram TaxRate Remove Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenKolagaramTaxRateRemoveFormAtMandalLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_500|Remove Kolagaram TaxRate at Mandal Level| N/A |Will not be Removed|1|testNegRemoveKolagaramTaxRateAtMandalLevel|
|1.0|View|ut_n_v_GSTS_WEB_KOLAGARAMTAXRATE_560|View Kolagaram TaxRate at State Level| N/A |Will not be Accessed|1|testNegViewKolagaramTaxRateAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_KOLAGARAMTAXRATE_570|View Kolagaram TaxRate at District Level| N/A |Will not be Accessed|1|testNegViewKolagaramTaxRateAtDistLevel|
|1.0|View|ut_n_v_GSTS_WEB_KOLAGARAMTAXRATE_580|View Kolagaram TaxRate at Division Level| N/A |Will not be Accessed|1|testNegViewKolagaramTaxRateAtDivLevel|
|1.0|View|ut_n_v_GSTS_WEB_KOLAGARAMTAXRATE_590|View Kolagaram TaxRate at Mandal Level| N/A |Will not be Accessed|1|testNegViewKolagaramTaxRateAtMandalLevel|
|1.0|List|ut_n_l_GSTS_WEB_KOLAGARAMTAXRATE_630|Get Kolagaram TaxRate List at State Level| N/A |Will not be Accessed|1|testNegKolagaramTaxRateListAtStateLevel|
|1.0|List|ut_n_l_GSTS_WEB_KOLAGARAMTAXRATE_640|Get Kolagaram TaxRate List at District Level| N/A |Will not be Accessed|1|testNegKolagaramTaxRateListAtDistLevel|
|1.0|List|ut_n_l_GSTS_WEB_KOLAGARAMTAXRATE_650|Get Kolagaram TaxRate List at Division Level| N/A |Will not be Accessed|1|testNegKolagaramTaxRateListAtDivLevel|
|1.0|List|ut_n_l_GSTS_WEB_KOLAGARAMTAXRATE_660|Get Kolagaram TaxRate List at Mandal Level| N/A |Will not be Accessed|1|testNegKolagaramTaxRateListAtMandalLevel|
|1.0|Search|ut_n_s_GSTS_WEB_KOLAGARAMTAXRATE_710|Search Kolagaram TaxRate  at State Level| N/A |Will not be Accessed|1|testNegSearchKolagaramTaxRateAtStateLevel|
|1.0|Search|ut_n_s_GSTS_WEB_KOLAGARAMTAXRATE_720|Search Kolagaram TaxRate  at District Level| N/A |Will not be Accessed|1|testNegSearchKolagaramTaxRateAtDistLevel|
|1.0|Search|ut_n_s_GSTS_WEB_KOLAGARAMTAXRATE_730|Search Kolagaram TaxRate  at Division Level| N/A |Will not be Accessed|1|testNegSearchKolagaramTaxRateAtDivLevel|
|1.0|Search|ut_n_s_GSTS_WEB_KOLAGARAMTAXRATE_740|Search Kolagaram TaxRate  at Mandal Level| N/A |Will not be Accessed|1|testNegSearchKolagaramTaxRateAtMandalLevel|
|1.0|Pdf|ut_n_p_GSTS_WEB_KOLAGARAMTAXRATE_880|Export Kolagaram TaxRate Pdf at State Level| N/A |Will not be exported|1|testNegExportKolagaramTaxRatePdfAtStateLevel|
|1.0|List Pdf|ut_n_p_GSTS_WEB_KOLAGARAMTAXRATE_890|Export Kolagaram TaxRate List Pdf at State Level| N/A |Will not be exported|1|testNegExportKolagaramTaxRateListPdfAtStateLevel|
|1.0|Xlx|ut_n_p_GSTS_WEB_KOLAGARAMTAXRATE_900|Export Kolagaram TaxRate Xlx at State Level| N/A |Will not be exported|1|testNegExportKolagaramTaxRateXlxAtStateLevel|
|1.0|List Xlx|ut_n_p_GSTS_WEB_KOLAGARAMTAXRATE_910|Export Kolagaram TaxRate List Xlx at State Level| N/A |Will not be exported|1|testNegExportKolagaramTaxRateListXlxAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_KOLAGARAMTAXRATE_960|Panchayat1112 user trying to access Panchayat1111 Kolagaram TaxRate which does not belongs to his context| N/A |Will not be accessed|1|testNegPanchayat1112UserAccessingPanchayat1111KolagaramTaxRate|
|1.0|Remove|ut_n_r_GSTS_WEB_KOLAGARAMTAXRATE_965|Panchayat1112 user trying to remove Panchayat1111 Kolagaram TaxRate which does not belongs to his context| N/A |Will not be removed|1|testNegPanchayat1112UserRemovingPanchayat1111KolagaramTaxRate|


## Security compliance check
1. Only user having the permission **ROLE_KOLAGARAM_TAX_RATE_VIEW** should view this functionality 
1. Only user having the permission **ROLE_KOLAGARAM_TAX_RATE_CREATE** should create this functionality 
1. Only user having the permission **ROLE_KOLAGARAM_TAX_RATE_REMOVE** should remove this functionality 
1. Only user having the permission **ROLE_KOLAGARAM_TAX_RATE_VIEW** should export this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Kolagaram Tax Rate in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
