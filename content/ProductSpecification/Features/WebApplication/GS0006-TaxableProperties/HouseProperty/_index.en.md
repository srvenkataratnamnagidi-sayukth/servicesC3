---
title: House Property
tags : ["Composing"]
---

## Introduction
House Property is one of the basic features of the software product which contains the data of all the house properties in the Telangana state. By using this house property feature, user have to store every house property data and user can know about every house property in the state. Every house property should be stored under the respective panchayat only. House Module feature embedded in the house property. While creating house property, house module details are also collected and stored. House Modules means house is divided into modules i.e. each floor in a buidling as one house module and each building as another module. All the Building Floor details and Building Numbers are stored in house module feature.

## Business Assumptions
1. House Property feature should be planned at the design phase.
1. User should be in the panchayat level to create the house property.
1. Owner Aadhaar number is required to create the house property.

## Requirements
### Functional Requirements
1. House Property feature only accessible at the panchayat level.
1. While creating house property, the owner's aadhaar number will bind to it.
1. Only one house property is allowed with the same name.

### Non-functional Requirements
1. To create the house Property, an organization survey status type should be started.
1. Multiple users can create house property in the same panchayat.
1. One citizen can have multiple house properties in the same panchayat or different panchayats.

### Problem Statement
House Property feature is required to store all the house property details in the panchayat level.

### Design 
1. Each House property has an owner's Aadhaar number, Door number, Latitude, Longitude, Building Category, Site Area, and Plinth Area.
1. Each House Module has Building Number, Building Floor Number, Roof Type, Construction Type, Plinth Length, Plinth Breadth, Plinth Area, and Tax Start Date.
1. We can Create, Update, View, and remove the house property.
1. Only one house property is allowed with the same name.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Citizen|||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_house_property_search|To search the house property|
|uc_house_property_create|To create the house property|
|uc_house_property_update|To update the house property|
|uc_house_property_remove|To remove the house property|
|uc_house_property_view|To view the house property|
|uc_house_property_list|To view all the house properties|
|uc_house_property_export|To export the house property in 2 formats Excel, PDF|


