---
title: Trade Property
tags : ["Composing"]
---

## Introduction
Trade Property is one of the basic features of the software product which contains the data of all the trade properties in the Telangana state. By using this trade property feature, we have to store every trade property data and know about every trade property in the state. Every trade property should be stored under the respective panchayat only.

## Business Assumptions
1. Trade Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the trade property.
1. Owner Aadhaar number is required to create the trade property.

## Requirements
### Functional Requirements
1. Trade Property feature only accessible at the panchayat level.
1. While creating trade property, the owner’s aadhaar number will bind to it.
1. Only one trade property is allowed with the same name.

### Non-functional Requirements
1. To create the trade Property, an organization survey status type should be started.
1. Multiple users can create trade property in the same panchayat.
1. One citizen can have multiple trade properties in the same panchayat or different panchayats.

### Problem Statement
Trade Property feature is required to store all the trade property details in the panchayat level.

### Design 
1. Each Trade property has an owner's Aadhaar number, Name, Latitude, Longitude, Trade Category, Motor capacity, Business Sanction Id, and Annual Turn over.
1. We can Create, Update, View, and remove the trade property.
1. Only one trade property is allowed with the same name.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Citizen|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_trade_property_list|To view all the trade properties|
|uc_trade_property_search|To search the trade property|
|uc_trade_property_create|To create the trade property|
|uc_trade_property_update|To update the trade property|
|uc_trade_property_remove|To remove the trade property|
|uc_trade_property_view|To view the trade property|
|uc_trade_property_export|To export the trade property in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9/:#, _\.\-, @, &, Space, minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|NO|YES|YES|YES|YES||
|location|YES|NA|a-zA-Z0-9/:#, _\.\-, @, &, (, ), Space, minlen=3, maxlen=64|@Column(name = "location", length = 64, nullable = false)|location varchar(64) NOT NULL|YES|NO|YES|YES|YES|YES||
|geoLat|YES|NA|0-9.|@Column(name = "geo_lat", length = 24, nullable = false)|geo_lat varchar(24) NOT NULL|YES|NO|YES|YES|NO|NO||
|geoLng|YES|NA|0-9.|@Column(name = "geo_lng", length = 24, nullable = false)|geo_lng varchar(24) NOT NULL|YES|NO|YES|YES|NO|NO||
|tradeCategory|YES|NA|DropDown Values|@Enumerated(EnumType.STRING)	@Column(name = "trade_category", length = 64, nullable = true)|trade_category varchar(64) DEFAULT NULL|YES|NO|YES|YES|YES|YES||
|motorHorsePower|YES|NA|DropDown Values|@Column(name = "motor_horse_power", nullable = false)|motor_horse_power bigint(20) DEFAULT NULL|YES|NO|YES|YES|NO|NO||
|businessSanctionId|NO|NA|a-zA-Z0-9/:#, _\.\-,Space, @, &|@Column(name = "business_sanction_id", length = 32, nullable = true)|business_sanction_id varchar(32) DEFAULT NULL|YES|NO|YES|YES|NO|NO||
|annualTurnover|NO|NA|0-9|@Column(name = "annual_turnover", nullable = true)|annual_turnover bigint(20) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|frontPhoto|YES|NA|Attachment|@Column(name = "front_photo", length = 36, nullable = false)|front_photo varchar(36) NOT NULL|YES|NO|NO|YES|NO|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Trade Category

