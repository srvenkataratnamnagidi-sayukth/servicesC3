---
title: GS0002 - Feature Permission Management
tags : ["Composing"]
---

## Introduction
Feature Permissions are one of the basic building blocks of the software product. Product can be used by different users at various levels of the organization.
Each Product Feature we are developing should be bind to a **PERMISSION** that way  it will be accessible to the user binded to that **PERMISSION**.   

## Business Assumptions
Product Features should be planned at the design phase and no updates to the permissions at the run time. 

## Requirements
### Functional Requirements
1. The name of the permision should not start with 'ROLE_' because the Spring Security will add the prefix 'ROLE_' to the permission name. Please refer the file 'com.shadkona.gramsevak.auth.app.UserAuthService' for more details.
1. Use the [Spring Security](https://spring.io/projects/spring-security) constructs to provide access to the functionality in the JSP and JAVA files
1. While using the permission name in the JSP pages as **hasAnyRole('ROLE_<permission_name>')** or ServiceLayer page as **@PreAuthorize("hasAnyRole('ROLE_<permission_name>')")** make sure the prefix "ROLE_" along with the role name.

### Non-functional Requirements
1. System can support any number of permissions but this design will limit 1000 permissions for this system. Beyond the 1000 permissions the system may experience performance issues. 
If there are none which are specific to this design (i.e. the requirements are the same as those for the system), then this section can simply state: "Nothing specific to this design noted."

### Problem Statement
Feature permissions are required to provide access to each product feature for all the logged in users based on the permission(s) binded to the user. 

### Design 
1. Each product feature have name and display name
1. Insert the product feature in the Database directly. We should not have options to Create and Update the product permission

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_user_permission_list|To view all the user/feature permission|
|uc_user_permission_search|To search the user/feature permission|
|uc_user_permission_view|To view the user/feature permission|
|uc_user_permission_export|To export the user/feature permission in 2 formats Excel, PDF|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9, maxlen=64|@Column(name = "name", length = 64, unique = true, nullable = false)|name varchar(64) not null|NA|NA|NA|YES|YES|YES||
|code|YES|NA|a-zA-Z0-9, maxlen=32|@Column(name = "code", length = 32, unique = true, nullable = false)|code varchar(32) not null|NA|NA|NA|YES|YES|NO||
|descr|YES|NA|a-zA-Z0-9, maxlen=128|@Column(name = "descr", length = 128, unique = true, nullable = false)|descr varchar(128) not null|NA|NA|NA|NO|YES|YES||
|groupName|YES|NA|a-zA-Z0-9, maxlen=32|@Column(name = "group_name", length = 32, unique = true, nullable = false)|group_name varchar(32) not null|NA|NA|NA|YES|YES|NO||

#### ENUM CONSTANTS
No Enum Constants in Feature Permission.

#### Feature Permission
This is an exception only for this topic, **Feature Permissions** controlling itself.

|Permission code|Action|
|---------------|-------|
|USER_PERMISSION_VIEW|View|
|USER_PERMISSION_VIEW|List|
|USER_PERMISSION_VIEW|Export|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|AC_ROLE_PERMISSION_VIEW|Only user having this permission should view this functionality|
|AC_ROLE_PERMISSION_VIEW|Only user having this permission should export the user role in 2 formats Excel, PDF|

## User Experience
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="center">}}
flowchart TD 
	UserPermissionMenu((User Permission Menu))
	ListPage{Permission List Page}
	ErrorPage((ErrorPage))
	ViewPage((ViewPage))
	DownloadFile>Save File On Disk]
	Stop((Stop))
	Start((Start))
	Start-->UserPermissionMenu
	subgraph Menu
	UserPermissionMenu
	end
	subgraph List
	UserPermissionMenu-->ListPage
	ListPage--V-E-->ListPage
	end
	subgraph Error
	UserPermissionMenu-->ErrorPage
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
	%%For Success Representation
	linkStyle 1 stroke:green,stroke-width:2px;
	linkStyle 5 stroke:green,stroke-width:2px;
	linkStyle 6 stroke:green,stroke-width:2px;
	linkStyle 8 stroke:green,stroke-width:2px;
	%%For Failure Representation
	linkStyle 2 stroke:red,stroke-width:2px;
	linkStyle 3 stroke:red,stroke-width:2px;
	linkStyle 7 stroke:red,stroke-width:2px;
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|V|View|
|E|Export|
|B|Back|
|F|Failure|
|VE|View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Sequence Diagram
1. Only a user with the USER_PERMISSION_VIEW permission will be allowed to perform the below operations.

