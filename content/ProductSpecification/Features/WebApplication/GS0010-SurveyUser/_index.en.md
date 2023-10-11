---
title: GS0010 - Survey User
tags : ["Composing"]
---

## Introduction
Survey User are one of the basic building blocks of the software product. Survey user is the person who surveys the all citizen data and stores the information in the application. Survey user is approved and converted to user and the default login for the user is api login.

## Business Assumptions
Survey User Feature should be planned at the design phase and updates to the survey user at the run time based on the requirement.

## Requirements
### Functional Requirements
1. Survey user feature is accessible at all levels of organization.
1. Survey user would be converted as user to access the application.
1. Only one survey user is allowed with one aadhaar number.
1. Only one survey user is allowed with one mobile number, email, and one device.

### Non-functional Requirements
1. Until survey user is approved, survey user has no permission to access the application.
1. Limited access is given to survey user.

### Problem Statement
Survey User feature holds the information of all citizens who are registered as survey user.

### Design 
1. We can create, update, remove, delete, approve and view the survey user.
1. Each Survey User has Name, Aadhaar Number, Mobile Number, Email, Survey Company Name, Mobile manufacturer, Mobile Model, and Device UUID.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	
|Users|[gs0004-users]({{< ref "gs0004-users" >}})|User Page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_survey_user_list|To view all the survey users|
|uc_survey_user_search|To search the survey user|
|uc_survey_user_create|To create the survey user|
|uc_survey_user_update|To update the survey user|
|uc_survey_user_remove|To remove the survey user|
|uc_survey_user_delete|To delete the survey user|
|uc_survey_user_approve|To approve the survey user|
|uc_survey_user_view|To view the survey user|
|uc_survey_user_export|To export the survey user in 2 formats Excel, PDF|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|Delete|Approve|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|--------|----|----|------|-------|----|
|aadharId|YES|NA|0-9,maxlen=12|@Column(name = "aadhar_id", length = 12, nullable = false, unique = true)|aadhar_id varchar(12) NOT NULL|YES|NO|YES|YES|NO|YES|YES|YES||
|name|YES|NA|a-zA-Z0-9. _-,minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|YES|YES|YES|NO|YES|YES|YES||
|surName|YES|NA|a-zA-Z0-9. _-,minlen=1, maxlen=64|@Column(name = "sur_name", length = 32, nullable = false)|sur_name varchar(32) NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|spouseName|YES|NA|a-zA-Z0-9. _-,minlen=3, maxlen=64|@Column(name = "spouse_name", length = 64, nullable = false)|spouse_name varchar(64) NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|gender|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "gender", length = 6, nullable = false)|gender varchar(6) NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|dob|YES|NA|Date dd-MM-YYYY|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "dob", nullable = false)|dob datetime NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|marriedStatus|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "married", length = 16, nullable = false)|married varchar(16) NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|surveyCompanyName|YES|NA|Drop Down Values|@Column(name = "survey_company_name", length = 64, nullable = false)|survey_company_name varchar(64) NOT NULL|YES|NO|YES|YES|NO|YES|NO|YES||
|geoLat|YES|NA|0-9.|@Column(name = "geo_lat", length = 24, nullable = false)|geo_lat varchar(24) NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|geoLng|YES|NA|0-9.|@Column(name = "geo_lng", length = 24, nullable = false)|geo_lng varchar(24) NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|mobileNumber|YES|NA|0-9, maxlen=10|@Column(name = "mobile_number", length = 14, nullable = false, unique = true)|mobile_number varchar(14) NOT NULL|YES|NO|YES|YES|NO|YES|YES|YES||
|mobileNumber2|NO|NA|0-9, maxlen=10|@Column(name = "mobile_number2", length = 14, nullable = true)|mobile_number2 varchar(14) DEFAULT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|email|YES|NA|a-zA-Z0-9._@|@Column(name = "email", length = 64, nullable = false, unique = true)|email varchar(64) NOT NULL|YES|NO|YES|YES|NO|YES|YES|YES||
|email2|NO|NA|a-zA-Z0-9._@|@Column(name = "email2", length = 64, nullable = true)|email2 varchar(64) DEFAULT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|address|YES|NA|a-zA-Z0-9/:#, _-,minlen=6, maxlen=128|@Column(name = "address", length = 128, nullable = false)|address varchar(128) NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|make|YES|NA|Drop Down Values|@Column(name = "make", length = 16, nullable = false)|make varchar(16) NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|model|YES|NA|a-zA-Z0-9. _-,minlen=1, maxlen=64|@Column(name = "model", length = 24, nullable = false)|model varchar(24) NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|os|YES|NA|Drop Down Values|@Column(name = "os", length = 16, nullable = false)|os varchar(16) NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|osver|YES|NA|Drop Down Values|@Column(name = "os_ver", length = 16, nullable = false)|os_ver varchar(16) NOT NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|isp|NO|NA|Drop Down Values|@Column(name = "isp", length = 64, nullable = true)|isp varchar(64) NULL|YES|YES|YES|YES|NO|YES|NO|NO||
|devUuid|YES|NA|a-zA-Z0-9|@Column(name = "dev_uuid", length = 64, nullable = false, unique = true)|dev_uuid varchar(64) NOT NULL|YES|NO|YES|YES|NO|YES|YES|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|NO|NO|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|NO|YES|YES|NO|NO||
|deleteComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "delete_comment", nullable = true)|delete_comment varchar(255) DEFAULT NULL|NO|NO|NO|YES|NO|NO|NO|NO||

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

