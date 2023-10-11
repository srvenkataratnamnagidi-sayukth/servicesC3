---
title: Panchayat Assests
tags : ["Composing"]
---

## Introduction
Panchayat Assets in GIS Maps are one of the features of our software product. Panchayat assets in GIS Maps show the assets of a panchayat in the map. Users should have permission to access this feature.

## Business Assumptions
Creating or updating the panchayat assets is not possible in GIS Maps. Only the user with permission will have access to search or view the panchayat assets on the map.

## Requirements
### Functional Requirements
1. Only panchayat level users should search or view the panchayat assets on the map.
1. The assets which were already created in panchayat assets can only be visible in this panchayat assets of GIS Maps.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access assets.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Panchayat assets of GIS Maps are required to show the assets of a panchayat in the map. 

### Design 
1. We can search and view the assets of a panchayat in map.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Panchayat Assets|[gs0007-panchayatAssets]({{< ref "gs0007-panchayatAssets" >}})||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_asset_map_view|To view the asset|
|uc_asset_map_search|To search the asset|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|Asset Type|YES|NA|DropDown Values|@Enumerated (EnumType.STRING) @Column(name = "asset_type", length = 256, nullable = false)|asset_type varchar(256) not null|NO|NO|NO|NO|YES|YES||
|Asset Tag|YES|NA|Allowed a-z, A-Z, 0-9, space, _ , - and length 3 to 64|@Column(name = "asset_tag", length = 64, nullable = false)|asset_tag varchar(64) not null|NO|NO|NO|NO|YES|YES||
|Asset Value|YES|NA|Allowed 0-9 only|@Column(name = "asset_value", nullable = false)|asset_value float(9,2) not null|NO|NO|NO|NO|YES|NO||

#### ENUM CONSTANTS

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

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|ASSET_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|||

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|ASSET_VIEW|To view the panchayat assets|

## User Experience
1. Listing page based on the standard UX Listing Template

### List Page Buttons
{{<mermaid align="left">}}
graph LR 
    SearchBtn[Search]
{{< /mermaid >}}


### State Machine

{{<mermaid align="left">}}
flowchart TD
	PanchayatAssetMenu((Panchayat Asset Menu))
    ListPage((List Page))
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->PanchayatAssetMenu
	PanchayatAssetMenu-->ErrorPage
	PanchayatAssetMenu-->ListPage
	ErrorPage-->Stop
    %%For success Representation
    linkStyle 2 stroke:green,stroke-width:2px;
    %%For failure representation
    linkStyle 1 stroke:red,stroke-width:2px;
	
{{< /mermaid >}}

|Symbol|Action|
|:-----|:----|
|Green Arrow|Success|
|Red Arrow|Failure|


### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant AssetGeoMapListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        AssetGeoMapListPage->>+Net: Check Internet, GET /app/ctx/OrganizationAssetMapDo/list
        Net--x-AssetGeoMapListPage: F : Connection Error
        AssetGeoMapListPage->>+cloud: S : GET /app/ctx/OrganizationAssetMapDo/list
        cloud-->>-AssetGeoMapListPage: RES: List Page
    end
          
{{< /mermaid >}}

## Security compliance check
1. Only user having the user role with permission **ROLE_ASSET_MAP_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Panchayat Asset Map should be provided in the User Manual.

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




 