#### Model Attributes
##### House Property
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9/:#, _\.\-,@,&, Space, minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|YES|NO|YES|YES|YES|YES||
|location|YES|NA|a-zA-Z0-9/:#, _\.\-,@,&, (, ), Space, minlen=3, maxlen=64|@Column(name = "location", length = 64, nullable = false)|location varchar(64) NOT NULL|YES|NO|YES|YES|YES|YES||
|geoLat|YES|NA|0-9.|@Column(name = "geo_lat", length = 24, nullable = false)|geo_lat varchar(24) NOT NULL|YES|NO|YES|YES|NO|NO||
|geoLng|YES|NA|0-9.|@Column(name = "geo_lng", length = 24, nullable = false)|geo_lng varchar(24) NOT NULL|YES|NO|YES|YES|NO|NO||
|block|YES|NA|Drop Down Values|@Column(name = "block", nullable = false)|block bigint(20) NOT NULL|YES|NO|YES|YES|NO|NO||
|pvtTap|YES|NA|Drop Down Values|@Column(name = "pvt_tap", nullable = false)|pvt_tap bigint(20) NOT NULL|YES|YES|YES|YES|NO|NO||
|houseCategory|YES|NA|DropDown Values|@Enumerated(EnumType.STRING)	@Column(name = "house_category", length = 16, nullable = true)|house_category varchar(16) NOT NULL|YES|NO|YES|YES|YES|YES||
|commercialType|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "commercial_type", length = 16, nullable = true)|commercial_type varchar(64) DEFAULT NULL,|YES|NO|YES|YES|NO|NO||
|exemptionType|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "exemption_type", length = 16, nullable = true)|exemption_type varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|NO||
|concessionType|YES|NA|DropDown Values|@Enumerated(EnumType.STRING)@Column(name = "concession_type", length = 64, nullable = true)|concession_type varchar(64) DEFAULT NULL|YES|NO|YES|YES|NO|NO||
|siteLength|YES|NA|0-9.|@Column(name = "site_length", nullable = true)|site_length float(9,2) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|siteBreadth|YES|NA|0-9.|@Column(name = "site_breadth", nullable = true)|site_breadth float(9,2) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|siteArea|YES|NA|0-9.|@Column(name = "site_area", nullable = true)|site_area float(16,2) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|drainageType|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "drainage", length = 16, nullable = true)|drainage varchar(16) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|roadType|YES|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "road", length = 16, nullable = true)|road varchar(16) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|landRecordType|YES|NA|DropDown Values|@Enumerated(EnumType.STRING)	@Column(name = "land_record_type", length = 32, nullable = true)|land_record_type varchar(32) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|landSurveyNumber|YES|NA|DropDown Values|@Column(name = "land_survey_number", nullable = true)|land_survey_number varchar(64) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|electricityConnections|YES|0|Drop Down Values|@Column(name = "electricity_Connections", nullable = true)|electricity_Connections bigint(20) DEFAULT '0'|YES|YES|YES|YES|NO|NO||
|soakPitsCount|YES|0|Drop Down Values|@Column(name = "soakPits_Count", nullable = true)|soakPits_Count bigint(20) DEFAULT '0'|YES|YES|YES|YES|NO|NO||
|lpgConnectionCount|YES|0|Drop Down Values|@Column(name = "lpg_ConnectionCount", nullable = true)|lpg_ConnectionCount bigint(20) DEFAULT '0'|YES|YES|YES|YES|NO|NO||
|toiletCount|YES|0|Drop Down Values|@Column(name = "toilet_Count", nullable = true)|toilet_Count bigint(20) DEFAULT '0'|YES|YES|YES|YES|NO|NO||
|treesCount|YES|0|Drop Down Values|@Column(name = "trees_Count", nullable = true)|trees_Count bigint(20) DEFAULT '0'|YES|YES|YES|YES|NO|NO||
|legalIssues|YES|0|Boolean|@Column(name = "legal_issues", nullable = false)|legal_issues boolean DEFAULT false|YES|YES|YES|YES|NO|NO||
|frontPhoto|YES|NA|Attachment|@Column(name = "front_photo", length = 36, nullable = false)|front_photo varchar(36) NOT NULL|YES|NO|NO|YES|NO|NO||
|apartment|YES|0|Boolean|@Column(name = "apartment", nullable = true)|apartment boolean DEFAULT false|YES|YES|YES|YES|NO|NO||
|apartmentName|NO|NA|a-zA-Z0-9/:#, _\.\-,@,&, Space, minlen=3, maxlen=64|@Column(name = "apartment_name", length = 64, nullable = true)|apartment_name varchar(64) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|communityName|NO|NA|a-zA-Z0-9/:#, _\.\- Space, minlen=3, maxlen=64|@Column(name = "community_name", length = 64, nullable = true)|community_name varchar(64) DEFAULT NULL|YES|YES|YES|YES|NO|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=256|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

##### House Module
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|buildingNumber|YES|NA|0-9|@Column(name = "building_number", length = 8, nullable = false)|building_number bigint(20) NOT NULL|YES|YES|NO|YES|NO|NO||
|buildingFloorType|YES|NA|0-9|@Column(name = "building_floor_type", length = 16, nullable = false)|building_floor_type bigint(20) NOT NULL|YES|YES|NO|YES|NO|NO||
|RoofType|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "roof", length = 16, nullable = false)|roof varchar(32) NOT NULL|YES|YES|NO|YES|NO|NO||
|ConstructionType|YES|NA|Drop Down Values|@Enumerated(EnumType.STRING) @Column(name = "construction", length = 16, nullable = false)|construction varchar(16) NOT NULL|YES|YES|NO|YES|NO|NO||
|plingthLength|YES|NA|0-9|@Column(name = "plingth_length", nullable = true)|plingth_length float(9,2) DEFAULT NULL|YES|YES|NO|YES|NO|NO||
|plingthBreadth|YES|NA|0-9|@Column(name = "plingth_breadth", nullable = true)|plingth_breadth float(9,2) DEFAULT NULL|YES|YES|NO|YES|NO|NO||
|area|YES|NA|0-9|@Column(name = "area", nullable = false)|area float(16,2) NOT NULL|YES|YES|NO|YES|NO|NO||
|taxStartDate|YES|NA|Date Time|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "tax_start_date", length = 16, nullable = false)|tax_start_date datetime NOT NULL|YES|YES|NO|YES|NO|NO||

#### ENUM CONSTANTS

##### House Category

{{<mermaid align="left">}}
classDiagram
    class HouseCategory{
      RESIDENTIAL
      COMMERCIAL
      EXEMPTION
      NONE
    }
{{< /mermaid >}}

