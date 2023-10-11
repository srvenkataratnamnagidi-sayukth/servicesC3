---
title: Advertisement Property
tags : ["Composing"]
---

## Introduction
Advertisement Property is one of the basic features of the software product which contains the data of all the advertisement properties in the Telangana state. By using this advertisement property feature we have to store every advertisement property data and know about every advertisement property in the state. Every advertisement property should be stored under the respective panchayat only.

## Business Assumptions
1. Advertisement Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the advertisement property.
1. Owner Aadhaar number is required to create the advertisement property.

## Requirements
### Functional Requirements
1. Advertisement Property feature only accessible at the panchayat level.
1. While creating advertisement property, the owner's aadhaar number will bind to it.
1. Only one advertisement property is allowed with the same name.

### Non-functional Requirements
1. To create the advertisement Property, an organization survey status type should be started.
1. Multiple users can create advertisement property in the same panchayat.
1. One citizen can have multiple advertisement properties in the same panchayat or different panchayats.

### Problem Statement
Advertisement Property feature is required to store all the advertisement property details in the panchayat level.

### Design 
1. Each Advertisement property has an owner's Aadhaar number, Name, Latitude, Longitude, Advertisement Category, Advertisement Asset,Board Size,AdvInstallmentCount, and BusinessSanctionId.
1. We can Create, Update, View, and remove the advertisement property.
1. Only one advertisement property is allowed with the same name.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Citizen|||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_adv_property_list|To view all the advertisement properties|
|uc_adv_property_search|To search the advertisement property|
|uc_adv_property_create|To create the advertisement property|
|uc_adv_property_update|To update the advertisement property|
|uc_adv_property_remove|To remove the advertisement property|
|uc_adv_property_view|To view the advertisement property|
|uc_adv_property_export|To export the advertisement property in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9/:#, _\.\-, @, &, Space, minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|NO|YES|YES|YES|YES||
|location|YES|NA|a-zA-Z0-9/:#, _\.\-, (, ), @, &, Space, minlen=3, maxlen=64|@Column(name = "location", length = 64, nullable = false)|location varchar(64) NOT NULL|YES|NO|YES|YES|YES|YES||
|geoLat|YES|NA|0-9.|@Column(name = "geo_lat", length = 24, nullable = false)|geo_lat varchar(24) NOT NULL|YES|NO|YES|YES|NO|NO||
|geoLng|YES|NA|0-9.|@Column(name = "geo_lng", length = 24, nullable = false)|geo_lng varchar(24) NOT NULL|YES|NO|YES|YES|NO|NO||
|advCategory|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "adv_category", length = 16, nullable = true)|adv_category varchar(16) DEFAULT NULL|YES|YES|YES|YES|YES|YES||
|advAsset|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "adv_asset", length = 16, nullable = true)|adv_asset varchar(16) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|boardSize|YES|NA|0-9|@Column(name = "board_size", nullable = true)|board_size bigint(20) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|advInstallmentCount|YES|NA|dropdown values|@Column(name = "adv_installment_count", nullable = true)|adv_installment_count bigint(20) DEFAULT NULL|YES|NO|YES|YES|NO|NO||
|businessSanctionId|YES|NA|a-zA-Z0-9/:#, _\.\-, Space, @, &|@Column(name = "business_sanction_id", length = 32, nullable = true)|business_sanction_id varchar(32) DEFAULT NULL|YES|NO|YES|YES|NO|NO||
|frontPhoto|YES|NA|Attachment|@Column(name = "front_photo", length = 36, nullable = false)|front_photo varchar(36) NOT NULL|YES|NO|NO|YES|NO|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Adv Category

{{<mermaid align="left">}}
classDiagram
    class Name{
      GROUND_BASED
	  MOVING
	  LIGHTING
	  NONE
    }
{{< /mermaid >}}

##### Adv Asset