{{<mermaid align="center">}}
sequenceDiagram
    participant UserPermissionListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        UserPermissionListPage->>+Net: Check Internet, GET /app/ctx/UserPermission/list ListPage
        Net--x-UserPermissionListPage: F : Connection Error
        UserPermissionListPage->>+cloud: S:  GET /app/ctx/UserPermission/list ListPage
        cloud-->>-UserPermissionListPage: RES:List Page
    end
    rect rgb(244,244,244)
        UserPermissionListPage->>+Net: Check Internet, GET /app/UserPermission/view ViewPage
        Net--x-UserPermissionListPage: F : Connection Error
        UserPermissionListPage->>+cloud: S : GET /app/UserPermission/view ViewPage
        cloud-->>-UserPermissionListPage: RES: userPermission View
    end
    rect rgb(244,244,244)
        UserPermissionListPage->>+Net: Check Internet, GET /app/UserPermission/exportPdf ExportPdf
        Net--x-UserPermissionListPage: F : Connection Error
        UserPermissionListPage->>+cloud: S : GET /app/UserPermission/exportPdf ExportPdf
        cloud-->>-UserPermissionListPage: RES: userPermission Pdf
    end
    rect rgb(244,244,244)
        UserPermissionListPage->>+Net: Check Internet, GET /app/UserPermission/exportListPdf ExportListPdf
        Net--x-UserPermissionListPage: F : Connection Error
        UserPermissionListPage->>+cloud: S : GET /app/UserPermission/exportListPdf ExportListPdf
        cloud-->>-UserPermissionListPage: RES: userPermission List Pdf
    end
    rect rgb(244,244,244)
        UserPermissionListPage->>+Net: Check Internet, GET /app/UserPermission/exportXlx ExportXlx
        Net--x-UserPermissionListPage: F : Connection Error
        UserPermissionListPage->>+cloud: S : GET /app/UserPermission/exportXlx ExportXlx
        cloud-->>-UserPermissionListPage: RES: userPermission Xlx
    end
    rect rgb(244,244,244)
        UserPermissionListPage->>+Net: Check Internet, GET /app/UserPermission/exportListXlx ExportListXlx
        Net--x-UserPermissionListPage: F : Connection Error
        UserPermissionListPage->>+cloud: S : GET /app/UserPermission/exportListXlx ExportListXlx
        cloud-->>-UserPermissionListPage: RES: userPermission List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0|View|ut_p_v_GSTS_WEB_USERPERMISSION_100 ut_p_v_GSTS_WEB_USERPERMISSION_104 ut_p_v_GSTS_WEB_USERPERMISSION_105 ut_p_v_GSTS_WEB_USERPERMISSION_106 ut_p_v_GSTS_WEB_USERPERMISSION_107 ut_n_v_GSTS_WEB_USERPERMISSION_101 ut_n_v_GSTS_WEB_USERPERMISSION_103|**Positive Test Cases:** 1.View UserPermission with valid Id with Authorized User  2.View UserPermission at District level with Authorized User 3.View UserPermission at Division level with Authorized User 4.View UserPermission at Mandal level with Authorized User 5.View UserPermission at Panchayat level with Authorised User **Negative Test Cases:** 1.View UserPermission with Invalid Id with Authorized User 2.View UserPermission without DB Connection|1.Valid Id 2.Invalid Id|4|2|6|testAuthorisedUserViewUserPermissionValidId, testAuthorisedUserViewUserPermissionInValidId, testAuthorisedUserViewUserPermissionWithoutDBConnection, testAuthorisedUserViewUserPermissionValidIdAtDistrictLevel, testAuthorisedUserViewUserPermissionValidIdAtDivLevel, testAuthorisedUserViewUserPermissionValidIdAtMandalLevel, testAuthorisedUserViewUserPermissionValidIdAtPanchayatLevel|