##### Commercial Type

{{<mermaid align="left">}}
classDiagram
    class CommercialType{
      SHOPS
      OFFICES_AND_BANKS
      HOSPITAL_AND_NURSING_HOME
      EDUCATIONAL_INSTITUTIONS
      HOTELS_LODGING_AND_RESTAURANTS
      GODOWNS
      INDUSTRIES
      CINEMA_THEATRES
      OTHERS
	  NONE
    }
{{< /mermaid >}}

##### Exemption Type

{{<mermaid align="left">}}
classDiagram
    class ExemptionType{
      ARV_OR_CAP_EXEMPTION
      CHOULTARIES
      EDUCATIONAL_INSTITUTIONS
      ANCIENT_MONUMENTS
      CHARITABLE_HOSPITALS
      PUBLIC_WORSHIP
      OTHERS
      GP_PROPERTY
      TEMPLES
      CENTRAL_OR_STATE_PROPERTY													
	  CHURCH
	  MAZEED
	  WAQF_BOARD_PROPERTY
	  ELECTRICITY_TRANSCO
	  RTC
	  COLLAPSED_HOUSES
	  OPEN_LANDS
	  NONE
    }
{{< /mermaid >}}

##### Drainage Type

{{<mermaid align="left">}}
classDiagram
    class DrainageType{
      NONE
	  OTHER
	  UNDER_GROUND
	  KACCHA
	  PAKKA
    }
{{< /mermaid >}}
##### Road Type

{{<mermaid align="left">}}
classDiagram
    class RoadType{
      EARTHEN
      GRAVEL
      WBM
      CC
      BT
      NONE
    }
{{< /mermaid >}}

##### Land Record Type

{{<mermaid align="left">}}
classDiagram
    class Name{
      NONE
	  REVENUE_REGISTRATION
	  PD_ACT
    }
{{< /mermaid >}}

##### Roof Type

{{<mermaid align="left">}}
classDiagram
    class RoofType{
      RCC
      AC_SHEETS_OR_ZINC_SHEETS
      COUNTRY_OR_MANGALORE_TILES
      SHABAD_STONES
      THATCHED_OR_MUD_ROOF
      NONE
    }
{{< /mermaid >}}

##### Construction Type

{{<mermaid align="left">}}
classDiagram
    class ConstructionType{
      COMPLETED
      NOT_COMPLETED
      NONE
    }
{{< /mermaid >}}


#### Feature Permission
|Permission code|Action|
|---------------|-------|
|HOUSE_PROPERTY_CREATE|Create|
|HOUSE_PROPERTY_UPDATE|Update|
|HOUSE_PROPERTY_REMOVE|Remove|
|HOUSE_PROPERTY_VIEW|View|
|HOUSE_PROPERTY_VIEW|List|
|HOUSE_PROPERTY_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|gs_property__name__category__org_panchayat_id (org_panchayat_id, category, name)|
|Foreign Key|fk__gs_property__caid(caid) REFERENCES gs_citizen (aid)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_HOUSE_PROPERTY_CREATE|Only user having the user role with this permission should create this functionality|
|AC_ROLE_HOUSE_PROPERTY_UPDATE|Only user having the user role with this permission should update this functionality|
|AC_ROLE_HOUSE_PROPERTY_REMOVE|Only user having the user role with this permission should remove this functionality|
|AC_ROLE_HOUSE_PROPERTY_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_HOUSE_PROPERTY_VIEW|Only user having the user role with this permission should export the house property in 2 formats Excel, PDF|

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
	HousePropertyMenu((House Property Menu))
	ListPage{House Property List Page}
	CreatePage((Create Page))
	UpdatePage((Update Page))
    RemovePage((Remove Page))
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->HousePropertyMenu
    subgraph Menu
    HousePropertyMenu
	end
	subgraph List
	HousePropertyMenu-->ListPage
	ListPage--C-U-R-V-E-->ListPage
	end
	subgraph Error
	HousePropertyMenu-->ErrorPage
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
1. Only a user with the HOUSE_PROPERTY_VIEW permission will be allowed to perform the below operations.

