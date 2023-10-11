---
title: Kolagaram Property
tags : ["Composing"]
---

## Introduction
Kolagaram Property is one of the basic features of the software product which contains the data of all the kolagaram properties in the Telangana state. By using this kolagaram property feature, we have to store every kolagaram property data and know about every kolagaram property in the state. Every kolagaram property should be stored under the respective panchayat only.

## Business Assumptions
1. Kolagaram Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the kolagaram property.
1. Owner Aadhaar number is required to create the kolagaram property.

## Requirements
### Functional Requirements
1. Kolagaram Property feature only accessible at the panchayat level.
1. While creating kolagaram property, the owner’s aadhaar number will bind to it.
1. Only one kolagaram property is allowed with the same name.

### Non-functional Requirements
1. To create the kolagaram Property, an organization survey status type should be started.
1. Multiple users can create kolagaram property in the same panchayat.
1. One citizen can have multiple kolagaram properties in the same panchayat or different panchayats.

### Problem Statement
Kolagaram Property feature is required to store all the kolagaram property details in the panchayat level.

### Design 
1. Each Kolagaram property has an owner's Aadhaar number, Name, Latitude, Longitude, Kolagaram Category, Motor capacity, Business Sanction Id, and Annual Turn over.
1. We can Create, Update, View, and remove the kolagaram property.
1. Only one kolagaram property is allowed with the same name.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Citizen|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_kolagaram_property_list|To view all the kolagaram properties|
|uc_kolagaram_property_search|To search the kolagaram property|
|uc_kolagaram_property_create|To create the kolagaram property|
|uc_kolagaram_property_update|To update the kolagaram property|
|uc_kolagaram_property_remove|To remove the kolagaram property|
|uc_kolagaram_property_view|To view the kolagaram property|
|uc_kolagaram_property_export|To export the kolagaram property in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9/:#, _\.\-, @, &, Space, minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|NO|YES|YES|YES|YES||
|location|YES|NA|a-zA-Z0-9/:#, _\.\-, @, &, (, ), Space, minlen=3, maxlen=64|@Column(name = "location", length = 64, nullable = false)|location varchar(64) NOT NULL|YES|NO|YES|YES|YES|YES||
|geoLat|YES|NA|0-9.|@Column(name = "geo_lat", length = 24, nullable = false)|geo_lat varchar(24) NOT NULL|YES|NO|YES|YES|NO|NO||
|geoLng|YES|NA|0-9.|@Column(name = "geo_lng", length = 24, nullable = false)|geo_lng varchar(24) NOT NULL|YES|NO|YES|YES|NO|NO||
|kolagaramCategory|YES|NA|DropDown Values|@Enumerated(EnumType.STRING)	@Column(name = "kolg_category", length = 64, nullable = true)|kolg_category varchar(64) DEFAULT NULL|YES|NO|YES|YES|YES|YES||
|motorHorsePower|YES|NA|DropDown Values|@Column(name = "motor_horse_power", nullable = false)|motor_horse_power bigint(20) DEFAULT NULL|YES|YES|YES|YES|NO|NO|ArrayList values of 0-20|
|businessSanctionId|NO|NA|a-zA-Z0-9/:#, _\.\-, Space, @, &|@Column(name = "business_sanction_id", length = 32, nullable = true)|business_sanction_id varchar(32) DEFAULT NULL|YES|NO|YES|YES|NO|NO||
|annualTurnover|NO|NA|0-9|@Column(name = "annual_turnover", nullable = true)|annual_turnover bigint(20) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|frontPhoto|YES|NA|Attachment|@Column(name = "front_photo", length = 36, nullable = false)|front_photo varchar(36) NOT NULL|YES|NO|NO|YES|NO|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Kolagaram Category

{{<mermaid align="left">}}
classDiagram
    class KolagaramCategory{
      BRICKS
      CEMENT_BRICKS
      EGGS
      COMMERCIAL_CROPS
      GLASS_BEADS
      OTHER
      NONE
    }
{{< /mermaid >}}


