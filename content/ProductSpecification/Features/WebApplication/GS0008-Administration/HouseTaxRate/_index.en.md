---
title: House Tax Rate
tags : ["Composing"]
---

## Introduction
House Tax Rate is one of the features of this software product. House tax rate is a tax rate defined for houses in panchayat. House tax rate depends upon panchayat resolution. House tax rate includes GOVT Land Value per SFT (RS), Residential House Tax Value (%), Commercial House Tax Value (%), Residential Water Tap Service (RS), Commercial Water Tap Service (RS), Public Water Service Tax (%), Public Drainage Service Tax(%), Public Library Service Cess (%), Public Street Light Service Tax (%). It may vary from one panchayat to other panchayat and also from one block from one block in same panchayat. Users will have access to house tax rates if they have permission, Otherwise will not access.

## Business Assumptions
What type of users can create house tax rate should be planned at design phase.

## Requirements
### Functional Requirements
1. Users of all levels can create, remove, view and export the house tax rate.  
1. We can create and remove house tax rate at panchayat level only.
1. House Tax Rate feature is accessible at panchayat level only.
1. Panchayat Resolution is required to create a house tax rate.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access house tax rates.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
House tax rate feature contains information about different house tax rates of panchayat.

### Design 
1. Each house tax rate has Panchayat Resolution, GOVT Land Value per SFT (RS), Residential House Tax Value (%), Commercial House Tax Value (%),
 Residential Water Tap Service (RS), Commercial Water Tap Service (RS), Public Water Service Tax (%), Public Drainage Service Tax(%), Public Library Service Cess (%), Public Street Light Service Tax (%), Start Block, and End Block.
