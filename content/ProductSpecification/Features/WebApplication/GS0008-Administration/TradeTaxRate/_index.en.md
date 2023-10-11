---
title: Trade Tax Rate
tags : ["Composing"]
---

## Introduction
Trade Tax Rate is one of the features of this software product. Trade tax rate is a tax rate defined for trade properties. It depends upon panchayat resolution. Trade tax rate may be different for trade properties based on trade category. It may vary from one panchayat to other panchayat. Users will have access to trade tax rates if they have permission, Otherwise will not access.

## Business Assumptions
What type of users can create trade tax rate should be planned at design phase.

## Requirements
### Functional Requirements
1. Users of all levels can create, remove, view and export the trade tax rate.  
1. We can create and remove trade tax rate at panchayat level only.
1. Trade Tax Rate feature is accessible at panchayat level only.
1. Panchayat Resolution is required to create a trade tax rate.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access trade tax rates.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Trade tax rate feature contains information about different trade tax rates of panchayat.

### Design 
1. Each trade tax rate has Panchayat Resolution, Tax Value (%), Trade Category Type, and Motor HP Tax (RS).
1. Each trade tax rate in same panchayat has unique panchayat resolution or unique trade cateogry.
1. We can create, remove, view and export the trade tax rate.


#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_trade_tax_rate_list|To view all the trade tax rates. This listing page should bind to a permission|
|uc_trade_tax_rate_create|To create the trade tax rate. This create page should bind to a permission|
|uc_trade_tax_rate_remove|To remove the trade tax rate. This remove page should bind to a permission|
|uc_trade_tax_rate_view|To view the trade tax rate. This view page should bind to a permission|
|uc_trade_tax_rate_search|To search the trade tax rate. This search page should bind to a permission|
|uc_trade_tax_rate_export|To export the trade tax rate in 2 formats Excel, PDF. This Export page should bind to a permission|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|panchayatResolution|YES|NA|Dropdown values|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "pr_id", nullable = false)|pr_id varchar(32) NOT NULL|YES|YES|YES|YES|NO||
|taxVal|YES|NA|0-9 and ., maxlen=6|@Column(name = "tax_val", nullable = false)|tax_val float(9,2) NOT NULL|YES|YES|YES|YES|NO||
|tradeCategory|YES|NA|Dropdown values|@Enumerated(EnumType.STRING) @Column(name = "trade_category", length = 32, nullable = false)|trade_category varchar(32) NOT NULL|YES|YES|YES|YES|YES||
|motorHpTaxVal|YES|NA|0-9 and ., maxlen=7|@Column(name = "motor_hptax", nullable = false)|motor_hptax float(9,2) NOT NULL|YES|YES|YES|YES|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ space _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Trade Category

{{<mermaid align="left">}}
classDiagram
    class TradeCatType{
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
|TRADE_TAX_RATE_VIEW|View|
|TRADE_TAX_RATE_CREATE|Create|
|TRADE_TAX_RATE_REMOVE|Remove|
|TRADE_TAX_RATE_VIEW|Export|
|TRADE_TAX_RATE_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_trade_tax_rate__prid__org_panchayat_id__trade_category (pr_id, org_panchayat_id, trade_category)|
|Foreign Key|fk__gs_trade_tax_rate__pr_id (pr_id) REFERENCES gs_pr (id)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_TRADE_TAX_RATE_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_TRADE_TAX_RATE_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_TRADE_TAX_RATE_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_TRADE_TAX_RATE_VIEW|Only user having the user role with this permission should export the user in 2 formats Excel, PDF|

## User Experience
1. Create page based on the standard UX Listing Template
1. Remove page based on the standard UX Listing Template
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    CreateBtn[Create]---RemoveBtn[Remove]---ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}

