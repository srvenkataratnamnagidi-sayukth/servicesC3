---
title: Auction Assets
tags : ["Composing"]
---

## Introduction
Auction Assets are one of the features of our software product. User should have the permission to access this feature.

## Business Assumptions
Creating, updating and removing the auction assets can be done at the run time based on the requirement.

## Requirements
### Functional Requirements
Only panchayat level users should create, update, remove or view the auction assets.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access auction assets.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Details of assets in a panchayat that were auctioned should be captured.

### Design 
1. We can Create, Update, View, and remove the auction assets.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_auction_data_create|To create the auction asset|
|uc_auction_data_update|To update the auction asset|
|uc_auction_data_remove|To remove the auction asset|
|uc_auction_data_view|To view the auction asset|
|uc_auction_data_search|To search the auction asset|
|uc_auction_data_export|To export the auction asset in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|Name|YES|NA|a-zA-Z0-9/:#, _\.\-, @, &, Space, minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false|name varchar(64) not null|YES|YES|YES|YES|YES|YES||
|Street Name|YES|NA|a-zA-Z0-9/:#, _\.\-, @, &, (, ), Space, minlen=3, maxlen=64|@Column(name = "location", length = 64, nullable = false)|location varchar(64) not null|YES|YES|YES|YES|YES|YES||
|Latitude|YES|NA|Allowed 0-9 and . only and in the format (xx.xxxxxxxx)|@Column(name = "geo_lat", length = 24, nullable = false)|geo_lat varchar(24) not null|YES|YES|YES|YES|NO|NO||
|Longitude|YES|NA|Allowed 0-9 and . only and in the format (xx.xxxxxxxx)|@Column(name = "geo_lng", length = 24, nullable = false)|geo_lng varchar(24) not null|YES|YES|YES|YES|NO|NO||
|Auction Category|YES|NA|Drop Down List|@Enumerated(EnumType.STRING) @Column(name = "auc_category", length = 64, nullable = false)|auc_category varchar(64) not null|YES|YES|YES|YES|YES|YES||
|StartBid|Yes|NA|Allowed 0-9 only|@Column(name = "start_bid", nullable = false)|start_bid bigint(20) not null|YES|YES|YES|YES|NO|NO||
|Auction Installment Count|YES|NA|Drop Down List|@Column(name = "auc_installment_count", nullable = false)|auc_installment_count bigint(20) not null|YES|YES|YES|YES|NO|NO||
|Deposit Amount|YES|NA|Allowed 0-9 only|@Column(name = "deposit_amt", nullable = false)|deposit_amt bigint(20) not null|YES|YES|YES|YES|NO|NO||
|Auction Installment1 (In %)|YES|NA|Allowed 0-9 only|@Column(name = "auc_install1", nullable = true)|auc_install1 float(9,2) default null|YES|YES|YES|YES|NO|NO||
|Auction Installment2 (In %)|YES|NA|Allowed 0-9 only|@Column(name = "auc_install2", nullable = true)|auc_install2 float(9,2) default null|YES|YES|YES|YES|NO|NO||
|Auction Installment3 (In %)|YES|NA|Allowed 0-9 only|@Column(name = "auc_install3", nullable = true)|auc_install3 float(9,2) default null|YES|YES|YES|YES|NO|NO||
|Auction Installment4 (In %)|YES|NA|Allowed 0-9 only|@Column(name = "auc_install4", nullable = true)|auc_install4 float(9,2) default null|YES|YES|YES|YES|NO|NO||
|Auction Installment5 (In %)|YES|NA|Allowed 0-9 only|@Column(name = "auc_install5", nullable = true)|auc_install5 float(9,2) default null|YES|YES|YES|YES|NO|NO||
|Front Photo|YES|NA|Upload Front Photo, Allowed formats like jpg, png, jpeg.|@Column(name = "front_photo", length = 36, nullable = false)|front_photo varchar(36) default null|YES|YES|NO|YES|NO|NO||
|Updated Reason|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . and length 6 to 256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|Removed Reason|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - , . and length 6 to 256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|AUCTION_DATA_CREATE|Create|
|AUCTION_DATA_UPDATE|Update|
|AUCTION_DATA_REMOVE|Remove|
|AUCTION_DATAY_VIEW|View|
|AUCTION_DATA_VIEW|List|
|AUCTION_DATA_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Keys|gs_auction_data__name (name)|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|ac_auction_data_create|Only user having the permission to create, should create this functionality|
|ac_auction_data_update|Only user having the permission to update, should update this functionality|
|ac_auction_data_remove|Only user having the permission to remove, should remove this functionality|
|ac_auction_data_view|Only user having the permission to view, should view this functionality|
|ac_auction_data_view|Only user having the permission to export, should export the user role in 2 formats Excel, PDF|

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
	AuctionAssetsMenu((Auction Assets Menu))
	ListPage{Auction Assets List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->AuctionAssetsMenu
    subgraph Menu
    AuctionAssetsMenu
	end
	subgraph List
	AuctionAssetsMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	AuctionAssetsMenu-->ErrorPage
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
    participant AuctionAssetsListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        AuctionAssetsListPage->>+Net: Check Internet, GET /app/ctx/AuctionData/list ListPage
        Net--x-AuctionAssetsListPage: F : Connection Error
        AuctionAssetsListPage->>+cloud: S:  GET /app/ctx/AuctionData/list ListPage
        cloud-->>-AuctionAssetsListPage: RES:List Page
    end
    rect rgb(244,244,244)
        AuctionAssetsListPage->>+Net: Check Internet, GET /app/AuctionData/create/form CreateFormPage
        Net--x-AuctionAssetsListPage: F : Connection Error
        AuctionAssetsListPage->>+cloud: S : GET /app/AuctionData/create/form CreateFormPage
        cloud-->>-AuctionAssetsListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        AuctionAssetsListPage->>+Net: Check Internet: POST /app/AuctionData/create Create
        Net--x-AuctionAssetsListPage: F : Connection Error
        AuctionAssetsListPage->>+cloud: S : POST /app/AuctionData/create Create
        cloud-->>-AuctionAssetsListPage: RES: An AuctionData Successfully Created
    end
    rect rgb(244,244,244)
        AuctionAssetsListPage->>+Net: Check Internet: POST /app/AuctionData/update update
        Net--x-AuctionAssetsListPage: F : Connection Error
        AuctionAssetsListPage->>+cloud: S : POST /app/AuctionData/update Update
        cloud-->>-AuctionAssetsListPage: RES: An AuctionData Successfully Updated
    end
    rect rgb(244,244,244)
        AuctionAssetsListPage->>+Net: Check Internet: GET /app/AuctionData/remove/form RemoveFormPage
        Net--x-AuctionAssetsListPage: F : Connection Error
        AuctionAssetsListPage->>+cloud: S : GET /app/AuctionData/remove/form RemoveFormPage
        cloud-->>-AuctionAssetsListPage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        AuctionAssetsListPage->>+Net: Check Internet: POST /app/AuctionData/remove Remove
        Net--x-AuctionAssetsListPage: F : Connection Error
        AuctionAssetsListPage->>+cloud: S : POST /app/AuctionData/remove Remove
        cloud-->>-AuctionAssetsListPage: RES: A AuctionData Successfully Removed
    end
    rect rgb(244,244,244)
        AuctionAssetsListPage->>+Net: Check Internet: GET /app/AuctionData/exportListPdf ExportListPdf
        Net--x-AuctionAssetsListPage: F : Connection Error
        AuctionAssetsListPage->>+cloud: S : GET /app/AuctionData/exportListPdf ExportListPdf
        cloud-->>-AuctionAssetsListPage: RES: auctionData List Pdf
    end
    rect rgb(244,244,244)
        AuctionAssetsListPage->>+Net: Check Internet: GET /app/AuctionData/exportListXlx ExportListXlx
        Net--x-AuctionAssetsListPage: F : Connection Error
        AuctionAssetsListPage->>+cloud: S : GET /app/AuctionData/exportListXlx ExportListXlx
        cloud-->>-AuctionAssetsListPage: RES: auctionData List Xlx
    end
    
          
{{< /mermaid >}}


## Unit Test Cases
#### Authorized User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0|Create| ut_p_c_GSTS_WEB_AUCTIONDATA_100 ut_n_c_GSTS_WEB_AUCTIONDATA_101| **Positive Test Cases:** Creating Auction data with Authorised User **Negative Test Cases:** 1.Create AuctionData with Invalid Inputs| **name:** 1.Valid Characters 2.length>3 and length<64 3.null **Location:** 1.Valid Characters 2.length>3 and length<64 3.null	**Latitude** **Longitude** **Auction Category:** Enum values:15 **Start bid:** 1.length>0 2.null 3.Valid characters **Deposit Amount:** 1.length>0 2.null 3.Valid characters **Auction Installment count:** 1.null 2.length>0 3.values should be <= 5 **aucInstall1** **aucInstall2** **aucInstall3** **aucInstall4** **aucInstall5**|15|4|19|testCreateAuctionData, testAuthorisedUserCreateAuctionDataNegativeTestCases|
|1.0|Create Form| ut_p_c_GSTS_WEB_AUCTIONDATA_105 ut_n_c_GSTS_WEB_AUCTIONDATA_106 |**Positive Test Cases:** Open AuctionData Create Form with authorised user **Negative Test Cases:** 1.Creating AuctionData without DB Connection|N/A|1|1|2|testAuthorisedUserOpenAuctionDataCreateForm, testAuthorisedUserCreateAuctionDataWithoutDBConnection|
|1.0|Update| ut_p_u_GSTS_WEB_AUCTIONDATA_200 ut_p_u_GSTS_WEB_AUCTIONDATA_209 ut_p_u_GSTS_WEB_AUCTIONDATA_211 ut_n_u_GSTS_WEB_AUCTIONDATA_201 ut_n_u_GSTS_WEB_AUCTIONDATA_203 ut_n_u_GSTS_WEB_AUCTIONDATA_204 ut_n_u_GSTS_WEB_AUCTIONDATA_210|**Positive Test Cases:** 1.Updating Auction Data with Authorised User 2.Updating Auction Data with All AuctionInstallment 3.Updating Auction Data with Authorised User**Negative Test Cases:** 1.Updating Auction Data with Invalid Comment 2.Updating Auction Data without DB Connection 3.Updating Auction Data with Invalid Id 4.Updating Auction Data with Invalid AuctionInstallments|**updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |2|4|6|testAuthorisedUserUpdateAuctionData, testAuthorisedUserUpdateAuctionDataNegativeTestCases, testAuthorisedUserUpdateAuctionDataWithoutDBConnection, testAuthorisedUserUpdateAuctionDataWithInvalidId, testAuthorisedUserUpdateAuctionDataAuctionInstallment1, testAuthorisedUserUpdateAuctionDataWithInvalidAuctionInstallments, testAuthorisedUserUpdateAuctionData6|
|1.0|Update Form|ut_p_u_GSTS_WEB_AUCTIONDATA_205 ut_n_u_GSTS_WEB_AUCTIONDATA_206 ut_n_u_GSTS_WEB_AUCTIONDATA_208|**Positive Test Cases:** Open Auction Data Update Form with valid Id **Negative Test Cases:** 1.Open Auction Data Update Form with Invalid Id 2.Open Auction Data Update Form without DB Connection|1.Valid Id|1|2|3|testAuthorisedUserOpenAuctionDataUpdateFormWithvalidId, testAuthorisedUserOpenAuctionDataUpdateFormWithInvalidId, testAuthorisedUserOpenAuctionDataUpdateFormWithoutDBConnection|
|1.0| Remove |ut_p_r_GSTS_WEB_AUCTIONDATA_300  ut_n_r_GSTS_WEB_AUCTIONDATA_301 ut_n_r_GSTS_WEB_AUCTIONDATA_303 ut_n_r_GSTS_WEB_AUCTIONDATA_304 ut_n_r_GSTS_WEB_AUCTIONDATA_305 |**Positive Test Cases:** Removing Auction Data with Authorised User **Negative Test Cases:** 1.Removing AuctionData with Invalid Comment 2.Removing AuctionData without DB Connection 3.Removing AuctionData with Invalid Id 4.Removing AuctionData with Invalid Id and comment|**removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|4|5|testAuthorisedUserRemoveAuctionData, testAuthorisedUserRemoveAuctionDataNegativeTestCases, testAuthorisedUserRemoveAuctionDataWithoutDBConnection, testAuthorisedUserRemoveAuctionDataWithInvalidId, testAuthorisedUserRemoveAuctionDataWithInvalidIdAndComment|
|1.0|Remove Form| ut_p_r_GSTS_WEB_AUCTIONDATA_306 ut_n_r_GSTS_WEB_AUCTIONDATA_307 ut_n_r_GSTS_WEB_AUCTIONDATA_309|**Positive Test Cases:** Open Auction Data Remove Form with valid Id **Negative Test Cases:** 1.Open Auction Data Remove Form with Invalid Id 2.Open Auction Data Remove Form without DB Connection|1.Valid Id|1|2|3|testAuthorisedUserOpenAuctionDataRemoveFormWithvalidId, testAuthorisedUserOpenAuctionDataRemoveFormWithInvalidId, testAuthorisedUserOpenAuctionDataRemoveFormWithoutDBConnection|
|1.0| View |ut_p_v_GSTS_WEB_AUCTIONDATA_400  ut_n_v_GSTS_WEB_AUCTIONDATA_401 ut_n_v_GSTS_WEB_AUCTIONDATA_403 |**Positive Test Cases:** View Auction Data with Valid Id  with Authorised User**Negative Test Cases:** 1.View Auction Data with Invalid ID with Authorised User 2.View Auction Data without DB Connection|1.Valid Id 2.Invalid Id|1|2|3|testAuthorisedUserViewAuctionDataWithValidId, testAuthorisedUserViewAuctionDataWithInValidId, testAuthorisedUserViewAuctionDataWithoutDBConnection|
|1.0| Search |ut_p_s_GSTS_WEB_AUCTIONDATA_500  ut_n_s_GSTS_WEB_AUCTIONDATA_501 ut_n_s_GSTS_WEB_AUCTIONDATA_503 ut_n_s_GSTS_WEB_AUCTIONDATA_504 |**Positive Test Cases:** Search Auction Data with Authorised User **Negative Test Cases:** 1.Search Auction Data with Invalid Inputs 2.Search Auction Data without DB Connection 3.Search Auction Data with Invalid dates with Authorised User|**1.name** **2.location** **3.AuctionCategoryType**|4|5|9|testAuthorisedUserSearchAuctionData, testAuthorisedUserSearchAuctionDataNegativeCases, testAuthorisedUserSearchAuctionDataWithoutDBConnection, testAuthorisedUserSearchAuctionDataNegativeCase|
|1.0| List |ut_p_l_GSTS_WEB_AUCTIONDATA_600  ut_n_l_GSTS_WEB_AUCTIONDATA_601|**Positive Test Cases:** Check the object list with valid data  with Authorised User **Negative Test Cases:** 1.Check the object list with Invalid data with Authorised User|Validating with unique field|1|1|2|testAuthorisedUserListAuctionData, testAuthorisedUserListAuctionDataNegativeTestCase|
|1.0| PDF |ut_p_ep_GSTS_WEB_AUCTIONDATA_800 ut_n_ep_GSTS_WEB_AUCTIONDATA_805 ut_n_ep_GSTS_WEB_AUCTIONDATA_812 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|2|3|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId, testAuthorisedUserExportPdfWithoutDBConnection|
|1.0| List PDF |ut_p_elp_GSTS_WEB_AUCTIONDATA_801 ut_n_elp_GSTS_WEB_AUCTIONDATA_806 ut_n_elp_GSTS_WEB_AUCTIONDATA_813|**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_AUCTIONDATA_802 ut_n_ex_GSTS_WEB_AUCTIONDATA_807 ut_n_ex_GSTS_WEB_AUCTIONDATA_814|**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId, testAuthorisedUserExportXlxWithoutDBConnection|
|1.0| List XLX |ut_p_elx_GSTS_WEB_AUCTIONDATA_803 ut_n_elx_GSTS_WEB_AUCTIONDATA_808 ut_n_elx_GSTS_WEB_AUCTIONDATA_815|**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|
|1.0| Download|ut_p_d_GSTS_WEB_AUCTIONDATA_900 ut_n_d_GSTS_WEB_AUCTIONDATA_901 ut_n_d_GSTS_WEB_AUCTIONDATA_903 ut_n_d_GSTS_WEB_AUCTIONDATA_904 ut_n_d_GSTS_WEB_AUCTIONDATA_905|**Positive Test Cases:** Download Asset with Authorised User **Negative Test Cases:** 1.Download Auction Asset with Invalid Id 2.Download Auction Asset without DB Connection 3.Download Auction Asset with file type: Image 4.Download Auction Asset with Invalid file type|Id|1|4|5|testAuthorisedUserDownloadAuctionAsset, testAuthorisedUserDownloadAuctionAssetWithInvalidId, testAuthorisedUserDownloadAuctionAssetWithoutDBConnection, testAuthorisedUserDownloadAuctionAssetWithAttachmentTypeImage, testAuthorisedUserDownloadAuctionAssetWithInvalidFileType|

#### Un Authorized User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0|Create| ut_n_c_GSTS_WEB_AUCTIONDATA_104| Unauthorised User does not have permission to CREATE| **name:** 1.Valid Characters 2.length>3 and length<64 3.null **Location:** 1.Valid Characters 2.length>3 and length<64 3.null	**Latitude** **Longitude** **Auction Category:** Enum values:15 **Start bid:** 1.length>0 2.null 3.Valid characters **Deposit Amount:** 1.length>0 2.null 3.Valid characters **Auction Installment count:** 1.null 2.length>0 3.values should be <= 5 **aucInstall1** **aucInstall2** **aucInstall3** **aucInstall4** **aucInstall5**|0|1|1|testUnAuthorisedUserCreateAuctionData|
|1.0|Update|ut_n_u_GSTS_WEB_AUCTIONDATA_202| Unauthorised User does not have permission to UPDATE | **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserUpdateAuctionData|
|1.0|Update Form|ut_n_u_GSTS_WEB_AUCTIONDATA_207|Open Auction Data Update Form with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserOpenAuctionDataUpdateForm|
|1.0| Remove |ut_n_r_GSTS_WEB_AUCTIONDATA_302|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserRemoveAuctionData|
|1.0|Remove Form|ut_n_r_GSTS_WEB_AUCTIONDATA_308|Open Auction Data Remove Form with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserOpenAuctionDataRemoveForm|
|1.0| View |ut_n_v_GSTS_WEB_AUCTIONDATA_402 |Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testUnAuthorisedUserViewAuctionDataWithValidId|
|1.0| Search |ut_n_s_GSTS_WEB_AUCTIONDATA_502|Unauthorised User does not have permission to search|  **1.name** **2.location** **3.AuctionCategoryType**|0|1|1|testUnAuthorisedUserSearchAuctionData|
|1.0| List |ut_n_l_GSTS_WEB_AUCTIONDATA_602|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testUnAuthorisedUserListAuctionData|
|1.0| PDF |ut_n_ep_GSTS_WEB_AUCTIONDATA_808 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_AUCTIONDATA_809 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_AUCTIONDATA_810 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_AUCTIONDATA_811 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListXlx|
|1.0| Download |ut_n_d_GSTS_WEB_AUCTIONDATA_902|Download Auction Asset with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserDownloadAuctionAsset|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|----|
|1.0|Create|ut_n_l_GSTS_WEB_AUCTIONDATA_700| Creating Auction Data at state level with authorised User| N/A |Will not be created|1|testCreateAuctionDataAtStateLevel|
|1.0|View|ut_n_l_GSTS_WEB_AUCTIONDATA_701| View One panchayat Auction data at Another Panchayat with authorised user| N/A |Able to view with authorised user|1|testAuthorisedUserViewAuctionDataAtAnotherPanchayat|

## Security compliance check
1. Only user having the user role with permission **ROLE_AUCTION_DATA_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_AUCTION_DATA_UPDATE** should update this functionality 
1. Only user having the user role with permission **ROLE_AUCTION_DATA_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_AUCTION_DATA_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the AUCTION ASSETS in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
