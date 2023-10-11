---
title: Assets
tags : ["Composing"]
---

## Introduction
Assets are one of the features of our software product. Assets are the properties or things that belong to a panchayat. Users should have permission to access this feature.

## Business Assumptions
Creating, updating and removing the assets can be done at the run time based on the requirement.

## Requirements
### Functional Requirements
Only panchayat level users should create, update, remove or view the assets.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access assets.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Assets contain information about things or properties that belongs to a panchayat.

### Design 
1. We can Create, Update, View, and remove the assets.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_asset_create|To create the asset|
|uc_asset_update|To update the asset|
|uc_asset_remove|To remove the asset|
|uc_asset_view|To view the asset|
|uc_asset_search|To search the asset|
|uc_asset_export|To export the asset in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|Asset Type|YES|NA|DropDown Values|@Enumerated (EnumType.STRING) @Column(name = "asset_type", length = 256, nullable = false)|asset_type varchar(256) not null|YES|NO|YES|YES|YES|YES||
|Movable Type|YES|NA|DropDown Values|@Column(name = "movable_type", length = 32, nullable = false)|movable_type varchar(32) not null|YES|NO|YES|YES|YES|NO||
|Asset Tag|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - and length 3 to 64|@Column(name = "asset_tag", length = 64, nullable = false)|asset_tag varchar(64) not null|YES|NO|YES|YES|YES|YES||
|Asset Value|YES|NA|Allowed 0-9 only|@Column(name = "asset_value", nullable = false)|asset_value float(9,2) not null|YES|NO|YES|YES|YES|NO||
|Purchase Date|YES|NA|Date|@DateTimeFormat (pattern = "dd-MM-yyyy") @Temporal (TemporalType.TIMESTAMP) @Column(name = "purchase_date", nullable = false)|purchase_date datetime not null|YES|NO|YES|YES|NO|NO||
|Warranty Period|YES|NA|Allowed 0-9 only|@Column(name = "warranty_period", nullable = false)|warranty_period bigint(20) not null|YES|YES|YES|YES|NO|NO||
|Latitude|YES|NA|Allowed a-z = A-Z = 0-9 = space = _ = - and length 8 to 32|@Column(name = "latitude", length = 32, nullable = true)|latitude varchar(32) default null|YES|YES|YES|YES|NO|NO||
|Longitude|YES|NA|Allowed a-z = A-Z = 0-9 = space = _ = - and length 8 to 32|@Column(name = "longitude", length = 32, nullable = true)|longitude varchar(32) default null|YES|YES|YES|YES|NO|NO||
|Manufacturer|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - and length 3 to 32|@Column(name = "manfacturer", length =32, nullable = false)|manfacturer varchar(32) not null|YES|YES|YES|YES|NO|NO||
|Asset Description|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . and length 6 to 256|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) not null|YES|YES|YES|YES|NO|NO||
|Attachement|YES|NA|Allowed PDF, JPG, PNG files only|@Column(name = "file_name", length = 64, nullable = true)|file_name varchar(64) default null|YES|YES|YES|YES|NO|NO||
|Approver Or Verifier|YES|NA|Drop Down List|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "approver_id", nullable = false)|approver_id varchar(36) not null|YES|YES|NO|NO|NO|NO||
|Updated Reason|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . and length 6 to 256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|Removed Reason|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . and length 6 to 256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### Enum Constants

##### Asset Type

{{<mermaid align="left">}}
classDiagram
    class Name{
      NONE
      MIDDLE_SCHOOL
      ANGAAWADI
      PUBLIC_LIBRARY
      FAN
      CHAIR
      WATERTANK
      WATER_TANKER
      AC
      TRACTOR
      AUTO_RICKSHAW
      OTHERS
    }
{{< /mermaid >}}

##### Movable Type

