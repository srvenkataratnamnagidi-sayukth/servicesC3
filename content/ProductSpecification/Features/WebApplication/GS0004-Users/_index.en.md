---
title: GS0004 - Users
tags : ["Composing"]
---

## Introduction
Users are one of the basic building blocks of the software product. Product can be used by different users at various levels of the organization.
Here we assign **User Roles** to the user based on their level.Set of permissions to product features is called User Role.Based on assigned user roles to the user,user can access to the specific product feature.

## Business Assumptions
What type of users can be access to our product should be planned at design phase.

## Requirements
### Functional Requirements
1. State level user should have access only to all districts, divisions, mandals and panchayats in that state.  
1. District level user should have access only to all divisions, mandals and panchayats in that district.  
1. Division level user should have access only to all mandals and panchayats in that division.  
1. Mandal level user should have access only to all panchayats in that Mandal. 
1. Panchayat level user should have access only to his panchayat. 
1. we can create,update and remove users at any level.

### Non-functional Requirements
Based on **Personas of Users**, user roles are binded to the user.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Users are the persons who can login into product and also have access to assigned product features in particular assigned organization(s).

### Design 
1. We can create, update, remove, activate and view the user.
1. Each user has username and password to login into product.
1. Each user has minimum one User Role.
1. Insert atleast one user(state level) in the Database directly. Otherwise we cannot login.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	
|User Role|[gs0003-userroles]({{< ref "gs0003-userroles" >}})|User Role Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_user_list|Provide a List page to view all the users, Even this listing page should bind to a permission|
|uc_user_create|Provide a Create page to create the user, Even this create page should bind to a permission|
|uc_user_update|Provide a Update page to update the user, Even this update page should bind to a permission|
|uc_user_remove|Provide a Remove page to remove the user, Even this remove page should bind to a permission|
|uc_user_activate|Provide a Activate page to activate the user, Even this activate page should bind to a permission|
|uc_user_view|Provide a View page to view the user, Even this view page should bind to a permission|
|uc_user_export|Provide a Export page to export the user in 2 formats Excel, PDF, Even this Export page should bind to a permission|
|uc_user_create_failure|Creating user with existing email or existing login name or existing aadhaar number should be failed|
|uc_user_login_success|User should exists in database and his object state should be active and entered credentials should be correct|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|Activate|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|--------|----|----|------|-------|
|aadharId|YES|NA|0-9,maxlen=12|@Column(name = "aadhar_id", length = 12, unique = true, nullable = false)|aadhar_id varchar(12) not null|YES|NA|YES|YES|YES|YES|YES||
|firstName|YES|NA|a-zA-Z0-9. _-,minlen=3, maxlen=64|@Column(name = "fname", length = 64, nullable = false)|fname varchar(64) not null|YES|YES|YES|YES|YES|YES|NO||
|lastName|YES|NA|a-zA-Z0-9. _-,minlen=1, maxlen=64|@Column(name = "lname", length = 64, nullable = false)|lname varchar(64) not null|YES|YES|YES|YES|YES|NA|NO||
|fsName|YES|NA|a-zA-Z0-9. _-,minlen=3, maxlen=64|@Column(name = "fsname", length = 32, nullable = false)|fsname varchar(64) not null|YES|YES|YES|YES|YES|NA|NO||
|email|YES|NA|a-zA-Z0-9._@,minlen=3, maxlen=64|@Column(name = "email", length = 64, nullable = false, unique = true)|email varchar(64) not null|YES|YES|YES|YES|YES|YES|YES||
|loginName|YES|NA|a-zA-Z0-9._@,minlen=3, maxlen=64|@Column(name = "login_name", length = 64, nullable = false, unique = true)|login_name varchar(64) not null|YES|NA|YES|YES|YES|YES|YES||
|loginPassword|YES|NA|maxlen=64|@Column(name = "login_password", length = 128, nullable = false)|login_password varchar(128) not null|YES|NA|NA|NA|NA|NA|NO||
|gender|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "gender", length = 6, nullable = false)|gender varchar(6) not null|YES|YES|YES|YES|YES|NA|NO||
|dob|YES|NA|Date dd-MM-YYYY|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "dob", nullable = false)|dob datetime not null|YES|YES|YES|YES|YES|NA|NO||
|designation|YES|NA|a-zA-Z0-9. _-,minlen=3, maxlen=24|@Column(name = "designation", length = 24, nullable = false)|designation varchar(64) not null|YES|YES|YES|YES|YES|NA|NO||
|mobileNumber|YES|NA|0-9, maxlen=10|@Column(name = "mobile_number", length = 14, nullable = false)|mobile_number varchar(14) not null|YES|YES|YES|YES|YES|YES|YES||
|appLogin|YES|false|Boolean|@Column(name = "app_login", nullable = false)|app_login boolean DEFAULT false|YES|YES|YES|YES|YES|NA|NO||
|apiLogin|YES|false|Boolean|@Column(name = "api_login", nullable = false)|api_login boolean DEFAULT false|YES|YES|YES|YES|YES|NA|NO||
|roleSet|YES|NA||@ManyToMany(fetch = FetchType.LAZY) @JoinTable(name = "gs_user_role_map", joinColumns = { @JoinColumn(name = "user_id", nullable = false) }, inverseJoinColumns = {@JoinColumn(name = "role_id", nullable = false) }, uniqueConstraints = @UniqueConstraint(columnNames = { "user_id", "role_id" }))||YES|YES|YES|YES|YES|NA|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|NO|YES|NO|NO||