{{<mermaid align="center">}}
sequenceDiagram
    participant HousePropertyListPage as Browser
    participant Net as Browser Net Tools
	participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, GET /app/ctx/HouseProperty/list ListPage
        Net--x-HousePropertyListPage: F : Connection Error
        HousePropertyListPage->>+cloud: S:  GET /app/ctx/HouseProperty/list ListPage
        cloud-->>-HousePropertyListPage: RES: List Page
    end
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, GET /app/HouseProperty/create/form CreateFormPage
        Net--x-HousePropertyListPage: F : Connection Error
        HousePropertyListPage->>+cloud: S : GET /app/HouseProperty/create/form CreateFormPage
        cloud-->>-HousePropertyListPage: RES: Create Form Loaded
    end
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, POST /app/HouseProperty/create Create
        Net--x-HousePropertyListPage: F : Connection Error
        HousePropertyListPage->>+cloud: S : POST /app/HouseProperty/create Create
        cloud-->>-HousePropertyListPage: RES: A House Property Successfully Created
    end
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, GET /app/HouseProperty/update/form UpdateFormPage
        Net--x-HousePropertyListPage: F : Connection Error
        alt
		note right of Net:  House Property Cache Object Found
        HousePropertyListPage->>+Cache: S : GET /app/HouseProperty/update/form UpdateFormPage
        Cache-->>-HousePropertyListPage: RES: Update Form Loaded
        else
		note right of Net:  House Property Cache Object Not Found
        Cache->>+cloud: GET /app/HouseProperty/update/form UpdateFormPage
        cloud-->>-HousePropertyListPage: RES: Update Form Loaded
        end
    end
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, POST /app/HouseProperty/update update
        Net--x-HousePropertyListPage: F : Connection Error
        HousePropertyListPage->>+cloud: S : POST /app/HouseProperty/update Update
        cloud-->>-HousePropertyListPage: RES: A House Property Successfully Updated
    end
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, GET /app/HouseProperty/remove/form RemoveFormPage
        Net--x-HousePropertyListPage: F : Connection Error
        alt
		note right of Net:  House Property Cache Object Found
        HousePropertyListPage->>+Cache: S : GET /app/HouseProperty/remove/form RemoveFormPage
        Cache-->>-HousePropertyListPage: RES : Remove Form Loaded
        else
		note right of Net:  House Property Cache Object Not Found
        Cache->>+cloud: S : GET /app/HouseProperty/remove/form RemoveFormPage
        cloud-->>-HousePropertyListPage: RES : Remove Form Loaded
        end
    end
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, POST /app/HouseProperty/remove Remove
        Net--x-HousePropertyListPage: F : Connection Error
        HousePropertyListPage->>+cloud: S : POST /app/HouseProperty/remove Remove
        cloud-->>-HousePropertyListPage: RES: A House Property Successfully Removed
    end
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, GET /app/HouseProperty/view ViewPage
        Net--x-HousePropertyListPage: F : Connection Error
        alt
		note right of Net:  House Property Cache Object Found
        HousePropertyListPage->>+Cache: S : GET /app/HouseProperty/view ViewPage
        Cache-->>-HousePropertyListPage: RES: houseProperty View
        else
		note right of Net:  House Property Cache Object Not Found
        Cache->>+cloud: GET /app/HouseProperty/view ViewPage
        cloud-->>-HousePropertyListPage: RES: houseProperty View
        end
    end
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, GET /app/HouseProperty/exportPdf ExportPdf
        Net--x-HousePropertyListPage: F : Connection Error
        alt
		note right of Net:  House Property Cache Object Found
        HousePropertyListPage->>+Cache: S : GET /app/HouseProperty/exportPdf ExportPdf
        Cache-->>-HousePropertyListPage: RES: houseProperty Pdf
        else
		note right of Net:  House Property Cache Object Not Found
        Cache->>+cloud: GET /app/HouseProperty/exportPdf ExportPdf
        cloud-->>-HousePropertyListPage: RES: houseProperty Pdf
        end
    end
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, GET /app/HouseProperty/exportListPdf ExportListPdf
        Net--x-HousePropertyListPage: F : Connection Error
        HousePropertyListPage->>+cloud: S : GET /app/HouseProperty/exportListPdf ExportListPdf
        cloud-->>-HousePropertyListPage: RES: houseProperty List Pdf
    end
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, GET /app/HouseProperty/exportXlx ExportXlx
        Net--x-HousePropertyListPage: F : Connection Error
        alt
		note right of Net:  House Property Cache Object Found
        HousePropertyListPage->>+Cache: S : GET /app/HouseProperty/exportXlx ExportXlx
        Cache-->>-HousePropertyListPage: RES: House Property Xlx
        else
		note right of Net:  House Property Cache Object Not Found
        Cache->>+cloud: GET /app/HouseProperty/exportXlx ExportXlx
        cloud-->>-HousePropertyListPage: RES: houseProperty Xlx
        end
    end
    rect rgb(244,244,244)
        HousePropertyListPage->>+Net: Check Internet, GET /app/HouseProperty/exportListXlx ExportListXlx
        Net--x-HousePropertyListPage: F : Connection Error
        HousePropertyListPage->>+cloud: S : GET /app/HouseProperty/exportListXlx ExportListXlx
        cloud-->>-HousePropertyListPage: RES: houseProperty List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create | ut_p_c_GSTS_WEB_HOUSEPROPERTY_101 ut_p_c_GSTS_WEB_HOUSEPROPERTY_113 ut_n_c_GSTS_WEB_HOUSEPROPERTY_102 ut_n_c_GSTS_WEB_HOUSEPROPERTY_108 ut_n_c_GSTS_WEB_HOUSEPROPERTY_700 ut_n_c_GSTS_WEB_HOUSEPROPERTY_1016 ut_n_c_GSTS_WEB_HOUSEPROPERTY_1017 ut_n_c_GSTS_WEB_HOUSEPROPERTY_1018 ut_n_c_GSTS_WEB_HOUSEPROPERTY_1019 ut_n_c_GSTS_WEB_HOUSEPROPERTY_212 ut_n_c_GSTS_WEB_HOUSEPROPERTY_114|**Positive Test Cases:** Creating House Property with Authorised User **Negative Test Cases:** 1.Creating House Property with Invalid Inputs 2.Creating House Property without DB Connection 3.Creating House Property with Authorised User At State level 4.Test- Negative Test Cases - Creating House Property with ground floor roof type is COUNTRY_OR_MANGALORE_TILES and first floor roof type is RCC 5.Test- Negative Test Cases - Creating House Property with Top floor length, breadth is greater than lower floor 6.Test- Negative Test Cases - Creating House Property with Plingth Area greater than Site Area 7.Test- Negative Test Cases - Creating House Property with Plingth length greater than Site Length 8.Creating House Property with Invalid House Module Inputs| **citizenId:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null  **Location:** 1.Valid Characters 2.length>3 and length<64 3.null **Latitude** **Longitude** **block:** 1.value >1 and value <99 2.null **pvtTap:** 1.value >1 and value <99 2.null **houseCategory:** Enumvalues:4 **siteLength:** 1.value >0 2.null 3.accepts max 6 digits either 123456 or 1234.56 **siteBreadth:** 1.value >0 2.null 3.accepts max 6 digits either 123456 or 1234.56 **siteArea:** 1.value >0 2.null 3.accepts max 10 digits **drainageType:** EnumValues:5 **roadType:** EnumValues:6 **landRecordType:** Enumvalues:3 **landSurveyNumber:** From Organization **electricityConnections:** 1.value >1 and value <99 2.null **soakPitsCount:** 1.value >1 and value <=20 2.null **lpgConnectionCount:** 1.value >1 and value <=20 2.null **toiletCount:** 1.value >1 and value <=20 2.null **treesCount:** 1.value >1 and value <=20 2.null **legalIssues:** Boolean **apartment:** Boolean **apartmentName:** 1.Valid Characters 2.length>3 and length<64 3.null **communityName:** 1.Valid Characters 2.length>3 and length<64 3.null|35|16|51|testAuthorisedUserCreateHouseProperty, testAuthorisedUserCreateHousePropertyNegativeTestCases, testAuthorisedUserCreateHousePropertyWithoutDBConnection, testAuthorisedUserCreateHousePropertyWithInvalidRoofType, testAuthorisedUserCreateHousePropertyWithInvalidLengthBreadthType, testAuthorisedUserCreateHousePropertyWithInvalidSiteArea, testAuthorisedUserCreateHousePropertyWithInvalidSiteLength, testAuthorisedUserCreateHousePropertyWithInvalidHouseModuleInputs, testAuthorisedUserCreateHousePropertyWithApartmentTrue, testAuthorisedUserCreateHousePropertyWithApartmentTrueNegativeTestCases| 
