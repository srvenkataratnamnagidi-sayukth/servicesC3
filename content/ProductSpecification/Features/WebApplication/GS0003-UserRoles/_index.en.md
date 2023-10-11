---
title: GS0003 - User Roles
tags : ["Composing"]
---

## Introduction
User Roles are one of the basic building blocks of the software product. The product can be used by different users at various levels of the organization. Each and every user role is a combination of one or more user permission(s). Based on user position, a user role will bind to the user that way user can access the feature.

Security is key for the project. If a project failed to maintain security, project data will be easily manipulated and it leads to project failure. User roles provide a way to increase security to the project by providing a specific role to the user and restricting the user to access product features that do not have permission to the user.

## Business Assumptions
User roles should be planned at the launching phase and updates to the user roles at the run time based on the requirement.

## Requirements
### Functional Requirements
User role is a combination of one or more user permission(s). Each Product Feature bound to a **PERMISSION**, If the logged-in user has a role with that permission then the user can access the Product Feature otherwise the user is not allowed to access the Product Feature.

### Non-functional Requirements
Each and every user has a minimum of one user role. Based on **[Personas of users](http://localhost:1313/#personas-of-users)**, user roles are bound to the user.  

### Problem Statement
User roles are required to provide access to each product feature for all the logged in users based on the user role(s) bound to the user.

### Design 
1. Each User role has a name, description, organization type, and user permission(s).
1. We can Create, Update, View, and remove the user role.
1. One user role should be inserted manually to provide access to each product feature for admin user.
1. Only one user role is allowed with the same name.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|
|Feature Permission|[gs0002-featurepermissionmanagement]({{< ref "gs0002-featurepermissionmanagement" >}})|Feature Permission Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_user_role_create|To create the user role|
|uc_user_role_update|To update the user role|
|uc_user_role_remove|To remove the user role|
|uc_user_role_view|To view the user role|
|uc_user_role_list|To view all the user roles|
|uc_user_role_search|To search the user role|
|uc_user_role_export|To export the user role in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9. _-,minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false, unique = true)|name varchar(64) not null|YES|YES|YES|YES|YES|YES||
|descr|YES|NA|a-zA-Z0-9/:#, _.-[]()@, minlen=6, maxlen=256|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) not null|YES|YES|YES|YES|YES|YES||
|orgType|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "org_type", length = 64, nullable = false)|org_type varchar(64) not null|YES|NO|YES|YES|YES|YES||
|permissionSet|YES|NA||@ManyToMany(fetch = FetchType.LAZY) @JoinTable(name = "gs_user_role_permission_map", joinColumns ={@JoinColumn(name = "role_id", nullable = false) }, inverseJoinColumns = {@JoinColumn(name = "permission_id", nullable = false) }, uniqueConstraints =@UniqueConstraint(columnNames = {"role_id", "permission_id"}))||YES|YES|YES|YES|NO|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Org Type

{{<mermaid align="left">}}
classDiagram
    class OrgType{
      STATE
      DISTRICT
      DIVISION
      MANDAL
      PANCHAYAT
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|USER_ROLE_CREATE|Create|
|USER_ROLE_UPDATE|Update|
|USER_ROLE_REMOVE|Remove|
|USER_ROLE_VIEW|View|
|USER_ROLE_VIEW|List|
|USER_ROLE_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_user_role__name (name)|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|AC_ROLE_USER_ROLE_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_USER_ROLE_UPDATE|Only user having the user role with this permission should update this functionality|
|AC_ROLE_USER_ROLE_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_USER_ROLE_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_USER_ROLE_VIEW|Only user having the user role with this permission should export the user role in 2 formats Excel, PDF|

## User Experience
1. Create page based on the standard UX Listing Template
1. Update page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreteBtn[Create]---UpdateBtn[Update]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}