{{<mermaid align="left">}}
classDiagram
    class Name{
      PUBLIC
	  PRIVATE
	  NONE
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|ADV_PROPERTY_CREATE|Create|
|ADV_PROPERTY_UPDATE|Update|
|ADV_PROPERTY_REMOVE|Remove|
|ADV_PROPERTY_VIEW|View|
|ADV_PROPERTY_VIEW|List|
|ADV_PROPERTY_VIEW|Export|

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
|AC_ROLE_ADV_PROPERTY_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_ADV_PROPERTY_UPDATE|Only user having the user role with this permission should update this functionality|
|AC_ROLE_ADV_PROPERTY_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_ADV_PROPERTY_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_ADV_PROPERTY_VIEW|Only user having the user role with this permission should export the advertisement property in 2 formats Excel, PDF|

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
	AdvertisementPropertyMenu((Advertisement Property Menu))
	ListPage{Advertisement Property List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->AdvertisementPropertyMenu
    subgraph Menu
    AdvertisementPropertyMenu
	end
	subgraph List
	AdvertisementPropertyMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	AdvertisementPropertyMenu-->ErrorPage
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
1. Only a user with the ADV_PROPERTY_VIEW permission will be allowed to perform the below operations.

{{<mermaid align="center">}}
sequenceDiagram
    participant AdvertisementPropertyListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, GET /app/ctx/AdvProperty/list ListPage
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        AdvertisementPropertyListPage->>+cloud: S:  GET /app/ctx/AdvProperty/list ListPage
        cloud-->>-AdvertisementPropertyListPage: RES: List Page
    end
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, GET /app/AdvProperty/create/form CreateFormPage
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        AdvertisementPropertyListPage->>+cloud: S : GET /app/AdvProperty/create/form CreateFormPage
        cloud-->>-AdvertisementPropertyListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, POST /app/AdvProperty/create Create
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        AdvertisementPropertyListPage->>+cloud: S : POST /app/AdvProperty/create Create
        cloud-->>-AdvertisementPropertyListPage: RES: An Advertisement Property Successfully Created
    end
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, GET /app/AdvProperty/update/form UpdateFormPage
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        alt
		note right of Net:  Advertisement Property Cache Object Found
        AdvertisementPropertyListPage->>+Cache: S : GET /app/AdvProperty/update/form UpdateFormPage
        Cache-->>-AdvertisementPropertyListPage: RES: Update Form Loaded
        else
		note right of Net:  Advertisement Property Cache Object Not Found
        Cache->>+cloud: GET /app/AdvProperty/update/form UpdateFormPage
        cloud-->>-AdvertisementPropertyListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, POST /app/AdvProperty/update update
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        AdvertisementPropertyListPage->>+cloud: S : POST /app/AdvProperty/update Update
        cloud-->>-AdvertisementPropertyListPage: RES: An Advertisement Property Successfully Updated
    end
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, GET /app/AdvProperty/remove/form RemoveFormPage
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        alt
		note right of Net:  Advertisement Property Cache Object Found
        AdvertisementPropertyListPage->>+Cache: S : GET /app/AdvProperty/remove/form RemoveFormPage
        Cache-->>-AdvertisementPropertyListPage: RES : Remove Form Loaded
        else
		note right of Net:  Advertisement Property Cache Object Not Found
        Cache->>+cloud: S : GET /app/AdvProperty/remove/form RemoveFormPage
        cloud-->>-AdvertisementPropertyListPage: RES : Remove Form Loaded
        end
    end
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, POST /app/AdvProperty/remove Remove
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        AdvertisementPropertyListPage->>+cloud: S : POST /app/AdvProperty/remove Remove
        cloud-->>-AdvertisementPropertyListPage: RES: An Advertisement Property Successfully Removed
    end
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, GET /app/AdvProperty/view ViewPage
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        alt
		note right of Net:  Advertisement Property Cache Object Found
        AdvertisementPropertyListPage->>+Cache: S : GET /app/AdvProperty/view ViewPage
        Cache-->>-AdvertisementPropertyListPage: RES: advProperty View
        else
		note right of Net:  Advertisement Property Cache Object Not Found
        Cache->>+cloud: GET /app/AdvProperty/view ViewPage
        cloud-->>-AdvertisementPropertyListPage: RES: advProperty View
        end
    end
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, GET /app/AdvProperty/exportPdf ExportPdf
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        alt
		note right of Net:  Advertisement Property Cache Object Found
        AdvertisementPropertyListPage->>+Cache: S : GET /app/AdvProperty/exportPdf ExportPdf
        Cache-->>-AdvertisementPropertyListPage: RES: advProperty Pdf
        else
		note right of Net:  Advertisement Property Cache Object Not Found
        Cache->>+cloud: GET /app/AdvProperty/exportPdf ExportPdf
        cloud-->>-AdvertisementPropertyListPage: RES: advProperty Pdf
        end
    end
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, GET /app/AdvProperty/exportListPdf ExportListPdf
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        AdvertisementPropertyListPage->>+cloud: S : GET /app/AdvProperty/exportListPdf ExportListPdf
        cloud-->>-AdvertisementPropertyListPage: RES: advProperty List Pdf
    end
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, GET /app/AdvProperty/exportXlx ExportXlx
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        alt
		note right of Net:  Advertisement Property Cache Object Found
        AdvertisementPropertyListPage->>+Cache: S : GET /app/AdvProperty/exportXlx ExportXlx
        Cache-->>-AdvertisementPropertyListPage: RES: Advertisement Property Xlx
        else
		note right of Net:  Advertisement Property Cache Object Not Found
        Cache->>+cloud: GET /app/AdvProperty/exportXlx ExportXlx
        cloud-->>-AdvertisementPropertyListPage: RES: advProperty Xlx
        end
    end
    rect rgb(244,244,244)
        AdvertisementPropertyListPage->>+Net: Check Internet, GET /app/AdvProperty/exportListXlx ExportListXlx
        Net--x-AdvertisementPropertyListPage: F : Connection Error
        AdvertisementPropertyListPage->>+cloud: S : GET /app/AdvProperty/exportListXlx ExportListXlx
        cloud-->>-AdvertisementPropertyListPage: RES: advProperty List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|-----|
|1.0| Create Form |ut_p_c_GSTS_WEB_ADV_PROPERTY_120 ut_n_c_GSTS_WEB_ADV_PROPERTY_130 |**Positive Test Cases:** 1.Open Advertisement Property Create Form At panchayat level **Negative Test Cases:** 1.Open Advertisement Property Create Form Without Db connection|-|1|1|2|testPosOpenAdvertisementPropertyCreateFormWithAuthorisedUser,  testNegOpenAdvertisementPropertyCreateFormWithoutDBConnection|
|1.0| Create |ut_p_c_GSTS_WEB_ADV_PROPERTY_150  ut_n_c_GSTS_WEB_ADV_PROPERTY_160 ut_n_c_GSTS_WEB_ADV_PROPERTY_140 |**Positive Test Cases:** Creating Advertisement Property  with valid inputs with Panchayat Level Authorised User**Negative Test Cases:** Creating Advertisement Property  with invalid inputs 2.Open Advertisement Property Create Without Db connection|**citizenId:** 1.Valid Characters 2.length must be 12 3.null **name:** 1.Valid Characters 2.length>=3 and length<=64 3.null 4.unique **location:** 1.Valid Characters 2.length>=3 and length<=64 3.null **geoLat:** **geoLng:** **advCategory:** Enums **advAsset:** Enums **advInstallmentCount:** dropdown values 1L,2L,3L,4L,5L **businessSanctionId:** 1.Valid Characters 2.length>=3 and length<=64 3.null 4.unique **boardSize:** 1.null 2.length>=1 and length<=10|5|6|11|testPosAuthorisedPanchayatLevelUserCreateAdvertisementPropertyWithValidInputs,  testNegAuthorisedPanchayatLevelUserCreateAdvertisementPropertyWithInValidInputs,  testNegCreateAdvertisementPropertyWithoutDBconnection|
|1.0| Create |ut_n_c_GSTS_WEB_ADV_PROPERTY_165 |**Positive Test Cases:** **Negative Test Cases:** 1.Create Advertisement Property without Image Attachment|-|0|1|1|testNegCreateAdvertisementPropertyWithoutImageAttachment|
|1.0| Update Form |ut_p_u_GSTS_WEB_ADV_PROPERTY_270   ut_n_u_GSTS_WEB_ADV_PROPERTY_280   ut_n_u_GSTS_WEB_ADV_PROPERTY_290|**Positive Test Cases:** Open Advertisement Property update form with valid Id with Authorised Panchayat level user    **Negative Test Cases:**  1.Open Advertisement Property update Form Without DB Connection 2. Open Advertisement Property update Form with Invalid id|Id|1|2|3|testPosAuthorisedPanLevelUserOpenAdvertisementPropertyUpdateFormWithValidId,  testNegAuthorisedPanLevelUserOpenAdvertisementPropertyUpdateFormWithoutDBConnection,  testNegAuthorisedPanLevelUserOpenAdvertisementPropertyUdpateFormWithInValidId|
|1.0| Update |ut_p_u_GSTS_WEB_ADV_PROPERTY_300  ut_n_u_GSTS_WEB_ADV_PROPERTY_310 ut_n_u_GSTS_WEB_ADV_PROPERTY_320 ut_n_u_GSTS_WEB_ADV_PROPERTY_330 ut_n_u_GSTS_WEB_ADV_PROPERTY_470 |**Positive Test Cases:** Updating Advertisement Property  with valid inputs with Panchayat Level Authorised User **Negative Test Cases:** 1. Updating Advertisement Property  with invalid inputs 2. Update Advertisement Property without db connection 3.Update Advertisement Property with Invalid Id 4.Update removed Advertisement Property|**updateComment:** 1.valid characters 2. length>=6 and length<=255 3.null|1|4|5|testPosPanLevelAuthorisedUserUpdateAdvertisementPropertyWithValidInputs,  testNegPanLevelAuthorisedUserUpdateAdvertisementPropertyWithInValidInputs,  testNegUpdateAdvertisementPropertyWithoutDbConnection,  testNegPanLevelAuthorisedUserUpdateAdvertisementPropertyWithInvalidId,  testNegAuthorisedUserUpdateAlreadyRemovedAdvertisementProperty|
|1.0| Remove Form |ut_p_r_GSTS_WEB_ADV_PROPERTY_380   ut_n_r_GSTS_WEB_ADV_PROPERTY_390   ut_n_r_GSTS_WEB_ADV_PROPERTY_400  ut_n_r_GSTS_WEB_ADV_PROPERTY_460|**Positive Test Cases:** Open Advertisement Property remove form with valid Id with Authorised Panchayat level user    **Negative Test Cases:**  1.Open Advertisement Property remove Form Without DB Connection 2. Open Advertisement Property remove Form with Invalid id   3.Open Advertisement Property remove form with Already removed Advertisement Property Id with Authorised user|Id|1|3|4|testPosAuthorisedPanLevelUserOpenPanLevelAdvertisementPropertyRemoveFormWithValidId,  testNegAuthorisedPanLevelUserOpenAdvertisementPropertyRemoveFormWithoutDBConnection,  testNegAuthorisedPanLevelUserOpenAdvertisementPropertyRemoveFormWithInValidId,  testNegAuthorisedPanUserOpenAdvertisementPropertyRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_ADV_PROPERTY_410  ut_n_r_GSTS_WEB_ADV_PROPERTY_420 ut_n_r_GSTS_WEB_ADV_PROPERTY_440  ut_n_r_GSTS_WEB_ADV_PROPERTY_450  ut_n_r_GSTS_WEB_ADV_PROPERTY_480 |**Positive Test Cases:** Remove Advertisement Property with Valid Remove Comment with Panchayat Level Authorised User **Negative Test Cases:** 1. Removing Advertisement Property with invalid remove comment 2.Remove Advertisement Property without db connection 3.Remove already removed Advertisement Property  4. Remove Advertisement Property with invalid Id| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|testPosPanLevelAuthorisedUserRemoveAdvertisementPropertyWithValidRemoveCommentAndValidId,  testNegPanLevelAuthorisedUserRemoveAdvertisementPropertyWithInValidRemoveCommentAndValidId,  testNegRemoveAdvertisementPropertyWithoutDbConnection,  testNegAuthorisedUserRemoveAlreadyRemovedAdvertisementProperty,  testNegPanLevelAuthorisedUserRemoveAdvertisementPropertyWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_ADV_PROPERTY_590  ut_n_v_GSTS_WEB_ADV_PROPERTY_600 ut_n_v_GSTS_WEB_ADV_PROPERTY_610 |**Positive Test Cases:** View Advertisement Property  with Valid Id  with Authorised User **Negative Test Cases:** 1.View Advertisement Property without db connection 2.View Advertisement Property  with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewAdvertisementPropertyWithValidId,  testNegAuthorisedUserViewAdvertisementPropertyWithoutDbConnection,  testNegAuthorisedUserViewAdvertisementPropertywithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_ADV_PROPERTY_740  ut_n_s_GSTS_WEB_ADV_PROPERTY_750 ut_n_s_GSTS_WEB_ADV_PROPERTY_760 |**Positive Test Cases:** Search Advertisement Property with valid inputs **Negative Test Cases:** 1.Search Advertisement Property without db connection 2.Search Advertisement Property  with invalid inputs|**1.name 2.advCategory 3.citizenId 4.location**|1|2|3|testPosAuthorisedUserSearchAdvertisementPropertyWithValidInputs,  testNegAuthorisedUserSearchAdvertisementPropertyWithoutDBconnection,  testNegAuthorisedUserSearchAdvertisementPropertyWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_ADV_PROPERTY_670 ut_n_l_GSTS_WEB_ADV_PROPERTY_680|**Positive Test Cases:** Get Advertisement Property List with Authorised User **Negative Test Cases:** Get Advertisement Property List without db connection|Validating with unique field|1|1|2|testPosAuthorisedUserGetAdvertisementPropertyList,  testNegAuthorisedUserAdvertisementPropertyListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_ADV_PROPERTY_810   ut_n_ep_GSTS_WEB_ADV_PROPERTY_820   ut_n_ep_GSTS_WEB_ADV_PROPERTY_830 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportAdvertisementPropertyPdfWithValidId,  testNegAuthorisedUserExportAdvertisementPropertyPdfwithoutDbconnection,  testNegAuthorisedUserExportAdvertisementPropertyPdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_ADV_PROPERTY_840   ut_n_elp_GSTS_WEB_ADV_PROPERTY_850   ut_n_elp_GSTS_WEB_ADV_PROPERTY_860 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportAdvertisementPropertyListPdfWithValidId,  testNegAuthorisedUserExportAdvertisementPropertyListPdfwithoutDbconnection,  testNegAuthorisedUserExportAdvertisementPropertyListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_ADV_PROPERTY_870   ut_n_ex_GSTS_WEB_ADV_PROPERTY_880   ut_n_ex_GSTS_WEB_ADV_PROPERTY_890 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportAdvertisementPropertyXlxValidId,  testNegAuthorisedUserExportAdvertisementPropertyXlxwithoutDbconnection,  testNegAuthorisedUserExportAdvertisementPropertyXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_ADV_PROPERTY_900   ut_n_elx_GSTS_WEB_ADV_PROPERTY_910   ut_n_elx_GSTS_WEB_ADV_PROPERTY_920 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportAdvertisementPropertyListXlxValidId,  testNegAuthorisedUserExportAdvertisementPropertyListXlxwithoutDbconnection,  testNegAuthorisedUserExportAdvertisementPropertyListXlxInValidId|
|1.0| Download|ut_p_elx_GSTS_WEB_ADV_PROPERTY_930   ut_n_elx_GSTS_WEB_ADV_PROPERTY_940   ut_n_elx_GSTS_WEB_ADV_PROPERTY_950 ut_n_elx_GSTS_WEB_ADV_PROPERTY_960 |**Positive Test Cases:** Download Advertisement Property attachment with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Advertisement Property attachment with Invalid Id 3.Download Advertisement Property Attachment with valid Id and Invalid Document type|Id |1|3|4|testPosAuthorisedUserDownloadAdvertisementPropertyAttachmentValidId,  testNegAuthorisedUserDownloadAdvertisementPropertyAttachmentwithoutDbConnection,  testNegAuthorisedUserDownloadAdvertisementPropertyAttachmentInValidId, testNegAuthorisedUserDownloadAdvertisementPropertyAttachmentWithValidIdAndInvalidDocType|


#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|-----|
|1.0| Create Form|ut_n_c_GSTS_WEB_ADV_PROPERTY_260|Unauthorised User opening Advertisement Property create form||0|1|1|testNegUnAuthorisedUserOpenAdvertisementPropertyCreateForm|
|1.0| Create |ut_n_c_GSTS_WEB_ADV_PROPERTY_250 |Unauthorised User does not have permission to create|**citizenId:** 1.Valid Characters 2.length must be 12 3.null **name:** 1.Valid Characters 2.length>=3 and length<=64 3.null 4.unique **location:** 1.Valid Characters 2.length>=3 and length<=64 3.null **geoLat:** **geoLng:** **advCategory:** Enums **advAsset:** Enums **advInstallmentCount:** dropdown values 1L,2L,3L,4L,5L **businessSanctionId:** 1.Valid Characters 2.length>=3 and length<=64 3.null 4.unique **boardSize:** 1.null 2.length>=1 and length<=10|0|1|1|testNegUnAuthorisedUserCreateAdvertisementProperty|
|1.0| Update Form|ut_n_u_GSTS_WEB_ADV_PROPERTY_370|Unauthorised User opening Advertisement Property update form||0|1|1|testNegUnAuthorisedPanLevelUserOpenAdvertisementPropertyUpdateForm|
|1.0| Update |ut_n_u_GSTS_WEB_ADV_PROPERTY_360|Unauthorised User does not have permission to update|**updateComment:** 1.valid characters 2.length >=6 and length<=255 3.null|0|1|1|testNegUnAuthorisedUserUpdateAdvertisementProperty|
|1.0| Remove Form|ut_n_r_GSTS_WEB_ADV_PROPERTY_570|Unauthorised User opening Advertisement Property remove form||0|1|1|testNegUnAuthorisedPanLevelUserOpenAdvertisementPropertyRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_ADV_PROPERTY_580|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserRemoveAdvertisementProperty|
|1.0| View |ut_n_v_GSTS_WEB_ADV_PROPERTY_660|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewAdvertisementProperty|
|1.0| Search |ut_n_s_GSTS_WEB_ADV_PROPERTY_800|Unauthorised User does not have permission to search|**1.name 2.advCategory 3.citizenId 4.location**|0|1|1|testNegUnAuthorisedUserSearchAdvertisementProperty|
|1.0| List |ut_n_l_GSTS_WEB_ADV_PROPERTY_730|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserAdvertisementPropertyList|
|1.0| List |ut_n_l_GSTS_WEB_ADV_PROPERTY_730|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserAdvertisementPropertyList|
|1.0| PDF |ut_n_ep_GSTS_WEB_ADV_PROPERTY_1020 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportAdvertisementPropertyPdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_ADV_PROPERTY_1030 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportAdvertisementPropertyListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_ADV_PROPERTY_1040 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportAdvertisementPropertyXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_ADV_PROPERTY_1050 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportAdvertisementPropertyListXlxWithValidId|
|1.0| Download |ut_n_elx_GSTS_WEB_ADV_PROPERTY_1060 |Download Advertisement Property attachment with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserDownloadAdvertisementPropertyAttachmentWithValidId|


#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|------------|
|1.0|Create|ut_n_c_GSTS_WEB_ADV_PROPERTY_170|Create Advertisement Property at State Level| N/A |Will not be Created|1|testNegCreateAdvertisementPropertyAtStateLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_ADV_PROPERTY_180|Open Advertisement Property Create Form at State Level| N/A |Will not be Opened|1|testNegOpenAdvertisementPropertyCreateFormAtStateLevel|
|1.0|Create|ut_n_c_GSTS_WEB_ADV_PROPERTY_190|Create Advertisement Property at District Level| N/A |Will not be Created|1|testNegCreateAdvertisementPropertyAtDistLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_ADV_PROPERTY_200|Open Advertisement Property Create Form at District Level| N/A |Will not be Opened|1|testNegOpenAdvertisementPropertyCreateFormAtDistLevel|
|1.0|Create|ut_n_c_GSTS_WEB_ADV_PROPERTY_210|Create Advertisement Property at Division Level| N/A |Will not be Created|1|testNegCreateAdvertisementPropertyAtDivLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_ADV_PROPERTY_220|Open Advertisement Property Create Form at Division Level| N/A |Will not be Opened|1|testNegOpenAdvertisementPropertyCreateFormAtDivLevel|
|1.0|Create|ut_n_c_GSTS_WEB_ADV_PROPERTY_230|Create Advertisement Property at Mandal Level| N/A |Will not be Created|1|testNegCreateAdvertisementPropertyAtMandalLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_ADV_PROPERTY_240|Open Advertisement Property Create Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenAdvertisementPropertyCreateFormAtMandalLevel|
|1.0|Update Form|ut_n_u_GSTS_WEB_ADV_PROPERTY_340|Open Advertisement Property update Form at State Level| N/A |Will not be Opened|1|testNegOpenAdvertisementPropertyUpdateFormAtStateLevel|
|1.0|Update|ut_n_u_GSTS_WEB_ADV_PROPERTY_350|Update Advertisement Property at State Level| N/A |Will not be updated|1|testNegUpdateAdvertisementPropertyAtStateLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_ADV_PROPERTY_490|Open Advertisement Property Remove Form at State Level| N/A |Will not be Opened|1|testNegOpenAdvertisementPropertyRemoveFormAtStateLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_ADV_PROPERTY_500|Remove Advertisement Property at State Level| N/A |Will not be Removed|1|testNegRemoveAdvertisementPropertyAtStateLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_ADV_PROPERTY_510|Open Advertisement Property Remove Form at District Level| N/A |Will not be Opened|1|testNegOpenAdvertisementPropertyRemoveFormAtDistLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_ADV_PROPERTY_520|Remove Advertisement Property at District Level| N/A |Will not be Removed|1|testNegRemoveAdvertisementPropertyAtDistLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_ADV_PROPERTY_530|Open Advertisement Property Remove Form at Division Level| N/A |Will not be Opened|1|testNegOpenAdvertisementPropertyRemoveFormAtDivLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_ADV_PROPERTY_540|Remove Advertisement Property at Division Level| N/A |Will not be Removed|1|testNegRemoveAdvertisementPropertyAtDivLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_ADV_PROPERTY_550|Open Advertisement Property Remove Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenAdvertisementPropertyRemoveFormAtMandalLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_ADV_PROPERTY_560|Remove Advertisement Property at Mandal Level| N/A |Will not be Removed|1|testNegRemoveAdvertisementPropertyAtMandalLevel|
|1.0|View|ut_n_v_GSTS_WEB_ADV_PROPERTY_620|View Advertisement Property at State Level| N/A |Will not be Accessed|1|testNegViewAdvertisementPropertyAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_ADV_PROPERTY_630|View Advertisement Property at District Level| N/A |Will not be Accessed|1|testNegViewAdvertisementPropertyAtDistLevel|
|1.0|View|ut_n_v_GSTS_WEB_ADV_PROPERTY_640|View Advertisement Property at Division Level| N/A |Will not be Accessed|1|testNegViewAdvertisementPropertyAtDivLevel|
|1.0|View|ut_n_v_GSTS_WEB_ADV_PROPERTY_650|View Advertisement Property at Mandal Level| N/A |Will not be Accessed|1|testNegViewAdvertisementPropertyAtMandalLevel|
|1.0|List|ut_n_l_GSTS_WEB_ADV_PROPERTY_690|Get Advertisement Property List at State Level| N/A |Will not be Accessed|1|testNegAdvertisementPropertyListAtStateLevel|
|1.0|List|ut_n_l_GSTS_WEB_ADV_PROPERTY_700|Get Advertisement Property List at District Level| N/A |Will not be Accessed|1|testNegAdvertisementPropertyListAtDistLevel|
|1.0|List|ut_n_l_GSTS_WEB_ADV_PROPERTY_710|Get Advertisement Property List at Division Level| N/A |Will not be Accessed|1|testNegAdvertisementPropertyListAtDivLevel|
|1.0|List|ut_n_l_GSTS_WEB_ADV_PROPERTY_720|Get Advertisement Property List at Mandal Level| N/A |Will not be Accessed|1|testNegAdvertisementPropertyListAtMandalLevel|
|1.0|Search|ut_n_s_GSTS_WEB_ADV_PROPERTY_770|Search Advertisement Property  at State Level| N/A |Will not be Accessed|1|testNegSearchAdvertisementPropertyAtStateLevel|
|1.0|Search|ut_n_s_GSTS_WEB_ADV_PROPERTY_780|Search Advertisement Property  at District Level| N/A |Will not be Accessed|1|testNegSearchAdvertisementPropertyAtDistLevel|
|1.0|Search|ut_n_s_GSTS_WEB_ADV_PROPERTY_790|Search Advertisement Property  at Division Level| N/A |Will not be Accessed|1|testNegSearchAdvertisementPropertyAtDivLevel|
|1.0|Pdf|ut_n_p_GSTS_WEB_ADV_PROPERTY_970|Export Advertisement Property Pdf at State Level| N/A |Will not be exported|1|testNegExportAdvertisementPropertyPdfAtStateLevel|
|1.0|List Pdf|ut_n_p_GSTS_WEB_ADV_PROPERTY_980|Export Advertisement Property List Pdf at State Level| N/A |Will not be exported|1|testNegExportAdvertisementPropertyListPdfAtStateLevel|
|1.0|Xlx|ut_n_p_GSTS_WEB_ADV_PROPERTY_990|Export Advertisement Property Xlx at State Level| N/A |Will not be exported|1|testNegExportAdvertisementPropertyXlxAtStateLevel|
|1.0|List Xlx|ut_n_p_GSTS_WEB_ADV_PROPERTY_1000|Export Advertisement Property List Xlx at State Level| N/A |Will not be exported|1|testNegExportAdvertisementPropertyListXlxAtStateLevel|
|1.0|Download|ut_n_p_GSTS_WEB_ADV_PROPERTY_1010|Download Advertisement Property Attachment at State Level| N/A |Will not be downloaded|1|testNegDownloadAdvertisementPropertyAttachmentAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_ADV_PROPERTY_1070|Panchayat1112 user trying to access Panchayat1111 Advertisement Property which does not belongs to his context| N/A |Will not be accessed|1|testNegPanchayat1112UserAccessingPanchayat1111AdvertisementProperty|
|1.0|Remove|ut_n_r_GSTS_WEB_ADV_PROPERTY_1080|Panchayat1112 user trying to remove Panchayat1111 Advertisement Property which does not belongs to his context| N/A |Will not be removed|1|testNegPanchayat1112UserRemovingPanchayat1111AdvertisementProperty|
|1.0|Update|ut_n_u_GSTS_WEB_ADV_PROPERTY_1090|Panchayat1112 user trying to update Panchayat1111 Advertisement Property which does not belongs to his context| N/A |Will not be updated|1|testNegPanchayat1112UserUpdatingPanchayat1111AdvertisementProperty|

## Security compliance check
1. Only user having the user role with permission **ROLE_ADV_PROPERTY_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_ADV_PROPERTY_UPDATE** should update this functionality 
1. Only user having the user role with permission **ROLE_ADV_PROPERTY_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_ADV_PROPERTY_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Advertisement Property should be provided in the User Manual.

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




 