{{<mermaid align="left">}}
classDiagram
    class TradeCategory{
      AGRO_CENTER
      ANIMAL_FEED
      AUTO_MOBILES
      BAKERY
      BOOKSTORE
      BRICKWORK
      CEMENT_SHOP
      CLOTH_SHOWROOM
      COMPUTER_CENTER
      COOL_DRINKS
      CRACKERS
      CYCLE_SHOP
      EGG_MART
      ELECTRICAL_ELECTRONICS
      EMPORIUM
      ENTERPRISE
      FERTILIZERS_PESTICIDES
      FINANCE
      FOOTWARE
      FURNITURE
      GAS_AGENCY
      GENERAL_STORES
      HARDWARE_SHOWROOM
      HOSPITALS
      HOTELS
      HOSTELS
      TEA_STALL
      DHABHA
      RICE_MILL
      INSTITUTE
      JEWELLERY
      KIRANA_GENERAL_STORE
      LODGE
      MEAT_CHICKEN_CENTER
      MEDICAL_STORE
      METAL_BRASS_ITEMS
      MILK_PARLOUR
      MILLS
      MOTOR_HP_BASED
      MUSICAL_SHOW_ROOM
      NET_CAFE
      OILS_PULSES
      OPTICAL_SHOWROOM
      PAINT_SHOP
      PAN_SHOP
      PETROL_BUNK
      PHOTO_STUDIO
      PLASTIC_ITEM_SHOP
      POULTRY_FORM
      PRINTING_PRESS
      REPAIRING_SHOP
      RICE_BOILERS
      STALLS
      STEEL_ITEMS
      SWEET_SHOP
      TAILORING_SHOP
      TENT_HOUSE
      THEATRES
      TILES_SANITORY
      TIMBER_SHOP
      TOY_SHOP
      TRADER_AGENCIES
      TRANSPORT
      VEGETABLES
      FRUITS
      WHOLESALE_MANDI
      WINE_SHOP
      WORKSHOP_LAZER
      XEROX_SHOP
      CELLPHONE_SHOP
      FISH_PRAWN_SHOP
      BAJJI_SHOP
      FRUIT_JUICE_SHOP
      BEAUTY_PARLOUR
	  BARBER_SHOP
	  GYM
	  CELL_TOWER
	  OTHER
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|TRADE_PROPERTY_CREATE|Create|
|TRADE_PROPERTY_UPDATE|Update|
|TRADE_PROPERTY_REMOVE|Remove|
|TRADE_PROPERTY_VIEW|View|
|TRADE_PROPERTY_VIEW|List|
|TRADE_PROPERTY_VIEW|Export|

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
|AC_ROLE_TRADE_PROPERTY_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_TRADE_PROPERTY_UPDATE|Only user having the user role with this permission should update this functionality|
|AC_ROLE_TRADE_PROPERTY_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_TRADE_PROPERTY_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_TRADE_PROPERTY_VIEW|Only user having the user role with this permission should export the user role in 2 formats Excel, PDF|

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
	TradePropertyMenu((Trade Property Menu))
	ListPage{Trade Property List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->TradePropertyMenu
    subgraph Menu
    TradePropertyMenu
	end
	subgraph List
	TradePropertyMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	TradePropertyMenu-->ErrorPage
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
1. Only a user with the TRADE_PROPERTY_VIEW permission will be allowed to perform the below operations.

{{<mermaid align="center">}}
sequenceDiagram
    participant TradePropertyListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, GET /app/ctx/TradeProperty/list ListPage
        Net--x-TradePropertyListPage: F : Connection Error
        TradePropertyListPage->>+cloud: S:  GET /app/ctx/TradeProperty/list ListPage
        cloud-->>-TradePropertyListPage: RES: List Page
    end
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, GET /app/TradeProperty/create/form CreateFormPage
        Net--x-TradePropertyListPage: F : Connection Error
        TradePropertyListPage->>+cloud: S : GET /app/TradeProperty/create/form CreateFormPage
        cloud-->>-TradePropertyListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, POST /app/TradeProperty/create Create
        Net--x-TradePropertyListPage: F : Connection Error
        TradePropertyListPage->>+cloud: S : POST /app/TradeProperty/create Create
        cloud-->>-TradePropertyListPage: RES: A Trade Property Successfully Created
    end
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, GET /app/TradeProperty/update/form UpdateFormPage
        Net--x-TradePropertyListPage: F : Connection Error
        alt
		note right of Net:  Trade Property Cache Object Found
        TradePropertyListPage->>+Cache: S : GET /app/TradeProperty/update/form UpdateFormPage
        Cache-->>-TradePropertyListPage: RES: Update Form Loaded
        else
		note right of Net:  Trade Property Cache Object Not Found
        Cache->>+cloud: GET /app/TradeProperty/update/form UpdateFormPage
        cloud-->>-TradePropertyListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, POST /app/TradeProperty/update update
        Net--x-TradePropertyListPage: F : Connection Error
        TradePropertyListPage->>+cloud: S : POST /app/TradeProperty/update Update
        cloud-->>-TradePropertyListPage: RES: A Trade Property Successfully Updated
    end
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, GET /app/TradeProperty/remove/form RemoveFormPage
        Net--x-TradePropertyListPage: F : Connection Error
        alt
		note right of Net:  Trade Property Cache Object Found
        TradePropertyListPage->>+Cache: S : GET /app/TradeProperty/remove/form RemoveFormPage
        Cache-->>-TradePropertyListPage: RES : Remove Form Loaded
        else
		note right of Net:  Trade Property Cache Object Not Found
        Cache->>+cloud: S : GET /app/TradeProperty/remove/form RemoveFormPage
        cloud-->>-TradePropertyListPage: RES : Remove Form Loaded
        end
    end
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, POST /app/TradeProperty/remove Remove
        Net--x-TradePropertyListPage: F : Connection Error
        TradePropertyListPage->>+cloud: S : POST /app/TradeProperty/remove Remove
        cloud-->>-TradePropertyListPage: RES: A Trade Property Successfully Removed
    end
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, GET /app/TradeProperty/view ViewPage
        Net--x-TradePropertyListPage: F : Connection Error
        alt
		note right of Net:  Trade Property Cache Object Found
        TradePropertyListPage->>+Cache: S : GET /app/TradeProperty/view ViewPage
        Cache-->>-TradePropertyListPage: RES: tradeProperty View
        else
		note right of Net:  Trade Property Cache Object Not Found
        Cache->>+cloud: GET /app/TradeProperty/view ViewPage
        cloud-->>-TradePropertyListPage: RES: tradeProperty View
        end
    end
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, GET /app/TradeProperty/exportPdf ExportPdf
        Net--x-TradePropertyListPage: F : Connection Error
        alt
		note right of Net:  Trade Property Cache Object Found
        TradePropertyListPage->>+Cache: S : GET /app/TradeProperty/exportPdf ExportPdf
        Cache-->>-TradePropertyListPage: RES: tradeProperty Pdf
        else
		note right of Net:  Trade Property Cache Object Not Found
        Cache->>+cloud: GET /app/TradeProperty/exportPdf ExportPdf
        cloud-->>-TradePropertyListPage: RES: tradeProperty Pdf
        end
    end
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, GET /app/TradeProperty/exportListPdf ExportListPdf
        Net--x-TradePropertyListPage: F : Connection Error
        TradePropertyListPage->>+cloud: S : GET /app/TradeProperty/exportListPdf ExportListPdf
        cloud-->>-TradePropertyListPage: RES: tradeProperty List Pdf
    end
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, GET /app/TradeProperty/exportXlx ExportXlx
        Net--x-TradePropertyListPage: F : Connection Error
        alt
		note right of Net:  Trade Property Cache Object Found
        TradePropertyListPage->>+Cache: S : GET /app/TradeProperty/exportXlx ExportXlx
        Cache-->>-TradePropertyListPage: RES: Trade Property Xlx
        else
		note right of Net:  Trade Property Cache Object Not Found
        Cache->>+cloud: GET /app/TradeProperty/exportXlx ExportXlx
        cloud-->>-TradePropertyListPage: RES: tradeProperty Xlx
        end
    end
    rect rgb(244,244,244)
        TradePropertyListPage->>+Net: Check Internet, GET /app/TradeProperty/exportListXlx ExportListXlx
        Net--x-TradePropertyListPage: F : Connection Error
        TradePropertyListPage->>+cloud: S : GET /app/TradeProperty/exportListXlx ExportListXlx
        cloud-->>-TradePropertyListPage: RES: tradeProperty List Xlx
    end
    
          
{{< /mermaid >}}


## Unit Test Cases
#### Authorised User  

|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create | ut_p_c_GSTS_WEB_TRADEPROPERTY_100 ut_n_c_GSTS_WEB_TRADEPROPERTY_101 ut_n_c_GSTS_WEB_TRADEPROPERTY_105 ut_n_c_GSTS_WEB_TRADEPROPERTY_110|**Positive Test Cases:** Creating Auction Property with Authorised User **Negative Test Cases:** 1.Creating Auction Property with Invalid Input 2.Creating Trade Property without DB Connecction 3.Creating Trade Property with Invalid Citizen Id At Wizard Step03| **citizenId:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null **Location:** 1.Valid Characters 2.length>3 and length<64 3.null **Latitude** **Longitude** **tradeCategory:** Enum Values **businessSanctionId:** 1.Valid Characters 2.length>=3 and length<=64 3.null 4. unique **annualTurnover:** 1.null 2.length>=3 and length<=10 **motorHorsePower:** Enum Values: 0L,1L,5L,10L,25L,50L,100L|15|7|22|testAuthorisedUserCreateTradeProperty, testAuthorisedUserCreateTradePropertyNegativeTestCases, testAuthorisedUserCreateTradePropertyWithoutDBConnection, testAuthorisedUserCreateTradePropertyWithInvalidCitizenId| 
|1.0|Create Form| ut_p_c_GSTS_WEB_TRADEPROPERTY_106 ut_n_c_GSTS_WEB_TRADEPROPERTY_108 |**Positive Test Cases:** Open Trade Property Create Form **Negative Test Cases:** 1.Open Trade Property Create Form without DB Connection|N/A|1|1|2|testAuthorisedUserOpenTradePropertyCreateForm, testAuthorisedUserOpenTradePropertyCreateFormWithoutDBConnection| 
|1.0|Update| ut_p_u_GSTS_WEB_TRADEPROPERTY_200 ut_n_u_GSTS_WEB_TRADEPROPERTY_201 ut_n_u_GSTS_WEB_TRADEPROPERTY_203 ut_n_u_GSTS_WEB_TRADEPROPERTY_204 |**Positive Test Cases:** Updating Trade Property with Authorised User **Negative Test Cases:** 1.Updating Trade Property with Invalid Comment 2.Updating Trade Property without DB Connection 3.Updating Trade Property with Invalid Id| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|3|4|testAuthorisedUserUpdateTradeProperty, testAuthorisedUserUpdateTradePropertyNegativeTestCases, testAuthorisedUserUpdateTradePropertyWithoutDBConnection, testAuthorisedUserUpdateTradePropertyWithInvalidId| 
|1.0|Update Form| ut_p_u_GSTS_WEB_TRADEPROPERTY_205 ut_n_u_GSTS_WEB_TRADEPROPERTY_206 ut_n_u_GSTS_WEB_TRADEPROPERTY_208 |**Positive Test Cases:** Open Trade Property Update Form with Valid Id **Negative Test Cases:** 1.Open Trade Property Update Form with Invalid Id 2.Open Trade Property Update Form without DB Connection|1.Valid Id|1|2|3|testAuthorisedUserOpenTradePropertyUpdateFormWithValidId, testAuthorisedUserOpenTradePropertyUpdateFormWithInvalidId, testAuthorisedUserOpenTradePropertyUpdateFormWithoutDBConnection| 
|1.0|Remove| ut_p_r_GSTS_WEB_TRADEPROPERTY_303 ut_n_r_GSTS_WEB_TRADEPROPERTY_300 ut_n_r_GSTS_WEB_TRADEPROPERTY_301 ut_n_r_GSTS_WEB_TRADEPROPERTY_302 ut_n_r_GSTS_WEB_TRADEPROPERTY_304 |**Positive Test Cases:** Removing Trade Property with Authorised User **Negative Test Cases:** 1.Removing Trade Property with Invalid Id 2.Removing Trade Property without DB Connection 3.Removing Trade Property with Invalid Id and Comment 4.Removing Trade Property with Invalid Comment| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|4|5| testAuthorisedUserRemoveTradeProperty, testAuthorisedUserRemoveTradePropertyWithInvalidId, testAuthorisedUserRemoveTradePropertyWithoutDBConnection, testAuthorisedUserRemoveTradePropertyWithInvalidIdAndComment, testAuthorisedUserRemoveTradePropertyNegativeTestCase| 
|1.0|Remove Form|ut_p_r_GSTS_WEB_TRADEPROPERTY_306 ut_n_r_GSTS_WEB_TRADEPROPERTY_307 ut_n_r_GSTS_WEB_TRADEPROPERTY_309|**Positive Test Cases:** Open Trade Property Remove Form with Valid Id **Negative Test Cases:** 1.Open Trade Property Remove Form with Invalid Id 2.Open Trade Property Remove Form without DB Connection|1.Valid Id|1|2|3|testAuthorisedUserOpenTradePropertyRemoveFormWithValidId, testAuthorisedUserOpenTradePropertyRemoveFormWithInvalidId, testAuthorisedUserOpenTradePropertyRemoveFormWithoutDBConnection| 
|1.0| View |ut_p_v_GSTS_WEB_TRADEPROPERTY_400 ut_n_v_GSTS_WEB_TRADEPROPERTY_401 ut_n_v_GSTS_WEB_TRADEPROPERTY_403 |**Positive Test Cases:** View Trade Property with Valid Id  with Authorised User**Negative Test Cases:** 1.View Trade Property with Invalid ID with Authorised User 2.View Trade Property without DB Connection|1.Valid Id 2.Invalid Id|1|2|3|testAuthorisedUserViewTradePropertyWithValidId, testAuthorisedUserViewTradePropertyWithInValidId, testAuthorisedUserViewTradePropertyWithoutDBConnection| 
|1.0| Search |ut_p_s_GSTS_WEB_TRADEPROPERTY_500 ut_n_s_GSTS_WEB_TRADEPROPERTY_501 ut_n_s_GSTS_WEB_TRADEPROPERTY_503 ut_n_s_GSTS_WEB_TRADEPROPERTY_504 |**Positive Test Cases:** Search Trade Property with Authorised User **Negative Test Cases:** 1.Search Trade Property with Invalid Inputs 2.Search Trade Property without DB Connection 3. Search Trade Property with Invalid dates with Authorised User| **name:** 1.valid characters 2.length>3 and length<64 **citizenId:** 1.valid characters 2.length=4 or length=12 **location:** 1.valid characters 2.length>3 and length<64 **tradeCategory:** Enum Values |4|7|11|testAuthorisedUserSearchTradeProperty, testAuthorisedUserSearchTradePropertyNegativeTestCases, testAuthorisedUserSearchTradePropertyWithoutDBConnection, testAuthorisedUserSearchTradePropertyNegativeCase| 
|1.0| List |ut_p_l_GSTS_WEB_TRADEPROPERTY_600 ut_n_l_GSTS_WEB_TRADEPROPERTY_601 ut_n_l_GSTS_WEB_TRADEPROPERTY_603 |**Positive Test Cases:** Check the object list with valid data with Authorised User **Negative Test Cases:** 1.Check the object list with Invalid data with Authorised User|Validating with unique field|1|2|3|testAuthorisedUserListTradeProperty, testAuthorisedUserListTradePropertyNegativeTestCase, testAuthorisedUserListTradePropertyWithoutDBConnection| 
|1.0| PDF |ut_p_ep_GSTS_WEB_TRADEPROPERTY_800 ut_n_ep_GSTS_WEB_TRADEPROPERTY_805 ut_n_ep_GSTS_WEB_TRADEPROPERTY_817 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection 3.Export Removed Trade Property Pdf, Xlx with Authorised User|Id |1|1|2|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId, testAuthorisedUserExportRemovedTradePropertyPdfXlx| 
|1.0| List PDF |ut_p_elp_GSTS_WEB_TRADEPROPERTY_801 ut_n_elp_GSTS_WEB_TRADEPROPERTY_806 ut_n_elp_GSTS_WEB_TRADEPROPERTY_813 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection| 
|1.0| XLX |ut_p_ex_GSTS_WEB_TRADEPROPERTY_802 ut_p_ex_GSTS_WEB_TRADEPROPERTY_816 ut_n_ex_GSTS_WEB_TRADEPROPERTY_807 |**Positive Test Cases:** 1.Export Xlx with Authorised User 2. Export Xlx with Valid id **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |2|1|3|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId, testAuthorisedUserExportXlxWithValidIdWithTradePropertyViewUser| 
|1.0| List XLX |ut_p_elx_GSTS_WEB_TRADEPROPERTY_803 ut_n_elx_GSTS_WEB_TRADEPROPERTY_808 ut_n_elx_GSTS_WEB_TRADEPROPERTY_815 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection| 

#### UnAuthorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create | ut_n_c_GSTS_WEB_TRADEPROPERTY_104|Unauthorised User does not have permission to create| **citizenId:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null **Location:** 1.Valid Characters 2.length>3 and length<64 3.null **Latitude** **Longitude** **tradeCategory:** Enum Values **businessSanctionId:** 1.Valid Characters 2.length>=3 and length<=64 3.null 4. unique **annualTurnover:** 1.null 2.length>=3 and length<=10 **motorHorsePower:** Enum Values: 0L,1L,5L,10L,25L,50L,100L|0|1|1| testUnAuthorisedUserCreateTradeProperty|
|1.0|Create Form|ut_n_c_GSTS_WEB_TRADEPROPERTY_107 |Open Trade Property Create Form with UnAuthorised user|N/A|0|1|1|
|1.0|Update| ut_n_u_GSTS_WEB_TRADEPROPERTY_202 |Unauthorised User does not have permission to update| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserUpdateTradeProperty|
|1.0|Update Form|ut_n_u_GSTS_WEB_TRADEPROPERTY_207|Open Trade Property Update Form with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserOpenTradePropertyUpdateForm|
|1.0|Remove| ut_n_r_GSTS_WEB_TRADEPROPERTY_305|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserRemoveTradeProperty|
|1.0|Update Form|ut_n_r_GSTS_WEB_TRADEPROPERTY_308|Open Trade Property Remove Form with UnAuthorised User|1.Valid Id|0|1|1|testUnAuthorisedUserOpenTradePropertyRemoveForm|
|1.0| View |ut_n_v_GSTS_WEB_TRADEPROPERTY_402|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testUnAuthorisedUserViewTradePropertyWithValidId|
|1.0| Search |ut_n_s_GSTS_WEB_TRADEPROPERTY_502 |Unauthorised User does not have permission to search|  **name:** 1.valid characters 2.length>3 and length<64 **citizenId:** 1.valid characters 2.length=4 or length=12 **location:** 1.valid characters 2.length>3 and length<64 **tradeCategory:** Enum Values |0|1|1|testUnAuthorisedUserSearchTradeProperty|
|1.0| List |ut_n_l_GSTS_WEB_TRADEPROPERTY_602 |Unauthorised User does not have permission to search|Validating with unique field|0|1|1|testUnAuthorisedUserListTradeProperty|
|1.0| PDF |ut_n_ep_GSTS_WEB_TRADEPROPERTY_808 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_TRADEPROPERTY_809 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_TRADEPROPERTY_810 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_TRADEPROPERTY_811 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListXlx|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Name|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|-----------|
|1.0|Create|ut_n_c_GSTS_WEB_TRADEPROPERTY_700| Creating Trade Property at state level with authorised User| N/A |Will not be created|1|testAuthorisedUserCreateTradePropertyAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_TRADEPROPERTY_701| View Trade Property at state level with authorised user| N/A |User not able to view the auction property at state level|1|testAuthorisedUserViewTradePropertyAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_TRADEPROPERTY_702| View Trade Property with Valid Id with Authorised User at Another Panchayat| N/A |User able to view the trade property at Another Panchayat if user has permission|1|testAuthorisedUserViewTradePropertyAtAnotherPanchayat|

## Security compliance check
1. Only user having the user role with permission **ROLE_TRADE_PROPERTY_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_TRADE_PROPERTY_UPDATE** should update this functionality 
1. Only user having the user role with permission **ROLE_TRADE_PROPERTY_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_TRADE_PROPERTY_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Trade Property should be provided in the User Manual.

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




 