#### Feature Permission
|Permission code|Action|
|---------------|-------|
|KOLAGARAM_PROPERTY_CREATE|Create|
|KOLAGARAM_PROPERTY_UPDATE|Update|
|KOLAGARAM_PROPERTY_REMOVE|Remove|
|KOLAGARAM_PROPERTY_VIEW|View|
|KOLAGARAM_PROPERTY_VIEW|List|
|KOLAGARAM_PROPERTY_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Keys|1. gs_property__name__category__org_panchayat_id (org_panchayat_id, category, name)|
||2. gs_property__business_sanction_id__category__org_panchayat_id (org_panchayat_id, category, business_sanction_id)|
|Foreign Key|fk__gs_property__caid(caid) REFERENCES gs_citizen (aid)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_KOLAGARAM_PROPERTY_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_KOLAGARAM_PROPERTY_UPDATE|Only user having the user role with this permission should update this functionality|
|AC_ROLE_KOLAGARAM_PROPERTY_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_KOLAGARAM_PROPERTY_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_KOLAGARAM_PROPERTY_VIEW|Only user having the user role with this permission should export the user role in 2 formats Excel, PDF|

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
	KolagaramPropertyMenu((Kolagaram Property Menu))
	ListPage{Kolagaram Property List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->KolagaramPropertyMenu
    subgraph Menu
    KolagaramPropertyMenu
	end
	subgraph List
	KolagaramPropertyMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	KolagaramPropertyMenu-->ErrorPage
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
1. Only a user with the KOLAGARAM_PROPERTY_VIEW permission will be allowed to perform the below operations.

{{<mermaid align="center">}}
sequenceDiagram
    participant KolagaramPropertyListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, GET /app/ctx/KolagaramProperty/list ListPage
        Net--x-KolagaramPropertyListPage: F : Connection Error
        KolagaramPropertyListPage->>+cloud: S:  GET /app/ctx/KolagaramProperty/list ListPage
        cloud-->>-KolagaramPropertyListPage: RES: List Page
    end
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, GET /app/KolagaramProperty/create/form CreateFormPage
        Net--x-KolagaramPropertyListPage: F : Connection Error
        KolagaramPropertyListPage->>+cloud: S : GET /app/KolagaramProperty/create/form CreateFormPage
        cloud-->>-KolagaramPropertyListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, POST /app/KolagaramProperty/create Create
        Net--x-KolagaramPropertyListPage: F : Connection Error
        KolagaramPropertyListPage->>+cloud: S : POST /app/KolagaramProperty/create Create
        cloud-->>-KolagaramPropertyListPage: RES: A Kolagaram Property Successfully Created
    end
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, GET /app/KolagaramProperty/update/form UpdateFormPage
        Net--x-KolagaramPropertyListPage: F : Connection Error
        alt
		note right of Net:  Kolagaram Property Cache Object Found
        KolagaramPropertyListPage->>+Cache: S : GET /app/KolagaramProperty/update/form UpdateFormPage
        Cache-->>-KolagaramPropertyListPage: RES: Update Form Loaded
        else
		note right of Net:  Kolagaram Property Cache Object Not Found
        Cache->>+cloud: GET /app/KolagaramProperty/update/form UpdateFormPage
        cloud-->>-KolagaramPropertyListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, POST /app/KolagaramProperty/update update
        Net--x-KolagaramPropertyListPage: F : Connection Error
        KolagaramPropertyListPage->>+cloud: S : POST /app/KolagaramProperty/update Update
        cloud-->>-KolagaramPropertyListPage: RES: A Kolagaram Property Successfully Updated
    end
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, GET /app/KolagaramProperty/remove/form RemoveFormPage
        Net--x-KolagaramPropertyListPage: F : Connection Error
        alt
		note right of Net:  Kolagaram Property Cache Object Found
        KolagaramPropertyListPage->>+Cache: S : GET /app/KolagaramProperty/remove/form RemoveFormPage
        Cache-->>-KolagaramPropertyListPage: RES : Remove Form Loaded
        else
		note right of Net:  Kolagaram Property Cache Object Not Found
        Cache->>+cloud: S : GET /app/KolagaramProperty/remove/form RemoveFormPage
        cloud-->>-KolagaramPropertyListPage: RES : Remove Form Loaded
        end
    end
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, POST /app/KolagaramProperty/remove Remove
        Net--x-KolagaramPropertyListPage: F : Connection Error
        KolagaramPropertyListPage->>+cloud: S : POST /app/KolagaramProperty/remove Remove
        cloud-->>-KolagaramPropertyListPage: RES: A Kolagaram Property Successfully Removed
    end
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, GET /app/KolagaramProperty/view ViewPage
        Net--x-KolagaramPropertyListPage: F : Connection Error
        alt
		note right of Net:  Kolagaram Property Cache Object Found
        KolagaramPropertyListPage->>+Cache: S : GET /app/KolagaramProperty/view ViewPage
        Cache-->>-KolagaramPropertyListPage: RES: kolagaramProperty View
        else
		note right of Net:  Kolagaram Property Cache Object Not Found
        Cache->>+cloud: GET /app/KolagaramProperty/view ViewPage
        cloud-->>-KolagaramPropertyListPage: RES: kolagaramProperty View
        end
    end
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, GET /app/KolagaramProperty/exportPdf ExportPdf
        Net--x-KolagaramPropertyListPage: F : Connection Error
        alt
		note right of Net:  Kolagaram Property Cache Object Found
        KolagaramPropertyListPage->>+Cache: S : GET /app/KolagaramProperty/exportPdf ExportPdf
        Cache-->>-KolagaramPropertyListPage: RES: kolagaramProperty Pdf
        else
		note right of Net:  Kolagaram Property Cache Object Not Found
        Cache->>+cloud: GET /app/KolagaramProperty/exportPdf ExportPdf
        cloud-->>-KolagaramPropertyListPage: RES: kolagaramProperty Pdf
        end
    end
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, GET /app/KolagaramProperty/exportListPdf ExportListPdf
        Net--x-KolagaramPropertyListPage: F : Connection Error
        KolagaramPropertyListPage->>+cloud: S : GET /app/KolagaramProperty/exportListPdf ExportListPdf
        cloud-->>-KolagaramPropertyListPage: RES: kolagaramProperty List Pdf
    end
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, GET /app/KolagaramProperty/exportXlx ExportXlx
        Net--x-KolagaramPropertyListPage: F : Connection Error
        alt
		note right of Net:  Kolagaram Property Cache Object Found
        KolagaramPropertyListPage->>+Cache: S : GET /app/KolagaramProperty/exportXlx ExportXlx
        Cache-->>-KolagaramPropertyListPage: RES: Kolagaram Property Xlx
        else
		note right of Net:  Kolagaram Property Cache Object Not Found
        Cache->>+cloud: GET /app/KolagaramProperty/exportXlx ExportXlx
        cloud-->>-KolagaramPropertyListPage: RES: kolagaramProperty Xlx
        end
    end
    rect rgb(244,244,244)
        KolagaramPropertyListPage->>+Net: Check Internet, GET /app/KolagaramProperty/exportListXlx ExportListXlx
        Net--x-KolagaramPropertyListPage: F : Connection Error
        KolagaramPropertyListPage->>+cloud: S : GET /app/KolagaramProperty/exportListXlx ExportListXlx
        cloud-->>-KolagaramPropertyListPage: RES: kolagaramProperty List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|-----|
|1.0| Create Form |ut_p_c_GSTS_WEB_KOLAGARAM_PROPERTY_120 ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_130 |**Positive Test Cases:** 1.Open Kolagaram Property Create Form At panchayat level **Negative Test Cases:** 1.Open Kolagaram Property Create Form Without Db connection|-|1|1|2|testPosOpenKolagaramPropertyCreateFormWithAuthorisedUser,  testNegOpenKolagaramPropertyCreateFormWithoutDBConnection|
|1.0| Create |ut_p_c_GSTS_WEB_KOLAGARAM_PROPERTY_150  ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_160 ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_140 |**Positive Test Cases:** Creating Kolagaram Property  with valid inputs with Panchayat Level Authorised User**Negative Test Cases:** Creating Kolagaram Property  with invalid inputs 2.Open Kolagaram Property Create Without Db connection|**citizenId:** 1.Valid Characters 2.length must be 12 3.null **name:** 1.Valid Characters 2.length>=3 and length<=64 3.null 4.unique **location:** 1.Valid Characters 2.length>=3 and length<=64 3.null **geoLat:** **geoLng:** **kolagaramCategory:** Enums **motorHorsePower:** dropdown values **businessSanctionId:** 1.Valid Characters 2.length>=3 and length<=64 3.null 4. unique **annualTurnover:** 1.null 2.length>=3 and length<=10|7|6|13|testPosAuthorisedPanchayatLevelUserCreateKolagaramPropertyWithValidInputs, testNegAuthorisedPanchayatLevelUserCreateKolagaramPropertyWithInValidInputs,  testNegCreateKolagaramPropertyWithoutDBconnection|
|1.0| Create |ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_165 |**Positive Test Cases:** **Negative Test Cases:** 1.Create Kolagaram Property without Image Attachment|-|0|1|1|testNegCreateKolagaramPropertyWithoutImageAttachment|
|1.0| Update Form |ut_p_u_GSTS_WEB_KOLAGARAM_PROPERTY_270   ut_n_u_GSTS_WEB_KOLAGARAM_PROPERTY_280   ut_n_u_GSTS_WEB_KOLAGARAM_PROPERTY_290|**Positive Test Cases:** Open Kolagaram Property update form with valid Id with Authorised Panchayat level user    **Negative Test Cases:**  1.Open Kolagaram Property update Form Without DB Connection 2. Open Kolagaram Property update Form with Invalid id|Id|1|2|3|testPosAuthorisedPanLevelUserOpenKolagaramPropertyUpdateFormWithValidId,  testNegAuthorisedPanLevelUserOpenKolagaramPropertyUpdateFormWithoutDBConnection,  testNegAuthorisedPanLevelUserOpenKolagaramPropertyUdpateFormWithInValidId|
|1.0| Update |ut_p_u_GSTS_WEB_KOLAGARAM_PROPERTY_300  ut_n_u_GSTS_WEB_KOLAGARAM_PROPERTY_310 ut_n_u_GSTS_WEB_KOLAGARAM_PROPERTY_320 ut_n_u_GSTS_WEB_KOLAGARAM_PROPERTY_330 ut_n_u_GSTS_WEB_KOLAGARAM_PROPERTY_470 |**Positive Test Cases:** Updating Kolagaram Property  with valid inputs with Panchayat Level Authorised User **Negative Test Cases:** 1. Updating Kolagaram Property  with invalid inputs 2. Update Kolagaram Property without db connection 3.Update Kolagaram Property with Invalid Id 4.Update removed kolagaram property|**updateComment:** 1.valid characters 2. length>=6 and length<=255 3.null|1|4|5|testPosPanLevelAuthorisedUserUpdateKolagaramPropertyWithValidInputs,  testNegPanLevelAuthorisedUserUpdateKolagaramPropertyWithInValidInputs,  testNegUpdateKolagaramPropertyWithoutDbConnection,  testNegPanLevelAuthorisedUserUpdateKolagaramPropertyWithInvalidId,  testNegAuthorisedUserUpdateAlreadyRemovedKolagaramProperty|
|1.0| Remove Form |ut_p_r_GSTS_WEB_KOLAGARAM_PROPERTY_380   ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_390   ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_400  ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_460|**Positive Test Cases:** Open Kolagaram Property remove form with valid Id with Authorised Panchayat level user    **Negative Test Cases:**  1.Open Kolagaram Property remove Form Without DB Connection 2. Open Kolagaram Property remove Form with Invalid id   3.Open Kolagaram Property remove form with Already removed Kolagaram Property Id with Authorised user|Id|1|3|4|testPosAuthorisedPanLevelUserOpenPanLevelKolagaramPropertyRemoveFormWithValidId,  testNegAuthorisedPanLevelUserOpenKolagaramPropertyRemoveFormWithoutDBConnection,  testNegAuthorisedPanLevelUserOpenKolagaramPropertyRemoveFormWithInValidId,  testNegAuthorisedPanUserOpenKolagaramPropertyRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_KOLAGARAM_PROPERTY_410  ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_420 ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_440  ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_450  ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_480 |**Positive Test Cases:** Remove Kolagaram Property with Valid Remove Comment with Panchayat Level Authorised User **Negative Test Cases:** 1. Removing Kolagaram Property with invalid remove comment 2.Remove Kolagaram Property without db connection 3.Remove already removed Kolagaram Property  4. Remove Kolagaram Property with invalid Id| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|testPosPanLevelAuthorisedUserRemoveKolagaramPropertyWithValidRemoveCommentAndValidId,  testNegPanLevelAuthorisedUserRemoveKolagaramPropertyWithInValidRemoveCommentAndValidId,  testNegRemoveKolagaramPropertyWithoutDbConnection,  testNegAuthorisedUserRemoveAlreadyRemovedKolagaramProperty,  testNegPanLevelAuthorisedUserRemoveKolagaramPropertyWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_KOLAGARAM_PROPERTY_590  ut_n_v_GSTS_WEB_KOLAGARAM_PROPERTY_600 ut_n_v_GSTS_WEB_KOLAGARAM_PROPERTY_610 |**Positive Test Cases:** View Kolagaram Property  with Valid Id  with Authorised User **Negative Test Cases:** 1.View Kolagaram Property without db connection 2.View Kolagaram Property  with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewKolagaramPropertyWithValidId,  testNegAuthorisedUserViewKolagaramPropertyWithoutDbConnection,  testNegAuthorisedUserViewKolagaramPropertywithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_KOLAGARAM_PROPERTY_740  ut_n_s_GSTS_WEB_KOLAGARAM_PROPERTY_750 ut_n_s_GSTS_WEB_KOLAGARAM_PROPERTY_760 |**Positive Test Cases:** Search Kolagaram Property with valid inputs **Negative Test Cases:** 1.Search Kolagaram Property without db connection 2.Search Kolagaram Property  with invalid inputs|1.name 2.kolagaramCategory 3.citizenId 4.location|6|3|9|testPosAuthorisedUserSearchKolagaramPropertyWithValidInputs,  testNegAuthorisedUserSearchKolagaramPropertyWithoutDBconnection,  testNegAuthorisedUserSearchKolagaramPropertyWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_KOLAGARAM_PROPERTY_670 ut_n_l_GSTS_WEB_KOLAGARAM_PROPERTY_680|**Positive Test Cases:** Get Kolagaram Property List with Authorised User **Negative Test Cases:** Get Kolagaram Property List without db connection|Validating with unique field|1|1|2|testPosAuthorisedUserGetKolagaramPropertyList,  testNegAuthorisedUserKolagaramPropertyListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_KOLAGARAM_PROPERTY_810   ut_n_ep_GSTS_WEB_KOLAGARAM_PROPERTY_820   ut_n_ep_GSTS_WEB_KOLAGARAM_PROPERTY_830 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportKolagaramPropertyPdfWithValidId,  testNegAuthorisedUserExportKolagaramPropertyPdfwithoutDbconnection,  testNegAuthorisedUserExportKolagaramPropertyPdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_KOLAGARAM_PROPERTY_840   ut_n_elp_GSTS_WEB_KOLAGARAM_PROPERTY_850   ut_n_elp_GSTS_WEB_KOLAGARAM_PROPERTY_860 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportKolagaramPropertyListPdfWithValidId,  testNegAuthorisedUserExportKolagaramPropertyListPdfwithoutDbconnection,  testNegAuthorisedUserExportKolagaramPropertyListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_KOLAGARAM_PROPERTY_870   ut_n_ex_GSTS_WEB_KOLAGARAM_PROPERTY_880   ut_n_ex_GSTS_WEB_KOLAGARAM_PROPERTY_890 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportKolagaramPropertyXlxValidId,  testNegAuthorisedUserExportKolagaramPropertyXlxwithoutDbconnection,  testNegAuthorisedUserExportKolagaramPropertyXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_KOLAGARAM_PROPERTY_900   ut_n_elx_GSTS_WEB_KOLAGARAM_PROPERTY_910   ut_n_elx_GSTS_WEB_KOLAGARAM_PROPERTY_920 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportKolagaramPropertyListXlxValidId,  testNegAuthorisedUserExportKolagaramPropertyListXlxwithoutDbconnection,  testNegAuthorisedUserExportKolagaramPropertyListXlxInValidId|
|1.0| Download|ut_p_elx_GSTS_WEB_KOLAGARAM_PROPERTY_930   ut_n_elx_GSTS_WEB_KOLAGARAM_PROPERTY_940   ut_n_elx_GSTS_WEB_KOLAGARAM_PROPERTY_950 ut_n_elx_GSTS_WEB_KOLAGARAM_PROPERTY_960 |**Positive Test Cases:** Download Kolagaram Property attachment with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Kolagaram Property attachment with Invalid Id 3.Download Kolagaram Property Attachment with valid Id and Invalid Document type|Id |1|3|4|testPosAuthorisedUserDownloadKolagaramPropertyAttachmentValidId,  testNegAuthorisedUserDownloadKolagaramPropertyAttachmentwithoutDbConnection,  testNegAuthorisedUserDownloadKolagaramPropertyAttachmentInValidId, testNegAuthorisedUserDownloadKolagaramPropertyAttachmentWithValidIdAndInvalidDocType|


#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|-----|
|1.0| Create Form|ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_260|Unauthorised User opening Kolagaram Property create form||0|1|1|testNegUnAuthorisedUserOpenKolagaramPropertyCreateForm|
|1.0| Create |ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_250 |Unauthorised User does not have permission to create|**citizenId:** 1.Valid Characters 2.length must be 12 3.null **name:** 1.Valid Characters 2.length>=3 and length<=64 3.null 4.unique **location:** 1.Valid Characters 2.length>=3 and length<=64 3.null **geoLat:** **geoLng:** **kolagaramCategory:** Enums **motorHorsePower:** dropdown values **businessSanctionId:** 1.Valid Characters 2.length>=3 and length<=64 3.null 4. unique **annualTurnover:** 1.null 2.length>=3 and length<=10|0|1|1|testNegUnAuthorisedUserCreateKolagaramProperty|
|1.0| Update Form|ut_n_u_GSTS_WEB_KOLAGARAM_PROPERTY_370|Unauthorised User opening Kolagaram Property update form||0|1|1|testNegUnAuthorisedPanLevelUserOpenKolagaramPropertyUpdateForm|
|1.0| Update |ut_n_u_GSTS_WEB_KOLAGARAM_PROPERTY_360|Unauthorised User does not have permission to update|**updateComment:** 1.valid characters 2.length >=6 and length<=255 3.null|0|1|1|testNegUnAuthorisedUserUpdateKolagaramProperty|
|1.0| Remove Form|ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_570|Unauthorised User opening Kolagaram Property remove form||0|1|1|testNegUnAuthorisedPanLevelUserOpenKolagaramPropertyRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_580|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserRemoveKolagaramProperty|
|1.0| View |ut_n_v_GSTS_WEB_KOLAGARAM_PROPERTY_660|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewKolagaramProperty|
|1.0| Search |ut_n_s_GSTS_WEB_KOLAGARAM_PROPERTY_800|Unauthorised User does not have permission to search|1.name 2.kolagaramCategory 3.citizenId   4.location|0|1|1|testNegUnAuthorisedUserSearchKolagaramProperty|
|1.0| List |ut_n_l_GSTS_WEB_KOLAGARAM_PROPERTY_730|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserKolagaramPropertyList|
|1.0| PDF |ut_n_ep_GSTS_WEB_KOLAGARAM_PROPERTY_1020 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportKolagaramPropertyPdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_KOLAGARAM_PROPERTY_1030 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportKolagaramPropertyListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_KOLAGARAM_PROPERTY_1040 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportKolagaramPropertyXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_KOLAGARAM_PROPERTY_1050 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportKolagaramPropertyListXlxWithValidId|
|1.0| Download |ut_n_elx_GSTS_WEB_KOLAGARAM_PROPERTY_1060 |Download Kolagaram Property attachment with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserDownloadKolagaramPropertyAttachmentWithValidId|


#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|------------|
|1.0|Create|ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_170|Create Kolagaram Property at State Level| N/A |Will not be Created|1|testNegCreateKolagaramPropertyAtStateLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_180|Open Kolagaram Property Create Form at State Level| N/A |Will not be Opened|1|testNegOpenKolagaramPropertyCreateFormAtStateLevel|
|1.0|Create|ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_190|Create Kolagaram Property at District Level| N/A |Will not be Created|1|testNegCreateKolagaramPropertyAtDistLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_200|Open Kolagaram Property Create Form at District Level| N/A |Will not be Opened|1|testNegOpenKolagaramPropertyCreateFormAtDistLevel|
|1.0|Create|ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_210|Create Kolagaram Property at Division Level| N/A |Will not be Created|1|testNegCreateKolagaramPropertyAtDivLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_220|Open Kolagaram Property Create Form at Division Level| N/A |Will not be Opened|1|testNegOpenKolagaramPropertyCreateFormAtDivLevel|
|1.0|Create|ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_230|Create Kolagaram Property at Mandal Level| N/A |Will not be Created|1|testNegCreateKolagaramPropertyAtMandalLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_KOLAGARAM_PROPERTY_240|Open Kolagaram Property Create Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenKolagaramPropertyCreateFormAtMandalLevel|
|1.0|Update Form|ut_n_u_GSTS_WEB_KOLAGARAM_PROPERTY_340|Open Kolagaram Property update Form at State Level| N/A |Will not be Opened|1|testNegOpenKolagaramPropertyUpdateFormAtStateLevel|
|1.0|Update|ut_n_u_GSTS_WEB_KOLAGARAM_PROPERTY_350|Update Kolagaram Property at State Level| N/A |Will not be updated|1|testNegUpdateKolagaramPropertyAtStateLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_490|Open Kolagaram Property Remove Form at State Level| N/A |Will not be Opened|1|testNegOpenKolagaramPropertyRemoveFormAtStateLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_500|Remove Kolagaram Property at State Level| N/A |Will not be Removed|1|testNegRemoveKolagaramPropertyAtStateLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_510|Open Kolagaram Property Remove Form at District Level| N/A |Will not be Opened|1|testNegOpenKolagaramPropertyRemoveFormAtDistLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_520|Remove Kolagaram Property at District Level| N/A |Will not be Removed|1|testNegRemoveKolagaramPropertyAtDistLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_530|Open Kolagaram Property Remove Form at Division Level| N/A |Will not be Opened|1|testNegOpenKolagaramPropertyRemoveFormAtDivLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_540|Remove Kolagaram Property at Division Level| N/A |Will not be Removed|1|testNegRemoveKolagaramPropertyAtDivLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_550|Open Kolagaram Property Remove Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenKolagaramPropertyRemoveFormAtMandalLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_560|Remove Kolagaram Property at Mandal Level| N/A |Will not be Removed|1|testNegRemoveKolagaramPropertyAtMandalLevel|
|1.0|View|ut_n_v_GSTS_WEB_KOLAGARAM_PROPERTY_620|View Kolagaram Property at State Level| N/A |Will not be Accessed|1|testNegViewKolagaramPropertyAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_KOLAGARAM_PROPERTY_630|View Kolagaram Property at District Level| N/A |Will not be Accessed|1|testNegViewKolagaramPropertyAtDistLevel|
|1.0|View|ut_n_v_GSTS_WEB_KOLAGARAM_PROPERTY_640|View Kolagaram Property at Division Level| N/A |Will not be Accessed|1|testNegViewKolagaramPropertyAtDivLevel|
|1.0|View|ut_n_v_GSTS_WEB_KOLAGARAM_PROPERTY_650|View Kolagaram Property at Mandal Level| N/A |Will not be Accessed|1|testNegViewKolagaramPropertyAtMandalLevel|
|1.0|List|ut_n_l_GSTS_WEB_KOLAGARAM_PROPERTY_690|Get Kolagaram Property List at State Level| N/A |Will not be Accessed|1|testNegKolagaramPropertyListAtStateLevel|
|1.0|List|ut_n_l_GSTS_WEB_KOLAGARAM_PROPERTY_700|Get Kolagaram Property List at District Level| N/A |Will not be Accessed|1|testNegKolagaramPropertyListAtDistLevel|
|1.0|List|ut_n_l_GSTS_WEB_KOLAGARAM_PROPERTY_710|Get Kolagaram Property List at Division Level| N/A |Will not be Accessed|1|testNegKolagaramPropertyListAtDivLevel|
|1.0|List|ut_n_l_GSTS_WEB_KOLAGARAM_PROPERTY_720|Get Kolagaram Property List at Mandal Level| N/A |Will not be Accessed|1|testNegKolagaramPropertyListAtMandalLevel|
|1.0|Search|ut_n_s_GSTS_WEB_KOLAGARAM_PROPERTY_770|Search Kolagaram Property  at State Level| N/A |Will not be Accessed|1|testNegSearchKolagaramPropertyAtStateLevel|
|1.0|Search|ut_n_s_GSTS_WEB_KOLAGARAM_PROPERTY_780|Search Kolagaram Property  at District Level| N/A |Will not be Accessed|1|testNegSearchKolagaramPropertyAtDistLevel|
|1.0|Search|ut_n_s_GSTS_WEB_KOLAGARAM_PROPERTY_790|Search Kolagaram Property  at Division Level| N/A |Will not be Accessed|1|testNegSearchKolagaramPropertyAtDivLevel|
|1.0|Pdf|ut_n_p_GSTS_WEB_KOLAGARAM_PROPERTY_970|Export Kolagaram Property Pdf at State Level| N/A |Will not be exported|1|testNegExportKolagaramPropertyPdfAtStateLevel|
|1.0|List Pdf|ut_n_p_GSTS_WEB_KOLAGARAM_PROPERTY_980|Export Kolagaram Property List Pdf at State Level| N/A |Will not be exported|1|testNegExportKolagaramPropertyListPdfAtStateLevel|
|1.0|Xlx|ut_n_p_GSTS_WEB_KOLAGARAM_PROPERTY_990|Export Kolagaram Property Xlx at State Level| N/A |Will not be exported|1|testNegExportKolagaramPropertyXlxAtStateLevel|
|1.0|List Xlx|ut_n_p_GSTS_WEB_KOLAGARAM_PROPERTY_1000|Export Kolagaram Property List Xlx at State Level| N/A |Will not be exported|1|testNegExportKolagaramPropertyListXlxAtStateLevel|
|1.0|Download|ut_n_p_GSTS_WEB_KOLAGARAM_PROPERTY_1010|Download Kolagaram Property Attachment at State Level| N/A |Will not be downloaded|1|testNegDownloadKolagaramPropertyAttachmentAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_KOLAGARAM_PROPERTY_1070|Panchayat1112 user trying to access Panchayat1111 Kolagaram Property which does not belongs to his context| N/A |Will not be accessed|1|testNegPanchayat1112UserAccessingPanchayat1111KolagaramProperty|
|1.0|Remove|ut_n_r_GSTS_WEB_KOLAGARAM_PROPERTY_1080|Panchayat1112 user trying to remove Panchayat1111 Kolagaram Property which does not belongs to his context| N/A |Will not be removed|1|testNegPanchayat1112UserRemovingPanchayat1111KolagaramProperty|
|1.0|Update|ut_n_u_GSTS_WEB_KOLAGARAM_PROPERTY_1090|Panchayat1112 user trying to update Panchayat1111 Kolagaram Property which does not belongs to his context| N/A |Will not be updated|1|testNegPanchayat1112UserUpdatingPanchayat1111KolagaramProperty|

## Security compliance check
1. Only user having the user role with permission **ROLE_KOLAGARAM_PROPERTY_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_KOLAGARAM_PROPERTY_UPDATE** should update this functionality 
1. Only user having the user role with permission **ROLE_KOLAGARAM_PROPERTY_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_KOLAGARAM_PROPERTY_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Kolagaram Property should be provided in the User Manual.

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




 
