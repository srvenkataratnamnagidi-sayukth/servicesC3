---
title: Auction Property
tags : ["Composing"]
---

## Introduction
Auction Property is one of the basic features of the software product which contains the data of all the auction properties in the Telangana state. By using this auction property feature, user have to store every auction property data and user can know about every auction property in the state. Every auction property should be stored under the respective panchayat only. Auction property will be created based on auction assets. Auction assets is a feature that facilitates the buying and selling of assets. Assets may be Agricultural Lands, Fishing Ponds, Cattle Shed, Bandela Doddi, Shopping Malls, Tree, and more.  

## Business Assumptions
1. Auction Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the auction property.
1. Owner Aadhaar number is required to create the auction property.

## Requirements
### Functional Requirements
1. Auction Property feature only accessible at the panchayat level.
1. While creating auction property, the owner's aadhaar number will bind to it.
1. At least one Auction Asset is required to create the auction property.
1. Only one auction property creation will be allowed for a single auction asset

### Non-functional Requirements
1. To create the auction Property, an organization survey status type should be started.
1. Multiple users can create the auction property in the same panchayat.
1. One citizen can have multiple auction properties in the same panchayat or different panchayats.

### Problem Statement
Auction Property feature is required to store all the auction property details in the panchayat level.

### Design 
1. Each Auction property has an owner's Aadhaar number, Tax StartDate, Tax EndDate, Auction Data, Auction Date, and End bid.
1. We can Create, Update, View, and remove the auction property.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Citizen|||
|Auction Assets|||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_auction_property_list|To view all the auction properties|
|uc_auction_property_search|To search the auction property|
|uc_auction_property_create|To create the auction property|
|uc_auction_property_update|To update the auction property|
|uc_auction_property_remove|To remove the auction property|
|uc_auction_property_view|To view the auction property|
|uc_auction_property_export|To export the auction property in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|taxStartDate|YES|NA|Date|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "tax_start_date", length = 16, nullable = false)|tax_start_date datetime NOT NULL|YES|YES|YES|YES|NO|NO||
|taxEndDate|YES|NA|Date|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "tax_end_date", length = 16, nullable = false)|tax_end_date datetime DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|auctionData|YES|NA|DropDown Values|@ManyToOne(fetch = FetchType.LAZY, cascade = CascadeType.ALL) @JoinColumn(name = "auction_data_id", nullable = true)|auction_data_id VARCHAR(36) DEFAULT NULL|YES|NO|YES|YES|NO|NO||
|aucDate|YES|NA|Date|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "auc_date", length = 16, nullable = false)|auc_date datetime DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|endBid|YES|NA|0-9|@Column(name = "end_bid", nullable = true)|end_bid bigint(20) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|frontPhoto|YES|NA|Attachment|@Column(name = "front_photo", length = 36, nullable = false)|front_photo varchar(36) NOT NULL|YES|NO|NO|YES|NO|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS
No Enum Constants in auction property.

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|AUCTION_PROPERTY_CREATE|Create|
|AUCTION_PROPERTY_UPDATE|Update|
|AUCTION_PROPERTY_REMOVE|Remove|
|AUCTION_PROPERTY_VIEW|View|
|AUCTION_PROPERTY_VIEW|List|
|AUCTION_PROPERTY_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|gs_property__name__category__org_panchayat_id (org_panchayat_id, category, name)|
|Foreign Keys|1. fk__gs_property__caid(caid) REFERENCES gs_citizen (aid) |
||2. fk__gs_property__auction_data_id(auction_data_id) REFERENCES gs_auction_data (id)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_AUCTION_PROPERTY_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_AUCTION_PROPERTY_UPDATE|Only user having the user role with this permission should update this functionality|
|AC_ROLE_AUCTION_PROPERTY_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_AUCTION_PROPERTY_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_AUCTION_PROPERTY_VIEW|Only user having the user role with this permission should export the user role in 2 formats Excel, PDF|

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
	AuctionPropertyMenu((Auction Property Menu))
	ListPage{Auction Property List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->AuctionPropertyMenu
    subgraph Menu
    AuctionPropertyMenu
	end
	subgraph List
	AuctionPropertyMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	AuctionPropertyMenu-->ErrorPage
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
1. Only a user with the AUCTION_PROPERTY_VIEW permission will be allowed to perform the below operations.

{{<mermaid align="center">}}
sequenceDiagram
    participant AuctionPropertyListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, GET /app/ctx/AuctionProperty/list ListPage
        Net--x-AuctionPropertyListPage: F : Connection Error
        AuctionPropertyListPage->>+cloud: S:  GET /app/ctx/AuctionProperty/list ListPage
        cloud-->>-AuctionPropertyListPage: RES: List Page
    end
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, GET /app/AuctionProperty/create/form CreateFormPage
        Net--x-AuctionPropertyListPage: F : Connection Error
        AuctionPropertyListPage->>+cloud: S : GET /app/AuctionProperty/create/form CreateFormPage
        cloud-->>-AuctionPropertyListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, POST /app/AuctionProperty/create Create
        Net--x-AuctionPropertyListPage: F : Connection Error
        AuctionPropertyListPage->>+cloud: S : POST /app/AuctionProperty/create Create
        cloud-->>-AuctionPropertyListPage: RES: An Auction Property Successfully Created
    end
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, GET /app/AuctionProperty/update/form UpdateFormPage
        Net--x-AuctionPropertyListPage: F : Connection Error
        alt
		note right of Net:  Auction Property Cache Object Found
        AuctionPropertyListPage->>+Cache: S : GET /app/AuctionProperty/update/form UpdateFormPage
        Cache-->>-AuctionPropertyListPage: RES: Update Form Loaded
        else
		note right of Net:  Auction Property Cache Object Not Found
        Cache->>+cloud: GET /app/AuctionProperty/update/form UpdateFormPage
        cloud-->>-AuctionPropertyListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, POST /app/AuctionProperty/update update
        Net--x-AuctionPropertyListPage: F : Connection Error
        AuctionPropertyListPage->>+cloud: S : POST /app/AuctionProperty/update Update
        cloud-->>-AuctionPropertyListPage: RES: An Auction Property Successfully Updated
    end
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, GET /app/AuctionProperty/remove/form RemoveFormPage
        Net--x-AuctionPropertyListPage: F : Connection Error
        alt
		note right of Net:  Auction Property Cache Object Found
        AuctionPropertyListPage->>+Cache: S : GET /app/AuctionProperty/remove/form RemoveFormPage
        Cache-->>-AuctionPropertyListPage: RES : Remove Form Loaded
        else
		note right of Net:  Auction Property Cache Object Not Found
        Cache->>+cloud: S : GET /app/AuctionProperty/remove/form RemoveFormPage
        cloud-->>-AuctionPropertyListPage: RES : Remove Form Loaded
        end
    end
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, POST /app/AuctionProperty/remove Remove
        Net--x-AuctionPropertyListPage: F : Connection Error
        AuctionPropertyListPage->>+cloud: S : POST /app/AuctionProperty/remove Remove
        cloud-->>-AuctionPropertyListPage: RES: An Auction Property Successfully Removed
    end
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, GET /app/AuctionProperty/view ViewPage
        Net--x-AuctionPropertyListPage: F : Connection Error
        alt
		note right of Net:  Auction Property Cache Object Found
        AuctionPropertyListPage->>+Cache: S : GET /app/AuctionProperty/view ViewPage
        Cache-->>-AuctionPropertyListPage: RES: auctionProperty View
        else
		note right of Net:  Auction Property Cache Object Not Found
        Cache->>+cloud: GET /app/AuctionProperty/view ViewPage
        cloud-->>-AuctionPropertyListPage: RES: auctionProperty View
        end
    end
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, GET /app/AuctionProperty/exportPdf ExportPdf
        Net--x-AuctionPropertyListPage: F : Connection Error
        alt
		note right of Net:  Auction Property Cache Object Found
        AuctionPropertyListPage->>+Cache: S : GET /app/AuctionProperty/exportPdf ExportPdf
        Cache-->>-AuctionPropertyListPage: RES: auctionProperty Pdf
        else
		note right of Net:  Auction Property Cache Object Not Found
        Cache->>+cloud: GET /app/AuctionProperty/exportPdf ExportPdf
        cloud-->>-AuctionPropertyListPage: RES: auctionProperty Pdf
        end
    end
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, GET /app/AuctionProperty/exportListPdf ExportListPdf
        Net--x-AuctionPropertyListPage: F : Connection Error
        AuctionPropertyListPage->>+cloud: S : GET /app/AuctionProperty/exportListPdf ExportListPdf
        cloud-->>-AuctionPropertyListPage: RES: auctionProperty List Pdf
    end
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, GET /app/AuctionProperty/exportXlx ExportXlx
        Net--x-AuctionPropertyListPage: F : Connection Error
        alt
		note right of Net:  Auction Property Cache Object Found
        AuctionPropertyListPage->>+Cache: S : GET /app/AuctionProperty/exportXlx ExportXlx
        Cache-->>-AuctionPropertyListPage: RES: Auction Property Xlx
        else
		note right of Net:  Auction Property Cache Object Not Found
        Cache->>+cloud: GET /app/AuctionProperty/exportXlx ExportXlx
        cloud-->>-AuctionPropertyListPage: RES: auctionProperty Xlx
        end
    end
    rect rgb(244,244,244)
        AuctionPropertyListPage->>+Net: Check Internet, GET /app/AuctionProperty/exportListXlx ExportListXlx
        Net--x-AuctionPropertyListPage: F : Connection Error
        AuctionPropertyListPage->>+cloud: S : GET /app/AuctionProperty/exportListXlx ExportListXlx
        cloud-->>-AuctionPropertyListPage: RES: auctionProperty List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names| 
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create |ut_p_c_GSTS_WEB_AUCTIONPROPERTY_101 ut_n_c_GSTS_WEB_AUCTIONPROPERTY_102 ut_n_c_GSTS_WEB_AUCTIONPROPERTY_107|**Positive Test Cases:** Creating Auction Property with Authorised User **Negative Test Cases:** 1.Creating Auction Property with Invalid Inputs 2.Creating Auction Property without DB Connection| **citizenId:** 1.Valid characters 2.length=12 3.null **taxStartDate:** 1.null 2.Current Data or Before Current data 3.Before Tax End Date 4.After auction date **taxEndDate:** 1.null 2.After Tax start date **aucDate:** 1.null 2.Current Data or Before Current data 3.Before tax Start Date **auctionData:** 1.Null 2.Same Panchayat Auction Data 3.One auction data for one auction property only **endBid:** 1.null 2.Value > 0|3|8|11|testAuthorisedUserCreateAuctionProperty, testAuthorisedUserCreateAuctionPropertyNegativeTestCases, testAuthorisedUserCreateAuctionPropertyWithoutDBConnection|
|1.0|Create Form|ut_p_c_GSTS_WEB_AUCTIONPROPERTY_108 ut_n_c_GSTS_WEB_AUCTIONPROPERTY_110 |**Positive Test Cases:** Open Auction Property Create form With Authorised User **Negative Test Cases:** 1.Open Auction Property Create form Without DB Connection|N/A|1|1|2|testAuthorisedUserOpenAuctionPropertyCreateForm, testAuthorisedUserOpenAuctionPropertyCreateFormWithoutDBConnection|
|1.0|Update| ut_p_u_GSTS_WEB_AUCTIONPROPERTY_200 ut_n_u_GSTS_WEB_AUCTIONPROPERTY_201 ut_n_u_GSTS_WEB_AUCTIONPROPERTY_203 ut_n_u_GSTS_WEB_AUCTIONPROPERTY_207 ut_n_u_GSTS_WEB_AUCTIONPROPERTY_204 |**Positive Test Cases:** Updating Auction Property with Authorised User **Negative Test Cases:** 1.Updating Auction Property with Invalid Inputs 2.Updating Auction Property with Invalid Id 3.Updating Auction Property without DB Connection| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|4|5|testAuthorisedUserUpdateAuctionProperty, testAuthorisedUserUpdateAuctionPropertyNegativeTestCases, testAuthorisedUserUpdateAuctionPropertyWithInvalidId, testAuthorisedUserUpdateAuctionPropertyWithoutDBConnection, testAuthorisedUserUpdateAuctionPropertyNegativeTestCase|
|1.0|Update Form|ut_p_u_GSTS_WEB_AUCTIONPROPERTY_205 ut_n_u_GSTS_WEB_AUCTIONPROPERTY_206 |**Positive Test Cases:** Open Auction Property Update form With Authorised User **Negative Test Cases:** 1.Open Auction Property Update form Without DB Connection 2.Open Auction Property Update form with Invalid Id|1.Valid Id|1|1|2|testAuthorisedUserOpenAuctionPropertyUpdateFormWithValidId, testAuthorisedUserOpenAuctionPropertyUpdateFormWithInvalidId|
|1.0|Remove| ut_p_r_GSTS_WEB_AUCTIONPROPERTY_306 ut_n_r_GSTS_WEB_AUCTIONPROPERTY_304 ut_n_r_GSTS_WEB_AUCTIONPROPERTY_305 ut_n_r_GSTS_WEB_AUCTIONPROPERTY_307 ut_n_r_GSTS_WEB_AUCTIONPROPERTY_309 |**Positive Test Cases:** Removing Auction Property with Authorised User **Negative Test Cases:** 1.Removing Auction Property with Invalid Id 2.Removing Auction Property without DB Connection 3.Removing Auction Property with Invalid Comment 4.Removing Auction Property with Invalid Id and Comment| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|4|5|testAuthorisedUserRemoveAuctionProperty, testAuthorisedUserRemoveAuctionPropertyWithInvalidId, testAuthorisedUserRemoveAuctionPropertyWithoutDBConnection, testAuthorisedUserRemoveAuctionPropertyNegativeTestCases, testAuthorisedUserRemoveAuctionPropertyInvalidIdAndComment|
|1.0|Remove Form|ut_p_r_GSTS_WEB_AUCTIONPROPERTY_300 ut_n_r_GSTS_WEB_AUCTIONPROPERTY_301 ut_n_r_GSTS_WEB_AUCTIONPROPERTY_303 |**Positive Test Cases:** Open Auction Property Remove form With Authorised User **Negative Test Cases:** 1.Open Auction Property Remove form Without DB Connection 2.Open Auction Property Remove form with Invalid Id|1.Valid Id|1|2|3|testAuthorisedUserOpenAuctionPropertyRemoveFormWithValidId, testAuthorisedUserOpenAuctionPropertyRemoveFormWithInvalidId, testAuthorisedUserOpenAuctionPropertyRemoveFormWithoutDBConnection|
|1.0| View |ut_p_v_GSTS_WEB_AUCTIONPROPERTY_400 ut_n_v_GSTS_WEB_AUCTIONPROPERTY_401 |**Positive Test Cases:** View Auction Property with Valid Id with Authorised User**Negative Test Cases:** 1.View Auction Property with Invalid ID with Authorised User|1.Valid Id 2.Invalid Id|1|1|2|testAuthorisedUserViewAuctionPropertyWithValidId, testAuthorisedUserViewAuctionPropertyWithInValidId|
|1.0| Search |ut_p_s_GSTS_WEB_AUCTIONPROPERTY_500  ut_n_s_GSTS_WEB_AUCTIONPROPERTY_501 ut_n_s_GSTS_WEB_AUCTIONPROPERTY_503 ut_n_s_GSTS_WEB_AUCTIONPROPERTY_504 |**Positive Test Cases:** Search Auction Property with Authorised User **Negative Test Cases:** 1.Search Auction Property with Invalid Inputs 2.Search Auction Property without DB Connection 3.Search Auction Property with Invalid dates with Authorised User|  **name:** 1.valid characters 2.length>3 and length<64 **citizenId:** 1.valid characters 2.length=4 or length=12 **location:** 1.valid characters 2.length>3 and length<64 **auctionCategory:** Enum Values |4|4|8|testAuthorisedUserSearchAuctionProperty, testAuthorisedUserSearchAuctionPropertyNegativeTestCases, testAuthorisedUserSearchAuctionPropertyWithoutDBConnection, testAuthorisedUserSearchAuctionPropertyNegativeCase|
|1.0| List |ut_p_l_GSTS_WEB_AUCTIONPROPERTY_600  ut_n_l_GSTS_WEB_AUCTIONPROPERTY_601 |**Positive Test Cases:** Check the object list with valid data  with Authorised User **Negative Test Cases:** 1.Check the object list with Invalid data with Authorised User|Validating with unique field|1|1|2|testAuthorisedUserListAuctionProperty, testAuthorisedUserListAuctionPropertyNegativeTestCases|
|1.0| PDF |ut_p_ep_GSTS_WEB_AUCTIONPROPERTY_800 ut_n_ep_GSTS_WEB_AUCTIONPROPERTY_804 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|1|2|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_AUCTIONPROPERTY_801 ut_n_elp_GSTS_WEB_AUCTIONPROPERTY_805 ut_n_elp_GSTS_WEB_AUCTIONPROPERTY_812 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_AUCTIONPROPERTY_802 ut_n_ex_GSTS_WEB_AUCTIONPROPERTY_806 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|1|2|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_AUCTIONPROPERTY_803 ut_n_elx_GSTS_WEB_AUCTIONPROPERTY_807 ut_n_elx_GSTS_WEB_AUCTIONPROPERTY_813 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### UnAuthorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create | ut_n_c_GSTS_WEB_AUCTIONPROPERTY_105 |Unauthorised User does not have permission to create| **citizenId:** 1.Valid characters 2.length=12 3.null **taxStartDate:** 1.null 2.Current Data or Before Current data 3.Before Tax End Date 4.After auction date **taxEndDate:** 1.null 2.After Tax start date **aucDate:** 1.null 2.Current Data or Before Current data 3.Before tax Start Date **auctionData:** 1.Null 2.Same Panchayat Auction Data 3.One auction data for one auction property only **endBid:** 1.null 2.Value > 0|0|1|1|testUnAuthorisedUserCreateAuctionProperty|
|1.0|Create Form|ut_n_c_GSTS_WEB_AUCTIONPROPERTY_109 |Unauthorised User does not have permission to open create form|N/A|0|1|1|testUnAuthorisedUserOpenAuctionPropertyCreateForm|
|1.0|Update| ut_n_u_GSTS_WEB_AUCTIONPROPERTY_202 |Unauthorised User does not have permission to update| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserUpdateAuctionProperty|
|1.0|Remove| ut_n_r_GSTS_WEB_AUCTIONPROPERTY_308 |Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserRemoveAuctionProperty|
|1.0|Remove Form|ut_n_r_GSTS_WEB_AUCTIONPROPERTY_302 |Unauthorised User does not have permission to open remove form|N/A|0|1|1|testUnAuthorisedUserOpenAuctionPropertyRemoveForm|
|1.0| View |ut_n_v_GSTS_WEB_AUCTIONPROPERTY_12 |Unauthorised User does not have permission to view|1.Valid Id|0|0|0|
|1.0| Search |ut_n_s_GSTS_WEB_AUCTIONPROPERTY_502|Unauthorised User does not have permission to search|  **name:** 1.valid characters 2.length>3 and length<64 **citizenId:** 1.valid characters 2.length=4 or length=12 **location:** 1.valid characters 2.length>3 and length<64 **auctionCategory:** Enum Values |0|1|1|testUnAuthorisedUserSearchAuctionProperty|
|1.0| List |ut_n_l_GSTS_WEB_AUCTIONPROPERTY_602|Unauthorised User does not have permission to view the list of auction property|Validating with unique field|0|1|1|testUnAuthorisedUserListAuctionProperty|
|1.0| PDF |ut_n_ep_GSTS_WEB_AUCTIONPROPERTY_808 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_AUCTIONPROPERTY_809 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_AUCTIONPROPERTY_810 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_AUCTIONPROPERTY_811 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListXlx|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|-----------|
|1.0|Create|ut_n_c_GSTS_WEB_AUCTIONPROPERTY_700| Creating Auction Property at state level with authorised User| N/A |Will not be created|1|testAuthorisedUserCreateAuctionPropertyAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_AUCTIONPROPERTY_701| View Auction Property at state level with authorised user| N/A |User not able to view the auction property at state level|1|testAuthorisedUserViewAuctionPropertyAtStateLevel|


## Security compliance check
1. Only user having the user role with permission **ROLE_AUCTION_PROPERTY_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_AUCTION_PROPERTY_UPDATE** should update this functionality 
1. Only user having the user role with permission **ROLE_AUCTION_PROPERTY_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_AUCTION_PROPERTY_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Auction Property should be provided in the User Manual.

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




 
