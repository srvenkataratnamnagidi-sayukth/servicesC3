---
title: Taxable Properties
tags : ["Composing"]
---

## Introduction
Taxable properties in GIS Maps are one of the features of our software product. Taxable properties in GIS Maps show every taxable property of a panchayat in the map. Taxable properties of a panchayat include houses, kolagarams, auctions, advertisements, trade licenses, vacant lands, door locked properties. Users should have permission to access this feature.

## Business Assumptions
Creating or updating the taxable properties is not possible in GIS Maps. Only the user with permission will have access to search or view the taxable properties on the map.

## Requirements
### Functional Requirements
1. Only panchayat level users should search or view the taxable properties on the map.
1. The properties which were already created in taxable properties can only be visible in this taxable properties of GIS Maps.

### Non-functional Requirements
Based on **Personas of Users**, we will give permission to access taxable properties.   
Reference:[Personas of users](http://localhost:1313/#personas-of-users)

### Problem Statement
Taxable properties of GIS Maps are required to show the taxable properties of a panchayat in the map. 

### Design 
1. We can search and view the taxable properties of a panchayat in map.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Taxable Properties|[gs0006-taxableproperties]({{< ref "gs0006-taxableproperties" >}})||

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_trade_property_view|To view the taxable properties in GIS maps|

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|aid|YES|NA|Allowed 0-9 and length should be 12|@Column(name = "aid", length = 12, nullable = false)|aid varchar(12) not null |NO|NO|NO|NO|YES|YES||
|mobile|YES|NA|Allowed 0-9 and length should be 10|@Column(name = "mobile", length = 13, nullable = false)|mobile varchar(13) not null |NO|NO|NO|NO|YES|YES||
|fname|YES|NA|Allowed a-z = A-Z = 0-9 = _ = - and length 3 to 64|@Column(name = "fname", length = 64, nullable = false)|fname varchar(64) not null|NO|NO|NO|NO|YES|YES||
|surname|YES|NA|Allowed a-z = A-Z = 0-9 = _ = - and length 3 to 32|@Column(name = "surname", length = 32, nullable = false)|surname varchar(32) not null|NO|NO|NO|NO|YES|YES||
|geoid|YES|NA|Allowed a-z = A-Z = 0-9 = . = , and length 3 to 64|@Column(name = "geoid", length = 64, nullable = false, unique = true)|geoid varchar(64) not null|NO|NO|NO|NO|YES|YES||
|name|YES|NA|Allowed a-z = A-Z = 0-9 = _ = - and length 3 to 64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) not null|NO|NO|NO|NO|YES|YES||

#### ENUM CONSTANTS

##### Asset Type

{{<mermaid align="left">}}
classDiagram
    class Name{
      HOUSE
      ADVERTISEMENT
      KOLAGARAM
      TRADE_LICENSE
      AUCTION
      VACANT_LAND
      OTHER
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|
|TRADE_PROPERTY_VIEW|List|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Keys|gs_property__geoid (geoid)|
|Foreign Keys|1. fk__gs_property__caid FOREIGN KEY (caid) REFERENCES gs_citizen (aid)|


## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|TRADE_PROPERTY_VIEW|To view the taxable properties|

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
	TaxablePropertiesMenu((Taxable Properties Menu))
    ListPage((List Page))
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->TaxablePropertiesMenu
	TaxablePropertiesMenu-->ErrorPage
	TaxablePropertiesMenu-->ListPage
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
    participant TaxablePropertiesListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        TaxablePropertiesListPage->>+Net: Check Internet, GET /app/ctx/OrganizationPropertyMapDo/list
        Net--x-TaxablePropertiesListPage: F : Connection Error
        TaxablePropertiesListPage->>+cloud: S : GET /app/ctx/OrganizationPropertyMapDo/list
        cloud-->>-TaxablePropertiesListPage: RES: List Page
    end
          
{{< /mermaid >}}

## Security compliance check
1. Only user having the user role with permission **ROLE_TRADE_PROPERTY_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Information about the Taxable Property Map should be provided in the User Manual.

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