|1.0|Create Form| ut_p_c_GSTS_WEB_HOUSEPROPERTY_109 ut_n_c_GSTS_WEB_HOUSEPROPERTY_111 |**Positive Test Cases:** Open House Property Create Form with Authorised User **Negative Test Cases:** 1.Open House Property Create form without DB Connection|N/A|1|1|2|testAuthorisedUserOpenHousePropertyCreateForm, testAuthorisedUserOpenHousePropertyCreateFormWithoutDBConnection|
|1.0|Update| ut_p_u_GSTS_WEB_HOUSEPROPERTY_200 ut_n_u_GSTS_WEB_HOUSEPROPERTY_201 ut_n_u_GSTS_WEB_HOUSEPROPERTY_203 ut_n_u_GSTS_WEB_HOUSEPROPERTY_207 ut_n_u_GSTS_WEB_HOUSEPROPERTY_208 |**Positive Test Cases:** Updating House Property with Authorised User **Negative Test Cases:** 1.Updating House Property with Invalid Inputs 2.Updating House Property without DB Connection 3.Updating House Property with Invalid Id 4.Updating House Property with Invalid House Module Inputs| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|3|4|testAuthorisedUserUpdateHouseProperty, testAuthorisedUserUpdateHousePropertyNegativeTestCase, testAuthorisedUpdateHousePropertyWithoutDBConnection, testAuthorisedUserUpdateHousePropertyWithInvalidId, testAuthorisedUserUpdateHousePropertyWithInvalidHouseModuleInputs|
|1.0|Update Form| ut_n_u_GSTS_WEB_HOUSEPROPERTY_204 ut_n_u_GSTS_WEB_HOUSEPROPERTY_206 |**Positive Test Cases:** Open House Property Update Form with Authorised User **Negative Test Cases:** 1.Open House Property Update Form without DB Connection 2.Open House Property Update Form with Invalid Id|1.Valid Id |1|1|2|testAuthorisedUserOpenHousePropertyUpdateFormWithoutDBConnection, testAuthorisedUserOpenHousePropertyUpdateFormWithInvalidId|
|1.0|Remove| ut_p_r_GSTS_WEB_HOUSEPROPERTY_301 ut_n_r_GSTS_WEB_HOUSEPROPERTY_300 ut_n_r_GSTS_WEB_HOUSEPROPERTY_302 ut_n_r_GSTS_WEB_HOUSEPROPERTY_304 ut_n_r_GSTS_WEB_HOUSEPROPERTY_309 |**Positive Test Cases:** Removing House Property with Authorised User **Negative Test Cases:** 1.Removing House Property with Invalid Id 2.Removing House Property with Invalid Input 3.Removing House Property without DB Connection 4.Removing House Property with Invalid Comment| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |1|4|5|testAuthorisedUserRemoveHouseProperty, testAuthorisedUserRemoveHousePropertyWithInvalidId, testAuthorisedUserRemoveHousePropertyNegativeTestCase, testAuthorisedUserRemoveHousePropertyWithoutDBConnection, testAuthorisedUserRemoveHousePropertyWithInvalidComment|
|1.0|Remove Form| ut_p_r_GSTS_WEB_HOUSEPROPERTY_305 ut_n_r_GSTS_WEB_HOUSEPROPERTY_306 ut_n_r_GSTS_WEB_HOUSEPROPERTY_308 |**Positive Test Cases:** Open House Property Remove Form with Authorised User **Negative Test Cases:** 1.Open House Property Remove Form with Invalid Id 2.Open House Property Remove Form without DB Connection|1.Valid Id |1|2|3|testAuthorisedUserOpenHousePropertyRemoveForm, testAuthorisedUserOpenHousePropertyRemoveFormWithInvalidId, testAuthorisedUserOpenHousePropertyRemoveFormWithoutDBConnection|
|1.0| View |ut_p_v_GSTS_WEB_HOUSEPROPERTY_400 ut_p_v_GSTS_WEB_HOUSEPROPERTY_405 ut_n_v_GSTS_WEB_HOUSEPROPERTY_401 ut_n_v_GSTS_WEB_HOUSEPROPERTY_403 ut_n_v_GSTS_WEB_HOUSEPROPERTY_701 |**Positive Test Cases:** 1.View House Property with Valid Id  with Authorised User 2.View House Property with Valid Id with Authorised User **Negative Test Cases:** 1.View House Property with Invalid ID with Authorised User 2.View House Property without DB Connection 3.View House Property with Valid Id with Authorised User At State Level|1.Valid Id 2.Invalid Id|1|3|4|testAuthorisedUserViewHousePropertyWithValidId, testAuthorisedUserViewHousePropertyWithInValidId, testAuthorisedUserViewHousePropertyWithoutDBCnnection, testAuthorisedUserViewHousePropertyWithValidIdAndFamily|
|1.0| Search |ut_p_s_GSTS_WEB_HOUSEPROPERTY_500 ut_n_s_GSTS_WEB_HOUSEPROPERTY_501 ut_n_s_GSTS_WEB_HOUSEPROPERTY_502 ut_n_s_GSTS_WEB_HOUSEPROPERTY_504 |**Positive Test Cases:** Search House Property with Authorised User **Negative Test Cases:** 1.Search House Property with Invalid Inputs 2.Search House Property without DB Connection| **name:** 1.valid characters 2.length>3 and length<64 **citizenId:** 1.valid characters 2.length=4 or length=12 **location:** 1.valid characters 2.length>3 and length<64 **houseCategory:** Enum Values |4|5|9|testAuthorisedUserSearchHouseProperty, testAuthorisedUserSearchAuctionPropertyNegativeTestCases, testAuthorisedUserSearchHousePropertyWithoutDBConnection, testAuthorisedUserSearchHousePropertyNegativeCase|
|1.0| List |ut_p_l_GSTS_WEB_HOUSEPROPERTY_600 ut_n_l_GSTS_WEB_HOUSEPROPERTY_601 |**Positive Test Cases:** Check the object list with valid data  with Authorised User **Negative Test Cases:** 1.Check the object list with Invalid data|Validating with unique field|1|1|2|testAuthorisedUserListHouseProperty, testAuthorisedUserListHousePropertyNegativeTestCase|
|1.0| PDF |ut_p_ep_GSTS_WEB_HOUSEPROPERTY_800 ut_n_ep_GSTS_WEB_HOUSEPROPERTY_805 ut_p_ep_GSTS_WEB_HOUSEPROPERTY_818 |**Positive Test Cases:** 1.Export Pdf with Authorised User 2. Export House Property with Valid Id with Authorised User**Negative Test Cases:** 1.Export Pdf with Invalid Id 2.Export Pdf Without DB Connection|Id |1|1|2|testAuthorisedUserExportPdfWithValidId, testAuthorisedUserExportPdfWithInvalidId, testAuthorisedUserExportPdfHousePropertyWithValidIdAndFamily |
|1.0| List PDF |ut_p_elp_GSTS_WEB_HOUSEPROPERTY_801 ut_n_elp_GSTS_WEB_HOUSEPROPERTY_806 ut_n_elp_GSTS_WEB_HOUSEPROPERTY_815 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** Export List Pdf with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListPdfWithValidId, testAuthorisedUserExportListPdfWithInvalidId, testAuthorisedUserExportListPdfWithoutDBConnection|
|1.0| XLX |ut_p_ex_GSTS_WEB_HOUSEPROPERTY_802 ut_n_ex_GSTS_WEB_HOUSEPROPERTY_807 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** Export Xlx with Invalid Id and Without DB Connection|Id |1|1|2|testAuthorisedUserExportXlxWithValidId, testAuthorisedUserExportXlxWithInvalidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_HOUSEPROPERTY_803 ut_n_elx_GSTS_WEB_HOUSEPROPERTY_808 ut_n_elx_GSTS_WEB_HOUSEPROPERTY_816 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** Export List Xlx with Invalid Id and Without DB Connection|Id |1|2|3|testAuthorisedUserExportListXlxWithValidId, testAuthorisedUserExportListXlxWithInvalidId, testAuthorisedUserExportListXlxWithoutDBConnection|

