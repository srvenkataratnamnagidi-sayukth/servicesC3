---
title: GS0009 - Organizations
tags : ["Composing"]
---

## Introduction
Organizations are one of the basic building blocks of the software product. The product can be used by different users at various levels of the organization. Organization may be State, District, Division, Mandal, and Panchayat.

## Business Assumptions
Organizations Feature should be planned at the design phase and updates to the organizations at the run time based on the requirement.

## Requirements
### Functional Requirements
1. Panchayat level users should only view the organization.
1. Organizations is used to create Organization on the basis of organization type.
1. Organization types are State, District, Division, Mandal, and Panchayat.

### Non-functional Requirements
1. we cannot create, and update organizations at the panchayat level.

### Problem Statement
Organizations feature contains the information of all districts, divisions, mandals, and panchayats data.

### Design 
1. We can create, update, view, and export the organization.
1. Each organization has Name, OrgType, Latitude, Longitude, and Survey Status.
1. Insert at least one Organization(state level) in the Database directly.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_organization_list|To view all the organizations|
|uc_organization_search|To search the organization|
|uc_organization_create|To create the organization|
|uc_organization_update|To update the organization|
|uc_organization_view|To view the organization|
|uc_organization_export|To export the organization in 2 formats Excel, PDF|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|--------|----|----|------|-------|
|orgType|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "org_type", length = 16, nullable = false)|org_type varchar(16) NOT NULL|YES|NO|NA|YES|YES|YES||
|geoCode|YES|NA|a-zA-Z0-9. _-,minlen=3, maxlen=64|@Column(name = "geo_code", length = 24, nullable = false, unique = true)|geo_code varchar(24) NOT NULL|NO|YES|NA|YES|YES|NO||
|seqNo|YES|NA|0-9 -|@Column(name = "seq_no", nullable = false, unique = false)|seq_no bigint(20) NOT NULL|YES|YES|NA|NO|NA|NO||
|geoLat|YES|NA|0-9.|@Column(name = "geo_lat", length = 16, nullable = false)|geo_lat varchar(16) NOT NULL|YES|YES|NA|YES|NA|NO||
|geoLng|YES|NA|0-9.|@Column(name = "geo_lng", length = 16, nullable = false)|geo_lng varchar(16) NOT NULL|YES|YES|NA|YES|NA|NO||
|name|YES|NA|a-zA-Z0-9._@,minlen=3, maxlen=64|@Column(name = "org_name", length = 64, nullable = false)|org_name varchar(64) NOT NULL|YES|NO|NA|YES|YES|YES||
|orgCode|YES|NA|a-zA-Z0-9 _-,minlen=3, maxlen=64|@Column(name = "org_code", length = 6, nullable = false)|org_code varchar(6) NOT NULL|YES|NO|NA|NO|NO|NO||
|phoneNumber|NO|NA|0-9 -, maxlen=10|@Column(name = "support_phone_number", length = 15, nullable = true)|support_phone_number varchar(15) DEFAULT NULL|YES|YES|NA|YES|YES|NO||
|mobileNumber|YES|NA|0-9, maxlen=10|@Column(name = "support_mobile_number", length = 10, nullable = false)|support_mobile_number varchar(10) NOT NULL|YES|YES|NA|YES|YES|NO||
|emailId|YES|NA|a-zA-Z0-9._@|@Column(name = "support_email_id", length = 64, nullable = false)|support_email_id varchar(64) NOT NULL|YES|YES|NA|YES|YES|NO||
|panchayatType|NO|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "panchayat_type", length = 16, nullable = true)|panchayat_type varchar(16) DEFAULT NULL|YES|YES|NA|YES|YES|NO||
|surveyStatus|NO|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "survey_status", length = 24, nullable = true)|survey_status varchar(24) DEFAULT NULL|YES|YES|NA|YES|YES|NO||
|targetSurveyAssetCount|NO|0|0-9, maxlen=10|@Column(name = "target_survey_asset_count", nullable = true)|target_survey_asset_count bigint(20) DEFAULT '0'|YES|YES|NA|YES|YES|NO||
|mapPlaceId|YES|0|minlen=6,maxlen=32|@Column(name = "map_place_id", nullable = false)|map_place_id varchar(32) NOT NULL|YES|YES|NA|NO|YES|NO||
|landSurveyNumber|YES|0|0-9.,, maxlen=10|@Column(name = "land_survey_number", nullable = true)|land_survey_number varchar(1024) DEFAULT NULL|YES|YES|NA|YES|YES|NO||
|pincode|YES|0|0-9, maxlen=10|@Column(name = "pincode", length = 6, nullable = false)|pincode  bigint(6) DEFAULT NULL|YES|YES|NA|YES|YES|YES||
|postOfficeName|YES|NA|a-zA-Z0-9/:, _.-,minlen=3, maxlen=128|@Column(name = "post_office_name", length = 128, nullable = false)|post_office_name varchar(128) DEFAULT NULL|YES|YES|NA|YES|YES|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NA|YES|YES|NO||

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

