---
title: GS0015 - Organization Employs
tags : ["Composing"]
---

## Introduction
Product can be used at various levels of organizations. Each Panchayat has secretary and sarpanch to perform their roles. Organization Employs feature will list the details of sarpanch and secretary in all panchayat level organizations.

## Business Assumptions
Creating, updating and removing the organization employs can be done at the run time based on the requirement.

## Requirements
### Functional Requirements
1. Only Panchayat level organization has Sarpanch and secretary officers.
2. Appointed date and Qualification of the organization employs are also stored.
3. It is accessible at panchayat level only.

### Non-functional Requirements
Organization Employ feature has Create, Update, and Remove Features only.

### Problem Statement
Organization Employs feature is required to store the organization secretary and sarpanch information.

### Design 
1. Each organization employ has aid, name, gender, mobile, designation, qualification, and dob.
1. We can create, update, view, export and remove the organization employ.
1. Only one Active organization employee is allowed with given aadhaar number.
1. Only one Active panchayat president and one Active panchayat secretary is allowed in the panchayat.
1. Age of organization employee should be greater than or equal to 15 years.
1. In organization employee update if relieving date is not null, set the object state to Removed.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	
|Organization|[gs0009-organizations]({{< ref "gs0009-organizations" >}})|Organization Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_org_employ_list|Provide a List page to view all the Organization Employs, Even this listing page should bind to a permission|
|uc_org_employ_create|Provide a Create page to create the Organization Employ, Even this create page should bind to a permission|
|uc_org_employ_update|Provide a Update page to update the Organization Employ, Even this update page should bind to a permission|
|uc_org_employ_remove|Provide a Remove page to remove the Organization Employ, Even this remove page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|--------|----|----|------|-------|
|aid|YES|NA|0-9,maxlen=12|@Column(name = "aid", length = 12, nullable = false)|aid varchar(12) NOT NULL|YES|NO|YES|YES|YES|YES||
|name|YES|NA|a-zA-Z0-9. _-,minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|YES|YES|YES|YES|NO||
|surname|YES|NA|a-zA-Z0-9. _-,minlen=1, maxlen=32|@Column(name = "surname", length = 32, nullable = false)|surname varchar(32) NOT NULL|YES|YES|YES|YES|YES|NO||
|fsname|YES|NA|a-zA-Z0-9. _-,minlen=3, maxlen=64|@Column(name = "fsname", length = 64, nullable = false)|fsname varchar(64) NOT NULL|YES|YES|YES|YES|NO|NO||
|email|NO|NA|a-zA-Z0-9._@,minlen=3, maxlen=64|@Column(name = "email", length = 64, nullable = true)|email varchar(64) DEFAULT NULL|YES|YES|YES|YES|YES|NO||
|gender|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "gender", length = 8, nullable = false)|gender varchar(8) NOT NULL|YES|YES|YES|YES|NO|NO||
|dob|YES|NA|Date dd-MM-YYYY|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "dob", nullable = false)|dob datetime NOT NULL|YES|YES|YES|YES|NO|NO||
|qualification|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "qualification", length = 24, nullable = false)|qualification varchar(24) NOT NULL|YES|YES|YES|YES|NO|NO||
|designation|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "designation", length = 32, nullable = false)|designation varchar(32) NOT NULL|YES|YES|YES|YES|YES|YES||
|appointed date|YES|NA|Date dd-MM-YYYY From now to past 15 years|@DateTimeFormat(pattern = "dd-MM-yyyy")@Temporal(TemporalType.TIMESTAMP)	@Column(name = "appointed_date", nullable = false)|appointed_date datetime NOT NULL|YES|YES|YES|YES|YES|YES||
|relievingDate|NO|NA|Date dd-MM-YYYY|@DateTimeFormat(pattern = "dd-MM-yyyy")@Temporal(TemporalType.TIMESTAMP)	@Column(name = "relieving_date", nullable = true)|relieving_date datetime DEFAULT NULL|NO|YES|YES|YES|NO|NO||
|mobile|YES|NA|0-9, maxlen=13|@Column(name = "mobile", length = 13, nullable = false)|mobile varchar(13) NOT NULL|YES|YES|YES|YES|YES|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|NO|NO|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

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

