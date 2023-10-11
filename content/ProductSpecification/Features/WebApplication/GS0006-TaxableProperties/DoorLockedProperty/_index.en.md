---
title: Pending Property
tags : ["Composing"]
---

## Introduction
Pending Property is one of the basic features of the software product which contains the data of all the pending properties in the Telangana state. By using this pending property feature we have to store every pending property data and know about every pending property in the state. Every pending property should be stored under the respective panchayat only. Pending property means the property has no owner or no person is present at the property at the time of surveying. Pending properties will be later converted to the respected property if the property owner is present at the time of the second survey.

## Business Assumptions
1. Pending Property feature should be planned at the design phase.
1. Pending Property should be inserted manually to DB.

## Requirements
### Functional Requirements
1. Pending Property feature only accessible at the panchayat level.
1. Only one pending property is allowed with the same name for similar property.

### Non-functional Requirements
1. No Create, Update, and Remove operations for Pending Property.
1. Pending Property should be inserted manually to DB.

### Problem Statement
Pending Property feature is required to store all the pending property details in the panchayat level.

### Design 
1. Each Pending property has an Name, Location, Latitude, Longitude, Property Category Type, Land Record Type, Survey Number,Tax EndDate and Tax StartDate.
1. We can View, and Export the pending property.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|	

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_pending_property_list|To view all the pending properties|
|uc_pending_property_search|To search the pending property|
|uc_pending_property_view|To view the pending property|
|uc_pending_property_export|To export the pending property in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|name|YES|NA|a-zA-Z0-9/:#, _\\.\\-, Space, minlen=3, maxlen=64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) NOT NULL|NO|NO|NO|YES|YES|YES||
|location|YES|NA|a-zA-Z0-9/:#, _\\.\\-, (, ), @, &, Space, minlen=3, maxlen=64|@Column(name = "location", length = 64, nullable = false)|location varchar(64) NOT NULL|NO|NO|NO|YES|YES|YES||
|geoId|YES|NA|a-zA-Z0-9.,|@Column(name = "geoid", length = 64, nullable = false, unique = true)|geoid varchar(64) NOT NULL|NO|NO|NO|YES|YES|YES||
|category|YES|NA|DropDown Values|@Enumerated(EnumType.STRING)	@Column(name = "category", length = 16, nullable = false)|category varchar(16) NOT NULL|NO|NO|NO|YES|YES|YES||
|geoLat|YES|NA|0-9.|@Column(name = "geo_lat", length = 24, nullable = false)|geo_lat varchar(24) NOT NULL|NO|NO|NO|YES|NO|NO||
|geoLng|YES|NA|0-9.|@Column(name = "geo_lng", length = 24, nullable = false)|geo_lng varchar(24) NOT NULL|NO|NO|NO|YES|NO|NO||
|houseCategory|NO|NA|DropDown Values|@Enumerated(EnumType.STRING)	@Column(name = "house_category", length = 16, nullable = true)|house_category varchar(16) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|commercialType|NO|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "commercial_type", length = 64, nullable = true)|commercial_type varchar(64) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|exemptionType|NO|NA|DropDown Values|@Enumerated(EnumType.STRING) @Column(name = "exemption_type", length = 64, nullable = true)|exemption_type varchar(64) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|concessionType|YES|NA|DropDown Values|@Enumerated(EnumType.STRING)@Column(name = "concession_type", length = 64, nullable = true)|concession_type varchar(64) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|siteLength|NO|NA|0-9.|@Column(name = "site_length", nullable = true)|site_length float(9,2) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|siteBreadth|NO|NA|0-9.|@Column(name = "site_breadth", nullable = true)|site_breadth float(9,2) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|siteArea|NO|NA|0-9.|@Column(name = "site_area", nullable = true)|site_area float(16,2) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|landRecordType|YES|NA|DropDown Values|@Enumerated(EnumType.STRING)	@Column(name = "land_record_type", length = 32, nullable = false)|land_record_type varchar(32) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|surveyNumber|YES|NA|DropDown Values|@Column(name = "survey_number", length = 16, nullable = false)|survey_number varchar(16) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|legalIssues|YES|0|Boolean|@Column(name = "legal_issues", nullable = true)|legal_issues boolean DEFAULT false|NO|NO|NO|YES|NO|NO||
|surveyTime|NO|NA|0-9|@Column(name = "survey_time", nullable = true)|survey_time bigint(20) DEFAULT 0|NO|NO|NO|YES|NO|NO||
|surveyStartTime|NO|NA|DateTime|@DateTimeFormat(pattern = "dd-MM-yyyy HH:mm") @Temporal(TemporalType.TIMESTAMP)	@Column(name = "survey_start_time", nullable = true)|survey_start_time datetime DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|surveyEndTime|NO|NA|DateTime|@DateTimeFormat(pattern = "dd-MM-yyyy HH:mm") @Temporal(TemporalType.TIMESTAMP) @Column(name = "survey_end_time", nullable = true)|survey_end_time datetime DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|taxStartDate|YES|NA|DateTime|@DateTimeFormat(pattern = "dd-MM-yyyy HH:mm") @Temporal(TemporalType.TIMESTAMP) @Column(name = "tax_start_date", length = 16, nullable = false)|tax_start_date datetime NOT NULL|NO|NO|NO|YES|NO|NO||
|taxEndDate|YES|NA|DateTime|@DateTimeFormat(pattern = "dd-MM-yyyy HH:mm") @Temporal(TemporalType.TIMESTAMP) @Column(name = "tax_end_date", length = 16, nullable = false)|tax_end_date datetime DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|frontPhoto|YES|NA|Attachment|@Column(name = "front_photo", length = 36, nullable = false)|front_photo varchar(36) NOT NULL|NO|NO|NO|YES|NO|NO||
|apartment|YES|0|Boolean|@Column(name = "apartment", nullable = true)|apartment boolean DEFAULT false|NO|NO|NO|YES|NO|NO||
|apartmentName|NO|NA|a-zA-Z0-9/:#, _\.\-,@,&, Space, minlen=3, maxlen=64|@Column(name = "apartment_name", length = 64, nullable = true)|apartment_name varchar(64) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|communityName|NO|NA|a-zA-Z0-9/:#, _\.\- Space, minlen=3, maxlen=64|@Column(name = "community_name", length = 64, nullable = true)|community_name varchar(64) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|vacantLandCategory|YES|NA|DropDown Values|@Enumerated(EnumType.STRING)  @Column(name = "vacant_land_category", length = 64, nullable = true)|vacant_land_category varchar(64) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|auctionCategory|YES|NA|DropDown Values|@Enumerated(EnumType.STRING)  @Column(name = "auc_category", length = 64, nullable = true)|auc_category varchar(64) DEFAULT NULL|NO|NO|NO|YES|NO|NO||
|updateComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "update_comment", nullable = true)|update_comment varchar(255) DEFAULT NULL|NO|YES|NO|YES|NO|NO||
|removeComment|YES|NA|a-zA-Z0-9,.#:/ _-, minlen=6, maxlen=255|@Column(name = "remove_comment", nullable = true)|remove_comment varchar(255) DEFAULT NULL|NO|NO|YES|YES|NO|NO||

