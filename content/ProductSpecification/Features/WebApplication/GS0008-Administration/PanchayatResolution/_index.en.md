---
title: Panchayat Resolution
tags : ["Composing"]
---

## Introduction
Panchayat Resolution is one of the features of this software product. Panchayat Resolution is a decision to do or not to do something in panchayat. Users will have access to panchayat resolution if they have permission, Otherwise will not access. 

## Business Assumptions
what type of users can create panchayat resolution should be planned at design phase.

## Requirements
### Functional Requirements
1. Users of all levels can create, remove, view and export the panchayat resolution.  
1. we can create and remove panchayat resolution at panchayat level only.
1. Panchayat Resolution feature is accessible at panchayat level only.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access panchayat resolution.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Panchayat resolution contains information about the resolutions which are passed by the panchayat.

### Design 
1. Each panchayat resolution has name, description, code(government order number), attendees list, meeting date, resolution type, approval percentage, and panchayat resolution copy.
1. Each panchayat resolution in the same panchayat has an unique code.
1. We can create, remove, view and export the panchayat resolution.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_panchayat_resolution_list|To view all the panchayat resolutions. This listing page should bind to a permission|
|uc_panchayat_resolution_create|To create the panchayat resolution. This create page should bind to a permission|
|uc_panchayat_resolution_remove|To remove the panchayat resolution. This remove page should bind to a permission|
|uc_panchayat_resolution_view|To view the panchayat resolution. This view page should bind to a permission|
|uc_panchayat_resolution_search|To search the panchayat resolution. This search page should bind to a permission|
|uc_panchayat_resolution_export|To export the panchayat resolution in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9. space _-, minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|YES|YES|YES|YES||
|descr|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=256|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) NOT NULL|YES|YES|YES|YES|NO||
|code|YES|NA|a-zA-Z0-9, minlen=3, maxlen=32|@Column(name = "code", length = 32, nullable = false, unique = true)|code varchar(32) NOT NULL|YES|YES|YES|YES|YES||
|resolutionType|YES|NA|Dropdown values|@Enumerated(EnumType.STRING) @Column(name = "resolution_type", length = 32, nullable = false)|resolution_type varchar(32) NOT NULL|YES|YES|YES|YES|YES||
|approvalPercentage|YES|NA|0-9 and ., maxlen=6|@Column(name = "approval_percentage", nullable = false)|approval_percentage float(9,2) NOT NULL|YES|YES|YES|YES|NO||
|attendeesList|YES|NA|a-zA-Z0-9,:/. space _\-, minlen=6, maxlen=256|@Column(name = "attendees_list", length = 256, nullable = false)|attendees_list varchar(256) NOT NULL|YES|YES|YES|NO|NO||
|meetingDate|YES|NA|Date dd-MM-YYYY|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "meeting_date", nullable = false)|meeting_date datetime NOT NULL|YES|NO|YES|NO|NO||
|fileName|YES|NA|Attachment|@Column(name = "file_name", length = 64, nullable = false)|file_name varchar(64) NOT NULL|YES|NO|YES|YES|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Resolution Type

{{<mermaid align="left">}}
classDiagram
    class ResolutionType{
      PANCHAYAT_RESOLUTION
      GRAMA_SABHA
      NONE
    }
{{< /mermaid >}}


#### Feature Permission

