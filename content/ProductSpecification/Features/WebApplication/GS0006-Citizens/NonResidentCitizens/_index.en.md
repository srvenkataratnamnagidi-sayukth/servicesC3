---
title: Non-Resident Citizens
tags : ["Composing"]
---

## Introduction
Non Resident Citizens are one of the features of our software product. A Non-resident citizen is an individual who mainly resides in one region but has interests in another region. All these Non-resident Citizens are stored in this feature. Users should have permission to access this feature.

## Business Assumptions
Non-Resident Citizen should be created and uploaded from mobile and no updates to the citizens at the run time. 

## Requirements
### Functional Requirements
Non-Resident Citizens can be accessible at all levels of the organization.

### Non-functional Requirements
The system can support any number of citizens but this design will limit 3,00,00,000 citizens for this system. Beyond the 3,00,00,000 citizens may experience performance issues. 


### Problem Statement
The identity of a Non-Resident Citizen in a state should be captured.

### Design 
1. We can View, and export the non-resident citizens.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Dashboard|[gs0001-dashbaord]({{< ref "gs0001-dashbaord" >}})|Parent page|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|uc_nr_citizen_view|To view the citizen|
|uc_nr_citizen_search|To search the citizen|
|uc_nr_citizen_export|To export the citizen in 2 formats Excel, PDF|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|Create|Update|Remove|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|------|----|----|------|-------|
|Aadhaar Number|YES|NA|Allowed 0-9 and length should be 12|@Column(name = "aid", length = 12, nullable = false)|aid varchar(12) not null |NO|NO|NO|YES|YES|YES||
|Name|YES|NA|Allowed a-z = A-Z = 0-9 = _ = - and length 3 to 64|@Column(name = "name", length = 64, nullable = false)|name varchar(64) not null|NO|NO|NO|YES|YES|YES||
|Surname|YES|NA|Allowed a-z = A-Z = 0-9 = _ = - and length 3 to 32|@Column(name = "surname", length = 32, nullable = false)|surname varchar(32) not null|NO|NO|NO|YES|YES|YES||
|Father / Spouse Name|YES|NA|Allowed a-z = A-Z = 0-9 = _ = - and length 3 to 64|@Column(name = "fsname", length = 64, nullable = false)|fsname varchar(64) not null|NO|NO|NO|YES|NO|NO||
|Mobile Number|YES|NA|Allowed 0-9 and length should be 10|@Column(name = "mobile", length = 13, nullable = false)|mobile varchar(13) not null |NO|NO|NO|YES|YES|YES||
|Gender|YES|NA|Drop Down List|@Column(name = "gender", length = 8, nullable = false)|gender varchar(8) not null |NO|NO|NO|YES|NO|NO||
|Date Of Birth|YES|NA|Date dd-MM-YYYY|@Column(name = "dob", nullable = false)|dob datetime not null|NO|NO|NO|YES|NO|NO||
|Marital Status|YES|NA|Drop Down List|@Column(name = "married", length = 16, nullable = false)|married varchar(16) not null |NO|NO|NO|YES|NO|NO||
|Email|YES|NA|Allowed a-z = A-Z = 0-9 = @ and length 3 to 64|@Column(name = "email", length = 64, nullable = true)|email varchar(64) default null|NO|NO|NO|YES|NO|NO||

#### ENUM CONSTANTS

##### Gender

{{<mermaid align="left">}}
classDiagram
    class Gender{
      MALE
      FEMALE
      OTHER
    }
{{< /mermaid >}}

##### Marital Status

{{<mermaid align="left">}}
classDiagram
    class MaritalStatus{
      SINGLE
      MARRIED 
      DIVORCED 
      WIDOWED
      SEPERATED
      SPOUSE_DEAD
      LIVING_RELATION
    }
{{< /mermaid >}}


#### Feature Permission
|Permission code|Action|
|---------------|-------|
|CITIZEN_VIEW|View|
|CITIZEN_VIEW|List|
|CITIZEN_VIEW|Export|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Keys|uk__gs_citizen__aid (aid)|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|
|ac_nr_citizen_view|Only user having the permission to view, should view this functionality|
|ac_nr_citizen_view|Only user having the permission to export, should export the user role in 2 formats Excel, PDF|

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
	CitizensMenu((Non Resident Citizens Menu))
	ListPage{Non Resident Citizens List Page}
    ViewPage((View Page))
    DownloadFile>Save File On Disk]
    ErrorPage((Error Page))
    Stop((Stop))
	Start((Start))
	Start-->CitizensMenu
    subgraph Menu
    CitizensMenu
	end
	subgraph List
	CitizensMenu-->ListPage
	ListPage--V-E-->ListPage
	end
	subgraph Error
	CitizensMenu-->ErrorPage
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
|S|Submit|
|B|Back|
|SB|Submit or Back|
|VE|View or Export|
|Green Arrow|Success|
|Red Arrow|Failure|


## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
||||
||||

### Sequence Diagram

{{<mermaid align="center">}}
sequenceDiagram
    participant CitizensListPage as Browser
    participant Net as Browser Net Tools
    participant cloud as GS-Cloud
    autonumber
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet, GET /app/ctx/Citizen/list/nr ListPage
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S:  GET /app/ctx/Citizen/list/nr ListPage
        cloud-->>-CitizensListPage: RES:List Page
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/view ViewPage
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : GET /app/Citizen/view ViewPage
        cloud-->>-CitizensListPage: RES: citizen View
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/exportPdf ExportPdf
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : GET /app/Citizen/exportPdf ExportPdf
        cloud-->>-CitizensListPage: RES: citizen Pdf
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/exportListPdf ExportListPdf
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : GET /app/Citizen/exportListPdf ExportListPdf
        cloud-->>-CitizensListPage: RES: citizen List Pdf
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/exportXlx ExportXlx
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : GET /app/Citizen/exportXlx ExportXlx
        cloud-->>-CitizensListPage: RES: citizen Xlx
    end
    rect rgb(244,244,244)
        CitizensListPage->>+Net: Check Internet: GET /app/Citizen/exportListXlx ExportListXlx
        Net--x-CitizensListPage: F : Connection Error
        CitizensListPage->>+cloud: S : GET /app/Citizen/exportListXlx ExportListXlx
        cloud-->>-CitizensListPage: RES: citizen List Xlx
    end
    
          
{{< /mermaid >}}


## Security compliance check
1. Only user having the user role with permission **ROLE_CITIZEN_VIEW** should view this functionality 

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the NON RESIDENT CITIZENS in the User Manual. Its scope is limited to Developer Technical Documentation

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




 