##### Designation Type

{{<mermaid align="left">}}
classDiagram
    class DesignationType{
	 	PANCHAYAT_PRESIDENT
	 	PANCHAYAT_SECRETARY
	 	PANCHAYAT_WARD_MEMBER 
	 	CONTRACT_EMPLOYEE
    }
{{< /mermaid >}}

##### Education Qualification 

{{<mermaid align="left">}}
classDiagram
    class Name{
      NURSERY 
      PRIMARY 
      SECONDARY 
      SSC 
      ITI 
      INTERMEDIATE 
      DIPLOMA 
      GRADUATE 
      POST_GRADUATE 
      DOCTORATE
      NONE 
      OTHER 
    }
{{< /mermaid >}} 
   
#### Feature Permission

|Permission code|Action|
|---------------|-------|
|ORGEMPLOY_VIEW|View|
|ORGEMPLOY_CREATE|Create|
|ORGEMPLOY_UPDATE|Update|
|ORGEMPLOY_REMOVE|Remove|
|ORGEMPLOY_VIEW|Export|
|ORGEMPLOY_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_ORGEMPLOY_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_ORGEMPLOY_UPDATE|Only user having the user role with this permission should update this functionality|
|AC_ROLE_ORGEMPLOY_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_ORGEMPLOY_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_ORGEMPLOY_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|