### State Machine
{{<mermaid align="left">}}
flowchart TD
	TradeTaxRateMenu((Trade Tax Rate Menu))
	ListPage{Trade Tax Rate List Page}
	CreatePage((Create Page))
	RemovePage((Remove Page))
	ViewPage((View Page))
	DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->TradeTaxRateMenu
    subgraph Menu
    TradeTaxRateMenu
    end
    subgraph   
    TradeTaxRateMenu-->ListPage
    ListPage--C-R-V-E-->ListPage
    end
    subgraph  
    TradeTaxRateMenu--F-->ErrorPage
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
|R|Remove|
|V|View|
|E|Export|
|S|Submit|
|B|Back|
|SB|Submit or Back|
|C-R-V-E|Create or Remove or View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|

### Sequence Diagram
1. Only a user with the TRADE_TAX_RATE_VIEW permission will be allowed to perform the below operations.


{{<mermaid align="center">}}
sequenceDiagram
    participant TradeTaxRateListpage as Browser
    participant Net as Browser Net Tools
    participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        TradeTaxRateListpage->>+Net: Check Internet, GET /app/ctx/TradeTaxRate/list ListPage
        Net--x-TradeTaxRateListpage: F : Connection Error
        TradeTaxRateListpage->>+cloud: S:  GET /app/ctx/TradeTaxRate/list ListPage
        cloud-->>-TradeTaxRateListpage: RES:List Page
    end
    rect rgb(244,244,244)
        TradeTaxRateListpage->>+Net: Check Internet, GET /app/TradeTaxRate/create/form CreateFormPage
        Net--x-TradeTaxRateListpage: F : Connection Error
        TradeTaxRateListpage->>+cloud: S : GET /app/TradeTaxRate/create/form CreateFormPage
        cloud-->>-TradeTaxRateListpage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        TradeTaxRateListpage->>+Net: Check Internet: POST /app/TradeTaxRate/create Create
        Net--x-TradeTaxRateListpage: F : Connection Error
        TradeTaxRateListpage->>+cloud: S : POST /app/TradeTaxRate/create Create
        cloud-->>-TradeTaxRateListpage: RES: An Trade TaxRate Successfully Created
    end
    rect rgb(244,244,244)
        TradeTaxRateListpage->>+Net: Check Internet: GET /app/TradeTaxRate/remove/form RemoveFormPage
        Net--x-TradeTaxRateListpage: F : Connection Error
        TradeTaxRateListpage->>+cloud: S : GET /app/TradeTaxRate/remove/form RemoveFormPage
        cloud-->>-TradeTaxRateListpage: RES : Remove Form Loaded
    end
    rect rgb(244,244,244)
        TradeTaxRateListpage->>+Net: Check Internet: POST /app/TradeTaxRate/remove Remove
        Net--x-TradeTaxRateListpage: F : Connection Error
        TradeTaxRateListpage->>+cloud: S : POST /app/TradeTaxRate/remove Remove
        cloud-->>-TradeTaxRateListpage: RES: An Trade TaxRate Successfully Removed
    end
    rect rgb(244,244,244)
        TradeTaxRateListpage->>+Net: Check Internet: GET /app/TradeTaxRate/view ViewPage
        Net--x-TradeTaxRateListpage: F : Connection Error
        alt
		note right of Net:  Trade Tax Rate Cache Object Found
        TradeTaxRateListpage->>+Cache: S : GET /app/TradeTaxRate/view ViewPage
        Cache-->>-TradeTaxRateListpage: RES: Trade TaxRate View
        else
		note right of Net:  Trade Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/TradeTaxRate/view ViewPage
        cloud-->>-TradeTaxRateListpage: RES: Trade TaxRate View
        end
    end
    rect rgb(244,244,244)
        TradeTaxRateListpage->>+Net: Check Internet: GET /app/TradeTaxRate/exportPdf ExportPdf
        Net--x-TradeTaxRateListpage: F : Connection Error 
        alt
		note right of Net:  Trade Tax Rate Cache Object Found
        TradeTaxRateListpage->>+Cache: S : GET /app/TradeTaxRate/exportPdf ExportPdf
        Cache-->>-TradeTaxRateListpage: RES: Trade TaxRate Pdf
        else
		note right of Net:  Trade Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/TradeTaxRate/exportPdf ExportPdf
        cloud-->>-TradeTaxRateListpage: RES: Trade TaxRate Pdf
        end
    end
    rect rgb(244,244,244)
        TradeTaxRateListpage->>+Net: Check Internet: GET /app/TradeTaxRate/exportListPdf ExportListPdf
        Net--x-TradeTaxRateListpage: F : Connection Error
        TradeTaxRateListpage->>+cloud: S : GET /app/TradeTaxRate/exportListPdf ExportListPdf
        cloud-->>-TradeTaxRateListpage: RES: Trade TaxRate List Pdf
    end
    rect rgb(244,244,244)
        TradeTaxRateListpage->>+Net: Check Internet: GET /app/TradeTaxRate/exportXlx ExportXlx
        Net--x-TradeTaxRateListpage: F : Connection Error
        alt
		note right of Net:  Trade Tax Rate Cache Object Found
        TradeTaxRateListpage->>+Cache: S : GET /app/TradeTaxRate/exportXlx ExportXlx
        Cache-->>-TradeTaxRateListpage: RES: Trade TaxRate Xlx
        else
		note right of Net:  Trade Tax Rate Cache Object Not Found
        Cache->>+cloud: GET /app/TradeTaxRate/exportXlx ExportXlx
        cloud-->>-TradeTaxRateListpage: RES: Trade TaxRate Xlx
        end
    end
    rect rgb(244,244,244)
        TradeTaxRateListpage->>+Net: Check Internet: GET /app/TradeTaxRate/exportListXlx ExportListXlx
        Net--x-TradeTaxRateListpage: F : Connection Error
        TradeTaxRateListpage->>+cloud: S : GET /app/TradeTaxRate/exportListXlx ExportListXlx
        cloud-->>-TradeTaxRateListpage: RES: Trade TaxRate List Xlx
    end

          
{{< /mermaid >}}