|1.0| Search |ut_p_s_GSTS_WEB_USERPERMISSION_200 ut_n_s_GSTS_WEB_USERPERMISSION_201 ut_n_s_GSTS_WEB_USERPERMISSION_203|**Positive Test Cases:** 1.Search UserPermission with Valid input with Authorised User **Negative Test Cases:** 1.Search UserPermission with Invalid inputs 2.Search UserPermission without DB Connection with Authorised User|N/A|4|3|7|testAuthorisedUserSearchUserPermission, testAuthorisedUserSearchUserPermissionNegativeCase, testAuthorisedUserSearchUserPermissionWithoutDBConnection|
|1.0| List |ut_p_l_GSTS_WEB_USERPERMISSION_300 ut_n_l_GSTS_WEB_USERPERMISSION_301 ut_n_l_GSTS_WEB_USERPERMISSION_303 |**Positive Test Cases:** Check the object list with Valid data with Authorised User  **Negative Test Cases:** 1.Check the object list with InValid data with Authorised User 2.Check the object list with Valid data without DB Connection with Authorised User|N/A|5|6|11|testAuthorisedUserUserPermissionList, testAuthorisedUserUserPermissionListNegativeTestCase, testAuthorisedUserUserPermissionListWithoutDBConnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_USERPERMISSION_400 ut_n_ep_GSTS_WEB_USERPERMISSION_401 ut_n_ep_GSTS_WEB_USERPERMISSION_412 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|2|3|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId, testAuthorisedUserExportPdfWithoutDBConnection|
|1.0| List PDF |ut_p_elp_GSTS_WEB_USERPERMISSION_402 ut_n_elp_GSTS_WEB_USERPERMISSION_403 ut_n_elp_GSTS_WEB_USERPERMISSION_413 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_USERPERMISSION_404 ut_n_ex_GSTS_WEB_USERPERMISSION_405 ut_n_ex_GSTS_WEB_USERPERMISSION_414 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId, testAuthorisedUserExportXlxWithoutDBConnection|
|1.0| List XLX |ut_p_elx_GSTS_WEB_USERPERMISSION_406 ut_n_elx_GSTS_WEB_USERPERMISSION_407 ut_n_elx_GSTS_WEB_USERPERMISSION_415 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### UnAuthorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0|View|ut_n_v_GSTS_WEB_USERPERMISSION_102|View UserPermission with Unauthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserViewUserPermission|
|1.0|Search|ut_n_s_GSTS_WEB_USERPERMISSION_202|Search UserPermission with Unauthorised User|N/A|0|1|1|testUnAuthorisedUserSearchUserPermission|
|1.0|List|ut_n_l_GSTS_WEB_USERPERMISSION_302|Check the object list with Valid data with UnAuthorised User|N/A|0|1|1|testUnAuthorisedUserUserPermissionList|
|1.0| PDF |ut_n_ep_GSTS_WEB_USERPERMISSION_408 |Export List Pdf with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_USERPERMISSION_409 |Export Pdf with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_USERPERMISSION_410 |Export XLX with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_USERPERMISSION_411 |Export List XLX with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserExportListXlx|

## Security compliance check
1. Only user having the permission ROLE_PERMISSION_VIEW should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the USER PERMISSIONs in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