##### Panchayat Type

{{<mermaid align="left">}}
classDiagram
    class PanchayatType{
      NON_NOTIFIED
      NOTIFIED
      MASTER_PALN
    }
{{< /mermaid >}}

##### Survey Status Type

{{<mermaid align="left">}}
classDiagram
    class SurveyStatusType{
      NOT_STARTED
      IN_PROGRESS
      COMPLETED
      AUTHORIZE_PENDING
      DATA_LOCKED
    }
{{< /mermaid >}}

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|ORGANIZATION_CREATE|Create|
|ORGANIZATION_UPDATE|Update|
|ORGANIZATION_VIEW|Export|
|ORGANIZATION_VIEW|List|
|ORGANIZATION_VIEW|View|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk_gs_organization__geo_code (geo_code)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_ORGANIZATION_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_ORGANIZATION_UPDATE|Only user having the user role with this permission should update this functionality|
|AC_ROLE_ORGANIZATION_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_ORGANIZATION_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

## User Experience
1. Create page based on the standard UX Listing Template
1. Update page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreateBtn[Create]---UpdateBtn[Update]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="left">}}
flowchart TD
	OrganizationMenu((Organizations Menu))
	ListPage{Organizations List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->OrganizationMenu
    subgraph Menu    
    OrganizationMenu
    end
    subgraph   
    OrganizationMenu-->ListPage
    ListPage--C-U-V-E-->ListPage
    end
    subgraph  
    OrganizationMenu--F-->ErrorPage
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
|U|Update|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|SB|Submit or Back|
|VE|View or Export|
|C-U-V-E|Create or Update or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Survey Statustype
{{<mermaid align="left">}}
flowchart LR 
	NotStarted((Not Started))
	InProgress((In Progress))
	Completed((Completed))
	AuthorizePending((Authorize Pending))
	DataLocked((Data Locked))
	Stop((Stop))
	Start((Start))
	Start-->NotStarted
	NotStarted-->InProgress
	InProgress-->Completed
	Completed-->InProgress
	Completed-->AuthorizePending
	AuthorizePending-->InProgress
	AuthorizePending-->DataLocked 
	DataLocked-->Stop
	 
	
{{< /mermaid >}} 


### Sequence Diagram
1. Only a user with the ORGANIZATION_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant OrganizationListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        OrganizationListPage->>+Net: Check Internet, GET /app/ctx/Organization/list ListPage
        Net--x-OrganizationListPage: F : Connection Error
        OrganizationListPage->>+cloud: S:  GET /app/ctx/Organization/list ListPage
        cloud-->>-OrganizationListPage: RES:List Page
    end
    rect rgb(244,244,244)
        OrganizationListPage->>+Net: Check Internet, GET /app/Organization/create/form CreateFormPage
        Net--x-OrganizationListPage: F : Connection Error
        OrganizationListPage->>+cloud: S : GET /app/Organization/create/form CreateFormPage
        cloud-->>-OrganizationListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        OrganizationListPage->>+Net: Check Internet: POST /app/Organization/create Create
        Net--x-OrganizationListPage: F : Connection Error
        OrganizationListPage->>+cloud: S : POST /app/Organization/create Create
        cloud-->>-OrganizationListPage: RES: An Organization Successfully Created
    end
    rect rgb(244,244,244)
        OrganizationListPage->>+Net: Check Internet: GET /app/Organization/update/form UpdateFormPage
        Net--x-OrganizationListPage: F : Connection Error
        alt 
        Note right of Net: Organization Cache Object Found
        OrganizationListPage->>+Cache: S : GET /app/Organization/update/form UpdateFormPage
        Cache-->>-OrganizationListPage: RES: Update Form Loaded
        else 
        Note right of Net: Organization Cache Object Not Found
        Cache->>+cloud: GET /app/Organization/update/form UpdateFormPage
        cloud-->>-OrganizationListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        OrganizationListPage->>+Net: Check Internet: POST /app/Organization/update update
        Net--x-OrganizationListPage: F : Connection Error
        OrganizationListPage->>+cloud: S : POST /app/Organization/update Update
        cloud-->>-OrganizationListPage: RES: An Organization Successfully Updated
    end
    rect rgb(244,244,244)
        OrganizationListPage->>+Net: Check Internet: GET /app/Organization/view ViewPage
        Net--x-OrganizationListPage: F : Connection Error
        alt 
        Note right of Net: Organization Cache Object Found
        Net->>+Cache: S : GET /app/Organization/view ViewPage
        Cache-->>-OrganizationListPage: RES: Organization View
        else  
        Note right of Net: Organization Cache Object Not Found
        Cache->>+cloud: GET /app/Organization/view ViewPage
        cloud-->>-OrganizationListPage: RES: Organization View
        end
    end
    rect rgb(244,244,244)
        OrganizationListPage->>+Net: Check Internet: GET /app/Organization/exportPdf ExportPdf
        Net--x-OrganizationListPage: F : Connection Error
        alt 
        Note right of Net: Organization Cache Object Found
        OrganizationListPage->>+Cache: S : GET /app/Organization/exportPdf ExportPdf
        Cache-->>-OrganizationListPage: RES: Organization Pdf
        else  
        Note right of Net: Organization Cache Object Not Found
        Cache->>+cloud: GET /app/Organization/exportPdf ExportPdf
        cloud-->>-OrganizationListPage: RES: Organization Pdf
        end
    end
    rect rgb(244,244,244)
        OrganizationListPage->>+Net: Check Internet: GET /app/Organization/exportListPdf ExportListPdf
        Net--x-OrganizationListPage: F : Connection Error
        OrganizationListPage->>+cloud: S : GET /app/Organization/exportListPdf ExportListPdf
        cloud-->>-OrganizationListPage: RES: Organization List Pdf
    end
    rect rgb(244,244,244)
        OrganizationListPage->>+Net: Check Internet: GET /app/Organization/exportXlx ExportXlx
        Net--x-OrganizationListPage: F : Connection Error
        alt 
        Note right of Net: Organization Cache Object Found
        OrganizationListPage->>+Cache: S : GET /app/Organization/exportXlx ExportXlx
        Cache-->>-OrganizationListPage: RES: Organization Xlx
        else 
        Note right of Net: Organization Cache Object Not Found
        Cache->>+cloud: GET /app/Organization/exportXlx ExportXlx
        cloud-->>-OrganizationListPage: RES: Organization Xlx
        end
    end
    rect rgb(244,244,244)
        OrganizationListPage->>+Net: Check Internet: GET /app/Organization/exportListXlx ExportListXlx
        Net--x-OrganizationListPage: F : Connection Error
        OrganizationListPage->>+cloud: S : GET /app/Organization/exportListXlx ExportListXlx
        cloud-->>-OrganizationListPage: RES: Organization List Xlx
    end
    
          
{{< /mermaid >}}


## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|-------|
|1.0| Create Form |ut_p_c_GSTS_WEB_ORGANIZATION_160 |**Positive Test Cases:** Open Organization Create Form at mandal level with Authorised User|-|1||1|testPosOpenOrganizationCreateFormAtMandalLevelWithAuthorisedUser|
|1.0| Create |ut_p_c_GSTS_WEB_ORGANIZATION_140  ut_n_c_GSTS_WEB_ORGANIZATION_150 ut_n_c_GSTS_WEB_ORGANIZATION_170 ut_n_c_GSTS_WEB_ORGANIZATION_171  ut_n_c_GSTS_WEB_ORGANIZATION_172  ut_n_c_GSTS_WEB_ORGANIZATION_173|**Positive Test Cases:** Create Panchayat Organization with valid inputs **Negative Test Cases:** 1. Create Panchayat Organization with Invalid inputs   2.Create Organization without db connection   3.Create District Organization with invalid inputs  4.Create Division Organization with invalid inputs  5.Create Mandal Organization with invalid inputs| **orgType:** enums **seqNo:** 1.valid characters [0-9] 2.null **name:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **orgCode:** 1.valid characters[a-zA-Z0-9 _-] 2. length>=3 and length<=6 3.null **geoLat:** **geoLng:** **emailId:** 1.valid characters 2.null **mapPlaceId:** 1. length>=6 and length<=32 2.null **phoneNumber:** **mobileNumber:** 1.Start with [6789] 2.length= 10 3.valid characters 4.null **pincode:** 1.Start with 5 2.length= 6 3.valid characters[0-9] 4.null **postOfficeName:** 1.valid characters[a-zA-Z0-9:\. _-/] 2.length>=3 and length<=128 3.null **panchayatType:** enums **landSurveyNumber:**|4|5|9|testPosAuthorisedUserCreatePanOrganizationWithValidInputs, testNegAuthorisedUserCreatePanchayatOrganizationWithInvalidinputs,  testNegCreateOrganizationWithoutDBconnection,  testNegCreateDistOrgWithInvalidInputs,  testNegCreateDivOrgWithInvalidInputs,  testCreateMandalOrgWithInvalidInputs|
|1.0| Update Form |ut_p_u_GSTS_WEB_ORGANIZATION_510   ut_n_u_GSTS_WEB_ORGANIZATION_530  ut_n_u_GSTS_WEB_ORGANIZATION_530 |**Positive Test Cases:** Open Organization update form with valid Id at panchayat level   **Negative Test Cases:** 1. Open Org Employee Update Form with Invalid id |Id|1|2|3|testPosAuthorisedUserOpenOrganizationUpdateFormWithValidIdAtPanchayatLevel, testNegAuthorisedUserOpenOrganizationUdpateFormWithInValidId|
|1.0| Update |ut_p_u_GSTS_WEB_ORGANIZATION_540  ut_n_u_GSTS_WEB_ORGANIZATION_550 ut_n_u_GSTS_WEB_ORGANIZATION_560 |**Positive Test Cases:** Update Panchayat Level Organization with valid inputs **Negative Test Cases:** 1. Updating Organization with invalid inputs  2. update organization with invalid id| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=6 and length<=256 3.null|1|2|3|testPosAuthorisedUserUpdatePanchayatLevelOrganizationWithValidInputs,  testNegAuthorisedUserUpdatePanchayatLevelOrganizationWithInvalidInputs,  testNegAuthorisedUserUpdateOrganizationWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_ORGANIZATION_250  ut_n_v_GSTS_WEB_ORGANIZATION_255 ut_n_v_GSTS_WEB_ORGANIZATION_260 |**Positive Test Cases:** View Organization with Valid Id  with Authorised User **Negative Test Cases:** 1.without db connection   2.View Organization with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewOrganizationWithValidId, testNegAuthorisedUserViewOrganizationWithoutDbConnection, testNegAuthorisedUserViewOrganizationwithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_ORGANIZATION_310  ut_n_s_GSTS_WEB_ORGANIZATION_320 ut_n_s_GSTS_WEB_ORGANIZATION_330|**Positive Test Cases:** 1. Search Organization with valid inputs **Negative Test Cases:** 1. Search Organization without db connection 2. Search Organization with invalid inputs | **name:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=3 and length<=64 3.null **orgType:** enums **surveyStatus:** enums **pincode:** 1.Start with 5 2.length= 6 3.valid characters[0-9] 4.null|6|3|9|testPosAuthorisedUserSearchOrganizationWithValidInputs, testNegAuthorisedUserSearchOrganizationWithoutDBconnection,  testPosAuthorisedUserSearchOrganizationWithInValidInputs|
|1.0| List |ut_p_l_GSTS_WEB_ORGANIZATION_280 ut_n_l_GSTS_WEB_ORGANIZATION_290|**Positive Test Cases:** Get Organization List with Authorised User **Negative Test Cases:** Get Organization List without db connection||1|1|2|testPosAuthorisedUserGetOrganizationList, testNegAuthorisedUserOrganizationListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_ORGANIZATION_350   ut_n_ep_GSTS_WEB_ORGANIZATION_360   ut_n_ep_GSTS_WEB_ORGANIZATION_370 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportOrganizationPdfWithValidId,  testNegAuthorisedUserExportOrganizationPdfwithoutDbconnection,  testNegAuthorisedUserExportOrganizationPdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_ORGANIZATION_380   ut_n_elp_GSTS_WEB_ORGANIZATION_390   ut_n_elp_GSTS_WEB_ORGANIZATION_400 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportOrganizationListPdfWithValidId,  testNegAuthorisedUserExportOrganizationListPdfwithoutDbconnection,  testNegAuthorisedUserExportOrganizationListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_ORGANIZATION_410   ut_n_ex_GSTS_WEB_ORGANIZATION_420   ut_n_ex_GSTS_WEB_ORGANIZATION_430 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportOrganizationXlxWithValidId,  testNegAuthorisedUserExportOrganizationXlxwithoutDbconnection,  testNegAuthorisedUserExportOrganizationXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_ORGANIZATION_440   ut_n_elx_GSTS_WEB_ORGANIZATION_450   ut_n_elx_GSTS_WEB_ORGANIZATION_460 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportOrganizationListXlxWithValidId,  testNegAuthorisedUserExportOrganizationListXlxwithoutDbconnection,  testNegAuthorisedUserExportOrganizationListXlxInValidId|


#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|-----|
|1.0| Create |ut_n_c_GSTS_WEB_ORGANIZATION_10 |Unauthorised User does not have permission to create| **orgType:** enums **seqNo:** 1.valid characters [0-9] 2.null **name:** 1.valid characters 2. length>=3 and length<=64 3.null **orgCode:** 1.valid characters[a-zA-Z0-9 _-] 2. length>=3 and length<=6 3.null **geoLat:** **geoLng:** **emailId:** 1.valid characters 2.null **mapPlaceId:** 1. length>=6 and length<=32 2.null **phoneNumber:** **mobileNumber:** 1.Start with [6789] 2.length= 10 3.valid characters 4.null **pincode:** 1.Start with 5 2.length= 6 3.valid characters[0-9] 4.null **postOfficeName:** 1.valid characters[a-zA-Z0-9:\. _-/] 2.length>=3 and length<=128 3.null **panchayatType:** enums **landSurveyNumber:**|0|1|1|testUnAuthorisedUserCreateOrganization|
|1.0| Update Form|ut_n_r_GSTS_WEB_ORGEMPLOY_570|Unauthorised User opening org employee update form||0|1|1|testNegUnAuthorisedUserOpenOrganizationUpdateForm|
|1.0| Update |ut_N_u_GSTS_WEB_ORGANIZATION_580|Unauthorised User does not have permission to update| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>=6 and length<=256 3.null|0|1|1|testNegUnAuthorisedUserUpdateOrganization|
|1.0| View |ut_n_v_GSTS_WEB_ORGANIZATION_270|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewOrganization|
|1.0| Search |ut_n_s_GSTS_WEB_ORGANIZATION_340|Unauthorised User does not have permission to search|**name:** 1.valid characters 2.length>=3 and length<=64 3.null **orgType:** enums **surveyStatus:** enums **pincode:** 1.Start with 5 2.length= 6 3.valid characters[0-9] 4.null|0|1|1|testNegUnAuthorisedUserSearchOrganization|
|1.0| List |ut_n_l_GSTS_WEB_ORGANIZATION_300|Unauthorised User does not have permission to list||0|1|1|testNegUnAuthorisedUserGetOrganizationList|
|1.0| PDF |ut_n_ep_GSTS_WEB_ORGANIZATION_470 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportORGANIZATIONeePdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_ORGANIZATION_480 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportORGANIZATIONeeListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_ORGANIZATION_490 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportORGANIZATIONeeXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_ORGANIZATION_500 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportORGANIZATIONeeListXlxWithValidId|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|---------|
|1.0|Create|ut_p_c_GSTS_WEB_ORGANIZATION_100|Create District Organization| N/A |will be created|1|testCreateDistOrg|
|1.0|Create|ut_p_c_GSTS_WEB_ORGANIZATION_110|Create Division Organization| N/A |will be created|1|testCreateDivOrg|
|1.0|Create|ut_p_c_GSTS_WEB_ORGANIZATION_120|Create Mandal Organization| N/A |will be created|1|testCreateMandalOrg|
|1.0|Create|ut_p_c_GSTS_WEB_ORGANIZATION_130|Create Panchayat Organization| N/A |will be created|1|testCreatePanchayatOrg|
|1.0|Create|ut_n_c_GSTS_WEB_ORGANIZATION_190|Create Organization at Panchayat level with Authorised User| N/A |Will not be Created|1|testAuthorisedUserCreateOrganizationAtPanchayatLevel|
|1.0|View|ut_n_c_GSTS_WEB_ORGEMPLOY_590|Panchayat1112 user trying to access Panchayat1111 Org Employee which does not belongs to his context| N/A |Will not be accessed|1|testNegPanchayat1112UserAccessingPanchayat1111Organization|
|1.0|View|ut_n_c_GSTS_WEB_ORGEMPLOY_600|Mandal112 user trying to access Mandal111 Organization which does not belongs to his context| N/A |Will not be accessed|1|testNegMandal112UserAccessingMandal111Organization|
|1.0|View|ut_n_c_GSTS_WEB_ORGEMPLOY_610|District2 user trying to access District1 Organization which does not belongs to his context| N/A |Will not be accessed|1|testNegDistrict2UserAccessingDistrict1Organization|


## Security compliance check
1. Only user having the permission **ROLE_ORGANIZATION_VIEW** should view this functionality 
1. Only user having the permission **ROLE_ORGANIZATION_CREATE** should create this functionality 
1. Only user having the permission **ROLE_ORGANIZATION_UPDATE** should update this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the ORGANIZATIONs in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