## Unit Test Cases
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|--------------------|-----|
|1.0| Create Form |ut_p_c_GSTS_WEB_TRADETAXRATE_120 ut_n_c_GSTS_WEB_TRADETAXRATE_115 ut_n_c_GSTS_WEB_TRADETAXRATE_130 |**Positive Test Cases:** 1.Open Trade TaxRate Create Form At panchayat level  **Negative Test Cases:** 1. Open Trade TaxRate Create Form with no panchayat resolution exists 2. Open Trade TaxRate Create Form Without Db connection |-|1|2|3|testPosOpenTradeTaxRateCreateFormWithAuthorisedUser,  testNegOpenTradeTaxRateCreateFormWithNoPanchayatResolutionExists,  testNegOpenTradeTaxRateCreateFormWithoutDBConnection|
|1.0| Create |ut_p_c_GSTS_WEB_TRADETAXRATE_150  ut_n_c_GSTS_WEB_TRADETAXRATE_160 ut_n_c_GSTS_WEB_TRADETAXRATE_140 ut_n_c_GSTS_WEB_TRADETAXRATE_270 ut_n_c_GSTS_WEB_TRADETAXRATE_280 |**Positive Test Cases:** Create Trade TaxRate with valid inputs with Panchayat Level Authorised User **Negative Test Cases:** 1.Create Trade TaxRate with Invalid inputs 2.Create Trade TaxRate without db connection 3.Create Trade TaxRate with Removed Panchayat Resolution Id  4.Create Trade TaxRate with Invalid Panchayat Resolution Id|**panchayatResolutionId:** drop down list **tradeCategory:** enums **taxVal:** 1.null 2. >=1 and <=100 **motorHpTaxVal:** 1.null 2. >=25 and <=2333|77|78|155|testPosAuthorisedPanchayatLevelUserCreateTradeTaxRateWithValidInputs,   testNegAuthorisedPanchayatLevelUserCreateTradeTaxRateWithInValidInputs,  testNegCreateTradeTaxRateWithoutDBconnection,  testNegCreateTradeTaxRateWithRemovedPanchayatResolutionId,  testNegCreateTradeTaxRateWithInvalidPanchayatResolutionId|
|1.0| Remove Form |ut_p_r_GSTS_WEB_TRADETAXRATE_330   ut_n_r_GSTS_WEB_TRADETAXRATE_340   ut_n_r_GSTS_WEB_TRADETAXRATE_350  ut_n_r_GSTS_WEB_TRADETAXRATE_410|**Positive Test Cases:** Open Trade TaxRate remove form with valid Id with Authorised Panchayat level user    **Negative Test Cases:**  1.Open Trade TaxRate remove Form Without DB Connection 2. Open Trade TaxRate remove Form with Invalid id   3.Open Trade TaxRate remove form with Already removed Trade TaxRate Id with Authorised user|Id|1|3|4|testPosAuthorisedPanLevelUserOpenPanLevelTradeTaxRateRemoveFormWithValidId,  testNegAuthorisedPanLevelUserOpenTradeTaxRateRemoveFormWithoutDBConnection,  testNegAuthorisedPanLevelUserOpenTradeTaxRateRemoveFormWithInValidId,  testNegAuthorisedPanUserOpenTradeTaxRateRemoveFormWithAlreadyRemovedId|
|1.0| Remove |ut_p_r_GSTS_WEB_TRADETAXRATE_360  ut_n_r_GSTS_WEB_TRADETAXRATE_370 ut_n_r_GSTS_WEB_TRADETAXRATE_390  ut_n_r_GSTS_WEB_TRADETAXRATE_400  ut_n_r_GSTS_WEB_TRADETAXRATE_420 |**Positive Test Cases:** Remove Trade TaxRate with Valid Remove Comment with Panchayat Level Authorised User **Negative Test Cases:** 1. Removing Trade TaxRate with invalid remove comment 2.Remove Trade TaxRate without db connection 3.Remove already removed Trade TaxRate  4. Remove Trade TaxRate with invalid Id| **removeComment:** 1.valid characters 2.length>=6 and length<=255 3.null |1|4|5|testPosPanLevelAuthorisedUserRemoveTradeTaxRateWithValidRemoveCommentAndValidId,  testNegPanLevelAuthorisedUserRemoveTradeTaxRateWithInValidRemoveCommentAndValidId,  testNegRemoveTradeTaxRateWithoutDbConnection,  testNegAuthorisedUserRemoveAlreadyRemovedTradeTaxRate,  testNegPanLevelAuthorisedUserRemoveTradeTaxRateWithInvalidId|
|1.0| View |ut_p_v_GSTS_WEB_TRADETAXRATE_530  ut_n_v_GSTS_WEB_TRADETAXRATE_540 ut_n_v_GSTS_WEB_TRADETAXRATE_550 |**Positive Test Cases:** View Trade TaxRate with Valid Id  with Authorised User **Negative Test Cases:** 1. View Trade TaxRate without db connection  2.View Trade TaxRate with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewTradeTaxRateWithValidId,  testNegAuthorisedUserViewTradeTaxRateWithoutDbConnection,  testNegAuthorisedUserViewTradeTaxRatewithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_TRADETAXRATE_680 ut_n_s_GSTS_WEB_TRADETAXRATE_690 ut_n_s_GSTS_WEB_TRADETAXRATE_700|**Positive Test Cases:** Search Trade TaxRate with valid inputs **Negative Test Cases:** 1.Search Trade TaxRate without db connection 2.Search Trade TaxRate with invalid inputs|**1.tradeCategory**|1|2|3|testPosAuthorisedUserSearchTradeTaxRateWithValidInputs,  testNegAuthorisedUserSearchTradeTaxRateWithoutDBconnection,  testNegAuthorisedUserSearchTradeTaxRateWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_TRADETAXRATE_610 ut_n_l_GSTS_WEB_TRADETAXRATE_620|**Positive Test Cases:** Get Trade TaxRate List **Negative Test Cases:** Get Trade TaxRate List without db connection|Validating with unique field|1|1|2|testPosAuthorisedUserGetTradeTaxRateList,  testNegAuthorisedUserTradeTaxRateListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_TRADETAXRATE_760   ut_n_ep_GSTS_WEB_TRADETAXRATE_770   ut_n_ep_GSTS_WEB_TRADETAXRATE_780 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportTradeTaxRatePdfWithValidId,  testNegAuthorisedUserExportTradeTaxRatePdfwithoutDbconnection,  testNegAuthorisedUserExportTradeTaxRatePdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_TRADETAXRATE_790   ut_n_elp_GSTS_WEB_TRADETAXRATE_800   ut_n_elp_GSTS_WEB_TRADETAXRATE_810 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportTradeTaxRateListPdfWithValidId,  testNegAuthorisedUserExportTradeTaxRateListPdfwithoutDbconnection,  testNegAuthorisedUserExportTradeTaxRateListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_TRADETAXRATE_820   ut_n_ex_GSTS_WEB_TRADETAXRATE_830   ut_n_ex_GSTS_WEB_TRADETAXRATE_840 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportTradeTaxRateXlxWithValidId,  testNegAuthorisedUserExportTradeTaxRateXlxwithoutDbconnection,  testNegAuthorisedUserExportTradeTaxRateXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_TRADETAXRATE_850   ut_n_elx_GSTS_WEB_TRADETAXRATE_860   ut_n_elx_GSTS_WEB_TRADETAXRATE_870 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportTradeTaxRateListXlxWithValidId,  testNegAuthorisedUserExportTradeTaxRateListXlxwithoutDbconnection,  testNegAuthorisedUserExportTradeTaxRateListXlxInValidId|