#### ENUM CONSTANTS

##### Property Category Type

{{<mermaid align="left">}}
classDiagram
    class PropertyCategory{
      HOUSE
      ADVERTISEMENT
      KOLAGARAM
      TRADE_LICENSE
      AUCTION
      VACANT_LAND
      OTHER
    }
{{< /mermaid >}}

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

##### Vacant Land Category Type

{{<mermaid align="left">}}
classDiagram
    class VacantLandCatType{
     	PRIVATE
     	PANCHAYAT
     	EXEMPTION
     	CONCESSION
    }
{{< /mermaid >}}

##### Auction Category Type

{{<mermaid align="left">}}
classDiagram
    class AuctionCatType{
     	AGRICULTURAL_LAND
     	BANDELA_DODDI
     	CATTLE_SHED 
     	DAILY_MARKET 
     	FERRY 
     	FISHING_RIGHTS
     	FISHING_PONDS
    	GREEN_GRASS
		KABELA
		OLD_CONDEMNED_ITEMS
		SHOPPING_MALLS
		TREE 
		WEEKLY_MARKET
		OTHER 
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

##### Land Record Type

{{<mermaid align="left">}}
classDiagram
    class Name{
      NONE
	  REVENUE_REGISTRATION
	  PD_ACT
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|PENDING_PROPERTY_VIEW|View|
|PENDING_PROPERTY_VIEW|List|
|PENDING_PROPERTY_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Keys|1. gs_pending_property__name__category__org_panchayat_id (org_panchayat_id, category, name)|
||2. gs_pending_property__geoid (geoid)|

## Acceptance Criteria
|Permission|Description|
|----------|-----------|
|AC_ROLE_PENDING_PROPERTY_VIEW|Only user having the user role with this permission should view this functionality|
|AC_ROLE_PENDING_PROPERTY_VIEW|Only user having the user role with this permission should export the pending property in 2 formats Excel, PDF|

## User Experience
1. Listing page based on the standard UX Listing Template
1. View page based on the standard UX Listing Template
1. Export functionality based on the standard UX Listing Template 

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    ViewBtn[View]---ExportBtn[Export]---SearchBtn[Search]
{{< /mermaid >}}


### State Machine
{{<mermaid align="left">}}
flowchart TD
	PendingPropertyMenu((Pending Property Menu))
	ListPage{Pending Property List Page}
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->PendingPropertyMenu
    subgraph Menu
    PendingPropertyMenu
	end
	subgraph List
	PendingPropertyMenu-->ListPage
	ListPage--V-E-->ListPage
	end
	subgraph Error
	PendingPropertyMenu-->ErrorPage
	ErrorPage-->Stop
	end
	subgraph View
	ListPage--V-->ViewPage
	ViewPage--B-->ListPage
	ViewPage--B-->ViewPage
	end
	subgraph Download
    ListPage--E-->DownloadFile
    end
    %%For success Representation
    linkStyle 1 stroke:green,stroke-width:2px;
    linkStyle 5 stroke:green,stroke-width:2px;
    linkStyle 6 stroke:green,stroke-width:2px;
    linkStyle 8 stroke:green,stroke-width:2px;
    %%For failure representation
    linkStyle 2 stroke:red,stroke-width:2px;
    linkStyle 3 stroke:red,stroke-width:2px;
    linkStyle 7 stroke:red,stroke-width:2px;
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|V|View|
|E|Export|
|B|Back|
|F|Failure|
|V-E|View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram
1. Only a user with the PENDING_PROPERTY_VIEW permission will be allowed to perform the below operations.

{{<mermaid align="center">}}
sequenceDiagram
    participant PendingPropertyListPage as Browser
    participant Net as Browser Net Tools
	%%participant Cache as GS-Cloud-Cache
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        PendingPropertyListPage->>+Net: Check Internet, GET /app/ctx/PendingProperty/list ListPage
        Net--x-PendingPropertyListPage: F : Connection Error
        PendingPropertyListPage->>+cloud: S:  GET /app/ctx/PendingProperty/list ListPage
        cloud-->>-PendingPropertyListPage: RES: List Page
    end
    rect rgb(244,244,244)
        PendingPropertyListPage->>+Net: Check Internet, GET /app/PendingProperty/view ViewPage
        Net--x-PendingPropertyListPage: F : Connection Error
        PendingPropertyListPage->>+cloud: S : GET /app/PendingProperty/view ViewPage
        cloud-->>-PendingPropertyListPage: RES: pendingProperty View
    end
    rect rgb(244,244,244)
        PendingPropertyListPage->>+Net: Check Internet, GET /app/PendingProperty/exportPdf ExportPdf
        Net--x-PendingPropertyListPage: F : Connection Error
        PendingPropertyListPage->>+cloud: S : GET /app/PendingProperty/exportPdf ExportPdf
        cloud-->>-PendingPropertyListPage: RES: pendingProperty Pdf
    end
    rect rgb(244,244,244)
        PendingPropertyListPage->>+Net: Check Internet, GET /app/PendingProperty/exportListPdf ExportListPdf
        Net--x-PendingPropertyListPage: F : Connection Error
        PendingPropertyListPage->>+cloud: S : GET /app/PendingProperty/exportListPdf ExportListPdf
        cloud-->>-PendingPropertyListPage: RES: pendingProperty List Pdf
    end
    rect rgb(244,244,244)
        PendingPropertyListPage->>+Net: Check Internet, GET /app/PendingProperty/exportXlx ExportXlx
        Net--x-PendingPropertyListPage: F : Connection Error
        PendingPropertyListPage->>+cloud: S : GET /app/PendingProperty/exportXlx ExportXlx
        cloud-->>-PendingPropertyListPage: RES: pendingProperty Xlx
    end
    rect rgb(244,244,244)
        PendingPropertyListPage->>+Net: Check Internet, GET /app/PendingProperty/exportListXlx ExportListXlx
        Net--x-PendingPropertyListPage: F : Connection Error
        PendingPropertyListPage->>+cloud: S : GET /app/PendingProperty/exportListXlx ExportListXlx
        cloud-->>-PendingPropertyListPage: RES: pendingProperty List Xlx
    end
    
          
{{< /mermaid >}}

## Unit Test Cases
#### Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|-------------------|---|
|1.0| View |ut_p_v_GSTS_WEB_PENDING_PROPERTY_100  ut_n_v_GSTS_WEB_PENDING_PROPERTY_110 ut_n_v_GSTS_WEB_PENDING_PROPERTY_120 |**Positive Test Cases:** View Pending Property with Valid Id  with Authorised User **Negative Test Cases:** 1.View Pending Property without DB Connection 2.View Pending Property with Invalid ID with Authorised User||1|2|3|testPosAuthorisedUserViewPendingPropertyWithValidId,  testNegAuthorisedUserViewPendingPropertyWithoutDbConnection,  testNegAuthorisedUserViewPendingPropertywithInvalidId|
|1.0| Search |ut_p_s_GSTS_WEB_PENDING_PROPERTY_170  ut_n_s_GSTS_WEB_PENDING_PROPERTY_180 ut_n_s_GSTS_WEB_PENDING_PROPERTY_190 |**Positive Test Cases:** Search Pending Property with valid inputs **Negative Test Cases:** 1.Search Pending Property without db connection 2.Search Pending Property with invalid inputs| **name:** 1.valid characters2. length>=3 and length=<64  3.null **location:** **category**|1|2|3|testPosAuthorisedUserSearchPendingPropertyWithValidInputs, testNegAuthorisedUserSearchPendingPropertyWithoutDBconnection,  testNegAuthorisedUserSearchPendingPropertyWithInvalidInputs|
|1.0| List |ut_p_l_GSTS_WEB_PENDING_PROPERTY_140 ut_n_l_GSTS_WEB_PENDING_PROPERTY_150|**Positive Test Cases:** Get Pending Property List **Negative Test Cases:** Get Pending Property List without db connection|Validating with unique field|1|1|2|testPosAuthorisedUserPendingPropertyList,  testNegAuthorisedUserPendingPropertyListWithoutDBconnection|
|1.0| PDF |ut_p_ep_GSTS_WEB_PENDING_PROPERTY_360   ut_n_ep_GSTS_WEB_PENDING_PROPERTY_370   ut_n_ep_GSTS_WEB_PENDING_PROPERTY_380 |**Positive Test Cases:** Export Pdf with Authorised User **Negative Test Cases:**  1. Without DB Connection 2. Export Pdf with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportPendingPropertyPdfWithValidId,  testNegAuthorisedUserExportPendingPropertyPdfwithoutDbConnection,  testNegAuthorisedUserExportPendingPropertyPdfInValidId|
|1.0| List PDF |ut_p_elp_GSTS_WEB_PENDING_PROPERTY_390   ut_n_elp_GSTS_WEB_PENDING_PROPERTY_400   ut_n_elp_GSTS_WEB_PENDING_PROPERTY_410 |**Positive Test Cases:** Export List Pdf with Authorised User **Negative Test Cases:** 1.Without DB Connection 2. Export List Pdf with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportPendingPropertyListPdfWithValidId,  testNegAuthorisedUserExportPendingPropertyListPdfwithoutDbConnection,  testNegAuthorisedUserExportPendingPropertyListPdfInValidId|
|1.0| XLX |ut_p_ex_GSTS_WEB_PENDING_PROPERTY_420   ut_n_ex_GSTS_WEB_PENDING_PROPERTY_430   ut_n_ex_GSTS_WEB_PENDING_PROPERTY_440 |**Positive Test Cases:** Export Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export Xlx with Invalid Id |Id |1|2|3|testPosAuthorisedUserExportPendingPropertyXlxValidId,  testNegAuthorisedUserExportPendingPropertyXlxwithoutDbConnection,  testNegAuthorisedUserExportPendingPropertyXlxInValidId|
|1.0| List XLX |ut_p_elx_GSTS_WEB_PENDING_PROPERTY_450   ut_n_elx_GSTS_WEB_PENDING_PROPERTY_460   ut_n_elx_GSTS_WEB_PENDING_PROPERTY_470 |**Positive Test Cases:** Export List Xlx with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Export List Xlx with Invalid Id|Id |1|2|3|testPosAuthorisedUserExportPendingPropertyListXlxValidId,  testNegAuthorisedUserExportPendingPropertyListXlxWithoutDbConnection,  testNegAuthorisedUserExportPendingPropertyListXlxInValidId|
|1.0| Download|ut_p_d_GSTS_WEB_PENDING_PROPERTY_480   ut_n_d_GSTS_WEB_PENDING_PROPERTY_490   ut_n_d_GSTS_WEB_PENDING_PROPERTY_500 ut_d_elx_GSTS_WEB_PENDING_PROPERTY_510 |**Positive Test Cases:** Download Pending Property attachment with Authorised User **Negative Test Cases:** 1. Without DB Connection 2.Pending Property attachment with Invalid Id 3.Download Pending Property Attachment with valid Id and Invalid Document type|Id |1|3|4|testPosAuthorisedUserDownloadPendingPropertyAttachmentValidId,  testPosAuthorisedUserDownloadPendingPropertyAttachmentwithoutDbConnection,  testNegAuthorisedUserDownloadPendingPropertyAttachmentInValidId, testNegAuthorisedUserDownloadPendingPropertyAttachmentWithValidIdAndInvalidDocType|


#### Un Authorised User
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Positive Test Cases Count|Negative Test Cases Count|Total Test Cases Count|Method Names|
|---------------|--------|-----------|--------|----------------------|--------------------------|-------------------------|------------------|-----|
|1.0| View |ut_n_v_GSTS_WEB_PENDING_PROPERTY_130|Unauthorised User does not have permission to view|1.Valid Id|0|1|1|testNegUnAuthorisedUserViewPendingProperty|
|1.0| Search |ut_n_s_GSTS_WEB_PENDING_PROPERTY_200|Unauthorised User does not have permission to search|**name:** 1.valid characters 2. length>=3 and length=<64  3.null **location:** **category**|0|1|1|testNegUnAuthorisedUserSearchPendingProperty|
|1.0| List |ut_n_l_GSTS_WEB_PENDING_PROPERTY_160|Unauthorised User does not have permission to list|Validating with the unique field|0|1|1|testNegUnAuthorisedUserPendingPropertyList|
|1.0| PDF |ut_n_ep_GSTS_WEB_PENDING_PROPERTY_520 |Export Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPendingPropertyPdfWithValidId|
|1.0| List PDF |ut_n_elp_GSTS_WEB_PENDING_PROPERTY_530 |Export List Pdf with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPendingPropertyListPdfWithValidId|
|1.0| XLX |ut_n_ex_GSTS_WEB_PENDING_PROPERTY_540 |Export XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPendingPropertyXlxWithValidId|
|1.0| List XLX |ut_n_elx_GSTS_WEB_PENDING_PROPERTY_550 |Export List XLX with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserExportPendingPropertyListXlxWithValidId|
|1.0| Download |ut_n_d_GSTS_WEB_PENDING_PROPERTY_560 |Download Pending Property attachment with UnAuthorised User|1.Valid Id |0|1|1|testNegUnAuthorisedUserDownloadPendingPropertyAttachmentWithValidId|


#### Scope Level Testing
|Product Version|Category|UnitTest Id|Description|Attributes Test Cases | Expected Test Case Result|Total Test Cases Count|Method Names|
|---------------|--------|-----------|-----------|----------------------|--------------------------|----------------------|------------|
|1.0|View|ut_n_v_GSTS_WEB_PENDING_PROPERTY_570|One Panchayat user trying to access different Panchayat Pending Property which does not belongs to his context| N/A |Will not be accessed|1|testNegOnePanchayatUserAccessingDifferentPanchayatPendingProperty|


## Security compliance check
1. Only user having the user role with permission **ROLE_PENDING_PROPERTY_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Pending Property should be provided in the User Manual.

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




 
