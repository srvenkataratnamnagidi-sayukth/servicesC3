---
title: Govt Orders
tags : ["Composing"]
---

## Introduction
Government orders are one of the features of this software product. Government Orders are rules, decisions, approvals which are released by government to make something official. Users will have access to government orders if they have permission, Otherwise will not access. 

## Business Assumptions
what type of users can create government orders should be planned at design phase.

## Requirements
### Functional Requirements
1. Only state level users can create government orders.
1. Only state level users can remove government orders.
1. Any level of user can view government orders if they have permission.
1. we can create and remove government orders at the state level only.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access govt orders.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Government orders contain information about all government orders which are released by government.

### Design 
1. Each govt order has name, description, code(government order number) and govt order copy.
1. Each govt order has unique code.
1. We can create, remove, view and export the government order.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_government_order_list|To view all the government orders. This listing page should bind to a permission|
|uc_government_order_create|To create the government order. This create page should bind to a permission|
|uc_government_order_remove|To remove the government order. This remove page should bind to a permission|
|uc_government_order_view|To view the government order. This view page should bind to a permission|
|uc_government_order_search|To search the government order. This search page should bind to a permission|
|uc_government_order_export|To export the government order in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9. space _-, minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|YES|YES|YES|YES||
|descr|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=256|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) NOT NULL|YES|YES|YES|YES|YES||
|code|YES|NA|a-zA-Z0-9, minlen=3, maxlen=32|@Column(name = "code", length = 32, nullable = false, unique = true)|code varchar(32) NOT NULL|YES|YES|YES|NO|NO||
|fileName|YES|NA|Attachment|@Column(name = "file_name", length = 64, nullable = false)|file_name varchar(64) NOT NULL|YES|NO|YES|YES|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS
No Enum Constants in govt orders.

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|GOVERNMENT_ORDER_VIEW|View|
|GOVERNMENT_ORDER_CREATE|Create|
|GOVERNMENT_ORDER_REMOVE|Remove|
|GOVERNMENT_ORDER_VIEW|Export|
|GOVERNMENT_ORDER_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_go__code (code)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_GOVERNMENT_ORDER_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_GOVERNMENT_ORDER_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_GOVERNMENT_ORDER_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_GOVERNMENT_ORDER_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

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
	GovtOrdersMenu((Govt Orders Menu))
	ListPage{Govt Orders List Page}
	CreatePage((Create Page))
	RemovePage((Remove Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->GovtOrdersMenu
    subgraph Menu
    GovtOrdersMenu
    end
    subgraph   
    GovtOrdersMenu-->ListPage
    ListPage--C-R-V-E-->ListPage
    end
    subgraph  
    GovtOrdersMenu--F-->ErrorPage
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
1. Only a user with the GOVERNMENT_ORDER_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant GovtOrdersListpage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        GovtOrdersListpage->>+Net: Check Internet, GET /app/ctx/GO/list ListPage
        Net--x-GovtOrdersListpage: F : Connection Error
        GovtOrdersListpage->>+cloud: S:  GET /app/ctx/GO/list ListPage
        cloud-->>-GovtOrdersListpage: RES:List Page
    end
    rect rgb(244,244,244)
        GovtOrdersListpage->>+Net: Check Internet, GET /app/GO/create/form CreateFormPage
        Net--x-GovtOrdersListpage: F : Connection Error
        GovtOrdersListpage->>+cloud: S : GET /app/GO/create/form CreateFormPage
        cloud-->>-GovtOrdersListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        GovtOrdersListpage->>+Net: Check Internet: POST /app/GO/create Create
        Net--x-GovtOrdersListpage: F : Connection Error
        GovtOrdersListpage->>+cloud: S : POST /app/GO/create Create
        cloud-->>-GovtOrdersListpage: RES: An Govt Order Successfully Created
    end
    rect rgb(244,244,244)
        GovtOrdersListpage->>+Net: Check Internet: GET /app/GO/remove/form RemoveFormPage
        Net--x-GovtOrdersListpage: F : Connection Error
        GovtOrdersListpage->>+cloud: S : GET /app/GO/remove/form RemoveFormPage
        cloud-->>-GovtOrdersListpage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        GovtOrdersListpage->>+Net: Check Internet: POST /app/GO/remove Remove
        Net--x-GovtOrdersListpage: F : Connection Error
        GovtOrdersListpage->>+cloud: S : POST /app/GO/remove Remove
        cloud-->>-GovtOrdersListpage: RES: An Govt Order Successfully Removed
    end
    rect rgb(244,244,244)
        GovtOrdersListpage->>+Net: Check Internet: GET /app/GO/view ViewPage
        Net--x-GovtOrdersListpage: F : Connection Error
        GovtOrdersListpage->>+cloud: GET /app/GO/view ViewPage
        cloud-->>-GovtOrdersListpage: RES: Govt Order View
    end
    rect rgb(244,244,244)
        GovtOrdersListpage->>+Net: Check Internet: GET /app/GO/exportPdf ExportPdf
        Net--x-GovtOrdersListpage: F : Connection Error 
        GovtOrdersListpage->>+cloud: GET /app/GO/exportPdf ExportPdf
        cloud-->>-GovtOrdersListpage: RES: Govt Order Pdf
    end
    rect rgb(244,244,244)
        GovtOrdersListpage->>+Net: Check Internet: GET /app/GO/exportListPdf ExportListPdf
        Net--x-GovtOrdersListpage: F : Connection Error
        GovtOrdersListpage->>+cloud: S : GET /app/GO/exportListPdf ExportListPdf
        cloud-->>-GovtOrdersListpage: RES: Govt Order List Pdf
    end
    rect rgb(244,244,244)
        GovtOrdersListpage->>+Net: Check Internet: GET /app/GO/exportXlx ExportXlx
        Net--x-GovtOrdersListpage: F : Connection Error
        GovtOrdersListpage->>+cloud: GET /app/GO/exportXlx ExportXlx
        cloud-->>-GovtOrdersListpage: RES: Govt Order Xlx
    end
    rect rgb(244,244,244)
        GovtOrdersListpage->>+Net: Check Internet: GET /app/GO/exportListXlx ExportListXlx
        Net--x-GovtOrdersListpage: F : Connection Error
        GovtOrdersListpage->>+cloud: S : GET /app/GO/exportListXlx ExportListXlx
        cloud-->>-GovtOrdersListpage: RES: Govt Order List Xlx
    end
    rect rgb(244,244,244)
        GovtOrdersListpage->>+Net: Check Internet: GET /app/GO/download DownloadCopy
        Net--x-GovtOrdersListpage: F : Connection Error
        GovtOrdersListpage->>+cloud: S : GET /app/GO/download DownloadCopy
        cloud-->>-GovtOrdersListpage: RES: Govt Order Copy
    end
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_WEB_GOVTORDER_103  ut_n_c_GSTS_WEB_GOVTORDER_104 ut_n_c_GSTS_WEB_GOVTORDER_106 ut_n_c_GSTS_WEB_GOVTORDER_107 ut_n_c_GSTS_WEB_GOVTORDER_108 ut_n_c_GSTS_WEB_GOVTORDER_109|**Positive Test Cases:** Creating Govt Order with Authorised User **Negative Test Cases:** 1.Creating Govt Order with Invalid Inputs 2.Creating GovtOrder without DB Connection 3.Creating Govt Order at Dist Level 4.Creating Govt Order at Div Level 5.Creating Govt Order at Mandal Level|**name:** 1.valid characters[a-zA-Z0-9 :_/-.\]2. length>3 and length<64  3.null **code:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null 4.unique key  **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null|3|9|12|testAuthorisedUserCreateGovtOrder, testAuthorisedUserCreateGovtOrderNegativeCases, testAuthorisedUserCreateGovtOrderWithoutDBConnection, testAuthorisedUserCreateGovtOrderAtDistLevel, testAuthorisedUserCreateGovtOrderAtDivLevel, testAuthorisedUserCreateGovtOrderAtMandalLevel|
|1.0| Create Form|ut_p_c_GSTS_WEB_GOVTORDER_100  ut_n_c_GSTS_WEB_GOVTORDER_101 |**Positive Test Cases:** Open Govt Order Create Form with Authorised User **Negative Test Cases:** 1.Open Govt Order Create Form with Panchayat Level User|N/A|1|1|2|testOpenCreateFormWithAuthorisedUser, testOpenCreateFormWithPanchayatLevelUser|
|1.0| Remove |ut_p_r_GSTS_WEB_GOVTORDER_207 ut_n_r_GSTS_WEB_GOVTORDER_205 ut_n_r_GSTS_WEB_GOVTORDER_206 ut_n_r_GSTS_WEB_GOVTORDER_208 ut_n_r_GSTS_WEB_GOVTORDER_209 ut_n_r_GSTS_WEB_GOVTORDER_211|**Positive Test Cases:** Removing Govt Order with Authorised User **Negative Test Cases:** 1.Removing Govt Order At Dist Level 2.Removing Govt Order Without DB Connection 3.Removing Govt Order by Passing Invalid Id 4.Removing Already Govt Order Obj with Authorised User| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|5|6|testAuthorisedUserRemoveGovtOrder, testAuthorisedUserRemoveGovtOrderAtDistLevel, testAuthorisedUserRemoveGovtOrderWithoutDBConnection, testAuthorisedUserRemoveGovtOrderNegativeCase, testAuthorisedUserRemoveGovtOrderWithInvalidId, testAuthorisedUserRemoveAlreadyRemovedGovtOrder|
|1.0| Remove Form|ut_p_r_GSTS_WEB_GOVTORDER_200 ut_n_r_GSTS_WEB_GOVTORDER_201 ut_n_r_GSTS_WEB_GOVTORDER_202 ut_n_r_GSTS_WEB_GOVTORDER_212 |**Positive Test Cases:** Open Govt Order Remove Form with Authorised User **Negative Test Cases:** 1.Open Govt Order Remove Form At District Level 2.Open Govt Order Remove Form Without DB Connection 3.Open Govt Order Remove Form with Invalid Id|1.Valid Id 2.Invalid Id|1|2|3|testAuthorisedUserOpenGovtOrderRemoveForm, testAuthorisedUserOpenGovtOrderRemoveFormAtDistLevel, testAuthorisedUserOpenGovtOrderRemoveFormWithoutDbConnection, testAuthorisedUserOpenGovtOrderRemoveFormWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_GOVTORDER_500 ut_n_r_GSTS_WEB_GOVTORDER_501 ut_n_r_GSTS_WEB_GOVTORDER_503|**Positive Test Cases:** View Govt Order with Valid Id  with Authorised User**Negative Test Cases:** 1.View Govt Order with Invalid ID with Authorised User 2.View Govt Order without DB Connection||1|2|3|testAuthorisedUserViewGovtOrderValidId, testAuthorisedUserViewGovtOrderInValidId, testAuthorisedUserViewGovtOrderWithoutDBConnection|
|1.0| Search |ut_p_s_GSTS_WEB_GOVTORDER_400 ut_n_s_GSTS_WEB_GOVTORDER_401 ut_n_s_GSTS_WEB_GOVTORDER_403 ut_n_s_GSTS_WEB_GOVTORDER_404 |**Positive Test Cases:** Search Govt Order with Authorised User **Negative Test Cases:** 1.Search Govt Order with Invalid Inputs 2.Search Govt Order without DB Connection 3.Search Govt Order with Invalid dates with Authorised User|  **name:** 1.valid characters[a-zA-Z0-9 :_/-.\]2. length>3 and length<64  3.null **code:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null 4.unique key  **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null|5|5|10|testAuthorisedUserSearchGovtOrder, testAuthorisedUserSearchGovtOrderNegativeCase, testAuthorisedUserSearchGovtOrderWithoutDbConnection, testAuthorisedUserSearchGoNegativeCase|
|1.0| List |ut_p_l_GSTS_WEB_GOVTORDER_300 ut_n_l_GSTS_WEB_GOVTORDER_301 |**Positive Test Cases:** Check the object list with valid data  with Authorised User **Negative Test Cases:** 1.Check the object list with Invalid data with Authorised User|Validating with unique field|1|1|2|testAuthorisedUserListGovtOrder, testAuthorisedUserListGovtOrderNegativeCase|
|1.0| PDF |ut_p_ep_GSTS_WEB_GOVTORDER_800 ut_n_ep_GSTS_WEB_GOVTORDER_805 ut_n_ep_GSTS_WEB_GOVTORDER_812 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|2|3|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId, testAuthorisedUserExportPdfWithoutDBConnection|
|1.0| List PDF |ut_p_elp_GSTS_WEB_GOVTORDER_801 ut_n_elp_GSTS_WEB_GOVTORDER_806 ut_n_elp_GSTS_WEB_GOVTORDER_813 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_GOVTORDER_802 ut_n_ex_GSTS_WEB_GOVTORDER_807 ut_n_ex_GSTS_WEB_GOVTORDER_814 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId, testAuthorisedUserExportXlxWithoutDBConnection|
|1.0| List XLX |ut_p_elx_GSTS_WEB_GOVTORDER_803 ut_n_elx_GSTS_WEB_GOVTORDER_808 ut_n_elx_GSTS_WEB_GOVTORDER_815 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_n_c_GSTS_WEB_GOVTORDER_105 |Unauthorised User does not have permission to create|  **name:** 1.valid characters[a-zA-Z0-9 :_/-.\]2. length>3 and length<64  3.null **code:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null 4.unique key  **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null|0|1|1|testUnAuthorisedUserCreateGovtOrder|
|1.0|Update|N/A| N/A | N/A |N/A|N/A|N/A|
|1.0| Remove |ut_n_r_GSTS_WEB_GOVTORDER_210|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserRemoveGovtOrder|
|1.0| Remove Form|ut_n_r_GSTS_WEB_GOVTORDER_203|Open Govt Order Remove Form With UnAuthorised user|1.Valid Id|0|1|1|testUnAuthorisedUserOpenGovtOrderRemoveForm|
|1.0| View |ut_n_v_GSTS_WEB_GOVTORDER_502|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testUnAuthorisedUserViewGovtOrder|
|1.0| Search |ut_n_s_GSTS_WEB_GOVTORDER_402|Unauthorised User does not have permission to search|  **name:** 1.valid characters[a-zA-Z0-9 :_/-.\]2. length>3 and length<64  3.null **code:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null 4.unique key  **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null|0|1|1|testUnAuthorisedUserSearchGovtOrder|
|1.0| List |ut_n_l_GSTS_WEB_GOVTORDER_302|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testUnAuthorisedUserListGovtOrder|
|1.0| PDF |ut_n_ep_GSTS_WEB_GOVTORDER_808 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_GOVTORDER_809 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_GOVTORDER_810 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_GOVTORDER_811 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListXlx|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|-----------|
|1.0|Create|ut_n_c_GSTS_WEB_GOVTORDER_601| Create GovtOrder at Panchayat Level with Authorised User| N/A |Will not be Created|1|testAuthorisedPanchayatLevelUserCreateGovtOrder|
|1.0|Create|ut_n_c_GSTS_WEB_GOVTORDER_602| Create GovtOrder at State Level with Panchayat Level Authorised User| N/A |Will not be Created|1|testAuthorisedPanchayatLevelUserCreateGovtOrderStateLevel|
|1.0|List|ut_n_l_GSTS_WEB_GOVTORDER_600| Check the object list with state level data at panchayat level with Authorised User| N/A |Will not be Created|1|testAuthorisedPanchayatLevelUserListGovtOrder|

## Security compliance check
1. Only user having the permission **ROLE_GOVERNMENT_ORDER_VIEW** should view this functionality 
1. Only user having the permission **ROLE_GOVERNMENT_ORDER_CREATE** should create this functionality 
1. Only user having the permission **ROLE_GOVERNMENT_ORDER_REMOVE** should remove this functionality 
1. Only user having the permission **ROLE_GOVERNMENT_ORDER_VIEW** should export this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Government Orders in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