1. Each house tax rate in same panchayat has unique panchayat resolution.
1. We can create, remove, view and export the house tax rate.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_house_tax_rate_list|To view all the house tax rates. This listing page should bind to a permission|
|uc_house_tax_rate_create|To create the house tax rate. This create page should bind to a permission|
|uc_house_tax_rate_remove|To remove the house tax rate. This remove page should bind to a permission|
|uc_house_tax_rate_view|To view the house tax rate. This view page should bind to a permission|
|uc_house_tax_rate_search|To search the house tax rate. This search page should bind to a permission|
|uc_house_tax_rate_export|To export the house tax rate in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|panchayatResolution|YES|NA|Dropdown values|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "pr_id", nullable = false)|pr_id varchar(32) NOT NULL|YES|YES|YES|YES|NO||
|landGovtVal|YES|NA|0-9 and ., maxlen=10|@Column(name = "land_govt_val", nullable = false)|land_govt_val float(9,2) NOT NULL|YES|YES|YES|YES|NO||
|residentialHouseVal|YES|NA|0-9 and ., maxlen=10|@Column(name = "residential_house_val", nullable = false)|residential_house_val float(9,2) NOT NULL|YES|YES|YES|YES|NO||
|commercialHouseVal|YES|NA|0-9 and ., maxlen=5|@Column(name = "commercial_house_val", nullable = false)|commercial_house_val float(9,2) NOT NULL|YES|YES|YES|NO|NO||
|residentialWaterVal|YES|NA|0-9 and ., maxlen=7|@Column(name = "residential_water_val", nullable = false)|residential_water_val float(9,2) NOT NULL|YES|YES|YES|NO|NO||
|commercialWaterVal|YES|NA|0-9 and ., maxlen=7|@Column(name = "commercial_water_val", nullable = false)|commercial_water_val float(9,2) NOT NULL|YES|YES|YES|NO|NO||
|waterServiceVal|YES|NA|0-9 and ., maxlen=6|@Column(name = "water_service_val", nullable = false)|water_service_val float(9,2) NOT NULL|YES|YES|YES|NO|NO||
|drainageServiceVal|YES|NA|0-9 and ., maxlen=6|@Column(name = "drainage_service_val", nullable = false)|drainage_service_val float(9,2) NOT NULL|YES|YES|YES|NO|NO||
|libraryCessVal|YES|NA|0-9 and ., maxlen=6|@Column(name = "library_cess_val", nullable = false)|library_cess_val float(9,2) NOT NULL|YES|YES|YES|NO|NO||
|lightServiceVal|YES|NA|0-9 and ., maxlen=6|@Column(name = "light_service_val", nullable = false)|light_service_val float(9,2) NOT NULL|YES|YES|YES|NO|NO||
|startBlock|YES|NA|Dropdown values|@Column(name = "start_block", nullable = false)|start_block bigint(20) NOT NULL|YES|YES|YES|NO|NO||
|endBlock|YES|NA|Dropdown values|@Column(name = "end_block", nullable = false)|end_block bigint(20) NOT NULL|YES|YES|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS
No Enum Constants in house tax rate.

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|HOUSE_TAX_RATE_VIEW|View|
|HOUSE_TAX_RATE_CREATE|Create|
|HOUSE_TAX_RATE_REMOVE|Remove|
|HOUSE_TAX_RATE_VIEW|Export|
|HOUSE_TAX_RATE_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_house_tax_rate__prid__org_panchayat_id (pr_id, org_panchayat_id)|
|Foreign Key|fk__gs_house_tax_rate__pr_id (pr_id) REFERENCES gs_pr (id)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_HOUSE_TAX_RATE_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_HOUSE_TAX_RATE_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_HOUSE_TAX_RATE_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_HOUSE_TAX_RATE_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

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
	HouseTaxRateMenu((House Tax Rate Menu))
	ListPage{House Tax Rate List Page}
	CreatePage((Create Page))
	RemovePage((Remove Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->HouseTaxRateMenu
    subgraph Menu
    HouseTaxRateMenu
    end
    subgraph   
    HouseTaxRateMenu-->ListPage
    ListPage--C-R-V-E-->ListPage
    end
    subgraph  
    HouseTaxRateMenu--F-->ErrorPage
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
1. Only a user with the HOUSE_TAX_RATE_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant HouseTaxRateListpage as Browser
    participant Net as Browser Net Tools
    participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        HouseTaxRateListpage->>+Net: Check Internet, GET /app/ctx/HouseTaxRate/list ListPage
        Net--x-HouseTaxRateListpage: F : Connection Error
        HouseTaxRateListpage->>+cloud: S:  GET /app/ctx/HouseTaxRate/list ListPage
        cloud-->>-HouseTaxRateListpage: RES:List Page
    end
    rect rgb(244,244,244)
        HouseTaxRateListpage->>+Net: Check Internet, GET /app/HouseTaxRate/create/form CreateFormPage
        Net--x-HouseTaxRateListpage: F : Connection Error
        HouseTaxRateListpage->>+cloud: S : GET /app/HouseTaxRate/create/form CreateFormPage
        cloud-->>-HouseTaxRateListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        HouseTaxRateListpage->>+Net: Check Internet: POST /app/HouseTaxRate/create Create
        Net--x-HouseTaxRateListpage: F : Connection Error
        HouseTaxRateListpage->>+cloud: S : POST /app/HouseTaxRate/create Create
        cloud-->>-HouseTaxRateListpage: RES: An House TaxRate Successfully Created
    end
    rect rgb(244,244,244)
        HouseTaxRateListpage->>+Net: Check Internet: GET /app/HouseTaxRate/remove/form RemoveFormPage
        Net--x-HouseTaxRateListpage: F : Connection Error
        HouseTaxRateListpage->>+cloud: S : GET /app/HouseTaxRate/remove/form RemoveFormPage
        cloud-->>-HouseTaxRateListpage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        HouseTaxRateListpage->>+Net: Check Internet: POST /app/HouseTaxRate/remove Remove
        Net--x-HouseTaxRateListpage: F : Connection Error
        HouseTaxRateListpage->>+cloud: S : POST /app/HouseTaxRate/remove Remove
        cloud-->>-HouseTaxRateListpage: RES: An House TaxRate Successfully Removed
    end
    rect rgb(244,244,244)
        HouseTaxRateListpage->>+Net: Check Internet: GET /app/HouseTaxRate/view ViewPage
        Net--x-HouseTaxRateListpage: F : Connection Error
        alt
		note right of Net:  House Tax Rate Cache Object Found
        HouseTaxRateListpage->>+Cache: S : GET /app/HouseTaxRate/view ViewPage
        Cache-->>-HouseTaxRateListpage: RES: House TaxRate View
        else
		note right of Net:  House Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/HouseTaxRate/view ViewPage
        cloud-->>-HouseTaxRateListpage: RES: House TaxRate View
        end
    end
    rect rgb(244,244,244)
        HouseTaxRateListpage->>+Net: Check Internet: GET /app/HouseTaxRate/exportPdf ExportPdf
        Net--x-HouseTaxRateListpage: F : Connection Error         
        alt
		note right of Net:  House Tax Rate Cache Object Found
        HouseTaxRateListpage->>+Cache: S : GET /app/HouseTaxRate/exportPdf ExportPdf
        Cache-->>-HouseTaxRateListpage: RES: House TaxRate Pdf
        else
		note right of Net:  House Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/HouseTaxRate/exportPdf ExportPdf
        cloud-->>-HouseTaxRateListpage: RES: House TaxRate Pdf
        end
    end
    rect rgb(244,244,244)
        HouseTaxRateListpage->>+Net: Check Internet: GET /app/HouseTaxRate/exportListPdf ExportListPdf
        Net--x-HouseTaxRateListpage: F : Connection Error
        HouseTaxRateListpage->>+cloud: S : GET /app/HouseTaxRate/exportListPdf ExportListPdf
        cloud-->>-HouseTaxRateListpage: RES: House TaxRate List Pdf
    end
    rect rgb(244,244,244)
        HouseTaxRateListpage->>+Net: Check Internet: GET /app/HouseTaxRate/exportXlx ExportXlx
        Net--x-HouseTaxRateListpage: F : Connection Error
        alt
		note right of Net:  House Tax Rate Cache Object Found
        HouseTaxRateListpage->>+Cache: S : GET /app/HouseTaxRate/exportXlx ExportXlx
        Cache-->>-HouseTaxRateListpage: RES: House TaxRate Xlx
        else
		note right of Net:  House Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/HouseTaxRate/exportXlx ExportXlx
        cloud-->>-HouseTaxRateListpage: RES: House TaxRate Xlx
        end
    end
    rect rgb(244,244,244)
        HouseTaxRateListpage->>+Net: Check Internet: GET /app/HouseTaxRate/exportListXlx ExportListXlx
        Net--x-HouseTaxRateListpage: F : Connection Error
        HouseTaxRateListpage->>+cloud: S : GET /app/HouseTaxRate/exportListXlx ExportListXlx
        cloud-->>-HouseTaxRateListpage: RES: House TaxRate List Xlx
    end

          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count| Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_WEB_HOUSETAXRATE_200  ut_n_c_GSTS_WEB_HOUSETAXRATE_201 ut_n_c_GSTS_WEB_HOUSETAXRATE_211 ut_n_c_GSTS_WEB_HOUSETAXRATE_212 |**Positive Test Cases:** Creating House TaxRate  with Authorised User **Negative Test Cases:** 1.Creating House TaxRate with Invalid Inputs and without DB Connection 2.Creating HouseTaxRate with Empy Panchayat Resolution Id|**panchayatResolutionId:** drop down list **landGovtVal:** 1.value>1 and value<1000000  2.null **residentialHouseVal:** 1.value>0.10 and value<10.0 2.null**commercialHouseVal:** 1.value>0.10 and value<10.0 2.null **residentialWaterVal:** 1.value>=0 and value<10000 2.null **commercialWaterVal:** 1.value>=0 and value<10000 2.null **waterServiceVal:** 1.value>=0 and value<100 2.null **drainageServiceVal:** 1.value>=0 and value<100 2.null **libraryCessVal:** 1.value>=0 and value<100 2.null **lightServiceVal:** 1.value>=0 and value<100 2.null **startBlock:** 1.value>=1 and value<=99 2.null **endBlock:** 1.value>=1 and value<=99 2.null |2|5|7| testAuthorisedUserCreateHouseTaxRate, testAuthorisedUserCreateHouseTaxRateNegativeTestCase, testAuthorisedUserCreateHouseTaxRateWithoutDBConnection, testAuthorisedUserCreateHouseTaxRateWithInvalidPRId|
|1.0| Create Form |ut_p_c_GSTS_WEB_HOUSETAXRATE_207 ut_n_c_GSTS_WEB_HOUSETAXRATE_209 |**Positive Test Cases:** Open House TaxRate Create Form with Authorised User **Negative Test Cases:** Open House TaxRate Create Form without DB Connection|Id |1|1|2|testAuthorisedUserOpenHouseTaxRateCreateForm, testAuthorisedUserOpenHouseTaxRateCreateFormWithoutDBConnection, testAuthorisedUserOpenHouseTaxRateCreateFormWithDifferentPanchayat|
|1.0| Remove |ut_p_r_GSTS_WEB_HOUSETAXRATE_306  ut_n_r_GSTS_WEB_HOUSETAXRATE_304 ut_n_r_GSTS_WEB_HOUSETAXRATE_305 ut_n_r_GSTS_WEB_HOUSETAXRATE_307 ut_n_r_GSTS_WEB_HOUSETAXRATE_309 |**Positive Test Cases:** Removing House TaxRate  with Authorised User **Negative Test Cases:** Removing House TaxRate with Invalid Inputs and without DB Connection| **removeComment:** 1.valid characters 2.length>=6 and length<=256 3.null |1|4|5|testAuthorisedUserRemoveHouseTaxRate, testAuthorisedUserRemoveHouseTaxRateWithInvalidId, testAuthorisedUserRemoveHouseTaxRateWithoutDBConnection, testAuthorisedUserRemoveHouseTaxRateNegativeTestCase, testAuthorisedUserRemoveHouseTaxRateWithInvalidIdAndComment|
|1.0| Remove Form |ut_p_r_GSTS_WEB_HOUSETAXRATE_300 ut_n_r_GSTS_WEB_HOUSETAXRATE_301 ut_n_r_GSTS_WEB_HOUSETAXRATE_303 |**Positive Test Cases:** Open House TaxRate Remove Form with Authorised User **Negative Test Cases:** Open House TaxRate Create Form with Invalid id and Without DB Connection|Id |1|2|3|testAuthorisedUserOpenHouseTaxRateRemoveForm, testAuthorisedUserOpenHouseTaxRateRemoveFormWithInvalidId, testAuthorisedUserOpenHouseTaxRateRemoveFormWithoutDBConnection|
|1.0| View |ut_p_v_GSTS_WEB_HOUSETAXRATE_400 ut_n_v_GSTS_WEB_HOUSETAXRATE_401 |**Positive Test Cases:** View House Tax Rate with Valid Id  with Authorised User**Negative Test Cases:** View House tax Rate with Invalid ID  with Authorised User|1.Valid Id 2.Invalid Id|1|1|2|testAuthorisedUserViewHouseTaxRate, testAuthorisedUserViewHouseTaxRateNetgativeTestCase|
|1.0| Search |ut_p_s_GSTS_WEB_HOUSETAXRATE_500 ut_n_s_GSTS_WEB_HOUSETAXRATE_502 ut_n_s_GSTS_WEB_HOUSETAXRATE_503 |**Positive Test Cases:** Search House Tax Rate with Authorised User **Negative Test Cases:** Search House Tax Rate without DB Connection | **objStateSet:** Enum Values|1|2|3| testAuthorisedUserSearchHouseTaxRate, testAuthorisedUserSearchHouseTaxRateWithoutDBConnection, testAuthorisedUserSearchHouseTaxNegativeCase|
|1.0| List |ut_p_l_GSTS_WEB_HOUSETAXRATE_600 ut_n_l_GSTS_WEB_HOUSETAXRATE_601 ut_n_l_GSTS_WEB_HOUSETAXRATE_603 |**Positive Test Cases:** Check the object list with valid data  with Authorised User **Negative Test Cases:** Check the object list with Invalid data  with Authorised User|Validating with the field|1|2|3|testAuthorisedUserListHouseTaxRate, testAuthorisedUserListHouseTaxRateNegativeTestCase, testAuthorisedUserListHouseTaxRateWithoutDBConnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_HOUSETAXRATE_800 ut_n_ep_GSTS_WEB_HOUSETAXRATE_804 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** Export Pdf with Invalid Id and Without DB Connection|Id |1|1|2|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_HOUSETAXRATE_801 ut_n_elp_GSTS_WEB_HOUSETAXRATE_805 ut_n_elp_GSTS_WEB_HOUSETAXRATE_812 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_HOUSETAXRATE_802 ut_n_ex_GSTS_WEB_HOUSETAXRATE_806 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|1|2|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_HOUSETAXRATE_803 ut_n_elx_GSTS_WEB_HOUSETAXRATE_807 ut_n_elx_GSTS_WEB_HOUSETAXRATE_813 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### UnAuthorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count| Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|-----|
|1.0| Create |ut_n_c_GSTS_WEB_HOUSETAXRATE_204 |Unauthorised User does not have permission to create|**panchayatResolutionId:** drop down list **landGovtVal:** 1.value>1 and value<1000000  2.null **residentialHouseVal:** 1.value>0.10 and value<10.0 2.null**commercialHouseVal:** 1.value>0.10 and value<10.0 2.null **residentialWaterVal:** 1.value>=0 and value<10000 2.null **commercialWaterVal:** 1.value>=0 and value<10000 2.null **waterServiceVal:** 1.value>=0 and value<100 2.null **drainageServiceVal:** 1.value>=0 and value<100 2.null **libraryCessVal:** 1.value>=0 and value<100 2.null **lightServiceVal:** 1.value>=0 and value<100 2.null **startBlock:** 1.value>=1 and value<=99 2.null **endBlock:** 1.value>=1 and value<=99 2.null |1|N/A|1|testUnAuthorisedUserCreateHouseTaxRate|
|1.0| Create Form |ut_n_c_GSTS_WEB_HOUSETAXRATE_208 |Unauthorised User does not have permission to open create form|Id |1|0|1|testUnAuthorisedUserOpenHouseTaxRateCreateForm|
|1.0| Remove |ut_n_r_GSTS_WEB_HOUSETAXRATE_308 |Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2.length>=6 and length<=256 3.null |1|N/A|1|testUnAuthorisedUserRemoveHouseTaxRate|
|1.0| Remove Form |ut_n_r_GSTS_WEB_HOUSETAXRATE_302 |Unauthorised User does not have permission to open remove form|Id |1|0|1|testUnAuthorisedUserOpenHouseTaxRateRemoveForm|
|1.0| View |ut_n_v_GSTS_WEB_HOUSETAXRATE_402 |Unauthorised User does not have permission to view|1.Valid Id |1|N/A|1|testUnAuthorisedUserViewHouseTaxRate|
|1.0| Search |ut_n_s_GSTS_WEB_HOUSETAXRATE_501 |Unauthorised User does not have permission to search | **objStateSet:** Enum Values|1|N/A|1| testUnAuthorisedUserSearchHouseTaxRateNegativetestCase|
|1.0| List |ut_n_l_GSTS_WEB_HOUSETAXRATE_602 |Unauthorised User does not have permission to view the list of house tax rates|Validating with the field|1|N/A|1|testUnAuthorisedUserListHouseTaxRate|
|1.0| PDF |ut_n_ep_GSTS_WEB_HOUSETAXRATE_810 |Export List Pdf with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_HOUSETAXRATE_808 |Export Pdf with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_HOUSETAXRATE_811 |Export XLX with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_HOUSETAXRATE_809 |Export List XLX with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportListXlx|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|------------|
|1.0|Create|ut_n_c_GSTS_WEB_HOUSETAXRATE_700|Create House TaxRate with different Panchayat Context Panchayat Resolution| N/A |Able to set different panchayat context -panchayat resolution to house tax rate creation in testing but it is not allowing in Web|1|testAuthorisedUserCreateHouseTaxRateWithDifferentPanchayatContextPanchayatResolution|
|1.0|View|ut_n_c_GSTS_WEB_HOUSETAXRATE_701|View House TaxRate At different Panchayat | Id |SecurityUnAuthorisedExcepion will be thrown|1| testAuthorisedUserViewHouseTaxRateAtDifferentPanchayat|

## Security compliance check
1. Only user having the permission **ROLE_HOUSE_TAX_RATE_VIEW** should view this functionality 
1. Only user having the permission **ROLE_HOUSE_TAX_RATE_CREATE** should create this functionality 
1. Only user having the permission **ROLE_HOUSE_TAX_RATE_REMOVE** should remove this functionality 
1. Only user having the permission **ROLE_HOUSE_TAX_RATE_VIEW** should export this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the House Tax Rate in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