{{<mermaid align="left">}}
classDiagram
    class Name{
      TRUE
      FALSE
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|ASSET_CREATE|Create|
|ASSET_UPDATE|Update|
|ASSET_REMOVE|Remove|
|ASSET_VIEW|View|
|ASSET_VIEW|List|
|ASSET_VIEW|Export|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|ac_asset_create|Only user having the permission to create, should create this functionality|
|ac_asset_update|Only user having the permission to update, should update this functionality|
|ac_asset_remove|Only user having the permission to remove, should remove this functionality|
|ac_asset_view|Only user having the permission to view, should view this functionality|
|ac_asset_view|Only user having the permission to export, should export the user role in 2 formats Excel, PDF|

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
	AssetsMenu((Assets Menu))
	ListPage{Assets List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->AssetsMenu
    subgraph Menu
    AssetsMenu
	end
	subgraph List
	AssetsMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	AssetsMenu-->ErrorPage
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
|SB|Submit or Back|
|VE|View or Export|
|C-U-R-V-E|Create or Update or Remove or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant AssetsListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        AssetsListPage->>+Net: Check Internet, GET /app/ctx/Asset/list ListPage
        Net--x-AssetsListPage: F : Connection Error
        AssetsListPage->>+cloud: S:  GET /app/ctx/Asset/list ListPage
        cloud-->>-AssetsListPage: RES:List Page
    end
    rect rgb(244,244,244)
        AssetsListPage->>+Net: Check Internet, GET /app/Asset/create/form CreateFormPage
        Net--x-AssetsListPage: F : Connection Error
        AssetsListPage->>+cloud: S : GET /app/Asset/create/form CreateFormPage
        cloud-->>-AssetsListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        AssetsListPage->>+Net: Check Internet: POST /app/Asset/create Create
        Net--x-AssetsListPage: F : Connection Error
        AssetsListPage->>+cloud: S : POST /app/Asset/create Create
        cloud-->>-AssetsListPage: RES: An Asset Successfully Created
    end
    rect rgb(244,244,244)
        AssetsListPage->>+Net: Check Internet: POST /app/Asset/update update
        Net--x-AssetsListPage: F : Connection Error
        AssetsListPage->>+cloud: S : POST /app/Asset/update Update
        cloud-->>-AssetsListPage: RES: An Asset Successfully Updated
    end
    rect rgb(244,244,244)
        AssetsListPage->>+Net: Check Internet: GET /app/Asset/remove/form RemoveFormPage
        Net--x-AssetsListPage: F : Connection Error
        AssetsListPage->>+cloud: S : GET /app/Asset/remove/form RemoveFormPage
        cloud-->>-AssetsListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        AssetsListPage->>+Net: Check Internet: POST /app/Asset/remove Remove
        Net--x-AssetsListPage: F : Connection Error
        AssetsListPage->>+cloud: S : POST /app/Asset/remove Remove
        cloud-->>-AssetsListPage: RES: A Asset Successfully Removed
    end
    rect rgb(244,244,244)
        AssetsListPage->>+Net: Check Internet: GET /app/Asset/exportListPdf ExportListPdf
        Net--x-AssetsListPage: F : Connection Error
        AssetsListPage->>+cloud: S : GET /app/Asset/exportListPdf ExportListPdf
        cloud-->>-AssetsListPage: RES: asset List Pdf
    end
    rect rgb(244,244,244)
        AssetsListPage->>+Net: Check Internet: GET /app/Asset/exportListXlx ExportListXlx
        Net--x-AssetsListPage: F : Connection Error
        AssetsListPage->>+cloud: S : GET /app/Asset/exportListXlx ExportListXlx
        cloud-->>-AssetsListPage: RES: asset List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User 

|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create | **Positive Test Case:** ut_p_c_GSTS_WEB_ASSET_100 **Negative Test Case:** ut_n_c_GSTS_WEB_ASSET_101 ut_n_c_GSTS_WEB_ASSET_113|**Positive Test Cases:** Creating Asset with Authorised User **Negative Test Cases:** 1.Creating Asset with Invalid Input 2.Creating Asset with different Panchayat User as approver| **AssetType:** Enum Values **MovableType:** Enum Values **assetTag:** 1.Valid Characters 2.length>3 and length<64 3.null **assetValue:** 1.value>0 2.null **purchaseDate:** 1.null 2.Date before Present Date **warrantyPeriod:** 1.value > 0 2.null **latitude** **longitude**  **manufacturer:** 1.valid characters 2.length > 3 and length < 32 3.null **descr:** 1.Valid characters 2.length >6 and length<256 3.null **approverName**|12|5|17|testAuthorisedUserCreateAsset, testAuthorisedUserCreateAssetNegativeTestCases, testAuthorisedUserCreateAssetWithAnotherPanchayatApprover|
|1.0|Create Form| ut_p_c_GSTS_WEB_ASSET_110 ut_n_c_GSTS_WEB_ASSET_112 |**Positive Test Cases:** Open Asset Create Form with Authorised User **Negative Test Cases:** Open Asset Create Form without DB Connection|N/A|1|1|2|testAuthorisedUserOpenAssetCreateForm, testAuthorisedUserOpenAssetCreateFormWithoutDBConnection|
|1.0|Update|ut_p_u_GSTS_WEB_ASSET_200 ut_n_u_GSTS_WEB_ASSET_201 ut_n_u_GSTS_WEB_ASSET_203 ut_n_u_GSTS_WEB_ASSET_204 ut_n_u_GSTS_WEB_ASSET_209 ut_n_u_GSTS_WEB_ASSET_210 |**Positive Test Cases:** Updating Asset with Authorised User **Negative Test Cases:** 1.Updating Asset with Invalid Inputs 2.Updating Asset without DB Connection 3.Updating Asset with Invalid Id 4.Updating Asset With Invalid attachment 5.Updating Panchayat1111 Asset with panchayat1112 context|**updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|5|6|testUpdateAsset, testAuthorisedUserUpdateAssetNegativeTestCases, testAuthorisedUpdateAssetWithoutDBConnection, testAuthorisedUpdateAssetWithInvalidId, testAuthorisedUserUpdateAssetWithInvalidAttachment, testUpdateAssetWithAnotherPanchayat|
|1.0|Update Form|ut_p_u_GSTS_WEB_ASSET_205 ut_n_u_GSTS_WEB_ASSET_206 ut_n_u_GSTS_WEB_ASSET_208 |**Positive Test Cases:** Open Asset Update Form with Authorised User **Negative Test Cases:** 1.Open Asset Update Form with Invalid Id 2.Open Asset Update Form without DB Connection|1.Valid Id|1|2|3|testAuthorisedUserOpenAssetUpdateFormWithValidId, testAuthorisedUserOpenAssetUpdateFormWithInvalidId, testAuthorisedUserOpenAssetUpdateFormWithoutDBConnection|
|1.0| Remove |ut_p_r_GSTS_WEB_ASSET_302 ut_n_r_GSTS_WEB_ASSET_300 ut_n_r_GSTS_WEB_ASSET_301 ut_n_r_GSTS_WEB_ASSET_303 ut_n_r_GSTS_WEB_ASSET_304 |**Positive Test Cases:** Removing Asset with Authorised User **Negative Test Cases:** 1.Remove Asset without DB Connection 2.Remove Asset with Invalid Id 3.Remove Asset with Invalid Input| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|4|5|testAuthorisedUserRemoveAsset, testAuthorisedUserRemoveAssetWithoutDBConnection, testAuthorisedUserRemoveAssetWithInvalidId, testAuthorisedUserRemoveAssetNegativeTestCases, testAuthorisedUserRemoveAssetWithInvalidIdAndComment|
|1.0|Remove Form|ut_p_r_GSTS_WEB_ASSET_306 ut_n_r_GSTS_WEB_ASSET_307 ut_n_r_GSTS_WEB_ASSET_309 |**Positive Test Cases:** Open Asset Remove Form with Authorised User **Negative Test Cases:** 1.Open Asset Remove Form with Invalid Id 2.Open Asset Remove Form without DB Connection|1.Valid Id|1|2|3|testAuthorisedUserOpenAssetRemoveForm, testAuthorisedUserOpenAssetRemoveFormWithInvalidId, testAuthorisedUserOpenAssetRemoveFormWithoutDBConnection|
|1.0| View |ut_p_v_GSTS_WEB_ASSET_400 ut_n_v_GSTS_WEB_ASSET_401 |**Positive Test Cases:** View Asset with Valid Id with Authorised User**Negative Test Cases:** View Asset with Invalid ID  with Authorised User|1.Valid Id 2.Invalid Id|1|1|2|testViewAssetWithValidId, testViewAssetWithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_ASSET_500 ut_n_s_GSTS_WEB_ASSET_501 ut_n_s_GSTS_WEB_ASSET_503 ut_n_s_GSTS_WEB_ASSET_504|**Positive Test Cases:** Search Asset with Authorised User **Negative Test Cases:** 1.Search Asset with Invalid Inputs 2.Search Asset without DB Connection 3.Search Asset with Invalid dates with Authorised User|**AssetType:** Enum Values **assetTag:** 1.valid characters 2.length>3 and length<64 3.null|12|5|17|testAuthorisedUserSearchAsset, testAuthorisedUserSearchAssetNegativeTestCase, testAuthorisedUserSearchAssetWithoutDBConnection, testAuthorisedUserSearchAssetNegativeCase|
|1.0| List |ut_p_l_GSTS_WEB_ASSET_600 ut_n_l_GSTS_WEB_ASSET_601 |**Positive Test Cases:** Check the object list with valid data  with Authorised User **Negative Test Cases:** 1.Check the object list with Invalid data with Authorised User|Validating with unique field|1|1|2|testAuthorisedUserListAsset, testAuthorisedUserListAssetNegativeTestCase|
|1.0| PDF |ut_p_ep_GSTS_WEB_ASSET_800 ut_n_ep_GSTS_WEB_ASSET_805 ut_n_ep_GSTS_WEB_ASSET_812 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|2|3|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId, testAuthorisedUserExportPdfWithoutDBConnection|
|1.0| List PDF |ut_p_elp_GSTS_WEB_ASSET_801 ut_n_elp_GSTS_WEB_ASSET_806 ut_n_elp_GSTS_WEB_ASSET_813 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_ASSET_802 ut_n_ex_GSTS_WEB_ASSET_807 ut_n_ex_GSTS_WEB_ASSET_814 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId, testAuthorisedUserExportXlxWithoutDBConnection|
|1.0| List XLX |ut_p_elx_GSTS_WEB_ASSET_803 ut_n_elx_GSTS_WEB_ASSET_808 ut_n_elx_GSTS_WEB_ASSET_815 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|
|1.0| Download|ut_p_d_GSTS_WEB_ASSET_900 ut_n_d_GSTS_WEB_ASSET_901 ut_n_d_GSTS_WEB_ASSET_903 ut_n_d_GSTS_WEB_ASSET_904 ut_n_d_GSTS_WEB_ASSET_905|**Positive Test Cases:** Download Asset with Authorised User **Negative Test Cases:** 1.Download Asset with Invalid Id 2.Download Asset without DB Connection 3.Download Asset with file type: Image 4.Download Asset with Invalid file type|Id|1|4|5|testAuthorisedUserDownloadAsset, testAuthorisedUserDownloadAssetWithInvalidId, testAuthorisedUserDownloadAssetWithoutDBConnection, testAuthorisedUserDownloadAssetWithAttachmentTypeImage, testAuthorisedUserDownloadAssetWithInvalidFileType|

#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_n_c_GSTS_WEB_ASSET_4|Unauthorised User does not have permission to create| **AssetType:** Enum Values **MovableType** **assetTag:** 1.Valid Characters 2.length>3 and length<64 3.null **assetValue:** 1.value>0 2.null **purchaseDate:** 1.null 2.Date before Present Date **warrantyPeriod:** 1.value > 0 2.null **latitude** **longitude**  **manufacturer:** 1.valid characters 2.length > 3 and length < 32 3.null **descr:** 1.Valid characters 2.length >6 and length<256 3.null **approverName**|0|1|1|testUnAuthorisedUserCreateAsset|
|1.0|Create Form|ut_n_c_GSTS_WEB_ASSET_111 |Open Asset Create Form with UnAuthorised User|N/A|0|1|1|testUnAuthorisedUserOpenAssetCreateForm|
|1.0|Update|ut_n_u_GSTS_WEB_ASSET_202| Unauthorised User does not have permission to UPDATE | **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserUpdateAsset|
|1.0|Update Form|ut_n_u_GSTS_WEB_ASSET_207|Open Asset Update Form with Unauthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserOpenAssetUpdateFormWithInvalidId|
|1.0| Remove |ut_n_r_GSTS_WEB_ASSET_305|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserRemoveAsset|
|1.0|Remove Form|ut_n_r_GSTS_WEB_ASSET_308|Open Asset Remove Form with Unauthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserOpenAssetRemoveForm|
|1.0| View |ut_n_v_GSTS_WEB_ASSET_402 |Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testUnauthorisedUserViewAssetWithValidId|
|1.0| Search |ut_n_s_GSTS_WEB_ASSET_502|Unauthorised User does not have permission to search|  **AssetType:** Enum Values **assetTag:** 1.valid characters 2.length>3 and length<64 3.null|0|1|1|testUnAuthorisedUserSearchAsset|
|1.0| List |ut_n_l_GSTS_WEB_ASSET_602|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testUnAuthorisedUserListAsset|
|1.0| PDF |ut_n_ep_GSTS_WEB_ASSET_808 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_ASSET_809 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_ASSET_810 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_ASSET_811 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListXlx|
|1.0| Download |ut_n_d_GSTS_WEB_ASSET_902|Download Asset with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserDownloadAsset|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|-----------|
|1.0|Create|ut_n_v_GSTS_WEB_ASSET_700| Creating Asset at state level with authorised User| N/A |Will not be created|1|testAuthorisedUserCreateAssetStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_ASSET_701| View Asset at state level with authorised user| N/A |User not able to view the asset at state level|1|testViewAssetAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_ASSET_702| View One panchayat Asset at Another Panchayat with authorised user| N/A |Not to able to view asset at different panchayat|1|testViewAssetAtAnotherPanchayat|
|1.0|Remove|ut_n_v_GSTS_WEB_ASSET_703|Remove Asset with Authorised User at State Level| N/A |Will not be Removed|1|testAuthorisedUserRemoveAssetAtStateLevel|
|1.0|Create|ut_n_v_GSTS_WEB_ASSET_704| Creating Asset at district level with authorised User| N/A |Will not be created|1|testAuthorisedUserCreateAssetStateLevel|testAuthorisedUserCreateAssetDistrictLevel|
|1.0|Create|ut_n_v_GSTS_WEB_ASSET_705| Creating Asset at division level with authorised User| N/A |Will not be created|1|testAuthorisedUserCreateAssetStateLevel|testAuthorisedUserCreateAssetDivisionLevel|
|1.0|Create|ut_n_v_GSTS_WEB_ASSET_706| Creating Asset at mandal level with authorised User| N/A |Will not be created|1|testAuthorisedUserCreateAssetStateLevel|testAuthorisedUserCreateAssetMandalLevel|

## Security compliance check
1. Only user having the user role with permission **ROLE_ASSET_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_ASSET_UPDATE** should update this functionality 
1. Only user having the user role with permission **ROLE_ASSET_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_ASSET_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the ASSETS in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