## User Experience
1. Create page based on the standard UX Listing Template
1. Update page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreateBtn[Create]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="left">}}
flowchart TD
	OrgEmployMenu((Org Employ Menu))
	ListPage{Org Employ List Page}
	CreatePage((Create Page))
	RemovePage((Remove Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->OrgEmployMenu
    subgraph Menu
    OrgEmployMenu
    end
    subgraph   
    OrgEmployMenu-->ListPage
    ListPage--C-R-V-E-->ListPage
    end
    subgraph  
    OrgEmployMenu--F-->ErrorPage
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
|U|Update|
|R|Remove|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|SB|Submit or Back|
|VE|View or Export|
|C-U-R|Create or Update or Remove|
|Green Arrow|Success|
|Red Arrow|Failure|

### Sequence Diagram
1. Only a user with the ORGEMPLOY_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant OrgEmployListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet, GET /app/ctx/OrgEmploy/list ListPage
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: S:  GET /app/ctx/OrgEmploy/list ListPage
        cloud-->>-OrgEmployListPage: RES:List Page
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet, GET /app/OrgEmploy/create/form CreateFormPage
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: S : GET /app/OrgEmploy/create/form CreateFormPage
        cloud-->>-OrgEmployListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet: POST /app/OrgEmploy/create Create
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: S : POST /app/OrgEmploy/create Create
        cloud-->>-OrgEmployListPage: RES: An Organization Employ Successfully Created
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet: GET /app/OrgEmploy/update/form UpdateFormPage
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: GET /app/OrgEmploy/update/form UpdateFormPage
        cloud-->>-OrgEmployListPage: RES: Update Form Loaded
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet: POST /app/OrgEmploy/update update
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: S : POST /app/OrgEmploy/update Update
        cloud-->>-OrgEmployListPage: RES: An Organization Employ Successfully Updated
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet: GET /app/OrgEmploy/remove/form RemoveFormPage
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: S : GET /app/OrgEmploy/remove/form RemoveFormPage
        cloud-->>-OrgEmployListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet: POST /app/OrgEmploy/remove Remove
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: S : POST /app/OrgEmploy/remove Remove
        cloud-->>-OrgEmployListPage: RES: An Organization Employ Successfully Removed
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet: GET /app/OrgEmploy/view ViewPage
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: GET /app/OrgEmploy/view ViewPage
        cloud-->>-OrgEmployListPage: RES: Organization Employ View
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet: GET /app/OrgEmploy/exportPdf ExportPdf
        Net--x-OrgEmployListPage: F : Connection Error 
        OrgEmployListPage->>+cloud: GET /app/OrgEmploy/exportPdf ExportPdf
        cloud-->>-OrgEmployListPage: RES: Organization Employ Pdf
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet: GET /app/OrgEmploy/exportListPdf ExportListPdf
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: S : GET /app/OrgEmploy/exportListPdf ExportListPdf
        cloud-->>-OrgEmployListPage: RES: Organization Employ List Pdf
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet: GET /app/OrgEmploy/exportXlx ExportXlx
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: GET /app/OrgEmploy/exportXlx ExportXlx
        cloud-->>-OrgEmployListPage: RES: Organization Employ Xlx
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet: GET /app/OrgEmploy/exportListXlx ExportListXlx
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: S : GET /app/OrgEmploy/exportListXlx ExportListXlx
        cloud-->>-OrgEmployListPage: RES: Organization Employ List Xlx
    end
    rect rgb(244,244,244)
        OrgEmployListPage->>+Net: Check Internet: GET /app/OrgEmploy/download DownloadCopy
        Net--x-OrgEmployListPage: F : Connection Error
        OrgEmployListPage->>+cloud: S : GET /app/OrgEmploy/download DownloadCopy
        cloud-->>-OrgEmployListPage: RES: Organization Employ Copy
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------|--------|
|1.0| Create Form |ut_p_c_GSTS_WEB_ORGEMPLOY_120 |**Positive Test Cases:** Open Organization Employee Create Form at panchayat level with Authorised User|-|1||1|testPosOpenOrgEmployeeCreateFormAtPanchayatLevelWithAuthorisedUser|
|1.0| Create |ut_p_c_GSTS_WEB_ORGEMPLOY_150  ut_n_c_GSTS_WEB_ORGEMPLOY_160   ut_n_c_GSTS_WEB_ORGEMPLOY_140 ut_n_c_GSTS_WEB_ORGEMPLOY_162 ut_n_c_GSTS_WEB_ORGEMPLOY_163 ut_n_c_GSTS_WEB_ORGEMPLOY_164|**Positive Test Cases:** Creating Panchayat Level Organization Employee  with Authorised User   **Negative Test Cases:** 1.Creating Panchayat Level Organization Employee with invalid inputs 2.Create Org Employee without db connection  3.Create Org Employee when an active employee already exists with given aadhaar number 4.Create Org Employee with designation panchayat president when an active president already exists 5.Create Org Employee with designation panchayat secretary when an active secretary already exists|**aid:** 1.valid characters 2.null 3.length==12 **name:** 1.valid characters 2.length>=3 and length<=64 3.null **surname:** 1.valid characters 2.length>=1 and length<=32 3.null   **fsname:** 1.valid characters 2.length>=3 and length<=64 3.null **gender:** enums **mobile:** 1.valid characters 2.length==10 3.null   **email:** 1.valid characters 2.null 3.not mandatory **dob:** 1.null 2.valid date **appointedDate:** 1.null 2.valid date **qualification:** enums **designation:** enums **frontPhoto:** 1.image upload|12|4|16|testPosAuthorisedUserCreatePanchayatLevelOrgEmployWithValidInputs,  testNegAuthorisedUserCreateOrgEmployWithInvalidInputs,  testNegCreateOrgEmployeeWithoutDBconnection,  testNegAuthorisedUserCreateOrgEmployWhenActiveEmployAlreadyExistsWithGivenAadharNumber,  testNegAuthorisedUserCreateOrgEmployWithDesignationPresidentSyncWhenActivePresidentAlreadyExists, testNegAuthorisedUserCreateOrgEmployWithDesignationSecretarySyncWhenActiveSecretaryAlreadyExists|
|1.0| Create |ut_n_c_GSTS_WEB_ORGEMPLOY_165 |**Negative Test Cases:** Create Org Employee without image attachment|-||1|1|testNegCreateOrgEmployeeWithoutImageAttachment|
|1.0| Update Form |ut_p_u_GSTS_WEB_ORGEMPLOY_180   ut_n_u_GSTS_WEB_ORGEMPLOY_190   ut_n_u_GSTS_WEB_ORGEMPLOY_200 |**Positive Test Cases:** Open Org Employee update form with valid Id at panchayat level   **Negative Test Cases:**  1.Open Org Employee Update Form Without DB Connection 2. Open Org Employee Update Form with Invalid id |Id|1|2|3|testPosAuthorisedUserOpenOrgEmployeeUpdateFormWithValidIdAtPanchayatLevel,  testNegAuthorisedUserOpenOrgEmployeeUpdateFormWithoutDBConnection,  testNegAuthorisedUserOpenOrgEmployeeUdpateFormWithInValidId|
|1.0| Update |ut_p_u_GSTS_WEB_ORGEMPLOY_210  ut_n_u_GSTS_WEB_ORGEMPLOY_220   ut_n_u_GSTS_WEB_ORGEMPLOY_230 ut_n_u_GSTS_WEB_ORGEMPLOY_240 ut_n_u_GSTS_WEB_ORGEMPLOY_470  ut_n_u_GSTS_WEB_ORGEMPLOY_223 ut_n_u_GSTS_WEB_ORGEMPLOY_223 ut_n_u_GSTS_WEB_ORGEMPLOY_225|**Positive Test Cases:** Update Panchayat Level Org Employee with valid inputs    **Negative Test Cases:** 1. Updating Organization Employee with Invalid inputs   2. updating without db connection 3.Update Org Employee with Invalid Id 4.Update already removed Org Employee  5.Update Org Employee Designation to President when an other active president already exists 6.Update Org Employee Designation to Panchayat Secretary when an other active Secretary already exists|**relievingDate:** 1.null 2.valid date 3.not Mandatory **updateComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|6|7|testPosAuthorisedUserUpdatePanchayatLevelOrgEmployWithValidInputs,  testNegAuthorisedUserUpdatePanchayatLevelOrgEmployWithInvalidInputs,  testNegUpdateOrgEmployeeWithoutDbConnection,  testNegAuthorisedUserUpdateOrgEmployeeWithInvalidId,  testNegAuthorisedUserUpdateAlreadyRemovedOrgEmployee, testNegAuthorisedUserUpdateOrgEmployDesignationPresident,  testNegAuthorisedUserUpdateOrgEmployDesignationSecretary|
|1.0| Remove Form |ut_p_r_GSTS_WEB_ORGEMPLOY_380   ut_n_r_GSTS_WEB_ORGEMPLOY_390   ut_n_r_GSTS_WEB_ORGEMPLOY_400 ut_n_r_GSTS_WEB_ORGEMPLOY_460|**Positive Test Cases:** Open Org employee remove Form with valid Id at panchayat level   **Negative Test Cases:**  1.Open Org Employee remove Form Without DB Connection 2. Open Org Employee remove Form with Invalid id   3.Open Org Employee remove form with Already removed Org Employee Id with Authorised user|Id|1|3|4|testPosAuthorisedUserOpenPanLevelOrgEmployeeRemoveFormWithValidId,  testNegAuthorisedUserOpenOrgEmployeeRemoveFormWithoutDBConnection,  testNegAuthorisedUserOpenOrgEmployeeRemoveFormWithInValidId,  testNegAuthorisedUserOpenOrgEmployeeRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_ORGEMPLOY_410  ut_n_r_GSTS_WEB_ORGEMPLOY_420 ut_n_r_GSTS_WEB_ORGEMPLOY_440 ut_n_r_GSTS_WEB_ORGEMPLOY_450 ut_n_r_GSTS_WEB_ORGEMPLOY_480 |**Positive Test Cases:** Removing Panchayat Level Org Employee with valid remove comment   **Negative Test Cases:** 1. Remove Org Employee with InValid Remove Comment 2. Remove  Org Employee without DB connection  3. Remove already removed Org Employee with Authorised User 4. Remove Org Employee with invalid id| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|testPosAuthorisedUserRemovePanLevelOrgEmployeeWithValidRemoveCommentAndValidId,  testNegAuthorisedUserRemoveOrgEmployeeWithInValidRemoveCommentAndValidId,  testNegRemoveOrgEmployeeWithoutDbConnection,  testNegAuthorisedUserRemoveAlreadyRemovedOrgEmployee,  testNegPanLevelAuthorisedUserRemoveOrgEmployeeWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_ORGEMPLOY_590 ut_n_v_GSTS_WEB_ORGEMPLOY_600 ut_n_v_GSTS_WEB_ORGEMPLOY_610 |**Positive Test Cases:** View Organization Employee with Valid Id **Negative Test Cases:** 1. without db connection 2. View Organization Employee with Invalid ID ||1|2|3|testPosAuthorisedUserViewOrgEmployeeWithValidId,  testNegAuthorisedUserViewOrgEmployeeWithoutDbConnection,  testNegAuthorisedUserViewOrgEmployeewithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_ORGEMPLOY_740 ut_n_s_GSTS_WEB_ORGEMPLOY_750 ut_n_s_GSTS_WEB_ORGEMPLOY_760 |**Positive Test Cases:** Search Org Employee with valid inputs **Negative Test Cases:** 1.Search Org Employee without db connection 2.Search Org Employee with invalid inputs with Authorised User|**1.aid 2.name 3.surname 4.gender 5.mobile 6.dob 7.appointedDate 8.designation**|11|6|17|testPosAuthorisedUserSearchOrgEmployeWithValidInputs,  testNegAuthorisedUserSearchOrgEmployeeWithoutDBconnection,  testPosAuthorisedUserSearchOrgEmployeWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_ORGEMPLOY_670 ut_n_l_GSTS_WEB_ORGEMPLOY_680|**Positive Test Cases:** Get Org Employee List **Negative Test Cases:** Access Org Employee List without db connection||1|1|2|testPosAuthorisedUserGetOrgEmployeeList,  testNegAuthorisedUserOrgEmployeeListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_ORGEMPLOY_810   ut_n_ep_GSTS_WEB_ORGEMPLOY_820   ut_n_ep_GSTS_WEB_ORGEMPLOY_830 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportOrgEmployeePdfWithValidId,  testNegAuthorisedUserExportOrgEmployeePdfwithoutDbconnection,  testNegAuthorisedUserExportOrgEmployeePdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_ORGEMPLOY_840   ut_n_elp_GSTS_WEB_ORGEMPLOY_850   ut_n_elp_GSTS_WEB_ORGEMPLOY_860 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportOrgEmployeeListPdfWithValidId,  testNegAuthorisedUserExportOrgEmployeeListPdfwithoutDbconnection,  testNegAuthorisedUserExportOrgEmployeeListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_ORGEMPLOY_870   ut_n_ex_GSTS_WEB_ORGEMPLOY_880   ut_n_ex_GSTS_WEB_ORGEMPLOY_890 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportOrgEmployeeXlxWithValidId,  testNegAuthorisedUserExportOrgEmployeeXlxwithoutDbconnection,  testNegAuthorisedUserExportOrgEmployeeXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_ORGEMPLOY_900   ut_n_elx_GSTS_WEB_ORGEMPLOY_910   ut_n_elx_GSTS_WEB_ORGEMPLOY_920 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportOrgEmployeeListXlxWithValidId,  testNegAuthorisedUserExportOrgEmployeeListXlxwithoutDbconnection,  testNegAuthorisedUserExportOrgEmployeeListXlxInValidId|
|1.0| Download|ut_p_elx_GSTS_WEB_ORGEMPLOY_930   ut_n_elx_GSTS_WEB_ORGEMPLOY_940   ut_n_elx_GSTS_WEB_ORGEMPLOY_950 |**Positive Test Cases:** Download org employee attachment with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.org employee attachment with Invalid Id|Id |1|2|3|testPosAuthorisedUserDownloadOrgEmployeeAttachmentValidId,  testPosAuthorisedUserDownloadOrgEmployeeAttachmentwithoutDbConnection,  testNegAuthorisedUserDownloadOrgEmployeeAttachmentInValidId|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|---|
|1.0| Create |ut_n_c_GSTS_WEB_ORGEMPLOY_170 |Unauthorised User does not have permission to create|***aid:** 1.valid characters 2.null 3.length==12 **name:** 1.valid characters 2.length>=3 and length<=64 3.null   **surname:** 1.valid characters 2.length>=1 and length<=32 3.null **fsname:** 1.valid characters 2.length>=3 and length<=64 3.null **gender:** enums   **mobile:** 1.valid characters 2.length==10 3.null **email:** 1.valid characters 2.null 3.not mandatory **dob:** 1.null 2.valid date **appointedDate:** 1.null 2.valid date **qualification:** enums **designation:** enums **frontPhoto:** 1.image upload|0|1|1|testNegUnAuthorisedUserCreateOrgEmploy|
|1.0| Update Form|ut_n_r_GSTS_WEB_ORGEMPLOY_260|Unauthorised User opening org employee update form||0|1|1|testNegUnAuthorisedUserOpenOrgEmployeeUpdateForm|
|1.0| Update |ut_n_u_GSTS_WEB_ORGEMPLOY_250|Unauthorised User does not have permission to remove|**relievingDate:** 1.null 2.valid date 3.not Mandatory **updateComment:** 1.valid characters 2. length>=6 and length<=255 3.null |1|0|1|testNegUnAuthorisedUserUpdateOrgEmploy|
|1.0| Remove Form|ut_n_r_GSTS_WEB_ORGEMPLOY_570|Unauthorised User opening org employee remove form||0|1|1|testNegUnAuthorisedUserOpenOrgEmployeeRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_ORGEMPLOY_580|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserUpdateOrgEmploy|
|1.0| View |ut_n_v_GSTS_WEB_ORGEMPLOY_660|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewOrgEmploy|
|1.0| Search |ut_n_s_GSTS_WEB_ORGEMPLOY_800|Unauthorised User does not have permission to search|**1.aid 2.name 3.surname 4.gender 5.mobile 6.dob 7.appointedDate 8.designation**|0|1|1|testNegUnAuthorisedUserSearchOrgEmployee|
|1.0| List |ut_n_l_GSTS_WEB_ORGEMPLOY_730|Unauthorised User does not have permission to list||0|1|1|testNegUnAuthorisedUserGetOrgEmployeeList|
|1.0| PDF |ut_n_ep_GSTS_WEB_ORGEMPLOY_1020 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportOrgEmployeePdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_ORGEMPLOY_1030 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportOrgEmployeeListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_ORGEMPLOY_1040 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportOrgEmployeeXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_ORGEMPLOY_1050 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportOrgEmployeeListXlxWithValidId|
|1.0| Download |ut_n_elx_GSTS_WEB_ORGEMPLOY_1060 |Download org employee attachment with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserDownloadOrgEmployeeAttachmentWithValidId|


#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method name|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|-----------|
|1.0|View|ut_n_c_GSTS_WEB_ORGEMPLOY_1110|Panchayat1112 user trying to access Panchayat1111 Org Employee which does not belongs to his context| N/A |Will not be accessed|1|testNegPanchayat1112UserAccessingPanchayat1111OrgEmployee|
|1.0|Remove|ut_n_r_GSTS_WEB_ORGEMPLOY_1150|Panchayat1112 user trying to remove Panchayat1111 Org Employee which does not belongs to his context| N/A |Will not be removed|1|testNegPanchayat1112UserRemovingPanchayat1111OrgEmployee|
|1.0|Update|ut_n_u_GSTS_WEB_ORGEMPLOY_1190|Panchayat1112 user trying to update Panchayat1111 Org Employee which does not belongs to his context| N/A |Will not be removed|1|testNegPanchayat1112UserUpdatingPanchayat1111OrgEmployee|

## Security compliance check

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Organization Employ in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
