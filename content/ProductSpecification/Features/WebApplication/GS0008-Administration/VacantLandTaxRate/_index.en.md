---
title: Vacant Land Tax Rate
tags : ["Composing"]
---

## Introduction
Vacant Land Tax Rate is one of the features of this software product. Vacant land tax rate is a tax rate defined for vacant land properties. It depends upon panchayat resolution. It may vary from one panchayat to other panchayat. Users will have access to vacant land tax rates if they have permission, Otherwise will not access.

## Business Assumptions
What type of users can create vacant land tax rate should be planned at design phase.

## Requirements
### Functional Requirements
1. Users of all levels can create, remove, view and export the vacant land tax rate.  
1. We can create and remove vacant land tax rate at panchayat level only.
1. Vacant Land Tax Rate feature is accessible at panchayat level only.
1. Panchayat Resolution is required to create a vacant land tax rate.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access vacant land tax rates.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Vacant land tax rate feature contains information about different vacant land tax rates of panchayat.

### Design 
1. Each vacant land tax rate has Panchayat Resolution, and Tax Value (%).
1. Each vacant land tax rate in same panchayat has unique panchayat resolution.
1. We can create, remove, view and export the vacant land tax rate.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_vacant_land_tax_rate_list|To view all the vacant land tax rates. This listing page should bind to a permission|
|uc_vacant_land_tax_rate_create|To create the vacant land tax rate. This create page should bind to a permission|
|uc_vacant_land_tax_rate_remove|To remove the vacant land tax rate. This remove page should bind to a permission|
|uc_vacant_land_tax_rate_view|To view the vacant land tax rate. This view page should bind to a permission|
|uc_vacant_land_tax_rate_search|To search the vacant land tax rate. This search page should bind to a permission|
|uc_vacant_land_tax_rate_export|To export the vacant land tax rate in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|panchayatResolution|YES|NA|Dropdown values|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "pr_id", nullable = false)|pr_id varchar(32) NOT NULL|YES|YES|YES|YES|NO||
|taxVal|YES|NA|0-9 and ., maxlen=6|@Column(name = "tax_val", nullable = false)|tax_val float(9,2) NOT NULL|YES|YES|YES|YES|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS
No Enum Constants in vacant land tax rate.

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|VACANT_LAND_TAX_RATE_VIEW|View|
|VACANT_LAND_TAX_RATE_CREATE|Create|
|VACANT_LAND_TAX_RATE_REMOVE|Remove|
|VACANT_LAND_TAX_RATE_VIEW|Export|
|VACANT_LAND_TAX_RATE_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_vacant_land_tax_rate__prid__org_panchayat_id (pr_id, org_panchayat_id)|
|Foreign Key|fk__gs_vacant_land_tax_rate__pr_id (pr_id) REFERENCES gs_pr (id)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_VACANT_LAND_TAX_RATE_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_VACANT_LAND_TAX_RATE_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_VACANT_LAND_TAX_RATE_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_VACANT_LAND_TAX_RATE_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

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
	VacantLandTaxRateMenu((Vacant Land Tax Rate Menu))
	ListPage{Vacant Land Tax Rate List Page}
	CreatePage((Create Page))
	RemovePage((Remove Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->VacantLandTaxRateMenu
    subgraph Menu
    VacantLandTaxRateMenu
    end
    subgraph   
    VacantLandTaxRateMenu-->ListPage
    ListPage--C-R-V-E-->ListPage
    end
    subgraph  
    VacantLandTaxRateMenu--F-->ErrorPage
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
1. Only a user with the VACANT_LAND_TAX_RATE_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant VacantLandTaxRateListpage as Browser
    participant Net as Browser Net Tools
    participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        VacantLandTaxRateListpage->>+Net: Check Internet, GET /app/ctx/VacantLandTaxRate/list ListPage
        Net--x-VacantLandTaxRateListpage: F : Connection Error
        VacantLandTaxRateListpage->>+cloud: S:  GET /app/ctx/VacantLandTaxRate/list ListPage
        cloud-->>-VacantLandTaxRateListpage: RES:List Page
    end
    rect rgb(244,244,244)
        VacantLandTaxRateListpage->>+Net: Check Internet, GET /app/VacantLandTaxRate/create/form CreateFormPage
        Net--x-VacantLandTaxRateListpage: F : Connection Error
        VacantLandTaxRateListpage->>+cloud: S : GET /app/VacantLandTaxRate/create/form CreateFormPage
        cloud-->>-VacantLandTaxRateListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        VacantLandTaxRateListpage->>+Net: Check Internet: POST /app/VacantLandTaxRate/create Create
        Net--x-VacantLandTaxRateListpage: F : Connection Error
        VacantLandTaxRateListpage->>+cloud: S : POST /app/VacantLandTaxRate/create Create
        cloud-->>-VacantLandTaxRateListpage: RES: An Vacant Land Tax Rate Successfully Created
    end
    rect rgb(244,244,244)
        VacantLandTaxRateListpage->>+Net: Check Internet: GET /app/VacantLandTaxRate/remove/form RemoveFormPage
        Net--x-VacantLandTaxRateListpage: F : Connection Error
        VacantLandTaxRateListpage->>+cloud: S : GET /app/VacantLandTaxRate/remove/form RemoveFormPage
        cloud-->>-VacantLandTaxRateListpage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        VacantLandTaxRateListpage->>+Net: Check Internet: POST /app/VacantLandTaxRate/remove Remove
        Net--x-VacantLandTaxRateListpage: F : Connection Error
        VacantLandTaxRateListpage->>+cloud: S : POST /app/VacantLandTaxRate/remove Remove
        cloud-->>-VacantLandTaxRateListpage: RES: An Vacant Land Tax Rate Successfully Removed
    end
    rect rgb(244,244,244)
        VacantLandTaxRateListpage->>+Net: Check Internet: GET /app/VacantLandTaxRate/view ViewPage
        Net--x-VacantLandTaxRateListpage: F : Connection Error
        alt
		note right of Net:  Vacant Land Tax Rate Cache Object Found
        VacantLandTaxRateListpage->>+Cache: S : GET /app/VacantLandTaxRate/view ViewPage
        Cache-->>-VacantLandTaxRateListpage: RES: Vacant Land Tax Rate View
        else
		note right of Net:  Vacant Land Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/VacantLandTaxRate/view ViewPage
        cloud-->>-VacantLandTaxRateListpage: RES: Vacant Land Tax Rate View
        end
    end
    rect rgb(244,244,244)
        VacantLandTaxRateListpage->>+Net: Check Internet: GET /app/VacantLandTaxRate/exportPdf ExportPdf
        Net--x-VacantLandTaxRateListpage: F : Connection Error 
        alt
		note right of Net:  Vacant Land Tax Rate Cache Object Found
        VacantLandTaxRateListpage->>+Cache: S : GET /app/VacantLandTaxRate/exportPdf ExportPdf
        Cache-->>-VacantLandTaxRateListpage: RES: Vacant Land Tax Rate Pdf
        else
		note right of Net:  House Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/VacantLandTaxRate/exportPdf ExportPdf
        cloud-->>-VacantLandTaxRateListpage: RES: Vacant Land Tax Rate Pdf
        end
    end
    rect rgb(244,244,244)
        VacantLandTaxRateListpage->>+Net: Check Internet: GET /app/VacantLandTaxRate/exportListPdf ExportListPdf
        Net--x-VacantLandTaxRateListpage: F : Connection Error
        VacantLandTaxRateListpage->>+cloud: S : GET /app/VacantLandTaxRate/exportListPdf ExportListPdf
        cloud-->>-VacantLandTaxRateListpage: RES: Vacant Land Tax Rate List Pdf
    end
    rect rgb(244,244,244)
        VacantLandTaxRateListpage->>+Net: Check Internet: GET /app/VacantLandTaxRate/exportXlx ExportXlx
        Net--x-VacantLandTaxRateListpage: F : Connection Error
        alt
		note right of Net:  Vacant Land Tax Rate Cache Object Found
        VacantLandTaxRateListpage->>+Cache: S : GET /app/VacantLandTaxRate/exportXlx ExportXlx
        Cache-->>-VacantLandTaxRateListpage: RES: Vacant Land Tax Rate Xlx
        else
		note right of Net:  Vacant Land Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/VacantLandTaxRate/exportXlx ExportXlx
        cloud-->>-VacantLandTaxRateListpage: RES: Vacant Land Tax Rate Xlx
        end
    end
    rect rgb(244,244,244)
        VacantLandTaxRateListpage->>+Net: Check Internet: GET /app/VacantLandTaxRate/exportListXlx ExportListXlx
        Net--x-VacantLandTaxRateListpage: F : Connection Error
        VacantLandTaxRateListpage->>+cloud: S : GET /app/VacantLandTaxRate/exportListXlx ExportListXlx
        cloud-->>-VacantLandTaxRateListpage: RES: Vacant Land Tax Rate List Xlx
    end

          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count| Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|-----|
|1.0| Create |ut_p_c_GSTS_WEB_VACANTLANDTAXRATE_200  ut_n_c_GSTS_WEB_VACANTLANDTAXRATE_201 ut_n_c_GSTS_WEB_VACANTLANDTAXRATE_207 ut_n_c_GSTS_WEB_VACANTLANDTAXRATE_212 |**Positive Test Cases:** Creating Vacant Land TaxRate  with Authorised User **Negative Test Cases:** 1.Creating Vacant Land TaxRate with Invalid Inputs and Without DB Connection 2.Creating VacantLandTaxRate with Empty Panchayat Resolution Id |**panchayatResolutionId:** drop down list **taxVal:** 1.value>=0 and value<=100  2.null|2|3|5| testAuthorisedUserCreateVacantLandTaxRate, testAuthorisedUserCreateVacantLandTaxRateNegative, testAuthorisedUserCreateVacantLandTaxRateWithoutDBConnection, testAuthorisedUserCreateVacantLandTaxRateWithEmptyPRId|
|1.0| Create Form |ut_p_c_GSTS_WEB_VACANTLANDTAXRATE_208 ut_n_c_GSTS_WEB_VACANTLANDTAXRATE_211 |**Positive Test Cases:** Open Vacant Land TaxRate Create Form with Authorised User **Negative Test Cases:** Open House TaxRate Create Form without DB Connection|Id |1|1|2| testAuthorisedUserOpenVacantLandTaxRateCreateForm, testAuthorisedUserOpenVacantLandTaxRateCreateFormWithEmptyPanchayatResolution, testAuthorisedUserOpenVacantLandTaxRateCreateFormWithoutDBConnection|
|1.0| Remove |ut_p_r_GSTS_WEB_VACANTLANDTAXRATE_306 ut_n_r_GSTS_WEB_VACANTLANDTAXRATE_304 ut_n_r_GSTS_WEB_VACANTLANDTAXRATE_305 ut_n_r_GSTS_WEB_VACANTLANDTAXRATE_307 ut_n_r_GSTS_WEB_VACANTLANDTAXRATE_308 |**Positive Test Cases:** Removing Vacant Land TaxRate  with Authorised User **Negative Test Cases:** Removing Vacant Land TaxRate with Invalid Inputs and Without DB Connection| **removeComment:** 1.valid characters 2.length>=6 and length<=256 3.null |1|4|5|testAuthorisedUserRemoveVacantLandTaxRate, testAuthorisedUserRemoveVacantLandTaxRateWithInvalidId, testAuthorisedUserRemoveVacantLandTaxRateWithoutDBConnection, testAuthorisedUserRemoveVacantLandTaxRateNegativeTestCase, testAuthorisedUserRemoveVacantLandTaxRateWithInvalidIdAndComment|
|1.0| Remove Form |ut_p_r_GSTS_WEB_VACANTLANDTAXRATE_300 ut_n_r_GSTS_WEB_VACANTLANDTAXRATE_301 ut_n_r_GSTS_WEB_VACANTLANDTAXRATE_303 |**Positive Test Cases:** Open House TaxRate Remove Form with Authorised User **Negative Test Cases:** Open House TaxRate Create Form with Invalid id and Without DB Connection|Id |1|2|3|testAuthorisedUserOpenVacantLandTaxRateRemoveFormWithValidId, testAuthorisedUserOpenVacantLandTaxRateRemoveFormWithInvalidId, testAuthorisedUserOpenVacantLandTaxRateRemoveFormWithoutDBConnection|
|1.0| View |ut_p_v_GSTS_WEB_VACANTLANDTAXRATE_400 ut_n_v_GSTS_WEB_VACANTLANDTAXRATE_401 |**Positive Test Cases:** View Vacant Land Tax Rate with Valid Id  with Authorised User**Negative Test Cases:** View Vacant Land tax Rate with Invalid ID  with Authorised User|1.Valid Id 2.Invalid Id|1|1|2|testAuthorisedUserViewVacantLandTaxRate, testAuthorisedUserViewVacantLandTaxRateWithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_VACANTLANDTAXRATE_500 ut_n_s_GSTS_WEB_VACANTLANDTAXRATE_502 ut_n_s_GSTS_WEB_VACANTLANDTAXRATE_503 |**Positive Test Cases:** Search Vacant land Tax Rate with Authorised User | **objStateSet:** Enum Values|1|2|3| testAuthorisedUserSearchVacantLandNegativetestCases, testAuthorisedUserSearchVacantLandWithoutDBConnection, testAuthorisedUserSearchVacantLandTaxNegativeCase |
|1.0| List |ut_p_l_GSTS_WEB_VACANTLANDTAXRATE_600 ut_n_l_GSTS_WEB_VACANTLANDTAXRATE_601 ut_n_l_GSTS_WEB_VACANTLANDTAXRATE_603 |**Positive Test Cases:** Check the object list with valid data  with Authorised User **Negative Test Cases:** Check the object list with Invalid data  with Authorised User|Validating with the field|1|2|3|testAuthorisedUserListVacantLandTaxRate, testAuthorisedUserListVacantLandTaxRateNegativeTestCase, testAuthorisedUserListVacantLandTaxRateWithoutDBConnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_VACANTLANDTAXRATE_800 ut_n_ep_GSTS_WEB_VACANTLANDTAXRATE_804 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** Export Pdf with Invalid Id and Without DB Connection|Id |1|1|2|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_VACANTLANDTAXRATE_801 ut_n_elp_GSTS_WEB_VACANTLANDTAXRATE_805 ut_n_elp_GSTS_WEB_VACANTLANDTAXRATE_812 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_VACANTLANDTAXRATE_802 ut_n_ex_GSTS_WEB_VACANTLANDTAXRATE_806 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|1|2|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_VACANTLANDTAXRATE_803 ut_n_elx_GSTS_WEB_VACANTLANDTAXRATE_807 ut_n_elx_GSTS_WEB_VACANTLANDTAXRATE_813 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### UnAuthorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count| Method Name| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_WEB_VACANTLANDTAXRATE_204 |Unauthorised User does not have permission to create|**panchayatResolutionId:** drop down list **taxVal:** 1.value>=0 and value<=100  2.null|1|N/A|1| testUnAuthorisedUserCreateVacantLandTaxRate|
|1.0| Create Form |ut_n_c_GSTS_WEB_VACANTLANDTAXRATE_210 |Unauthorised User does not have permission to open create form|Id |1|0|1|testUnAuthorisedUserOpenVacantLandTaxRateCreateForm|
|1.0| Remove |ut_p_r_GSTS_WEB_VACANTLANDTAXRATE_309 |Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2.length>=6 and length<=256 3.null |1|N/A|1|testUnAuthorisedUserRemoveVacantLandTaxRate|
|1.0| Remove Form |ut_n_r_GSTS_WEB_VACANTLANDTAXRATE_302 |Unauthorised User does not have permission to open remove form|Id |1|0|1|testUnAuthorisedUserOpenVacantLandTaxRateRemoveForm|
|1.0| View |ut_p_v_GSTS_WEB_VACANTLANDTAXRATE_402 |Unauthorised User does not have permission to view|1.Valid Id|1|N/A|1|testUnAuthorisedUserViewVacantLandTaxRate|
|1.0| Search |ut_p_s_GSTS_WEB_VACANTLANDTAXRATE_501 |Unauthorised User does not have permission to search | **objStateSet:** Enum Values|1|N/A|1| testUnAuthorisedUserSearchVacantLandTaxRate|
|1.0| List |ut_p_l_GSTS_WEB_VACANTLANDTAXRATE_602 |Unauthorised User does not have permission to view the list of vacant land tax rates|Validating with the field|1|N/A|1| testUnAuthorisedUserListVacantLandTaxRate|
|1.0| PDF |ut_n_ep_GSTS_WEB_VACANTLANDTAXRATE_808 |Export List Pdf with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportPdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_VACANTLANDTAXRATE_809 |Export Pdf with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_VACANTLANDTAXRATE_810 |Export XLX with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_VACANTLANDTAXRATE_811 |Export List XLX with UnAuthorised User|1.Valid Id |1|N/A|1|testUnAuthorisedUserExportListXlxWithValidId|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|-----------|
|1.0|Create|ut_n_c_GSTS_WEB_VACANTLANDTAXRATE_700|Create Vacant Land TaxRate with different Panchayat Context Panchayat Resolution| N/A |Not able to set Different Panchayat Context Panchayat Resolution|1| testAuthorisedUserCreateVacantLandTaxRateWithDifferentPanchayatContextPanchayatResolution|
|1.0|View|ut_n_v_GSTS_WEB_VACANTLANDTAXRATE_701|View Vacant Land TaxRate At different Panchayat | Id |SecurityUnAuthorisedExcepion will be thrown|1| testAuthorisedUserViewVacantLandTaxRateAtAnotherPanchayat|


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




 