#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|----|
|1.0| Create Form|ut_n_c_GSTS_WEB_TRADETAXRATE_260|Unauthorised User opening Trade TaxRate create form||0|1|1|testNegUnAuthorisedUserOpenTradeTaxRateCreateForm|
|1.0| Create |ut_n_c_GSTS_WEB_TRADETAXRATE_250 |Unauthorised User does not have permission to create|**panchayatResolutionId:** drop down list **tradeCategory:** enums **taxVal:** 1.null 2. >=1 and <=100 **motorHpTaxVal:** 1.null 2. >=25 and <=2333|0|1|1|testNegUnAuthorisedUserCreateTradeTaxRate|
|1.0| Remove Form|ut_n_r_GSTS_WEB_TRADETAXRATE_510|Unauthorised User opening Trade TaxRate remove form||0|1|1|testNegUnAuthorisedPanLevelUserOpenTradeTaxRateRemoveForm|
|1.0| Remove |ut_n_r_GSTS_WEB_TRADETAXRATE_520|Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters 2. length>=6 and length<=255 3.null |0|1|1|testNegUnAuthorisedUserRemoveTradeTaxRate|
|1.0| View |ut_n_v_GSTS_WEB_TRADETAXRATE_600|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewTradeTaxRate|
|1.0| Search |ut_n_s_GSTS_WEB_TRADETAXRATE_750|Unauthorised User does not have permission to search|**1.tradeCategory**|0|1|1|testNegUnAuthorisedUserSearchTradeTaxRate|
|1.0| List |ut_n_l_GSTS_WEB_TRADETAXRATE_670|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserTradeTaxRateList|
|1.0| PDF |ut_n_ep_GSTS_WEB_TRADETAXRATE_920 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportTradeTaxRatePdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_TRADETAXRATE_930 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportTradeTaxRateListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_TRADETAXRATE_940 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportTradeTaxRateXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_TRADETAXRATE_950 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportTradeTaxRateListXlxWithValidId|


#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|-------|
|1.0|Create|ut_n_c_GSTS_WEB_TRADETAXRATE_170|Create Trade TaxRate at State Level| N/A |Will not be Created|1|testNegCreateTradeTaxRateAtStateLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_TRADETAXRATE_180|Open Trade TaxRate Create Form at State Level| N/A |Will not be Opened|1|testNegOpenTradeTaxRateCreateFormAtStateLevel|
|1.0|Create|ut_n_c_GSTS_WEB_TRADETAXRATE_190|Create Trade TaxRate at District Level| N/A |Will not be Created|1|testNegCreateTradeTaxRateAtDistLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_TRADETAXRATE_200|Open Trade TaxRate Create Form at District Level| N/A |Will not be Opened|1|testNegOpenTradeTaxRateCreateFormAtDistLevel|
|1.0|Create|ut_n_c_GSTS_WEB_TRADETAXRATE_210|Create Trade TaxRate at Division Level| N/A |Will not be Created|1|testNegCreateTradeTaxRateAtDivLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_TRADETAXRATE_220|Open Trade TaxRate Create Form at Division Level| N/A |Will not be Opened|1|testNegOpenTradeTaxRateCreateFormAtDivLevel|
|1.0|Create|ut_n_c_GSTS_WEB_TRADETAXRATE_230|Create Trade TaxRate at Mandal Level| N/A |Will not be Created|1|testNegCreateTradeTaxRateAtMandalLevel|
|1.0|Create Form|ut_n_c_GSTS_WEB_TRADETAXRATE_240|Open Trade TaxRate Create Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenTradeTaxRateCreateFormAtMandalLevel|
1.0|Create|ut_n_c_GSTS_WEB_TRADETAXRATE_290|Create Trade TaxRate in panchayat1112 with panchayat1111 Panchayat Resolution Id| N/A |Will not be Created|1|testNegCreateTradeTaxRateInpanchayat1112WithPanchayat1111PanchayatResolutionId|
|1.0|Remove Form|ut_n_r_GSTS_WEB_TRADETAXRATE_430|Open Trade TaxRate Remove Form at State Level| N/A |Will not be Opened|1|testNegOpenTradeTaxRateRemoveFormAtStateLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_TRADETAXRATE_440|Remove Trade TaxRate at State Level| N/A |Will not be Removed|1|testNegRemoveTradeTaxRateAtStateLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_TRADETAXRATE_450|Open Trade TaxRate Remove Form at District Level| N/A |Will not be Opened|1|testNegOpenTradeTaxRateRemoveFormAtDistLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_TRADETAXRATE_460|Remove Trade TaxRate at District Level| N/A |Will not be Removed|1|testNegRemoveTradeTaxRateAtDistLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_TRADETAXRATE_470|Open Trade TaxRate Remove Form at Division Level| N/A |Will not be Opened|1|testNegOpenTradeTaxRateRemoveFormAtDivLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_TRADETAXRATE_480|Remove Trade TaxRate at Division Level| N/A |Will not be Removed|1|testNegRemoveTradeTaxRateAtDivLevel|
|1.0|Remove Form|ut_n_r_GSTS_WEB_TRADETAXRATE_490|Open Trade TaxRate Remove Form at Mandal Level| N/A |Will not be Opened|1|testNegOpenTradeTaxRateRemoveFormAtMandalLevel|
|1.0|Remove|ut_n_r_GSTS_WEB_TRADETAXRATE_500|Remove Trade TaxRate at Mandal Level| N/A |Will not be Removed|1|testNegRemoveTradeTaxRateAtMandalLevel|
|1.0|View|ut_n_v_GSTS_WEB_TRADETAXRATE_560|View Trade TaxRate at State Level| N/A |Will not be Accessed|1|testNegViewTradeTaxRateAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_TRADETAXRATE_570|View Trade TaxRate at District Level| N/A |Will not be Accessed|1|testNegViewTradeTaxRateAtDistLevel|
|1.0|View|ut_n_v_GSTS_WEB_TRADETAXRATE_580|View Trade TaxRate at Division Level| N/A |Will not be Accessed|1|testNegViewTradeTaxRateAtDivLevel|
|1.0|View|ut_n_v_GSTS_WEB_TRADETAXRATE_590|View Trade TaxRate at Mandal Level| N/A |Will not be Accessed|1|testNegViewTradeTaxRateAtMandalLevel|
|1.0|List|ut_n_l_GSTS_WEB_TRADETAXRATE_630|Get Trade TaxRate List at State Level| N/A |Will not be Accessed|1|testNegTradeTaxRateListAtStateLevel|
|1.0|List|ut_n_l_GSTS_WEB_TRADETAXRATE_640|Get Trade TaxRate List at District Level| N/A |Will not be Accessed|1|testNegTradeTaxRateListAtDistLevel|
|1.0|List|ut_n_l_GSTS_WEB_TRADETAXRATE_650|Get Trade TaxRate List at Division Level| N/A |Will not be Accessed|1|testNegTradeTaxRateListAtDivLevel|
|1.0|List|ut_n_l_GSTS_WEB_TRADETAXRATE_660|Get Trade TaxRate List at Mandal Level| N/A |Will not be Accessed|1|testNegTradeTaxRateListAtMandalLevel|
|1.0|Search|ut_n_s_GSTS_WEB_TRADETAXRATE_710|Search Trade TaxRate  at State Level| N/A |Will not be Accessed|1|testNegSearchTradeTaxRateAtStateLevel|
|1.0|Search|ut_n_s_GSTS_WEB_TRADETAXRATE_720|Search Trade TaxRate  at District Level| N/A |Will not be Accessed|1|testNegSearchTradeTaxRateAtDistLevel|
|1.0|Search|ut_n_s_GSTS_WEB_TRADETAXRATE_730|Search Trade TaxRate  at Division Level| N/A |Will not be Accessed|1|testNegSearchTradeTaxRateAtDivLevel|
|1.0|Search|ut_n_s_GSTS_WEB_TRADETAXRATE_740|Search Trade TaxRate  at Mandal Level| N/A |Will not be Accessed|1|testNegSearchTradeTaxRateAtMandalLevel|
|1.0|Pdf|ut_n_p_GSTS_WEB_TRADETAXRATE_880|Export Trade TaxRate Pdf at State Level| N/A |Will not be exported|1|testNegExportTradeTaxRatePdfAtStateLevel|
|1.0|List Pdf|ut_n_p_GSTS_WEB_TRADETAXRATE_890|Export Trade TaxRate List Pdf at State Level| N/A |Will not be exported|1|testNegExportTradeTaxRateListPdfAtStateLevel|
|1.0|Xlx|ut_n_p_GSTS_WEB_TRADETAXRATE_900|Export Trade TaxRate Xlx at State Level| N/A |Will not be exported|1|testNegExportTradeTaxRateXlxAtStateLevel|
|1.0|List Xlx|ut_n_p_GSTS_WEB_TRADETAXRATE_910|Export Trade TaxRate List Xlx at State Level| N/A |Will not be exported|1|testNegExportTradeTaxRateListXlxAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_TRADETAXRATE_960|Panchayat1112 user trying to access Panchayat1111 Trade TaxRate which does not belongs to his context| N/A |Will not be accessed|1|testNegPanchayat1112UserAccessingPanchayat1111TradeTaxRate|
|1.0|Remove|ut_n_r_GSTS_WEB_TRADETAXRATE_965|Panchayat1112 user trying to remove Panchayat1111 Trade TaxRate which does not belongs to his context| N/A |Will not be removed|1|testNegPanchayat1112UserRemovingPanchayat1111TradeTaxRate|


## Security compliance check
1. Only user having the permission **ROLE_TRADE_TAX_RATE_VIEW** should view this functionality 
1. Only user having the permission **ROLE_TRADE_TAX_RATE_CREATE** should create this functionality 
1. Only user having the permission **ROLE_TRADE_TAX_RATE_REMOVE** should remove this functionality 
1. Only user having the permission **ROLE_TRADE_TAX_RATE_VIEW** should export this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the Trade Tax Rate in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