|Permission code|Action|
|---------------|-------|
|PANCHAYAT_RESOLUTION_VIEW|View|
|PANCHAYAT_RESOLUTION_CREATE|Create|
|PANCHAYAT_RESOLUTION_REMOVE|Remove|
|PANCHAYAT_RESOLUTION_VIEW|Export|
|PANCHAYAT_RESOLUTION_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_pr__code__pid (code,org_panchayat_id)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_PANCHAYAT_RESOLUTION_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_PANCHAYAT_RESOLUTION_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_PANCHAYAT_RESOLUTION_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_PANCHAYAT_RESOLUTION_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

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
	PanchayatResolutionMenu((Panchayat Resolution Menu))
	ListPage{Panchayat Resolution List Page}
	CreatePage((Create Page))
	RemovePage((Remove Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->PanchayatResolutionMenu
    subgraph Menu
    PanchayatResolutionMenu
    end
    subgraph   
    PanchayatResolutionMenu-->ListPage
    ListPage--C-R-V-E-->ListPage
    end
    subgraph  
    PanchayatResolutionMenu--F-->ErrorPage
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
1. Only a user with the PANCHAYAT_RESOLUTION_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant PanchayatResolutionListpage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        PanchayatResolutionListpage->>+Net: Check Internet, GET /app/ctx/PanchayatResolution/list ListPage
        Net--x-PanchayatResolutionListpage: F : Connection Error
        PanchayatResolutionListpage->>+cloud: S:  GET /app/ctx/PanchayatResolution/list ListPage
        cloud-->>-PanchayatResolutionListpage: RES:List Page
    end
    rect rgb(244,244,244)
        PanchayatResolutionListpage->>+Net: Check Internet, GET /app/PanchayatResolution/create/form CreateFormPage
        Net--x-PanchayatResolutionListpage: F : Connection Error
        PanchayatResolutionListpage->>+cloud: S : GET /app/PanchayatResolution/create/form CreateFormPage
        cloud-->>-PanchayatResolutionListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        PanchayatResolutionListpage->>+Net: Check Internet: POST /app/PanchayatResolution/create Create
        Net--x-PanchayatResolutionListpage: F : Connection Error
        PanchayatResolutionListpage->>+cloud: S : POST /app/PanchayatResolution/create Create
        cloud-->>-PanchayatResolutionListpage: RES: An PanchayatResolution Successfully Created
    end
    rect rgb(244,244,244)
        PanchayatResolutionListpage->>+Net: Check Internet: GET /app/PanchayatResolution/remove/form RemoveFormPage
        Net--x-PanchayatResolutionListpage: F : Connection Error
        PanchayatResolutionListpage->>+cloud: S : GET /app/PanchayatResolution/remove/form RemoveFormPage
        cloud-->>-PanchayatResolutionListpage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        PanchayatResolutionListpage->>+Net: Check Internet: POST /app/PanchayatResolution/remove Remove
        Net--x-PanchayatResolutionListpage: F : Connection Error
        PanchayatResolutionListpage->>+cloud: S : POST /app/PanchayatResolution/remove Remove
        cloud-->>-PanchayatResolutionListpage: RES: An PanchayatResolution Successfully Removed
    end
    rect rgb(244,244,244)
        PanchayatResolutionListpage->>+Net: Check Internet: GET /app/PanchayatResolution/view ViewPage
        Net--x-PanchayatResolutionListpage: F : Connection Error
        PanchayatResolutionListpage->>+cloud: GET /app/PanchayatResolution/view ViewPage
        cloud-->>-PanchayatResolutionListpage: RES: PanchayatResolution View
    end
    rect rgb(244,244,244)
        PanchayatResolutionListpage->>+Net: Check Internet: GET /app/PanchayatResolution/exportPdf ExportPdf
        Net--x-PanchayatResolutionListpage: F : Connection Error 
        PanchayatResolutionListpage->>+cloud: GET /app/PanchayatResolution/exportPdf ExportPdf
        cloud-->>-PanchayatResolutionListpage: RES: PanchayatResolution Pdf
    end
    rect rgb(244,244,244)
        PanchayatResolutionListpage->>+Net: Check Internet: GET /app/PanchayatResolution/exportListPdf ExportListPdf
        Net--x-PanchayatResolutionListpage: F : Connection Error
        PanchayatResolutionListpage->>+cloud: S : GET /app/PanchayatResolution/exportListPdf ExportListPdf
        cloud-->>-PanchayatResolutionListpage: RES: PanchayatResolution List Pdf
    end
    rect rgb(244,244,244)
        PanchayatResolutionListpage->>+Net: Check Internet: GET /app/PanchayatResolution/exportXlx ExportXlx
        Net--x-PanchayatResolutionListpage: F : Connection Error
        PanchayatResolutionListpage->>+cloud: GET /app/PanchayatResolution/exportXlx ExportXlx
        cloud-->>-PanchayatResolutionListpage: RES: PanchayatResolution Xlx
    end
    rect rgb(244,244,244)
        PanchayatResolutionListpage->>+Net: Check Internet: GET /app/PanchayatResolution/exportListXlx ExportListXlx
        Net--x-PanchayatResolutionListpage: F : Connection Error
        PanchayatResolutionListpage->>+cloud: S : GET /app/PanchayatResolution/exportListXlx ExportListXlx
        cloud-->>-PanchayatResolutionListpage: RES: PanchayatResolution List Xlx
    end
    rect rgb(244,244,244)
        PanchayatResolutionListpage->>+Net: Check Internet: GET /app/PanchayatResolution/download DownloadCopy
        Net--x-PanchayatResolutionListpage: F : Connection Error
        PanchayatResolutionListpage->>+cloud: S : GET /app/PanchayatResolution/download DownloadCopy
        cloud-->>-PanchayatResolutionListpage: RES: PanchayatResolution Copy
    end
          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------------|------|
|1.0| Create Form |ut_p_c_GSTS_WEB_PANCHAYAT_RESOLUTION_120 |**Positive Test Cases:** 1.Open Panchayat Resolution Create Form At panchayat level |-|1|0|1|testPosOpenPanchayatResolutionCreateFormWithAuthorisedUser|
|1.0| Create |ut_p_c_GSTS_WEB_PANCHAYAT_RESOLUTION_140  ut_n_c_GSTS_WEB_PANCHAYAT_RESOLUTION_150 ut_n_c_GSTS_WEB_PANCHAYAT_RESOLUTION_130 |**Positive Test Cases:** Creating Panchayat Resolution with valid inputs **Negative Test Cases:** 1. Creating Panchayat Resolution  with invalid inputs 2.Create Panchayat Resolution without db connection|**resolutionType:** enums **name:** 1.Valid Characters 2.length>=3 and length<=64 3.null **code:** 1.Valid Characters 2.length>=3 and length<=32 3.null 4. unique in same panchayat **descr:** 1.Valid Characters 2.length>=6 and length<=256 3.null **attendeesList:** 1.Valid Characters 2.length>=6 and length<=256 3.null **approvalPercentage:** 1.null 2. >=0 and <=100 **meetingDate:** 1.null|6|5|11|testPosAuthorisedPanchayatLevelUserCreatePanchayatLevelPanchayatResolutionWithValidInputs, testNegAuthorisedPanchayatLevelUserCreatePanchayatLevelPanchayatResolution,  testNegCreatePanchayatResolutionWithoutDBconnection|
|1.0| Remove Form |ut_p_r_GSTS_WEB_PANCHAYAT_RESOLUTION_210   ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_215   ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_220  ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_270|**Positive Test Cases:** Open Panchayat Resolution remove form with valid Id with Authorised Panchayat level user    **Negative Test Cases:**  1.Open Panchayat Resolution remove Form Without DB Connection 2. Open Panchayat Resolution remove Form with Invalid id   3.Open Panchayat Resolution remove form with Already removed Panchayat Resolution Id with Authorised user|Id|1|3|4|testPosAuthorisedPanLevelUserOpenPanLevelPanchayatResolutionRemoveFormWithValidId,  testNegOpenPanchayatResolutionRemoveFormWithoutDbConnection,  testNegAuthorisedPanLevelUserOpenPanchayatResolutionRemoveFormWithInValidId,  testNegAuthorisedPanUserOpenPanchayatResolutionRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_PANCHAYAT_RESOLUTION_280  ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_240 ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_255  ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_260  ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_420 |**Positive Test Cases:** Remove Panchayat Resolution with Valid Remove Comment with Panchayat Level Authorised User **Negative Test Cases:** 1. Removing Panchayat Resolution with invalid remove comment 2.Remove Panchayat Resolution without db connection 3.Remove already removed Panchayat Resolution  4. Remove Panchayat Resolution with invalid Id| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|testPosPanLevelAuthorisedUserRemovePanPanchayatResolutionWithValidRemoveCommentAndValidId,  testNegPanLevelAuthorisedUserRemovePanLevelPanchayatResolutionWithInValidRemoveCommentAndValidId,  testNegRemovePanchayatResolutionWithoutDbConnection,  testNegAuthorisedUserRemoveAlreadyRemovedPanchayatResolution,  testNegPanLevelAuthorisedUserRemovePanchayatResolutionWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_PANCHAYAT_RESOLUTION_310  ut_n_v_GSTS_WEB_PANCHAYAT_RESOLUTION_320 ut_n_v_GSTS_WEB_PANCHAYAT_RESOLUTION_330 |**Positive Test Cases:** View Panchayat Resolution with Valid Id  with Authorised User **Negative Test Cases:** 1.View Panchayat Resolution without db connection 2.View Panchayat Resolution  with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewPanchayatResolutionWithValidId,  testPosAuthorisedUserViewPanchayatResolutionWithoutDbConnection,  testNegAuthorisedUserViewPanchayatResolutionwithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_PANCHAYAT_RESOLUTION_360  ut_n_s_GSTS_WEB_PANCHAYAT_RESOLUTION_365 ut_n_s_GSTS_WEB_PANCHAYAT_RESOLUTION_370 |**Positive Test Cases:** Search Panchayat Resolution  with valid inputs **Negative Test Cases:** 1.Search Panchayat Resolution without db connection 2.Search Panchayat Resolution with invalid inputs| **1.name 2.code 3.resolutionType**|1|2|3|testPosAuthorisedUserSearchPanchayatResolutionWithValidInputs,  testNegAuthorisedUserSearchPanchayatResolutionWithoutDBconnection,  testNegAuthorisedUserSearchPanchayatResolutionWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_PANCHAYAT_RESOLUTION_340 ut_n_l_GSTS_WEB_PANCHAYAT_RESOLUTION_350|**Positive Test Cases:** Get Panchayat Resolution List with Authorised User **Negative Test Cases:** |Validating with unique field|1|1|2|testPosAuthorisedUserPanchayatResolutionList,  testNegAuthorisedUserPanchayatResolutionListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_PANCHAYAT_RESOLUTION_500   ut_n_ep_GSTS_WEB_PANCHAYAT_RESOLUTION_505   ut_n_ep_GSTS_WEB_PANCHAYAT_RESOLUTION_510 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportPanchayatResolutionPdfWithValidId,  testNegAuthorisedUserExportPanchayatResolutionPdfwithoutDbconnection,  testNegAuthorisedUserExportPanchayatResolutionPdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_PANCHAYAT_RESOLUTION_520   ut_n_elp_GSTS_WEB_PANCHAYAT_RESOLUTION_525   ut_n_elp_GSTS_WEB_PANCHAYAT_RESOLUTION_530 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportPanchayatResolutionListPdfWithValidId,  testNegAuthorisedUserExportPanchayatResolutionListPdfwithoutDbconnection,  testNegAuthorisedUserExportPanchayatResolutionListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_PANCHAYAT_RESOLUTION_540   ut_n_ex_GSTS_WEB_PANCHAYAT_RESOLUTION_545   ut_n_ex_GSTS_WEB_PANCHAYAT_RESOLUTION_550 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportPanchayatResolutionXlxValidId,  testNegAuthorisedUserExportPanchayatResolutionXlxwithoutDbconnection,  testNegAuthorisedUserExportPanchayatResolutionXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_PANCHAYAT_RESOLUTION_560   ut_n_elx_GSTS_WEB_PANCHAYAT_RESOLUTION_565   ut_n_elx_GSTS_WEB_PANCHAYAT_RESOLUTION_570 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportPanchayatResolutionListXlxValidId,  testNegAuthorisedUserExportPanchayatResolutionListXlxwithoutDbconnection,  testNegAuthorisedUserExportPanchayatResolutionListXlxInValidId|
|1.0| Download|ut_p_elx_GSTS_WEB_PANCHAYAT_RESOLUTION_580   ut_n_elx_GSTS_WEB_PANCHAYAT_RESOLUTION_585   ut_n_elx_GSTS_WEB_PANCHAYAT_RESOLUTION_590 ut_n_elx_GSTS_WEB_PANCHAYAT_RESOLUTION_600 |**Positive Test Cases:** Download panchayat resolution attachment with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.panchayat resolution attachment with Invalid Id 3.Download Panchayat Resolution Attachment with valid Id and Invalid Document type|Id |1|3|4|testPosAuthorisedUserDownloadPanchayatResolutionAttachmentValidId,  testNegAuthorisedUserDownloadPanchayatResolutionAttachmentwithoutDbConnection,  testNegAuthorisedUserDownloadPanchayatResolutionAttachmentInValidId, testNegAuthorisedUserDownloadPanchayatResolutionAttachmentWithValidIdAndInvalidDocType|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------------|-----|
|1.0| Create |ut_n_c_GSTS_WEB_PANCHAYAT_RESOLUTION_200 |Unauthorised User does not have permission to create|**resolutionType:** enums **name:** 1.Valid Characters 2.length>=3 and length<=64 3.null **code:** 1.Valid Characters 2.length>=3 and length<=32 3.null 4. unique in same panchayat **descr:** 1.Valid Characters 2.length>=6 and length<=256 3.null **attendeesList:** 1.Valid Characters 2.length>=6 and length<=256 3.null **approvalPercentage:** 1.null 2. >=0 and <=100 **meetingDate:** 1.null|0|1|1|testNegUnAuthorisedUserCreatePanchayatResolution|
|1.0| Remove Form|ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_290|Unauthorised User opening Panchayat Resolution remove form||0|1|1|testNegUnAuthorisedPanLevelUserOpenPanchayatResolutionRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_300|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserRemovePanchayatResolution|
|1.0| View |ut_n_v_GSTS_WEB_PANCHAYAT_RESOLUTION_335|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewPanchayatResolution|
|1.0| Search |ut_n_s_GSTS_WEB_PANCHAYAT_RESOLUTION_380|Unauthorised User does not have permission to search|**1.name 2.code 3.resolutionType**|0|1|1|testNegUnAuthorisedUserSearchPanchayatResolution|
|1.0| List |ut_n_l_GSTS_WEB_PANCHAYAT_RESOLUTION_355|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserPanchayatResolutionList|
|1.0| PDF |ut_n_ep_GSTS_WEB_PANCHAYAT_RESOLUTION_610 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPanchayatResolutionPdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_PANCHAYAT_RESOLUTION_620 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPanchayatResolutionListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_PANCHAYAT_RESOLUTION_630 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPanchayatResolutionXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_PANCHAYAT_RESOLUTION_640 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPanchayatResolutionListXlxWithValidId|
|1.0| Download |ut_n_elx_GSTS_WEB_PANCHAYAT_RESOLUTION_650 |Download panchayat resolution attachment with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserDownloadPanchayatResolutionAttachmentWithValidId|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|-----------|
|1.0|Create|ut_n_c_GSTS_WEB_PANCHAYAT_RESOLUTION_160|Create Panchayat Resolution at State Level| N/A |Will not be Created|1|testNegCreatePanchayatResolutionAtStateLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_PANCHAYAT_RESOLUTION_165|Open Panchayat Resolution Create Form at State Level| N/A |Will not be Opened|1|testNegOpenPanchayatResolutionCreateFormAtStateLevel|
|1.0|Create|ut_n_c_GSTS_WEB_PANCHAYAT_RESOLUTION_170|Create Panchayat Resolution at District Level| N/A |Will not be Created|1|testNegCreatePanchayatResolutionAtDistLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_PANCHAYAT_RESOLUTION_175|Open Panchayat Resolution Create Form at District Level| N/A |Will not be Opened|1|testNegOpenPanchayatResolutionCreateFormAtDistrictLevel|
|1.0|Create|ut_n_c_GSTS_WEB_PANCHAYAT_RESOLUTION_180|Create Panchayat Resolution at Division Level| N/A |Will not be Created|1|testNegCreatePanchayatResolutionAtDivLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_PANCHAYAT_RESOLUTION_185|Open Panchayat Resolution Create Form at Division Level| N/A |Will not be Opened|1|testNegOpenPanchayatResolutionCreateFormAtDivLevel|
|1.0|Create|ut_n_c_GSTS_WEB_PANCHAYAT_RESOLUTION_190|Create Panchayat Resolution at Mandal Level| N/A |Will not be Created|1|testNegCreatePanchayatResolutionAtMandalLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_PANCHAYAT_RESOLUTION_195|Open Panchayat Resolution Create Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenPanchayatResolutionCreateFormAtMandalLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_281|Open Panchayat Resolution Remove Form at State Level| N/A |Will not be Opened|1|testNegOpenPanchayatResolutionRemoveFormAtStateLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_282|Remove Panchayat Resolution at State Level| N/A |Will not be Removed|1|testNegRemovePanchayatResolutionAtStateLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_283|Open Panchayat Resolution Remove Form at District Level| N/A |Will not be Opened|1|testNegOpenPanchayatResolutionRemoveFormAtDistLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_284|Remove Panchayat Resolution at District Level| N/A |Will not be Removed|1|testNegRemovePanchayatResolutionAtDistLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_285|Open Panchayat Resolution Remove Form at Division Level| N/A |Will not be Opened|1|testNegOpenPanchayatResolutionRemoveFormAtDivLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_286|Remove Panchayat Resolution at Division Level| N/A |Will not be Removed|1|testNegRemovePanchayatResolutionAtDivLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_287|Open Panchayat Resolution Remove Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenPanchayatResolutionRemoveFormAtMandalLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_288|Remove Panchayat Resolution at Mandal Level| N/A |Will not be Removed|1|testNegRemovePanchayatResolutionAtMandalLevel|
|1.0|View|ut_n_v_GSTS_WEB_PANCHAYAT_RESOLUTION_331|View Panchayat Resolution at State Level| N/A |Will not be Accessed|1|testNegViewPanchayatResolutionAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_PANCHAYAT_RESOLUTION_332|View Panchayat Resolution at District Level| N/A |Will not be Accessed|1|testNegViewPanchayatResolutionAtDistLevel|
|1.0|View|ut_n_v_GSTS_WEB_PANCHAYAT_RESOLUTION_333|View Panchayat Resolution at Division Level| N/A |Will not be Accessed|1|testNegViewPanchayatResolutionAtDivLevel|
|1.0|View|ut_n_v_GSTS_WEB_PANCHAYAT_RESOLUTION_334|View Panchayat Resolution at Mandal Level| N/A |Will not be Accessed|1|testNegViewPanchayatResolutionAtMandalLevel|
|1.0|List|ut_n_l_GSTS_WEB_PANCHAYAT_RESOLUTION_351|Get Panchayat Resolution List at State Level| N/A |Will not be Accessed|1|testNegPanchayatResolutionListAtStateLevel|
|1.0|List|ut_n_l_GSTS_WEB_PANCHAYAT_RESOLUTION_352|Get Panchayat Resolution List at District Level| N/A |Will not be Accessed|1|testNegPanchayatResolutionListAtDistLevel|
|1.0|List|ut_n_l_GSTS_WEB_PANCHAYAT_RESOLUTION_353|Get Panchayat Resolution List at Division Level| N/A |Will not be Accessed|1|testNegPanchayatResolutionListAtDivLevel|
|1.0|List|ut_n_l_GSTS_WEB_PANCHAYAT_RESOLUTION_354|Get Panchayat Resolution List at Mandal Level| N/A |Will not be Accessed|1|testNegPanchayatResolutionListAtMandalLevel|
|1.0|Search|ut_n_s_GSTS_WEB_PANCHAYAT_RESOLUTION_371|Search Panchayat Resolution  at State Level| N/A |Will not be Accessed|1|testNegSearchPanchayatResolutionAtStateLevel|
|1.0|Search|ut_n_s_GSTS_WEB_PANCHAYAT_RESOLUTION_372|Search Panchayat Resolution  at District Level| N/A |Will not be Accessed|1|testNegSearchPanchayatResolutionAtDistLevel|
|1.0|Search|ut_n_s_GSTS_WEB_PANCHAYAT_RESOLUTION_373|Search Panchayat Resolution  at Division Level| N/A |Will not be Accessed|1|testNegSearchPanchayatResolutionAtDivLevel|
|1.0|Search|ut_n_s_GSTS_WEB_PANCHAYAT_RESOLUTION_374|Search Panchayat Resolution  at Mandal Level| N/A |Will not be Accessed|1|testNegSearchPanchayatResolutionAtMandalLevel|
|1.0|Pdf|ut_n_p_GSTS_WEB_PANCHAYAT_RESOLUTION_601|Export Panchayat Resolution Pdf at State Level| N/A |Will not be exported|1|testNegExportPanchayatResolutionPdfAtStateLevel|
|1.0|List Pdf|ut_n_p_GSTS_WEB_PANCHAYAT_RESOLUTION_602|Export Panchayat Resolution List Pdf at State Level| N/A |Will not be exported|1|testNegExportPanchayatResolutionListPdfAtStateLevel|
|1.0|Xlx|ut_n_p_GSTS_WEB_PANCHAYAT_RESOLUTION_603|Export Panchayat Resolution Xlx at State Level| N/A |Will not be exported|1|testNegExportPanchayatResolutionXlxAtStateLevel|
|1.0|List Xlx|ut_n_p_GSTS_WEB_PANCHAYAT_RESOLUTION_604|Export Panchayat Resolution List Xlx at State Level| N/A |Will not be exported|1|testNegExportPanchayatResolutionListXlxAtStateLevel|
|1.0|Download|ut_n_p_GSTS_WEB_PANCHAYAT_RESOLUTION_605|Download Panchayat Resolution Attachment at State Level| N/A |Will not be downloaded|1|testNegDownloadPanchayatResolutionAttachmentAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_PANCHAYAT_RESOLUTION_660|Panchayat1112 user trying to access Panchayat1111 Panchayat Resolution which does not belongs to his context| N/A |Will not be accessed|1|testNegPanchayat1112UserAccessingPanchayat1111PanchayatResolution|
|1.0|Remove|ut_n_r_GSTS_WEB_PANCHAYAT_RESOLUTION_665|Panchayat1112 user trying to remove Panchayat1111 Panchayat Resolution which does not belongs to his context| N/A |Will not be removed|1|testNegPanchayat1112UserRemovingPanchayat1111PanchayatResolution|


## Security compliance check
1. Only user having the permission **ROLE_PANCHAYAT_RESOLUTION_VIEW** should view this functionality 
1. Only user having the permission **ROLE_PANCHAYAT_RESOLUTION_CREATE** should create this functionality 
1. Only user having the permission **ROLE_PANCHAYAT_RESOLUTION_REMOVE** should remove this functionality 
1. Only user having the permission **ROLE_PANCHAYAT_RESOLUTION_VIEW** should export this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Panchayat Resolution in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