#### UnAuthorised User  
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Name|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|----------------------|----|
|1.0| Create | ut_n_c_GSTS_WEB_HOUSEPROPERTY_105|Unauthorised User does not have permission to create| **citizenId:** 1.Valid characters 2.length=12 3.null **name:** 1.Valid Characters 2.length>3 and length<64 3.null  **Location:** 1.Valid Characters 2.length>3 and length<64 3.null **Latitude** **Longitude** **block:** 1.value >1 and value <99 2.null **pvtTap:** 1.value >1 and value <99 2.null **houseCategory:** Enumvalues:4 **siteLength:** 1.value >0 2.null 3.accepts max 6 digits either 123456 or 1234.56 **siteBreadth:** 1.value >0 2.null 3.accepts max 6 digits either 123456 or 1234.56 **siteArea:** 1.value >0 2.null 3.accepts max 10 digits **drainageType:** EnumValues:5 **roadType:** EnumValues:6 **landRecordType:** Enumvalues:3 **landSurveyNumber:** From Organization **electricityConnections:** 1.value >1 and value <99 2.null **soakPitsCount:** 1.value >1 and value <=20 2.null **lpgConnectionCount:** 1.value >1 and value <=20 2.null **toiletCount:** 1.value >1 and value <=20 2.null **treesCount:** 1.value >1 and value <=20 2.null **legalIssues:** Boolean|0|1|1|testUnAuthorisedUserCreateHouseProperty|
|1.0|Create Form| ut_n_c_GSTS_WEB_HOUSEPROPERTY_110|Open House Property Create form with UnAuthorised User|N/A|0|1|1|testUnAuthorisedUserOpenHousePropertyCreateForm|
|1.0|Update| ut_n_u_GSTS_WEB_HOUSEPROPERTY_202 |Unauthorised User does not have permission to update| **updateComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUpdateHouseProperty|
|1.0|Update Form| ut_n_u_GSTS_WEB_HOUSEPROPERTY_205|Open House Property Update Form with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserOpenHousePropertyUpdateForm|
|1.0|Remove| ut_n_r_GSTS_WEB_HOUSEPROPERTY_303 |Unauthorised User does not have permission to remove| **removeComment:** 1.valid characters[a-zA-Z0-9 :_/-.\] 2. length>3 and length<64 3.null |0|1|1|testUnAuthorisedUserRemoveHouseProperty|
|1.0|Remove Form| ut_n_r_GSTS_WEB_HOUSEPROPERTY_307 |Open House Property Remove Form with unauthorised user|1.Valid Id |0|1|1|testUnAuthorisedUserOpenHousePropertyRemoveForm|
|1.0| View |ut_n_v_GSTS_WEB_HOUSEPROPERTY_402 |Unauthorised User does not have permission to view|1.Valid Id |0|1|1|testUnAuthorisedUserViewHouseProperty|
|1.0| Search |ut_n_s_GSTS_WEB_HOUSEPROPERTY_503 |Unauthorised User does not have permission to search|  **name:** 1.valid characters 2.length>3 and length<64 **citizenId:** 1.valid characters 2.length=4 or length=12 **location:** 1.valid characters 2.length>3 and length<64 **houseCategory:** Enum Values |0|1|1|testUnAuthorisedUserSearchHouseProperty|
|1.0| List |ut_n_l_GSTS_WEB_HOUSEPROPERTY_602 |Unauthorised User does not have permission to list|Validating with unique field|0|1|1|testUnAuthorisedUserListHouseProperty|
|1.0| PDF |ut_n_ep_GSTS_WEB_HOUSEPROPERTY_810 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportPdf|
|1.0| List PDF |ut_n_elp_GSTS_WEB_HOUSEPROPERTY_811 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListPdf|
|1.0| XLX |ut_n_ex_GSTS_WEB_HOUSEPROPERTY_812 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportXlx|
|1.0| List XLX |ut_n_elx_GSTS_WEB_HOUSEPROPERTY_813 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testUnAuthorisedUserExportListXlx|

#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------| 
|1.0|Create|ut_n_c_GSTS_WEB_HOUSEPROPERTY_700| Creating House Property at state level with authorised User| N/A |Will not be created|1|testAuthorisedUserCreateHousePropertyAtStateLevel|
|1.0|View|ut_n_v_GSTS_WEB_HOUSEPROPERTY_701| View House Property at state level with authorised user| N/A |User not able to view the house property at state level|1|testAuthorisedUserViewHousePropertyAtStateLevel|

## Security compliance check
1. Only user having the user role with permission **ROLE_HOUSE_PROPERTY_CREATE** should create this functionality 
1. Only user having the user role with permission **ROLE_HOUSE_PROPERTY_UPDATE** should update this functionality 
1. Only user having the user role with permission **ROLE_HOUSE_PROPERTY_REMOVE** should remove this functionality 
1. Only user having the user role with permission **ROLE_HOUSE_PROPERTY_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the House Property should be provided in the User Manual.

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




 
