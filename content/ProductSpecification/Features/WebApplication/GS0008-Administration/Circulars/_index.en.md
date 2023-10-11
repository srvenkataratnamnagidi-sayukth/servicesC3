---
title: Circulars
tags : ["Composing"]
---

## Introduction
Circulars are one of the features of this software product. Circular is notice or statement for some purposes and will be released by officers. Users will have access to circulars if they have permission, Otherwise will not access. 

## Business Assumptions
what type of users can create circulars should be planned at design phase.

## Requirements
### Functional Requirements
1. Users of all levels can create circulars.
1. Users of all levels can remove circulars.
1. we can create and remove circulars at any level.
1. It is accessible at all levels of organization.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access circulars.  
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Circular feature contains information about all circulars which are released by officers.

### Design 
1. Each circular has name, description, code and circular copy.
1. Each circular has unique code(circular number).
1. We can create, remove, view and export the circular.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_CIRCULAR_list|To view all the circulars. This listing page should bind to a permission|
|uc_CIRCULAR_create|To create the circular. This create page should bind to a permission|
|uc_CIRCULAR_remove|To remove the circular. This remove page should bind to a permission|
|uc_CIRCULAR_view|To view the circular. This view page should bind to a permission|
|uc_CIRCULAR_search|To search the circular. This search page should bind to a permission|
|uc_CIRCULAR_export|To export the circular in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9. space _-, minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|YES|YES|YES|YES||
|descr|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=256|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) NOT NULL|YES|YES|YES|YES|YES||
|code|YES|NA|a-zA-Z0-9, minlen=3, maxlen=32|@Column(name = "code", length = 32, nullable = false, unique = true)|code varchar(32) NOT NULL|YES|YES|YES|NO|NO||
|fileName|YES|NA|Attachment|@Column(name = "file_name", length = 64, nullable = false)|file_name varchar(64) NOT NULL|YES|NO|YES|YES|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS
No Enum Constants in circulars.

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|CIRCULAR_VIEW|View|
|CIRCULAR_CREATE|Create|
|CIRCULAR_REMOVE|Remove|
|CIRCULAR_VIEW|Export|
|CIRCULAR_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_circular__code (code)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_CIRCULAR_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_CIRCULAR_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_CIRCULAR_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_CIRCULAR_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

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
	CircularsMenu((Circulars Menu))
	ListPage{Circulars List Page}
	CreatePage((Create Page))
	RemovePage((Remove Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->CircularsMenu
    subgraph Menu
    CircularsMenu
    end
    subgraph   
    CircularsMenu-->ListPage
    ListPage--C-R-V-E-->ListPage
    end
    subgraph  
    CircularsMenu--F-->ErrorPage
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
1. Only a user with the CIRCULAR_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant CircularsListpage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        CircularsListpage->>+Net: Check Internet, GET /app/ctx/Circular/list ListPage
        Net--x-CircularsListpage: F : Connection Error
        CircularsListpage->>+cloud: S:  GET /app/ctx/Circular/list ListPage
        cloud-->>-CircularsListpage: RES:List Page
    end
    rect rgb(244,244,244)
        CircularsListpage->>+Net: Check Internet, GET /app/Circular/create/form CreateFormPage
        Net--x-CircularsListpage: F : Connection Error
        CircularsListpage->>+cloud: S : GET /app/Circular/create/form CreateFormPage
        cloud-->>-CircularsListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        CircularsListpage->>+Net: Check Internet: POST /app/Circular/create Create
        Net--x-CircularsListpage: F : Connection Error
        CircularsListpage->>+cloud: S : POST /app/Circular/create Create
        cloud-->>-CircularsListpage: RES: An Circular Successfully Created
    end
    rect rgb(244,244,244)
        CircularsListpage->>+Net: Check Internet: GET /app/Circular/remove/form RemoveFormPage
        Net--x-CircularsListpage: F : Connection Error
        CircularsListpage->>+cloud: S : GET /app/Circular/remove/form RemoveFormPage
        cloud-->>-CircularsListpage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        CircularsListpage->>+Net: Check Internet: POST /app/Circular/remove Remove
        Net--x-CircularsListpage: F : Connection Error
        CircularsListpage->>+cloud: S : POST /app/Circular/remove Remove
        cloud-->>-CircularsListpage: RES: An Circular Successfully Removed
    end
    rect rgb(244,244,244)
        CircularsListpage->>+Net: Check Internet: GET /app/Circular/view ViewPage
        Net--x-CircularsListpage: F : Connection Error
        CircularsListpage->>+cloud: GET /app/Circular/view ViewPage
        cloud-->>-CircularsListpage: RES: Circular View
    end
    rect rgb(244,244,244)
        CircularsListpage->>+Net: Check Internet: GET /app/Circular/exportPdf ExportPdf
        Net--x-CircularsListpage: F : Connection Error 
        CircularsListpage->>+cloud: GET /app/Circular/exportPdf ExportPdf
        cloud-->>-CircularsListpage: RES: Circular Pdf
    end
    rect rgb(244,244,244)
        CircularsListpage->>+Net: Check Internet: GET /app/Circular/exportListPdf ExportListPdf
        Net--x-CircularsListpage: F : Connection Error
        CircularsListpage->>+cloud: S : GET /app/Circular/exportListPdf ExportListPdf
        cloud-->>-CircularsListpage: RES: Circular List Pdf
    end
    rect rgb(244,244,244)
        CircularsListpage->>+Net: Check Internet: GET /app/Circular/exportXlx ExportXlx
        Net--x-CircularsListpage: F : Connection Error
        CircularsListpage->>+cloud: GET /app/Circular/exportXlx ExportXlx
        cloud-->>-CircularsListpage: RES: Circular Xlx
    end
    rect rgb(244,244,244)
        CircularsListpage->>+Net: Check Internet: GET /app/Circular/exportListXlx ExportListXlx
        Net--x-CircularsListpage: F : Connection Error
        CircularsListpage->>+cloud: S : GET /app/Circular/exportListXlx ExportListXlx
        cloud-->>-CircularsListpage: RES: Circular List Xlx
    end
    rect rgb(244,244,244)
        CircularsListpage->>+Net: Check Internet: GET /app/Circular/download DownloadCopy
        Net--x-CircularsListpage: F : Connection Error
        CircularsListpage->>+cloud: S : GET /app/Circular/download DownloadCopy
        cloud-->>-CircularsListpage: RES: Circular Copy
    end
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|-----|
|1.0| Create Form |ut_p_c_GSTS_WEB_CIRCULAR_20|**Positive Test Cases:** 1.Open Circular Create Form|-|1|0|1|testPosOpenCircularCreateFormWithAuthorisedUser|
|1.0| Create |ut_p_c_GSTS_WEB_CIRCULAR_40  ut_n_c_GSTS_WEB_CIRCULAR_50 ut_n_c_GSTS_WEB_CIRCULAR_30 |**Positive Test Cases:** Create State Level Circular with valid inputs **Negative Test Cases:** 1.Creating Circular with invalid inputs 2.Create Circular without db connection|  **name:**  1.valid characters 2. length>=3 and length<=64  3.null **code:** 1.valid characters 2. length>=3 and length<=32 3.null 4.unique key  **descr:** 1.valid characters 2. length>=6 and length<=256 3.null|3|5|8|testPosAuthorisedUserStateLevelUserCreateStateLevelCircularWithValidInputs,  testNegAuthorisedStateLevelUserCreateStateLevelCircularWithInvalidInputs,  testNegCreateStateLevelCircularWithoutDBconnection|
|1.0| Remove Form |ut_p_r_GSTS_WEB_CIRCULAR_70   ut_n_r_GSTS_WEB_CIRCULAR_80   ut_n_r_GSTS_WEB_CIRCULAR_90  ut_n_r_GSTS_WEB_CIRCULAR_150|**Positive Test Cases:** Open circular remove form with valid Id   **Negative Test Cases:**  1.Open Circular remove Form Without DB Connection 2. Open Circular remove Form with Invalid id   3.Open Circular remove form with Already removed Circular Id with Authorised user|Id|1|3|4|testPosAuthorisedStateLevelUserOpenCircularRemoveFormWithValidId,  testNegAuthorisedStateLevelUserOpenCircularRemoveFormWithoutDbConnection,  testNegAuthorisedStateLevelUserOpenCircularRemoveFormWithInValidId,  testNegAuthorisedSLUserOpenCircularRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_CIRCULAR_100  ut_n_r_GSTS_WEB_CIRCULAR_110 ut_n_r_GSTS_WEB_CIRCULAR_130 ut_n_r_GSTS_WEB_CIRCULAR_140 ut_n_r_GSTS_WEB_CIRCULAR_160 |**Positive Test Cases:** 1. Remove State Level Circular with Valid Remove Comment  **Negative Test Cases:** 1.Removing Circular with invalid remove comment 2.Remove Circular without db connection 3.Remove already removed Circular 4.Remove Circular with Invalid Id| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |1|4|5|testPosStateLevelAuthorisedUserRemoveSLCircularWithValidRemoveCommentAndValidId,  testNegStateLevelAuthorisedUserRemoveSLCircularWithInValidRemoveCommentAndValidId,  testNegSLAuthorisedUserRemoveCircularWithoutDbConnection,  testNegSLAuthorisedUserRemoveAlreadyRemovedCircular,  testNegStateLevelAuthorisedUserRemoveSLCircularInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_CIRCULAR_190  ut_n_v_GSTS_WEB_CIRCULAR_200 ut_n_v_GSTS_WEB_CIRCULAR_210 |**Positive Test Cases:** View State Level Circular with Valid Id  with Authorised User **Negative Test Cases:** 1.View Circular without DB Connection 2.View Circular with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewSLCircularValidId,  testNegAuthorisedUserViewSLCircularWithoutDbConnection,  testNegAuthorisedUserViewSLCircularwithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_CIRCULAR_260  ut_n_s_GSTS_WEB_CIRCULAR_270 ut_n_s_GSTS_WEB_CIRCULAR_280 |**Positive Test Cases:** Search State Level Circular with Valids inputs  **Negative Test Cases:** 1.Search State Level Circular without db connection 2.Search Circular with Invalid inputs|  **name:** 1.valid characters 2. length>=3 and length=<64  3.null **code:** 1.valid characters 2. length>=3 and length<=32 3.null **descr:** 1.valid characters 2. length>=6 and length<=256 3.null|1|2|3|testPosAuthorisedUserSearchSLCircularWithValidInputs,  testNegAuthorisedUserSearchSLCircularWithoutDBconnection,  testNegAuthorisedUserSearchSLCircularWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_CIRCULAR_230 ut_n_l_GSTS_WEB_CIRCULAR_240|**Positive Test Cases:** Get Circular State Level List **Negative Test Cases:** Get Circular List without db connection|Validating with unique field|1|1|2|testPosAuthorisedUserSLCircularList,  testNegAuthorisedUserSLCircularListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_CIRCULAR_360   ut_n_ep_GSTS_WEB_CIRCULAR_370   ut_n_ep_GSTS_WEB_CIRCULAR_380 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportPdfWithValidId,  testNegAuthorisedUserExportPdfwithoutDbConnection,  testNegAuthorisedUserExportPdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_CIRCULAR_390   ut_n_elp_GSTS_WEB_CIRCULAR_400   ut_n_elp_GSTS_WEB_CIRCULAR_410 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportListPdfWithValidId,  testNegAuthorisedUserExportListPdfwithoutDbConnection,  testNegAuthorisedUserExportListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_CIRCULAR_420   ut_n_ex_GSTS_WEB_CIRCULAR_430   ut_n_ex_GSTS_WEB_CIRCULAR_440 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportXlxValidId,  testNegAuthorisedUserExportXlxwithoutDbConnection,  testNegAuthorisedUserExportXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_CIRCULAR_450   ut_n_elx_GSTS_WEB_CIRCULAR_460   ut_n_elx_GSTS_WEB_CIRCULAR_470 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportListXlxValidId,  testNegAuthorisedUserExportListXlxWithoutDbConnection,  testNegAuthorisedUserExportListXlxInValidId|
|1.0| Download|ut_p_elx_GSTS_WEB_CIRCULAR_480   ut_n_elx_GSTS_WEB_CIRCULAR_490   ut_n_elx_GSTS_WEB_CIRCULAR_500 ut_n_elx_GSTS_WEB_CIRCULAR_505 |**Positive Test Cases:** Download Circular attachment with valid id **Negative Test Cases:** 1. Without DB Connection 2.Circular attachment with Invalid Id 3.Download Circular Attachment with valid Id and Invalid Document type|Id |1|3|4|testPosAuthorisedUserDownloadCircularAttachmentValidId,  testNegAuthorisedUserDownloadCircularAttachmentWithoutDbconnection,  testNegAuthorisedUserDownloadCircularAttachmentInValidId, testNegAuthorisedUserDownloadCircularAttachmentWithValidIdAndInvalidDocType|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|------|
|1.0| Create |ut_n_c_GSTS_WEB_CIRCULAR_60 |Unauthorised User does not have permission to create|  **name:** 1.valid characters 2. length>=3 and length<=64  3.null **code:** 1.valid characters 2. length>=3 and length<=32 3.null 4.unique key  **descr:** 1.valid characters 2. length>=6 and length<=256 3.null|0|1|1|testNegUnAuthorisedUserCreateStateLevelCircular|
|1.0| Remove Form|ut_n_r_GSTS_WEB_CIRCULAR_170|Unauthorised User opening Circular remove form||0|1|1|testNegUnAuthorisedStateLevelUserOpenCircularRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_CIRCULAR_180|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserRemoveSLCircular|
|1.0| View |ut_n_v_GSTS_WEB_CIRCULAR_220|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewCircular|
|1.0| Search |ut_n_s_GSTS_WEB_CIRCULAR_290|Unauthorised User does not have permission to search|  **name:** 1.valid characters2. length>=3 and length=<64  3.null **code:** 1.valid characters 2. length>=3 and length<=32 3.null **descr:** 1.valid characters 2. length>=6 and length<=256 3.null|0|1|1|testNegUnAuthorisedUserSearchSLCircular|
|1.0| List |ut_n_l_GSTS_WEB_CIRCULAR_250|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserSLCircularList|
|1.0| PDF |ut_n_ep_GSTS_WEB_CIRCULAR_510 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_CIRCULAR_520 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_CIRCULAR_530 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_CIRCULAR_540 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportListXlxWithValidId|
|1.0| Download |ut_n_d_GSTS_WEB_CIRCULAR_550 |Download Circular Attachment with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserDownloadCircularAttachmentWithValidId|


#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|------------|
|1.0|Create|ut_p_c_GSTS_WEB_CIRCULAR_300|Create District Level Circular with Authorised district level user| N/A |Will be Created|1|testPosCreateDistLevelCircularWithAuthorisedDistLeveluser|
|1.0|Create|ut_p_c_GSTS_WEB_CIRCULAR_310|Create Division Level Circular with Authorised division level user| N/A |Will be Created|1|testPosCreateDivLevelCircularwithAuthorisedDivLevelUser|
|1.0|Create|ut_p_c_GSTS_WEB_CIRCULAR_320|Create Mandal Level Circular with Authorised mandal level user| N/A |Will be Created|1|testPosCreateMandalLevelCircularwithAuthorizedManLevelUser|
|1.0|Create|ut_p_c_GSTS_WEB_CIRCULAR_330|Create Panchayat Level Circular with Authorised panchayat level user| N/A |Will be Created|1|testPosCreatePanchayatLevelCircularwithAuthorizedPanLevelUser|
|1.0|View|ut_n_v_GSTS_WEB_CIRCULAR_340|Scope Level for Circular View| N/A |Will not be accessed|1|testNegScopeLevelForCircularView|
|1.0|Remove|ut_n_r_GSTS_WEB_CIRCULAR_350|Scope Level for Circular Remove| N/A |Will not be removed|1|testNegScopeLevelForCircularRemove|
|1.0|Remove|ut_p_r_GSTS_WEB_CIRCULAR_560|Remove District Level Circular with Authorised district level user| N/A |Will be Removed|1|testPosDistLevelAuthorisedUserRemoveDistCircularWithValidRemoveCommentAndValidId|
|1.0|Remove|ut_p_r_GSTS_WEB_CIRCULAR_570|Remove Division Level Circular with Authorised division level user| N/A |Will be Removed|1|testPosDivLevelAuthorisedUserRemoveDivCircularWithValidRemoveCommentAndValidId|
|1.0|Remove|ut_p_r_GSTS_WEB_CIRCULAR_580|Remove Mandal Level Circular with Authorised mandal level user| N/A |Will be Removed|1|testPosMandalLevelAuthorisedUserRemoveMandalCircularWithValidRemoveCommentAndValidId|
|1.0|Remove|ut_p_r_GSTS_WEB_CIRCULAR_590|Remove Panchayat Level Circular with Authorised panchayat level user| N/A |Will be Removed|1|testPosPanchayatLevelAuthorisedUserRemovePanchayatCircularWithValidRemoveCommentAndValidId|

## Security compliance check
1. Only user having the permission **ROLE_CIRCULAR_VIEW** should view this functionality 
1. Only user having the permission **ROLE_CIRCULAR_CREATE** should create this functionality 
1. Only user having the permission **ROLE_CIRCULAR_REMOVE** should remove this functionality 
1. Only user having the permission **ROLE_CIRCULAR_VIEW** should export this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Circulars in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