##### Marital Status

{{<mermaid align="left">}}
classDiagram
    class MaritalStatus{
      SINGLE
      MARRIED
      DIVORCED
      WIDOWED
      SEPERATED
      SPOUSE_DEAD
      LIVING_RELATION
    }
{{< /mermaid >}}

##### Mobile Manufacturer

{{<mermaid align="left">}}
classDiagram
    class MobileManufacturer{
        ACER
        ALCATEL
	  	AMAZON
		AMOI
		APPLE
		ASUS
		BENQ
		BIRD
		BLACKBERRY
		BQ
		CASIO
		CAT
		CELKON
		CHEA
		COOLPAD
		DELL
		GIONEE
		GOOGLE
		HAIER
		HONOR
		HP
		HTC
		HUAWEI
		I-MATE
		I-MOBILE
		ICEMOBILE
		INFINIX
		INNOSTREAM
		INQ
		INTEX
		JOLLA
		KARBONN
		KYOCERA
		LAVA
		LEECO
		LENOVO
		LG
		MAXON
		MEIZU
		MICROMAX
		MICROSOFT
		MITAC
		MITSUBISHI
		MODU
		MOTOROLA
		MWG
		NEC
		NEONODE
		NIU
		NOKIA
		NVIDIA
		O2
		ONEPLUS
		OPPO
		ORANGE
		PANASONIC
		PHILIPS
		QTEK
		RAZER
		REALME
		SAMSUNG
		SENDO
		SHARP
		SIEMENS
		SONIM
		SONY
		SONY ERICSSON
		SPICE
		T-MOBILE
		TCL
		TECNO
		TEL.ME.
		TELIT
		THURAYA
		TOSHIBA
		ULEFONE
		UNNECTO
		VERTU
		VERYKOOL
		VIVO
		VK MOBILE
		VODAFONE
		WIKO
		WND
		XCUTE
		XIAOMI
		XOLO
		YEZZ
		YOTA
		YU
		ZTE
		OTHER
    }
{{< /mermaid >}}

##### Mobile OS

{{<mermaid align="left">}}
classDiagram
    class MobileOS{
      Android
    }
{{< /mermaid >}}

##### OS Version

{{<mermaid align="left">}}
classDiagram
    class OSVersion{
      5
      6
      7
      8
      9
      10
    }
{{< /mermaid >}}

##### Internet Service Provider

{{<mermaid align="left">}}
classDiagram
    class ISP{
      AIRTEL
      JIO
      IDEA
      BSNL
      MTNL
    }
{{< /mermaid >}}