### State Machine
{{<mermaid align="left">}}
flowchart TD
	UserRoleMenu((User Roles Menu))
	ListPage{User Roles List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->UserRoleMenu
    subgraph Menu
    UserRoleMenu
	end
	subgraph List
	UserRoleMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	UserRoleMenu-->ErrorPage
	ErrorPage-->Stop
	end
	subgraph Create
	ListPage--C-->CreatePage
	CreatePage--SB-->ListPage
	CreatePage--SB-->CreatePage
	end
	subgraph Update
	ListPage--U-->UpdatePage
	UpdatePage--SB-->ListPage
	UpdatePage--SB-->UpdatePage
	end
	subgraph View
	ListPage--V-->ViewPage
	ViewPage--SB-->ListPage
	ViewPage--SB-->ViewPage
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
    linkStyle 15 stroke:green,stroke-width:2px;
    linkStyle 17 stroke:green,stroke-width:2px;    
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;
    linkStyle 13 stroke:red,stroke-width:2px;
    linkStyle 16 stroke:red,stroke-width:2px;
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|C|Create|
|U|Update|
|R|Remove|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|F|Failure|
|SB|Submit or Back|
|VE|View or Export|
|C-U-R-V-E|Create or Update or Remove or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram
1. Only a user with the USER_ROLE_VIEW permission will be allowed to perform the below operations.

{{<mermaid align="center">}}
sequenceDiagram
    participant UserRoleListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet, GET /app/ctx/UserRole/list ListPage
        Net--x-UserRoleListPage: F : Connection Error
        UserRoleListPage->>+cloud: S:  GET /app/ctx/UserRole/list ListPage
        cloud-->>-UserRoleListPage: RES:List Page
    end
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet, GET /app/UserRole/create/form CreateFormPage
        Net--x-UserRoleListPage: F : Connection Error
        UserRoleListPage->>+cloud: S : GET /app/UserRole/create/form CreateFormPage
        cloud-->>-UserRoleListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet: POST /app/UserRole/create Create
        Net--x-UserRoleListPage: F : Connection Error
        UserRoleListPage->>+cloud: S : POST /app/UserRole/create Create
        cloud-->>-UserRoleListPage: RES: An User Role Successfully Created
    end
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet: GET /app/UserRole/update/form UpdateFormPage
        Net--x-UserRoleListPage: F : Connection Error
        alt
        note right of Net:  UserRole Cache Object Found
        UserRoleListPage->>+Cache: S : GET /app/UserRole/update/form UpdateFormPage
        Cache-->>-UserRoleListPage: RES: Update Form Loaded
        else
		note right of Net:  UserRole Cache Object Not Found
        Cache->>+cloud: GET /app/UserRole/update/form UpdateFormPage
        cloud-->>-UserRoleListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet: POST /app/UserRole/update update
        Net--x-UserRoleListPage: F : Connection Error
        UserRoleListPage->>+cloud: S : POST /app/UserRole/update Update
        cloud-->>-UserRoleListPage: RES: An User Role Successfully Updated
    end
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet: GET /app/UserRole/remove/form RemoveFormPage
        Net--x-UserRoleListPage: F : Connection Error
        UserRoleListPage->>+cloud: S : GET /app/UserRole/remove/form RemoveFormPage
        cloud-->>-UserRoleListPage: Response : Remove Form Loaded
    end
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet: POST /app/UserRole/remove Remove
        Net--x-UserRoleListPage: F : Connection Error
        UserRoleListPage->>+cloud: S : POST /app/UserRole/remove Remove
        cloud-->>-UserRoleListPage: RES: An User Role Successfully Removed
    end
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet: GET /app/UserRole/view ViewPage
        Net--x-UserRoleListPage: F : Connection Error
        alt
		note right of Net:  UserRole Cache Object Found
        UserRoleListPage->>+Cache: S : GET /app/UserRole/view ViewPage
        Cache-->>-UserRoleListPage: RES: userRole View
        else
		note right of Net:  UserRole Cache Object Not Found
        Cache->>+cloud: GET /app/UserRole/view ViewPage
        cloud-->>-UserRoleListPage: RES: userRole View
        end
    end
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet: GET /app/UserRole/exportPdf ExportPdf
        Net--x-UserRoleListPage: F : Connection Error
        alt
		note right of Net:  UserRole Cache Object Found
        UserRoleListPage->>+Cache: S : GET /app/UserRole/exportPdf ExportPdf
        Cache-->>-UserRoleListPage: RES: userRole Pdf
        else
		note right of Net:  UserRole Cache Object Not Found
        Cache->>+cloud: GET /app/UserRole/exportPdf ExportPdf
        cloud-->>-UserRoleListPage: RES: userRole Pdf
        end
    end
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet: GET /app/UserRole/exportListPdf ExportListPdf
        Net--x-UserRoleListPage: F : Connection Error
        UserRoleListPage->>+cloud: S : GET /app/UserRole/exportListPdf ExportListPdf
        cloud-->>-UserRoleListPage: RES: userRole List Pdf
    end
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet: GET /app/UserRole/exportXlx ExportXlx
        Net--x-UserRoleListPage: F : Connection Error
        alt
		note right of Net:  UserRole Cache Object Found
        UserRoleListPage->>+Cache: S : GET /app/UserRole/exportXlx ExportXlx
        Cache-->>-UserRoleListPage: RES: userRole Xlx
        else
		note right of Net:  UserRole Cache Object Not Found
        Cache->>+cloud: GET /app/UserRole/exportXlx ExportXlx
        cloud-->>-UserRoleListPage: RES: userRole Xlx
        end
    end
    rect rgb(244,244,244)
        UserRoleListPage->>+Net: Check Internet: GET /app/UserRole/exportListXlx ExportListXlx
        Net--x-UserRoleListPage: F : Connection Error
        UserRoleListPage->>+cloud: S : GET /app/UserRole/exportListXlx ExportListXlx
        cloud-->>-UserRoleListPage: RES: userRole List Xlx
    end
    
          
{{< /mermaid >}}


## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------|--------|
|1.0| Create Form |ut_p_c_GSTS_WEB_USER_ROLE_200 ut_n_c_GSTS_WEB_USER_ROLE_210 |**Positive Test Cases:** 1.Open User Role Create Form **Negative Test Cases:** 1.Open User Role Create Form without DB connection|-|1|1|2|testPosOpenUserRoleCreateFormWithAuthorisedUser,  testNegOpenUserRoleCreateFormWithoutDBconnection|
|1.0| Create |ut_p_c_GSTS_WEB_USERROLE_230  ut_n_c_GSTS_WEB_USERROLE_240 ut_n_c_GSTS_WEB_USERROLE_220 ut_n_c_GSTS_WEB_USERROLE_250 |**Positive Test Cases:** Creating User Role with State level Authorised User **Negative Test Cases:** 1.Create User Role with Invalid inputs with State Level Authorised User 2.Create User Role without db connection 3.Create User Role with invalid permission Id| **name:** 1.valid characters 2. length>=3 and length<=64 3.null 4.unique **orgType:** enums **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2.length>=6 and length<=256 3.null|5|5|10|testPosAuthorisedStateLevelUserCreateUserRoleWithValidInputs,  testNegAuthorisedStateLevelUserCreateUserRoleWithInValidInputs,  testNegCreateStateUserRoleWithoutDBconnection,  testNegAuthorisedStateLevelUserCreateUserRoleWithInvalidPermissionId|
|1.0| Update Form |ut_p_u_GSTS_WEB_USER_ROLE_330   ut_n_u_GSTS_WEB_USER_ROLE_340   ut_n_u_GSTS_WEB_USER_ROLE_350|**Positive Test Cases:** Open User Role update form with valid Id with Authorised Panchayat level user    **Negative Test Cases:**  1.Open VUser Role update  Without DB Connection 2. Open User Role update Form with Invalid id|Id|1|2|3|testPosAuthorisedStateLevelUserOpenUserRoleUpdateFormWithValidId,  testNegAuthorisedStateLevelUserOpenUserRoleUpdateFormWithoutDbConnection,  testNegAuthorisedStateLevelUserOpenUserRoleUpdateFormWithInValidId|
|1.0| Update |ut_p_u_GSTS_WEB_USERROLE_360  ut_n_u_GSTS_WEB_USERROLE_370 ut_n_u_GSTS_WEB_USERROLE_380 ut_n_u_GSTS_WEB_USERROLE_390 ut_n_u_GSTS_WEB_USERROLE_400 ut_n_u_GSTS_WEB_USERROLE_560 |**Positive Test Cases:** 1. Update User Role with valid inputs with State Level Authorised User **Negative Test Cases:** 1.Updating User Role with invalid inputs 2.Update User Role with Invalid Permission Id 3.Update User Role without db connection 4.Update User Role with invalid id  5.Update removed user role | **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=6 and length<=256 3.null **updateComment:** 1.valid characters 2. length>=6 and length<=255 3.null|1|5|6|testPosStateLevelAuthorisedUserUpdateUserRoleWithValidInputs, testNegStateLevelAuthorisedUserUpdateUserRoleWithInValidInputs, testNegStateLevelAuthorisedUserUpdateUserRole,  testNegStateLevelAuthorisedUserUpdateUserRoleWithInvalidPermissionId,  testNegStateLevelAuthorisedUserUpdateUserRoleWithoutDBconnection,  testNegStateLevelAuthorisedUserUpdateUserRoleWithInvalidId,  testNegSLAuthorisedUserUpdatedRemovedUserRole|
|1.0| Remove Form |ut_p_r_GSTS_WEB_USER_ROLE_470   ut_n_r_GSTS_WEB_USER_ROLE_480   ut_n_r_GSTS_WEB_USER_ROLE_490  ut_n_r_GSTS_WEB_USER_ROLE_550|**Positive Test Cases:** Open User Role remove form with valid Id   **Negative Test Cases:**  1.Open User Role remove Form Without DB Connection 2. Open User Role remove Form with Invalid id   3.Open User Role remove form with Already removed User Role Id with Authorised user|Id|1|3|4|testPosAuthorisedStateLevelUserOpenUserRoleRemoveFormWithValidId,  testNegAuthorisedStateLevelUserOpenUserRoleRemoveFormWithoutDbConnection,  testNegAuthorisedStateLevelUserOpenUserRoleRemoveFormWithInValidId,  testNegAuthorisedSLUserOpenUserRoleRemoveFormWithAlreadyRemovedURId|
|1.0| Remove |ut_p_r_GSTS_WEB_USERROLE_500  ut_n_r_GSTS_WEB_USERROLE_510 ut_n_r_GSTS_WEB_USERROLE_530 ut_n_r_GSTS_WEB_USERROLE_540 ut_n_r_GSTS_WEB_USERROLE_570 |**Positive Test Cases:** 1. Remove User Role with Valid Remove Comment with State Level Authorised User  **Negative Test Cases:** 1.Removing User Role with invalid remove comment 2.Remove User Role without db connection 3.Remove already removed user role 4.Remove User Role with Invalid Id| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |1|4|5|testPosStateLevelAuthorisedUserRemoveUserRoleWithValidRemoveCommentAndValidId,  testNegStateLevelAuthorisedUserRemoveUserRoleWithInValidRemoveCommentAndValidId,  testNegSLAuthorisedUserRemoveUserRoleWithoutDbConnection,  testNegSLAuthorisedUserRemoveAlreadyRemovedUserRole,  testNegStateLevelAuthorisedUserRemoveUserRoleInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_USERROLE_600  ut_n_v_GSTS_WEB_USERROLE_610 ut_n_v_GSTS_WEB_USERROLE_620 |**Positive Test Cases:** View User Role with Valid Id  with Authorised User **Negative Test Cases:** 1. View User Role without DB Connection 2.View User Role with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewUserRoleValidId,  testNegAuthorisedUserViewUserRoleWithoutDbConnection,  testNegAuthorisedUserViewUserRolewithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_USERROLE_670  ut_n_s_GSTS_WEB_USERROLE_680 ut_n_s_GSTS_WEB_USERROLE_690 |**Positive Test Cases:** Search User Role with valid inputs **Negative Test Cases:** 1.Search User Role without db connection 2.Search User Role with invalid inputs| **name:** 1.valid characters 2. length>=3 and length<=64 3.null **orgType:** enums **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2.length>=6 and length<=256 3.null|1|2|3|testPosAuthorisedUserSearchUserRoleWithValidInputs,  testNegAuthorisedUserSearchUserRoleWithoutDBconnection,  testNegAuthorisedUserSearchUserRoleWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_USERROLE_640 ut_n_l_GSTS_WEB_USERROLE_650|**Positive Test Cases:** Get User Role List with Authorised User **Negative Test Cases:** Get User Role List without db connection|Validating with unique field|1|1|2|testPosAuthorisedUserGetUserRoleList,  testNegAuthorisedUserGetUserRoleListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_USER_ROLE_710   ut_n_ep_GSTS_WEB_USER_ROLE_720   ut_n_ep_GSTS_WEB_USER_ROLE_730 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportUserRolePdfWithValidId,  testNegAuthorisedUserExportUserRolePdfwithoutDbconnection,  testNegAuthorisedUserExportUserRolePdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_USER_ROLE_740   ut_n_elp_GSTS_WEB_USER_ROLE_750   ut_n_elp_GSTS_WEB_USER_ROLE_760 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportUserRoleListPdfWithValidId,  testNegAuthorisedUserExportUserRoleListPdfwithoutDbconnection,  testNegAuthorisedUserExportUserRoleListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_USER_ROLE_790   ut_n_ex_GSTS_WEB_USER_ROLE_800   ut_n_ex_GSTS_WEB_USER_ROLE_810 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportUserRoleXlxValidId,  testNegAuthorisedUserExportUserRoleXlxwithoutDbconnection,  testNegAuthorisedUserExportUserRoleXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_USER_ROLE_820   ut_n_elx_GSTS_WEB_USER_ROLE_830   ut_n_elx_GSTS_WEB_USER_ROLE_840 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportUserRoleListXlxValidId,  testNegAuthorisedUserExportUserRoleListXlxwithoutDbconnection,  testNegAuthorisedUserExportUserRoleListXlxInValidId|


#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------------|-----|
|1.0| Create Form|ut_n_c_GSTS_WEB_USER_ROLE_310|Unauthorised User opening User Role create form||0|1|1|testNegOpenUserRoleCreateFormWithUnAuthorisedUser|
|1.0| Create |ut_n_c_GSTS_WEB_USERROLE_320 |Unauthorised User does not have permission to create| **name:** 1.valid characters 2. length>=3 and length<=64 3.null 4.unique **orgType:** enums **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2.length>=6 and length<=256 3.null|0|1|1|testNegUnAuthorisedUserCreateUserRole|
|1.0| Update Form|ut_n_u_GSTS_WEB_USER_ROLE_460|Unauthorised User opening User Role update form||0|1|1|testNegUnAuthorisedStateLevelUserOpenUserRoleUpdateForm|
|1.0| Update |ut_n_u_GSTS_WEB_USERROLE_450|Unauthorised User does not have permission to update| **descr:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=6 and length<=256 3.null **updateComment:** 1.valid characters 2. length>=6 and length<=255 3.null|0|1|1|testNegUnAuthorisedUserUpdateUserRole|
|1.0| Remove Form|ut_n_r_GSTS_WEB_USER_ROLE_580|Unauthorised User opening User Role remove form||0|1|1|testNegUnAuthorisedStateLevelUserOpenUserRoleRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_USERROLE_590|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserRemoveUserRole|
|1.0| View |ut_n_v_GSTS_WEB_USERROLE_630|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewUserRole|
|1.0| Search |ut_n_s_GSTS_WEB_USERROLE_700|Unauthorised User does not have permission to search| **name:** 1.valid characters 2. length>=3 and length<=64 3.null **orgType:** enums **descr:** 1.valid characters 2.length>=6 and length<=256 3.null|0|1|1|testNegUnAuthorisedUserSearchUserRole|
|1.0| List |ut_n_l_GSTS_WEB_USERROLE_660|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserGetUserRoleList|
|1.0| PDF |ut_n_ep_GSTS_WEB_USER_ROLE_850 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportUserRolePdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_USER_ROLE_890 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportUserRoleListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_USER_ROLE_900 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportUserRoleXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_USER_ROLE_910 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportUserRoleListXlxWithValidId|


#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|----------|
|1.0|Create|ut_p_c_GSTS_WEB_USER_ROLE_270|Create User Role with Authorised District Level User| N/A |Will be Created|1|testPosAuthorisedDistLevelUserCreateUserRole|
|1.0|Create|ut_p_c_GSTS_WEB_USER_ROLE_280|Create User Role with Authorised Division Level User| N/A |Will be Created|1|testPosAuthorisedDivLevelUserCreateUserRole|
|1.0|Create|ut_p_c_GSTS_WEB_USER_ROLE_290|Create User Role with Authorised Mandal Level User| N/A |Will be Created|1|testPosAuthorisedMandalLevelUserCreateUserRole|
|1.0|Create|ut_p_c_GSTS_WEB_USER_ROLE_300|Create User Role with Authorised Panchayat Level User| N/A |Will be Created|1|testPosAuthorisedPanLevelUserCreateUserRole|
|1.0|Update|ut_p_u_GSTS_WEB_USER_ROLE_410|Update User Role with Authorised District Level User| N/A |Will be Updated|1|testPosDistLevelAuthorisedUserUpdateUserRole|
|1.0|Update|ut_p_u_GSTS_WEB_USER_ROLE_420|Update User Role with Authorised Division Level User| N/A |Will be Updated|1|testPosDivLevelAuthorisedUserUpdateUserRole|
|1.0|Update|ut_p_u_GSTS_WEB_USER_ROLE_430|Update User Role with Authorised Mandal Level User| N/A |Will be Updated|1|testPosMandalLevelAuthorisedUserUpdateUserRole|
|1.0|Update|ut_p_u_GSTS_WEB_USER_ROLE_440|Update User Role with Authorised Panchayat Level User| N/A |Will be Updated|1|testPosPanchayatLevelAuthorisedUserUpdateUserRole|
|1.0|Remove|ut_p_u_GSTS_WEB_USER_ROLE_920|Remove User Role with Authorised District Level User| N/A |Will be Removed|1|testPosDistLevelAuthorisedUserRemoveUserRole|
|1.0|Remove|ut_p_u_GSTS_WEB_USER_ROLE_930|Remove User Role with Authorised Division Level User| N/A |Will be Removed|1|testPosDivLevelAuthorisedUserRemoveUserRole|
|1.0|Remove|ut_p_u_GSTS_WEB_USER_ROLE_940|Remove User Role with Authorised Mandal Level User| N/A |Will be Removed|1|testPosMandalLevelAuthorisedUserRemoveUserRole|
|1.0|Remove|ut_p_u_GSTS_WEB_USER_ROLE_950|Remove User Role with Authorised Panchayat Level User| N/A |Will be Removed|1|testPosPanchayatLevelAuthorisedUserRemoveUserRole|

## Security compliance check
1. Only user having the user role with permission **ROLE_USER_ROLE_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_USER_ROLE_UPDATE** should update this functionality 
1. Only user having the user role with permission **ROLE_USER_ROLE_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_USER_ROLE_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the USER ROles in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0003|[GS-0003](https://shadkona.atlassian.net/browse/GS-0003)|Closed|


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




 