#### ENUM CONSTANTS

##### Gender

{{<mermaid align="left">}}
classDiagram
    class GenderType{
	  MALE
	  FEMALE
	  OTHER
    }
{{< /mermaid >}}

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|USER_VIEW|View|
|USER_CREATE|Create|
|USER_UPDATE|Update|
|USER_REMOVE|Remove|
|USER_UPDATE|Activate|
|USER_VIEW|Export|
|USER_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_user__login_name (login_name)|
|Unique Key|uk__gs_user__email (email)|
|Unique Key|uk__gs_user__aadhar_id (aadhar_id)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_USER_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_USER_UPDATE|Only user having the user role with this permission should update this functionality|
|AC_ROLE_USER_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_USER_UPDATE|Only user having the user role with this permission should activate this functionality|
|AC_ROLE_USER_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_USER_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

## User Experience
1. Create page based on the standard UX Listing Template
1. Update page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Activate page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreateBtn[Create]---UpdateBtn[Update]---RemoveBtn[Remove]---ActivateBtn[Activate]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="left">}}
flowchart TD
	UserMenu((Users Menu))
	ListPage{Users List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
	RemovePage((Remove Page))
	ActivatePage((Activate Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->UserMenu
    subgraph Menu    
    UserMenu
    end
    subgraph   
    UserMenu-->ListPage
    ListPage--C-U-R-A-V-E-->ListPage
    end
    subgraph  
    UserMenu--F-->ErrorPage
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
    ViewPage--B-->ListPage
    ViewPage--B-->ViewPage
    end
    subgraph Remove
    ListPage--R-->RemovePage
    RemovePage--SB-->ListPage
    RemovePage--SB-->RemovePage
    end
    subgraph Activate
    ListPage--A-->ActivatePage
    ActivatePage--SB-->ListPage
    ActivatePage--SB-->ActivatePage
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
    linkStyle 18 stroke:green,stroke-width:2px;
    linkStyle 20 stroke:green,stroke-width:2px;    
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;    
    linkStyle 13 stroke:red,stroke-width:2px;
    linkStyle 16 stroke:red,stroke-width:2px;
    linkStyle 19 stroke:red,stroke-width:2px;

    
    
{{< /mermaid >}}


|Symbol|Action|
|:-----|:-----|
|C|Create|
|U|Update|
|R|Remove|
|A|Activate|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|SB|Submit or Back|
|VE|View or Export|
|C-U-R-A-V-E|Create or Update or Remove or Activate or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Sequence Diagram
1. Only a user with the USER_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant UserListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet, GET /app/ctx/User/list ListPage
        Net--x-UserListPage: F : Connection Error
        UserListPage->>+cloud: S:  GET /app/ctx/User/list ListPage
        cloud-->>-UserListPage: RES:List Page
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet, GET /app/User/create/form CreateFormPage
        Net--x-UserListPage: F : Connection Error
        UserListPage->>+cloud: S : GET /app/User/create/form CreateFormPage
        cloud-->>-UserListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: POST /app/User/create Create
        Net--x-UserListPage: F : Connection Error
        UserListPage->>+cloud: S : POST /app/User/create Create
        cloud-->>-UserListPage: RES: An User Successfully Created
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: GET /app/User/update/form UpdateFormPage
        Net--x-UserListPage: F : Connection Error
        alt 
        Note right of Net: User Cache Object Found
        UserListPage->>+Cache: S : GET /app/User/update/form UpdateFormPage
        Cache-->>-UserListPage: RES: Update Form Loaded
        else 
        Note right of Net: User Cache Object Not Found
        Cache->>+cloud: GET /app/User/update/form UpdateFormPage
        cloud-->>-UserListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: POST /app/User/update update
        Net--x-UserListPage: F : Connection Error
        UserListPage->>+cloud: S : POST /app/User/update Update
        cloud-->>-UserListPage: RES: An User Successfully Updated
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: GET /app/User/remove/form RemoveFormPage
        Net--x-UserListPage: F : Connection Error
        UserListPage->>+cloud: S : GET /app/User/remove/form RemoveFormPage
        cloud-->>-UserListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: POST /app/User/remove Remove
        Net--x-UserListPage: F : Connection Error
        UserListPage->>+cloud: S : POST /app/User/remove Remove
        cloud-->>-UserListPage: RES: An User Successfully Removed
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: Get /app/User/active/form ActivateFormPage
        Net--x-UserListPage: F : Connection Error
		UserListPage->>+cloud: S : Get /app/User/active/form ActivateFormPage
        cloud-->>-UserListPage: RES: Active Form Loaded
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: Post /app/User/active Activate
        Net--x-UserListPage: F : Connection Error
        UserListPage->>+cloud: S : POST /app/User/active Activate
        cloud-->>-UserListPage: RES: An User Successfully Activated
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: GET /app/User/view ViewPage
        Net--x-UserListPage: F : Connection Error
        alt 
        Note right of Net: User Cache Object Found
        UserListPage->>+Cache: S : GET /app/User/view ViewPage
        Cache-->>-UserListPage: RES: User View
        else  
        Note right of Net: User Cache Object Not Found
        Cache->>+cloud: GET /app/User/view ViewPage
        cloud-->>-UserListPage: RES: User View
        end
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: GET /app/User/exportPdf ExportPdf
        Net--x-UserListPage: F : Connection Error
        alt 
        Note right of Net: User Cache Object Found
        UserListPage->>+Cache: S : GET /app/User/exportPdf ExportPdf
        Cache-->>-UserListPage: RES: User Pdf
        else  
        Note right of Net: User Cache Object Not Found
        Cache->>+cloud: GET /app/User/exportPdf ExportPdf
        cloud-->>-UserListPage: RES: User Pdf
        end
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: GET /app/User/exportListPdf ExportListPdf
        Net--x-UserListPage: F : Connection Error
        UserListPage->>+cloud: S : GET /app/User/exportListPdf ExportListPdf
        cloud-->>-UserListPage: RES: User List Pdf
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: GET /app/User/exportXlx ExportXlx
        Net--x-UserListPage: F : Connection Error
        alt 
        Note right of Net: User Cache Object Found
        UserListPage->>+Cache: S : GET /app/User/exportXlx ExportXlx
        Cache-->>-UserListPage: RES: User Xlx
        else 
        Note right of Net: User Cache Object Not Found
        Cache->>+cloud: GET /app/User/exportXlx ExportXlx
        cloud-->>-UserListPage: RES: User Xlx
        end
    end
    rect rgb(244,244,244)
        UserListPage->>+Net: Check Internet: GET /app/User/exportListXlx ExportListXlx
        Net--x-UserListPage: F : Connection Error
        UserListPage->>+cloud: S : GET /app/User/exportListXlx ExportListXlx
        cloud-->>-UserListPage: RES: User List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_WEB_USER_202 ut_p_c_GSTS_WEB_USER_203 ut_p_c_GSTS_WEB_USER_204 ut_p_c_GSTS_WEB_USER_205 ut_p_c_GSTS_WEB_USER_206 ut_p_c_GSTS_WEB_USER_210 ut_n_c_GSTS_WEB_USER_207 ut_n_c_GSTS_WEB_USER_210 ut_n_c_GSTS_WEB_USER_211|**Positive Test Cases:** 1.Creating State Level User with Authorized User 2.Creating District Level User with Authorized User 3.Creating Mandal Level User with Authorized user 4.Creating Panchayat Level User with Authorized User 5.Creating User **Negative Test Cases:** 1.Creating State Level User with Authorised User(Invalid Inputs) 2.Creating Panchayat Level User without DB connection 3.Creating Panchayat Level User with Authorised User(Invalid Inputs)| **aadharId:** 1.does not start with '0' 2.length = 12 3.unique key 4.null **firstName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **lastName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=1 and length<=64 3.null **fsName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **loginName:** 1.valid characters 2.null **loginPassword:** 1.length>=7 and length<=128 2.valid characters 3.null **confirmLoginPassword** **email:** 1.valid characters 2.null **gender** **mobileNumber:** 1.Start with [6789] 2.length= 10 3.valid characters 4.null **appLogin** **apiLogin** **designation:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **mfaType** |11|6|17|testCreateUser, testCreateStateLevelUser, testCreateDistrictLevelUser, testCreateDivLevelUser, testCreateMandalLevelUser, testCreatePanchayatLevelUser, testCreateStateLevelUserNegativeCases, testCreateUserByBlockingDBWithAuthorisedUser, testCreatePanchayatLevelUserNegativeTestCase|
|1.0|Create Form|ut_p_c_GSTS_WEB_USER_200 ut_n_c_GSTS_WEB_USER_209|**Positive Test Cases:** 1.Open Create User Form with Authorised User **Negative Test Cases:** 1.Open Create User Form without DB connection with Authorised User |N/A|1|1|2|testOpenCreateFormWithAuthorisedUser, testOpenCreateFormByBlockingDBWithAuthorisedUser|
|1.0|Update|ut_p_u_GSTS_WEB_USER_306 ut_p_u_GSTS_WEB_USER_307 ut_p_u_GSTS_WEB_USER_308 ut_p_u_GSTS_WEB_USER_309 ut_p_u_GSTS_WEB_USER_310 ut_n_u_GSTS_WEB_USER_311 ut_n_u_GSTS_WEB_USER_312 ut_n_u_GSTS_WEB_USER_313 ut_n_u_GSTS_WEB_USER_314 ut_n_u_GSTS_WEB_USER_315 ut_n_u_GSTS_WEB_USER_318 ut_n_u_GSTS_WEB_USER_320 ut_n_u_GSTS_WEB_USER_410 |**Positive Test Cases:** 1.Updating State level user with Authorised user 2.Updating District level user with Authorised User 3.Updating Division level user with Authorised User 4.Updating Mandal level user with Authorised User **Negative Test Cases:** 1.Updating State level user with Invalid inputs with Authorised user 2.Updating District level user with Invalid inputs with Authorised User 3.Updating Division level user with Invalid inputs with Authorised User 4.Updating Mandal level user passing Invalid inputs with Authorised User 5.Updating Panchayat Level User passing Invalid inputs with Authorised User 6.Updating Panchayat Level User without DB Connection with Authorised User 7.Updating Panchayat Level User with Invalid id with Authorised User 8.Updating already removed Panchayat Level User with Authorised User|**updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null|5|8|13|testAuthorisedUserUpdateStateLeveluser, testAuthorisedUserUpdateDistLevelUser, testAuthorisedUserUpdateDivLevelUser, testAuthorisedUserUpdateMandalLevelUser, testUpdatePanchayatLevelUser, testAuthorisedUserUpdateStateLeveluserNegativeTestCase, testAuthorisedUserUpdateDistLevelUserNegativeTestCase, testAuthorisedUserUpdateDivLevelUserNegativeTestCase, testAuthorisedUserUpdateMandalLevelUserNegativeTestCase, testUpdatePanchayatLevelUserNegativeCases, testUpdatePanchayatLevelUserWithoutDbConnection, testUpdatePanchayatLevelUserWithInvalidId, testUpdateAlreadyRemovedPanchayatLevelUser|
|1.0|Update Form|ut_p_u_GSTS_WEB_USER_300 ut_p_u_GSTS_WEB_USER_301 ut_p_u_GSTS_WEB_USER_302 ut_p_u_GSTS_WEB_USER_303 ut_p_u_GSTS_WEB_USER_304 ut_n_u_GSTS_WEB_USER_305 ut_n_u_GSTS_WEB_USER_317|**Positive Test Cases:** 1.View User Update Form at state level with valid Id with Authorised user 2.View User Update Form at District level with valid Id with Authorised user 3.View User Update Form at Division level with valid Id with Authorised user 4.View User Update Form at Mandal level with valid Id with Authorised user 5.View User Update Form at Panchayat level with valid Id with Authorised user **Negative Test Cases:** 1.View user update form with Invalid Id with Authorised user 2.View User Update Form at state level without DB Connection with valid Id with Authorised user |1.Valid Id 2.Invalid Id|5|2|7|testAuthorisedUserViewUpdateFormAtStateLevel, testAuthorisedUserViewUpdateFormatAtDistLevel, testAuthorisedUserViewUpdateFormatAtDivLevel, testAuthorisedUserViewUpdateFormatAtMandalLevel, testAuthorisedUserViewUpdateFormatAtPanchayatLevel, testAuthorisedUserUpdateFormWithInvalidId, testAuthorisedUserViewUpdateFormWithoutDBConnection|
|1.0| Remove |ut_p_r_GSTS_WEB_USER_403  ut_n_r_GSTS_WEB_USER_404 ut_n_r_GSTS_WEB_USER_407 ut_n_r_GSTS_WEB_USER_408 ut_n_r_GSTS_WEB_USER_409 |**Positive Test Cases:** Removing User with Authorised User **Negative Test Cases:** 1.Removing Mandal Level User with Invalid inputs with Authorised User 2.Removing Mandal Level User with Passing Invalid Id in Object with Authorised User 3.Removing Mandal Level User by Passing Invalid Id and Invalid characters in removed comment in user Object with Authorised User 4.Removing Already Removed Panchayat Level User with Authorised User| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|4|5|testRemovePanchayatLevelUser, testRemoveMandalLevelUserNegativeCase, testRemoveMandalLevelUserWithInvalidId, testRemoveMandalLevelUserWithInvalidIdNegativeCase, testRemoveAlreadyRemovedPanchayatLevelUser|
|1.0|Remove Form|ut_p_r_GSTS_WEB_USER_400 ut_n_r_GSTS_WEB_USER_401 ut_n_r_GSTS_WEB_USER_406 ut_n_r_GSTS_WEB_USER_411 ut_n_r_GSTS_WEB_USER_412 |**Positive Test Cases:** Open User Remove Form with Valid Id with Authorised User **Negative Test Cases:** 1.View User Remove Form with Invalid Id with Authorised User 2.View User Remove Form for Already Removed User with Authorised User 3.View User Remove Form without DB connection 4.Removing Mandal Level User without DB Connection with Authorised User|1.Valid Id 2.Invalid Id|1|4|5|testAuthorisedUserViewRemoveForm, testAuthorisedUserViewRemoveFormWithInvalidId, testAuthorisedUserViewRemoveFormForAlreadyRemovedUser, testAuthorisedUserViewRemoveFormWithoutDbConnection, testRemovemandalLevelUserWithoutDbConnection|
|1.0|Active|ut_p_a_GSTS_WEB_USER_508 ut_n_a_GSTS_WEB_USER_504 ut_n_a_GSTS_WEB_USER_505 ut_n_a_GSTS_WEB_USER_507 ut_n_a_GSTS_WEB_USER_509 ut_n_a_GSTS_WEB_USER_510| **Positive Test Cases:** Activating User with Authorised User **Negative Test Cases:** 1.Activating Panchayat Level User by passing invalid id and comment in object with Authorised User 2.Activating Panchayat Level User without DB Connection with Authorised User 3.Activating Panchayat Level User with Invalid id with Authorised User 4.Activating Already Active Panchayat Level User with Authorised User 5.Activating Mandal Level User passing Null update comment with Authorised User| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|5|6|testActivePanchayatLevelUserWithInvalidIdAndComment, testActivePanchayatLevelUserWithoutDbConnection, testActivePanchayatLevelUserWithInvalidId, testActivePanchayatLevelUser, testActiveAlreadyActivePanchayatLevelUser, testActivePanchayatLevelUserNegativeCase|
|1.0|Active Form|ut_p_a_GSTS_WEB_USER_9 ut_n_a_GSTS_WEB_USER_500 ut_n_a_GSTS_WEB_USER_502 ut_n_a_GSTS_WEB_USER_503 |**Positive Test Cases:** View User Activate Form with Valid Id with Authorised User **Negative Test Cases:** 1.View User Activate Form without DB Connection with Valid Id with Authorised User 2.View User Activate Form with InValid Id with Authorised User|1.Valid Id 2.Invalid Id|1|3|4|testAuthorisedUserViewActivateForm, testAuthorisedUserViewActivateFormWithoutDbConnection, testAuthorisedUserViewActivateFormWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_USER_900 ut_n_v_GSTS_WEB_USER_901 ut_n_v_GSTS_WEB_USER_903 |**Positive Test Cases:** View User with Valid Id  with Authorised User **Negative Test Cases:** 1.View User with Invalid ID with Authorised User 2.View user without DB Connection with Authorised user|1.Valid Id 2.Invalid Id|1|2|3|testAuthorisedUserViewUserWithValidId, testAuthorisedUserViewUserWithInValidId, testAuthorisedUserViewUserWithoutDbConnection|
|1.0| Search |ut_p_s_GSTS_WEB_USER_1100  ut_n_s_GSTS_WEB_USER_701 ut_n_s_GSTS_WEB_USER_702 ut_n_s_GSTS_WEB_USER_703 ut_n_s_GSTS_WEB_USER_704 ut_n_s_GSTS_WEB_USER_1101 ut_n_s_GSTS_WEB_USER_1104 ut_n_s_GSTS_WEB_USER_1105 |**Positive Test Cases:** Search User with Authorised User **Negative Test Cases:** 1.Search User with Authorised User 2.Search Mandal111 Lvl User in Mandal112 Lvl with Authorised User 3.Search Division Lvl User in Division12 Context with Authorised User 4.Search District1 User in District2 Context with Authorised User 5.Search User with Invalid inputs with Authorised User 6.Search User with Invalid dates with Authorised User|**loginName:** 1.valid characters 2.null **mobileNumber:** 1.Start with [6789] 2.length= 10 3.valid characters 4.null **email:** 1.valid characters 2.null **aadharId:** 1.does not start with '0' 2.length = 12 3.null|8|5|13|testScopeLvlSearchUserPanchayatLvl, testScopeLvlSearchUserMandalLvl, testScopeLvlSearchUserDivisionLvl, testScopeLvlSearchUserDistLvl, testAuthorisedUserSearchUser, testAuthorisedUserSearchUserNegativeCases, testAuthorisedUserSearchUserWithoutDbConnection, testAuthorisedUserSearchUserNegativeCase|
|1.0| List |ut_p_l_GSTS_WEB_USER_1000 ut_n_l_GSTS_WEB_USER_1001 ut_n_l_GSTS_WEB_USER_1003 |**Positive Test Cases:** Check the object list with valid data  with Authorised User **Negative Test Cases:** 1.Check the object list with Invalid data with Authorised User 2.Check the object list without DB connection with Authorised User|Validating with unique field|1|2|3|testAuthorisedUserListUser, testAuthorisedUserListUserNegativeCase, testAuthorisedUserListUserWithoutDbConnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_USER_1201 ut_n_ep_GSTS_WEB_USER_1202 ut_n_ep_GSTS_WEB_USER_1213|**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id|1|2|3|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId, testAuthorisedUserExportPdfWithoutDBConnection|
|1.0| List PDF |ut_p_elp_GSTS_WEB_USER_1203 ut_n_elp_GSTS_WEB_USER_1204 ut_n_elp_GSTS_WEB_USER_1214|**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_USER_1205 ut_n_ex_GSTS_WEB_USER_1206 ut_n_ex_GSTS_WEB_USER_1215|**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId, testAuthorisedUserExportXlxWithoutDBConnection|
|1.0| List XLX |ut_p_elx_GSTS_WEB_USER_1207 ut_n_elx_GSTS_WEB_USER_1208 ut_n_elx_GSTS_WEB_USER_1216|**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name||
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_n_c_GSTS_WEB_USER_208|Unauthorised User does not have permission to create|**aadharId:** 1.does not start with '0' 2.length = 12 3.unique key 4.null **firstName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **lastName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=1 and length<=64 3.null **fsName:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **loginName:** 1.valid characters 2.null **loginPassword:** 1.length>=7 and length<=128 2.valid characters 3.null **confirmLoginPassword** **email:** 1.valid characters 2.null **gender** **mobileNumber:** 1.Start with [6789] 2.length= 10 3.valid characters 4.null **appLogin** **apiLogin** **designation:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **mfaType** |0|1|1|testCreateStateLevelUserWithUnAuthorisedUser|
|1.0|Create Form|ut_n_c_GSTS_WEB_USER_201|Open Create User Form with UnAuthorised User|N/A|0|1|1|testOpenCreateFormWithUnAuthorisedUser|
|1.0|Update|ut_n_u_GSTS_WEB_USER_316| Unauthorised User does not have permission to UPDATE | **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserUpdatePanchayatLevelUser|
|1.0|Update Form|ut_n_u_GSTS_WEB_USER_319|View User Update Form at Panchayat level with valid Id with UnAuthorised user|1.Valid Id 2.Invalid Id|0|1|1|testUnAuthorisedUserViewUpdateFormatAtPanchayatLevel|
|1.0| Remove |ut_n_r_GSTS_WEB_USER_405|Removing Division Level User with UnAuthorised User| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserRemoveDivisionLevelUser|
|1.0|Remove Form|ut_n_r_GSTS_WEB_USER_402|Open User Remove Form with Valid Id with UnAuthorised User|1.Valid Id 2.Invalid Id|0|1|1|testUnAuthorisedUserViewRemoveForm|
|1.0|Active|ut_n_a_GSTS_WEB_USER_506| Active Panchayat Level User with UnAuthorised User|**updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserActivePanchayatLevelUser|
|1.0|Active Form|ut_n_a_GSTS_WEB_USER_501|View User Activate Form with Valid Id with UnAuthorised User|1.Valid Id 2.Invalid Id|0|1|1|testUnAuthorisedUserViewActivateForm|
|1.0| View |ut_n_v_GSTS_WEB_USER_902|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testUnAuthorisedUserViewUser|
|1.0| Search |ut_n_s_GSTS_WEB_USER_1102 ut_n_s_GSTS_WEB_USER_1103|1.Unauthorised User does not have permission to search 2.Search User with UnAuthorised User|**loginName:** 1.valid characters 2.null **mobileNumber:** 1.Start with [6789] 2.length= 10 3.valid characters 4.null **email:** 1.valid characters 2.null **aadharId:** 1.does not start with '0' 2.length = 12 3.null|0|2|2|testUnAuthorisedUserViewUserWithValidId, testUnAuthorisedUserSearchUser|
|1.0| List |ut_n_l_GSTS_WEB_USER_1002|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testUnAuthorisedUserListUser|
|1.0| PDF |ut_n_ep_GSTS_WEB_USER_1209 |Export List Pdf with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_USER_1210 |Export Pdf with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_USER_1211 |Export XLX with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_USER_1212 |Export List XLX with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserExportListXlx|


#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|-----------|
|1.0|View|ut_n_v_GSTS_WEB_USER_600| View State level object At panchayat context with authorised user| N/A |Denied Exception|1|testScopeLevelPanchayatToState|
|1.0|Search|ut_n_s_GSTS_WEB_USER_601| Search state level object with panchayat level authorised user| N/A |Empty object list|1|testAuthorisedScopeLevelPanchayatToState|
|1.0|Create|ut_n_c_GSTS_WEB_USER_700| Create state level user with panchayat scope authorised user| N/A |Will not be Created|1|testPanchayatScopeUserCreateStateLevelUser|
|1.0|Update|ut_n_u_GSTS_WEB_USER_705|Update state level user with panchayat scope authorised user| N/A |Will not be Updated|1|testPanchayatUserUpdateStateLevelUser|
|1.0|Remove|ut_n_r_GSTS_WEB_USER_706| Remove state level user with panchayat scope authorised user| N/A |Will not be Removed|1|testPanchayatUserRemoveStateLevelObj|
|1.0|Activate|ut_n_a_GSTS_WEB_USER_707| Activate state level removed user with panchayat scope authorised user| N/A |Will not be Activated|1|testPanchayatUserActivateStateLevelObj|
|1.0|Activate|ut_n_a_GSTS_WEB_USER_708| Activate the user which is already in Active state| N/A |Will not be Activated|1|testActivateAlreadyActivateStateLevelObj|


## Security compliance check
1. Only user having the permission **ROLE_USER_VIEW** should view this functionality 
1. Only user having the permission **ROLE_USER_CREATE** should create this functionality 
1. Only user having the permission **ROLE_USER_UPDATE** should update this functionality 
1. Only user having the permission **ROLE_USER_UPDATE** should activate this functionality 
1. Only user having the permission **ROLE_USER_REMOVE** should remove this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the USERs in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