#### Feature Permission

|Permission code|Action|
|---------------|-------|
|SURVEY_USER_CREATE|Create|
|SURVEY_USER_UPDATE|Update|
|SURVEY_USER_REMOVE|Remove|
|SURVEY_USER_DELETE|Delete|
|SURVEY_USER_UPDATE|Approve|
|SURVEY_USER_VIEW|View|
|SURVEY_USER_VIEW|Export|
|SURVEY_USER_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Keys|1. uk__gs_survey_user__mobile_number (mobile_number)|
||2. uk__gs_survey_user__email (email)|
||3. uk__gs_survey_user__aadhar_id (aadhar_id)|
||4. uk__gs_survey_user__dev_uuid (dev_uuid)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_SURVEY_USER_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_SURVEY_USER_UPDATE|Only user having the user role with this permission should update this functionality|
|AC_ROLE_SURVEY_USER_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_SURVEY_USER_DELETE|Only user having the user role with this permission should delete this functionality|
|AC_ROLE_SURVEY_USER_UPDATE|Only user having the user role with this permission should approve the survey user|
|AC_ROLE_SURVEY_USER_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_SURVEY_USER_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

## User Experience
1. Create page based on the standard UX Listing Template
1. Update page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Delete page based on the standard UX Listing Template
1. Approve page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreateBtn[Create]---UpdateBtn[Update]---RemoveBtn[Remove]---DeleteBtn[Delete]---ApproveBtn[Approve]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="left">}}
flowchart TD
	UserMenu((Survey User Menu))
	ListPage{Survey User List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
	RemovePage((Remove Page))
	DeletePage((Delete Page))
	ApprovePage((Approve Page))
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
    ListPage--C-U-R-D-A-V-E-->ListPage
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
    subgraph Approve
    ListPage--A-->ApprovePage
    ApprovePage--SB-->ListPage
    ApprovePage--SB-->ApprovePage
    end
    subgraph Download
    ListPage--E-->DownloadFile
    end
    subgraph Delete
    ListPage--D-->DeletePage
    DeletePage--SB-->ListPage
    DeletePage--SB-->DeletePage
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
    linkStyle 21 stroke:green,stroke-width:2px;  
    linkStyle 22 stroke:green,stroke-width:2px;    
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
    linkStyle 10 stroke:red,stroke-width:2px;    
    linkStyle 13 stroke:red,stroke-width:2px;
    linkStyle 16 stroke:red,stroke-width:2px;
    linkStyle 19 stroke:red,stroke-width:2px;
    linkStyle 23 stroke:red,stroke-width:2px;
    
    
{{< /mermaid >}}


|Symbol|Action|
|:-----|:-----|
|C|Create|
|U|Update|
|R|Remove|
|D|Delete|
|A|Approve|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|SB|Submit or Back|
|VE|View or Export|
|C-U-R-A-V-E|Create or Update or Remove or Delete or Approve or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Sequence Diagram
1. Only a user with the SURVEY_USER_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant SurveyUserListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet, GET /app/ctx/SurveyUser/list ListPage
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S:  GET /app/ctx/SurveyUser/list ListPage
        cloud-->>-SurveyUserListPage: RES:List Page
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet, GET /app/SurveyUser/create/form CreateFormPage
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : GET /app/SurveyUser/create/form CreateFormPage
        cloud-->>-SurveyUserListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: POST /app/SurveyUser/create Create
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : POST /app/SurveyUser/create Create
        cloud-->>-SurveyUserListPage: RES: An SurveyUser Successfully Created
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: GET /app/SurveyUser/update/form UpdateFormPage
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : GET /app/SurveyUser/update/form UpdateFormPage
        cloud-->>-SurveyUserListPage: RES: Update Form Loaded
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: POST /app/SurveyUser/update update
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : POST /app/SurveyUser/update Update
        cloud-->>-SurveyUserListPage: RES: An SurveyUser Successfully Updated
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: GET /app/SurveyUser/remove/form RemoveFormPage
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : GET /app/SurveyUser/remove/form RemoveFormPage
        cloud-->>-SurveyUserListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: POST /app/SurveyUser/remove Remove
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : POST /app/SurveyUser/remove Remove
        cloud-->>-SurveyUserListPage: RES: An SurveyUser Successfully Removed
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: Get /app/SurveyUser/active/form ApproveFormPage
        Net--x-SurveyUserListPage: F : Connection Error
		SurveyUserListPage->>+cloud: S : Get /app/SurveyUser/active/form ApproveFormPage
        cloud-->>-SurveyUserListPage: RES: Approve Form Loaded
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: Post /app/SurveyUser/active Approve
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : POST /app/SurveyUser/active Approve
        cloud-->>-SurveyUserListPage: RES: An SurveyUser Successfully Approved
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: GET /app/SurveyUser/view ViewPage
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : GET /app/SurveyUser/view ViewPage
        cloud-->>-SurveyUserListPage: RES: SurveyUser View
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: GET /app/SurveyUser/exportPdf ExportPdf
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : GET /app/SurveyUser/exportPdf ExportPdf
        cloud-->>-SurveyUserListPage: RES: SurveyUser Pdf
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: GET /app/SurveyUser/exportListPdf ExportListPdf
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : GET /app/SurveyUser/exportListPdf ExportListPdf
        cloud-->>-SurveyUserListPage: RES: SurveyUser List Pdf
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: GET /app/SurveyUser/exportXlx ExportXlx
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : GET /app/SurveyUser/exportXlx ExportXlx
        cloud-->>-SurveyUserListPage: RES: SurveyUser Xlx
    end
    rect rgb(244,244,244)
        SurveyUserListPage->>+Net: Check Internet: GET /app/SurveyUser/exportListXlx ExportListXlx
        Net--x-SurveyUserListPage: F : Connection Error
        SurveyUserListPage->>+cloud: S : GET /app/SurveyUser/exportListXlx ExportListXlx
        cloud-->>-SurveyUserListPage: RES: SurveyUser List Xlx
    end
    
          
{{< /mermaid >}}


## Unit Test Cases
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|
|1.0| Create Form |ut_p_c_GSTS_WEB_SURVEYUSER_120 |**Positive Test Cases:** Open Survey User Create Form with Authorised User|-|1||1|
|1.0| Create |ut_p_c_GSTS_WEB_SURVEYUSER_140 |**Negative Test Cases:** Create Survey User without db connection|-||1|1|
|1.0| Create |ut_p_c_GSTS_WEB_SURVEYUSER_150  ut_n_c_GSTS_WEB_SURVEYUSER_160|**Positive Test Cases:** Creating Survey User with valid Inputs with Authorised User **Negative Test Cases:** Creating Survey User with invalid inputs with Authorised User|**aadharId:** 1.valid characters 2.null 3.length==12 4.unique **name:** 1.valid characters 2.length>=3 and length<=64 3.null **surName:** 1.valid characters 2.length>=1 and length<=32 3.null **spouseName:** 1.valid characters 2.length>=3 and length<=64 3.null **gender:** enums **marriedStatus:** enums **surveyCompanyName:** 1.Drop Down Values **geoLat:** **geoLng:** **mobileNumber:** 1.valid characters 2.length==10 3.null 4.unique **mobileNumber2:** 1.valid characters 2.length==10 3.null 4.not mandatory **email:** 1.valid characters 2.null 3.unique **email2:** 1.valid characters 2.null 3.not mandatory **address:** 1.valid characters 2.length>=6 and length<=128 3.null **make:** drop down values **model:** 1.valid characters 2.length>=1 and length<=64 3.null **os:** drop down values **osver:** drop down values **isp:** drop down values **devUuid:** 1.valid characters 2.length>=6 and length<=64 3.null 4.unique **userPassword:** 1.length>=7 and length<=128 2.valid characters 3.null **confirmLoginPassword:** **tshirtSize:** enums **dob:** 1.null 2.valid date **fileName:** 1.image upload|8|11|19|
|1.0| Create |ut_n_c_GSTS_WEB_SURVEYUSER_165 |**Negative Test Cases:** Create Survey User without image attachment|-||1|1|
|1.0| Update Form |ut_p_u_GSTS_WEB_SURVEYUSER_180 ut_p_u_GSTS_WEB_SURVEYUSER_190 ut_p_u_GSTS_WEB_SURVEYUSER_200 |**Positive Test Cases:** Open Survey User Update Form with valid Id with Authorised User **Negative Test Cases:**  1.Open Survey User Update Form Without DB Connection 2. Open Survey User Update Form with Invalid id |Id|1|2|3|
|1.0| Update |ut_p_u_GSTS_WEB_SURVEYUSER_210  ut_n_u_GSTS_WEB_SURVEYUSER_220 ut_n_u_GSTS_WEB_SURVEYUSER_230 ut_n_u_GSTS_WEB_SURVEYUSER_240 ut_p_u_GSTS_WEB_SURVEYUSER_360|**Positive Test Cases:** Updating Survey User with invalid inputs with Authorised User **Negative Test Cases:** 1. Updating Survey User with invalid inputs Authorised User 2. Update Survey User without DB connection 3. Update Survey User with invalid Id 4. Update already removed Survey User with Authorised User| **updateComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|
|1.0| Remove Form |ut_p_r_GSTS_WEB_SURVEYUSER_270 ut_n_r_GSTS_WEB_SURVEYUSER_280 ut_n_r_GSTS_WEB_SURVEYUSER_290 ut_n_r_GSTS_WEB_SURVEYUSER_350|**Positive Test Cases:** Open Survey User remove Form with valid Id with Authorised User **Negative Test Cases:**  1.Open Survey User remove Form Without DB Connection 2. Open Survey User remove Form with Invalid id 3.Open Survey User remove form with Already removed Survey User Id with Authorised user|Id|1|3|4|
|1.0| Remove |ut_p_r_GSTS_WEB_SURVEYUSER_300  ut_n_r_GSTS_WEB_SURVEYUSER_310 ut_n_r_GSTS_WEB_SURVEYUSER_330 ut_n_r_GSTS_WEB_SURVEYUSER_340 ut_n_r_GSTS_WEB_SURVEYUSER_370|**Positive Test Cases:** Removing Survey User with valid remove comment with Authorised User **Negative Test Cases:** 1. Removing Survey User with invalid remove comment with Authorised User  2. Remove Survey User without DB connection 3. Remove already removed Survey User with Authorised User 4. Remove Survey User with invalid id| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|
|1.0| Delete Form |ut_p_d_GSTS_WEB_SURVEYUSER_420 ut_n_d_GSTS_WEB_SURVEYUSER_430 ut_n_d_GSTS_WEB_SURVEYUSER_440|**Positive Test Cases:** Open Survey User delete Form with valid Id with Authorised User **Negative Test Cases:**  1.Open Survey User delete Form Without DB Connection 2. Open Survey User delete Form with Invalid id|Id|1|2|3|
|1.0| Delete |ut_p_d_GSTS_WEB_SURVEYUSER_450  ut_n_d_GSTS_WEB_SURVEYUSER_460 ut_n_d_GSTS_WEB_SURVEYUSER_470 ut_n_d_GSTS_WEB_SURVEYUSER_480 ut_n_r_GSTS_WEB_SURVEYUSER_490 ut_n_r_GSTS_WEB_SURVEYUSER_490|**Positive Test Cases:** Deleting Survey User with valid delete comment with Authorised User **Negative Test Cases:** 1. Deleting Survey User with invalid delete comment Authorised User 2. Delete Survey User without DB connection 3.Delete Active Survey User 4.Delete Survey User with Invalid Id | **deleteComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|
|1.0| Approve Form |ut_p_u_GSTS_WEB_SURVEYUSER_500 ut_p_u_GSTS_WEB_SURVEYUSER_510 ut_p_u_GSTS_WEB_SURVEYUSER_520|**Positive Test Cases:** Open Survey User convert Form with valid Id with Authorised User **Negative Test Cases:**  1.Open Survey User convert Form Without DB Connection 2. Open Survey User convert Form with Invalid id|Id|1|2|3|
|1.0| Approve |ut_p_r_GSTS_WEB_SURVEYUSER_530  ut_n_r_GSTS_WEB_SURVEYUSER_540 ut_n_r_GSTS_WEB_SURVEYUSER_550 ut_n_r_GSTS_WEB_SURVEYUSER_560 |**Positive Test Cases:** Converting Survey User to user with Authorised User **Negative Test Cases:** 1.Convert survey user to user without invalid comment 2.Convert survey user to user without db connection 3. Converting Survey User to user with invalid id| **updateComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|3|4|
|1.0| View |ut_p_v_GSTS_WEB_SURVEYUSER_590  ut_n_v_GSTS_WEB_SURVEYUSER_600 ut_n_v_GSTS_WEB_SURVEYUSER_610 |**Positive Test Cases:** View Survey User with Valid Id  with Authorised User **Negative Test Cases:** 1.View Survey User without db connection 2.View Survey User with Invalid ID with Authorised User||1|2|3|
|1.0| List |ut_p_l_GSTS_WEB_SURVEYUSER_670 ut_p_l_GSTS_WEB_SURVEYUSER_680|**Positive Test Cases:** Access the object list with Authorised User **Negative Test Cases:** Access Survey User List without db connection||1|1|2|
|1.0| Search |ut_p_s_GSTS_WEB_SURVEYUSER_740 ut_n_s_GSTS_WEB_SURVEYUSER_750 ut_n_s_GSTS_WEB_SURVEYUSER_760|**Positive Test Cases:** Search Survey User with valid inputs with Authorised User **Negative Test Cases:** 1.Search survey User without db connection 2.Search Survey User with invalid inputs with Authorised User|**1.aadharId 2.name 3.email 4.mobileNumber 5.surveyCompanyName**|8|5|13|
|1.0| PDF |ut_p_ep_GSTS_WEB_SURVEYUSER_810 ut_n_ep_GSTS_WEB_SURVEYUSER_820 ut_n_ep_GSTS_WEB_SURVEYUSER_830 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|
|1.0| List PDF |ut_p_elp_GSTS_WEB_SURVEYUSER_840 ut_n_elp_GSTS_WEB_SURVEYUSER_850 ut_n_elp_GSTS_WEB_SURVEYUSER_860 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|
|1.0| XLX |ut_p_ex_GSTS_WEB_SURVEYUSER_870 ut_n_ex_GSTS_WEB_SURVEYUSER_880 ut_n_ex_GSTS_WEB_SURVEYUSER_890 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|
|1.0| List XLX |ut_p_elx_GSTS_WEB_SURVEYUSER_900 ut_n_elx_GSTS_WEB_SURVEYUSER_910 ut_n_elx_GSTS_WEB_SURVEYUSER_920 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|
|1.0| List XLX |ut_p_elx_GSTS_WEB_SURVEYUSER_930 ut_n_elx_GSTS_WEB_SURVEYUSER_940 ut_n_elx_GSTS_WEB_SURVEYUSER_950 |**Positive Test Cases:** Download Survey user attachment with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Survey user attachment with Invalid Id|Id |1|2|3|


#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|
|1.0| Create |ut_p_c_GSTS_WEB_SURVEYUSER_170 |Unauthorised User does not have permission to create|**aadharId:** 1.valid characters 2.null 3.length==12 4.unique **name:** 1.valid characters 2.length>=3 and length<=64 3.null **surName:** 1.valid characters 2.length>=1 and length<=32 3.null **spouseName:** 1.valid characters 2.length>=3 and length<=64 3.null **gender:** enums **marriedStatus:** enums **surveyCompanyName:** 1.Drop Down Values **geoLat:** **geoLng:** **mobileNumber:** 1.valid characters 2.length==10 3.null 4.unique **mobileNumber2:** 1.valid characters 2.length==10 3.null 4.not mandatory **email:** 1.valid characters 2.null 3.unique **email2:** 1.valid characters 2.null 3.not mandatory **address:** 1.valid characters 2.length>=6 and length<=128 3.null **make:** drop down values **model:** 1.valid characters 2.length>=1 and length<=64 3.null **os:** drop down values **osver:** drop down values **isp:** drop down values **devUuid:** 1.valid characters 2.length>=6 and length<=64 3.null 4.unique **userPassword:** 1.length>=7 and length<=128 2.valid characters 3.null **confirmLoginPassword:** **tshirtSize:** enums **dob:** 1.null 2.valid date **fileName:** 1.image upload|1|0|1|
|1.0| Update |ut_p_r_GSTS_WEB_SURVEYUSER_250|Unauthorised User does not have permission to update| **updateComment:** 1.valid characters 2. length>=6 and length<=255 3.null |1|0|1|
|1.0| Update Form|ut_p_r_GSTS_WEB_SURVEYUSER_260|Unauthorised User opening survey user update form||1|0|1|
|1.0| Remove Form|ut_p_r_GSTS_WEB_SURVEYUSER_380|Unauthorised User opening survey user remove form||1|0|1|
|1.0| Remove |ut_p_r_GSTS_WEB_SURVEYUSER_390|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |1|0|1|
|1.0| Delete Form|ut_p_r_GSTS_WEB_SURVEYUSER_400|Unauthorised User opening survey user delete form||1|0|1|
|1.0| Delete |ut_p_r_GSTS_WEB_SURVEYUSER_410|Unauthorised User does not have permission to delete| **deleteComment:** 1.valid characters 2. length>=6 and length<=255 3.null |1|0|1|
|1.0| Approve Form|ut_p_r_GSTS_WEB_SURVEYUSER_570|Unauthorised User opening survey user convert form||1|0|1|
|1.0| Approve |ut_p_r_GSTS_WEB_SURVEYUSER_580|Unauthorised User does not have permission to approve| **updateComment:** 1.valid characters 2. length>=6 and length<=255 3.null |1|0|1|
|1.0| View |ut_p_v_GSTS_WEB_SURVEYUSER_660|Unauthorised User does not have permission to view|1.Valid Id|1|0|1|
|1.0| List |ut_p_l_GSTS_WEB_SURVEYUSER_730|Unauthorised User does not have permission to list||1|0|1|
|1.0| Search |ut_p_s_GSTS_WEB_SURVEYUSER_800|Unauthorised User does not have permission to search|**1.aadharId 2.name 3.email 4.mobileNumber 5.surveyCompanyName**|1|0|1|
|1.0| PDF |ut_p_ep_GSTS_WEB_SURVEYUSER_1020 |Export List Pdf with UnAuthorised User|1.Valid Id |1|N/A|1|
|1.0| List PDF |ut_p_elp_GSTS_WEB_SURVEYUSER_1030 |Export Pdf with UnAuthorised User|1.Valid Id |1|N/A|1|
|1.0| XLX |ut_p_ex_GSTS_WEB_SURVEYUSER_1040 |Export XLX with UnAuthorised User|1.Valid Id |1|N/A|1|
|1.0| List XLX |ut_p_elx_GSTS_WEB_SURVEYUSER_1050 |Export List XLX with UnAuthorised User|1.Valid Id |1|N/A|1|
|1.0| Download |ut_p_elx_GSTS_WEB_SURVEYUSER_1060 |Download survey user attachment with UnAuthorised User|1.Valid Id |1|N/A|1|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|


## Security compliance check
1. Only user having the permission **ROLE_SURVEY_USER_VIEW** should view this functionality 
1. Only user having the permission **ROLE_SURVEY_USER_CREATE** should create this functionality 
1. Only user having the permission **ROLE_SURVEY_USER_UPDATE** should update this functionality 
1. Only user having the permission **ROLE_SURVEY_USER_UPDATE** should activate this functionality 
1. Only user having the permission **ROLE_SURVEY_USER_REMOVE** should remove this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Survey User should be provided in the User Manual.

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




 
